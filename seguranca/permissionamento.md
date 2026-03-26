# permissionamento.md — Mapeamento de Acesso

> Fonte de verdade para roteamento de agentes e permissões de usuários.
> Grupo: **Imersão OpenClaw nos Negócios** (`-1003617656481`)

---

## 1. Tópicos → Agentes (este grupo)

| Tópico | topic_id | Agente responsável | Bot |
|--------|----------|--------------------|-----|
| General | 1 | Assistente Geral | @agente_geral_imersao_bot |
| ⚙️ Operações | 29 | Assistente Geral | @agente_geral_imersao_bot |
| 📢 Marketing | 8 | Beatriz Almeida | @agente_marketing_imersao_bot |

**Regra:** Cada agente só responde nos tópicos mapeados para ele. Mensagem em tópico não mapeado = ignora silenciosamente (agentId: none).

---

## 2. Pessoas → Bots que podem invocar

| Nome (exemplo) | Telegram ID | Bots permitidos |
|----------------|-------------|-----------------|
| Admin Principal | `111111111` | todos |
| Gestor de Marketing | `222222222` | @agente_marketing_imersao_bot |
| Analista de Operações | `333333333` | @agente_geral_imersao_bot |
| Visitante / Aluno | `444444444` | nenhum (somente leitura) |

> **Nota:** IDs acima são exemplos fictícios. Substituir pelos IDs reais da equipe ao onboar pessoas.

---

## 3. Como funciona o enforcement

### Em grupos com tópicos
- O OpenClaw roteia por `topic_id` → cada tópico tem um `agentId` fixo
- Se `agentId: none`, o bot está presente mas não processa mensagens
- Se o tópico não está mapeado, o comportamento padrão do grupo se aplica

### Em grupos sem tópicos
- O roteamento é por `agentId` do grupo inteiro
- Recomendado: um bot por grupo, com escopo claro

### Por pessoa (allowFrom)
- `allowFrom` define quais Telegram IDs podem acionar cada bot
- Usuário fora da lista = mensagem ignorada
- Para adicionar alguém: incluir o ID em `allowFrom` do bot correspondente no `openclaw.json`

---

## 4. Estado atual do config (openclaw.json)

```
account: assistente → topics: 1=assistente, 8=none, 29=assistente
account: marketing  → topics: 1=none, 8=marketing, 29=none
```

---

*Atualizado: 2026-03-26*
