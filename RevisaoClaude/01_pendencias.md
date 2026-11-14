# O que falta no TCC (situação em 13/11/2026)

Conferido no `trabalho.tex` do commit `71aac81` ("slide(2) + subsections corrigidas"). Ele substitui os antigos `01_pendencias_email.md` e `02_revisao_completa.md`. Cada bloco "Procure / Substitua por" deles foi comparado com o texto atual, e aqui ficou **só o que ainda falta**.

**Como usar**

- As páginas são as impressas no PDF compilado hoje (110 páginas, sem erro de compilação nem referência quebrada).
- Localize pelo texto (Ctrl+F), não pelo número da linha. Os blocos **Procure** existem exatamente assim no arquivo atual (conferido por script).
- ⚠️ marca o que depende de uma informação que só você tem.

---

## Placar

**Já resolvido desde 08/11:** apêndices A e B, com remissão no roteiro e na 4.8; parágrafo de dificuldades duplicado removido, e a conclusão continua em 3 páginas (pp. 98–100); "assegurada" trocado por "tratada"; calibração do SVM (A1); *out-of-bag*, *kernel*, `probability=True`, cinco atributos no Random Forest; "padrão ouro" trocado por "referência"; Abdullah × UMAP; Quadros 2 e 3; Tabelas 5 e 6; curva risco-cobertura; "sugere" e "não foi observado"; ponto e vírgula na p. 82; frase da p. 73; jogos, "expressa" e "em que"; itálico de *Machine Learning*; títulos da Seção 4.8 e da 4.8.7; subtítulos de nível 3 em minúsculas; "inversa exata" do UMAP.

**Falta:**

| Prioridade | Itens |
|---|---|
| 🔴 Pedido pela professora | 1 a 7 |
| 🔴 Exigido pelo manual da UTP | 8 a 10 |
| 🔴 Erro técnico | 11 (introduzido na última edição) e 12 |
| 🟡 Recomendado | 13 a 19 |
| ⚪ Estilo | 20 a 22 |
| 🔴 Fora do texto | 23 (Release do executável) |

---

## 🔴 Pedidos pela professora

### 1. Resumo sem resultados de desempenho nem limitações da base (p. 3)

**Procure:**
```latex
Os resultados quanto à explicabilidade indicam
```

**Substitua por:**
```latex
Quanto ao desempenho, a validação cruzada repetida não encontrou diferença estatisticamente significativa entre Regressão Logística, SVM, Random Forest e KNN, com acurácia média entre 0,960 e 0,973, e a Regressão Logística, modelo intrinsecamente interpretável, igualou os modelos mais complexos. Com probabilidades recalibradas e uma faixa de recusa, a Regressão Logística, o Random Forest, o SVM e o comitê de voto suave decidiram entre 67\% e 74\% dos pacientes do conjunto de teste sem erro, devolvendo os demais à revisão humana. Os resultados quanto à explicabilidade indicam
```

**Procure:**
```latex
Contudo, essa interpretabilidade ainda não foi avaliada por profissionais de saúde.
```

**Substitua por:**
```latex
Contudo, essa interpretabilidade ainda não foi avaliada por profissionais de saúde, e os modelos, treinados em uma base de 569 amostras, não foram validados em dados de outras instituições.
```

### 2. O UMAP ainda "identifica anomalias" (p. 17)

A Seção 1 explica, dois parágrafos depois, que essa função passou à distância de Mahalanobis.

**Procure:**
```latex
identificando agrupamentos (\textit{clusters}) e anomalias de forma gráfica.
```

**Substitua por:**
```latex
identificando agrupamentos (\textit{clusters}) de forma gráfica.
```

### 3. Verbos no futuro para o que já foi feito (pp. 22, 44, 49, 62)

**Procure:**
```latex
a construção do agente racional será fundamentada especificamente
```

**Substitua por:**
```latex
a construção do agente racional foi fundamentada especificamente
```

**Procure:**
```latex
cada uma das variáveis que serão processadas pelos modelos de SHAP e UMAP.
```

**Substitua por:**
```latex
cada uma das variáveis processadas pelos modelos e analisadas pelo SHAP e pelo UMAP.
```

**Procure:**
```latex
estabelecendo o patamar de desempenho que este TCC deve buscar atingir antes de aplicar as camadas de explicabilidade.
```

**Substitua por:**
```latex
estabelecendo o patamar de desempenho tomado como referência por este TCC antes da aplicação das camadas de explicabilidade.
```

