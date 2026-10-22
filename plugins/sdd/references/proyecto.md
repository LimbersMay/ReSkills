# El proyecto que espera `sdd`

Las skills de `sdd` ponen el método; el proyecto pone sus piezas. Nada de este plugin depende de un
producto, un framework o un sistema de diseño concretos: lo que cambia de un proyecto a otro lo declara
su `AGENTS.md`, y las skills lo leen ahí.

Una plantilla puede dejarlo todo listo (ReTemplate lo hace para las extensiones de la suite Re), pero no
hace falta: cualquier repo que tenga esta estructura sirve.

## Lo que tiene que existir

| Archivo | Para qué | Lo redacta |
|---|---|---|
| `AGENTS.md` | Las reglas del proyecto y sus piezas (abajo). Manda sobre las skills si chocan | El usuario |
| `docs/inbox/` | El material de partida, tal como llegó. No se edita nunca | El usuario |
| `docs/product.md` | Problema, alcance y decisiones de producto (P-nn) | `/sdd:discover` |
| `docs/requirements.md` | Cada comportamiento, en EARS y con ID | `/sdd:discover` |
| `docs/domain.md` | Glosario, estados, invariantes y entidades | `/sdd:design` |
| `docs/architecture.md` | Estructura, decisiones (A-nn) y riesgos | `/sdd:design` |
| `docs/ux.md` | Vistas, estados de pantalla y su traducción al sistema de diseño | `/sdd:design` |
| `docs/roadmap.md` | Los slices y su estado | `/sdd:design` |
| `docs/specs/Sxx-nombre/` | La spec, las tareas y la verificación de cada slice | `/sdd:slice`, `/sdd:work`, `/sdd:verify` |

Los cuatro primeros tienen que existir antes de `/sdd:discover`, aunque sea con su marcador
`<!-- sdd:pendiente -->`. Si falta alguno, la skill lo dice y para: no monta la estructura por su cuenta.
Los demás los crea la skill que los redacta, si el proyecto no los trae.

## Lo que declara el `AGENTS.md`

Cada pieza es opcional. Si el `AGENTS.md` no la nombra, la skill usa lo de la última columna y no
pregunta por ello.

| Pieza | Dónde la busca la skill | Ejemplo (ReTemplate) | Si no está |
|---|---|---|---|
| **Sistema de diseño** | Qué leer antes de tocar interfaz | ReDesign: `node_modules/re-design/AGENTS.md` y el doc del producto en `docs/products/<slug>.md` | El aspecto lo decide la fase de diseño: lo visual del material se anota como referencia, no como requisito, y la interfaz se explora sobre una base neutra |
| **Estado** | Qué leer al empezar o retomar | `npm run status`: rama, fase, slice y tareas | Se lee en `docs/`: el marcador `sdd:pendiente`, la primera fila sin ✅ de `roadmap.md` y el `tasks.md` del slice |
| **Verde** | Qué tiene que pasar antes de dar algo por terminado | `npm run check` | Se pregunta una vez y se propone añadirlo al `AGENTS.md` |
| **Trazabilidad** | Cómo se sabe qué requisito no tiene test | `npm run trace` | Se busca a mano el ID del requisito en los nombres de los tests |
| **Git** | La norma de ramas, commits y PRs | El plugin `git` | Lo que diga el `AGENTS.md`, o la costumbre del repo según `git log` |
| **Textos** | Dónde vive el texto visible | Transloco, `src/assets/i18n/` | Los textos del material se copian tal cual a `ux.md` |

La skill nombra la pieza por lo que declara el proyecto («el sistema de diseño», «el verde»), no por el
ejemplo. ReDesign, `npm run status` y el resto de la columna de ejemplo son solo eso: la forma que toman
en los proyectos de la suite Re.
