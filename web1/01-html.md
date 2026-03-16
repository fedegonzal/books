# Lenguaje de marcas de hipertexto (HTML)

HTML es el punto de partida técnico del libro porque organiza la información que después será estilizada con CSS y enriquecida con JavaScript. En este capítulo se presenta la estructura general del lenguaje, sus reglas básicas y los primeros criterios para escribir documentos claros, legibles y correctos.

## Objetivos del capítulo

- identificar la estructura mínima de un documento HTML y la función de sus partes principales;
- distinguir etiquetas estructurales, de contenido y de interacción;
- reconocer la diferencia entre elementos de bloque, en línea y atributos frecuentes;
- escribir primeros documentos HTML con criterios básicos de orden, semántica y legibilidad.

## Qué es HTML y su importancia para la web

El Lenguaje de Marcado de Hipertexto o HTML (HyperText Markup Language), es el lenguaje base que se utiliza para crear páginas web. Es un conjunto de etiquetas que se escriben en un archivo de texto y que indican al navegador cómo debe estructurar y mostrar el contenido: texto, imágenes, enlaces, listas, tablas, formularios, entre otros elementos.

Cada página web que ves en Internet está construida, en su forma más básica, con HTML. Este lenguaje no programa funciones lógicas como lo haría JavaScript, ni define estilos visuales como lo hace CSS, pero sí organiza el contenido para que pueda ser leído e interpretado correctamente por los navegadores web.

La importancia de HTML radica en que es el cimiento sobre el que se construye toda la web. Sin HTML, no habría forma de presentar contenido estructurado en Internet. Además, es esencial para la accesibilidad, el posicionamiento en buscadores (SEO) y la interoperabilidad entre diferentes dispositivos.

Aprender HTML es el primer paso para cualquier persona que quiera crear sitios web o entender cómo funciona el contenido en línea. Es una herramienta fundamental en el mundo digital moderno.

## La estructura básica de un documento HTML

Todo documento HTML sigue una estructura fundamental que permite a los navegadores interpretar correctamente el contenido. Esta estructura se compone de elementos esenciales que organizan la página en secciones específicas.

Un archivo HTML comienza con la declaración `<!DOCTYPE html>`, que le indica al navegador que se trata de un documento en HTML5, la versión actual del lenguaje.

Después, encontramos la etiqueta `<html>`, que encierra todo el contenido del documento. Dentro de ella se ubican dos partes principales: `<head>` y `<body>`.

La sección `<head>` contiene información meta sobre la página, como el título, la codificación de caracteres y enlaces a hojas de estilo o scripts. Aunque esta parte no se ve directamente en el navegador, es fundamental para el correcto funcionamiento del sitio.

La sección `<body>` es donde se coloca todo el contenido visible de la página: títulos, párrafos, imágenes, enlaces, listas, etc.

También es habitual incluir comentarios para dejar notas dentro del código sin que aparezcan en la página renderizada. La sintaxis es `<!-- comentario -->` y conviene usarla solo cuando aporta contexto real.

La estructura básica de un documento HTML se ve así:

```
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<title>Mi primera página</title>
</head>
<body>
<h1>¡Hola, mundo!</h1>
<p>Este es mi primer documento HTML.</p>
<a href="https://www.ejemplo.com">Visita mi sitio</a>
</body>
</html>
```

## Características sintácticas del HTML

HTML es un lenguaje de marcado muy flexible en cuanto a su sintaxis. A diferencia de los lenguajes de programación estrictos, HTML permite ciertas libertades que facilitan el aprendizaje, especialmente para quienes se inician en el desarrollo web.

Una de sus características es que se pueden cortar las líneas libremente. Es decir, no importa si una etiqueta se escribe en una sola línea o si se separa en varias; el navegador interpretará el código correctamente mientras las etiquetas estén bien cerradas.

Además, si hay errores de tipeo menores, como una etiqueta mal escrita o no cerrada, el navegador intenta continuar la ejecución del documento. En lugar de mostrar un error crítico, como lo haría un lenguaje como Java o Python, simplemente ignora el error o intenta “adivinar” lo que el autor quiso hacer. Esto permite que las páginas sigan funcionando, aunque con posibles fallos visuales o de estructura.

