# Guia de publicação

O site é 100% estático — não precisa de PHP, banco de dados nem build. Publicar significa apenas enviar estes arquivos para a hospedagem, **mantendo a estrutura de pastas**:

```
index.html
css/style.css
img/oficina.jpg
img/podcast.jpg
```

(O arquivo `img/circuito-bg.svg` é um fundo alternativo — só precisa ir para o servidor se estiver em uso no CSS.)

As pastas `docs/` e `.claude/` e o `README.md` são documentação e configuração de desenvolvimento — não precisam (nem devem) ir para o servidor.

## Opção 1 — Hospedagem tradicional (Locaweb, Hostinger, HostGator…)

1. Acesse o gerenciador de arquivos ou FTP da hospedagem.
2. Entre na pasta pública do domínio (geralmente `public_html/` ou `www/`).
3. Envie o `index.html` e as pastas `css/` e `img/`.
4. Acesse o domínio no navegador e confira.

## Opção 2 — Hospedagem gratuita (Netlify / Vercel / GitHub Pages / Cloudflare Pages)

Qualquer uma serve bem para um site estático; todas têm plano gratuito com HTTPS automático.

**Netlify (mais simples):**
1. Crie uma conta em [netlify.com](https://www.netlify.com).
2. Arraste a pasta do projeto (contendo `index.html`, `css/` e `img/`) para a área "Deploy".
3. O site fica no ar em um subdomínio `*.netlify.app`; depois é possível apontar um domínio próprio.

**GitHub Pages:**
1. Crie um repositório e envie `index.html`, `css/` e `img/`.
2. Em *Settings → Pages*, selecione a branch principal como origem.
3. O site fica em `https://usuario.github.io/repositorio/`.

## Domínio próprio

Sugestões de registro: [registro.br](https://registro.br) para `.com.br` (ex.: `inovatechpalhoca.com.br`). Depois de registrar, aponte o DNS para a hospedagem escolhida (a própria hospedagem informa os valores — registros `A` ou `CNAME`).

## Checklist pós-publicação

- [ ] Site abre com `https://` (cadeado no navegador).
- [ ] Links de WhatsApp abrem a conversa certa **com o número confirmado** (ver pendência no README).
- [ ] Mapa do Google carrega e aponta para a R. Antônio Viêira, 27.
- [ ] Teste no celular (não só no modo responsivo do desktop).
- [ ] Cadastre a empresa no [Google Business Profile](https://business.google.com) e inclua o link do site — é o que faz a empresa aparecer no Google Maps e na busca local.

## Dicas de divulgação local

- Incluir o link do site no perfil do WhatsApp Business, Instagram e na descrição dos episódios do Inova Cast.
- O título e a descrição da página (tags `<title>` e `<meta name="description">` no `index.html`) já estão otimizados para busca local ("tecnologia e eletrônica em Palhoça") — se mudar o foco, atualize os dois.
