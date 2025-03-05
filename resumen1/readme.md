# Tipos De Mime

Este encabezado determina el "tipo de contenido" o "tipo MIME" del recurso y le dice al navegador cómo debe representarse.Tambien estos sirven para identificar que ripo de archivo estas cargando  
Por ejemplo:

- `text/html` para páginas HTML
- `image/jpeg` para imágenes JPEG
- `image/png` para imágenes PNG
- `application/javascript` para archivos JavaScript
- `text/css` para hojas de estilo CSS

Cada tipo de contenido tiene su propio tipo MIME, y la web se basa en estos tipos para funcionar correctamente.

## Historia

La historia de los tipos MIME se remonta a los primeros días de la web. Los primeros servidores web no enviaban el encabezado `Content-Type` porque aún no existía. Fue inventado en 1994. Debido a razones de compatibilidad, algunos navegadores populares pueden ignorar este encabezado en ciertas circunstancias, una técnica conocida como "rastreo de contenido".

## Importancia en la Web Actual

En general, todo lo que ves en la web (páginas HTML, imágenes, scripts, videos, PDFs, etc.) se te sirve con un tipo MIME específico en el encabezado. Esto asegura que tu navegador sepa cómo manejar cada tipo de archivo correctamente.

Recuerda, aunque no veas estos encabezados, están trabajando en segundo plano para que tu experiencia en la web sea fluida y eficiente.
