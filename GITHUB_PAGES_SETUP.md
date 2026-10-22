# GitHub Pages — ativação e verificação

O site está na raiz deste repositório, com HTML e CSS estáticos. `.nojekyll`
dispensa processamento Jekyll. Não há etapa de instalação ou compilação.

## 1. Ativar Pages

Com uma conta proprietária ou administradora:

1. Abra [Vtmathias/ary-rongel-position-logger-site](https://github.com/Vtmathias/ary-rongel-position-logger-site).
2. Confirme que este repositório está **Public**, condição para Pages gratuito
   nesta configuração. O repositório do aplicativo pode continuar privado.
3. Entre em **Settings → Pages**.
4. Em **Build and deployment**, escolha **Source: Deploy from a branch**.
5. Selecione **Branch: main** e **Folder: / (root)**.
6. Clique em **Save** e aguarde o deploy.

```text
Repository → Settings → Pages → Build and deployment
→ Source: Deploy from a branch → Branch: main → Folder: / (root) → Save
```

Não selecione `/docs` e não crie um diretório intermediário para os arquivos.
`index.html`, `privacy.html`, `terms.html` e `styles.css` devem permanecer na raiz.
Não é necessário criar um workflow próprio: o GitHub executa o deploy por branch.

## 2. Confirmar a publicação

Acompanhe o resultado em **Actions** e o endereço mostrado em **Settings → Pages**.
URLs esperadas:

| Página | Endereço |
| --- | --- |
| Home | https://vtmathias.github.io/ary-rongel-position-logger-site/ |
| Privacidade | https://vtmathias.github.io/ary-rongel-position-logger-site/privacy.html |
| Termos | https://vtmathias.github.io/ary-rongel-position-logger-site/terms.html |

Os endereços acima não são uma confirmação de que Pages já esteja ativado.
Abra os três sem estar conectado ao GitHub e confirme conteúdo e HTTP 200.
Para testar GET no PowerShell:

```powershell
$pages = @(
  'https://vtmathias.github.io/ary-rongel-position-logger-site/',
  'https://vtmathias.github.io/ary-rongel-position-logger-site/privacy.html',
  'https://vtmathias.github.io/ary-rongel-position-logger-site/terms.html'
)
foreach ($page in $pages) {
  $response = Invoke-WebRequest -Uri $page -UseBasicParsing
  "{0} {1}" -f $response.StatusCode, $page
}
```

O contato público em `privacy.html` é **vitortcc01@gmail.com**. Confira o texto
antes de usar a política na configuração OAuth.

## 3. Diagnosticar problemas

| Sintoma | O que conferir |
| --- | --- |
| Upgrade or make this repository public | O repositório do site precisa estar Public para Pages gratuito nessa conta. |
| Branch ou pasta indisponível | Confirme a existência dos arquivos na main e selecione `/ (root)`. |
| HTTP 404 | Aguarde o deploy e confira `index.html` na raiz, a origem selecionada e o resultado em Actions. |
| Página sem estilo | Confirme `styles.css` na mesma raiz; o HTML usa link relativo. |
| URL de github.com/blob | Esse endereço exibe código no GitHub; use a URL de github.io mostrada por Pages. |

## 4. Configurar Google OAuth depois da publicação

Siga [GOOGLE_OAUTH_SETUP.md](GOOGLE_OAUTH_SETUP.md). O fato de as páginas estarem
online não comprova automaticamente a propriedade do domínio para o Google.
Se for exigido controle DNS, siga [CUSTOM_DOMAIN_SETUP.md](CUSTOM_DOMAIN_SETUP.md).

Não há domínio fictício em `CNAME` e não foi presumida aprovação de `github.io`
no OAuth. Não publique credenciais ou tokens junto do site.

Referência oficial: [configurar a origem de publicação de Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
