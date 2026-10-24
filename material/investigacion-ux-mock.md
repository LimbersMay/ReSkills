# Investigación: `ux:mock`

Respuestas a las preguntas de [brief-ux-mock.md](brief-ux-mock.md), del 2026-10-23. No escribe la ruta
ni la skill: dice qué decisión toma cada respuesta y qué cambia en el borrador de la ruta
(`README-retomar.md`, «La ruta propuesta»).

**Cómo leer las fuentes.** Al lado de cada una se dice cómo se comprobó:
- **original:** leído el texto del autor;
- **resumen fiable:** leído en una fuente seria que lo resume con datos (MeasuringU, NN/g, un libro);
- **secundaria:** solo en apuntes o reseñas. Lo que se apoya solo en estas lleva confianza más baja.

Las referencias de v0.3.1 (`plugins/ux/references/`) se consultaron donde la pregunta lo pedía y se
citan por archivo. **El 2026-10-23 se retiraron del plugin**, porque `ux` se rehace desde cero. Siguen en
el tag: `git show v0.3.1:plugins/ux/references/metodo.md`. Las fuentes que se citan desde ellas hay que
verificarlas antes de usarlas en la ruta.

## Resumen

| Pregunta | Respuesta corta | Confianza |
|---|---|---|
| P1. Fases | Hay consenso en el ciclo: entender el uso → fijar requisitos medibles → diseñar → evaluar contra ellos → repetir hasta cumplirlos. Cada prototipo responde preguntas escritas de antemano. La primera vuelta busca *el diseño correcto*; las siguientes, *hacerlo bien* | alta (el ciclo); media (las dos clases de vuelta) |
| P2. Fidelidad | La fidelidad baja encuentra casi los mismos problemas que la alta. La alta solo hace falta para el tiempo, la estética y lo que la baja no puede simular. Cada vuelta dice qué dimensiones del prototipo están «encendidas» | alta (problemas); media (la regla por dimensión) |
| P3. Anclaje | Varias alternativas a la vez dan mejores resultados y una crítica más dura que una sola. No hay estudio sobre su tamaño: alternativas por decisión, de 2 a 3, mostradas juntas | alta (paralelo); baja (tamaño) |
| P4. Prueba sin usuarios externos | Ningún método basta solo. El autor detecta los fallos graves pero subestima los de aprendizaje; el recorrido cognitivo cubre esos; una IA que recorre la interfaz es «demasiado buena» y ve menos fallos. La IA registra hallazgos, no veredictos | media |
| P5. Cuándo parar | Al menos dos vueltas con prueba; los rendimientos bajan con cada una. Se para cuando una vuelta completa no pide cambios y el usuario aprueba. El tope es una decisión justificada, no un dato | media (mínimo); baja (tope) |
| P6. Skills | La guía oficial es clara y se resume en reglas. Se evalúa sin subagentes con sesiones nuevas de Claude Code y, para lo no interactivo, con `claude plugin eval` en serie y con tope de coste | alta (guía); media (cómo evaluar una skill interactiva) |

---

## P1. ¿Qué fases tiene el prototipado y cuándo termina cada una?

**Decide:** los pasos de la skill y su criterio de salida.

### Respuesta

1. **El ciclo tiene consenso.** ISO 9241-210 describe cuatro actividades que se repiten: entender y
   especificar el contexto de uso, especificar los requisitos del usuario, producir soluciones de
   diseño y evaluarlas contra esos requisitos. Se itera «donde haga falta» hasta que la solución
   cumple los requisitos. Nielsen (1993) llega a lo mismo desde la práctica: diseñar, probar,
   corregir y volver a probar.
2. **Cada prototipo responde preguntas escritas antes de hacerlo.** Houde y Hill (1997) separan tres
   clases de pregunta: el *papel* (para qué le sirve al usuario), el *aspecto y la sensación* (qué ve
   y qué hace) y la *implementación* (cómo funciona por dentro). «Ser explícito sobre qué preguntas de
   diseño hay que responder es una ayuda esencial para decidir qué prototipo construir.» Recomiendan
   decir a quien lo ve **qué explora el prototipo y qué no**, porque el prototipo no comunica solo su
   propósito.
3. **Hay dos clases de vuelta.** Buxton (2007) pone el boceto y el prototipo en un mismo continuo:
   primero se dibuja para encontrar *el diseño correcto* (barato, varias opciones, explorar); después
   se prototipa para *hacer bien el diseño* (refinar, probar, resolver). El título de Tohidi et al.
   (2006), «Getting the right design and the design right», es esa misma distinción, con experimento.
