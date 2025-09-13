
=========
# Git commands

```
git branch feature-rolo
git checkout feature-rolo
git add .
git commit -m "feature-rolo: Estrategia de Ramas Sostenible y Prevención de *Branching Hell*"
git push origin feature-rolo
```
=========

# Estrategia de Ramas Sostenible y Prevención de *Branching Hell*

## Principios Clave
- **Trunk-Based Development (TBD)**: ramas cortas (≤ 3–5 días) y merge continuo a `main`.
- **Feature Flags**: evita ramas largas liberando código parcialmente sin exponerlo.
- **Pequeño y frecuente**: PRs de ≤ 400 LOC, 1–2 revisores, ciclo < 24h.
- **Automatización**: todo lo repetitivo debe ir a CI/CD.

---

## Modelo de Ramas
- **`main`**: siempre desplegable (rama protegida).
- **`release/x.y`** *(opcional)*: solo para QA prolongado o soporte de versiones.
- **Trabajo diario**:
  - `feat/<área>/<resumen-kebab>`
  - `fix/<área>/<resumen-kebab>`
  - `refactor/<área>/<resumen-kebab>`
  - `chore/`, `docs/`, `perf/`

**Ejemplos**:
- `feat/cart/guest-checkout`
- `fix/payments/retry-timeout`

---

## Convenciones de Naming y Commits
- **Ramas**: `<tipo>/<área>/<resumen>`  
- **Commits**: [Conventional Commits](https://www.conventionalcommits.org/)  
  - `feat(cart): add guest checkout flow`
  - `fix(api): handle 429 with jitter`
- **PRs**: plantilla con:
  - Contexto
  - Cambios
  - Riesgos
  - Flags/Rollout
  - Checklist de pruebas

---

## Reglas de Protección de Ramas
- `main` protegida:
  - Solo merges vía PR.
  - **Squash & merge** para historial limpio.
  - Requerir build, tests, linters, cobertura mínima y revisiones aprobadas.
  - Bloquear force-push.
  - **CODEOWNERS** para revisión por área.
- TTL de ramas: cerrar o marcar `stale` tras 10–14 días sin actividad.

---

## CI/CD Essentials

### CI por PR
- Linter + formateo (Prettier, ESLint, Black).
- Unit tests + cobertura (≥ 80%).
- Static Analysis (Sonar/CodeQL).
- Security Scans (SCA, SAST, gitleaks).
- Entorno de **preview** por PR.

### CD
- `main` → **staging** automático (con smoke tests).
- Promoción a **prod** con *gate* manual o *release trains*.
- **Blue/Green o Canary** + rollback automático si falla healthcheck.
- **Semantic Release** o **Changesets**: genera changelog, tag y release notes.

---

## Automatizaciones y Bots
- **Renovate/Dependabot**: mantener dependencias al día.
- **Mergify/Danger**: auto-merge de PRs aprobados, bloquea PRs grandes sin tests.
- **Semantic Release / Changesets**: versionado semántico + changelog.
- **Git Hooks** (`pre-commit`): lint-staged, formateo, detección de secretos.
- **Backport bot**: para `release/x.y`.
- **Branch cleanup**: borrar ramas después del merge.

---

## Gestión de Releases y Hotfixes
- **Tren de releases**: cadencia fija (diaria/semanal).
- **Hotfix**: `hotfix/<issue>` desde el tag de producción → merge a `main` y backport.
- **Tags**: `vMAJOR.MINOR.PATCH`, firmados y con changelog generado.

---

## Feature Flags y Rollout
- Uso de LaunchDarkly/Unleash/ConfigCat (o propio).
- Soporte para:
  - Rollouts por porcentaje.
  - Filtrado por país, tenant, usuario.
  - Kill switch inmediato.
- Merge a `main` **solo con flag** activado/desactivado según estado de la feature.

---

## Monorepo / Multi-servicio
- Nx / Turborepo / Bazel para caching y *affected builds*.
- Pipelines con matriz selectiva (solo construir/testear lo afectado).
- CODEOWNERS por carpeta o paquete.

---

## Métricas de Salud
- **Lead Time PR**: < 24h.
- **Tamaño PR**: mediana < 300 LOC.
- **Ramas activas > 7 días**: < 5%.
- **Rollback rate**: < 2% de despliegues/mes.
- **DORA metrics**: medir MTTR y Change Failure Rate.

---

## Checklist Express
- [ ] Activar branch protection en `main`.
- [ ] Adoptar Conventional Commits + plantilla de PR.
- [ ] Configurar CI con lint, tests, cobertura, SAST/SCA y preview env.
- [ ] CD: staging automático, producción con gates + canary.
- [ ] Implementar feature flags para todo lo no trivial.
- [ ] Activar bots (Renovate, Semantic Release, Mergify, Stale).
- [ ] Política de PR pequeño y TTL de ramas.
- [ ] Documentar en `CONTRIBUTING.md` y usar `CODEOWNERS`.

