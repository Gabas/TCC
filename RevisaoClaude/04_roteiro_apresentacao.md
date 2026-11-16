# Roteiro da apresentação: DiagnosisXAI (19 min 30 s)

Roteiro fala a fala do `Apresentacao3TCC.pptx` (19 slides). Os números conferem com o `trabalho.tex` de 15/11.

## Como usar este roteiro

- **Fala**: o texto entre aspas e recuado é o que você diz. Cada fala foi medida em palavras para caber no tempo do slide, num ritmo calmo de cerca de 135 palavras por minuto.
- **Não decore palavra por palavra.** Decore a **frase-âncora** de cada slide e a ordem das ideias. Se der branco, diga a frase-âncora e siga para o slide seguinte.
- `▶` marca uma ação: apontar, clicar ou avançar. `[pausa]` é um silêncio de 1 a 2 segundos. As palavras em **negrito** são para enfatizar com a voz.
- Os tempos somam **19 min 30 s** e deixam 30 s de folga até os 20 min. Na prática, a apresentação tende a crescer com o nervosismo, então respeite os marcos do cronômetro (seção 3).

---

## 1. Antes de entrar na sala

**Na véspera**

- [ ] Ensaie **três vezes com cronômetro**: a primeira lendo o roteiro, a segunda só com as frases-âncora e a terceira com a demonstração real. Grave pelo menos um dos ensaios no celular e ouça.
- [ ] No ensaio da demonstração, **anote quais pacientes vai mostrar** (um Maligno, um Benigno e um Revisar) e a certeza de cada um. Nas capturas do texto, com o comitê, são o paciente 0 (Maligno, 94,8%), o paciente 5 (Benigno, 1,06%) e o paciente 1 (Revisar, 1,2%). Confirme na versão que você vai usar.
- [ ] Exporte os slides também em **PDF** e leve num pendrive, para o caso de o PowerPoint falhar.
- [ ] Deixe salvo um **PDF de paciente já exportado**, para mostrar se a exportação travar.

**No dia, antes de começar**

- [ ] Abra o **DiagnosisXAI** e rode o `--autoteste` antes de entrar na sala. Depois deixe o programa aberto na aba **Novo Diagnóstico**.
- [ ] Confira se `dataTeste_sem_diagnostico.csv` está na pasta `exemplos`, fácil de achar.
- [ ] Desligue as notificações (modo Não Perturbe), feche os outros programas e conecte o carregador.
- [ ] Teste no projetor a troca entre os slides e o programa (Alt+Tab no Windows, Cmd+Tab no Mac). O DiagnosisXAI foi feito para 1920×1080; em telas menores, as janelas ocupam até 90% da área.
- [ ] Deixe um cronômetro visível e um copo de água por perto.
- [ ] Confirme com a Angela o tempo exato da apresentação.

---

## 2. Mapa do tempo

| Slide | Título | Duração | Começa em | Termina em |
|---|---|---|---|---|
| 1 | Capa | 25 s | 0:00 | 0:25 |
| 2 | Justificativa | 1:05 | 0:25 | 1:30 |
| 3 | Objetivos da pesquisa | 55 s | 1:30 | 2:25 |
| 4 | Situação atual, usuários e clientes | 55 s | 2:25 | 3:20 |
| 5 | Trabalhos relacionados | 1:05 | 3:20 | 4:25 |
| 6 | Construção da solução | 1:15 | 4:25 | 5:40 |
| 7 | Arquitetura e ferramentas | 55 s | 5:40 | 6:35 |
| 8 | O protótipo em funcionamento | 50 s | 6:35 | 7:25 |
| 9 | **Demonstração ao vivo** | **3:00** | 7:25 | 10:25 |
| 10 | Desempenho dos modelos | 1:15 | 10:25 | 11:40 |
| 11 | Qual erro é pior? | 45 s | 11:40 | 12:25 |
| 12 | A certeza exibida é confiável? | 1:05 | 12:25 | 13:30 |
| 13 | Decidir ou devolver ao especialista | 1:15 | 13:30 | 14:45 |
| 14 | IA explicável | 1:15 | 14:45 | 16:00 |
| 15 | Validação do software | 45 s | 16:00 | 16:45 |
| 16 | Alcance dos objetivos | 45 s | 16:45 | 17:30 |
| 17 | Importância e dificuldades | 1:00 | 17:30 | 18:30 |
| 18 | Limitações e trabalhos futuros | 45 s | 18:30 | 19:15 |
| 19 | Obrigado | 15 s | 19:15 | **19:30** |

Por bloco: introdução e tema, 4:25; método e protótipo, 3:00; demonstração, 3:00; resultados, 5:35; conclusão, 3:30.

---

## 3. Marcos do cronômetro e plano de corte

Olhe o cronômetro só nestes quatro momentos:

