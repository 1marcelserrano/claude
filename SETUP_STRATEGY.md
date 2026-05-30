# SETUP_STRATEGY — Auditoria e Roadmap de Organização

> Registro do diagnóstico e do plano em fases para profissionalizar este repositório.
> Gerado por auditoria em **2026-05-30** (branch `claude/repo-organization-CAruX`).

## 1. Contexto verificado

| Item | Valor (verificado) |
|---|---|
| Repositório | `1marcelserrano/claude` — MSCREATIVE.SYSTEMS — Hub de Skills |
| Natureza | Site estático (Vercel) + acervo de método. Sem build. |
| 1º commit real | `2026-04-23` (`git log --diff-filter=A`) |
| Commits | 6 · working tree limpo |
| Tamanho | ~100K conteúdo / ~460K `.git` |
| Maior arquivo | `skills/aboissa-teams-hub/index.html` (24K) |
| Idioma adotado | Português (docs e commits) |

## 2. Diagnóstico — problemas estruturais

| # | Problema | Evidência | Prioridade |
|---|---|---|---|
| P1 | Sem fundação para colaboração/agentes | faltavam `.gitignore`, `.gitattributes`, `CLAUDE.md`, `.github/`, CI | Alta |
| P2 | Doc de processo misturado com o site publicado | `SETUP_HUB_GUIDE.md` na raiz → servido em `/SETUP_HUB_GUIDE.md` | Média |
| P3 | Design system declarado ≠ implementado | `aboissa-teams-hub/index.html` usa `Inter`, não IBM Plex (V3.0) | Média — requer dono |
| P4 | Skill `aboissa-teams-hub` sem arquivo `.skill` | só `teams-setup-playbook` tem `.skill` | Baixa — não verificável |
| P5 | Sem LICENSE | ausente | Baixa — adiada |

**Tensão central:** o repositório é simultaneamente um **artefato publicado** e um
**acervo de método**, mas ambos viviam misturados na raiz, sem camada de fundação, e a
regra de design que o próprio repo declara não bate com uma das skills.

## 3. Roadmap em fases

### Fase 0 — Fundação (não-destrutiva) ✅
Cria o que falta sem mover nada:
- `.gitignore`, `.gitattributes`
- `CLAUDE.md` (contexto para agentes)
- `.github/` — template de PR, templates de issue (nova skill / bug), workflow de CI
- `SETUP_STRATEGY.md` (este arquivo)

### Fase 1 — Taxonomia ✅
Separa o **durável/processo** do **artefato publicado**, via `git mv` (preserva histórico):
- `SETUP_HUB_GUIDE.md` → `docs/setup-hub-guide.md`
- Atualiza referências no `README.md`

### Fase 2 — Convenções ✅
- `CONTRIBUTING.md` — padrão de nomes (kebab-case), commits (Conventional Commits),
  como adicionar uma skill, aderência ao design system.
- **Legado não é renomeado em massa** — os arquivos existentes já estão em kebab-case.

### Fase 3 — Higiene de Git ✅
- `.gitattributes`: marca `*.skill` como binário.
- **Git LFS: não necessário** — maior arquivo é 24K (limiar de LFS é tipicamente >1MB).
  Comando documentado abaixo caso mídia pesada seja adicionada no futuro.
- **Histórico: saudável** — sem artefatos efêmeros rastreados, sem mídia pesada,
  nada a remover. Nenhuma reescrita de histórico/force-push proposta.

## 4. Ações pendentes do dono (requerem decisão humana)

- [ ] **LICENSE** — escolher (CC BY 4.0 para conteúdo, MIT para código, ou manter privado).
- [ ] **P3** — decidir se `aboissa-teams-hub` deve migrar de `Inter` para IBM Plex (V3.0)
      ou se o uso de `Inter` é branding intencional a ser grandfatherado.
- [ ] **P4** — confirmar se `aboissa-teams-hub` precisa de um arquivo `.skill` ou é um
      hub de onboarding sem download.

## 5. Comandos que exigem ambiente real (fora do sandbox)

```bash
# Git LFS — SOMENTE se mídia pesada (>1MB) for adicionada futuramente:
git lfs install
git lfs track "*.mp4" "*.png" "*.jpg" "*.pdf"
git add .gitattributes
git commit -m "chore: habilita Git LFS para mídia pesada"
```
