# CLAUDE.md

O RCube CRM é um CRM de código aberto baseado no Twenty, organizado como um monorepo Nx / Yarn 4. Os principais pacotes são: `twenty-front` (React 18, Jotai, Linaria, Vite), `twenty-server` (NestJS, TypeORM, PostgreSQL, Redis, GraphQL), `twenty-shared` (tipos e utilitários isomórficos), `twenty-ui`, `twenty-sdk` (SDK de aplicativos e CLI) e `twenty-e2e-testing` (Playwright).

Siga os padrões do código ao redor. Os arquivos adjacentes ao que está sendo editado têm prioridade sobre regras escritas, inclusive na nomenclatura, que varia entre áreas.

## Convenções do projeto

Onde este repositório divergir dos padrões gerais:

- Prefira comentários curtos com `//`, nunca blocos JSDoc. Comente apenas o motivo — uma restrição que o código não expressa e que continuará relevante para quem não viu a alteração —, nunca o que o código faz.
- Prefira `type` a `interface` (exceto ao estender interfaces de terceiros); literais de string a enums (exceto enums GraphQL); não use `any`; use nomes descritivos para genéricos (`TData`, não `T`).
- Use apenas exports nomeados. Componentes devem ser funções.
- Prefira manipuladores de eventos a `useEffect` para atualizar estado.
- Não abrevie nomes (`fieldMetadata`, não `fm`); use `SCREAMING_SNAKE_CASE` para constantes; sufixe os tipos de propriedades de componentes com `Props`.
- Antes de criar helpers, procure os existentes: `isDefined`, `isNonEmptyArray`, `isPlainObject`, entre outros, em `twenty-shared/utils`; `isNonEmptyString`, `isString`, `isNull`, `isObject`, entre outros, em `@sniptt/guards`. Reimplementar um utilitário existente é um defeito frequente em código gerado por IA.
- Use Lingui para textos da interface e `doNotTranslate()` de `twenty-shared/i18n` para textos que não devem ser traduzidos, como diagnósticos e tokens de protocolo. Use Linaria para estilos em `twenty-front`.
- Para conceitos do produto RCube CRM, consulte `packages/twenty-ui/src/icon/icon-dictionary.md` e use o ícone canônico.
- Importe ícones de `twenty-ui/icon`, nunca diretamente de `@tabler/icons-react`; conceitos de ação e status devem usar os respectivos ícones.
- Teste o comportamento, não a implementação: consulte texto e papéis visíveis para a pessoa usuária e use `@testing-library/user-event` nas interações.

## Comentários

A maioria do código é autoexplicativa. Comente apenas código genuinamente complexo ou pouco intuitivo: um motivo não óbvio, uma solução alternativa, uma invariante sutil ou um desvio deliberado da abordagem esperada. Não descreva o que o código já deixa claro. Comentários devem ser concisos, com no máximo cinco linhas.

Docstrings explicam o que o código faz e suas decisões de projeto. Também devem ser concisas; use-as quando a explicação for extensa demais para um comentário breve.

## Comandos

```bash
bash packages/twenty-utils/setup-dev-env.sh   # Postgres/Redis + inicialização do banco; apenas para tarefas que precisam executar o aplicativo
yarn start                                    # front + server + worker

npx jest caminho/para/arquivo.spec.ts --config=packages/<pacote>/jest.config.mjs   # teste unitário de um arquivo (preferencial)
npx vitest run --root packages/twenty-ui --project unit <arquivo>                  # twenty-ui usa Vitest, não Jest
npx nx test twenty-server                     # testes do pacote (também disponível para twenty-front etc.)
npx nx run twenty-server:test:integration:with-db-reset
npx nx storybook:build twenty-front && npx nx storybook:test twenty-front

npx nx lint:diff-with-main twenty-server      # lint rápido das diferenças; adicione --configuration=fix para corrigir
npx nx fmt <pacote>                           # formatação
npx nx build twenty-shared                    # necessário antes de compilar/testar pacotes dependentes
npx nx database:reset twenty-server
npx nx run twenty-front:graphql:generate      # após alterações no schema GraphQL; use --configuration=metadata para o schema de metadados
```

## Pontos de atenção

- **`twenty-shared/dist` é um artefato local por branch e não é versionado.** Após trocar de branch ou editar `twenty-shared`, execute `npx nx build twenty-shared --skip-nx-cache` antes de confiar em falhas de tipos ou testes de pacotes dependentes.
- **O cache do Nx pode retornar resultados desatualizados.** Para verificar uma correção, execute `npx tsgo -p tsconfig.json --noEmit` diretamente no pacote, em vez de `nx typecheck`.
- **Não versione catálogos de tradução, a menos que a tarefa seja sobre eles.** `lingui extract` e `lingui compile` regeneram `packages/twenty-server/src/engine/core-modules/i18n/locales/*.po` e `locales/generated/*` com milhares de linhas de alterações ao tocar em qualquer string `msg`. O pipeline de i18n mantém esses arquivos; não os inclua.
- **Mensagens de commit não devem atribuir autoria a IA.** A CI rejeita commits com trailers de coautoria `@anthropic.com` ou linhas como "Generated with Claude Code".
- **Comandos de atualização** (`packages/twenty-server/src/database/commands/upgrade-version-command/`): crie ou edite arquivos apenas no diretório da versão atual `TWENTY_CURRENT_VERSION`, usando um timestamp real em milissegundos desde o epoch, maior que todos os existentes nesse diretório. A CI valida isso, e o cursor de atualização ignora silenciosamente comandos ordenados antes de um já aplicado. Inclua `up` e `down`; nunca reescreva a lógica de comandos já versionados. Mantenha helpers e constantes exclusivos dos comandos na pasta da versão, nunca em módulos de runtime, e não condicione o código de runtime ao estado da migração. Consulte `packages/twenty-server/docs/UPGRADE_COMMANDS.md`.
- **Alterações em arquivos de entidades precisam de um comando de instância gerado**: `npx nx run twenty-server:database:migrate:generate --name <nome> --type <fast|slow>` (`slow` adiciona uma etapa de atualização de dados).
- Há um servidor MCP Postgres somente leitura configurado em `.mcp.json` para consultar dados do workspace, metadados e resultados de migrações. Escritas devem ser feitas pelos comandos da CLI.
- Para entrar no ambiente E2E, clique em "Continue with Email" e use as credenciais já preenchidas.
