# 🎨 Visual System Map (Radiography)
*Generated: Dec 13, 2025*
*Updated: Dec 13, 2025 (Refactor Completed)*
*Status: Verified against Codebase*

# 🗺️ Visual Architecture Map - Grid Shell Era (Fase 5+)

## Current Layout System: CSS Grid "App Shell"

### Desktop View (1920px+) - Grid Active
┌─────────────────────────────────────────────────────────────┐
│                      #app Container                         │
│                     (display: grid)                         │
├──────────┬──────────────────────────────────┬───────────────┤
│   NAV    │                                  │    SIDEBAR    │
│  (80px)  │           MAIN CONTENT           │   (0→350px)   │
│  Fixed   │        (Flexible: 1fr)           │    Dynamic    │
│          │                                  │               │
│ .drawer- │      .main-content-screen        │    #order-    │
│   menu   │        - Product Tables          │    sidebar    │
│          │        - Product Grid            │               │
│          │        - Orders View             │     (Cart)    │
│          │                                  │               │
│   Nav    │            Content               │    Sidebar    │
│  z-idx:  │           z-idx: 50              │   z-idx: 90   │
│   100    │                                  │               │
└──────────┴──────────────────────────────────┴───────────────┘

**CSS Grid:**
- `grid-template-columns: 80px 1fr 0px` | `80px 1fr 350px`
- `grid-template-areas: "nav content sidebar"`
- `gap: 0`
- `Transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1)`


### Tablet View (1024px) - Mixed Mode
┌─────────────────────────────┐
│       #app Container        │
│      (Grid + Overlay)       │
├──────────┬──────────────────┤
│   NAV    │     CONTENT      │
│  (80px)  │      (1fr)       │
│          │                  │
│ .drawer- │  .main-content   │
│   menu   │                  │
│          │ [SIDEBAR OVERLAY]│
│          │  position: fixed │
│          │  z-index: 1000   │
└──────────┴──────────────────┘

**CSS Grid:**
- `grid-template-columns: 80px 1fr`
- `grid-template-areas: "nav content"`
- Sidebar desconectado del grid
- Sidebar actúa como overlay cuando abre


### Mobile View (375px) - Overlay Only
┌────────────────────┐
│   #app Container   │
│     (1 Column)     │
├────────────────────┤
│                    │
│   CONTENT (100%)   │
│   .main-content    │
│                    │
│   [NAV OVERLAY]    │
│ [SIDEBAR OVERLAY]  │
│  Both: position:   │
│  fixed, full-      │
│      screen        │
└────────────────────┘

**CSS Grid:**
- `grid-template-columns: 1fr`
- `grid-template-areas: "content"`
- Navs flotantes (`position: fixed`)


## Component Hierarchy (Post Transplant - Fase 5)
```html
<body>
  ├─ <div id="app">  ✅ GRID CONTAINER (display: grid)
  │   ├─ <nav class="sidebar-navigation">  ← grid-area: nav
  │   │    └─ Menu items
  │   │
  │   ├─ <div class="main-content-screen"> ← grid-area: content
  │   │    ├─ Product Tables
  │   │    ├─ Product Grid
  │   │    └─ Orders View
  │   │
  │   └─ <div id="order-sidebar">          ← grid-area: sidebar
  │        └─ Order Cart
  └─ <script>...</script>
```

### Grid Areas Reference
| Area | Component | Purpose | Width (Desktop) |
| :--- | :--- | :--- | :--- |
| **nav** | `.sidebar-navigation` | Left menu/navigation | `80px` (fixed) |
| **content** | `.main-content-screen` | Main viewport | `1fr` (flexible) |
| **sidebar** | `#order-sidebar` | Right panel (orders) | `0px`→`350px` (dynamic) |

### State Management (SidebarManager Control)
| State | Desktop (1920px+) | Tablet (1024px) | Mobile (375px) |
| :--- | :--- | :--- | :--- |
| **Sidebar Closed** | 80px + 1fr + 0px | 80px + 1fr | 1fr (overlay hidden) |
| **Sidebar Open** | 80px + 1fr + 350px | 80px + 1fr + overlay | 1fr + overlay |
| **Layout Mode** | Grid (native) | Grid + Overlay | Overlay only |
| **Animation** | Push (smooth) | Overlay slide | Full-screen slide |

### Layout System Implementation Files
| File | Purpose | Status |
| :--- | :--- | :--- |
| `index.html` | DOM structure | ✅ Transplant complete |
| `Shared/styles/layout/_layout-shell.scss` | Grid definition | ✅ Active |
| `Shared/styles/layout/_sidebars.scss` | Sidebar styling | ✅ Updated |
| `SidebarManager.js` | State control | ✅ Active |
| `OrderUI.js` | Order logic | ✅ Legacy cleaned |

