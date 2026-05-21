# Manual de Skills para Diseño de Canvas desde Cero

> Guía paso a paso para diseñar el canvas de cero, validar la visión creativa
> y comunicársela al equipo de frontend usando las skills de Matt Pocock.

> **Contexto importante:** Este proyecto no tiene código base existente.
> El canvas se diseña desde cero, lo que significa que la etapa creativa
> y de ideación es tan importante como la técnica. Este manual cubre ambas.

---

## Orden recomendado de uso

```
[Ideación libre] → setup-matt-pocock-skills → grill-me → frontend-design → to-prd → to-issues → triage
```

> `/zoom-out` no aplica al inicio porque no hay código que mapear.
> Se vuelve útil una vez que el frontend entregue las primeras pantallas.

---

## FASE PREVIA — Ideación libre con Claude (sin skills)

### ¿Cuándo usarla?
**Antes de cualquier skill**, cuando tienes sensaciones o referencias sobre cómo
quieres el canvas pero aún no tienes una visión estructurada. Aquí no usas
ningún skill — solo conversas con Claude de forma abierta.

### ¿Por qué esta fase existe?
Los skills están diseñados para refinar y documentar ideas que ya existen.
Si llegas al `grill-me` sin haber explorado tu visión, el resultado será
genérico. Esta fase libre es donde nace la identidad del diseño.

### ¿Qué herramientas usar aquí?

**1. Conversación libre con Claude**
Cuéntale tu visión de la forma más natural posible. No necesitas estructura.
Claude puede ayudarte a descubrir qué quieres antes de que lo sepas tú mismo.

Ejemplos de cómo arrancar:

```
Estoy diseñando un canvas de gestión visual de tareas desde cero.
Tengo referencias visuales en mente: algo entre Notion y Miro,
pero más simple. ¿Puedes hacerme preguntas para ayudarme a definir
la personalidad visual y funcional del canvas antes de que empiece
a especificarlo formalmente?
```

```
Quiero que el canvas se sienta fluido y sin fricciones. El usuario
principal es un project manager que trabaja con 20-50 tareas a la vez.
¿Qué patrones de interacción deberíamos explorar para ese perfil?
```

**2. Diagramas de flujo con Mermaid**
Antes de pensar en colores o componentes, mapea los flujos del usuario
con diagramas. Claude puede generarlos directamente en la conversación.

Cómo pedirlos:

```
Genera un diagrama de flujo en Mermaid que muestre cómo un usuario
crea una tarea, la mueve entre estados y la conecta con otra tarea
dentro del canvas.
```

```
Dibuja en Mermaid el árbol de componentes visual que propones para
el canvas: qué contiene qué, qué es hijo de qué.
```

```
Genera un diagrama de estados en Mermaid para una tarjeta dentro
del canvas: todos los estados posibles y qué evento desencadena
cada transición.
```

Los diagramas Mermaid se renderizan directamente en Claude Code y en GitHub.
Son la forma más rápida de alinear visión antes de escribir una línea de código.

**3. Referencias visuales**
Si tienes capturas de pantalla o referencias de otras apps, compártelas
en la conversación. Claude puede analizar la estructura visual y ayudarte
a identificar los patrones que te gustan.

```
Aquí hay una captura de Linear. Me gusta cómo organizan la barra lateral
pero el canvas principal se siente demasiado denso. ¿Qué cambiarías
para hacer algo más respirable manteniendo esa estructura?
```

### Resultado esperado de esta fase
Al terminar deberías poder completar estas frases:
- "El canvas se siente como..."
- "El usuario principal es... y su tarea más frecuente es..."
- "Las páginas que tiene la app son... y el canvas vive en..."
- "Las funcionalidades core son... (máximo 5)"
- "Lo que definitivamente NO quiero es..."

Con eso estás listo para el `grill-me`.

---

## 1. `/setup-matt-pocock-skills`

### ¿Cuándo usarlo?
**Una sola vez, antes de usar cualquier otra skill.** Es el paso de configuración
inicial del proyecto. Puedes hacerlo antes o después de la ideación libre,
pero debe ocurrir antes del `grill-me`.

### ¿Qué hace?
Configura el repositorio para que las demás skills entiendan:
- Dónde está el issue tracker (GitHub, GitLab o markdown local)
- Qué etiquetas de triage se usan
- Dónde están los documentos de dominio (`CONTEXT.md`, ADRs)

