# 1. O que ainda falta do e-mail da professora

Conferido em 08/11/2026 no `trabalho.tex` do último commit (`02ed0b2`) e no PDF compilado a partir dele (104 páginas). As páginas citadas são as **impressas no canto da página** da versão atual, e não as do PDF de outubro que a professora leu.

**Como usar este arquivo**

- A ordem é a do e-mail. Cada item diz o que já está resolvido e o que falta.
- Os blocos **Procure / Substitua por** seguem a regra de correção mínima: muda só o trecho apontado, e o resto da frase fica igual.
- Localize pelo texto (Ctrl+F no VS Code), não pelo número da linha. As linhas indicadas são as do arquivo atual, antes de qualquer edição.
- **Todos os blocos deste arquivo foram aplicados numa cópia do projeto e compilados** (pdflatex + bibtex + pdflatex ×2). Todos os trechos existem no `trabalho.tex` atual e o resultado compila sem erro.
- ⚠️ marca o que depende de uma informação que só você tem.

---

## Placar

| # | Item do e-mail | Situação |
|---|---|---|
| 1 | Resumo: "propõe", "resultados esperados", "garantida" | ⚠️ Parcial: as três trocas foram feitas, mas falta sintetizar os **resultados de desempenho** e as **limitações** |
| 2 | Roteiro dos capítulos | ⚠️ Parcial: o roteiro existe, mas não menciona os apêndices |
| 3 | Apêndices com os manuais de instalação e uso | ❌ **Falta**: o arquivo ainda termina nas referências |
| 4 | UMAP × Mahalanobis | ⚠️ Parcial: a explicação foi incluída (linha 208), mas a linha 202 ainda atribui "anomalias" ao UMAP |
| 5 | Verbos no futuro | ⚠️ Parcial: restam 4 trechos |
| 6 | Dificuldades na conclusão | ⚠️ Feito, mas **em dois parágrafos que se repetem**, e a conclusão passou do limite de 3 páginas (está com ~3,3) |
| 7 | Afirmações absolutas (pp. 27, 40, 37) | ⚠️ pp. 27 e 40 resolvidas; a da **p. 37 continua** (linha 487) |
| 8 | Contagem de colunas (33) | ✅ O número errado saiu (opcional: escrever "33") |
| 9 | Figura 9 e Gráfico 1 cortando o texto | ✅ Conferido no PDF: o texto corre sem cortes (pp. 61–63) |
| 10 | Tabelas das pp. 77 e 83 vazando a margem | ✅ Cabem. **Novo:** o Quadro 4 (p. 57) passa 7 pt da margem |
| 11 | Friedman: blocos, dependência, 5×2cv × Nemenyi | ⚠️ Blocos e dependência ok; a explicação vem **depois** de "é inequívoca", e a professora pediu antes |
| 12 | Faixa de recusa: erro zero × FN, inclusão dos limites, "um terço" | ⚠️ Falta dizer explicitamente se os limites estão dentro ou fora da faixa |
| 13 | Revisão linguística (pp. 18, 24, 34, 62, 80, 88) | ✅ Todas feitas |
| 14 | Russell, IBM, SCHÜTZE, Faceli/Manning, INCA | ✅ Todas feitas |
| 15 | Figura 6: legenda × referência | ✅ Coincidem (⚠️ confirme que a imagem saiu mesmo de aionlinecourse.com) |
| 16 | Referência da base de dados | ⚠️ Feita (UCI + DOI), mas o arquivo usado parece ser a versão do **Kaggle** |
| 17 | Fontes de figuras e quadros uniformes | ⚠️ Os nomes estão uniformes, mas há 21 "O Autor" e 19 "O autor" |
| 18 | Entrega de 14/11: texto + programa | ⚠️ O **Release v1.0 é anterior** ao retreino da Árvore de Decisão |

---

## 1. Resumo (p. 3) ⚠️

**Já feito:** "propõe" virou "desenvolveu", os "resultados esperados" saíram e a explicabilidade "garantida" virou "oferecida por valores de Shapley".