4. **Prototipos enfocados, y se tiran.** Houde y Hill: en las fases tempranas puede ser imposible un
   prototipo integrado; hay que elegir prototipos enfocados y estar dispuesto a tirar algunos.

Con eso, la secuencia de `ux:mock` queda así. Cada fase tiene entrada, salida y quién decide:

| Fase | Entra | Sale (criterio de fin) | Decide |
|---|---|---|---|
| 0. Preparar | Requisitos aprobados, quick design | Lista de tareas con prioridad y, para cada una, qué cuenta como éxito | El usuario aprueba la lista |
| 1. Plan de la vuelta | Tareas, hallazgos de la vuelta anterior | 1–3 preguntas de la vuelta, tareas que se prueban, qué está fuera | El usuario aprueba el plan |
| 2. Construir | Plan, quick design o versión anterior | Prototipo donde todas las tareas del plan se pueden hacer de principio a fin, y las comprobaciones automáticas pasan | La IA (comprobable) |
| 3. Probar | Prototipo, tareas sin pistas | Tabla de hallazgos con sitio y gravedad | El usuario hace; la IA anota |
| 4. Decidir | Hallazgos | Cada hallazgo grave tiene arreglo o alternativa; cada decisión, su porqué | El usuario elige |
| 5. ¿Otra vuelta? | Hallazgos, número de vuelta | Ver P5 | El usuario, con el criterio delante |
| 6. Cerrar | Versión aprobada, registro de decisiones | `docs/ux.md` | El usuario aprueba |

### Fuentes
- ISO 9241-210:2019. *Human-centred design for interactive systems*. **Secundaria:** la norma es de
  pago; las cuatro actividades y «hasta que cumple los requisitos» se comprobaron en varias fuentes
  que la resumen (Maguire, 2013; apuntes de cursos). La ficha oficial dice que se revisó y confirmó en
  2025. https://www.iso.org/standard/77520.html
- Houde, S. y Hill, C. (1997). What do prototypes prototype? En *Handbook of Human-Computer
  Interaction* (2.ª ed.). **Original.** https://creativetech.mat.ucsb.edu/readings/Prototypes_prototype.pdf
- Buxton, B. (2007). *Sketching User Experiences*. Morgan Kaufmann. **Secundaria** (reseña de
  UXmatters y apuntes); la lista de atributos del boceto no se pudo comprobar.
  https://www.uxmatters.com/mt/archives/2007/10/book-review-sketching-user-experiences.php
- Tohidi, M., Buxton, W., Baecker, R. y Sellen, A. (2006). Getting the right design and the design
  right. *CHI 2006*. Ya en [metodo.md](../plugins/ux/references/metodo.md).
- Nielsen, J. (1993). Iterative user-interface design. *IEEE Computer*, 26(11), 32–41. **Original**
  (versión en NN/g). https://www.nngroup.com/articles/iterative-design/

**Confianza:** alta para el ciclo (norma y práctica coinciden); media para separar la primera vuelta de
las demás (Buxton y Tohidi, sin un estudio que compare las dos formas de empezar).

### Qué cambia en el borrador
- **Nueva fase 0:** las tareas no «entran» hechas. Se escriben con su criterio de éxito y el usuario
  las aprueba. Es la parte «requisitos medibles» de ISO, y sin ella P5 no tiene con qué medir.
- **El plan de la vuelta dice también qué queda fuera** (Houde y Hill).
- **La vuelta 1 es distinta:** busca el diseño correcto. Las siguientes lo refinan. Ver P3.
- Cada fase lleva un criterio de fin comprobable, como en la tabla.

---

## P2. ¿Qué fidelidad conviene para cada pregunta?

**Decide:** qué genera la IA en cada vuelta: detalle, grises o color, contenido real, cuánta interacción.

### Respuesta

1. **Baja y alta fidelidad encuentran casi los mismos problemas.** Virzi, Sokolov y Karis (1996), con
   dos productos y 20 personas cada uno: el papel encontró 32 de 38 problemas y el producto real 34 de
   38; en el segundo, 20 de 21 frente a 19 de 21. Las diferencias no fueron significativas.
   Concluyen que la baja fidelidad sirve «durante todo el ciclo», no solo al principio. MeasuringU
   resume once estudios entre 1990 y 2013 con el mismo resultado (Walker, Takayama y Landay, 2002;
   Catani y Biers, 1998; Sauer et al., 2010…).
