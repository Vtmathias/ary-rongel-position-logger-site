# Domínio próprio para o site e o Google OAuth

Use estas instruções se o Google exigir um domínio cujo DNS esteja sob controle
do responsável, ou se a organização já preferir usar seu domínio institucional.
Hospedar o site no GitHub Pages continua sendo possível; registrar um domínio
novo pode ter custo no registrador. Não é necessário adquirir hospedagem web
separada para estas páginas estáticas.

## 1. Escolher um domínio real sob controle do responsável

Confirme com o administrador qual domínio institucional ou domínio próprio
poderá ser usado. Escolha o hostname do site, por exemplo um subdomínio dedicado.
Os nomes `cats.exemplo.com` e `aryrongel.exemplo.com` citados no pedido são
**ilustrações**, não domínios configurados deste projeto.

É necessário poder adicionar registros DNS no registrador/provedor DNS.
Ter permissão para editar o conteúdo de um repositório GitHub não permite
editar o DNS de `github.io`.

## 2. Verificar o domínio no GitHub, quando aplicável

O proprietário pode verificar o domínio nas configurações da conta/organização
GitHub, em **Settings → Pages → Add a domain / Verify domain**. Use o registro
TXT e o valor exatos gerados pelo GitHub para aquele domínio e conta.

Essa verificação ajuda a proteger o domínio contra uso indevido no Pages.
Ela é diferente da verificação do Google Search Console. Não reutilize um
TXT de um serviço como se verificasse automaticamente o outro.

## 3. Configurar o hostname no GitHub Pages

Depois que os arquivos do site estiverem na `main`:

1. Abra o repositório **Settings → Pages**.
2. Mantenha a origem **Deploy from a branch → main → / (root)**.
3. Em **Custom domain**, informe o hostname real aprovado, sem protocolo,
   porta ou caminho. Salve.
4. O GitHub poderá criar/atualizar `CNAME` para a fonte por branch. Confira
   se o conteúdo é somente o hostname real. Não crie `CNAME` com um exemplo.
5. Configure o DNS conforme as instruções oficiais e o diagnóstico de Pages.

Para um subdomínio, o apontamento costuma ser um **CNAME** para o hostname de
Pages da conta, neste caso `vtmathias.github.io`, sem `https://` e sem
`/ary-rongel-position-logger-site/`. O nome do registro depende do hostname real escolhido.
Confirme o destino e a configuração na documentação do GitHub antes de aplicar.

Para domínio raiz/apex, use os registros suportados pelo seu provedor e os
valores atuais publicados pelo GitHub. Não copie endereços IP ou TXT de exemplos
não correspondentes à sua configuração. Esta documentação não fornece valores
DNS inventados para um domínio que ainda não foi escolhido.

Após a propagação e a emissão do certificado, habilite **Enforce HTTPS** quando
disponível. Confirme HTTPS, certificado válido e HTTP 200 nas três páginas.

## 4. Verificar a propriedade no Google Search Console

1. Entre no [Google Search Console](https://search.google.com/search-console)
   com a conta que será usada para comprovar a propriedade ao projeto Google.
2. Adicione a propriedade **Domain** correspondente ao domínio sob seu controle,
   sem `https://` e sem caminho, conforme solicitado pelo Google.
3. Copie o registro **TXT** de verificação que o Google gerar.
4. Adicione-o ao DNS usando o nome e o valor exatos indicados pelo Console.
5. Aguarde a propagação e clique em **Verify**.
6. **Mantenha o TXT no DNS depois da verificação.** A comprovação pode ser
   revalidada; remover o registro pode fazer perder a condição verificada.
7. Confirme se a conta com a propriedade verificada é proprietária/editora
   adequada do projeto Google Cloud, conforme o fluxo de verificação exigido.

Não envie o TXT para o GitHub como se isso o publicasse no DNS. A existência de
uma meta tag HTML ou de uma propriedade URL-prefix não substitui obrigatoriamente
a validação DNS de uma propriedade Domain. Use a modalidade exigida pelo Google.

## 5. Atualizar o Branding do Google Auth Platform

Depois que o novo endereço estiver funcionando, preencha os campos com as URLs
reais verificadas:

| Campo | Valor a informar |
| --- | --- |
| Homepage | A raiz HTTPS do hostname real do site |
| Privacy Policy | A mesma raiz seguida de `privacy.html` |
| Terms of Service | A mesma raiz seguida de `terms.html` |
| Authorized Domains | O domínio registrável que o Console exigir, sem protocolo, porta ou caminho |

Não use os domínios de exemplo desta documentação. Confirme o nome do aplicativo
e o contato público aprovado em `privacy.html`, `vitortcc01@gmail.com`.
Depois, siga o processo de Production e as verificações aplicáveis no Google.

O tipo do cliente continua **Desktop App** e o escopo continua `drive.file`.
O endereço do site não deve ser adicionado como um callback de login Web para
substituir o retorno local do aplicativo.

## 6. Conferir links após a migração

As três páginas e o CSS usam caminhos relativos (`./`, `privacy.html`,
`terms.html`, `styles.css`), por isso funcionam sob `/ary-rongel-position-logger-site/` e na raiz de
um domínio próprio. Não há `<base>`, domínio hardcoded nos links internos ou
`CNAME` fictício.

Atualize os endereços esperados nas instruções e no Branding para o hostname
real, teste Home → Privacy/Terms → Home e confira os links públicos no Console.
Não presuma que o endereço antigo ou seus redirecionamentos foram aceitos pelo
Google; use a origem final aprovada.

## Referências oficiais

- [Gerenciar um domínio próprio no GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).
- [Verificar um domínio no GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages).
- [Verificar propriedade no Search Console](https://support.google.com/webmasters/answer/9008080).
- [Verificação de Branding do Google](https://developers.google.com/identity/protocols/oauth2/production-readiness/brand-verification).
- [Fluxos Testing e Production deste projeto](GOOGLE_OAUTH_SETUP.md).
