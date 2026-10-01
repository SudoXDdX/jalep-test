# JALEP Test — MEMORY.md

## Purpose
Sandbox for testing dangerous/experimental changes before applying to jalep-mano or jalep-glass.

## Sites
- **jalep-mano** (Material Web): https://sudoxddx.github.io/jalep-mano/
- **jalep-glass** (Liquid Glass): https://sudoxddx.github.io/jalep-glass/
- **jalep-test** (Sandbox): https://sudoxddx.github.io/jalep-test/

## Current State (2026-10-01)
- Both sites deployed and working
- Blur reduced ~30% from previous values
- Google Sans Flex font implemented (6-axis variable font)
- André's card: "TI · Técnico · Security Researcher · Influencer"
  - Bio includes CVE-2026-43499 (Ghost Lock), Root-My-Galaxy, bug bounty
- Gender text REMOVED from Pedro's card (no more "giselle gulosa, K")
- jalep-glass: REAL Liquid Glass with SVG feDisplacementMap refraction + chromatic aberration + Fresnel rim highlights + ambient mesh

## Architecture
- Static Next.js 16 export (output: "export") for GitHub Pages
- basePath: /jalep-mano/ or /jalep-glass/
- CSS override via upgrade.css (loaded after main CSS)
- JS data in 2f96d62cb546de75.js (Turbopack RSC chunk)

## Research Findings
### Google Sans Flex
- 6-axis variable font: opsz(6-144), wdth(25-151), wght(1-1000), GRAD(0-100), ROND(0-100), slnt(-10-0)
- CDN: fonts.googleapis.com/css2?family=Google+Sans+Flex
- npm: @fontsource/google-sans-flex

### Liquid Glass Implementations
1. **liquid-dom** (AndrewPrifer) — WebGPU, most advanced
2. **archisvaze/liquid-glass** — SVG + WebGL, best demo
3. **hyalite** (VII-Cae) — Pure SVG, no WebGL, folding technique

### Tool Recommendations
- Runtime: Node.js 22 LTS (prod) + Bun (dev)
- CSS: Tailwind CSS v4
- PM: pnpm 10 (monorepo)
- React: React 19 (for Next.js 16)

## Next Steps
- [ ] Transform to /src project with Backend
- [ ] Template-ize both sites
- [ ] Consider hyalite.js for even better Liquid Glass