### Paso a paso

1. Abre Claude Code en la raíz de tu proyecto.
2. Escribe `/setup-matt-pocock-skills`.
3. La skill explorará el proyecto y te preguntará:
   - ¿Usas GitHub Issues, GitLab o archivos markdown locales?
   - ¿Cuáles son tus etiquetas de triage?
4. Confirma o corrige las respuestas.
5. La skill crea los archivos de configuración automáticamente.

### Consejo para proyectos nuevos sin código
Si el proyecto está vacío, la skill lo detectará. Dale el contexto manualmente:

```
El proyecto no tiene código aún. Usaremos GitHub Issues como tracker.
Las etiquetas serán: needs-triage, ready, in-progress, on-hold, done.
El equipo es frontend-heavy, así que los tickets deben ser legibles
para alguien que no conoce decisiones de arquitectura backend.
```

### Resultado
Tu proyecto queda listo para que `grill-me`, `to-prd`, `to-issues` y
`triage` funcionen con el contexto correcto.

---

## 2. `/grill-me`

### ¿Cuándo usarlo?
**Después de la ideación libre**, cuando ya tienes una visión aunque sea
incompleta y quieres que alguien la desafíe, la complete y ayude a tomar
las decisiones que aún están abiertas.

### Dos modos de uso según tu punto de partida

**Modo A — Tengo una visión clara (validación):**
Le describes tu diseño y el skill lo cuestiona para encontrar huecos.

**Modo B — Tengo ideas sueltas (generación creativa):**
Le describes tus referencias, sensaciones y restricciones, y el skill
te ayuda a construir la visión haciéndote preguntas generativas.

Para un proyecto desde cero, **empieza con el Modo B**.

### ¿Qué hace?
El agente te entrevista de forma implacable, una pregunta a la vez, recorriendo
cada rama del árbol de decisiones. Para cada pregunta te da su recomendación
para que no partas de cero.

### Paso a paso

**Si usas Modo B (desde cero):**

1. Resume lo que salió de la ideación libre:
```
/grill-me

Contexto: estamos diseñando el canvas desde cero, no hay código existente.
Lo que sé hasta ahora:
- El usuario principal es un project manager con 20-50 tareas simultáneas
- Quiero que se sienta entre Notion y Miro, pero más simple
- Funcionalidades core: mover tarjetas, conectar nodos, filtrar, zoom
- Páginas de la app: Dashboard, Canvas, Detalle de tarea, Configuración
- Lo que NO quiero: toolbars sobrecargadas, sidebars que compitan con el canvas

Por favor empieza por las decisiones de mayor impacto en la experiencia.
```

2. El agente hará preguntas una por una. Ejemplos:
   - ¿Las conexiones entre nodos son direccionales o bidireccionales?
   - ¿El zoom es libre o tiene niveles fijos?
   - ¿El panel de detalle reemplaza el canvas o coexiste?
   - ¿Qué pasa en móvil: versión reducida o bloqueado?

3. Responde cada pregunta con decisiones concretas.
   Si no sabes: `"no lo sé, ¿qué recomiendas para este tipo de usuario?"`

4. Cuando sientas que las decisiones importantes están tomadas, cierra con:
```
¿Qué decisiones quedaron abiertas que puedan bloquear al frontend?
```

### Situación típica
> "Tengo ideas sueltas sobre cómo quiero el canvas. Necesito que alguien
> me ayude a estructurarlas y desafiarlas antes de hacer cualquier mockup."

### Consejo
En modo generativo, no tengas miedo de decir "no lo sé" o "dame opciones".
El grilling es más valioso cuando eres honesto sobre lo que aún no tienes claro.

---

## 3. `/frontend-design`

### ¿Cuándo usarlo?
**Después del `grill-me`**, cuando las decisiones de diseño están tomadas
y quieres ver cómo se ve antes de documentarlo formalmente. Es la validación
visual de todo lo que decidiste.

### ¿Por qué es especialmente importante aquí?
Al no tener código existente, este paso es la única forma de confirmar
que la visión que tienes en la cabeza coincide con lo que realmente quieres
proyectar. Un PRD sin validación visual puede llevar al frontend en la
dirección equivocada.

