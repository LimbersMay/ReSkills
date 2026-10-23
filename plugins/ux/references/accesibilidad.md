# Accesibilidad

El suelo es WCAG 2.2, nivel AA (recomendación del W3C desde el 5 de octubre de 2023). Aquí están solo
los criterios que cambian una decisión de diseño, y cómo se comprueba cada uno con Playwright. Las
referencias completas están en [fuentes.md](fuentes.md).

## Qué mide una herramienta y qué no

axe se ejecuta dentro de Playwright con `@axe-core/playwright`: `new AxeBuilder({ page })`, se filtra
con `.withTags(['wcag2a', 'wcag2aa', 'wcag21aa', 'wcag22aa'])` y se lanza con `.analyze()`. Se corre en
cada estado capturado ([estados.md](estados.md)), no solo en el inicial.

Una herramienta encuentra una minoría de las barreras. En la prueba del equipo de accesibilidad del
gobierno británico, con 142 barreras puestas a propósito en una página, axe encontró el 29 % y la mejor
herramienta, el 40 % (2017, revisado en 2018). Deque, que hace axe, da un 57 %, pero mide otra cosa: el
volumen de incidencias en sus auditorías, dominado por los tipos más frecuentes. La propia documentación
de Playwright dice que muchos problemas solo aparecen con pruebas manuales.

Por eso cada principio dice cómo se comprueba más allá de axe: con un script de Playwright o a ojo, con
un criterio.

## Principios

