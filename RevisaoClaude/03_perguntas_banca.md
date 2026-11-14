# 3. Setenta perguntas que a banca pode fazer

As perguntas estão em nove blocos, na ordem em que o trabalho se apresenta, para facilitar a montagem do roteiro e dos slides. Cada uma traz:

- **Onde:** a seção do trabalho que sustenta a resposta;
- **Pontos-chave:** o que a resposta precisa conter. Os números foram conferidos contra o notebook e o código.

As marcadas com 🎯 são as que considero **mais prováveis** (26 no total). As marcadas com ⚠️ tocam em pontos que o texto ainda trata de forma frágil; o arquivo `01_pendencias.md` traz a correção.

| Bloco | Tema | Perguntas |
|---|---|---|
| 1 | Problema, objetivo e contribuição | 1–7 |
| 2 | Base de dados e pré-processamento | 8–15 |
| 3 | Algoritmos e hiperparâmetros | 16–24 |
| 4 | Avaliação e testes estatísticos | 25–35 |
| 5 | Calibração, limiar e recusa | 36–45 |
| 6 | Explicabilidade | 46–54 |
| 7 | UMAP e perfis atípicos | 55–59 |
| 8 | Software e engenharia | 60–65 |
| 9 | Ética, limitações e futuro | 66–70 |

---

## Bloco 1. Problema, objetivo e contribuição

**1. 🎯 Em uma frase: qual é a contribuição do seu trabalho? O que ele faz que o de Shaon et al. (2024), o mais próximo, não faz?**
*Onde:* Seções 3.8 e 3.9; conclusão.
*Pontos-chave:* Shaon et al. usam o SHAP só como **filtro global de atributos** e param na análise. Aqui o SHAP explica **cada paciente**, sobre a mesma certeza que a tela mostra. Além disso, o trabalho testa estatisticamente as diferenças entre modelos (nenhum trabalho relacionado faz isso), calibra as probabilidades, permite ao sistema se abster e entrega um software instalável. Contribuição em uma frase: um sistema de apoio que é transparente quanto à própria incerteza.

**2. 🎯 Qual é a pergunta de pesquisa, e qual é a resposta?**
*Onde:* Introdução (problema); conclusão (4º parágrafo).
*Pontos-chave:* "Como integrar explicabilidade e redução de dimensionalidade a um modelo preditivo de modo que os diagnósticos sejam acurados e interpretáveis?" A resposta é que não basta acoplar o SHAP a um classificador. É preciso combinar certeza **calibrada**, uma regra de decisão capaz de **se abster**, explicações que **fecham** na certeza exibida e recursos que **situam** o paciente na população e avisam quando ele foge dela.

**3. 🎯 Se a Regressão Logística empatou com os modelos de caixa preta, por que manter SVM, Random Forest e o SHAP no sistema? Rudin (2019) não diria para usar só o modelo interpretável?**
*Onde:* Seções 2.4, 4.6.6 e 4.7.2. ⚠️ Ver o item 4 do `01_pendencias.md`: hoje o texto atribui a Rudin a ideia oposta.
*Pontos-chave:* concordar com Rudin e mostrar que o resultado do trabalho é **coerente** com ela: nesta base, a complexidade não trouxe ganho significativo. O sistema mantém os outros modelos porque (a) o empate vale para esta base e talvez não para outra; (b) comparar mecanismos diferentes é parte da contribuição; (c) o comitê dilui o erro de um membro e expõe a divergência entre eles. O SHAP serve também à RL: o bloco de fatores dá a todos os modelos a mesma linguagem de explicação.

**4. O objetivo geral foi atingido? O que ficou de fora?**
*Onde:* Conclusão.
*Pontos-chave:* sim, no plano técnico: o software está implementado, testado (231 testes) e distribuído como executável para Windows e Linux. Ficou de fora: a avaliação com patologistas, a validação em dados externos e o processamento de imagens (a segmentação dos núcleos).

**5. O que mudou entre a proposta e o que foi entregue? Por quê?**
*Onde:* Introdução (linha 208); Seções 4.7 e 4.8.
*Pontos-chave:* (a) a detecção de anomalias saiu do UMAP e passou à distância de Mahalanobis (ver pergunta 55); (b) entraram a calibração, o ponto de operação e a faixa de recusa, porque a certeza bruta não era confiável; (c) entraram o comitê e os executáveis; (d) XGBoost e redes neurais saíram (ver pergunta 24).

**6. Quem é o usuário do sistema e em que momento do fluxo clínico ele entra?**
*Onde:* Seções 2.1 e 4.8.
*Pontos-chave:* o patologista ou laboratório, depois da punção aspirativa por agulha fina (PAAF) e da extração dos 30 atributos das imagens. O sistema é uma **segunda opinião** que organiza a fila: decide os casos claros, devolve os duvidosos e sinaliza os atípicos. Não substitui o laudo; o LEIA-ME do executável diz isso explicitamente.

**7. Onde está a Ciência da Computação no trabalho, além da estatística?**
*Onde:* Seções 4.2 e 4.8.
*Pontos-chave:* a arquitetura desacoplada (notebook → artefatos → aplicação); o cálculo exato de Shapley por enumeração das 256 coalizões; a interpolação no UMAP; os 231 testes automatizados; o empacotamento multiplataforma com autoteste e integração contínua (GitHub Actions).

