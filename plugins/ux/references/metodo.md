# Método: explorar y decidir

Cómo se pasa de unos requisitos a un diseño elegido sin quedarse en la primera idea. Primero el método en
pasos; después, cada principio con su evidencia. Las referencias completas están en
[fuentes.md](fuentes.md).

## El método en pasos

| Paso | Qué se hace | Por qué | Principio |
|---|---|---|---|
| 1 | Escribir las preguntas de estructura de cada vista | Una variante es una respuesta distinta a esas preguntas; sin ellas, las variantes salen distintas solo en superficie | [Preguntas, opciones y criterios](#preguntas-opciones-y-criterios) |
| 2 | Fijar los criterios de juicio antes de generar | Si los criterios llegan después, se eligen a medida de la variante favorita | [Abrir y cerrar por separado](#abrir-y-cerrar-por-separado) |
| 3 | Elegir de 3 a 5 direcciones distintas de estructura | Con varias a la vez salen mejores diseños y más variados que puliendo una | [Variantes en paralelo](#variantes-en-paralelo) · [Cuántas](#cuántas-variantes) |
| 4 | Construir cada variante sin ver el mock ni las otras | Quien ve un ejemplo copia sus rasgos, también los malos | [Fijación](#la-fijación-en-el-ejemplo) · [Aislar al que genera](#aislar-al-que-genera) |
| 5 | Comprobar que difieren en estructura | Dos variantes con las mismas respuestas son una sola | [Estructura frente a superficie](#estructura-frente-a-superficie) |
| 6 | Meter el mock como una variante más, sin marcarlo | Se juzga con los mismos criterios y sin saber que es el original; no se traduce 1:1 | [Fijación](#la-fijación-en-el-ejemplo) |
| 7 | Evaluar sin ver el razonamiento de quien diseñó | El que diseñó, y el modelo que generó, juzgan a favor de lo suyo | [Aislar al que evalúa](#aislar-al-que-evalúa) |
| 8 | Comparar contra la variante mejor puntuada, criterio a criterio; elige el usuario | Obliga a mirar cada criterio y deja ver qué hace bien cada variante; cada signo sale de un hallazgo | [Comparar contra una referencia](#comparar-contra-una-referencia) |
| 9 | Combinar decisiones, no trozos de pantalla, y evaluar la mezcla | Fusionar lo mejor rinde más que quedarse con la mejor, si el conjunto es coherente | [Combinar sin Frankenstein](#combinar-sin-frankenstein) |
| 10 | Escribir el porqué de cada decisión en `ux.md` | Lo puede leer alguien que no es diseñador | [Preguntas, opciones y criterios](#preguntas-opciones-y-criterios) |

Para cómo se evalúa (heurísticas, recorrido cognitivo, métricas), ver [evaluar.md](evaluar.md).

## Principios

### Abrir y cerrar por separado
**Dice:** primero se abren opciones sin juzgarlas y después se elige con criterios. Si se hacen las dos
cosas a la vez, la primera opción aceptable gana. El doble diamante lo formula en dos fases, divergir y
converger, para el problema y para la solución.
**Se aplica:** ¿hay al menos tres variantes completas antes de la primera puntuación? ¿Los criterios
estaban escritos antes de generar?
**Se mide:** a ojo: el orden de los archivos o de los mensajes (criterios, después variantes, después
juicio).
**No aplica o choca con:** con un cambio pequeño en una vista que ya funciona, se itera sobre ella. El
doble diamante es un marco de la práctica, no un resultado experimental: su respaldo empírico viene de
Dow et al. (2010) y de Nielsen y Faber (1996).
**Fuente:** Design Council (2005, revisado en 2019); Dow et al. (2010).
**Confianza:** media.

### Preguntas, opciones y criterios
**Dice:** cada decisión de diseño se escribe como una pregunta («¿dónde vive la acción principal?»),
las opciones que se consideraron y los criterios que las separan, con qué opción cumple cada criterio.
Es el *design rationale* QOC.
**Se aplica:** antes de generar, la skill lista las preguntas de estructura de cada vista: qué hay en
ella, dónde viven las acciones, cómo se llega y cómo se sale. Al cerrar, `ux.md` guarda cada pregunta
con la opción elegida, las descartadas y el criterio que decidió.
**Se mide:** a ojo: cada decisión de `ux.md` tiene pregunta, al menos dos opciones y un criterio que
cita una tarea o un requisito.
**No aplica o choca con:** escribir todas las preguntas cuesta; se escriben solo las que separan
variantes. Choca con decidir rápido en vistas triviales.
**Fuente:** MacLean, Young, Bellotti y Moran (1991).
**Confianza:** media (método establecido, poca evidencia de efecto medido).

### Variantes en paralelo
**Dice:** hacer varias variantes antes de recibir crítica da mejores resultados que hacer una, criticarla
y rehacerla. En el experimento de Dow et al., con el mismo tiempo, los anuncios del grupo en paralelo
(tres prototipos, crítica, dos más, crítica, final) superaron a los del grupo en serie en clics y en
valoración experta, y fueron más variados.
**Se aplica:** ¿la crítica llegó cuando ya había varias variantes, o después de la primera?
**Se mide:** número de variantes completas antes de la primera evaluación.
**No aplica o choca con:** cuesta más por ronda. Choca con la iteración, que es más barata: NN/g
recomienda abrir en paralelo una vez y después iterar sobre la mezcla.
**Fuente:** Dow et al. (2010); Nielsen y Faber (1996); Tohidi et al. (2006).
**Confianza:** alta (experimentos controlados), con la salvedad de que se hicieron con diseñadores
novatos y anuncios web.

### Cuántas variantes
**Dice:** entre tres y cinco. Tres es el mínimo que usan los estudios (Dow: 3 + 2; Tohidi: 3). NN/g pone
cinco como máximo práctico. Más allá, cada variante sale más pobre y la comparación cuesta más de lo que
aporta.
**Se aplica:** tres variantes por defecto. Cinco si la vista es central y las preguntas de estructura
tienen muchas respuestas plausibles.
**Se mide:** número de variantes.
**No aplica o choca con:** no hay un número óptimo demostrado; es consenso de la práctica apoyado en lo
que usaron los experimentos.
**Fuente:** Dow et al. (2010); NN/g, Nielsen (2011); Tohidi et al. (2006).
**Confianza:** media.

### Mostrar varias a la vez mejora la crítica
**Dice:** quien ve un solo diseño lo puntúa más alto y lo critica menos que quien ve el mismo diseño
junto a otros dos. Con alternativas, la crítica es más dura y más concreta.
**Se aplica:** el usuario revisa las variantes juntas, no de una en una. Lo mismo para un evaluador
automático.
**Se mide:** a ojo: la revisión enseña todas las variantes en la misma pantalla o en el mismo mensaje.
**No aplica o choca con:** los participantes de Tohidi señalaron problemas, pero no propusieron
soluciones: ver alternativas sirve para encontrar fallos, no para que el usuario rediseñe.
**Fuente:** Tohidi, Buxton, Baecker y Sellen (2006).
**Confianza:** alta.

### La fijación en el ejemplo
**Dice:** quien ve un ejemplo antes de diseñar repite sus rasgos, incluso los que se le han señalado como
defectos. Un mock de referencia es un ejemplo. También lo son las imágenes generadas por IA: en un
experimento de 2024, usar un generador de imágenes durante la ideación aumentó la fijación en el ejemplo
inicial y redujo la variedad de las ideas.
**Se aplica:** el mock no entra hasta que las variantes están construidas. Después entra como una
variante más, con un nombre neutro como las demás, y se juzga con los mismos criterios. Quien evalúa no
sabe cuál es el original.
**Se mide:** cuántos rasgos de estructura del mock (qué hay en cada vista, dónde viven las acciones,
cómo se navega) repite cada variante. Si todas los repiten, hubo fijación.
**No aplica o choca con:** los ejemplos también inspiran. El metaanálisis de Sio et al. (43 estudios)
encuentra que reducen la variedad de las ideas pero aumentan su novedad, y que ayudan más cuando son
pocos y poco comunes. La fijación depende de la formación: Purcell y Gero no la encontraron en
diseñadores industriales con el mismo protocolo que sí fijó a los ingenieros.
**Fuente:** Jansson y Smith (1991); Purcell y Gero (1996); Sio, Kotovsky y Cagan (2015);
Wadinambiarachchi et al. (2024).
**Confianza:** alta.

### Avisar no basta
**Dice:** decir «no copies el ejemplo» funciona poco. Chrysikou y Weisberg sí redujeron la fijación con
instrucciones explícitas sobre qué evitar, pero en un estudio con 303 participantes las instrucciones
que desaconsejaban copiar no cambiaron ni el número ni el tipo de ideas; solo las que animaban a copiar
tuvieron efecto.
**Se aplica:** no se confía en una instrucción en el prompt («no te bases en el mock») para evitar la
fijación. Se evita que el mock esté en el contexto de quien genera.
**Se mide:** a ojo: el mock no aparece en el brief de quien genera las variantes.
**No aplica o choca con:** si el mock trae una restricción real (una pieza obligatoria, un orden que
pide el negocio), esa restricción se escribe en el brief como requisito, sin enseñar el mock.
**Fuente:** Chrysikou y Weisberg (2005); Vasconcelos, Neroni y Crilly (2018).
**Confianza:** media (los resultados no coinciden).

### Aislar al que genera
**Dice:** las variantes no se ven entre sí ni ven el mock mientras se construyen. En personas, generar
por separado y juntar después produce más ideas que generar en grupo (grupos nominales). El motivo
principal es el bloqueo: mientras uno habla, los demás no producen.
**Se aplica:** cada variante se construye a partir del brief (requisitos, tareas, superficie) y de su
dirección, sin el resto.
**Se mide:** a ojo: qué tenía delante quien construyó cada variante.
**No aplica o choca con:** **en modelos de lenguaje, aislar no basta.** Varias llamadas independientes
con el mismo prompt devuelven respuestas casi iguales: el modelo cae en su respuesta más típica (*mode
collapse*). Pedir la lista entera en un mismo contexto, y además pedir que cada elemento sea distinto de
los anteriores, da más variedad (Meincke et al.; Zhang et al.). Aislar solo ayuda si cada uno recibe
una dirección distinta. Ver [Decisión abierta: subagentes](#decisión-abierta-subagentes).
**Fuente:** Diehl y Stroebe (1987); Meincke, Mollick y Terwiesch (2024); Zhang et al. (2025).
**Confianza:** alta en personas; media en modelos (estudios recientes, tareas de texto).

### Aislar al que evalúa
**Dice:** quien juzga no ve el razonamiento de quien diseñó. Es otro aislamiento, contra otro sesgo: no
reduce la fijación, reduce el sesgo al juzgar. Las personas tienden a preferir sus propias ideas, aunque
el efecto varía con la calidad de la idea. En modelos de lenguaje está mejor medido: un modelo puntúa
más alto lo que generó él mismo; cambia de juicio si el texto cita una autoridad, y tiende a darle la
razón a quien le habla.
**Se aplica:** el evaluador recibe las variantes (capturas, DOM) y el brief, pero no las notas de
diseño, ni qué variante prefiere el agente, ni qué opina el usuario, ni cuál es el mock. Las variantes
llegan sin nombre de autor y en otro orden en cada pasada, porque los modelos también prefieren según
la posición.
**Se mide:** a ojo: el contexto del evaluador no contiene el razonamiento. Se compara el veredicto con
las variantes en dos órdenes distintos.
**No aplica o choca con:** el evaluador ve las tareas y los criterios. Aislar el contexto no basta: un
modelo reconoce y prefiere lo suyo aunque lo juzgue en otra llamada, y en la skill genera y evalúa el
mismo modelo. Lo reducen las etiquetas neutras, juzgar contra criterios y no por preferencia, dar más
peso a lo medido con herramientas y, si se puede, evaluar con otro modelo. Cuesta otra pasada.
**Fuente:** Toh y Miller (2015); Toh, Strohmetz y Miller (2016); Zheng et al. (2023); Panickssery,
Bowman y Feng (2024); Chen et al. (2024); Sharma et al. (2024).
**Confianza:** media en personas; alta en modelos (el sesgo). Que esas medidas basten es una hipótesis
para la pasada a mano.

### Estructura frente a superficie
**Dice:** una variante cuenta si cambia la estructura: qué hay en cada vista, dónde viven las acciones o
cómo se navega. Cambiar color, tipografía o espaciado es superficie. Garrett separa los planos:
estrategia, alcance, estructura, esqueleto y superficie. Las variantes de este método se mueven en
estructura y esqueleto.
**Se aplica:** la prueba es describir cada variante en una línea sin palabras visuales («la lista es la
vista principal y el detalle se abre en un panel lateral»). Si dos descripciones coinciden, son la misma
variante. Otra forma: dos variantes que responden igual a las preguntas de estructura (paso 1) son una.
**Se mide:** a ojo, con esa prueba. Ayuda una tabla con una fila por pregunta y una columna por
variante: cada par de columnas tiene que diferir en al menos una fila.
**No aplica o choca con:** la superficie importa para la jerarquía (ver [jerarquia.md](jerarquia.md)),
pero se decide después, sobre la estructura elegida.
**Fuente:** Garrett (2011); MacLean et al. (1991).
**Confianza:** media.

### Comparar contra una referencia
**Dice:** se elige una variante como referencia y cada una de las demás se marca criterio a criterio
como mejor (+), igual (S) o peor (−). Las cuentas no deciden solas: sirven para ver qué hace bien cada
variante, que es lo que luego se rescata. Es la convergencia controlada de Pugh: se combinan las
fuerzas, se vuelve a comparar y en cada ronda puede cambiar la referencia.
**Se aplica:** la tabla tiene una fila por criterio y una columna por variante. La referencia de la
primera ronda es la variante mejor puntuada en la evaluación aislada, **nunca el mock**: medirlo todo
como «mejor o peor que el mock» vuelve a meter al juzgar la fijación que se evitó al generar. El mock es
una columna más, sin marcar.
**Se mide:** la tabla misma. Cada «+» y cada «−» cita un hallazgo ya registrado (un problema de la
tabla de problemas, una medida, una tarea); sin hallazgo, la celda es «S». Nunca sale de una impresión
del conjunto: en pares, un modelo acierta casi al azar salvo que la diferencia sea grande
([evaluar.md](evaluar.md#modelos-de-lenguaje-que-evalúan-interfaces)). Elige el usuario, con la tabla
delante.
**No aplica o choca con:** el resultado puede cambiar según qué referencia se elija; Nicholson y Collopy
lo encontraron en cerca de un tercio de los casos que analizaron. Por eso se repite la comparación con
otra referencia antes de elegir. No sustituye a la evaluación: la ordena.
**Fuente:** Pugh (1991); Nicholson y Collopy (2019).
**Confianza:** media.

### Combinar sin Frankenstein
**Dice:** el objetivo no es escoger la variante ganadora, sino un diseño que reúna las mejores ideas de
todas. En el caso de Nielsen y Faber, con la media de las cuatro originales en 100, la mejor original
valía 136; iterarla sola dio 156 (+56 %) y la mezcla de las cuatro, 170 (+70 %). Pero la mezcla tiene
que ser coherente: se rescatan decisiones (respuestas a una pregunta de estructura), no trozos de
pantalla.
**Se aplica:** de cada variante descartada se anota qué respuesta a qué pregunta hizo bien, según la
tabla de comparación. La mezcla toma una respuesta por pregunta. Después se evalúa como una variante
nueva, con los mismos criterios y el mismo evaluador aislado.
**Se mide:** la mezcla no puede empeorar en ningún criterio en que la referencia era mejor sin
explicarlo. La heurística de consistencia de Nielsen (ver [evaluar.md](evaluar.md)) es la que detecta
el Frankenstein: dos formas distintas de hacer lo mismo en la misma vista.
**No aplica o choca con:** algunas respuestas dependen unas de otras: si la navegación es por
pestañas, la acción principal no puede vivir donde lo pedía una variante con maestro-detalle. Esas
respuestas se rescatan juntas o no se rescatan.
**Fuente:** Nielsen y Faber (1996); NN/g, Nielsen (2011).
**Confianza:** media (un caso de estudio, consenso de la práctica).

## Modelos de lenguaje que generan variantes

Lo que dice la investigación desde 2023, para cuando el que genera es un agente.

- **Menos variedad que las personas.** Con GPT-4, los conjuntos de ideas son menos diversos que los de
  un grupo de personas, con casi cualquier prompt (Meincke et al., 2024; Ma et al., 2025). Entre
  modelos distintos, las respuestas también se parecen entre sí (Jiang et al., 2025).
- **Quien usa un modelo para idear acaba pareciéndose a los demás que lo usan.** Las ideas de cada
  persona son más detalladas, pero las de distintas personas se parecen más (Anderson et al., 2024).
- **El prompt pesa más que la temperatura.** Subir la temperatura no dio una tendencia clara; pedir
  ideas «muy alejadas» y revisar cada una, sí (Ma et al., 2025). La cadena de pasos (primero la
  lista, después hacer cada idea distinta) fue lo más cercano a un grupo de personas (Meincke et al.).
- **Pedir varias a la vez, no una cada vez.** Pedir k respuestas en un mismo prompt da más variedad que
  k llamadas independientes; pedirlas con su probabilidad estimada, más aún (Zhang et al., 2025).

**Se aplica:** las direcciones de estructura (paso 3) se piden todas juntas, en un mismo contexto, con
la instrucción de que difieran en las preguntas de estructura. Después se comprueba con la prueba de
[estructura frente a superficie](#estructura-frente-a-superficie).

## Decisión abierta: subagentes

¿Se genera cada variante en un subagente aislado que solo ve el brief? No se cierra aquí. Lo que dice
la evidencia:

- **A favor de aislar:** la fijación en el mock y en las otras variantes está bien probada en personas
  (Jansson y Smith; Sio et al.) y aparece también con imágenes de IA (Wadinambiarachchi et al.). Avisar
  no basta (Vasconcelos et al.): la forma segura de que el mock no ancle es que no esté en el contexto.
- **En contra de aislar sin más:** varios subagentes con el mismo brief tienden a la misma respuesta
  típica (Zhang et al.; Jiang et al.). La variedad sale mejor pidiendo las direcciones juntas (Meincke
  et al.).
- **Lo que encaja con las dos cosas:** las direcciones se generan juntas y sin el mock; cada variante
  se construye después por separado, con su dirección y el brief. Falta probarlo en la pasada a mano.
- **El evaluador** sí tiene respaldo para ir aislado ([Aislar al que evalúa](#aislar-al-que-evalúa)),
  como en la crítica de impeccable, que separa en subagentes la revisión y el detector (Bakaus).

## Mitos

| Creencia | Qué dice la evidencia | Fuente |
|---|---|---|
| «Subir la temperatura da variantes más distintas» | Sin tendencia clara; el prompt pesa más | Ma et al. (2025) |
| «Basta con pedirle que no copie el ejemplo» | Las instrucciones que desaconsejan copiar apenas cambian el resultado | Vasconcelos et al. (2018) |
