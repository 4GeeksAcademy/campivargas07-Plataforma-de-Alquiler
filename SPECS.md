# Especificación de Producto y UI

## 1) Descripción breve del producto

**AgentHub** es una plataforma SaaS para alquiler de agentes de IA preconfigurados que pueden equiparse con skills según necesidades de negocio.

Este entregable define un **panel de administración interno** orientado a un usuario administrador (operaciones/producto) que necesita supervisar ingresos, usuarios, agentes, contrataciones y errores de ejecución desde una interfaz única.

El objetivo del prototipo es servir como referencia visual y funcional para implementación posterior con backend real.

## 2) Stack tecnológico y restricciones

1. La implementación será en **HTML5** (estructura) + **Tailwind CSS vía CDN** (estilos) + **JavaScript vanilla** (interacciones).
2. No se usarán frameworks de frontend (React, Vue, Angular, Svelte) ni librerías de estado.
3. No se implementará backend, autenticación real ni llamadas API (`fetch`, `axios`, XHR).
4. Todos los datos visibles del panel serán **hardcodeados** dentro del prototipo.
5. La UI incluirá soporte de **modo claro/oscuro global** usando utilidades `dark:` de Tailwind.
6. La navegación principal será lateral y persistente durante todo el uso del panel.

## 3) Arquitectura visual global

1. Layout de aplicación con dos zonas fijas: sidebar izquierda persistente y área de contenido principal con barra superior.
2. Barra superior con título contextual de sección y toggle de tema (claro/oscuro) accesible y visible en desktop y mobile.
3. El contenido principal se organiza por secciones (vistas) mostradas/ocultadas por navegación lateral sin recarga de página.
4. Diseño responsive: sidebar colapsable en pantallas pequeñas y panel principal en columna única.

## 4) Especificaciones por sección

### 4.1 Dashboard

1. Componente: **Grid de métricas 2x2 responsive**.
Contenido: cuatro tarjetas con icono, etiqueta y valor hardcodeado para:
	- Ingresos totales del mes.
	- Pérdida por descuentos/cupones.
	- Número de agentes activos.
	- Número de agentes fallando.
Comportamiento: en mobile se muestra como 1 columna; en tablet/desktop pasa a 2 y 4 columnas según ancho disponible.
2. Componente: **Tarjetas de métrica con acento visual por tipo**.
Contenido: color de acento distinto por tarjeta (ej. verde, ámbar, azul, rojo), borde sutil y sombra suave.
Comportamiento: estado hover eleva la tarjeta y refuerza contraste sin romper legibilidad en modo dark.
3. Componente: **Placeholder de gráfico semanal**.
Contenido: bloque de ancho completo debajo de tarjetas con borde discontinuo, altura fija y texto centrado “Actividad semanal (placeholder)”.
Comportamiento: mantiene proporción visual en ambos temas y ocupa 100% del ancho del contenedor.

### 4.2 Gestión de usuarios

1. Componente: **Tabla de usuarios**.
Contenido: columnas Nombre, Email, Plan y Estado con al menos 6 usuarios hardcodeados.
Comportamiento: tabla con scroll horizontal en pantallas pequeñas.
2. Componente: **Dropdown de acciones por fila** (botón `⋮`).
Contenido: opciones “Ver detalle” y “Eliminar”.
Comportamiento: el menú se abre/cierra al hacer clic en `⋮`; al abrir un dropdown se cierran otros dropdowns abiertos.
3. Componente: **Modal de detalle de usuario**.
Contenido: nombre completo, email, plan, estado, fecha de alta y notas.
Comportamiento: se abre desde “Ver detalle”, se cierra con botón “Cerrar” y al hacer clic en backdrop.
4. Componente: **Acción eliminar (UI-only)**.
Contenido: opción visible en dropdown.
Comportamiento: al hacer clic muestra feedback visual (ej. toast o texto temporal) sin persistencia real.

### 4.3 Gestión de agentes

1. Componente: **Listado de agentes**.
Contenido: nombre del agente, propietario, estado (activo / inactivo / fallando) y bloque de skills.
Comportamiento: estado renderizado con badge de color según criticidad.
2. Componente: **Lista de skills colapsable por agente**.
Contenido: skills ocultas por defecto.
Comportamiento: control “Ver skills” expande/colapsa con transición suave de altura/opacidad.
3. Componente: **Dropdown de acciones por agente**.
Contenido: “Configurar” y “Eliminar”.
Comportamiento: “Configurar” abre modal con prompt de sistema hardcodeado del agente.
4. Componente: **Modal de configuración**.
Contenido: prompt del sistema en bloque monoespaciado, botón de cierre.
Comportamiento: cierre por botón y backdrop.

