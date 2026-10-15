# Inova Tech — Landing Page

Site institucional de página única (landing page) da **Inova Tech**, empresa de tecnologia de Palhoça/SC — venda, reparo e manutenção de computadores, notebooks e aparelhos vintage, com especialização em eletrônica avançada — e do **Inova Cast**, o podcast da empresa.

## Visão geral

| | |
|---|---|
| Tipo | Landing page estática (HTML + CSS puros, sem JavaScript) |
| Idioma | Português (pt-BR) |
| Dependências | Nenhuma biblioteca ou framework. Apenas fontes do Google Fonts |
| Navegadores | Chrome, Edge, Firefox e Safari atuais; layout responsivo até 375 px |
| Identidade visual | Preto puro e amarelo-ouro, fiel 1:1 ao cartão de visita da empresa |

## Estrutura de arquivos

```
Projeto site/
├── index.html          # Página única: estrutura e conteúdo, comentado bloco a bloco
├── css/
│   └── style.css       # Toda a aparência; o cabeçalho do arquivo é a documentação técnica
├── img/
│   ├── oficina.jpg     # Foto de fundo da página inteira (bancada de manutenção — Unsplash)
│   ├── podcast.jpg     # Foto de fundo da seção Inova Cast (microfone dourado — Unsplash)
│   └── circuito-bg.svg # Ilustração alternativa (placa de circuito dourada, vetorial)
├── docs/
│   ├── manutencao.md   # Como editar textos, contato, fundos, mapa e seções
│   ├── guia-de-estilo.md  # Cores, tipografia e componentes em detalhe
│   └── publicacao.md   # Como colocar o site no ar
├── .claude/
│   └── launch.json     # Configuração do servidor local de preview (só desenvolvimento)
└── README.md           # Este arquivo
```

## Como o site foi construído

### Identidade visual — cores

A paleta foi extraída diretamente do cartão de visita (preto com letras douradas). Todas as cores são variáveis CSS no bloco `:root` do [css/style.css](css/style.css) — para mudar uma cor no site inteiro, altera-se um único valor.

| Variável | Hex | Uso |
|---|---|---|
| `--preto` | `#000000` | Fundo principal — o preto puro do cartão |
| `--preto-2` | `#0B0A08` | Superfícies escuras alternativas |
| `--preto-3` | `#14120D` | Superfícies elevadas (reserva) |
| `--dourado` | `#F2B705` | Cor da marca: títulos de seção, ícones, detalhes |
| `--dourado-escuro` | `#C9971A` | Bordas e detalhes discretos |
| `--dourado-claro` | `#FFD147` | Estados de hover e brilhos |
| `--whatsapp` | `#25D366` | Verde oficial do WhatsApp — exclusivo dos botões de contato |
| `--whatsapp-claro` | `#4AE387` | Hover dos botões de WhatsApp |
| `--claro` | `#F4EFE2` | Texto principal (off-white quente) |
| `--cinza` | `#9C9480` | Texto secundário e descrições |
| `--linha` | `#241F14` | Divisórias e bordas sutis |

**Regra da paleta:** o dourado é a única cor de destaque do site; a única exceção é o verde dos botões de WhatsApp, mantido na cor oficial da marca para reconhecimento imediato.

### Tipografia

Três famílias do Google Fonts, cada uma com um papel:

| Fonte | Pesos | Papel |
|---|---|---|
| **Space Grotesk** | 500–700 | Display — títulos (`h1`–`h3`), nome da marca e números de destaque. Desenho técnico e característico, no espírito da eletrônica. Peso máximo 700 (não usar 800) |
| **Archivo** | 400–700 | Corpo de texto — parágrafos, botões, menu (padrão do `body`) |
| **IBM Plex Mono** | 400–600 | Detalhes técnicos — etiquetas de seção, CEP, telefone, lema do rodapé. Ecoa a fonte monoespaçada do cartão de visita. Aplicada pela classe utilitária `.mono` |

Títulos usam `clamp()` para escalar com a largura da tela (nada de tamanho fixo em px).

### Fundos fotográficos em camadas

O efeito de foto na página inteira é construído em quatro camadas (documentadas também no cabeçalho do CSS):

