# HTML5: Fechas, Tiempos, Navegación y Footers

# Fechas y Tiempos en HTML5

Anteriormente, las fechas se incluían en etiquetas genéricas con clases personalizadas, lo cual carecía de significado semántico. Con HTML5, podemos utilizar la etiqueta `<time>`.

Ejemplo anterior:

```html
<div class="entry">
  <p class="post-date">October 22, 2009</p>
  <h2>Travel day</h2>
</div>
```

    HTML5 introduce `<time>` para representar fechas y horas de manera semántica.

```html
<time datetime="2009-10-22" pubdate>October 22, 2009</time>
```

# Partes del elemento `<time>`:

    Timestamp legible por máquina (atributo `datetime`)
    Texto legible por humanos (contenido de la etiqueta)
    Atributo `pubdate` opcional para marcar la fecha de publicación

Ejemplo con hora y zona horaria:

```html
<time datetime="2009-10-22T13:59:47-04:00" pubdate>
  October 22, 2009 1:59pm EDT
</time>
```

El texto dentro de `<time>` no necesita coincidir con el timestamp, por ejemplo:

```html
<time datetime="2009-10-22">last Thursday</time>
```

# Navegación en HTML5

Los sitios web dependen en gran medida de la navegación. Antes de HTML5, la navegación se implementaba con `<div>` sin un significado semántico.

Ejemplo clásico:

```html
<div id="nav">
  <ul>
    <li><a href="#">home</a></li>
    <li><a href="#">blog</a></li>
    <li><a href="#">gallery</a></li>
    <li><a href="#">about</a></li>
  </ul>
</div>
```

Con HTML5, podemos usar `<nav>`, lo que mejora la accesibilidad:

```html
<nav>
  <ul>
    <li><a href="#">home</a></li>
    <li><a href="#">blog</a></li>
    <li><a href="#">gallery</a></li>
    <li><a href="#">about</a></li>
  </ul>
</nav>
```

# Accesibilidad

Los usuarios con discapacidades pueden beneficiarse de `<nav>`, ya que permite a los lectores de pantalla identificar rápidamente la sección de navegación.

Aunque `<nav>` mejora la semántica, se recomienda seguir proporcionando "skip links" hasta que todos los lectores de pantalla soporten completamente HTML5.

# Footer en HTML5

Al final de una página web, es común encontrar información como derechos de autor, enlaces de contacto y otras referencias.

Ejemplo tradicional con `<div>`:

```html
<div id="footer">
  <p>HELLO WORLD;</p>
  <p>&#169; 2001&#8211;9 <a href="#">Mark Pilgrim</a></p>
</div>
```

Con HTML5, podemos usar `<footer>`:

```html
<footer>
  <p>&#167;</p>
  <p>&#169; 2001&#8211;9 <a href="#">Mark Pilgrim</a></p>
</footer>
```

El contenido común en un `<footer>` incluye:

- Autor del contenido
- Enlaces a documentos relacionados
- Derechos de autor
- Contacto y términos de uso

# "Fat Footers"

Algunos sitios incluyen "fat footers" con muchas secciones.

Ejemplo mejorado de un footer en HTML5:

```html
<footer>
  <nav>
    <h1>Navigation</h1>
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/standards/">Standards</a></li>
      <li><a href="/participate/">Participate</a></li>
      <li><a href="/Consortium/membership">Membership</a></li>
      <li><a href="/Consortium/">About W3C</a></li>
    </ul>
  </nav>

  <nav>
    <h1>Contact W3C</h1>
    <ul>
      <li><a href="/Consortium/contact">Contact</a></li>
      <li><a href="/Help/">Help and FAQ</a></li>
      <li><a href="/Consortium/sup">Donate</a></li>
      <li><a href="/Consortium/siteindex">Site Map</a></li>
    </ul>
  </nav>

  <section>
    <h1>W3C Updates</h1>
    <ul>
      <li><a href="http://twitter.com/W3C">Twitter</a></li>
      <li><a href="http://identi.ca/w3c">Identi.ca</a></li>
    </ul>
  </section>

  <p class="copyright">Copyright © 2009 W3C</p>
</footer>
```
