# Plan de imagenes para Web 1

Este documento reúne las imágenes e infografías que conviene incorporar o revisar en el libro Introducción al desarrollo web frontend. La idea no es ilustrar cada sección, sino reforzar los conceptos que más se benefician de una explicación visual.

## Criterio general

Conviene priorizar imágenes cuando ocurra al menos una de estas situaciones:

- el concepto describe una estructura o un flujo;
- la explicación requiere comparar estados o comportamientos;
- el lector necesita "ver" relaciones espaciales o jerárquicas;
- una imagen puede reemplazar varios párrafos sin perder precisión.

## Prompt general de estilo visual

Este prompt puede reutilizarse como base en ChatGPT o Gemini para mantener consistencia entre las imágenes del libro.

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9
```

## Imágenes prioritarias

### 1. Navegador, servidor y respuesta web

- Capítulo: `00-intro.md`
- Ubicación sugerida: después de la sección "Qué ocurre cuando abrimos una página web"
- Archivo existente: `assets/intro-request.png`
- Objetivo: mostrar el ciclo URL -> DNS -> solicitud HTTP -> servidor -> respuesta -> navegador
- Tipo de imagen: diagrama de flujo simple
- Valor pedagógico: alto
- Nota: serviría como imagen base para entender luego formularios, APIs y `fetch`

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una infografía horizontal que explique el flujo entre navegador, DNS, servidor web y respuesta HTTP. Mostrar de izquierda a derecha: navegador con barra de URL, resolución DNS, envío de solicitud HTTP, servidor procesando, respuesta HTTP y navegador renderizando el contenido. Incluir flechas claras entre etapas y una línea inferior opcional con pasos resumidos: URL, DNS, solicitud HTTP, servidor, respuesta, navegador. Evitar detalles de red avanzados; el objetivo es que un estudiante principiante entienda el circuito general de apertura de una página web.
```

### 2. Diferencia entre Internet y la Web

- Capítulo: `00-intro.md`
- Ubicación sugerida: después de "Internet y la Web, parecidos pero distintos"
- Archivo existente: `assets/intro-internet-web.png`
- Objetivo: separar infraestructura, servicios y navegación web
- Tipo de imagen: esquema conceptual comparativo
- Valor pedagógico: medio
- Nota: puede resolverse con un gráfico muy simple, sin detalles históricos

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una imagen comparativa simple que diferencie Internet y la Web. Representar Internet como infraestructura amplia de red y servicios, y la Web como uno de esos servicios dentro de esa infraestructura. Incluir visualmente dispositivos conectados o una red general para Internet, y dentro de ella un subconjunto asociado a páginas, navegador, enlaces y HTTP para la Web. La composición debe dejar muy clara la relación de inclusión: la Web forma parte de Internet, pero no es lo mismo. Mantener muy poco texto y rótulos directos.
```

### 3. Anatomía de un documento HTML

- Capítulo: `01-html.md`
- Ubicación sugerida: después de "La estructura básica de un documento HTML"
- Archivo existente: `assets/html-estructura-documento.png`
- Objetivo: mostrar visualmente `doctype`, `html`, `head` y `body`
- Tipo de imagen: diagrama en capas o bloque anotado
- Valor pedagógico: alto
- Nota: ayudaría a fijar la diferencia entre estructura del archivo y contenido visible

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear un diagrama vertical u horizontal que muestre la estructura de un archivo HTML. Representar claramente `<!DOCTYPE html>`, `<html lang="es">`, `<head>` y `<body>` como bloques jerárquicos. A la derecha o debajo, agregar anotaciones breves que expliquen qué entiende el navegador en cada parte. Debe quedar muy clara la diferencia entre información estructural del archivo y contenido visible del documento. No incluir demasiadas etiquetas secundarias; priorizar solo la estructura base.
```

### 4. Estructura semántica de una página