---

## Bloco 2. Base de dados e pré-processamento

**8. 🎯 De onde veio exatamente o arquivo que você usou? Qual versão?**
*Onde:* Seção 4.3. ⚠️ Ver o item 8 do `01_pendencias.md`.
*Pontos-chave:* a base é a WDBC, de Wolberg, Street e Mangasarian, no UCI Machine Learning Repository (DOI 10.24432/C5DW2B). O `data.csv`, com cabeçalho e a coluna `Unnamed: 32`, é o formato da cópia do Kaggle. Tenha a resposta exata (site e data do download).

**9. O que significam os sufixos _mean, _se e _worst? Como esses números foram obtidos?**
*Onde:* Seções 2.1 e 3.1.
*Pontos-chave:* para cada uma das 10 medidas do núcleo (raio, textura, perímetro, área, suavidade, compacidade, concavidade, pontos côncavos, simetria e dimensão fractal), calcula-se sobre os núcleos da imagem a **média**, o **erro padrão** e o **"pior" valor** (a média dos três maiores). São 10 × 3 = 30 atributos. Os contornos foram traçados com contornos ativos (*snakes*) sobre imagens de PAAF (Street et al., 1993). Cada linha da base é **uma amostra (um tumor)**, e não uma célula.

**10. Quantas colunas tinha o arquivo e por que você removeu duas?**
*Onde:* Seções 4.3 e 4.4.1.
*Pontos-chave:* são 33 colunas: `id`, `diagnosis`, 30 atributos e `Unnamed: 32`. O `id` é um identificador administrativo; deixá-lo como atributo permitiria ao modelo aprender um padrão espúrio. `Unnamed: 32` é uma coluna vazia, criada por uma vírgula sobrando no fim do cabeçalho do CSV. Restam 569 amostras e 31 colunas.

**11. A base é desbalanceada? Como você tratou isso?**
*Onde:* Seções 4.5.2 e 4.6.
*Pontos-chave:* levemente: 357 benignos (62,7%) e 212 malignos (37,3%). Tratamento: divisão estratificada (`stratify=y`), `class_weight='balanced'` (ou `balanced_subsample` no RF), métricas que não dependem da prevalência (sensibilidade, especificidade, PR-AUC) e o limiar ajustado. Não foi usado SMOTE (ver pergunta 21).

**12. Por que você não removeu os *outliers* que os boxplots mostraram?**
*Onde:* Seção 4.5.4.
*Pontos-chave:* nos tumores malignos, valores extremos são esperados, porque a morfologia agressiva é justamente o sinal. Removê-los seria apagar informação clínica. A atipicidade é tratada **na inferência** pela coluna Perfil (Mahalanobis).

**13. 🎯 Onde poderia ter ocorrido vazamento de dados (*data leakage*) e como você o evitou?**
*Onde:* Seções 4.4.3, 4.7.1 e 4.7.4.
*Pontos-chave:* (a) o padronizador é ajustado só no treino e, na validação cruzada, reajustado dentro de cada dobra (*pipeline*); (b) o limiar e a faixa de recusa são escolhidos com probabilidades *out-of-fold* do treino, e o teste não participa; (c) o calibrador é ajustado sobre previsões *out-of-fold*; (d) a Árvore de Decisão chegou a usar uma partição própria, sem estratificação; isso foi percebido e corrigido em outubro, e hoje todos os modelos usam a mesma partição.

**14. Raio, perímetro e área são quase a mesma medida. Essa colinearidade atrapalha?**
*Onde:* Seções 4.6.3 e 4.8.4.
*Pontos-chave:* a correlação entre eles vai de 0,98 a 0,998 no treino. Na RL, a colinearidade torna os coeficientes instáveis, por isso a regularização L2 forte (C = 0,1). No RF, o `max_features` sorteia atributos diferentes a cada divisão. Nas explicações, os três foram fundidos no fator "tamanho do núcleo", para que o peso não se espalhe artificialmente entre eles. Para a acurácia, a colinearidade não é um problema.

**15. 🎯 São 569 amostras, coletadas nos anos 1990, em uma única instituição. O modelo funciona em outro laboratório?**
*Onde:* Conclusão (limitações); Seção 4.8.7.
*Pontos-chave:* não há como garantir; é a principal limitação. Os atributos dependem do protocolo de captura e segmentação. Outro laboratório pode ter outra distribuição, e as probabilidades perderiam a calibração. A arquitetura permite retreinar e recalibrar sem mexer na aplicação, e a coluna Perfil acusa pacientes fora da distribuição de treino. Trabalho futuro: validação externa.

---

## Bloco 3. Algoritmos e hiperparâmetros

**16. Por que esses cinco algoritmos?**
*Onde:* Seção 4.6.
*Pontos-chave:* um representante de cada família: regras (Árvore de Decisão), distância/memória (KNN), linear probabilístico (RL), comitê de árvores (RF) e margem (SVM). Todos são comuns na literatura de diagnóstico assistido por computador e permitem comparar mecanismos de explicação diferentes.

**17. A Árvore de Decisão sem poda não é um *baseline* fraco de propósito?**
*Onde:* Seção 4.6.1.
*Pontos-chave:* a Árvore é o modelo **interpretável por excelência**, e o *baseline* mede quanto a complexidade dos outros acrescenta. Sem poda ela cresce até folhas puras (profundidade 7, 18 folhas) e acerta os 426 pacientes do treino, o que mostra o sobreajuste. Uma árvore podada seria mais justa. Admitir isso e citá-lo como melhoria possível é melhor do que defender a escolha.

