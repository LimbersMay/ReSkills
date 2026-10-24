# Formato de `docs/discovery.md`

Es el cuaderno del descubrimiento: el estado entre sesiones. Lo escribe y lo mantiene `/sdd:discover`;
el usuario lo puede leer para ver qué falta. Al cerrar el descubrimiento se queda como historia.

El ejemplo es de un producto inventado, Regadera: una app que avisa cuándo toca regar cada planta.

````markdown
# Descubrimiento

Estado: ronda 2 · 4 huecos Bloquea · 3 Propuestas sin respuesta · 1 En su slice
Material: requisitos.md (2026-03-02) · mock.html (2026-03-02)

## Mapa

| Material | Sección | Destino | Nota |
|---|---|---|---|
| requisitos.md | §1 Problema | product.md › Problema | |
| requisitos.md | §2 Avisos, «Notificar» | requirements.md (AVI) · architecture.md | El qué va a requisitos; cómo se programan los avisos, a arquitectura |
| mock.html | Pestaña Hoy | Para sdd-design › ux.md | Hipótesis de interfaz; la necesidad, en AVI-02 |
| mock.html | Tienda de semillas | Fuera | P-01 |

## Ya resuelto por el sistema

| Diferencia | Se queda | Por qué |
|---|---|---|
| El mock se llama «Riego» | Regadera | Nombre del producto en el sistema de diseño |

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
| H-07 | Regar una planta dos veces el mismo día cuenta como un solo riego | RIE-05 | ⏳ sin respuesta |

## Requisitos en espera

| Requisito (provisional) | Espera a |
|---|---|
| Compartir una planta con otra persona | H-05 |

## Para sdd-design

- **domain.md:** estados «al día → toca regar → atrasada»; invariante candidata: ningún riego del
  historial se borra sin que el usuario lo pida (inbox §1).
- **architecture.md:** notificaciones locales y almacenamiento en el dispositivo (inbox §6).
- **ux.md:** hipótesis de interfaz del mock (pestañas Hoy y Plantas, vista Estadísticas), cada una con
  la necesidad que cubre; el mock como referencia de contenido.

## Rondas

### Ronda 1 · 2026-03-02

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
  AVI-04 (P-12)`.