| Ao chegar em | O ideal é | Se passou de | Corte |
|---|---|---|---|
| Slide 9 (demonstração) | 7:25 | **8:00** | Na demonstração, pule a coluna Perfil e a exportação do PDF (passos D2 e F): ela cai para cerca de 2:15 |
| Slide 10 (resultados) | 10:25 | **11:00** | No slide 12, pule as definições de Brier e ECE. No slide 13, pule a explicação dos eixos do gráfico |
| Slide 14 (SHAP) | 14:45 | **15:15** | No slide 15, diga só os três números. No slide 16, diga só "os quatro objetivos foram atendidos" e passe direto à resposta da pergunta de pesquisa |
| Slide 17 (importância) | 17:30 | **18:00** | No slide 17, cite as três dificuldades em uma frase cada, sem explicar |

**Nunca corte:** a pergunta de pesquisa (slide 2), o empate e a validação cruzada (slide 10), a pergunta do slide 11, os números 96, 47 e 67 a 74% (slide 13), a ressalva do SHAP (slide 14) e as limitações (slide 18).

---

## 4. Roteiro slide a slide

### Slide 1. Capa (0:00 → 0:25, 25 s)

**Na tela:** título, seu nome, o orientador e duas imagens do software (à esquerda, a importância SHAP; à direita, o mapa UMAP).

**Fala**

> "Boa noite a todos. Meu nome é Gabriel Ast dos Santos, sou aluno do Bacharelado em Ciência da Computação da Universidade Tuiuti do Paraná, e vou apresentar o meu Trabalho de Conclusão de Curso: um software com Inteligência Artificial Explicável para apoio ao diagnóstico de câncer de mama, utilizando SHAP e UMAP, com orientação do professor Rodrigo Ramos Alves."

▶ Se der tempo, aponte para as imagens: "As duas imagens já são do próprio software." Depois avance.

**Frase-âncora:** "Um software que explica cada diagnóstico de câncer de mama."

---

### Slide 2. Justificativa (0:25 → 1:30, 1 min 05 s)

**Na tela:** os três números (30%, 781 mil e 1,4 milhão) e a caixa verde com o problema e a pergunta.

**Objetivo do slide:** mostrar por que o trabalho existe e chegar à pergunta de pesquisa.

**Fala**

> "Começo pelo porquê deste trabalho. ▶ *(aponte para os três números)* Segundo o INCA, **30%** dos novos diagnósticos de câncer em mulheres no Brasil são de mama. O país deve ter **781 mil** novos casos de câncer por ano no triênio de 2026 a 2028, e, nas Américas, o câncer causou **1,4 milhão** de mortes em 2022, segundo a OPAS. E muitos desses casos têm alta chance de cura quando o diagnóstico é precoce.
>
> O aprendizado de máquina já classifica tumores com acurácia muito alta. ▶ *(aponte para a caixa verde)* O problema é que esses modelos são **caixas pretas**: dizem 'benigno' ou 'maligno' sem mostrar por quê. E, na prática médica, um diagnóstico de malignidade sem fundamentação não basta: o profissional precisa saber o que pesou na decisão para poder confiar nela.
>
> [pausa] Daí a minha pergunta de pesquisa: **como integrar explicabilidade e redução de dimensionalidade a um modelo preditivo, para obter diagnósticos ao mesmo tempo acurados e interpretáveis por profissionais de saúde?**"

▶ Avance.

**Frase-âncora:** "Os modelos acertam muito, mas são caixas pretas, e o médico precisa saber o porquê."

---

### Slide 3. Objetivos da pesquisa (1:30 → 2:25, 55 s)

**Na tela:** o objetivo geral no bloco verde e os quatro objetivos específicos numerados.

**Fala**

> "▶ *(aponte para o bloco verde)* O objetivo geral foi desenvolver um software de apoio ao diagnóstico de câncer de mama que acompanhe **cada diagnóstico de uma justificativa transparente**.
>
> ▶ *(percorra os números de 1 a 4)* Ele se desdobra em quatro objetivos específicos, que são também o roteiro desta apresentação. Um: comparar cinco classificadores na base pública Breast Cancer Wisconsin. Dois: avaliar esses modelos com rigor; não só com uma divisão de treino e teste, mas com validação cruzada, testes estatísticos e calibração. Três: explicar cada decisão, com o SHAP, que mostra quanto cada atributo pesou para aquele paciente, e com o UMAP, que situa o caso no mapa da população conhecida. E quatro: entregar um software funcional, o DiagnosisXAI, para Windows e Linux. No final, volto a esses quatro pontos."

▶ Avance.

**Frase-âncora:** "Comparar, avaliar com rigor, explicar e entregar o software."

---

### Slide 4. Situação atual, usuários e clientes (2:25 → 3:20, 55 s)

**Na tela:** três colunas (Situação atual, Usuários e Clientes).

**Fala**