2. **Lo que la baja fidelidad no da:**
   - **El tiempo:** predice mal cuánto tarda la tarea. Mide mejor la eficiencia en pasos (pasos ideales
     entre pasos dados) (Sauer y Sonderegger, 2009, vía MeasuringU).
   - **La estética:** las valoraciones de aspecto no se trasladan al producto final.
   - **Lo que no simula:** en Virzi et al., dos problemas solo salieron en alta fidelidad porque el
     prototipo de papel manejaba esa función de otra forma. Lo que no funciona en el prototipo no se
     prueba.
   - **La preferencia:** la gente prefiere el prototipo más acabado (Sefelin et al., 2003), sin que
     eso cambie los problemas que encuentra.
3. **El aspecto cambia el juicio de usabilidad.** Con dos móviles idénticos en función y distintos en
   aspecto, el atractivo se valoró como más usable (Sonderegger y Sauer, 2010). Es un argumento para
   los grises mientras se decide la estructura: el color atractivo infla la nota, y el feo la hunde,
   sin que cambie la estructura.
4. **La fidelidad no es una sola cosa.** Lim, Stolterman y Tenenberg (2008) separan lo que el
   prototipo *filtra* en cinco dimensiones: **aspecto, datos, funcionalidad, interactividad y
   estructura espacial**. Su principio económico: «el mejor prototipo es el que, de la forma más
   simple y eficiente, hace visibles y medibles las posibilidades y los límites de una idea». Houde y
   Hill añaden que el acabado engaña: un prototipo pulido parece casi terminado aunque no lo esté.

La regla para `ux:mock`, por dimensión:

| Dimensión | En el prototipo | Por qué |
|---|---|---|
| Aspecto | **Apagado:** grises, una tipografía, sin iconos de marca | El aspecto sesga el juicio de usabilidad; se decide en `ux:polish` |
| Datos | **Encendido:** contenido real o realista, con casos raros (nombres largos, listas vacías, cientos de elementos) | Los problemas de contenido solo salen con contenido |
| Funcionalidad | **Solo la de las tareas del plan**, simulada si hace falta | Lo que no funciona no se prueba (Virzi) |
| Interactividad | **Encendida** para las tareas: clics, navegación, estados como comportamiento | Las tareas se tienen que poder hacer |
| Estructura espacial | **Encendida:** es la pregunta principal | Es lo que decide `ux:mock` |

### Fuentes
- Virzi, R. A., Sokolov, J. L. y Karis, D. (1996). Usability problem identification using both low-
  and high-fidelity prototypes. *CHI '96*. **Original.**
  https://chi1996.acm.org/proceedings/papers/Virzi/RAVtext.html
- Sauro, J. Does the fidelity of a prototype affect results? MeasuringU. **Resumen fiable** de once
  estudios, entre ellos Walker, Takayama y Landay (2002), *HFES 46*, 661–665, que no se pudo leer en
  el original. https://measuringu.com/prototype-fidelity/
- Lim, Y.-K., Stolterman, E. y Tenenberg, J. (2008). The anatomy of prototypes. *ACM TOCHI*, 15(2).
  **Original.** https://faculty.washington.edu/jtenenbg/publications/limAnatomyOfPrototypes-tochi2008.pdf
- Sonderegger, A. y Sauer, J. (2010). The influence of design aesthetics in usability testing.
  *Applied Ergonomics*, 41, 403–410. **Secundaria** (resumen). Nota: otro trabajo de los mismos autores
  da el efecto contrario en el tiempo de tarea; aquí solo se usa el efecto en la valoración, que
  coincide en los dos. https://sonar.ch/documents/302271/files/Sonderegger_Sauer2010.pdf
- Houde y Hill (1997), arriba.

**Confianza:** alta en que la baja fidelidad encuentra los mismos problemas (estudios replicados, pero
de los años 90 y 2000, con papel frente a pantalla); media en la tabla por dimensión, que aplica un
marco y no un experimento.

### Qué cambia en el borrador
- **Se confirma** «en grises, con contenido real y los estados como comportamiento».
- **Se precisa:** el plan de cada vuelta dice qué dimensiones van encendidas. Si una vuelta pregunta
  por una funcionalidad, esa se implementa de verdad; si no, se simula.
- **No se mide el tiempo** en el prototipo: se mide si se completa la tarea, los errores, las dudas y
  los pasos frente a los ideales.
- **No se pregunta al usuario si le gusta** el prototipo: su opinión estética no vale en grises y su
  preferencia por lo acabado no indica nada.

---

