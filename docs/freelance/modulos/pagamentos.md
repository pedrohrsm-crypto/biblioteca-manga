# Módulo — Pagamentos

**Quando usar:** qualquer cobrança do cliente aos usuários dele. **Variantes:** pagamento único · assinatura · sinal de reserva · marketplace (repasse a terceiros, tratar como inédito).
**Horas do dono (hipótese):** 1,5 a 2 h (conta do cliente verificada, meios de pagamento, preço, roteiro de virada). **Construção:** a variante único vem pronta no `starter`; assinatura é inédito até existir em código. Calibrar com `prever.py calibrar --recurso dono`.

## 1. Decisões do Dia 0 (registrar como `decisao`)
- **Processador:** o padrão é o Stripe (02 §6). Meios locais como Pix e boleto dependem do país e do tipo de conta do cliente: **conferir na documentação atual do processador, no Dia 0**, antes de prometer na proposta. Alternativa local comum: Mercado Pago (vira inédito até existir módulo).
- **Titular da conta:** o cliente, com a verificação da empresa feita por ele. Sem conta verificada, o módulo fica em modo de teste e a proposta diz isso.
- **Nota fiscal:** o processador **não** emite. Se o cliente precisa, é integração à parte (inédito) ou processo manual do cliente, escrito na proposta.
- **Versão da API** fixada no código (04, 3.2).
- **Regra única de "o que o usuário tem direito"** (plano efetivo, compra válida) num lugar só (04, 3.3).

## 2. O que inclui
- Checkout (ou link de pagamento) com a chave de idempotência derivada do **pedido**, nunca de horário.
- Webhook assinado e verificado, idempotente, que só responde 2xx depois de gravar.
- Tela de volta do pagamento que consulta o estado real, e não o que a URL diz.
- Estorno e cancelamento com efeito no acesso.
- Reconciliação diária: um job que confere o processador contra o banco e corrige o que o webhook perdeu.
- Roteiro de virada de teste para produção.

## 3. Guardas obrigatórias
| Guarda | Previne | Caso real |
|---|---|---|
| Webhook devolve 500 quando a gravação falha, para o processador retentar | cobrança sem acesso liberado | 04, 3.1; Velix #205 |
| Evento registrado antes de processar, com reserva recuperável se o processamento morrer no meio | evento preso para sempre | Velix #205 |
| Chave de idempotência derivada do pedido, e trava contra segunda compra enquanto a primeira está aberta | duas abas cobram duas vezes | Velix #206 (a chave usava `Date.now()`) |
| Nenhuma restrição única que impeça o mesmo cliente de assinar de novo depois de cancelar | recompra bloqueada | Velix #203 |
| Exclusão de conta cancela antes as cobranças recorrentes vivas | cobrança de quem saiu | Velix #204 |
| Evento de conta já excluída vira aviso e 2xx, não erro em laço | reentrega infinita | Velix #234 |
| Customer de teste nunca reaproveitado em produção | checkout travado na virada | 04, 3.4 |
| Checklist "evento novo tratado → marcar no endpoint de produção" | evento ignorado em produção | 04, 3.6 |

## 4. Teste de aceite (modo de teste do processador)
1. Compra com sucesso → acesso liberado; webhook reenviado duas vezes → nada duplica.
2. Cartão recusado → nenhum acesso, mensagem clara.
3. Duas abas pagando o mesmo pedido → uma cobrança só.
4. Estorno → acesso retirado; recompra depois do estorno → funciona (04, 3.5).
5. Assinatura: troca de plano, falha de renovação (inadimplência), cancelamento.
6. Reconciliação: apagar à mão a gravação de um pagamento de teste → o job de reconciliação recupera.

## 5. Fontes
04 categoria 3 · 02 §6 · Velix, épico de resiliência (#202) e frentes #203 a #206, #211 (26 e 27-Set-2026).
