# Módulo — Acessibilidade (base)

**Meta:** WCAG 2.2 nível AA nas telas do escopo. No Brasil, a Lei 13.146/2015 (art. 63) exige acessibilidade nos sites de empresas com sede ou representação no país: é requisito legal do cliente.
**Horas do dono (hipótese):** 0,5 h (temas e cores da marca; a guarda de contraste pode recusar a cor original, como no piloto-a). **Construção:** pronta no `starter`; cada tela nova entra no e2e com axe.
**Fonte da área:** UX-UI, `07-checklists.md` §A e §G (14 §2); categorias 5, 6 e 7 do 04.

## 1. Decisões do Dia 0
- Temas do produto (claro, escuro, marca) e a largura mínima (360 px).
- Tokens de cor com par em **todos** os temas, e tamanhos em `rem`.

## 2. O que inclui
- Contraste mínimo de 4,5:1 no texto e 3:1 em componentes e foco, em todos os temas.
- Foco visível no teclado, ordem lógica, link para pular ao conteúdo.
- Nome acessível igual ao texto visível (WCAG 2.5.3; Velix #224).
- Escala de fonte de 140% sem quebrar o layout; nada cortado a 360 px.
- Formulários com rótulo, erro anunciado e o que foi digitado preservado quando o envio falha (Velix #207).

## 3. Guardas obrigatórias
- axe no e2e de toda tela do escopo.
- Teste de pareamento de tokens por tema (04, 6.2) e guarda do anel de foco (Velix, `guarda-anel-de-foco`, 26-Set).
- Catraca de `px` e de hex literal: o número só desce.

## 4. Teste de aceite
Linhas da seção 3 do `ACEITE.md`.
