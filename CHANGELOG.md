# Changelog

## Sin publicar

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
