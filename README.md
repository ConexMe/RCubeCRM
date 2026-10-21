<h1 align="center">RCube CRM</h1>

<h2 align="center">CRM de código aberto, adaptável às necessidades do seu negócio</h2>

<p align="center">
  <a href="https://github.com/ConexMe/RCubeCRM">Repositório do RCube CRM</a> ·
  <a href="https://docs.twenty.com">Documentação do projeto-base</a> ·
  <a href="https://github.com/twentyhq/twenty">Projeto original Twenty</a>
</p>

> O RCube CRM é baseado no projeto open source [Twenty](https://github.com/twentyhq/twenty). Nesta etapa, a marca foi atualizada na documentação principal; a interface e os recursos visuais do produto ainda podem exibir a identidade do projeto-base.

<br />

# Sobre o RCube CRM

O RCube CRM oferece a equipes técnicas os componentes necessários para criar um CRM personalizado, atender a necessidades complexas e acompanhar a evolução do negócio. Ele pode ser desenvolvido, implantado e versionado junto com o restante da sua infraestrutura.

<br />

# Instalação e primeiros passos

### Nuvem do projeto-base

Para testar a versão hospedada pelo projeto original Twenty, acesse [twenty.com](https://twenty.com). Esse serviço é mantido pelo Twenty e não representa uma oferta de hospedagem do RCube CRM.

### Crie um aplicativo

Use a CLI do projeto-base Twenty para iniciar um aplicativo:

```bash
npx create-twenty-app meu-app
```

Defina objetos, campos e visualizações como código:

```ts
import { defineObject, FieldType } from 'twenty-sdk/define';

export default defineObject({
  nameSingular: 'deal',
  namePlural: 'deals',
  labelSingular: 'Negócio',
  labelPlural: 'Negócios',
  fields: [
    { name: 'name', label: 'Nome', type: FieldType.TEXT },
    { name: 'amount', label: 'Valor', type: FieldType.CURRENCY },
    { name: 'closeDate', label: 'Data de fechamento', type: FieldType.DATE_TIME },
  ],
});
```

Publique no workspace:

```bash
npx twenty app:publish --private
```

Consulte o [guia de desenvolvimento de aplicativos](https://docs.twenty.com/developers/extend/apps/getting-started) do projeto-base para saber mais sobre objetos, visualizações, agentes e funções de lógica.

Se você usa um agente de programação, instale as [skills oficiais do Twenty para desenvolvimento de aplicativos](./packages/twenty-agent-skills). Elas funcionam com Claude Code, Codex, Cursor, Pi e outros ambientes compatíveis com a CLI `skills`:

```bash
npx skills add https://github.com/twentyhq/twenty/tree/agent-skills --list
```

A branch `agent-skills` é criada após a primeira publicação bem-sucedida de `main`. Até lá, use as [instruções de compilação local](./packages/twenty-agent-skills#local-development). O arquivo [`SKILLS.md`](./SKILLS.md) descreve as outras famílias de skills deste repositório.

### Hospede por conta própria

Execute o projeto em sua infraestrutura com [Docker Compose](https://docs.twenty.com/developers/self-host/capabilities/docker-compose) ou contribua localmente seguindo o [guia de configuração de desenvolvimento](https://docs.twenty.com/developers/contribute/capabilities/local-setup) do projeto-base.

<br />
<br />

# Recursos

O projeto-base oferece os componentes de um CRM moderno — objetos, visualizações, fluxos de trabalho e agentes — e permite estendê-los como código. As imagens abaixo ilustram recursos do Twenty e podem não refletir a identidade visual atual do RCube CRM.

Consulte o [guia do usuário do Twenty](https://docs.twenty.com/user-guide/introduction) para conhecer os recursos do produto ou a [documentação técnica do projeto-base](https://docs.twenty.com) para referências de desenvolvimento.

<table align="center">
  <tr>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="./packages/twenty-website/public/images/readme/v2-build-apps-dark.webp" />
        <source media="(prefers-color-scheme: light)" srcset="./packages/twenty-website/public/images/readme/v2-build-apps-light.webp" />
        <img src="./packages/twenty-website/public/images/readme/v2-build-apps-light.webp" alt="Crie seus aplicativos" />
      </picture>
      <p align="center"><a href="https://docs.twenty.com/developers/extend/apps/getting-started"><img src="./packages/twenty-website/public/images/readme/code-icon.svg" width="16" height="16"/> Saiba mais sobre aplicativos</a></p>
    </td>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="./packages/twenty-website/public/images/readme/v2-version-control-dark.webp" />
        <source media="(prefers-color-scheme: light)" srcset="./packages/twenty-website/public/images/readme/v2-version-control-light.webp" />
        <img src="./packages/twenty-website/public/images/readme/v2-version-control-light.webp" alt="Acompanhe as alterações com controle de versão" />
      </picture>
      <p align="center"><a href="https://docs.twenty.com/developers/extend/apps/publishing"><img src="./packages/twenty-website/public/images/readme/monitor-icon.svg" width="16" height="16"/> Saiba mais sobre controle de versão</a></p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="./packages/twenty-website/public/images/readme/v2-all-tools-dark.webp" />
        <source media="(prefers-color-scheme: light)" srcset="./packages/twenty-website/public/images/readme/v2-all-tools-light.webp" />
        <img src="./packages/twenty-website/public/images/readme/v2-all-tools-light.webp" alt="Ferramentas para criar diferentes soluções" />
      </picture>
      <p align="center"><a href="https://docs.twenty.com/developers/extend/apps/building"><img src="./packages/twenty-website/public/images/readme/rocket-icon.svg" width="16" height="16"/> Saiba mais sobre os componentes disponíveis</a></p>
    </td>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="./packages/twenty-website/public/images/readme/v2-tools-dark.webp" />
        <source media="(prefers-color-scheme: light)" srcset="./packages/twenty-website/public/images/readme/v2-tools-light.webp" />
        <img src="./packages/twenty-website/public/images/readme/v2-tools-light.webp" alt="Personalize os layouts" />
      </picture>
      <p align="center"><a href="https://docs.twenty.com/user-guide/layout/overview"><img src="./packages/twenty-website/public/images/readme/planner-icon.svg" width="16" height="16"/> Saiba mais sobre layouts</a></p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="./packages/twenty-website/public/images/readme/v2-ai-agents-dark.webp" />
        <source media="(prefers-color-scheme: light)" srcset="./packages/twenty-website/public/images/readme/v2-ai-agents-light.webp" />
        <img src="./packages/twenty-website/public/images/readme/v2-ai-agents-light.webp" alt="Agentes de IA e conversas" />
      </picture>
      <p align="center"><a href="https://docs.twenty.com/user-guide/ai/overview"><img src="./packages/twenty-website/public/images/readme/message-icon.svg" width="16" height="16"/> Saiba mais sobre IA</a></p>
    </td>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="./packages/twenty-website/public/images/readme/v2-crm-tools-dark.webp" />
        <source media="(prefers-color-scheme: light)" srcset="./packages/twenty-website/public/images/readme/v2-crm-tools-light.webp" />
        <img src="./packages/twenty-website/public/images/readme/v2-crm-tools-light.webp" alt="Ferramentas essenciais de CRM" />
      </picture>
      <p align="center"><a href="https://docs.twenty.com/user-guide/introduction"><img src="./packages/twenty-website/public/images/readme/star-icon.svg" width="16" height="16"/> Saiba mais sobre os recursos de CRM</a></p>
    </td>
  </tr>
</table>

<br />

# Tecnologias

- <a href="https://www.typescriptlang.org/"><img src="./packages/twenty-website/public/images/readme/stack-typescript.svg" width="14" height="14"/> TypeScript</a>
- <a href="https://nx.dev/"><img src="./packages/twenty-website/public/images/readme/stack-nx.svg" width="14" height="14"/> Nx</a>
- <a href="https://nestjs.com/"><img src="./packages/twenty-website/public/images/readme/stack-nestjs.svg" width="14" height="14"/> NestJS</a>, com <a href="https://bullmq.io/">BullMQ</a>, <a href="https://www.postgresql.org/"><img src="./packages/twenty-website/public/images/readme/stack-postgresql.svg" width="14" height="14"/> PostgreSQL</a> e <a href="https://redis.io/"><img src="./packages/twenty-website/public/images/readme/stack-redis.svg" width="14" height="14"/> Redis</a>
- <a href="https://reactjs.org/"><img src="./packages/twenty-website/public/images/readme/stack-react.svg" width="14" height="14"/> React</a>, com <a href="https://jotai.org/">Jotai</a>, <a href="https://linaria.dev/">Linaria</a> e <a href="https://lingui.dev/">Lingui</a>

# Agradecimentos

<p align="center">
  <a href="https://greptile.com"><img src="./packages/twenty-website/public/images/readme/greptile.webp" height="28" alt="Greptile" /></a>
  &nbsp;&nbsp;&nbsp;&nbsp;
  <a href="https://sentry.io/"><img src="./packages/twenty-website/public/images/readme/sentry.webp" height="28" alt="Sentry" /></a>
  &nbsp;&nbsp;&nbsp;&nbsp;
  <a href="https://crowdin.com/"><img src="./packages/twenty-website/public/images/readme/crowdin.webp" height="28" alt="Crowdin" /></a>
</p>

Agradecemos aos serviços que usamos e recomendamos: Greptile para revisão de código, Sentry para identificar problemas e Crowdin para tradução.

# Comunidade do projeto-base

<p><a href="https://github.com/twentyhq/twenty"><img src="./packages/twenty-website/public/images/readme/star-icon.svg" width="12" height="12"/> Repositório Twenty</a> · <a href="https://discord.gg/cx5n4Jzs57"><img src="./packages/twenty-website/public/images/readme/discord-icon.svg" width="12" height="12"/> Discord</a> · <a href="https://github.com/twentyhq/twenty/discussions"><img src="./packages/twenty-website/public/images/readme/message-icon.svg" width="12" height="12"/> Sugestões e discussões</a> · <a href="https://github.com/orgs/twentyhq/projects/1/views/35"><img src="./packages/twenty-website/public/images/readme/rocket-icon.svg" width="12" height="12"/> Lançamentos</a> · <a href="https://twitter.com/twentycrm"><img src="./packages/twenty-website/public/images/readme/x-icon.svg" width="12" height="12"/> X</a> · <a href="https://www.linkedin.com/company/twenty/"><img src="./packages/twenty-website/public/images/readme/linkedin-icon.svg" width="12" height="12"/> LinkedIn</a> · <a href="https://twenty.crowdin.com/twenty"><img src="./packages/twenty-website/public/images/readme/language-icon.svg" width="12" height="12"/> Crowdin</a> · <a href="https://github.com/twentyhq/twenty/contribute"><img src="./packages/twenty-website/public/images/readme/code-icon.svg" width="12" height="12"/> Contribua ao Twenty</a></p>