**Falta:** a professora pediu para *sintetizar os resultados efetivamente obtidos e suas limitações*. O resumo atual só traz o resultado da explicabilidade e uma limitação (não ter sido avaliado por profissionais). Faltam o resultado da comparação entre os modelos, o da faixa de recusa e as limitações da base. Os números vêm do próprio texto (Tabela 2 e Tabela 7) e repetem os da conclusão.

**Arquivo:** `trabalho.tex`, linha 65

**(a) Resultados de desempenho, antes da frase sobre explicabilidade**

**Procure:**
```latex
Os resultados quanto à explicabilidade indicam
```

**Substitua por:**
```latex
Quanto ao desempenho, a validação cruzada repetida não encontrou diferença estatisticamente significativa entre Regressão Logística, SVM, Random Forest e KNN, com acurácia média entre 0,960 e 0,973, e a Regressão Logística, modelo intrinsecamente interpretável, igualou os modelos mais complexos. Com probabilidades recalibradas e uma faixa de recusa, a Regressão Logística, o Random Forest, o SVM e o comitê de voto suave decidiram entre 67\% e 74\% dos pacientes do conjunto de teste sem erro, devolvendo os demais à revisão humana. Os resultados quanto à explicabilidade indicam
```

**(b) Limitações, na última frase**

**Procure:**
```latex
Contudo, essa interpretabilidade ainda não foi avaliada por profissionais de saúde.
```

**Substitua por:**
```latex
Contudo, essa interpretabilidade ainda não foi avaliada por profissionais de saúde, e os modelos, treinados em uma base de 569 amostras, não foram validados em dados de outras instituições.
```

> Com as duas inserções, o resumo fica com cerca de 260 palavras (a NBR 6028 pede de 150 a 500) e continua cabendo em uma página.

---

## 2. Roteiro dos capítulos (p. 18) ⚠️

**Já feito:** o parágrafo do roteiro existe (linha 210).

**Falta:** a professora pediu "o roteiro dos capítulos **e a indicação dos apêndices com os manuais**".

**Procure:**
```latex
O Capítulo 5 retoma os resultados obtidos, suas limitações e os trabalhos futuros.
```

**Substitua por:**
```latex
O Capítulo 5 retoma os resultados obtidos, suas limitações e os trabalhos futuros. Os Apêndices A e B trazem, respectivamente, os manuais de instalação e de uso do software.
```

---

## 3. Apêndices com os manuais de instalação e uso ❌

**Falta por inteiro.** O `trabalho.tex` vai de `\bibliography{referencias}` direto para `\end{document}`. A professora pediu: *"transforme as orientações operacionais das pp. 87–98 em documentação de instalação e uso identificada como apêndice, completando-a quando necessário"*.

O texto pronto está em **`RevisaoClaude/apendices_A_B.tex`**:

- **Apêndice A, Manual de instalação:** requisitos, instalação do executável (Windows e Linux, aviso do SmartScreen, `--autoteste`, pasta de exemplos, onde ficam os dados) e execução pelo código-fonte (Tkinter, venv, `requirements`, retreino, `calibrar_limiares.py`, `pytest`).
- **Apêndice B, Manual de uso:** abas, preparação da planilha, os seis passos, leitura das colunas e cuidados de uso.

Os nomes de botões, abas, arquivos e mensagens foram conferidos no código do repositório (versão de 13/10) e no `LEIA-ME.txt` do empacotamento.

A formatação segue o manual de Normas Técnicas da UTP (4. ed., 2024). Os comentários no início do arquivo indicam a página de cada regra:

- o manual de instalação e uso é um dos exemplos de apêndice do próprio manual (p. 48);
- os apêndices vêm depois das referências;
- a identificação é "APÊNDICE A – TÍTULO", em maiúsculas e com travessão (p. 49), centralizada e começando em página nova (p. 16);
- o título aparece em maiúsculas também no sumário, que deve ter a "mesma grafia" do texto (pp. 42–43);
- os subtítulos de nível 2 vão em maiúsculas, sem negrito (p. 16);
- as alíneas começam com minúscula e terminam em ponto e vírgula, e só a última em ponto final;
- o itálico fica só para palavras estrangeiras (p. 20).