### Phases Completed vs. Pending
- **✅ Fase 5: Layout Shell System (COMPLETE)**
  - Grid Shell active on Desktop
  - Sidebars unified under SidebarManager
  - BackstopJS baseline created
  - Zero layout shifts

- **✅ Fase 6: Responsividad Unificada (COMPLETE)**
  - Unified Breakpoints (xs, sm, md, lg, xl, xxl)
  - Layout logic moved entirely to CSS Grid (No JS listeners)
  - Table Mobile Strategy: Responsive Horizontal Scroll
  - Forms standardized to SCSS

---

## 🧬 Materia Prima (Global Variables)
**Source:** `Shared/styles/settings/variables.css`
These are the atoms of the design. Changes here ripple everywhere.

| Variable | Token Name | Actual Value (Code) | Notes |
| :--- | :--- | :--- | :--- |
| **Fuente Principal** | --n/a | 'Montserrat', sans-serif | Hardcoded in Components |
| **Fuente Secundaria** | --n/a | 'Roboto', sans-serif | Assumed default |
| **Color Acento** | `--accent-color` | `#00f7ff` (Cyan) | *User noted #00d4ff* |
| **Color Fondo** | `--background-color` | `#000000` | *User noted #0a0a0a* |
| **Color Texto** | `--text-color` | `var(--color-gray-200)` | #ECE9D8 |
| **Radio Borde** | `--radius-md` | `12px` | |

---

## 🎛️ PANEL A: MODO GRID (Tarjetas)
**Independence Status:** ✅ TOTAL
**Source:** `Shared/styles/views/_view-grid.scss`
*Unified View (formerly cards.css + product-table-v2)*

### 1. Estructura (Grid Layout)
Uses `tools/_mixins.scss` for responsive logic.

| Dispositivo | Breakpoint (Sass) | Valor | Mixin | Columnas |
| :--- | :--- | :--- | :--- | :--- |
| **Mobile Small** | `xs` | `375px` | `@include respond-to('xs')` | 2 Cols |
| **Mobile Landscape** | `sm` | `640px` | `@include respond-to('sm')` | 3 Cols |
| **Tablet Portrait** | `md` | `768px` | `@include respond-to('md')` | 3 Cols |
| **Tablet Landscape** | `lg` | `1024px` | `@include respond-to('lg')` | 3 Cols (Desktop logic) |
| **Desktop** | `xl` | `1280px` | `@include respond-to('xl')` | Fluid (Grid Shell) |

### 2. La Tarjeta (Componente `.product-card`)
**Architecture:** Uses `%card-shell` mixin (The Skeleton).
- **Core Styles:** Shared border, shadow, transition, hover effect (Golden Glow).
- **Altura Base:** `200px` (min).
- **Twins Variant:**
  - Standard: `min-height: 300px`, `object-fit: cover`.
  - Liquor: `min-height: 200px` (variable), `object-fit: contain` (Bottles).

### 3. Tipografía & Precios
- **Título:** `.product-name` -> `1.1rem` (Bold 600).
- **Precios (Unified Logic):**
  - Renderizado por `_renderCardPrices` (JS Strategy Pattern).
  - **Licores:** Alineación Vertical (Etiqueta + Botón).
  - **Standard:** Flex Wrap Centered.
  - **Estilo:** `.price-button` (Golden Standard).

---

## 🎛️ PANEL B: MODO TABLA (Listas)
**Independence Status:** ✅ TOTAL
**Source:** `Shared/styles/views/_view-table.scss`
*Refactored from _tables.scss*

### 1. Estructura (Table Layout)
- **Ancho:** 100% (Max 1400px).
- **Estilo:** `border-collapse: separate` con `border-spacing` variable (ver Modifiers).
- **El Esqueleto (`%table-core`):**
  - Nuevo Mixin maestro que combate la duplicidad.
  - Hereda `padding` y `text-align` centralizados.
  - **Defensa de Títulos:** Protege `tr.title-row` de heredar bordes o estilos destructivos.

### 2. The Twins Architecture (Gemelos)
Hemos separado el diseño en dos entidades distintas:

#### A. Tabla Estándar (`.standard-table`)
Diseñada para Alitas, Snacks, Pizzas (información densa).
- **Layout:** `auto` (Se adapta al contenido).
- **Thumbnails:** `80px x 56px` (Landscape) - FIXED with `!important`.
- **Ingredientes:** Ancho preferente `40%` (min `250px`).
- **Nombres:** Min `150px`.

#### B. Tabla Visual (`.liquor-table`)
Diseñada para Licores, Cervezas, Refrescos (Impacto visual).
- **Layout:** `fixed` (Control milimétrico).
- **Ancho:** Compactado al 95% (Max 1080px).
- **Imágenes:** `95px` (Grandes, aisladas).

