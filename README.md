# Sitio estático F1 - Demo

Página estática de ejemplo sobre la Fórmula 1 con imágenes, enlaces, una tabla y un formulario.

Cómo usar:

- Abrir `index.html` en un navegador (doble click o "Abrir con").
- Las imágenes de ejemplo se esperan en la carpeta `images/` dentro del proyecto. Si no existen, reemplazar con rutas reales o usar imágenes en línea.

Archivos:

- `index.html` - Estructura principal (encabezado, nav, main, footer).
- `styles.css` - Estilos básicos.
- `README.md` - Esta documentación.
 - `ACCESSIBILITY.md` - Declaración de accesibilidad y medidas aplicadas (WCAG quick reference).

Notas:

- El formulario no envía datos a un servidor (action="#"). Para probar envío, cambiar `action` a un endpoint real.
- Las imágenes en `index.html` son referencias locales: `images/f1-car-1.jpg` y `images/podium.jpg`.

Accesibilidad:

- Se añadió un enlace de salto (skip link), roles landmark ARIA, mejoras en formularios, tablas y foco visible.
- Revisa `ACCESSIBILITY.md` para un mapeo a las pautas WCAG y pasos de prueba.