**(a) Inserir os apêndices depois das referências**

**Procure:**
```latex
% Carrega o arquivo referencias.bib
\bibliography{referencias}
```

**Substitua por:**
```latex
% Carrega o arquivo referencias.bib
\bibliography{referencias}

% >>> COLE AQUI O CONTEÚDO DE RevisaoClaude/apendices_A_B.tex <<<
```

> Na compilação de teste, os apêndices saíram como "APÊNDICE A – MANUAL DE INSTALAÇÃO DO DIAGNOSISXAI" (pp. 104–106) e "APÊNDICE B – MANUAL DE USO DO DIAGNOSISXAI" (pp. 107–109), com a mesma grafia no sumário. Medi o recuo de todos os parágrafos: 1,25 cm, como pede o manual (p. 17).

**(b) Remissão aos apêndices no fim da Subseção 4.8.6 (Distribuição)**

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

## 4. UMAP × Mahalanobis (pp. 17–18) ⚠️

**Já feito:** a linha 208 explica que o UMAP deixou de sinalizar anomalias e que essa função passou à distância de Mahalanobis.

**Falta:** dois parágrafos antes, a linha 202 ainda diz que o UMAP identifica "agrupamentos e anomalias". Quem lê na ordem vê a afirmação antes da correção.

**Procure:**
```latex
identificando agrupamentos (\textit{clusters}) e anomalias de forma gráfica.
```

**Substitua por:**
```latex
identificando agrupamentos (\textit{clusters}) de forma gráfica.
```

---

## 5. Verbos no futuro referentes ao que já foi feito ⚠️

Restam quatro trechos. "Serão explorados" na abertura de capítulo (linha 220), que só anuncia as seções seguintes, pode ficar.

**(a) Linha 262, fim da Seção 2.2**

**Procure:**
```latex
a construção do agente racional será fundamentada especificamente
```

**Substitua por:**
```latex
a construção do agente racional foi fundamentada especificamente
```

**(b) Linha 607, Street et al.** (aproveita para corrigir "modelos de SHAP e UMAP": SHAP e UMAP não são modelos)

**Procure:**
```latex
cada uma das variáveis que serão processadas pelos modelos de SHAP e UMAP.
```

**Substitua por:**
```latex
cada uma das variáveis processadas pelos modelos e analisadas pelo SHAP e pelo UMAP.
```

**(c) Linha 667, Chen et al.**

**Procure:**
```latex
estabelecendo o patamar de desempenho que este TCC deve buscar atingir antes de aplicar as camadas de explicabilidade.
```

**Substitua por:**
```latex
estabelecendo o patamar de desempenho tomado como referência por este TCC antes da aplicação das camadas de explicabilidade.
```

**(d) Linhas 1177–1178, histogramas** (além do futuro, o texto promete uma projeção **PCA** que não aparece em nenhum lugar do trabalho)

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

---

## 6. Dificuldades na conclusão (pp. 97–100) ⚠️

**Já feito:** o relato das dificuldades existe e cita os exemplos que a professora deu (decisão exibida × classificador, calibração, empacotamento).

**Problema:** está **duas vezes**.

- Linha 2467: "Ao longo do desenvolvimento, três obstáculos exigiram ajustes..." (divergência SVM/KNN, calibração, empacotamento).
- Linha 2471: "Durante o desenvolvimento, três dificuldades exigiram ajustes..." repete a divergência e a calibração e acrescenta o limiar de 92%. O limiar já está no parágrafo 2461 ("a decisão deixou de usar o corte de 50%...").

Além da repetição, o segundo parágrafo diz "equilibrar a sensibilidade com a **precisão**" e resolve isso com um piso de **especificidade**, que é outra métrica. Com os dois parágrafos, a conclusão ocupa ~3,3 páginas, acima das 3 que o orientador fixou.

