# Módulo — Segurança (base)

**Horas do dono (hipótese):** 1 h (mapa de acesso com o cliente). **Construção:** pronta no `starter`; papéis em `lib/seguranca/papeis.ts` e no `CHECK` da migration, com guarda de igualdade.
**Fonte da área:** CyberOps, `seguranca/PRATICAS_SEGURANCA.md` (14 §2); categorias 1 e 2 do 04.

## 1. Decisões do Dia 0
- **Mapa de acesso:** tabela papel × recurso × ação (ler, criar, editar, apagar). É a especificação da RLS e dos testes.
- **Onde moram os segredos:** variáveis da hospedagem; `.env.example` completo e conferido contra o código.
- **Rotas públicas** (formulário, login, cadastro, webhook) e o limite de requisição de cada uma.

## 2. O que inclui
- Autenticação do provedor (Supabase Auth), com a guarda de área pura e testada (02 §2; 04, 2.2).
- Autorização **no servidor** em toda ação; a interface só esconde, não protege.
- A guarda roda **na página** (ou na camada de acesso aos dados), não só no layout: o layout não re-renderiza na navegação nem impede a página de rodar e entrar no payload RSC (04, 2.9).
- RLS em toda tabela, mais `GRANT` por coluna onde o cliente escreve (RLS não protege coluna: 04, 1.4 e 1.5).
- Funções `SECURITY DEFINER` com `REVOKE … FROM anon` explícito (04, 1.6).
- Cabeçalhos de segurança, cookies seguros e redirects que copiam os cookies (04, 2.1).
- Limite de requisição nas rotas públicas.

## 3. Guardas obrigatórias
- `ASSERT has_column_privilege` e `has_function_privilege` dentro de cada migration que cria tabela ou função (04, 1.5 e 1.6).
- Toda escrita confere as linhas afetadas; nenhum `error` descartado, com lint (04, 1.7; Velix #214).
- Teste de acesso cruzado por papel no e2e.
- Página sob layout com guarda chama a guarda de novo; nenhum `user!.` em `app/` (04, 2.9; `lib/guardas.test.ts` do starter).
- Leitura de tabela que cresce com `limit` ou paginação; o PostgREST corta em 1.000 linhas sem erro (04, 1.11).
- Varredura de segredos no CI.

## 4. Teste de aceite
Linhas da seção 2 do `ACEITE.md`.