## P3. ¿Cómo se itera sobre un diseño que ya existe sin quedarse anclado?

**Decide:** cuándo se hacen alternativas, cuántas y de qué tamaño.

### Respuesta

1. **Varias a la vez es mejor que una tras otra.** En Dow et al. (2010), con el mismo tiempo, quienes
   hicieron tres prototipos, recibieron crítica, hicieron dos más y después el final superaron a
   quienes hicieron los cinco en serie: más clics reales, mejor valoración experta, más variedad. La
   explicación de los autores: comparar críticas entre varias opciones y separar la crítica de la
   persona. Nielsen y Faber (1996): la mezcla de cuatro diseños en paralelo rindió más que iterar el
   mejor solo (170 frente a 156, con la media de los originales en 100).
2. **Con una sola opción, la crítica es blanda.** Quien ve un diseño solo lo puntúa más alto y lo
   critica menos que quien lo ve junto a otros dos. Pero los participantes señalan problemas, no
   proponen soluciones (Tohidi et al., 2006).
3. **Iterar una sola versión ancla.** Quien ve un ejemplo repite sus rasgos, también los malos
   (Jansson y Smith, 1991). Con imágenes de IA, la fijación en el primer ejemplo aumenta
   (Wadinambiarachchi et al., 2024). El quick design es justo eso: un ejemplo hecho con IA. Avisar
   «no te ancles» funciona poco (Vasconcelos et al., 2018). Todo esto ya está en
   [metodo.md](../plugins/ux/references/metodo.md).
4. **No hay estudio sobre el tamaño de las alternativas.** Los experimentos usan artefactos pequeños
   y completos (anuncios, un control de clima). Que las alternativas vayan por decisión y no por
   estructura entera se justifica con otras piezas: los prototipos enfocados de Houde y Hill, la
   dimensión *alcance* de Lim et al., las preguntas de diseño de QOC (MacLean et al., 1991) y el
   coste del intento 1.
5. **La IA no da mucha variedad sola.** Pedir varias en un mismo contexto, distintas entre sí, da más
   variedad que pedirlas por separado (Meincke et al., 2024; Zhang et al., 2025, en metodo.md).

### Fuentes
- Dow, S. P. et al. (2010). Parallel prototyping leads to better design results, more divergence, and
  increased self-efficacy. *ACM TOCHI*, 17(4). **Resumen fiable** (Human Factors International) más
  el resumen de metodo.md; el PDF de Stanford no se pudo abrir.
  https://www.humanfactors.com/newsletters/parallel_prototyping.asp
- Tohidi et al. (2006); Nielsen y Faber (1996); Jansson y Smith (1991); Wadinambiarachchi et al.
  (2024); Vasconcelos et al. (2018); Meincke et al. (2024); Zhang et al. (2025): ver
  [fuentes.md](../plugins/ux/references/fuentes.md).
- MacLean, A. et al. (1991). Questions, Options, and Criteria. Ver fuentes.md.
- Pista sin comprobar: *Inkspire* (CHI 2025) dice que las herramientas de imagen por IA llevan a
  fijarse en vez de explorar. https://doi.org/10.1145/3706598.3713397

**Confianza:** alta en que el paralelo mejora el resultado y la crítica (experimentos controlados, con
la salvedad de que eran novatos y artefactos pequeños); baja en el tamaño y el número exacto.

### Qué cambia en el borrador
- **La vuelta 1 lleva alternativas siempre, no solo «si hay duda».** Para las 1 o 2 decisiones de
  estructura más grandes (por ejemplo, cómo se navega o dónde vive la acción principal), la respuesta
  del quick design y 1 o 2 respuestas distintas, en bocetos baratos. Se enseñan juntas. Motivo:
  con una sola opción el usuario la aprueba sin criticarla (Tohidi), y el quick design ancla.
- **En las vueltas siguientes**, alternativas solo cuando una decisión queda en duda, como decía el
  borrador.
- **De 2 a 3 por decisión, contando la del quick design.** Las alternativas se piden juntas y deben
  diferir en la decisión, no en el aspecto.
- **El usuario señala problemas; la IA propone arreglos.** Tohidi: ver alternativas sirve para
  encontrar fallos, no para que el usuario rediseñe.
- **Se retira lo de esconder el mock** (metodo.md, pasos 4 y 6). El quick design es la base.

---

## P4. ¿Cómo se prueba cuando el único usuario es el autor?

**Decide:** la fase de prueba: quién hace qué, qué se anota y qué se mide.

### Respuesta