**Solução:** apagar o segundo parágrafo. Na compilação de teste, com todos os blocos deste arquivo aplicados, a conclusão voltou para **3 páginas** (pp. 98–100; ela passa a começar uma página depois por causa dos acréscimos anteriores). Ela fica no limite: se quiser acrescentar algo nela, corte o equivalente.

**(a) Apagar o parágrafo duplicado** (é a linha 2471 inteira; apague também a linha em branco que a segue)

**Procure:**
```latex
Durante o desenvolvimento, três dificuldades exigiram ajustes. A decisão exibida na interface divergia da decisão real do SVM e do KNN, o que foi corrigido e passou a ser verificado por testes automatizados. A regressão isotônica, apesar do melhor escore de Brier, tende a se sobreajustar em amostras pequenas, e por isso foi adotado o escalonamento de Platt, que no SVM atua sobre a função de decisão. Por fim, equilibrar a sensibilidade com a precisão, que o F1-score combina, exigiu maximizar a detecção de malignos sem que o programa sinalizasse câncer em pacientes saudáveis. Essa tensão foi resolvida com o menor limiar cuja especificidade, medida sobre as probabilidades out-of-fold do treino, atingisse 92\%, e com uma faixa de recusa para os casos intermediários, sem que o conjunto de teste participasse da escolha.

```

**Substitua por:** *(nada; apague)*
```latex
```

**(b) Recomendado: "assegurada" repete o problema de "garantida"** (linha 2465)

A professora pediu para trocar a explicabilidade "garantida" porque a compreensão pelos profissionais não foi avaliada. "Assegurada", na conclusão, tem o mesmo sentido.

**Procure:**
```latex
A interpretabilidade, porém, foi assegurada no plano técnico
```

**Substitua por:**
```latex
A interpretabilidade, porém, foi tratada no plano técnico
```

> A explicação do SVM no parágrafo 2467 ("Como a aplicação direta de Platt sobre o SVM piorava sua calibração...") tem um erro técnico. Ele está no item A3 do arquivo `02_revisao_completa.md`, com a correção.

---

## 7. Afirmações absolutas da fundamentação ⚠️

**Já resolvidas:** "comprova a verdadeira eficácia [...] na prática médica" (p. 27) e "seguro e incontestável" (p. 40) não existem mais. O parágrafo da linha 479 ("É essa diferença de transparência, e não necessariamente de desempenho...") ajuda.

**Falta:** a da **p. 37** continua. É a linha 487, que hoje cai na p. 37:

> "modelos intrinsecamente interpretáveis [...] embora frequentemente apresentem **limitações de desempenho** em dados biológicos complexos" [...] "opta-se pela segunda via [...] que alie o **máximo desempenho preditivo**"

Há dois problemas. O primeiro é que o texto associa interpretabilidade a pior desempenho, que é justamente a associação que a professora apontou e que os seus resultados desmentem (a RL igualou os modelos complexos). O segundo é mais grave: a frase atribui essa ideia a **Rudin (2019)**, cujo artigo defende o contrário. O título dele é "*Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead*". Alguém da banca que conheça o artigo vai notar.

**(a) Linha 487, primeira frase**

**Procure:**
```latex
cujas equações matemáticas são naturalmente transparentes, embora frequentemente apresentem limitações de desempenho em dados biológicos complexos.
```

**Substitua por:**
```latex
cujas equações matemáticas são naturalmente transparentes. Para a autora, em decisões de alto risco esses modelos frequentemente alcançam desempenho comparável ao dos modelos de caixa preta, possibilidade que deve ser verificada antes de se recorrer a estes.
```

**(b) Linha 487, últimas frases**

**Procure:**
```latex
No escopo deste estudo, opta-se pela segunda via. Ao aplicar métodos \textit{post-hoc} sobre classificadores robustos, busca-se entregar ao oncologista uma ferramenta que alie o máximo desempenho preditivo da computação moderna à transparência analítica exigida pela ética médica.
```