**18. 🎯 Como você escolheu os hiperparâmetros? Houve uma busca sistemática?**
*Onde:* Seções 4.6.2 a 4.6.5.
*Pontos-chave:* seja honesto. O KNN foi escolhido por validação cruzada de 5 dobras no treino (k = 4, com ponderação por distância e Manhattan, contra k = 20 com voto uniforme). Na RL, C = 0,1 por causa da colinearidade. No RF, as restrições de profundidade e folha contêm o sobreajuste. O SVM ficou nos padrões (C = 1, `gamma='scale'`). Não houve *grid search* com validação cruzada aninhada. Como os modelos já empatam estatisticamente, ajustar mais arriscaria sobreajustar uma base pequena. A validação aninhada é uma melhoria possível.

**19. Por que k = 4, um número par, se a teoria recomenda k ímpar?**
*Onde:* Seção 4.6.2.
*Pontos-chave:* com ponderação por distância, um empate exigiria que a soma dos pesos das duas classes fosse exatamente igual, o que, com distâncias contínuas, praticamente não acontece. A escolha veio da validação cruzada. Manhattan foi usada por ser menos sensível a uma única medida discrepante (não eleva as diferenças ao quadrado).

**20. Por que o SVM usou C e gamma padrão?**
*Onde:* Seção 4.6.5.
*Pontos-chave:* com os padrões, o SVM já alcança ROC-AUC de 0,995 na validação cruzada e empata com os demais. Explique o que cada um faz: C controla a tolerância a erros de margem (margem flexível); gamma, o alcance de influência de cada vetor de suporte no RBF (`'scale'` = 1 / (n_atributos × variância)).

**21. Por que `class_weight='balanced'` e não SMOTE?**
*Onde:* Seções 3.5 e 4.6.3.
*Pontos-chave:* o desbalanceamento é leve. A ponderação ajusta o custo dos erros sem criar pacientes sintéticos, que numa base médica pequena podem gerar perfis irreais. E é mais simples de explicar e reproduzir.

**22. Por que entropia e não Gini, que é o padrão do scikit-learn?**
*Onde:* Seções 2.3.4, 4.6.1 e 4.6.4.
*Pontos-chave:* por coerência com a fundamentação (ganho de informação, ID3/C4.5) e para que a comparação Árvore × RF isole o efeito do comitê. Na prática, os dois critérios costumam produzir árvores muito parecidas. A janela do RF mostra a importância como "redução média de entropia (MDI)" justamente porque o critério é a entropia.

**23. ⚠️ Como o Random Forest decide: por votação majoritária ou pela média das probabilidades? Quantos atributos ele sorteia por divisão?**
*Onde:* Seções 2.3.4 e 4.6.4.
*Pontos-chave:* no scikit-learn, pela **média das probabilidades** das 500 árvores (voto suave). A votação majoritária é a formulação clássica de Breiman. O `max_features='sqrt'` sorteia **5** atributos (a parte inteira de √30 ≈ 5,48), e não "aproximadamente seis", como diz o texto atual.

**24. 🎯 Os trabalhos relacionados usam XGBoost e redes neurais, e Chen et al. tiveram o XGBoost como melhor modelo. Por que eles não estão no seu trabalho?**
*Onde:* Seção 3.7 (Chen et al.).
*Pontos-chave:* **prepare a sua justificativa real** (o commit de 07/11 os retirou do texto). Argumentos que costumam ser aceitos: (a) os quatro modelos já empatam no teto da base (ROC-AUC ≈ 0,99), e o ganho de Chen et al. (acurácia 0,974) está dentro da variação da validação cruzada (DP ≈ 0,02); (b) o foco do trabalho é explicar e calibrar, e não maximizar a acurácia; (c) com 426 pacientes, uma rede neural tende a sobreajustar; (d) o software precisava de um explicador nativo para cada modelo. Se a banca leu a versão de outubro, que os incluía, ela pode perguntar o que mudou.

---

## Bloco 4. Avaliação e testes estatísticos

**25. 🎯 Por que a acurácia no teste (0,993) é maior que na validação cruzada (0,973)?**
*Onde:* Seção 4.7.1.
*Pontos-chave:* aquela partição única foi favorável. Com 143 pacientes, **um erro vale 0,7 ponto percentual** de acurácia, e um maligno a mais ou a menos vale 1,9 ponto de sensibilidade (53 malignos). A validação cruzada (50 ajustes) mede a variação: os desvios-padrão de cerca de 0,02 a 0,04 mostram que diferenças de um ou dois acertos não significam nada.

**26. Você usou o conjunto de teste várias vezes (Tabelas 1, 5, 6 e 7). Isso não o contamina?**
*Onde:* Seções 4.6.6, 4.7.3 e 4.7.4.
*Pontos-chave:* o teste foi usado só para **reportar**, nunca para **escolher**. O limiar e a faixa vieram do treino (*out-of-fold*). O método de calibração foi escolhido pela literatura, e a prova é que a isotônica, **melhor no teste**, foi descartada. Os hiperparâmetros vieram do treino.

