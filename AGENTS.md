# Squat Gym — AGENTS.md

## Stack
- HTML estático puro · Tailwind CSS vía CDN · Google Fonts (Lexend headlines, Manrope body) · Material Symbols Outlined
- Sin build tools, sin package.json, sin framework, sin tests, sin linter

## Arquitectura de carpetas

```
index.html                # Landing page
login.html                # NO EXISTE aún (referenciado desde index.html)
Administrador/            # dashboard.html vacío
profesor/                 # dashboard-profesor.html + 13 .html en clases/
secretaria/               # dashboard.html + kiosko/ + clases/
encargado/                # dashboard.html vacío + kiosko/ + clases/
1-Pantallas-generales-... # Ayuda, Contacto, Privacidad
assets/css/               # consistency.css (NO incluido en ninguna página)
assets/img/               # vacío
```

## ⚠️ Regla de diseño #1 (del usuario)

**`profesor/dashboard-profesor.html` es el template canónico.** Toda página nueva o refactor debe seguir SU estructura:
- `<div class="layout-shell">` con grid `header / main / footer`
- Sidebar overlay: clase `sidebar` + `sidebar-visible` + `sidebar-backdrop`
- Header teal (`#005a52`), footer teal oscuro (`#00675f`)
- Tarjetas con clase `card-premium`, paginación, dropdown de notificaciones
- Colores exactos del `tailwind.config` inline (especialmente `on-surface: #1a1c1d`, `borderRadius default: 0.25rem`, `bg-mesh: #f8fafa`)

## Inconsistencias que YA existen — no repetir

Diseño del sidebar: 3 variantes distintas según el archivo (overlay, collapsed, transform). Usar siempre la de `dashboard-profesor.html` (fixed overlay con toggle).
Paletas: algunos html usan `#2c2f30` para `on-surface` y `#f5f7f7` para `background`. Usar los de dashboard-profesor (`#1a1c1d`, `#f8fafa`).
`borderRadius` default: `0.25rem` en dashboard-profesor, `0.125rem` en secretaria. Usar `0.25rem`.
`consistency.css` en `assets/css/` no está linkeado desde ninguna página — ignorarlo o eliminarlo.
Páginas vacías: `encargado/dashboard.html`, `Administrador/dashboard.html`, `secretaria/kiosko/1-apertura.html` — no están implementadas.

## Navegación
- Enlaces **relativos** entre páginas (ej. `kiosko/3-venta.html` desde dashboard)
- Footer links apuntan a `../1-Pantallas-generales-ayuda-contacto-etc/Ayuda.html` (y similares)

## Lo que NO existe
- login.html (referenciado desde index.html con ruta `1-General-login-sobreempresa-cambiarperfil/login.html`)
- package.json, opencode.json, CI/CD, tests
