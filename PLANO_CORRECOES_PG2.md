# Plano de correções — devolutiva da versão do PG II (outubro)

Plano para aplicar, à mão, todas as correções do e-mail da professora no `trabalho.tex` e no `referencias.bib`.

## Como usar este plano

- **A ordem é a do e-mail.** As Seções 1 a 4 têm os mesmos títulos do e-mail (Resumo e introdução; Coerência e fechamento; Revisão linguística; Citações e referências). Cada item abre com o trecho do e-mail a que responde (**E-mail:**), na mesma sequência. O checklist final corresponde ao último parágrafo do e-mail (entrega de 14/11).
- **Correções mínimas.** Cada bloco muda só o que o e-mail aponta; o resto da frase e do parágrafo fica como está. Onde a professora pede conteúdo novo (roteiro, dificuldades, blocos do Friedman, limites da faixa, referência da base), ele é **acrescentado** ao texto existente, sem reescrever o que está em volta.
- Cada item traz o **arquivo**, a **linha** de referência (do `trabalho.tex` atual, antes de qualquer edição), um bloco **Procure** e um bloco **Substitua por**.
- Os números de linha mudam conforme você edita. **Localize sempre pelo texto do bloco Procure** (Ctrl+F no VS Code), e não pelo número da linha. Nos parágrafos longos dos Capítulos 1 e 2 (uma linha por parágrafo), o Procure é só o trecho que muda.
- Blocos marcados como **Alternativa B** só valem se a situação descrita for a sua.
- Todos os blocos Procure / Substitua por deste arquivo foram aplicados numa cópia do projeto e compilados (pdflatex + bibtex) antes de o plano ser entregue: todos os trechos existem no arquivo e o resultado compila.
- Itens marcados com ⚠️ dependem de uma informação que só você tem. A lista completa está em [Pendências que só você pode confirmar](#pendências-que-só-você-pode-confirmar).

---

## 1. Resumo e introdução

### 1.1 Atualizar o resumo (p. 3)

> **E-mail:** "Atualize o resumo (p. 3): 'propõe o desenvolvimento' e 'resultados esperados' não correspondem ao software implementado e aos experimentos apresentados. Sintetize os resultados efetivamente obtidos e suas limitações. Substitua a afirmação de explicabilidade 'garantida' por uma descrição do recurso implementado [...]."

**Arquivo:** `trabalho.tex` — linha 60 (ambiente `resumo`)

São três trocas no mesmo parágrafo; as demais frases do resumo ficam iguais.

**(a) "propõe o desenvolvimento"**

**Procure:**
```latex
Este trabalho propõe o desenvolvimento de um software
```

**Substitua por:**
```latex
Este trabalho apresenta o desenvolvimento de um software
```

**(b) Explicabilidade "garantida"**

**Procure:**
```latex
A explicabilidade das decisões é garantida pela integração da biblioteca SHAP, enquanto
```

**Substitua por:**
```latex
A explicabilidade das decisões é apoiada pela biblioteca SHAP, que quantifica a contribuição de cada atributo celular para o risco estimado, enquanto
```

**(c) "Resultados esperados" → resultados obtidos e limitações** (última frase do resumo)

**Procure:**
```latex
Os resultados esperados indicam que a combinação de modelos preditivos de alto desempenho com técnicas de inteligência artificial explicável constitui uma solução viável e eticamente fundamentada para o apoio ao diagnóstico oncológico assistido por computador.
```

**Substitua por:**
```latex
Os resultados indicam que, na base estudada, a Regressão Logística, modelo intrinsecamente interpretável, igualou modelos mais complexos: entre os quatro melhores classificadores, com acurácia média entre 0,960 e 0,973 sob validação cruzada, não houve diferença estatisticamente significativa. Com probabilidades recalibradas e uma faixa de recusa, os modelos decidiram entre 67\% e 74\% dos pacientes do conjunto de teste sem erro, devolvendo os demais à revisão humana. Como limitações, destacam-se o tamanho reduzido da base, a ausência de validação em dados externos e a falta de avaliação das explicações por profissionais de saúde.
```

> Os números vêm do texto: Tabela 2 (0,960 a 0,973) e Tabela 7 (67% a 74%).

---

### 1.2 Roteiro dos capítulos e apêndices com os manuais (p. 19)

> **E-mail:** "Acrescente, ao final da introdução (p. 19), o roteiro dos capítulos e a indicação dos apêndices com os manuais. O arquivo termina nas referências; transforme as orientações operacionais das pp. 87–98 em documentação de instalação e uso identificada como apêndice, completando-a quando necessário."

**(a) Roteiro: novo parágrafo no fim da introdução**

**Arquivo:** `trabalho.tex` — fim da linha 203 (último parágrafo da introdução)

O parágrafo do roteiro entra logo depois do último parágrafo da introdução, que termina em "...fundamentações visuais.".

**Procure:**
```latex
com os resumos dos diagnósticos e suas respectivas fundamentações visuais.
```

**Substitua por:**
```latex
com os resumos dos diagnósticos e suas respectivas fundamentações visuais.

Além desta introdução, o trabalho está organizado em quatro capítulos. O Capítulo~\ref{cap:fundamentacao} apresenta a fundamentação teórica sobre o câncer de mama, o aprendizado de máquina, a inteligência artificial explicável, o SHAP e o UMAP. O Capítulo~\ref{cap:trabalhos_relacionados} discute os trabalhos relacionados e a lacuna de pesquisa. O Capítulo~\ref{cap:metodologia} descreve a metodologia de construção da solução, as ferramentas utilizadas, os resultados obtidos e o software desenvolvido. O Capítulo~\ref{cap:consideracoes-finais} apresenta a conclusão. Os Apêndices~A e~B trazem, respectivamente, os manuais de instalação e de uso do software.
```

**(b) Apêndices A (instalação) e B (uso)**

**Arquivo:** `trabalho.tex` — linhas 3583–3584 (logo após `\bibliography{referencias}`)

Pela ABNT, os apêndices vêm **depois** das referências. O template da UTP já tem o comando `\apendice{Título}`, que gera "APÊNDICE A – TÍTULO" e a entrada no sumário. O conteúdo reaproveita as orientações operacionais das Seções 4.8.2 a 4.8.6 e as completa (requisitos, instalação do executável e do código-fonte, formato da planilha, leitura das colunas e cuidados de uso).

⚠️ Antes de entregar, confira no Release do GitHub os três pontos marcados com `% CONFIRMAR` no bloco: nome do executável, aviso do Windows e permissão de execução no Linux.

**Procure:**
```latex
% Carrega o arquivo referencias.bib
\bibliography{referencias}
```

**Substitua por:**
```latex
% Carrega o arquivo referencias.bib
\bibliography{referencias}

% -------------------------------------------------------------------------------------------------
% APÊNDICES
% -------------------------------------------------------------------------------------------------
\apendice{Manual de instalação do DiagnosisXAI}

Este apêndice descreve como instalar e executar o DiagnosisXAI, software
desenvolvido neste trabalho. Há duas formas de uso: o executável, indicado a
quem deseja apenas operar o sistema, e o código-fonte, necessário para
reproduzir os experimentos ou retreinar os modelos. O código-fonte e os
executáveis estão disponíveis no repositório
\url{https://github.com/Gabas/DiagnosisXAI}.

\section*{A.1 Requisitos}

Para utilizar o sistema, são necessários:

\begin{alineas}
    \item computador com Windows ou Linux de 64 bits, para o executável, ou com
          Windows, Linux ou macOS, para o código-fonte;
    \item tela com resolução de 1920~$\times$~1080 pixels ou próxima dela; em
          telas menores, a interface reduz proporcionalmente a escala dos
          componentes e limita cada janela a 90\% da área disponível;
    \item navegador web, para as versões interativas do mapa populacional e da
          margem do SVM;
    \item para o código-fonte, Python 3.12 e Git.
\end{alineas}

\section*{A.2 Instalação do executável}

O executável dispensa a instalação do Python e de qualquer biblioteca. Para
instalá-lo:

\begin{alineas}
    \item acesse a página de versões (\textit{Releases}) do repositório,
          \url{https://github.com/Gabas/DiagnosisXAI/releases}, e baixe o
          arquivo .zip da versão mais recente correspondente ao seu sistema
          operacional;
    \item extraia o conteúdo do arquivo .zip em uma pasta de sua escolha,
          mantendo todos os arquivos juntos, pois o programa depende da pasta
          inteira, e não apenas do executável;
    % CONFIRMAR: nome do executável e o aviso exibido pelo Windows.
    \item no Windows, abra o arquivo DiagnosisXAI.exe; caso o sistema exiba um
          aviso de segurança por se tratar de um programa sem assinatura
          digital, selecione Mais informações e, em seguida, Executar assim
          mesmo;
    % CONFIRMAR: nome do executável no Linux e se o .zip preserva a permissão de execução.
    \item no Linux, abra um terminal na pasta extraída e execute
          \texttt{./DiagnosisXAI}; se necessário, conceda antes a permissão de
          execução com \texttt{chmod +x DiagnosisXAI};
    \item opcionalmente, para conferir a instalação, execute o programa com a
          opção \texttt{-}\texttt{-autoteste}, que percorre sem interface as
          catorze etapas do uso real e informa se alguma falhou.
\end{alineas}

O executável grava o histórico de sessões e os relatórios em PDF na pasta
DiagnosisXAI do diretório pessoal do usuário, pois a pasta do programa pode ser
somente leitura. Para desinstalar o sistema, basta apagar a pasta extraída e,
se desejado, essa pasta de dados.

\section*{A.3 Execução a partir do código-fonte}

A execução pelo código-fonte é indicada para reproduzir os experimentos do
Capítulo~\ref{cap:metodologia}. No macOS e no Linux, a biblioteca gráfica
Tkinter, usada pela interface, é distribuída separadamente do Python e deve ser
instalada junto com ele, por exemplo pelo pacote python3-tk, no Ubuntu, ou
python-tk@3.12, no Homebrew. Os passos são:

\begin{alineas}
    \item clone o repositório com o comando \texttt{git clone}, seguido do
          endereço \url{https://github.com/Gabas/DiagnosisXAI.git}, e entre na
          pasta DiagnosisXAI;
    \item crie um ambiente virtual com \texttt{python3 -m venv .venv} e
          ative-o com \texttt{source .venv/bin/activate}, no Linux e no macOS,
          ou \texttt{.venv\textbackslash Scripts\textbackslash activate}, no
          Windows;
    \item instale as dependências com
          \texttt{pip install -r requirements.txt}; para reproduzir exatamente o
          ambiente que gerou o arquivo wisconsin.pkl, use o arquivo
          requirements-executavel.txt, que fixa as versões exatas;
    \item entre na pasta app e inicie a aplicação com
          \texttt{python main.py}.
\end{alineas}

Os modelos treinados já acompanham o repositório, no arquivo
data/wisconsin.pkl. Para retreiná-los, abra o \textit{notebook}
notebooks/Wisconsin.ipynb no Jupyter e execute todas as células, o que regrava o
wisconsin.pkl; em seguida, execute \texttt{python scripts/calibrar\_limiares.py}
a partir da raiz do repositório, para recalcular os limiares e as faixas de
recusa gravados em data/limiares.json. Os testes automatizados são executados
com o comando \texttt{pytest}, também a partir da raiz.

\apendice{Manual de uso do DiagnosisXAI}

Este apêndice orienta a operação do DiagnosisXAI. As telas mencionadas estão
ilustradas na Seção~\ref{sec:software}.

\section*{B.1 Organização da interface}

A barra lateral dá acesso a quatro abas:

\begin{alineas}
    \item Início: exibe o estado do sistema, como os modelos carregados e os
          biomarcadores ativos;
    \item Novo Diagnóstico: conduz o processamento de um lote em seis passos;
    \item Histórico: lista as sessões anteriores e permite reabrir seus
          relatórios de explicabilidade sem reprocessar o lote;
    \item Sobre: reúne o memorial de cálculo, que explica a origem de cada
          número exibido, e o glossário dos trinta biomarcadores.
\end{alineas}

O tema claro ou escuro da interface pode ser trocado no seletor do rodapé da
barra lateral.

\section*{B.2 Preparação da planilha de entrada}

O sistema recebe os pacientes em um arquivo CSV, uma linha por paciente, com as
trinta colunas morfológicas da base Wisconsin, nomeadas como na base original
(radius\_mean, texture\_mean, \ldots, fractal\_dimension\_worst). Os valores
devem ser os brutos, medidos pelo laboratório, e não padronizados, pois a
padronização é feita pelo próprio sistema. A planilha não deve conter as colunas
id nem diagnosis. O lote é recusado, com mensagem que indica a coluna e a linha
do problema, quando falta alguma coluna, há células vazias, texto onde se
esperava número, valores negativos ou nenhuma linha de dados. O repositório
traz um arquivo de exemplo, data/dataTeste\_sem\_diagnostico.csv, com os 143
pacientes do conjunto de teste.

Para a auditoria do quarto passo, usa-se um segundo arquivo, o gabarito, com as
mesmas colunas acrescidas da coluna diagnosis, preenchida com 1 para maligno e
0 para benigno, como no arquivo data/dataTeste\_com\_diagnostico.csv.

\section*{B.3 Processamento de um lote}

Na aba Novo Diagnóstico, cada passo é liberado somente após a conclusão do
anterior, conforme a Figura~\ref{fig:app_pipeline}:

\begin{alineas}
    \item Passo 1, Importar Dados Brutos (CSV): selecione a planilha; os valores
          aparecem na tabela;
    \item Passo 2, Higienizar e Escalar (Z-Score): clique em Aplicar
          Padronização; o sistema valida a planilha e aplica a padronização
          ajustada no conjunto de treino;
    \item Passo 3, Inteligência Artificial: escolha na lista um dos cinco
          classificadores, o Comitê (voto suave) ou Todos (Comparação), opção
          selecionada ao abrir a tela; confira a régua de decisão exibida e
          clique em Processar Diagnóstico. A opção Adiar casos incertos em vez
          de decidir vem ligada e só está disponível para a Regressão
          Logística, o Random Forest, o SVM e o comitê;
    \item Passo 4, Auditoria Acadêmica (opcional): carregue o gabarito para
          obter a cobertura, as métricas de desempenho, a matriz de confusão e
          uma leitura crítica dos resultados;
    \item Passo 5, Explicabilidade (XAI): abra a janela de explicação do modelo
          executado e selecione um paciente para ver os fatores que mais
          pesaram e o raciocínio próprio do modelo; a partir dessa janela, é
          possível exportar o laudo individual do paciente em PDF;
    \item Passo 6, Exportar Resultados: salve a tabela completa em CSV ou o
          relatório do lote em PDF, acompanhado da régua de decisão.
\end{alineas}

\section*{B.4 Leitura dos resultados}

A tabela de resultados traz, para cada paciente, as seguintes colunas:

\begin{alineas}
    \item Diagnóstico\_IA: Maligno, Benigno ou Revisar; Revisar não é uma
          classe intermediária, e sim a indicação de que o sistema se absteve e
          de que o caso deve ser avaliado pelo especialista;
    \item Certeza\_Maligno(\%): probabilidade calibrada de malignidade; ela não
          deve ser comparada a 50\%, pois o diagnóstico decorre dos cortes da
          régua exibida no terceiro passo;
    \item Zona\_de\_Decisão: Definida, Revisar ou, quando a recusa está
          desligada, Limítrofe, para os casos a menos de dez pontos percentuais
          do limiar de operação;
    \item Perfil: Típico ou Atípico; Atípico indica que o paciente se afasta da
          população de treino, situação em que a predição merece cautela, e não
          que o tumor seja maligno.
\end{alineas}

No modo Todos (Comparação), essas colunas são substituídas por uma coluna por
modelo, com o diagnóstico que cada um daria ao mesmo paciente.

\section*{B.5 Cuidados de uso}

O DiagnosisXAI é uma ferramenta de apoio e não substitui o diagnóstico do
profissional de saúde. O sistema não processa imagens: opera apenas sobre os
trinta atributos já extraídos pelo laboratório, obtidos pelo mesmo procedimento
da base Wisconsin. Os casos devolvidos para revisão e os pacientes de perfil
atípico devem ser examinados com atenção redobrada.
```

> Os dados dos manuais vêm do próprio TCC (Seções 4.3 e 4.8) e do repositório DiagnosisXAI: README, `predict_view.py` (a opção inicial é "Todos (Comparação)") e os CSVs de exemplo (o gabarito usa 0/1 na coluna `diagnosis`).

**(c) Remissão aos apêndices no Cap. 4** (fim da Subseção 4.8.6, Distribuição, linha 2451)

**Arquivo:** `trabalho.tex`

**Procure:**
```latex
pasta do programa pode ser somente leitura.
```

**Substitua por:**
```latex
pasta do programa pode ser somente leitura. As instruções de instalação e de uso
estão nos Apêndices~A e~B.
```

---

### 1.3 Objetivos coerentes com a implementação: UMAP × Mahalanobis e verbos no futuro (pp. 18–19)

> **E-mail:** "Harmonize os objetivos apresentados na introdução com a implementação: o texto atribui ao UMAP a identificação de anomalias (pp. 18–19), mas a solução e a conclusão atribuem essa função à distância de Mahalanobis (pp. 89 e 100). Explique essa mudança e retire os verbos no futuro referentes ao que já foi feito."

**Arquivo:** `trabalho.tex`

**(a) p. 18 (linha 197): o UMAP deixa de identificar anomalias**

**Procure:**
```latex
identificando agrupamentos (\textit{clusters}) e anomalias de forma gráfica.
```

**Substitua por:**
```latex
identificando agrupamentos (\textit{clusters}) de forma gráfica.
```

**(b) p. 19 (linha 203): "engloba" → "englobou"**

**Procure:**
```latex
Para alcançar esse propósito, o projeto engloba o treinamento
```

**Substitua por:**
```latex
Para alcançar esse propósito, o projeto englobou o treinamento
```

**(c) p. 19 (linha 203): explicar a mudança do UMAP para a distância de Mahalanobis**

A explicação se apoia no que já está na Seção 4.8.4 ("nenhum ponto cai fora da nuvem do treino").

**Procure:**
```latex
facilitando a identificação de agrupamentos (\textit{clusters}) e anomalias (\textit{outliers}) biológicas.
```

**Substitua por:**
```latex
facilitando a identificação de agrupamentos (\textit{clusters}). A identificação de anomalias (\textit{outliers}), inicialmente atribuída ao UMAP, passou à distância de Mahalanobis, calculada no espaço completo dos trinta atributos, pois a projeção posiciona cada paciente novo a partir de seus vizinhos de treino e, por isso, não o coloca fora da nuvem conhecida, mesmo quando ele é atípico.
```

**(d) p. 19 (linha 203): "integrará" → "integrou"**

**Procure:**
```latex
o sistema integrará a biblioteca SHAP
```

**Substitua por:**
```latex
o sistema integrou a biblioteca SHAP
```

**(e) p. 19 (linha 203): "contempla" → "contemplou", e formatos que o software realmente exporta**

O software exporta PDF e CSV, não Excel.

**Procure:**
```latex
o trabalho contempla a criação de uma interface capaz de receber dados em lote via upload de planilhas, automatizando a geração de relatórios de saída estruturados (como PDF, Excel ou CSV)
```

**Substitua por:**
```latex
o trabalho contemplou a criação de uma interface capaz de receber dados em lote via upload de planilhas, automatizando a geração de relatórios de saída estruturados (PDF e CSV)
```

**(f) Outros verbos no futuro**

Linha 256 (fim da Seção 2.2):

**Procure:**
```latex
a construção do agente racional será fundamentada
```

**Substitua por:**
```latex
a construção do agente racional é fundamentada
```

Linha 603 (Seção 3.1):

**Procure:**
```latex
variáveis que serão processadas pelos modelos de SHAP e UMAP.
```

**Substitua por:**
```latex
variáveis que foram processadas pelos modelos de SHAP e UMAP.
```

Linhas 1176–1177 (Seção 4.5.3). A frase promete projeções UMAP e PCA que não aparecem no texto; basta encerrá-la antes.

**Procure:**
```latex
um indicativo qualitativo da separabilidade entre as classes que será
explorada formalmente nas projeções UMAP e PCA.
```

**Substitua por:**
```latex
um indicativo qualitativo da separabilidade entre as classes.
```

---

## 2. Coerência e fechamento

### 2.1 Conclusão: dificuldades enfrentadas e como foram superadas (pp. 99–101)

> **E-mail:** "Na conclusão (pp. 99–101), explicite as dificuldades enfrentadas durante o desenvolvimento e como foram superadas. Retome, por exemplo, as inconsistências entre a decisão exibida e a decisão dos classificadores, citadas nas pp. 85–87, e os ajustes necessários à calibração e ao empacotamento. Limitações da base e trabalhos futuros não substituem esse relato."

**Arquivo:** `trabalho.tex` — Capítulo 5 (linha 2547)

Um parágrafo novo entra **antes** do parágrafo de limitações: primeiro o que foi superado, depois o que permanece. Ele só retoma o que já está no corpo do texto (regra do orientador de não trazer dado novo):

- a inconsistência no SVM e no KNN, na Subseção 4.8.1;
- a escolha de Platt e o calibrador sobre a função de decisão do SVM, na Subseção 4.7.3;
- o empacotamento, na Subseção 4.8.6 e na Seção 4.3.

**Procure:**
```latex
Essas conclusões têm limites. A base Wisconsin reúne apenas 569 amostras de uma
```

**Substitua por:**
```latex
Durante o desenvolvimento, três dificuldades exigiram ajustes: a decisão exibida
na interface divergia da decisão real do SVM e do KNN, o que foi corrigido e
passou a ser verificado por testes automatizados; a regressão isotônica, apesar
do melhor escore de Brier, tende a se sobreajustar em amostras pequenas, e por
isso foi adotado o escalonamento de Platt, que no SVM atua sobre a função de
decisão; e, como o PyInstaller só gera o executável para o sistema em que roda e
inclui apenas o que enxerga nas importações, o empacotamento passou a ser feito
em máquinas Windows e Linux, com as versões exatas das dependências e um
autoteste antes de cada distribuição.

Essas conclusões têm limites. A base Wisconsin reúne apenas 569 amostras de uma
```

> Na compilação de teste com o plano inteiro aplicado, a conclusão continuou com 3 páginas (pp. 98–100, a última cerca de 70% ocupada), como hoje, dentro da regra do orientador. Se você aumentar o parágrafo novo, confira no sumário se as Referências continuam começando 3 páginas depois do início da conclusão.

### 2.2 Afirmações absolutas da fundamentação (pp. 27, 40 e 37)

> **E-mail:** "Revise as afirmações absolutas da fundamentação: 'comprova a verdadeira eficácia [...] na prática médica' (p. 27), 'seguro e incontestável' (p. 40) e a associação automática entre maior complexidade e maior acurácia (p. 37) entram em conflito com as limitações e os resultados das pp. 77–81 e 101. Restrinja as conclusões às evidências efetivamente apresentadas."

**Arquivo:** `trabalho.tex`

**(a) p. 27, "comprova a verdadeira eficácia [...] na prática médica"** (linha 281)

**Procure:**
```latex
é o indicador soberano que comprova a verdadeira eficácia do sistema em acertar diagnósticos na prática médica
```

**Substitua por:**
```latex
é a principal estimativa da capacidade do sistema de acertar diagnósticos em dados novos, sem substituir a validação em outras bases nem na prática médica
```

**(b) p. 40, "seguro e incontestável"** (linha 494, última frase do parágrafo)

**Procure:**
```latex
Essa garantia de exatidão torna o método estatisticamente seguro e incontestável para auditar diagnósticos críticos na área da saúde
```

**Substitua por:**
```latex
Essa propriedade torna o método adequado para auditar diagnósticos críticos na área da saúde, embora a decomposição seja aproximada quando os valores são estimados por amostragem, como no \textit{KernelExplainer}
```

**(c) p. 37, complexidade associada automaticamente à acurácia**

Os resultados mostram que a Regressão Logística igualou os modelos complexos (Seções 4.6.6 e 4.7). São três frases com a mesma associação.

Linha 475 (fim da Subseção 2.3.4):

**Procure:**
```latex
o modelo ganha acurácia estatística, mas perde drasticamente a sua interpretabilidade
```

**Substitua por:**
```latex
o modelo pode ganhar acurácia estatística, ganho que depende dos dados e nem sempre se confirma, mas perde drasticamente a sua interpretabilidade
```

Linha 479 (início da Seção 2.4):

**Procure:**
```latex
alcançam taxas de acerto notáveis na classificação de tumores. Contudo, essa elevada acurácia estatística impôs
```

**Substitua por:**
```latex
podem alcançar taxas de acerto notáveis na classificação de tumores. Contudo, essa complexidade impôs
```

Linha 483 (Seção 2.4):

**Procure:**
```latex
embora frequentemente apresentem limitações de desempenho
```

**Substitua por:**
```latex
embora possam apresentar limitações de desempenho
```

### 2.3 Contagem de colunas (pp. 56–57)

> **E-mail:** "Nas pp. 56–57, corrija a contagem de colunas: se o arquivo bruto tem id, diagnosis, 30 atributos e Unnamed: 32, são 33 colunas antes das duas exclusões, e não 32."

**Arquivo:** `trabalho.tex` — linhas 898–902 (Seção 4.3)

Conferi o `data/data.csv` do repositório: a linha de cabeçalho termina com uma vírgula a mais, e é isso que faz o pandas criar a coluna `Unnamed: 32`. São duas trocas: o número de colunas e a inclusão da `Unnamed: 32` na lista.

**Procure:**
```latex
por 569 amostras e 32 colunas em sua forma bruta: um
identificador numérico único (id), a variável alvo (diagnosis) e trinta atributos
```

**Substitua por:**
```latex
por 569 amostras e 33 colunas em sua forma bruta: um
identificador numérico único (id), a variável alvo (diagnosis), trinta atributos
```

**Procure:**
```latex
via Punção Aspirativa por Agulha Fina, conforme descrito por
\citeonline{Street1993}.
```

**Substitua por:**
```latex
via Punção Aspirativa por Agulha Fina, conforme descrito por
\citeonline{Street1993}, e uma coluna vazia, Unnamed: 32.
```

> A conta fecha: 33 − 2 = 31 colunas (alvo + 30 atributos), como o texto já diz logo depois. A referência da base, que o e-mail pede mais adiante, entra no início deste mesmo parágrafo (item 4.3).

### 2.4 Figura 9 e Gráfico 1 cortando o texto (pp. 62–63)

> **E-mail:** "Na página 62-63: a figura 9 e o gráfico 1 cortaram o texto que termina na página 61 e retoma na 63, precisa arrumar isso."

**Arquivo:** `trabalho.tex` — linhas 1140 e 1158

O corte vem da opção `p` em `[htbp]`, que permite ao LaTeX montar uma página só com figuras: foi o que ele fez na p. 62, com o Gráfico 1 e a Figura 9 juntos. Trocando `[htbp]` por `[!htb]`, essa página deixa de ser possível. Cada figura passa a ficar no ponto do texto ou no topo da página seguinte, com o texto continuando normalmente em volta. Os tamanhos das figuras não mudam.

**Gráfico 1** (linha 1140)

**Procure:**
```latex
\begin{grafico}[htbp]
    \centering
    \caption{DISTRIBUIÇÃO DAS CLASSES NA BASE WISCONSIN}
```

**Substitua por:**
```latex
\begin{grafico}[!htb]
    \centering
    \caption{DISTRIBUIÇÃO DAS CLASSES NA BASE WISCONSIN}
```

**Figura 9** (linha 1158)

**Procure:**
```latex
\begin{figure}[htbp]
    \centering
    \caption{HISTOGRAMAS DOS TRINTA ATRIBUTOS MORFOLÓGICOS DA BASE WISCONSIN}
```

**Substitua por:**
```latex
\begin{figure}[!htb]
    \centering
    \caption{HISTOGRAMAS DOS TRINTA ATRIBUTOS MORFOLÓGICOS DA BASE WISCONSIN}
```

> Na compilação de teste com o plano inteiro aplicado, a p. 61 tem só texto (da Subseção 4.5.1 ao início da 4.5.3). O Gráfico 1 abre a p. 62 e a Figura 9 abre a p. 63, cada um seguido de texto. Nenhuma página fica só com figuras e nenhuma sobra em branco, e o Gráfico 1 passa a vir antes da Figura 9, na ordem em que são citados. Como `[!htb]` não permite página só de figuras, isso continua valendo mesmo que outras edições mudem as quebras de página.

### 2.5 Tabelas que vazam a margem direita (pp. 77 e 83)

> **E-mail:** "As tabelas na página 77 e na 83: vazou a margem direita, reduza um pouco o tamanho da letra dentro da tabela e faça caber dentro das margens."

**Arquivo:** `trabalho.tex`

O `trabalho.log` atual registra os dois estouros: a Tabela 2 passa 30 pt (cerca de 1,1 cm) da margem, e a Tabela 7 passa 41 pt (cerca de 1,5 cm). As alterações abaixo eliminam ambos.

**(a) Tabela 2 (p. 77), validação cruzada** (linha 1769): acrescentar `\small`

**Procure:**
```latex
    \label{tab:validacao_cruzada}
    \setlength{\tabcolsep}{3pt}
```

**Substitua por:**
```latex
    \label{tab:validacao_cruzada}
    \small
    \setlength{\tabcolsep}{3pt}
```

**(b) Tabela 7 (p. 83), ponto de operação** (linhas 2051–2052): de `\small` para `\footnotesize` e espaçamento entre colunas de 3 pt para 2 pt

**Procure:**
```latex
    \label{tab:ponto_operacao}
    \small
    \setlength{\tabcolsep}{3pt}
```

**Substitua por:**
```latex
    \label{tab:ponto_operacao}
    \footnotesize
    \setlength{\tabcolsep}{2pt}
```

> O `\small` e o `\footnotesize` ficam **depois** do `\caption`, então reduzem só o corpo da tabela, e não o título.

### 2.6 Teste de Friedman: blocos, dependência e divergência com o 5×2cv (pp. 79–81)

> **E-mail:** "Nas pp. 79–81, identifique quais unidades foram usadas como blocos no teste de Friedman e justifique o tratamento da dependência entre as avaliações. Explique por que o teste pareado não encontrou diferença para a Árvore de Decisão, enquanto o pós-hoc encontrou, antes de apresentar sua inferioridade como conclusão definitiva."

**Arquivo:** `trabalho.tex` — Subseção 4.7.2 e Capítulo 5

Conferi no `notebooks/Wisconsin.ipynb` (Seções 10.1 e 10.2 do notebook):

- **blocos do Friedman** = as **50 dobras** da validação cruzada 10×5, feita **sobre o conjunto de treino**, com a mesma semente para todos os modelos;
- a métrica comparada é a **acurácia** por dobra.

**Por que os testes divergem.** O Friedman foi proposto por Demšar para **vários conjuntos de dados**, que são blocos independentes. Aqui, as dobras de uma mesma repetição compartilham 8/9 ≈ 89% do treino, o que faz o teste produzir valores de *p* pequenos demais. O 5×2cv corrige essa dependência.

**(a) Identificar os blocos** (linha 1871): uma frase nova no parágrafo do Friedman

**Procure:**
```latex
de comparações pareadas repetidas. O Friedman rejeitou a hipótese nula de
```

**Substitua por:**
```latex
de comparações pareadas repetidas. Os blocos do teste foram as 50 dobras da
validação cruzada da Subseção~\ref{subsec:validacao-cruzada}, realizada sobre o
conjunto de treino: como a semente aleatória foi fixada, os cinco modelos foram
avaliados sobre as mesmas amostras em cada dobra, e o teste compara os postos
médios de suas acurácias. O Friedman rejeitou a hipótese nula de
```

**(b) Não apresentar a inferioridade como definitiva antes da explicação** (linhas 1896–1899)

**Procure:**
```latex
A leitura da Tabela~\ref{tab:nemenyi} é inequívoca e constitui o principal
achado desta seção. A Árvore de Decisão difere significativamente de todos os
demais classificadores, com valores de $p$ entre 0,0000 e 0,0004, sua
inferioridade como \textit{baseline} é estatisticamente sustentada. Entre os
```

**Substitua por:**
```latex
A leitura da Tabela~\ref{tab:nemenyi} constitui o principal achado desta seção.
A Árvore de Decisão difere significativamente de todos os demais
classificadores, com valores de $p$ entre 0,0000 e 0,0004, resultado que
contrasta com o do teste 5$\times$2cv e é discutido a seguir. Entre os
```

**(c) Explicar a divergência e justificar o tratamento da dependência:** parágrafo novo logo após esse (linha 1902)

**Procure:**
```latex
Forest, e o maior chega a 0,9834, entre Regressão Logística e SVM.
```

**Substitua por:**
```latex
Forest, e o maior chega a 0,9834, entre Regressão Logística e SVM.

A divergência entre os dois testes quanto à Árvore de Decisão decorre do
tratamento da dependência entre as avaliações. \citeauthoronline{Demsar2006}
(\citeyear{Demsar2006}) propõe o Friedman para comparar classificadores sobre
vários conjuntos de dados, que são blocos independentes. Aqui, as 50 dobras vêm
de um único conjunto, e os treinos de duas dobras da mesma repetição
compartilham cerca de 89\% das amostras; tratadas como independentes, essas
avaliações levam o teste a produzir valores de $p$ menores do que os reais. O
5$\times$2cv, ao contrário, corrige essa dependência e é, por isso,
conservador. A inferioridade da Árvore de Decisão é, portanto, um indício
consistente, pois ela tem o pior desempenho médio em todas as métricas da
Tabela~\ref{tab:validacao_cruzada} e o 5$\times$2cv aponta na mesma direção
($t = +2{,}346$; $p = 0{,}0659$), mas não uma conclusão definitiva.
```

**(d) Mesmo ajuste na conclusão** (Capítulo 5, linhas 2491–2493)

**Procure:**
```latex
distingue do ruído amostral; apenas a inferioridade da Árvore de Decisão tem
respaldo estatístico.
```

**Substitua por:**
```latex
distingue do ruído amostral; a inferioridade da Árvore de Decisão é um indício
consistente, mas não definitivo.
```

> A correção de "a conhecida conservadorismo", que fica no mesmo trecho, está no item 3.4.

### 2.7 Faixa de recusa: falso negativo no treino, limites da faixa e "um terço" (pp. 83–85)

> **E-mail:** "Nas pp. 83–85, harmonize a descrição de que a faixa foi definida para não haver erro no treino com os falsos negativos ainda registrados na Tabela 7. Esclareça a inclusão dos limites da faixa. Na p. 84, 'cerca de um terço' deve ser identificado como resultado do teste; a cobertura de 50% a 65% no treino implica devolução de aproximadamente 35% a 50%."

**Arquivo:** `trabalho.tex` — Subseção 4.7.4 e Capítulo 5

**Diagnóstico (verificado).** Recalculei as probabilidades *out-of-fold* do treino numa cópia do repositório DiagnosisXAI (mesmo procedimento do `calibrar_limiares.py`) e comparei duas versões da faixa:

| Modelo | Faixa **exata** | Faixa **gravada** no `limiares.json` |
|---|---|---|
| Regressão Logística | [0,00297; 0,66985[ → 59,9% de cobertura, **0 FN** | [0,0030; 0,6698[ → **60,1%, 1 FN** |
| SVM | [0,00417; 0,72979[ → 64,8% de cobertura, **0 FN** | [0,0042; 0,7298[ → **65,3%, 1 FN** |

Os números da coluna "gravada" são **exatamente** os da Tabela 7. A faixa construída zera os erros no treino; o falso negativo aparece porque o limite inferior foi gravado com 4 casas e arredondado **para cima** (0,00297 → 0,0030), deixando abaixo dele o maligno que o define. Pela regra do `decision.py` (**Benigno se certeza < inferior; Maligno se certeza ≥ superior; senão, Revisar**), o limite inferior pertence à faixa e o superior não.

Há dois caminhos possíveis:

- **Opção A (só texto, recomendada pelo prazo):** manter os números e explicar a origem do falso negativo, com os blocos abaixo.
- **Opção B (corrigir o código):** no `calibrar_limiares.py`, gravar o limite inferior arredondado **para baixo** (por exemplo, `math.floor(inferior * 1e4) / 1e4`). Depois, rodar o script de novo, refazer a Tabela 7 e o Gráfico 7 e regenerar o executável. Nesse caso, no bloco (b), não acrescente a frase sobre o arredondamento ("O falso negativo restante ... não há erro no treino.").

**(a) Esclarecer a inclusão dos limites** (linhas 2025–2026)

**Procure:**
```latex
dentro dela são devolvidos para revisão humana. A faixa só é adotada se o modelo
```

**Substitua por:**
```latex
dentro dela são devolvidos para revisão humana. O limite inferior pertence à
faixa, e o superior, posicionado um décimo de milésimo acima da maior certeza de
um benigno, não: certeza abaixo do limite inferior leva a Benigno, e certeza
igual ou superior ao limite superior, a Maligno. A faixa só é adotada se o modelo
```

**(b) Harmonizar com o falso negativo da Tabela 7 e corrigir a proporção do treino** (linhas 2082–2084)

**Procure:**
```latex
contra três a cinco se decidissem todos os casos. O preço é explícito: cerca de
um terço do lote volta para revisão humana.
```

**Substitua por:**
```latex
contra três a cinco se decidissem todos os casos. O falso negativo restante não
contradiz a construção da faixa: os limites são gravados no arquivo
limiares.json com quatro casas decimais, e, na Regressão Logística, no SVM e no
comitê, o arredondamento elevou o limite inferior acima da certeza do maligno
que o define (de 0,00297 para 0,0030, na Regressão Logística), que passou a ser
decidido como Benigno; com os limites exatos, não há erro no treino. O preço é
explícito: no treino, entre 35\% e 50\% dos casos voltam para revisão humana.
```

**(c) "Cerca de um terço" como resultado do teste** (linha 2091)

Cobertura no teste: 67,1% a 74,1%, isto é, devolução de 25,9% a 32,9%.

**Procure:**
```latex
74\% do lote sem nenhum erro.
```

**Substitua por:**
```latex
74\% do lote sem nenhum erro e devolvem para revisão humana entre 26\% e 33\%
dos pacientes, cerca de um terço do lote de teste.
```

**(d) Mesmo ajuste na conclusão** (Capítulo 5, linhas 2503–2504)

**Procure:**
```latex
cerca de um
terço do lote volta para revisão humana.
```

**Substitua por:**
```latex
cerca de um
terço do lote de teste volta para revisão humana.
```

> A Subseção 4.8.7 (Limitações) já diz "no conjunto de teste, cerca de um terço do lote volta para revisão humana" e está correta.

---

## 3. Revisão linguística

**Arquivo:** `trabalho.tex`

### 3.1 p. 18, `"abrir"essa`, e p. 34, `"K"vizinhos` e "mais idênticas"

> **E-mail:** "P. 18: insira espaço em '"abrir"essa'. P. 34: faça o mesmo em '"K"vizinhos' e substitua 'mais idênticas' por 'mais semelhantes'."

Com o `babel` em português, as aspas retas "engolem" o espaço seguinte; o resto do texto já usa `"palavra"\ ` para evitar isso.

**p. 18** (linha 197)

**Procure:**
```latex
permite "abrir" essa caixa preta
```

**Substitua por:**
```latex
permite "abrir"\ essa caixa preta
```

**p. 34** (linha 431)

**Procure:**
```latex
identifica os "K" vizinhos mais próximos, ou seja, os exames históricos que possuem as medidas anatômicas mais idênticas ao caso atual.
```

**Substitua por:**
```latex
identifica os "K"\ vizinhos mais próximos, ou seja, os exames históricos que possuem as medidas anatômicas mais semelhantes ao caso atual.
```

### 3.2 p. 24, orações sem pontuação (linha 261)

> **E-mail:** "P. 24: separe por ponto ou ponto e vírgula as orações de 'não segue uma receita universal, a abordagem escolhida...'."

**Procure:**
```latex
não segue uma receita universal, a abordagem escolhida depende
```

**Substitua por:**
```latex
não segue uma receita universal. A abordagem escolhida depende
```

### 3.3 p. 62, "que sempre predisse benigno" (linha 1135)

> **E-mail:** "P. 62: substitua 'que sempre predisse benigno atingiria' por 'que sempre predissesse a classe benigna atingiria'."

**Procure:**
```latex
trivial que sempre predisse benigno atingiria
```

**Substitua por:**
```latex
trivial que sempre predissesse a classe benigna atingiria
```

### 3.4 p. 80, "a conhecida conservadorismo" (linha 1863)

> **E-mail:** "P. 80: corrija 'a conhecida conservadorismo' para 'o conhecido conservadorismo'."

**Procure:**
```latex
ilustra a conhecida conservadorismo do teste
```

**Substitua por:**
```latex
ilustra o conhecido conservadorismo do teste
```

### 3.5 p. 88, "no qual a tela abre" (linha 2204)

> **E-mail:** "P. 88: esclareça a construção 'no qual a tela abre', indicando que o modo de comparação é a opção inicial da interface, se esse for o sentido."

É esse o sentido. Conferi no código (`app/views/predict_view.py`): "Todos (Comparação)" é o primeiro item da lista do seletor de modelos e, por isso, a opção selecionada quando a tela abre.

**Procure:**
```latex
simultânea, no qual a tela abre, e processa o lote;
```

**Substitua por:**
```latex
simultânea, que é a opção selecionada quando a tela é aberta, e processa o lote;
```

---

## 4. Citações e referências

### 4.1 "Russel; Norvig, 2010" → "Russell" (p. 22)

> **E-mail:** "Corrija 'Russel; Norvig, 2010' (p. 22) para a grafia 'Russell', utilizada nas referências."

**Arquivo:** `trabalho.tex` — linha 240

**Procure:**
```latex
(Russel; Norvig, 2010)
```

**Substitua por:**
```latex
(Russell; Norvig, 2010)
```

### 4.2 Figura 6: autoria "AI Online Course" × endereço da Coursera (p. 33)

> **E-mail:** "Na Figura 6 (p. 33), resolva a divergência entre a autoria 'AI Online Course' e o endereço da Coursera. A referência da p. 102 aponta para outro site. Identifique a fonte efetivamente utilizada e faça coincidir legenda e referência."

**Arquivo:** `trabalho.tex` — linha 412

A referência `AIOnlineCourse2023` aponta para `aionlinecourse.com`. Verifiquei a página: ela tem uma imagem de mapeamento para dimensão superior (`11_21_kernel_svm_3.png`), que provavelmente é a sua `hyperplane.png`.

⚠️ Abra <https://www.aionlinecourse.com/tutorial/machine-learning/kernel-svm> e confira se a imagem é a mesma.

**Se for a mesma (Alternativa A, provável):** troque só o endereço da legenda pelo da referência.

**Procure:**
```latex
\url{https://www.coursera.org/learn/machine-learning/lecture/2s9nP/support-vector-machines}
```

**Substitua por:**
```latex
\url{https://www.aionlinecourse.com/tutorial/machine-learning/kernel-svm}
```

**Alternativa B — se a imagem veio mesmo da Coursera:** crie uma entrada nova no `.bib` e troque, na legenda, a chave `AIOnlineCourse2023` por `NgCoursera`. Mantenha `AIOnlineCourse2023` no `.bib`, porque ela continua citada no texto, na linha 390.

```latex
@misc{NgCoursera,
  author = {Ng, Andrew},
  title = {Support Vector Machines},
  howpublished = {Coursera},
  note = {Videoaula do curso Machine Learning},
  year = {ANO},
  url = {https://www.coursera.org/learn/machine-learning/lecture/2s9nP/support-vector-machines},
  urlaccessdate = {DD mmm. 2026}
}
```

### 4.3 Referência específica da base de dados (p. 56)

> **E-mail:** "Na p. 56, acrescente a referência específica da base de dados e sua versão/local de obtenção; o artigo de Street et al. não substitui a identificação do arquivo utilizado."

O formato do `data.csv` (cabeçalho com uma vírgula a mais e a coluna `Unnamed: 32`) é o da redistribuição do Kaggle (`uciml/breast-cancer-wisconsin-data`); o arquivo original do UCI (`wdbc.data`) nem tem cabeçalho. Por isso, o texto passa a citar o UCI como origem da base e o Kaggle como local de obtenção do arquivo.

⚠️ Confirme de onde você baixou o `data.csv`. Se não foi do Kaggle, ajuste o trecho "obtido na cópia publicada no Kaggle" e a entrada `KaggleWDBC2016`.

**(a) Citar a base e o arquivo no texto** (início da Seção 4.3, linhas 897–898)

**Arquivo:** `trabalho.tex`

**Procure:**
```latex
Repository e referenciada ao longo deste trabalho como base Wisconsin. O arquivo
data.csv é composto
```

**Substitua por:**
```latex
Repository (\citeauthoronline{WolbergUCI1993}, \citeyear{WolbergUCI1993}) e
referenciada ao longo deste trabalho como base Wisconsin. O arquivo
data.csv, obtido na cópia publicada no Kaggle
(\citeauthoronline{KaggleWDBC2016}, \citeyear{KaggleWDBC2016}), é composto
```

**(b) Entradas novas** (inserir após a entrada `Street1993`)

**Arquivo:** `referencias.bib`

A do UCI segue a citação oficial do repositório (autores, ano de 1993 e DOI 10.24432/C5DW2B, conferidos na página do UCI).

⚠️ Na do Kaggle, confira na página do dataset a **versão** e o **ano** e preencha a **data de acesso** real das duas.

**Procure:**
```latex
  organization = {International Society for Optics and Photonics},
  publisher = {SPIE}
}
```

**Substitua por:**
```latex
  organization = {International Society for Optics and Photonics},
  publisher = {SPIE}
}

@misc{WolbergUCI1993,
  author = {Wolberg, William and Mangasarian, Olvi and Street, Nick and Street, W.},
  title = {Breast Cancer Wisconsin (Diagnostic)},
  howpublished = {UCI Machine Learning Repository},
  note = {Conjunto de dados. DOI: 10.24432/C5DW2B},
  year = {1993},
  url = {https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic},
  urlaccessdate = {06 nov. 2026}
}

@misc{KaggleWDBC2016,
  author = {{UCI Machine Learning}},
  title = {Breast Cancer Wisconsin (Diagnostic) Data Set},
  howpublished = {Kaggle},
  note = {Conjunto de dados, versão 2. Arquivo data.csv},
  year = {2016},
  url = {https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data},
  urlaccessdate = {06 nov. 2026}
}
```

### 4.4 IBM, "SCHüTZE", Faceli, Manning e INCA (pp. 102–103)

> **E-mail:** "Complete a data de acesso da referência IBM (p. 103), normalize 'SCHüTZE' e confira a compatibilidade entre ano e edição das entradas de Faceli et al. e Manning et al. (pp. 102–103). Na entrada INCA (2026), faça o título corresponder ao documento efetivamente consultado, pois o endereço remete a uma notícia sobre estimativas nacionais."

**Arquivo:** `referencias.bib`

**(a) IBM sem data de acesso** (entrada `ibm_random_forest_2026`)

⚠️ Use a data real em que você consultou a página. As outras páginas da IBM foram acessadas em 31 mai. 2026, o que é provável também para esta.

**Procure:**
```latex
  url          = {https://www.ibm.com/br-pt/think/topics/random-forest}
}
```

**Substitua por:**
```latex
  url          = {https://www.ibm.com/br-pt/think/topics/random-forest},
  urlaccessdate = {31 mai. 2026}
}
```

**(b) "SCHüTZE" → "SCHÜTZE"** (entrada `Manning2006`). O acento precisa estar entre chaves, `{\"u}`, para o BibTeX convertê-lo em maiúscula.

**Procure:**
```latex
Sch\"{u}tze, Hinrich}
```

**Substitua por:**
```latex
Sch{\"u}tze, Hinrich}
```

**(c) Faceli et al.: ano × edição** (entrada `Faceli2011`)

A 1.ª edição é de **2011** (LTC); a 2.ª edição é de **2021** e tem um quinto autor, Tiago A. Almeida. Hoje a entrada mistura "2nd" com 2011.

⚠️ Confira qual livro você leu.

**Se foi a edição de 2011 (1.ª), basta tirar a edição:**

**Procure:**
```latex
  year = {2011},
  edition = {2nd}
```

**Substitua por:**
```latex
  year = {2011}
```

**Alternativa B — se foi a 2.ª edição (2021):** troque também os autores e o ano. As citações no texto mudam sozinhas para 2021, porque usam `\citeyear`.

```latex
  author = {Faceli, Katti and Lorena, Ana Carolina and Gama, Jo{\~a}o and Almeida, Tiago Agostinho de and Carvalho, Andr{\'e} C. P. de L. F. de},
  ...
  year = {2021},
  edition = {2}
```

**(d) Manning et al.: ano** (entrada `Manning2006`)

*Introduction to Information Retrieval* foi publicado em **2008**, 1.ª edição; não existe edição de 2006. A chave `Manning2006` pode continuar, pois é invisível no PDF.

**Procure:**
```latex
  title = {Introduction to Information Retrieval},
  year = {2006},
```

**Substitua por:**
```latex
  title = {Introduction to Information Retrieval},
  year = {2008},
```

**(e) INCA (2026): título da notícia efetivamente consultada** (entrada `Inca-781`)

O endereço é a notícia de 4 fev. 2026 sobre a Estimativa 2026–2028.

⚠️ Abra o link e copie o título exatamente como aparece; o do bloco abaixo segue o endereço da página.

**Procure:**
```latex
  title     = {Câncer de Mama},
```

**Substitua por:**
```latex
  title     = {INCA estima 781 mil novos casos de câncer por ano no Brasil entre 2026 e 2028},
```

### 4.5 Uniformizar as fontes de figuras e quadros (pp. 29, 30, 43 e 44)

> **E-mail:** "Uniformize as chamadas das fontes de figuras e quadros, que alternam nomes em caixa alta e iniciais maiúsculas (por exemplo, pp. 29, 30, 43 e 44)."

**Arquivo:** `trabalho.tex`

As fontes das pp. 29, 30, 43 e 44 usam `\cite{X}`, que gera o autor em **caixa alta** ("(DAVIS; GOADRICH, 2006)"). As demais fontes externas (Figuras 1, 2 e 6) usam `\citeauthoronline{X}, \citeyear{X}`, com iniciais maiúsculas ("INCA, 2022c"). A correção mínima é passar as quatro do primeiro grupo para o formato do segundo. Há ainda "O Autor" (`\fonte{O Autor}`) alternando com "O autor" (`\fonteautor`), que também é diferença de maiúsculas.

**(a) Figura 4 (p. 29)** (linha 349)

**Procure:**
```latex
\fonte{Adaptado de \cite{Davis2006}}
```

**Substitua por:**
```latex
\fonte{Adaptado de \citeauthoronline{Davis2006}, \citeyear{Davis2006}}
```

**(b) Figura 5 (p. 30)** (linha 367)

**Procure:**
```latex
\fonte{Adaptado de \cite{Faceli2011}}
```

**Substitua por:**
```latex
\fonte{Adaptado de \citeauthoronline{Faceli2011}, \citeyear{Faceli2011}}
```

**(c) Quadro 1 e Figura 7 (pp. 43 e 44)** (linhas 546 e 580): duas ocorrências, substitua **as duas**

**Procure (todas as ocorrências):**
```latex
\fonte{Adaptado de \cite{Bollon2022}}
```

**Substitua por:**
```latex
\fonte{Adaptado de \citeauthoronline{Bollon2022}, \citeyear{Bollon2022}}
```

**(d) "O Autor" × "O autor"**: no VS Code, use "Substituir tudo" (Ctrl+H) **só no `trabalho.tex`**; são 20 ocorrências

**Procure (todas as ocorrências):**
```latex
\fonte{O Autor}
```

**Substitua por:**
```latex
\fonteautor
```

**(e) Tabela 1** (linha 1680), que usa outro formato de fonte

**Procure:**
```latex
    \legend{Fonte: O Autor}
```

**Substitua por:**
```latex
    \fonteautor
```

---

## Pendências que só você pode confirmar

| # | O que confirmar | Onde está no plano |
|---|---|---|
| 1 | Nome do executável e do `.zip` no Release, aviso do Windows e permissão no Linux (`% CONFIRMAR` no apêndice) | 1.2(b) |
| 2 | Opção A (só texto) ou B (corrigir o arredondamento no código) para a faixa de recusa | 2.7 |
| 3 | Se a `hyperplane.png` é a imagem da página do AI Online Course | 4.2 |
| 4 | De onde baixou o `data.csv` (o formato indica o Kaggle), a versão e as datas de acesso | 4.3 |
| 5 | Data de acesso da página da IBM sobre *random forest* | 4.4(a) |
| 6 | Qual edição de Faceli et al. você leu (2011 ou 2021) | 4.4(c) |
| 7 | Título exato da notícia do INCA | 4.4(e) |

## Checklist final antes da entrega (14/11)

> **E-mail:** "[...] no dia 14/11 temos a entrega para a banca, ou seja, trabalho pronto. [...] Postar o texto monográfico [...]. Também, postar o programa implementado (se necessário, incluir o(s) programa(s) instalador(es)). Os trabalhos devem estar formatados de acordo com as normas da ABNT/UTP."

- [ ] Compilar com `make` (pdflatex → bibtex → pdflatex → pdflatex) e conferir se não aparece `??` no lugar de referências cruzadas, como Apêndice, Capítulo e Subseção.
- [ ] Procurar `Overfull \hbox` no `trabalho.log`: os das Tabelas 2 e 7 devem ter sumido.
- [ ] No sumário: aparecem "APÊNDICE A – MANUAL DE INSTALAÇÃO DO DIAGNOSISXAI" e "APÊNDICE B – MANUAL DE USO DO DIAGNOSISXAI" depois de "REFERÊNCIAS".
- [ ] Conclusão com no máximo 3 páginas (regra do orientador).
- [ ] Nas Referências: WOLBERG et al. (1993), UCI Machine Learning (2016), MANNING et al. (2008), "SCHÜTZE", IBM com "Acesso em", Faceli sem "2nd. ed." e INCA com o título da notícia.
- [ ] Pp. 61–63: o texto da Seção 4.5 não fica mais partido por uma página só de figuras, e o Gráfico 1 vem antes da Figura 9.
- [ ] Tabelas 2 e 7 dentro das margens.
- [ ] Entrega no OneDrive: o PDF do texto e o programa, isto é, os `.zip` do executável para Windows e Linux (Release do GitHub) e o link ou `.zip` do código-fonte, com o Apêndice A como guia de instalação.
- [ ] Commit no git com o `.tex`, o `.bib` e o PDF finais.
