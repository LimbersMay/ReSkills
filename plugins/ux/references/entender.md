# Entender antes de diseñar

Qué hay que saber antes de dibujar una vista y cómo se saca de los requisitos. Sale una tabla de tareas
y una lista de preguntas para el usuario. Las referencias completas están en [fuentes.md](fuentes.md).

## Principios

### Las tareas antes que las pantallas
**Dice:** una interfaz es usable o no lo es para unos usuarios concretos, que persiguen unos objetivos
concretos en un contexto concreto. La usabilidad no es una propiedad del producto, sino un resultado de
su uso. Por eso se empieza por lo que el usuario viene a hacer, no por las pantallas que tendrá.
**Se aplica:** antes de generar variantes, existe la tabla de tareas (abajo). Ninguna vista se diseña
sin saber qué tareas sirve.
**Se mide:** a ojo: cada vista de cada variante nombra las tareas de la tabla que resuelve. Una vista
que no resuelve ninguna sobra.
**No aplica o choca con:** en un producto exploratorio, sin tareas claras, la tabla queda provisional
y se dice.
**Fuente:** ISO 9241-11:2018, 3.1.1 y sección 1 (Alcance); NN/g, *Task Analysis*.
**Confianza:** alta (norma).

### El contexto de uso
**Dice:** el contexto de uso son los usuarios, sus objetivos y tareas, los recursos y el entorno. El
entorno incluye lo técnico, lo físico, lo social, lo cultural y lo organizativo. Una misma interfaz
puede ser usable en un contexto y no en otro.
**Se aplica:** por cada grupo de usuarios, una ficha corta: quién es, qué quiere conseguir, con qué lo
hace (dispositivo, superficie, tiempo, atención) y dónde está (en movimiento, interrumpido, con otra
aplicación delante).
**Se mide:** a ojo: la ficha existe y cada variante dice para qué ficha está pensada.
**No aplica o choca con:** no hace falta un grupo por cada matiz. La norma define grupo de usuarios como
el que difiere en algo que cambia la usabilidad; si no lo cambia, es el mismo grupo.
**Fuente:** ISO 9241-11:2018, 3.1.8 y 3.1.15.
**Confianza:** alta (norma).

### Cada cuánto se abre cambia el diseño
**Dice:** la norma distingue el uso habitual, el aprendizaje y el uso infrecuente. En el uso infrecuente
el usuario tiene que ser eficaz cada vez que vuelve, sin recordar lo que aprendió. Una interfaz que se
abre dos veces al año no puede depender de atajos ni de que el usuario recuerde dónde estaba algo.
**Se aplica:** se pregunta la frecuencia (ver las preguntas). Si es baja, prima reconocer sobre
recordar ([estructura.md](estructura.md)) y las etiquetas explícitas. Si es alta, cuentan los atajos y
la densidad.
**Se mide:** la columna «Frecuencia» de la tabla de tareas.
**No aplica o choca con:** un mismo producto puede tener tareas diarias y tareas anuales. Se diseña por
tarea, no por producto.
**Fuente:** ISO 9241-11:2018, sección 1; Cooper, Reimann y Cronin (2007), sobre usuarios intermedios.
**Confianza:** alta.

### Las tareas principales
**Dice:** pocas tareas, casi siempre menos de diez y a menudo menos de cinco, acumulan la mayor parte
del interés de los usuarios. En el caso de Cisco que cita McGovern, 3 tareas de 67 se llevaron el
primer 25 % de los votos. Las tareas pequeñas, cada una inofensiva, juntas ahogan a las principales.
**Se aplica:** se marcan como principales de una a cinco tareas. La estructura se decide por ellas: van
en la vista de entrada o a un paso de ella. Las demás se acomodan sin quitarles sitio.
**Se mide:** en cada variante, cuántos pasos hay desde la entrada hasta cada tarea principal.
**No aplica o choca con:** el método original es una encuesta a usuarios reales, que la skill no puede
hacer. Las prioridades salen de los requisitos y de las respuestas del usuario, y son una hipótesis;
la skill lo dice. Choca con lo raro pero crítico (siguiente principio).
**Fuente:** McGovern (2015), *What Really Matters: Focusing on Top Tasks*, A List Apart.
**Confianza:** media (práctica muy extendida, datos de casos propios del autor).

### Frecuencia frente a importancia
**Dice:** lo probable tiene que ser fácil y lo posible, alcanzable. El análisis de tareas mira al menos
dos cosas de cada tarea: con qué frecuencia se hace y cuánto importa que salga bien.
**Se aplica:** cada tarea cae en una casilla:

| | Importa mucho | Importa poco |
|---|---|---|
| **Frecuente** | A la vista, a un paso como mucho | A mano, sin protagonismo |
| **Rara** | Fácil de encontrar y protegida contra errores ([estados.md](estados.md)) | Detrás de una revelación progresiva, o fuera |

**Se mide:** la columna «Casilla» de la tabla de tareas, contrastada con dónde vive cada tarea en cada
variante.
**No aplica o choca con:** si la frecuencia y la importancia no se conocen, no se adivinan: se
preguntan.
**Fuente:** Cooper, Reimann y Cronin (2007), «diseñar para lo probable, prever lo posible»; Hackos y Redish (1998).
**Confianza:** media.