- Capítulo: `02-html-detalle.md`
- Ubicación sugerida: en la sección de HTML5 semántico
- Archivo existente: `assets/html-layout.png`
- Objetivo: mostrar `header`, `nav`, `main`, `section`, `article`, `aside` y `footer`
- Tipo de imagen: wireframe semántico etiquetado
- Valor pedagógico: muy alto
- Nota: probablemente sea una de las imágenes más útiles del libro

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear un wireframe semántico de una página web con bloques claramente etiquetados como `header`, `nav`, `main`, `section`, `article`, `aside` y `footer`. La composición debe parecer un esquema de layout, no una interfaz terminada. Mostrar cómo se distribuyen estas regiones dentro de una página típica y remarcar visualmente que cada bloque cumple una función estructural distinta. Mantener etiquetas visibles y ordenadas, con pocas distracciones.
```

### 5. Anatomía de un formulario accesible

- Capítulo: `02-html-detalle.md`
- Ubicación sugerida: antes o durante la sección de formularios
- Archivo existente: `assets/html-fieldset.png`
- Objetivo: mostrar relación entre `label`, `input`, `fieldset`, `legend`, ayuda y mensaje de error
- Tipo de imagen: diagrama anotado de formulario
- Valor pedagógico: alto
- Nota: esta imagen puede reutilizarse conceptualmente en accesibilidad

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear un diagrama anotado de un formulario accesible, pero simplificado para nivel inicial. Mostrar solo estos elementos: `label` + `input` asociados, un `fieldset` con `legend`, un texto de ayuda y un único ejemplo de error. Limitar la pieza a 5 o 6 llamadas breves como máximo. Evitar lista larga de atributos ARIA o bloques secundarios extensos. El objetivo es explicar relaciones estructurales básicas del formulario (qué etiqueta describe qué campo y cómo se comunica ayuda/error), no construir una lámina de referencia completa.
```

### 6. Cascada y especificidad

- Capítulo: `03-css.md`
- Ubicación sugerida: en "Especificidad y cascada en CSS"
- Archivo existente: `assets/css-prioridad-reglas.png`
- Objetivo: mostrar cómo compiten varias reglas sobre un mismo elemento
- Tipo de imagen: tabla o diagrama de prioridad
- Valor pedagógico: muy alto
- Nota: ayudaría más que seguir agregando ejemplos textuales

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una infografía de prioridad entre reglas CSS con enfoque minimalista. Estructurar en 3 zonas: (1) un ejemplo corto con 3 o 4 reglas que compiten sobre el mismo elemento, (2) un flujo de decisión simple con solo estos pasos: `!important` (si aparece), especificidad, orden de aparición, (3) una mini tabla de puntajes con `elemento`, `clase`, `id` y `estilo en línea`. Evitar tablas grandes, listas largas y demasiados casos simultáneos. Debe sentirse como una guía de lectura rápida, no como una lámina enciclopédica.
```

### 7. Box model

- Capítulo: `03-css.md`
- Ubicación sugerida: ya incorporada en la sección correspondiente
- Archivo existente: `assets/css-box-model.png`
- Objetivo: mantenerla y revisar si el estilo visual sigue siendo consistente con el resto del libro
- Valor pedagógico: alto

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una infografía del box model de CSS que muestre con claridad `content`, `padding`, `border` y `margin`, con medidas de ancho y alto cuando ayuden a interpretar el concepto. Puede añadirse una comparación pequeña sobre margen colapsado y no colapsado si la composición sigue siendo clara. La prioridad es explicar cómo se organiza el espacio de un elemento CSS, no decorar la pieza.
```

### 8. Dirección y salto de línea en Flexbox

- Capítulo: `03-css.md`
- Ubicación sugerida: en "Cómo pensar los ejes en Flexbox"
- Archivo existente: `assets/css-flexbox-direction.png`
- Objetivo: mostrar `flex-direction` y `flex-wrap` como base para entender el eje principal y el salto de línea
- Valor pedagógico: alto

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una infografía centrada solo en `flex-direction` y `flex-wrap`. Incluir `row`, `row-reverse`, `column` y `column-reverse`, y una comparación simple entre `nowrap` y `wrap`. Usar flechas, ejes y distribución de cajas para que el lector vea rápidamente cómo cambia la disposición de los ítems. No agregar todavía `justify-content`, `align-items` ni `align-content`.
```

### 9. Alineación en Flexbox

- Capítulo: `03-css.md`
- Ubicación sugerida: después de la sección de ejes y cerca de `justify-content` y `align-items`
- Archivo existente: `assets/css-flexbox-alineacion.png`
- Objetivo: mostrar cómo cambian la distribución y la alineación con `justify-content`, `align-items` y, si entra con claridad, `align-content`
- Tipo de imagen: comparación de distribuciones dentro de un contenedor flex
- Valor pedagógico: alto
- Nota: conviene resolverla como una segunda pieza breve y no como una lámina enciclopédica

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una infografía centrada en alineación dentro de Flexbox. Incluir pocos casos de `justify-content` y `align-items`, mostrando diferencias claras entre inicio, fin, centro y distribución del espacio. Solo agregar `align-content` si la composición sigue siendo simple y muy legible. La imagen debe sentirse como una continuación de la pieza sobre `flex-direction` y `flex-wrap`, no como una lámina de referencia total.
```

