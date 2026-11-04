# Módulo — Operação (base)

**Horas do dono (hipótese):** 1 a 2 h (contas em nome do cliente, domínio, primeira restauração de backup). **Construção:** CI, bancada SQL e runbooks prontos no `starter`.
**Fonte da área:** DevOps (vazio em 26-Set-2026: usar as categorias 4 e 10 do 04).

## 1. Decisões do Dia 0
- Onde o CI roda e quem paga a cota (04, 4.11: o CI parou sem aviso quando a cota acabou).
- Hospedagem, região e plano; limites e cotas de cada fornecedor conferidos (04, 2.7).
- Política de backup e quem restaura.

## 2. O que inclui
- CI com os 4 portões desde o primeiro commit (04, 4.1), `npm ci`, Node fixado, UTC.
- Lint de mensagem de commit (Velix #269) e PR obrigatório para a `main`.
- Deploy com migration **antes** e código tolerante ao schema antigo (04, 1.1).
- Backup automático e **uma restauração testada** antes do aceite.
- Alertas: erro em produção, cobrança dos fornecedores, fila de eventos presa.
- Runbooks da `PASSAGEM.md`.

## 3. Guardas obrigatórias
- Teste de CI que reprova migrations com prefixo duplicado (04, 1.9).
- `.env.example` conferido contra o código.

## 4. Teste de aceite
Linhas das seções 1 e 8 do `ACEITE.md`.