Lo que detecta y lo que no detecta cada método:

| Método | Detecta | No detecta, o su límite | Fuente |
|---|---|---|---|
| **El autor hace las tareas** | Los fallos en los que tropieza hasta quien conoce el producto: suelen ser graves | Subestima lo que le cuesta a alguien nuevo. Pensar en cómo aprendió él no lo corrige | Hinds (1999) |
| **Recorrido cognitivo** (como alguien que lo usa por primera vez, paso a paso) | Los problemas de aprendizaje: ¿verá la acción?, ¿la entenderá?, ¿sabrá que avanzó? | La eficiencia del uso diario; es inspección, no uso real | Wharton et al. (1994), en [evaluar.md](../plugins/ux/references/evaluar.md) |
| **Evaluación heurística** | Problemas frecuentes conocidos (estado visible, consistencia, errores…) | Un solo evaluador encuentra entre el 20 % y el 51 % | Nielsen y Molich (1990), en evaluar.md |
| **Una persona cercana** | Lo que el autor no ve: de media, una persona encuentra en torno a un 31 % de los problemas, con mucha variación | Hace falta tenerla; una sola es poco | Nielsen y Landauer (1993) |
| **Comprobaciones automáticas** | Que cada tarea se puede hacer, que cada estado se alcanza, barreras básicas de accesibilidad | No dicen nada de si se entiende | Playwright, axe (evaluar.md, accesibilidad.md) |
| **La IA recorriendo la interfaz** | Fallos que las personas pasan por alto | Es «demasiado buena»: completa más tareas que las personas, va por el camino óptimo y ve menos puntos de fallo. Con más instrucciones se acerca a las personas | Zhong et al. (2025, preprint) |

Además:
1. **Las tareas no llevan pistas.** Se escriben como un objetivo realista, sin nombrar botones ni usar
   las palabras de la interfaz, y con los datos necesarios (McCloskey, 2014, NN/g).
2. **Se observa sin guiar.** La IA da la tarea y no explica la interfaz. Si el usuario pregunta,
   se anota como hallazgo.
