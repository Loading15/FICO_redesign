# FICO Mockup — Goals & Steps

## Contexto
Mockup web para FICO, app de facturación para pymes peruanas.
Empresa demo: Mayra S.A.C. (organización de eventos corporativos)
Archivo destino: `mockup.html` — single file, HTML + CSS + JS embebido

---

## Steps

### STEP 1 — Base + Login + Register ✅ Completado
Construir la estructura base del archivo:
- CSS variables, reset, tipografía (Outfit + DM Sans vía Google Fonts)
- Toggle Desktop / Móvil (esquina superior derecha)
- Pantalla Login (hero izquierda + formulario derecha)
- Pantalla Register (RUC → razón social auto, Usuario SOL, Clave SOL, Email, Contraseña)
- JS básico de navegación entre login ↔ register ↔ app

---

### STEP 2 — Sidebar + Header + Dashboard ✅ Completado
- Sidebar desktop (gradiente índigo→azul, 240px fijo)
- Top header (64px, título de página, campana, avatar)
- Panel Dashboard:
  - 3 KPI cards (Ingresos del mes, Por cobrar, Cotizaciones activas)
  - Card Salud Financiera (score 82/100, arco SVG, 4 factores con barras)
  - Gráfico evolutivo de ventas últimos 6 meses (SVG)
  - Sección logros: 4 badges + barra "próximo logro"

---

### STEP 3 — Facturación (4 tabs) ✅ Completado
Panel Facturación con tabs:
- **Cotizaciones**: tabla con menú 3 puntos por fila (Ver detalle, Subir OC, Emitir factura)
- **Facturas**: tabla con estado SUNAT
- **Guías de Remisión**: tabla
- **Notas de Crédito/Débito**: tabla
- Toolbar de búsqueda + botón "Nueva" por tab

---

### STEP 4 — Cotización Detalle + Emitir Documento ✅ Completado
- Panel Cotización Detalle (COT-2025-0023):
  - Header con estado badge
  - Sección OC (archivo adjunto OC-BCP-2025-0892.pdf + zona drag & drop)
  - Tabla de ítems + totales (Subtotal, IGV, Total)
  - Botones "Emitir Factura" y "Emitir Guía de Remisión"
- Panel Emitir Documento:
  - Selector de tipo de documento
  - Campos precargados (badge "precargado")
  - Campos editables
  - Tabla de ítems editable
  - Botón "Enviar a SUNAT" → dispara modal de celebración

---

### STEP 5 — Modal de Celebración ✅ Completado
- Overlay con blur
- Versión A (sin logro): confetti + monto + mensaje cálido rotatorio
- Versión B (con logro): igual + banner de logro desbloqueado (Velocista)
- Animación de entrada del modal
- Confetti generado por JS

---

### STEP 6 — Financiamiento + Perfil ✅ Completado
- Panel Financiamiento:
  - Banner introductorio
  - Tabla de facturas elegibles
  - Botón "Financiar" → abre WhatsApp con mensaje precargado
- Panel Perfil:
  - Sección datos editables de empresa
  - Galería completa de 6 logros
  - Gestión de usuarios (admin + form asistente con toggles de módulos)

---

### STEP 7 — Vista Móvil (phone frame) ✅ Completado
Marco de teléfono centrado (390×844px) con:
- Header móvil (logo FICO + ícono notificaciones)
- Bottom navigation bar (Dashboard, Facturar, Financiar, Perfil)
- Panel Dashboard móvil: KPIs en grid 2×2 + salud financiera + logros
- Panel Facturación móvil: tabs + tarjetas verticales (no tablas)
- Panel Financiamiento móvil: banner + tarjetas de facturas
- Panel Perfil móvil: secciones apiladas

---

### STEP 8 — Pulido final ✅ Completado
- Revisar consistencia visual en todos los panels
- Verificar que todos los flujos de navegación funcionan
- Verificar menús de 3 puntos, tabs, modal, links de WhatsApp
- Ajustar responsive del phone frame

---

