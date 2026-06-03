# CardioU — Project Brief
**Documento vivo. Actualizar al cerrar cada sesión.**
**Última actualización: 2026-06-02**

---

## 01. Datos del proyecto

| Campo | Detalle |
|---|---|
| **Producto** | Landing page / home CardioU |
| **Cliente** | Fundación Cardioinfantil (LaCardio) |
| **Repo GitHub** | https://github.com/Serandom91/CardioU |
| **URL live** | https://serandom91.github.io/CardioU/home.html |
| **Figma** | `gqtZDeE0aTzPRGavReundi` (fileKey para MCP) |
| **Git user** | Serandom91 |

---

## 02. Stack técnico

| Archivo | Rol |
|---|---|
| `home.html` | HTML principal — Bootstrap 5 + bloque `<style>` inline para mobile |
| `landing.css` | Estilos de componentes desktop |
| `lacardio-tokens.css` | Tokens de marca (fuente de verdad: colores, tipografía, spacing) |
| `Assets/` | Imágenes, SVGs de íconos, logos, fuentes |
| `Fonts/Garet-Heavy.ttf` / `Garet-Book.ttf` | Fuentes locales (+ WOFF2 para Safari) |

**Dependencias externas:** Bootstrap 5 CDN, Inter (Google Fonts)

---

## 03. Sistema de diseño — Tokens

### Tipografía
| Rol | Familia | Peso | Tamaño desktop |
|---|---|---|---|
| H1 | Garet Heavy | 800 | 46px / lh 1.2 |
| H2 | Garet Heavy | 800 | 38px / lh 1.24 |
| H3 | Garet Heavy | 800 | 32px / lh 1.24 |
| Eyebrow | Garet Book | 400 | 13px / ls 0.2em / uppercase |
| Body | Inter | 400 | 16px / lh 1.3 |
| Btn lg | Inter | 700 | 16px / ls -0.02em |
| Btn sm | Inter | 700 | 13px |

**Escala mobile (Garet Heavy):** H1 37px, H2 32px, H3 26px / lh 31px / ls -0.01em

### Paleta
| Token CSS | Valor | Uso |
|---|---|---|
| `--color-blue-500` | `#1d386d` | Azul primario, bg dark sections |
| `--color-blue-400` | `#254686` | Bg surface |
| `--color-blue-300` | `#426cbe` | Números/stats, degradé schools |
| `--color-blue-100` | `#b8cef9` | Texto secundario dark, badges |
| `--color-blue-50` | `#e0eaff` | Bordes, estrellas |
| `--color-red-400` | `#ee335a` | Rojo acento, botones primarios |
| `--color-gray-50` | `#f4f3f0` | Bg secciones light (cifras, courses) |
| `--text-primary` | `#ffffff` | Texto sobre fondos dark |
| `--text-secondary` | `#b8cef9` | Subtexto sobre fondos dark |

**No usar:** `#23366a` (old blue), `#ed1f46` (old red)

### Paleta de escuelas
Medicina `#2a60c9` · Enfermería `#accdfc` · Innovación `#0059f7` · Servicio `#008bd0` · Habilidades `#066696` · Formación `#76aee1`

---

## 04. Estado de implementación — Secciones

| Sección | Desktop | Mobile | Notas |
|---|---|---|---|
| **Topbar** | ✅ | — (oculto mobile) | |
| **Header / Navbar** | ✅ | ✅ | Sólido `#1d386d`, sin borde toggler, links H3 mobile (`var(--font-display)`), btn full width |
| **Hero** | ✅ | ✅ | 2 slides carousel; mobile: imagen arriba, controles `[← ● ○ →]` debajo de trust |
| **Course List** | ✅ | ✅ | Fondo `#f4f3f0`; 4 columnas desktop, cards verticales (img arriba, body abajo); CTA "Ver todos" inline en header (derecha); mobile 1 col |
| **Schools** | ✅ | ✅ | Outer `#f4f3f0` + inner container `#1d386d` border-radius 24px; mobile padding 16px, border-radius xl, 1 col |
| **Cifras** | ✅ | ✅ | Fondo `#f4f3f0`, padding 64px top / 48px bottom / 155px lateral, gap 140px |
| **Differentiator** | ✅ | ✅ | Gradiente `#426cbe → #1d386d`, layout header arriba + img/pillars abajo; 155px lateral |
| **Testimonials** | ✅ | ✅ | Título "Esto dicen nuestros graduados", estrellas `#e0eaff`; mobile scroll horizontal, margin-left/right en first/last card |
| **FAQ** | ✅ | ✅ | Fondo `#ffffff`, grid 322px + 1fr + gap 140px; mobile orden: título → accordion → support, 24px padding |
| **CTA Final** | ✅ | ✅ | Fondo `#0d1931`, imagen `img-cta-final.png`; mobile ilustración oculta |
| **Footer** | ✅ | ⚠️ | Mobile pendiente de revisión |

