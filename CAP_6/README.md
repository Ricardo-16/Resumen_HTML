# Estas aquí (Y asi esta todo el mundo)

# La api de Geolocalización

    La API de Geolocalización permite a las aplicaciones obtener la ubicación geográfica del dispositivo del usuario. Esto se logra a través de métodos como `getCurrentPosition` y `watchPosition`, que proporcionan coordenadas como latitud y longitud. Es útil para aplicaciones de mapas, seguimiento en tiempo real y servicios basados en ubicación. Es importante manejar los permisos de usuario y considerar la privacidad al implementar esta funcionalidad.

# Soporte de Geolocalización

    firefox, Safari, Chorme, Opera, Iphone, Android.
     3.5+     5.0+    5.0+   10.6+   3.0+    2.0+

# Muestrame el Código

El uso mas simple de la gelocalizacion es el siguiente.

```
    function get_location(){
    navigator.geolocation.getCurrentPosition(show_map);
}
```

Esta función solicita la ubicación actual del dispositivo y muestra un mapa con la ubicación marc.

Es probable que la aplicación web incluya al menos los dos primeros. Para detectar la compatibilidad con la API de geolocalización, puede usar Modernizr:

```
    function get_location() {

    if (
    Modernizr.geolocation) {
    navigator.geolocation.getCurrentPosition(show_map);
    } else {
    // no native support; maybe try Gears?
    }
}
```

Al hacer el llamado de la funcion getCurrentPosition() de la API de geolocalización hará que el navegador muestre una "barra de información" en la parte superior de la ventana del navegador.

El siguiente codigo muestra como se obtiene la ubicacion mediante la AAPI de Geolocalizacion.
```
    function get_location() {
        navigator.geolocation.getCurrentPosition(show_map);
    }
```

Este método devuelve inmediatamente, pero los datos de ubicación solo estarán disponibles dentro de la función de callback , como 'show_map en el ejemplo. Aquí puedes acceder a las coordenadas.
```
    function show_map(position) {
    var latitude = position.coords.latitude;
    var longitude = position.coords.longitude;
    // Mostrar mapa o realizar una acción interesante con los datos
   }
```

# Manejo de errores 
La geolocalización no siempre funciona correctamente. Pueden surgir errores. Ya mencioné el tema del consentimiento del usuario : si tu aplicación web necesita

Pero, ¿cómo se maneja eso en el código? A través del segundo argumento de la función :getCurrentPosition()
```
    navigator.geolocation.getCurrentPosition(
        show_map,     
        handle_error  
    );
 ```   
Si algo falla, se llamará a tu función de error con un objeto 'PositionErrorPositionError, que contiene información sobre lo que salió mal.

El objeto 'PositionErrorPositionError tiene una propiedad 'codecode que puede tener uno de los siguientes valores:
    PERMISSION_DENIED (1)
        Si el usuario hace clic en el botón "No compartir" o niega explícitamente el acceso a su ubicación.
    POSITION_UNAVAILABLE (2)
        Si la red está caída o no se puede contactar con los satélites de posicionamiento.
    TIMEOUT (3)
        Si la red funciona, pero tarda demasiado en calcular la posición del usuario.
        ¿Cuánto es "demasiado"? En la siguiente sección te mostraré cómo definir este tiempo límite.
    UNKNOWN_ERROR (0)
        Si ocurre cualquier otro error desconocido. 

# ¡OPCIONES! ¡EXIJO OPCIONES!
    La API de Geolocalización ofrece opciones adicionales que puedes usar al llamar a métodos como getCurrentPosition() o . Estas opciones te permiten controlar cómo se obtiene la ubicación del usuario.watchPosition()

1. enableHighAccuracy
Esta propiedad hace exactamente lo que su nombre indica: habilita una ubicación de alta precisión si:

