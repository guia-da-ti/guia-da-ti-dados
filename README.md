# Guia da TI — dados da comunidade

Catálogo público que alimenta o [Guia da TI](https://github.com/guia-da-ti/guia-da-ti). O código do site fica no outro repositório. Aqui você adiciona e corrige recursos.

As empresas apoiadoras ficam na lista `supporters` de `community.json`. Cada registro contém `name`, `url` HTTPS e `description` curta, e passa por revisão por Pull Request. Os contribuidores são consultados automaticamente no GitHub pela aplicação, sem lista manual neste repositório.

## Contribuir

- [Sugira um recurso pelo formulário](https://github.com/guia-da-ti/guia-da-ti-dados/issues/new?template=recurso.yml), sem precisar editar JSON.
- Corrija um arquivo em `data/` pelo lápis do GitHub e envie um Pull Request.
- Para adicionar, copie um modelo de `templates/` para `data/<categoria>/<slug>.json`.

Consulte [CONTRIBUTING.md](CONTRIBUTING.md) e o [guia editorial](docs/editorial.md).

## Estrutura

- `data/`: um JSON por cadastro, organizado nas [32 categorias aceitas](docs/categories.md), entre aprendizado, informação, estudos, conexões, prática e oportunidades.
- `templates/`: modelos para copiar.
- `schemas/`: campos obrigatórios e limites.
- `taxonomy/`: IDs normalizados de áreas, tecnologias, idiomas e categorias.
- `scripts/` e `test/`: validação e testes.
- `.github/`: CI, revisão e formulário de sugestão.

## Validar localmente

Requer Node.js 22.12+.

```sh
npm ci
npm run validate
npm test
npm run format:check
```

O resultado está em `dist/catalog.json`. Entregue esse arquivo à aplicação por `CATALOG_PATH`. Os exemplos desta fundação são fictícios e estão identificados com `demo: true`.

## Como chega ao site

PR → validação automática → revisão humana → merge na main → solicitação de build e publicação do site.

Após o merge, o workflow deste repositório solicita o build da aplicação com os dados atuais. A aplicação valida o catálogo antes de publicar. Um build horário continua como alternativa e avisa no resumo quando o último sucesso ocorreu há mais de duas horas.

Para habilitar o gatilho após o merge, configure neste repositório o segredo `SITE_REPOSITORY_DISPATCH_TOKEN`. Use um token fine-grained com permissão `Contents: Read and write` apenas no repositório `guia-da-ti/guia-da-ti`.

Uma sugestão por issue não publica um cadastro automaticamente.

CODEOWNERS identifica o revisor, mas não bloqueia merges sozinho. A revisão obrigatória e os checks precisam ser exigidos pela proteção de branch nas configurações do GitHub.
