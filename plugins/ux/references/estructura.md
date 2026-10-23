# Estructura: arquitectura de información y navegación

Cómo se reparte el contenido en vistas, cómo se pasa de una a otra y dónde viven las acciones. Es el
material del que salen las variantes de [metodo.md](metodo.md). Hay dos catálogos: uno responde a
«¿cómo se navega?» y otro a «¿dónde viven las acciones?». Una variante que solo cambia la navegación
explora la mitad del espacio. Las referencias completas están en [fuentes.md](fuentes.md).

## Catálogo de navegación

| Patrón | Qué es | Sirve cuando | No sirve cuando | En superficie pequeña |
|---|---|---|---|---|
| **Barra de navegación (pestañas de secciones)** | De 3 a 5 destinos fijos del mismo nivel, siempre visibles | Hay pocas secciones independientes y el usuario salta entre ellas | Hay más de 5, o los destinos son acciones y no lugares | Abajo en móvil; en un popup, cuesta su altura en cada vista |
| **Pestañas dentro de una vista** | Paneles alternativos del mismo contexto | El contenido es largo, se agrupa con claridad y no hace falta comparar entre pestañas | El usuario tiene que comparar, o lo crítico quedaría en una pestaña no visible por defecto | Mejor acordeones (NN/g) |
| **Segmentado** | Dos o tres modos o filtros de la misma vista («Lista / Mapa») | Se cambia la forma de ver lo mismo | Se cambia de sección: eso es navegación | Funciona bien si caben las etiquetas |
| **Lista-detalle (maestro-detalle)** | Una lista de elementos; al elegir uno, su detalle | El contenido es una colección y cada elemento tiene más información | Hay pocos elementos o el detalle es casi igual que la fila | Un solo panel: la lista, y el detalle encima con «atrás» |
| **Panel de apoyo** | Un área principal y otra secundaria que solo tiene sentido junto a ella | Lo secundario (ajustes, comentarios) se consulta sin dejar lo principal | Lo secundario es independiente | No cabe: pasa a hoja inferior o a otra vista |
| **Profundizar con migas** | Una jerarquía de varios niveles, con el camino visible | El contenido tiene jerarquía real y el usuario la conoce | La jerarquía es del sistema, no del usuario | Se reduce a «atrás» más el título del nivel |
| **Centro y radios (*hub and spoke*)** | Una vista central; cada sección es una ida y vuelta | Las tareas son independientes y se hace una por visita | El usuario encadena tareas de varias secciones | Funciona bien: una tarea por vista |
| **Búsqueda primero** | La entrada es un buscador | El usuario sabe cómo se llama lo que busca y el conjunto es grande | El usuario no conoce el vocabulario o el conjunto es pequeño | Funciona bien si el teclado no tapa los resultados |
| **Lista única con filtros** | Todo en una lista, acotada con filtros o agrupaciones | Los elementos son del mismo tipo y difieren en atributos | Los elementos son de tipos distintos, con tareas distintas | Filtros plegados en una fila o una hoja |
| **Por pasos (asistente)** | Una secuencia lineal, un subconjunto por paso | La tarea se divide en pasos que apenas dependen entre sí | Los pasos dependen unos de otros y hay que ir y volver | Funciona bien: un paso por pantalla |
| **Vista única con secciones** | Sin navegación: todo en una vista, con encabezados y desplazamiento | Hay poco contenido, las tareas se encadenan o la navegación se comería la altura útil | Hay mucho contenido y lo importante quedaría abajo: la atención cae tras la primera pantalla | Opción legítima: a menudo la mejor en un popup o un panel estrecho |

**Fuentes del catálogo:** Tidwell, Brewer y Valencia (2020), cap. 3; Android, *Canonical layouts*
(lista-detalle, panel de apoyo, feed) y *Navigation bar* (3 a 5 destinos); Apple HIG, *Tab bars*; NN/g,
Sunwall (2024), *Tabs, Used Right*; NN/g, Nielsen (2006), *Progressive Disclosure* (por pasos); NN/g,
Fessenden (2018), *Scrolling and Attention* (el 57 % del tiempo de lectura cae en la primera pantalla y
el 74 %, en las dos primeras). Las guías de plataforma se usan como catálogo, no como reglas.

## Catálogo de acciones