**27. Por que reportar a PR-AUC se o desbalanceamento é leve?**
*Onde:* Seção 2.3.3.
*Pontos-chave:* a curva ROC usa a taxa de falsos positivos, normalizada pelos negativos, que são a maioria; a curva PR olha diretamente a classe de interesse, a maligna (Davis e Goadrich, 2006; Saito e Rehmsmeier, 2015). Com 37% de malignos, as duas contam praticamente a mesma história: é complemento, não substituição.

**28. ⚠️ Defina especificidade. Por que ela é o critério do limiar, e não a precisão?**
*Onde:* Seção 4.7.4. A especificidade ainda não está definida na fundamentação (item 12 do `01_pendencias.md`).
*Pontos-chave:* especificidade = VN / (VN + FP), a proporção de benignos reconhecidos como benignos. A especificidade não depende da prevalência; a precisão depende (muda se a proporção de malignos no lote mudar). Por isso o piso foi posto na especificidade.

**29. 🎯 Explique o teste 5×2cv de Dietterich. Por que não um teste t comum sobre as 50 dobras?**
*Onde:* Seção 4.7.2.
*Pontos-chave:* nas 50 dobras, os conjuntos de treino se sobrepõem, então as estimativas não são independentes, e o teste t comum subestima a variância e acusa diferenças que não existem (erro tipo I alto). O 5×2cv faz 5 repetições de validação cruzada de 2 dobras (treinos disjuntos dentro de cada repetição) e usa uma estatística t com 5 graus de liberdade. É conservador (pouco poder).

**30. 🎯 Por que o 5×2cv não viu diferença entre RL e Árvore (p = 0,066), mas o Nemenyi viu?**
*Onde:* Seção 4.7.2.
*Pontos-chave:* questão de poder. O 5×2cv tem só 10 estimativas de diferença, cada uma treinando com metade dos dados. O Nemenyi usa as posições (*ranks*) nas 50 dobras, e a Árvore é quase sempre a pior. Os dois não se contradizem: um tem pouco poder; o outro tende a ser otimista, porque as dobras são dependentes. A conclusão segura é que a Árvore é inferior; a conclusão sobre os quatro restantes é que não se distinguem.

**31. No teste de Friedman, quais são os blocos? Isso respeita a independência que o teste supõe?**
*Onde:* Seção 4.7.2 (pedido da professora, já respondido no texto).
*Pontos-chave:* os blocos são as 50 dobras da validação cruzada 10×5, e cada dobra fornece a acurácia dos cinco modelos. **Não** respeitam a independência: Demšar (2006) recomenda usar **bases de dados diferentes** como blocos. Por isso o resultado é lido como panorama, e não como prova (χ² = 65,77, p ≈ 1,8 × 10⁻¹³).

**32. O que o pós-hoc de Nemenyi compara? O que é a distância crítica?**
*Onde:* Seção 4.7.2.
*Pontos-chave:* compara os **postos médios** dos modelos. Dois modelos diferem se a diferença de postos médios supera a distância crítica CD = q_α · √(k(k+1)/(6N)). Com k = 5 modelos, N = 50 blocos e q₀,₀₅ ≈ 2,728, CD ≈ 0,86 posto.

**33. Você fez correção para comparações múltiplas nos quatro testes 5×2cv?**
*Onde:* Tabela 3.
*Pontos-chave:* não, e nesse caso não mudaria nada: nenhuma das quatro comparações foi significativa nem a 5%. Com Bonferroni (α = 0,05/4 = 0,0125), continuariam não significativas. O Nemenyi já controla o erro para as comparações múltiplas.

**34. 🎯 "Sem diferença significativa" quer dizer que os modelos são iguais?**
*Onde:* Seção 4.7.2.
*Pontos-chave:* não. Ausência de evidência não é evidência de ausência. O teste tem pouco poder com 426 pacientes. Para afirmar equivalência, seria preciso um teste de equivalência, com margem definida antes. A frase correta é "nesta base, os dados não permitem afirmar que um seja superior".

**35. Por que priorizar a sensibilidade? Qual é o custo disso?**
*Onde:* Seção 4.7.4.
*Pontos-chave:* o falso negativo custa um tumor sem tratamento; o falso positivo, um exame a mais. O custo aparece nos números: sem recusa, no limiar de 0,151, a RL troca 1 FN e 0 FP (no corte de 0,5, com a probabilidade bruta) por 1 FN e 6 FP no teste. O piso de 92% de especificidade é o freio que impede o limiar de acusar todo mundo.

---

## Bloco 5. Calibração, limiar e recusa

**36. 🎯 O que é calibração e por que ela importa num sistema clínico?**
*Onde:* Seção 4.7.3.
*Pontos-chave:* um modelo está calibrado quando, entre os pacientes a quem ele dá 70% de certeza, cerca de 70% são de fato malignos. Como a tela mostra a certeza ao médico, uma certeza mal calibrada induz decisões erradas, mesmo que a acurácia seja alta (Guo et al., 2017).