### 3. Universal Optimizations (Grand Unification)
*Features implementados en `Dec 15` para consistencia total.*

#### A. El "Renglón" (Visual Separator)
Todas las celdas (`td`) incluyen ahora un borde inferior sutil:
- **Color:** `var(--border-color)` (Sincronizado con Tema).
- **Grosor:** `1px` (Elegante).
- **Excepción:** `tr.title-row` y `.compact` overrides.

#### B. El Botón Dorado (`.price-button`)
Estilo unificado para TODOS los precios (simples o múltiples).
- **Visual:** Glassmorphism + Borde Dorado + Glow.
- **Comportamiento Híbrido:**
  - En tablas simples: Se centra (`margin: 0 auto`) y toma `75%` ancho.
  - En grids (Alitas/Licores): Se alinea a la derecha (`justify-self: end`).

#### C. The Ghost Grid (`.stacked-price-container`)
Sistema universal para precios múltiples (Antes exclusivo de Licores).
- Renderizado por `_createMultiPriceCell` (JS).
- Alinea `Label (Izq)` vs `Button (Der)` perfectamente.
- Usado ahora en: Licores, Alitas, Cervezas.

#### D. Calibración de Spacing
- **Padding Vertical:** `18px` (Reducido de 25px para balance).
- **Modifiers:**
  - `.table-compact`: `10px` spacing (Ideal para Alitas).
  - `.table-spacious`: `20px` spacing (Standard Food).

### 4. Strategy: Responsive Scroll (Mobile Unification)
**Source:** `_view-table.scss` -> `.table-wrapper`

Goodbye "Squish Protocol" (nuclear-mobile). Hello **Responsive Scroll**.
Instead of forcing columns to be tiny (and unreadable), we wrap the table in a scrollable container.

- **Wrapper:** `.table-wrapper` (`overflow-x: auto`).
- **Min-Widths:** Every column has a strict `min-width` (e.g., `140px`) to ensure readability.
- **Behavior:** On small screens (Mobile/Tablet), the user swipes horizontally to see extra columns.
- **Benefits:** No broken layouts, no hidden data, consistent rendering.

---

## 🛠️ Guía de Edición (New Hacker's Manual)

### Si quieres cambiar...

1.  **Tamaño Tarjetas (PC/Tablet):**
    - Ir a `Shared/styles/views/_view-grid.scss`.
    - Buscar `@include tablet-portrait` o start of file.
    - Cambiar `repeat(3, ...)` a `repeat(2, ...)`.

2.  **Comportamiento Móvil Landscape:**
    - Ir a `Shared/styles/views/_view-grid.scss`.
    - Buscar `@include mobile-landscape`.
    - Modificar la regla `.app-container.order-mode &` si quieres cambiar el comportamiento con Sidebar.

3.  **Letra de Tabla:**
    - Ir a `Shared/styles/views/_view-table.scss`.
    - Buscar `.product-table td`.
    - Editar `font-size` (Solo afectará tablas).

4.  **Imágenes de Licores:**
    - Ir a `Shared/styles/views/_view-grid.scss`.
    - Buscar `.product-card.liquor-card .product-image`.
    - Ajustar height clamp.
    
---

## 🎭 Coreografía de Animación (Anti-FOUC)
**Logic:** Centralized Robust Animation System
**Goal:** Prevent pile-up, ensure smooth entry/exit.
**Location:** 
- **Tool:** `tools/_mixins.scss` -> `@mixin stagger-children`
- **Keyframes:** `base/animations.css` -> `fadeIn`, `fadeOut`
- **States:** `layout/_containers.scss` -> `.screen-hidden`, `.fade-out`

### 1. El Orquestador (Mixin)
En lugar de bucles manuales, usamos el mixin robusto:
```scss
/* Usage in Views */
.product-card {
    /* Automates opacity:0 and delays */
    @include stagger-children(20, 0.05s); 
}
```

### 2. Máquina de Estados (Visibilidad)
El sistema de navegación (`app-init.js`, `ScreenManager.js`) depende de estas clases CSS críticas.

| Clase | Función | Comportamiento (CSS) |
| :--- | :--- | :--- |
| `.screen-hidden` | **Estado Final** | `display: none !important; opacity: 0;` |
| `.fade-out` | **Transición Salida** | `animation: fadeOut 1s ...` (Fuerza opacidad a 0) |
| `.screen-visible` | **Estado Visible** | `display: flex/block; opacity: 1;` |
| `.fade-in` | **Transición Entrada** | `animation: fadeIn 1s ...` |

> **Nota Crítica:** `.fade-out` usa `@keyframes` explícitos para garantizar que el elemento desaparezca visualmente antes de ser eliminado del flujo (display: none).

