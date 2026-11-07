# Plano de crescimento DigiPop — 12 meses

Atualizado em 07/11/2026. Versão com comentários e edição inline: documento no Claude (o texto daqui é a fonte de registro a partir de agora).

## Ponto de partida

O DigiPop fatura R$ 14.164 por mês em 62 assinaturas ativas do Asaas, e 43% disso vem de um único cliente, a rede de 200 seats. O gargalo é venda e preço, não código.

| Fonte | Assinaturas | MRR (R$/mês) | Observação |
| --- | --- | --- | --- |
| Rede de 200 seats | 1 | 6.032 | Cerca de R$ 30 por loja; 42,6% do total |
| Consultoria técnica | 1 | 900 | Não é o SaaS |
| Avulsos | 60 | 7.232 | Ticket médio R$ 120; valores de R$ 79 a R$ 345 |
| **Total** | **62** | **14.164** | Asaas, assinaturas abertas, 05/11/2026 |

- **Custo:** cerca de R$ 400 por mês (Railway entre US$ 20 e 30, Cloudflare cerca de US$ 1, Vercel grátis, cerca de R$ 200 do legado, que deve cair com o fim da migração).
- **Preço:** lista consolidada de **R$ 150 por loja** (ver `decisoes/0001`). Com 20% de imposto, sobram R$ 120 por cliente; a infraestrutura se paga com 3 a 4 clientes.
- **Entrada de clientes:** 1 a 2 vendas por mês, quase todas dentro do treinamento da consultoria do Farmácia Popular. Estimativa do dono: de cada 5 cadastros, 1 ou 2 fecham.
- **Sem medição:** o Asaas não exporta assinaturas encerradas, então o churn é desconhecido. A fase 1 mede com o banco.
- **Equipe:** o dono é o único em marketing e desenvolvimento. Chat e comercial têm equipe. O sistema base foi feito por desenvolvedores externos, sem contrato de manutenção.

## Metas

A meta de 12 meses é levar os avulsos a cerca de R$ 18 mil de MRR, quase o triplo do que a rede de 200 seats paga, e deixar essa rede abaixo de 30% do total. Isso exige sair de 1 a 2 vendas por mês para 6 a 10.

| Horizonte | Vendas novas/mês | Avulsos líquidos | MRR avulsos (R$) | MRR total (R$) | Rede de 200 seats no total |
| --- | --- | --- | --- | --- | --- |
| Hoje (05/11/2026) | 1 a 2 | 60 | 7.232 | 14.164 | 43% |
| 90 dias (fev/2027) | 4 | 72 | 9.000 | 15.900 | 38% |
| 6 meses (mai/2027) | 6 | 88 | 11.400 | 18.300 | 33% |
| 12 meses (nov/2027) | 6 a 10 | 130 | 17.700 | 24.900 | 25% |

**Premissas, a revisar quando o churn for medido:**

- Cada cliente novo entra a R$ 150; o ticket dos antigos não muda.
- A consultoria fica em R$ 900. A rede de 200 seats renova em maio/2027 com reajuste proposto de 4,5% (R$ 6.032 para cerca de R$ 6.303).
- Os avulsos líquidos já descontam churn assumido de 2% ao mês. Para fechar 70 líquidos em 12 meses é preciso vender cerca de 94 brutos.
- Receita líquida de imposto (20%) a R$ 24.900 é cerca de R$ 19.900. Descontados os R$ 400 de infraestrutura, o resultado antes de equipe e horas passa de R$ 19 mil por mês.

**De onde virão as vendas (premissas a validar):**

| Fonte | Base por mês | Fechamento assumido | Vendas por mês |
| --- | --- | --- | --- |
| Cadastros do Farmácia Popular | 5 | 30% a 45% (hoje 20% a 40%) | 1,5 a 2,3 |
| Regularização, troca de endereço e dados (clientes do programa) | cerca de 22 | 10% a 20% | 2,2 a 4,4 |
| Testes vindos do site | 5 a 10 | 20% | 1 a 2 |
| Indicação dos clientes | 60 clientes | 1 indicação por mês | 1 |
| **Total** | | | **6 a 10** |

A linha de regularização é a maior alavanca e a menos certa. Cerca de 50% dos cerca de 45 contratos de consultoria que não são cadastro são de clientes do Farmácia Popular (estimativa do dono). Eles já são clientes e já estão no programa, por isso assumo fechamento mais alto que o do cadastro novo.

## Fase 0 — Rede de segurança (semanas 1 e 2)

Objetivo: poder anunciar sem medo de o sistema cair ou de alguém antigo ter acesso.

**Chave do Google Cloud (verificação de 10 minutos).** A chave veio da versão antiga do sistema. As variáveis `GOOGLE_DRIVE_*` já não existem na Railway, então o sistema atual não a usa. O projeto dela não está nas contas da empresa. Em ordem:

