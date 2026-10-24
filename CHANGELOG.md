# Changelog

## Sin publicar

- `discover` separa la necesidad de la vista. Las vistas de un mock o un quick design ya no se escriben
  como requisitos: van a «Para sdd-design › ux.md» como hipótesis de interfaz, y la estructura se decide
  al prototipar. Hay regla nueva en el paso 1 y un punto nuevo, «Sin vistas», en la lista de calidad de
  `ears.md`. Los puntos siguientes de esa lista se renumeran.
- Los ejemplos de `discover`, de `sdd/references/proyecto.md` y de la norma de git son de un producto
  inventado, Regadera, en vez de productos reales. Los huecos de `gaps.md` dejan de suponer una
  extensión de navegador.
- El repo se aísla. `.claude/settings.json` bloquea las lecturas fuera del repo, y un hook bloquea los
  comandos de terminal que salen de él. El `CLAUDE.md` del repo explica la regla.
- Plugin `ux`: se retiran del plugin las referencias de la 0.3.1, que siguen en el tag `v0.3.1`. La
  skill se rehace desde cero con el brief y la investigación de `material/`. El plan del README pasa a
  dos skills, `/ux:mock` y `/ux:polish`.

## 0.3.1 · 2026-10-22

- Plugin `ux` (planeado): sus referencias de investigación, en `plugins/ux/references/`. Son nueve
  archivos con los principios de UI/UX que usará `/ux:explore`: método, tareas, estructura, jerarquía,
  estados y textos, evaluación y accesibilidad. Cada principio lleva su fuente, cómo se mide con
  Playwright y su confianza. Los mitos van en cada archivo, y las decisiones abiertas, en el índice.
- El README describe de nuevo `/ux:explore`. El método saldrá de esta investigación y de una pasada a
  mano con un producto real, no de la exploración por tandas que anunciaba la 0.3.0.

## 0.3.0 · 2026-10-22

- **Rompe:** el repo pasa a ser `LimbersMay/skills`, el marketplace `limbersmay` y los plugins `sdd` y
  `git`. Las skills se invocan sin prefijos repetidos: `/sdd:discover`, `/git:commit`, `/git:ship`. Para
  migrar: `/plugin marketplace remove re-skills` y los pasos de «Instalar» del README.
- Las skills ya no dependen de la suite Re. `sdd/references/proyecto.md` dice qué estructura de `docs/`
  espera `sdd` y qué piezas declara el proyecto en su `AGENTS.md` (sistema de diseño, estado, verde,
  trazabilidad, git, textos), con lo que hace la skill si falta alguna. `discover` y la norma de git
  hablan de esas piezas, y ReTemplate y ReDesign quedan como ejemplo.
- Plan: nuevo plugin `ux` con `/ux:explore`, la exploración de interfaz por tandas que `/sdd:design`
  llamará para `ux.md`.

## 0.2.2 · 2026-10-22

- Plan de skills: `sdd-plan` entra en `sdd-design`, `sdd-guide` en `sdd-work` (con un modo para cuando el
  usuario se atora) y `sdd-close` en `sdd-verify`, que también llama a `re-git`. `/re-sdd:next` es la
  entrada única. Solo cambia el plan del README: ninguna skill construida cambia.

## 0.2.1 · 2026-10-22

- `re-git`: la norma prohíbe la atribución también en los cuerpos de las PRs y en las notas de las
  releases, no solo en los commits, aunque el entorno pida añadirla. `ship` y `commit` lo repiten en «Lo
  que nunca haces».

## 0.2.0 · 2026-10-22

- Nuevo plugin `re-git` con la norma de git de la suite (ramas, commits, PRs, versiones) y dos skills:
  `/re-git:commit` (rama si hace falta, commits por tarea con `[Sxx-Tn]` y pie `Requisitos:`) y
  `/re-git:ship` (comprobaciones, CHANGELOG, versión, PR, merge commit, tag y release).
- Un directorio por plugin: `plugin/` pasa a `plugins/re-sdd/`. Quien lo tenga instalado solo necesita
  `/plugin marketplace update re-skills`.
- `sdd-discover`: ronda de cierre. La revisión de calidad corrige sin preguntar lo que no cambia el
  comportamiento y convierte en Propuestas de cierre lo que sí (sobre todo los «SI … ENTONCES» que
  faltan). No se pide la aprobación hasta que todas tienen respuesta.
- `sdd-discover`: requisitos retirados. Cuándo se corrige en el sitio y cuándo se retira, y el formato
  (ID fuera del tachado, línea `Retirado:`).
- `sdd-discover`: doce Propuestas por ronda como mucho; las demás pasan a `⏳ próxima ronda`.

## 0.1.0 · 2026-10-21

- `sdd-discover`: mapa del material, contradicciones, huecos en seis categorías MECE (Alcance, Tiempo,
  Transiciones, Datos, Fallos, Interfaz) con tres clases (Bloquea, Propuesta, En su slice), rondas de
  tres preguntas como máximo y borradores de `product.md` y `requirements.md` en EARS.
