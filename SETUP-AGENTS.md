# LuzIAssistant Agents - Setup Guide

**Data:** 2026-02-25
**Projeto:** LuzIAssistant Blog + Twitter/X Autônomo

---

## Visão Geral

Este guia explica como configurar e integrar os 3 agentes especializados do projeto LuzIAssistant ao OpenClaw principal.

### Agentes Criados

1. **TwitterManager** 🐦 - Gerencia postagens no Twitter/X
2. **BlogManager** 📝 - Gerencia posts do blog Jekyll
3. **ContentManager** 🎯 - Orquestrador principal (coordena os outros 2)

---

## Estrutura do Projeto

```
luziassistant-twitter-blog/
├── agents/
│   ├── TwitterManager/
│   │   ├── SOUL.md
│   │   ├── templates/
│   │   └── logs/
│   ├── BlogManager/
│   │   ├── SOUL.md
│   │   ├── templates/
│   │   └── logs/
│   └── ContentManager/
│       ├── SOUL.md
│       ├── docs/
│       │   ├── themes.md
│       │   └── calendar.md
│       └── logs/
├── posts/                    # Posts Jekyll
├── premium/                  # Conteúdo premium
└── README.md
```

---

## Integração com OpenClaw

### Opção 1: Como Sub-Agentes (RECOMENDADO)

Os agentes funcionam como sub-agentes do agent principal, sem ser registrados globalmente.

#### Vantagens:
- Isolamento total no projeto LuzIAssistant
- Fácil de gerenciar e testar
- Pode ser usado via `sessions_spawn`

#### Como usar:

```python
# No agent principal (ex: Bard ou novo "LuzIAssistant" agent)
sessions_spawn(
    agentId="twitter-manager",
    task="Criar thread de Twitter para o tema: AI Delta Framework",
    mode="run"
)
```

### Opção 2: Como Agentes Globais

Registrar no `openclaw.json` como agents completos.

#### Vantagens:
- Acesso direto via comando
- Pode ser chamado de qualquer parte do sistema

#### Como configurar:

**1. Criar os agentes no sistema:**

```bash
# Copiar SOUL.md para o local correto
mkdir -p ~/.openclaw/agents/twitter-manager
mkdir -p ~/.openclaw/agents/blog-manager
mkdir -p ~/.openclaw/agents/content-manager

cp /Volumes/Nino1TB/openclaw-home/.openclaw/workspace/projects/luziassistant-twitter-blog/agents/TwitterManager/SOUL.md \
   ~/.openclaw/agents/twitter-manager/

cp /Volumes/Nino1TB/openclaw-home/.openclaw/workspace/projects/luziassistant-twitter-blog/agents/BlogManager/SOUL.md \
   ~/.openclaw/agents/blog-manager/

cp /Volumes/Nino1TB/openclaw-home/.openclaw/workspace/projects/luziassistant-twitter-blog/agents/ContentManager/SOUL.md \
   ~/.openclaw/agents/content-manager/
```

**2. Registrar no openclaw.json:**

```json
{
  "agents": {
    "list": [
      {
        "id": "twitter-manager",
        "name": "TwitterManager",
        "skills": ["twitter-xapi"],
        "identity": {
          "name": "TwitterManager",
          "emoji": "🐦"
        },
        "subagents": {
          "allowAgents": []
        }
      },
      {
        "id": "blog-manager",
        "name": "BlogManager",
        "skills": [],
        "identity": {
          "name": "BlogManager",
          "emoji": "📝"
        },
        "subagents": {
          "allowAgents": ["twitter-manager"]
        }
      },
      {
        "id": "content-manager",
        "name": "ContentManager",
        "skills": [],
        "identity": {
          "name": "ContentManager",
          "emoji": "🎯"
        },
        "subagents": {
          "allowAgents": ["twitter-manager", "blog-manager"]
        }
      }
    ]
  }
}
```

**3. Reiniciar OpenClaw:**

```bash
openclaw gateway restart
```

---

## Uso Recomendado

### Para Produção LuzIAssistant (Autônoma)

Criar um agent global chamado "LuzIAssistant" que coordena todo o fluxo:

```json
{
  "id": "luziassistant",
  "name": "LuzIAssistant",
  "skills": ["twitter-xapi"],
  "identity": {
    "name": "LuzIAssistant",
    "emoji": "🤖"
  },
  "subagents": {
    "allowAgents": ["twitter-manager", "blog-manager", "content-manager"]
  }
}
```

**Workflow do LuzIAssistant:**

1. Receber temas do Product Owner (via Telegram topic 3)
2. Delegar para ContentManager
3. ContentManager coordena TwitterManager + BlogManager
4. Reportar progresso ao Product Owner

### Para Teste e Desenvolvimento

Usar `sessions_spawn` sem registro global:

```python
# Testar TwitterManager
sessions_spawn(
    agentId="twitter-manager",
    task="Criar thread de teste",
    mode="run"
)

# Testar BlogManager
sessions_spawn(
    agentId="blog-manager",
    task="Criar post de teste",
    mode="run"
)

# Testar ContentManager (workflow completo)
sessions_spawn(
    agentId="content-manager",
    task="Orquestrar produção completa para tema: AI Delta",
    mode="run"
)
```

---

## Workflow Completo

### 1. Product Owner Define Temas
```
Input para ContentManager:
- Lista de temas
- Abordagem de cada tema
- Prioridade
- Data alvo
```

### 2. ContentManager Coordena
```
Processo:
1. Receber temas
2. Priorizar tema atual
3. Delegar para TwitterManager
4. Receber thread_id
5. Delegar para BlogManager
6. Receber blog_url
7. Verificar sincronização
8. Atualizar calendário
```