- [ ] Conferir, em Compartilhar, se o Drive do backup externo do legado está compartilhado com algum endereço `*.iam.gserviceaccount.com`; se estiver, remover
- [ ] Revisar colaboradores de `novo-digipop` e `novo-digipop-front`
- [ ] Procurar o mesmo arquivo nos repositórios antigos e nos segredos de Actions
- [ ] Registrar o que sobra como risco aceito (a chave pode continuar válida num projeto de terceiros)

**Acessos de quem saiu.** Repositórios, Railway, Vercel, Cloudflare e AWS são novos e da empresa; os desenvolvedores externos não têm mais acesso à infraestrutura atual (confirmado pelo dono em 07/11/2026).

- [x] GitHub, Railway, Vercel, Cloudflare R2, bucket Amazon (novo, conta da empresa)
- [x] Asaas, Bitrix, domínio e e-mail
- [x] `JWT_SECRET`, `MIGRATION_API_KEY` e senhas de admin

**Ainda por fazer:**

- [ ] Monitor externo de uptime em `/health` da API e na página de login, com aviso no WhatsApp ou e-mail
- [ ] Alerta de erros 5xx e de webhook do Asaas falhando (foi o que quebrou na queda de 22/10)
- [ ] Backup do Postgres: confirmar a política e fazer **um restore completo em banco de teste**, medindo o tempo
- [ ] Runbook de uma página: o que olhar primeiro, como reiniciar, como fazer rollback, quem chamar, acesso de emergência
- [ ] Teste de carga com o dobro do tráfego atual (cerca de 221 mil requisições por semana em setembro) em staging

**Pronto quando:** chave antiga sem acesso a nada seu, alerta de uptime testado, restore feito com tempo medido e runbook salvo no repositório da API.

## Fase 1 — Medição e churn (semanas 2 e 3)

O churn sai do banco: `network_subscriptions` guarda `created_at`, `first_payment_confirmed_at`, `activated_at`, `suspended_at` e `cancelled_at`. Rodar em sessão somente leitura, conferindo as colunas com `\d network_subscriptions`.

```sql
-- Funil por mês de cadastro
SELECT date_trunc('month', created_at)              AS mes,
       count(*)                                     AS cadastros,
       count(first_payment_confirmed_at)            AS pagaram,
       count(*) FILTER (WHERE status IN ('cancelled','suspended')) AS perdidos
FROM network_subscriptions
WHERE status <> 'legacy'
GROUP BY 1 ORDER BY 1;

-- Cancelamentos por mês e MRR perdido
SELECT date_trunc('month', cancelled_at)            AS mes,
       count(*)                                     AS cancelamentos,
       sum(total_price::numeric)                    AS mrr_perdido
FROM network_subscriptions
WHERE cancelled_at IS NOT NULL
GROUP BY 1 ORDER BY 1;
```

Redes migradas do legado podem ter `first_payment_confirmed_at` vazio e distorcer a primeira consulta; listar à parte.

- [ ] Rodar as duas consultas e registrar o churn dos últimos 12 meses em `metricas/`
- [ ] Revisar as metas com o churn real
- [ ] Campo "Como conheceu o DigiPop?" no cadastro e no trial (`novo-digipop`)
- [ ] Painel mensal em `metricas/` (modelo em `metricas/TEMPLATE.md`)

## Fase 2 — Vender mais com o que já existe (semanas 3 a 8)

Meta: 4 vendas por mês.

**A. Consultoria.**

- [ ] Roteiro padrão de 10 minutos: o problema (documento da venda desorganizado e risco de descredenciamento), a demonstração e o preço de R$ 150
- [ ] Criar a conta de teste do cliente durante a reunião (trial de 7 dias)
- [ ] Acompanhamento do comercial nos dias 1, 4 e 7 do trial, com mensagem pronta
- [ ] Registrar cada cadastro e o resultado (fechou, em teste, recusou e por quê) no Bitrix
- [ ] Levar a mesma oferta aos serviços de regularização, troca de endereço e dados
- [ ] Campanha única para a base antiga que nunca assinou o sistema

**B. Site.** Regras do `wordpress-solucao` se aplicam: toda mudança com issue, em rascunho com `noindex` até o dono autorizar.

- [ ] Chamada para o teste grátis nos 5 posts de maior tráfego, com `utm_source` e `utm_content` por post
- [ ] Reescrever `/digipop/` como página de produto, com preço e botão único para o teste
- [ ] Prova social só com autorização por escrito (número real de lojas ativas e depoimentos curtos)
- [ ] Decidir o destino de `/auditoria-farmacia-popular/` depois do checkpoint de 19/11/2026

**Pronto quando:** 2 meses seguidos com 4 ou mais vendas, taxa de fechamento da consultoria medida e pelo menos 5 testes por mês vindos do site.

## Fase 3 — Previsibilidade (semanas 6 a 16)