> "▶ *(coluna Situação atual)* Hoje, classificar tumores com aprendizado de máquina já é uma linha de pesquisa consolidada, com acurácias altíssimas. Mas, na clínica, isso esbarra na caixa preta. A explicabilidade, a XAI, ataca exatamente esse ponto: mostra o peso de cada atributo em cada decisão.
>
> ▶ *(coluna Usuários)* Os usuários são os profissionais que validam o diagnóstico, patologistas e oncologistas, e os laboratórios de citopatologia, que já extraem os trinta atributos do núcleo celular a partir da punção aspirativa por agulha fina. Pesquisadores também podem usar o sistema para auditar o desempenho contra um gabarito.
>
> ▶ *(coluna Clientes)* Os clientes são hospitais, clínicas oncológicas e empresas de software para a saúde. E um detalhe importante: o sistema roda localmente, então **os dados dos pacientes não saem da instituição**."

▶ Avance.

**Frase-âncora:** "Quem valida o diagnóstico usa; os dados não saem da instituição."

---

### Slide 5. Trabalhos relacionados (3:20 → 4:25, 1 min 05 s)

**Na tela:** a tabela com cinco trabalhos e a linha "Este projeto", mais a caixa verde com a lacuna.

**Fala**

> "▶ Analisei oito trabalhos relacionados; nesta tabela estão os cinco sobre câncer de mama, comparados em três pontos: validação, interface e explicabilidade.
>
> ▶ *(coluna Validação)* O trabalho que deu origem à base, de Street e colaboradores, de 1993, já usava validação cruzada. Mas Rabiei e Chen medem o desempenho numa partição única de treino e teste, e Silva Júnior não chega a ter validação quantitativa. Como vou mostrar nos resultados, uma partição única pode dar uma estimativa otimista.
>
> ▶ *(coluna XAI)* Só Shaon e colaboradores, em 2024, usam SHAP, e mesmo assim como filtro global de atributos, sem explicar paciente por paciente.
>
> ▶ *(caixa da lacuna)* A lacuna, então, é esta: **nenhum testa a significância das diferenças entre os modelos nem avalia a calibração, e nenhum reúne aprendizado de máquina, explicabilidade e uma interface utilizável.** ▶ *(última linha da tabela)* É isso que este projeto faz."

▶ Avance.

**Frase-âncora:** "Ninguém testou significância nem calibração, e ninguém juntou ML, XAI e interface."

**Se perguntarem aqui:** os outros três trabalhos são Cruz e Wishart (2006), uma revisão; Masud et al. (2021), sobre pulmão e cólon; e Abdullah et al. (2021), sobre pulmão. Estão no Capítulo 3.

---

### Slide 6. Construção da solução (4:25 → 5:40, 1 min 15 s)

**Na tela:** seis etapas numeradas com setas.

**Fala**

> "▶ *(etapa 1)* A solução foi construída em seis etapas. A base é a Breast Cancer Wisconsin Diagnostic: **569 amostras**, 357 benignas e 212 malignas, com **30 atributos** do núcleo celular. São dez medidas, como raio, textura, área e concavidade, cada uma em média, erro padrão e pior valor.
>
> ▶ *(etapa 2)* Na preparação, separei 75% para treino e 25% para teste, de forma estratificada. O teste, com 143 pacientes, ficou isolado até a avaliação final, e o Z-score foi ajustado só no treino, para não vazar informação do teste.
>
> ▶ *(etapa 3)* Treinei cinco classificadores: Árvore de Decisão, KNN, Regressão Logística, Random Forest e SVM.
>
> ▶ *(etapa 4)* Na validação, fui além da divisão única: validação cruzada estratificada dez por cinco, ou seja, 50 dobras, e o teste de Friedman com pós-hoc de Nemenyi, para saber quais diferenças entre os modelos são reais.
>
> ▶ *(etapa 5)* Calibrei as probabilidades com o escalonamento de Platt e escolhi, só com o treino, um limiar de decisão e uma faixa de recusa.
>
> ▶ *(etapa 6)* E integrei tudo ao software, com SHAP, UMAP e relatórios."

▶ Avance.

**Frase-âncora:** "O teste ficou isolado; tudo foi escolhido só com o treino."

**Se perguntarem aqui:** a pesquisa é aplicada, quantitativa, experimental e computacional, com a semente de aleatoriedade fixa (RANDOM_STATE = 42) para tornar os experimentos reprodutíveis.

---

### Slide 7. Arquitetura e ferramentas (5:40 → 6:35, 55 s)

**Na tela:** o fluxo Dados CSV → Notebook → wisconsin.pkl e limiares.json → DiagnosisXAI, e três cartões de ferramentas.

**Fala**

