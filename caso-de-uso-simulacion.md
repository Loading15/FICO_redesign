# Caso de Uso: Cómo usar Claude Code para diseñar desde cero

> Simulación de conversación real entre un desarrollador nuevo en IA y Claude Code.
> El objetivo es aprender a expresarse bien, cuándo usar cada skill y por qué.

---

## Contexto del proyecto simulado

**Proyecto:** Rediseño del canvas de una aplicación de gestión visual de tareas.
**La persona sabe:**
- Qué páginas tiene la app (Dashboard, Canvas, Detalle de tarea, Configuración)
- Qué funcionalidades necesita el canvas (arrastrar tarjetas, conectar nodos, zoom, filtros)
- Que el diseño actual no comunica bien la jerarquía visual

**La persona NO sabe:**
- Cómo hablarle bien a Claude
- Cuándo usar los skills
- Cómo estructurar sus ideas para obtener el mejor resultado

---

## La simulación

---

### PASO 0 — El error más común del principiante

Antes de mostrar cómo hacerlo bien, aquí está cómo lo haría alguien sin guía:

> ❌ **Prompt malo:**
> ```
> rediseña mi canvas
> ```

**Por qué es malo:** Claude no sabe nada de tu proyecto, tu stack, tus usuarios,
tus restricciones ni tu visión. Va a inventar algo genérico que probablemente
no tiene nada que ver con lo que quieres.

> ❌ **Prompt malo:**
> ```
> necesito que el canvas tenga drag and drop, zoom, filtros, colores,
> conexiones entre nodos, un panel lateral, toolbar arriba, modo oscuro,
> responsive, animaciones suaves, y que se vea moderno
> ```

**Por qué es malo:** Es una lista de deseos sin contexto, sin prioridad y sin
estructura. Claude intentará hacer todo a la vez y el resultado será superficial.

---

### PASO 1 — Configurar el proyecto correctamente

**Situación:** Es el primer día. La persona acaba de clonar el repo y quiere empezar.

---

> ✅ **La persona escribe:**
> ```
> /setup-matt-pocock-skills
> ```

**Por qué usar este skill aquí:**
Es obligatorio antes que todo. Sin esto, los demás skills no saben dónde
guardar los issues, qué vocabulario usar ni cómo estructurar los documentos.
Es como configurar el idioma antes de empezar a escribir.

---

> **Claude responde algo como:**
> ```
> Exploré el proyecto. Encontré que usas GitHub. ¿Confirmas que los issues
> deben crearse en este repositorio? ¿Qué etiquetas de triage usas?
> (Ejemplo: needs-triage, in-progress, ready, blocked, done)
> ```

---

> ✅ **La persona responde con contexto real, no con monosílabos:**
> ```
> Sí, usamos GitHub Issues en este mismo repo. Las etiquetas que usamos son:
> needs-triage, ready, in-progress, on-hold y done. El equipo de frontend
> es quien toma los tickets, así que los títulos deben ser claros para
> alguien que no conoce el backend.
> ```

**Por qué este nivel de detalle importa:**
Cada dato que das aquí se guarda en la configuración y las demás skills lo
usarán automáticamente. Si dices "el frontend toma los tickets", Claude
escribirá los issues con ese lector en mente desde ahora en adelante.

---

### PASO 2 — Entender el terreno antes de diseñar

**Situación:** La persona quiere rediseñar el canvas pero no recuerda exactamente
cómo está conectado con el resto de la app.

---

> ✅ **La persona escribe:**
> ```
> /zoom-out
>
> Estoy parado en el componente Canvas.jsx. Necesito entender qué otros
> módulos dependen de él antes de proponer cambios, para no romper nada
> ni diseñar algo que el código actual no pueda soportar.
> ```

**Por qué agregar contexto al skill:**
El skill sabe qué hacer, pero darle el punto de partida (`Canvas.jsx`) y
la razón (`no romper dependencias`) lo hace más preciso. En lugar de darte
un mapa genérico, te dará exactamente lo que necesitas.

