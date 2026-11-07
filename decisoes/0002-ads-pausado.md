# 0002 — Google Ads pausado até rastrear a origem dos leads

**Data:** 07/11/2026
**Estado:** vigente

## Contexto

Primeiro teste com disciplina de custo (novembro/2026): R$ 500 na conta, orçamento diário de R$ 19, cerca de 20 resultados no primeiro ciclo. O Google sugeriu aumentar o orçamento e o aumento foi aceito. Resultado final: 32 resultados, a cerca de R$ 15 cada. Não foi possível saber quantos viraram cliente, porque:

- a conversão medida era o clique no botão de WhatsApp, que mede interesse e não lead qualificado;
- o lead no Bitrix e o cadastro no sistema não guardam a origem;
- o histórico anterior (R$ 4,8 mil, 745 cliques no WhatsApp) tem o mesmo problema.

## Decisão

Não colocar mais dinheiro no Ads até a dívida de rastreamento ser paga (issue de dívida no fim do `PLANO.md`).

## Para retomar

- Conversão principal do Ads = `generate_lead` (cadastro do teste grátis).
- Campo "Origem" no Bitrix preenchido pelo comercial na primeira conversa.
- Pergunta "Como conheceu o DigiPop?" no cadastro do sistema.
- UTM em todos os links de anúncio.
- Página `/digipop/` reescrita com preço e botão único para o teste.
- Orçamento de R$ 20 a 30 por dia durante 4 semanas, sem aceitar sugestões automáticas de aumento.
- Critério para continuar: custo por teste de até R$ 100 e custo por cliente pago de até R$ 600.

## Como reverter

Reativar a campanha existente no Google Ads. O custo da pausa é zero.