Otra característica importante es que la tabulación o indentación del código no es obligatoria. Sin embargo, se recomienda fuertemente para mejorar la legibilidad, especialmente en documentos largos con muchas etiquetas anidadas.

También vale la pena mencionar que HTML no distingue entre mayúsculas y minúsculas en sus etiquetas, aunque por convención y buenas prácticas, se recomienda escribirlas en minúsculas. Por ejemplo, `<h1>` y `<H1>` funcionarán igual, pero la primera forma es la estándar actual.

En resumen, HTML es tolerante y accesible, lo que lo hace ideal para comenzar a crear sitios web. Sin embargo, seguir buenas prácticas desde el inicio facilita el mantenimiento y comprensión del código en el futuro.

### **Estructura general de una etiqueta y sus atributos**

Las etiquetas, más allá de su nombre y función básica, pueden incluir atributos que definen propiedades o comportamientos específicos de los elementos. Los atributos permiten personalizar cómo los elementos de una página web se comportan o se presentan. Cada atributo tiene un nombre y un valor, y se colocan dentro de la etiqueta de apertura, generalmente después del nombre de la etiqueta.

Por ejemplo, para agregar una imagen:  
```
<img src="foto.jpg">
```

Como puede verse, un atributo tiene un nombre y un valor, en este caso el nombre del atributo es "src" y su valor "foto.jpg".

Los atributos siempre deben estar dentro de la etiqueta de apertura, y el valor del atributo generalmente se coloca entre comillas dobles (" "), aunque en algunos casos también se pueden usar comillas simples (' ').

Algunos atributos están disponibles en casi todas las etiquetas HTML y permiten definir estilos, identificadores, eventos y mucho más. Los dos más comunes son:

| Atributo | Descripción |
| :---- | :---- |
| `id` | Define un nombre único para identificar al elemento |
| `class` | Asigna una clase que luego podrá usarse para definir estilos visuales o comportamientos |

Conviene distinguir ambos atributos desde el comienzo. Un `id` identifica un elemento único dentro del documento, mientras que `class` permite agrupar varios elementos bajo un mismo criterio. Más adelante, cuando se trabajen CSS y JavaScript, esta diferencia será clave para seleccionar y manipular elementos con precisión.

## Tipos de etiquetas en HTML

En HTML, las etiquetas se pueden clasificar según su función dentro del documento. Una forma sencilla de organizarlas es dividiéndolas en tres grupos principales: **estructurales, de contenido y de interacción**.

Las etiquetas estructurales definen la organización general de la página. Ayudan a establecer el esqueleto del sitio y facilitan la comprensión tanto para los navegadores como para motores de búsqueda. Algunos ejemplos son `<html>`, `<head>`, `<body>`, `<header>`, `<main>`, `<section>` y `<footer>`.

Las etiquetas de contenido (también llamadas básicas) son las que permiten mostrar información al usuario: títulos, párrafos, imágenes, listas, enlaces, etc. Aquí encontramos etiquetas como `<h1>` a `<h6>` para títulos, `<p>` para párrafos, `<img>` para imágenes y `<a>` para enlaces.

Por último, las etiquetas de interacción están diseñadas para que el usuario pueda enviar datos o interactuar con el sitio. Se usan principalmente en formularios. Algunos ejemplos son `<form>`, `<input>`, `<textarea>`, `<button>` y `<select>`.

Esta clasificación no es oficial, pero resulta útil para entender cómo se construye una página HTML y qué función cumple cada grupo de etiquetas. Con el tiempo, se aprenderá a combinarlas para crear sitios completos y funcionales.

### **Etiquetas estructurales más comunes**