**37. Qual a diferença entre o escore de Brier e o ECE? Por que a RL tem um bom Brier e o pior ECE?**
*Onde:* Seção 4.7.3.
*Pontos-chave:* o Brier é o erro quadrático médio entre a probabilidade e o desfecho; mistura discriminação e calibração. O ECE separa as previsões em 10 faixas e mede a distância média entre a confiança e a acerto observado; isola a calibração. A RL separa muito bem as classes (bom Brier), mas suas probabilidades são deslocadas (ECE ruim). Explicação provável, que você pode conferir no diagrama de confiabilidade da célula 39: o `class_weight='balanced'` aumenta artificialmente o peso dos malignos, o que infla a probabilidade de malignidade, e a regularização forte (C = 0,1) puxa as probabilidades para perto de 0,5. Lembrete: o ECE foi calculado em 143 pacientes com 10 faixas, o que dá poucos pacientes por faixa e uma estimativa ruidosa.

**38. Por que escolher Platt, se a regressão isotônica teve o melhor Brier?**
*Onde:* Seção 4.7.3.
*Pontos-chave:* a isotônica é uma função em degraus com muitos graus de liberdade e, em bases pequenas, sobreajusta o conjunto de calibração (Niculescu-Mizil e Caruana, 2005). O Platt ajusta só dois parâmetros (uma sigmoide) e é monotônico, então preserva a ordem dos pacientes. Escolher a isotônica **por ter sido melhor no teste** seria usar o teste para decidir.

**39. 🎯 Em que dados o calibrador foi ajustado? Não há vazamento?**
*Onde:* Seção 4.7.3.
*Pontos-chave:* `CalibratedClassifierCV(method='sigmoid', cv=5, ensemble=False)`: o calibrador é ajustado sobre as previsões ***out-of-fold*** de 5 dobras do treino, e o modelo final é treinado em todo o treino. O teste não participa.

**40. Na Tabela 6, o Platt piorou o SVM (Brier de 0,0156 para 0,0213), mas no software o SVM calibrado ficou em 0,0156. Por quê?**
*Onde:* Seção 4.7.3 (parágrafo após a Tabela 6, já corrigido).
*Pontos-chave:* na Tabela 6 foi usado `ensemble=True` (cinco SVMs, cada um treinado em 80% dos dados, com a média das cinco probabilidades). No software, `ensemble=False` (um único SVM em 100% do treino, calibrado uma vez). Testei as combinações: `probability=True` ou `False` não muda nada (o calibrador sempre usa a função de decisão); o que muda o resultado é o `ensemble`.

**41. 🎯 Como foi escolhido o limiar de operação? Por que 92% de especificidade?**
*Onde:* Seção 4.7.4.
*Pontos-chave:* é o **menor** limiar cuja especificidade *out-of-fold* no treino chega a 92%, o que, entre os limiares aceitáveis, dá a maior sensibilidade. Os 92% são uma **escolha de projeto**, não um resultado: um piso que impede o limiar de descer até acusar todos. Por exemplo, se o critério fosse só "sensibilidade ≥ 98%", sem piso, o KNN cairia para 36% de especificidade no treino (docstring do `calibrar_limiares.py`). O script aceita outro piso (`--piso`). Diga que, numa implantação real, esse valor seria definido com os médicos.

**42. 🎯 Se a faixa de recusa foi construída para não errar no treino, por que a Tabela 7 mostra um falso negativo?**
*Onde:* Seção 4.7.4.
*Pontos-chave:* com os limites exatos, não há nenhum erro. O `limiares.json` grava os limites com 4 casas, e o limite inferior é **arredondado para cima** em alguns modelos. Com isso, o maligno de menor certeza fica logo abaixo do limite e é decidido como benigno. Isso ocorre na RL, no SVM e no comitê. A correção é arredondar o limite inferior para baixo. Tenha uma resposta pronta para "por que não corrigiu?" (ver a seção "O que depende de você" do `01_pendencias.md`).

**43. Os limites da faixa estão dentro ou fora dela?**
*Onde:* Seção 4.7.4 (item 6 do `01_pendencias.md`).
*Pontos-chave:* a faixa é [inferior; superior). Certeza abaixo do inferior → Benigno; entre os dois, incluindo o inferior → Revisar; a partir do superior → Maligno. O superior é gravado 0,0001 acima do benigno de maior certeza, para que esse benigno não seja decidido. No comitê: Benigno abaixo de 1,1%; Revisar de 1,1% a 68,2%; Maligno a partir de 68,2%.

**44. 🎯 Devolver cerca de um terço dos pacientes não torna o sistema inútil?**
*Onde:* Seção 4.7.4 (curva risco-cobertura).
*Pontos-chave:* o custo é explícito e controlável. A curva mostra que o erro se concentra em poucos casos difíceis. Aceitando errar 1% por classe, a cobertura no treino sobe de 60% para cerca de 90% na RL, com 2 FN e 3 FP (saída do `calibrar_limiares.py`). Tolerância zero foi uma escolha conservadora. O operador pode desligar a recusa, e um sistema que decide dois terços sem erro e devolve o resto já reduz a carga de trabalho.

**45. 🎯 No teste, os modelos com faixa não erraram nenhum caso decidido. Isso prova que o sistema não erra?**
*Onde:* Seção 4.7.4.
*Pontos-chave:* não. Zero erros em cerca de 100 casos decididos (96 no comitê) é compatível com uma taxa real de erro de até ~3%, com 95% de confiança (regra de três: 3/n ≈ 3/96 ≈ 3,1%). A faixa também foi ajustada com tolerância zero sobre as mesmas probabilidades em que foi avaliada no treino, então o desempenho no treino é esperado por construção. A evidência honesta é o teste, que é pequeno.