1. **`body::after`** — a foto da bancada de manutenção (`img/oficina.jpg`) fica **fixa** atrás de todo o conteúdo, sob um véu preto de 80%. Por ser uma camada `position: fixed`, funciona também em celulares (onde `background-attachment: fixed` costuma falhar) e cria profundidade ao rolar.
2. **`.hero`** — o topo adiciona apenas um reforço de gradiente à esquerda (atrás do texto); é a "janela" mais aberta para a foto.
3. **`section` e `footer`** — as seções internas somam um escurecimento extra (`rgba(0,0,0,0.62)`) para priorizar a leitura.
4. **`.cast`** — a seção do podcast substitui tudo pela foto própria (`img/podcast.jpg`, microfone condensador dourado), com gradiente mais aberto à direita.

As duas fotos vêm do Unsplash (licença livre para uso comercial, sem atribuição obrigatória). A ilustração `img/circuito-bg.svg` — placa de circuito dourada com processador "INOVA", desenhada em SVG para este projeto — fica como alternativa vetorial.

### Componentes e detalhes

- **Marca**: ícone de chip em SVG inline + nome, no cabeçalho fixo com fundo translúcido e desfoque.
- **Filete dourado** no topo da página (pseudo-elemento `body::before`), como a borda de um cartão.
- **Botões**: verde WhatsApp para contato (com o logo oficial em SVG); contorno dourado para ações internas.
- **Serviços**: linhas de três colunas (ícone | nome | descrição); ícones SVG de traço que herdam o dourado via `currentColor`.
- **Inova Cast**: barras de equalizador em CSS puro (10 `<span>` com alturas via `nth-child`) e quadro de temas com cabeçalho dourado.
- **Mapa**: `<iframe>` gratuito do Google Maps (sem chave de API), escurecido só com filtro CSS (`grayscale` + `invert`).

### Responsividade

| Largura | O que muda |
|---|---|
| ≤ 820 px | Grades de duas colunas viram uma; véus dos fundos ficam uniformes (texto ocupa a largura toda) |
| ≤ 720 px | Menu do topo é ocultado; serviços colapsam para ícone + conteúdo |

### Acessibilidade

- Foco de teclado visível (contorno dourado) em links e botões.
- `prefers-reduced-motion` respeitado: transições e rolagem suave desligam.
- SVGs decorativos com `aria-hidden="true"`; mapa com `title` descritivo; seções com `aria-label`.
- Contraste: dourado `#F2B705` e off-white `#F4EFE2` sobre os fundos escuros atendem o nível AA.

## Seções da página

Todas na mesma página, acessíveis pelo menu fixo do topo:

1. **Hero** — apresentação da empresa, botão de WhatsApp e destaques (+4 anos, venda e reparo, eletrônica avançada).
2. **Serviços** (`#servicos`) — venda de equipamentos, reparo e manutenção, aparelhos vintage, eletrônica avançada e compra de usados.
3. **Inova Cast** (`#inovacast`) — o podcast da empresa (~1 ano no ar) e seus temas, sobre foto de estúdio.
4. **Onde estamos** (`#contato`) — endereço, contato de WhatsApp e mapa do Google incorporado.

## Como visualizar localmente

O site usa CSS e imagens em arquivos separados, então abra-o por um servidor HTTP local:

```bash
python -m http.server 8742
```

Depois acesse `http://localhost:8742` no navegador.

## Manutenção rápida

- **Trocar um texto** → edite direto no `index.html` (os comentários indicam cada bloco); veja [docs/manutencao.md](docs/manutencao.md).
- **Trocar uma cor** → altere as variáveis no `:root` do `css/style.css`; veja [docs/guia-de-estilo.md](docs/guia-de-estilo.md).
- **Trocar uma foto de fundo** → tabela de onde cada foto é aplicada em [docs/manutencao.md](docs/manutencao.md).
- **Publicar** → envie `index.html` + pastas `css/` e `img/` para a hospedagem; veja [docs/publicacao.md](docs/publicacao.md).

## Pendências

- **Número do WhatsApp**: o último dígito está como palpite (`+55 48 98494-1001`), pois a foto do cartão de visita corta o número. Confirmar e corrigir nos três pontos indicados em [docs/manutencao.md](docs/manutencao.md) (procure por `wa.me`).
- Links do Inova Cast (Spotify/YouTube), horário de atendimento e redes sociais podem ser adicionados quando a empresa fornecer.
- Melhorias sugeridas (fotos reais da loja, galeria antes/depois, player do podcast, favicon + Open Graph + schema.org) discutidas e à disposição para implementar.