| Patrón | Qué es | Sirve cuando | No sirve cuando | En superficie pequeña o táctil |
|---|---|---|---|---|
| **Acción en cada fila** | Un botón o icono visible en cada elemento de una lista | Hay una o dos acciones frecuentes por elemento | Hay muchas: se repiten en cada fila y hacen ruido; o la acción es destructiva y fácil de pulsar sin querer | Cuesta ancho; el objetivo necesita tamaño mínimo ([accesibilidad.md](accesibilidad.md)) |
| **Acción en el detalle** | Las acciones viven dentro del elemento abierto | Las acciones son raras o exigen ver el elemento entero | La acción es frecuente y se hace sobre muchos elementos: obliga a entrar y salir | Funciona bien |
| **Barra de la vista** | Acciones que afectan a toda la vista o al elemento abierto, en una barra superior o de herramientas | Hay pocas acciones de la vista | La acción es de un elemento concreto de una lista: queda lejos de lo que afecta | Unos tres iconos; el resto, al desbordamiento |
| **Acción principal fija** | Un único botón destacado y fijo para la acción más importante de la pantalla | Hay una acción constructiva claramente principal (crear, empezar) | La acción es secundaria, destructiva o poco clara, o hay varias que compiten: una por pantalla | Habitual en móvil; tapa contenido al desplazar |
| **Modo de selección (en lote)** | Casillas en cada elemento y una barra con las acciones y el número de elementos elegidos | El usuario actúa a menudo sobre muchos elementos a la vez | Casi siempre se actúa sobre uno: añade un modo que hay que entender | Se entra con un control visible, no solo con pulsación larga |
| **Menú de desbordamiento** | Acciones secundarias detrás de un icono (⋮ o …), junto a la vista o al elemento | Las acciones se usan de vez en cuando | La acción es principal o muy frecuente; o solo hay una o dos (mejor visibles) | Icono pequeño, fácil de pasar por alto |
| **Menú contextual** | Clic derecho o pulsación larga sobre el elemento; no se ve hasta que se abre | Es un atajo para quien ya conoce el producto | Es el único camino a una acción: está oculto y el usuario puede no saber que existe | La pulsación larga tampoco se ve |
| **Acciones al pasar el ratón** | Aparecen solo cuando el puntero está sobre el elemento | Quitan ruido en listas densas de escritorio, si hay otro camino | Es el único camino: no existen con teclado ni en pantallas táctiles ([accesibilidad.md](accesibilidad.md)) | No sirve: en táctil no hay «pasar por encima» |

**Fuentes del catálogo:** NN/g, Kaplan (2025), *Designing Effective Contextual Menus: 10 Guidelines*;
Apple HIG, *Context menus*; Material Design, *Floating action button* y *Top app bar*; Android,
*Layout and navigation patterns* (lo menos frecuente, al desbordamiento). El modo de selección sale de
la práctica de los sistemas de diseño y no tiene un estudio detrás: confianza baja.

### Las acciones, cerca de lo que afectan
**Dice:** una acción se pone dentro o junto al objeto que modifica. Así el usuario predice qué hace y
qué hay en su menú. Lejos del objeto, se pasa por alto o se aplica a lo que no era.
**Se aplica:** en cada variante, para cada acción de la tabla de tareas: ¿qué afecta (un elemento,
varios, la vista entera) y dónde está?
**Se mide:** a ojo, por acción. La distancia del puntero hasta la acción entra en la ley de Fitts
([accesibilidad.md](accesibilidad.md) y [evaluar.md](evaluar.md)).
**No aplica o choca con:** con la densidad: poner todas las acciones junto a cada elemento repite ruido
en cada fila. Ahí entra el desbordamiento, para lo secundario.
**Fuente:** NN/g, Kaplan (2025), pautas 2 y 3.
**Confianza:** media.

### Ninguna acción vive solo en un sitio oculto
**Dice:** el menú contextual, la pulsación larga, el gesto y el paso del ratón están ocultos por
defecto. Sirven de atajo, pero cada acción que esté en ellos tiene que estar también en un sitio
visible. Las acciones principales y frecuentes no van en menús.
**Se aplica:** por cada acción, ¿hay un camino visible, sin ratón, que llegue a ella? ¿Alguna tarea
principal está detrás de un menú?
**Se mide:** con Playwright: recorrer la vista solo con teclado, y en una emulación táctil, y comprobar
que cada acción de la tabla de tareas es alcanzable.
**No aplica o choca con:** con la limpieza visual: lo visible ocupa sitio. La revelación progresiva
resuelve lo raro; lo frecuente se queda a la vista.
**Fuente:** Apple HIG, *Context menus*; NN/g, Kaplan (2025), pautas 1, 3 y 8; Nielsen (1994),
heurística 6.
**Confianza:** alta.