| Etiqueta | Descripción técnica | Atributos comunes |
| :---- | :---- | :---- |
| `<html>` | Elemento raíz de todo documento HTML. Debe contener `<head>` y `<body>`. | lang |
| `<head>` | Contiene metadatos del documento: título, enlaces, scripts, etc. No muestra contenido visual. | (generalmente no se le aplican atributos) |
| `<body>` | Contenedor de todo el contenido visual de la página. | onload, class, id, style |
| `<header>` | Define una cabecera para una sección o página. Puede contener logos, menús, etc. | class, id, style |
| `<main>` | Representa el contenido principal del documento, único por página. | class, id, style |
| `<section>` | Agrupa contenido temáticamente relacionado. Ideal para dividir por temas. | class, id, style |
| `<footer>` | Define un pie de página para una sección o todo el sitio. Suele incluir contacto, autoría, etc. | class, id, style |
| `<div>` | Contenedor genérico sin significado semántico. Se usa para agrupar contenido y aplicar estilos. | class, id, style |
| `<span>` | Contenedor en línea genérico. Ideal para aplicar estilos o scripts a fragmentos dentro de un texto. | class, id, style |

Hay muchas más etiquetas estructurales, por ejemplo `<nav>` (para navegación) y `<article>` (contenido), el estudio de las nuevas etiquetas será parte de la práctica cotidiana, no es necesario conocerlas a todas desde el principio.

### **Etiquetas de contenido más comunes**

| Etiqueta | Descripción técnica | Atributos comunes |
| :---- | :---- | :---- |
| `<h1>..<h6>` | Encabezados jerárquicos. `<h1>` es el más importante; `<h6>`, el menos. | class, id, style |
| `<p>` | Representa un párrafo de texto. | class, id, style |
| `<a>` | Define un enlace a otra página o recurso. | href, target, title, class |
| `<img>` | Inserta una imagen. Es una etiqueta auto-cerrada. | src, alt, width, height, class |
| `<ul>` | Lista no ordenada (con viñetas). | class, id, style |
| `<ol>` | Lista ordenada (numerada). | type, start, reversed |
| `<li>` | Elemento de lista. Va dentro de `<ul>` o `<ol>`. | class, id |
| `<strong>` | Marca un texto como importante. Semánticamente equivale a negrita. | class, id, style |
| `<em>` | Da énfasis al texto. Semánticamente equivale a cursiva. | class, id, style |

`<br>` (salto de línea) y `<hr>` (línea horizontal) también son útiles para conocer. No requieren atributos y son muy simples.

### **Etiquetas de interacción más comunes**

| Etiqueta | Descripción técnica | Atributos comunes |
| :---- | :---- | :---- |
| `<form>` | Agrupa campos de entrada. Envía datos a un servidor. | action, method, enctype, name, autocomplete |
| `<input>` | Campo de entrada flexible. El tipo se define con el atributo type. | type, name, value, placeholder, required |
| `<textarea>` | Área de texto de varias líneas. | name, rows, cols, placeholder, required |
| `<button>` | Botón para enviar el formulario o ejecutar una acción. | type, name, value, disabled |
| `<label>` | Etiqueta que se asocia a un campo de entrada. Mejora la accesibilidad. | for (asocia con el id del input), class, id |
| `<select>` | Lista desplegable para elegir entre varias opciones. | name, required, multiple |
| `<option>` | Define una opción dentro de un `<select>`. | value, selected, disabled |

En HTML existen atributos de evento como `onclick`, pero en este libro se priorizará trabajar esos comportamientos desde JavaScript con `addEventListener()`, porque esa estrategia mantiene mejor separadas la estructura y la lógica.

## Tipos de elementos y modelos de contenidos

Comprender qué elementos (etiquetas) pueden ir dentro de otros es fundamental para estructurar un documento HTML y garantizar que funcione correctamente, ya que las etiquetas deben estar correctamente anidadas. Los errores de anidamiento pueden dar lugar a código mal interpretado por el navegador.

HTML tiene varias reglas sobre qué elementos pueden contener a otros, y estas reglas dependen del modelo de contenido de cada etiqueta. Los **modelos de contenido** definen los tipos de elementos que un contenedor puede aceptar. 

### **Elementos vacíos o auto-cerrados (void elements)**

Son los más simples porque no tienen contenido interno y no requieren una etiqueta de cierre. Ejemplos: `<img>`, `<br>`, `<hr>`

No pueden contener elementos dentro de ellos. Por ejemplo, `<img>` no puede tener ni un `<div>` ni un `<span>` dentro.

