# Guia de estilo

Identidade visual do site, fiel ao cartão de visita da Inova Tech: fundo preto puro com amarelo-ouro como única cor de destaque.

## Cores

Todas as cores são variáveis CSS definidas no bloco `:root` no topo do `css/style.css`. Para mudar uma cor em todo o site, altere apenas ali.

| Variável | Valor | Uso |
|---|---|---|
| `--preto` | `#000000` | Fundo principal da página (preto puro do cartão) |
| `--preto-2` | `#0B0A08` | Fundo alternativo (seção Inova Cast, caixa de citação) |
| `--preto-3` | `#14120D` | Superfícies elevadas (reservada) |
| `--dourado` | `#F2B705` | Cor principal: marca, botões, títulos de seção, detalhes |
| `--dourado-escuro` | `#C9971A` | Bordas e detalhes discretos |
| `--dourado-claro` | `#FFD147` | Estados de hover e brilhos |
| `--whatsapp` | `#25D366` | Verde oficial do WhatsApp — exclusivo dos botões de contato |
| `--whatsapp-claro` | `#4AE387` | Hover dos botões de WhatsApp |
| `--claro` | `#F4EFE2` | Texto principal (off-white quente) |
| `--cinza` | `#9C9480` | Texto secundário e descrições |
| `--linha` | `#241F14` | Divisórias e bordas sutis |

**Regra da paleta:** o dourado é a única cor de destaque do site. A única exceção é o verde `#25D366` dos botões de WhatsApp, que segue a cor oficial da marca WhatsApp para reconhecimento imediato. Fora isso, não introduzir azuis, verdes ou vermelhos — qualquer elemento novo usa variações de preto, dourado e off-white.

## Tipografia

Três famílias, carregadas do Google Fonts no `<head>` do `index.html`:

| Fonte | Papel | Onde |
|---|---|---|
| **Space Grotesk** (500–700) | Display — a voz da marca | Títulos (`h1`–`h3`), nome da marca no topo e números de destaque do hero; desenho técnico e característico, no espírito da eletrônica |
| **Archivo** (400–700) | Corpo de texto | Padrão do `body`: parágrafos, botões, menu |
| **IBM Plex Mono** (400–600) | Detalhes técnicos | Etiquetas de seção, CEP, telefone, citação do rodapé — ecoa a fonte monoespaçada do cartão de visita |

A regra que aplica a Space Grotesk fica logo no início do `style.css` (seletor `h1, h2, h3, .marca, .hero-dados strong`). O peso máximo dela é 700 — não usar `font-weight: 800` nesses elementos. Para aplicar a fonte mono em um elemento, use a classe utilitária `.mono`.

Escala de títulos: o `h1` do hero e os `h2` de seção usam `clamp()` para escalar com a largura da tela — não definir tamanhos fixos em px para títulos novos.

## Componentes

### Botões
- `.botao` — botão principal: fundo verde WhatsApp (`--whatsapp`), texto preto, usado só para a ação de WhatsApp.
- `.botao-secundario` — contorno dourado-escuro, texto claro, para ações internas ("Ver serviços").

### Etiqueta de seção
`.secao-titulo` — texto mono dourado precedido de um traço horizontal. Abre todas as seções. Para uma seção nova, repita o padrão:

```html
<p class="secao-titulo">Nome da seção</p>
```

### Lista de serviços
`.servico` — grade de três colunas (ícone, título, descrição) que colapsa no celular. Ícones dentro de `.servico-icone` (44×44, borda dourada).

### Quadro de temas (Inova Cast)
`.cast-temas` — cartão com cabeçalho dourado, lista com marcadores circulares e rodapé mono ("1 ano no ar").

### Barras de equalizador
`.cast-ondas` — dez `<span>` com alturas variadas, assinatura visual do podcast. Alturas definidas no CSS por `nth-child`.

### Fundos fotográficos
- **Página inteira**: foto `img/oficina.jpg` (bancada de manutenção — Unsplash, licença livre) fixa atrás de todo o conteúdo via `body::after` (posição `fixed`, véu preto de 80%), criando profundidade ao rolar. O hero adiciona apenas um reforço à esquerda — é a "janela" mais aberta para a foto; as seções internas e o rodapé adicionam um escurecimento extra (`rgba(0,0,0,0.62)`) para priorizar a leitura.
- **Inova Cast**: foto própria `img/podcast.jpg` (microfone condensador dourado de estúdio — Unsplash, licença livre), aplicada na regra `.cast` com gradiente mais aberto à direita; o dourado do microfone conversa diretamente com a paleta.
- Alternativa na pasta: `img/circuito-bg.svg`, ilustração vetorial de placa de circuito dourada no estilo da marca.

### Elementos decorativos
- Filete dourado no topo da página: pseudo-elemento `body::before`.

## Responsividade

Pontos de quebra usados:

| Largura | O que muda |
|---|---|
| ≤ 820 px | Grades de duas colunas (cast, contato) viram uma coluna; véu do fundo do hero fica uniforme |
| ≤ 720 px | Menu do topo é ocultado; serviços colapsam para duas colunas (ícone + conteúdo) |

## Acessibilidade

Padrões já aplicados — manter em alterações futuras:

- Foco de teclado visível (contorno dourado) em links e botões.
- `prefers-reduced-motion` respeitado: transições e rolagem suave desligam.
- SVGs decorativos com `aria-hidden="true"`; mapa com `title` descritivo.
- Contraste: dourado `#F2B705` e off-white `#F4EFE2` sobre preto puro passam do nível AA para texto normal.
