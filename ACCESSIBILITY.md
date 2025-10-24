# Declaración de accesibilidad - Sitio F1 (demo)

Este documento describe las mejoras de accesibilidad aplicadas a la página estática y cómo se alinean con las pautas WCAG (Quick Reference / Design and Develop Overview).

Resumen de medidas aplicadas

- Estructura semántica y roles
  - Uso de elementos semánticos nativos (`<header>`, `<nav>`, `<main>`, `<footer>`) en lugar de roles ARIA redundantes. Esto asegura que los lectores de pantalla como NVDA detecten únicamente las regiones principales relevantes (header, navigation, main, footer) y evita la duplicación de landmarks.
  - Se añadieron `aria-label` explícitos a las regiones principales con los nombres solicitados: `aria-label="header"`, `aria-label="nav"`, `aria-label="main"`, `aria-label="footer"`. Esto hace que NVDA muestre exactamente esos nombres en la lista de regiones.
  - Títulos con `id` en secciones; las secciones usan encabezados (`<h2>`) y no usan `aria-labelledby` para evitar que lectores de pantalla las listaran como regiones adicionales. Esto ayuda a que NVDA muestre principalmente header, navigation, main y footer.

- Saltar al contenido (Skip link)
  - Se añadió un enlace de salto al contenido principal que es visible al recibir foco desde el teclado.
  - El enlace de salto (`.skip-link`) está implementado y visible al recibir foco. Se mejoraron los estilos para que tenga buen contraste y sea fácil de usar con teclado.

- Imágenes
  - Atributos `alt` descriptivos en imágenes. Se añadió texto alternativo más descriptivo (por ejemplo: "Foto de Max Verstappen, piloto de Red Bull Racing").
  - En esta versión las fotos de la galería se consideran decorativas (mientras el texto de la leyenda repita la información) y por tanto se marcaron con `alt=""` para que sean ignoradas por lectores de pantalla.
  - Se añadió `loading="lazy"` a imágenes de la galería para mejorar rendimiento y experiencia en dispositivos con lectores de pantalla.

- Tablas
  - Se añadieron atributos `scope="col"` en encabezados y `caption` para describir la tabla.
  - Además, las celdas de posición (primera columna) ahora son encabezados de fila: `<th scope="row">` para mejorar la lectura por AT.

- Formularios
  - Uso de `label` explícitos y ahora los campos están agrupados dentro de un `fieldset` con `legend` para mayor claridad.
  - Se añadieron `aria-required="true"` en los campos obligatorios (`nombre`, `email`).
    - Se añadió un contenedor con `role="status"` y `aria-live="polite"` (id `form-status`) para comunicar mensajes tras el envío del formulario. El script actual muestra mensajes ahí, pero evita mover el foco automáticamente para no desorientar a usuarios de teclado; los errores por campo se muestran en spans inline con `aria-describedby` y el foco se mueve al primer campo inválido.
    - Se añadió un control para elegir el piloto favorito mediante radios. En la versión actual ya no se muestra un mensaje breve automáticamente al cambiar la selección de piloto (para evitar anuncios inesperados mientras el usuario completa el formulario). Los mensajes se muestran en `#form-status` únicamente para errores (por ejemplo, "Selecciona un piloto favorito") y para la confirmación tras el envío del formulario.
      - El mensaje de envío incluye el nombre del usuario (si ya lo ingresó), el piloto seleccionado y el equipo asociado, obtenido leyendo la tabla de clasificación presente en la página. Ejemplo: "Gracias por suscribirte. Felicidades, Javier! Apoyas a Max Verstappen del equipo Red Bull Racing."
        - Se añadió un área de análisis (`#pilot-analysis`) que puede mostrar estadísticas básicas del piloto seleccionado (posición y puntos) extraídas de la tabla en la página. En la versión actual no se preselecciona ningún piloto al cargar la página; el área de análisis permanece oculta hasta que el usuario envíe el formulario o solicite ver el análisis. Además, el valor por defecto del campo "Interés" ahora es "Resultados y clasificaciones" (antes era "Estadísticas y análisis"). El contenido del análisis es accesible mediante `aria-live` cuando se muestra.
    - Se añadió un script JS que valida el formulario en el cliente, muestra mensajes en `#form-status` y mueve el foco a ese contenedor cuando hay mensajes (errores o éxito). Esto permite que los lectores de pantalla anuncien el resultado inmediatamente.

- Foco y contraste
  - Estilos visibles y grandes para el foco de teclado; se usa `:focus-visible` cuando está disponible para evitar mostrar outline al clicar con ratón.
  - Se mejoraron estilos visuales del enlace de salto y el color del foco para mantener contraste suficiente.
    - Se ajustó el color de acento a `#b71c1c` para mejorar contraste en botones y encabezados y acercarse a WCAG 2.1 AA; se recomienda validar con una herramienta de contraste para casos límite.

- Accesibilidad para enlaces externos
  - Los enlaces que abren en una nueva ventana incluyen `rel="noopener noreferrer"` y el texto aclara que se abrirá una ventana nueva.
  - Se añadió un texto accesible y oculto visualmente para indicar que el enlace al sitio oficial se abre en una nueva pestaña: `Sitio oficial (se abre en nueva pestaña)`.

  ## Interacción "Otro" en el formulario de piloto favorito

  - Se añadió en el formulario una opción de selección "Otro" después de los 5 primeros pilotos de la clasificación.
  - Al seleccionar "Otro" se muestra un campo de texto (`#piloto-otro-text`) donde el usuario puede escribir el nombre del piloto. El contenedor tiene `aria-hidden` cuando está oculto y se remueve ese atributo cuando se muestra.
  - El campo de texto tiene un `span` de error con id `error-piloto-otro` que usa `aria-live="assertive"` para anunciar errores.
  - Reglas de validación accesible:
    - Si el usuario selecciona "Otro", el campo de texto se vuelve obligatorio. Si está vacío, se muestra el mensaje de error y el foco se mueve al campo.
    - Si se selecciona un piloto de la lista (top 5), el campo "Otro" permanece oculto y sus errores se limpian.

  Cómo probarlo (teclado y NVDA):

  1. Navegar al formulario con la tecla Tab hasta llegar al grupo "Elige tu piloto favorito".
  2. Verás radios con los 5 primeros pilotos y una opción "Otro".
  3. Selecciona "Otro" (con la barra espaciadora). El campo de texto aparecerá y recibirá foco automáticamente.
  4. Intenta enviar el formulario sin escribir nada en el campo "Otro": NVDA anunciará el error, el `span` de error será visible y el foco quedará en el campo.
  5. Escribe un nombre y vuelve a enviar: se mostrará el mensaje de éxito en `#form-status` (anunciado por `aria-live`) y el formulario se restablecerá.

  Notas de accesibilidad técnica:

  - Evitar `aria-hidden` permanente en elementos que pueden recibir foco; aquí `aria-hidden` se usa sólo mientras el campo está oculto y se elimina cuando se muestra.
  - Asegurar que los `id` de los spans de error son únicos y referenciados desde `aria-describedby` cuando hay error.
  - Mantener el flujo de foco (no forzar saltos inesperados) y sólo mover foco al primer campo inválido para ayudar a usuarios de teclado y lectores de pantalla.

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