**Substitua por:**
```latex
No escopo deste estudo, as duas vias são combinadas: modelos intrinsecamente interpretáveis são comparados a modelos de caixa preta, e métodos \textit{post-hoc} são aplicados a todos eles, de modo a verificar se a complexidade adicional se traduz em ganho de desempenho e a acompanhar cada diagnóstico de uma explicação.
```

**Mesma natureza, ainda na fundamentação (recomendados).** A professora pediu para revisar "as afirmações absolutas da fundamentação" e deu três exemplos. Estas são do mesmo tipo:

**(c) Linha 285**

**Procure:**
```latex
Para garantir que o classificador encontre o equilíbrio estatístico perfeito e seja seguro para uso clínico, é obrigatório adotar
```

**Substitua por:**
```latex
Para buscar esse equilíbrio e estimar honestamente o desempenho do classificador, é necessário adotar
```

**(d) Linha 396**

**Procure:**
```latex
os mais utilizados na prática para garantir que o algoritmo se adapte perfeitamente à complexidade biológica do câncer.
```

**Substitua por:**
```latex
os mais utilizados na prática para que o algoritmo se adapte a fronteiras de decisão não lineares.
```

**(e) Linha 475**

**Procure:**
```latex
gera um sistema preditivo altamente estável e protegido contra anomalias
```

**Substitua por:**
```latex
gera um sistema preditivo mais estável e menos sensível a ruídos
```

**(f) Linha 511** (no software, os valores de Shapley da RL, do SVM e do KNN são aproximados pelo KernelExplainer, o que o próprio texto reconhece na p. 92)

**Procure:**
```latex
garantindo que o valor final seja distribuído de maneira perfeitamente justa.
```

**Substitua por:**
```latex
de modo que o valor final seja distribuído de maneira justa, no sentido dos axiomas propostos por Shapley.
```

**Procure:**
```latex
O resultado é um único valor $\phi_i$ que quantifica, com exatidão matemática, o impacto líquido
```

**Substitua por:**
```latex
O resultado é um único valor $\phi_i$ que quantifica o impacto líquido
```

**(g) Linha 524.** Além de absoluta, a frase está **errada**: o UMAP não preserva distâncias, e as distâncias entre grupos numa projeção UMAP não devem ser lidas como reais. Essa limitação é a mesma que o Cap. 4 constata ao trocar o UMAP pela distância de Mahalanobis.

**Procure:**
```latex
o UMAP assegura que as proporções de distância sejam mantidas na projeção visual.
```

**Substitua por:**
```latex
o UMAP tende a preservar melhor a disposição geral dos dados, embora as distâncias entre agrupamentos na projeção não devam ser lidas como distâncias reais.
```

**(h) Linha 577**

**Procure:**
```latex
Essa representação comprova a capacidade visual do algoritmo
```

**Substitua por:**
```latex
Essa representação ilustra a capacidade visual do algoritmo
```

---

## 8. Contagem de colunas (pp. 55–56) ✅

O "32" errado saiu do texto e nenhum total de colunas é citado agora. Como a professora vai procurar essa correção, vale deixá-la visível (opcional).

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

## 9. Figura 9 e Gráfico 1 ✅

Conferido no PDF compilado: a Subseção 4.5.2 termina na p. 61, o Gráfico 1 entra no fim da mesma página, a Figura 9 ocupa o topo da p. 62 e o texto continua logo abaixo. Nada a fazer.

---

## 10. Tabelas das pp. 77 e 83 ✅ e Quadro 4 (novo)

As Tabelas 2 (p. 77) e 7 (p. 83) agora cabem nas margens (conferido na imagem da página). O log da compilação acusa um único estouro no corpo do texto: o **Quadro 4 (Bibliotecas, p. 57) passa 7 pt da margem direita**.

**Procure:**
```latex
\begin{tabular}{|l|p{12.6cm}|}
```

**Substitua por:**
```latex
\begin{tabular}{|l|p{12.3cm}|}
```

---

## 11. Friedman e 5×2cv (pp. 78–80) ⚠️

