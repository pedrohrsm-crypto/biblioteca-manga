# Prospecto do usuário final — biblioteca — 2026-11-03

**SHA:** framework `191b99b` (o repositório `biblioteca-manga` foi criado vazio em 3-Nov; recebe código no Dia 0) · **Rotas:** 0 em código; 5 telas planejadas (`DESCOBERTA.md` §7, UX/UI) · **Sinais do usuário presentes:** não medido (sem código; `contexto.py` não rodado) · **Rodada anterior:** nenhuma (linha de base) · **Custo:** incluído na linha da sessão do PM

> Rodada **manual** do Agente Multidisciplinar (F0b do PFA-F; `ROTINA.md`: "sem conector, a rodada é manual"), no modelo do prospecto da loja-online. Pacote de contexto: `DESCOBERTA.md` (deste diretório, F0 fechado em 3-Nov-2026) e a issue #39. Cliente fictício: toda evidência que vem da descoberta é, por origem, **premissa do cliente fictício** ou **resposta do Pedro (D1 a D8)**. Cito a seção (`D§n`), e o que não está nem lá vai marcado `[hipótese]`.
>
> **Coluna "Quando":** **MVP** = cabe no MVP de 17-Nov-2026 sem mudar o escopo da descoberta · **opcional** = cabe se sobrar folga; senão vira pedido de mudança · **fase 2** = fora do MVP.

## 1. Quem é o usuário final
| Perfil | O que quer resolver | Em que condição usa | Evidência |
|---|---|---|---|
| **Leitor de livros e poemas** | Ler os próprios EPUB num lugar só e voltar ao ponto em que parou, em qualquer aparelho | Celular, em pé no transporte, na fila ou antes de dormir; leitura em trechos curtos | D§1, D§2 (D3: celular), D§5 (EPUB) |
| **Leitor de mangá** | Ler volumes em CBZ da direita para a esquerda, com as páginas na ordem certa | Celular na vertical, rolando rápido; arquivos grandes | D§5 (CBZ), D§6 (R8: 20 a 100 MB por volume) |
| **Leitor sem acervo próprio** | Começar a ler algo bom sem ter arquivo nenhum | Celular; chega à página inicial sem saber o que enviar | D§5 (acervo de domínio público, D6) |
| **Cliente (dono do app)** | Mostrar um produto que funciona para si e para outros leitores, sem custo de operação | Celular; 2 contas na demonstração | D§0, D1, D2, D5 |

## 2. As jornadas
- **Leitor:** descobrir (página inicial e acervo público) → criar conta → enviar o primeiro arquivo (ou abrir uma obra do acervo) → ler → continuar em outro aparelho → organizar a estante (quero ler, lendo, lido) → receber recomendações → bater no limite de espaço → pedir ajuda → sair (exportar e excluir a conta).
- **Cliente:** criar as 2 contas da demonstração → conferir que uma não vê a outra → mostrar o app a alguém.
- Pagar não existe no MVP: a compra de espaço é da fase 2 (D8).

