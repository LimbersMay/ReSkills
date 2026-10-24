# Huecos: categorías MECE

Seis categorías, recorridas en este orden y para cada flujo del material. Un flujo es una cadena de
comportamiento. En Regadera, el producto inventado de los ejemplos (una app que avisa cuándo toca regar
cada planta): «planta añadida → toca regar → regada», «registrar un riego atrasado», «modo vacaciones».

**Desempate:** un hueco va a la categoría de **la decisión que pide su respuesta**, no a la de dónde se
nota. «¿Qué muestra la lista si no hay plantas?» es Interfaz; «¿qué pasa si el usuario borra una planta
con un aviso pendiente?» es Transiciones aunque se vea en la interfaz; «¿y si el sistema no deja enviar
notificaciones?» es Fallos. Si dos categorías siguen sirviendo, gana la primera de la lista.

## 1. Alcance

¿Qué entra en la v1, para quién y qué no?

- Cada función del material: ¿está en la v1, más tarde, o fuera? (MoSCoW)
- Lo que el usuario ya descartó: ¿hay algo del material que dependa de ello y caiga también?
- Extras del mock que el documento no menciona (una vista, un botón, un pie, una integración).
- Plataformas: ¿solo una (un navegador, un sistema), o también las que cita el material?
- ¿Hay algo que el producto promete que debería estar en la garantía?

## 2. Tiempo

¿Cuándo empieza, cuánto dura y desde cuándo se cuenta?

- Cada temporizador o umbral: desde qué momento cuenta, en qué unidad, valor por defecto, valores
  permitidos, si hay «nunca».
- ¿Qué cuenta como «actividad» o «uso»? (abrir el producto, tocar un elemento, una acción en segundo
  plano…)
- ¿Por elemento, por usuario o global? ¿Qué pasa con varias ventanas o varios dispositivos?
- Cambiar un ajuste a mitad: ¿afecta a lo que ya está contando?
- Reinicio del producto o del equipo: ¿el tiempo se conserva, se reinicia o se descuenta?
- Pausas del sistema (bloqueo, suspensión): ¿se congela, se descuenta, desde cuándo?
- Frecuencia con que se comprueba (precisión aceptable: un minuto, cinco…).

## 3. Transiciones

Por cada estado del flujo: ¿cómo se entra, cómo se sale y qué pasa con cada evento?

- Lista los estados que sugiere el material y busca los que falten (¿«en vacaciones» es un estado o
  una condición?).
- Para cada estado × cada evento (el usuario lo abre, lo edita, lo borra, lo mueve, cambia un ajuste,
  llega un aviso…): ¿qué pasa? Lo que el material no dice es un hueco.
- Acciones del usuario a mitad de una transición automática.
- ¿Es reversible cada paso? ¿Cómo se deshace y qué se recupera exactamente (posición, orden, datos
  asociados)?
- Elementos que ya estaban al instalar o al activar el producto (datos de una versión anterior,
  elementos creados fuera del producto).
- Concurrencia: dos eventos a la vez, dos dispositivos, el mismo elemento dos veces.

## 4. Datos

¿Qué se guarda, cuánto, y qué pasa con ello?

- Qué campos se guardan de cada elemento y para qué sirve cada uno.
- Identidad y duplicados: ¿dos elementos con el mismo nombre son dos entradas?
- Cuánto tiempo se conservan, límite de cantidad, qué pasa al llegar al límite.
- Borrado: ¿se puede borrar una entrada, todo? ¿Deshacer una acción quita la entrada?
- Datos derivados (un total calculado, una agrupación): ¿cuándo se calculan y si se recalculan?
- Privacidad: ¿qué sale del equipo? ¿Se guarda algo sensible (datos personales, enlaces con tokens)?
- Exportar o importar, y sincronizar entre equipos: ¿sí, no, más tarde?

## 5. Fallos

¿Qué pasa cuando algo no sale como se espera?

- Cada API que el material cita puede fallar o negarse: ¿qué hace el producto y qué ve el usuario?
- Los casos especiales de la plataforma, que el producto no puede tocar o que se comportan distinto (en
  un navegador: páginas internas, incógnito; en un móvil: ahorro de batería, modo avión).
- Permisos que el usuario no da o retira.
- Almacenamiento lleno o datos guardados corruptos.
- El proceso en segundo plano se duerme o se reinicia a mitad de una acción.
- Un dato de entrada mal formado (una fecha o un dominio escrito a mano).

## 6. Interfaz

Aquí se pregunta qué tiene que mostrar el producto y cuándo. Cómo se reparte en vistas lo decide la
fase de interfaz, al prototipar: las vistas del material son hipótesis (ver la skill, paso 1).

Por cada pantalla del material y cada número que se muestra:

- Estados: vacío, con un elemento, con muchos (¿cien?), búsqueda sin resultados, error.
- Cada número o contador: qué cuenta exactamente y de dónde sale (un «ahorro estimado» necesita una
  fórmula y un periodo: ¿«hoy» desde las 00:00 o en las últimas 24 h?).
- Acciones destructivas o masivas: ¿confirmación, deshacer, ninguna?
- Qué necesita ver el usuario nada más abrir, y si se recuerda lo último que hizo.
- Lo que el mock muestra con datos de ejemplo: ¿es un formato fijo («hace 3 horas», «ayer · 18:20»)?
- Acciones fuera de la pantalla principal (avisos, atajos, un contador en el icono).