> "▶ *(fluxo de cima)* A arquitetura tem dois módulos desacoplados. O módulo científico é um notebook Jupyter que lê os dados em CSV, treina e avalia os modelos e grava dois arquivos: o wisconsin.pkl, com os modelos, o padronizador, os explicadores e o mapa UMAP, e o limiares.json, com o limiar e a faixa de recusa de cada modelo. A aplicação só lê esses dois arquivos e devolve os resultados em CSV e PDF. Para retreinar com outra base, basta reexecutar o notebook e o script de limiares, sem mexer na aplicação.
>
> ▶ *(cartões de baixo)* As ferramentas: Python 3.12, scikit-learn, shap, umap-learn e scipy na parte científica; CustomTkinter, matplotlib, bokeh e reportlab na aplicação; e PyInstaller com GitHub Actions para gerar os executáveis de Windows e Linux."

▶ Avance.

**Frase-âncora:** "Dois módulos que conversam por dois arquivos."

---

### Slide 8. O protótipo em funcionamento (6:35 → 7:25, 50 s)

**Na tela:** a captura da tela de diagnóstico e os seis passos numerados.

**Fala**

> "▶ *(aponte para a captura)* O trabalho não parou na comparação dos modelos: **foi desenvolvido um software funcional**. A tela de diagnóstico organiza o uso em seis passos, e cada um só é liberado depois do anterior. Isso impede, por exemplo, diagnosticar dados que ainda não foram padronizados, o que daria resultados errados sem nenhum aviso.
>
> ▶ *(percorra os passos de 1 a 6)* O profissional importa a planilha, padroniza, escolhe um dos cinco modelos ou o comitê de voto suave, que faz a média das certezas de quatro deles, e processa. Depois, se quiser, audita contra um gabarito, abre as explicações e exporta em CSV e PDF.
>
> Em vez de descrever cada tela, vou mostrar o sistema funcionando."

▶ Avance para o slide 9 **e já troque para o DiagnosisXAI**.

**Frase-âncora:** "Seis passos em sequência, para não diagnosticar dado errado."

---

### Slide 9. Demonstração ao vivo (7:25 → 10:25, 3 min)

**Na tela:** primeiro o slide 9 e logo depois o DiagnosisXAI, aberto na aba Novo Diagnóstico.

**Marco do cronômetro:** se começar depois de **8:00**, pule os passos D2 e F.

| Tempo | Ação | Fala |
|---|---|---|
| **A** · 0:00–0:15 | ▶ Alt+Tab / Cmd+Tab para o DiagnosisXAI | "Este é o DiagnosisXAI. Vou usar o próprio conjunto de teste: 143 pacientes que nenhum modelo viu no treino." |
| **B** · 0:15–0:40 | ▶ **Passo 1:** clique em *Procurar Arquivo*, abra a pasta `exemplos` e escolha `dataTeste_sem_diagnostico.csv`. ▶ **Passo 2:** clique em *Aplicar Padronização* | "A planilha traz os 30 atributos brutos, como o laboratório mede. Ao padronizar, o sistema primeiro valida a planilha, e recusaria o lote se faltasse uma coluna ou houvesse célula vazia. Depois aplica o mesmo Z-score ajustado no treino." |
| **C** · 0:40–1:20 | ▶ **Passo 3:** escolha *Comitê (voto suave)* e confira se *Adiar casos incertos em vez de decidir* está marcado. ▶ Aponte para a **régua de decisão**. ▶ Clique em *Processar Diagnóstico* e aponte para a mensagem em laranja | "Escolho o comitê, com a recusa ligada. A régua mostra como ele decide: abaixo de **1,1%** de certeza, Benigno; a partir de **68,2%**, Maligno; no meio, Revisar. Os cortes não são arbitrários: 1,1% é a menor certeza que um tumor maligno recebeu no treino, e 68,2% é a maior que um benigno recebeu. *(clique)* Pronto: **96 pacientes receberam diagnóstico, e 47 foram devolvidos para revisão.**" |
| **D1** · 1:20–1:50 | ▶ Na tabela, aponte para os três pacientes que você anotou no ensaio | "Este paciente saiu Maligno, com 94,8% de certeza. Este, Benigno, com cerca de 1%. E este ficou em Revisar com 1,2%: parece pouco, mas está dentro da faixa, porque no treino houve tumor maligno com certeza tão baixa quanto essa. **O sistema prefere devolver o caso a arriscar um palpite.**" |
| **D2** · 1:50–2:05 *(pule se estiver atrasado)* | ▶ Aponte para a coluna **Perfil** | "E a coluna Perfil avisa quando o paciente foge da população de treino, pela distância de Mahalanobis. Aqui, todos os 143 são típicos." |
| **E** · 2:05–2:45 | ▶ **Passo 5:** escolha *Comitê: concordância dos membros* e clique em *Abrir Relatório*. ▶ Selecione o paciente Maligno | "No quinto passo abro a explicação. Para este paciente vejo a posição de cada membro do comitê e o bloco **'Fatores que mais pesaram'**, que decompõe a certeza da tabela nos fatores morfológicos, com valores de Shapley exatos. A soma fecha exatamente no número que o profissional viu." |
| **F** · 2:45–3:00 *(pule se estiver atrasado)* | ▶ Clique em *Exportar Paciente (PDF)*. ▶ Volte aos slides e avance para o 10 | "E esse laudo, com a justificativa, pode ser exportado em PDF, para ser conferido fora do sistema. Agora, os números por trás do que vimos." |