### 4.4 Skills

1. Componente: **Texto explicativo de contexto**.
Contenido: bloque introductorio explicando que una skill es una capacidad modular reutilizable por agentes.
Comportamiento: permanece visible al inicio de la sección y adapta contraste en dark mode.
2. Componente: **Lista/Cards de skills disponibles**.
Contenido: nombre, descripción breve, contador de agentes que la usan.
Comportamiento: distribución responsive en grid de 1 a 3 columnas.
3. Componente: **Dropdown de acciones por skill**.
Contenido: “Ver detalle” y “Eliminar”.
Comportamiento: “Ver detalle” abre modal con descripción extendida, casos de uso y uso actual.
4. Componente: **Indicador de adopción**.
Contenido: contador numérico visible (ej. “12 agentes”).
Comportamiento: formato consistente en todas las cards.

### 4.5 Contrataciones de agentes

1. Componente: **Tabla de contratos activos e históricos**.
Contenido: columnas Cliente, Agente, Skills contratadas, Fechas (inicio/fin), Importe total pagado.
Comportamiento: datos hardcodeados con al menos 5 contratos.
2. Componente: **Dropdown de acciones por contrato**.
Contenido: mínimo “Ver detalle” y “Eliminar”.
Comportamiento: apertura contextual por fila con cierre automático al hacer clic fuera.
3. Componente: **Modal de detalle de contrato**.
Contenido: resumen del contrato + desglose de skills contratadas y precio individual por skill.
Comportamiento: se abre desde “Ver detalle” y se cierra por botón o backdrop.
4. Componente: **Formato monetario**.
Contenido: montos en USD con dos decimales.
Comportamiento: formato consistente en tabla y modal.

### 4.6 Log de errores

1. Componente: **Tabla/listado de errores**.
Contenido: timestamp, nombre del agente, tipo de error y descripción breve.
Comportamiento: orden descendente por fecha/hora (más reciente arriba).
2. Componente: **Badges de severidad/tipo**.
Contenido: categorías visuales (ej. warning, error, crítico) con código de color.
Comportamiento: cada badge mantiene legibilidad en claro/oscuro.
3. Componente: **Dropdown de acciones por error**.
Contenido: “Ver detalle” y “Marcar como resuelto”.
Comportamiento: “Ver detalle” abre modal con traza completa hardcodeada.
4. Componente: **Acción marcar como resuelto (UI-only)**.
Contenido: control visible por fila.
Comportamiento: cambia etiqueta/estilo de estado local en la UI sin persistencia backend.

## 5) Inventario de componentes reutilizables

1. **Sidebar persistente**: navegación entre 6 secciones con item activo destacado.
2. **Topbar**: título de sección + toggle de modo oscuro.
3. **Tarjeta de métrica**: icono, etiqueta, valor, acento de color.
4. **Dropdown de acciones (`⋮`)**: menú contextual reutilizable para tablas/listados.
5. **Modal overlay**: encabezado, contenido dinámico, botón cerrar, cierre por backdrop.
6. **Badge de estado/severidad**: variantes para activo/inactivo/fallando y warning/error/crítico.
7. **Lista de skills colapsable**: control expandir/contraer con transición.
8. **Tabla responsive**: cabecera fija visual y scroll horizontal en mobile.
9. **Toast/feedback UI-only**: confirmaciones no persistentes (eliminar/resolver).

## 6) Criterios de aceptación

1. La interfaz muestra una sidebar persistente con acceso a las seis secciones definidas.
2. El Dashboard presenta exactamente cuatro tarjetas de métricas y un placeholder de gráfico semanal debajo.
3. Cada sección de datos (Usuarios, Agentes, Skills, Contrataciones, Log) renderiza datos hardcodeados sin llamadas de red.
4. Cada fila/card que lo requiera incluye dropdown `⋮` funcional con sus acciones mínimas especificadas.
5. Solo un dropdown puede permanecer abierto al mismo tiempo; clic fuera cierra dropdowns abiertos.
6. Los modales de “Ver detalle” y “Configurar” se abren con su acción correspondiente y muestran contenido contextual correcto.
7. Todo modal se puede cerrar por botón explícito y clic en el backdrop.
8. En Gestión de agentes, las skills están colapsadas por defecto y se expanden/colapsan con transición visible.
9. El toggle de la barra superior cambia globalmente entre modo claro y oscuro usando clases `dark:`.
10. La apariencia en modo oscuro mantiene contraste legible en tarjetas, tablas, badges, dropdowns y modales.
11. El Log de errores categoriza visualmente eventos con badges de color por tipo/severidad.
12. El prototipo es navegable, coherente y utilizable como referencia para desarrollo posterior con backend.

