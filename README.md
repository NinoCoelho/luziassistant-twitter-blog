# LuzIAssistant Blog - Content Factory

Blog do @LuzIAssistant conectado ao Twitter/X. Conteúdo premium e posts automatizados com **sistema de aprovação** antes da publicação.

---

## Estrutura

Este projeto gerencia:
- **Twitter/X Threads** - Conteúdo teaser gratuito
- **Blog** - Expansão de temas (luzia.center)
- **Conteúdo Premium** - Vídeos para assinantes
- **Sistema de Aprovação** - Rascunhos → Revisão → Publicação

---

## Stack

- **GitHub Pages** - Hosting do blog
- **Twitter/X API** - Automação de tweets
- **Jekyll** - Static site generator
- **Markdown** - Conteúdo em Markdown
- **Replicate** - Geração de imagens (Nano Banana Pro)

---

## NEXUS AI Master Plan

**42 Posts** em 7 meses (Jan-Jul 2026)

**Público:** Leigos → Profissionais IA (vendem serviço)
**Progressão Psicológica:**
- 👶 Fase 1 (Confiança) → "Entendo IA!"
- 🧒 Fase 2 (Vitórias) → "Funciona pra mim!"
- 🧑 Fase 3 (Produtividade) → "Economizo 2h/dia!"
- 🧔 Fase 4 (Automação) → "Trabalha sozinho!"
- 👨 Fase 5 (Profissional) → "Ganho R$5k/mês!"
- 👴 Fase 6 (Líder) → "Lidero agência R$20k!"
- 👑 Fase 7 (Mestre) → "Ensino outros!"

Veja `docs/topics.md` para o calendário completo de 42 posts.

---

## Agentes Especializados

### 1. LuzIAssistant 🎯 - Agente Principal
- **Missão:** Orquestrar todo o ecossistema (Twitter + Blog + Visual + Aprovação)
- **Responsabilidade:** Coordenar 42 posts do NEXUS AI Master Plan
- **Sistema de aprovação:** Rascunho → Revisão → Publicação

### 2. TwitterManager 🐦
- **Missão:** Gerenciar postagens no Twitter/X da conta @LuzIAssistant
- **Skill:** twitter-xapi

### 3. BlogManager 📝
- **Missão:** Gerenciar posts do blog Jekyll (luzia.center)

### 4. ContentManager 🎓
- **Missão:** Orquestrador principal de conteúdo

### 5. ImageManager 🎨
- **Missão:** Gerar banners, diagramas e ilustrações (Replicate)
- **Skill:** replicate-image-gen

### 6. Copywriter 🖊
- **Missão:** Escrever texto (blog + thread)

---

## Workflow de Produção Completo

### Pipeline com Aprovação
```
backlog → researching → imagesReady → textReady → draft → review → ready → blogPosted → tweetPosted → completed
```

**Legenda:**
- **draft** - Rascunho criado no GitHub (aguardando aprovação)
- **review** - Em revisão/aprovação pelo Product Owner
- **ready** - Aprovado, pronto para publicar
- **blogPosted** - Post publicado no blog
- **tweetPosted** - Thread publicada no Twitter/X
- **completed** - Tudo sincronizado e feito

---

## Como Usar

### Iniciar Produção de Post

**Opção 1 - Via LuzIAssistant (Recomendado):**
```bash
openclaw sessions spawn agentId="luziassistant" \
  task="Produzir Post 002: Cloud vs Local com imagens + blog post + thread twitter"
```

**Opção 2 - Via Comando:**
```bash
openclaw sessions spawn \
  agentId="content-manager" \
  task="Orquestrar produção completa do Post 002: Cloud vs Local"
```

### Sistema de Aprovação

**1. LuzIAssistant cria rascunho:**
   - Gera imagens (banners, diagramas)
   - Escreve texto (blog + thread)
   - Salva rascunho no GitHub (status: "draft")
   - Envia preview no Telegram para aprovação

**2. Product Owner aprova:**
   - Via comando `/aprovar {ID}`
   - LuzIAssistant publica final (blog + Twitter)

**3. Status atualizado:**
   - draft → ready → blogPosted → tweetPosted → completed

---

## Links

- **Twitter:** [@LuzIAssistant](https://x.com/LuzIAssistant)
- **Blog:** [luzia.center](https://luzia.center)
- **GitHub:** [NinoCoelho/luziassistant-twitter-blog](https://github.com/NinoCoelho/luziassistant-twitter-blog)
- **Controle:** [docs/topics.md](https://github.com/NinoCoelho/luziassistant-twitter-blog/blob/main/docs/topics.md)

---

## Status

- [x] Repositório criado
- [x] GitHub Pages configurado (luzia.center)
- [x] Twitter integration ativa (skill funcionando)
- [x] Tabela de controle atualizada (42 posts)
- [x] LuzIAssistant criado (agente principal)
- [x] Sistema de aprovação documentado

---

## Próximos Passos

### 1. Configurar Agentes no OpenClaw
Veja `SETUP-AGENTS.md` para instruções de como configurar os agentes no sistema OpenClaw.

### 2. Começar Produção
Produzir os próximos 41 posts do NEXUS AI Master Plan seguindo o calendário (2x/semana).

### 3. Expandir Conteúdo Premium
Definir plataforma de assinatura (YouTube, Patreon, Substack) e começar a gravar vídeos.

---

**Atualizado:** 2026-02-25
**Progresso:** 1/42 posts (2.4%)
