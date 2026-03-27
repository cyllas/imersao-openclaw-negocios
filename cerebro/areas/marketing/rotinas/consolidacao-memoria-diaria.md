# Rotina: Consolidação de Memória Diária

## O que faz
Revisa as notas do dia em `memory/YYYY-MM-DD.md`, identifica informações relevantes e consolida nos arquivos corretos do `cerebro/`. Faz git push ao final.

## Frequência
1x/dia — 23:00 BRT (02:00 UTC)

## Escopo de consolidação

| Tipo de informação | Destino no cerebro/ |
|-------------------|---------------------|
| Decisões de campanha, pausas, escaladas | `areas/marketing/sub-areas/trafego-pago/` |
| Novos criativos testados, resultados | `areas/marketing/sub-areas/trafego-pago/criativos/` |
| Atualizações de contexto da empresa | `empresa/contexto/` |
| Insights de conteúdo / calendário | `areas/marketing/sub-areas/conteudo/` |

## Critério de relevância
Consolidar no cerebro/ quando a nota contiver:
- Decisão tomada (pausar/escalar campanha)
- Dado de performance (ROAS, CPA, CTR, CPM)
- Novo contexto de empresa relevante para marketing
- Alerta de ROAS < 1.0 por 3+ dias

Notas de rascunho sem decisão clara podem permanecer só em `memory/`.

## Passos
1. Ler `memory/YYYY-MM-DD.md` do dia atual
2. Classificar cada nota por tipo
3. Gravar nos arquivos corretos do `cerebro/`
4. `git add . && git commit -m "consolidação diária marketing [YYYY-MM-DD]" && git push`
5. Confirmar consolidação no chat

## Configuração do Cron

```
Nome: consolidacao-memoria-diaria-marketing
Schedule: 0 2 * * *  (23h BRT, todo dia)
Prompt: "Execute a rotina de consolidação de memória diária: leia memory/ do dia, grave informações relevantes no cerebro/ e faça git push."
```

---

*Criado: março 2026*
