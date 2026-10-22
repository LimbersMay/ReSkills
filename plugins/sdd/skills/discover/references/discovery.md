# Formato de `docs/discovery.md`

Es el cuaderno del descubrimiento: el estado entre sesiones. Lo escribe y lo mantiene `/sdd:discover`;
el usuario lo puede leer para ver qué falta. Al cerrar el descubrimiento se queda como historia.

````markdown
# Descubrimiento

Estado: ronda 2 · 4 huecos Bloquea · 3 Propuestas sin respuesta · 1 En su slice
Material: requisitos.md (2026-10-21) · mock.html (2026-10-21)

## Mapa

| Material | Sección | Destino | Nota |
|---|---|---|---|
| requisitos.md | §1 Problema | product.md › Problema | |
| requisitos.md | §2 Fase 1, «Acción» | requirements.md (PAU) · architecture.md | El qué va a requisitos; las APIs, a arquitectura |
| mock.html | Vista En Pausa, grupo «⏳» | Fuera | P-01 |

## Ya resuelto por el sistema

| Diferencia | Se queda | Por qué |
|---|---|---|
| El mock se llama «RePause» | ReTame | Nombre de producto en ReDesign |

## Huecos

### Alcance

| ID | Hueco | Origen | Clase | Estado |
|---|---|---|---|---|
| H-01 | El mock tiene una vista de estadísticas que el documento no menciona: ¿entra en la v1? | mock › Estadísticas | Bloquea | Ronda 1 |

### Tiempo

…una tabla por categoría, en el orden de references/gaps.md; «Sin huecos: <lo que se comprobó>» si no hay…

## Propuestas

| ID | Propuesta | Desbloquea | Estado |
|---|---|---|---|
| H-07 | Una URL repetida en el baúl es una entrada por vez que se archivó | BAU-04 | ⏳ sin respuesta |

## Requisitos en espera

| Requisito (provisional) | Espera a |
|---|---|
| Restaurar un hilo completo | H-05 |

## Para sdd-design

- **domain.md:** estados «abierta → en pausa → en el baúl»; invariante candidata: ninguna pestaña se
  cierra sin quedar en el baúl (inbox §1 «no destructivo»).
- **architecture.md:** permisos tabs, tabGroups, idle, alarms, storage (inbox §6).
- **ux.md:** tres vistas (inbox §5); el mock como referencia de contenido.

## Rondas

### Ronda 1 · 2026-10-21

Preguntas: H-01, H-03, H-04 · Propuestas: H-07, H-08
Respuestas: (vacío hasta la ronda siguiente)
````

- Los IDs de hueco no se reutilizan. Un hueco resuelto se queda en su tabla con `✅ P-nn` en Estado.
- Estados de una Propuesta: `⏳ sin respuesta` (presentada en una ronda), `⏳ próxima ronda` (no cupo en
  el tope de doce), `✅ P-nn` (aceptada) y `❌ vetada → Bloquea`.
- Una Propuesta vetada pasa a Bloquea con la objeción del usuario como contexto de la pregunta.
- Las Propuestas de cierre van en la misma tabla, en un bloque «De cierre» al final, y la ronda en que
  se presentan se titula `### Cierre · <fecha>`. Mientras están abiertas, la línea de estado empieza por
  `Estado: cierre`.
- Un requisito retirado durante el descubrimiento se anota en el resumen de su ronda: `Retirados:
  PAU-07 (P-31)`.