O último bloco também tira a promessa de uma projeção PCA, que não aparece no trabalho:

**Procure:**
```latex
um indicativo qualitativo da separabilidade entre as classes que será
explorada formalmente nas projeções UMAP e PCA.
```

**Substitua por:**
```latex
um indicativo qualitativo da separabilidade entre as classes, retomada no
mapa populacional UMAP da Subseção~\ref{subsec:relatorios-xai}.
```

### 4. Afirmações absolutas na fundamentação, e Rudin citada ao contrário (pp. 25–43)

O mais grave é o da **p. 37**. O texto atribui a Rudin (2019) a ideia de que modelos interpretáveis têm desempenho pior, mas o artigo dela se chama *"Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead"*. Além disso, os seus próprios resultados mostram a Regressão Logística empatando com os modelos complexos.

**Procure:**
```latex
cujas equações matemáticas são naturalmente transparentes, embora frequentemente apresentem limitações de desempenho em dados biológicos complexos.
```

**Substitua por:**
```latex
cujas equações matemáticas são naturalmente transparentes. Para a autora, em decisões de alto risco esses modelos frequentemente alcançam desempenho comparável ao dos modelos de caixa preta, possibilidade que deve ser verificada antes de se recorrer a estes.
```

**Procure:**
```latex
No escopo deste estudo, opta-se pela segunda via. Ao aplicar métodos \textit{post-hoc} sobre classificadores robustos, busca-se entregar ao oncologista uma ferramenta que alie o máximo desempenho preditivo da computação moderna à transparência analítica exigida pela ética médica.
```

**Substitua por:**
```latex
No escopo deste estudo, as duas vias são combinadas: modelos intrinsecamente interpretáveis são comparados a modelos de caixa preta, e métodos \textit{post-hoc} são aplicados a todos eles, de modo a verificar se a complexidade adicional se traduz em ganho de desempenho e a acompanhar cada diagnóstico de uma explicação.
```

As demais são do mesmo tipo que a professora apontou:

| Página | Procure | Substitua por |
|---|---|---|
| 25 | `Para garantir que o classificador encontre o equilíbrio estatístico perfeito e seja seguro para uso clínico, é obrigatório adotar` | `Para buscar esse equilíbrio e estimar honestamente o desempenho do classificador, é necessário adotar` |
| 31 | `os mais utilizados na prática para garantir que o algoritmo se adapte perfeitamente à complexidade biológica do câncer.` | `os mais utilizados na prática para que o algoritmo se adapte a fronteiras de decisão não lineares.` |
| 36 | `gera um sistema preditivo altamente estável e protegido contra anomalias` | `gera um sistema preditivo mais estável e menos sensível a ruídos` |
| 39 | `garantindo que o valor final seja distribuído de maneira perfeitamente justa.` | `de modo que o valor final seja distribuído de maneira justa, no sentido dos axiomas propostos por Shapley.` |
| 39 | `O resultado é um único valor $\phi_i$ que quantifica, com exatidão matemática, o impacto líquido` | `O resultado é um único valor $\phi_i$ que quantifica o impacto líquido` |
| 41 | `o UMAP assegura que as proporções de distância sejam mantidas na projeção visual.` | `o UMAP tende a preservar melhor a disposição geral dos dados, embora as distâncias entre agrupamentos na projeção não devam ser lidas como distâncias reais.` |
| 43 | `Essa representação comprova a capacidade visual do algoritmo` | `Essa representação ilustra a capacidade visual do algoritmo` |

A frase da p. 41 também está **errada**: o UMAP não preserva distâncias, e é justamente por isso que o Capítulo 4 passa a detecção de atípicos à distância de Mahalanobis.

### 5. Friedman: a ressalva vem depois do "inequívoca" (pp. 78–80)

A professora pediu a explicação 5×2cv × Nemenyi **antes** de concluir que a Árvore de Decisão é inferior. Hoje a ordem é: Tabela 4 → "é inequívoca" → explicação. Além disso, "inequívoca" contradiz o "lidos como panorama" de dois parágrafos antes.

**(a) Pontuação**

**Procure:**
```latex
otimistas, por isso, o Friedman e o Nemenyi são lidos como panorama.
```

**Substitua por:**
```latex
otimistas; por isso, o Friedman e o Nemenyi são lidos como panorama.
```

**(b) Apagar o parágrafo do lugar atual** (ele volta no passo c). Apague também a linha em branco que vem depois dele.

