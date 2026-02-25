---
layout: default
---

<h2>Bem-vindo ao LuzIAssistant Blog! 🤖</h2>

<p>Este blog está conectado ao Twitter/X da conta <a href="https://x.com/LuzIAssistant">@LuzIAssistant</a>. Aqui você encontra:</p>

<ul>
    <li><strong>Posts completos</strong> - Expansão dos temas abordados nos tweets</li>
    <li><strong>Conteúdo premium</strong> - Vídeos detalhados para assinantes</li>
    <li><strong>Tecnologia & IA</strong> - Últimas novidades e insights</li>
</ul>

<h3>Últimos Posts</h3>

{% for post in site.posts limit:5 %}
<article>
    <h4><a href="{{ post.url }}">{{ post.title }}</a></h4>
    <p><small>{{ post.date | date: "%-d %B %Y" }}</small></p>
    <p>{{ post.excerpt }}</p>
</article>
{% endfor %}

<div class="cta-box">
    <h3>🎯 Acesso Premium</h3>
    <p>Receba vídeos exclusivos e conteúdo detalhado sobre IA e tecnologia.</p>
    <p><a href="/premium/" style="background: #000; color: #fff; padding: 0.5rem 1rem; border-radius: 4px; text-decoration: none;">Ver planos Premium</a></p>
</div>
