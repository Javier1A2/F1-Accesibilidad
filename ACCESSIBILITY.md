# Declaración de accesibilidad - Sitio F1 (demo)

Este documento describe las mejoras de accesibilidad aplicadas a la página estática y cómo se alinean con las pautas WCAG (Quick Reference / Design and Develop Overview).

Resumen de medidas aplicadas

- Estructura semántica y roles
  - Uso de landmarks: `role="banner"`, `role="navigation"`, `role="main"`, `role="contentinfo"` para facilitar la navegación con tecnología asistiva.
  - Títulos con `id` y `aria-labelledby` en secciones para referencias claras.

- Saltar al contenido (Skip link)
  - Se añadió un enlace de salto al contenido principal que es visible al recibir foco desde el teclado.

- Imágenes
  - Atributos `alt` descriptivos en imágenes. Se evita el uso de alt vacíos para imágenes significativas.

- Tablas
  - Se añadieron atributos `scope="col"` en encabezados y `caption` para describir la tabla.

- Formularios
  - Uso de `label` explícitos, `fieldset` y `legend` para agrupar campos.
  - `aria-required="true"` en campos obligatorios.
  - Un contenedor con `role="status"` y `aria-live="polite"` para mostrar mensajes de estado (p. ej. envío de formulario).

- Foco y contraste
  - Estilos visibles y grandes para el foco de teclado (outline claramente visible).
  - Contrastes mejorados entre fondo y elementos interactivos (botones y entradas) para legibilidad.

- Accesibilidad para enlaces externos
  - Los enlaces que abren en una nueva ventana incluyen `rel="noopener noreferrer"` y el texto aclara que se abrirá una ventana nueva.

Mapeo rápido a WCAG (Quick Reference)

- Perceivable
  - Text alternatives (Images): etiquetas `alt` descriptivas.
  - Captions and labels (Forms and Tables): `caption`, `label`, `legend`.

- Operable
  - Keyboard accessible (Skip link y foco visible): permite navegar sin ratón.
  - No contenido que provoque convulsiones (no hay animaciones intermitentes).

- Understandable
  - Uso de etiquetas y descripciones claras en formularios y tablas.

- Robust
  - Uso de roles ARIA sencillos y atributos compatibles con tecnologías asistivas.

Cómo probar localmente

1. Abre `index.html` en un navegador.
2. Presiona Tab repetidamente para verificar que el enlace "Saltar al contenido" recibe foco y funciona.
3. Usa el lector de pantalla (NVDA, VoiceOver, Narrator) para comprobar landmarks y orden lógico.
4. Ejecuta una revisión rápida con herramientas como Lighthouse, axe-core o la extensión WAVE para identificar problemas adicionales.

Limitaciones y próximos pasos recomendados

- Validación automática: ejecutar axe-core o Lighthouse para identificar problemas concretos.
- Formularios: para que el formulario sea completamente accesible tras el envío, conectar un endpoint y proporcionar mensajes de éxito/errores visibles y accesibles.
- Contraste: revisar colores con una herramienta de contraste para asegurar cumplimiento WCAG AA/AAA según la necesidad.

Si quieres que ejecute pruebas automáticas (axe, Lighthouse) en este proyecto o que haga que el formulario envíe datos y muestre mensajes accesibles, indícalo y lo implemento.
