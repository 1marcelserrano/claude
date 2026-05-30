# CLAUDE.md — Contexto para agentes

> Este arquivo orienta o Claude Code (e outros agentes) ao trabalhar neste repositório.
> Leia antes de propor ou executar mudanças.

## O que é este repositório

**MSCREATIVE.SYSTEMS — Hub de Skills.** Um repositório de **landing pages estáticas**
para skills do Claude Cowork. É, ao mesmo tempo:

1. **Um artefato publicado** — site estático servido pela Vercel (`vercel.json`).
2. **Um acervo de método** — o guia `docs/setup-hub-guide.md` documenta como criar
   um hub novo do zero.

Não é uma aplicação com backend nem um pacote de código. Não há build: o site é
HTML/CSS/JS puro servido diretamente da raiz.

## Estrutura

```
.
├── index.html                       ← Hub: lista navegável de skills (porta de entrada)
├── README.md                        ← Documentação de entrada do repositório
├── vercel.json                      ← Config de deploy (site estático, sem build)
├── docs/
│   └── setup-hub-guide.md           ← Guia: como criar um hub novo (processo/método)
└── skills/
    └── <nome-da-skill>/
        ├── index.html               ← Landing page da skill
        └── <nome-da-skill>.skill    ← Arquivo de instalação (ZIP)
```

## Como rodar / visualizar localmente

Site estático — basta abrir os arquivos ou servir a pasta:

```bash
python3 -m http.server 8000
# abrir http://localhost:8000
```

## Como fazer deploy

A Vercel publica automaticamente a partir da branch `main` (`vercel.json`:
`outputDirectory "."`, sem build). **Não há deploy a partir de branches de trabalho** —
então mudanças nesta branch não afetam o site ao vivo até o merge em `main`.

## Convenções

- **Idioma** de docs e commits: **português**.
- **Commits**: Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`, `style:`,
  `refactor:`). Um assunto por commit.
- **Nomes de arquivos/pastas novos**: `kebab-case` (ex.: `skills/minha-skill/`).
- **Branches**: trabalho em `claude/<descrição>`; nunca commitar direto em `main`.
- **Design system** das páginas: MSCREATIVE.SYSTEMS V3.0 — ver `docs/setup-hub-guide.md`
  (IBM Plex Sans 300 + Libre Caslon Text + Space Mono; paleta `#0A0C10`/`#B2A898`/`#A89D80`;
  grid de fundo 54×54px; CSS inline).

## O que NÃO commitar

- `.DS_Store`, artefatos de editor, `node_modules/`, `.vercel/`, logs e temporários
  (ver `.gitignore`).
- Segredos, tokens ou credenciais — este é um site público.

## Inconsistências conhecidas (não "corrigir" sem aprovação do dono)

Itens detectados na auditoria que dependem de decisão humana — **não tratar como bug**:

- **`skills/aboissa-teams-hub/index.html` usa a fonte `Inter`**, divergindo do design
  system V3.0 (IBM Plex Sans). Pode ser branding intencional ("ABOISSA-OS V3"). Confirmar
  com o dono antes de alinhar.
- **`skills/aboissa-teams-hub/` não tem arquivo `.skill`** (diferente de
  `teams-setup-playbook`). Não verificável se é um hub de onboarding (sem download) ou
  uma pendência. Confirmar antes de agir.

Ver `SETUP_STRATEGY.md` para o diagnóstico completo e o roadmap.