**Se a demonstração falhar** (o programa não abre, trava ou demora):

> "Por segurança, trouxe a captura. ▶ *(volte ao slide 9 e aponte para a imagem)* Este é o relatório do comitê: à esquerda, em que fração do lote cada membro concorda com a média; à direita, a posição de cada membro para o paciente selecionado; embaixo, a decisão de cada paciente e o bloco de fatores que mais pesaram."

Depois siga para o slide 10. O tempo que sobrar vira folga; não tente recuperar a demonstração.

**Se o processamento demorar:** enquanto espera, explique a régua; a fala do passo C serve para isso.

**Frase-âncora:** "Ele decide quando tem segurança e devolve quando não tem."

---

### Slide 10. Desempenho dos modelos (10:25 → 11:40, 1 min 15 s)

**Marco:** se chegar depois de **11:00**, use os cortes dos slides 12 e 13.

**Na tela:** gráfico de barras com acurácia e sensibilidade de cada modelo no teste e, à direita, a caixa da validação cruzada.

**Fala**

> "▶ *(gráfico)* Agora, os resultados. No teste, com 143 pacientes e o corte padrão de 50%, **a Regressão Logística e o SVM empataram no topo: 99,3% de acurácia e 98,1% de sensibilidade.** Isso é um único tumor maligno não detectado entre 53, e nenhum falso positivo. A Árvore de Decisão ficou bem abaixo, com 88,7% de sensibilidade. E repare: o melhor resultado coube ao modelo mais simples, a Regressão Logística, que já é interpretável por natureza.
>
> ▶ *(caixa da direita)* Mas eu não parei no teste único, e foi bom não parar. Na validação cruzada, a Regressão Logística cai de 99,3% para 97,3% de acurácia média: **aquela partição era otimista.** Os quatro modelos avançados ficam entre 96,0% e 97,3%. O teste de Friedman confirma que há diferença entre os cinco, mas o pós-hoc de Nemenyi mostra que ela está só na Árvore; **entre os quatro avançados, nenhuma diferença é significativa.**
>
> [pausa] Por isso, o software não elege um modelo único: oferece os cinco e o comitê."

▶ Avance.

**Frase-âncora:** "Empate no topo, e a validação cruzada mostrou que o teste único era otimista."

**Se perguntarem aqui:** Friedman com χ² = 65,766 e p = 1,775 × 10⁻¹³. No Nemenyi, a Árvore difere de todos (p de 0,0000 a 0,0004), e entre os quatro avançados o menor p é 0,1231.

---

### Slide 11. Qual erro é pior? (11:40 → 12:25, 45 s)

**Na tela:** os cartões Falso positivo (claro) e Falso negativo (vermelho), e 98,1% para RL e para SVM.

**Fala**

> "▶ *(olhe para a banca, não para o slide)* Agora, uma pergunta para a banca: **qual erro é pior?** Dizer que um paciente saudável está doente, ou dizer que um paciente com câncer está saudável? [pausa de 2 s]
>
> ▶ *(cartão da esquerda)* O falso positivo custa um exame a mais. ▶ *(cartão vermelho)* O falso negativo custa um tumor sem tratamento. Por isso, a métrica principal deste trabalho é a **sensibilidade**, a fração dos tumores malignos que o modelo detecta. E é também por isso que o software não usa o corte de 50%, que trata os dois erros como iguais: cada modelo decide com um limiar próprio, escolhido no treino, e com uma faixa de recusa."

▶ Avance.

**Frase-âncora:** "O falso negativo custa um tumor sem tratamento."

**Dica:** é o momento de mais contato com a banca. Faça a pergunta devagar e espere de verdade os 2 segundos.

---

### Slide 12. A certeza exibida é confiável? (12:25 → 13:30, 1 min 05 s)

**Na tela:** tabela de Brier e ECE dos quatro modelos e a caixa verde com a mensagem.

**Fala**

> "▶ Acertar não basta: a **certeza** que o sistema mostra também precisa ser confiável. Se ele diz 80% de chance de malignidade, entre os pacientes com essa certeza cerca de 80% devem de fato ser malignos.
>
> ▶ *(tabela)* Medi isso com duas métricas, em que menor é melhor. O escore de Brier é o erro quadrático médio entre a probabilidade prevista e o desfecho real. O ECE mede a distância média entre a confiança declarada e a acurácia observada. **O SVM é o melhor nas duas**: Brier de 0,0156 e ECE de 0,0306. A Regressão Logística tem bom Brier, mas o pior ECE: separa bem as classes, mas declara uma confiança desalinhada.
>
> ▶ *(caixa verde)* Por isso, no software, os quatro modelos com probabilidade são recalibrados com o escalonamento de Platt, e com ele o Brier da Regressão Logística cai para 0,0156, igual ao do SVM."