El dispositivo lo soporta,
Y el usuario da su consentimiento.
En dispositivos como iPhones y Android, los permisos de baja y alta precisión están separados. Esto significa que llamar a con podría fallar, mientras que hacerlo con sí podría funcionargetCurrentPosition(){ enableHighAccuracy: true }{ enableHighAccuracy: false }

2. timeout
Es el tiempo máximo (en milisegundos ) que tu aplicación está dispuesta a esperar para obtener una posición.
Este temporizador no empieza hasta que el usuario haya dado su permiso , así que no estás midiendo cuánto tarda el usuario en

3. maximumAge
Permite al dispositivo devolver una ubicación almacenada en caché , si aún es válida según el tiempo especificado (en miliseg)

Por ejemplo:

Imagina que llamas a por primera vez, el usuario acepta, y obtienes una posición calculada exactamente a las 10:00 AM .
Un minuto después, a las 10:01 AM , vuelves a llamar a con estagetCurrentPosition()getCurrentPosition()
```
navigator.geolocation.getCurrentPosition(
    show_map,
    handle_error,
    { maximumAge: 75000 }
);
```
Esto le dice al dispositivo que aceptas una ubicación con hasta 75 segundos de antigüedad . Como solo han pasado 60 segundos desde la última vez, el dispositivo simplemente devuelve la misma información que ya tenía:

Misma latitud y longitud,
Misma precisión,
Y la misma marca de tiempo (10:00 AM).
¿Qué pasa si necesito la ubicación varias veces?
Antes de pedir siempre una nueva ubicación, piensa qué tan precisa la necesitas y establece enableHighAccuracy correctamente. Si vas a pedirla más de una vez, piensa también cuánto tiempo puede tener la información y seguir siendo útil. Eso te ayudará a decidir el valor de .maximumAge

Pero si necesitas seguir la ubicación del usuario continuamente, entonces no es lo que necesitas.getCurrentPosition()

– Seguimiento continuowatchPosition()
El método tiene la misma estructura que 'getCurrentwatchPosition()getCurrentPosition():

Toma dos funciones de callback : una para éxito y otra opcional para errores.
Puede tomar un objeto con las mismas propiedades (, , ).PositionOptionsenableHighAccuracytimeoutmaximumAge
La diferencia es que tu función de éxito se llamará cada vez que cambie la ubicación del usuario . No necesitas preguntar manualmente; el dispositivo decide cuál es el intervalo óptimo de actualización, y te notifica cuando hay cambios.

Puedes usar esto para:

Actualizar un marcador en un mapa,
Dar instrucciones paso a paso,
O cualquier acción basada en movimiento.
Ejemplo básico:
```
const watchId = navigator.geolocation.watchPosition(
    show_map,
    handle_error,
    {
        enableHighAccuracy: true,
        timeout: 10000,
        maximumAge: 0
    }
);
```
Detener el seguimiento: clearWatch()
El método devuelve un número identificador (). GuárdalowatchPosition()watchId
Si en algún momento quieres dejar de recibir actualizaciones de ubicación, llama a:
```
vigator.geolocation.clearWatch(watchId);
```
Este sistema funciona de forma muy parecida a las funciones y de JavaScript.setInterval()clearInterval()

# ¿QUÉ PASA CON IE?

###  Compatibilidad con navegadores antiguos

Internet Explorer **no soporta** la API de geolocalización estándar del W3C que acabo de describir. ¡Pero no te desesperes!

