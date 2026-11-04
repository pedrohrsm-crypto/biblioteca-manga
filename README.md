# biblioteca-manga

App de leitura pessoal, instalável no celular, para guardar e ler livros, poemas (EPUB) e mangás (CBZ), voltar ao ponto em que parou em qualquer aparelho, organizar a estante e receber sugestões de um acervo de domínio público.

Trabalho de **portfólio** feito pelo método PFA-F do [Framework Aprendido](https://github.com/pedrohrsm-crypto/framework-aprendido) (capítulo 15), para um cliente fictício. A proposta aceita, a descoberta e a baixa fidelidade estão em [`docs/freelance/`](docs/freelance/).

## Stack
Next.js 16 · Supabase (Postgres, Auth e Storage) · Vercel · PWA. A base de código é o `starter` do framework (licença MIT). O módulo de pagamentos do starter fica desligado no MVP; a compra de espaço extra é da fase 2.

## Rodar localmente
```bash
cp .env.example .env.local   # preencher com as contas do projeto; nunca commitar
npm ci
npm run lint && npm run typecheck && npm test && npm run test:sql && npm run e2e
```

## Estado
Dia 0 em 4-Nov-2026. Entrega do MVP prevista para 17-Nov-2026.
