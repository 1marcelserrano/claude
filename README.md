# MSCREATIVE.SYSTEMS — Hub de Skills

Repositório de landing pages para skills do Claude Cowork.
Cada skill tem sua própria pasta em `skills/` com uma landing page independente.

## Estrutura

```
skills/
└── [nome-da-skill]/
    ├── index.html                  ← landing page da skill
    └── [nome-da-skill].skill       ← arquivo de instalação
```

## Como adicionar uma nova skill

1. Criar pasta: `skills/[nome-da-skill]/`
2. Adicionar `index.html` seguindo o design system MSCREATIVE.SYSTEMS V3.0
3. Adicionar o arquivo `.skill` na mesma pasta
4. Adicionar card no `index.html` da raiz

## Design System

Todas as páginas seguem MSCREATIVE.SYSTEMS V3.0:
- Tipografia: Editorial Stack Typo B — IBM Plex Sans 300 + Libre Caslon Text italic + Space Mono
- Cores: fundo #0A0C10, texto #B2A898, accent #A89D80
- Grid de fundo: 54×54px
- CSS e JS 100% inline — zero dependências externas além do Google Fonts

## Skills disponíveis

| Skill | Descrição | Pasta |
|-------|-----------|-------|
| Teams Setup Playbook | Implanta o Claude Teams em 7 dias | `skills/teams-setup-playbook/` |
