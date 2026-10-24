# Brief de investigación: `ux:mock`

Borrador del 2026-10-23, pendiente de aprobar.

## Para qué

Decidir cómo es `ux:mock`, la fase que lleva de los requisitos y un quick design a una estructura
probada y aprobada. Esta investigación no escribe la skill ni la ruta: **contesta las preguntas de las
que dependen sus decisiones.** Con las respuestas se escribe la ruta, y con la ruta, la skill.

## Alcance

**Entra:** solo lo que necesita `ux:mock`: fases del prototipado, fidelidad, iterar sobre un diseño que
ya existe, probar con pocos usuarios, cuándo parar y cómo se escribe una skill.

**No entra:** el pulido, las convenciones visuales actuales, el sistema de diseño, la accesibilidad
completa, impeccable y cualquier producto concreto. Todo eso es de `ux:polish` o de otro momento.

**Punto de partida:**
- El borrador de la ruta, en `README-retomar.md` («La ruta propuesta»). Se usa como hipótesis.
- El artículo de Jafari, en `material/`. Sirve como mapa, no como evidencia.
- Las referencias de v0.3.1, en `plugins/ux/references/`. No se rehacen: se consultan solo si una
  pregunta lo pide.

## Reglas

1. **Cada respuesta dice qué decisión cambia.** Si no cambia ninguna, sobra.
2. **Fuentes primarias o reconocidas:** artículos revisados, normas, libros de referencia y
   documentación oficial. Un blog solo vale como pista para encontrar la fuente.
3. **Cada respuesta lleva su confianza:**
   - **alta:** varias fuentes coinciden o hay estudios replicados;
   - **media:** una fuente sólida;
   - **baja:** opinión o práctica sin estudio detrás.
4. **Filtro de fecha.** Para cómo percibe y decide una persona, vale lo clásico si se ha replicado. Para
   herramientas, la IA y el formato de las skills, tiene que ser actual.
5. **Se para al poder decidir,** no cuando el tema se agota: de 2 a 4 fuentes por pregunta. Si una
   pregunta abre otra, se apunta y no se persigue.
6. Sin subagentes. Una pregunta tras otra, en este contexto.

## Las preguntas

### P1. ¿Qué fases tiene el prototipado y cuándo termina cada una?

- **Decide:** los pasos de la skill y su criterio de salida.
- **Hipótesis:** plan de la vuelta → prototipo → prueba → refinar → repetir → `ux.md`.
- **Contestada cuando:** hay una secuencia con entrada y salida en cada fase, respaldada por al menos
  dos fuentes. Si no hay consenso, se dice.
- **Candidatas:** ISO 9241-210 (2019); Houde y Hill (1997); Buxton (2007).

### P2. ¿Qué fidelidad conviene para cada pregunta?

- **Decide:** qué genera la IA en cada vuelta: nivel de detalle, grises o color, contenido real,
  cuánta interacción.
- **Hipótesis:** fidelidad baja o media, en grises, con contenido real y los estados como
  comportamiento.
- **Contestada cuando:** hay una regla del tipo «para esta pregunta, esta fidelidad», con evidencia de
  si la fidelidad cambia los problemas que se encuentran al probar.
- **Candidatas:** Houde y Hill (1997), que separan función, aspecto e implementación; Walker,
  Takayama y Landay (2002), sobre baja frente a alta fidelidad; Virzi et al. (1996).

### P3. ¿Cómo se itera sobre un diseño que ya existe sin quedarse anclado?

- **Decide:** cuándo se hacen alternativas, cuántas y de qué tamaño.
- **Hipótesis:** el quick design es la base, y cada decisión en duda lleva de 2 a 3 bocetos rápidos.
- **Contestada cuando:** se sabe si las alternativas en paralelo mejoran el resultado frente a iterar
  una sola versión, y con qué número y tamaño.
- **Candidatas:** Dow et al. (2010); Tohidi et al. (2006), sobre si los usuarios critican más cuando
  ven varias opciones; Buxton (2007).

### P4. ¿Cómo se prueba cuando el único usuario es el autor?

- **Decide:** la fase de prueba: quién hace qué, qué se anota y qué se mide.
- **Hipótesis:** el usuario hace tareas sin guía, la IA anota sus dudas y se corren unas pocas medidas
  automáticas.
- **Contestada cuando:** se sabe qué métodos funcionan sin usuarios externos, qué detecta cada uno y
  sus límites:
  - el autor haciendo las tareas;
  - un recorrido cognitivo;
  - una evaluación heurística;
  - una persona cercana;
  - comprobaciones automáticas.

  También se sabe si una IA puede evaluar sin juzgar su propio trabajo, que fue un fallo del intento 1.
- **Candidatas:** Wharton et al. (1994), sobre el recorrido cognitivo; Nielsen (1994), sobre la
  evaluación heurística; Hertzum y Jacobsen (2001), sobre el efecto evaluador; Nielsen y Landauer
  (1993). Lo de la IA como evaluadora tiene que ser reciente.

### P5. ¿Cuándo se deja de iterar?

- **Decide:** el criterio de aprobación y el tope de vueltas.
- **Hipótesis:** se repite hasta que el usuario lo aprueba, con un tope.
- **Contestada cuando:** hay un criterio de salida concreto (por ejemplo, «las tareas se completan sin
  errores graves») y un tope respaldado o al menos justificado.
- **Candidatas:** ISO 9241-210, sobre los criterios de usabilidad; Nielsen (1993), sobre el diseño
  iterativo.

### P6. ¿Cómo se escribe y se prueba una buena skill?

- **Decide:** la forma del `SKILL.md`, cómo se reparten las referencias y cómo se comprueba que la
  skill funciona sin subagentes.
- **Hipótesis:**
  - primero se hace la tarea a mano con un caso inventado y se apunta qué contexto hubo que repetir;
  - el `SKILL.md` es corto;
  - cada referencia la pide un paso concreto;
  - las pruebas se definen antes de escribir.
- **Contestada cuando:** la guía oficial está leída y resumida en reglas aplicables, y hay una forma de
  evaluar la skill compatible con «sin subagentes».
- **Candidatas:** la documentación de Anthropic sobre Agent Skills y sus buenas prácticas, y la de
  skills de Claude Code. Tiene que ser actual.

## No se investiga: se decide al escribir la ruta

- Los nombres de las skills (`ux:mock` y `ux:polish`, en principio).
- El formato de `docs/ux.md`.
- Qué hacer si no hay quick design.
- Cómo se abre el prototipo para probarlo (por ejemplo, una página local para una extensión).

## Entregable

`material/investigacion-ux-mock.md`. Para cada pregunta:
- la respuesta corta;
- las fuentes;
- la confianza;
- **qué cambia en el borrador de la ruta**.

Al final, una lista de lo que no se pudo contestar y de las preguntas nuevas que salieron.

**Orden:** de P1 a P5, porque cada una se apoya en la anterior. P6 es independiente y puede ir al final.
