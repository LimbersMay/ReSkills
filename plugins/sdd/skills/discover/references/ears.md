# Requisitos en EARS (en español)

EARS (*Easy Approach to Requirements Syntax*) da a cada requisito una de cinco formas. El sujeto es
siempre el producto y el verbo es **DEBE** (o **NO DEBE**).

| Patrón | Forma | Ejemplo |
|---|---|---|
| Ubicuo | \<Producto> DEBE … | ReTame DEBE guardar el baúl solo en el equipo. |
| Por evento | CUANDO \<evento>, \<Producto> DEBE … | CUANDO el usuario enfoque una pestaña en pausa, ReTame DEBE sacarla del grupo de pausa. |
| Por estado | MIENTRAS \<estado>, \<Producto> DEBE … | MIENTRAS el equipo esté bloqueado, ReTame NO DEBE sumar inactividad a ninguna pestaña. |
| No deseado | SI \<condición>, ENTONCES \<Producto> DEBE … | SI Chrome no permite descartar una pestaña, ENTONCES ReTame DEBE dejarla en pausa sin descartar. |
| Opcional | DONDE \<opción activada>, \<Producto> DEBE … | DONDE «Ignorar pestañas con audio» esté activo, ReTame NO DEBE pausar una pestaña que reproduce audio. |

Se pueden combinar un estado y un evento: «MIENTRAS el umbral de pestañas no se supere, CUANDO una
pestaña cumpla T1, ReTame NO DEBE pausarla.» Más de dos condiciones es señal de que son dos requisitos.

## Formato en `docs/requirements.md`

```text
### PAU-03 · Despertar al enfocar
CUANDO el usuario enfoque una pestaña en pausa, ReTame DEBE sacarla del grupo de pausa y poner su inactividad a cero.
Prioridad: Must · Origen: inbox §2 Fase 1 · Slice: —
```

- El encabezado `### ID · título` lo leen `npm run trace` y las skills: no cambies su forma.
- `Slice` queda en `—` hasta que `/sdd:design` lo asigna al hacer el roadmap.
- Los IDs no se reutilizan nunca, ni los de requisitos retirados.

## Requisitos retirados

Un requisito no se borra: se retira. Así un test, una tarea o una decisión que lo citaba sigue
encontrando qué decía y por qué dejó de valer.

```text
### PAU-07 · ~~Vista En Pausa~~
~~ReTame DEBE mostrar en la vista En Pausa las pestañas del grupo de pausa de la ventana actual, con su título y su URL.~~
Retirado: la vista muestra todas las ventanas (P-36); lo sustituye PAU-19.
```

- El ID queda **fuera** del tachado: es lo que leen `trace` y las skills. Se tachan el título y el texto.
- La línea `Prioridad · Origen · Slice` se sustituye por `Retirado: <motivo> (P-nn)`, y si otro
  requisito ocupa su lugar, «lo sustituye <ID>».
- `npm run trace` los reconoce por la línea `Retirado:`: no cuentan como activos y un test que cite uno
  sale como error, igual que un ID que no existe.
- Cuándo se retira y cuándo se corrige en el sitio lo dice la skill (Ronda siguiente, paso 4). Después de
  aprobado `requirements.md`, cualquier cambio de comportamiento es una retirada.

## Lista de calidad

Cada requisito, antes de darlo por redactado:

1. **Un comportamiento.** Si tiene «y» entre dos acciones que se pueden probar por separado, son dos
   requisitos. («Sacarla del grupo y poner su inactividad a cero» pasa: es una sola reacción al mismo
   evento y se prueba junta. «Pausarla y mostrar un aviso», no.)
2. **Observable.** Se puede comprobar desde fuera: en el navegador, en la interfaz o en un test del
   engine. «Gestiona eficientemente» no se puede.
3. **Sin implementación.** Nada de nombres de API, módulos o almacenes (`chrome.tabs.discard`,
   `storage.local`, «el Service Worker»). Eso va a `architecture.md`. La excepción es lo que el usuario
   ve: un permiso que Chrome le pide, un grupo de pestañas nativo.
4. **Valores concretos o un ajuste con nombre.** «Tras un tiempo» no; «tras el tiempo de “Pausar
   pestaña tras”» sí. Un valor por defecto se escribe en el requisito del ajuste.
5. **Sin palabras vagas:** rápido, fácil, intuitivo, adecuado, razonable, normalmente, etc., y/o,
   si es posible.
6. **Con origen.** Una cita del material o una decisión P-nn. Sin origen no se escribe.
7. **El caso no deseado tiene su requisito.** Por cada requisito por evento que dependa de Chrome o de
   datos guardados, comprueba si hace falta un «SI … ENTONCES».
8. **«NUNCA» es una invariante.** Lo que no puede pasar nunca («ninguna pestaña se cierra sin quedar en
   el baúl») se escribe como requisito ubicuo con NO DEBE y se anota en «Para sdd-design» como candidata a
   invariante de `domain.md`.
