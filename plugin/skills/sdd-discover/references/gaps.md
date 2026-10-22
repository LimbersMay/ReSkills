# Huecos: categorías MECE

Seis categorías, recorridas en este orden y para cada flujo del material (un flujo es una cadena de
comportamiento: «pestaña abierta → pausa → baúl», «restaurar desde el baúl», «proteger un sitio»).

**Desempate:** un hueco va a la categoría de **la decisión que pide su respuesta**, no a la de dónde se
nota. «¿Qué muestra el baúl si está vacío?» es Interfaz; «¿qué pasa si el usuario cierra a mano una
pestaña en pausa?» es Transiciones aunque se vea en la interfaz; «¿y si Chrome no deja descartarla?» es
Fallos. Si dos categorías siguen sirviendo, gana la primera de la lista.

## 1. Alcance

¿Qué entra en la v1, para quién y qué no?

- Cada función del material: ¿está en la v1, más tarde, o fuera? (MoSCoW)
- Lo que el usuario ya descartó: ¿hay algo del material que dependa de ello y caiga también?
- Extras del mock que el documento no menciona (una vista, un botón, un pie, una integración).
- Navegadores y plataformas: ¿solo Chrome, o también los que cita el material?
- ¿Hay algo que el producto promete que debería estar en la garantía?

## 2. Tiempo

¿Cuándo empieza, cuánto dura y desde cuándo se cuenta?

- Cada temporizador o umbral: desde qué momento cuenta, en qué unidad, valor por defecto, valores
  permitidos, si hay «nunca».
- ¿Qué cuenta como «actividad» o «uso»? (foco, clic, scroll, audio, la ventana activa…)
- ¿Por ventana o global? ¿Qué pasa con varias ventanas?
- Cambiar un ajuste a mitad: ¿afecta a lo que ya está contando?
- Reinicio del navegador o del equipo: ¿el tiempo se conserva, se reinicia o se descuenta?
- Pausas del sistema (bloqueo, suspensión): ¿se congela, se descuenta, desde cuándo?
- Frecuencia con que se comprueba (precisión aceptable: un minuto, cinco…).

## 3. Transiciones

Por cada estado del flujo: ¿cómo se entra, cómo se sale y qué pasa con cada evento?

- Lista los estados que sugiere el material y busca los que falten (¿«protegida» es un estado o una
  condición?).
- Para cada estado × cada evento (el usuario la abre, la cierra, la mueve, la fija, la protege, cambia
  un ajuste, empieza a sonar…): ¿qué pasa? Lo que el material no dice es un hueco.
- Acciones del usuario a mitad de una transición automática.
- ¿Es reversible cada paso? ¿Cómo se deshace y qué se recupera exactamente (posición, ventana, grupo)?
- Elementos que ya estaban en el estado al instalar o al activar el producto (un grupo de Chrome ya
  existente, pestañas viejas).
- Concurrencia: dos eventos a la vez, dos ventanas, la misma URL dos veces.

## 4. Datos

¿Qué se guarda, cuánto, y qué pasa con ello?

- Qué campos se guardan de cada elemento y para qué sirve cada uno.
- Identidad y duplicados: ¿dos veces la misma URL son dos entradas?
- Cuánto tiempo se conservan, límite de cantidad, qué pasa al llegar al límite.
- Borrado: ¿se puede borrar una entrada, todo? ¿Restaurar quita la entrada?
- Datos derivados (un título calculado, una agrupación): ¿cuándo se calculan y si se recalculan?
- Privacidad: nada sale del equipo; ¿se guarda algo sensible (URLs con tokens)?
- Exportar o importar, y sincronizar entre equipos: ¿sí, no, más tarde?

## 5. Fallos

¿Qué pasa cuando algo no sale como se espera?

- Cada API que el material cita puede fallar o negarse: ¿qué hace el producto y qué ve el usuario?
- Páginas especiales (`chrome://`, la tienda, PDFs, `file://`), incógnito, pestañas con formularios a
  medio rellenar.
- Permisos que el usuario no da o retira.
- Almacenamiento lleno o datos guardados corruptos.
- El service worker se duerme o se reinicia a mitad de una acción.
- Un dato de entrada mal formado (un dominio escrito a mano).

## 6. Interfaz

Por cada vista y cada número que se muestra:

- Estados de la vista: vacía, con un elemento, con muchos (¿cien?), búsqueda sin resultados, error.
- Cada número o contador: qué cuenta exactamente y de dónde sale (un «ahorro estimado» necesita una
  fórmula y un periodo: ¿«hoy» desde las 00:00 o en las últimas 24 h?).
- Acciones destructivas o masivas: ¿confirmación, deshacer, ninguna?
- Qué vista se abre por defecto y si recuerda la última.
- Lo que el mock muestra con datos de ejemplo: ¿es un formato fijo («hace 3 horas», «ayer · 18:20»)?
- Atajos o acciones fuera del popup (menú contextual, icono con contador).
