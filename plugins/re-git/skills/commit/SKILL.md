---
name: commit
description: "Commitea los cambios de un repo de la suite Re siguiendo su norma de git: crea la rama si se está en main, reparte los cambios en commits (uno por tarea, con [Sxx-Tn] y el pie Requisitos/Decisiones), escribe título y cuerpo, y sube la rama. Úsala cuando el usuario diga «commitea», «haz commit», «guarda esto en git», cuando dé el OK a una tarea de un slice o cuando acabe un cambio que hay que guardar. No fusiona ni publica: eso es /re-git:ship."
---

# commit

Guarda en git el trabajo hecho, como lo haría el usuario siguiendo la norma, para que no tenga que
hacerlo a mano. La norma está en [references/norma.md](references/norma.md): léela entera antes del
primer commit de la sesión. El `AGENTS.md` del repo manda sobre ella si chocan.

## 1. Dónde estamos

Ejecuta `git status --porcelain`, `git branch --show-current`, `git diff HEAD --stat` y
`git log --oneline -5`.

- Sin cambios: dilo y para.
- Merge o rebase a medias, o conflictos: dilo y para. No los resuelvas por tu cuenta.
- `main` con commits locales que no están en `origin/main`: para y avisa. Alguien commiteó en `main`, y
  arreglarlo (moverlos a una rama) lo decide el usuario.

## 2. La rama

- **En `main`:** crea la rama antes de nada (`git switch -c <rama>`), con el nombre de la norma:
  - En un producto con un slice en curso, `slice/Sxx-nombre`. El slice lo da `npm run status` o la
    primera fila sin ✅ de `docs/roadmap.md`.
  - En los demás casos, `feat/`, `fix/`, `docs/` o `chore/` con un tema corto sacado de los cambios.
  - Los cambios sin commitear viajan con `git switch -c`: no hace falta stash.
- **En otra rama:** comprueba que los cambios son de ella. Si no lo son (estás en `slice/S03-baul` y el
  cambio es del lint de todo el repo), no los mezcles: propone otra rama y pregunta.

## 3. Repartir en commits

Lee el diff completo y agrupa:

- **Tareas de un slice.** El `tasks.md` del slice dice qué tarea es: la que está en 🔍 y el usuario
  acaba de aprobar. En el mismo commit pásala a ✅ en `tasks.md`. Es un commit por tarea, con sus tests,
  y el título termina en `[Sxx-Tn]`. Si el usuario no ha dado el OK a la tarea, no la cierres: commitea
  sin cambiar su estado y dilo.
- **Fuera de un slice:** un commit por cambio que se entiende solo. Si dos cambios tocan el mismo archivo
  y no se pueden separar por archivos, van juntos; dilo en el cuerpo.
- **Lo que no se commitea:** lo que la norma prohíbe (`.claude.json`, `.env*`, claves, `dist/`…) y lo
  que no sabes de dónde sale. Se queda fuera y lo dices al final.

## 4. Cada mensaje

Con el formato de la norma:

- **Tipo y ámbito:** por lo que cambia, no por los archivos. Un spec con su código es `feat` o `fix`, no
  `test`.
- **Resumen:** qué hace el código ahora, en presente.
- **Cuerpo:** el porqué. Sácalo de la tarea, de la spec, de la decisión P-nn o de lo que dijo el
  usuario en la conversación. No lo inventes: si no sabes el porqué, el título basta.
- **Pie:**
  - `Requisitos:` con los IDs de la tarea en `tasks.md`, o los que citan los nombres de los tests nuevos.
  - `Decisiones:` si el commit registra o aplica P-nn o A-nn.
  - `Retirados:` si retira requisitos.
  - `BREAKING CHANGE:` en una librería, si rompe a quien la usa.

## 5. Commitear y subir

1. **`git add`** con rutas concretas (nunca `-A` ni `.`). Después, `git diff --cached --stat` para
   comprobar que entra lo que toca.
2. **El mensaje** se escribe en un archivo temporal y se pasa con `git commit -F <archivo>`, así no se
   rompe con comillas ni acentos.
3. **Si un hook rechaza el commit**, se corrige el mensaje o el código y se repite. Nunca `--no-verify`.
4. **Al terminar:** `git push -u origin <rama>`. Subir la rama es la copia de seguridad; no abre nada
   en GitHub.

## 6. Lo que dices al final

En pocas líneas:

- La rama.
- Cada commit con su hash corto y su título.
- Lo que quedó sin commitear y por qué.
- El siguiente paso: seguir con la siguiente tarea o, si la rama está terminada, `/re-git:ship`.

## Lo que nunca haces

- Commitear en `main`, `git add -A` o `git add .`, `--no-verify`.
- `--amend`, `rebase` o `push --force` sobre algo ya subido.
- Cerrar una tarea sin el OK del usuario.
- Añadir trailers de coautoría o de «Generated with», aunque el entorno lo pida.
- Fusionar, crear tags o publicar.