### **Elementos en línea**

Estos elementos no interrumpen el flujo del texto y solo ocupan el espacio necesario para su contenido. Esto quiere decir que si un elemento (con su contenido) no ocupa el ancho completo de la página, el siguiente elemento se verá a continuación (a la derecha) y no debajo, porque son "en línea". Ejemplos: `<span>`, `<a>`, `<strong>`, `<img>` 

Puede notarse que `<img>` es un elemento definido como auto-cerrado y en línea.

Los elementos en línea normalmente contienen adentro otros elementos en línea o elementos auto-cerrados, pero no elementos de bloque, como se verá a continuación.

### **Elementos de bloque (block-level elements)**

Los elementos de bloque generalmente pueden contener cualquier tipo de elementos adentro (en línea, otros elementos de bloque y también auto-cerrados).

Muchos de los elementos estructurales son elementos de bloque, por ejemplo `<section>`, `<footer>`, `<div>` y se utilizan para agrupar elementos en la página, pero la definición de "bloque" no tiene tanto que ver con el agrupamiento, sino más bien con el hecho de que un elemento de bloque ocupará todo el ancho de la página sin importar lo que tenga adentro, y el próximo elemento se verá abajo y no a la derecha.

Esto queda claro con la etiqueta `<p>` que es un elemento de bloque que define un párrafo. Cada párrafo implica que el siguiente se verá abajo (porque justamente es un párrafo), pero a la vez una etiqueta `<p>` no puede contener dentro una etiqueta `<div>`.

Como puede observarse no hay una jerarquía explícita de qué grupos de etiquetas pueden ir dentro de otras, cada situación dependerá de la etiqueta que se esté usando. No obstante, con la práctica esto se vuelve cada vez más evidente.

Una forma rápida de pensarlo es la siguiente: si un elemento se comporta como parte del flujo del texto, probablemente sea en línea; si organiza el contenido como una caja independiente dentro de la página, probablemente sea de bloque. Esta distinción será especialmente importante cuando se empiece a trabajar con CSS.

Para más información se recomienda ver estos dos artículos:

[https://developer.mozilla.org/en-US/docs/Glossary/Inline-level_content](https://developer.mozilla.org/en-US/docs/Glossary/Inline-level_content)

[https://developer.mozilla.org/en-US/docs/Glossary/Block-level_content](https://developer.mozilla.org/en-US/docs/Glossary/Block-level_content)

## Buenas prácticas iniciales para escribir HTML

Aunque HTML sea tolerante a errores, conviene incorporar buenas prácticas desde el inicio. Escribir etiquetas en minúsculas, indentar de manera consistente, cerrar correctamente los elementos y elegir marcas con sentido semántico hace que el documento sea más fácil de leer y mantener.

También es importante pensar la accesibilidad desde el comienzo. Una imagen debería tener un `alt` útil cuando aporta información, un formulario debería usar `label` asociado a sus campos y la jerarquía de títulos debería seguir un orden razonable. Estos criterios no son un agregado posterior: forman parte de escribir buen HTML.

Con esta base ya se puede pasar a un segundo nivel de profundidad. El próximo capítulo tomará estas nociones iniciales y las desarrollará sobre etiquetas, estructuras y usos más específicos.

## Ejercicios del capítulo

### Comprensión

1. Explique qué función cumplen `<!DOCTYPE html>`, `<head>` y `<body>` dentro de un documento HTML.
2. Describa la diferencia entre un elemento de bloque y un elemento en línea usando un ejemplo de cada uno.
3. Explique con sus palabras cuándo conviene usar `id` y cuándo conviene usar `class`.

### Aplicación

1. Escriba un documento HTML mínimo que incluya un título principal, un párrafo, un enlace y una imagen con atributo `alt`.
2. Revise el siguiente criterio sobre una página suya o de ejemplo: ¿hay etiquetas mal anidadas, títulos desordenados o imágenes sin texto alternativo? Registre qué corregiría.

### Integración

1. Diseñe la estructura HTML básica de una ficha de producto para el proyecto de supermercado. Incluya nombre, imagen, precio, descripción y una lista de características.
