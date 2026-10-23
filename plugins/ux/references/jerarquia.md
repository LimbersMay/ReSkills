# Jerarquía, disposición y densidad

Cómo se ordena lo que hay dentro de una vista una vez elegida su estructura. Cada principio se puede
comprobar sobre una captura o sobre el DOM; lo que se mide con Playwright lo dice. Las referencias
completas están en [fuentes.md](fuentes.md).

## Principios

### En cada vista manda una cosa
**Dice:** el ojo va primero a lo que más contrasta con su entorno: tamaño, peso, color, posición,
espacio alrededor. Si todo pesa igual, nada guía la mirada y el usuario lee al azar o en F (ver
[patrones de lectura](#patrones-de-lectura)). Lo que más pesa tiene que ser la tarea principal de esa
vista.
**Se aplica:** por cada vista, ¿cuál es el elemento que más destaca? ¿Coincide con la tarea principal
de la [tabla de tareas](entender.md#plantilla-de-la-tabla-de-tareas)? ¿Hay un segundo nivel claro y el
resto en un tercero?
**Se mide:** con Playwright, una captura desenfocada (por ejemplo, un filtro de desenfoque de 8 a 12 px):
lo que aún se distingue es lo que manda. A ojo: no más de un elemento en el primer nivel.
**No aplica o choca con:** en vistas de consulta, como un panel con varios indicadores del mismo valor,
puede no haber una única cosa principal; entonces manda el orden.
**Fuente:** Johnson (2020), caps. 2 y 3; Pernice (2017).
**Confianza:** media (la prueba del desenfoque es práctica, no un método validado).

### Proximidad
**Dice:** lo que está cerca se percibe como un grupo. Es el principio de agrupación más fuerte y el más
barato: no añade bordes ni color.
**Se aplica:** el espacio entre grupos es claramente mayor que el espacio dentro de cada grupo. Una
etiqueta está más cerca de su valor que del valor de al lado.
**Se mide:** con Playwright, sobre las cajas del DOM: en cada grupo, el hueco mayor dentro del grupo
tiene que ser menor que el hueco menor hasta el grupo vecino. Una proporción de al menos 1,5 entre
ambos es un umbral práctico, no un dato de la investigación.
**No aplica o choca con:** en superficie pequeña, el espacio entre grupos cuesta altura; ahí puede
convenir una línea fina o un cambio de fondo.
**Fuente:** Wagemans et al. (2012); Johnson (2020), cap. 2.
**Confianza:** alta (el principio); baja (el umbral).

### Región común
**Dice:** lo que comparte un fondo o un borde se percibe como un grupo, aunque no esté cerca. Es un
principio distinto de la proximidad, y sirve para agrupar lo que la disposición separa.
**Se aplica:** se usa una caja o un fondo solo cuando el espacio no basta para agrupar, o cuando hay que
agrupar cosas separadas. No se mete cada elemento en su caja.
**Se mide:** a ojo: ¿cada caja agrupa algo que el espacio solo no agruparía? Con Playwright, cuántas
cajas con borde o fondo propio hay en la vista; muchas cajas anidadas son una señal de aviso.
**No aplica o choca con:** cada borde añade aristas, y la densidad de aristas es una de las medidas de
desorden visual (Rosenholtz et al.). Agrupar con cajas tiene un coste que agrupar con espacio no tiene.
**Fuente:** Palmer (1992); Wagemans et al. (2012); Rosenholtz, Li y Nakano (2007).
**Confianza:** alta.

### Semejanza
**Dice:** lo que se parece se percibe como relacionado. Por eso lo que funciona igual tiene que verse
igual, y lo que funciona distinto tiene que verse distinto.
**Se aplica:** todos los elementos pulsables del mismo tipo comparten estilo; ningún texto que no se
pulsa se parece a un enlace o a un botón.
**Se mide:** con Playwright: agrupar los elementos interactivos por estilo calculado (color, borde,
peso) y comprobar que cada estilo corresponde a un solo tipo de acción.
**No aplica o choca con:** con la jerarquía: la acción principal tiene que verse distinta de las
secundarias aunque sean del mismo tipo.
**Fuente:** Wagemans et al. (2012); Nielsen (1994), heurística 4 (consistencia).
**Confianza:** alta.

### Alineación
**Dice:** cuantas menos líneas de alineación distintas, más ordenada y fácil de recorrer parece la
vista. Tullis encontró que la complejidad de la disposición y la agrupación predecían el tiempo de
búsqueda en pantallas de texto; las métricas automáticas de estética usan la calidad de la retícula
con el mismo fin.
**Se aplica:** los bordes izquierdos de los bloques de texto caen en pocas columnas; los valores
numéricos se alinean a la derecha.
**Se mide:** con Playwright: contar las coordenadas x distintas donde empiezan los bloques de texto
visibles (con una tolerancia de 2 px). Comparar entre variantes: menos es mejor, a igualdad de
contenido.
**No aplica o choca con:** con la jerarquía: romper la alineación es una forma de destacar algo. Se
hace a propósito y una vez.
**Fuente:** Tullis (1983); Miniukovich y De Angeli (2015).
**Confianza:** media (las medidas vienen de pantallas de texto y de estudios de estética).

### Patrones de lectura
**Dice:** sin pistas fuertes, el usuario escanea en F: lee las primeras líneas, baja por el margen
izquierdo y se salta lo de la derecha. La F es un fallo, no una forma de diseñar: aparece con bloques
de texto sin formato y hace que se pierda contenido. Con encabezados claros, el usuario escanea en
capas (de encabezado en encabezado), que es la forma más eficaz.
**Se aplica:** lo importante va primero, en el encabezado o en las primeras palabras de cada línea.
Los encabezados empiezan por la palabra que más informa. Nada crítico depende de que se lea la
columna derecha.
**Se mide:** a ojo: ¿se entiende la vista leyendo solo los encabezados y las primeras palabras? Con
Playwright: en listas, que la información que distingue cada elemento esté en la mitad izquierda.
**No aplica o choca con:** en idiomas que se leen de derecha a izquierda, el patrón se invierte. En una
interfaz con poco texto (botones, iconos, cifras) manda la jerarquía visual, no la lectura.
**Fuente:** Pernice (2017), *F-Shaped Pattern of Reading on the Web: Misunderstood, But Still
Relevant (Even on Mobile)*.
**Confianza:** alta (seguimiento ocular). Ver el mito en [Mitos](#mitos).

### La primera pantalla
**Dice:** la atención cae con fuerza tras la primera pantalla. En el estudio de NN/g de 2018, el 57 %
del tiempo de mirada se quedó en la primera pantalla y el 74 % en las dos primeras. El usuario sí
desplaza, pero lo hace cuando tiene un motivo.
**Se aplica:** la tarea principal de la vista y su primer dato caben en la primera pantalla de la
superficie más pequeña que se sirve.
**Se mide:** con Playwright, al tamaño real de la superficie: la distancia en píxeles desde arriba
hasta el primer dato o control de la tarea principal, como fracción de la altura visible. Cabeceras,
avisos y espacio decorativo que empujan ese dato hacia abajo cuentan en contra.
**No aplica o choca con:** con la [vista única con secciones](estructura.md#catálogo-de-navegación):
desplazar está bien si lo que hay arriba invita a seguir.
**Fuente:** Fessenden (2018), *Scrolling and Attention*.
**Confianza:** alta en el dato; media en el umbral, que depende de la superficie.

### Densidad y relación dato/tinta
**Dice:** cada elemento que no informa compite con los que sí. Tufte lo formuló para los gráficos: la
mayor parte de la tinta tiene que estar en los datos. Tullis encontró que, en pantallas de texto, lo
que más predecía el tiempo de búsqueda era cuántos grupos había y lo grandes que eran.
**Se aplica:** se quitan los adornos que no ayudan a una tarea (bordes dobles, iconos decorativos,
etiquetas repetidas). Se agrupa en lugar de apretar.
**Se mide:** con Playwright, sobre la captura: medidas de desorden visual (densidad de aristas o
congestión de rasgos, Rosenholtz et al.) o de complejidad visual (Reinecke et al.), para comparar
variantes entre sí. No hay un valor absoluto bueno.
**No aplica o choca con:** con el uso frecuente: una vista de uso diario puede enseñar más a la vez
que una de uso raro. Esto es práctica de diseño, no un resultado medido; no hay un estudio que aísle la
pericia como causa. Y con la memoria: Bateman et al. encontraron que los gráficos con adornos se
entendían igual de bien y se recordaban mejor; estudiaron gráficos, no interfaces. Minimizar no es un fin.
**Fuente:** Tufte (2001); Tullis (1983); Bateman et al. (2010); Rosenholtz, Li y Nakano (2007);
Reinecke et al. (2013).
**Confianza:** media (las medidas predicen búsqueda o estética, no usabilidad); baja en lo del uso
frecuente.

### Ley de Fitts: tamaño y distancia
**Dice:** el tiempo de llegar a un objetivo crece con la distancia y baja con su tamaño, de forma
logarítmica. Lo que se pulsa a menudo tiene que ser grande y estar cerca de donde ya está la mano o la
vista.
**Se aplica:** la acción principal es el objetivo más fácil de alcanzar de la vista. Las acciones
frecuentes no están en el extremo opuesto de aquello sobre lo que actúan
([estructura.md](estructura.md#las-acciones-cerca-de-lo-que-afectan)). Las destructivas no están pegadas
a las frecuentes.
**Se mide:** con Playwright: tamaño de cada objetivo interactivo y distancia hasta el elemento sobre el
que actúa. El tamaño mínimo es un criterio de WCAG ([accesibilidad.md](accesibilidad.md)).
**No aplica o choca con:** con la densidad: objetivos grandes ocupan sitio. En pantallas táctiles el
dedo impone un mínimo propio, que Fitts no recoge.
**Fuente:** Fitts (1954); MacKenzie (1992).
**Confianza:** alta.

## Mitos

| Creencia | Qué dice la evidencia | Fuente |
|---|---|---|
| «Hay que diseñar en F» | La F es el patrón que aparece cuando faltan pistas, y hace perder contenido; el objetivo es evitarla | Pernice (2017) |
| «Menos es siempre mejor» | En gráficos, quitar adornos no mejoró la comprensión y empeoró el recuerdo | Bateman et al. (2010) |
| «Lo que no está en la primera pantalla no se ve» | Los usuarios desplazan; la atención cae, pero no desaparece | Fessenden (2018) |
