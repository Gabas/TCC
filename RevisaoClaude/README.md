# RevisaoClaude: revisão do TCC para a entrega de 15/11/2026

Situação conferida em 13/11/2026 sobre o `trabalho.tex` do commit `71aac81` e o repositório DiagnosisXAI (GitHub, commit `22cbe5a`).

| Arquivo | Conteúdo |
|---|---|
| `01_pendencias.md` | Tudo o que ainda falta, em ordem de prioridade, com os blocos Procure / Substitua por |
| `03_perguntas_banca.md` | 70 perguntas prováveis da banca, com onde está a resposta no texto e os pontos-chave de cada uma |
| `apendices_A_B.tex` | Rascunho original dos Apêndices A e B (já incorporados ao `trabalho.tex`) |
| `Apresentacao_TCC*.pptx` | Slides da defesa |

O `01_pendencias.md` substitui os antigos `01_pendencias_email.md` e `02_revisao_completa.md`. Todos os blocos dele foram aplicados numa cópia do projeto e compilados (pdflatex + bibtex + pdflatex ×2), junto com a troca no `.sty` do item 10. O resultado não teve erro nem estouro de margem, saiu com 114 páginas e manteve a conclusão em 3 páginas.

## Prioridades até 15/11

**Pedidos pela professora e ainda pendentes:**

1. Resumo com os resultados de desempenho e as limitações da base.
2. UMAP ainda "identifica anomalias" (p. 17).
3. Quatro verbos no futuro.
4. Rudin (2019) citada ao contrário (p. 37) e outras afirmações absolutas da fundamentação.
5. Friedman: a ressalva do 5×2cv tem de vir antes do "inequívoca".
6. Faixa de recusa: dizer que ela é [inferior; superior).
7. Fonte das figuras em dois formatos ("O Autor" × "O autor").
8. Chamada e origem da base de dados (Kaggle × UCI).

**Exigidos pelo manual da UTP:** abstract, folha de aprovação, palavras-chave em minúsculas e citações de dois e três autores (itens 9 e 10).

**Erros técnicos:** "intervalo aberto [0, 1]" (item 11, introduzido na última edição) e especificidade sem definição (item 12).

**Fora do texto:** o único Release publicado ainda é o v1.0 (02/10), anterior ao retreino da Árvore de Decisão. É preciso gerar o v1.1 (item 23).
