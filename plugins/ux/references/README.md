# Referencias de `ux`

Principios y métodos de UI/UX con su evidencia, para llevar la interfaz de un producto desde sus
requisitos hasta un diseño elegido. Cada principio dice qué afirma, cómo se aplica, cómo se mide, cuándo
no sirve, de dónde sale y con qué confianza.

## Qué archivo sirve en cada momento

| Archivo | Para qué | Pasos del método |
|---|---|---|
| [metodo.md](metodo.md) | El método en diez pasos: abrir variantes, aislar, evaluar, combinar | Todos; se lee primero |
| [entender.md](entender.md) | Tareas, contexto de uso, preguntas para el usuario, tabla de tareas | Antes del paso 1 |
| [estructura.md](estructura.md) | Catálogos de navegación y de acciones; arquitectura de información | 1 y 3 (preguntas y direcciones) |
| [jerarquia.md](jerarquia.md) | Qué manda en cada vista, agrupación, lectura, densidad, Fitts | 4 (construir cada variante) |
| [estados.md](estados.md) | Los estados de cada vista, errores, lo automático, textos | 4 (construir) y 7 (evaluar) |
| [accesibilidad.md](accesibilidad.md) | Lo de WCAG 2.2 AA que cambia el diseño, con su prueba en Playwright | 4 (construir) y 7 (medir) |
| [evaluar.md](evaluar.md) | Heurísticas, gravedad, efecto evaluador, recorrido cognitivo, KLM, métricas, modelos como evaluadores | 7 y 8 |
| [fuentes.md](fuentes.md) | Bibliografía y lo pendiente; no se carga, sirve para comprobar | — |

Los mitos están al final de cada archivo de tema, junto a los principios que los desmienten.

## Orden de lectura para la pasada a mano

1. **metodo.md**, entero. Es el guion de la pasada; los demás archivos se abren desde sus pasos.
2. **entender.md**. Se hacen las preguntas al usuario, primero abiertas, y se rellena la tabla de
   tareas. Sin la tabla no se pasa al paso 1 del método.
3. **estructura.md**. Con la tabla delante, se escriben las preguntas de estructura de cada vista y se
   eligen de 3 a 5 direcciones del catálogo.
4. **jerarquia.md, estados.md y accesibilidad.md**, al construir cada variante. La tabla de estados de
   estados.md dice qué capturas tiene que tener cada variante.
5. **evaluar.md**, al juzgar. Varias pasadas aisladas, con la plantilla de la tabla de problemas.

## Qué poner a prueba en la pasada a mano

Son hipótesis que la investigación deja abiertas o que solo se resuelven con un caso real:

- **Generar las direcciones juntas y construir cada variante aislada** ([metodo.md](metodo.md#decisión-abierta-subagentes)).
  ¿Salen variantes distintas en estructura, o convergen?
- **El mock como una variante más, sin marcar.** ¿El evaluador lo trata igual que a las demás?
- **Las reglas para el evaluador que es un modelo** ([evaluar.md](evaluar.md#modelos-de-lenguaje-que-evalúan-interfaces)):
  capturas en vez de código, flujos en orden, preferencias solo si se mantienen al invertir el orden.
- **La autopreferencia del mismo modelo.** ¿Bastan las etiquetas neutras, los criterios y las medidas,
  o hace falta otro modelo como evaluador?
- **La matriz de Pugh rellena solo con hallazgos.** ¿Quedan celdas sin hallazgo que el usuario quiera
  juzgar él?
- **Las medidas con Playwright.** Cuáles se pueden automatizar sin esfuerzo y cuáles salen tan caras que
  conviene dejarlas a ojo.
- **La tabla de tareas y las preguntas.** ¿Bastan para empezar, o falta algo que el usuario no sabía
  contestar?

## Decisiones abiertas

No se cierran aquí. Lo que dice la investigación de cada una:

| Decisión | Lo que dice la evidencia |
|---|---|
| Nombre final de la skill | Nada. Es una decisión de producto. |
| Si `ux` usa impeccable cuando está instalado | Su crítica aísla al evaluador en subagentes, que tiene respaldo ([metodo.md](metodo.md#aislar-al-que-evalúa)). Pero suma las heurísticas sobre 40, que no está validado, y aplica «≤4 opciones» citando mal a Cowan ([evaluar.md](evaluar.md#mitos)). Si se usa, conviene tomar su aislamiento y no su puntuación. |
| Variantes en subagentes aislados | A favor: la fijación en el ejemplo está bien probada, y avisar no basta. En contra: varios subagentes con el mismo brief convergen en la respuesta típica. Hipótesis: direcciones juntas, construcción aislada ([metodo.md](metodo.md#decisión-abierta-subagentes)). |
| Cómo revisa el usuario las variantes | Quien ve varias a la vez critica más duro y más concreto que quien ve una sola ([metodo.md](metodo.md#mostrar-varias-a-la-vez-mejora-la-crítica)). Eso favorece una vista lado a lado, con los mismos estados de cada variante. Si son capturas o maquetas vivas no lo decide ninguna fuente: depende de si hay que probar la interacción. |

## Lo que faltó

- **Originales no leídos.** Lee y See (2004), con la confianza bajada a media hasta comprobarlo, y varios
  libros de referencia. La lista está en [fuentes.md](fuentes.md#pendiente).
- **Kulkarni et al. (2014)**, sobre cuándo enseñar ejemplos. No se pudo leer el original.
- **Evidencia de que el usuario frecuente rinde con más densidad.** No se encontró un estudio que aísle
  la pericia; queda como práctica, con confianza baja.
- **Modelos como evaluadores.** Varios estudios son preprints de 2025 y usan modelos que ya han
  cambiado. Conviene repasarlos antes de escribir la skill.
- **ISO 9241-110** (principios de diálogo), citada como fuente preferente en el traspaso. No se usó:
  las heurísticas de Nielsen y las pautas de NN/g cubren lo mismo con fuentes accesibles.