### STEP 9 — Réplica SUNAT: Wizard de Creación de Factura ✅ Completado
Objetivo: replicar el flujo de SUNAT dentro de FICO con mejor UX, como pantalla intermedia entre "Nueva factura" y el formulario de ítems.

**Vista 9A — Wizard SUNAT (panel `panel-sunat-wizard`)**
Formulario tipo tabla con separador ":" — replicar exactamente las preguntas de SUNAT:
1. Tipo de Transacción: radio Al Contado / Al Crédito (default: Al Contado)
2. Operaciones sujetas a Detracción: Sí / No (default: No)
3. Factura de Exportación: Sí / No (default: No)
4. RUC del Receptor: input 11 dígitos + auto-fetch Razón Social (debajo)
5. Vinculada a Colaboración Empresarial Sin Contabilidad independiente: Sí / No (No)
6. Emitida por Pago Anticipado: Sí / No (No)
7. Emitida por Emisor Itinerante: Sí / No (No)
8. Establecimiento del Emisor donde entrega el bien/servicio: Sí / No (Sí)
9. Dirección donde entrega el bien/servicio: Sí / No (No)
10. Emitida por venta de combustible y/o mantenimiento de vehículo: Sí / No (No)
11. Tipo de Moneda: select SOLES / DÓLARES (default: SOLES)
12. Descuentos o Deduce Anticipos: Sí / No (No)
13. Tiene ISC: Sí / No (No)
14. Operaciones Gratuitas: Sí / No (No)
15. Cargos u Otros Tributos fuera de la base imponible del IGV: Sí / No (No)

