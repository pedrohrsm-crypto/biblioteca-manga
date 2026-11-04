# Módulo — Privacidade e LGPD (base)

**Papéis:** o cliente é o **controlador**; o freelancer é **operador** (`CONTRATO_CHECKLIST.md`).
**Horas do dono (hipótese):** 1 h (mapa de dados e aprovação da política pelo cliente). Dado sensível (saúde, crianças, biometria) é inédito e pede revisão do cliente. **Construção:** exclusão de conta e log sem dado pessoal prontos no `starter`.

## 1. Decisões do Dia 0
- **Mapa de dados:** que dado pessoal, para quê (base legal), onde mora, quem lê, por quanto tempo.
- **Retenção:** prazo de cada tabela com dado pessoal (Velix #104: nenhuma tabela tinha retenção).
- Textos de política e termos: do cliente. O freelancer liga ao cadastro, não redige como advogado.

## 2. O que inclui
- Consentimento registrado quando a base legal for consentimento.
- Exclusão de conta que apaga ou anonimiza os dados pessoais de verdade, cancela cobranças vivas e encerra a sessão (Velix #204, #247).
- Exportação dos dados do titular, quando o escopo pedir.
- Logs e monitoramento de erros sem dado pessoal.
- Origem declarada em links e funis, sem rastrear além do que a política diz (Velix #158).

## 3. Guardas obrigatórias
- Teste de exclusão de ponta a ponta.
- Logger que recusa campos de dado pessoal.

## 4. Teste de aceite
Linhas da seção 6 do `ACEITE.md`.