**Procure:**
```latex
A diferença entre os dois testes para a Árvore de Decisão decorre do que cada um usa. O 5×2cv compara dois modelos com apenas dez estimativas de diferença, cada uma obtida treinando em metade do conjunto de treino, o que reduz seu poder. O Nemenyi usa as posições dos cinco modelos nas 50 dobras, e nelas a Árvore de Decisão fica quase sempre entre as piores, o que produz uma diferença de postos superior à distância crítica do teste. Assim, o resultado do 5×2cv não contradiz o do Nemenyi: o primeiro não tem poder para detectar essa diferença.
```

**Substitua por:** *(nada; apague)*

**(c) Pôr a explicação antes da leitura da Tabela 4 e tirar o "inequívoca"**

**Procure:**
```latex
A leitura da Tabela~\ref{tab:nemenyi} é inequívoca e constitui o principal
```

**Substitua por:**
```latex
Antes de ler a Tabela~\ref{tab:nemenyi}, é preciso explicar por que ela aponta, para a Árvore de Decisão, uma diferença que o 5$\times$2cv não detectou. A diferença entre os dois testes decorre do que cada um usa. O 5$\times$2cv compara dois modelos com apenas dez estimativas de diferença, cada uma obtida treinando em metade do conjunto de treino, o que reduz seu poder. O Nemenyi usa as posições dos cinco modelos nas 50 dobras, e nelas a Árvore de Decisão fica quase sempre entre as piores, o que produz uma diferença de postos superior à distância crítica do teste. Assim, o resultado do 5$\times$2cv não contradiz o do Nemenyi: o primeiro tem pouco poder para detectar essa diferença.

Com essa ressalva, a leitura da Tabela~\ref{tab:nemenyi} constitui o principal
```

**(d) Tirar o "estatisticamente sustentada"**

**Procure:**
```latex
demais classificadores, com valores de $p$ entre 0,0000 e 0,0004, sua
inferioridade como \textit{baseline} é estatisticamente sustentada.
```

**Substitua por:**
```latex
demais classificadores, com valores de $p$ entre 0,0000 e 0,0004; sua
inferioridade como \textit{baseline} é sustentada pelo pós-hoc, com a ressalva
de dependência entre as dobras já apontada.
```

### 6. Faixa de recusa: os limites estão dentro ou fora? (p. 82)

A professora pediu: *"Esclareça a inclusão dos limites da faixa."* No código (`decision.py`), a faixa é [inferior; superior).

**Procure:**
```latex
dentro dela são devolvidos para revisão humana.
```

**Substitua por:**
```latex
dentro dela são devolvidos para revisão humana. A faixa inclui o limite
inferior e exclui o superior: o paciente com certeza igual ao limite inferior é
devolvido para revisão, e o paciente com certeza igual ou maior que o limite
superior é decidido como maligno, razão pela qual esse limite é gravado
0,0001 acima da maior certeza atribuída a um benigno.
```

### 7. Fonte das figuras em dois formatos

O PDF tem 20 figuras com "FONTE: O Autor" e 20 com "FONTE: O autor", e a Tabela 1 usa ainda um terceiro formato, "Fonte: O Autor".

Use **Substituir tudo** para trocar `\fonte{O Autor}` por `\fonteautor`. Depois troque `\legend{Fonte: O Autor}` por `\fonteautor`.

### 8. ⚠️ Referência da base de dados (p. 55)

**(a) A chamada destoa das outras.** É a única citação feita com `\cite{}`, por isso sai em caixa alta, "(WOLBERG et al., 1995)", e o texto ainda repete "repositório UCI Machine Learning Repository".

**Procure:**
```latex
(Diagnostic)}, disponibilizada publicamente no repositório UCI Machine Learning
Repository \cite{Wolberg1995}, e referenciada ao longo
```

**Substitua por:**
```latex
(Diagnostic)}, disponibilizada publicamente no UCI Machine Learning
Repository (Wolberg; Street; Mangasarian, \citeyear{Wolberg1995}), e referenciada ao longo
```

**(b) ⚠️ De onde veio o arquivo.** O `data.csv` tem cabeçalho e a coluna `Unnamed: 32`, que é o formato da cópia do **Kaggle** (`uciml/breast-cancer-wisconsin-data`); o arquivo do UCI não tem nenhum dos dois. A professora pediu "a versão/local de obtenção". Se você baixou do Kaggle, acrescente esta entrada ao `.bib`:

