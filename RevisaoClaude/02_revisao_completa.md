# 2. Revisão completa do trabalho (além do e-mail)

Este arquivo traz o que encontrei relendo o trabalho inteiro (`trabalho.tex`, commit `02ed0b2`) e conferindo o texto contra o código e o notebook do repositório DiagnosisXAI (versão do GitHub, commit `22cbe5a`, de 13/10).

**Nada aqui foi pedido pela professora.** Os itens do e-mail estão no `01_pendencias_email.md`, e este arquivo não os repete. Cada sugestão traz uma prioridade:

- 🔴 **Alta:** erro de conceito ou contradição interna que a banca pode apontar. Vale corrigir antes de 14/11.
- 🟡 **Média:** imprecisão técnica ou incoerência menor. Corrija se der tempo.
- ⚪ **Baixa:** estilo e padronização.

Os blocos Procure / Substitua por seguem a mesma regra de correção mínima do outro arquivo e **também foram aplicados e compilados** numa cópia, depois dos blocos do `01`. Aplique o `01` primeiro.

---

## O que foi conferido e está certo

Para você não gastar tempo com isto:

- **Todas as tabelas batem com as saídas do notebook:** Tabela 1 (células 23–32), Tabela 2 (célula 35), Tabelas 3 e 4 (célula 37), Tabela 5 (célula 39), Tabela 6 (célula 40), Tabela 7 (célula 45), além dos Briers recalibrados da p. 81 (célula 59).
- Árvore de Decisão no `wisconsin.pkl`: critério entropia, **profundidade 7 e 18 folhas**, como diz o texto.
- **231 testes** coletados pelo `pytest` (o texto diz 231).
- Python **3.12.3** (metadados do notebook), como diz a Seção 4.3.
- Os limiares e as faixas do `limiares.json` são os da Tabela 7.
- A regra de decisão do app (`decision.py`) é a descrita na Seção 4.8.3.
- A projeção de paciente novo no UMAP (média ponderada dos vizinhos de treino) é a descrita na p. 93.
- A distância de Mahalanobis com Ledoit-Wolf e o corte no percentil 99 conferem com `ood_detector.py`.
- O agrupamento em 8 fatores e as 2⁸ = 256 coalizões exatas conferem com `fatores.py`.

---

## A. Conceitos e precisão técnica

### A1 🔴 Calibração do SVM: a explicação do texto não corresponde ao que acontece no código

**Onde:** p. 81 (linhas 1998–2004) e conclusão (linha 2467: "Como a aplicação direta de Platt sobre o SVM piorava sua calibração, o ajuste passou a ser feito sobre a função de decisão desse modelo").

**O problema:** o texto diz que o Platt piorou o SVM (Brier 0,0156 → 0,0213, Tabela 6) e que a solução foi calibrar "sobre a função de decisão, em vez de sobre probabilidades que já resultam de um ajuste de Platt interno". Mas o `CalibratedClassifierCV` **sempre usa a função de decisão** quando ela existe, com ou sem `probability=True`. A diferença real entre a Tabela 6 e o software é outra:

- **Tabela 6 (célula 40):** `CalibratedClassifierCV(..., cv=5)` com o padrão `ensemble=True`, que treina **cinco pares** de SVM e calibrador, cada um em 80% do treino, e faz a média das cinco probabilidades.
- **Software (célula 59):** `ensemble=False`, que treina **um único SVM em todo o treino** e ajusta o calibrador nas previsões *out-of-fold*.

Testei as quatro combinações com o `wisconsin.pkl` do repositório:

| `probability` | `ensemble` | Brier no teste |
|---|---|---|
| False | True | 0,0213 |
| True | True | 0,0213 |
| False | False | 0,0156 |
| True | False | 0,0156 |

O que muda o resultado é o `ensemble`, não o `probability`. Corrigir isso é importante porque é exatamente o tipo de pergunta que um membro da banca com experiência em scikit-learn faz.

**Procure:**
```latex
modelos de probabilidade informativa, com um único estimador ajustado sobre
todo o treino e o calibrador sobre ele; no SVM, o calibrador atua diretamente
sobre a função de decisão, em vez de sobre probabilidades que já resultam de um
ajuste de Platt interno. Nessa configuração, o escore de Brier no teste passa
de 0,0292 para 0,0243 no KNN, de 0,0202 para 0,0156 na Regressão Logística e de
0,0269 para 0,0232 no Random Forest, e permanece em 0,0156 no SVM.
```

**Substitua por:**
```latex
modelos de probabilidade informativa, com um único estimador ajustado sobre
todo o treino e o calibrador ajustado sobre as previsões \textit{out-of-fold}
de 5 dobras desse mesmo treino; no SVM, o calibrador atua sobre a função de
decisão. Nessa configuração, o escore de Brier no teste passa
de 0,0292 para 0,0243 no KNN, de 0,0202 para 0,0156 na Regressão Logística e de
0,0269 para 0,0232 no Random Forest, e permanece em 0,0156 no SVM. A diferença
em relação à Tabela~\ref{tab:recalibracao}, em que o escalonamento de Platt
elevou o Brier do SVM para 0,0213, decorre da forma de ajuste: naquela
comparação, o scikit-learn treina cinco pares de modelo e calibrador, um por
dobra, e faz a média de suas probabilidades; na versão do software, um único
SVM, ajustado sobre todo o treino, é calibrado uma única vez.
```

E na conclusão (mesmo tamanho, para não estourar as 3 páginas):

**Procure:**
```latex
Como a aplicação direta de Platt sobre o SVM piorava sua calibração, o ajuste passou a ser feito sobre a função de decisão desse modelo.
```

**Substitua por:**
```latex
Como a calibração padrão, que faz a média de cinco SVMs calibrados, piorava o Brier, o software passou a calibrar um único SVM sobre previsões \textit{out-of-fold}.
```

> No notebook, o comentário da célula 59 ("o calibrador usa decision_function; evita Platt duplo") e o `set_params(probability=False)` podem ficar: não fazem mal e deixam o treino mais rápido. Só a justificativa no texto é que estava errada.

### A2 🔴 "Especificidade" é métrica central, mas não é definida na fundamentação

**Onde:** a Subseção 2.3.3 define acurácia, sensibilidade, **precisão**, F1, ROC e PR. A metodologia usa **especificidade** nas Tabelas 1, 2 e 7, na auditoria e, principalmente, no critério do limiar (piso de 92%), e quase não usa precisão. A banca pode pedir a fórmula.

**Procure:**
```latex
\begin{equation}
    \label{eq:sensibilidade}
    Sensibilidade = \frac{VP}{VP + FN}
\end{equation}
```

