# Introducción al desarrollo web

Antes de escribir la primera etiqueta HTML conviene entender, aunque sea de forma general, en qué entorno técnico se construyen las páginas web. Este capítulo presenta ese marco: qué es Internet, qué es la Web, qué papel cumplen los navegadores, cómo se relacionan frontend y backend y por qué el desarrollo web exige pensar en diversidad de dispositivos, personas y contextos de uso.

## Objetivos del capítulo

- distinguir Internet de la Web y ubicar a la Web como un servicio dentro de esa infraestructura;
- describir de manera general cómo interactúan navegador, servidor, URL y protocolos web;
- reconocer el papel de HTML, CSS y JavaScript dentro del desarrollo frontend;
- comprender por qué la diversidad de usuarios, dispositivos y contextos forma parte del problema técnico.

## Internet y la Web, parecidos pero distintos

Al hablar de Internet, muchas veces se confunde el término con la Web, pero se trata de dos conceptos relacionados y diferentes. Internet es la infraestructura: una red global de computadoras y dispositivos conectados que permite intercambiar datos. Sobre esa infraestructura funcionan muchos servicios, por ejemplo correo electrónico, transferencia de archivos, videollamadas, mensajería instantánea, streaming y, entre ellos, también la Web.

Una analogía útil es pensar en Internet como el sistema de carreteras que conecta ciudades (dispositivos), y en la Web como los edificios y tiendas a los que se accede por esas carreteras.

La Web (o World Wide Web, WWW) es un servicio dentro de Internet que permite acceder y compartir información a través de páginas web. Funciona con protocolos como HTTP y HTTPS, y se basa en enlaces hipertextuales que permiten navegar de una página a otra. Se accede a través de navegadores como Chrome o Firefox, y su contenido incluye textos, imágenes, videos y aplicaciones interactivas.

## Breve historia de internet

Internet nació en la década de 1960 como un proyecto del Departamento de Defensa de EE.UU. para crear una red de comunicación resistente a fallos. En 1969, se estableció ARPANET, la primera red de computadoras interconectadas, conectando universidades como UCLA y Stanford.

En los años 70, se desarrollaron los protocolos TCP/IP, que permitieron la expansión de la red y su estandarización. En 1983, ARPANET adoptó oficialmente TCP/IP, marcando el inicio de Internet moderno. Durante los 80, se crearon redes académicas y comerciales, y en 1989, Tim Berners-Lee inventó la World Wide Web (WWW), introduciendo los conceptos de páginas web, enlaces y navegadores.

En los años 90, la Web popularizó Internet con navegadores como Mosaic y Netscape, facilitando el acceso a información y servicios. Empresas como Google (1998) y Amazon (1994) transformaron la forma en que usamos la red.

En el siglo XXI, Internet evolucionó con redes sociales, servicios de streaming y dispositivos móviles. Hoy, con tecnologías como 5G, inteligencia artificial y computación en la nube, Internet sigue revolucionando la comunicación, la educación y la economía a nivel global.

## Breve historia de la Web

La World Wide Web (WWW) fue desarrollada entre marzo y diciembre de 1989​ por el inglés Tim Berners-Lee con la ayuda del belga Robert Cailliau, mientras trabajaban en el CERN en Ginebra, Suiza.

El objetivo inicial fue compartir información entre investigadores. La Web fue pensada a partir de tres elementos fundamentales: HTML (lenguaje de marcado), HTTP (protocolo de transferencia) y URL (sistema de direcciones web). 

El primer servidor Web se encontraba en la oficina de Tim Berners-Lee en el CERN y fue puesto en línea el 6 de agosto de 1991. El número de servidores Web pasó a 26 en 1992, y a 200 en octubre de 1995. En la actualidad se estima que existen casi 1.000 millones en todo el mundo.