####  Gears: una alternativa de Google
[Gears](https://developers.google.com/gears/) es un **complemento de navegador de código abierto desarrollado por Google**, compatible con:
- Windows  
- Mac  
- Linux  
- Windows Mobile  
- Android  

Este plugin ofrece características avanzadas para navegadores más antiguos, entre ellas una **API de geolocalización**. Aunque no es exactamente igual a la API estándar del W3C, cumple el mismo propósito.



###  Plataformas móviles antiguas también tenían sus propias APIs

Mientras estamos en el tema de plataformas heredadas, vale la pena mencionar que muchas de las plataformas móviles antiguas ofrecían su propia API de geolocalización específica del dispositivo.

Algunas de estas plataformas incluyen:
- BlackBerry  
- Nokia  
- Palm  
- OMTP BONDI  

Por supuesto, **todas funcionan de forma diferente entre sí**. La API de Gears funciona distinto a la del W3C, y a su vez distinto a las APIs nativas de cada fabricante.  
# GEO.JS Al rescate
geo.js es una biblioteca JavaScript de código abierto con licencia MIT que simplifica las diferencias entre:
La API de geolocalización estándar del W3C,
La API de geolocalización de Gears,
Y las APIs específicas de varias plataformas móviles.
Gracias a 'geo.js, puedes escribir código compatible con múltiples navegadores y dispositivos sin preocuparte por las diferencias técnicas subyacentes.
```
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="utf-8">
    <title>Dive Into HTML5</title>
    </head>
    <body>
    ...
    <script src="gears_init.js"></script>
    <script src="geo.js"></script>
    diveintohtml5.org 
    YOU ARE HERE (AND SO IS EVERYBODY ELSE)
    to your <head>
    <script src="geo.js"></script>
    </body>
    </html>

```
¡Claro! Aquí tienes la **traducción al español** del texto que proporcionaste, ideal para incluir en un `README.md` o documentación técnica sobre el uso de `geo.js`.

---

##  Cómo usar `geo.js`: Paso a paso

### 1. **Inicializar la biblioteca**
Primero, debes llamar explícitamente a la función `init()`. Esta función verifica si hay disponible alguna API de geolocalización compatible.

```javascript
if (geo_position_js.init()) {
    // La geolocalización está disponible
}
```

 **Nota:** Llamar a `init()` **no obtiene tu ubicación**, solo comprueba si es posible obtenerla.

---

### 2. **Obtener la ubicación actual**
Para obtener realmente la ubicación del usuario, llama a la función `getCurrentPosition()`:

```javascript
geo_position_js.getCurrentPosition(geo_success, geo_error);
```

Esta función:
- Pide permiso al usuario para acceder a su ubicación.
- Si se usa Gears, mostrará un diálogo pidiendo confianza para usarlo.
- En navegadores modernos (como Firefox 3.5), se mostrará una barra de información solicitando permiso para compartir la ubicación.

---

### 3. **Manejar los resultados**

####  Función de éxito (`geo_success`)
Se ejecuta si el usuario acepta y el sistema logra encontrar la ubicación.

```javascript
function geo_success(p) {
    alert("Te encontré en latitud " + p.coords.latitude +
          ", longitud " + p.coords.longitude);
}
```

La variable `p` contiene toda la información de la posición, incluyendo:
- `latitude`
- `longitude`
- `accuracy`
- Y otros campos opcionales según el dispositivo.

####  Función de error (`geo_error`)
Se ejecuta si:
- El usuario no da permiso,
- O si por algún motivo falla la API de geolocalización.

```javascript
function geo_error() {
    alert("¡No pude encontrarte!");
}
```

 Esta función **no recibe argumentos**, solo indica que algo salió mal.

---

### Limitaciones actuales de `geo.js`

> **Importante:** `geo.js` **no soporta actualmente** la función `watchPosition()`.  
Si necesitas obtener la ubicación del usuario continuamente, tendrás que llamar manualmente a `getCurrentPosition()` en intervalos regulares con `setInterval()`.

**Ejemplo:**

```javascript
setInterval(function() {
    geo_position_js.getCurrentPosition(geo_success, geo_error);
}, 10000);
```

---

###  Resumen final

Con `geo.js`, puedes usar una única interfaz para detectar la ubicación del usuario, sin importar qué tecnología esté usando el navegador o dispositivo. Es ideal para aplicaciones compatibles con navegadores antiguos o plataformas móviles heterogéneas.