**Substitua por:**
```latex
\begin{equation}
    \label{eq:sensibilidade}
    Sensibilidade = \frac{VP}{VP + FN}
\end{equation}

De forma complementar, a especificidade mede a capacidade do algoritmo de reconhecer corretamente os pacientes que não possuem a doença, isto é, a proporção de tumores benignos classificados como benignos, conforme a Equação \ref{eq:especificidade}. Em um sistema de apoio ao diagnóstico, ela controla a quantidade de alarmes falsos e é o critério usado na escolha do limiar de operação deste trabalho (\citeauthoronline{Faceli2011}, \citeyear{Faceli2011}).

\begin{equation}
    \label{eq:especificidade}
    Especificidade = \frac{VN}{VN + FP}
\end{equation}
```

> Confira em Faceli et al. a página em que a especificidade é definida. Se não estiver lá, troque a citação por Davis e Goadrich (2006), que usam a taxa de falsos positivos (1 − especificidade).

### A3 🔴 Código 1 (Cap. 2) mostra hiperparâmetros do UMAP que o projeto não usa

**Onde:** o Código 1 (p. 41) usa `n_neighbors=65, min_dist=0.0`, e o texto da p. 40 diz que "a adoção de uma distância mínima nula maximiza a coesão biológica". O notebook (célula 48) e o mapa populacional do app usam **`n_neighbors=15, min_dist=0.1`** (os padrões da biblioteca). A metodologia não informa em lugar nenhum os valores usados. A pergunta "quais parâmetros do UMAP você usou?" é provável, e o próprio código do texto contradiz a resposta.

**Procure:**
```latex
O Código \ref{cod:umap-python} ilustra a instanciação do algoritmo com a definição de seus respectivos hiperparâmetros para a posterior redução de dimensionalidade de um conjunto de dados clínicos.
```

**Substitua por:**
```latex
O Código \ref{cod:umap-python} ilustra a instanciação do algoritmo com a definição de seus respectivos hiperparâmetros para a posterior redução de dimensionalidade de um conjunto de dados clínicos. Os valores do exemplo são ilustrativos; o mapa populacional deste trabalho utiliza n\_neighbors = 15 e min\_dist = 0,1, valores padrão da biblioteca, conforme a Subseção~\ref{subsec:relatorios-xai}.
```

**Procure:**
```latex
treino, discutido na Seção~\ref{sec:umap}. Como o UMAP não é reajustado a cada
```

**Substitua por:**
```latex
treino com n\_neighbors = 15, min\_dist = 0,1 e semente fixa, discutido na
Seção~\ref{sec:umap}. Como o UMAP não é reajustado a cada
```

### A4 🟡 Random Forest: `max_features='sqrt'` dá 5 atributos, não "aproximadamente seis"

**Onde:** p. 70 (linha 1530). O scikit-learn usa a parte inteira de √30 ≈ 5,48, ou seja, 5. Conferi no modelo salvo: `estimators_[0].max_features_ == 5`.

**Procure:**
```latex
cada divisão a um subconjunto aleatório de aproximadamente seis atributos,
```

**Substitua por:**
```latex
cada divisão a um subconjunto aleatório de cinco atributos, a parte inteira de $\sqrt{30}$,
```

### A5 🟡 SVM: `probability=True` não é "obrigatório" para as curvas ROC e PR

**Onde:** p. 72 (linhas 1600–1603). As curvas podem ser feitas com a função de decisão, e o próprio notebook faz isso na validação cruzada (comentário da célula 35: "os scorers ROC-AUC/PR-AUC usam a decision_function").

**Procure:**
```latex
probability = True é um requisito técnico obrigatório para a geração das curvas
ROC e Precisão-Revocação pelas funções auxiliares, pois habilita o método
predict\_proba que estima a probabilidade de cada classe para cada amostra.
```

**Substitua por:**
```latex
probability = True habilita o método predict\_proba, que estima a probabilidade
de cada classe por um ajuste de Platt interno e é usado pelas funções auxiliares
para traçar as curvas ROC e Precisão-Revocação; as curvas também poderiam ser
obtidas diretamente da função de decisão, como na validação cruzada da
Seção~\ref{sec:rigor-estatistico}.
```

### A6 🟡 Regressão Logística: sigmoide, otimização e equação

**Onde:** pp. 31–32 (linhas 380–391).

- A sigmoide nunca chega a 0 nem a 1: o intervalo é **aberto**, (0, 1), e não [0, 1]. "A fração converge para uma escala de probabilidade" é impreciso.
- "Otimizado iterativamente por gradiente descendente": o projeto usa o *solver* `liblinear`, que não é gradiente descendente. Além disso, com penalidade L2 o problema é uma máxima verossimilhança **penalizada**.
- A Equação 2.5 tem um único atributo (β₀ + β₁x₁), mas o modelo usa 30. A lista de símbolos chama x₁ de "vetor". Isso não é erro grave, mas a banca pode perguntar como fica com 30 variáveis. A resposta é β₀ + Σⱼ βⱼxⱼ.

**Procure:**
```latex
para o intervalo $[0, 1]$ ao calcular
```

**Substitua por:**
```latex
para o intervalo aberto $(0, 1)$ ao calcular
```

**Procure:**
```latex
a fração resultante converge para uma escala de probabilidade válida,
```

**Substitua por:**
```latex
a fração resultante fica sempre entre 0 e 1 e pode ser lida como probabilidade,
```

**Procure:**
```latex
um processo otimizado iterativamente por gradiente descendente que busca
```

**Substitua por:**
```latex
um processo resolvido iterativamente por métodos de otimização numérica, como o gradiente descendente, que busca
```

### A7 🟡 SVM: o *kernel* não é a função de mapeamento

**Onde:** p. 32 (linha 396). O mapeamento é φ. O *kernel* calcula o produto interno nesse espaço **sem construí-lo**, e isso é o "truque". No RBF, o espaço tem dimensão infinita, então o mapeamento nem poderia ser feito explicitamente.

**Procure:**
```latex
o \textit{kernel} atua como uma função de mapeamento que eleva os dados originais de um espaço de baixa dimensão para um espaço de dimensão superior.
```

**Substitua por:**
```latex
o \textit{kernel} permite operar como se os dados originais fossem elevados de um espaço de baixa dimensão para um espaço de dimensão superior, calculando os produtos internos nesse novo espaço sem construí-lo explicitamente.
```

### A8 🟡 Random Forest: amostra *out-of-bag*

**Onde:** p. 35 (linha 477). Cerca de 37% (≈ 1/e) das amostras ficam fora de cada *bootstrap*, por acaso e não "estrategicamente". A amostra OOB serve para estimar o erro de generalização, não para "validações cruzadas".

**Procure:**
```latex
Durante as amostragens no conjunto original, um terço dos dados é estrategicamente blindado sob a nomenclatura de amostra \textit{out-of-bag} (oob), servindo primariamente para validações cruzadas \cite{ibm_random_forest_2026}.
```