3. **La IA no juzga su propio trabajo.** Un modelo prefiere lo que generó, aunque lo juzgue en otra
   llamada (Panickssery et al., 2024), y en pares acierta casi al azar salvo que la diferencia sea
   grande (Wu et al., 2024). Ya está en [metodo.md](../plugins/ux/references/metodo.md#aislar-al-que-evalúa):
   la IA registra **hallazgos con sitio**, no veredictos; lo medido pesa más que lo juzgado; y elige el
   usuario.
4. **No toda evaluación ayuda al principio.** Greenberg y Buxton (2008): una prueba de usabilidad
   hecha por norma, demasiado pronto, puede matar ideas buenas que aún no están resueltas. En la
   vuelta 1 la pregunta es qué diseño, no cuántos errores tiene.

### Fuentes
- Hinds, P. J. (1999). The curse of expertise. *Journal of Experimental Psychology: Applied*, 5(2).
  **Secundaria** (resúmenes que coinciden); el original no se leyó.
- Nielsen, J. y Landauer, T. K. (1993). A mathematical model of the finding of usability problems.
  *INTERCHI '93*, 206–213. **Secundaria**; el 31 % es una media de once estudios y otros trabajos dan
  cifras mucho más bajas (Spool y Schroeder, 2001).
- Zhong, R., McDonald, D. W. y Hsieh, G. (2025). Synthetic cognitive walkthrough. Preprint, arXiv
  2512.03568. **Original** (resumen del artículo). https://arxiv.org/abs/2512.03568
- McCloskey, M. (2014). Turn user goals into task scenarios for usability testing. NN/g. **Original.**
  https://www.nngroup.com/articles/task-scenarios-usability-testing/
- Greenberg, S. y Buxton, B. (2008). Usability evaluation considered harmful (some of the time).
  *CHI 2008*, 111–120. **Secundaria** (resumen y comentarios).
  https://prism.ucalgary.ca/items/02f50447-4c66-4263-9d42-0b8e420f6169/full
- Wharton et al. (1994); Nielsen y Molich (1990); Panickssery et al. (2024); Wu et al. (2024): ver
  fuentes.md.
- Pista: UXAgent (CHI EA 2025) simula usuarios con agentes; sus autores dicen que no sustituye a las
  personas y que el comportamiento «no es como el de personas reales».
  https://arxiv.org/abs/2502.12561

**Confianza:** media. Cada pieza tiene respaldo, pero no hay un estudio de la combinación «autor + IA»,
y los trabajos sobre IA son recientes y varios sin revisar.

### Qué cambia en el borrador
- **La prueba tiene tres partes, en este orden:**
  1. **El usuario hace las tareas** sin pistas. La IA anota dónde duda, se equivoca, vuelve atrás o
     pregunta.
  2. **La IA hace un recorrido cognitivo** de cada tarea, como alguien que la usa por primera vez,
     para cubrir lo que el autor no ve. Deja hallazgos con sitio y gravedad, sin veredicto.
  3. **Comprobaciones automáticas** con Playwright: que cada tarea se completa de principio a fin y
     que cada estado (vacío, error, cargando) se alcanza. axe solo como suelo, no como pulido.
- **Opcional y recomendado:** una persona cercana hace las mismas tareas una vez, por ejemplo antes de
  aprobar. La skill lo ofrece; no lo exige.
- **Se mide:** tarea completada o no, errores, dudas, pasos frente a los ideales. No el tiempo (P2).
- **La IA no puntúa el diseño ni elige.** Ya estaba en el borrador; se mantiene.
- **El informe dice qué no cubre la prueba:** el autor no es un usuario nuevo.

---

## P5. ¿Cuándo se deja de iterar?

**Decide:** el criterio de aprobación y el tope de vueltas.

### Respuesta

1. **Al menos tres versiones, es decir, dos vueltas.** En cuatro casos, la mejora media fue del 38 %
   por vuelta y del 165 % de la primera versión a la última. Las primeras vueltas dan las mejoras
   grandes y las siguientes, cada vez menos. A veces una vuelta empeora algo, porque un arreglo trae
   problemas nuevos: por eso no basta con una (Nielsen, 1993).
2. **Se para cuando una vuelta no pide cambios.** El método RITE de Microsoft arregla después de cada
   participante, en cuanto el problema y su solución están claros, y comprueba el arreglo con el
   siguiente. En el caso del tutorial de *Age of Empires II*, tras diez participantes con cambios, los
   seis siguientes no pidieron ninguno: eso fue la verificación (Medlock et al., 2002, vía MeasuringU).
3. **El criterio se mide contra los requisitos.** ISO 9241-210 itera hasta que el diseño cumple los
   requisitos del usuario; ISO 9241-11 los mide en eficacia, eficiencia y satisfacción
   ([entender.md](../plugins/ux/references/entender.md)). La gravedad de cada problema, de 0 a 4,
   está en [evaluar.md](../plugins/ux/references/evaluar.md).
4. **No hay un tope respaldado.** Nada fija el número máximo. Hay dos argumentos para ponerlo: los
   rendimientos bajan con cada vuelta y cada una cuesta créditos.

### Fuentes
- Nielsen (1993), arriba. **Original.**
- Medlock, M. C., Wixon, D., Terrano, M., Romero, R. y Fulton, B. (2002). Using the RITE method to
  improve products: A definition and a case study. *UPA 2002*. **Secundaria:** Wikipedia y MeasuringU;
  el original no se leyó. https://measuringu.com/rite-method/
- ISO 9241-210 e ISO 9241-11: ver P1 y fuentes.md.

**Confianza:** media en el mínimo de dos vueltas y en el criterio de «una vuelta sin cambios»; baja en
el tope, que es una decisión.

### Qué cambia en el borrador
- **Criterio de salida, las tres cosas a la vez:**
  1. las preguntas del plan de la vuelta tienen respuesta;
  2. en la prueba, todas las tareas principales se completan sin problemas de gravedad 3 o 4;
  3. **una vuelta de verificación**: la última prueba no pidió cambios de estructura (RITE). Con una
     sola persona que prueba, «no pidió cambios» es la señal de que se ha llegado.

  Con eso delante, aprueba el usuario.
- **Mínimo de dos vueltas con prueba**, aunque la primera salga bien: el arreglo de la vuelta 1 se
  comprueba en la 2.
- **Tope propuesto: cinco vueltas.** Es una decisión, no un dato: dos para el mínimo, dos más para lo
  normal y una de margen. Si se llega al tope sin cumplir el criterio, la skill no sigue sola:
  presenta lo que falla y el usuario elige entre aprobar con pendientes, reducir el alcance o seguir.
- Los problemas de gravedad 1 o 2 no bloquean: se apuntan en `ux.md` para `ux:polish`.

---

## P6. ¿Cómo se escribe y se prueba una buena skill?

**Decide:** la forma del `SKILL.md`, cómo se reparten las referencias y cómo se comprueba la skill sin
subagentes.

### Respuesta

**Reglas de escritura** (guía oficial de Anthropic y de Claude Code, leídas en octubre de 2026):

1. **Corto.** El cuerpo del `SKILL.md`, por debajo de 500 líneas; lo demás, en archivos aparte. Solo
   se escribe lo que Claude no sabe ya. En el `SKILL.md`, **qué hacer, no por qué**: una vez cargado,
   cada línea cuesta en cada turno. El porqué va a las referencias.
2. **Lo importante, arriba.** Al compactar la conversación, Claude Code conserva solo los primeros
   5.000 tokens de cada skill invocada.
3. **La descripción dice qué hace y cuándo usarla**, en tercera persona y con las palabras que diría
   el usuario. La de Claude Code se corta a 1.536 caracteres: lo principal, primero.
4. **Referencias a un solo nivel.** Todas se enlazan desde el `SKILL.md`; una referencia que enlaza a
   otra se lee a medias. Las de más de 100 líneas llevan índice al principio.
5. **Un flujo con pasos y una lista de comprobación** que Claude copia en su respuesta y va marcando.
   Bucles de validación: comprobar → arreglar → repetir.
6. **Libertad según el riesgo:** instrucciones abiertas donde caben varios caminos; un script exacto
   donde un error rompe algo. Las operaciones deterministas (capturas, comprobaciones de Playwright)
   van mejor como scripts que como instrucciones.
7. **Un término por concepto** en toda la skill. Plantillas para lo que debe salir igual (`ux.md`, la
   tabla de hallazgos). Nada que caduque con la fecha.
8. **Sin subagentes:** no usar `context: fork` ni `agent` en el frontmatter, porque ejecutan la skill
   en un subagente. Para una skill que dirige el usuario, `disable-model-invocation: true` evita que
   Claude la lance por su cuenta.

**Cómo se prueba:**

1. **Primero las pruebas, después el texto.** Se hace la tarea sin skill, se anotan los fallos, se
   escriben al menos tres escenarios que los cubran y se mide el punto de partida sin la skill. Luego
   se escribe lo mínimo para pasarlos.
2. **Claude A y Claude B.** Una sesión escribe la skill y **otra sesión nueva** la usa en una tarea
   real. Se observa dónde falla y se vuelve a la primera con lo observado. Claude Code insiste:
   probar en una sesión nueva, porque el contexto de haberla escrito tapa sus huecos. **Una sesión
   nueva no es un subagente:** la abre el usuario, en serie, y cuesta lo de una conversación.
3. **Qué observar:** si lee los archivos en el orden esperado, si se salta referencias, si relee
   siempre el mismo archivo (debería ir en el `SKILL.md`) o si nunca abre otro (sobra).
4. **Automático, con cuidado.** `claude plugin eval` ejecuta cada caso en una sesión sin interfaz,
   aislada, **una tras otra por defecto** (`-j 1`). Controla el coste con `--runs 1`,
   `--ablation none` (sin la comparación sin plugin) y `--max-cost-usd`. Los evaluadores `regex`,
   `tool_used` y `file_exists` no cuestan nada; los que usan un modelo juez, sí. No son subagentes,
   pero cada caso consume del plan: según las reglas del usuario, se pregunta antes de usarlo.
5. **El límite:** `ux:mock` es interactiva (el usuario aprueba, prueba y elige). Una sesión sin
   interfaz solo puede probar los pasos que no esperan al usuario, como preparar las tareas o
   construir el prototipo desde un plan aprobado. El resto se prueba a mano, con Claude A y B.

### Fuentes
- Anthropic. Skill authoring best practices. **Original.**
  https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices
- Claude Code. Extend Claude with skills. **Original.** https://code.claude.com/docs/en/skills
- Claude Code. Test plugins with evals. **Original.** https://code.claude.com/docs/en/plugin-evals

**Confianza:** alta en las reglas (documentación oficial y actual); media en cómo evaluar una skill
interactiva, que la guía no trata.

### Qué cambia en el borrador
- **Se confirma la hipótesis del brief:** pasada a mano primero, `SKILL.md` corto, cada referencia
  pedida por un paso, pruebas antes de escribir.
- **Se añade:** la pasada a mano (paso 5 de «El orden») es el «Claude A» de la guía. Lo que hubo que
  repetir en ella es lo que entra en la skill.
- **Se añade:** al menos tres escenarios de prueba escritos antes del `SKILL.md`, con el resultado
  esperado, y una prueba en una sesión nueva antes de dar la skill por buena.
- **Se añade:** las comprobaciones de Playwright van como script dentro de la skill, no como
  instrucciones.
- **Decisión pendiente:** si se usa `claude plugin eval` para los pasos no interactivos. Cuesta poco
  con las opciones de arriba, pero cuesta.
- **No se usa** el plugin `skill-creator` sin comprobar antes si lanza subagentes.

---

## El borrador de la ruta, con los cambios

Para que se vea junto. Lo nuevo va en **negrita**.

**Fase 1, `ux:mock` (sin sistema de diseño):**
0. **Preparar: tareas con prioridad y criterio de éxito. Las aprueba el usuario.**
1. Plan de la vuelta: **1–3 preguntas**, las tareas que se prueban, **qué queda fuera y qué
   dimensiones del prototipo van encendidas.**
2. Prototipo navegable, en grises, desde el quick design, con contenido real y los estados como
   comportamiento. **En la vuelta 1, de 2 a 3 bocetos para las 1–2 decisiones de estructura más
   grandes, mostrados juntos.**
3. Prueba: **el usuario hace las tareas sin pistas; la IA hace un recorrido cognitivo; Playwright
   comprueba que las tareas se completan y que los estados se alcanzan. Se ofrece probar con una
   persona cercana.** No se mide el tiempo.
4. Refinar: la IA propone arreglos; si una decisión queda en duda, de 2 a 3 bocetos de esa pieza y el
   usuario elige.
5. **Se repite al menos dos veces, hasta que una vuelta no pida cambios y no queden problemas
   graves; tope de cinco, y en el tope decide el usuario.**
6. Sale `docs/ux.md`, con la estructura, los flujos, el porqué de cada decisión **y los problemas
   menores pendientes para el pulido.**

## Las referencias de v0.3.1, a la luz de esto

Solo donde la ruta las toca. No se ha cambiado ninguna.

- **[metodo.md](../plugins/ux/references/metodo.md):** el método en diez pasos (3 a 5 variantes
  completas, esconder el mock, meterlo como una variante más) era el del intento 1 y **choca con la
  ruta nueva**. Sus principios siguen valiendo (paralelo, fijación, aislar al que evalúa, QOC), pero
  la tabla de pasos hay que rehacerla o retirarla.
- **[evaluar.md](../plugins/ux/references/evaluar.md):** encaja casi entero en la fase de prueba
  (heurísticas, gravedad, efecto evaluador, recorrido cognitivo, IA como evaluadora). Falta lo de P4
  sobre el autor que prueba y la IA «demasiado buena».
- **[entender.md](../plugins/ux/references/entender.md):** su tabla de tareas sirve para la fase 0.
- **Falta en las referencias:** fidelidad (P2), cuándo parar (P5) y escribir tareas sin pistas (P4).

## Lo que no se pudo contestar

- **ISO 9241-210, el texto de la norma:** es de pago. Se usaron resúmenes.
- **Los originales de** Buxton (2007), Walker et al. (2002), Hinds (1999), Medlock et al. (2002),
  Nielsen y Landauer (1993) y Greenberg y Buxton (2008). Sus cifras salen de resúmenes fiables o de
  fuentes secundarias, y así se marca.
- **El tamaño de las alternativas** (pieza frente a estructura entera): no hay estudio.
- **El tope de vueltas:** no hay dato; queda como decisión.
- **Si una IA que construyó el prototipo puede hacer su recorrido cognitivo sin sesgo.** Lo de que un
  modelo prefiere lo suyo se midió en textos y puntuaciones, no en recorridos que dejan hallazgos con
  sitio.

## Preguntas nuevas (apuntadas, sin perseguir)

1. **¿Cómo ve la IA la prueba del usuario?** Pensar en voz alta pide a alguien que observe, y la IA
   no ve la pantalla. Opciones: el usuario cuenta cada tarea al terminarla; el prototipo registra los
   clics y las vueltas atrás en un archivo; o una traza de Playwright. Se decide al escribir la ruta,
   junto con «cómo se abre el prototipo».
2. **El quick design viene de otra IA.** ¿Trae ya los rasgos típicos de las interfaces generadas, que
   luego se repiten? Afecta a cuánto se fía la vuelta 1 de él.
3. **`/sdd:discover` y las vistas:** resuelta el 2026-10-23. Discover ya separa la necesidad de la
   vista y pasa las vistas del material como hipótesis de interfaz. La fase 0 de `ux:mock` las recibe
   de ahí.
