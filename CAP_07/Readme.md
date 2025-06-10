
### EL PASADO, EL PRESENTE Y EL PASADO, PRESENTE Y FUTURO DEL ALMACENAMIENTO LOCAL EL FUTURO DEL ALMACENAMIENTO LOCAL PARA APLICACIONES WEB

 **HTML5 Storage y Web SQL Database**

Este proyecto explora las capacidades de almacenamiento local en aplicaciones web utilizando **HTML5 Storage**, con ejemplos prácticos, explicaciones sobre su funcionamiento y limitaciones, así como una discusión sobre las tecnologías alternativas como **Web SQL Database** y **IndexedDB**.

**HTML5 Storage**
 **¿Qué es HTML5 Storage?**

HTML5 Storage, también conocido como **Web Storage** o **Local Storage**, permite a las aplicaciones web almacenar pares de clave/valor en el navegador del cliente. Este almacenamiento es persistente y no requiere el uso de cookies. Los datos se mantienen incluso después de cerrar el navegador, pero no se envían al servidor a menos que el desarrollador lo decida.
 **Características:**

* **localStorage y sessionStorage**: Los datos se almacenan de forma local en el navegador mediante `localStorage` (persistente) o `sessionStorage` (por sesión).
* **Almacenamiento persistente**: A diferencia de las cookies, los datos no se envían al servidor con cada solicitud.
* **Limitaciones**:

  * **5MB por origen**: El almacenamiento tiene un límite de aproximadamente 5MB por dominio (esto puede variar según el navegador).
  * Los datos solo se almacenan como **cadenas de texto**. Si se desean almacenar otros tipos de datos (como números o objetos), es necesario convertirlos manualmente con funciones como `parseInt()`, `parseFloat()`, o `JSON.parse()`.

**Métodos disponibles**:

* **setItem(key, value)**: Guarda un valor bajo una clave especificada.
* **getItem(key)**: Recupera el valor asociado a una clave.
* **removeItem(key)**: Elimina el valor asociado a una clave.
* **clear()**: Elimina todos los elementos almacenados.
* **length**: Obtiene el número de claves almacenadas.

**Juego Halma**:

Este ejemplo muestra cómo utilizar HTML5 Storage para guardar y recuperar el estado de un juego en progreso. Se guarda información sobre el estado del juego (si está en progreso), la posición de las piezas y el número de movimientos realizados.

 **Guardar el estado del juego**:

```javascript
function saveGameState() {
    if (!supportsLocalStorage()) { return false; }
    localStorage["halma.game.in.progress"] = gGameInProgress;
    for (var i = 0; i < kNumPieces; i++) {
        localStorage["halma.piece." + i + ".row"] = gPieces[i].row;
        localStorage["halma.piece." + i + ".column"] = gPieces[i].column;
    }
    localStorage["halma.selectedpiece"] = gSelectedPieceIndex;
    localStorage["halma.selectedpiecehasmoved"] = gSelectedPieceHasMoved;
    localStorage["halma.movecount"] = gMoveCount;
    return true;
}
```
 **Recuperar el estado del juego**:

```javascript
function resumeGame() {
    if (!supportsLocalStorage()) { return false; }
    gGameInProgress = (localStorage["halma.game.in.progress"] == "true");
    if (!gGameInProgress) { return false; }
    gPieces = new Array(kNumPieces);
    for (var i = 0; i < kNumPieces; i++) {
        var row = parseInt(localStorage["halma.piece." + i + ".row"]);
        var column = parseInt(localStorage["halma.piece." + i + ".column"]);
        gPieces[i] = new Cell(row, column);
    }
    gNumPieces = kNumPieces;
    gSelectedPieceIndex = parseInt(localStorage["halma.selectedpiece"]);
    gSelectedPieceHasMoved = localStorage["halma.selectedpiecehasmoved"] == "true";
    gMoveCount = parseInt(localStorage["halma.movecount"]);
    drawBoard();
    return true;
}
```

### **Eventos de almacenamiento**:

El evento `storage` se dispara cada vez que se realiza un cambio en el almacenamiento local, lo que permite mantener el seguimiento de los cambios en los datos.

Claro, aquí tienes la continuación y finalización del resumen que ya comenzaste:

---

### **Eventos de almacenamiento**

El evento `storage` se dispara cuando una pestaña o ventana modifica el `localStorage`, lo que permite a otras pestañas del mismo origen reaccionar a estos cambios. Es útil para mantener sincronizadas múltiples instancias de una aplicación.

Ejemplo de uso:

```javascript
window.addEventListener("storage", function(event) {
    console.log("La clave modificada fue: " + event.key);
    console.log("Valor anterior: " + event.oldValue);
    console.log("Nuevo valor: " + event.newValue);
});
```

---

### **Web SQL Database** (Obsoleto)

Web SQL Database fue una especificación que permitía a los desarrolladores ejecutar consultas SQL desde JavaScript en una base de datos SQLite incrustada en el navegador. Aunque fue adoptada inicialmente por algunos navegadores (como Chrome y Safari), **el W3C decidió descontinuarla** por depender exclusivamente de SQLite, lo que limitaba su interoperabilidad.

#### Características:

* Uso de SQL para manipular datos.
* Asincronía mediante callbacks.
* Poco soporte actual, especialmente en Firefox y Edge.

---

### **IndexedDB: El futuro del almacenamiento local**

**IndexedDB** es la alternativa moderna y recomendada para almacenamiento estructurado y de gran volumen en el navegador. A diferencia de `localStorage`, permite almacenar objetos complejos y manejar transacciones.

#### Características:

* **Soporta grandes cantidades de datos.**
* Permite **almacenar objetos completos**, no solo cadenas de texto.
* Usa **eventos y transacciones asincrónicas**.
* **API más compleja**, pero más poderosa y escalable.
* Soportada ampliamente por los navegadores modernos.

---

### 🔚 **Conclusión**

El almacenamiento local ha evolucionado desde soluciones específicas de navegador (como `userData` en IE) hasta llegar a estándares robustos como **HTML5 Storage**, **Web SQL Database** (ya en desuso) e **IndexedDB**.

* `localStorage` es ideal para necesidades simples, como guardar configuraciones de usuario o estados temporales.
* Para aplicaciones web avanzadas que requieren persistencia de datos complejos o grandes volúmenes, **IndexedDB** es la solución más sólida y moderna.
* Entender estas herramientas permite desarrollar aplicaciones web más ricas, eficientes y funcionales en el cliente.

---

¿Quieres que este resumen lo convierta en una presentación, infografía o en formato PDF para entregarlo o estudiarlo mejor?
 