**Substitua por:**
```latex
Em cada amostragem \textit{bootstrap}, cerca de um terço dos dados (aproximadamente 37\%) fica fora do treino da árvore; essa amostra \textit{out-of-bag} (OOB) permite estimar o erro de generalização sem um conjunto de validação separado \cite{ibm_random_forest_2026}.
```

> Ainda sobre o Random Forest: a fundamentação (linha 475) fala em "votação majoritária", mas no scikit-learn a floresta faz a **média das probabilidades** das árvores (voto suave). Não precisa mudar a fundamentação, que descreve o algoritmo clássico de Breiman, mas saiba responder (pergunta 23 do arquivo de perguntas).

### A9 🟡 "Padrão ouro" para a base WDBC

**Onde:** p. 44 (linha 603). Em medicina, "padrão ouro" é o exame de referência para o diagnóstico (aqui, a histopatologia). Uma base de dados é uma **referência** (*benchmark*). Um avaliador da área da saúde pode estranhar.

**Procure:**
```latex
que é utilizada como padrão ouro na literatura acadêmica até os dias atuais.
```

**Substitua por:**
```latex
que é utilizada como referência (\textit{benchmark}) na literatura acadêmica até os dias atuais.
```

### A10 🟡 Abdullah et al. não "corroboram a utilidade do UMAP"

**Onde:** p. 46 (linha 637). Abdullah et al. fazem **seleção de atributos por correlação**. O UMAP deste trabalho é **visualização** e não reduz os atributos que entram nos classificadores. A ligação feita no texto não se sustenta. A ligação que se sustenta é com a colinearidade, que você trata de verdade.

**Procure:**
```latex
Este estudo corrobora a utilidade do UMAP no presente projeto. Ao discutir a redução de dimensionalidade, o trabalho de Abdullah et al. fornece o embasamento sobre como a simplificação de dados complexos pode levar a diagnósticos mais precisos e interpretáveis.
```

**Substitua por:**
```latex
Este estudo dialoga com o presente projeto na questão dos atributos redundantes. Ao mostrar que a remoção de variáveis correlacionadas não prejudica o desempenho, o trabalho de Abdullah, Abdulazeez e Sallow ampara o tratamento da colinearidade adotado aqui, como a regularização da Regressão Logística e o agrupamento de raio, perímetro e área em um único fator nas explicações.
```

### A11 🟡 Calibração: tabela sem conjunto identificado e justificativa da Tabela 6

**Onde:** pp. 80–81.

- A Tabela 5 é calculada no **conjunto de teste** (célula 39), mas o título não diz isso. O ECE usa 10 faixas sobre 143 pacientes, o que é pouco por faixa (pergunta provável).
- A Tabela 6 diz que compara "os dois modelos de melhor desempenho discriminativo", mas no teste o melhor ROC-AUC é o da Regressão Logística (0,998) e, na validação cruzada, SVM e RL empatam. O critério real (comentário da célula 40) é que SVM e RF "são tipicamente os mais mal calibrados".

**Procure:**
```latex
\caption{MÉTRICAS DE CALIBRAÇÃO DAS PROBABILIDADES (MENOR É MELHOR)}
```

**Substitua por:**
```latex
\caption{MÉTRICAS DE CALIBRAÇÃO DAS PROBABILIDADES NO CONJUNTO DE TESTE (MENOR É MELHOR)}
```

**Procure:**
```latex
Tabela~\ref{tab:recalibracao} apresenta o efeito de cada método sobre os dois
modelos de melhor desempenho discriminativo.
```

**Substitua por:**
```latex
Tabela~\ref{tab:recalibracao} apresenta o efeito de cada método sobre o SVM e
o Random Forest, cujos escores de origem são, respectivamente, uma distância à
margem e uma fração de votos entre árvores.
```

**Procure:**
```latex
sobre as quais a noção de calibração não se aplica.
```

**Substitua por:**
```latex
sobre as quais a análise de calibração é pouco informativa.
```

### A12 🟡 Curva risco-cobertura: "maior risco previsto" é ambíguo

**Onde:** p. 82 (linhas 2031–2032). O leitor entende "maior risco de câncer", mas a curva adia primeiro os casos com maior chance de a **decisão** estar errada (célula 45: `risco = 1 − p` se decidido maligno, `p` se benigno).

**Procure:**
```latex
adiando primeiro os casos de maior
risco previsto,
```

**Substitua por:**
```latex
adiando primeiro os casos cuja
decisão tem maior probabilidade estimada de estar errada,
```

### A12b ⚪ "O UMAP não tem inversa"

**Onde:** p. 91 (linhas 2298–2299). O umap-learn tem `transform()`, para novos pontos, e `inverse_transform()`, uma inversa **aproximada** (conferido na versão 0.5.12). O argumento do texto continua válido; só falta a palavra "exata".

**Procure:**
```latex
tem inversa: não há como avaliar
```

**Substitua por:**
```latex
tem inversa exata (a biblioteca oferece apenas uma aproximação): não há como avaliar
```

### A13 🟡 Quadros 2 e 3: duas células incoerentes com o texto

- **Quadro 3, "Este Projeto", coluna "Melhor algoritmo": "Comitê de voto suave".** A Seção 4.7.2 conclui que nenhum dos quatro modelos é superior, e o comitê nem entra na validação cruzada nem nos testes. A célula contradiz o principal resultado do trabalho.
- **Quadro 2, Cruz e Wishart, coluna "Câncer de mama": "Não".** O texto da p. 45 diz que, na revisão deles, "o câncer de mama [era] o mais estudado".

**Procure:**
```latex
\textbf{Comitê de voto suave}
```

**Substitua por:**
```latex
\textbf{Sem diferença entre RL, SVM, RF e KNN}
```

**Procure:**
```latex
Cruz \& Wishart (2006) & Sim & Sim & Sim & Não & Não & Não \\ \hline
```

**Substitua por:**
```latex
Cruz \& Wishart (2006) & Sim & Sim & Sim & Sim & Não & Não \\ \hline
```

### A14 🟡 Afirmações mais fortes que a evidência, no Cap. 4

Na mesma linha do que a professora pediu para a fundamentação:

**Procure:**
```latex
Esse comportamento confirma que
```

**Substitua por:**
```latex
Esse comportamento sugere que
```

> O KNN teve o menor AUC entre os quatro modelos avançados; "confirma" é forte demais.

**Procure:**
```latex
ganho de desempenho, uma vez que ele não existe.
```

**Substitua por:**
```latex
ganho de desempenho, uma vez que esse ganho não foi observado.
```

> O próprio parágrafo seguinte lembra que essa comparação usa uma única partição.

### A15 🟡 Classificação da pesquisa (Seção 4.1): categorias que Gil não usa