---

## Bloco 6. Explicabilidade

**46. 🎯 Explique o valor de Shapley com um exemplo do seu sistema.**
*Onde:* Seções 2.5 e 4.8.4.
*Pontos-chave:* a predição é o "prêmio"; os fatores são os "jogadores". O valor de cada fator é a média da sua contribuição marginal em todas as ordens possíveis de entrada na coalizão. Exemplo: a certeza média do treino é ~37%; para um paciente com 90%, o bloco mostra quanto cada fator somou (tamanho do núcleo +30 pontos, concavidade +15 pontos...) até fechar em 90%. A propriedade que importa é a **aditividade**: a base mais a soma das contribuições dá exatamente a certeza da tabela.

**47. Por que agrupar as 30 colunas em 8 fatores? Isso não esconde informação?**
*Onde:* Seção 4.8.4.
*Pontos-chave:* (a) colinearidade: raio, perímetro e área somam a mesma informação, e o SHAP dividiria o peso entre eles de forma arbitrária; (b) com 8 fatores há só 2⁸ = 256 coalizões, então o Shapley é **exato**, por enumeração, sem amostragem; (c) é mais legível para o médico. Nada se perde: a janela SHAP continua mostrando as 30 colunas.

**48. Qual é a diferença entre o bloco "Fatores que mais pesaram" e a janela SHAP? Por que mostrar dois números?**
*Onde:* Seção 4.8.4.
*Pontos-chave:* o bloco de fatores explica a **certeza calibrada** (o número da tabela), com 8 fatores e valores exatos. A janela SHAP explica a **probabilidade antes da calibração**, em 30 colunas, exata na Árvore e no RF (TreeExplainer) e aproximada na RL, no SVM e no KNN (KernelExplainer). Por isso a janela mostra os dois números lado a lado, cada um com seu nome.

**49. Por que usar o KernelExplainer na Regressão Logística, se existe o LinearExplainer, que é exato?**
*Onde:* Seção 4.8.4.
*Pontos-chave:* o LinearExplainer explica a saída linear (o *log-odds*). O trabalho quis explicar a **probabilidade**, que passa pela sigmoide e já não é linear, e na mesma escala do SVM e do KNN. É uma troca: comparabilidade em vez de exatidão. O bloco de fatores, que é exato, cobre a explicação principal.

**50. O que é o "valor-base" (*background*) do SHAP e como ele afeta a explicação?**
*Onde:* Seção 4.8.4.
*Pontos-chave:* "retirar" um atributo significa substituí-lo por valores de referência. No KernelExplainer, a referência são 25 centroides (k-means) do treino; no bloco de fatores, o ponto de partida é a certeza média do modelo no treino (~37,3%, perto da prevalência). Outra referência mudaria os valores: a explicação é sempre relativa a uma população.

**51. 🎯 O SHAP mostra a causa do câncer?**
*Onde:* Seção 4.8.4; conclusão (limitações).
*Pontos-chave:* não. Mostra o que **o modelo usou** para chegar à certeza. Com atributos correlacionados, o crédito pode ir para um ou para outro sem relação com a biologia. O que dá confiança clínica é a concordância com o conhecimento médico: tamanho do núcleo e concavidades são alterações associadas à malignidade.

**52. A RL e o RF concordaram só em parte nos atributos mais importantes. Isso não enfraquece a explicabilidade?**
*Onde:* Seção 4.6.3.
*Pontos-chave:* dos 6 atributos de maior peso, 4 são comuns (perimeter_worst, area_worst, radius_worst e concave points_mean), todos ligados a tamanho e concavidade. O que muda é a ordem entre atributos colineares, porque cada modelo distribui o peso de um jeito. O núcleo comum é estável, e é isso que importa clinicamente. Esse resultado também justifica o agrupamento em fatores.

**53. Como o comitê é explicado, se ele não tem coeficientes nem regras?**
*Onde:* Seção 4.8.4.
*Pontos-chave:* como a certeza do comitê é a média das certezas dos quatro membros e o valor de Shapley é linear, os fatores do comitê são exatamente a média dos fatores dos membros. A janela própria do comitê mostra a **concordância**: quem votou o quê e por que um caso foi devolvido (divergência entre os membros, proximidade da fronteira ou conservadorismo da política). Limitação: quando os membros discordam, a média esconde a divergência; por isso o relatório de cada membro continua disponível.

**54. 🎯 Como você sabe que as explicações são compreensíveis e úteis para um patologista?**
*Onde:* Conclusão.
*Pontos-chave:* não sei, e o trabalho diz isso: a validação foi técnica. O que se pode afirmar é que as explicações são **corretas** (fecham na certeza exibida, e os testes conferem) e **coerentes** com a morfologia. O próximo passo é um estudo com usuários: tarefas com casos reais, tempo, concordância e confiança, antes e depois de ver a explicação.

---

## Bloco 7. UMAP e perfis atípicos

