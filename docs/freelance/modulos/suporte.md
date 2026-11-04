# Módulo — Suporte (base)

**Duas fases, separadas de propósito** (item 23a do Velix, 13 §4.6): **pré-aquisição** (quem pergunta antes de comprar) e **pós-aquisição** (quem já comprou e tem um problema). Num trabalho freelance há ainda uma terceira: o suporte **do freelancer ao cliente**, na garantia e depois dela.
**Horas do dono (hipótese):** 1 h (canais, prazos e quem responde, decididos com o cliente). **Construção:** a página de contato e o FAQ são do `starter`; o widget de relato com triagem no admin ainda é inédito (existe no Velix, primeira ocorrência).
**Fonte da área:** `pedrohrsm-crypto/suporte` (criado em 30-Set-2026, a absorver em `analistas/suporte/`).

## 1. Decisões do Dia 0 (registrar como `decisao`)
- **Canais do produto do cliente:** um endereço de atendimento no domínio do cliente (nunca o de privacidade, que é canal de LGPD) e, se houver, WhatsApp comercial. Tudo em nome do cliente.
- **Quem responde e em quanto tempo:** uma pessoa nomeada do lado do cliente, com prazo de primeira resposta (sugestão: 1 dia útil) e de resolução.
- **Onde fica o histórico** de cada conversa (a caixa do e-mail, uma ferramenta de atendimento), para quem assumir depois.
- **Suporte do freelancer:** canal e prazo na garantia (sugestão: defeito da barra respondido em 1 dia útil) e o plano depois dela (por hora ou pacote mensal, opcional).

## 2. O que inclui
- **Pré-aquisição:** FAQ com as objeções reais da descoberta, contato visível antes do pagamento, e o que acontece depois da compra dito na página de venda.
- **Pós-aquisição:** contato visível na área logada; guia de uso por papel; mensagens de erro que dizem o que fazer; e-mail de confirmação de pagamento.
- **Ciclo pergunta → melhoria:** a terceira pergunta igual no mês vira FAQ, guia ou issue `erro` (13 §4.6).

## 3. Guardas obrigatórias
- O canal de contato **recebe de verdade**: e-mail de teste enviado e respondido antes do aceite (04, erro 2.8: o botão que nunca enviou e-mail).
- Formulário de contato com proteção contra robô e sem guardar mais dado pessoal do que a resposta precisa.
- Nenhum endereço de suporte aponta para a caixa pessoal do freelancer.

## 4. Teste de aceite
Linhas da seção 9 do `ACEITE.md`.
