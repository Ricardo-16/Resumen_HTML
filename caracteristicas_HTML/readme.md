# Detección de Características en HTML5

HTML5 nos proporciona diversas herramientas para resolver problemas y mejorar la experiencia en la web, como "Canvas", "Vídeo" y "Geolocalización". Para garantizar que estas características sean compatibles con distintos navegadores, se pueden utilizar varios métodos de detección.

# Construcción del DOM

Los navegadores generan un "Document Object Model (DOM)", una estructura de objetos que representan los elementos HTML en la página web. Cada elemento del DOM tiene características únicas que se pueden manipular mediante JavaScript.

# Métodos para Detectar Soporte en el Navegador

Existen cuatro formas principales para comprobar si una propiedad es compatible con el navegador:

Verificar si la propiedad existe en un objeto global**.
Crear un elemento y comprobar si la propiedad existe en él**.
Crear un elemento, revisar si el método existe y comprobar su valor de retorno**.
Crear un elemento, asignarle un valor y verificar si lo mantiene**.

# Modernizr: Detección Simplificada

Modernizr es una biblioteca que facilita la detección de compatibilidad con "HTML5 y CSS3". Para utilizarla, se debe incluir en la etiqueta `<head>`:

```html
<script src="modernizr.min.js"></script>
```

Modernizr crea automáticamente un objeto llamado `Modernizr`, que contiene propiedades booleanas para cada característica soportada.

Ejemplo de detección de soporte para Canvas:

```javascript
if (Modernizr.canvas) {
} else {
}
```

# Características de HTML5

# Canvas

El elemento `<canvas>` permite dibujar gráficos mediante JavaScript. Se verifica su compatibilidad comprobando si el método `getContext()` existe:

```javascript
function supports_canvas() {
  return !!document.createElement("canvas").getContext;
}
```

# Vídeo

El elemento `<video>` permite la reproducción de contenido multimedia. Los navegadores pueden soportar diferentes formatos según el códec utilizado. Se puede verificar su compatibilidad con la función `canPlayType()`

```javascript
var video = document.createElement("video");
console.log(video.canPlayType("video/mp4"));
```

# Almacenamiento Local

El almacenamiento local permite guardar datos en el navegador. Su compatibilidad se puede verificar con:

```javascript
function supports_local_storage() {
  try {
    return "localStorage" in window && window["localStorage"] !== null;
  } catch (e) {
    return false;
  }
}
```

# Web Workers

Los Web Workers permiten ejecutar procesos en segundo plano sin afectar la interfaz del usuario. Se puede comprobar su compatibilidad con:

```javascript
function supports_web_workers() {
  return !!window.Worker;
}
```

# Aplicaciones Fuera de Línea

HTML5 permite el desarrollo de aplicaciones web que pueden funcionar sin conexión a Internet, aunque los cambios no se guardarán hasta que haya conexión nuevamente.

# Geolocalización

Permite conocer la ubicación del usuario a través de su dirección IP o GPS. Se puede detectar con:

```javascript
function supports_geolocation() {
  return !!navigator.geolocation;
}
```

# Tipos de Entrada en Formularios

El elemento <input> es una etiqueta en HTML que se utiliza para crear campos interactivos en un formulario, donde los usuarios pueden ingresar datos. Dependiendo del tipo de input, este puede aceptar diferentes tipos de datos (texto, contraseñas, fechas, etc.) y realizar acciones como enviar información a un servidor.
como fecha, color y correo electrónico. Su compatibilidad se puede verificar creando un elemento:

```javascript
var input = document.createElement("input");
```

# Placeholder Text

El atributo "placeholder" muestra un texto dentro de los campos de entrada hasta que el usuario comienza a escribir, tambien puede ser acompañado de un "required"
Ejemplo:
<input type="text" placeholder="" name="" id="" required>

# Autofocus

Permite que un campo de entrada tenga el foco automáticamente al cargar la página:

`````javascript
function supports_input_autofocus() {
  var i = document.createElement("input");
  return "autofocus" in i;
}

# Microdatos

Los microdatos permiten añadir información adicional a la página web, como detalles del autor. Se verifica su compatibilidad con:

````javascript
function supports_microdata_api() {
  return !!document.getItems;
}
`````