**55. 🎯 Por que o UMAP deixou de ser usado para detectar anomalias?**
*Onde:* Introdução (linha 208); Seção 4.8.4.
*Pontos-chave:* o app não reajusta o UMAP a cada lote nem usa o umap-learn em tempo de execução: um paciente novo é posicionado pela média ponderada das posições dos seus vizinhos de treino, o que é rápido e determinístico. Por construção, então, ele **nunca cai fora da nuvem**, mesmo sendo muito diferente. E mesmo o `transform()` da biblioteca não resolveria, porque a projeção em 2D distorce as distâncias: "longe no mapa" não é uma medida confiável de "atípico". A atipicidade passou a ser medida no espaço completo de 30 dimensões, pela distância de Mahalanobis.

**56. ⚠️ Quais hiperparâmetros do UMAP você usou, e por quê?**
*Onde:* Seção 2.6 (Código 1) e célula 48 do notebook. Ver o item 13 do `01_pendencias.md`.
*Pontos-chave:* `n_neighbors=15`, `min_dist=0.1` (os padrões da biblioteca), `random_state=42`, ajustado só nos 426 pacientes de treino. O Código 1 do Cap. 2 mostra 65 e 0,0, que são valores ilustrativos, inspirados em Bollon et al.; deixe isso claro no texto. `n_neighbors` equilibra a estrutura local e a global; `min_dist` controla o quanto os pontos se compactam.

**57. Dá para ler as distâncias no mapa UMAP? Dois grupos distantes no mapa são muito diferentes?**
*Onde:* Seção 2.6. ⚠️ Ver o item 4 do `01_pendencias.md` (frase da p. 41).
*Pontos-chave:* não. O UMAP preserva vizinhanças (topologia), e não distâncias. O tamanho dos grupos e a distância entre eles no mapa não têm significado métrico. O mapa serve para **situar** o paciente ("ele está entre os malignos"), não para medir quão diferente ele é.

**58. Por que a distância de Mahalanobis, e não a euclidiana? Por que Ledoit-Wolf e o percentil 99?**
*Onde:* Seção 4.8.3.
*Pontos-chave:* a Mahalanobis, d² = (x − μ)ᵀ Σ⁻¹ (x − μ), leva em conta a correlação entre atributos: um paciente com raio grande e área pequena é estranho, mesmo que cada valor isolado seja normal. Estimar uma covariância 30 × 30 com 426 pacientes é instável e difícil de inverter; o encolhimento de Ledoit-Wolf estabiliza a estimativa. O percentil 99 do treino é um corte empírico: **por construção, 1% dos pacientes de treino** são marcados como atípicos. "Atípico" significa "fora do que o modelo viu", e não "maligno".

**59. Por que não desenhar a fronteira do SVM sobre o mapa UMAP?**
*Onde:* Seção 4.8.4.
*Pontos-chave:* o UMAP não tem inversa exata (o umap-learn oferece só uma aproximação), então não dá para avaliar a função de decisão num ponto qualquer do plano, só interpolar a partir dos vizinhos. Na validação *leave-one-out*, a interpolação acerta o lado da fronteira em ~96% dos casos, mas desenharia metade dos pacientes da margem (|z| < 1) fora dela, ou seja, erraria justamente os casos limítrofes. Por isso a margem é mostrada num painel próprio, cujo eixo é o próprio escore z.

---

## Bloco 8. Software e engenharia

**60. 🎯 Explique a arquitetura: como o notebook e o aplicativo se comunicam?**
*Onde:* Seção 4.2 (Figura 8).
*Pontos-chave:* são dois módulos desacoplados. O notebook treina e grava três artefatos: o `wisconsin.pkl` (modelos, versões calibradas, padronizador, explicadores e partições), o `limiares.json` (gerado pelo `calibrar_limiares.py`) e o `umap_train_2d.npy`. O app só carrega esses arquivos e faz inferência local. Para retreinar, basta rodar o notebook e o script, sem mudar o código do app. Os explicadores ficam em `app/core/explainers.py` e são serializados por referência, então o notebook e o app executam o mesmo código.

**61. 🎯 Que divergência entre a decisão exibida e a decisão do classificador você encontrou? Como os testes evitam que ela volte?**
*Onde:* Seção 4.8.1; conclusão.
*Pontos-chave:* **confirme o caso concreto no seu histórico.** Uma causa conhecida no SVM: com `probability=True`, o `predict()` usa o sinal da função de decisão, enquanto o `predict_proba()` vem de um Platt interno; os dois podem discordar perto da fronteira (a documentação do scikit-learn avisa disso). Hoje o diagnóstico sai da **mesma** probabilidade calibrada que a tela mostra, comparada aos cortes do `limiares.json`. Os testes treinam modelos na hora e verificam, paciente a paciente, que o rótulo exibido corresponde à decisão real.

**62. O que os 231 testes automatizados cobrem?**
*Onde:* Seção 4.8.1.
*Pontos-chave:* testes **isolados**, que treinam modelos na hora com a base pública do scikit-learn e conferem a decisão exibida, a política de recusa, a validação da planilha, os fatores, os PDFs e o memorial de cálculo; e testes de **integração**, que usam o próprio `wisconsin.pkl` versionado, conferem que o bloco de fatores fecha na certeza exibida e acusam mudanças no formato do artefato.

**63. Por que PyInstaller e GitHub Actions? O que o autoteste verifica?**
*Onde:* Seção 4.8.6.
*Pontos-chave:* o PyInstaller dispensa a instalação do Python, mas só empacota o que enxerga nas importações e só gera executável para o sistema em que roda. Daí o GitHub Actions, que compila em máquinas Windows e Linux a cada tag `v*`. O `--autoteste` percorre sem interface as 14 etapas do uso real e interrompe o empacotamento se alguma falhar, porque um módulo faltando só aparece com o programa rodando.

