# Descoberta — biblioteca — 2026-11-03 (F0 fechado; respostas do Pedro em 3-Nov)

> **Trabalho de portfólio com cliente fictício** (issue #39; PFA-F, 15 §1, etapa F0). O "cliente" é
> fictício e documentado; o Pedro faz o papel dele no aceite. Nenhum dado real de pessoa ou empresa.
> **Respostas do Pedro (3-Nov-2026, sessão "PM Biblioteca"):** D1 sim · D2 duas contas de até 50 MB,
> com mais espaço mediante pagamento · D3 celular · D4 pediu a sugestão do PM · D5 gratuito · D6 sim ·
> D7 17-Nov-2026 · D4 e D8 aceitas como o PM sugeriu (EPUB e CBZ no MVP, PDF na fase 2; compra de
> espaço na fase 2). Marca **[Pedro 3-Nov]**. Nenhuma pergunta aberta: F0 fechado.
> Template: `kit/freelance/DESCOBERTA.md` · Framework na `origin/main` `191b99b` · PM: sessão "PM Biblioteca".
>
> **Marcas:** **[#39]** = decidido na issue #39 (comentário de 27-Out-2026) · **[proposta #39]** =
> escrito na leitura do pedido, ainda sem decisão · **[premissa]** = inventado pelo PM para o cliente
> fictício, vale se o Pedro não mudar · **[falta Dn]** = só o Pedro responde (card Dn no quadro
> "Atividades — Biblioteca").
>
> Este rascunho mora no framework porque o repositório do projeto só recebe conteúdo no Dia 0, depois
> do aceite da proposta (15 §1, regra 1). No Dia 0 ele muda para `docs/DESCOBERTA.md` do projeto.

**Cliente:** pessoa física, leitora, que contrata pela plataforma de freelance o seu "primeiro projeto"
(texto original da #39), que quer o app para si e para abrir a outros leitores [Pedro 3-Nov, D1] · **Quem decide e quem aceita:** o cliente, papel
feito pelo Pedro [#39] · **Tempo de resposta combinado:** até 48 h em dia útil, por ser iniciante [premissa]

## 0. O pedido original (#39)
> "Como é meu primeiro projeto, gostaria de fazer um Organizador de Biblioteca Pessoal, aonde o usuario
> pode ler livros, mangás e poemas, continuar ou começar uma nova leitura, sem falar nas recomendações de novos livros."

## 1. O problema
- **Alternativa real hoje:** os arquivos ficam espalhados entre pastas do computador, apps de leitura
  diferentes para EPUB, PDF e mangá, e uma lista de "quero ler" numa planilha ou no bloco de notas [premissa].
- **O que dói:** perder o ponto de leitura ao trocar de aparelho ou de app; não saber o que já leu; ficar
  sem ideia do que ler depois [premissa].
- **Critério de sucesso (vai para o aceite):** (a) o leitor envia um arquivo e começa a ler em até 3
  toques, no celular; (b) ao reabrir, em qualquer aparelho, volta à mesma página; (c) a estante mostra
  "quero ler, lendo, lido" sem digitação manual; (d) recebe ao menos 5 recomendações a partir do
  histórico; (e) nenhum arquivo de uma conta é visível a outra (guarda de acesso cruzado, 15 §5) [premissa, exceto (e): #39].

## 2. Quem usa
| Papel | O que precisa fazer | Aparelho e condição | Quantos |
|---|---|---|---|
| **Leitor** (único papel do MVP) | Criar conta, enviar arquivo, organizar a estante, ler, continuar, marcar status, ver recomendações, excluir a conta e os arquivos | **Celular** (PWA a 360 px) [Pedro 3-Nov, D3]; computador funciona, sem ser prioridade | **2 contas** na demonstração [Pedro 3-Nov, D2] |
| **Visitante** | Ver a página inicial e o acervo de domínio público, sem ler | Celular | — |

- **O que cada papel não pode ver nem fazer:** nenhum leitor vê arquivo, estante, histórico ou posição
  de outro leitor; nada é compartilhado entre contas [#39]. Não há papel de administrador no MVP: o
  acervo de domínio público é carregado por migration ou script do PM, não por tela [premissa].

## 3. Dinheiro
- **O produto cobra alguém?** **Gratuito** na base [Pedro 3-Nov, D5], com **espaço extra mediante
  pagamento** [Pedro 3-Nov, D2] → modelo freemium. **Quando cobrar:** no MVP, a barra de uso e o aviso de limite,
  sem cobrança; a compra de espaço (módulo Pagamentos do `starter`, pagamento único por pacote) na
  fase 2 [Pedro 3-Nov, D8].
- **Orçamento do projeto (fictício):** até R$ 4.000 [premissa aceita com a D5]; infraestrutura em planos
  gratuitos na demonstração, a conferir no Dia 0.
- **Nota fiscal e estorno:** só existem quando a compra de espaço entrar (D8).

## 4. Dados
- **Dados pessoais:** e-mail, nome de exibição, os arquivos enviados, a estante, o histórico e a posição
  de leitura. **O que alguém lê é dado pessoal e pode revelar opinião religiosa, política ou vida sexual**
  (LGPD, art. 11): tratado como sensível no desenho, mesmo sem coletar o dado explicitamente [premissa;
  não é aconselhamento jurídico].
- **Retenção:** enquanto a conta existir; exclusão da conta apaga arquivos, estante e histórico na hora;
  exportação da estante em JSON [premissa].
- **Política e termos:** não tem. Entram no escopo a partir de um modelo, dizendo que só se envia
  arquivo de uso pessoal e que nada é compartilhado [#39].

## 5. Sistemas e conteúdo
- **De onde vêm os arquivos:** só **envio pelo próprio usuário**, visível só a ele, e **obras de domínio
  público** [#39]. Sem DRM (Kindle, Kobo) [proposta #39].
- **Formatos do MVP [Pedro 3-Nov, D4]:** **EPUB** (livros e poemas) e **CBZ**
  (mangá, leitura da direita para a esquerda). **PDF fica para a fase 2**: no celular a 360 px o PDF
  vira zoom e rolagem lateral, o EPUB já cobre livros e poemas, e o prazo de 17-Nov pede um leitor a menos.
- **Acervo de domínio público:** aprovado [Pedro 3-Nov, D6]: uma seleção curada de 20 a 30 obras em
  português, de autores mortos há mais de 70 anos (Lei 9.610/98, art. 41), guardadas no próprio Storage
  com a fonte citada [premissa; a origem dos arquivos a conferir no F1].
- **Recomendações:** por regra no MVP (gênero, autor, histórico e títulos parecidos pela Open Library);
  IA na fase 2, com orçamento de tokens [#39]. Termos e limites de uso da API da Open Library a conferir no F1.
- **Identidade visual, domínio e e-mail:** sem logo nem domínio; a URL da Vercel basta para o portfólio [premissa].
- **Repositório:** público, **`pedrohrsm-crypto/biblioteca-manga`**, criado vazio pelo Pedro em 3-Nov-2026;
  o nome substitui `biblioteca-pessoal` da #39, sem mudar o escopo (livros, poemas e mangá) [Pedro 3-Nov, D9].
  Fica vazio até o aceite da proposta: o primeiro commit é o do Dia 0 (15 §1, regra 1).

## 5b. Suporte
- Um único canal: e-mail de contato na página "Ajuda", com resposta em até 2 dias úteis [premissa].
- **As perguntas que viram o FAQ:** 1. "Que formatos posso enviar?" 2. "Alguém vê os meus arquivos?"
  3. "Por que não abre meu livro do Kindle?" 4. "Qual o limite de espaço?" 5. "Como apago minha conta?" [premissa]

## 6. Prazo e restrições
- **Data que não pode passar:** **17-Nov-2026** [Pedro 3-Nov, D7]; classe `data-fixa`. O PM entende
  como **MVP no ar e aceito** nessa data. A previsão da #39 era de 3 a 4 semanas depois do aceite; daqui
  até 17-Nov há **10 dias úteis**, então o escopo encolhe (abaixo) e o risco R7 fica aberto.
- **Calendário proposto:** 4-Nov F0 fechado e F0b · 5-Nov proposta (F1) e baixa fidelidade · 6-Nov aceite
  e Dia 0 · 9-Nov prova de conceito do leitor (EPUB e CBZ) · 10 a 13-Nov construção por fatias · 16-Nov
  endurecimento (F2) · 17-Nov aceite e passagem (F3).
- **Se apertar, sai primeiro:** metas de leitura, depois a busca textual (fica o filtro por status e
  gênero), depois as recomendações pela Open Library (ficam só as por regra local).
- **Armazenamento:** 2 contas de até 50 MB [Pedro 3-Nov, D2]. Cabe uma dezena de EPUB (1 a 5 MB cada),
  mas **um volume de mangá em CBZ costuma ter de 20 a 100 MB** (a medir no Dia 0): com 50 MB, cabe um
  volume ou nenhum. Risco R8 abaixo.
- **Stack exigida:** nenhuma; segue a de referência (15 §3.1) mais PWA, `epub.js`, `pdf.js` [proposta #39].

## 7. Perguntas das nove áreas (14 §2) — o que já se sabe
| Área | Resposta ou o que falta |
|---|---|
| **UX/UI** | Leitor a 360 px, temas claro, escuro e sépia, fonte ajustável, escala de 140%. Telas do 1º marco: estante, envio, leitor (EPUB e CBZ), recomendações, conta. Celular primeiro (D3) |
| **Segurança** | Arquivos em bucket privado com política por dono; URL assinada e de vida curta para ler; RLS em estante, histórico e posição; validação de tipo e tamanho no envio (CBZ é ZIP: risco de ZIP bomb e de caminho malicioso) |
| **DevOps** | CI no GitHub Actions do repositório público; Vercel; projeto gratuito do Supabase pausa por inatividade (aceitável na demonstração) |
| **Desempenho** | Abrir o leitor em ≤ 2,5 s no 4G simulado; carregar página a página no PDF e no CBZ, nunca o arquivo inteiro de uma vez |
| **Marketing** | Projeto de portfólio, gratuito com espaço extra pago (D5 e D2); promessa: "sua estante, em qualquer aparelho, de onde parou" |
| **Suporte** | §5b |
| **Back-end e dados** | `obras`, `arquivos`, `estante` (status), `posicoes` (por obra e por aparelho), `recomendacoes_cache`; Storage com limite por conta |
| **Pagamentos** | Só quando a compra de espaço entrar (D8); pagamento único por pacote, Stripe do `starter` em modo de teste |
| **Privacidade e LGPD** | §4; exportação e exclusão pela conta; operadores: Supabase, Vercel, Open Library (só título e autor saem, nunca o arquivo nem o e-mail) |

## 8. Classificação (preliminar; fecha depois das respostas)
- **Tipo de produto:** app web de uso pessoal com contas, entregue como PWA (11 §5, mais perto de "SaaS web multipapel" com um papel só) [proposta #39].
- **Módulos base:** Segurança · Acessibilidade · Privacidade · Operação · Suporte.
- **Módulos contextuais:** nenhum no MVP; **Pagamentos (único)** entra quando a compra de espaço entrar (D8).
- **Inédito:** (1) leitor de EPUB e CBZ (PDF na fase 2, D4); (2) posição de leitura por obra e por aparelho; (3) envio e
  guarda de arquivos com limite por conta; (4) recomendações por regra com a Open Library; (5) acervo de domínio público.
- **Riscos vistos (viram issues `risco` no Dia 0):** R1 direito autoral (mitigado pelo acervo da #39) ·
  R2 leitor inédito, a maior incerteza (prova de conceito no Dia 1) · R3 custo e cota de Storage ·
  R4 cliente iniciante, escopo que cresce · R5 arquivo malicioso no envio (CBZ, PDF) · R6 histórico de
  leitura como dado sensível · **R7 prazo de 17-Nov com 10 dias úteis** (resposta: escopo cortado
  nesta descoberta e prova de conceito do leitor no primeiro dia de construção; gatilho: a prova de
  conceito não abrir EPUB e CBZ no celular até 9-Nov) · **R8 mangá não cabe em 50 MB** (resposta a
  decidir no F1: limite por arquivo e aviso claro; ou compressão das imagens no envio, que é escopo a mais).

## 9. Perguntas que só o Pedro responde
| Código | Pergunta | Recomendação do PM |
|---|---|---|
| **D1** | Perfil do cliente fictício | **Respondida:** sim, como recomendado |
| **D2** | Usuários e espaço por conta | **Respondida:** 2 contas de até 50 MB; mais espaço mediante pagamento |
| **D3** | Aparelho principal | **Respondida:** celular |
| **D4** | Formatos do MVP e ordem de corte | **Respondida:** EPUB e CBZ no MVP; PDF na fase 2 |
| **D5** | Cobrança e orçamento fictício | **Respondida:** gratuito (com o espaço extra pago da D2) |
| **D6** | Acervo de domínio público | **Respondida:** sim, como recomendado |
| **D7** | Data fixa | **Respondida:** 17-Nov-2026 |
| **D8** | A compra de espaço extra entra no MVP ou na fase 2? | **Respondida:** fase 2; no MVP, barra de uso e aviso de limite |

**Próximo passo depois das respostas:** F0b (prospecto do Agente Multidisciplinar) e F1 (proposta com a
baixa fidelidade), 15 §1.

## Não medido
- Tamanho médio de EPUB, PDF e CBZ, cota de Storage gratuita do Supabase e limites da API da Open Library: ficam para o F1 e o Dia 0.

## Para o framework
- O template `kit/freelance/DESCOBERTA.md` não tem pergunta sobre **conteúdo enviado pelo usuário**
  (direito autoral, limite de espaço, arquivo malicioso). Candidata a lição se aparecer num segundo projeto.