**Onde:** p. 53. Gil (2002) classifica a pesquisa, **quanto aos objetivos**, em exploratória, descritiva ou explicativa. "Preditiva" não é uma dessas categorias, e a citação de Cruz e Wishart (2006) para justificar "exploratório" está fora de lugar, porque eles não tratam de metodologia de pesquisa. Sugestão: "Quanto aos objetivos, a pesquisa é exploratória e explicativa (Gil, 2002)", mantendo a explicação dos componentes preditivo e exploratório como descrição. Não montei bloco porque a mudança depende de como você quer reescrever o parágrafo.

### A16 ⚪ "Célula" × "amostra"

Em vários pontos do Cap. 2 (linhas 394, 396, 437, 516), o texto diz que o algoritmo compara "células" ("as características dessa nova célula e todas as células antigas"). Cada linha da base é **uma amostra de PAAF (um tumor)**, cujos atributos são média, erro padrão e pior valor calculados **sobre os núcleos** da imagem. Um avaliador da área da saúde pode perguntar isso. Basta trocar "célula" por "amostra" ou "paciente" onde o sentido for o registro.

### A17 ⚪ "Precisão" no sentido comum

Como "precisão" é uma métrica definida no texto, usar a palavra no sentido comum confunde o leitor. Ocorrências: "alta precisão analítica" (resumo e linha 206), "precisão artificialmente alta" (linha 283), "precisão local" (linha 498, a tradução de *local accuracy*; prefira "exatidão local") e "o algoritmo mais preciso" (conclusão). Prefira "desempenho" ou "exatidão".

---

## B. Coerência interna

### B1 🟡 "Estado atual do software" soa como relatório parcial

O título da Seção 4.8 ("Estado Atual do Software"), o da 4.8.7 ("Limitações da Versão Atual") e o roteiro ("e o estado atual do software") vêm do PG I. Na versão final, o software está pronto.

**Procure:**
```latex
\section{Estado Atual do Software}
```

**Substitua por:**
```latex
\section{O Software Desenvolvido}
```

**Procure:**
```latex
\subsection{Limitações da Versão Atual}
```

**Substitua por:**
```latex
\subsection{Limitações do software}
```

**Procure:**
```latex
a avaliação e a calibração dos modelos, e o estado atual do software.
```

**Substitua por:**
```latex
a avaliação e a calibração dos modelos, e o software desenvolvido.
```

### B2 🟡 Reprodutibilidade do Random Forest entre máquinas

Rodei `scripts/calibrar_limiares.py --so-relatorio` no Mac, com o ambiente da sua pasta local (Python 3.11, scikit-learn 1.9.0). Regressão Logística e SVM reproduziram a Tabela 7 **exatamente**. O Random Forest saiu levemente diferente: limiar 0,123 contra 0,1205, e erro sem recusa de 6,57% contra 6,10%. O notebook foi executado no Linux com Python 3.12, e os números do texto são os dele.

Isso **não é erro no texto**, mas pode virar pergunta: "se eu rodar de novo, obtenho os mesmos números?". Resposta honesta: as sementes são fixas e os modelos determinísticos reproduzem exatamente; o Random Forest pode variar na terceira casa decimal entre plataformas e versões; por isso as versões do ambiente estão fixadas em `requirements-executavel.txt`.

### B3 ⚪ O "comitê" aparece cedo como "melhor"

Além do Quadro 3 (A13), a Seção 4.7.4 apresenta o comitê como "a opção que menos erra sem recusa no treino" (5,63% contra 5,87% da RL e do SVM). É um caso a menos em 426. Não precisa mudar, mas, se perguntarem, diga que o comitê foi adotado como **padrão prático** (dilui o erro de um membro e expõe a divergência entre os modelos), e não por superioridade estatística.

---

## C. Escrita

### C1 🟡 Vírgulas onde deveria haver ponto e vírgula (orações independentes)

A professora já tinha apontado um caso desses na p. 24. Restam:

**Procure:**
```latex
conforme o modelo, decidindo todos, sobe para
```

**Substitua por:**
```latex
conforme o modelo; decidindo todos, sobe para
```

**Procure:**
```latex
se decidissem todos os casos, assim, entre 35\%
```

**Substitua por:**
```latex
se decidissem todos os casos; assim, entre 35\%
```

**Procure:**
```latex
menos de 45\% do treino, ele opera com cobertura total
```

**Substitua por:**
```latex
menos de 45\% do treino; por isso, opera com cobertura total
```

### C2 🟡 Frase confusa na p. 73

**Procure:**
```latex
sensibilidade completa a unidade em falsos positivos de 0,167.
```

**Substitua por:**
```latex
sensibilidade chega a 1,0 quando a taxa de falsos positivos atinge 0,167.
```

### C3 ⚪ Pequenas correções pontuais

**Procure:**
```latex
pode-se estabelecer um paralelo com o aprendizado humano em jogos.
```

**Substitua por:**
```latex
pode-se estabelecer um paralelo com o aprendizado humano.
```

> O parágrafo anuncia um paralelo com jogos (o exemplo original de Mitchell é o jogo de damas), mas o exemplo que vem logo depois é o de identificar tumores.

**Procure:**
```latex
qual proporção realmente era, expressada pela Equação
```

**Substitua por:**
```latex
qual proporção realmente era, expressa pela Equação
```

**Procure:**
```latex
onde $w$ é o vetor de peso que dita
```

**Substitua por:**
```latex
em que $w$ é o vetor de pesos que dita
```

### C4 ⚪ Itálico de termos estrangeiros

O padrão do trabalho é italicizar termos em inglês, mas algumas ocorrências escaparam:

**Procure:**
```latex
utilizando algoritmos de Machine Learning e a base
```

**Substitua por:**
```latex
utilizando algoritmos de \textit{Machine Learning} e a base
```

**Procure:**
```latex
Esta vertente do machine learning usa
```

**Substitua por:**
```latex
Esta vertente do \textit{Machine Learning} usa
```

**Procure:**
```latex
facilitando a identificação de agrupamentos (clusters)
```

**Substitua por:**
```latex
facilitando a identificação de agrupamentos (\textit{clusters})
```

**Procure:**
```latex
também identificasse anomalias (outliers).
```

**Substitua por:**
```latex
também identificasse anomalias (\textit{outliers}).
```

Outras, sem bloco: "K-Nearest Neighbors" (linha 663), "Abdullah et al." e "Shaon et al." sem itálico no *et al.* (linhas 637 e 677, quando no resto do texto ele está em itálico) e "upload" (resumo e linha 208).

### C5 ⚪ "Onde" como pronome relativo fora de lugar

A norma culta reserva "onde" para lugar. Há 17 ocorrências; as que não indicam lugar e ficariam melhor com "em que" ou "no qual" estão nas linhas 224, 287, 295, 307 (duas), 316, 336, 360, 466, 1582 e 1584. Exemplo: "uma situação **onde** a base de dados possui" → "uma situação **em que** a base de dados possui".

### C6 ⚪ Aspas retas

