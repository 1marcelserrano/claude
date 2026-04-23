# SETUP_HUB_GUIDE — Criar um Hub de Skills do Zero

**Versão:** 1.0  
**Data:** 2026-04-23  
**Escopo:** Guia completo para estruturar, desenhar e publicar um novo hub de skills MSCREATIVE.SYSTEMS

---

## 1. VISÃO GERAL

Um **hub de skills** é um repositório com:
- **Índice navegável** (`index.html` na raiz) que lista todas as skills disponíveis
- **Pasta por skill** (`skills/[nome]/`) com landing page e arquivo `.skill`
- **Design system unificado** (tipografia, cores, grid 54×54px, CSS inline)
- **Zero dependências externas** além do Google Fonts

### Exemplo de estrutura:
```
github.com/[user]/[hub-name]/
├── index.html                           ← Hub principal (lista de skills)
├── README.md                            ← Documentação do repositório
├── SETUP_HUB_GUIDE.md                   ← Este guia
├── skills/
│   ├── [skill-1]/
│   │   ├── index.html                   ← Landing page
│   │   └── [skill-1].skill              ← Arquivo da skill
│   └── [skill-2]/
│       ├── index.html
│       └── [skill-2].skill
└── assets/shared/                       ← Recursos compartilhados (futuro)
```

---

## 2. DESIGN SYSTEM — MSCREATIVE.SYSTEMS V3.0

Todos os arquivos HTML do hub seguem este design system:

### Tipografia
- **Display/Heading:** IBM Plex Sans 300 (font-weight: 300)
- **Body:** IBM Plex Sans 300 (font-weight: 300)
- **Label/Monospace:** Space Mono 400/700
- **Accent/Serif:** Libre Caslon Text (italic para destaque)

### Importação do Google Fonts
```html
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:ital,wght@0,300;1,300&family=Libre+Caslon+Text:ital,wght@0,400;1,400&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
```

### Paleta de Cores
```
--ds-bg-primary:       #0A0C10  ← Fundo geral
--ds-bg-secondary:     #12141A  ← Fundo para seções
--ds-bg-surface:       #1A1D26  ← Cards e superfícies
--ds-bg-surface-hover: #22262F  ← Hover em cards
--ds-text-primary:     #B2A898  ← Títulos e destaque
--ds-text-body:        #B2A898  ← Corpo de texto
--ds-text-secondary:   rgba(178, 168, 152, 0.65)  ← Subtítulos
--ds-text-muted:       rgba(178, 168, 152, 0.38)  ← Labels e metadata
--ds-ms-accent-1:      #A89D80  ← Accent principal (botões, bordas)
--ds-ms-accent-2:      #756750  ← Accent secundário (hover)
--ds-border-subtle:    rgba(255, 255, 255, 0.06)  ← Bordas finas
--ds-grid-color:       rgba(255, 255, 255, 0.025) ← Grid de fundo
--ds-grid-size:        54px                        ← Tamanho da célula do grid
--ds-radius-sm:        2px                         ← Border radius pequeno
--ds-radius-md:        4px                         ← Border radius médio
```

### Grid de Fundo
```css
background-image:
  linear-gradient(var(--ds-grid-color) 1px, transparent 1px),
  linear-gradient(90deg, var(--ds-grid-color) 1px, transparent 1px);
background-size: var(--ds-grid-size) var(--ds-grid-size);
```

### Estratégia de CSS
- **100% inline** — todo CSS dentro de `<style>` na head
- **Nenhuma dependência** além do Google Fonts
- **Mobile first** — media queries para responsividade
- **Variáveis CSS** — todos os valores hardcoded como custom properties `:root {}`

---

## 3. PASSO A PASSO — CRIAR UM HUB NOVO

### 3.1 Clonar ou criar o repositório

```bash
# Opção A: Clonar um hub existente e limpar
git clone https://github.com/[user]/[hub-name].git
cd [hub-name]
git checkout --orphan main
git rm -rf .

# Opção B: Inicializar novo repo
mkdir [hub-name]
cd [hub-name]
git init
git config user.email "[seu-email]"
git config user.name "[seu-nome]"
```

### 3.2 Criar estrutura de pastas

```bash
mkdir -p skills/[skill-1]
mkdir -p skills/[skill-2]
mkdir -p assets/shared
```

### 3.3 Criar `README.md` na raiz

