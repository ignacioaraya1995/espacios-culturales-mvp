# Handoff - Espacios Culturales MVP

Fecha: 2026-06-24

## Estado actual

- Deploy online: https://ignacioaraya1995.github.io/espacios-culturales-mvp/
- Repositorio: https://github.com/ignacioaraya1995/espacios-culturales-mvp
- Rama: `main`
- Ultimo deploy de app verificado: commit `1536102` (`Update cultural map MVP`)
- App: HTML estatico en `index.html`; no build, no dependencias.
- Documentacion de diseno: `DESIGN.md`

## Feedback incorporado

- Vitrina para arriendo de venues, oferta cultural y activaciones de marca.
- Red Alameda Cultural como fuente publica de instituciones, fotos y agenda.
- Todo debe verse dentro del MVP; no mandar al usuario fuera para revisar datos.
- Fotos de espacios visibles, incluyendo Centro Cultural CIMA y Cine Arte Alameda.
- Mapa gratuito/open-source con OpenStreetMap.
- Mapa sectorial con informacion de llegada, estacionamientos, gastronomia, hoteleria y rutas patrimoniales.

## Cambios principales

- Nueva seccion Red Alameda en `Explorar`.
- 6 tarjetas de espacios scrapeados desde Red Alameda:
  - Centro Cultural CIMA - modulo `2242`
  - Cine Arte Alameda - modulo `2243`
  - Libreria GAM - modulo `2244`
  - Museo Nacional de Bellas Artes - modulo `2245`
  - Museo de la Solidaridad Salvador Allende - modulo `2247`
  - Centro Cultural CEINA - modulo `2142`
- Click en tarjeta/pin/leyenda abre pop-up modal con:
  - foto,
  - nombre,
  - direccion,
  - estado del scrape,
  - modulo fuente,
  - agenda relacionada si existe.
- Nueva opcion `Mapa` en encabezado.
- Nueva pagina `Mapa` con:
  - buscador,
  - filtros,
  - resultados al lado,
  - mockup mapa con pins.
- Filtros de mapa:
  - Todos
  - Espacios
  - Estacionamientos
  - Metro
  - Gastronomia
  - Hoteles
  - Patrimonio
- OpenStreetMap embed usado como base.
- Footer/clutter del iframe OSM se recorto visualmente; atribucion legal queda visible fuera:
  - `Mapa base: © OpenStreetMap contributors / ODbL.`

## Datos scrapeados usados

Fuentes:

- https://www.redalamedacultural.cl/secciones/espacios-culturales-7550
- https://www.redalamedacultural.cl/actividades?modulo=2242
- https://www.redalamedacultural.cl/actividades?modulo=2243
- https://www.redalamedacultural.cl/actividades?modulo=2151

Hallazgos:

- CIMA modulo `2242`: sin actividades publicadas al momento del scrape.
- Cine Arte Alameda modulo `2243`: 4 actividades encontradas:
  - Ale Castillo en concierto - 24 jun 2026, 20:00
  - Tan inmunda y tan feliz (2022) - 26 jun 2026, 20:30
  - Witness for the Prosecution (1957) - 26 jun 2026, 16:30
  - Los fuertes (2019) - 28 jun 2026, 17:00
- Agenda adicional de Red Alameda desde modulo `2151` se muestra como referencia.

## Archivos importantes

- `index.html`: app completa, estilos y JS inline.
- `DESIGN.md`: contrato de diseno y decisiones UX.
- `HANDOFF.md`: este documento.
- `.nojekyll`: mantiene GitHub Pages sirviendo archivos estaticos sin Jekyll.

## Validaciones hechas

- `node --check` sobre JS extraido desde `index.html`: OK.
- Smoke browser local con Playwright + Chrome sistema:
  - tab `Mapa` visible,
  - buscador `estacionamiento` + filtro `Estacionamientos` devuelve 2 resultados y 2 pins,
  - click Cine Arte Alameda abre modal,
  - modal muestra 4 actividades,
  - mapa tiene 6 pins,
  - sin overflow horizontal.
- GitHub Pages verificado con HTML online que contiene `page-mapa`.

## Deploy

Comandos usados:

```bash
git add index.html DESIGN.md
git commit -m "Update cultural map MVP"
git push origin main
```

GitHub Pages URL verificada:

```text
https://ignacioaraya1995.github.io/espacios-culturales-mvp/
```

## Pendientes sugeridos

- Reemplazar direcciones aproximadas por geocoding real o coordenadas confirmadas.
- Separar datos Red Alameda a JSON local si empieza a crecer.
- Agregar busqueda real por cercania cuando haya coordenadas por espacio.
- Definir si fotos publicas de Red Alameda se pueden usar en produccion o si cada institucion entregara assets limpios.
- Confirmar fuente oficial para estacionamientos, hoteles y gastronomia antes de produccion.
- Si se mantiene OpenStreetMap, usar Leaflet o MapLibre cuando se necesite interaccion real. Ahora es mockup sin dependencia nueva.

## Notas de repo

- `.omc/state/hud-stdin-cache.json` aparece modificado por tooling local. No se debe commitear salvo que el usuario lo pida.
- App no tiene build step. Para probar local:

```bash
open index.html
```

O con servidor local:

```bash
python3 -m http.server 4173
```