O texto usa `"palavra"\ ` (13 pares). No PDF isso sai como aspas retas ("), e foi esse padrão que gerou os erros de espaço de "abrir" e "K" apontados pela professora. Em LaTeX, as aspas tipográficas são ` ``palavra'' `. Elas saem como “palavra” e dispensam o `\ `. É opcional, mas resolve o problema de vez.

### C7 ⚪ Redundâncias

- Os parágrafos das linhas 271 e 273 dizem praticamente a mesma coisa (aprendizado supervisionado com exemplos rotulados que generaliza para dados novos). Um deles pode ser cortado.
- "no repositório UCI Machine Learning Repository" já foi resolvido no item 16 do `01`.
- Exageros que não acrescentam nada: "milimetricamente" (linha 496), "estritamente necessário" (linha 502), "altíssimo desempenho" (linha 520), "rigorosamente" (linhas 520 e 522) e "recurso indispensável" (linha 524).

---

## D. Formatação (ABNT/UTP)

> **Os itens D1 e D8 a D12 vêm do manual da UTP** (*Normas Técnicas: elaboração e apresentação de trabalhos acadêmico-científicos*, 4. ed., 2024). As páginas citadas são as do manual. O trabalho é uma monografia apresentada a banca, que é o caso descrito nas pp. 33 e 143.

### D1 🔴 Falta o resumo em língua estrangeira (*abstract*)

O manual da UTP: "O primeiro resumo do trabalho a aparecer deve estar em português. Em seguida, com as mesmas características, aparecem o(s) resumo(s) em língua estrangeira [...] Em inglês, o resumo é chamado de *Abstract*, e as palavras-chave de *Key words*" (p. 37). "Cada resumo deve ser apresentado em folha separada" (p. 37). Só os relatórios dispensam o resumo estrangeiro (p. 136); a monografia não. O documento só tem o resumo em português.

O bloco abaixo cria a página com a mesma formatação do resumo. O texto é um marcador: traduza o resumo **depois** de aplicar o item 1 do `01`.

**Procure:**
```latex
\end{resumo}
```

**Substitua por:**
```latex
\end{resumo}

% Resumo em língua estrangeira (Normas Técnicas UTP, 4. ed., 2024, p. 37)
\begin{resumo}[ABSTRACT]
    [Tradução do resumo para o inglês.]

    \vspace{.6cm}\textbf{Key words}: Machine learning; Wisconsin dataset; explainable artificial intelligence; SHAP; UMAP.
\end{resumo}
```

### D2 🟡 Ordem das listas pré-textuais

Pela NBR 14724, a ordem é: lista de ilustrações, **lista de tabelas**, lista de siglas, lista de símbolos e sumário. Hoje a lista de tabelas vem **depois** da de símbolos.

**Procure:**
```latex
\listadetabelas
```

**Substitua por:** *(nada; apague)*
```latex
```

**Procure:**
```latex
\listadequadros
```

**Substitua por:**
```latex
\listadequadros
\listadetabelas
```

### D3 🟡 Lista de siglas incompleta

Siglas usadas no texto que não estão na lista: ECE, OOD, PCA, CSV, PDF, EDA, MCC, LASSO, SMOTE, UCI, CNN, ERT, MSM-T, TCC, NN, MD e WEKA. Já CART está na lista, mas não aparece no texto. A ordem DNA/DL também está trocada.

**Procure:**
```latex
  \item[AUC] \textit{Area Under the Curve} (Área Sob a Curva)
  \item[CART] \textit{Classification and Regression Trees} (Árvores de Classificação e Regressão)
  \item[DNA] Ácido Desoxirribonucleico
  \item[DL] \textit{Deep Learning} (Aprendizado Profundo)
  \item[FN] Falso Negativo
```

**Substitua por:**
```latex
  \item[AUC] \textit{Area Under the Curve} (Área Sob a Curva)
  \item[CNN] \textit{Convolutional Neural Network} (Rede Neural Convolucional)
  \item[CSV] \textit{Comma-Separated Values} (Valores Separados por Vírgula)
  \item[DL] \textit{Deep Learning} (Aprendizado Profundo)
  \item[DNA] Ácido Desoxirribonucleico
  \item[ECE] \textit{Expected Calibration Error} (Erro Esperado de Calibração)
  \item[EDA] \textit{Exploratory Data Analysis} (Análise Exploratória de Dados)
  \item[ERT] \textit{Extremely Randomized Trees} (Árvores Extremamente Aleatorizadas)
  \item[FN] Falso Negativo
```

**Procure:**
```latex
  \item[KNN] \textit{K-Nearest Neighbors} (K-Vizinhos Mais Próximos)
  \item[LIME] \textit{Local Interpretable Model-agnostic Explanations}
```

**Substitua por:**
```latex
  \item[KNN] \textit{K-Nearest Neighbors} (K-Vizinhos Mais Próximos)
  \item[LASSO] \textit{Least Absolute Shrinkage and Selection Operator}
  \item[LIME] \textit{Local Interpretable Model-agnostic Explanations}
  \item[MCC] \textit{Matthews Correlation Coefficient} (Coeficiente de Correlação de Matthews)
  \item[MD] \textit{Minimum Distance} (Distância Mínima)
```

**Procure:**
```latex
  \item[MLE] \textit{Maximum Likelihood Estimation} (Estimativa de Máxima Verossimilhança)
  \item[OOB] \textit{Out-of-Bag}
  \item[PAAF] Punção Aspirativa por Agulha Fina
  \item[PAHO] \textit{Pan American Health Organization} (Organização Pan-Americana da Saúde)
```

**Substitua por:**
```latex
  \item[MLE] \textit{Maximum Likelihood Estimation} (Estimativa de Máxima Verossimilhança)
  \item[MSM-T] \textit{Multisurface Method-Tree} (Método Multissuperfície em Árvore)
  \item[NN] \textit{Nearest Neighbors} (Vizinhos Mais Próximos)
  \item[OOB] \textit{Out-of-Bag}
  \item[OOD] \textit{Out-of-Distribution} (Fora da Distribuição)
  \item[PAAF] Punção Aspirativa por Agulha Fina
  \item[PAHO] \textit{Pan American Health Organization} (Organização Pan-Americana da Saúde)
  \item[PCA] \textit{Principal Component Analysis} (Análise de Componentes Principais)
  \item[PDF] \textit{Portable Document Format}
```

**Procure:**
```latex
  \item[SHAP] \textit{SHapley Additive exPlanations}
  \item[SVM] \textit{Support Vector Machine} (Máquina de Vetores de Suporte)
  \item[UMAP] \textit{Uniform Manifold Approximation and Projection}
```

**Substitua por:**
```latex
  \item[SHAP] \textit{SHapley Additive exPlanations}
  \item[SMOTE] \textit{Synthetic Minority Over-sampling Technique}
  \item[SVM] \textit{Support Vector Machine} (Máquina de Vetores de Suporte)
  \item[TCC] Trabalho de Conclusão de Curso
  \item[UCI] \textit{University of California, Irvine}
  \item[UMAP] \textit{Uniform Manifold Approximation and Projection}
```

**Procure:**
```latex
  \item[WDBC] \textit{Wisconsin Diagnostic Breast Cancer}
```

**Substitua por:**
```latex
  \item[WDBC] \textit{Wisconsin Diagnostic Breast Cancer}
  \item[WEKA] \textit{Waikato Environment for Knowledge Analysis}
```

### D4 ⚪ Lista de símbolos

- $x_1$ está descrito como "Vetor de características", mas na Equação 2.5 é um único atributo (ver A6).
- $S$ tem dois significados: o conjunto de dados de um nó, na entropia, e o subconjunto de características, no SHAP. $C$ também: o hiperparâmetro do SVM e o número de classes, na Equação 2.12.
- Faltam símbolos usados no texto: $\varphi$ (mapeamento do *kernel*), $p$ (Minkowski) e $E$, $T$, $P$ (Mitchell).

### D5 ⚪ Equações com palavras em modo matemático

`Acur\acute{a}cia`, `Precis\tilde{a}o` e `F1\text{-}Score` saem em itálico matemático, com espaçamento estranho entre as letras. O padrão é `\text{Acurácia}`, `\text{Precisão}`, `\text{Sensibilidade}` etc.

### D6 Citação com dois autores entre parênteses

Este item foi incorporado ao D10, que o resolve junto com a regra dos três autores do manual da UTP.

### D7 ⚪ Pontos finais nas legendas

As legendas das Figuras 1 e 2 terminam com ponto (no código-fonte); as das outras figuras, não. Os quadros recebem ponto automaticamente do template. Basta tirar o ponto das Figuras 1 e 2.

### D8 🔴 Falta a folha de aprovação

O manual da UTP: a folha de aprovação "aparece somente em trabalhos que são apresentados para uma banca examinadora, como os Trabalhos de Conclusão de Curso [...]. Deve ser inserida após a folha de rosto" (p. 33). Na monografia, "quando houver defesa perante banca [...] deve conter um elemento chamado de 'Folha de Aprovação'" (p. 143). A UTP usa o título "Folha de Aprovação", mesmo que a NBR dispense o título (p. 34); o exemplo do manual traz "TERMO DE APROVAÇÃO". O documento não tem esse elemento.

O bloco segue os elementos e a formatação da p. 33: título; autor e título do trabalho com a formatação da capa; texto de aprovação, data e curso em espaçamento simples, sem negrito; e a banca, com o orientador primeiro (p. 33). ⚠️ Os campos entre colchetes dependem de você: a data da defesa e os nomes, titulações e instituições da banca. Confirme também com o orientador se a folha vai em branco na entrega de 14/11 ou só na versão final.

**Procure:**
```latex
\imprimirfolhaderosto
```

**Substitua por:**
```latex
\imprimirfolhaderosto

% Folha de aprovação (Normas Técnicas UTP, 4. ed., 2024, pp. 33-34)
\begin{folhadeaprovacao}
    \begin{center}
        \textbf{FOLHA DE APROVAÇÃO}

        \vspace{1cm}
        \textbf{GABRIEL AST DOS SANTOS}

        \vspace{1cm}
        \textbf{DESENVOLVIMENTO DE UM SOFTWARE COM INTELIGÊNCIA ARTIFICIAL
        EXPLICÁVEL (XAI) PARA APOIO AO DIAGNÓSTICO PREDITIVO DE CÂNCER DE MAMA
        UTILIZANDO SHAP E UMAP}
    \end{center}

    \vspace{1cm}
    \begin{SingleSpace}
        \noindent Esta monografia foi julgada e aprovada para a obtenção do
        título de Bacharel no Curso de Ciência da Computação da Universidade
        Tuiuti do Paraná.

        \begin{center}
            Curitiba, [dia] de [mês] de 2026.

            \rule{0.6\textwidth}{0.4pt}

            Bacharelado em Ciência da Computação\\
            Universidade Tuiuti do Paraná
        \end{center}

        \vspace{0.8cm}
        \noindent
        \begin{tabular}{@{}ll@{}}
            Orientador: & Prof. [titulação] Rodrigo Ramos Alves \\
                        & Universidade Tuiuti do Paraná \\[1.2cm]
                        & Prof. [titulação] [nome do membro da banca] \\
                        & [instituição] \\[1.2cm]
                        & Prof. [titulação] [nome do membro da banca] \\
                        & [instituição] \\
        \end{tabular}
    \end{SingleSpace}
\end{folhadeaprovacao}
```

### D9 🟡 Palavras-chave com iniciais maiúsculas

O manual da UTP: as palavras-chave "devem ser grafadas com as iniciais em letra minúscula, com exceção dos substantivos próprios e nomes científicos" (p. 36). No exemplo do manual, só a primeira palavra da lista vem com inicial maiúscula (p. 37). O ponto final já é posto pelo comando `\palavraschave`.

**Procure:**
```latex
\palavraschave{Aprendizado de máquina; Base de dados Wisconsin; Inteligência Artificial Explicável; SHAP; UMAP}
```

**Substitua por:**
```latex
\palavraschave{Aprendizado de máquina; base de dados Wisconsin; inteligência artificial explicável; SHAP; UMAP}
```

### D10 🟡 "et al." com três autores e "e" entre parênteses

O manual da UTP dá duas regras para as citações (pp. 23 e 56):

- com **três autores**, citam-se os três sobrenomes; "et al." só a partir de **quatro**;
- **entre parênteses**, os sobrenomes são separados por **ponto e vírgula**: "(Braz; Perez, 2018)"; **na frase**, por vírgula e "e": "Braz e Perez (2018)". A mesma regra vale para a fonte das figuras: "FONTE: Braz; Perez, 2018".

O trabalho quebra as duas regras:

- o template está configurado com `abnt-etal-cite=2` (em `packages/abnt-UTP.sty`), o que abrevia como "et al." as obras de três autores: Street, Wolberg e Mangasarian (1993); Wolberg, Street e Mangasarian (1995); Abdullah, Abdulazeez e Sallow (2021); e Manning, Raghavan e Schütze (2008);
- o padrão `(\citeauthoronline{...}, \citeyear{...})` gera, entre parênteses, a forma da frase: "(Davis e Goadrich, 2006)".

**Passo 1, no arquivo `packages/abnt-UTP.sty`** (linha 39): troque `abnt-etal-cite=2,` por `abnt-etal-cite=3,`. Com isso, as citações na frase (`\citeonline`) passam a listar os três autores, como em "Street, Wolberg e Mangasarian (1993)". Testei: compila e produz exatamente essa forma. O `abnt-etal-list=3` das referências já está de acordo com a p. 67 (et al. a partir de quatro autores).

**Passo 2, no `trabalho.tex`:** as citações entre parênteses das obras de dois e três autores passam a ter os sobrenomes digitados, mantendo o `\citeyear`, que preserva a ligação com a referência. Cada bloco abaixo substitui **todas as ocorrências**.

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
(\citeauthoronline{Street1993}, \citeyear{Street1993})
```

**Substitua por:**
```latex
(Street; Wolberg; Mangasarian, \citeyear{Street1993})
```

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
(\citeauthoronline{Davis2006}, \citeyear{Davis2006})
```

**Substitua por:**
```latex
(Davis; Goadrich, \citeyear{Davis2006})
```

**Procure:**
```latex
Adaptado de \citeauthoronline{Davis2006}, \citeyear{Davis2006}
```

**Substitua por:**
```latex
Adaptado de Davis; Goadrich, \citeyear{Davis2006}
```

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
(\citeauthoronline{Lundberg2017}, \citeyear{Lundberg2017})
```

**Substitua por:**
```latex
(Lundberg; Lee, \citeyear{Lundberg2017})
```

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
(\citeauthoronline{Adadi2018}, \citeyear{Adadi2018})
```

**Substitua por:**
```latex
(Adadi; Berrada, \citeyear{Adadi2018})
```

**Procure:**
```latex
(\citeauthoronline{NiculescuMizil2005}, \citeyear{NiculescuMizil2005})
```

**Substitua por:**
```latex
(Niculescu-Mizil; Caruana, \citeyear{NiculescuMizil2005})
```

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
(\citeauthoronline{Cruz2006}, \citeyear{Cruz2006})
```

**Substitua por:**
```latex
(Cruz; Wishart, \citeyear{Cruz2006})
```

**Procure:**
```latex
(\citeauthoronline{Manning2006}, \citeyear{Manning2006})
```

**Substitua por:**
```latex
(Manning; Raghavan; Schütze, \citeyear{Manning2006})
```

Duas citações estão quebradas em duas linhas no código-fonte, e o "Substituir tudo" não as pega:

**Procure:**
```latex
espaço original de trinta dimensões (\citeauthoronline{Cruz2006},
\citeyear{Cruz2006}).
```

**Substitua por:**
```latex
espaço original de trinta dimensões (Cruz; Wishart, \citeyear{Cruz2006}).
```

**Procure:**
```latex
importância global fornecida pelo MDI (\citeauthoronline{Lundberg2017},
\citeyear{Lundberg2017}).
```

**Substitua por:**
```latex
importância global fornecida pelo MDI (Lundberg; Lee, \citeyear{Lundberg2017}).
```

Este depende do item 16 do `01` (que troca o `\cite{Wolberg1995}`):

**Procure:**
```latex
(\citeauthoronline{Wolberg1995}, \citeyear{Wolberg1995})
```

**Substitua por:**
```latex
(Wolberg; Street; Mangasarian, \citeyear{Wolberg1995})
```

**Passo 3, os nomes digitados à mão** nos títulos do Cap. 3 e nos Quadros 2 e 3. No Quadro 2, a primeira coluna passa a ter largura fixa, para os nomes mais longos quebrarem a linha em vez de empurrar a tabela para fora da margem.

**Procure:**
```latex
(Street \textit{et al.}, 1993)}
```

**Substitua por:**
```latex
(Street; Wolberg; Mangasarian, 1993)}
```

**Procure:**
```latex
(Cruz e Wishart, 2006)}
```

**Substitua por:**
```latex
(Cruz; Wishart, 2006)}
```

**Procure:**
```latex
(Abdullah \textit{et al.}, 2021)}
```

**Substitua por:**
```latex
(Abdullah; Abdulazeez; Sallow, 2021)}
```

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
Street \textit{et al.} (1993)
```

