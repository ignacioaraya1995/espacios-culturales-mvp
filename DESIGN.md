# Design

## Source of truth
- Status: Draft
- Last refreshed: 2026-06-24
- Primary product surfaces: `index.html` static MVP, Explorar, Mapa, Detalle, Reservas, Calendario, Mensajes, Anfitrión.
- Evidence reviewed: `README.md`, `index.html`, `hero.mp4`, Red Alameda Cultural `https://www.redalamedacultural.cl/secciones/espacios-culturales-7550`, Red Alameda Cultural `https://www.redalamedacultural.cl/actividades?modulo=2151`, feedback de Julio Pertuze del 2026-06-24.

## Brand
- Personality: cultural, operativo, claro, institucional sin sentirse burocrático.
- Trust signals: MVP declarado, fuente Red Alameda visible, datos de agenda/instituciones trazables, disponibilidad y precios legibles.
- Avoid: marketing vacío, fotos o widgets externos con textos incrustados que compitan con el mockup, secciones decorativas sin acción.

## Product goals
- Goals: mostrar vitrina de espacios culturales para arriendo, programación cultural y activaciones de marca; conectar cada espacio con mapa del sector.
- Non-goals: resolver gobernanza de la red, pagos reales, booking real, scraping automático en producción.
- Success signals: usuario entiende qué se arrienda, qué programación existe, cómo llegar y qué hay alrededor.

## Personas and jobs
- Primary personas: gestor de espacio cultural, director ejecutivo de institución miembro, marca/empresa que busca activación, productor cultural, visitante/turista cultural.
- User jobs: evaluar un venue, revisar agenda cultural, encontrar contacto, planificar llegada y servicios cercanos.
- Key contexts of use: desktop para revisión comercial; mobile para exploración rápida y llegada al lugar sin salir del MVP.

## Information architecture
- Primary navigation: Explorar, Mapa, Reservas, Mensajes, Calendario, Dashboard Anfitrión.
- Core routes/screens: home/listado, mapa sectorial, ficha detalle, reserva simulada, agenda/calendario, chat simulado, panel anfitrión.
- Content hierarchy: valor de red, búsqueda, mapa/servicios cercanos, categorías, fichas, detalle de entorno, reserva.

## Design principles
- Principle 1: Primero utilidad operativa, luego narrativa cultural.
- Principle 2: Toda fuente externa debe verse limpia o quedar como referencia textual.
- Tradeoffs: imágenes externas públicas ayudan a contextualizar, pero si llegan como piezas con texto incrustado se reemplazan por chips o links limpios.

## Visual language
- Color: base cream/warm-white, énfasis sky blue, texto charcoal.
- Typography: DM Sans para display, Inter para UI, JetBrains Mono para datos.
- Spacing/layout rhythm: grids densos, bandas sin cards anidados.
- Shape/radius/elevation: radios moderados, bordes suaves, sombras mínimas.
- Motion: transiciones cortas; respetar reduced motion.
- Imagery/iconography: video local para hero, iconos SVG existentes, fotos públicas de Red Alameda recortadas para evitar textos/botones incrustados.

## Components
- Existing components to reuse: searchbar, category row, listing card, PDP, booking widget, dashboard chrome.
- New/changed components: Red Alameda brief, scraped space cards, pop-up space detail modal, internal agenda cards, OpenStreetMap sector map panel with all-place pins, Mapa tab with service search.
- Variants and states: responsive one-column mobile for brief, agenda and sector map.
- Token/component ownership: tokens en `:root`; componentes en CSS inline de `index.html`.

## Accessibility
- Target standard: basic WCAG AA intent.
- Keyboard/focus behavior: controls reachable, links explicit, focus-visible retained.
- Contrast/readability: text over images avoided unless controlled by local overlay.
- Screen-reader semantics: section labels and link labels kept meaningful.
- Reduced motion and sensory considerations: existing reduced-motion hero fallback retained.

## Responsive behavior
- Supported breakpoints/devices: desktop, tablet, mobile down to 360px.
- Layout adaptations: Red Alameda brief, agenda and sector panels collapse to one column.
- Touch/hover differences: mobile search keeps bottom-sheet trigger.

## Interaction states
- Loading: remote images are not required for core flow.
- Empty: listing empty state unchanged.
- Error: broken external links do not block booking mockup.
- Success: booking/payment/chat remain simulated via existing toasts.
- Disabled: existing button disabled styles retained.
- Offline/slow network, if applicable: MVP still usable without external Red Alameda media because core data is local.

## Content voice
- Tone: directo, institucional, comercial-cultural.
- Terminology: espacio cultural, arriendo venue, oferta cultural, activaciones, mapa del sector, turismo cultural.
- Microcopy rules: declarar MVP/mockup; no prometer pagos, reservas ni datos reales donde están simulados.

## Implementation constraints
- Framework/styling system: single-file HTML/CSS/JS, no build.
- Design-token constraints: use existing tokens; no new dependency.
- Performance constraints: keep remote assets limited and lazy where possible; OpenStreetMap iframe and Red Alameda photos load lazily. OSM attribution stays visible outside embed clutter.
- Compatibility constraints: opening `index.html` directly should work.
- Test/screenshot expectations: run `node --check` on extracted script and inspect desktop/mobile after UI changes.

## Open questions
- [ ] Confirmar si se usarán logos limpios entregados por cada institución o solo nombres/fotos públicas desde Red Alameda / owner: cliente / impact: mejora visual y derechos de uso.
- [x] Confirmar nivel de mapa real esperado: usar mapa gratuito/open-source con OpenStreetMap en el MVP / owner: cliente / impact: producción.
- [ ] Confirmar quién entrega feedback en gobernanza: directores ejecutivos, administradores de espacios, marcas, turistas culturales / owner: cliente / impact: flujos y dashboard.