## Principios

### Esquemas de organización
**Dice:** hay esquemas exactos (alfabético, cronológico, geográfico), que dividen sin solaparse y sirven
cuando el usuario sabe qué busca. Y hay esquemas ambiguos (por tema, por tarea, por público, por
metáfora), que sirven cuando no lo sabe, pero cuyas categorías se pueden discutir. Mezclar varios en el
mismo nivel confunde.
**Se aplica:** por cada vista con una colección, ¿qué esquema ordena los elementos? ¿Es el mismo en
todo el nivel?
**Se mide:** a ojo: en un mismo menú o lista no conviven dos esquemas (por ejemplo, unas entradas por
tema y otras por público).
**No aplica o choca con:** un esquema híbrido puede funcionar si cada nivel usa uno solo.
**Fuente:** Rosenfeld, Morville y Arango (2015), cap. 6.
**Confianza:** media (consenso de la práctica).

### El rastro de la información
**Dice:** el usuario decide dónde pulsar estimando qué hay detrás a partir de lo que ve: la etiqueta, el
icono, el contexto. Es el «olor» de la información (*information scent*). Con un rastro claro y menús
amplios, el usuario navega más y busca menos; Katz y Byrne midieron que, con menús amplios y etiquetas
concretas, se usó la búsqueda en menos del 10 % de los intentos.
**Se aplica:** cada etiqueta de navegación anuncia lo que hay detrás con las palabras del usuario. Se
lee la etiqueta sola, sin la pantalla de destino: ¿se adivina qué hay?
**Se mide:** a ojo, con esa prueba. Un recorrido cognitivo ([evaluar.md](evaluar.md)) lo comprueba paso
a paso.
**No aplica o choca con:** choca con la brevedad: una etiqueta más larga puede tener mejor rastro.
**Fuente:** Pirolli y Card (1999); Katz y Byrne (2003).
**Confianza:** alta.

### Buscar o navegar
**Dice:** la búsqueda sirve cuando el usuario sabe cómo se llama lo que quiere y el conjunto es grande.
Pero escribir la consulta exige recordar, no reconocer. Katz y Byrne no encontraron que la búsqueda
fuera más rápida ni más precisa que navegar, y concluyen que no compensa una navegación mal hecha.
**Se aplica:** ¿la tarea es encontrar un elemento conocido por su nombre (búsqueda), o explorar sin
saber qué hay (navegación)? Si las dos, la navegación tiene que funcionar sola.
**Se mide:** por tarea principal, si se completa sin escribir nada.
**No aplica o choca con:** en colecciones muy grandes de elementos con nombre (contactos, archivos), la
búsqueda es la vía principal.
**Fuente:** Katz y Byrne (2003); NN/g, Budiu (2014), *Recognition and Recall*.
**Confianza:** alta.

### Anchura frente a profundidad
**Dice:** a igualdad de rastro, una estructura ancha y poco profunda suele rendir mejor que una estrecha
y profunda. Pero la más ancha no siempre gana: Larson y Czerwinski encontraron que una intermedia
superaba a la más plana. Cada nivel extra es una decisión más en la que equivocarse.
**Se aplica:** ¿cuántos niveles hay hasta cada tarea principal? Si son más de dos, ¿se puede aplanar
sin perder el rastro?
**Se mide:** número de niveles hasta cada tarea principal; número de opciones por nivel.
**No aplica o choca con:** con la superficie: en una superficie pequeña no caben muchas opciones a la
vez. Y con la claridad: una lista de cuarenta opciones sin agrupar tampoco tiene buen rastro.
**Fuente:** Larson y Czerwinski (1998); Landauer y Nachbar (1985).
**Confianza:** alta. Ver el mito de los tres clics, abajo.

