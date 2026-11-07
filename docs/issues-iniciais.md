# Issues iniciais

Para criar neste repositório, uma por item, na ordem. Rótulos entre colchetes. Cada issue de execução técnica é aberta no repositório do sistema e ligada à mestra daqui.

## Fase 0 — Rede de segurança [fase-0-seguranca]

1. **Verificar chave antiga do GCP e Drive** [tarefa] — checklist da fase 0 do `PLANO.md`. Execução manual do dono (compartilhamento do Drive, colaboradores, repositórios antigos). Pronto quando o risco residual estiver registrado no memorando do `novo-digipop`.
2. **Monitor de uptime e alertas** [tarefa, repo-api] — `/health`, página de login, 5xx e webhook do Asaas. Execução em `novo-digipop`.
3. **Restore de backup testado e runbook** [tarefa, repo-api] — restore completo em banco de teste com tempo medido; runbook de uma página. Execução em `novo-digipop`.
4. **Teste de carga com o dobro do tráfego** [tarefa, repo-api] — `stress-test.yml` contra staging. Execução em `novo-digipop`.

## Fase 1 — Medição [fase-1-medicao]

5. **Churn e funil dos últimos 12 meses** [tarefa, metrica] — duas consultas do `PLANO.md`, resultado em `metricas/`. Revisar as metas.
6. **Campo "Como conheceu o DigiPop?" no cadastro** [tarefa, repo-api, repo-front] — cadastro e trial.
7. **Painel mensal de métricas** [tarefa, metrica] — primeiro fechamento em `metricas/2026-11.md`.

## Fase 2 — Venda [fase-2-venda]

8. **Roteiro de venda no treinamento e nos serviços de regularização** [tarefa] — roteiro de 10 minutos, conta de teste criada na reunião, acompanhamento nos dias 1, 4 e 7.
9. **Registro de cadastros e resultado no Bitrix** [tarefa] — inclui o campo "Origem".
10. **Chamada para o teste grátis nos 5 posts de maior tráfego** [tarefa, repo-site] — com UTM. Execução em `wordpress-solucao`.
11. **Reescrever `/digipop/` como página de produto** [tarefa, repo-site] — preço e botão único. Execução em `wordpress-solucao`.
12. **Campanha para a base antiga** [tarefa] — clientes de cadastro e renovação que nunca assinaram o sistema.

## Fase 3 — Previsibilidade [fase-3-previsibilidade]

13. **Ciclo anual de cobrança** [tarefa, repo-api] — hoje só `MONTHLY`. Exige confirmação do mantenedor.
14. **Auditar o `ReferralCode` e definir a recompensa** [tarefa, repo-api]
15. **Renovação da rede de 200 seats (maio/2027)** [tarefa, decisao] — reajuste de 4,5% proposto; prazo e autorização de caso.
16. **Parcerias com redes, centrais e associações** [tarefa]

## Fase 4 — Ads [fase-4-ads]

17. **Dívida: saber de onde vem cada cliente** [divida] — checklist da seção "Dívida" do `PLANO.md`. Bloqueia o retorno do Ads.
18. **Retomar o Google Ads** [tarefa] — depende da #17. R$ 20 a 30 por dia por 4 semanas; critérios em `decisoes/0002-ads-pausado.md`.
