# Requisitos en EARS (en español)

EARS (*Easy Approach to Requirements Syntax*) da a cada requisito una de cinco formas. El sujeto es
siempre el producto y el verbo es **DEBE** (o **NO DEBE**).

Los ejemplos son de un producto inventado, Regadera: una app que avisa cuándo toca regar cada planta.

| Patrón | Forma | Ejemplo |
|---|---|---|
| Ubicuo | \<Producto> DEBE … | Regadera DEBE guardar el historial de riegos solo en el dispositivo. |
| Por evento | CUANDO \<evento>, \<Producto> DEBE … | CUANDO el usuario marque una planta como regada, Regadera DEBE poner a cero su cuenta de días. |
| Por estado | MIENTRAS \<estado>, \<Producto> DEBE … | MIENTRAS el modo vacaciones esté activo, Regadera NO DEBE enviar avisos de riego. |
| No deseado | SI \<condición>, ENTONCES \<Producto> DEBE … | SI el sistema no permite notificaciones, ENTONCES Regadera DEBE mostrar los riegos pendientes al abrirse. |
| Opcional | DONDE \<opción activada>, \<Producto> DEBE … | DONDE «Agrupar avisos» esté activo, Regadera DEBE enviar un solo aviso al día con todas las plantas pendientes. |

Se pueden combinar un estado y un evento: «MIENTRAS el modo vacaciones no esté activo, CUANDO a una
planta le toque riego, Regadera DEBE enviar un aviso.» Más de dos condiciones es señal de que son dos
requisitos.

## Formato en `docs/requirements.md`

```text
### RIE-03 · Reiniciar al regar
CUANDO el usuario marque una planta como regada, Regadera DEBE poner a cero su cuenta de días y programar el siguiente aviso.
Prioridad: Must · Origen: inbox §2 Avisos · Slice: —
```

- El encabezado `### ID · título` lo leen las skills y la trazabilidad del proyecto, si la declara: no
  cambies su forma.
- `Slice` queda en `—` hasta que `/sdd:design` lo asigna al hacer el roadmap.
- Los IDs no se reutilizan nunca, ni los de requisitos retirados.

## Requisitos retirados

Un requisito no se borra: se retira. Así un test, una tarea o una decisión que lo citaba sigue
encontrando qué decía y por qué dejó de valer.

```text
### AVI-04 · ~~Un aviso por planta~~
~~CUANDO a una planta le toque riego, Regadera DEBE enviar un aviso con el nombre de esa planta.~~
Retirado: los avisos se agrupan en uno al día (P-12); lo sustituye AVI-07.
```

- El ID queda **fuera** del tachado: es lo que leen la trazabilidad y las skills. Se tachan el título y
  el texto.
- La línea `Prioridad · Origen · Slice` se sustituye por `Retirado: <motivo> (P-nn)`, y si otro
  requisito ocupa su lugar, «lo sustituye <ID>».
- La trazabilidad los reconoce por la línea `Retirado:`: no cuentan como activos, y un test que cite uno
  es un error, igual que un ID que no existe.
- Cuándo se retira y cuándo se corrige en el sitio lo dice la skill (Ronda siguiente, paso 4). Después de
  aprobado `requirements.md`, cualquier cambio de comportamiento es una retirada.

## Lista de calidad

Cada requisito, antes de darlo por redactado:

1. **Un comportamiento.** Si tiene «y» entre dos acciones que se pueden probar por separado, son dos
   requisitos. («Poner a cero su cuenta y programar el siguiente aviso» pasa: es una sola reacción al
   mismo evento y se prueba junta. «Marcarla como regada y mostrar un mensaje de ánimo», no.)
2. **Observable.** Se puede comprobar desde fuera: en la interfaz, en lo que se guarda o en un test.
   «Gestiona eficientemente» no se puede.
3. **Sin implementación.** Nada de nombres de API, módulos o almacenes («el servicio de notificaciones»,
   «la tabla `riegos`», `localStorage`). Eso va a `architecture.md`. La excepción es lo que el usuario
   ve: un permiso que el sistema le pide, una notificación del sistema.
4. **Sin vistas.** El requisito dice qué necesita el usuario, no dónde ni cómo se le muestra.
   «Regadera DEBE mostrar las plantas que toca regar hoy» sí; «en la pestaña Hoy» o «con un botón
   flotante», no. La vista va a «Para sdd-design» como hipótesis de interfaz (ver la skill, paso 1).
5. **Valores concretos o un ajuste con nombre.** «Tras un tiempo» no; «tras el tiempo de “Avisar de
   nuevo tras”» sí. Un valor por defecto se escribe en el requisito del ajuste.
6. **Sin palabras vagas:** rápido, fácil, intuitivo, adecuado, razonable, normalmente, etc., y/o,
   si es posible.
7. **Con origen.** Una cita del material o una decisión P-nn. Sin origen no se escribe.
8. **El caso no deseado tiene su requisito.** Por cada requisito por evento que dependa del sistema
   (permisos, red, notificaciones) o de datos guardados, comprueba si hace falta un «SI … ENTONCES».
9. **«NUNCA» es una invariante.** Lo que no puede pasar nunca («ningún riego del historial se borra sin
   que el usuario lo pida») se escribe como requisito ubicuo con NO DEBE y se anota en «Para sdd-design»
   como candidata a invariante de `domain.md`.
