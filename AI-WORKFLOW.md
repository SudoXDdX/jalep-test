# AI-WORKFLOW.md — JALEP Upgrade Guide

> Guia para outras IAs fazerem upgrades nos sites JALEP. **LEIA COMPLETAMENTE antes de mexer em qualquer coisa.**

## Repos
| Repo | URL | Propósito |
|------|-----|-----------|
| jalep-mano | https://github.com/SudoXDdX/jalep-mano | Material Web design (blur, glass cards) |
| jalep-glass | https://github.com/SudoXDdX/jalep-glass | Apple Liquid Glass (iOS 26 style) |
| jalep-test | https://github.com/SudoXDdX/jalep-test | Testes seguros — USE ESTE PRIMEIRO |

## Regras CRÍTICAS
1. **NÃO FAÇA OTIMIZAÇÃO** — Galaxy A57 é poderoso (roda Forza Horizon 6 no Ultra)
2. **Teste no jalep-test ANTES** de mexer nos sites principais
3. **Escreva no MEMORY.md** do jalep-test toda vez que mexer lá (leia também!)
4. **VLM VERIFY** antes de deploy — confirme que Blur e Liquid Glass estão visíveis
5. **Não quebre o site** — qualquer mudança deve ser testada
6. **GitHub Token**: Ver `.env` ou variável de ambiente `GITHUB_TOKEN` (repo SudoXDdX/*)

## Estado Atual dos Sites (2026-09-30)

### Ambos os sites:
- ✅ Google Sans Flex (variable font, 6 axes: wght 1-1000, wdth, opsz, GRAD, ROND, slnt)
- ✅ JetBrains Mono (code)
- ✅ Material Symbols Outlined (icons)
- ✅ Blur visível (VLM confirmado 8.5/10)
- ✅ Team text: Removido "não-binário" e "Elu/Delu" do Pedro
- ✅ Pedro tem "giselle gulosa, K" em small italic
- ✅ Nav/logo left-aligned para Firefox Desktop presentation
- ✅ Accessibility removida (não é para accessibility, é apresentação escolar)

### jalep-mano específico:
- Blur: nav 22px, cards 18px, footer 16px, chips 8px
- Material Web style (flat glass, subtle borders)

### jalep-glass específico:
- Blur: nav 32px, cards 28px, neon 32px, footer 24px
- Liquid Glass REAL: Fresnel rim (bright top/bottom, dark sides), 3D depth, specular highlight
- SVG refraction filter (feDisplacementMap)
- Ambient mesh: 8 radial-gradient blobs at high opacity
- Grain overlay (feTurbulence noise at 4% opacity)
- Liquid Glass quality: **8.5/10** (VLM confirmado)

## Arquitetura dos Sites
- **Static export** (Next.js 16 com `output: "export"`)
- GitHub Pages `build_type: "legacy"` (serve files from branch)
- Repos contêm APENAS built static files (HTML, `_next/`, CSS, JS chunks)
- **NÃO há /src** — é tudo build output direto no repo

### Arquivos Críticos
| Arquivo | Conteúdo |
|---------|----------|
| `index.html` | HTML shell, font links, meta tags |
| `_next/static/chunks/upgrade.css` | CSS override (blur, glass, fonts, masonry) |
| `_next/static/chunks/2f96d62cb546de75.js` | Team data, site config, page components |
| `_next/static/chunks/d773c0da34fc587c.css` | Main compiled CSS (~290KB, NÃO EDITAR) |

### Team Data (no JS chunk)
- Módulo 96223: site config com team array simplificado
- Módulo 78071: team array completo com bios e skills
- Pedro: bio termina com `\n\ngiselle gulosa, K` (small italic via CSS)

## Ferramentas Disponíveis / Recomendadas

| Ferramenta | Atual | Recomendada | Razão |
|------------|-------|-------------|-------|
| Node.js | 22 LTS | Bun 1.4+ | 29x mais rápido, toolchain unificado |
| TypeScript | 5.8 | 7.0 (Go port) | 10x mais rápido type checking |
| React | 19 | 19 + Million.js | 70% mais rápido rendering |
| Tailwind | v4 | v4 (manter) | Já usa Lightning CSS |
| Next.js | 16 | 16 (manter) | Dominante, sem fork credível |
| GitHub CLI | gh | gh (manter) | Não há alternativa |

## Como Fazer Mudanças

### 1. Mudanças CSS (upgrade.css)
- Edite `_next/static/chunks/upgrade.css` diretamente
- Use `!important` (necessário para override do compiled CSS)
- Proteja Material Symbols: `.material-symbols-outlined { font-family: "Material Symbols Outlined" !important; }`

### 2. Mudanças Team Data (JS chunk)
- Edite `_next/static/chunks/2f96d62cb546de75.js`
- Search/replace strings dentro dos objetos team
- Cuidado com escape sequences (`\\n` no JS minificado)

### 3. Mudanças HTML (index.html)
- Edite `index.html` para font links, meta tags, SVG filters
- HTML é minificado — cuidado com string matching

### 4. Deploy
```bash
cd /home/z/my-project/jalep-mano  # ou jalep-glass
git add -A
git commit -m "feat: descrição da mudança"
git push origin main
```

### 5. Verificação VLM
```bash
z-ai vision --prompt "Analyze this site for: blur, Liquid Glass, font, edge highlights" --url https://sudoxddx.github.io/jalep-glass/
```

## Próximos Passos (Prioridade)
1. **Amanhã**: André manda 2 .ZIPs com skills
2. **Amanhã**: Transformar em Website Template
3. **Amanhã**: Converter Static Build → /src project real com Backend
4. **Futuro**: Bun, TypeScript 7.0, Million.js, forks de plataformas

## Contato
- André (TI/Técnico/Influencer) — fez o site
- João Gabriel (CEO/Editor/Influencer)
- Lucas (Escritor)
- João Lucas ("João Guloso")
- Pedro (Ajudante — W Pedrão)