---

## 05. Patrones de layout establecidos

- **Padding lateral desktop:** 155px en todas las secciones principales
- **Padding lateral mobile:** 24px uniforme
- **Gap entre imagen y texto:** 140px (cifras, differentiator, FAQ)
- **Columna fija izquierda:** 322px (FAQ, differentiator title block)
- **Mobile breakpoint principal:** `max-width: 991px` (Bootstrap lg)
- **Mobile overrides:** en bloque `<style>` inline de `home.html` (no en `landing.css`)

---

## 06. Componentes / patrones especiales

- **Hover-always-on mobile** (school-cards): replicar reglas `:hover` como reglas normales dentro del media query
- **Pills de curso:** `border-bottom: 3px solid` sin background, sin border-radius
- **Scroll horizontal testimonials:** `overflow-x: auto` + `margin-left: 24px` en first-child / `margin-right: 24px` en last-child (no usar padding en el contenedor)
- **FAQ grid desktop:** `display: grid; grid-template-columns: 322px 1fr; grid-template-rows: auto 1fr` — left en row 1, list span rows 1–2, support en row 2
- **Hero bottom controls mobile:** `.hero__bottom-dots` contiene `[← btn] [dot] [dot] [→ btn]`, reutiliza clases `.hero__ctrl` y `.hero__dot`
- **Course list header con CTA inline:** `.course-list__header` flex row, `align-items: flex-end`, `justify-content: space-between`; izquierda `.course-list__header-text` (eyebrow + H2), derecha `.btn`
- **Schools inner container:** `.schools` es el wrapper `#f4f3f0`; `.schools__inner` es el contenedor oscuro con `border-radius: 24px` y `overflow: hidden`; no usar `.container` de Bootstrap en esta sección
- **Navbar links inline-flex:** evitar whitespace entre `<a>` y el texto interior — los nodos de texto anónimos se convierten en flex items y generan indent visual en mobile

---

## 07. Botones disponibles

| Clase | Uso |
|---|---|
| `.btn-primary` | Rojo `#ee335a`, texto blanco |
| `.btn-outline-white` | Borde blanco, texto blanco (sobre fondos dark) |
| `.btn-outline-red` | Borde `#ee335a`, texto `#ee335a` (sobre fondos light) |
| `.btn-lg` | 16px Inter Bold |
| `.btn-md` | 14px |
| `.btn-sm` | 13px |

---

## 08. Assets en `/Assets`

| Archivo | Uso |
|---|---|
| `Cardio_u_Logo_blanco.svg` | Logo navbar |
| `hero-img-slide-1.png` | Hero slide 1 |
| `img-card-destacada-hero.jpg` | Hero slide 2 |
| `img-cifras.png` | Sección cifras |
| `img-diferentes.png` | Sección differentiator |
| `img-cta-final.png` | Sección CTA final |
| `IMG_card-1.png` … `IMG_card-4.png` | Fotos course cards |
| `img-anticoagulacion.png` / `img-cava.png` / `img-ia.png` / `img-innovacion.png` | Nuevas imágenes de cursos |
| `Icons/tiempo-dm.svg` / `modulos-dm.svg` / `Feature Icon-dm.svg` | Íconos curso (horas, módulos, certificado) |
| `Icons/Check-circle-dm.svg` / `Shield-dm.svg` / `Screen-dm.svg` | Trust icons |
| `Google_logo.svg` / `Wompi_LogoPrincipal 1.svg` | Logos externos |

---

## 09. Cómo retomar con Claude Code

1. Abrir el proyecto: `cd /Users/sergio/Legger/2026-Workflow/CardioU`
2. Decirle a Claude: *"Lee CardioU_ProjectBrief_Mayo2026.md y retomemos el proyecto"*
3. Claude leerá este archivo y tendrá contexto completo sin re-explicaciones

Para consultar el diseño en Figma usar el MCP tool `get_design_context` con `fileKey: gqtZDeE0aTzPRGavReundi` y el `nodeId` de la sección a implementar.

---

## 10. Orden de secciones (actual)

