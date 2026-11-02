# VegaPlayer

Aplicativo React Native para Vega OS 2.0, criado com o template `vegaWebview`.
O componente `src/App.tsx` abre `assets/index.html` em um WebView nativo.
O conteúdo atual é a demonstração do template; não há integração com UniTV.

## Ambiente

- Node.js: 26.13.0 via NVM; npm: 11.20.0.
- Amazon Vega SDK: 2.0.13986; Vega CLI: 1.4.7.
- Package ID: `com.atl4s.vegaplayer`.
- Componente: `com.atl4s.vegaplayer.main`.
- Fire TV consultado: Vega OS 2.0 (TV Ship/532), arquitetura `armv7l`.

## Desenvolvimento

```bash
source ~/vega/env
npm ci
npm run lint
npm test -- --runInBand
npx --no-install tsc --noEmit
npm run build:debug -- --target armv7 --max-workers 1
```

Use `vega exec vda devices` para consultar a conexão. O `env` do SDK
adiciona o comando `vega` ao PATH; ferramentas como `vda` e `vpt` podem
ser executadas por `vega exec`, sem alterar o PATH global.

Use o script React Native acima para gerar também o bundle JavaScript/Hermes.
`vega build` isolado pode empacotar apenas a parte nativa e produzir um
`.vpkg` incompleto quando os bundles ainda não foram gerados.

## Instalação e validação na TV

A instalação e a abertura na televisão dependem de aprovação explícita do
usuário. Não executar automaticamente como parte do build.

Após aprovação, instalar o pacote Debug validado com `vega device install-app`,
informando o caminho exato do `.vpkg` e `--device 192.168.68.58:5555`.
Abrir `com.atl4s.vegaplayer.main` e conferir a página local, eventos de carga,
eventuais erros do WebView e resposta ao controle remoto. O teste local de
renderização não substitui essa validação física.

## Próxima investigação

Para avaliar UniTV, verificar primeiro se existe uma interface web oficial
autorizada e quais APIs, codecs, DRM e formas de autenticação ela exige.
Compatibilidade de APK Android não deve ser presumida em Vega OS.