- [ ] **Plano anual (a testar):** 10 mensalidades à vista por 12 meses (R$ 1.500 por loja em vez de R$ 1.800), ou 12x no cartão. O código só aceita ciclo mensal (`cycle: 'MONTHLY'` em `src/asaas/asaas.types.ts`): abrir issue para o ciclo anual; até lá, piloto com cobrança avulsa no Asaas vinculada pelo Command Center. Mexer em billing exige confirmação do mantenedor. Meta: 20% das vendas novas no anual até o mês 6
- [ ] **Indicação:** o `ReferralCode` é criado no cadastro e a assinatura tem `referred_by_network_id` e `referrer_reward_granted_at`. Auditar o que o código faz antes de prometer prêmio. Oferta sugerida: um mês grátis para quem indica e para quem entra, concedido na primeira fatura paga
- [ ] **Parcerias:** redes pequenas e médias, centrais de compras, associações e sindicatos de farmácias. Tabela com preço decrescente por faixa a partir de 5 lojas, com piso acima de R$ 30 por loja
- [ ] **Renovação da rede de 200 seats (maio/2027):** reajuste de 4,5% proposto; aproveitar para combinar prazo e pedir autorização por escrito para uso do caso. O reajuste é manual no Asaas e no sistema (o preço negociado fica em `total_price`)

**Pronto quando:** 5 planos anuais vendidos, indicação gerando ao menos 1 cliente por mês e conversa ativa com 3 grupos ou associações.

## Fase 4 — Teste pago e decisão de escalar (semanas 8 a 16)

Teto de custo por cliente: **R$ 600**, cerca de 5 meses de margem líquida. Ads só depois das fases 0 e 1 e da dívida abaixo.

- Orçamento de R$ 20 a 30 por dia durante 4 a 8 semanas, Google Ads de busca, termos de intenção de compra, com a lista de palavras negativas do repositório do site
- Conversão do Ads = cadastro do teste grátis, não clique no WhatsApp

| Resultado | Decisão |
| --- | --- |
| Custo por cliente pago até R$ 600 e pelo menos 2 clientes | Dobrar o orçamento, depois subir 30% por mês enquanto o custo se mantiver |
| Custo por teste acima de R$ 100 ou menos de 15% dos testes virando pagos | Pausar e corrigir página e acompanhamento |
| Poucos testes, fechamento alto | Ampliar termos e público, não o orçamento |
| Nenhum cliente com custo por teste normal | O problema é a venda do teste: voltar à fase 2 |

## Dívida — saber de onde vem cada cliente

Primeiro teste de Ads (novembro/2026): R$ 500 na conta, orçamento de R$ 19 por dia, 32 resultados a cerca de R$ 15 cada, sem saber quantos viraram cliente (ver `decisoes/0002`). Ads pausado até pagar:

- [ ] Reconstruir o período: contatos do Bitrix e do WhatsApp, assinaturas e testes criados nas mesmas datas, termos de pesquisa do Ads e eventos `generate_lead` e `whatsapp_click` com origem `google / cpc` no GA4
- [ ] Trocar a conversão principal do Ads para `generate_lead`
- [ ] Campo "Origem" nos leads do Bitrix, preenchido na primeira conversa
- [ ] Pergunta "Como conheceu o DigiPop?" no cadastro e no trial
- [ ] UTM em todos os links de anúncio
- [ ] `/digipop/` reescrita com preço e botão único

## Riscos

| Risco | Sinal | Resposta |
| --- | --- | --- |
| Dependência da rede de 200 seats (43% do MRR) | Aviso de reajuste ou fim de contrato | Crescer avulsos até ela ficar abaixo de 30%; renovação em maio/2027 com reajuste de 4,5% proposto; combinar prazo e autorização de caso |
| Dono como único dev e único marketing | Incidente fora do horário, ou o dono em férias | Runbook, acesso de emergência e alertas na fase 0; contratar manutenção por horas |
| Queda do Postgres (3 GB de RAM, um só) | Repetição da queda de 22/10 | Restore testado, monitor e plano de comunicação com clientes |
| Preço desigual entre clientes | Valores de R$ 79 a R$ 150 para o mesmo produto | Tabela única para novos; reajuste dos antigos só com aviso e depois da fase 2 |
| Meta de vendas acima da capacidade do comercial | Fila de testes sem acompanhamento | Medir cadastros e fechamento antes de subir a meta |
| Mudança legal no Farmácia Popular | Nova portaria ou regra de documento | O site acompanha as portarias; manter o produto alinhado e comunicar rápido |

## O que não fazer agora

- Não anunciar antes das fases 0 e 1 e da dívida de origem.
- Não aceitar sugestões automáticas do Google de aumentar orçamento.
- Não reajustar clientes antigos sem plano de comunicação.
- Não mexer no preço ou contrato da rede de 200 seats fora da renovação de maio/2027.
- Não promover novas funcionalidades pesadas antes de medir o funil.

## Perguntas em aberto

- Quantos dos cerca de 22 clientes de regularização por mês já têm outro sistema.
- Se o legado de R$ 200 por mês tem data para terminar.
