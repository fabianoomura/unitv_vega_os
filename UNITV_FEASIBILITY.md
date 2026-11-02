# UniTV no Vega OS: investigação inicial

Data: 2026-11-02. Serviço indicado pelo usuário: https://baixarunitv.com/.

## Constatações

A página indicada anuncia `unitv_apk.apk`, versão 4.14.1, como aplicativo
Android. Na seção sobre a origem, declara expressamente que o site é
independente e não é o desenvolvedor oficial. As informações de versão e
tamanho são declarações da página; o binário não foi baixado nem analisado.

Fonte: https://baixarunitv.com/

A Amazon documenta que Vega OS não fornece o runtime Android e não executa
APKs Fire OS diretamente. Renomear ou empacotar o APK em um VPKG não resolve
essa dependência. Um porte depende de código compatível com Vega ou de uma
interface web utilizável.

Fonte: https://developer.amazon.com/apps-and-games/blogs/2026/10/port-your-tv-app-to-react-native-with-adbt

O WebView de Vega usa Chromium, oferece reprodução de mídia e suporte a
Widevine/PlayReady sujeito ao dispositivo e à configuração. Isso torna um
cliente web uma hipótese técnica plausível, sem demonstrar compatibilidade
com o UniTV.

Fonte: https://developer.amazon.com/docs/vega/2.0/overview-of-webview

## Endereços candidatos, sem vínculo oficial confirmado

Sites de terceiros divulgam `www.unitv.tube`, `www.unitvweb.org` e
`www.uvweboficial.com` como acesso web. Não foi estabelecido que pertencem
ao aplicativo distribuído pelo site indicado ou que aceitam a mesma conta.
Uma página de divulgação consultada foi https://totalplaybr.com/downloads.html.

Na tentativa pelo serviço de pesquisa:

- `https://www.unitv.tube`: erro de acesso 502.
- `https://www.unitvweb.org`: timeout.
- `https://www.uvweboficial.com`: redirecionamento para verificação CAPTCHA.

Esses resultados são limitações daquela tentativa e não demonstram
indisponibilidade no navegador do usuário ou no Fire Stick. Não houve login,
teste de assinatura, reprodução ou tentativa de contornar a verificação.

## Próximo teste necessário

Confirmar com o usuário ou com o fornecedor da conta qual endereço web
corresponde ao serviço contratado. O usuário deve digitar credenciais apenas
na interface que reconhecer; não devem ser enviadas à conversa, ao repositório
ou aos logs.

Com um endereço confirmado, preparar o VegaPlayer para abrir essa página e
testar no aparelho: HTTPS, login/teclado, navegação pelo controle, reprodução,
áudio, tela cheia e recuperação de erros. Verificar DRM e serviços necessários
somente conforme os requisitos observados. Solicitar aprovação antes de
instalar ou abrir uma nova versão na TV.

Se não houver interface web compatível, será necessário acesso ao código-fonte
ou a uma integração disponibilizada pelo fornecedor para construir um cliente
Vega. A viabilidade final permanece em aberto.