### 10. Grilla de CSS Grid

- Capítulo: `03-css.md`
- Ubicación sugerida: entre "Grid Layout" y "Ubicar elementos en filas y columnas"
- Archivo existente: `assets/css-grid.png`
- Objetivo: mostrar filas, columnas, áreas y spans
- Tipo de imagen: grilla anotada
- Valor pedagógico: muy alto
- Nota: hoy es el concepto visual más huérfano del capítulo de CSS

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una infografía de CSS Grid centrada en una sola idea principal: Grid como estructura bidimensional de filas y columnas. Mostrar una grilla base con filas y columnas claramente visibles, y solo uno o dos ejemplos simples de elementos ocupando varias columnas o varias filas. Evitar convertir la imagen en una referencia completa de Grid: no mezclar demasiadas etiquetas, no mostrar demasiadas líneas o numeraciones, y no agregar áreas nombradas salvo que la composición siga siendo extremadamente simple. El objetivo es que el lector entienda de un vistazo cómo Grid organiza el espacio y cómo un elemento puede expandirse dentro de esa estructura.
```

### 11. Orden de foco y navegación por teclado

**NO USAREMOS ESTA IMAGEN**

- Capítulo: `06-accesibilidad.md`
- Ubicación sugerida: en "Contraste, foco y navegación por teclado"
- Objetivo: mostrar recorrido de foco correcto e incorrecto sobre una interfaz simple
- Tipo de imagen: comparación lado a lado
- Valor pedagógico: muy alto
- Nota: sería más útil que una imagen puramente decorativa

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una comparación lado a lado entre una interfaz con orden de foco correcto y otra con orden de foco incorrecto. Representar botones, enlaces o campos simples y usar flechas numeradas o una secuencia visual de tabulación. El foco debe verse claramente en cada paso. La imagen debe dejar en evidencia qué recorrido respeta el orden lógico de lectura e interacción y cuál genera confusión para quien navega con teclado.
```

### 12. Responsive como reorganización, no solo reducción

- Capítulo: `06-accesibilidad.md`
- Ubicación sugerida: en "Responsive design como parte de la experiencia"
- Archivo existente: `assets/css-responsive.png`
- Objetivo: comparar una misma pantalla en desktop y mobile mostrando cambio de jerarquía y no solo cambio de ancho
- Tipo de imagen: comparación de dos wireframes
- Valor pedagógico: alto

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una comparación entre una misma interfaz en desktop y mobile. No mostrar solo una reducción de tamaño: mostrar reorganización real de jerarquía y layout. Incluir, por ejemplo, encabezado, navegación, contenido principal, tarjeta o lista, y acciones principales reubicadas según el dispositivo. El objetivo es enseñar que responsive design implica reorganizar la experiencia, no solo achicar elementos.
```

### 13. Árbol DOM y selección de nodos

- Capítulo: `08-dom-debugging.md`
- Ubicación sugerida: después de "Qué es el DOM"
- Archivo existente: `assets/js-dom.png`
- Objetivo: mostrar HTML fuente, árbol DOM y un selector apuntando a un nodo concreto
- Tipo de imagen: árbol simplificado
- Valor pedagógico: muy alto
- Nota: ayudaría a separar mejor DOM de HTML escrito

Prompt sugerido:

```
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear una imagen que conecte tres niveles: a la izquierda un fragmento simple de HTML, en el centro un árbol DOM simplificado derivado de ese HTML, y a la derecha o sobre el árbol una indicación de un selector que apunta a un nodo concreto. El objetivo es que el lector vea que el DOM no es solo texto escrito, sino una estructura jerárquica sobre la que JavaScript puede operar.
```

### 14. Flujo básico de un evento

- Capítulo: `09-interaccion.md`
- Ubicación sugerida: después de "Eventos del navegador" o "El objeto event y preventDefault"
- Archivo existente: `assets/js-eventos.png`
- Objetivo: mostrar evento -> handler -> validación -> actualización de interfaz
- Tipo de imagen: diagrama de flujo
- Valor pedagógico: alto

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Crear un diagrama de flujo simple sobre eventos en el navegador. Mostrar una interacción inicial, por ejemplo click o submit, seguida por el evento, el handler en JavaScript, una validación o condición, y finalmente una actualización visible de la interfaz. Usar cajas conectadas por flechas, con rótulos muy breves. El objetivo es explicar el circuito mínimo que sigue una interacción controlada con JavaScript.
```