### ¿Qué hace?
Genera un archivo HTML standalone (sin build, sin dependencias externas)
que puedes abrir directamente en el browser para validar la distribución
visual, los colores, la jerarquía y la interacción básica.

### Paso a paso

1. Sin cerrar la conversación del `grill-me`, escribe:
```
/frontend-design

Genera una maqueta HTML standalone del canvas con estas características
(basadas en lo que decidimos):
- Layout: [describe lo que decidiste]
- Componentes: [lista los elementos principales]
- Colores: [paleta o referencias]
- Nivel de fidelidad: distribución y jerarquía visual, no funcional al 100%
- Sin frameworks de build. Tailwind CDN está bien para estilos.
```

2. Claude genera un archivo `canvas-mockup.html`.

3. Abre el archivo en tu browser y valida:
   - ¿La distribución visual es la que imaginabas?
   - ¿La jerarquía es clara (qué es lo más importante visualmente)?
   - ¿Algo se siente incorrecto aunque no sepas exactamente por qué?

4. Da feedback específico:
```
El layout general está bien. Dos ajustes:
1. El panel lateral ocupa demasiado espacio, quiero que sea 320px fijo.
2. Las tarjetas necesitan más respiración, aumenta el padding interno.
El resto está perfecto, no lo toques.
```

### Iteraciones creativas
Si en la primera maqueta descubres que la visión no era lo que esperabas,
es válido y valioso. Puedes pedir variaciones:

```
Genera una variante donde el panel de detalle está abajo en lugar de
a la derecha. Quiero comparar ambas distribuciones antes de decidir.
```

```
Muéstrame cómo se vería el canvas con modo oscuro. Mantén el mismo
layout pero cambia la paleta completa.
```

### Resultado
Un archivo HTML que puedes compartir con cualquier persona del equipo
para validar la visión antes de escribir una línea de código real.

---

## 4. `/to-prd`

### ¿Cuándo usarlo?
**Después de validar la maqueta**, cuando la visión está confirmada visualmente
y necesitas un documento formal para que el equipo de frontend sepa qué construir.

### ¿Qué hace?
Toma todo el contexto acumulado en la conversación (decisiones del grilling,
ajustes de la maqueta, funcionalidades definidas) y produce un PRD estructurado
que publica directamente en tu issue tracker.

### Paso a paso

1. Sin cerrar la conversación, escribe `/to-prd`.
2. El agente sintetizará todo el contexto de la sesión.
3. Como no hay código existente, describirá los módulos a construir desde cero.
4. Te mostrará un borrador con:
   - Descripción del canvas y su propósito
   - Componentes a construir
   - Comportamiento esperado por componente
   - Criterios de aceptación
5. Confirma o ajusta el borrador.
6. El agente publica el PRD en tu issue tracker con la etiqueta `needs-triage`.

### Consejo para proyectos sin código
Cuando no hay código base, dile explícitamente al skill el stack tecnológico
que usará el frontend para que el PRD use los términos correctos:

```
/to-prd

El PRD es para un equipo frontend que usará React + TypeScript.
Describe los componentes usando convenciones de React (no genéricas).
```

### Resultado
Un PRD publicado en GitHub Issues listo para ser revisado y aprobado.

---

## 5. `/to-issues`

### ¿Cuándo usarlo?
**Después de que el PRD esté aprobado**, para convertirlo en tickets concretos
y accionables que el frontend pueda tomar uno a uno.

### ¿Qué hace?
Divide el PRD en issues independientes usando rebanadas verticales completas
(tracer bullets), de modo que cada ticket puede tomarse sin depender de los
demás en orden estricto.

### Paso a paso

1. Escribe `/to-issues #[número del PRD]`.
2. El agente leerá el PRD y propondrá una lista de issues con:
   - Título usando el vocabulario del dominio
   - Descripción clara de qué construir
   - Criterios de aceptación medibles (no subjetivos)
   - Etiqueta de triage correspondiente
3. Revisa la lista y confirma.
4. El agente crea todos los issues en tu tracker.

### Consejo
Pide explícitamente criterios medibles para tickets de diseño:

```
/to-issues #42

Asegúrate de que los criterios de aceptación sean medibles.
"Se ve bien" no es válido. "El panel tiene 320px de ancho en desktop" sí.
Prioriza primero estructura, luego interacción, al final detalle visual.
```