---

> **Claude responde algo como:**
> ```
> Mapa de módulos relevantes al Canvas:
>
> - TaskBoard → pasa el array de tareas al Canvas como prop `items`
> - FilterBar → emite eventos de filtro que Canvas consume
> - TaskDetail → se abre cuando Canvas emite onTaskClick
> - useCanvasState (hook) → maneja posición, zoom y selección
>
> El Canvas no tiene estado propio de datos, solo de UI.
> Actualmente no soporta conexiones entre nodos (no hay ese modelo en el código).
> ```

**Qué hace la persona con esto:**
Antes de diseñar sabe que: (1) las conexiones entre nodos son algo nuevo que
hay que construir desde cero, (2) el estado de UI ya está separado en un hook,
lo cual es buena señal.

---

### PASO 3 — Validar y profundizar la visión con preguntas

**Situación:** La persona tiene una visión clara del rediseño pero no está segura
de haber considerado todos los casos. Quiere que alguien la desafíe.

---

> ✅ **La persona escribe:**
> ```
> /grill-me
>
> Quiero rediseñar el canvas con estas ideas principales:
> - Las tarjetas deben poder agruparse en columnas (tipo kanban) o en
>   bloques libres (tipo miro), el usuario elige el modo
> - Debe haber conexiones visuales entre tarjetas relacionadas
> - Un panel lateral derecho muestra el detalle de la tarjeta seleccionada
>   sin salir del canvas
> - La toolbar debe estar arriba con las acciones principales
> - Quiero que sea usable en tablet también
>
> Por favor desafíame en cada decisión. Empieza por donde veas más riesgo.
> ```

**Por qué este prompt funciona:**
1. Da la visión completa pero en puntos separados, fáciles de cuestionar uno a uno.
2. Pide que empiece por donde hay más riesgo, lo que hace el grilling más valioso.
3. No pide que Claude lo implemente, solo que lo desafíe. Eso es todo lo que
   necesitas en esta etapa.

---

> **Claude responde algo como:**
> ```
> Empiezo por el riesgo más alto: el modo dual (kanban vs libre).
>
> Cuando el usuario cambia de modo kanban a modo libre, ¿qué pasa con
> el orden de las tarjetas? ¿Se preservan las posiciones relativas,
> se resetean, o el usuario puede volver al kanban y las columnas siguen?
>
> Mi recomendación: guardar ambos estados por separado en useCanvasState
> y hacer el cambio de modo no destructivo.
> ```

---

> ✅ **La persona responde siendo específica:**
> ```
> Buen punto. Prefiero que sea no destructivo. Cada modo guarda su propio
> estado y el usuario puede ir y venir sin perder nada. Si es la primera
> vez que entra a modo libre, las tarjetas heredan las posiciones del kanban
> como punto de partida.
> ```

**Consejo clave:**
En el grilling, responde con decisiones, no con dudas. Si no sabes algo,
dilo explícitamente: `"no lo sé, ¿qué recomiendas?"`. Claude te dará
una recomendación fundamentada y puedes aceptarla o ajustarla.

---

> **[...el grilling continúa varias rondas más sobre: comportamiento de
> conexiones, responsive en tablet, qué pasa cuando hay 200+ tarjetas,
> accesibilidad, estados de carga, etc.]**

---

> ✅ **Cuando la persona siente que ya no hay más preguntas importantes:**
> ```
> Creo que cubrimos todo lo relevante. ¿Hay alguna decisión que dejamos
> abierta que pueda bloquear al frontend más adelante?
> ```

**Por qué esta pregunta de cierre importa:**
Le pides a Claude que haga un último barrido sobre lo que quedó sin resolver.
Muchas veces hay una decisión menor que parece obvia pero que bloquea
la implementación.

---

