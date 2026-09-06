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

*Releases → Draft a new release*, anexe o arquivo, publique. O link da página
já está escrito como:

```
https://github.com/lipe-dev-ux/tibiame-site/releases/latest/download/tibiame-bot.dmg
```

`releases/latest/download/` faz o GitHub resolver sozinho para a versão mais
recente — o link na página **não precisa mudar a cada Release**. O nome do
arquivo, sim, precisa ser sempre o mesmo.

## O que trocar antes de publicar

O `index.html` tem quatro marcas `TROCAR`:

| onde | o quê |
| --- | --- |
| botão de baixar | o link do Release |
| linha abaixo do botão | versão, tamanho e data |
| rodapé | o e-mail de suporte |
| — | o `<title>` e o nome, se o produto for rebatizado |

## O que não vai aqui

Preço e checkout. Se um dia a página vender, o botão aponta para o provedor
(Gumroad, Lemon Squeezy, Stripe) e o preço vive **lá**. Dois lugares dizendo
valores é um deles ficar errado.
