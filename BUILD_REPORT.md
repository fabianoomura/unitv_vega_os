# Validação de desenvolvimento — 2026-11-02

## Resultado

Build Debug concluído com código 0:

```bash
npm run build:debug -- --target armv7 --max-workers 1
```

Pacote: `build/armv7-debug/vegaplayer_armv7.vpkg` (70.924 bytes).

SHA-256:
`5262ffdd7c47a2340693c3802352e813727a48a80678dbfad06df77ad32bad12`

O VPT validou o pacote sem erros. A listagem confirmou `assets/index.html`,
`bundle/index.bundle`, `bundle/index.hermes.bundle`, configuração do runtime,
manifesto e arquivos de assinatura.

## Correções e verificações

- Manifesto: módulo de OS corrigido de `IVega_1_2` para `IVega_2_0`,
  coerente com OS mínimo e alvo 2.0; título atualizado para VegaPlayer.
- Dependências instaladas; `package-lock.json` gerado.
- Lint, TypeScript (`tsc --noEmit`) e Jest aprovados (1 teste).
- `vega build` isolado gerou inicialmente um pacote sem bundles; o script
  `build:debug` gerou JavaScript/Hermes e substituiu o pacote incompleto.
- `.gitignore` atualizado para metadados de build e arquivos `.env`.
- Avisos remanescentes: pacotes transitivos descontinuados, depreciação do
  react-test-renderer, ícone padrão e cópia de assets do Metro sem arquivos.
  O HTML local e os bundles foram confirmados no pacote final.

## Dispositivo e próxima etapa

`vega exec vda devices` confirmou `192.168.68.58:5555` com estado `device`
após o build. Metadados: Fire Stick físico, Vega OS 2.0 (TV Ship/532),
produto callie, arquitetura armv7l, perfil tv, usuário app_user.

Instalação e execução realizadas após aprovação explícita do usuário.
O comando de instalação retornou `success`:

```bash
vega device install-app --device 192.168.68.58:5555 --packagePath /home/fabiano/projetos-vega/build/armv7-debug/vegaplayer_armv7.vpkg
```

A abertura via `vega device launch-app --device 192.168.68.58:5555 --appName
com.atl4s.vegaplayer.main` foi concluída. A consulta `is-app-running` confirmou
o aplicativo em execução. Os logs registraram:

- Transição para primeiro plano e confirmação de visibilidade no display 0.
- WebView com dimensões 1920 × 1080 e renderer conectado.
- `Page loading completed...` às 22:03:21 UTC.
- Apresentação de frames concluída após o carregamento.
- Nenhum callback `onError`, `onHttpError` ou `onSslError` observado.

O runtime emitiu mensagens internas de configuração EGL e de JavaScript
injetado nulo; depois registrou criação de contexto, apresentação de frames
e carga concluídas. Não foi observada falha de abertura. O usuário confirmou
a exibição correta da página na TV; interação pelo controle e reprodução de mídia
ainda não verificadas. A página atual é estática, sem controles interativos.
Compatibilidade com UniTV permanece não avaliada.

Destino Git informado pelo usuário: https://github.com/fabianoomura/unitv_vega_os.