**Substitua por:**
```latex
Street, Wolberg e Mangasarian (1993)
```

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
Abdullah \textit{et al.} (2021)
```

**Substitua por:**
```latex
Abdullah, Abdulazeez e Sallow (2021)
```

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
Cruz \& Wishart (2006)
```

**Substitua por:**
```latex
Cruz e Wishart (2006)
```

**Procure:**
```latex
\begin{tabular}{|l|c|c|c|c|c|c|}
```

**Substitua por:**
```latex
\begin{tabular}{|>{\raggedright\arraybackslash}p{3.9cm}|c|c|c|c|c|c|}
```

Com os nomes completos, os Quadros 2 e 3 ficam mais altos e não cabem mais juntos na mesma página. O Quadro 3 está preso no lugar com `[H]` e, sem esta troca, passa do pé da página e perde as duas últimas linhas (testado). Liberado, ele vai para a página seguinte, inteiro.

**Procure:**
```latex
\begin{quadro}[H]
```

**Substitua por:**
```latex
\begin{quadro}[htbp]
```

> O "Abdullah et al." do texto da p. 46 já sai corrigido pelo bloco do item A10. Se você não aplicar o A10, troque ali "Abdullah et al." por "Abdullah, Abdulazeez e Sallow".

### D11 🟡 Subtítulos de nível 3 com todas as iniciais maiúsculas

