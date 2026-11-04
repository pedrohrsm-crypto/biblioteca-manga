# Proposta — biblioteca — 2026-11-03

**Trabalho de portfólio com cliente fictício** (issue #39). O Pedro aceita no papel do cliente, nada é
cobrado e o preço é exercício (15 §2.4). **Validade da proposta:** 2026-11-05 · **Versão:** 2 · **Aceita em 2026-11-04**
**Insumos:** `DESCOBERTA.md` (F0 fechado, D1 a D9), `PROSPECTO.md` (F0b) e `FIDELIDADE.md` §1, todos nesta pasta.
**Repositório:** `pedrohrsm-crypto/biblioteca-manga`, público e vazio até o Dia 0 (D9).

**O que mudou da versão 1 para a 2 (3-Nov):**
- **Orçamento do cliente:** passou de R$ 4.000 para **R$ 3.000** (Pedro, 3-Nov). Para caber, o escopo encolheu:
  saem as recomendações pela Open Library (ficam só as do acervo, por regra local); o acervo cai de 20 a 30
  obras para 10; a alta fidelidade cobre 2 telas; as prévias passam de 6 para 4; e a garantia, de 30 para 15 dias.
- **Segurança:** entram as 11 correções da conferência da baixa fidelidade, de 3-Nov (`FIDELIDADE.md` §1, regras 1 a 10).
  As principais: cadastro só por convite, EPUB aberto sem executar script, RLS em toda tabela e o acervo
  separado das obras privadas.

## 1. O que será entregue
Um app de leitura pessoal, instalável no celular (PWA), em que o leitor guarda os próprios livros, poemas
e mangás, lê no próprio app e volta exatamente de onde parou em qualquer aparelho. Também organiza a estante
e recebe sugestões do acervo. Inclui um acervo de obras em domínio público para quem ainda não tem arquivo.
Gratuito, com 2 contas de até 50 MB na demonstração.

| Módulo | O que inclui neste trabalho | Critério de aceite (verificável; barra do 15 §5) |
|---|---|---|
| **Segurança** (base, starter) | Conta com e-mail e senha; **cadastro público desligado: só os 2 e-mails convidados entram** (allowlist em variável da Vercel); RLS em **toda** tabela, com policy de dono; acervo em tabela própria, só de leitura; arquivos em bucket privado com limite de tamanho e de tipo, caminho gerado pelo servidor e leitura por URL assinada de 60 a 300 s; **EPUB aberto sem executar script** e sem buscar nada fora (CSP do leitor); EPUB e CBZ validados no servidor (tipo real, tetos de descompactação, nenhum caminho fora da pasta); limite de requisição no login, na recuperação de senha e no envio; segredos só na Vercel | Teste de acesso cruzado verde: a conta B vê 0 obras, arquivos, posições e URLs da conta A, inclusive com o ID adivinhado; anônimo recebe 404 no leitor e no Storage; um 3º e-mail não consegue criar conta; arquivo renomeado (`.exe` como `.epub`), ZIP bomb e CBZ com `../` recusados; **EPUB com `<script>` e imagem remota abre sem executar nem buscar nada**; `ASSERT` de RLS em toda tabela nas migrations; varredura de segredos limpa |
| **Acessibilidade** (base, starter) | WCAG 2.2 AA nas 13 telas; 360 px; escala de 140%; teclado; no leitor, **fonte ajustável e temas claro, escuro e sépia salvos na conta** (prospecto I-04); EPUB legível por leitor de tela | axe sem violação no e2e das 13 telas; capturas a 360 px × 140% × 3 temas; um capítulo de EPUB lido pelo leitor de tela do celular |
| **Privacidade** (base, starter) | Termos de uso e política a partir de modelo: só arquivo de uso pessoal, nada compartilhado entre contas, histórico de leitura tratado como sensível; aviso "privacidade em 3 linhas" na tela de envio (I-06); exportação da estante em JSON com reautenticação (I-09); exclusão de conta que apaga Storage e banco, nessa ordem, com nova tentativa se falhar; log sem título de obra nem nome de arquivo; o app instalado não guarda nada da conta no aparelho | Teste de exclusão de ponta a ponta verde (0 linhas e 0 objetos da conta depois); exportação baixada e conferida; amostra do log sem título, arquivo nem e-mail; depois de sair, o cache do aparelho não tem página da estante |
| **Operação** (base, starter) | CI com os 4 portões desde o 1º commit; deploy na Vercel; backup semanal do banco e do Storage, com **uma restauração testada**; alerta de erro; runbooks (migrations, restauração, projeto Supabase pausado) | Run verde no commit do aceite; registro da restauração com data; captura do alerta disparado |
| **Suporte** (base) | Página "Ajuda" com e-mail de contato e prazo de 2 dias úteis escrito; FAQ com as 5 perguntas da descoberta; mensagem clara para arquivo com DRM ou formato não suportado, com link para o FAQ (I-05) | E-mail de teste respondido; FAQ publicado; envio de arquivo com DRM mostra a mensagem certa |
| **Leitor de EPUB** (inédito) | Livros e poemas em EPUB (`epub.js`, scripts desligados), paginação no celular, fonte, tema e espaçamento da conta; carregamento por capítulo | 3 EPUB reais (um de poemas) abrem a 360 px; abrir em ≤ 2,5 s no 4G simulado (medição registrada) |
| **Leitor de mangá (CBZ)** (inédito) | Imagens do CBZ **na ordem natural** (1, 2, … 10) e da direita para a esquerda por padrão, com troca por obra (I-03); só imagens JPEG, PNG, WebP ou GIF, exibidas como imagem; carregamento página a página | 3 CBZ reais abertos na ordem certa, nas duas direções; memória do celular estável ao folhear 100 páginas |
| **Posição de leitura e "Continuar lendo"** (inédito) | Posição salva por obra e por aparelho, com o mais recente vencendo; cartão "Continuar lendo" no topo da estante (I-01); "começar do início" sem perder o histórico | Ler no celular, abrir no computador e cair na mesma página (± 1 tela no EPUB); dois aparelhos ao mesmo tempo sem perder a posição mais nova |
| **Estante e envio** (inédito) | Estante com status (quero ler, lendo, lido), capa, autor e gênero; filtro por status e gênero e busca por título ou autor; envio com **barra de uso sempre visível** e aviso antes do envio (I-02); a cota de 50 MB é a soma da conta, conferida no servidor; excluir arquivo libera espaço | Arquivo que estoura os 50 MB é recusado **antes** do upload, com o tamanho que sobra; dois envios simultâneos não passam da soma; excluir devolve o espaço na barra |
| **Acervo e recomendações** (inédito) | **10 obras** em português, de autores mortos há mais de 70 anos (Lei 9.610/98, art. 41), com a fonte citada, validadas como qualquer envio e **fora** da cota do leitor; estante de boas-vindas com 3 obras (I-07); **recomendações por regra local**: obras do acervo do mesmo gênero ou autor do que o leitor leu, com o motivo à vista ("porque você leu…", I-08) | Lista do acervo com a fonte e o ano de morte de cada autor; conta nova lê uma obra do acervo sem enviar nada; 3 recomendações ou mais depois de 2 obras lidas, cada uma com o motivo |
| **PWA** (contextual) | Instalável no celular, com ícone e tela de abertura; o service worker guarda só o esqueleto do app, nunca página da conta, arquivo ou URL assinada | Instalado num Android e num iPhone (ou simulador), com captura; cache conferido depois de sair da conta |

**Baixa fidelidade anexada:** jornadas, mapa de 13 telas, mapa de acesso e as 10 regras de servidor em
`FIDELIDADE.md` §1 (versão 2). Aceitar esta proposta aprova também a baixa fidelidade. Mudança nela depois do
aceite é pedido de mudança (item 7).

## 2. Fora do escopo
O que não está aqui nem no item 1 não está incluído.
- **PDF** (D4: fase 2) e qualquer formato com DRM (Kindle, Kobo).
- **Compra de espaço extra** (D8: fase 2) e qualquer cobrança.
- **Recomendações pela Open Library** (títulos fora do acervo): saem na versão 2 por causa do orçamento.
  Candidatas ao primeiro pedido de mudança.
- **Acervo acima de 10 obras.** Cada obra a mais é curadoria e validação, e entra por pedido de mudança.
- **Compressão das imagens do CBZ no envio** (I-10). Volume acima de 50 MB fica fora. Se a medição do Dia 1
  mostrar que nenhum volume real cabe, a compressão vira pedido de mudança (risco R8).
- Leitura offline das obras (I-12), página dupla no celular deitado (I-11), marcadores e destaques (I-13).
- **Metas de leitura**: saem pela ordem de corte da descoberta (D§6), por causa do prazo de 17-Nov.
- Cadastro aberto, mais de 2 contas, painel de administração (o acervo entra por script).
- Recomendação por IA (fase 2, com orçamento de tokens), resenhas, rede social, compartilhamento.
- App nativo nas lojas, domínio próprio, identidade visual além de logo e cores simples.
- Orientação jurídica sobre direito autoral ou LGPD (os termos partem de modelo e não são aconselhamento jurídico).

## 3. Estimativa e premissas (15 §2.3: dois recursos e um calendário)
**Estimativa sem histórico, portanto hipótese:** `dados/estimativas.csv` não tem trabalho real que calibre (15 §2.3).
Fator **1,3** nos módulos do starter e **1,5** no inédito.

| Item | Horas do dono (base) | Fator | Horas do dono | Construção por IA (sessões) |
|---|---|---|---|---|
| Descoberta e proposta (ler, decidir, aceitar) | 1,50 | 1,3 | 1,95 | 1 (esta sessão de PM) |
| Segurança · Acessibilidade · Privacidade · Suporte (decisões do Dia 0) | 1,00 | 1,3 | 1,30 | pronto no starter |
| Operação (contas Supabase e Vercel, convites, backup) | 0,50 | 1,3 | 0,65 | 1 (Dia 0: kit, CI, starter) |
| Média e alta fidelidade (aprovar wireframes e 2 telas principais) | 1,00 | 1,3 | 1,30 | 2 + 2 conferências de analista |
| Prévias diárias (4 × 10 min) | 0,67 | 1,3 | 0,87 | — |
| Endurecimento, aceite e passagem | 1,00 | 1,3 | 1,30 | 1 rodada completa (4 áreas) |
| **Inédito: leitores EPUB e CBZ** (testar com arquivos reais no celular) | 1,00 | 1,5 | 1,50 | 2 |
| **Inédito: posição, estante e envio, acervo de 10 obras e recomendações locais** | 0,50 | 1,5 | 0,75 | 3 |
| PM (integração e relatório) | — | — | — | 4 |
| **Total** | **7,17** | | **9,62 h** | **6 frentes e PM + 8 de analista (2 já feitas)** |

**Custo de IA (hipótese):** pelas medianas internas de custo por sessão do framework (frente, analista e PM), com
fator 1,5 no inédito e 1,3 no resto, ≈ **US$ 163**, cerca de **R$ 880** com o câmbio de referência de R$ 5,40 (**não conferido**).

**Calendário (15 §2.3):** 9,6 h ÷ **5 h por semana** dedicadas à biblioteca (premissa: o Pedro divide a semana
com outros projetos) = **2 semanas de trabalho**, de 4-Nov a 17-Nov. A data de 17-Nov (D7) **cabe
sem folga**: qualquer espera do cliente acima de 24 h empurra a entrega (risco R7).

Premissas (se uma falhar, prazo e preço são revistos):
- O cliente (o Pedro, no papel) responde em até 24 h em dias úteis, e as prévias em até 1 dia útil.
- Projeto Supabase e projeto Vercel criados até o Dia 0 (4-Nov), com o PM com acesso de escrita ao `biblioteca-manga`.
- 3 EPUB e 3 CBZ reais (de domínio público ou do próprio Pedro, para teste) disponíveis até o Dia 1 (5-Nov),
  para a prova de conceito dos leitores, a medição do R8 e os tetos numéricos de descompactação.
- Até 13 telas (12 de uso e a de Não encontrado), conforme a `FIDELIDADE.md` §1.
- Alta fidelidade **só em código**, sem Figma (15 §12.1, regra 5; como na loja), para caber no prazo.
- Base de código: o `starter` do framework (15 §3.3).

## 4. Cronograma (porte curto, 16 §2; sem feriado nacional em dia útil até 17-Nov)
| Marco | Data | Entrega | Pagamento (exercício) |
|---|---|---|---|
| Aceite da proposta e da baixa fidelidade | **qua 4-Nov** | lista do Dia 0 (abaixo) | 40% · R$ 1.200 |
| **Dia 0** | qua 4-Nov | starter e kit `--freelance` no `biblioteca-manga`, CI verde, convites das 2 contas; **média fidelidade** (wireframes em código na prévia) para aprovar até qui 5-Nov | — |
| **Dia 1** | qui 5-Nov | **prova de conceito dos leitores** (EPUB e CBZ no celular, gatilho do R7) e medição do tamanho dos CBZ (R8); alta fidelidade em código de 2 telas (Estante e Leitor) | — |
| Dias 2 e 3 | sex 6 e seg 9-Nov | fatias: estante e envio com limite; posição e "Continuar lendo"; acervo e recomendações; prévias | — |
| Reserva do inédito | ter 10 e qua 11-Nov | folga para os leitores e a posição (o que estourar) | — |
| **Dia 4 · Endurecimento** | qui 12-Nov | barra inteira (15 §5), rodada da `analise`, acesso cruzado, EPUB com script, exclusão, restauração | — |
| Entrega para aceite | sex 13-Nov | produto publicado na URL de demonstração, `ACEITE.md` com evidência | 40% · R$ 1.200 |
| **Aceite final e passagem** | **ter 17-Nov** (D7) | termo de aceite, `PASSAGEM.md`, README do portfólio com capturas, rascunho do post do MVP no LinkedIn | 20% · R$ 600 |
| Garantia | até qua 2-Dez | defeitos da barra | — |
| Retro (P3) | semana de 23-Nov | estimado × realizado em `dados/estimativas.csv` | — |

### O que precisamos do cliente até o Dia 0
- [ ] Projeto Supabase e projeto Vercel criados, com o PM convidado. As chaves **nunca vão para arquivo nem para commit**: vão direto para as variáveis da Vercel.
- [ ] Acesso de escrita do PM ao `pedrohrsm-crypto/biblioteca-manga`.
- [ ] Os 2 e-mails convidados da demonstração, informados direto na variável da Vercel (não entram em arquivo).
- [ ] 3 EPUB e 3 CBZ reais para teste, até o Dia 1.
- [ ] Logo e duas cores (ou "escolha o PM"), e o e-mail de contato da página Ajuda (fictício no portfólio).
- [ ] Quem aprova os wireframes (Dia 0) e as telas principais (Dia 1), com retorno em até 1 dia útil: o Pedro.

## 5. Preço (exercício, 15 §2.4)
```
piso  = 9,6 h × R$ 180 (D-F2)                         = R$ 1.732
      + custo de IA ≈ US$ 163 × R$ 5,40 (não conferido) = R$   880
      + margem de risco 20% (dois leitores inéditos)   = R$   522
      + garantia: 1 h × R$ 180                        = R$   180
      = cerca de R$ 3.300
```
**Valor do pacote: R$ 3.000**, o orçamento do cliente fictício (Pedro, 3-Nov). **Fica cerca de R$ 300 (9%)
abaixo do piso, mesmo com os cortes da versão 2.** O 15 §2.4 manda cobrar o maior entre o piso e o valor
do pacote, então este preço só vale como **decisão do dono (D10)**: aceitar o prejuízo como investimento de portfólio.
Num cliente real, o PM recomendaria uma destas saídas: (a) cobrar R$ 3.300; (b) tirar o leitor de EPUB e entregar
só mangá, o que baixaria o piso para cerca de R$ 2.800; ou (c) tirar a margem de risco e aceitar estourar.
Custos de fornecedor (hospedagem, banco, e-mail) são do cliente, pagos direto nas contas dele; na demonstração, planos gratuitos.

## 6. Garantia e suporte
15 dias depois do aceite final, para defeitos da barra de qualidade. Canal: e-mail do freelancer, com primeira
resposta em até 1 dia útil. Pedido novo não é garantia: vira pedido de mudança. Depois da garantia (opcional):
R$ 180 por hora ou pacote mensal de 3 h por R$ 480.

## 7. Pedido de mudança
| # | Data | Mudança | Impacto no prazo | Impacto no preço | Aceito em |
|---|---|---|---|---|---|

## 8. Riscos que a proposta assume (viram issues `risco` no Dia 0)
| ID | Risco | Resposta | Gatilho |
|---|---|---|---|
| R7 | Prazo de 17-Nov sem folga | Escopo cortado (PDF, metas, compra de espaço, Open Library fora); prova de conceito dos leitores no Dia 1 | Leitor que não abre EPUB e CBZ no celular até 5-Nov: o PM avisa no mesmo dia |
| R8 | Mangá que não cabe em 50 MB | Medição no Dia 1 com 3 CBZ reais | Nenhum volume real ≤ 50 MB: pedido de mudança (compressão, I-10) ou aceitar volumes menores |
| R2 | Leitores inéditos (a maior incerteza) | Reserva de 2 dias (10 e 11-Nov) | Reserva consumida até 10-Nov |
| R5 | Arquivo malicioso no envio, inclusive EPUB com script | Regras 3 e 4 da `FIDELIDADE.md` §1 e o teste de aceite | — |
| R6 | Histórico de leitura como dado sensível | RLS em toda tabela, log sem título, exclusão real, nada no cache do aparelho | — |
| R3 | Projeto Supabase gratuito pausado na demonstração | Runbook; aceitável no portfólio | App fora do ar numa prévia |
| R9 | Preço abaixo do piso (D10) | Cortes da versão 2; estimado × realizado medido na retro | Horas do dono acima de 9,6 h até o endurecimento |

## 9. Aceite desta proposta
**Aceita** pelo Pedro, no papel do cliente, em **2026-11-04**, por escrito, na sessão "PM Biblioteca"
(resposta do Pedro: "D10 aceito, A1 aceito"). Registro: PR #56.

O aceite vale para esta proposta (versão 2), para a baixa fidelidade (`FIDELIDADE.md` §1, versão 2) e para as
decisões tomadas junto:
- **D10:** preço de R$ 3.000, cerca de R$ 300 abaixo do piso, aceito como investimento de portfólio. O estimado ×
  realizado vai para a retro (risco R9).
- **D9:** repositório `pedrohrsm-crypto/biblioteca-manga`.

Marco de 40% (exercício, nada é cobrado): registrado no aceite. O Dia 0 começa em 4-Nov.