### 3. TwitterManager Cria Thread
```
Processo:
1. Receber tema + abordagem
2. Criar 3-5 tweets
3. Postar no Twitter/X
4. Retornar thread_id
```

### 4. BlogManager Cria Post
```
Processo:
1. Receber tema + thread_id
2. Escrever post Markdown
3. Criar arquivo em posts/
4. Commit + push para GitHub
5. Retornar blog_url
```

---

## Configuração de Skills

### Twitter/X API Skill

Já deve estar registrado em `openclaw.json`:

```json
{
  "skills": {
    "entries": {
      "twitter-xapi": {
        "enabled": true
      }
    }
  }
}
```

### Verificar Skill

```bash
# Verificar se skill está carregado
openclaw status

# Testar skill via TwitterManager agent
sessions_spawn agentId="twitter-manager" task="twitter_health_check"
```

---

## Cron Jobs Sugeridos

### Daily Status Check (09:00)

```bash
openclaw cron add \
  --schedule '{"kind":"cron","expr":"0 9 * * *","tz":"America/New_York"}' \
  --sessionTarget isolated \
  --name "LuzIAssistant - Daily Status Check" \
  --payload '{"kind":"agentTurn","message":"Gerar status diário de produção de conteúdo LuzIAssistant. Verificar calendar.md, themes.md, atualizar métricas. Enviar relatório para Telegram topic 3.","timeoutSeconds":300}' \
  --delivery '{"mode":"announce","channel":"telegram","to":"-1003785765104"}'
```

### Weekly Content Publish (Terça e Sexta 14:00)

```bash
openclaw cron add \
  --schedule '{"kind":"cron","expr":"0 14 * * 2,5","tz":"America/New_York"}' \
  --sessionTarget isolated \
  --name "LuzIAssistant - Weekly Content Publish" \
  --payload '{"kind":"agentTurn","message":"Verificar e publicar conteúdo agendado para hoje (terça/sexta 14:00). Delegar para ContentManager.","timeoutSeconds":600}' \
  --delivery '{"mode":"announce","channel":"telegram","to":"-1003785765104"}'
```

---

## Teste do Sistema

### Teste 1: TwitterManager Isolado
```bash
sessions_spawn \
  agentId="twitter-manager" \
  task="Criar thread de teste para o tema: OpenClaw Showcase. CTA target: blog." \
  mode="run"
```

### Teste 2: BlogManager Isolado
```bash
sessions_spawn \
  agentId="blog-manager" \
  task="Criar post de blog para o tema: OpenClaw Showcase. Thread ID: TEST123." \
  mode="run"
```

### Teste 3: ContentManager (Workflow Completo)
```bash
sessions_spawn \
  agentId="content-manager" \
  task="Orquestrar produção completa para o tema: AI Delta Framework. Abordagem: Tutorial. Tem premium: true. Data alvo: 2026-02-28." \
  mode="run"
```

### Teste 4: LuzIAssistant (End-to-End)
```bash
sessions_spawn \
  agentId="luziassistant" \
  task="Processar tema pendente do backlog. Selecionar tema mais prioritário, delegar para ContentManager, publicar Twitter + Blog." \
  mode="run"
```

---

## Troubleshooting

### Problema: Skill twitter-xapi não encontrado

**Solução:**
1. Verificar se skill está em `skills.entries` do `openclaw.json`
2. Verificar se Bard agent tem skill `twitter-xapi` listado
3. Reiniciar gateway: `openclaw gateway restart`

### Problema: Agent não pode ser spawnado

**Solução:**
1. Verificar se SOUL.md existe no local correto
2. Verificar permissões de arquivo
3. Verificar logs do OpenClaw: `openclaw status --deep`

### Problema: Twitter/X não autenticado

**Solução:**
1. Verificar se xurl está autenticado: `xurl whoami`
2. Se 401, reautenticar no seu terminal
3. Verificar se créditos API estão disponíveis

### Problema: Blog não deploya no GitHub Pages

**Solução:**
1. Verificar se commit foi feito: `git log --oneline`
2. Verificar se push foi feito: `git log origin/main`
3. Verificar Settings → Pages no GitHub
4. Aguardar 2-3 minutos para deploy

---

## Próximos Passos

### Imediatos (hoje)
- [ ] Escolher método de integração (sub-agents ou global)
- [ ] Configurar agent LuzIAssistant (se global)
- [ ] Testar TwitterManager isolado
- [ ] Testar BlogManager isolado

### Curto prazo (esta semana)
- [ ] Testar ContentManager (workflow completo)
- [ ] Criar cron job para publicação semanal
- [ ] Publicar AI Delta Framework (2026-02-28)
- [ ] Configurar analytics do blog

### Médio prazo (próximas 2 semanas)
- [ ] Automatizar completamente o fluxo
- [ ] Configurar plataforma premium (YouTube/Patreon)
- [ ] Criar 2-3 temas novos
- [ ] Ajustar calendário editorial baseado em métricas

---

## Documentação Relacionada

- **TwitterManager:** `agents/TwitterManager/SOUL.md`
- **BlogManager:** `agents/BlogManager/SOUL.md`
- **ContentManager:** `agents/ContentManager/SOUL.md`
- **Temas:** `agents/ContentManager/docs/themes.md`
- **Calendário:** `agents/ContentManager/docs/calendar.md`
- **Setup Blog:** `SETUP.md`

---

**Atualizado:** 2026-02-25
**Responsável:** LuzIAssistant System
