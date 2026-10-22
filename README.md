# ReSkills

Skills de Claude Code para hacer spec-driven development en los productos de la suite Re. Funcionan
sobre la estructura de [ReTemplate](https://github.com/LimbersMay/ReTemplate): `docs/inbox/`,
`docs/product.md`, `docs/requirements.md`, `docs/specs/`…

## Instalar

Una vez por máquina, en Claude Code:

```text
/plugin marketplace add LimbersMay/ReSkills
/plugin install re-sdd@re-skills
```

Para probar cambios sin publicarlos, desde una copia local:

```text
/plugin marketplace add C:\Users\limbe\Documents\PersonalProjects\ReSkills
```

Después de cambiar una skill: `/plugin marketplace update re-skills`.

## Skills

| Skill | Fase | Qué hace | Estado |
|---|---|---|---|
| `/re-sdd:sdd-discover` | 0 | Del material de `docs/inbox/` a `product.md` y `requirements.md` en EARS, con huecos MECE y rondas de preguntas | ✅ 0.1 |
| `/re-sdd:sdd-design` | 0 | `domain.md`, `architecture.md`, `ux.md` y los spikes | Planeada |
| `/re-sdd:sdd-plan` | 0 | `roadmap.md`: slices verticales por dependencias y riesgo | Planeada |
| `/re-sdd:sdd-slice` | 1 | La spec y las tareas de un slice | Planeada |
| `/re-sdd:sdd-verify` | 1 | Verifica una tarea contra su spec y escribe `review.md` | Planeada |
| `/re-sdd:sdd-guide` | 1 | La guía de una tarea que programa el usuario | Planeada |

## Principios

- La spec describe comportamiento, no código. El código sale de la spec, y los tests también: los
  escribe el agente, antes que el código.
- El agente pregunta; el usuario decide. Nada que el material no diga se rellena por suposición.
- Rondas cortas: cada sesión cabe en un par de horas y deja escrito dónde se quedó.
- Las reglas del proyecto (`AGENTS.md`) mandan sobre las de las skills.

## Estructura

```text
.claude-plugin/marketplace.json   el marketplace (un solo plugin)
plugin/.claude-plugin/plugin.json el plugin
plugin/skills/<skill>/SKILL.md    cada skill, con sus references/
```

Versiones en [CHANGELOG.md](CHANGELOG.md). Al publicar, sube la versión en los dos JSON.
