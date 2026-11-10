# demo-django

Projeto desenvolvido seguindo o roteiro "Construindo um site com Django + Tailwind + Docker" — parte 4.

* Aluna: Michelle de Oliveira Pinheiro
* Disciplina: BCC481 – Programação Web
* Professora: Aline Brito

## Sobre o projeto

Site simples feito em Django 5.1, estilizado com Tailwind CSS (via CDN), com dados salvos em SQLite e executado dentro de um container Docker. A página inicial lista as mensagens cadastradas pelo painel administrativo do Django, mostrando o autor, a categoria e as tags de cada uma.

## O que foi feito

### Parte 2

* Novo campo no modelo: o modelo `Mensagem` ganhou o campo `autor` (padrão "Anônimo"), com migração gerada e aplicada no banco (`0002_mensagem_autor`). O autor aparece na página inicial e pode ser preenchido pelo painel admin.
* Nova página: criada a página `/sobre/`, seguindo o fluxo rota → view → template (`home/urls.py`, `home/views.py` e `templates/home/sobre.html`), com link no menu da página inicial.
* Novo visual: o gradiente de fundo da página inicial foi trocado por tons de verde (`emerald` e `teal`).

### Parte 3 — relacionamento um-para-muitos (1:N)

* Novo modelo `Categoria`, com o campo `nome` (único) e ordenação alfabética.
* O modelo `Mensagem` ganhou o campo `categoria`, um `ForeignKey` para `Categoria` com `on_delete=SET_NULL`, `null=True`, `blank=True` e `related_name="mensagens"`. Assim, apagar uma categoria não apaga as mensagens, e `categoria.mensagens.all()` lista as mensagens de uma categoria.
* Migração gerada e aplicada (`0003_categoria_mensagem_categoria`).
* Painel admin: `Categoria` foi registrada, e a lista de mensagens passou a mostrar a coluna de categoria e um filtro por categoria.
* Página inicial: cada mensagem exibe um selo com o nome da categoria, protegido por `{% if m.categoria %}` para mensagens sem categoria.
* Testado o relacionamento inverso pelo shell do Django (`categoria.mensagens.all()` e `.count()`).

### Parte 4 — relacionamento muitos-para-muitos (N:N)

* Novo modelo `Tag`, com o campo `nome` do tipo `SlugField` (único).
* O modelo `Mensagem` ganhou o campo `tags`, um `ManyToManyField` para `Tag` com `blank=True` e `related_name="mensagens"`. O Django criou automaticamente a tabela intermediária `home_mensagem_tags`, que guarda os pares (mensagem, tag).
* Migração gerada e aplicada (`0004_tag_mensagem_tags`).
* Painel admin: `Tag` foi registrada, o filtro lateral da lista de mensagens ganhou "tags" e o campo de tags usa `filter_horizontal`, com dois painéis (disponíveis e escolhidas).
* Dados inseridos pelo shell do Django, usando a API do ORM: criação de tags com `create` e `get_or_create`, criação de mensagem com categoria e associação de tags com `tags.add()`.
* Página inicial: as tags de cada mensagem aparecem abaixo do conteúdo, no formato `#tag`, protegidas por `{% if m.tags.all %}`.

## Como executar

```bash
docker compose up --build
```

O site fica em http://localhost:8000 e o painel administrativo em http://localhost:8000/admin/.

Para parar o projeto, use `Ctrl+C` e depois:

```bash
docker compose down
```

## Sistema em execução