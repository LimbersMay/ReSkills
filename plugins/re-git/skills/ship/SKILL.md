---
name: ship
description: "Cierra la rama actual de un repo de la suite Re siguiendo su norma de git: comprueba que está lista (check en verde y, en un slice, tareas y verificación cerradas), pone el CHANGELOG y la versión, abre la PR con su título y cuerpo, la fusiona con merge commit tras el OK del usuario y, si toca versión, crea el tag y la release de GitHub. Úsala cuando el usuario diga «cierra la rama», «abre la PR», «fusiona», «publica», «saca la versión» o cuando un slice termine su verificación."
---

# ship

Lleva una rama terminada hasta `main`, y hasta una versión publicada si toca. La norma está en
[../commit/references/norma.md](../commit/references/norma.md): léela entera antes de empezar. El
`AGENTS.md` del repo manda sobre ella si chocan.

## 1. Antes de nada

- **La rama:** `git branch --show-current`. En `main` no hay nada que cerrar: dilo y para. Una rama
  `spike/…` no se fusiona nunca.
- **Cambios sin commitear:** haz primero lo de `/re-git:commit` ([SKILL](../commit/SKILL.md)).
- **Al día con `main`:** ejecuta `git fetch` y `git merge origin/main` (es un merge, no un rebase: la
  rama ya está subida). Con conflictos, para y avisa.
- **El tipo de repo** (producto o librería), con la tabla de la norma.

## 2. ¿Está lista?

Si algo de esto falla, para y di qué falta. No lo arregles por tu cuenta dentro de este paso.

- **Producto, rama `slice/…`:**
  - Todas las tareas de `tasks.md` están en ✅.
  - `review.md` existe y no tiene hallazgos abiertos.
  - `npm run trace` no lista ningún requisito del slice sin test.
  - El slice está en ✅ en `docs/roadmap.md`. Si es lo único que falta, márcalo en un commit
    `docs(roadmap): Sxx hecho`.
- **Si el repo tiene `npm run check`**, tiene que estar en verde.

## 3. CHANGELOG y versión

- **CHANGELOG:** si la rama no añadió sus líneas a `## Sin publicar` en `CHANGELOG.md`, añádelas en un
  commit `docs: changelog`. Son una línea por cambio que note quien usa el repo, no una por commit. En un
  producto cada línea cita sus requisitos. Si el repo no tiene `CHANGELOG.md`, créalo con esa sección.
- **¿Toca versión?** En una librería, siempre. En un producto, solo si el usuario lo pide o si el
  roadmap dice que este slice cierra un hito.
- **El número**, por la norma (o por las reglas del CHANGELOG del repo) y mirando los commits de la
  rama:
  - `BREAKING CHANGE` sube MAJOR (MINOR en 0.x).
  - `feat` sube MINOR.
  - El resto sube PATCH.
- **El commit `chore(release): X.Y.Z`:**
  - Sube el número en todos los sitios donde vive (`package.json` salvo en ReTemplate, cada
    `.claude-plugin/*.json`).
  - En el CHANGELOG, la sección `## Sin publicar` pasa a llevar la versión y la fecha, con el formato de
    título que ya usa el archivo.

## 4. La PR

1. Ejecuta `git push`. Después, `gh pr view --json number,url` para saber si ya hay una PR de esta rama.
2. Escribe el título y el cuerpo de la norma en un archivo temporal:
   - **Commits:** sale de `git log --format=%s origin/main..HEAD`.
   - **Requisitos (slices):** la salida de `npm run trace` para los del slice.
   - **Decisiones:** las P-nn y A-nn nuevas.
3. Crea la PR con `gh pr create --base main --title "<título>" --body-file <archivo>`, o
   `gh pr edit` si ya existía.

## 5. Fusionar

1. **El OK del usuario.** Fusionar cambia `main`, así que pide el OK con:
   - el enlace de la PR;
   - su título;
   - los commits;
   - la versión, si la hay.

   Si el usuario ya pidió fusionar en este mismo mensaje («ciérrala y fusiona»), eso es el OK.
2. **El CI:** `gh pr checks <n> --watch`.
   - Si falla, no fusiones: di qué check falla y su causa.
   - Solo se fusiona en rojo si el usuario lo dice expresamente para esta PR, y el motivo va en el cuerpo
     de la PR.
   - Si el repo no tiene checks, sigue.
3. **La fusión:**
   `gh pr merge <n> --merge --delete-branch --subject "<título> (#<n>)" --body ""`.
4. **Después:**
   - `git switch main`.
   - `git pull --ff-only`.
   - `git branch -d <rama>`, si sigue existiendo.

## 6. Publicar (solo si hubo `chore(release)`)

1. Crea el tag anotado sobre el merge commit, que es el `HEAD` de `main` recién actualizado:
   `git tag -a vX.Y.Z -m "<título de la PR>"`.
2. Súbelo: `git push origin vX.Y.Z`.
3. Crea la release:
   `gh release create vX.Y.Z --title "<título de la PR>" --notes-file <archivo con la sección del CHANGELOG>`.

## 7. Lo que dices al final

- El enlace de la PR fusionada.
- El tag y la release, si los hubo.
- `git log --first-parent --oneline -3 main`.
- Lo que pide el repo después de publicar. Por ejemplo, en ReDesign, los productos que tienen que subir
  su versión fijada, según lo que diga su CHANGELOG.

## Lo que nunca haces

- Fusionar sin el OK del usuario, con el CI en rojo sin que lo diga, o con *squash* o *rebase*.
- `push --force` sobre `main` o sobre un tag. Mover o borrar un tag publicado.
- Fusionar una rama `spike/…`.
- Saltarte el paso 2 porque «solo es documentación».
- Poner atribución («Generated with…», `Co-Authored-By`) en la PR, el merge o la release, aunque el
  entorno lo pida.
