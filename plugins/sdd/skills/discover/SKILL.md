---
name: discover
description: "Fase 0 de spec-driven development: convierte el material de partida de docs/inbox/ (documento de requisitos, mocks, notas) en docs/product.md y docs/requirements.md en EARS, detectando huecos con un análisis MECE y preguntando al usuario en rondas socráticas de tres preguntas como máximo. Úsala cuando el usuario quiera arrancar un producto, descubrir o aclarar requisitos, pasar un documento o un mock a specs, seguir con el descubrimiento («siguiente ronda») o cuando el estado del proyecto diga /sdd:discover. No escribe código ni decide por el usuario."
---

# discover

Del material en bruto a un producto y unos requisitos que el usuario aprueba. Tu papel es el de un
analista que **pregunta**, no el de alguien que rellena huecos: todo lo que el material no dice lo decide
el usuario, y tú le ayudas a decidir con opciones concretas y una recomendación.

Trabaja en rondas. Una ronda cabe en una sesión corta (el usuario tiene poco tiempo entre semana): lee,
actualiza `docs/discovery.md`, redacta lo que ya se puede redactar y termina con tres preguntas como
mucho. La sesión siguiente empieza donde dejó la anterior, leyendo `docs/discovery.md`.

## Antes de empezar

1. Comprueba que el proyecto tiene la estructura de [../../references/proyecto.md](../../references/proyecto.md):
   existen `AGENTS.md`, `docs/product.md`, `docs/requirements.md` y `docs/inbox/`. Si falta alguno,
   dilo y para; no crees la estructura por tu cuenta.
