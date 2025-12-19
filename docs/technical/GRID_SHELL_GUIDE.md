# 🎯 Grid Shell Implementation & Maintenance Guide

## Quick Reference: How Grid Shell Works

### The Simplest Explanation

- **Desktop:** `[NAV: 80px]` `[CONTENT: Flexible]` `[SIDEBAR: 0→350px]`
- **Tablet:** `[NAV: 80px]` `[CONTENT: Flexible]` `[Sidebar as overlay]`
- **Mobile:** `[CONTENT: 100%]` `[Nav & Sidebar as overlays]`

### CSS Grid Template (Desktop)

```css
#app.grid-shell-mode {
  display: grid;
  grid-template-columns: 80px 1fr 0px; /* Sidebar closed */
  grid-template-areas: "nav content sidebar";
}

#app.grid-shell-mode[data-sidebar-state="open"] {
  grid-template-columns: 80px 1fr 350px; /* Sidebar open */
}
```

---

## For Adding New Features to the Grid

### Scenario 1: Add a New Right Sidebar (Notifications)

**Step 1:** Update HTML (`index.html`)
```html
<div id="app">
  <nav class="sidebar-navigation">...</nav>
  <div class="main-content-screen">...</div>
  <div id="notifications-sidebar">NEW</div> ← Add here
  <div id="order-sidebar">...</div>
</div>
```

**Step 2:** Update Grid Definition (`_layout-shell.scss`)
```css
.app-container.grid-shell-mode {
  /* Now 4 columns instead of 3 */
  grid-template-columns: 
    80px 
    1fr 
    var(--notifications-width, 0px)  ← NEW
    var(--sidebar-width, 0px);
  
  grid-template-areas: 
    "nav content notifications sidebar";  ← NEW
}
```

**Step 3:** Assign Grid Area
```css
#notifications-sidebar {
  grid-area: notifications;  ← NEW
}
```

**Step 4:** Control from SidebarManager (`SidebarManager.js`)
```javascript
openNotifications() {
  appContainer.style.setProperty('--notifications-width', '280px');
}

closeNotifications() {
  appContainer.style.setProperty('--notifications-width', '0px');
}
```
*Done! The grid recalculates automatically.*

### Scenario 2: Modify Sidebar Width

**Before:** Just change the CSS width and break the layout.
**Now:** Change the variable in the state selector.

```css
/* _layout-shell.scss */
.app-container.grid-shell-mode[data-sidebar-state="open"] {
    --sidebar-width: 400px; /* Changed from 350px */
}
```
*The Grid automatically pushes the content to accommodate the new 400px width.*