▶ Avance.

*Corte se estiver atrasado:* pule as duas frases que definem Brier e ECE.

**Frase-âncora:** "Se o sistema diz 80%, tem de ser 80% de verdade."

---

### Slide 13. Decidir ou devolver ao especialista (13:30 → 14:45, 1 min 15 s)

**Na tela:** a curva risco-cobertura à esquerda e os números 96 de 143, 47 e 67% a 74% à direita.

**Fala**

> "▶ *(gráfico)* Esta é a curva risco-cobertura, calculada no treino. No eixo horizontal está a fração de pacientes que o modelo aceita decidir; no vertical, o erro entre os decididos. ▶ *(percorra a curva com o dedo ou o ponteiro)* Ela fica perto de zero e só dispara no fim: **o erro não está espalhado, está concentrado num pequeno grupo de casos difíceis.** Decidindo 80% do treino, o erro fica entre 0,3% e 1,2%; decidindo todos, sobe para cerca de 6%.
>
> Então faz sentido o sistema se abster: os casos da faixa do meio voltam ao especialista com o rótulo Revisar. A faixa foi definida só com o treino, e a prova está no teste, que não participou da escolha. ▶ *(números)* O comitê decidiu **96 dos 143 pacientes sem nenhum erro** e devolveu 47, entre eles 5 malignos, que assim não receberam um falso 'benigno'. Os quatro modelos com faixa decidem entre 67% e 74% do teste sem erro. O custo é explícito: **cerca de um terço dos casos volta para revisão humana.**"

▶ Avance.

*Corte se estiver atrasado:* pule a frase dos eixos.

**Frase-âncora:** "Os erros se concentram em poucos casos difíceis, e o sistema devolve esses casos."

**Se perguntarem aqui:**
- **Os limites da faixa:** a faixa é [inferior; superior). No comitê, Benigno abaixo de 1,1%, Revisar de 1,1% a 68,2% e Maligno a partir de 68,2%.
- **Por que o KNN não tem faixa:** com k = 4, as probabilidades dele assumem poucos valores, e a faixa que zeraria os erros o faria decidir menos de 45% do treino.

---

### Slide 14. IA explicável: o que pesou na decisão (14:45 → 16:00, 1 min 15 s)

**Marco:** se chegar depois de **15:15**, use os cortes dos slides 15 e 16.

**Na tela:** gráfico de barras com a importância SHAP global do Random Forest e a caixa à direita.

**Fala**

> "▶ *(gráfico)* Agora, a explicabilidade. Esta é a importância global SHAP do Random Forest, tirada do próprio DiagnosisXAI. Os atributos que mais pesam são o perímetro e a área no pior valor da amostra, os pontos côncavos do contorno e o raio. **Pesam o tamanho do núcleo e as suas concavidades**, o que é coerente com as alterações morfológicas da malignidade. ▶ *(caixa)* E esse núcleo comum aparece em modelos diferentes: quatro dos seis atributos de maior coeficiente da Regressão Logística estão entre os seis de maior peso SHAP do Random Forest.
>
> Mas o principal é que **cada paciente recebe a sua explicação.** No software, o bloco 'Fatores que mais pesaram' agrupa os 30 atributos em 8 fatores e calcula os valores de Shapley exatos sobre a própria certeza calibrada; assim, a explicação fecha no número que o profissional vê. O UMAP situa o paciente no mapa da população, e a distância de Mahalanobis avisa quando ele foge do perfil de treino.
>
> [pausa] Uma ressalva: **o SHAP mostra o que o modelo usou, não a causa biológica do tumor.**"

▶ Avance.

**Frase-âncora:** "Cada paciente recebe a sua explicação, e ela fecha na certeza exibida."

**Se perguntarem aqui:**
- **Por que 8 fatores:** raio, perímetro e área têm correlação entre 0,98 e 0,998 no treino, então viraram um único fator, o tamanho do núcleo. Com 8 fatores há só 2⁸ = 256 coalizões, e o cálculo é exato, sem a amostragem do KernelExplainer.
- **"worst":** é o pior valor da medida na amostra. O texto chama de "valor máximo", mas na descrição original da base é a média dos três maiores valores.

---

### Slide 15. Validação do software (16:00 → 16:45, 45 s)

**Na tela:** três cartões (231, Autoteste e 100%).

**Fala**

> "▶ E como eu sei que o software faz o que deveria? Três evidências. ▶ *(cartão 1)* **231 testes automatizados** em pytest; entre eles, os que garantem que o diagnóstico exibido na tela é exatamente a decisão de cada modelo, um problema real que encontrei e corrigi no SVM e no KNN. ▶ *(cartão 2)* Um **modo de autoteste**, que percorre sem interface as 14 etapas do uso real e roda antes de publicar cada executável. ▶ *(cartão 3)* E a **auditoria contra o gabarito**: o comitê acertou 100% dos 96 casos que decidiu no teste."