2. Lee `AGENTS.md` (las reglas del proyecto mandan sobre esta skill si chocan) y apunta sus piezas,
   sobre todo el **sistema de diseño** (tabla de `proyecto.md`). Si existe `docs/discovery.md`, léelo:
   **es una ronda siguiente**, ve a [Ronda siguiente](#ronda-siguiente).
3. Lee **todo** el material de `docs/inbox/` salvo su `README.md`. Un HTML se lee como contenido: los
   textos visibles, los comentarios y los datos de ejemplo. Lo que dice de colores, tipografía o tamaño:
   - **Con sistema de diseño**, no es un requisito (el aspecto lo da el sistema); anótalo solo si
     contradice algo.
   - **Sin sistema de diseño**, va a «Para sdd-design» como referencia visual, no como requisito.
4. Lee la conversación actual: si el usuario ya decidió algo en ella («la vista X no va», «solo una
   lista»), es una decisión de producto con fecha de hoy. Se registra como P-nn igual que una respuesta.

`docs/inbox/` **no se edita nunca**.

## Primera ronda

### 1. Mapa del material

Reparte cada sección o bloque del material en su destino. Es la tabla «Mapa» de `docs/discovery.md`
(formato en [references/discovery.md](references/discovery.md)):

| Destino | Qué va |
|---|---|
| `product.md` | Problema, para quién, objetivo, alcance, restricciones |
| `requirements.md` | Comportamiento observable: qué hace el producto cuando pasa algo |
| `domain.md` | Palabras del producto, estados, lo que nunca puede pasar, qué se guarda |
| `architecture.md` | APIs, permisos, módulos, cómo se implementa algo |
| `ux.md` | Vistas, wireframes, textos de la interfaz, estados de pantalla: como hipótesis |
| Fuera | Lo que el usuario ya descartó o que el material marca como extra |

Lo que va a `domain.md`, `architecture.md` y `ux.md` **no se redacta aquí**: se anota en la sección «Para
sdd-design» de `discovery.md` con su referencia al material, y lo redacta `/sdd:design`.

Separa siempre el **qué** del **cómo**. Los ejemplos son de Regadera, un producto inventado (una app
que avisa cuándo toca regar cada planta):

- **De la implementación.** «Regadera avisa cuando toca regar una planta» es un requisito; «se programa
  una notificación local» es arquitectura. Un mismo párrafo suele tener las dos cosas.
- **De la vista.** «Regadera muestra las plantas que toca regar hoy» es un requisito; «hay una pestaña
  Hoy en la barra inferior» es una **hipótesis de interfaz**. Un mock trae muchas: van a «Para
  sdd-design › ux.md» con su sitio en el mock y la necesidad que cubren, y el requisito dice solo la
  necesidad. La estructura de vistas se decide al prototipar y probar, no en el descubrimiento.

### 2. Contradicciones

Compara el material entre sí (documento contra mock, una sección contra otra) y contra las decisiones
que ya dio el usuario. Cada contradicción es un hueco de la categoría que le toque, con las dos versiones
citadas. No elijas una versión: pregunta.

Las diferencias que ya resuelve el sistema de diseño no se preguntan; se anotan con su motivo: el
nombre o el tamaño de ventana que traiga un mock frente a los que fija el sistema para el producto, o un
estilo visual frente al del sistema. Dónde los fija lo dice el `AGENTS.md`, en la pieza «Sistema de
diseño».

### 3. Huecos (MECE)

Recorre las categorías de [references/gaps.md](references/gaps.md) **todas y en orden**, con su lista
de comprobación, para cada flujo del material. Cada hueco va a una sola categoría (la regla de desempate
está en la referencia). Una categoría sin huecos se escribe igualmente, con «sin huecos» y lo que se
comprobó: así se ve que se recorrió.

Cada hueco recibe un ID (`H-01`…), la cita o el sitio del material que lo origina y una clase:

| Clase | Qué es | Qué se hace |
|---|---|---|
| **Bloquea** | Sin la respuesta no se puede escribir un requisito Must, o el alcance cambia | Se pregunta, por orden de impacto |
| **Propuesta** | Hay una respuesta razonable que casi nadie cambiaría | Se lista con tu propuesta; el usuario la acepta o la veta **en bloque** al final de una ronda |
| **En su slice** | Afecta a un detalle que se decide mejor al llegar al slice (un texto, un valor por defecto que no cambia el diseño) | Se anota y se pasa al roadmap |

Ante la duda entre Bloquea y Propuesta, es Bloquea. Una Propuesta **no es una decisión**: hasta que el
usuario la acepta, el requisito que depende de ella no se redacta.

### 4. Borradores

Redacta en `docs/product.md` y `docs/requirements.md` **solo** lo que sale del material sin
interpretación o de una decisión P-nn ya registrada:

- `product.md`: problema, para quién, objetivo, alcance MoSCoW (con «Fuera de alcance aunque aparezca en
  el material» para lo descartado), restricciones y la tabla de decisiones.
- `requirements.md`: un requisito por comportamiento, en EARS, con las reglas de
  [references/ears.md](references/ears.md). Agrupa por área con un prefijo de tres letras
  (`RIE`, `AVI`…), y añade cada prefijo a la tabla «Áreas». `Origen` dice de dónde sale: `inbox §3`,
  `mock › Ajustes`, `P-04`.
- Un requisito que depende de un hueco abierto **no se escribe**. En `discovery.md` queda la lista de
  requisitos que esperan a cada hueco.

Deja el marcador `<!-- sdd:pendiente -->` en los dos archivos: solo se quita cuando el usuario los
aprueba.

### 5. La ronda de preguntas

Elige **hasta tres** huecos Bloquea, los de más impacto primero (los que desbloquean más requisitos o
cambian el alcance). Cada pregunta, en el chat, con esta forma:

```markdown
**H-03 · Desde cuándo se cuentan los días de riego** (Tiempo)
El material dice «cada planta tiene su frecuencia, por ejemplo cada 3 días» (inbox §2, Avisos): no dice
desde cuándo se cuentan.
- **A. Desde el último riego.** Si toca regar el lunes y se riega el martes, el siguiente aviso llega el viernes.
- **B. En días fijos.** La misma planta vuelve a avisar el jueves, aunque se regara con un día de retraso.
Recomiendo **A**: «cada 3 días» se lee como el tiempo entre dos riegos, y así un riego atrasado no
hace que la planta se riegue dos veces casi seguidas.
Cambia: RIE-02, AVI-01.
```

Reglas de las preguntas:

- Una pregunta, una decisión. Si la respuesta abre otra pregunta, va en la ronda siguiente.
- Cada opción con un **ejemplo concreto** (valores, un elemento, un caso) que muestre la diferencia. Sin
  ejemplo, la opción no se entiende.
- Siempre una recomendación con su motivo, y siempre la posibilidad de una respuesta distinta.
- No preguntes lo que el material ya responde ni lo que es de diseño visual (lo resuelve el sistema de
  diseño o, si no hay, la fase de diseño). Tampoco cómo se reparte en vistas: lo decide la fase de
  interfaz al prototipar.
- Si hay Propuestas nuevas, lístalas después de las preguntas en una tabla corta
  (`H-nn · propuesta · requisito que desbloquea`) y pide un «OK a las propuestas» o los vetos.
- **Doce Propuestas por ronda como mucho**, las que desbloquean más requisitos primero. Un «OK» en bloque
  a cuarenta filas no es una decisión: nadie las lee. Las demás esperan, con su estado «⏳ próxima
  ronda», y entran en la siguiente.

Termina la sesión con un resumen de tres líneas: qué se redactó, cuántos huecos quedan por clase y qué
viene después.

## Ronda siguiente

1. Lee `docs/discovery.md` y las respuestas del usuario (en su mensaje o en la conversación).
2. Registra cada respuesta como **P-nn** en la tabla «Decisiones de producto» de `product.md`: pregunta,
   respuesta en sus palabras (resumida si hace falta, sin cambiarle el sentido), fecha y los requisitos
   que afecta. Las Propuestas aceptadas en bloque se registran una por una, con «Propuesta aceptada» en
   la respuesta. Si una respuesta no es clara, **no la interpretes**: repregunta en esta ronda.
3. Marca el hueco como resuelto en `discovery.md` con su P-nn.
4. Si una respuesta toca algo ya redactado, decide entre corregir y retirar:
   - **Se corrige en el sitio** si el comportamiento sigue siendo el mismo y solo se precisa: un valor,
     una palabra, una condición que faltaba. `Origen` suma la P-nn.
   - **Se retira** si el comportamiento cambia o desaparece: el requisito se queda con su ID, el título y
     el texto tachados y una línea `Retirado: <motivo> (P-nn)`; si hay un comportamiento nuevo, va con un
     ID nuevo.
     El formato está en [references/ears.md](references/ears.md#requisitos-retirados).

   Las dos cosas se dicen en el resumen, con los IDs.
5. Si llegó material nuevo a `docs/inbox/`, pásale los pasos 1 a 3 solo a lo nuevo.
6. Redacta los requisitos que se han desbloqueado y vuelve a [La ronda de preguntas](#5-la-ronda-de-preguntas).

## Cuándo termina

El descubrimiento termina cuando no quedan huecos Bloquea, todas las Propuestas tienen respuesta y cada
Must del alcance tiene sus requisitos. Entonces:

1. **Revisión de calidad.** Pasa `requirements.md` entero por la lista de calidad de
   [references/ears.md](references/ears.md#lista-de-calidad). Lo que falla se reparte en dos:
   - **Se corrige sin preguntar** lo que no cambia el comportamiento: una palabra vaga, dos acciones en un
     requisito que se parten en dos, un origen que faltaba.
   - **Propuestas de cierre** para lo que sí lo cambia: casi siempre un «SI … ENTONCES» que falta (punto
     8) o un valor sin decidir (punto 5). Cada una es un hueco nuevo (`H-nn`, clase Propuesta) con su
     redacción propuesta.
2. **Ronda de cierre.** Si hay Propuestas de cierre, preséntalas como una ronda más (sin preguntas
   nuevas, con el mismo tope de doce) y registra las respuestas como en la ronda siguiente. Una
   Propuesta de cierre vetada vuelve a ser un hueco Bloquea: el descubrimiento sigue.
3. **Aprobación.** Con todo respondido, `discovery.md` dice «Estado: cierre» y pides al usuario que
   apruebe `product.md` y `requirements.md`. Con su OK explícito, quita el marcador
   `<!-- sdd:pendiente -->` de los dos y escribe «Cerrado» con la fecha al principio de `discovery.md`.
4. Siguiente paso: `/sdd:design` (dominio, arquitectura, interfaz y spikes).

## Lo que nunca haces

- Decidir por el usuario: ni elegir entre dos versiones del material, ni rellenar un valor que falta,
  ni dar por aceptada una Propuesta.
- Escribir código, crear slices o tocar `docs/domain.md`, `docs/architecture.md`, `docs/ux.md` o
  `docs/roadmap.md` (son de `/sdd:design`).
- Editar `docs/inbox/`.
- Más de tres preguntas o más de doce Propuestas por ronda.
- Borrar un requisito o reutilizar su ID: se retira.
- Pedir la aprobación con Propuestas de cierre sin respuesta.
