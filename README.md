# ReSkills

Skills de Claude Code para los repos de la suite Re, en dos plugins:

- **`re-sdd`:** spec-driven development sobre la estructura de
  [ReTemplate](https://github.com/LimbersMay/ReTemplate) (`docs/inbox/`, `docs/product.md`,
  `docs/requirements.md`, `docs/specs/`…).
- **`re-git`:** la [norma de git](plugins/re-git/skills/commit/references/norma.md) de la suite,
  aplicada. Vale para productos y librerías.

## Instalar

Una vez por máquina, en Claude Code:

```text
/plugin marketplace add LimbersMay/ReSkills
/plugin install re-sdd@re-skills
/plugin install re-git@re-skills
```

Para probar cambios sin publicarlos, desde una copia local:

```text
/plugin marketplace add C:\Users\limbe\Documents\PersonalProjects\ReSkills
```

Después de cambiar una skill: `/plugin marketplace update re-skills`.

## Skills

No hace falta recordarlas. `/re-sdd:next` lee `npm run status` y ejecuta el paso que toca, y cada skill
también se dispara hablando normal: «siguiente ronda», «estoy atorado en T3», «T2 ok».

| Skill | Cuándo | Qué hace | Estado |
|---|---|---|---|
| `/re-sdd:next` | Siempre | Lee el estado del proyecto y ejecuta el paso que toca | Planeada |
| `/re-sdd:sdd-discover` | Fase 0 | Del material de `docs/inbox/` a `product.md` y `requirements.md` en EARS, con huecos MECE y rondas de preguntas | ✅ 0.2.2 |
| `/re-sdd:sdd-design` | Fase 0 | `domain.md`, `architecture.md`, `ux.md`, los spikes y `roadmap.md` (slices verticales por dependencias y riesgo) | Planeada |
| `/re-sdd:sdd-slice` | Slice | La spec y las tareas de un slice | Planeada |
| `/re-sdd:sdd-work` | Slice | Una tarea, según su «Modo» en `tasks.md`. **Del agente:** tests primero y después el código. **Tuya, sin empezar:** tests en rojo y la guía. **Tuya, en curso:** si te atoras, lee tu diff y los tests que fallan y da pistas por niveles (qué pide el test → dónde mirar → la forma en palabras → el código, solo si lo pides), y anota el atasco en «Notas de estudio» | Planeada |
| `/re-sdd:sdd-verify` | Slice | Verifica una tarea contra su spec, escribe `review.md` y, con tu OK, la commitea. Con la última tarea, cierra el slice (docs al día, roadmap) y abre su PR | Planeada |
| `/re-git:commit` | Siempre | Rama si hace falta, un commit por tarea con `[Sxx-Tn]` y su pie, y sube la rama. En un producto lo llama `sdd-verify` | ✅ 0.2.2 |
| `/re-git:ship` | Al cerrar una rama | Comprueba, CHANGELOG y versión, PR, merge commit con tu OK, tag y release. En un producto lo llama `sdd-verify` al cerrar el slice | ✅ 0.2.2 |

`init` y `status` no son skills: son `npm run init` y `npm run status`, en la plantilla. `sdd-plan`,
`sdd-guide` y `sdd-close` se fundieron en `sdd-design`, `sdd-work` y `sdd-verify` (2026-10-22).

## Principios

- La spec describe comportamiento, no código. El código sale de la spec, y los tests también: los
  escribe el agente, antes que el código.
- El agente pregunta; el usuario decide. Nada que el material no diga se rellena por suposición.
- Rondas cortas: cada sesión cabe en un par de horas y deja escrito dónde se quedó.
- Las reglas del proyecto (`AGENTS.md`) mandan sobre las de las skills.

## Estructura

```text
.claude-plugin/marketplace.json             el marketplace
plugins/<plugin>/.claude-plugin/plugin.json cada plugin
plugins/<plugin>/skills/<skill>/SKILL.md    cada skill, con sus references/
```

Este repo sigue su propia norma: cada cambio va en una rama, entra por una PR y se publica con un tag
(`/re-git:ship`). Los dos plugins comparten número de versión, que vive en los tres JSON. Las versiones
están en [CHANGELOG.md](CHANGELOG.md).