### 15. Fetch y actualización de interfaz

- Capítulo: `09-interaccion.md`
- Ubicación sugerida: en "Fetch como interacción asincrónica"
- Archivo existente: `assets/js-fetch.png`
- Objetivo: mostrar solicitud -> estado cargando -> respuesta -> renderizado o error
- Tipo de imagen: diagrama de estados
- Valor pedagógico: alto
- Nota: conviene que use el caso del supermercado, por ejemplo categorías o productos

Prompt sugerido:

```text
Crear una infografía didáctica para un libro universitario introductorio sobre desarrollo web frontend. Estilo visual esquemático, limpio, moderno y consistente, con apariencia de diagrama editorial más que de interfaz realista. Fondo blanco, gran uso de espacio en blanco, bloques principales en azul profundo, elementos internos en turquesa/cian claro, si destacas elementos o bloques, usa rojo vino, el texto en negro o azul muy oscuro con tipografia sans-serif de facil lectura, líneas auxiliares punteadas o discontinuas, flechas simples, etiquetas claras y alto contraste.

Usar formas geométricas simples con bordes redondeados, composición ordenada, jerarquía visual clara y lectura inmediata. Evitar realismo, fotografías, texturas complejas, efectos 3D, exceso de detalle, mockups de software, sombras pesadas o estética corporativa genérica. Priorizar diagramas vectoriales, wireframes, cajas, contenedores, ejes, flechas, agrupaciones y rótulos breves.

Evita crear una “lámina de referencia” en vez de “infografía pedagógica rápida”. Queremos evitar: demasiadas etiquetas simultáneas, demasiados bloques secundarios, y exceso de texto explicativo. Recuerda que esta imagen sera parte de un libro y los conceptos ya estan explicados en el texto del libro.

La tipografía debe verse como sans serif o monoespaciada de alto peso, muy legible, con títulos cortos y etiquetas exactas. Mantener una paleta consistente: azul profundo para contenedores, turquesa/celeste para elementos activos o contenidos, rojo vino para destacar, blanco para flechas o líneas sobre fondos oscuros, y negro para títulos externos cuando haga falta. Evita textos largos, para que la tipografia no termine siendo muy pequeña. Preferiblemente esa formato 16:9

Usar el prompt general de estilo visual. Título exacto de la pieza: "FETCH EN EL SUPERMERCADO: ESTADOS DE INTERFAZ".

Crear un diagrama de estados para explicar `fetch` en la interfaz del supermercado. Mostrar cuatro momentos: `solicitud`, `cargando`, `éxito` y `error`. Mantener un solo caso concreto para evitar ruido: carga de categorías (`GET /categories/`). En éxito, mostrar categorías renderizadas; en error, mostrar un mensaje breve visible para el usuario. No incluir rutas ficticias como `/api/categories` ni detalles de backend.

La composición debe ser limpia: un flujo principal horizontal y, desde `cargando`, bifurcación simple a `éxito` o `error`. Máximo 1 línea de texto por bloque y etiquetas cortas. El objetivo es conectar asincronía con experiencia de usuario de un vistazo.
```

## Orden sugerido de producción

1. Estructura semántica de una página
2. Navegador, servidor y respuesta web
3. Cascada y especificidad
4. Dirección y salto de línea en Flexbox
5. Alineación en Flexbox
6. Grilla de CSS Grid
7. Árbol DOM y selección de nodos
8. Flujo básico de un evento
9. Orden de foco y navegación por teclado
10. Responsive como reorganización
11. Anatomía de un formulario accesible
12. Fetch y actualización de interfaz

## Observaciones finales

- No conviene saturar el libro con capturas de pantalla genéricas.
- En general, los diagramas esquemáticos enseñan mejor que las interfaces demasiado realistas.
- Siempre que una imagen represente estructura o flujo, conviene acompañarla con una leyenda breve que recupere la idea principal.
- Las imágenes de CSS, DOM y accesibilidad son las que más retorno pedagógico deberían tener en una próxima iteración.
