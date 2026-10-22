# Ary Rongel Position Logger — site público

Site de documentação do aplicativo Windows Ary Rongel Position Logger, usado
no registro de posições do Navio de Apoio Oceanográfico Ary Rongel, callsign PWAR.
O aplicativo utiliza arquivos GeoJSON e Google Drive autorizado pelo operador.

Este repositório contém somente HTML, CSS e documentação pública. O código do
aplicativo, seus dados operacionais e suas credenciais ficam no projeto e no
computador operacional correspondentes. Não há scripts, frameworks, analytics,
cookies ou dependências externas para executar o site.

## Publicar gratuitamente

Este repositório deve estar **Public** para usar GitHub Pages na conta gratuita.
Como as páginas estão na raiz, configure:

```text
Settings → Pages → Build and deployment
Source: Deploy from a branch
Branch: main
Folder: / (root)
Save
```

Não selecione `/docs`: este repositório tem estrutura própria e os arquivos HTML
estão diretamente na raiz. Não é necessário instalar nada ou executar um build.

Depois do deploy, as URLs esperadas são:

| Página | URL prevista |
| --- | --- |
| Home | https://vtmathias.github.io/ary-rongel-position-logger-site/ |
| Privacy Policy | https://vtmathias.github.io/ary-rongel-position-logger-site/privacy.html |
| Terms of Service | https://vtmathias.github.io/ary-rongel-position-logger-site/terms.html |

Essas URLs só devem ser usadas no Google depois de confirmar que as páginas
estão publicadas e acessíveis por HTTPS, sem login, com HTTP 200.

## Arquivos

| Arquivo | Função |
| --- | --- |
| [index.html](index.html) | Página inicial e explicação do uso de `drive.file` |
| [privacy.html](privacy.html) | Política de Privacidade em inglês |
| [terms.html](terms.html) | Termos de Serviço em inglês |
| [styles.css](styles.css) | Layout compartilhado para desktop e celular |
| `.nojekyll` | Publicação estática direta, sem Jekyll |
| [GITHUB_PAGES_SETUP.md](GITHUB_PAGES_SETUP.md) | Ativação, verificação e diagnóstico de Pages |
| [GOOGLE_OAUTH_SETUP.md](GOOGLE_OAUTH_SETUP.md) | Google OAuth Testing e Production |
| [CUSTOM_DOMAIN_SETUP.md](CUSTOM_DOMAIN_SETUP.md) | Domínio próprio e comprovação por DNS |
| `.gitignore` | Proteção contra publicação acidental de credenciais locais |

Contato público aprovado na política: **vitortcc01@gmail.com**.

## Google Auth Platform

Use um cliente OAuth **Desktop App**, Google Drive API habilitada e o escopo
mínimo `https://www.googleapis.com/auth/drive.file`. As páginas deste site são
documentos de Branding, não callbacks OAuth ou endpoints para receber tokens.

Em Testing, adicione a conta operacional como Test User e considere a expiração
periódica da autorização. Para Production, preencha o Branding, confirme os
links publicados e cumpra as verificações apresentadas pelo Google.

A aceitação do domínio padrão do GitHub Pages pelo Google não foi confirmada.
Se o Google exigir controle DNS, será necessário um domínio próprio sob controle
do responsável. Uma meta tag HTML não substitui obrigatoriamente uma propriedade
Domain verificada por DNS. Consulte os guias acima antes de publicar em Production.

## Prévia local opcional

Na raiz deste repositório:

```bat
py -m http.server 8000 --bind 127.0.0.1
```

Abra `http://127.0.0.1:8000/`. Python serve apenas para essa prévia; o GitHub
Pages hospeda os arquivos sem executar Python. Os links relativos também
funcionam na raiz de um futuro domínio próprio.

## Atualizações

Edite as páginas correspondentes e faça commit na `main`. Com Pages configurado,
o GitHub publicará a atualização. Mantenha os textos de privacidade e termos
coerentes com o aplicativo e revise a data de atualização quando o conteúdo mudar.

Não envie Client Secret, JSON de credenciais, tokens, arquivos `.env`, chaves
privadas ou registros reais de posição para este repositório público.