**Já feito:** os blocos estão identificados (as 50 dobras da validação cruzada 10×5), a dependência entre as dobras foi reconhecida ("lidos como panorama") e o parágrafo da linha 1898 explica por que o 5×2cv não viu a diferença que o Nemenyi viu.

**Falta:** a professora pediu essa explicação **antes** de apresentar a inferioridade da Árvore como conclusão definitiva. Hoje a ordem é: Tabela 4 → "A leitura da Tabela é **inequívoca** [...] sua inferioridade é **estatisticamente sustentada**" → só depois a explicação. E "inequívoca" contradiz o "lidos como panorama" de dois parágrafos antes.

**(a) Pontuação na linha 1869**

**Procure:**
```latex
otimistas, por isso, o Friedman e o Nemenyi são lidos como panorama.
```

**Substitua por:**
```latex
otimistas; por isso, o Friedman e o Nemenyi são lidos como panorama.
```

**(b) Apagar o parágrafo da linha 1898 do lugar atual** (ele volta no passo c)

**Procure:**
```latex
A diferença entre os dois testes para a Árvore de Decisão decorre do que cada um usa. O 5×2cv compara dois modelos com apenas dez estimativas de diferença, cada uma obtida treinando em metade do conjunto de treino, o que reduz seu poder. O Nemenyi usa as posições dos cinco modelos nas 50 dobras, e nelas a Árvore de Decisão fica quase sempre entre as piores, o que produz uma diferença de postos superior à distância crítica do teste. Assim, o resultado do 5×2cv não contradiz o do Nemenyi: o primeiro não tem poder para detectar essa diferença.

```

**Substitua por:** *(nada; apague)*
```latex
```

**(c) Recolocar a explicação antes da leitura da Tabela 4 e tirar o "inequívoca"**

**Procure:**
```latex
A leitura da Tabela~\ref{tab:nemenyi} é inequívoca e constitui o principal
```

**Substitua por:**
```latex
Antes de ler a Tabela~\ref{tab:nemenyi}, é preciso explicar por que ela aponta, para a Árvore de Decisão, uma diferença que o 5$\times$2cv não detectou. A diferença entre os dois testes decorre do que cada um usa. O 5$\times$2cv compara dois modelos com apenas dez estimativas de diferença, cada uma obtida treinando em metade do conjunto de treino, o que reduz seu poder. O Nemenyi usa as posições dos cinco modelos nas 50 dobras, e nelas a Árvore de Decisão fica quase sempre entre as piores, o que produz uma diferença de postos superior à distância crítica do teste. Assim, o resultado do 5$\times$2cv não contradiz o do Nemenyi: o primeiro tem pouco poder para detectar essa diferença.

Com essa ressalva, a leitura da Tabela~\ref{tab:nemenyi} constitui o principal
```

**(d) Linhas 1892–1893: pontuação e "estatisticamente sustentada"**

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

---

## 12. Faixa de recusa (pp. 82–84) ⚠️

**Já feito:** o texto explica que, com os limites exatos, não há erro no treino e que o falso negativo da Tabela 7 vem do arredondamento do limite inferior em `limiares.json`. "Cerca de um terço" agora está identificado como resultado do teste, e a devolução no treino ficou em "35% a 50%".

**Conferi no código** (`scripts/calibrar_limiares.py` e `app/core/decision.py`) e rodando o script em modo `--so-relatorio`: a explicação procede. O limite inferior é gravado com `round(…, 4)`; quando o arredondamento é para cima, o maligno de menor certeza fica abaixo do limite e é decidido como benigno. Os números da Tabela 7 batem com a saída da célula 45 do notebook.

**Falta:** *"Esclareça a inclusão dos limites da faixa."* O texto nunca diz se um paciente com certeza exatamente igual a um limite é decidido ou devolvido. No código, a faixa é **fechada à esquerda e aberta à direita**, [inferior; superior): benigno se certeza < inferior; maligno se certeza ≥ superior; revisar entre os dois. O limite superior é gravado 0,0001 acima do benigno de maior certeza.

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