Footer sticky: botones "× Cancelar" y "Continuar →"
Estilo: header negro "Creación de Factura", filas con borde inferior, radio buttons naranja (#ea580c) replicando exactamente SUNAT.
Triggers que abren el wizard:
- Botón "Nueva Factura" en tab Facturas → wizard (sin datos precargados) → Continuar → Vista 9B
- Opción "Emitir factura" en menú 3 puntos de Cotizaciones → wizard → Continuar → Vista 9B (con datos del receptor precargados desde la cotización)
- Botón "Emitir Factura" dentro del panel Cotización Detalle → mismo flujo
El wizard NO aplica a cotizaciones nuevas (flujo cotización sigue independiente).

**Vista 9B — Completar Cotización / Datos del documento (panel `panel-nueva-factura`)**
Pantalla para ingresar los ítems, cantidades y precios de la factura:
- Header con datos precargados del receptor (RUC + razón social desde wizard)
- Fecha de emisión + número correlativo autogenerado
- Tabla de ítems editable (descripción, unidad, cantidad, precio unit., IGV %, importe)
- Botón "+" para agregar ítem
- Panel resumen lateral: Subtotal, IGV (18%), Total en Soles
- Botón "Guardar como borrador" y botón primario "Enviar a SUNAT"
- "Enviar a SUNAT" → dispara modal de celebración (versión simple, sin logro)

---

### STEP 10 — Gamificación + Email de cotización + Filtros facturación ✅ Completado

**10A — Barra de progreso en cotizaciones**
Cada fila de la tabla de cotizaciones muestra debajo un pipeline visual de 4 etapas:
`Borrador → Enviada → Aprobada / OC → Facturada`
- Implementado como segunda `<tr class="cot-progress-row">` que colapsa el espacio entre filas
- Etapas: dots conectados por línea, coloreados según estado actual (gris/azul/verde/índigo)
- Estado "Rechazada" muestra pipeline en rojo con X

**10B — Indicador de velocidad cot→fac (semáforo)**
Dot circular junto a la fecha, sin texto visible hasta hover:
- Verde (⚡ < 12h): aplica al logro Velocista
- Amarillo (12h–72h sin avance)
- Rojo (> 3 días sin avance)
- Gris (rechazada o facturada)
Al pasar el cursor → tooltip oscuro con detalle ("8h — muy rápido", "9 días sin avance", etc.)
Barra de progreso por etapas eliminada (no incluida en versión final)

**10C — Notificación motivacional en dashboard**
Banner dismissible debajo del filter bar con mensaje contextual rotatorio:
- "Tienes 2 cotizaciones sin respuesta en más de 7 días — un seguimiento puede cerrarlas."
- "Estás a S/ 1,500 de desbloquear el logro S/ 50k facturados. ¡Ya casi!"
- Botón de acción contextual (ej: "Ir a cotizaciones") + botón × para cerrar
- Se oculta al hacer click en × y no vuelve a aparecer en la sesión

**10E — Filtros Mes / Año / Cliente en Facturación**
Barra de filtros idéntica a la del dashboard, encima de los tabs (aplica a todos: Cotizaciones, Facturas, Guías, Notas).
Seleccionar cliente filtra las filas visibles en la tabla activa por coincidencia de texto.
Mes y Año muestran chips visuales. Botón "Limpiar filtros" resetea todo.

**10D — Enviar cotización por correo**
Nueva opción en el menú 3 puntos de cada cotización: "Enviar por correo"
Abre modal con:
- Campo "Para": pre-llenado con correo del cliente (Banco Continental, Alicorp, etc.)
- Campo "CC": opcional
- Campo "Asunto": pre-llenado con "Cotización COT-2025-XXXX — Mayra S.A.C."
- Área "Mensaje": texto predeterminado cortés con placeholders del cliente
- Adjunto: pill visual "COT-2025-XXXX.pdf" con botón × para quitar
- Botón "Enviar" (dispara toast de confirmación) + "Cancelar"

---

### STEP 11 — Mejoras tabla Cotizaciones + Filtro de fechas funcional ✅ Completado

**11A — Botón "Nueva cotización" habilitado**
Abre un nuevo panel `panel-nueva-cotizacion` con formulario de creación:
- RUC receptor con auto-fetch de razón social
- Fecha de emisión + número de cotización autogenerado (COT-2025-0024)
- Tabla de ítems editable con recalculo de subtotal/IGV/total
- Botones: "Guardar borrador" y "Enviar al cliente" (dispara toast de confirmación)

**11B — Tabla Cotizaciones rediseñada**
- Columna `FECHA` renombrada a `FECHA CREACIÓN` con atributo `data-fecha="YYYY-MM"` en cada `<tr>`
- Nueva columna `FECHA ACTUALIZACIÓN` con timestamp del último cambio de estado
- Semáforo de velocidad movido a columna propia, centrado (`text-align:center`)
- Layout final: N° Cotización · Cliente · Fecha Creación · Fecha Actualización · ⬤ · Estado · Acciones

**11C — Filtro de fechas funcional (Fecha Creación)**
- Reemplaza el único dropdown Mes por "Desde" y "Hasta" (mes + año cada uno)
- Si sólo Desde tiene valor → filtra exacto por ese mes/año
- Si Desde + Hasta → filtra el rango de meses inclusive
- Filtro trabaja sobre `data-fecha="YYYY-MM"` en cada fila
- Al cambiar tab, el filtro se re-aplica a la tabla activa

---

### STEP 12 — Aprobar/Rechazar cotización + Vista móvil nueva cotización ✅ Completado

**12A — Aprobar / Rechazar en tabla de cotizaciones**
- Nuevas opciones en el menú de 3 puntos: "Aprobar cotización" (verde ✓) y "Rechazar cotización" (rojo ✕)
- Solo visibles en filas con estado **Enviada** (actualmente COT-2025-0022)
- Al aprobar: badge cambia a `Aprobada` (verde), semáforo pasa a verde/rápido, toast de confirmación
- Al rechazar: badge cambia a `Rechazada` (rojo), semáforo pasa a neutral, toast de confirmación
- Tras la acción, las opciones Aprobar/Rechazar desaparecen del menú (ya no aplican)
- Separadas del resto de opciones por dividers

**12B — Vista móvil: Nueva Cotización**
- Panel `m-panel-nueva-cotizacion` con `position:absolute;z-index:10` sobre el phone-frame
- Se activa con el FAB "Nueva" dentro de `m-panel-facturacion`
- Header con botón "← Volver" que regresa a facturación
- Campos: RUC + Razón Social (auto-fetch), N° Cotización (readonly), Fecha, Validez, Moneda
- Lista de ítems adaptada para móvil: descripción full-width + grid 3 col (Cant./P.Unit./Importe)
- Botón `+ Agregar` añade ítems; botón ✕ los elimina
- Totales sticky al fondo: Subtotal / IGV / Total
- Pie fijo con "Guardar borrador" y "Enviar al cliente" → toast de confirmación

---

### STEP 13 — Tutorial de onboarding ✅ Completado

Modo tutorial que se activa automáticamente la primera vez que el usuario ingresa a la app (al hacer click en "Ingresar" o "Registrarse").

**Comportamiento general**
- Se dispara desde `showApp()` con un delay de 400ms para que el layout esté pintado
- Solo aplica a la vista desktop (el overlay es `position:fixed` dentro de `screen-app`)
- Botón "Saltar tutorial" siempre visible (excepto en el último paso, donde desaparece)
- 8 pasos en total; dots de progreso en la parte superior de la tarjeta

**Técnica de spotlight**
- `#tut-spotlight`: div con `box-shadow: 0 0 0 9999px rgba(12,8,36,0.65)` que oscurece todo excepto el elemento objetivo
- Transiciones CSS suaves (`.32s cubic-bezier`) al moverse entre pasos
- Posicionamiento con `getBoundingClientRect()` + clamping al viewport
- Pasos "full screen" (`center:true`) ocultan el spotlight y centran la tarjeta

**Pasos del tour**
1. **Bienvenida** — tarjeta centrada, sin spotlight, sin navegación de panel
2. **KPIs** (`#tut-kpis`) — resumen de ingresos/cobrar/cotizaciones; panel: dashboard; pos: bottom
3. **Salud Financiera** (`#tut-health`) — puntaje 82/100; panel: dashboard; pos: right
4. **Logros** (`#tut-logros`) — sistema de insignias; panel: dashboard; pos: top
5. **Facturación** (`#panel-facturacion .tabs-header`) — tabs de cotizaciones/facturas/guías/notas; panel: facturacion; pos: bottom
6. **Financiamiento** (`#nav-financiamiento`) — factoring express por WhatsApp; sin navegación; pos: right
7. **Perfil y equipo** (`#nav-perfil`) — datos empresa, usuarios, logros; sin navegación; pos: right
8. **Final** — tarjeta centrada, botón "¡Empieza la aventura! 🚀" que cierra el tutorial

**IDs añadidos** al HTML del dashboard:
- `id="tut-kpis"` en `.kpi-row`
- `id="tut-health"` en la card de Salud Financiera
- `id="tut-logros"` en la card de Logros del dashboard

---

### STEP 16 — FICO-chat: consultor virtual ✅ Completado

**Concepto**
FICO-chat es un asistente virtual posicionado como consultor estratégico de negocio, no como un chatbot de soporte técnico. Conoce los datos de la empresa del usuario (facturación, clientes, nivel, KPIs) y responde con lenguaje profesional y cordial. Producto próximo a lanzar; en la versión actual se ofrece como X consultas de prueba incluidas en el nivel.

**Consultas por nivel**

| Nivel | Consultas FICO-chat |
|-------|---------------------|
| Inicio      | 3  |
| **Impulso** | 10 (Mayra S.A.C.) |
| Crecimiento | 25 |
| Expansión   | Ilimitadas |
| Referente   | Ilimitadas |

**Widget flotante**
- Botón circular fijo (`position:fixed; bottom:28px; right:28px`) con gradiente índigo→azul, ícono de chat y punto de notificación ámbar
- Al hacer clic: panel de 360×520px aparece con animación de fade+slide sobre el botón (`transform: translateY(20px) scale(.96) → translate(0) scale(1)`)
- Al minimizar: panel se oculta, el botón queda visible
- El punto de notificación desaparece al abrir el chat por primera vez

**UI del panel**
- **Header**: gradiente oscuro, avatar "FC", nombre "FICO-chat", badge "Beta", estado online (punto verde), botón ×
- **Barra de consultas**: contador de consultas restantes + 10 dots (se van poniendo gris conforme se usan)
- **Área de mensajes**: burbujas alineadas (bot=izquierda blanca, usuario=derecha índigo), typing indicator animado (3 dots bounce)
- **Quick replies**: chips clicables con preguntas sugeridas que desaparecen tras usar la primera
- **Input**: campo full-width con botón de envío; envío también con Enter

**Mensaje de bienvenida**
Al abrir el chat por primera vez:
> "Hola, Mayra 👋 Soy FICO-chat, tu consultor virtual. Conozco el estado financiero de Mayra S.A.C.: este mes llevas S/ 48,500 facturados, una tendencia positiva de +12% y una salud financiera de 82/100. Estoy aquí para ayudarte a tomar mejores decisiones. ¿En qué te puedo ayudar hoy?"

**Temas que responde (base de conocimiento simulada)**
- Crecimiento de facturación → estrategia de cotización y conversión
- Diversificación de clientes → análisis de riesgo de concentración sectorial
- Cobranza → protocolo de seguimiento 3/7/15/20 días
- Nivel y progreso → cuánto falta, qué se desbloquea, cómo acelerar
- Flujo de caja / liquidez → conexión con módulo de Financiamiento
- Propuestas / precios → estructura de 3 capas (base/estándar/premium)
- Saludos genéricos → respuesta de apertura con contexto

**Comportamiento**
- Typing indicator de 900–1600ms antes de responder (simula procesamiento real)
- Cada respuesta consume 1 consulta del contador
- Al llegar a 0 consultas: mensaje explicando el límite y cómo actualizar plan
- El chat se inicializa solo una vez; las Quick Replies desaparecen tras el primer uso

**Cambios en beneficios de nivel**
- Eliminado: "Sello verificado en documentos" (de dashboard card + perfil)
- Agregado: "10 consultas FICO-chat" en dashboard nivel card y en perfil benefits list

---

### STEP 15 — Sistema de Niveles FICO ✅ Completado

**Concepto: Escala FICO**
Sistema de 5 niveles basado en volumen de facturación mensual. El lenguaje es "tu empresa creció", no "subiste de nivel". Cada nivel desbloquea beneficios que resuelven dolores reales del negocio en esa etapa.

| Nivel | Icono | Rango mensual | Beneficios clave |
|-------|-------|---------------|------------------|
| Inicio      | 🌱 | 0 – S/20k   | Acceso básico, plantillas estándar |
| **Impulso** | 🚀 | S/20k–60k   | 1 sesión asesoría gratuita, reporte PDF mensual, sello verificado en documentos |
| Crecimiento | 💎 | S/60k–150k  | 2 sesiones, benchmark sectorial, plantillas premium, tasa preferente en factoring |
| Expansión   | 🏆 | S/150k–500k | Asesor dedicado con contacto directo |
| Referente   | 👑 | S/500k+     | Multiusuario ilimitado, SLA garantizado, onboarding personalizado |

Mayra S.A.C. está en **Impulso** (S/48,500/mes), a S/11,500 de alcanzar Crecimiento.

**Componentes implementados**

1. **Card de nivel en Dashboard** — tarjeta oscura (gradiente índigo→azul) con:
   - Badge del nivel actual + nombre
   - KPI de facturación del mes
   - Barra de progreso hacia el siguiente nivel con texto motivacional ("Te faltan S/ 11,500")
   - Pills de beneficios activos
   - Botón "Agendar sesión" → navega a Perfil

2. **Mini-indicador en Sidebar** — encima del avatar, muestra nivel + barra de progreso compacta con porcentaje y nombre del siguiente nivel. Clic navega a Perfil.

3. **Sección "Mi nivel FICO" en Perfil** (entre Datos de la empresa y Logros):
   - Escalera visual de 5 niveles (done / active / locked)
   - Barra de progreso detallada con estimación de días al siguiente nivel
   - Lista de beneficios activos con descripción detallada
   - CTA de asesoría: "Agendar sesión →" → toast de confirmación
   - Preview colapsada de beneficios del siguiente nivel

**Principios de diseño anti-forzado**
- Nombres de nivel sin jerga gaming (no "Rank Up", no puntos arbitrarios)
- Progreso medido en S/ reales, no puntos ficticios
- Beneficios son servicios reales con valor tangible (asesoría, informes, tasas)
- La asesoría se presenta como "sesión ganada" — no como formulario a completar
- El sello en documentos genera valor hacia los clientes de Mayra, no solo para ella

---

### STEP 14 — Secciones en tabla de Cotizaciones + Rechazadas colapsables ✅ Completado

**Definición de secciones**
La tabla de cotizaciones se divide en dos bloques visuales con encabezado de sección:

| Sección | Estados incluidos | Etiqueta visual |
|---|---|---|
| **En negociación** | Borrador, Enviada | Badge ámbar |
| **En producción** | Aprobada | Badge índigo |

Cada sección tiene su propio `<table class="data-table">` con thead independiente.
El botón "Emitir factura" solo aparece en filas de "En producción" (Aprobada).

**Rechazadas — patrón colapsable**
- Las cotizaciones rechazadas no aparecen en ninguna de las dos secciones activas.
- Al final del tab hay un toggle discreto: `"▾ N cotización(es) rechazada(s)"` con borde discontinuo y fondo gris suave.
- Por defecto: colapsado (no distrae el flujo normal).
- Al hacer clic: se expande mostrando las filas con `opacity: 0.52` (muted) y el ícono rota 180°.
- Función JS: `toggleRechazadas()` — alterna `display` del bloque `#cot-rechazadas-body` y la clase `.open` en el toggle.

**Razonamiento del patrón de rechazadas**
Se eligió colapso in-place (vs. tab separado, filtro chip, o panel archivo) porque:
- Zero clics para usuarios que nunca las necesitan (están ocultas).
- Un clic para encontrarlas (no hay navegación secundaria).
- El conteo numérico en el toggle da visibilidad sin ocupar espacio.
- La opacidad reducida al expandir refuerza visualmente que son registros inactivos.

---

## Datos clave

**Empresa**: Mayra S.A.C. | RUC: 20601234567 | Eventos corporativos
**Paleta de colores**:
- Índigo 900: `#1E1B4B` — fondos oscuros, sidebar
- Índigo 700: `#3730A3` — color primario principal
- Índigo 500: `#6366F1` — accents, hover states
- Índigo 100: `#E0E7FF` — fondos sutiles, badges
- Índigo 50:  `#EEF2FF` — backgrounds suaves
- Azul 900:   `#1E3A8A` — gradiente sidebar, contraste
- Azul 800:   `#1E40AF` — color primario secundario
- Azul 600:   `#2563EB` — links, botones secundarios
- Azul 100:   `#DBEAFE` — fondos informativos
- Azul 50:    `#EFF6FF` — highlights suaves
**Clientes**: Banco Continental, Minera Cerro Verde, Alicorp, Claro Perú, Interbank, Aceros Arequipa, Supermercados Tottus

**KPIs dashboard**:
- Ingresos del mes: S/ 48,500 (+12%)
- Por cobrar: S/ 28,750 (7 facturas)
- Cotizaciones activas: 5
- Salud financiera: 82/100

**Gráfico ventas**: Nov 32,400 | Dic 41,200 | Ene 28,900 | Feb 38,700 | Mar 44,100 | Abr 48,500

**Logros**:
1. 🚀 Primera factura — Desbloqueado
2. 📋 Cotizador Pro — Desbloqueado
3. ✅ Cero rechazos — Desbloqueado
4. ⚡ Velocista (< 12h) — Desbloqueado
5. 💰 S/ 50,000 facturados — En progreso 82%
6. 🏆 Cliente fiel — Bloqueado 2/3
