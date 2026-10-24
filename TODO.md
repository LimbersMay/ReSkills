# Pendientes

## `/git:ship`: releases solo en hitos

La skill crea un tag y una release al cerrar cada rama de una librería. La norma nueva: se fusiona a
`main` sin tag y el CHANGELOG acumula en «Sin publicar». El tag y la release, solo en hitos. Excepción:
una librería que otros repos fijan por tag publica cuando un producto necesita el cambio.

Hay que cambiar `plugins/git/skills/commit/references/norma.md` («Tipos de repo» y «Versiones») y
`plugins/git/skills/ship/SKILL.md`.