## 3. Preocupações do usuário
| ID | Jornada | O que preocupa, dito como o usuário diria | Severidade | Evidência | Área dona | Quando |
|---|---|---|---|---|---|---|
| P-01 | Continuar | "Abri no celular e voltou para a página 1" | **alta** | D§1, critério (b); posição por obra e por aparelho (D§8, inédito 2) | Back-end e dados · UX/UI | MVP |
| P-02 | Enviar · ler | "Alguém pode ver os meus arquivos ou o que eu ando lendo?" | **alta** | D§4 (histórico de leitura como dado sensível, R6); D§2 (nada compartilhado entre contas, #39) | Segurança · Privacidade | MVP |
| P-03 | Enviar (mangá) | "Meu mangá não sobe, ou sobe e acaba o espaço todo" | **alta** | D§6 (50 MB por conta; um volume em CBZ tem de 20 a 100 MB, R8) | UX/UI · Back-end e dados | MVP (aviso) · fase 2 (compressão ou compra) |
| P-04 | Ler (mangá) | "As páginas estão fora de ordem", ou "está lendo ao contrário" | **alta** | D§5 (leitura da direita para a esquerda); arquivos de imagem dentro do CBZ costumam ter nomes como `1, 2, … 10`, que a ordem alfabética embaralha `[hipótese: medir com 3 CBZ reais no Dia 0]` | UX/UI · Back-end e dados | MVP |
| P-05 | Enviar | "Mandei o livro que comprei no Kindle e não abre. O app está quebrado?" | média | D§5 (sem DRM); D§5b, pergunta 3 do FAQ | Suporte · UX/UI | MVP |
| P-06 | Ler | "A letra é pequena", ou "a tela branca cansa a vista à noite" | média | D§7, UX/UI (fonte ajustável, temas claro, escuro e sépia, escala de 140%) | UX/UI | MVP |
| P-07 | Ler | "Demora para abrir no 4G e gasta meu pacote de dados" | média | D§7, Desempenho (≤ 2,5 s; página a página, nunca o arquivo inteiro) | Desempenho | MVP |
| P-08 | Ler | "No metrô, sem sinal, não consigo continuar" | média | #39 (leitura offline completa fora do MVP; só o cache básico do PWA) | DevOps · UX/UI | fase 2 |
| P-09 | Recomendações | "Recomendou coisa sem nada a ver, ou só livro em inglês que eu não tenho" | média | D§5 (Open Library); catálogo majoritariamente em inglês `[hipótese]`; recomendar o que o leitor não tem como abrir frustra `[hipótese]` | Back-end e dados · Marketing | MVP (regra local) |
| P-10 | Limite | "O app vai começar a me cobrar sem eu saber?" | média | D§3 (gratuito com espaço extra pago na fase 2, D5 e D8) | Marketing · UX/UI | MVP (texto) |
| P-11 | Sair | "Se eu apagar a conta, os arquivos somem mesmo, ou ficam guardados em algum lugar?" | média | D§4 (exclusão apaga tudo na hora; exportação em JSON) | Privacidade | MVP |
| P-12 | Qualquer | "Abri o app e ele estava fora do ar" | média | D§7, DevOps (o projeto gratuito do Supabase pausa por inatividade) | DevOps | MVP (aceitável na demonstração; dito na passagem) |
| P-13 | Enviar | "Mandei o arquivo errado, ou em duplicata, e ocupou o meu espaço" | baixa | D§6 (50 MB por conta) | UX/UI | MVP (excluir arquivo) |
| P-14 | Acervo | "Essa edição de domínio público está com erro ou texto cortado" | baixa | D§5 (acervo curado de 20 a 30 obras, D6) | Marketing | MVP (curadoria) |

Severidade: **alta** = faz o usuário desistir ou perder dado ou confiança; **média** = atrito que ele contorna; **baixa** = incômodo.

## 4. Ideias de valor
| ID | Para quem | A ideia | Por que valeria (evidência) | Tamanho | Como validar | Área dona | Quando |
|---|---|---|---|---|---|---|---|
| I-01 | Leitor | **"Continuar lendo" como o primeiro cartão da página inicial**, com a capa, a página e o aparelho em que parou | P-01; D§1, critério (a): ler em até 3 toques | P | % das sessões que começam pelo cartão (meta ≥ 60% `[hipótese]`) | UX/UI · Back-end e dados | MVP |
| I-02 | Leitor | **Barra de uso do espaço sempre visível** e aviso antes do envio: "este arquivo tem 38 MB; sobram 12 MB" | P-03, P-10, P-13; D8 (barra no MVP) | P | Envios recusados por limite ÷ tentativas; nenhum envio falhando no meio | UX/UI | MVP |
| I-03 | Leitor de mangá | **Ordem natural das páginas e direção por obra** (direita para a esquerda por padrão no CBZ, com troca) | P-04 | M | 3 CBZ reais abertos na ordem certa no Dia 1 (prova de conceito do leitor, R7) | UX/UI · Back-end e dados | MVP |
| I-04 | Leitor | **Fonte, tema (claro, escuro e sépia) e espaçamento salvos na conta**, e não no aparelho | P-06; D3 (celular) | P | Pergunta de campo: "trocou a fonte ou o tema na primeira leitura?" | UX/UI | MVP |
| I-05 | Leitor | **Mensagem clara para arquivo com DRM ou formato não suportado**, com link para o FAQ ("de onde vêm os meus arquivos?") | P-05; D§5b, pergunta 3 | P | Contatos de suporte sobre "não abre" em 30 dias | Suporte · UX/UI | MVP |
| I-06 | Leitor | **"Privacidade em 3 linhas" na tela de envio:** só você vê; nada é compartilhado; apagar a conta apaga tudo | P-02, P-11; D§4 | P | Pergunta de campo: "você enviaria um arquivo pessoal aqui? Por quê?" | Privacidade · UX/UI | MVP |
| I-07 | Leitor sem acervo | **Estante de boas-vindas com 3 obras do acervo de domínio público** já na primeira entrada, para ler antes de enviar qualquer coisa | Perfil "sem acervo próprio"; D6 | P | % das contas novas que leem algo no primeiro dia | Marketing · UX/UI | MVP |
| I-08 | Leitor | **Recomendação com o motivo à vista** ("porque você leu Machado de Assis"), priorizando primeiro o acervo de domínio público, que ele pode abrir na hora, e depois a Open Library | P-09 | P | Recomendações abertas ÷ exibidas | Back-end e dados · Marketing | MVP |
| I-09 | Leitor | **Exportar a estante** (JSON, com títulos, status e posição) antes de excluir a conta | P-11; D§4 | P | Exportação conferida no endurecimento (F2) | Privacidade | MVP |
| I-10 | Leitor de mangá | **Comprimir as imagens do CBZ no envio** (WebP), para caber mais em 50 MB | P-03; R8 | M | Tamanho médio antes e depois em 3 volumes reais | Back-end e dados · Desempenho | opcional (decidir no F1, com a medição do Dia 0) |
| I-11 | Leitor de mangá | **Página dupla no celular deitado** | P-04 | M | Uso do modo deitado em 30 dias | UX/UI | fase 2 |
| I-12 | Leitor | **Leitura offline das últimas 3 obras abertas** | P-08 | G | Sessões começadas sem rede | DevOps · UX/UI | fase 2 |
| I-13 | Leitor | **Marcadores e destaques** no EPUB | Jornada "ler" `[hipótese: pedido comum em leitores digitais]` | M | Pergunta de campo: "você marca trechos quando lê?" | UX/UI · Back-end e dados | fase 2 |
| I-14 | Cliente | **Comprar espaço extra** em pacote, por pagamento único | D2 e D8 | M | Quantos leitores batem no limite em 30 dias | Pagamentos · Marketing | fase 2 |

## 5. Perguntas para o próximo contato com usuários
1. Para o leitor de mangá: qual o tamanho dos seus arquivos e quantos volumes você lê por mês? (valida o limite de 50 MB e o R8)
2. Para o leitor: em quantos aparelhos você lê, e qual foi a última vez que perdeu o ponto de leitura?
3. Para o leitor: você enviaria um arquivo pessoal a um app novo? O que faria você confiar?
4. Para o leitor sem acervo: você leria um clássico em domínio público pelo celular? Qual?
5. Para o cliente: quanto pagaria por espaço extra, e quanto espaço? (insumo da fase 2, D8)

## 6. O que não foi possível avaliar
- `[não conferido]` sinais no código (rotas, termos, FAQ, guia): não há código; a próxima rodada roda o `contexto.py` sobre o repositório no endurecimento (F2, 16-Nov).
- `[não conferido]` tamanho real de EPUB e CBZ (P-03, I-10) e a ordem das imagens dentro dos CBZ (P-04): medição no Dia 0 e na prova de conceito.
- `[não conferido]` cobertura em português e limites de uso da API da Open Library (P-09).
- Todo o perfil vem de cliente fictício: as severidades são hipótese até haver usuário real (15 §0).

## 7. Estado dos itens anteriores
Primeira rodada (linha de base): nada a atualizar.

---
**As 3 preocupações mais severas para a proposta:** P-02 (privacidade dos arquivos e do que se lê: acesso cruzado e histórico como dado sensível), P-01 (perder o ponto de leitura entre aparelhos: o inédito da posição) e P-03 com P-04 (mangá que não cabe em 50 MB ou abre fora de ordem: o leitor de CBZ é a maior incerteza, R7 e R8).
**Ideias que a proposta incorpora no escopo, por serem P e cobrirem preocupação alta ou média:** I-01, I-02, I-04, I-05, I-06, I-07, I-08 e I-09; e I-03 (M), por ser condição para o leitor de mangá funcionar. **Opcional, decidido no F1 com a medição do Dia 0:** I-10. **Fase 2:** I-11, I-12, I-13 e I-14.
