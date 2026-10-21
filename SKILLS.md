# Agent Skills neste repositório

Este repositório reúne diferentes famílias de Agent Skills, cada uma voltada a um público. Apenas a primeira família deve ser instalada por quem desenvolve aplicativos para o RCube CRM e para o projeto-base Twenty.

## Desenvolver um aplicativo Twenty

[`packages/twenty-agent-skills`](./packages/twenty-agent-skills) é a coleção oficial, independente de ambiente, para criar, desenvolver, operar e publicar aplicativos Twenty. Funciona com Claude Code, Codex, Cursor, Pi e outros ambientes compatíveis com a CLI `skills`, conectados a qualquer instância Twenty, incluindo instâncias auto-hospedadas e locais.

```bash
npx skills add https://github.com/twentyhq/twenty/tree/agent-skills --list
npx skills add https://github.com/twentyhq/twenty/tree/agent-skills --skill create-app
```

Instale a partir da branch `agent-skills`, que contém apenas as skills compiladas para aplicativos e o plugin do Codex. O pacote-fonte em `main` mantém referências compartilhadas e precisa ser compilado antes da instalação. A branch estará disponível após a primeira publicação bem-sucedida a partir de `main`; até lá, use as [instruções de desenvolvimento local](./packages/twenty-agent-skills#local-development).

| Skill            | Quando usar                                                                          |
| ---------------- | ------------------------------------------------------------------------------------ |
| `create-app`     | Iniciar a estrutura de um aplicativo Twenty.                                         |
| `develop-app`    | Adicionar ou modificar objetos, campos, funções de lógica, layouts, componentes e fluxos de trabalho. |
| `manage-app`     | Configurar remotes, sincronizar, compilar, implantar, consultar logs, solucionar problemas e CI/CD. |
| `publish-app`    | Preparar README, metadados do marketplace, logos, capturas de tela e assets públicos. |
| `use-twenty-mcp` | Opcional: conectar um agente a um workspace por MCP e apresentar registros de forma legível. |

## Trabalhar em um workspace Twenty

[`packages/twenty-claude-skills`](./packages/twenty-claude-skills) reúne skills para usar um workspace Twenty, em vez de desenvolver nele — por exemplo, para apresentar registros do CRM como resumos legíveis.

## Contribuir com o código do RCube CRM

[`.claude/skills`](./.claude/skills) contém skills para agentes e pessoas que contribuem com este repositório: `qa-scout`, para testes de interface no navegador, e a série `syncable-entity-*`, voltada ao sistema de migração de workspaces herdado do Twenty. Essas skills pressupõem um clone deste repositório e não são voltadas ao desenvolvimento de aplicativos; as descrições de `syncable-entity-*` deixam isso explícito.

Essas são as skills listadas ao executar `npx skills add twentyhq/twenty --list` no repositório. Para desenvolver aplicativos, use a branch `agent-skills` indicada acima.

## Skills distribuídas com aplicativos

`packages/twenty-apps/**/src/skills` contém skills distribuídas por aplicativos específicos do Twenty. Elas pertencem a esses aplicativos, não a esta coleção.

## Plugin do Codex

[`packages/twenty-agent-skills`](./packages/twenty-agent-skills) mantém as skills canônicas e os metadados do Codex. A compilação gera uma única distribuição, publicada na raiz da branch `agent-skills`, para a CLI `skills` e para o plugin do Codex chamado `twenty`. As cópias geradas não são versionadas em `main`.
