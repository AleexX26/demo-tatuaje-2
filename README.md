# Calco · demo de web para estudio de tatuajes

Web de una sola página para un estudio de tatuajes: galería filtrable por estilo y artista, fichas de artistas, hoja de flash con precio cerrado, cómo funciona, cuidados y preguntas frecuentes, y una reserva que prepara el mensaje de WhatsApp o email. Todo en `index.html`, sin backend y sin dependencias.

## Cómo personalizarla

Abre `index.html` y edita el bloque **DATOS DE LA WEB** del principio:

| Qué | Dónde |
| --- | --- |
| Nombre, ciudad, dirección, horario, email, WhatsApp, Instagram, color de acento | `const ESTUDIO` |
| Artistas (nombre, especialidad, frase, estilos, Instagram, foto) | `const ARTISTAS` |
| Trabajos de la galería (título, estilo, artista, zona, imagen) | `const TRABAJOS` |
| Flash (nombre, precio, tamaño, disponible, imagen) | `const FLASH` |

- Sustituye los marcadores `[DIRECCIÓN]`, `[CIUDAD]`, `[BARRIO]`, `[CORREO]`, `[WHATSAPP]`, `[INSTAGRAM]` y los Instagram de cada artista.
- WhatsApp va con prefijo de país y sin espacios: `34600111222`.
- Para añadir algo, copia un bloque `{ ... }` y cámbialo. Los filtros y los desplegables de la reserva se generan solos.
- Si un trabajo o flash no tiene `imagen`, la web dibuja una ilustración SVG con su nombre. Para usar fotos, crea una carpeta `img/` y pon la ruta: `imagen: "img/golondrina.jpg"`.
- El título y la descripción para Google están en las primeras líneas del `<head>`.

## Publicar

- **Cloudflare Pages**: Workers & Pages → Create → Pages → Connect to Git → este repositorio. Framework preset: *None*. Build command: vacío. Build output directory: `/`.
- **Netlify / Vercel**: importar el repositorio sin comando de build.
- **GitHub Pages**: Settings → Pages → Deploy from branch → `main` / root.

Para verla en local basta con abrir `index.html` en el navegador.