O manual da UTP fixa três níveis de título (p. 16): "1 **TÍTULO** (MAIÚSCULAS, negrito)", "1.1 SUBTÍTULO (MAIÚSCULAS, sem negrito)" e "1.1.1 Subtítulo (**só a inicial maiúscula**, sem negrito)". Os níveis 1 e 2 já saem certos, porque o template os põe em maiúsculas. Os de nível 3 (`\subsection`) saem como foram digitados, todos com as iniciais maiúsculas ("4.5.2 Distribuição das Classes"). Nomes próprios e nomes de modelos que o texto inteiro trata como nome próprio (Árvore de Decisão, KNN, Regressão Logística, Random Forest, SVM) ficam como estão. "Limitações da Versão Atual" é corrigido pelo bloco B1.

**Procure:**
```latex
\subsection{O Paradigma do Aprendizado Supervisionado e a Classificação Binária}
```

**Substitua por:**
```latex
\subsection{O paradigma do aprendizado supervisionado e a classificação binária}
```

**Procure:**
```latex
\subsection{O Dilema da Generalização e o Ciclo de Vida do Modelo}
```

**Substitua por:**
```latex
\subsection{O dilema da generalização e o ciclo de vida do modelo}
```

**Procure:**
```latex
\subsection{Métricas de Avaliação de Desempenho}
```

**Substitua por:**
```latex
\subsection{Métricas de avaliação de desempenho}
```

**Procure:**
```latex
\subsection{Principais Algoritmos Classificadores}
```

**Substitua por:**
```latex
\subsection{Principais algoritmos classificadores}
```

**Procure:**
```latex
\subsection{Fundamentação Matemática: A Equação de Shapley}
```

