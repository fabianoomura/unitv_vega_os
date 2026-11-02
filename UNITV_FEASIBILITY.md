# UniTV no Vega OS: investigação inicial

Data: 2026-11-02. Serviço indicado pelo usuário: https://baixarunitv.com/.

## Constatações

A página indicada anuncia `unitv_apk.apk`, versão 4.14.1, como aplicativo
Android. Na seção sobre a origem, declara expressamente que o site é
independente e não é o desenvolvedor oficial. As informações de versão e
tamanho são declarações da página; a análise posterior do binário está
registrada abaixo e encontrou uma divergência de versão.

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

## Análise estática do APK indicado

O link direto publicado em baixarunitv.com foi baixado em 2026-11-02:
`https://files.ciinemaapk.com.br/Unitv%20Apk/unitv_apk.apk`.
Nenhum código do APK foi executado; o arquivo não foi instalado na TV.
O binário permanece no cache local, fora do repositório.

Identificação do arquivo observado:

| Campo | Valor |
| --- | --- |
| Tamanho | 34.252.899 bytes |
| SHA-256 | `c2511e26b818bec76a5ccd267860e8b5fd67bf361d6afdc27b1acc97af913048` |
| Package ID no manifesto | `com.global.unitvmobile` |
| versionName / versionCode | `3.19.2` / `31902` |
| minSdkVersion / targetSdkVersion | `19` / `33` |
| Application / appComponentFactory | `s.h.e.l.l.S` / `s.h.e.l.l.A` |
| Entradas ZIP | 3.170 |

O tamanho coincide com o informado pela página, mas a versão do manifesto
diverge de 4.14.1. O package ID e os nomes das Activities apontam para uma
edição mobile. Não foi confirmada sua equivalência à edição de televisão,
sua procedência oficial ou sua segurança.

O manifesto declara Activities Android para login, catálogo, reprodução e
WebView, como `com.mobile.brasiltv.activity.MainAty`, `PlayAty`, `WebViewAty`
e `com.mobile.brasiltv.mine.activity.LoginAty`. A existência de `WebViewAty`
não demonstra que o catálogo e o player sejam um aplicativo web.

Não foram encontradas entradas com extensões `.html`, `.htm`, `.js`,
`.bundle` ou `.css` no ZIP. Há bibliotecas Android para `armeabi-v7a` e
`arm64-v8a`, incluindo `libijkplayer.so`, `libijkffmpeg.so` e `libijksdl.so`.
Compartilhar a arquitetura ARM com o Fire Stick não torna essas bibliotecas
compatíveis com os serviços e o runtime do Vega.

Os nomes `s.h.e.l.l.*`, `assets/ijiami.dat`, `assets/ijiami.ajm` e
`libijmDataEncryption*.so` são indícios de empacotamento/proteção de código.
O ZIP possui um `classes.dex` de 2.500.148 bytes. A inspeção simples desse
DEX não revelou marcadores de WebView/React Native/Flutter, mas isso não
exclui seu uso em código protegido ou carregado posteriormente. Nenhuma
tentativa de contornar essa proteção foi realizada.

Conclusão limitada a este arquivo: não há um frontend web exposto no pacote
que possa ser copiado diretamente para o VegaPlayer. Para avançar de forma
fundamentada, precisamos identificar uma interface web funcional do mesmo
serviço, uma integração documentada ou código-fonte para porte. Esta análise
não equivale a um teste de execução ou a uma auditoria de segurança.