> ⚠️ **Decisão sua: corrigir o arredondamento no código ou só explicar no texto?** Hoje o texto explica um defeito conhecido do script. A banca pode perguntar "por que não corrigiu?".
> - **Opção A (recomendada para o prazo):** manter como está e ter a resposta pronta (é a pergunta 42 do arquivo de perguntas). Nenhum número muda.
> - **Opção B:** em `faixa_de_recusa()`, gravar o limite inferior arredondado **para baixo** (`math.floor(inferior * 1e4) / 1e4`), rodar de novo `calibrar_limiares.py` e o notebook e atualizar a Tabela 7, o Gráfico 7, a régua citada na p. 86 e as capturas de tela. Isso dá muito retrabalho a seis dias da entrega.

---

## 13. Revisão linguística ✅

Todas as seis correções estão no texto: espaço em "abrir" (p. 17) e em "K" (p. 33), "mais semelhantes" (p. 33), oração separada (p. 23), "que sempre predissesse a classe benigna" (p. 61), "o conhecido conservadorismo" (p. 79) e "opção inicial do seletor" (p. 86).

Ajuste opcional na p. 86: "que é a opção inicial do seletor **e já vem selecionado**" diz a mesma coisa duas vezes.

**Procure:**
```latex
que é a opção inicial do seletor e já vem selecionado, e processa o lote;
```

**Substitua por:**
```latex
que é a opção inicial do seletor, e processa o lote;
```

---

## 14. Russell, IBM, SCHÜTZE, Faceli/Manning, INCA ✅

- "Russell; Norvig, 2010" corrigido (p. 21).
- IBM com data de acesso (07 nov. 2026).
- "SCHÜTZE" normalizado.
- Faceli et al. aparece como 2. ed. de 2021 e Manning et al. como 2008: ano e edição compatíveis.
- INCA (2026) com o título da notícia efetivamente consultada.

Os ajustes de formato que ainda cabem nas referências (ed., local, "maio", siglas em minúsculas) estão no item E do `02_revisao_completa.md`. Nenhum deles foi pedido pela professora.

---

## 15. Figura 6 ✅ (⚠️ confirmação sua)

A legenda e a referência agora apontam para o mesmo site (`aionlinecourse.com/tutorial/machine-learning/kernel-svm`). ⚠️ Só você pode confirmar que a imagem `hyperplane.png` saiu mesmo dessa página e que o ano da página é 2025. A chave do `.bib` se chama `AIOnlineCourse2023`, mas isso não aparece no PDF.

---

## 16. Referência da base de dados (p. 55) ⚠️

**Já feito:** a entrada `Wolberg1995` aponta para o UCI, com DOI e data de acesso.

**Dois problemas:**

1. ⚠️ **Origem do arquivo.** O `data/data.csv` do projeto tem cabeçalho entre aspas (`"id","diagnosis",...`) e gera a coluna `Unnamed: 32` ao ser lido. Esse é o formato da cópia publicada no **Kaggle** (`uciml/breast-cancer-wisconsin-data`). O arquivo do UCI (`wdbc.data`) não tem cabeçalho nem a coluna vazia. Como a professora pediu "a versão/local de obtenção" do arquivo utilizado, se você baixou do Kaggle, cite o Kaggle (alternativa abaixo).
2. **Formato da chamada.** É a única citação do trabalho feita com `\cite{}`, e por isso sai em caixa alta, "(WOLBERG et al., 1995)". Todas as outras saem como "(Street et al., 1993)". "Repositório UCI Machine Learning Repository" também repete "repositório".

**(a) Sempre: uniformizar a chamada**

**Procure:**
```latex
(Diagnostic)}, disponibilizada publicamente no repositório UCI Machine Learning
Repository \cite{Wolberg1995}, e referenciada ao longo
```

**Substitua por:**
```latex
(Diagnostic)}, disponibilizada publicamente no UCI Machine Learning
Repository (\citeauthoronline{Wolberg1995}, \citeyear{Wolberg1995}), e referenciada ao longo
```