### Revelación progresiva
**Dice:** lo frecuente se enseña de entrada y lo avanzado o raro se deja para un segundo nivel. El hecho
de que algo esté en la vista inicial ya le dice al usuario que es importante. Hay que acertar con el
reparto y el paso al segundo nivel tiene que ser evidente. Más de dos niveles de revelación suelen
funcionar mal.
**Se aplica:** el reparto sale de la [casilla](entender.md#frecuencia-frente-a-importancia) de cada
tarea: lo raro y poco importante va al segundo nivel. El control que lo abre dice qué hay detrás.
**Se mide:** número de niveles de revelación (máximo dos); ninguna tarea principal en el segundo nivel.
**No aplica o choca con:** con reconocer mejor que recordar: lo escondido no se reconoce. Si una
función rara pero crítica queda escondida, el usuario no la encuentra cuando la necesita.
**Fuente:** NN/g, Nielsen (2006), *Progressive Disclosure*.
**Confianza:** media (consenso de la práctica).

### Reconocer mejor que recordar
**Dice:** reconocer algo que se ve es más fácil que recordarlo sin pistas. Las opciones, los objetos y
las acciones tienen que estar a la vista o ser fáciles de recuperar. El usuario no tiene que llevar
información de una vista a otra en la cabeza.
**Se aplica:** ¿alguna tarea obliga a recordar algo de otra vista (un nombre, un código, dónde estaba
una opción)? ¿Hay acciones que solo existen como gesto o atajo, sin nada visible?
**Se mide:** a ojo, recorriendo cada tarea principal; iconos sin etiqueta en la navegación.
**No aplica o choca con:** con la revelación progresiva y con la densidad. Los atajos para expertos
están bien si además hay un camino visible.
**Fuente:** Nielsen (1994), heurística 6; NN/g, Budiu (2014).
**Confianza:** alta.

### La ley de Hick, con sus límites
**Dice:** el tiempo de elegir entre varias opciones igual de probables crece con el logaritmo de su
número. **Pero solo vale cuando el usuario ya sabe qué opción corresponde a qué** (una relación
practicada entre estímulo y respuesta). En un menú que hay que leer, el usuario novato busca con la
vista, y ese tiempo crece de forma lineal con el número de opciones. Hick solo describe al experto.
**Se aplica:** no se usa Hick para justificar «pocas opciones» en una vista que se lee. Se usa para lo
que sí predice: en menús que el usuario conoce, unas pocas opciones de más cuestan poco, y el orden
(por frecuencia o alfabético) y la agrupación ayudan más que recortar.
**Se mide:** con el modelo de Cockburn et al.: búsqueda visual lineal para el novato, Hick para el
experto, Fitts para apuntar. En la práctica, a ojo: ¿el usuario de esta vista es novato o experto?
**No aplica o choca con:** no es un mito, pero se cita mal. Ver «Hick prueba que menos opciones es
mejor» en los mitos.
**Fuente:** Hick (1952); Hyman (1953); Cockburn, Gutwin y Greenberg (2007); Seow (2005).
**Confianza:** alta (sobre sus límites).

### Superficie pequeña
**Dice:** en una superficie pequeña caben menos niveles visibles a la vez, menos opciones y un solo
panel. Las guías de plataforma coinciden: por debajo de 600 dp de ancho, una lista-detalle pasa a un
solo panel, y con poca altura los dos paneles no son prácticos. Un popup de extensión no pasa de 800 ×
600 px en Chrome ni en Firefox; lo que no cabe, se desplaza.
**Se aplica:** se decide primero la superficie más pequeña que hay que servir. En ella: una tarea
principal por vista, la prioridad de la tabla de tareas aún más estricta, acordeones antes que
pestañas, y la navegación que no se coma la altura útil.
**Se mide:** con Playwright, renderizar cada variante al tamaño real de la superficie y medir qué
queda visible sin desplazar: ¿está la tarea principal?
**No aplica o choca con:** con la anchura: en poco espacio, aplanar obliga a desplazar. Hay que elegir
entre otro nivel o una lista más larga, y la elección depende de la frecuencia de la tarea.
**Fuente:** Android, *Use window size classes*; Chrome, `browserAction` (límite del popup); NN/g,
Sunwall (2024).
**Confianza:** alta en los límites técnicos; media en la recomendación de diseño.

## Mitos

| Creencia | Qué dice la evidencia | Fuente |
|---|---|---|
| «Todo tiene que estar a tres clics» | En 44 usuarios y 620 tareas, ni el éxito ni la satisfacción caían a partir del tercer clic. Lo que cuenta es si cada paso tiene buen rastro | Porter (2003) |
| «No más de 7 ± 2 opciones en un menú» | Miller habló de memoria a corto plazo, y las opciones visibles se reconocen, no se recuerdan | Miller (1956); NN/g, Budiu (2014) |
| «Hick prueba que menos opciones es mejor» | Hick solo describe a usuarios que ya saben qué opción quieren; para el novato, la búsqueda visual es lineal | Cockburn et al. (2007) |
| «Si la navegación es mala, la búsqueda lo arregla» | La búsqueda no fue más rápida ni más precisa | Katz y Byrne (2003) |
