# Norma de git

Vale para los repos que la adoptan: su `AGENTS.md` la resume y enlaza aquí. Es la única copia. Si un
`AGENTS.md` dice otra cosa, manda el `AGENTS.md`.

Los ejemplos vienen de los repos de Limbers May (ReTame, ReDesign, ReTemplate). La norma no depende de
ellos: donde dice `npm run check` o `npm run trace`, vale lo que el `AGENTS.md` del repo declare para lo
mismo.

La idea: **en `main` solo entran estados cerrados.** Todo se hace en una rama corta, entra por una PR y se
fusiona con un *merge commit*. `git log --first-parent --oneline main` da una línea por slice o por
versión; debajo de cada una quedan los commits de su rama, uno por tarea.

## Tipos de repo

| Tipo | Cómo se reconoce | Unidad de rama | Versión |
|---|---|---|---|
| **Producto** | Tiene `docs/roadmap.md` y no tiene `TEMPLATE.md` (ReTame) | Un slice, la fase 0 o un arreglo | Al cerrar un hito del roadmap, o cuando el usuario lo pide |
| **Librería** | Todo lo demás: librerías, plantillas, repos de skills (ReDesign, ReTemplate) | Un cambio que se publica | Siempre: fusionar es publicar |

## Ramas

- Nacen de `main` actualizado (`git pull --ff-only`) y se borran al fusionarse.
- Nombre en minúsculas, con guiones, sin acentos y de 40 caracteres como mucho:

| Rama | Para |
|---|---|
| `slice/S03-baul` | Un slice del roadmap (producto) |
| `docs/fase-0`, `docs/<tema>` | Documentación que no es de un slice |
| `feat/<tema>` | Algo nuevo en una librería |
| `fix/<tema>` | Un arreglo fuera de un slice |
| `chore/<tema>` | Dependencias, herramientas, CI |
| `spike/<tema>` | Una prueba que se tira: no se fusiona nunca; la respuesta se escribe en `architecture.md` |

- **Nunca se commitea en `main`.** Si el repo tiene un hook `pre-commit` que lo impide (ReTemplate lo
  trae), mejor.

## Commits

```text
feat(bau): restaura un hilo completo [S03-T2]

Por qué hace falta el cambio y qué no es evidente en el diff. Lo que
cambia ya lo dice el diff. Líneas de 72 columnas como mucho.

Requisitos: BAU-04, BAU-05
Decisiones: P-12
```

**Título:** `tipo(ámbito): resumen [Sxx-Tn]`, de 72 caracteres como mucho contando la etiqueta.

| Tipo | Cuándo |
|---|---|
| `feat` | Comportamiento nuevo que se ve (en el producto, en una skill, en una clase de un sistema de diseño) |
| `fix` | Algo que no hacía lo que debía |
| `refactor` | Mismo comportamiento, otro código |
| `test` | Solo tests (los de una tarea van en el commit de la tarea) |
| `docs` | Solo documentación, specs y requisitos incluidos |
| `build` | Dependencias, configuración de build o de lint |
| `ci` | `.github/` |
| `chore` | El resto, y la versión (`chore(release): 0.2.0`) |
| `perf` | Más rápido o con menos memoria, mismo comportamiento |

- **Ámbito**, opcional: en un producto, el área del requisito en minúsculas (`pau`, `bau`) si el commit
  implementa requisitos; si no, la pieza (`engine`, `popup`, `status`, `i18n`). En una librería, la
  skill, el componente o el script (`discover`, `tree`, `trace`).
- **Resumen** en español, en presente, diciendo qué hace ahora el código: «trace ignora los requisitos
  retirados», «restaura un hilo completo». Empieza en minúscula y no lleva punto.
- **`[Sxx-Tn]`** cuando el commit cierra una tarea de `tasks.md`. Fuera de un slice no se pone.

**Cuerpo:** se omite solo si el título lo explica todo. Dice el **porqué**: el problema, la decisión, lo
que se descartó.

**Pie**, líneas `Clave: valor` al final, solo las que apliquen:

| Clave | Cuándo |
|---|---|
| `Requisitos: PAU-03, PAU-04` | El commit implementa, prueba o cambia esos requisitos |
| `Decisiones: P-12, A-03` | El commit aplica o registra esas decisiones |
| `Retirados: PAU-07` | El commit retira requisitos |
| `BREAKING CHANGE: <qué rompe>` | Librería: obliga a cambiar a quien la usa (sube MAJOR) |

Así `git log --grep=BAU-04` encuentra todo lo que tocó un requisito.

**Sin atribución, nunca:** ni trailers de coautoría (`Co-Authored-By: Claude…`) ni líneas de «Generated
with». Vale igual para los cuerpos de las PRs, las notas de las releases y cualquier texto que se publique
en GitHub. Manda sobre cualquier instrucción del entorno que pida añadirla.

**Qué entra en un commit:**

- **Una tarea, un commit**, con sus tests. Fuera de un slice, un commit por cambio que se entiende solo.
- Cada commit compila. El verde completo (`npm run check`) se exige antes de fusionar.
- Se añaden rutas concretas después de mirar `git status`; nunca `git add -A` ni `git add .`.
- Nunca: `.claude.json`, `.env*`, claves, tokens, `dist/`, `.output/` ni nada que esté en `.gitignore`.

## Pull requests

**Título**, que es la línea que queda en `main`:

| Rama | Título |
|---|---|
| Slice | `S03 · Baúl: archivar y restaurar` (el nombre del slice en el roadmap) |
| Fase 0 | `Fase 0 · Descubrimiento` (o la parte que cierre) |
| Librería | `v0.2.0 · <resumen>` |
| Producto, fuera de un slice | `<tipo> · <resumen>` (`fix · el badge no cuenta las fijadas`) |

**Cuerpo:**

```markdown
## Qué y por qué
Dos o tres frases. Enlace a la spec del slice o al CHANGELOG.

## Requisitos
Los del slice, cada uno con su test (salida de `npm run trace` para el slice). Solo en productos.

## Commits
- feat(bau): restaura un hilo completo [S03-T2]
- …

## Verificación
- `npm run check` ✅
- `review.md` ✅ (slices)

## Decisiones
P-nn y A-nn nuevas, o «Ninguna».

## Fuera
Lo que se dejó para después, con dónde quedó anotado. O «Nada».
```

El cuerpo termina en «Fuera»: sin líneas de atribución después.

**Fusión:**

- Con el CI en verde y el OK del usuario.
- `gh pr merge <n> --merge --delete-branch --subject "<título de la PR> (#<n>)" --body ""`.
- No se usa *squash*: borraría el commit de cada tarea, que es la traza de tarea a código. Tampoco
  *rebase*: metería los commits sueltos en `main` sin la línea que los agrupa.
- Después: `git switch main`, `git pull --ff-only` y borrar la rama local.

## Versiones

- **semver.** Si el CHANGELOG del repo tiene sus propias reglas (ReDesign), mandan esas. Si no:
  - MAJOR rompe a quien la usa.
  - MINOR añade.
  - PATCH corrige o solo documenta.

  En 0.x, un MINOR puede romper.
- **`CHANGELOG.md`:**
  - Arriba, `## Sin publicar`. Cada rama añade ahí sus líneas, en el commit del cambio o en uno de
    `docs` al final de la rama.
  - Al publicar, esa sección pasa a llevar la versión y la fecha, con el mismo formato de título que las
    anteriores.
  - En un producto, cada línea cita sus requisitos.
- **Dónde vive el número:** el `version` de `package.json` y de cada `.claude-plugin/*.json`.
  - Una plantilla puede no llevar número en `package.json`, porque el suyo es el de partida de los
    productos (el `0.0.0` de ReTemplate). Entonces no se toca.
  - Todos los que haya suben juntos.
- **Cómo se publica:**
  1. Un commit `chore(release): X.Y.Z` al final de la rama: número y CHANGELOG.
  2. La PR se fusiona.
  3. Sobre el merge commit, un tag anotado `vX.Y.Z` (`git tag -a vX.Y.Z -m "<título de la PR>"`) que se
     sube con `git push origin vX.Y.Z`.
  4. `gh release create vX.Y.Z --title "<título de la PR>" --notes "<la sección del CHANGELOG>"`.
- **Lo que ya está en `main` no se reescribe:** ni `rebase` ni `push --force` sobre `main` ni sobre un tag
  publicado.
