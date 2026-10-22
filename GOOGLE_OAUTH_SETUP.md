# Google OAuth: Testing, Branding e Production

Esta documentação descreve a configuração do Google Auth Platform para o
**Ary Rongel Position Logger**. Ela não altera o programa, não concede acesso
a uma conta Google e não confirma aprovação do Google.

## O que o código realmente usa

- Google Drive API v3 e OAuth 2.0 **Desktop App**, por `InstalledAppFlow`.
- Somente o escopo `https://www.googleapis.com/auth/drive.file`.
- Criação e consulta de pastas/arquivos próprios; diários publicados não são
  sobrescritos. O aplicativo não altera permissões de compartilhamento.
- Consulta de nome de exibição/e-mail da conta pelo `about` do Drive para
  identificar a conta conectada ao operador.
- Token local protegido com Windows DPAPI; `token.json` com permissões 0600
  somente no ambiente de desenvolvimento Linux.
- Cliente OAuth e token mantidos fora do repositório, no diretório de dados.

As páginas deste site são documentos públicos de Branding. **Não são um backend
OAuth nem um endpoint para receber tokens.** O cliente Desktop continua usando
o retorno local loopback gerado pelo SDK no computador do operador. Não crie
um cliente Web, não adicione scripts de login ao site e não use o endereço do
GitHub Pages como redirect URI do aplicativo Desktop.

## Preparação comum