**64. Usar pickle não é um risco? E se a versão do scikit-learn mudar?**
*Onde:* Seção 4.3.
*Pontos-chave:* dois riscos reais. (a) **Compatibilidade:** um objeto do scikit-learn gravado numa versão pode não abrir em outra; por isso as versões exatas estão fixadas em `requirements-executavel.txt`, e o executável leva o ambiente junto. (b) **Segurança:** carregar um pickle executa código, então o app só deve abrir o `wisconsin.pkl` distribuído com ele, nunca um arquivo de terceiros. Uma alternativa futura seria o skops ou o ONNX.

**65. Se eu rodar tudo de novo, obtenho exatamente os mesmos números?**
*Onde:* Seção 4.1 (reprodutibilidade).
*Pontos-chave:* as sementes são fixas (`RANDOM_STATE = 42`), a partição é a mesma e o padronizador é ajustado no treino. Rodando de novo o script de limiares em outra máquina, RL, SVM e KNN reproduziram a Tabela 7 exatamente. O Random Forest pode variar na terceira casa decimal entre sistemas operacionais e versões: rodando o script no Mac, o limiar do RF deu 0,123, e não 0,1205. Por isso o ambiente está fixado, e o executável carrega o modelo já treinado, em vez de retreiná-lo.

---

## Bloco 9. Ética, limitações e futuro

**66. Como o sistema trata a privacidade dos pacientes (LGPD)?**
*Onde:* Seção 4.2; conclusão.
*Pontos-chave:* todo o processamento é local, e nenhum dado vai para servidor. Dados de saúde são **dados pessoais sensíveis** na LGPD (Lei 13.709/2018, art. 5º, II, e art. 11). Limitação a admitir: o histórico e os PDFs ficam gravados sem criptografia na pasta do usuário. Numa implantação real, isso exigiria controle de acesso, anonimização e uma política de retenção.

**67. 🎯 O sistema poderia ser usado num hospital hoje? O que faltaria?**
*Onde:* Conclusão; LEIA-ME do executável.
*Pontos-chave:* não; é um software acadêmico. Faltariam: validação externa e prospectiva, em outras instituições e no fluxo real; estudo com usuários; integração com o processo de extração dos atributos do laboratório; e regularização na Anvisa como *software* como dispositivo médico (RDC 657/2022), com gestão de risco e rastreabilidade.

**68. Se o sistema errar e o médico seguir a recomendação, de quem é a responsabilidade? Uma explicação não pode fazer o médico confiar demais?**
*Onde:* Seções 2.4 e 4.8.3.
*Pontos-chave:* a decisão e a responsabilidade são do profissional; o sistema é apoio. O risco de **viés de automação** (confiar demais na máquina) existe, e o desenho do sistema tenta reduzi-lo: certeza calibrada em vez de um rótulo seco, recusa explícita nos casos duvidosos, aviso de perfil atípico e explicação que mostra a base da decisão. Medir se isso funciona exige o estudo com usuários.

**69. Quais são as principais limitações do trabalho?**
*Onde:* Seção 4.8.7; conclusão.
*Pontos-chave:* (a) base pequena (569 amostras), de uma população e de uma época; (b) sem validação externa; (c) atributos já extraídos: o sistema não processa imagens e depende do protocolo do laboratório; (d) as explicações mostram o que o modelo usou, não a causa biológica, e os valores SHAP da RL, do SVM e do KNN são aproximados; (e) sem avaliação com profissionais; (f) a recusa devolve cerca de um terço do lote de teste.

**70. 🎯 Se você tivesse mais seis meses, o que faria primeiro?**
*Onde:* Conclusão (trabalhos futuros).
*Pontos-chave:* (1) validação externa, retreinando e recalibrando os limiares, o que a arquitetura já permite; (2) estudo com patologistas sobre a utilidade das explicações e a aceitabilidade da taxa de devolução; (3) segmentação dos núcleos, para receber direto a imagem da punção; (4) variáveis clínicas para decidir parte dos casos hoje devolvidos. Melhorias técnicas menores: validação cruzada aninhada para os hiperparâmetros, recusa com tolerância calibrada e a correção do arredondamento da faixa.

---

## Sugestão de uso para o roteiro

As 26 perguntas marcadas com 🎯 cobrem a espinha da apresentação: problema → base → modelos → avaliação → calibração e recusa → explicabilidade → software → limitações. Um caminho possível para os slides:

1. **Problema e pergunta** (perguntas 1, 2 e 3)
2. **Base e cuidados com vazamento** (8, 13 e 15)
3. **Modelos e comparação honesta** (18, 24, 25, 29, 30 e 34)
4. **Calibração, limiar e recusa** (36, 39, 41, 42, 44 e 45)
5. **Explicabilidade no software**, com demonstração (46, 51, 54 e 55)
6. **Arquitetura e engenharia** (60 e 61)
7. **Limitações e próximos passos** (67 e 70)

Responder às perguntas 3, 30, 42 e 45 **antes** que a banca as faça (num slide de "limitações e cuidados", por exemplo) costuma passar boa impressão: mostra que você conhece os pontos fracos do próprio trabalho.