```bibtex
@misc{Kaggle2016,
  author        = {{UCI Machine Learning}},
  title         = {Breast Cancer Wisconsin (Diagnostic) Data Set},
  year          = {2016},
  howpublished  = {Kaggle},
  note          = {Arquivo data.csv},
  url           = {https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data},
  urlaccessdate = {13 nov. 2026}
}
```

e esta frase logo depois da do bloco (a):

```latex
O arquivo utilizado, data.csv, foi obtido na cópia da base publicada no Kaggle
(UCI Machine Learning, \citeyear{Kaggle2016}), que traz os nomes das colunas no
cabeçalho.
```

---

## 🔴 Exigidos pelo manual da UTP (Normas Técnicas, 4. ed., 2024)

### 9. Abstract e folha de aprovação

**Abstract** (manual, p. 37: em folha separada, logo depois do resumo). Traduza o resumo **depois** de aplicar o item 1.

**Procure:**
```latex
\end{resumo}
```

**Substitua por:**
```latex
\end{resumo}

\begin{resumo}[ABSTRACT]
    [Tradução do resumo para o inglês.]

    \vspace{.6cm}\textbf{Key words}: Machine learning; Wisconsin dataset; explainable artificial intelligence; SHAP; UMAP.
\end{resumo}
```

**Folha de aprovação** (manual, pp. 33–34: obrigatória em TCC apresentado a banca, logo depois da folha de rosto). ⚠️ Pergunte ao orientador se ela já vai nesta entrega ou só na versão final. Ela depende da data da defesa e dos nomes da banca.

**Procure:**
```latex
\imprimirfolhaderosto
```

**Substitua por:**
```latex
\imprimirfolhaderosto

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

Confira o título do trabalho com o da capa antes de usar.

### 10. Palavras-chave e citações de dois e três autores

**Palavras-chave** em minúsculas, exceto nomes próprios (manual, p. 36):

**Procure:**
```latex
\palavraschave{Aprendizado de máquina; Base de dados Wisconsin; Inteligência Artificial Explicável; SHAP; UMAP}
```

**Substitua por:**
```latex
\palavraschave{Aprendizado de máquina; base de dados Wisconsin; inteligência artificial explicável; SHAP; UMAP}
```

**Citações** (manual, pp. 23 e 56): "et al." só a partir de **quatro** autores, e, entre parênteses, os sobrenomes são separados por **ponto e vírgula**, como em "(Davis; Goadrich, 2006)". Hoje o texto abrevia obras de três autores e escreve "(Davis e Goadrich, 2006)".

**Passo 1:** em `packages/abnt-UTP.sty`, linha 39, troque `abnt-etal-cite=2,` por `abnt-etal-cite=3,`.

**Passo 2:** no `trabalho.tex`, use **Substituir tudo** em cada linha da tabela:

| Procure | Substitua por |
|---|---|
| `(\citeauthoronline{Street1993}, \citeyear{Street1993})` | `(Street; Wolberg; Mangasarian, \citeyear{Street1993})` |
| `(\citeauthoronline{Davis2006}, \citeyear{Davis2006})` | `(Davis; Goadrich, \citeyear{Davis2006})` |
| `Adaptado de \citeauthoronline{Davis2006}, \citeyear{Davis2006}` | `Adaptado de Davis; Goadrich, \citeyear{Davis2006}` |
| `(\citeauthoronline{Lundberg2017}, \citeyear{Lundberg2017})` | `(Lundberg; Lee, \citeyear{Lundberg2017})` |
| `(\citeauthoronline{Adadi2018}, \citeyear{Adadi2018})` | `(Adadi; Berrada, \citeyear{Adadi2018})` |
| `(\citeauthoronline{NiculescuMizil2005}, \citeyear{NiculescuMizil2005})` | `(Niculescu-Mizil; Caruana, \citeyear{NiculescuMizil2005})` |
| `(\citeauthoronline{Cruz2006}, \citeyear{Cruz2006})` | `(Cruz; Wishart, \citeyear{Cruz2006})` |
| `(\citeauthoronline{Manning2006}, \citeyear{Manning2006})` | `(Manning; Raghavan; Schütze, \citeyear{Manning2006})` |
| `(Street \textit{et al.}, 1993)}` | `(Street; Wolberg; Mangasarian, 1993)}` |
| `(Cruz e Wishart, 2006)}` | `(Cruz; Wishart, 2006)}` |
| `(Abdullah \textit{et al.}, 2021)}` | `(Abdullah; Abdulazeez; Sallow, 2021)}` |
| `Street \textit{et al.} (1993)` | `Street, Wolberg e Mangasarian (1993)` |
| `Abdullah \textit{et al.} (2021)` | `Abdullah, Abdulazeez e Sallow (2021)` |
| `Cruz \& Wishart (2006)` | `Cruz e Wishart (2006)` |

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

**Passo 3:** com os nomes completos, os Quadros 2 e 3 crescem. No Quadro 2, troque `\begin{tabular}{|l|c|c|c|c|c|c|}` por `\begin{tabular}{|>{\raggedright\arraybackslash}p{3.9cm}|c|c|c|c|c|c|}`. No Quadro 3, troque `\begin{quadro}[H]` (a única ocorrência ativa) por `\begin{quadro}[htbp]`; sem isso, ele passa do pé da página e perde as duas últimas linhas.

Recompile e confira os Quadros 2 e 3 no PDF.

---

## 🔴 Erros técnicos

### 11. "Intervalo aberto [0, 1]" (p. 30), introduzido na última edição

Os colchetes indicam intervalo **fechado**, o que contradiz a palavra "aberto". A sigmoide nunca chega a 0 nem a 1.

**Procure:**
```latex
para o intervalo aberto $[0, 1]$ ao calcular
```

**Substitua por:**
```latex
para o intervalo aberto $(0, 1)$ ao calcular
```

### 12. A especificidade não está definida na fundamentação (p. 27)

Ela é o critério do limiar (piso de 92%) e aparece nas Tabelas 1, 2 e 7 e na auditoria, mas a Seção 2.3.3 só define acurácia, sensibilidade, precisão e F1. É uma pergunta provável da banca.

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

⚠️ Confira se Faceli et al. definem a especificidade. Se não definirem, troque a citação.

---

## 🟡 Recomendados

### 13. Parâmetros do UMAP (pp. 42 e 92)

"Os valores do exemplo são ilustrativos" já entrou, mas o trabalho ainda não diz quais valores **foram** usados (15 e 0,1, os padrões da biblioteca). Essa pergunta é provável.

**Procure:**
```latex
Os valores do exemplo são ilustrativos.
```

**Substitua por:**
```latex
Os valores do exemplo são ilustrativos; o mapa populacional deste trabalho utiliza n\_neighbors = 15 e min\_dist = 0,1, valores padrão da biblioteca, conforme a Subseção~\ref{subsec:relatorios-xai}.
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