▶ Avance.

*Corte se estiver atrasado:* "231 testes, um autoteste de 14 etapas e 100% de acerto nos 96 casos decididos."

**Frase-âncora:** "Testes, autoteste e auditoria."

---

### Slide 16. Alcance dos objetivos (16:45 → 17:30, 45 s)

**Na tela:** os quatro objetivos com marcas de conferido.

**Fala**

> "▶ *(percorra as quatro linhas)* Voltando aos quatro objetivos. Comparar classificadores: comparei cinco, e só a Árvore de Decisão se mostrou inferior. Avaliar com rigor: validação cruzada, testes de significância e calibração. Explicar cada decisão: SHAP por paciente, UMAP e sinalização de perfis atípicos. E o software funcional: o DiagnosisXAI, para Windows e Linux, com código e executáveis públicos no GitHub.
>
> [pausa] **A resposta à pergunta de pesquisa é que não basta acoplar uma técnica de explicabilidade a um classificador:** foi preciso combinar certeza calibrada, uma regra de decisão capaz de se abster e explicações coerentes com essa certeza."

▶ Avance.

*Corte se estiver atrasado:* "Os quatro objetivos foram atendidos." Depois diga direto a resposta à pergunta de pesquisa.

**Frase-âncora:** "Não basta acoplar XAI a um classificador."

---

### Slide 17. Importância dos resultados e dificuldades (17:30 → 18:30, 1 min)

**Marco:** se chegar depois de **18:00**, cite as três dificuldades em uma frase cada.

**Na tela:** à esquerda, a importância; à direita, as dificuldades.

**Fala**

> "▶ *(Importância)* Por que esses resultados importam? Primeiro: nesta base, **acurácia e transparência não precisaram ser trocadas**; o modelo mais simples e interpretável está entre os melhores. Segundo: o trabalho tem um rigor ausente nos trabalhos relacionados, e foi esse rigor que mostrou que uma partição única pode ser otimista. Terceiro: o sistema diz quão segura é a sua resposta e sabe se abster.
>
> ▶ *(Dificuldades)* Foram três as principais dificuldades. No SVM e no KNN, a decisão exibida divergia da decisão real do modelo: corrigi e criei testes para que isso não volte. Na calibração, a regressão isotônica teve o menor Brier no teste, mas escolhi o Platt, mais robusto em amostras pequenas. E no empacotamento, o PyInstaller só revelava módulos faltando com o programa rodando; resolvi com o autoteste e com a compilação automática no GitHub Actions."

▶ Avance.

**Frase-âncora:** "Acurácia e transparência não precisaram ser trocadas."

---

### Slide 18. Limitações e trabalhos futuros (18:30 → 19:15, 45 s)

**Na tela:** duas colunas (Limitações e Trabalhos futuros).

**Fala**

> "▶ *(Limitações)* O trabalho tem limites claros: usa uma única base, com 569 amostras; não passou por validação clínica; não processa imagens, porque depende dos atributos que o laboratório extrai; e cerca de um terço dos casos volta para revisão. A interpretabilidade foi tratada no plano técnico e ainda precisa ser confirmada pelos profissionais.
>
> ▶ *(Trabalhos futuros)* Por isso, os próximos passos são validar com dados hospitalares reais, e a arquitetura já permite recalcular limiares e faixas sem mexer na aplicação; avaliar a ferramenta com patologistas; segmentar os núcleos a partir das imagens; e investigar variáveis clínicas que ajudem a decidir parte dos casos hoje devolvidos."

▶ Avance.

**Frase-âncora:** "Uma base, sem validação clínica: o próximo passo é o hospital."

---

### Slide 19. Obrigado (19:15 → 19:30, 15 s)

**Fala**

> "Agradeço ao professor Rodrigo pela orientação e à banca pela avaliação. O código, o notebook e os executáveis estão no GitHub. Fico à disposição para as perguntas."

Pare de falar, sorria e espere. Deixe este slide na tela durante as perguntas.

---

## 5. Pronúncia dos termos que travam a língua

| Escrito | Fale |
|---|---|
| 10×5 | "dez por cinco" |
| 0,0156 | "zero vírgula zero um cinco seis" |
| 0,0306 / 0,0609 | "zero vírgula zero três zero seis" / "zero vírgula zero seis zero nove" |
| p ≈ 10⁻¹³ | "p da ordem de dez elevado a menos treze" |
| Z-score | "zê-escore" |
| KNN | "cá-ene-ene" |
| SHAP / UMAP | "xépi" / "iú-mépi" (ou "u-map"; escolha uma e mantenha) |
| Nemenyi | "nê-mê-nhi" |
| Platt | "plát" |
| wisconsin.pkl / limiares.json | "wisconsin ponto pê-cá-éle" / "limiares ponto jêison" |

