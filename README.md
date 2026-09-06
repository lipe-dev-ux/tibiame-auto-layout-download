# tibiame-auto-layout-download

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
   git remote add origin git@github.com:lipe-dev-ux/tibiame-auto-layout-download.git
   ```

   ```bash
   git push -u origin main
   ```

3. No repositório: *Settings → Pages → Source: Deploy from a branch → main / (root)*.

   Fica no ar em `https://lipe-dev-ux.github.io/tibiame-auto-layout-download/` em um ou dois
   minutos.

## O instalador

Os três binários ficam em `download/`, **commitados no repositório**. A página
aponta para eles por caminho relativo, e o GitHub Pages os serve direto.

| sistema | arquivo |
| --- | --- |
| macOS | `download/tibiame-bot-macos.zip` — um `.app` universal (Apple Silicon + Intel) |
| Windows | `download/tibiame-bot.exe` |
| Linux | `download/tibiame-bot-linux.tar.gz` |

> **Por que compactado, e não o binário solto.** Download por HTTP não carrega
> permissão de arquivo. O binário cru chega **sem o bit de execução** e, no
> macOS, sem extensão — então o sistema faz a única coisa que pode e abre no
> editor de texto. Foi exatamente o que aconteceu no primeiro teste. O `.zip`
> (com um `.app` dentro) e o `.tar.gz` preservam a permissão. O `.exe` do
> Windows dispensa embrulho, porque roda pela extensão.

Saem de `tibiame-bot/instalador/construir.sh`, em `saida/`. Publicar versão
nova é copiar por cima, atualizar a linha da versão no `index.html` e dar push.

> **O preço de guardá-los aqui.** O git nunca esquece: cada versão soma ~23 MB
> ao histórico **para sempre**, mesmo depois de substituída. Dez versões são
> ~230 MB que todo clone passa a baixar, e o GitHub Pages tem teto de 1 GB de
> site. O jeito de não pagar isso é anexar os binários a um **Release** — que
> não é CDN nem custa nada, é o mesmo GitHub, e fica fora do histórico. Se um
> dia trocar, os links viram
> `https://github.com/lipe-dev-ux/tibiame-auto-layout-download/releases/latest/download/<arquivo>`
> e a pasta `download/` sai do repositório.

> **Eles não são assinados.** O macOS barra o primeiro arranque com "cannot be
> opened because the developer cannot be verified", e o Windows mostra a tela
> azul do SmartScreen. A página já explica o contorno — botão direito → Abrir,
> e "Mais informações → Executar assim mesmo". Resolver de verdade custa uma
> conta Apple Developer (99 USD/ano, com notarização) e um certificado de code
> signing para Windows. Vale decidir isso antes de vender, não depois do
> primeiro comprador desistir na tela de aviso.

### `.nojekyll`

O Pages roda Jekyll por padrão, e Jekyll tem regras próprias sobre quais
arquivos publica. O `.nojekyll` na raiz desliga esse processamento e faz o site
ser servido como ele é — sem isso, arquivo em `download/` pode simplesmente não
aparecer, e o 404 não explica por quê.

## O que trocar antes de publicar

O `index.html` tem quatro marcas `TROCAR`:

| onde | o quê |
| --- | --- |
| linha abaixo do botão | a versão, a cada Release |
| rodapé | o e-mail de suporte — está **comentado**, descomente quando houver quem responda |
| — | o `<title>` e o nome, se o produto for rebatizado |

Os links do Release já estão escritos com o seu usuário (`lipe-dev-ux`) e o nome
`tibiame-auto-layout-download`. Se um dia o repositório for renomeado, o endereço
aparece em **cinco** lugares do `index.html`: o botão, os três links de
plataforma e o javascript no fim do arquivo.

## O que não vai aqui

Preço e checkout. Se um dia a página vender, o botão aponta para o provedor
(Gumroad, Lemon Squeezy, Stripe) e o preço vive **lá**. Dois lugares dizendo
valores é um deles ficar errado.