Template mínimo:
```markdown
# [NOME DO HUB] — Hub de Skills

Repositório de landing pages para skills do Claude Cowork.
Cada skill tem sua própria pasta em `skills/` com uma landing page independente.

## Estrutura

\`\`\`
skills/
└── [nome-da-skill]/
    ├── index.html                  ← landing page da skill
    └── [nome-da-skill].skill       ← arquivo de instalação
\`\`\`

## Como adicionar uma nova skill

1. Criar pasta: \`skills/[nome-da-skill]/\`
2. Adicionar \`index.html\` seguindo o design system MSCREATIVE.SYSTEMS V3.0
3. Adicionar o arquivo \`.skill\` na mesma pasta
4. Adicionar card no \`index.html\` da raiz

## Design System

Todas as páginas seguem MSCREATIVE.SYSTEMS V3.0:
- Tipografia: IBM Plex Sans 300 + Libre Caslon Text italic + Space Mono
- Cores: fundo #0A0C10, texto #B2A898, accent #A89D80
- Grid de fundo: 54×54px
- CSS e JS 100% inline — zero dependências externas além do Google Fonts

## Skills disponíveis

| Skill | Descrição | Pasta |
|-------|-----------|-------|
| [Skill 1] | Descrição breve | \`skills/skill-1/\` |
```

### 3.4 Criar `index.html` na raiz (hub de navegação)

**Estrutura base:**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Skills — MSCREATIVE.SYSTEMS</title>
  <meta name="description" content="Hub de skills para Claude Cowork.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:ital,wght@0,300;1,300&family=Libre+Caslon+Text:ital,wght@0,400;1,400&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
  <style>
    /* VARIÁVEIS CSS */
    :root {
      --ds-font-display: 'IBM Plex Sans', sans-serif;
      --ds-font-body: 'IBM Plex Sans', sans-serif;
      --ds-font-label: 'Space Mono', monospace;
      --ds-font-accent: 'Libre Caslon Text', Georgia, serif;
      --ds-bg-primary: #0A0C10;
      --ds-text-primary: #B2A898;
      --ds-text-secondary: rgba(178, 168, 152, 0.65);
      --ds-text-muted: rgba(178, 168, 152, 0.38);
      --ds-ms-accent-1: #A89D80;
      --ds-border-subtle: rgba(255, 255, 255, 0.06);
      --ds-grid-color: rgba(255, 255, 255, 0.025);
      --ds-grid-size: 54px;
      --ds-radius-md: 4px;
    }

    /* RESET */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    /* BODY */
    body {
      background-color: var(--ds-bg-primary);
      color: var(--ds-text-body);
      font-family: var(--ds-font-body);
      font-size: 16px;
      line-height: 1.6;
      background-image:
        linear-gradient(var(--ds-grid-color) 1px, transparent 1px),
        linear-gradient(90deg, var(--ds-grid-color) 1px, transparent 1px);
      background-size: var(--ds-grid-size) var(--ds-grid-size);
      -webkit-font-smoothing: antialiased;
    }

    /* ... resto do CSS ... */
  </style>
</head>
<body>
  <!-- HEADER -->
  <header>
    <div class="container">
      <div class="header-inner">
        <span class="label">MSCREATIVE.SYSTEMS</span>
        <span class="label">SKILLS HUB</span>
      </div>
    </div>
  </header>

  <!-- HERO -->
  <div class="page-hero">
    <div class="container">
      <h1 class="page-title">Skills para<br>Claude Cowork.</h1>
      <p class="page-subtitle">Módulos prontos para instalar.</p>
    </div>
  </div>

  <!-- SKILLS GRID -->
  <section class="skills-section">
    <div class="container">
      <div class="skills-header"><span class="label">SKILLS DISPONÍVEIS</span></div>
      <div class="skills-grid">
        <a href="skills/[skill-1]/index.html" class="skill-card">
          <div class="skill-card-tag"><span class="label">[TAG] · V1 · GRATUITO</span></div>
          <h2 class="skill-card-title">[Skill Name]</h2>
          <p class="skill-card-desc">[Descrição breve]</p>
          <span class="skill-card-arrow">VER SKILL →</span>
        </a>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <div class="container">
      <div class="footer-inner">
        <span class="label">MSCREATIVE.SYSTEMS</span>
        <span class="label">SKILLS HUB</span>
      </div>
    </div>
  </footer>
