# Setup Guide - LuzIAssistant Blog

## Repositório criado localmente ✅

O repositório Git foi inicializado com sucesso.

## Próximo passo: Criar no GitHub

### Passo 1: Criar repositório no GitHub

1. Acesse [github.com/new](https://github.com/new)
2. Nome do repositório: `luziassistant-twitter-blog`
3. Descrição: Blog conectado ao Twitter/X - Conteúdo sobre IA e tecnologia
4. Marque "Public" (para GitHub Pages funcionar)
5. **Não** marque "Initialize with README" (já temos arquivos locais)
6. Clique em "Create repository"

### Passo 2: Conectar e fazer push

Execute no terminal:

```bash
cd /Volumes/Nino1TB/openclaw-home/.openclaw/workspace/projects/luziassistant-twitter-blog

git branch -M main
git remote add origin https://github.com/SEU_USERNAME/luziassistant-twitter-blog.git
git push -u origin main
```

### Passo 3: Configurar GitHub Pages

1. Acesse [github.com/settings/pages](https://github.com/settings/pages) para o repositório
2. Ou vá em: Settings → Pages (no menu lateral)
3. Source: Deploy from a branch
4. Branch: `main` / `root`
5. Clique em "Save"

### Passo 4: Aguardar deployment

- GitHub vai deployar o site Jekyll
- Aguarde 2-3 minutos
- Acesse: `https://SEU_USERNAME.github.io/luziassistant-twitter-blog/`

## Estrutura do Projeto

```
luziassistant-twitter-blog/
├── _config.yml           # Configuração Jekyll
├── _layouts/            # Layouts (default, post)
├── _includes/           # Componentes reutilizáveis
├── _sass/              # Estilos SCSS
├── posts/               # Posts do blog (Markdown)
├── premium/             # Conteúdo premium
├── assets/              # Imagens, CSS customizado
├── index.md            # Página inicial
└── README.md           # Documentação
```

## Como adicionar novos posts

1. Criar arquivo em `posts/` com formato:
   ```
   posts/AAAA-MM-DD-titulo-do-post.md
   ```

2. Frontmatter:
   ```yaml
   ---
   layout: post
   title: Título do Post
   date: AAAA-MM-DD HH:MM:SS -05:00
   twitter_id: ID_DO_TWEET  (opcional)
   twitter_thread: true/false
   categories: [tecnologia, ia]
   ---
   ```

3. Escrever conteúdo em Markdown
4. Commit e push:
   ```bash
   git add .
   git commit -m "Add: Novo post"
   git push
   ```

## Workflow de Conteúdo

### Criar novo tema (Twitter + Blog):

1. **Twitter Thread**
   - Copywriter cria thread (3-5 tweets)
   - Bard posta no Twitter/X
   - Obter tweet_id do primeiro tweet

2. **Blog Post**
   - Copywriter expande o tema
   - Adicionar frontmatter com twitter_id
   - Criar arquivo em posts/
   - Commit e push

3. **Vídeo Premium**
   - Gravar vídeo explicativo
   - Upload para plataforma premium
   - Adicionar CTA no post do blog

## Templates de CTA

### Twitter → Blog
```
🧵 Thread completa no blog:
[Resumo do tema]

📖 Leia o post completo:
https://SEU_USERNAME.github.io/luziassistant-twitter-blog/
```

### Blog → Premium
```
🎬 Conteúdo Premium
Este post tem um vídeo premium com explicação detalhada.

[Botão: Assinar Premium]
```

## Automação Futura

### Possível cron job:

```bash
# Diariamente: Checar tweets recentes e criar posts
0 10 * * * openclaw sessions spawn agent:content-manager \
  --task "Criar blog post para tweets recentes de @LuzIAssistant"
```

### Possível workflow:

1. Twitter post → Blog post (automático)
2. Blog post → Social media (cross-post)
3. Premium video → Notificação (assinantes)

---

**Links úteis:**
- [Jekyll Docs](https://jekyllrb.com/docs/)
- [GitHub Pages](https://pages.github.com/)
- [Markdown Guide](https://www.markdownguide.org/)
