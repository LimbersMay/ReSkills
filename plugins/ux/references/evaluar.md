# Evaluar sin usuarios

Cómo se juzgan las variantes antes de que las vea nadie. Los métodos de inspección encuentran problemas
probables; no demuestran que una interfaz sea usable. La skill lo dice al presentar los resultados.
Las referencias completas están en [fuentes.md](fuentes.md).

## Principios

### Las heurísticas, como lista de comprobación
**Dice:** las diez heurísticas de Nielsen son una lista de los tipos de problema más frecuentes:
visibilidad del estado, lenguaje del usuario, control y libertad, consistencia, prevención de errores,
reconocer mejor que recordar, flexibilidad, diseño minimalista, ayuda ante los errores y
documentación.
**Se aplica:** cada variante se recorre heurística por heurística. Cada problema se anota con la
heurística que incumple, el sitio exacto (vista, elemento, estado) y su gravedad.
**Se mide:** a ojo, con un criterio: un problema sin sitio exacto no cuenta. Las capturas de Playwright
de cada estado ([estados.md](estados.md)) son el material que se inspecciona.
**No aplica o choca con:** las heurísticas sirven para encontrar problemas, no para elegir entre
variantes; para elegir están los criterios de [metodo.md](metodo.md#preguntas-opciones-y-criterios).
**Fuente:** Nielsen (1994), *10 Usability Heuristics*; Nielsen y Molich (1990).
**Confianza:** media (consenso de práctica).

### La gravedad se pone a cada problema
**Dice:** la escala de Nielsen puntúa cada problema de 0 a 4: 0, no es un problema; 1, cosmético; 2,
menor; 3, grave; 4, catástrofe que impide publicar. La gravedad combina tres cosas: con qué frecuencia
ocurre, cuánto cuesta superarlo y si se repite cada vez. Se puntúa después de la inspección, no durante,
y cada evaluador por su cuenta. La puntuación de un solo evaluador no es fiable; la media de tres basta
para la mayoría de los usos.
**Se aplica:** cada problema lleva su gravedad y una línea sobre frecuencia, impacto y persistencia. Los
de gravedad 3 y 4 se arreglan antes de converger; los de 1 se anotan.
**Se mide:** la tabla de problemas tiene la columna de gravedad, y cada valor lo puntúan al menos dos
pasadas independientes.
**No aplica o choca con:** con puntuar las heurísticas. Dar a cada heurística una nota de 0 a 4 y sumar
sobre 40 no es la escala de Nielsen, que puntúa problemas, y no tiene validación. Sirve, como mucho,
para ver la tendencia de una misma herramienta.
**Fuente:** Nielsen (1994), *Severity Ratings for Usability Problems*.
**Confianza:** media.

### Varios evaluadores, por separado
**Dice:** un evaluador solo encuentra una parte de los problemas: en los experimentos de Nielsen y
Molich, entre el 20 % y el 51 %. Varios evaluadores juntan mucho más. La recomendación es de tres a
cinco, cada uno por su cuenta y sin ver lo de los demás hasta terminar.
**Se aplica:** la evaluación se hace en varias pasadas independientes, cada una en un contexto limpio,
y se juntan al final. Ver [Aislar al que evalúa](metodo.md#aislar-al-que-evalúa).
**Se mide:** cuántas pasadas hubo, y que ninguna vio el resultado de otra antes de terminar.
**No aplica o choca con:** con un agente, varias pasadas del mismo modelo con el mismo prompt se
parecen entre sí más que varias personas; conviene variar el ángulo de cada pasada (heurísticas,
recorrido cognitivo, accesibilidad).
**Fuente:** Nielsen y Molich (1990); Moran y Gordon (2023), *How to Conduct a Heuristic Evaluation*.
**Confianza:** alta (el fenómeno); media (el número de evaluadores).

### El efecto evaluador
**Dice:** evaluadores distintos que miran lo mismo con el mismo método encuentran problemas distintos.
En el estudio de Jacobsen, Hertzum y John, cuatro evaluadores analizaron las mismas sesiones: de 93
problemas, solo el 20 % lo encontraron los cuatro y el 46 % lo encontró uno solo. Los problemas graves
se compartieron más, pero el efecto seguía. La causa principal es que evaluar exige interpretar.
**Se aplica:** que una pasada no encuentre un problema no prueba que no exista. Para encontrar se usa la
unión de todas las pasadas; para priorizar, el acuerdo entre ellas.
**Se mide:** el acuerdo entre cada par de pasadas: problemas en común divididos entre problemas en
total de las dos, y la media de todos los pares. Un acuerdo bajo pide más pasadas, no elegir una.
**No aplica o choca con:** con dar por cerrada una evaluación porque una sola pasada salió limpia.
**Fuente:** Hertzum y Jacobsen (2001); Jacobsen, Hertzum y John (1998).
**Confianza:** alta.

### El recorrido cognitivo, para lo que se usa poco
**Dice:** se recorre una tarea paso a paso, como lo haría alguien que la hace por primera vez, y en cada
paso se responde a cuatro preguntas. ¿Intentará el usuario conseguir el efecto correcto? ¿Verá que la
acción correcta está disponible? ¿La asociará con lo que quiere conseguir? ¿Verá, tras hacerla, que
avanza? Hay una versión de dos preguntas: ¿sabrá el usuario qué hacer en este paso? Si lo hace bien,
¿sabrá que lo hizo bien y que avanza?
**Se aplica:** con cada tarea principal y con cada tarea rara pero importante de la
[tabla de tareas](entender.md#plantilla-de-la-tabla-de-tareas). Es el método adecuado para el uso
infrecuente, donde el usuario siempre es un poco novato.
**Se mide:** con Playwright, se ejecuta la secuencia de acciones y se captura cada paso; cada paso lleva
la respuesta a cada pregunta y, si alguna es «no», un problema con su gravedad.
**No aplica o choca con:** la versión de dos preguntas es más rápida, pero da un análisis más grueso y
no guarda el razonamiento. Ninguna de las dos evalúa la eficiencia del experto.
**Fuente:** Wharton, Rieman, Lewis y Polson (1994); Spencer (2000).
**Confianza:** media.

### KLM para comparar tiempos de experto
**Dice:** el modelo de pulsaciones (KLM) estima cuánto tarda un usuario experto, sin errores, sumando
tiempos estándar: pulsar una tecla o un botón, unos 0,2 s; señalar con el ratón, 1,1 s; llevar la mano
del teclado al ratón, 0,4 s; prepararse mentalmente, 1,35 s.
**Se aplica:** con las tareas frecuentes de la tabla de tareas, para comparar variantes entre sí. La
diferencia entre variantes importa más que el valor absoluto.
**Se mide:** con Playwright, sobre la secuencia de la tarea: contar pulsaciones, movimientos del
puntero y cambios entre teclado y ratón, y sumar. El tiempo de señalar depende de la distancia y el
tamaño ([Fitts](jerarquia.md#ley-de-fitts-tamaño-y-distancia)).
**No aplica o choca con:** no dice nada del aprendizaje, de los errores ni del uso infrecuente. Para eso,
el recorrido cognitivo. Sus tiempos son de teclado y ratón; en táctil cambian, y solo vale contar pasos.
**Fuente:** Card, Moran y Newell (1980).
**Confianza:** media (modelo validado para expertos; los tiempos, comprobados en fuentes secundarias).

### Métricas automáticas: cuáles tienen respaldo

| Métrica | Qué predice | Respaldo | Uso |
|---|---|---|---|
| Contraste, tamaño de objetivo, foco | Barreras de accesibilidad | Norma (WCAG 2.2) | Umbral: se cumple o no ([accesibilidad.md](accesibilidad.md)) |
| Reglas de axe | Una parte de las barreras | Herramienta; cubre una minoría | Necesaria, no suficiente |
| KLM | Tiempo de un experto sin errores | Modelo validado | Comparar variantes |
| Pasos hasta cada tarea principal | Esfuerzo de llegar | Práctica | Comparar variantes |
| Altura hasta el primer dato de la tarea | Si se ve sin desplazar | Datos de atención (Fessenden, 2018) | Comparar; umbral según la superficie ([jerarquia.md](jerarquia.md#la-primera-pantalla)) |
| Opciones visibles a la vez | Tiempo de elegir, solo en expertos | Hick, con límites ([estructura.md](estructura.md#la-ley-de-hick-con-sus-límites)) | Contar, sin umbral fijo |
| Desorden y complejidad visual | Estética y tiempo de búsqueda | Estudios con personas | Comparar variantes, sin umbral ([jerarquia.md](jerarquia.md)) |
| Nota de un modelo de lenguaje | Preferencias humanas, a veces | Débil (ver abajo) | Solo si la diferencia es grande |
| Suma de heurísticas sobre 40 | Nada validado | Ninguno | Tendencia dentro de una misma herramienta |
| «Cuatro opciones como máximo» | Nada | Ninguno (ver [Mitos](#mitos)) | No se usa |

### Lo que no se evalúa sin usuarios
**Dice:** la inspección encuentra problemas probables y deja otros sin ver. No puede decir si las
tareas son las correctas, si los nombres son los del usuario, cuánto se usa cada cosa ni si gusta.
**Se aplica:** el informe separa lo comprobado (con herramienta o con norma) de lo inspeccionado (con
juicio) y lo que hace falta probar con personas. Para eso último propone la prueba concreta
([entender.md](entender.md#cuándo-hace-falta-probar-con-personas)).
**Se mide:** a ojo: cada conclusión del informe dice de cuál de los tres tipos es.
**No aplica o choca con:** con presentar la evaluación como una validación.
**Fuente:** ISO 9241-11:2018 (la usabilidad es un resultado del uso, ver
[entender.md](entender.md#las-tareas-antes-que-las-pantallas)); Jacobsen, Hertzum y John (1998).
**Confianza:** alta.

## Plantilla de la tabla de problemas

Cada pasada de evaluación deja una tabla. Las tablas se juntan después, y la gravedad final es la media
de las pasadas que puntuaron cada problema.

```markdown
| # | Variante | Vista y estado | Problema | Heurística o criterio | Método | Gravedad (0–4) | Frecuencia · impacto · persistencia | Comprobado o inspeccionado |
|---|---|---|---|---|---|---|---|---|
| P1 | | | | | heurística · recorrido · herramienta | | | |
```

## Modelos de lenguaje que evalúan interfaces

Lo que dice la investigación desde 2023, para cuando el evaluador es un agente. Varios de estos trabajos
son preprints; se marca cuáles.

- **Útil para errores sutiles y textos, menos con cada ronda.** GPT-4 evaluó 51 interfaces con tres
  conjuntos de pautas, a partir de su descripción en JSON. Fue útil para detectar errores sutiles,
  mejorar los textos y razonar sobre el significado, pero su utilidad bajó con las iteraciones. Falló
  más cuando el JSON no coincidía con lo que se veía, y la heurística de diseño minimalista fue la menos
  precisa (Duan et al., CHI 2024).
- **Aún por debajo de los evaluadores humanos.** Con un conjunto de 3.059 críticas de siete diseñadores
  sobre 983 interfaces, los ejemplos en el prompt y las indicaciones visuales mejoraron un 55 % la
  calidad de las críticas generadas. El punto de partida no igualaba a las personas (Duan et al., UIST
  2024).
- **Elegir la mejor de dos, casi al azar.** Al comparar pares de interfaces por calidad de diseño, los
  modelos grandes de visión acertaron cerca del azar: GPT-4V, un 51,58 %, y se negó a contestar en
  torno al 10 % de los casos. En un ejemplo prefirió la versión con el texto desbordado (Wu et al.,
  UIST 2024).
- **Encuentra más, pero no ve el flujo.** Una evaluación heurística sintética encontró el 73 % y el 77 %
  de los problemas de dos aplicaciones, frente al 57 % y el 63 % de cinco evaluadores con experiencia.
  Fue mejor con los problemas de disposición. Le costó reconocer algunos componentes y convenciones,
  repitió el mismo problema en cada pantalla y no vio bien los que cruzan pantallas (Zhong, McDonald y
  Hsieh, 2025, preprint).
- **Acierta cuando la diferencia es grande.** GPT-4o, Claude y Llama se acercaron a las valoraciones de
  personas en unos factores y no en otros. En las comparaciones por pares, acertaron más cuanto mayor
  era la diferencia que veían las personas (Luera et al., 2025, preprint).
- **Lo que generan falla en accesibilidad e interacción.** Tres modelos de enero de 2025 generaron
  interfaces bien estructuradas, pero con problemas para cumplir las normas de accesibilidad y para
  dar funcionalidad interactiva (Sawicki et al., 2026).
- **Los sesgos del evaluador, también aquí.** El que juzga prefiere lo suyo, se deja llevar por el
  orden y por lo que sugiere quien pregunta. Ver [Aislar al que evalúa](metodo.md#aislar-al-que-evalúa).

**Se aplica:**
- El evaluador mira capturas renderizadas, no solo el código.
- Un flujo de varias pantallas se le da en orden y se le pide que lo evalúe como flujo.
- Su preferencia entre dos variantes cuenta solo si es clara y se mantiene al invertir el orden.
- Nunca evalúa las variantes que generó en el mismo contexto. Aun en otro, el mismo modelo prefiere
  lo suyo: etiquetas neutras, criterios en vez de preferencias, más peso a lo medido y, si se puede,
  otro modelo ([Aislar al que evalúa](metodo.md#aislar-al-que-evalúa)).
- No emite un veredicto global entre variantes; registra hallazgos, y la matriz de Pugh se rellena
  con ellos.
- La accesibilidad y la interacción se miden con herramientas, no se dejan a su juicio.

**Confianza:** media (estudios recientes, varios sin revisar, con modelos que ya han cambiado).

## Mitos

| Creencia | Qué dice la evidencia | Fuente |
|---|---|---|
| «Como mucho cuatro opciones visibles en cada decisión» | Cowan habla de lo que se retiene en la memoria a corto plazo; las opciones a la vista se reconocen, no se retienen | Cowan (2001); Budiu (2014) |
| «Con un buen experto basta» | Un evaluador encontró entre el 20 % y el 51 %; evaluadores distintos encuentran problemas distintos | Nielsen y Molich (1990); Jacobsen et al. (1998) |
| «La suma de heurísticas mide la usabilidad» | La escala de Nielsen puntúa problemas, no heurísticas, y la suma no está validada | Nielsen (1994) |
| «Si un modelo elige una variante, es la mejor» | En pares, cerca del azar salvo que la diferencia sea grande | Wu et al. (2024); Luera et al. (2025) |