¡La primera página web de la historia todavía existe! [https://info.cern.ch/hypertext/WWW/TheProject.html](https://info.cern.ch/hypertext/WWW/TheProject.html) 

A mediados de los 90, la Web se popularizó con navegadores como Mosaic y Netscape, que permitieron una navegación más fácil y visual. Empresas como Yahoo! (1994), Amazon (1994) y Google (1998) surgieron en esta época, expandiendo su uso comercial.

En los 2000, llegó la Web 2.0, caracterizada por la interactividad y el contenido generado por usuarios. Plataformas como Facebook (2004), YouTube (2005) y Twitter (2006) revolucionaron la comunicación y el entretenimiento.

Hoy, la Web sigue evolucionando con nuevas capacidades vinculadas a la inteligencia artificial, las aplicaciones en tiempo real, la computación en la nube y experiencias cada vez más interactivas. Desde su creación, ha transformado la forma en que accedemos a la información, compramos, trabajamos y nos conectamos globalmente.

Actualmente Tim Berners-Lee dirige el W3C, organismo que establece los estándares de la web.

## ¿Qué es la W3C? (y por qué es importante)

La W3C, cuyas siglas significan World Wide Web Consortium, es una organización internacional sin fines de lucro fundada en 1994 por Tim Berners-Lee, el creador de la World Wide Web. Desde sus inicios, su misión ha sido "desarrollar y promover estándares abiertos que aseguren el crecimiento y la estabilidad de la web a largo plazo".

Esta organización cumple un rol fundamental en el ecosistema digital actual. Entre sus principales tareas está la creación y mantenimiento de estándares como HTML, CSS, XML y SVG, entre muchos otros. Gracias a estos estándares, los desarrolladores web pueden crear sitios que funcionan de manera coherente y predecible en distintos navegadores, sistemas operativos y dispositivos. Sin estos lineamientos comunes, la experiencia de navegar por internet sería muy diferente y probablemente mucho más caótica.

Uno de los principios fundamentales que defiende la W3C es la accesibilidad. Es decir, que la web debe ser utilizable por todas las personas, incluidas aquellas con discapacidades. También trabaja por la interoperabilidad, que permite que las tecnologías funcionen bien juntas sin importar quién las haya creado, y promueve valores esenciales como la privacidad, la seguridad y la neutralidad tecnológica, evitando que una sola empresa o proveedor imponga sus reglas sobre el funcionamiento de la web.

La importancia de la W3C radica justamente en esto: al definir reglas claras y abiertas, ayuda a unificar la web y a mantenerla como un espacio libre y colaborativo. Esto no solo facilita el trabajo de los desarrolladores, que pueden aprender y aplicar los estándares con mayor facilidad, sino que también fomenta la innovación. Con una base sólida y compartida, es posible construir herramientas y experiencias nuevas sin tener que empezar desde cero cada vez.

En resumen, la W3C es una pieza clave en el funcionamiento y la evolución de la web. Su trabajo garantiza que internet siga siendo un entorno accesible, interoperable y abierto para todos.

## ¿Qué es un navegador web?

Un navegador web es un software que permite a los usuarios acceder, visualizar e interactuar con páginas y aplicaciones en Internet a través de la Web. Funciona interpretando HTML, CSS y JavaScript, que son los lenguajes principales de la web, para mostrar contenido de manera estructurada y clara.

Cuando un usuario ingresa una dirección web (URL) en la barra de direcciones, el navegador envía una solicitud al servidor correspondiente mediante el protocolo HTTP o HTTPS. El servidor responde enviando archivos que el navegador procesa para mostrar la página en pantalla.

Los navegadores modernos, como Google Chrome, Mozilla Firefox, Microsoft Edge, Safari y Brave, incluyen motores de renderizado como Blink (Chrome), Gecko (Firefox) y WebKit (Safari), que transforman el código en una interfaz visual. También ejecutan JavaScript mediante motores como V8 (Chrome) o SpiderMonkey (Firefox), permitiendo interactividad en las páginas web.

Además, los navegadores ofrecen funciones como pestañas múltiples, almacenamiento en caché, extensiones, navegación privada y compatibilidad con estándares de seguridad.

## Qué ocurre cuando abrimos una página web

Cuando una persona escribe una dirección en la barra del navegador o hace clic en un enlace, se pone en marcha una secuencia técnica que conviene entender desde el comienzo. Primero, el navegador necesita ubicar el servidor al que debe conectarse. Luego solicita recursos, recibe una respuesta y finalmente interpreta el contenido para mostrarlo en pantalla.

En una versión simplificada del proceso, ocurre algo así:

1. La persona escribe una URL o selecciona un enlace.
2. El navegador consulta a qué servidor corresponde ese dominio.
3. El navegador envía una solicitud HTTP o HTTPS.
4. El servidor responde con HTML y, en muchos casos, también con CSS, JavaScript, imágenes u otros recursos.
5. El navegador interpreta esos archivos y construye la página visible.

Esta lógica de solicitud y respuesta aparece todo el tiempo en desarrollo web. Más adelante, cuando se trabajen formularios, fetch o APIs, volverá a aparecer con más detalle.

## URLs, DNS y APIs en una primera aproximación

Una URL es la dirección de un recurso en la Web. Allí suelen aparecer el protocolo, el dominio y la ruta. Por ejemplo, en `https://www.ejemplo.com/productos`, `https` indica el protocolo, `www.ejemplo.com` es el dominio y `/productos` es la ruta solicitada.

Para que el navegador encuentre el servidor correcto, interviene el DNS (Domain Name System), que traduce nombres de dominio legibles para humanos en direcciones IP. Dicho de forma simple: el DNS funciona como una guía que ayuda a ubicar qué equipo debe responder cuando pedimos una dirección web.

También conviene introducir aquí la idea de API. Una API permite que dos sistemas se comuniquen intercambiando datos según reglas definidas. En desarrollo web, muchas interfaces frontend consumen APIs para obtener productos, usuarios, mensajes o resultados de búsqueda sin tener que recargar una página completa.

## Principales lenguajes de la Web

HTML, CSS y JavaScript son los tres principales lenguajes de la Web, ya que permiten estructurar, diseñar e interactuar con las páginas web. Por supuesto, no son los únicos lenguajes involucrados en el desarrollo web, pero sí los únicos que los navegadores pueden interpretar de manera estandarizada.

HTML (HyperText Markup Language) – Es el lenguaje base de la Web, utilizado para estructurar el contenido de las páginas mediante etiquetas. Define elementos como textos, imágenes, enlaces y formularios.

CSS (Cascading Style Sheets) – Se usa para diseñar y estilizar páginas web, permitiendo controlar colores, fuentes, márgenes y disposición de elementos.

JavaScript – Es un lenguaje de programación que permite agregar interactividad y dinamismo a los sitios web. Se usa para validar formularios, crear animaciones y desarrollar aplicaciones web completas.

En 2015 también se introdujo WebAssembly, un formato binario que permite ejecutar código de lenguajes como C, C++ y Rust dentro del navegador con alto rendimiento. Se usa en aplicaciones exigentes como juegos y editores gráficos en línea.

Más allá de los lenguajes, los navegadores también interpretan tecnologías como SVG (gráficos vectoriales), XML y JSON (para el intercambio de datos). También soportan API del navegador como WebGL (gráficos en 3D) y Service Workers (para apps web progresivas).

## Frontend y Backend, dos conceptos complementarios

En el desarrollo web, frontend y backend son dos partes fundamentales que trabajan juntas para hacer que un sitio o aplicación web funcione correctamente.

### **Frontend: La parte visible para el usuario**

El frontend es la interfaz con la que los usuarios interactúan directamente en un navegador web. Se encarga del diseño, la estructura y la interactividad de la página. Para desarrollar el frontend, se usan tres tecnologías principales:

HTML (HyperText Markup Language): Define la estructura y el contenido de la página.

CSS (Cascading Style Sheets): Se usa para dar estilo, colores, fuentes y disposición de elementos.

JavaScript: Permite agregar interactividad y dinamismo, como animaciones, validaciones de formularios y actualizaciones sin recargar la página.

También se usan frameworks y bibliotecas como React, Angular y Vue.js, que facilitan el desarrollo de interfaces modernas y eficientes.

El frontend también interactúa con el backend mediante APIs (Application Programming Interfaces), que permiten obtener o enviar datos a servidores sin necesidad de recargar la página.

### **Backend: La lógica y el procesamiento del servidor**

El backend es la parte del sitio web que los usuarios no ven, pero que maneja toda la lógica, el procesamiento de datos y la comunicación con bases de datos. Su función principal es recibir solicitudes del frontend, procesarlas y devolver una respuesta adecuada.

El backend no se ejecuta dentro del navegador del usuario, sino en servidores. Sin embargo, forma parte del ecosistema web actual porque responde solicitudes, entrega datos y coordina buena parte del comportamiento de las aplicaciones que usamos todos los días.

Los principales componentes del backend son:

Lenguajes de programación: Se usan para procesar la lógica del negocio y manejar solicitudes. Ejemplos: Node.js, Python, PHP, Ruby, Java.

Bases de datos: Almacenan información como usuarios, productos o mensajes. Ejemplos: MySQL, PostgreSQL, MongoDB.

Servidores: Son computadoras que ejecutan aplicaciones backend y responden a las solicitudes de los usuarios. Ejemplos: Apache, Nginx.

APIs y protocolos: El backend se comunica con el frontend a través de APIs REST o GraphQL, usando protocolos como HTTP y WebSockets.

## Distintos enfoques en la programación web

El frontend y el backend trabajan en conjunto para que un sitio web funcione de manera fluida. Simplificando un poco las cosas, el frontend se encarga de la interfaz y la experiencia del usuario, mientras que el backend maneja la lógica, el almacenamiento de datos y la seguridad. 

Dependiendo del tipo de aplicación web, esta interacción puede ocurrir de dos formas principales:

### **Aplicaciones Multi-Página (MPA)**

Las Multi-Page Applications (MPA) son las aplicaciones web tradicionales, donde cada acción del usuario (como hacer clic en un enlace) hace que el navegador cargue una nueva página completa desde el servidor.

Cómo interactúan frontend y backend en una MPA:

1. El usuario solicita una página web ingresando una URL.  
2. El navegador envía una solicitud al servidor backend.  
3. El backend procesa la solicitud, recupera datos de la base de datos y genera una nueva página HTML en el servidor.  
4. El servidor envía la página completa al navegador, que la muestra al usuario.

Cada nueva interacción (como navegar a otra sección) repite este proceso, recargando la página completamente.

Sitios web tradicionales como Wikipedia, portales de noticias suelen usar esta arquitectura, ya que se enfocan más en contenido poco interactivo y dan prioridad al SEO (posicionamiento en buscadores).

### **Aplicaciones de Página Única (SPA)**

Las Single Page Applications (SPA) son aplicaciones web que cargan una única página HTML en la primera solicitud y, a partir de ahí, actualizan dinámicamente el contenido sin necesidad de recargar toda la página cada vez que el usuario interactúa. En lugar de solicitar y renderizar una nueva página completa desde el servidor con cada acción, las SPA utilizan JavaScript para manejar la navegación y actualizar solo las secciones necesarias de la interfaz.

Cómo interactúan frontend y backend en una SPA:

1. El usuario accede a la aplicación y el navegador descarga un único archivo HTML, junto con CSS y JavaScript.  
2. Cuando el usuario interactúa, el frontend envía solicitudes al backend mediante APIs (REST o GraphQL).  
3. El backend responde con datos en formato JSON, y el frontend actualiza la vista sin recargar la página.

Este enfoque mejora significativamente la velocidad y la experiencia del usuario, ya que las interacciones son más rápidas y fluidas, similares a las de una aplicación de escritorio o móvil. En general la mayoría de las aplicaciones web modernas utilizan hoy este enfoque.

### **¿Es mejor MPA o SPA?**

No hay una respuesta absoluta sobre si las MPA (Multi-Page Applications) o las SPA (Single Page Applications) son mejores, ya que depende del tipo de aplicación, los objetivos del proyecto y los recursos disponibles.

Si el proyecto necesita rapidez e interactividad en la navegación, una SPA es mejor. Si el foco es el SEO, contenido poco interactivo y accesibilidad, una MPA es más conveniente. 

En algunos casos se usan enfoques híbridos. Uno de ellos es el Server-Side Rendering (SSR), donde el servidor entrega una primera versión de la página ya renderizada, y luego el navegador incorpora comportamiento dinámico con JavaScript. Para esta materia alcanza con reconocer que existen soluciones intermedias entre una MPA clásica y una SPA. El foco principal del libro estará puesto en los fundamentos del frontend, no en arquitecturas avanzadas de renderizado.

En este libro nos enfocaremos en el desarrollo web clásico, donde se abordarán los tres principales lenguajes mencionados (HTML, CSS y Javascript) sin la incorporación de frameworks ni librerías externos para Javascript, las que se verán en la siguiente edición de la materia "Desarrollo web 2".

## La web como diversidad

Desarrollar para la web implica aceptar una condición central: no se controla por completo ni el entorno técnico ni las capacidades de quienes navegan. Las personas pueden usar distintos navegadores, dispositivos, sistemas operativos, resoluciones de pantalla, velocidades de conexión o tecnologías de asistencia.

Por ese motivo, el desarrollo web no consiste en imponer una única forma correcta de acceso, sino en construir experiencias que funcionen de manera razonable dentro de un ecosistema diverso. Respetar estándares, escribir HTML semántico, usar CSS de forma progresiva y pensar en accesibilidad no son detalles secundarios: son parte del núcleo del trabajo frontend.

Esta idea acompañará todo el libro. A medida que avancemos, no solo se verá cómo construir páginas, sino también cómo hacerlas más robustas, mantenibles y útiles para más personas.

Con este marco ya es posible pasar al primer lenguaje del recorrido. En el próximo capítulo el foco estará puesto en HTML, que es la base estructural sobre la que se apoyan tanto el diseño visual como la interacción posterior.

## Ejercicios del capítulo

### Comprensión

1. Explique con sus palabras cuál es la diferencia entre Internet y la Web.
2. Identifique, en una URL real, el protocolo, el dominio y la ruta.
3. Describa qué papel cumplen el navegador, el servidor y los estándares web dentro de una aplicación web.
4. Elija dos sitios web que use con frecuencia y escriba, en pocas líneas, qué tareas resuelve en cada uno.
5. Explique con sus palabras por qué este libro empieza por HTML y no por JavaScript.

### Aplicación

1. Abra las herramientas de desarrollo del navegador en una página conocida e identifique qué tipos de recursos se descargan al cargarla.
2. Elija una aplicación web que use con frecuencia y clasifique su funcionamiento como más cercano a una MPA, una SPA o un enfoque híbrido. Justifique su respuesta.

### Integración

1. Escriba una breve descripción de la arquitectura general de una aplicación web conocida. Indique qué podría resolverse en el frontend, qué en el backend y qué datos deberían circular entre ambas partes.
