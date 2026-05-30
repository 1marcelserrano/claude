# Contribuindo — MSCREATIVE.SYSTEMS — Hub de Skills

Obrigado por contribuir. Este guia define as convenções do repositório.
Para o contexto técnico completo, ver [`CLAUDE.md`](CLAUDE.md) e o guia de criação de
hubs em [`docs/setup-hub-guide.md`](docs/setup-hub-guide.md).

## Fluxo de trabalho

1. Crie uma branch a partir de `main`: `claude/<descrição-curta>` ou `feat/<descrição>`.
   **Nunca** commite direto em `main`.
2. Faça as mudanças e teste localmente.
3. Abra um Pull Request (o template é preenchido automaticamente).
4. A Vercel publica somente após o merge em `main`.

## Padrão de commits — Conventional Commits

```
<tipo>: <descrição no imperativo, em português>
```

Tipos usados: `feat`, `fix`, `docs`, `style`, `chore`, `refactor`.

Exemplos:
- `feat: adiciona landing page da skill content-calendar`
- `style: alinha aboissa-teams-hub ao design system V3.0`
- `docs: atualiza guia de criação de hubs`

## Nomes de arquivos e pastas

- **Arquivos e pastas novos:** `kebab-case` (ex.: `skills/content-calendar/`).
- Uma skill = uma pasta em `skills/<nome>/` contendo:
  - `index.html` — a landing page;
  - `<nome>.skill` — o arquivo de instalação (quando a skill for instalável).
- Documentação de método/processo vai em `docs/`.

> **Legado:** os arquivos existentes já seguem `kebab-case` e **não devem ser renomeados
> em massa**. Renomeie apenas com motivo claro e aprovação.

## Design system

Todas as páginas seguem **MSCREATIVE.SYSTEMS V3.0** (detalhes em `docs/setup-hub-guide.md`):

- Tipografia: IBM Plex Sans 300 + Libre Caslon Text (italic) + Space Mono.
- Cores: fundo `#0A0C10`, texto `#B2A898`, accent `#A89D80`.
- Grid de fundo 54×54px; CSS **inline**; zero dependências além do Google Fonts.
- Mobile-first; breakpoints em 480px / 768px / 1080px.

Se uma página precisar divergir do design system (ex.: branding próprio de um cliente),
documente a divergência no PR para decisão explícita — não trate como padrão silencioso.

## Como adicionar uma nova skill

1. `skills/<nome-da-skill>/` em `kebab-case`.
2. Crie `index.html` a partir de uma skill existente como referência.
3. Adicione o arquivo `<nome-da-skill>.skill` (se instalável).
4. Adicione o card no `index.html` da raiz e a linha na tabela do `README.md`.
5. Teste localmente (`python3 -m http.server 8000`) e verifique os links.
6. Commit: `feat: adiciona landing page da skill <nome>`.

## Checklist antes do PR

- [ ] Páginas abrem sem erro de console.
- [ ] Links internos (hub → skill → download) funcionam.
- [ ] Nomes novos em `kebab-case`.
- [ ] Sem segredos ou arquivos ignorados commitados.
