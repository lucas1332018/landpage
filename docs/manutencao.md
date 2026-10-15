# Guia de manutenção

Como fazer as alterações mais comuns no site. Todas as edições de conteúdo são feitas no `index.html`; as de aparência, no `css/style.css`.

## Trocar o número do WhatsApp

O número aparece em **três pontos** do `index.html`. Procure por `wa.me` e por `98494`:

1. Botão "Falar no WhatsApp" no hero — atributo `href="https://wa.me/5548984941001"`.
2. Link do telefone na seção "Onde estamos" — o `href` **e** o texto visível `+55 (48) 98494-1001`.
3. Botão "Chamar no WhatsApp" na mesma seção — atributo `href`.

O formato do link `wa.me` é: `https://wa.me/55` + DDD + número, só dígitos, sem espaços ou traços. Exemplo: `(48) 98494-1234` vira `https://wa.me/5548984941234`.

> **Atenção:** o último dígito atual (`...1001`) é um palpite — a foto do cartão de visita corta o número. Confirme o número real antes de publicar.

## Trocar textos

Cada seção do `index.html` está delimitada por uma tag `<section>` com `id` e comentário claro:

| Seção | Onde procurar no `index.html` |
|---|---|
| Hero (título e subtítulo) | `<section class="hero">` |
| Serviços | `<section id="servicos">` — cada serviço é um bloco `<div class="servico">` |
| Inova Cast | `<section id="inovacast">` |
| Endereço e contato | `<section id="contato">` |
| Rodapé | `<footer>` |

Basta editar o texto entre as tags. Não é preciso mexer no CSS para mudanças de conteúdo.

## Adicionar ou remover um serviço

Na seção `#servicos`, duplique (ou apague) um bloco inteiro:

```html
<div class="servico">
  <div class="servico-icone" aria-hidden="true">
    <svg>…</svg>   <!-- ícone em SVG, traço na cor atual (stroke="currentColor") -->
  </div>
  <h3>Nome do serviço</h3>
  <p>Descrição do serviço.</p>
</div>
```

O layout (ícone + título + descrição) se ajusta sozinho. Para o ícone, qualquer SVG de 24×24 com `stroke="currentColor"` herda o dourado automaticamente. Fontes de ícones compatíveis: [Lucide](https://lucide.dev) ou [Feather](https://feathericons.com) (copie o código SVG do ícone).

## Alterar temas do Inova Cast

Na seção `#inovacast`, a lista de temas é um `<ul>` simples dentro de `<div class="cast-temas">`:

```html
<li>Novo tema aqui</li>
```

O marcador dourado à esquerda de cada item é gerado pelo CSS — não precisa adicionar nada.

## Alterar o endereço e o mapa

1. **Texto**: edite o bloco "Endereço" na seção `#contato`.
2. **Mapa**: o mapa é um `<iframe>` do Google Maps. Para apontar para outro endereço, troque o valor de `q=` na URL do atributo `src` pelo endereço novo (com espaços no formato `+` ou codificados), mantendo o final `&output=embed`:

```
https://www.google.com/maps?q=ENDEREÇO+AQUI&output=embed
```

O visual escuro do mapa é um filtro CSS (classe `.mapa iframe` no `style.css`) — nenhuma configuração no Google é necessária.

## Trocar as imagens de fundo

O site usa duas fotos de fundo (ambas do Unsplash — licença livre para uso comercial, sem atribuição obrigatória):

| Foto | Onde aparece | Regra no `css/style.css` |
|---|---|---|
| `img/oficina.jpg` (bancada de manutenção) | Página inteira, fixa atrás de todas as seções | `body::after` |
| `img/podcast.jpg` (microfone dourado de estúdio) | Só na seção Inova Cast | `.cast` (e sua versão `@media (max-width: 820px)`) |

Como funciona a legibilidade: a foto da página tem um véu preto de 80% (`body::after`); o hero adiciona só um reforço à esquerda (regra `.hero`), por isso é onde a foto mais aparece; as demais seções adicionam um escurecimento extra (`background` na regra `section` e no `footer`).

Para trocar uma foto (por uma da própria loja, por exemplo):

1. Coloque o arquivo novo em `img/` (ex.: `img/bancada.jpg`). Prefira imagens de pelo menos 1920 px de largura, escuras ou que combinem com o véu preto.
2. Troque o `url(...)` na regra correspondente da tabela acima — no caso da foto do podcast, **em dois lugares** (regra principal e versão para telas estreitas).
3. Se o texto ficar difícil de ler, aumente os valores de opacidade dos gradientes (`rgba(0, 0, 0, …)`).

A pasta `img/` também guarda `circuito-bg.svg`, uma ilustração de placa de circuito dourada no estilo da marca, que pode substituir qualquer uma das fotos.

## Alterar itens do menu

O menu fica no `<nav>` dentro do `<header>`. Cada link aponta para o `id` de uma seção (`#empresa`, `#servicos`…). Se criar uma seção nova, dê a ela um `id` e adicione o link correspondente. Em telas menores que 720 px o menu é ocultado (regra `@media (max-width: 720px)` no CSS).

## Atualizar o ano do rodapé

No `<footer>`, troque o ano em `© 2026 Inova Tech…`.

## Checklist antes de publicar qualquer alteração

- [ ] Abrir o site num servidor local e conferir no desktop.
- [ ] Estreitar a janela (ou usar o modo responsivo do navegador, tecla F12) e conferir no celular.
- [ ] Testar os links de WhatsApp e os links do menu.
- [ ] Conferir que o mapa carrega e aponta para o endereço certo.
