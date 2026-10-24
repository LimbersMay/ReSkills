# skills

Skills de Claude Code de Limbers May, en el marketplace `limbersmay`. No dependen de ningún producto: la
skill pone el método y cada proyecto declara sus piezas (sistema de diseño, estado, verde…) en su
`AGENTS.md` ([qué espera `sdd`](plugins/sdd/references/proyecto.md)).

- **`sdd`:** spec-driven development sobre una estructura de `docs/` (`inbox/`, `product.md`,
  `requirements.md`, `specs/`…). Una plantilla puede traerla lista, pero cualquier proyecto puede
  adoptarla.
- **`git`:** una [norma de git](plugins/git/skills/commit/references/norma.md) aplicada. Vale para
  productos y librerías.
- **`ux`** (planeado): diseño de interfaz en dos fases, un prototipo que se prueba y el pulido.

## Instalar

Una vez por máquina, en Claude Code:

```text
/plugin marketplace add LimbersMay/skills
/plugin install sdd@limbersmay
/plugin install git@limbersmay
```

Para probar cambios sin publicarlos, desde una copia local:

```text
/plugin marketplace add <ruta a la copia local>
```

Después de cambiar una skill: `/plugin marketplace update limbersmay`.

**Desde la 0.2.x** (marketplace `re-skills`): `/plugin marketplace remove re-skills` y después los pasos de
arriba. En un proyecto que lo declare en `.claude/settings.json`, se cambian `extraKnownMarketplaces` y
`enabledPlugins` a los nombres nuevos.

## Skills

No hace falta recordarlas. `/sdd:next` leerá el estado del proyecto y ejecutará el paso que toca, y cada
skill también se dispara hablando normal: «siguiente ronda», «estoy atorado en T3», «T2 ok».

| Skill | Cuándo | Qué hace | Estado |
|---|---|---|---|
| `/sdd:next` | Siempre | Lee el estado del proyecto y ejecuta el paso que toca | Planeada |
| `/sdd:discover` | Fase 0 | Del material de `docs/inbox/` a `product.md` y `requirements.md` en EARS, con huecos MECE y rondas de preguntas | ✅ 0.3.0 |
| `/sdd:design` | Fase 0 | `domain.md`, `architecture.md`, `ux.md`, los spikes y `roadmap.md` (slices verticales por dependencias y riesgo). Para la interfaz llama a `/ux:mock` y `/ux:polish` | Planeada |
| `/sdd:slice` | Slice | La spec y las tareas de un slice | Planeada |
| `/sdd:work` | Slice | Una tarea, según su «Modo» en `tasks.md`. **Del agente:** tests primero y después el código. **Tuya, sin empezar:** tests en rojo y la guía. **Tuya, en curso:** si te atoras, lee tu diff y los tests que fallan y da pistas por niveles (qué pide el test → dónde mirar → la forma en palabras → el código, solo si lo pides), y anota el atasco en «Notas de estudio» | Planeada |
| `/sdd:verify` | Slice | Verifica una tarea contra su spec, escribe `review.md` y, con tu OK, la commitea. Con la última tarea, cierra el slice (docs al día, roadmap) y abre su PR | Planeada |
| `/git:commit` | Siempre | Rama si hace falta, un commit por tarea con `[Sxx-Tn]` y su pie, y sube la rama. En un producto lo llama `/sdd:verify` | ✅ 0.3.0 |
| `/git:ship` | Al cerrar una rama | Comprueba, CHANGELOG y versión, PR, merge commit con tu OK, tag y release. En un producto lo llama `/sdd:verify` al cerrar el slice | ✅ 0.3.0 |
| `/ux:mock` (nombre provisional) | Interfaz | De los requisitos y un quick design a un prototipo navegable en grises, que el usuario prueba por vueltas hasta aprobar la estructura. Sin sistema de diseño. Termina en `ux.md` | Planeada |
| `/ux:polish` (nombre provisional) | Interfaz | Aplica el sistema de diseño a la estructura aprobada: estados visuales, modo oscuro y accesibilidad completa. Lo que el sistema no tiene se le propone | Planeada |

`init` y `status` no son skills: los pone la plantilla del proyecto, si la tiene (`npm run init`,
`npm run status`). `sdd-plan`,
`sdd-guide` y `sdd-close` se fundieron en `design`, `work` y `verify` (2026-10-22).

## Principios

- La spec describe comportamiento, no código. El código sale de la spec, y los tests también: los
  escribe el agente, antes que el código.
- El agente pregunta; el usuario decide. Nada que el material no diga se rellena por suposición.
- Rondas cortas: cada sesión cabe en un par de horas y deja escrito dónde se quedó.
- Las reglas del proyecto (`AGENTS.md`) mandan sobre las de las skills.
- Ninguna skill nombra un producto como requisito: lo propio de un proyecto se lee en su `AGENTS.md`.

## Estructura

```text
.claude-plugin/marketplace.json             el marketplace
plugins/<plugin>/.claude-plugin/plugin.json cada plugin
plugins/<plugin>/references/                lo que comparten las skills de un plugin
plugins/<plugin>/skills/<skill>/SKILL.md    cada skill, con sus references/
```

Este repo sigue su propia norma: cada cambio va en una rama, entra por una PR y se publica con un tag
(`/git:ship`). Los plugins comparten número de versión, que vive en todos los JSON. Las versiones
están en [CHANGELOG.md](CHANGELOG.md).