1. Hero
2. Course List (`#cursos`)
3. Schools (`#escuelas`)
4. Cifras
5. Differentiator
6. Testimonials
7. FAQ
8. CTA Final
9. Footer

---

## 11. Pendientes

**Flujo catálogo→curso→lead (en curso):**
- [x] `curso.html` — página de detalle (Opción A: marketplace + tarjeta sticky). Data-driven por `?id=`.
- [ ] **Pedir a LaCardio el temario real** (módulos/lecciones) — hoy placeholder con banner "en validación"; pieza clave para conversión
- [ ] Link de financiación **Wompi** real por curso (hoy botón principal apunta a placeholder `checkout.wompi.co`)
- [ ] Confirmar precio real CAVA ($1.800.000 web vs $1.600.000 dataset) e info de docente (no publicada)
- [ ] Formulario de lead — CTA "Solicitar información" y "Inscribirme y pagar" hoy `href=#`
- [ ] Reemplazar datasets placeholder (`COURSES`) por datos reales del CMS/backend
- [ ] Catálogo: en vistas muy filtradas con pocas destacadas puede quedar hueco de 4 col en una fila
- [ ] Validar mobile de `catalogo.html` y `curso.html` en dispositivo

**Home (pendientes previos):**
- [ ] Revisar/implementar mobile del **Footer**
- [ ] Verificar ajuste visual del hero bottom dots en dispositivo real
- [ ] Validar FAQ layout en desktop tras migración a CSS grid

---

## 12. Historial de sesiones

| Fecha | Trabajo realizado |
|---|---|
| Abr 2026 | Diseño inicial del home en Figma |
| 2026-05-12 | Implementación cifras, botones, course list, differentiator, testimonials |
| 2026-05-13 | Implementación FAQ, CTA final; rename a `home.html`; push a GitHub con PAT |
| 2026-05-21 | Mobile pass completo: schools, cifras, courses, differentiator, testimonials (scroll fix), FAQ (reorder + grid), navbar (sólido, sin borde toggler, H3 links, alineación, btn full width), hero controls (bottom dots con flechas) |
| 2026-05-25 | Ajustes cliente: course-list movida debajo del hero; schools movida debajo de course-list; schools rediseño (outer `#f4f3f0` + inner `#1d386d` border-radius 24px); course cards: layout vertical 4 columnas, img full-width arriba; CTA "Ver todos" movido a header inline; fix navbar mobile "Escuelas" (whitespace anonymous flex item); fix `--font-heading` → `--font-display` en navbar mobile |
| 2026-06-01 | **Buscador en home** (course-list): barra 8 col centrada + autocompletado en vivo (3 letras, resalta, ↑↓Enter/Esc) → `catalogo.html?q=`. **Catálogo nuevo `catalogo.html`** (Opción B de 2 wireframes): hero búsqueda + filtros + cards + "Cargar más" + estado vacío; flujo home→catálogo conectado (botones, buscador, escuelas con `?escuela=`) |
| 2026-06-02 | **Interna de curso `curso.html`** (Opción A de 2 wireframes: marketplace + tarjeta de inscripción sticky). Data-driven por `?id=`, reusa navbar/footer/cards/tokens. Hero oscuro + quick-facts montadas (incl. próxima fecha de inicio) + 2 columnas (qué aprenderás, sobre el curso, temario accordion, docente, para quién, FAQ) + tarjeta sticky con **fecha de inicio destacada + botón principal "Financiar con Wompi"** (flujo externo) + pago + lead. Datos reales del CAVA traídos de lacardio.org. Temario en placeholder con banner "en validación" (pendiente pedirlo a LaCardio) |
| 2026-06-02 | **Refinamiento catálogo con Figma:** superficie crema (`body #f4f3f0`), header sólido no-sticky, hero gradient + breadcrumb + padding 48px; barra de filtros azul flotante (radius-2xl, sombra hover/focus); Duración=radios + Precio=slider; pills hero por escuela (contraste WCAG); buscador + Inscríbete aparecen en barra al hacer scroll; card destacada grande (10/12 centrada, img 464px). **Card destacada en grid `.cat-dcard`** (Figma 2159:493, fondo azul + SVG, texto blanco) como componente compartido en `landing.css`: catálogo grid 10-col (normal span3 / destacada span4, alternando lado por fila); home aplicado a **1 fila** (2 normales + 1 destacada). Botones destacada quedan `#ee335a` (consistencia, no el `#ff0040` del Figma) |
