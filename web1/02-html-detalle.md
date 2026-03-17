# HTML en detalle

El capítulo anterior presentó la base del lenguaje. A partir de aquí el objetivo es profundizar en decisiones más concretas: cómo usar mejor el `head`, cómo estructurar el `body`, qué lugar ocupan las etiquetas semánticas y cómo construir ejemplos más próximos a situaciones reales de trabajo.

## Objetivos del capítulo

- profundizar en el uso de etiquetas semánticas y en la organización del `head` y del `body`;
- reconocer etiquetas frecuentes para contenido textual, multimedia, estructura y formularios;
- aplicar criterios de validación y recursos de consulta para trabajar con HTML más completo;
- trasladar esas decisiones a un primer proyecto guiado con páginas vinculadas entre sí.

Como se mencionó en el capítulo anterior, HTML es un lenguaje sencillo de entender y aprender, aunque al principio la cantidad de etiquetas disponibles puede sonar abrumadora.

Este libro se enfoca en las principales etiquetas y de uso cotidiano, mientras que el resto se irán aprendiendo con la práctica a medida que se necesiten.

**¿Dónde encontrar información detallada y una lista completa de todas las marcas de HTML?**

La W3C es el organismo que establece los estándares web, y por lo tanto la referencia oficial mundial del lenguaje. Su sitio web [https://www.w3.org/](https://www.w3.org/) es la principal fuente de información formal y la información oficial sobre HTML está publicada aquí [https://html.spec.whatwg.org/multipage/](https://html.spec.whatwg.org/multipage/) 

Esa misma información puede descargarse en PDF aquí [https://html.spec.whatwg.org/print.pdf](https://html.spec.whatwg.org/print.pdf) se trata de una publicación de 1500 páginas con detalle técnico de cada elemento disponible en HTML.

Otra **fuente de información muy útil** es la referencia publicada por Mozilla Developer Network (MDN). Además de desarrollar Firefox, este proyecto publica documentación clara y muy utilizada sobre HTML, CSS y JavaScript en todo el mundo [https://developer.mozilla.org/es/docs/Web/HTML](https://developer.mozilla.org/es/docs/Web/HTML) 

En el capítulo anterior se presentó la estructura general de un documento HTML, que básicamente se compone de una etiqueta `<head>` y otra `<body>`, cada una con sus marcas específicas y distintos propósitos. 

Este capítulo ahonda sobre cada una de las principales marcas, pero antes de avanzar, se presentará un concepto fundamental para el desarrollo web moderno: la semántica.

## HTML5 semántico

Desde sus inicios hasta la actualidad, la web ha cambiado muchísimo, y como es de esperar, los lenguajes de la web también. HTML5 semántico es una evolución del lenguaje HTML que incorpora etiquetas con significado específico sobre el contenido que encierran. A diferencia de versiones anteriores, donde se usaban etiquetas genéricas como `<div>` o `<span>` para todo tipo de estructuras, HTML5 introduce nuevas etiquetas como `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>` y `<footer>`, entre otras.

Estas etiquetas permiten describir la estructura de una página web de forma más clara y comprensible, tanto para personas como para máquinas. Por ejemplo, un lector de pantalla puede identificar que una sección es una navegación (`<nav>`) o que cierto contenido es un artículo independiente (`<article>`), lo cual mejora considerablemente la accesibilidad.

El uso de HTML semántico también favorece el posicionamiento en buscadores (SEO), ya que los motores de búsqueda comprenden mejor el contenido y la jerarquía de la información. Además, facilita el mantenimiento del código y el trabajo en equipo, ya que al leer el HTML es más fácil entender qué función cumple cada parte.

Escribir HTML semántico es una buena práctica que mejora la accesibilidad, el rendimiento y la organización del sitio, y es un estándar recomendado en el desarrollo web moderno.

## Etiqueta `<head>`

Antes de abordar los detalles de la etiqueta `<head>` se recordará brevemente la estructura general de un documento HTML y se explicarán algunos conceptos clave al iniciar un archivo HTML.

```html
<!DOCTYPE html>
<html lang="es">
<head>
<!-- metadatos, hojas de estilo, scripts, etc. -->
</head>
<body>
<!-- contenido visible de la página -->
</body>
</html>
```

Conviene leer ese ejemplo separando qué función cumple cada parte:

- `<!DOCTYPE html>` declara que el documento está escrito en HTML5.
- `<html lang="es">` identifica la raíz del documento y declara el idioma principal del contenido.
- `<head>` reúne metadatos y configuraciones que no aparecen como contenido visible en la página.
- `<meta>` define información como codificación, descripción o viewport.
- `<title>` define el texto que aparece en la pestaña del navegador.
- `<link>` permite enlazar recursos externos, como hojas de estilo.
- `<script>` vincula o contiene código JavaScript.
- `<style>` permite incluir CSS dentro del propio documento.

La etiqueta `<meta charset="UTF-8">` se recomienda como configuración general porque evita problemas con tildes, eñes y otros caracteres frecuentes en español, salvo que exista una razón técnica específica para usar otra codificación. También conviene incluir la configuración de `viewport` para que el documento responda correctamente en dispositivos móviles.

Un ejemplo más completo de `head` podría verse así:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <title>Mi Página Web</title>
  <meta name="description" content="Breve descripción">
  <meta name="keywords" content="palabras, clave">
  <meta name="author" content="Nombre del autor">
  <meta name="robots" content="index, follow">
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,
  initial-scale=1.0">
  <link rel="stylesheet" href="styles.css">
  <script src="script.js" defer></script>
  <style>
    /* Estilos CSS aquí */
  </style>
</head>
<body>
  <!-- contenido visible de la página -->
</body>
</html>
```

En ese ejemplo aparece `defer` en la etiqueta `<script>`. Ese atributo indica que el archivo JavaScript puede descargarse mientras el navegador procesa el HTML, pero que su ejecución debe esperar hasta que el documento esté interpretado. En una etapa inicial, esto ayuda a evitar errores causados por intentar usar elementos que todavía no existen en la página.

## Etiqueta `<body>`

La etiqueta `<body>` en HTML define el cuerpo principal de un documento web. Es donde se coloca el contenido visible de la página, como texto, imágenes, enlaces y otros elementos interactivos.

## Etiquetas de contenido textual

### Encabezados

Las etiquetas `<h1>` a `<h6>` se utilizan para definir títulos y subtítulos. `h1` representa el nivel más alto de jerarquía, mientras que `h6` representa el nivel más bajo. Estas etiquetas ayudan a ordenar el contenido, mejoran la lectura y también aportan información útil a buscadores y tecnologías de asistencia.

```html
<h1>Bienvenidos a mi sitio web</h1>
<h2>Sección de noticias</h2>
```

### Párrafos

La etiqueta `<p>` define un párrafo de texto. Es una de las etiquetas más comunes de HTML y permite organizar la información en bloques legibles. Los navegadores suelen dejar un espacio antes y después de cada párrafo, lo que mejora naturalmente la separación del contenido.

```html
<p>Este es un párrafo de ejemplo. Los párrafos son importantes para 
separar el texto y hacerlo más legible.</p>
```

### Enlaces

La etiqueta `<a>` se utiliza para crear enlaces. El atributo más importante es `href`, que especifica la URL o el recurso de destino. También puede incluir atributos como `target`, que define si el enlace se abre en la misma ventana o en una nueva. Es fundamental para la navegación en la web, ya que permite pasar de una página a otra.

```html
<a href="https://www.example.com" target="_blank">Visita nuestro
sitio</a>
```

### Listas

La etiqueta `<ul>` define una lista de elementos no ordenados, que se muestran como ítems con puntos o viñetas. Cada ítem se define usando la etiqueta `<li>`. Los atributos más comunes son `class` e `id`.

```html
<ul>
  <li>Manzanas</li>
  <li>Plátanos</li>
  <li>Peras</li>
</ul>
```

La etiqueta `<ol>` se utiliza para crear una lista ordenada, donde los ítems se representan numérica o alfabéticamente. Al igual que con las listas no ordenadas, los elementos se definen con la etiqueta `<li>`. Un atributo particular de `<ol>` es `start`, que permite especificar el número con el que comienza la lista, aunque generalmente no se lo usa porque la mayoría comienzan desde el inicio.

```html
<ol start="1">
  <li>Primero</li>
  <li>Segundo</li>
  <li>Tercero</li>
</ol>
```

### Tablas

Cuando se necesita mostrar datos comparables en filas y columnas, conviene usar una tabla HTML y no una grilla hecha con `div`. Las tablas son apropiadas para listados con estructura estable, por ejemplo una lista de productos, precios y categorías.

Las etiquetas más frecuentes son estas:

- `<table>`: contenedor general de la tabla.
- `<thead>`: encabezado de columnas.
- `<tbody>`: cuerpo principal con los datos.
- `<tr>`: fila.
- `<th>`: celda de encabezado.
- `<td>`: celda de datos.

Ejemplo:

```html
<table>
  <thead>
    <tr>
      <th>Producto</th>
      <th>Categoria</th>
      <th>Precio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Yerba</td>
      <td>Almacen</td>
      <td>$ 4200</td>
    </tr>
    <tr>
      <td>Leche</td>
      <td>Lacteos</td>
      <td>$ 1500</td>
    </tr>
  </tbody>
</table>
```

En el proyecto del supermercado, `lista.html` es un buen lugar para practicar este tipo de estructura.

### Énfasis y separaciones

La etiqueta `<strong>` se usa para marcar un texto como especialmente importante. En la mayoría de los navegadores se muestra en negrita, pero su valor principal es semántico: indica énfasis fuerte.

```html
<p><strong>Este es un mensaje importante</strong></p>
```

La etiqueta `<em>` también se utiliza para enfatizar texto, normalmente con cursiva. Igual que `<strong>`, aporta significado además del efecto visual.

```html
<p>Este es un <em>mensaje enfatizado</em> para dar énfasis en su
importancia.</p>
```

La etiqueta `<br>` se utiliza para insertar un salto de línea dentro de un texto o párrafo sin crear un nuevo bloque de contenido. La etiqueta `<hr>` se usa para insertar una separación temática entre secciones de contenido.

```html
<p>Esta es una dirección:<br> Calle Ficticia 123<br> Ciudad
Imaginaria</p>

<p>Sección 1</p>
<hr>
<p>Sección 2</p>
```

## Etiquetas de contenido multimedia

La etiqueta `<img>` se usa para insertar imágenes en una página web. Es una etiqueta autocontenida, lo que significa que no requiere una etiqueta de cierre. El atributo `src` especifica la URL de la imagen, mientras que `alt` proporciona una descripción alternativa, importante para accesibilidad y SEO.

```html
<img src="logo.png" alt="Logo del sitio web">
```

Cuando una imagen necesita acompañarse con un epígrafe o una breve explicación, conviene usar `figure` y `figcaption`.

```html
<figure>
  <img src="producto.jpg" alt="Paquete de yerba mate">
  <figcaption>Envase principal de la línea clásica.</figcaption>
</figure>
```

Esta estructura resulta útil cuando la imagen forma parte del contenido y no es solo un adorno. También vuelve más claro qué texto describe a qué recurso.

La etiqueta `<video>` se utiliza para incrustar un archivo de video. Es recomendable especificar varios formatos mediante etiquetas `<source>` para mejorar la compatibilidad. Algunos atributos importantes son `controls`, `autoplay` y `loop`.

```html
<video width="640" height="360" autoplay loop>
  <source src="video.mp4" type="video/mp4">
  <source src="video.ogg" type="video/ogg">
</video>
```

La etiqueta `<audio>` permite incrustar archivos de audio. Al igual que con `<video>`, se puede usar `<source>` para definir distintos formatos.

```html
<audio controls loop>
  <source src="audio.mp3" type="audio/mp3">
  <source src="audio.ogg" type="audio/ogg">
</audio>
```

La etiqueta `<iframe>` se utiliza para incrustar un documento HTML dentro de otro, por ejemplo un video de YouTube o un mapa. La etiqueta `<picture>` sirve para mostrar distintas imágenes según el contexto del dispositivo.

```html
<iframe src="https://www.youtube.com/embed/jMitTWFZHsc" width="560"
height="315" frameborder="0" allowfullscreen></iframe>

<picture>
  <source srcset="big.jpg" media="(min-width: 800px)">
  <source srcset="small.jpg" media="(max-width: 799px)">
  <img src="default.jpg" alt="Imagen predeterminada">
</picture>
```

Una ventaja importante de `picture` es que permite cargar versiones distintas de una misma imagen según el tamaño o la resolución de pantalla. Eso mejora dos cosas al mismo tiempo:

- la calidad visual, porque no hace falta mostrar una imagen demasiado pequeña en una pantalla grande;
- el rendimiento, porque un dispositivo pequeño no necesita descargar siempre la versión más pesada.

En proyectos reales, esto ayuda a equilibrar nitidez, velocidad de carga y consumo de datos. En otras palabras, no se trata solo de “hacer que la imagen se vea”, sino de elegir mejor qué recurso conviene cargar en cada contexto.

La etiqueta `<canvas>` se usa para dibujar gráficos, animaciones o contenido dinámico mediante JavaScript.

```html
<canvas id="miCanvas" width="200" height="100"></canvas>
<script>
  const canvas = document.getElementById("miCanvas");
  const ctx = canvas.getContext("2d");
  ctx.fillStyle = "red";
  ctx.fillRect(10, 10, 150, 75);
</script>
```

## Etiquetas de estructura

La etiqueta `<div>` es un contenedor genérico que se utiliza para agrupar otros elementos HTML. Aunque no tiene significado semántico propio, se usa mucho para estructurar secciones o aplicar estilos a un conjunto de elementos.

```html
<div>
  <p>Texto dentro del contenedor</p>
</div>
```

La etiqueta `<span>` es similar a `<div>`, pero se utiliza para agrupar contenido en línea sin romper el flujo del texto.

```html
<p>Este es un <span class="resaltado">texto destacado</span> en una
oración.</p>
```

## Etiquetas de estructura con semántica

La etiqueta `<header>` representa la cabecera de una página o sección. Suele contener título, logotipo, menú de navegación o información introductoria.

```html
<header>
  <h1>Mi Sitio Web</h1>
  <nav>
    <ul>
      <li><a href="#inicio">Inicio</a></li>
      <li><a href="#servicios">Servicios</a></li>
      <li><a href="#nosotros">Nosotros</a></li>
      <li><a href="#contacto">Contacto</a></li>
    </ul>
  </nav>
</header>
```

La etiqueta `<nav>` representa una sección del documento que contiene enlaces de navegación. La etiqueta `<main>` contiene el contenido principal del documento y debería aparecer una sola vez por página.

```html
<main>
  <h1>Bienvenido a nuestra página</h1>
  <p>Este es el contenido principal.</p>
</main>
```

La etiqueta `<section>` se usa para agrupar contenido relacionado dentro de una misma temática. La etiqueta `<article>` representa una unidad de contenido relativamente autónoma, como una noticia, una ficha, una publicación o un producto. La etiqueta `<aside>` sirve para contenido complementario: información relacionada, paneles laterales, enlaces secundarios o bloques de apoyo. La etiqueta `<footer>` representa el pie de página de un documento o sección.

```html
<section>
  <h2>Noticias recientes</h2>
  <h3>...</h3>
</section>

<article>
  <h2>Producto destacado</h2>
  <p>Descripción del producto.</p>
</article>

<aside>
  <h2>Productos relacionados</h2>
  <p>Otros recursos o enlaces complementarios.</p>
</aside>

<footer>
  <p>Todos los derechos reservados.</p>
  <a href="mailto:info@misitio.com">Contáctanos</a>
</footer>
```

Una forma simple de diferenciarlas es esta:

- `section` agrupa contenido por tema;
- `article` encapsula una pieza que podría tener sentido por sí sola;
- `aside` agrega contexto o contenido secundario alrededor de lo principal.

Esa distinción no siempre es perfecta, pero ayuda mucho a escribir HTML más claro y más semántico.

## Ejemplo de HTML para un sitio de videos

A continuación se muestra un ejemplo de un código sencillo, utilizando etiquetas semánticas sobre cómo podría ser el documento HTML de un sitio web de videos, similar a Youtube. El código a continuación mostraría una lista de títulos e imágenes con un link a la página para ver el video.

### **Resultados de búsqueda**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,
  initial-scale=1.0">
  <title>Mi Sitio de Videos</title>
</head>
<body>
  <header>
    <h1>Mi Sitio de Videos</h1>
  </header>

  <main>
    <section aria-label="Lista de videos">
      <article>
        <img src="imagen-video.jpg" alt="Mini video 1">
        <h2>Título del Video 1</h2>
        <p>Descripción breve del video 1.</p>
      </article>

      <article>
        ...
      </article>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 Mi Sitio de Videos</p>
  </footer>
</body>
</html>
```

En este ejemplo aparece `aria-label` para describir mejor la sección. Los atributos ARIA se retomarán con más detalle en el capítulo de accesibilidad. Por ahora alcanza con entender que sirven para agregar información útil a tecnologías de asistencia cuando la semántica HTML sola no alcanza.

### **Página de un video**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,
  initial-scale=1.0">
  <title>Ver Video - Mi Sitio de Videos</title>
</head>
<body>
  <header>
    <h1>Mi Sitio de Videos</h1>
  </header>

  <main>
    <article>
      <h1>Título del Video</h1>
      <video controls>
        <source src="video.mp4" type="video/mp4">
      </video>
      <p>Publicado el 14/04/2025 | 400 veces visto</p>
    </article>

    <aside>
      <h2>Videos relacionados</h2>
      <div class="related-video">
        <img src="imagen-video.jpg" alt="Mini video 1">
        <h3>Video Relacionado 1</h3>
      </div>
      ...
    </aside>
  </main>

  <footer>
    <p>&copy; 2025 Mi Sitio de Videos</p>
  </footer>
</body>
</html>
```

## Etiquetas de formularios y entrada de datos

En este punto conviene ser precisos con el vocabulario. Aunque estos elementos suelen ser el punto de partida de muchas interfaces interactivas, en HTML por sí solos funcionan principalmente como controles para ingresar y enviar datos. La interacción en sentido más amplio, como responder a eventos, validar con mensajes dinámicos o modificar la interfaz en tiempo real, se trabajará después con JavaScript.

La etiqueta `<form>` se utiliza para crear formularios en HTML. Dentro de un formulario se colocan los distintos campos que permiten al usuario ingresar y enviar datos a un servidor.

La etiqueta `<form>` tiene tres atributos muy importantes: `action`, `method` y `enctype`.

- `action` indica la URL o ruta a la que se enviarán los datos;
- `method` define si la solicitud usará `get` o `post`;
- `enctype` define cómo se codifican los datos antes de ser enviados.

En formularios que incluyen archivos, como imágenes o videos, es obligatorio usar `enctype="multipart/form-data"`.

```html
<form action="..." method="..." enctype="multipart/form-data">
  <!-- aquí irán todos los elementos del formulario -->
</form>
```

La etiqueta `<button>` permite crear botones, generalmente usados para enviar formularios con `type="submit"`. Más adelante también podrá usarse para disparar comportamientos desde JavaScript, pero aquí interesa sobre todo su papel dentro de formularios.

```html
<button type="submit">Enviar</button>
```

Conviene conocer al menos tres variantes comunes:

- `type="submit"`, para enviar el formulario;
- `type="button"`, para un botón que no envía automáticamente;
- `type="reset"`, para restablecer los valores iniciales del formulario.

Por ejemplo:

```html
<button type="submit">Guardar</button>
<button type="button">Vista previa</button>
<button type="reset">Limpiar</button>
```

En formularios reales, `submit` suele ser el caso principal. Los otros tipos conviene conocerlos para evitar comportamientos inesperados, especialmente cuando más adelante se combine HTML con JavaScript.

La etiqueta `<textarea>` se utiliza para campos de texto de varias líneas, como un comentario o la descripción de un contenido. El atributo `name` es muy importante porque es el nombre con el que el servidor recibirá esa información.

```html
<textarea name="mensaje" rows="4" cols="50" placeholder="Escribí tu
mensaje"></textarea>
```

La etiqueta `<select>` crea un menú desplegable y cada `<option>` representa una opción posible.

```html
<select name="pais">
  <option value="ar">Argentina</option>
  <option value="uy">Uruguay</option>
  <option value="cl">Chile</option>
</select>
```

La etiqueta `<input>` es una de las más versátiles de HTML. Se utiliza para crear distintos tipos de campos de entrada.

```html
<input type="text" name="nombre" placeholder="Tu nombre">
<input type="email" name="email" placeholder="Tu email">
<input type="password" name="clave" placeholder="Tu contraseña">
<input type="number" name="edad" min="0" max="120">
<input type="file" name="archivo">
<input type="checkbox" name="acepta"> Acepto los términos
<input type="radio" name="de_acuerdo" value="si"> Sí
<input type="radio" name="de_acuerdo" value="no"> No
```

Puede notarse en este caso, que `input type="radio"` **requiere repetir el atributo name con el mismo valor**, esto no es un problema porque sólo viajará al servidor la opción elegida.

Es común acompañar los campos de un formulario con un pequeño texto de ayuda. Para eso se usa la etiqueta `<label>`, que mejora la accesibilidad y la usabilidad al asociar una descripción con un campo concreto.

```html
<label for="email">Correo electrónico:</label>
<input type="email" id="email" name="email">
```

Cuando varios controles forman parte de una misma decisión, conviene agruparlos con `fieldset` y darles un título con `legend`.

```html
<fieldset>
  <legend>Visibilidad del video</legend>

  <input type="radio" id="publico" name="visibilidad" value="publico">
  <label for="publico">Público</label>

  <input type="radio" id="privado" name="visibilidad" value="privado">
  <label for="privado">Privado</label>
</fieldset>
```

Esto mejora la organización del formulario y también la accesibilidad, porque deja más claro que esas opciones pertenecen a un mismo grupo.

## Validación nativa de formularios

Antes de pensar en validaciones con JavaScript, conviene aprovechar lo que HTML ya ofrece de forma nativa. Algunos atributos útiles son:

- `required`, para indicar que un campo es obligatorio;
- `min` y `max`, para establecer rangos en campos numéricos o fechas;
- `minlength` y `maxlength`, para limitar la longitud del texto;
- `pattern`, para definir un formato esperado;
- `type="email"`, `type="number"` y otros tipos específicos, que activan validaciones y teclados más adecuados.

Ejemplo:

```html
<form action="/registro" method="post">
  <label for="nombre">Nombre</label>
  <input type="text" id="nombre" name="nombre" required minlength="3">

  <label for="email">Correo electrónico</label>
  <input type="email" id="email" name="email" required>

  <label for="edad">Edad</label>
  <input type="number" id="edad" name="edad" min="18" max="120">

  <button type="submit">Enviar</button>
</form>
```

Estas validaciones no reemplazan todas las verificaciones posibles, pero son una primera capa muy útil. Más adelante, cuando se trabaje interacción con JavaScript, se verá cómo complementar estos controles con mensajes, validaciones personalizadas y comportamientos más específicos.

## Ejemplo de form para un sitio de videos

Supongamos que estamos desarrollando un sitio web para ver videos, al estilo de Youtube. Los usuarios usarán un formulario para subir sus videos. A continuación se muestra un ejemplo de cómo podría ser ese formulario.

```html
<form action="/subir-video" method="post"
enctype="multipart/form-data">
  <h2>Subir nuevo video</h2>

  <section>
    <label for="titulo">Título del video:</label>
    <input type="text" id="titulo" name="titulo" required>
  </section>

  <section>
    <label for="descripcion">Descripción:</label>
    <textarea id="descripcion" name="descripcion"></textarea>
  </section>

  <section>
    <label for="archivo">Archivo de video:</label>
    <input type="file" id="archivo" name="video" required>
  </section>

  <section>
    <label for="categoria">Categoría:</label>
    <select id="categoria" name="categoria" required>
      <option value="">Seleccioná una categoría</option>
      <option value="musica">Música</option>
      <option value="educacion">Educación</option>
      <option value="deportes">Deportes</option>
    </select>
  </section>

  <fieldset>
    <legend>Visibilidad</legend>

    <input type="radio" id="publico" name="visibilidad"
    value="publico" checked>
    <label for="publico">Público</label>

    <input type="radio" id="privado" name="visibilidad"
    value="privado">
    <label for="privado">Privado</label>
  </fieldset>

  <section>
    <button type="submit">Subir video</button>
  </section>
</form>
```

## Resumen de elementos de formularios

| Etiqueta | Descripción |
| :---- | :---- |
| `<form>` | Contenedor de los elementos del formulario. Permite enviar datos a un servidor. |
| `<input type="text">` | Campo para ingresar texto libre. |
| `<input type="email">` | Valida que el texto sea un correo electrónico. |
| `<input type="password">` | Oculta el texto ingresado, ideal para contraseñas. |
| `<input type="number">` | Campo numérico. Se pueden definir rangos. |
| `<input type="file">` | Permite seleccionar archivos para enviar. |
| `<input type="checkbox">` | Casilla de verificación. Puede estar marcada o no. |
| `<input type="radio">` | Opción de selección única entre varias. |
| `<textarea> </textarea>` | Área de texto multilínea, útil para comentarios o mensajes. |
| `<button>` | Botón para enviar formularios o realizar acciones según su `type`. |
| `<label>` | Asocia texto descriptivo a un campo del formulario. Mejora la accesibilidad. |
| `<fieldset>` | Agrupa campos relacionados dentro de un formulario. |
| `<legend>` | Título o descripción breve de un grupo de campos dentro de `fieldset`. |
| `<select>` | Crea un menú desplegable de opciones. |
| `<option>` | Representa cada opción dentro de un `<select>`. |

## Proyecto guiado: sistema de supermercado

Para conectar los conceptos del módulo con una situación de desarrollo más realista, a lo largo de la cursada se propone un proyecto sencillo de supermercado. La idea no es construir una aplicación completa desde el comienzo, sino usar un caso concreto para practicar cómo se estructura la información con HTML.

En una primera etapa, el proyecto puede resolverse con tres pantallas básicas:

- `carga.html`, para cargar la información de un producto.
- `ficha.html`, para mostrar el detalle completo de un producto.
- `lista.html`, para presentar un resumen de varios productos en forma de tabla.

Este ejemplo permite reutilizar casi todas las etiquetas vistas en el módulo: encabezados, párrafos, imágenes, listas, tablas y formularios. También ayuda a pensar el HTML de forma más cercana al trabajo real, donde una misma aplicación necesita páginas con objetivos distintos.

Una versión inicial del proyecto podría organizarse así:

- `carga.html`: título, formulario, campos de texto, selección de tipo, carga de imagen, precio, descripción y características.
- `ficha.html`: título principal, imagen, tipo de producto, precio, descripción y lista de características.
- `lista.html`: tabla con tipo de producto, título, precio y características resumidas.

Este proyecto volverá a aparecer en los módulos siguientes. Primero servirá para practicar HTML, luego se utilizará para aplicar estilos con CSS, mejorar accesibilidad, reorganizar código con SASS e incorporar interactividad con JavaScript.

## Validación y recursos recomendados

Aunque HTML sea un lenguaje tolerante a errores, conviene validar el código desde el comienzo. Escribir un documento que "se vea bien" no siempre significa que esté correctamente estructurado.

Hay algunos aspectos especialmente importantes para revisar:

- que el documento tenga `<!DOCTYPE html>`;
- que exista una sola etiqueta `<html>` con su atributo `lang`;
- que los encabezados sigan una jerarquía razonable;
- que las imágenes tengan atributos `alt` útiles;
- que los formularios vinculen correctamente `label` con `id`;
- que no haya etiquetas mal anidadas.

Para profundizar y validar lo aprendido, estas referencias resultan especialmente útiles:

- MDN HTML: [https://developer.mozilla.org/es/docs/Web/HTML](https://developer.mozilla.org/es/docs/Web/HTML)
- Referencia de elementos HTML en MDN: [https://developer.mozilla.org/en-US/docs/Web/HTML/Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)
- Estructura semántica en WebAIM: [https://webaim.org/techniques/semanticstructure/](https://webaim.org/techniques/semanticstructure/)
- Especificación HTML: [https://html.spec.whatwg.org/multipage/](https://html.spec.whatwg.org/multipage/)
- Validador HTML del W3C: [https://validator.w3.org/nu/](https://validator.w3.org/nu/)

Con esto queda cerrada la base estructural del desarrollo web. A esta altura, ya debería poder leer un documento HTML con mayor criterio, distinguir estructuras semánticas mejores y peores, y construir formularios y páginas simples con un nivel inicial de validación.

En el próximo módulo, el foco pasará desde el contenido hacia la presentación visual mediante CSS.

## Ejercicios del capítulo

### Comprensión

1. Explique qué información corresponde al `head` y cuál corresponde al `body` de un documento HTML.
2. Describa por qué HTML semántico mejora la accesibilidad y el SEO.
3. Explique por qué un `label` bien asociado mejora la usabilidad de un formulario.

### Aplicación

1. Construya una página HTML que incluya `head` completo, estructura semántica básica (`header`, `main`, `section`, `footer`) y al menos un bloque de contenido textual con imagen.
2. Diseñe un formulario de carga de producto con campos de nombre, precio, categoría, descripción e imagen, usando `label`, `input`, `textarea`, `select` y `button`.

### Integración

1. Construya una mini página semántica para el proyecto del supermercado que combine una ficha de producto y un formulario breve de carga o edición. Valide el resultado y registre qué ajustes tuvo que hacer para corregir errores de estructura o accesibilidad.