### 14. Regressão Logística: "gradiente descendente" (p. 30)

O projeto usa o *solver* `liblinear`, que não usa gradiente descendente.

**Procure:**
```latex
um processo otimizado iterativamente por gradiente descendente que busca
```

**Substitua por:**
```latex
um processo resolvido iterativamente por métodos de otimização numérica, como o gradiente descendente, que busca
```

### 15. Sujeito ambíguo na 4.8.2 (p. 87), introduzido em 10/11

A frase anterior tem "o sistema" como sujeito, então parece que é o sistema quem escolhe o classificador.

**Procure:**
```latex
coluna e a linha do problema. Em seguida, seleciona
```

**Substitua por:**
```latex
coluna e a linha do problema. Em seguida, o profissional seleciona
```

### 16. Ordem das listas pré-textuais

Pela NBR 14724, a lista de tabelas vem antes da de siglas; hoje ela vem depois da de símbolos. Apague a linha `\listadetabelas` e troque `\listadequadros` por:

```latex
\listadequadros
\listadetabelas
```

### 17. Lista de siglas incompleta

Faltam ECE, OOD, PCA, CSV, PDF, EDA, MCC, LASSO, SMOTE, UCI, CNN, ERT, MSM-T, TCC, NN, MD e WEKA. CART está na lista mas não aparece no texto, e DNA e DL estão fora da ordem alfabética.

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
  \item[OOB] \textit{Out-of-Bag}
  \item[PAAF] Punção Aspirativa por Agulha Fina
  \item[PAHO] \textit{Pan American Health Organization} (Organização Pan-Americana da Saúde)
```

**Substitua por:**
```latex
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

### 18. Referências (formato ABNT)

No `referencias.bib`:

