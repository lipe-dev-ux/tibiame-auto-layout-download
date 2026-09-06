# tibiame-site

A página de download do tibiame-bot. **Público de propósito** — aqui não há nada
do produto, só a casca que entrega o instalador.

O bot mora em outro repositório, privado, e nunca é publicado. Quem compra
recebe a **imagem**, não o código: a chave libera o `docker pull`, e é isso que
a página instrui o instalador a fazer.

## Publicar no GitHub Pages

1. Crie este repositório no GitHub como **público**.

   > Pages a partir de repositório privado é recurso pago (GitHub Pro nas contas
   > pessoais). Como a página é pública de qualquer forma, o repositório público
   > evita a assinatura e mantém o produto onde ele deve estar.

2. Empurre o conteúdo:

   ```bash
   git init && git add . && git commit -m "Página de download"
   ```

   ```bash
   git remote add origin git@github.com:lipe-dev-ux/tibiame-site.git
   ```

   ```bash
   git push -u origin main
   ```

3. No repositório: *Settings → Pages → Source: Deploy from a branch → main / (root)*.

   Fica no ar em `https://lipe-dev-ux.github.io/tibiame-site/` em um ou dois
   minutos.

## O instalador

Sobe como **Release** deste mesmo repositório, e não como arquivo commitado:
binário no histórico do git incha o repositório para sempre, e cada versão nova
o incharia de novo.

*Releases → Draft a new release*, anexe os arquivos, publique.

São **três arquivos por Release**, com nomes fixos — a página aponta para eles
pelo nome:

| sistema | arquivo |
| --- | --- |
| macOS | `tibiame-bot.dmg` |
| Windows | `tibiame-bot.exe` |
| Linux | `tibiame-bot.AppImage` |

O link é sempre `releases/latest/download/<arquivo>`: o GitHub resolve sozinho
para a versão mais recente, então a página **não muda a cada Release**. Em troca,
o nome do arquivo tem de ser sempre o mesmo — se um Release chamar o instalador
de `tibiame-bot-1.1.dmg`, o link da página quebra em silêncio.

> **Enquanto só existir um sistema pronto.** O botão aponta para a página do
> Release, que lista o que existe. Um link para arquivo que não foi anexado dá
> 404 — então só publique o Release com os três, ou apague da página as
> plataformas que ainda não têm binário.

### Qual botão o visitante vê

O HTML traz o botão genérico apontando para a **página** do Release, e um
javascript o troca pelo arquivo do sistema de quem chegou. É palpite, e por isso
nunca é a única saída: os três arquivos ficam listados logo abaixo, e sem
javascript o botão continua funcionando.

## O que trocar antes de publicar

O `index.html` tem quatro marcas `TROCAR`:

| onde | o quê |
| --- | --- |
| linha abaixo do botão | a versão, a cada Release |
| rodapé | o e-mail de suporte — está **comentado**, descomente quando houver quem responda |
| — | o `<title>` e o nome, se o produto for rebatizado |

Os links do Release já estão escritos com o seu usuário (`lipe-dev-ux`) e o nome
`tibiame-site`. Se o repositório tiver outro nome, troque nos quatro lugares —
o botão, os três links de plataforma e o javascript no fim do arquivo.

## O que não vai aqui

Preço e checkout. Se um dia a página vender, o botão aponta para o provedor
(Gumroad, Lemon Squeezy, Stripe) e o preço vive **lá**. Dois lugares dizendo
valores é um deles ficar errado.
