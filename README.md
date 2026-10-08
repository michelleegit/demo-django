# demo-django

Projeto desenvolvido seguindo o roteiro "Construindo um site com Django + Tailwind + Docker" — parte 2.

- **Aluna:** Michelle de Oliveira Pinheiro
- **Disciplina:** BCC481 – Programação Web
- **Professora:** Aline Brito

## Sobre o projeto

Site simples feito em Django 5.1, estilizado com Tailwind CSS (via CDN),
com dados salvos em SQLite e executado dentro de um container Docker.
A página inicial lista as mensagens cadastradas pelo painel administrativo do Django.

## O que foi feito na parte 2

- **Novo campo no modelo:** o modelo `Mensagem` ganhou o campo `autor` (padrão "Anônimo"),
  com migração gerada e aplicada no banco (`0002_mensagem_autor`). O autor aparece na página inicial
  e pode ser preenchido pelo painel admin.
- **Nova página:** criada a página `/sobre/`, seguindo o fluxo rota → view → template
  (`home/urls.py`, `home/views.py` e `templates/home/sobre.html`), com link no menu da página inicial.
- **Novo visual:** o gradiente de fundo da página inicial foi trocado para tons de verde (`emerald` e `teal`).

## Sistema em execução

<img width="1847" height="1043" alt="Captura de tela de 2026-10-08 11-15-48" src="https://github.com/user-attachments/assets/937fada2-4a90-4b14-a784-67250a32b15b" />
<img width="1849" height="1046" alt="Captura de tela de 2026-10-08 11-16-19" src="https://github.com/user-attachments/assets/b04f5021-7f34-4746-a4ec-86b2fae14d2f" />
<img width="1850" height="1050" alt="Captura de tela de 2026-10-08 11-16-39" src="https://github.com/user-attachments/assets/e9e7cd93-9b15-4c50-87cc-b478f060c719" />