### PASO 4 — Generar la maqueta visual para validar

**Situación:** Las decisiones están tomadas. Antes de escribir el PRD formal,
la persona quiere ver el canvas para confirmar que la visión se ve como esperaba.

---

> ✅ **La persona escribe:**
> ```
> /frontend-design
>
> Genera una maqueta HTML standalone (sin build, sin dependencias externas
> excepto Tailwind CDN) del canvas rediseñado con estas características:
>
> - Layout: toolbar arriba, canvas en el centro, panel lateral derecho (colapsable)
> - Modo kanban: columnas con tarjetas arrastrables entre columnas
> - Tarjetas con: título, etiqueta de color, avatar del asignado
> - Panel lateral: muestra título, descripción y estado al hacer click en una tarjeta
> - Toolbar: botones de modo (kanban/libre), zoom in/out, filtro por etiqueta
> - Colores: fondo gris claro, tarjetas blancas, sidebar blanco, toolbar blanco
> - No necesita ser funcional al 100%, es para validar la distribución visual
> ```

**Por qué este prompt produce buenos resultados:**
1. Especifica el formato de salida (`HTML standalone, sin build`).
2. Lista el layout con jerarquía clara (toolbar / canvas / panel).
3. Describe las tarjetas con exactamente los campos que importan.
4. Aclara el nivel de fidelidad esperado (`validar distribución, no funcional al 100%`).
5. Da los colores para que no invente una paleta random.

---

> **Claude genera `canvas-mockup.html`.**

---

> ✅ **La persona abre el archivo en el browser y vuelve con feedback específico:**
> ```
> El layout general está bien. Tengo dos ajustes:
> 1. El panel lateral es demasiado ancho (ocupa ~40% del canvas), quiero
>    que sea de ancho fijo de 320px.
> 2. Las tarjetas necesitan mostrar también una fecha de vencimiento debajo
>    del avatar. Agrégala en rojo si está vencida.
>
> El resto está perfecto, puedes dejarlo igual.
> ```

**Cómo dar feedback a una maqueta:**
- Sé específico con medidas cuando importan (`320px`, no "más chico").
- Dile explícitamente qué NO cambiar para evitar que Claude "mejore" cosas que ya estaban bien.
- Un feedback por vez si son cambios grandes; varios juntos si son pequeños como en este caso.

---

### PASO 5 — Documentar el diseño como PRD

**Situación:** La maqueta está validada. Ahora hay que convertir todo lo decidido
en un documento formal para el equipo.

---

> ✅ **Sin cerrar la conversación, la persona escribe:**
> ```
> /to-prd
>
> Usa todo lo que decidimos en esta conversación para generar el PRD
> del rediseño del canvas. El documento es para el equipo de frontend,
> así que los módulos deben describirse desde la perspectiva de
> componentes React. Incluye los criterios de aceptación por módulo.
> ```

**Por qué NO cerrar la conversación:**
El `to-prd` construye el documento sobre el contexto acumulado de toda la sesión.
Si cierras y abres una nueva conversación, pierde todo el grilling, las decisiones
y los ajustes de la maqueta.

**Por qué agregar el contexto de "perspectiva React":**
Sin ese dato, Claude podría describir los módulos en términos genéricos.
Al especificarlo, los nombres de los componentes en el PRD van a coincidir
con lo que el frontend ya conoce.

---

> **Claude genera el PRD y lo publica en GitHub Issues con etiqueta `needs-triage`.**

---

### PASO 6 — Convertir el PRD en tickets accionables

**Situación:** El PRD está publicado y aprobado. Hay que crear los tickets.

---

> ✅ **La persona escribe:**
> ```
> /to-issues #42
>
> Divide el PRD en issues independientes. Prioriza en este orden:
> 1. Primero los tickets de estructura (layout, componentes base)
> 2. Luego los de interacción (drag, conexiones)
> 3. Al final los de detalle (animaciones, responsive)
>
> Cada ticket debe tener criterios de aceptación medibles, no subjetivos.
> "Se ve bien" no es un criterio válido. "El panel tiene 320px de ancho
> fijo en desktop" sí lo es.
> ```

