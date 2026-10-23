# Estados, errores, automatismos y textos

Una vista no es una sola pantalla: es la misma vista vacía, cargando, con un error o a medias. Aquí está
qué estados hay que diseñar, cómo se tratan los errores y lo que el producto hace solo, y cómo se
escriben los textos. Las referencias completas están en [fuentes.md](fuentes.md).

## Los estados de cada vista

Cada variante enseña, por cada vista principal, todos los estados que le tocan. Un estado que no se
dibuja lo acaba diseñando el código, por accidente.

| Estado | Cuándo aparece | Qué tiene que hacer | Ver |
|---|---|---|---|
| Primer uso | Aún no hay nada, porque el usuario acaba de empezar | Decir qué irá aquí y dar el primer paso | [El vacío que enseña](#el-vacío-que-enseña) |
| Sin resultados | Un filtro o una búsqueda no devuelve nada | Decir qué se buscó y cómo ampliarlo | [El vacío que enseña](#el-vacío-que-enseña) |
| Todo hecho | El usuario vació la lista a propósito | Confirmar que está al día; no parecer un fallo | [El vacío que enseña](#el-vacío-que-enseña) |
| Cargando | La respuesta tarda | Indicar que se trabaja, según cuánto tarde | [Tiempos de respuesta](#tiempos-de-respuesta) |
| Parcial | Llegó una parte de los datos, o falló una parte | Enseñar lo que hay y marcar lo que falta | [Mensajes de error](#mensajes-de-error) |
| Error | La acción o la carga falló | Decir qué pasó y cómo seguir, sin perder lo escrito | [Mensajes de error](#mensajes-de-error) |
| Desactivado | Una acción existe pero ahora no se puede hacer | Decir por qué y qué falta | [Desactivado, con el motivo](#desactivado-con-el-motivo) |
| Hecho solo | El sistema actuó sin que el usuario lo pidiera | Avisar, explicar y dejar deshacer | [Lo que el producto hace solo](#lo-que-el-producto-hace-solo) |
| Extremo | Textos muy largos, cientos de elementos, uno solo, valores fuera de lo normal | No romper la disposición: cortar, envolver o paginar a propósito | [jerarquia.md](jerarquia.md) |

**Se mide:** con Playwright, cada estado se provoca y se captura: datos vacíos por fixture, retrasos y
fallos con `page.route`, permisos o condiciones que desactivan acciones. El extremo, con fixtures de
nombres de 80 caracteres sin espacios, listas de cientos de elementos, un solo elemento y cifras de
muchos dígitos; se comprueba que ningún elemento se desborda de su caja (`scrollWidth >
clientWidth`) ni se superpone a otro. Es el estado que más rompe una disposición y el que menos se
dibuja. Una variante a la que le falta
la captura de un estado está incompleta.

## Principios

### Visibilidad del estado del sistema
**Dice:** el sistema tiene que decir siempre qué está pasando, con una respuesta adecuada y a tiempo.
Cada acción del usuario produce un cambio visible.
**Se aplica:** al pulsar, algo cambia enseguida: el control, la fila o un aviso. Si hay un modo activo
(selección, edición, filtro), se ve sin tener que buscarlo.
**Se mide:** con Playwright: tras cada acción, comprobar que el DOM cambia de forma visible en menos de
0,1 s. Para cada modo, que existe un indicador en la vista.
**No aplica o choca con:** avisar de todo genera ruido; lo que el usuario no necesita saber no se avisa.
**Fuente:** Nielsen (1994), heurística 1.
**Confianza:** media (consenso de práctica).

### Tiempos de respuesta
**Dice:** hay tres límites. Hasta 0,1 s se siente instantáneo y basta con mostrar el resultado. Hasta 1 s
no se rompe el hilo, aunque se nota el retraso. A partir de 10 s el usuario pierde la atención. Entre
2 y 10 s basta un indicador discreto. Por encima de 10 s hace falta progreso con porcentaje o tiempo
restante, y una forma de cancelar. Para el tramo de 1 a 2 s la fuente no da pauta.
**Se aplica:** cada operación de la vista se clasifica por lo que tarda y lleva el indicador que le
toca. Por debajo de 1 s no se pone un indicador: parpadearía. Entre 1 y 2 s, como regla práctica sin
fuente, el control pulsado cambia a un estado de ocupado, sin indicador aparte.
**Se mide:** con Playwright, retrasando la respuesta con `page.route`: a 3 s hay un indicador; a 12 s,
progreso y un botón de cancelar; a 0,3 s no parpadea nada.
**No aplica o choca con:** las cifras son órdenes de magnitud, no umbrales exactos.
**Fuente:** Nielsen (1993, actualizado en 2014), *Response Times: The 3 Important Limits*; Miller
(1968); Card, Robertson y Mackinlay (1991).
**Confianza:** media.

### Deshacer mejor que confirmar
**Dice:** pedir confirmación solo protege si el usuario lee el aviso, y deja de leerlo cuando lo ve a
menudo. La habituación se ve incluso en el cerebro: en el estudio de Anderson et al., la respuesta
visual a un aviso de seguridad caía mucho desde la segunda exposición. Deshacer protege sin
interrumpir.
**Se aplica:** las acciones que se pueden revertir se hacen ya y se ofrecen para deshacer. La
confirmación se reserva para lo grave o lo irreversible, y entonces nombra el elemento y la
consecuencia. Sus botones dicen lo que pasa («Borrar 3 notas», «Seguir editando»), no «Sí» o «Aceptar»,
y la opción destructiva no viene marcada por defecto.
**Se mide:** con Playwright: por cada acción destructiva, o hay deshacer tras hacerla, o hay un diálogo
que contiene el nombre del elemento y cuyos botones no son genéricos. El foco inicial del diálogo no
está en la opción destructiva.
**No aplica o choca con:** con lo que no se puede deshacer de verdad (un envío, un pago, algo que
afecta a otros). Ahí se confirma, y vale variar el aviso para que no se vuelva invisible.
**Fuente:** Nielsen (2018), *Confirmation Dialogs Can Prevent User Errors (If Not Overused)*; Anderson
et al. (2015); Vance et al. (2018).
**Confianza:** alta (habituación); media (las pautas de diseño).

### Prevenir antes que avisar
**Dice:** es mejor un diseño que impide el error que un buen mensaje de error. Hay dos tipos de error:
el desliz, cuando el usuario quería hacer lo correcto y se le fue la mano, y la equivocación, cuando su
idea de lo que tenía que hacer era errónea. El desliz se previene con restricciones y separación; la
equivocación, con un modelo mental claro.
**Se aplica:** se restringe la entrada a lo válido (selectores en vez de texto libre si el conjunto es
cerrado), se ponen valores por defecto sensatos y se separan las acciones destructivas de las
frecuentes. La validación en línea avisa cuando el usuario termina el campo, no mientras escribe.
**Se mide:** con Playwright: en cada formulario, intentar enviar valores inválidos y comprobar dónde y
cuándo aparece el aviso. A ojo: ninguna acción destructiva está pegada a una frecuente.
**No aplica o choca con:** restringir de más impide casos legítimos. Si no se sabe qué es válido, se
pregunta.
**Fuente:** Nielsen (1994), heurística 5; Norman (2013), cap. 5.
**Confianza:** media (consenso de práctica; el libro de Norman no se releyó en esta investigación).

### El vacío que enseña
**Dice:** una vista vacía es un estado con trabajo que hacer: decir en qué estado está el sistema,
enseñar para qué sirve la vista y dar un camino directo al primer paso. Dejarla en blanco, o poner
«Sin registros» mientras aún carga, confunde.
**Se aplica:** el vacío de primer uso dice qué aparecerá aquí y tiene el botón de la primera acción. El
vacío por un filtro dice qué se filtró y cómo quitarlo. Mientras carga, no se muestra el mensaje de
vacío.
**Se mide:** con Playwright, con datos vacíos: la vista tiene texto que explica y al menos un control
que lleva a la tarea. Con la carga retrasada: el mensaje de vacío no aparece antes de que lleguen los
datos.
**No aplica o choca con:** con el primer uso: el vacío no es sitio para un tutorial largo.
**Fuente:** Kaplan (2021), *Designing Empty States in Complex Applications*.
**Confianza:** media.

### El primer uso, sin tutorial
**Dice:** el usuario quiere hacer, no aprender: se salta las instrucciones y empieza a usar. En un
estudio con 70 usuarios de aplicaciones móviles, los tutoriales del principio no mejoraron ni el éxito
(91 % frente a 94 %) ni el tiempo, y quienes los vieron percibieron las tareas como más difíciles.
**Se aplica:** la ayuda va en contexto, junto a la función y cuando hace falta. Si algo necesita
explicarse antes de usarlo, se mira primero si se puede simplificar.
**Se mide:** a ojo: ninguna variante abre con una secuencia de pantallas explicativas. Las pistas, si
las hay, están junto a lo que explican y se pueden cerrar.
**No aplica o choca con:** con gestos o funciones que no se pueden descubrir mirando; ahí una pista
breve en el momento de usarla.
**Fuente:** Kendrick (2020), *Mobile Tutorials: Wasted Effort or Efficiency Boost?*; Carroll y Rosson
(1987), la paradoja del usuario activo.
**Confianza:** media (un estudio, en móvil, con aplicaciones concretas).

### Desactivado, con el motivo
**Dice:** un control desactivado sin explicación deja al usuario adivinando qué le falta. Mostrar el
control enseña que la función existe; ocultarlo tiene sentido cuando no aplica nunca a ese usuario.
**Se aplica:** se desactiva lo que existe pero aún no se puede hacer, y se dice por qué cerca del
control o al tocarlo. Se oculta lo que no aplica a ese usuario o a esa situación. Una alternativa es
dejar el control activo y explicar al pulsarlo qué falta.
**Se mide:** con Playwright: por cada control desactivado, hay texto visible o accesible que explica el
motivo. Que siga siendo alcanzable con el teclado lo trata [accesibilidad.md](accesibilidad.md).
**No aplica o choca con:** con la semejanza: un control desactivado tiene que distinguirse de uno
activo, y el contraste bajo choca con la legibilidad.
**Fuente:** Nielsen (2025), *Inactive GUI Controls: Show, Disable, or Hide?*, UX Tigers.
**Confianza:** baja (opinión experta).

## Lo que el producto hace solo

Cuando el sistema actúa sin que el usuario lo pida (ordenar, archivar, sugerir, rellenar, avisar), el
riesgo no es solo el error. Es que el usuario se fíe de más y deje de revisar, o se fíe de menos y deje
de usarlo. Y es que no se entere de que el sistema cambió algo. Los cuatro principios siguientes lo
tratan.

### Que se sepa qué hace y qué tan bien lo hace
**Dice:** la confianza adecuada es la calibrada: ni más ni menos de lo que el sistema merece. Se apoya
en tres cosas: lo bien que funciona, cómo funciona y para qué existe. Si el usuario no ve ninguna de las
tres, se fía de más o de menos.
**Se aplica:** la vista dice qué hace el automatismo y, si se equivoca a veces, cuánto o cuándo. Cada
acción automática deja un rastro: qué hizo, cuándo y por qué.
**Se mide:** a ojo, por cada tarea con disparador «el sistema» en la tabla de tareas: ¿la vista enseña
qué hizo y por qué? Con Playwright: provocar el automatismo y comprobar que aparece el rastro.
**No aplica o choca con:** explicar cada acción satura; se explica lo que cambia algo para el usuario.
**Fuente:** Lee y See (2004); Parasuraman y Riley (1997); Amershi et al. (2019), G1, G2 y G11.
**Confianza:** media. Lee y See revisan la evidencia empírica, pero el original no se pudo leer: la
definición de confianza calibrada y sus tres bases están comprobadas en fuentes que lo citan. Sube a
alta si se comprueba en el original.

### Fácil de pedir, de descartar y de corregir
**Dice:** el coste de que el sistema se equivoque tiene que ser bajo. El usuario lo invoca y lo
descarta con un gesto, y corrige el resultado sin rehacerlo todo.
**Se aplica:** cada acción automática se deshace en un paso. Cada sugerencia se ignora sin hacer nada.
Hay un control global para apagar el automatismo.
**Se mide:** con Playwright: tras cada acción automática, existe deshacer; cada sugerencia desaparece
sin aceptarla; existe un ajuste para desactivarlo.
**No aplica o choca con:** con lo que no puede deshacerse; entonces el sistema propone y el usuario
decide.
**Fuente:** Horvitz (1999), factores 6 y 7; Amershi et al. (2019), G7, G8, G9 y G17.
**Confianza:** media.

### Hacer menos cuando hay duda
**Dice:** si el sistema no está seguro de lo que el usuario quiere, es mejor hacer menos y acertar que
hacer más y fallar: preguntar, sugerir en lugar de actuar, o actuar sobre una parte.
**Se aplica:** por cada automatismo se decide si actúa, sugiere o pregunta, según lo seguro que esté y
lo que cuesta equivocarse. Lo caro de deshacer se sugiere; no se hace.
**Se mide:** a ojo: la tabla de tareas dice, por cada tarea que dispara el sistema, si actúa, sugiere o
pregunta, y por qué.
**No aplica o choca con:** preguntar de más es una interrupción; ver [Deshacer mejor que
confirmar](#deshacer-mejor-que-confirmar).
**Fuente:** Horvitz (1999), factores 5 y 8; Amershi et al. (2019), G10.
**Confianza:** media.

### Avisar de los cambios y de los modos
**Dice:** en automatización se llaman *sorpresas* a los casos en que el sistema hace algo que el usuario
no esperaba, casi siempre porque no sabía en qué modo estaba. Cuando el sistema cambia su forma de
actuar, o cambia algo que el usuario ya conocía, tiene que decirlo.
**Se aplica:** el modo del automatismo (activo, en pausa, solo sugerir) se ve en la vista donde actúa.
Los cambios de comportamiento se avisan una vez, donde ocurren.
**Se mide:** con Playwright: cambiar el modo y comprobar que la vista lo refleja sin abrir los ajustes.
**No aplica o choca con:** con el ruido; un aviso por cambio, no uno por acción.
**Fuente:** Sarter, Woods y Billings (1997); Amershi et al. (2019), G14 y G18.
**Confianza:** media.

## Textos

### Con las palabras del usuario
**Dice:** el sistema habla el idioma del usuario, con palabras y conceptos que conoce, no con términos
internos. Ver [El modelo mental del usuario](entender.md#el-modelo-mental-del-usuario).
**Se aplica:** los nombres de vistas, acciones y estados salen de la columna «Tarea» de la tabla de
tareas.
**Se mide:** con Playwright: extraer todos los textos visibles y compararlos con un glosario de
términos internos (nombres de tablas, de módulos, códigos de error). Ninguno aparece.
**No aplica o choca con:** con usuarios expertos de un dominio, la jerga del dominio sí es su idioma.
**Fuente:** Nielsen (1994), heurística 2.
**Confianza:** media.

### Botones que dicen lo que pasa
**Dice:** una etiqueta como «Guardar cambios» o «Borrar 3 notas» se entiende sin leer el resto; «Sí»,
«Aceptar» o «Enviar» obligan a leer la pregunta.
**Se aplica:** cada botón empieza por un verbo y nombra el objeto si hay duda.
**Se mide:** con Playwright: ningún botón dice solo «Sí», «No», «Aceptar» u «OK».
**No aplica o choca con:** en superficie pequeña, la etiqueta se acorta, pero conserva el verbo.
**Fuente:** Nielsen (2018), sobre los diálogos de confirmación.
**Confianza:** media.

### Mensajes de error
**Dice:** un buen mensaje de error cumple doce pautas, en tres grupos:
- **Visibilidad:** está junto a lo que falló, se marca de más de una forma (no solo con color), se
  corresponde con la gravedad y no aparece antes de tiempo.
- **Comunicación:** usa lenguaje llano, dice qué falló en concreto, explica cómo arreglarlo y no culpa
  al usuario.
- **Eficiencia:** previene el error si puede, conserva lo que el usuario escribió, ofrece arreglarlo
  fácil y da ayuda en contexto.
**Se aplica:** por cada error de la tabla de estados se escribe el texto con esas pautas.
**Se mide:** con Playwright, provocando cada error: el mensaje está junto al campo o al elemento (y
asociado con `aria-describedby`), lo escrito se conserva y el texto no contiene códigos ni términos
técnicos.
**No aplica o choca con:** con la prevención: el mejor mensaje es el que no hace falta.
**Fuente:** Neusesser y Sunwall (2023), rúbrica de mensajes de error, NN/g; Nielsen (1994), heurística 9.
**Confianza:** media.

### Iconos con etiqueta
**Dice:** fuera de unos pocos iconos casi universales, como inicio, imprimir o la lupa de buscar, un
icono solo es ambiguo. Una etiqueta de texto, visible siempre, lo resuelve. Confiar la etiqueta al
paso del ratón no sirve: en pantallas táctiles no existe.
**Se aplica:** los iconos de navegación y de acciones poco frecuentes llevan texto visible. Los que no
tienen sitio llevan al menos un nombre accesible, sabiendo que eso ayuda al lector de pantalla y no a
quien mira.
**Se mide:** con Playwright: listar los botones sin texto visible; cada uno es un icono universal o se
justifica.
**No aplica o choca con:** con la densidad y con la superficie pequeña; ahí se aceptan iconos solos en
acciones frecuentes que el usuario aprende.
**Fuente:** Harley (2014), *Icon Usability*, NN/g.
**Confianza:** media.

## Mitos

| Creencia | Qué dice la evidencia | Fuente |
|---|---|---|
| «Un tutorial al empezar ayuda a aprender» | No mejoró el éxito ni el tiempo, y empeoró la dificultad percibida | Kendrick (2020) |
| «Pedir confirmación evita errores» | Con el uso deja de leerse; deshacer protege mejor | Nielsen (2018); Anderson et al. (2015) |
| «Cuanto más automático, mejor» | Ante la duda, vale más hacer menos pero bien; lo automático tiene que aportar valor | Horvitz (1999), factores 1 y 8 |
