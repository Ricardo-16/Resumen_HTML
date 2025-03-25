# Guía para trabajar con el elemento `<canvas>` en HTML5

# Descripción

HTML5 define el elemento `<canvas>` como “un lienzo dependiente de resolución que se puede usar para renderizar gráficos, gráficos de juegos u otras imágenes visuales en tiempo real”. Un canvas es un rectángulo en tu página donde puedes usar JavaScript para dibujar lo que quieras.

# Soporte Básico para Canvas

El soporte para `<canvas>` está disponible en los siguientes navegadores:

- **Firefox**: 3.0+
- **Safari**: 3.0+
- **Chrome**: 3.0+
- **Opera**: 10.0+
- **Internet Explorer**: Requiere la librería de terceros `explorercanvas` (1.0+)
- **iPhone**: 1.0+
- **Android**: 1.0+

# 1. Estructura Básica del Canvas

Un canvas comienza vacío y no tiene contenido ni borde propio. El código básico para agregar un canvas a tu página es el siguiente:

```html
<canvas width="300" height="225"></canvas>
```

Puedes agregar un borde para que sea visible:

```html
<canvas width="300" height="225" style="border:1px dashed #000;"></canvas>
```

Es posible tener múltiples elementos `<canvas>` en la misma página. Cada uno tendrá su propio estado y se accederá mediante su `id`:

```html
<canvas id="a" width="300" height="225"></canvas>
```

Accediendo al canvas en JavaScript:

```javascript
var a_canvas = document.getElementById("a");
```

# 2. Dibujando Formas Simples

Para comenzar a dibujar, puedes utilizar la siguiente función de ejemplo para dibujar un rectángulo dentro del canvas:

```html
<canvas id="b" width="300" height="225"></canvas>
<button onclick="draw_b()">Click to draw on this canvas</button>
```

```javascript
function draw_b() {
  var b_canvas = document.getElementById("b");
  var b_context = b_canvas.getContext("2d");
  b_context.fillRect(50, 25, 150, 100);
}
```

3.  Contexto de Dibujo

Cada canvas tiene un "contexto de dibujo" donde se definen todos los métodos para dibujar. Para obtener el contexto 2D, se utiliza el método `getContext("2d")`:

```javascript
var context = canvas.getContext("2d");
```

# 3.1. ¿Existen contextos 3D?

Aún no. Aunque algunos proveedores han experimentado con APIs de canvas 3D, ninguna ha sido estandarizada. HTML5 menciona que probablemente en el futuro haya soporte para un contexto 3D.

# 4. Métodos y Propiedades para Dibujar

En el contexto de dibujo, hay varios métodos disponibles para dibujar diferentes formas y manipular el canvas. Un ejemplo de cómo dibujar un círculo es el siguiente:

```javascript
context.beginPath();
context.arc(x, y, radius, 0, Math.PI * 2, false);
context.closePath();
context.strokeStyle = "#000";
context.stroke();
```

Esto dibuja un círculo con un borde negro.

# 5. Interacción con el Canvas

Puedes hacer que el canvas sea interactivo. Por ejemplo, capturar eventos de clic y usarlos para realizar acciones en el canvas. Aquí tienes un ejemplo de cómo manejar un clic en el canvas:

```javascript
var canvas = document.getElementById("myCanvas");
canvas.addEventListener("click", function (e) {
  var x = e.pageX - canvas.offsetLeft;
  var y = e.pageY - canvas.offsetTop;
  alert("Clic en: " + x + ", " + y);
});
```

# 6. Ejemplo: Juego de Halma

En este ejemplo, se crea un juego en el canvas con un tablero y piezas. Cuando el usuario hace clic en una celda, el juego verifica si se hizo clic en una pieza o una celda vacía.

# Obtener la posición del clic:

```javascript
function getCursorPosition(e) {
  var x, y;
  if (e.pageX != undefined && e.pageY != undefined) {
    x = e.pageX;
    y = e.pageY;
  } else {
    x =
      e.clientX +
      document.body.scrollLeft +
      document.documentElement.scrollLeft;
    y =
      e.clientY + document.body.scrollTop + document.documentElement.scrollTop;
  }
  x -= gCanvasElement.offsetLeft;
  y -= gCanvasElement.offsetTop;
  return new Cell(Math.floor(y / kPieceHeight), Math.floor(x / kPieceWidth));
}
```

# 6 Dibujar el tablero:

El tablero se dibuja con líneas verticales y horizontales utilizando `moveTo()` y `lineTo()`:

```javascript
gDrawingContext.beginPath();
for (var x = 0; x <= kPixelWidth; x += kPieceWidth) {
  gDrawingContext.moveTo(0.5 + x, 0);
  gDrawingContext.lineTo(0.5 + x, kPixelHeight);
}
for (var y = 0; y <= kPixelHeight; y += kPieceHeight) {
  gDrawingContext.moveTo(0, 0.5 + y);
  gDrawingContext.lineTo(kPixelWidth, 0.5 + y);
}
gDrawingContext.strokeStyle = "#ccc";
gDrawingContext.stroke();
```

# 6 Dibujar las piezas:

Las piezas se dibujan como círculos y si están seleccionadas, se rellenan con un color sólido:

```javascript
function drawPiece(p, selected) {
  var x = p.column * kPieceWidth + kPieceWidth / 2;
  var y = p.row * kPieceHeight + kPieceHeight / 2;
  var radius = kPieceWidth / 2 - kPieceWidth / 10;

  gDrawingContext.beginPath();
  gDrawingContext.arc(x, y, radius, 0, Math.PI * 2, false);
  gDrawingContext.closePath();
  gDrawingContext.strokeStyle = "#000";
  gDrawingContext.stroke();

  if (selected) {
    gDrawingContext.fillStyle = "#000";
    gDrawingContext.fill();
  }
}
```

# 6 Redibujar el tablero después de cada cambio:

Cada vez que ocurre un cambio en el juego, el tablero completo se redibuja para reflejar el nuevo estado del juego:

```javascript
gDrawingContext.clearRect(0, 0, kPixelWidth, kPixelHeight);
```

Luego, se vuelve a dibujar el tablero y las piezas en sus nuevas posiciones.
