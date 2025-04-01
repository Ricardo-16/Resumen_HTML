# Video en la web

# Soporte de etiquetas <video>

    Internet Explorer: 9.0+
    Firefox: 3.5+
    Safari: 3.0+
    Chrome: 3.0+
    Opera: 10.5+
    iPhone: 1.0+
    Android: 2.0+

# Soporte de contenedores de video

    Por lo regular vemos una extensión de un video es .avi nos estamos refiriendo al container AVI, o Audio Video Interleave. El container de video se refiere en el que se almacenarán los datos del vídeo en su archivo.

# Códecs de video

    Un códec de video hace referencia a un algoritmo en el que la transmisión de vídeo es codificada. El reproductor decodifica la transmisión del vídeo de acuerdo al códec de vídeo para mostrar un fotograma despues de otro.
    Hay códecs de vídeo con perdida y sin perdida (lossy, y lossless en inglés).Los códecs con pérdida eliminan parte de la información para reducir el tamaño del archivo, lo que puede afectar la calidad, pero permite una alta compresión. Esto los hace más ligeros y adecuados para su uso en la web, a diferencia de los códecs sin pérdida, que generan archivos más pesados.
    Los códecs más comunes son: H.264, H.265, VP9

# Códecs de audio

    Un códec de audio es un algoritmo que codifica y decodifica señales de audio para su almacenamiento o transmisión. Al igual que los códecs de video, los códecs de audio pueden ser con pérdida (lossy) o sin pérdida (lossless).

    Los códecs con pérdida eliminan información del audio para reducir el tamaño del archivo, lo que puede afectar la calidad del sonido, pero son ideales para la transmisión en línea debido a su alta compresión. Por otro lado, los códecs sin pérdida conservan toda la información del audio original, lo que resulta en una calidad superior pero archivos más grandes.

    Algunos de los códecs de audio más comunes son:

- MP3: Códec con pérdida ampliamente utilizado para música y audio en general.
- AAC: Códec con pérdida que ofrece mejor calidad que MP3 a tasas de bits similares.
- FLAC: Códec sin pérdida que conserva la calidad original del audio.
- Opus: Códec versátil con pérdida, diseñado para aplicaciones de transmisión en tiempo real.
- WAV: Formato sin pérdida que almacena audio sin compresión.

# Marcado

En HTML5 utilizamos el elemento <video> para agregar vídeo en una página web, seguido de esto podemos agregar la fuente del vídeo ya sea como atributo dentro de la misma etiqueta:
`````HTML
<video src="pr6.webm"></video>

# O agregando el elemento source:

     `````HTML
     <video>
     	<source src="pr6.webm">
     </video>

# Posteriormente, podemos definir las dimensiones del marco del vídeo.

    <video
     width="320"
     height="240"
    >
    	<source src="pr6.webm">
    </video>

# Para añadir una interfaz de controles del vídeo (como ajustar el volumen, reproducir y pausar), incluimos el atributo controls

    <video
    width="320"
    height="240"
    controls
    >
    	<source src="pr6.webm">
    </video>

# Si deseamos que el vídeo empiece a descargarse tan pronto como la página cargue, debemos agregar el atributo preload, esto nos puede ser útil si el propósito principal de la página es reproducir el vídeo.

    <video
    width="320"
    height="240"
    controls
    preload
    >
    	<source src="pr6.webm">
    </video>

# Si no queremos esto, podemos ajustar este atributo.

    <video
    width="320"
    height="240"
    controls
    preload="none"
    >
    	<source src="pr6.webm">
    </video>

# También podemos agregar el autoplay, por si queremos que el vídeo además de cargarse junto con la página, se reproducirá al instante.

    <video
    width="320"
    height="240"
    controls
    autoplay
    >
    	<source src="pr6.webm">
    </video>

# A continuación agregaremos más fuentes de vídeo al elemento:

    <video
    width="320"
    height="240"
    controls
    >
    		<source
      			src="pr6.ogv"
      			type='video/ogg;
     		codecs= "theora, vorbis"'
    		>
    	<source

src="pr6.webm"
type='video/webm;
codecs="vp8, vorbis"' >
<source 
  			src="pr6.mp4"
     			type='video/mp4;
			codecs="avc1.42E01E, mp4a.40.2"'
   		>
</video>