1. Acesse o [Google Cloud Console](https://console.cloud.google.com/) com a conta
   autorizada e selecione o projeto correto.
2. Em **APIs e serviços → Biblioteca**, habilite **Google Drive API**.
3. No **Google Auth Platform**, configure nome do aplicativo, contato de suporte,
   contato do desenvolvedor e público apropriado. Os nomes dos menus podem variar
   conforme a interface do Console.
4. Em **Clients**, crie ou selecione um OAuth Client do tipo **Desktop App**.
5. Em **Data Access**, confira o escopo mínimo `drive.file`. Não solicite
   `https://www.googleapis.com/auth/drive` nem amplie o acesso para resolver
   problemas de Branding/domínio.
6. Mantenha o JSON do cliente e os tokens fora do Git e do site. O operador
   selecionará o JSON pelo botão **Conectar / Reconectar Google Drive**.

## Cenário A — Testing

Para um projeto com público **External**, mantenha o status **Testing** durante
a homologação:

1. Em **Audience → Test users**, adicione a conta operacional autorizada.
2. Salve a configuração e mantenha a API e o cliente Desktop configurados.
3. No Windows, abra o aplicativo e use **Conectar / Reconectar Google Drive**.
4. Selecione o JSON privado do cliente e autorize a conta adicionada como Test User.
5. Use **Testar Google Drive** e confirme a pasta `CATS - Ary Rongel` na conta
   correta. Faça um backup de homologação, sem publicar a pasta automaticamente.

No modo External/Testing, com escopo Drive, o refresh token pode expirar em
**sete dias**, conforme as regras de expiração do Google. A exceção relativa a
escopos básicos de identidade não deve ser presumida para `drive.file`.
O operador poderá precisar reconectar periodicamente. Revogação de acesso,
mudanças da conta ou políticas Workspace também podem invalidar a autorização.

Reconectar não apaga os registros locais. Uma falha definitiva de upload
permanece visível no histórico até uma tentativa bem-sucedida; reconhecer um
aviso não transforma a falha em envio.

Se a organização usar público **Internal** do Google Workspace, confirme com
o administrador quem pode autenticar e quais políticas se aplicam. Não selecione
Internal para tentar autorizar contas externas à organização.

## Cenário B — Production

Antes de publicar definitivamente:

1. Habilite Google Drive API e confirme o cliente **Desktop App** e `drive.file`.
2. Confirme o contato público da política, `vitortcc01@gmail.com`. Use contatos
   de suporte/desenvolvedor válidos no Google Auth Platform, conforme as opções
   aceitas pelo Console.
3. Publique as páginas e confirme acesso público por HTTPS, sem login e com
   resposta 200. O conteúdo deve corresponder ao aplicativo e ao escopo real.
4. Preencha **Branding**: nome, Homepage, Privacy Policy e Terms of Service.
5. Configure os domínios autorizados exigidos pelo Console e comprove a
   propriedade do domínio conforme as exigências atuais do Google, usando
   a conta/projeto apropriados.
6. Se for exigida uma propriedade **Domain** do Search Console, valide-a por
   DNS no domínio sob seu controle. Mantenha o TXT de verificação publicado.
7. Em **Audience**, solicite a mudança para **Production / Publish app** e
   conclua as etapas de verificação apresentadas pelo Google, quando aplicáveis.
8. Confira o resultado no Console e teste o consentimento com a conta autorizada.
   Status Production e aprovação de Branding/verificação são etapas distintas;
   não presuma aprovação apenas por mudar o status.

A classificação de escopos e os requisitos efetivamente apresentados no
Console determinam as verificações aplicáveis. Usar um escopo mínimo não é
uma garantia de aprovação, de aceitação de domínio ou de autorização por uma
política Workspace. Production também não torna tokens imunes a revogação ou
a outras causas de expiração.

### URLs previstas no GitHub Pages

Use estes valores **somente depois de publicar e validar as páginas**, e
somente se o Google os aceitar para o projeto:

| Campo de Branding | Valor previsto |
| --- | --- |
| Homepage | https://vtmathias.github.io/ary-rongel-position-logger-site/ |
| Privacy Policy | https://vtmathias.github.io/ary-rongel-position-logger-site/privacy.html |
| Terms of Service | https://vtmathias.github.io/ary-rongel-position-logger-site/terms.html |

## Limitação do domínio github.io

O site hospedado e a propriedade verificável do domínio são assuntos diferentes.
O repositório controla o conteúdo de `/ary-rongel-position-logger-site/`; isso não dá ao seu
proprietário controle dos registros DNS de `github.io`.

**Não foi confirmado que o Google aceite o domínio padrão deste GitHub Pages
como domínio OAuth definitivo.** Não cadastre simplesmente `github.io` como
se fosse seu domínio. Consulte o domínio registrável exigido pelo Console e
o método de comprovação aplicável à sua configuração.

Uma meta tag de verificação de uma propriedade **URL-prefix** pode comprovar
controle de um conteúdo específico, mas não deve ser apresentada como substituta
garantida de uma propriedade **Domain** validada por DNS. Não tente contornar
uma exigência de DNS com uma meta tag.

Se o Google rejeitar o domínio padrão ou exigir controle DNS, será necessário
usar um domínio próprio, já pertencente à organização ou adquirido pelo
responsável, e apontá-lo para o mesmo GitHub Pages. Siga
[CUSTOM_DOMAIN_SETUP.md](CUSTOM_DOMAIN_SETUP.md). Não há necessidade de alterar
a lógica NMEA, armazenamento ou OAuth do cliente Desktop para hospedar essas
páginas em outro domínio.

## Referências oficiais

- [Google: verificação de Branding](https://developers.google.com/identity/protocols/oauth2/production-readiness/brand-verification).
- [Google Drive: escolher escopos](https://developers.google.com/workspace/drive/api/guides/api-specific-auth).
- [Google OAuth: expiração de tokens](https://developers.google.com/identity/protocols/oauth2#expiration).
- [Search Console: verificação de propriedade](https://support.google.com/webmasters/answer/9008080).
- [Configuração de Pages neste repositório](GITHUB_PAGES_SETUP.md).

As exigências podem mudar; confirme as instruções apresentadas pelo Google no
momento da submissão. Esta documentação não é uma confirmação de que a
verificação foi solicitada ou aprovada.