### El modelo mental del usuario
**Dice:** el usuario se hace una idea de cómo funciona el sistema a partir de lo que ve. Si la
estructura y los nombres siguen cómo está hecho el sistema por dentro, y no cómo piensa el usuario, la
idea que se forma es errónea y se equivoca.
**Se aplica:** las vistas se agrupan y se nombran con las palabras del usuario. Esas palabras se sacan
de `product.md`, de los requisitos y de cómo habla el usuario en sus respuestas, no de los nombres de
las tablas ni de los módulos.
**Se mide:** a ojo: ningún nombre de vista ni de acción es un término interno del código.
**No aplica o choca con:** si no se sabe cómo agrupa el usuario, hace falta una ordenación de tarjetas
(*card sorting*) con personas reales. La skill no la puede simular: lo dice y sigue con una hipótesis.
**Fuente:** Norman (2013), cap. 1, modelos conceptuales; Rosenfeld, Morville y Arango (2015).
**Confianza:** media (libros de referencia, no releídos en esta investigación).

## De EARS a tareas

Cada patrón de EARS deja una pista distinta. La tabla dice qué se saca de cada uno y qué falta
preguntar.

| Patrón EARS | Forma | Qué sale | Qué falta preguntar |
|---|---|---|---|
| Por evento, iniciado por el usuario | CUANDO el usuario `<acción>`, el sistema DEBE… | Una tarea: verbo + objeto | Frecuencia, prisa, importancia |
| Por evento, iniciado por el sistema | CUANDO `<evento>`, el sistema DEBE… | Un aviso o un cambio de estado | ¿El usuario tiene que enterarse? ¿Cuándo y dónde? |
| Por estado | MIENTRAS `<estado>`, el sistema DEBE… | Un modo o un estado de una vista, que tiene que verse | ¿Cómo sabe el usuario que está en ese estado? ¿Cómo sale? |
| Comportamiento no deseado | SI `<condición>`, ENTONCES el sistema DEBE… | Un estado de error o una prevención ([estados.md](estados.md)) | ¿Qué puede hacer el usuario para arreglarlo? |
| Característica opcional | DONDE `<característica>`, el sistema DEBE… | Una opción o una variante del producto | ¿Cuántos la usan? ¿Merece sitio propio? |
| Ubicuo | El sistema DEBE… | Una restricción que afecta a todas las vistas, no una tarea | Normalmente nada |

Los requisitos dicen **qué** hace el sistema, no **cada cuánto**, **con qué prisa** ni **cuánto
importa**. Eso son las preguntas.

**Fuente:** Mavin, Wilkinson, Harwood y Novak (2009), los cinco patrones de EARS.

## Preguntas para el usuario

Se hacen cuando los requisitos y `product.md` no lo dicen. Primero las de contexto, una vez por
producto; después las de cada tarea.

**Primero abierta, después la hipótesis.** Una respuesta propuesta ancla a quien contesta: tiende a
darla por buena, y más si no es experto. Por eso las preguntas sobre hechos del contexto (frecuencia,
disparador, importancia, prisa, quién) se hacen abiertas, sin sugerir nada. Solo cuando el usuario ha
contestado, la skill enseña su hipótesis y dónde difiere. La respuesta propuesta se reserva para las
preguntas de detalle y para las decisiones de diseño, donde sí se recomienda una opción. (Fuentes:
Krosnick, 1999, sobre la aquiescencia, que es la tendencia a dar por buena la afirmación propuesta;
Tversky y Kahneman, 1974, sobre el anclaje.)

**Contexto (una vez):**
1. ¿Qué está haciendo la persona justo antes de abrir la interfaz? ¿Y qué hace justo después?
2. ¿Por qué la abre? ¿Viene a hacer algo concreto, a mirar cómo va algo o porque le ha llegado un aviso?
3. ¿Cada cuánto la abre? ¿Varias veces al día, cada semana, cada pocos meses?
4. ¿Cuánto tiempo y atención le dedica? ¿Segundos con prisa o un rato con calma?
5. ¿Dónde y con qué? Dispositivo, tamaño de la superficie, si la usa con una mano o interrumpido.
6. ¿Hay más de un tipo de usuario? ¿Qué los distingue?

**Por tarea:**
7. Si esta tarea falla o sale mal, ¿qué pasa? ¿Se puede deshacer?
8. ¿Esta tarea la hace casi todo el mundo o solo unos pocos?
9. ¿Cómo la llama el usuario, con sus palabras?
10. ¿El sistema la hace solo a veces? ¿El usuario quiere enterarse, aprobarla o solo poder revisarla?

## Plantilla de la tabla de tareas

```markdown
| # | Tarea (verbo + objeto, con las palabras del usuario) | Requisitos | Quién | Frecuencia | Importancia | Casilla | Principal | Disparador | Notas |
|---|---|---|---|---|---|---|---|---|---|
| T1 | | | | diaria · semanal · rara | alta · baja | | sí · no | el usuario · un aviso · el sistema | |
```

- **Requisitos:** los identificadores EARS de los que sale la tarea. Una tarea sin requisito es una
  suposición: se marca y se pregunta.
- **Casilla:** la de [frecuencia frente a importancia](#frecuencia-frente-a-importancia).
- **Principal:** de una a cinco tareas, nunca todas.
- **Disparador:** quién empieza la tarea. Si es el sistema, la tarea entra también en
  [estados.md](estados.md), en lo que actúa solo.

## Cuándo hace falta probar con personas

La skill trabaja sin usuarios reales. Lo dice, y propone una prueba concreta, cuando:

- Las tareas principales no salen de los requisitos y el usuario no está seguro de ellas: una encuesta
  de tareas principales (McGovern).
- No se sabe cómo agrupa ni cómo nombra las cosas el usuario: una ordenación de tarjetas.
- Las respuestas sobre el contexto son suposiciones del propio equipo, no observaciones.