**Substitua por:**
```latex
\subsection{Fundamentação matemática: a equação de Shapley}
```

**Procure:**
```latex
\subsection{Codificação da Variável Alvo}
```

**Substitua por:**
```latex
\subsection{Codificação da variável alvo}
```

**Procure:**
```latex
\subsection{Divisão Treino e Teste}
```

**Substitua por:**
```latex
\subsection{Divisão em treino e teste}
```

**Procure:**
```latex
\subsection{Estatísticas Descritivas}
```

**Substitua por:**
```latex
\subsection{Estatísticas descritivas}
```

**Procure:**
```latex
\subsection{Distribuição das Classes}
```

**Substitua por:**
```latex
\subsection{Distribuição das classes}
```

**Procure:**
```latex
\subsection{Histogramas dos Atributos}
```

**Substitua por:**
```latex
\subsection{Histogramas dos atributos}
```

**Procure:**
```latex
\subsection{Boxplots dos Atributos}
```

**Substitua por:**
```latex
\subsection{\textit{Boxplots} dos atributos}
```

**Procure:**
```latex
\subsection{Comparação entre os Modelos}
```

**Substitua por:**
```latex
\subsection{Comparação entre os modelos}
```

**Procure:**
```latex
\subsection{Validação Cruzada Estratificada Repetida}
```

**Substitua por:**
```latex
\subsection{Validação cruzada estratificada repetida}
```

**Procure:**
```latex
\subsection{Testes de Significância Estatística}
```

**Substitua por:**
```latex
\subsection{Testes de significância estatística}
```

**Procure:**
```latex
\subsection{Análise de Calibração das Probabilidades}
```

**Substitua por:**
```latex
\subsection{Análise de calibração das probabilidades}
```

**Procure:**
```latex
\subsection{Ponto de Operação e Curva Risco-Cobertura}
```

**Substitua por:**
```latex
\subsection{Ponto de operação e curva risco-cobertura}
```

**Procure:**
```latex
\subsection{Organização do Código}
```

**Substitua por:**
```latex
\subsection{Organização do código}
```

**Procure:**
```latex
\subsection{Fluxo de Trabalho}
```

**Substitua por:**
```latex
\subsection{Fluxo de trabalho}
```

**Procure:**
```latex
\subsection{Sinais de Confiabilidade}
```

**Substitua por:**
```latex
\subsection{Sinais de confiabilidade}
```

**Procure:**
```latex
\subsection{Relatórios de Explicabilidade}
```

**Substitua por:**
```latex
\subsection{Relatórios de explicabilidade}
```

**Procure:**
```latex
\subsection{Auditoria, Exportação e Consulta}
```

**Substitua por:**
```latex
\subsection{Auditoria, exportação e consulta}
```

### D12 ⚪ "Software" em itálico

O manual da UTP reserva o itálico para "palavras ou expressões de línguas estrangeiras" (p. 20) e escreve "o código-fonte do *software* desenvolvido" (p. 48). Os apêndices novos já seguem isso. No restante do texto, "software" aparece 30 vezes sem itálico. Para corrigir tudo de uma vez no VS Code, use a busca com expressão regular (botão `.*`):

- Procurar: `(?<![{:\\-])\bsoftware\b`
- Substituir: `\textit{software}`

A expressão ignora rótulos como `sec:software` e `subsec:limitacoes-software` e não mexe em "Software" com inicial maiúscula (títulos). Revise cada ocorrência antes de confirmar. Como o texto inteiro está consistente sem itálico, este item é opcional; o importante é não misturar os dois jeitos. Se preferir deixar o texto como está, tire o `\textit{}` de "software" nos apêndices.

---

## E. Referências (formato)

Nenhum destes itens foi pedido pela professora. Todos são de formatação ABNT.

1. 🟡 **Siglas em minúsculas nos títulos.** O BibTeX converte os títulos para minúsculas: "(xai)", "roc curves", "umap", "xgboost", "lasso and shap", "roc plot" e "IEEE access". No `.bib`, proteja com chaves: `{XAI}`, `{ROC}`, `{UMAP}`, `{XGBoost}`, `{LASSO}`, `{SHAP}`, `{IEEE Access}`.
2. 🟡 **Street et al. (1993) incompleta:** "Nuclear feature extraction for breast tumor diagnosis. SPIE, p. 861–870, 1993." Faltam o evento e o volume. Forma completa: *In:* IS&T/SPIE'S SYMPOSIUM ON ELECTRONIC IMAGING: SCIENCE AND TECHNOLOGY, 1993, San Jose. **Proceedings** [...]. Bellingham: SPIE, 1993. v. 1905, p. 861-870.
3. ⚪ **Edição:** "2nd. ed." (Faceli) e "3rd. ed." (Russell e Norvig) → "2. ed." e "3. ed.".
4. ⚪ **Local "[S.l.]" quando é conhecido:** Bishop e Mitchell (New York), Faceli (Rio de Janeiro), Russell e Norvig (Upper Saddle River), ACM (New York).
5. ⚪ **"mai."** Pela ABNT, maio não se abrevia. São quatro entradas com "31 mai. 2026" → "31 maio 2026".
6. ⚪ **McInnes et al. (2018)** está referenciado como a *documentação* da biblioteca, mas é citado para explicar a teoria do algoritmo. O ideal seria citar o artigo: McINNES, L.; HEALY, J.; MELVILLE, J. UMAP: Uniform Manifold Approximation and Projection for Dimension Reduction. arXiv:1802.03426, 2018.
7. ⚪ **"SILVA JÚNIOR, O. J. d."** → "SILVA JÚNIOR, O. J. de".
8. ⚪ **"AI Online Course."** Pela ABNT, autor entidade vai em caixa alta: "AI ONLINE COURSE.".

---

## F. Software e entrega

1. 🔴 **Release desatualizado:** os executáveis do v1.0 (02/10) não contêm o retreino da Árvore de Decisão (08/10) nem os ajustes de 13/10. Detalhes e checklist no item 18 do `01`.
2. 🟡 **Pasta local 7 commits atrás:** `~/DiagnosisXAI` não tem os commits de outubro. Rode `git pull` antes de usar essa pasta para qualquer coisa da entrega ou da apresentação, inclusive para a demonstração ao vivo.
3. 🟡 **Arredondamento do limite inferior da faixa** (`calibrar_limiares.py`, linha 282): explicado no texto e com as duas opções no item 12 do `01`. Correção, se for fazer: na gravação, `math.floor(v[0] * 1e4) / 1e4` para o inferior.
4. ⚪ **Demonstração ao vivo:** se for mostrar o app na banca, tenha à mão `dataTeste_sem_diagnostico.csv` e o gabarito, use o modo comitê com recusa ligada e mostre um paciente "Revisar", um "Atípico" (se houver) e o bloco de fatores fechando na certeza da tabela. Rode o `--autoteste` antes de entrar na sala.
