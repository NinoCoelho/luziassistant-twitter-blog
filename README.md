# LuzIAssistant Blog - Content Factory

Blog do @LuzIAssistant conectado ao Twitter/X. Conteúdo premium e posts automatizados.

## Estrutura

Este projeto gerencia:
- **Twitter/X Threads** - Conteúdo teaser gratuito
- **Blog** - Expansão de temas
- **Conteúdo Premium** - Vídeos para assinantes

## Stack

- **GitHub Pages** - Hosting do blog
- **Twitter/X API** - Automação de tweets
- **Jekyll** - Static site generator (ou Next.js/Vite)
- **Markdown** - Conteúdo em Markdown

## Workflow

1. Criar tema → 2. Gerar thread Twitter → 3. Escrever blog post → 4. Gravar vídeo premium
5. Publicar tweet com CTA para blog
6. Blog tem CTA para assinatura premium

## Setup

Veja [SETUP.md](SETUP.md) para instruções completas de como:
1. Criar repositório no GitHub
2. Configurar GitHub Pages
3. Fazer push do projeto
4. Adicionar novos posts

## Sistema de Controle

### Tópicos (42 Posts)
**Arquivo:** `docs/topics.md`

Contém:
- 42 posts estruturados (Jan-Jul 2026)
- Progressão psicológica em 7 fases (Confiança → Mestre)
- Sistema de status: `backlog → researching → imagesReady → textReady → blogPosted → tweetPosted → completed`
- Controle completo de cada post (banner URL, blog URL, thread ID, premium)

### Workflow de Controle
```bash
# Antes de postar:
git pull origin main  # Atualiza topics.md
cat docs/topics.md       # Lê tabela de controle

# Após postar:
git add docs/topics.md
git commit -m "Update: Post 001 status → completed"
git push
```

### Agents
- **ImageManager** 🎨 - Gera banners (com hooks), diagramas, ilustrações
- **TwitterManager** 🐦 - Posta threads (3-5 tweets)
- **BlogManager** 📝 - Cria posts Jekyll (Markdown)
- **ContentManager** 🎯 - Orquestrador (coordena todos)

Veja [SETUP-AGENTS.md](SETUP-AGENTS.md) para configuração completa.

## NEXUS AI Master Plan

**42 Posts em 7 Meses (Jan-Jul 2026)**
- Público: Leigos → Profissionais IA
- Progressão: Confiança (Mês 1) → Mestre (Mês 7)
- Regra: ZERO CLI até Post 30 (leigo não vê terminal)

**Controle completo:** `docs/topics.md`
- Tabela com todos os 42 posts
- Status de cada um
- Links (banner, blog, thread)
- Prioridade e fase

**Fluxo de produção:**
1. ImageManager gera imagens (banners, diagramas)
2. Copywriter escreve texto (blog + thread)
3. BlogManager cria post Jekyll
4. TwitterManager posta thread
5. Atualizar `docs/topics.md` (backlog → completed)

## Status

- [x] Repositório criado localmente
- [x] Estrutura Jekyll configurada
- [x] Repositório criado no GitHub ✅
- [x] GitHub Pages configurado ✅ (luzia.center)
- [x] Twitter integration ativa (skill funcionando)
- [x] Agentes especializados criados ✅
- [ ] Premium platform configurada

## Links

- Twitter: [@LuzIAssistant](https://x.com/LuzIAssistant)
- GitHub: [NinoCoelho/luziassistant-twitter-blog](https://github.com/NinoCoelho/luziassistant-twitter-blog)
- Blog: [luzia.center](https://luzia.center/)

## Agentes Especializados

- 🐦 **TwitterManager** - Gerencia postagens no Twitter/X
- 📝 **BlogManager** - Gerencia posts do blog Jekyll
- 🎯 **ContentManager** - Orquestrador principal
- 🎨 **ImageManager** - Gera banners, diagramas e ilustrações

Veja [SETUP-AGENTS.md](SETUP-AGENTS.md) para configurar os agentes.
