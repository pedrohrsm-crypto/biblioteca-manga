# Planejamento com as áreas — <projeto>

> Procedimento PFA-01, passo 1.0 (framework, capítulo 14). Preencha **antes** do primeiro commit de código.
> **Framework:** vX.Y · **Data:** AAAA-MM-DD · **Escala:** S | M | G · **Aprovado pelo dono:** [ ]
>
> Para cada área: leia a fonte indicada no capítulo 14, §2, com as perguntas de lá. Todo item cita de onde veio (`repo/arquivo §seção`); item sem fonte é opinião.
> Área que não se aplica: apague as linhas e escreva o motivo. Nenhuma área fica em branco.

## 0. O projeto em uma página
- **Problema e para quem:**
- **Tipo de produto** (capítulo 11, §5): SaaS web | API | mobile | IA/LLM | ferramenta interna
- **Porte** (capítulo 16): curto | médio | longo — cronograma em `docs/CRONOGRAMA.md`
- **Primeiro marco e data:**
- **Fora do escopo:**

## 1. UX/UI
- **Exige:**
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`):
- **Mede** (métrica e meta):
- **Portão** (→ `DIA_ZERO.md` ou CI):
- **Fontes lidas:**

## 2. Segurança
- **Exige:**
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`):
- **Mede** (métrica e meta):
- **Portão** (→ `DIA_ZERO.md` ou CI):
- **Fontes lidas:**

## 3. DevOps
- **Exige:**
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`):
- **Mede** (métrica e meta):
- **Portão** (→ `DIA_ZERO.md` ou CI):
- **Fontes lidas:**

## 4. Desempenho
- **Exige:**
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`):
- **Mede** (métrica e meta):
- **Portão** (→ `DIA_ZERO.md` ou CI):
- **Fontes lidas:**

## 5. Marketing
- **Exige:**
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`):
- **Mede** (métrica e meta; o critério de sucesso de valor vai para o `GESTAO.md` §1):
- **Portão** (→ `DIA_ZERO.md` ou CI):
- **Fontes lidas:**

## 6. Suporte
- **Exige** (canais de pré e pós-aquisição, prazo de resposta, rotina diária):
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`; ex.: quem responde e por qual meio):
- **Mede** (tempo de primeira resposta, tempo de resolução, contatos por cliente ativo):
- **Portão** (→ `DIA_ZERO.md`; ex.: o canal de contato recebe um e-mail de teste):
- **Fontes lidas:**

## 7. Back-end e dados
- **Exige** (modelo de dados e de acesso; ordem migration → deploy; teto de duração por rota):
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`):
- **Mede** (métrica e meta; ex.: rotas sem teto, rotinas agendadas sem trava):
- **Portão** (→ `DIA_ZERO.md` ou CI; ex.: migration aplicada antes do deploy):
- **Fontes lidas:**

## 8. Pagamentos
- **Exige** (processador e chave restrita; catálogo único em centavos; webhook e reconciliação):
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`; o modelo de preço vem do Marketing):
- **Mede** (métrica e meta; ex.: divergência de preço catálogo × processador, reconciliação parada):
- **Portão** (→ `DIA_ZERO.md` ou CI):
- **Fontes lidas:**

## 9. Privacidade e LGPD
- **Exige** (mapa de dados; operadores na política; exportação e exclusão; retenção por tabela):
- **Arrisca** (→ issue `risco`):
- **Decidir** (→ issue `decisao`; finalidade, base legal e prazo são do dono):
- **Mede** (métrica e meta; ex.: colunas pessoais sem finalidade, tabelas sem prazo de retenção):
- **Portão** (→ `DIA_ZERO.md` ou CI):
- **Fontes lidas:**

## 10. Conflitos entre áreas
| Área A quer | Área B exige | Issue `decisao` |
|---|---|---|
| | | #  |

## 11. O que sai deste plano
- [ ] Riscos abertos como issues `risco` (passo 1.5)
- [ ] Decisões abertas como issues `decisao` (passo 1.5)
- [ ] Portões copiados para o `DIA_ZERO.md` (passo 1.4)
- [ ] Critério de sucesso de valor no `GESTAO.md` §1