---

## 6. `/triage`

### ¿Cuándo usarlo?
**Después de crear los issues**, para revisarlos, completar los que tengan
información faltante y dejarlos listos para que el frontend los tome.

### ¿Qué hace?
Gestiona el flujo de los issues: `needs-triage` → `ready` → `in-progress` → `done`.
Revisa cada issue, aplica etiquetas y deja comentarios explicativos.

### Paso a paso

1. Escribe `/triage`.
2. El agente revisará todos los issues con etiqueta `needs-triage`.
3. Para cada issue verificará:
   - ¿Tiene suficiente información para tomarse sin preguntar?
   - ¿Los criterios de aceptación son medibles?
   - ¿Falta algo? Si falta, redacta la pregunta al autor como comentario.
4. Los issues quedan en `ready` cuando están completos.

---

## 7. `/zoom-out`

### ¿Cuándo usarlo?
**No al inicio.** Este skill es útil una vez que el frontend entregue
las primeras pantallas y necesites entender cómo el canvas ya construido
se conecta con el resto de la app para planear la siguiente iteración.

### ¿Qué hace?
Mapea todos los módulos que interactúan con el canvas, sus relaciones
y dependencias, usando el vocabulario del dominio del proyecto.

### Situación típica (iteración 2 en adelante)
> "El frontend entregó el canvas base. Ahora quiero añadir las conexiones
> entre nodos pero no sé si eso rompe algo de lo que ya está construido."

---

## Flujo completo para diseño desde cero

```
Día 1 — Ideación y configuración
│
├── [Conversación libre + Mermaid]
│   └── Explora la visión, mapea flujos, define personalidad del diseño
│
└── /setup-matt-pocock-skills
    └── Configura issue tracker y vocabulario del proyecto

Día 1 o 2 — Decisiones de diseño
│
└── /grill-me (Modo B: generativo)
    └── Construye y desafía la visión decisión por decisión

Día 2 — Validación visual
│
└── /frontend-design
    └── Genera maqueta HTML, valida en browser, itera hasta confirmar

Día 2 o 3 — Documentación
│
├── /to-prd
│   └── Convierte todo el contexto en PRD formal
│
└── /to-issues
    └── Divide el PRD en tickets accionables para el frontend

Ongoing — Gestión
│
└── /triage
    └── Revisa, completa y prioriza los issues

Iteración 2+ — Una vez que haya código
│
└── /zoom-out
    └── Mapea dependencias antes de cada nueva iteración
```

---

## Qué necesitas además de los skills

### Para la fase creativa

| Herramienta | Para qué | Cómo activarla |
|------------|----------|----------------|
| Conversación libre con Claude | Explorar ideas sin estructura | Sin skill, solo habla |
| Diagramas Mermaid | Mapear flujos, estados, componentes | Pídelos en la conversación |
| Referencias visuales (capturas) | Anclar la visión en ejemplos reales | Comparte imágenes en el chat |
| `/frontend-design` | Ver la distribución antes de documentar | Skill nativa de Claude Code |

### Para la fase de documentación

| Skill | Para qué |
|-------|----------|
| `/setup-matt-pocock-skills` | Configuración inicial del proyecto |
| `/grill-me` | Estructurar y desafiar la visión |
| `/to-prd` | Documento formal para el frontend |
| `/to-issues` | Tickets accionables |
| `/triage` | Calidad y priorización de issues |

---

## Notas importantes

- **Nunca saltes `/setup-matt-pocock-skills`**. Las demás skills necesitan saber
  dónde publicar los issues y qué vocabulario usar.
- **No cierres la conversación entre `/grill-me`, `/frontend-design` y `/to-prd`**.
  El PRD se construye sobre todo el contexto acumulado en esa sesión.
- **`/zoom-out` al inicio no sirve** si no hay código. Resérvalo para cuando
  el frontend empiece a entregar pantallas.
- **Los diagramas Mermaid son tu mejor aliado creativo** antes de tener código.
  Son gratis, rápidos y cualquiera del equipo puede leerlos en GitHub.
- Si una skill parece no tener contexto del tracker o vocabulario del proyecto,
  vuelve a correr `/setup-matt-pocock-skills`.
