# RevisaoClaude: revisão do TCC para a entrega de 14/11/2026

Revisão feita em 08/11/2026 sobre o `trabalho.tex` do commit `02ed0b2` e o repositório DiagnosisXAI do GitHub (commit `22cbe5a`).

| Arquivo | Conteúdo |
|---|---|
| `01_pendencias_email.md` | O que ainda falta do e-mail da professora, item a item, com os blocos Procure / Substitua por |
| `apendices_A_B.tex` | Texto pronto dos Apêndices A (instalação) e B (uso), que a professora pediu e ainda não existem |
| `02_revisao_completa.md` | Revisão do trabalho inteiro (conceitos, coerência, escrita, ABNT, referências e entrega), com prioridade em cada item |
| `03_perguntas_banca.md` | 70 perguntas prováveis da banca, com onde está a resposta no texto e os pontos-chave de cada uma |

Todos os blocos de correção dos arquivos `01` (32) e `02` (87) foram aplicados numa cópia do projeto, junto com a troca no `.sty` (D10) e a expressão regular do D12, e compilados: todos os trechos existem no `trabalho.tex` atual, e o resultado compila sem erro, sem estouro de margem novo e com a conclusão em 3 páginas. Aplique o `01` antes do `02`.

## Prioridades até 14/11

**Obrigatórios (pedidos pela professora e ainda pendentes):**

1. Criar os **Apêndices A e B** (`apendices_A_B.tex`) e citá-los no roteiro e na Seção 4.8.6.
2. **Apagar o parágrafo de dificuldades repetido** na conclusão. Isso também a traz de volta para 3 páginas.
3. Completar o **resumo** com os resultados de desempenho e as limitações.
4. Corrigir a afirmação da **p. 37**, que ainda associa interpretabilidade a pior desempenho e atribui a Rudin (2019) o contrário do que o artigo defende.
5. **Friedman:** pôr a explicação 5×2cv × Nemenyi antes da conclusão sobre a Árvore e tirar o "inequívoca".
6. **Faixa de recusa:** dizer explicitamente que ela é [inferior; superior).
7. Linha 202 (UMAP e "anomalias"), quatro verbos no futuro e "O Autor" × "O autor".

**Fora do texto, mas crítico para a entrega:**

8. **Gerar um Release novo (v1.1).** Os executáveis do v1.0 (02/10) foram feitos antes do retreino da Árvore de Decisão (08/10), então a Árvore do executável não é a do texto.

**Exigidos pelo manual de Normas Técnicas da UTP (4. ed., 2024), que o trabalho ainda não segue:**

9. D8: **folha de aprovação**, obrigatória em TCC apresentado a banca, logo depois da folha de rosto (manual, pp. 33–34). Bloco pronto, com campos a preencher (data e banca).
10. D1: **abstract**, o resumo em inglês, em folha separada (p. 37). Bloco pronto; falta a tradução.
11. D10: citações com **três autores** listam os três sobrenomes, e "et al." só a partir de quatro; **entre parênteses**, os autores são separados por ";" (pp. 23 e 56). Exige trocar uma opção no `packages/abnt-UTP.sty`.
12. D9 e D11: palavras-chave com inicial minúscula (p. 36) e subtítulos de nível 3 só com a inicial maiúscula (p. 16).

**Recomendados (revisão minha), em ordem de importância:**

13. A1: a explicação da calibração do SVM está errada. O que muda o resultado é o `ensemble`, não o `probability`; testei as quatro combinações.
14. A2: definir a especificidade na fundamentação.
15. A3: o Código 1 mostra parâmetros do UMAP diferentes dos usados (15 e 0,1).
16. A13: o Quadro 3 diz que o "Comitê" é o melhor algoritmo, o que contradiz a Seção 4.7.2.

## O que depende de você

- Origem do `data.csv`: Kaggle ou UCI (item 16 do `01`).
- Se a figura `hyperplane.png` saiu mesmo de aionlinecourse.com (item 15 do `01`).
- Corrigir o arredondamento da faixa no código ou só explicar no texto (item 12 do `01`; recomendo só explicar).
- Por que XGBoost e redes neurais saíram do trabalho: prepare a resposta (pergunta 24).
- Data da defesa e nomes, titulações e instituições da banca, para a folha de aprovação (D8).
- Itálico em "software": aplicar no texto todo ou tirar dos apêndices (D12).
- Qual foi exatamente a divergência entre a decisão exibida e o classificador no SVM e no KNN (pergunta 61).
