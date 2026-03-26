# permissionamento.md — Mapeamento de Acesso

> Fonte de verdade para roteamento de agentes e permissões de usuários.

---

## 1. Grupos → Agentes

| Grupo | group_id | Agente responsável | Bot |
|-------|----------|--------------------|-----|
| Ops - Imersão OpenClaw nos Negócios | `-1003617656481` | Assistente Geral | @agente_geral_imersao_bot |

---

## 2. Pessoas → Bots que podem invocar

| Nome (exemplo) | Telegram ID | Bots permitidos |
|----------------|-------------|-----------------|
| Admin Principal | `111111111` | todos |
| Colaborador de Operações | `222222222` | @agente_geral_imersao_bot |
| Visitante / Aluno | `333333333` | nenhum (somente leitura) |

> **Nota:** IDs acima são exemplos fictícios. Substituir pelos IDs reais ao onboar pessoas.

---

## 3. Como funciona o enforcement

### Em grupos
- Cada grupo tem um agente dono mapeado acima
- Usuário fora do `allowFrom` do bot = mensagem ignorada
- Para adicionar alguém: incluir o Telegram ID no `allowFrom` do bot correspondente no `openclaw.json`

### Regra geral
- Um grupo = um agente responsável
- Fora do mapeamento = sem resposta

---

*Atualizado: 2026-03-26*