- **Siglas em minúsculas no PDF:** hoje saem "(xai)", "IEEE access", "roc curves" e "the roc plot". Proteja com chaves no título: `{XAI}`, `{IEEE Access}`, `{ROC}`.
- **Street et al. (1993) incompleta:** a entrada é `@article` com `booktitle`, e sai sem evento nem volume. Troque por `@inproceedings`, acrescentando `volume = {1905}` e `address = {San Jose}`.
- **Edição:** `edition = {3rd}` (Russell e Norvig) e `{2nd}` (Faceli) saem "3rd. ed."; use `{3}` e `{2}`.
- **"31 mai. 2026"** (4 entradas IBM): pela ABNT, maio não se abrevia → `31 maio 2026`.
- **Local "[S.l.]"** em Bishop, Mitchell e Russell e Norvig: acrescente `address`.
- **"SILVA JÚNIOR, O. J. d."** → corrija o nome no `.bib` para sair "O. J. de".
- **"AI Online Course"**: autor entidade vai em caixa alta, "AI ONLINE COURSE".

### 19. Contagem de colunas (p. 55, opcional)

O número errado saiu, mas a professora vai procurar essa correção. Vale deixá-la visível.

**Procure:**
```latex
Antes do início do \textit{pipeline} de modelagem, duas colunas foram removidas
```

**Substitua por:**
```latex
O arquivo original possui 33 colunas: id, diagnosis, os trinta atributos e
Unnamed: 32. Antes do início do \textit{pipeline} de modelagem, duas colunas foram removidas
```

---

## ⚪ Estilo (se der tempo)

### 20. Equações com palavras em modo matemático (pp. 26–27)

`Acur\acute{a}cia`, `Precis\tilde{a}o` e `F1\text{-}Score` saem em itálico, com espaçamento estranho entre as letras. Use `\text{Acurácia}`, `\text{Precisão}`, `\text{Sensibilidade}`, `\text{F1-Score}`. As legendas das Figuras 1 e 2 terminam com ponto, e as outras não; tire o ponto delas.

### 21. "Precisão" no sentido comum

"Precisão" é uma métrica definida no texto, por isso usá-la no sentido comum confunde. Ocorrências: "alta precisão analítica" (resumo e Seção 1.2), "precisão artificialmente alta" (p. 25) e "precisão local" (p. 38, onde o certo é "exatidão local", tradução de *local accuracy*). Troque por "desempenho" ou "exatidão".

### 22. Miudezas

- **"Onde" fora do sentido de lugar:** 15 ocorrências; troque por "em que" quando não for lugar.
- **Aspas retas:** 12 pares no formato `"palavra"\ `. As tipográficas seriam ` ``palavra'' `.
- **Exageros:** "milimetricamente", "estritamente necessário", "altíssimo desempenho", "rigorosamente" (2) e "recurso indispensável".
- **Itálico faltando:** "upload" (resumo e linha 208) e "K-Nearest Neighbors" (linhas 63, 377, 598, 1227).
- **Classificação da pesquisa (4.1):** Gil (2002) classifica a pesquisa, quanto aos objetivos, em exploratória, descritiva ou explicativa; "preditiva" não é uma das categorias dele.
- **"Célula" × "amostra" no Cap. 2:** cada linha da base é uma amostra de PAAF, ou seja, um tumor, e não uma célula.

---

## 🔴 Fora do texto

### 23. Release do executável desatualizado

Conferido hoje no GitHub (`git ls-remote`): a única tag publicada é a **v1.0**, que aponta para `5ad719e` (02/10). Ela é anterior a `26d7558` (08/10, retreino da Árvore de Decisão sem vazamento) e a `22cbe5a` (13/10). Assim, **a Árvore do executável não é a da Tabela 1**, e quem abrir o v1.0 e comparar vai ver números diferentes.

- [ ] No `~/vscode/DiagnosisXAI`, que está em dia com o GitHub: `git tag v1.1 && git push origin v1.1`. O workflow `executavel.yml` gera e publica os dois `.zip`.
- [ ] Baixar os dois `.zip` do v1.1 e rodar `DiagnosisXAI --autoteste`.
- [ ] Na entrega: o PDF, os dois `.zip` e o link do repositório.

---

## ⚠️ O que depende de você

- Origem do `data.csv`, Kaggle ou UCI (item 8).
- Se `hyperplane.png` saiu mesmo de aionlinecourse.com (Figura 6).
- Folha de aprovação: data da defesa, banca e se ela vai nesta entrega (item 9).
- Tradução do abstract (item 9).
- Arredondamento do limite inferior da faixa: hoje o texto explica um defeito conhecido do `calibrar_limiares.py`. Prepare a resposta para "por que não corrigiu?" (pergunta 42 do `03_perguntas_banca.md`).
- Por que XGBoost e redes neurais saíram do trabalho (pergunta 24).