**Por qué dar el orden de prioridad:**
Sin este contexto, Claude divide el trabajo en orden lógico técnico pero no
necesariamente en el orden que le conviene a tu equipo. Si le dices la
prioridad, los tickets ya salen ordenados y etiquetados correctamente.

**Por qué pedir criterios medibles:**
Es el error más común en tickets de diseño: quedan con criterios subjetivos
que generan discusión en el code review. Si lo pides explícitamente desde el
principio, el frontend sabe exactamente cuándo un ticket está terminado.

---

### PASO 7 — Ordenar los tickets antes de entregarlos

**Situación:** Los tickets están creados pero algunos necesitan más detalle
o están mal priorizados.

---

> ✅ **La persona escribe:**
> ```
> /triage
>
> Revisa los issues creados del rediseño del canvas (los que tienen
> etiqueta needs-triage). Para cada uno verifica:
> - ¿Tiene suficiente información para que el frontend lo tome sin preguntar?
> - ¿Los criterios de aceptación son medibles?
> - Si falta algo, redacta la pregunta al autor (yo) como comentario en el issue.
>
> No cambies el orden de prioridad que ya tienen, solo mejora la calidad
> de los que están incompletos.
> ```

**Por qué agregar "no cambies el orden de prioridad":**
El triage por defecto puede reordenar según urgencia percibida. Si ya tienes
un orden definido y funcional, protégelo explícitamente.

---

## Resumen de principios aprendidos en la simulación

### Sobre cómo expresarse con Claude

| ❌ Evitar | ✅ Preferir |
|-----------|------------|
| Prompts de una línea sin contexto | Dar el punto de partida + la razón |
| Listas de deseos sin prioridad | Ordenar por lo que más importa primero |
| "que se vea bien" | Medidas, colores y comportamientos concretos |
| Responder "sí" o "no" en el grilling | Responder con la decisión completa |
| Cerrar la conversación entre skills | Mantener el hilo entre grill-me → to-prd |
| Pedir todo a la vez | Un objetivo claro por mensaje |

### Sobre cuándo usar cada skill

| Situación | Skill |
|-----------|-------|
| Primera vez en el proyecto | `/setup-matt-pocock-skills` |
| No entiendo cómo encaja este código | `/zoom-out` |
| Tengo una idea pero quiero validarla | `/grill-me` |
| Quiero ver cómo se ve antes de documentar | `/frontend-design` |
| Decisiones tomadas, necesito el spec | `/to-prd` |
| Spec aprobado, necesito los tickets | `/to-issues` |
| Los tickets necesitan revisión | `/triage` |

### La regla más importante

> **Claude es tan bueno como el contexto que le das.**
> No adivina. No asume. No recuerda conversaciones anteriores.
> Cada vez que abres una conversación, empieza desde cero.
> Tu trabajo es darle el contexto correcto en el momento correcto.

---

## Archivos que debería generar este flujo

Al final de todo el proceso deberías tener:

```
tu-proyecto/
├── CLAUDE.md o AGENTS.md     ← configurado por setup-matt-pocock-skills
├── docs/
│   └── canvas-prd.md         ← o publicado en GitHub Issues
├── canvas-mockup.html         ← generado por frontend-design
└── GitHub Issues:
    ├── #42 PRD: Rediseño del Canvas
    ├── #43 [Canvas] Estructura base y layout
    ├── #44 [Canvas] Componente CanvasCard
    ├── #45 [Canvas] Panel lateral colapsable
    ├── #46 [Canvas] Drag and drop entre columnas
    ├── #47 [Canvas] Conexiones visuales entre tarjetas
    └── #48 [Canvas] Responsive para tablet
```