</body>
</html>
```

**CSS essencial para index.html:**
- `.container` com max-width 1080px
- `.page-hero` para seção de boas-vindas
- `.skills-grid` com grid responsivo
- `.skill-card` com hover state
- `.label` em Space Mono com uppercase
- Responsividade para mobile (< 600px)

### 3.5 Criar `skills/[skill-name]/index.html` (landing page)

**Estrutura esperada:**
1. **Hero section** com título, subtitle e call-to-action para download
2. **Seção 1: O que é / Por que importa** — contexto e valor
3. **Seção 2: Comparação** (sem skill vs com skill)
4. **Seção 3: Entregáveis** — o que a skill fornece (grade)
5. **Seção 4: Como instalar** — 3 passos simples
6. **CTA final** — chamada repetida para download

**Animações:**
- Fade-in progressivo ao scroll (Intersection Observer)
- Transição de 0.6s com 20px translateY
- Delay escalonado por elemento (80ms entre eles)

**Componentes reutilizáveis:**
- `.btn-primary` — botão de download
- `.section-header` com número e título
- `.comparison-grid` — 2 colunas com cards
- `.deliverables-grid` — grid de entregáveis
- `.steps-grid` — 3 passos com números grandes

### 3.6 Criar `skills/[skill-name]/[skill-name].skill`

O arquivo `.skill` é um ZIP contendo:
```
[skill-name].skill
├── [skill-name]/SKILL.md
└── (outros arquivos, se necessário)
```

**Conteúdo mínimo de SKILL.md:**
- Frontmatter com name, description, type
- Prompt que define o comportamento da skill
- Instruções claras para o Claude

---

## 4. CHECKLIST DE IMPLEMENTAÇÃO

- [ ] Repositório criado e clone feito
- [ ] Pastas criadas: `skills/[skill]/`, `assets/shared/`
- [ ] `README.md` escrito e committado
- [ ] `index.html` na raiz com:
  - [ ] Fontes Google Fonts importadas
  - [ ] Variáveis CSS com paleta completa
  - [ ] Grid de fundo 54×54px
  - [ ] Header com MSCREATIVE.SYSTEMS label
  - [ ] Hero com título e subtitle
  - [ ] Skills grid com cards
  - [ ] Footer com labels
  - [ ] Responsividade (mobile < 600px)
- [ ] `skills/[skill-1]/index.html` com:
  - [ ] Hero section com botão de download
  - [ ] 5 seções de conteúdo (O que é, Por quê, Entregáveis, Como instalar, CTA)
  - [ ] Animações fade-in ao scroll
  - [ ] Tipografia e cores alinhadas ao design system
  - [ ] Responsividade
  - [ ] Link para download do `.skill`
- [ ] `skills/[skill-1]/[skill-1].skill` criado e testado
- [ ] Primeiro commit: `feat: initial structure + [skill-name] landing page`
- [ ] Push para `main` no GitHub
- [ ] Verificação final: landing page acessível e funcionando

---

## 5. MANUTENÇÃO E EXTENSÃO

### Adicionar uma nova skill ao hub existente

1. Criar pasta: `skills/[skill-novo]/`
2. Copiar template de `index.html` de uma skill existente
3. Personalizar conteúdo (textos, seções, entregáveis)
4. Criar arquivo `.skill` e testar
5. Adicionar card no `index.html` da raiz:
   ```html
   <a href="skills/[skill-novo]/index.html" class="skill-card">
     <div class="skill-card-tag"><span class="label">[TAG] · V1 · GRATUITO</span></div>
     <h2 class="skill-card-title">[Skill Name]</h2>
     <p class="skill-card-desc">[Descrição breve]</p>
     <span class="skill-card-arrow">VER SKILL →</span>
   </a>
   ```
6. Atualizar tabela no `README.md`
7. Commit e push: `feat: add [skill-novo] landing page`

### Atualizar design ou tipografia

- Modificar variáveis CSS `:root` em ambos os arquivos (raiz e skills)
- Testar responsividade com `@media (max-width: 768px)` e `@media (max-width: 480px)`
- Commit: `style: update [item] design`

---

## 6. EXEMPLO REAL

Veja `github.com/1marcelserrano/claude` para um exemplo completo:
- Repository: https://github.com/1marcelserrano/claude
- Hub ao vivo: (URL será adicionada quando hospedado)
- Skills: `teams-setup-playbook` + futuras

---

## 7. NOTAS TÉCNICAS

### CSS Inline vs External
- **Por quê inline?** Zero dependências, arquivo único por página, mais rápido para landing pages estáticas
- **Quando considerar externo?** Se o hub tiver >10 skills e muita repetição de CSS, considerar um `style.css` compartilhado

### Responsividade
- **Mobile-first:** começar com mobile, usar media queries para desktop
- **Breakpoints:** 480px (mobile), 768px (tablet), 1080px+ (desktop)
- **Grid:** ajustar de `grid-template-columns: repeat(3, 1fr)` para `grid-template-columns: 1fr` em mobile

### Performance
- **Grid de fundo:** renderiza via CSS, sem imagens
- **Fontes:** Google Fonts é carregado com `display=swap` para fallback rápido
- **Imagens:** não recomendadas, preferir SVG inline ou descrição textual

### Acessibilidade
- Usar `<h1>`, `<h2>`, `<section>` com semântica correta
- Labels e descrições em `<p>` ou `<span class="label">`
- Cores com contraste mínimo AA (verificar com ferramentas como WebAIM)
- Alt text em SVGs inline (ou `aria-label` se decorativo)

---

**Versão:** 1.0 | **Última atualização:** 2026-04-23 | **Autor:** Claude Code / MSCREATIVE.SYSTEMS