**(b) Se o arquivo veio do Kaggle (provável)**, acrescente ao `referencias.bib`:

```bibtex
@misc{Kaggle2016,
  author        = {{UCI Machine Learning}},
  title         = {Breast Cancer Wisconsin (Diagnostic) Data Set},
  year          = {2016},
  howpublished  = {Kaggle},
  note          = {Arquivo data.csv},
  url           = {https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data},
  urlaccessdate = {08 nov. 2026}
}
```

e, no texto, logo depois da frase do item (a):

```latex
O arquivo utilizado, data.csv, foi obtido na cópia da base publicada no Kaggle
(\citeauthoronline{Kaggle2016}, \citeyear{Kaggle2016}), que traz os nomes das
colunas no cabeçalho.
```

> ⚠️ Confira na página do Kaggle o número da versão do conjunto e ponha no campo `note` (por exemplo, "Arquivo data.csv, versão 2"). Esse bloco (b) não foi aplicado na compilação de teste, porque depende da sua confirmação.

---

## 17. Fontes das figuras e quadros ⚠️

**Já feito:** as chamadas com autor estão todas em maiúsculas e minúsculas ("Adaptado de Davis e Goadrich, 2006", "Richardson, 2022", "Bollon et al., 2022"...).

**Falta:** o próprio autor aparece de três jeitos. São 20 `\fonte{O Autor}` ("FONTE: O Autor"), 19 `\fonteautor` ("FONTE: O autor") e um `\legend{Fonte: O Autor}` na Tabela 1, que sai até com "Fonte" em outra caixa. O comando do template da UTP é `\fonteautor`.

**Procure (todas as ocorrências; use "Substituir tudo"):**
```latex
\fonte{O Autor}
```

**Substitua por:**
```latex
\fonteautor
```

**Procure:**
```latex
\legend{Fonte: O Autor}
```

**Substitua por:**
```latex
\fonteautor
```

---

## 18. Entrega de 14/11 (texto + programa) ⚠️

O e-mail pede o texto completo e "o programa implementado (se necessário, incluir o(s) programa(s) instalador(es))".

**Achado importante:** o Release **v1.0** do GitHub, com `DiagnosisXAI-windows-x64.zip` e `DiagnosisXAI-linux-x64.zip`, foi publicado em **02/10/2026**. Depois dele vieram dois commits:

- `26d7558` (08/10): **retreino da Árvore de Decisão sem vazamento de dados** e correção da impureza;
- `22cbe5a` (13/10): ajustes em `committee.py`, `metrics.py` e `predict_view.py`.

Ou seja, **os executáveis publicados não contêm a Árvore de Decisão descrita no texto** (profundidade 7, 18 folhas, Tabela 1). Até esse commit, a Árvore era treinada numa partição própria, sem `stratify`, diferente da dos outros modelos. Por isso, no v1.0, ela foi treinada com parte dos pacientes que estão no lote de teste de exemplo, e a auditoria da Árvore no executável sai otimista. Se a banca abrir o v1.0 e comparar com a Tabela 1, os números da Árvore não batem.

Checklist:

- [ ] Aplicar os itens 1 a 17 no `trabalho.tex` e recompilar (`make`).
- [ ] Gerar um Release novo para os executáveis incluírem os commits de outubro: `git tag v1.1 && git push origin v1.1` no repositório DiagnosisXAI. O workflow `executavel.yml` roda a cada tag `v*`, executa o `--autoteste` e publica os dois `.zip`.
- [ ] Atenção: a cópia local em `~/DiagnosisXAI` está **7 commits atrás** do GitHub. Rode `git pull` antes de mexer nela ou de empacotar algo a partir dela.
- [ ] Baixar os dois `.zip` do v1.1, abrir cada um e rodar `DiagnosisXAI --autoteste`.
- [ ] Na pasta do OneDrive: o PDF do texto, os dois `.zip` e o link do repositório (código-fonte, notebook e testes).
- [ ] Conferir se a UTP exige folha de aprovação e *abstract* nesta entrega (ver item D1 do `02_revisao_completa.md`).
