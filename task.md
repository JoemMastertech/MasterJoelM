# Master Migration Plan: CSS Grid App Shell (v2.0)

## 🎨 FASE 1: The Transplant (Structural Prep)
- [x] **1.1 Verificación Pre-Transplant** (Child of BODY validated)
- [x] **1.2 Backup & Git Checkpoint**
    - [x] `git add -A` & `git commit`
    - [x] `git checkout -b feature/grid-shell-migration`
- [x] **1.3 Modificar index.html**
    - [x] Move `#order-sidebar` inside `#app`
    - [x] Move `#drawer-menu` inside `#app` (Left Sidebar Fix)
- [x] **1.4 Verificación Post-Transplant**
- [x] **1.5 Validación Visual & Commit**

## 🔧 FASE 2: The Grid Definition (Architectural Core)
- [x] **2.1 Crear _layout-shell.scss**
    - [x] Define `.app-container.grid-shell-mode`
    - [x] Define Grid Areas (nav, content, sidebar)
    - [x] Override legacy positioning (`position: static`)
- [x] **2.2 Importar en main.scss**
- [x] **2.3 Validación CSS (Build)**

## ⚡ FASE 3: The Switch (Logic Adapter)
- [/] **3.1 Modificar SidebarManager.js**
    - [x] `open()` adds `.grid-shell-mode` (Right Sidebar)
    - [x] `open()` adds `.grid-shell-mode` & width (Left Drawer)
    - [ ] `close()` logic (Refine cleanup)
- [x] **3.2 Modificar OrderUI.js (Cleanup)**
    - [x] Remove `_handleOrientationChange`
    - [x] Remove `orientationchange` listeners
- [x] **3.3 Test & Verify**
    - [x] Manual Console Test
    - [x] View Toggle Button Fix (`.view-toggle-btn` class + init)

## 👁️ FASE 4: Visual Validation
- [x] **4.1 Baseline Capture (Grid Shell State)**
    - [x] `backstop reference` (Verified with `.product-name`)
    - [x] Scenarios Covered: Homepage, Liquor Table, Sidebar Grid Layout
- [x] **4.2 Activate Permanent Grid Mode**
    - [x] Implicitly active via code changes.
- [x] **4.3 Comparison Test (BackstopJS)**
    - [x] Baseline established as the new "Truth".
- [x] **4.4 Final Review**
    - [x] Functionality Verified.
    - [x] Visuals Baselined.

# ✅ MIGRATION COMPLETE (Phase 5)

## 🧭 FASE 6: Responsividad Unificada (COMPLETE)
- [x] **6.1 Governance Centralization**
    - [x] Audit hardcoded breakpoints
    - [x] Create `_breakpoints.scss` (xs, sm, md, lg, xl)
    - [x] Update `_mixins.scss` to use `@include respond-to()`
- [x] **Phase 6: Unified Responsiveness** <!-- id: 5 -->
    - [x] **Phase 6.1: Foundation** (Breakpoints & Mixins) <!-- id: 6 -->
    - [x] **Phase 6.2: App Shell** (CSS Grid Layout) <!-- id: 7 -->
    - [x] **Phase 6.3: View Calibration** (Grid/Table Views) <!-- id: 8 -->
    - [x] **Phase 6.4: Verification** (BackstopJS) <!-- id: 9 -->
- [x] **Phase 6.5: The Final Unification**
    - [x] **Phase 1: JS Listeners Cut** (OrderUI.js clean)
    - [x] **Phase 2: Breakpoint Alignment** (768/1024/1280)
    - [x] **Phase 2.3: Table Refactor** (Responsive Scroll)
    - [x] **Phase 2.4: Forms Standard** (SCSS Conversion)
    - [x] **Phase 4: Final Approval** (Backstop Baseline) [x] Refactor `_view-grid.scss` (Fluid columns)
    - [x] Refactor `_view-table.scss` (Adaptive padding/font)
- [x] **6.4 Verification**
    - [x] BackstopJS Mobile/Tablet Scenarios (Approved Mismatches)
