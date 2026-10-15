# CLAUDE.md — Calco (demo estudio de tatuajes)
Web demo de un estudio de tatuajes ficticio ("Calco") para enseñar a dueños de estudios: un único `index.html`, sin backend, reserva por WhatsApp/email.

## Stack
- HTML + CSS + JavaScript sin dependencias, todo en `index.html`.
- Google Fonts: Shrikhand (titulares, aire de rótulo pintado) + Archivo (texto).
- Ilustraciones 100 % SVG generadas en código (sin fotos ni imágenes externas).
- Despliegue estático: Cloudflare Pages (repo GitHub `AleexX26/demo-tatuaje-2`), vale también Netlify, Vercel o GitHub Pages.

## Arquitectura
- `index.html`
  - `<script>` al principio del `<head>`: **datos editables** `ESTUDIO`, `ARTISTAS`, `TRABAJOS`, `FLASH`.
  - `<style>`: tokens en `:root` (papel, tinta, violeta de calco, acento rojo) y modo oscuro con `prefers-color-scheme`.
  - `<svg>` oculto con defs compartidas: patrones `#punteado`, `#punteado-denso`, `#rayado`; filtros `#temblor` (línea de calco), `#goma` (sello), `#sangrado` (borde de tinta del entintado).
  - `<script>` final: `MOTIVOS` (dibujos de flash en caja 200×200), `svgPieza()` (capa calco violeta + capa tinta + nombre), `svgSello()`, portada entintable, galería con filtros, vista previa, lightbox, artistas, flash, pasos, plano, FAQ y formulario.
- Flujo de reserva: botones "Quiero algo así" / "Lo quiero" / "Reservar con…" llaman a `rellenarReserva()` → el formulario genera texto → abre `wa.me` o `mailto:`.
- `PRODUCT.md` y `.impeccable/` son contexto de la skill de diseño (no se publican: `.impeccable/` está en `.gitignore`).

## Comandos
- Ver en local: abrir `index.html` con doble clic, o `npx --yes http-server -p 4321 -c-1 .` (config en `.claude/launch.json`, nombre `web`).
- Sin build ni tests. Deploy: push a `main` → Cloudflare Pages (preset "None", build command vacío, output `/`).

## Decisiones
- 2026-10-15: dirección de arte "Calco que se entinta": cada dibujo aparece como línea violeta de stencil térmico y se entinta en negro/rojo (scroll, cursor o al aparecer). El violeta solo vive en dibujos sin entintar; el rojo es el único acento (acciones, precios, sello).
- 2026-10-15: datos de contacto como marcadores (`[DIRECCIÓN]`, `[CIUDAD]`, `[BARRIO]`, `[CORREO]`, `[WHATSAPP]`, `[INSTAGRAM]`, `[INSTAGRAM_<ARTISTA>]`) por petición del usuario; nada tomado de las webs de referencia.
- 2026-10-15: sin datos válidos, WhatsApp abre `https://wa.me/?text=…` (elegir contacto) y el email abre `mailto:` sin destinatario, para que la demo funcione igual.
- 2026-10-15: modo oscuro = "pared del estudio": fondo tinta y los dibujos siguen sobre hojas de papel (no se invierten).
- 2026-10-15: un único archivo en vez de Astro/React: no aporta nada a una landing estática y facilita que el cliente lo edite.

## Patrones reutilizables
- **Dibujo entintable**: dos copias del mismo SVG, `.calco` (violeta, filtro `#temblor`, desplazada 1.6px) debajo y `.tinta` encima revelada con `clip-path` (galería) o con `<mask>` de círculos (portada); en `index.html`, `svgPieza()` y `dibujoHero()`.
- **Estilos de tatuaje por clase CSS**: el mismo motivo cambia según `.e-fine`, `.e-black`, `.e-real`, `.e-trad`, `.e-letter` (clases `o/r/k/p/s/tb/tf`).
- **Sello de goma**: filtro `#goma` (feTurbulence + feColorMatrix) sobre SVG o HTML (`.agenda`, `.estampa`, sello del artista).
- **Reserva sin backend**: `mensaje()` + `wa.me/?text=` o `mailto:?subject&body`, con estado "Ficha lista" y botón copiar.
- **Capturas sin interfaz**: script CDP con Edge headless (`--remote-debugging-port`, `Emulation.setEmulatedMedia` para claro/oscuro) útil cuando el panel del navegador está pausado.

## Última actualización
2026-10-15