### Contraste del texto
**Dice:** el texto tiene un contraste de al menos 4,5:1 con su fondo; el texto grande (18 pt, o 14 pt en
negrita), de 3:1. La cifra no se redondea: 4,49:1 no cumple. El texto de un control inactivo está
exento.
**Se aplica:** la paleta se elige con el contraste ya comprobado, también en los estados de pasar el
ratón, foco, error y seleccionado.
**Se mide:** axe (regla de contraste) en cada estado capturado.
**No aplica o choca con:** que el control inactivo esté exento no lo libra de distinguirse de uno activo
([Desactivado, con el motivo](estados.md#desactivado-con-el-motivo)).
**Fuente:** WCAG 2.2, 1.4.3 (AA).
**Confianza:** alta (norma).

### Contraste de lo que no es texto
**Dice:** los bordes de los controles, los iconos que informan y los indicadores de estado tienen un
contraste de al menos 3:1 con lo que tienen al lado.
**Se aplica:** un campo de texto se distingue del fondo por su borde o su relleno; un icono que es la
única pista de algo cumple el 3:1.
**Se mide:** con Playwright: leer el color calculado del borde o del relleno de cada control y del
fondo que lo rodea, y calcular el contraste.
**No aplica o choca con:** con la agrupación sin cajas ([jerarquia.md](jerarquia.md#región-común)):
lo que agrupa no es un control y no tiene que cumplirlo; lo que se pulsa, sí.
**Fuente:** WCAG 2.2, 1.4.11 (AA).
**Confianza:** alta (norma).

### El color no va solo
**Dice:** el color no es el único medio visual de transmitir información, indicar una acción o
distinguir un elemento.
**Se aplica:** un error lleva icono o texto además del rojo; un enlace dentro de un texto se distingue
por algo más que el color; un estado seleccionado tiene una marca.
**Se mide:** con Playwright: capturar cada estado con un filtro de escala de grises (`filter:
grayscale(1)`) y comprobar que se siguen distinguiendo.
**No aplica o choca con:** nada; es un mínimo.
**Fuente:** WCAG 2.2, 1.4.1 (A).
**Confianza:** alta (norma).

### Tamaño de los objetivos
**Dice:** los objetivos que se pulsan miden al menos 24 × 24 px CSS (AA). Uno más pequeño vale si un
círculo de 24 px de diámetro centrado en él no toca otro objetivo ni el círculo de otro. Están exentos
los enlaces dentro de un texto y los que tienen un equivalente que cumple en la misma página. El nivel
AAA pide 44 × 44. Las plataformas piden más: Apple, 44 × 44 pt; Android, 48 × 48 dp con 8 dp de
separación.
**Se aplica:** 24 px es el suelo en la web; en táctil, se diseña con el tamaño de la plataforma. Las
acciones frecuentes, más grandes ([Fitts](jerarquia.md#ley-de-fitts-tamaño-y-distancia)).
**Se mide:** con Playwright: la caja de cada elemento interactivo visible; los menores de 24 px se
comprueban con la regla del círculo.
**No aplica o choca con:** con la densidad; la regla del círculo permite iconos pequeños si están
separados.
**Fuente:** WCAG 2.2, 2.5.8 (AA) y 2.5.5 (AAA); Apple, *Human Interface Guidelines*; Android, *Touch
target size*.
**Confianza:** alta (norma); media (las cifras de plataforma).

### Todo con el teclado, con el foco a la vista
**Dice:** todo se puede hacer con el teclado. El foco sigue un orden que conserva el sentido, siempre
se ve y no queda tapado del todo por contenido del propio sitio, como una cabecera fija.
**Se aplica:** el orden del foco sigue el orden de lectura. El indicador de foco es visible en todos
los controles. Las cabeceras y barras fijas no tapan el elemento con foco.
**Se mide:** con Playwright: pulsar Tab hasta recorrer la vista, anotar la secuencia de
`document.activeElement` y capturar cada paso. En cada uno, comprobar con `elementFromPoint` en varios
puntos del elemento que al menos uno no lo tapa otro.
**No aplica o choca con:** con las acciones que solo aparecen al pasar el ratón
([estructura.md](estructura.md#ninguna-acción-vive-solo-en-un-sitio-oculto)).
**Fuente:** WCAG 2.2, 2.1.1 (A), 2.4.3 (A), 2.4.7 (AA) y 2.4.11 (AA).
**Confianza:** alta (norma).

### Nombre, rol y estado
**Dice:** cada control tiene un nombre y un rol que el lector de pantalla puede leer, y sus estados
(marcado, desplegado, seleccionado) se exponen. La estructura que se ve (encabezados, listas, grupos,
etiquetas de campos) también existe en el código.
**Se aplica:** los botones de solo icono tienen nombre accesible
([Iconos con etiqueta](estados.md#iconos-con-etiqueta)). Los encabezados siguen la jerarquía visual.
**Se mide:** axe, más la instantánea del árbol de accesibilidad de Playwright (`ariaSnapshot`) de cada
vista: ningún control sin nombre y los encabezados en el orden visual.
**No aplica o choca con:** nada; es un mínimo.
**Fuente:** WCAG 2.2, 1.3.1 (A) y 4.1.2 (A).
**Confianza:** alta (norma).

### Avisos de estado sin mover el foco
**Dice:** los mensajes de estado (guardado, cargando, tres resultados, error) llegan al lector de
pantalla sin que el foco se mueva.
**Se aplica:** cada aviso de la tabla de estados ([estados.md](estados.md#los-estados-de-cada-vista))
se marca con `role="status"` o, si es urgente, `role="alert"`.
**Se mide:** con Playwright: provocar cada estado y comprobar que el texto del aviso está dentro de una
región con esos roles o con `aria-live`.
**No aplica o choca con:** con el ruido: no todo cambio es un aviso
([Visibilidad del estado](estados.md#visibilidad-del-estado-del-sistema)).
**Fuente:** WCAG 2.2, 4.1.3 (AA).
**Confianza:** alta (norma).

### Errores en texto, con sugerencia
**Dice:** el campo con error se identifica y el error se describe en texto. Si se sabe cómo
arreglarlo, se sugiere.
**Se aplica:** con la rúbrica de [Mensajes de error](estados.md#mensajes-de-error).
**Se mide:** con Playwright: enviar datos inválidos y comprobar que el campo tiene `aria-invalid` y
que el texto del error está asociado con `aria-describedby`.
**No aplica o choca con:** cuando sugerir comprometería la seguridad (por ejemplo, decir qué parte de
unas credenciales falló).
**Fuente:** WCAG 2.2, 3.3.1 (A) y 3.3.3 (AA).
**Confianza:** alta (norma).

### Ampliar y reajustar sin perder nada
**Dice:** el texto se puede ampliar al 200 % sin perder contenido ni funciones. A un ancho de 320 px CSS
no hace falta desplazarse en horizontal. Si el usuario aumenta el espaciado (interlineado de 1,5 veces
el tamaño de letra, 2 veces tras cada párrafo, 0,12 entre letras y 0,16 entre palabras), nada se corta.
**Se aplica:** la disposición se piensa también para la superficie más estrecha. Ningún contenedor de
texto tiene alto fijo.
**Se mide:** con Playwright: abrir cada vista a 320 px de ancho y comprobar que `scrollWidth` no supera
`clientWidth`; inyectar ese espaciado con CSS y comprobar que ningún texto se desborda de su caja. Es
la misma prueba que el [estado extremo](estados.md#los-estados-de-cada-vista).
**No aplica o choca con:** con tablas y mapas, que pueden necesitar desplazamiento en dos sentidos.
**Fuente:** WCAG 2.2, 1.4.4 (AA), 1.4.10 (AA) y 1.4.12 (AA).
**Confianza:** alta (norma).

### Sin gestos obligatorios
**Dice:** lo que se hace arrastrando también se puede hacer con un solo clic o toque. El contenido que
aparece al pasar el ratón o al recibir el foco se puede cerrar sin mover el puntero, se puede recorrer y
no desaparece solo.
**Se aplica:** reordenar tiene botones o un menú además del arrastre; los tooltips se cierran con
Escape.
**Se mide:** con Playwright: hacer cada tarea de arrastre solo con clics; abrir cada tooltip y cerrarlo
con Escape.
**No aplica o choca con:** cuando arrastrar es esencial (dibujar a mano alzada).
**Fuente:** WCAG 2.2, 2.5.7 (AA) y 1.4.13 (AA).
**Confianza:** alta (norma).

### Desactivados que se pueden encontrar
**Dice:** el atributo `disabled` saca un control del orden del teclado, y quien usa lector de pantalla
descubre los controles moviendo el foco. En barras de herramientas, menús, pestañas y listas, los
desactivados siguen siendo enfocables con `aria-disabled="true"`.
**Se aplica:** se usa `aria-disabled` cuando el usuario necesita saber que el control existe y por qué
no está disponible ([estados.md](estados.md#desactivado-con-el-motivo)); `disabled`, cuando los
controles de alrededor ya lo dejan claro.
**Se mide:** con Playwright: recorrer con Tab y comprobar que los desactivados con motivo reciben el
foco y anuncian el motivo.
**No aplica o choca con:** un control enfocable que no hace nada tiene que decir por qué, o confunde.
**Fuente:** W3C, *ARIA Authoring Practices Guide*, «Developing a Keyboard Interface».
**Confianza:** media (guía de práctica del W3C, no norma).

### Movimiento reducido
**Dice:** la animación que provoca una interacción se puede desactivar, salvo que sea esencial (AAA).
El sistema operativo expone la preferencia como `prefers-reduced-motion`.
**Se aplica:** toda animación de transición respeta la preferencia: con ella activa, se quita o se
cambia por un fundido.
**Se mide:** con Playwright: `page.emulateMedia({ reducedMotion: 'reduce' })` y comprobar que no hay
animaciones de desplazamiento ni de escala.
**No aplica o choca con:** nada; cuesta poco aunque sea AAA.
**Fuente:** WCAG 2.2, 2.3.3 (AAA).
**Confianza:** alta (norma).

### Lo nuevo de 2.2 que afecta a los flujos
**Dice:** lo ya introducido en un proceso no se vuelve a pedir: se rellena o se puede elegir (A). La
ayuda que se repite en varias vistas está en el mismo orden relativo en todas (A). Iniciar sesión no
exige una prueba cognitiva, como recordar o resolver un acertijo, sin una alternativa (AA).
**Se aplica:** en los flujos por pasos ([estructura.md](estructura.md#catálogo-de-navegación)) y en
el acceso.
**Se mide:** a ojo, recorriendo cada flujo: ningún dato se pide dos veces; la ayuda no cambia de sitio.
**No aplica o choca con:** cuando volver a pedir es esencial o es por seguridad (confirmar una
contraseña nueva).
**Fuente:** WCAG 2.2, 3.3.7 (A), 3.2.6 (A) y 3.3.8 (AA).
**Confianza:** alta (norma).

## Mitos

| Creencia | Qué dice la evidencia | Fuente |
|---|---|---|
| «Si axe no da errores, es accesible» | axe encontró el 29 % de 142 barreras puestas a propósito; la mejor herramienta, el 40 % | GOV.UK (2017, rev. 2018) |
| «WCAG pide objetivos de 44 × 44» | El nivel AA pide 24 × 24 o separación; 44 × 44 es AAA | WCAG 2.2, 2.5.8 y 2.5.5 |
| «Los controles desactivados no tienen que poder enfocarse» | En menús, pestañas y barras de herramientas conviene que sí, para que se descubran | W3C, APG |