---

## 6. Perguntas e respostas

Respostas curtas, de 30 a 60 segundos. As 70 perguntas completas, com os pontos-chave, estão em [03_perguntas_banca.md](03_perguntas_banca.md).

**Como responder**

1. Ouça a pergunta até o fim, sem interromper. Anote uma palavra-chave.
2. Agradeça e, se a pergunta for longa, reformule-a numa frase ("Se entendi bem, a pergunta é...").
3. Responda primeiro com a conclusão e depois com a justificativa. Se ajudar, volte ao slide correspondente.
4. Limitação reconhecida é ponto a favor: "Sim, é uma limitação, e por isso...".
5. Se não souber, diga: "Não avaliei isso no trabalho, mas o caminho seria...". Não invente números.

**As cinco que o orientador sugeriu**

1. **Por que a sensibilidade, e não a acurácia?** Porque o falso negativo é mais grave: custa um tumor sem tratamento, enquanto o falso positivo custa um exame a mais. Além disso, a base é desbalanceada (62,7% benignos), e a acurácia pode esconder erros na classe maligna. *(volte ao slide 11)*
2. **Por que não usar deep learning?** A base é pequena e tabular: 569 pacientes, 426 no treino, e 30 atributos já extraídos. Os modelos clássicos já chegam a 99% no teste e a cerca de 97% na validação cruzada. Uma rede profunda tenderia a sobreajustar e perderia a interpretabilidade, que é o foco do trabalho.
3. **O sistema substitui o médico?** Não. É um apoio à decisão: devolve cerca de um terço dos casos ao especialista, sinaliza os perfis atípicos e mostra a justificativa. A validação foi técnica; falta a avaliação com profissionais.
4. **Qual modelo você usaria na prática?** Os testes não separam os quatro avançados, então o software não elege um só: oferece os cinco e o comitê, que no teste decide 67,1% dos casos sem nenhum erro. Se fosse para escolher um, a Regressão Logística pela transparência ou o SVM pela calibração.
5. **Por que aparece um falso negativo na tabela do ponto de operação, se a faixa foi feita para ter erro zero no treino?** É arredondamento. Os limites são gravados no limiares.json com quatro casas decimais, e o arredondamento do limite inferior para cima faz um maligno, logo abaixo do limite, ser decidido como benigno. Com os limites exatos, não há erro no treino. No teste, que é a evidência que importa, os quatro modelos com faixa não erram.

**Outras que valem a pena ter prontas**

6. **Por que Platt, se a isotônica teve menor Brier?** A isotônica tem muito mais graus de liberdade e sobreajusta em amostras pequenas (Niculescu-Mizil e Caruana, 2005). Além disso, escolher o método pelo resultado no teste seria usar o teste para decidir.
7. **Como o limiar foi escolhido?** É o menor corte cuja especificidade out-of-fold no treino chega a 92%, com o Platt refeito dentro de cada dobra. O conjunto de teste não participa.
8. **Por que a detecção de perfis atípicos não ficou com o UMAP, como dizia a proposta?** A projeção em duas dimensões distorce as distâncias, e um paciente novo é posicionado pela média dos vizinhos de treino, então nunca cai fora da nuvem. A atipicidade passou a ser medida pela distância de Mahalanobis nos 30 atributos, com covariância de Ledoit-Wolf e corte no percentil 99.
9. **O que é o comitê, e por que a Árvore não entra nele?** É a média simples das certezas calibradas da Regressão Logística, do Random Forest, do SVM e do KNN. A Árvore fica de fora porque as folhas puras dão probabilidades 0 ou 1, sem calibração possível.
10. **O Friedman vale, se as dobras não são independentes?** As dobras compartilham dados, o que deixa os valores de p otimistas; por isso o Friedman e o Nemenyi são lidos como panorama, e o 5×2cv entra como complemento. E repare: se o p já é otimista e mesmo assim não houve diferença entre os quatro avançados, essa conclusão fica ainda mais segura.
11. **Por que XGBoost e redes neurais não estão no trabalho?** **Prepare a sua justificativa real**, porque eles estavam na versão de outubro. Argumentos que costumam ser aceitos: os quatro modelos já empatam no teto da base, e o ganho de Chen et al. (0,974) está dentro da variação da validação cruzada; o foco é explicar e calibrar, não maximizar a acurácia; e com 426 pacientes uma rede neural tende a sobreajustar. *(pergunta 24 do 03)*
12. **O SHAP mostra a causa do câncer?** Não. Mostra o que o modelo usou para chegar à certeza. E, entre atributos muito correlacionados, como raio, perímetro e área, a divisão do peso depende do modelo; por isso o software os junta num único fator.
13. **De onde veio a base?** Responda com o que você confirmou: UCI Machine Learning Repository, base Breast Cancer Wisconsin (Diagnostic), ou a cópia do Kaggle, se foi de lá que baixou o arquivo.
