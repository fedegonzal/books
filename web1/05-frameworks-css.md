# Frameworks CSS (Bootstrap y Tailwind)

Después de trabajar CSS y una primera capa de organización con SASS, es útil conocer herramientas que ofrecen soluciones listas para resolver problemas frecuentes de interfaz. Este capítulo no busca reemplazar el razonamiento sobre CSS, sino mostrar dos enfoques muy extendidos para acelerar el desarrollo: uno más orientado a componentes predefinidos y otro más orientado a utilidades pequeñas y combinables.

## Objetivos del capítulo

- reconocer qué problemas resuelven los frameworks CSS y qué decisiones siguen dependiendo del criterio del desarrollador;
- comparar Bootstrap y Tailwind según filosofía, velocidad de trabajo y mantenimiento;
- identificar contextos en los que conviene usar CSS propio, un framework o una combinación de ambos;
- evaluar el costo pedagógico y técnico de incorporar abstracciones sobre CSS.

## Qué es un framework CSS

Un framework CSS es un conjunto de estilos, convenciones y componentes reutilizables que ayuda a construir interfaces más rápido. En lugar de escribir todo desde cero, el desarrollador trabaja sobre una base predefinida que ya resuelve buena parte del layout, los espaciados, la tipografía, los formularios o ciertos componentes comunes.

Esto no significa que un framework “reemplaza” a CSS. En realidad, sigue siendo CSS, pero organizado de una manera más sistemática y acompañado por clases listas para usar.

Los frameworks pueden aportar varias ventajas:

- aceleran el desarrollo inicial;
- ofrecen consistencia visual;
- reducen la cantidad de CSS personalizado necesario;
- facilitan el armado de prototipos y pantallas funcionales;
- resuelven problemas frecuentes de layout y responsive design.

Sin embargo, también introducen decisiones propias sobre nomenclatura, estructura y forma de trabajo. Por eso conviene estudiarlos después de conocer bien HTML, CSS y una base de organización del código.

En este módulo se trabajará con dos enfoques muy representativos: Bootstrap y Tailwind CSS.

## Bootstrap: incorporación, grilla y componentes

Bootstrap es uno de los frameworks CSS más conocidos y usados. Su propuesta combina una grilla responsive, un conjunto amplio de componentes y muchas clases utilitarias listas para aplicar.

Una forma simple de incorporarlo en un proyecto de práctica es mediante CDN:

```html
<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
...
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

Una de sus herramientas principales es la grilla de 12 columnas. La estructura básica suele componerse con:

- `container` o `container-fluid`;
- `row`;
- `col`, `col-md-6`, `col-lg-4`, etc.

Ejemplo:

```html
<div class="container">
<div class="row g-3">
<div class="col-12 col-md-6 col-lg-4">Producto 1</div>
<div class="col-12 col-md-6 col-lg-4">Producto 2</div>
<div class="col-12 col-md-6 col-lg-4">Producto 3</div>
</div>
</div>
```

Bootstrap también ofrece componentes ya preparados, como botones, tarjetas, formularios, navbars, alerts o modals. Esto permite construir interfaces funcionales con bastante rapidez, especialmente en etapas de prototipado o en proyectos administrativos donde la consistencia pesa más que la originalidad visual.

## Tailwind CSS: utility-first y clases utilitarias

Tailwind CSS representa un enfoque distinto. En lugar de traer componentes completos como punto de partida, ofrece una gran cantidad de clases utilitarias pequeñas y combinables, con las que el diseño se construye directamente en el HTML.

Para una prueba rápida o una instancia de aprendizaje puede incorporarse mediante su CDN de práctica:

```html
<script src="https://cdn.tailwindcss.com"></script>
```

Ese mecanismo es útil para explorar Tailwind en ejercicios breves, pero no representa la forma habitual de trabajo en proyectos más grandes. En contextos reales suele integrarse con tooling específico, algo que excede el alcance de esta materia.

Luego se pueden usar clases como estas:

```html
<button class="bg-green-700 text-white px-4 py-2 rounded-lg shadow">
Guardar
</button>
```

Cada clase expresa una decisión puntual:

- `bg-green-700`: color de fondo;
- `text-white`: color del texto;
- `px-4` y `py-2`: padding horizontal y vertical;
- `rounded-lg`: bordes redondeados;
- `shadow`: sombra.

Este enfoque suele llamarse utility-first porque prioriza el uso de utilidades breves y combinables en vez de crear una clase personalizada para cada componente.

Tailwind ofrece mucha velocidad para construir interfaces, pero también exige acostumbrarse a una forma de lectura distinta, donde buena parte del estilo vive directamente en el HTML.

## Bootstrap vs Tailwind

Aunque ambos son frameworks CSS, no responden exactamente a la misma filosofía.

Bootstrap parte de una idea más tradicional: componentes predefinidos, grilla, clases utilitarias y una estética relativamente reconocible. Ayuda mucho cuando se necesita producir rápido con una base ya establecida.

Tailwind parte de una idea más compositiva: no impone tanto un componente cerrado, sino una caja de herramientas para construir componentes desde cero usando utilidades pequeñas.

Una forma simple de compararlos es esta:

- Bootstrap: más orientado a componentes listos;
- Tailwind: más orientado a composición desde utilidades;
- Bootstrap: curva inicial más amable para proyectos clásicos;
- Tailwind: mayor flexibilidad visual si se adopta bien su lógica;
- Bootstrap: puede dejar una apariencia reconocible si no se personaliza;
- Tailwind: puede volver el HTML más cargado si se usa sin criterio.

Ninguno es “mejor” de forma absoluta. La elección depende del contexto del proyecto, del tiempo disponible, del equipo y del tipo de interfaz que se necesite construir.

## Cuándo conviene usar un framework y cuándo no

Usar un framework CSS puede ser muy conveniente cuando:

- se necesita prototipar rápido;
- el proyecto requiere una interfaz consistente en poco tiempo;
- el equipo necesita una base común;
- la prioridad está en productividad más que en diseño visual completamente original.

En cambio, puede no ser la mejor opción cuando:

- el proyecto es pequeño y el CSS propio ya alcanza;
- se busca un diseño muy específico y artesanal;
- el equipo todavía no comprende bien los fundamentos de CSS;
- el framework termina ocultando decisiones que conviene entender desde la base.

En una materia inicial, lo importante es que el framework no tape el aprendizaje del lenguaje. Por eso tiene sentido estudiarlo después de haber trabajado CSS puro.

En otras palabras, un framework puede ahorrar tiempo, pero no debería reemplazar el criterio técnico. Si una clase funciona y no se entiende por qué, el aprendizaje queda incompleto. Por eso conviene usar estos recursos como apoyo sobre una base ya construida, no como un atajo para evitar comprender CSS.

En el marco de Web 1, el objetivo de este capítulo es reconocer estos enfoques y poder evaluarlos con criterio. Su uso más profundo en combinación con otros lenguajes, librerías o arquitecturas corresponde a etapas posteriores del recorrido.

## Ejemplo comparativo sobre una misma interfaz

Supongamos una tarjeta simple de producto del sistema de supermercado.

En Bootstrap podría escribirse así:

```html
<div class="card shadow-sm">
<img src="galletitas.jpg" class="card-img-top" alt="Paquete de galletitas">
<div class="card-body">
<h5 class="card-title">Galletitas</h5>
<p class="card-text">Paquete de 250 gramos.</p>
<a href="#" class="btn btn-success">Ver más</a>
</div>
</div>
```

En Tailwind, una interfaz parecida podría escribirse así:

```html
<div class="rounded-xl shadow-sm border bg-white overflow-hidden">
<img src="galletitas.jpg" alt="Paquete de galletitas" class="w-full h-48 object-cover">
<div class="p-4">
<h5 class="text-lg font-semibold mb-2">Galletitas</h5>
<p class="text-sm text-gray-600 mb-4">Paquete de 250 gramos.</p>
<a href="#" class="inline-block bg-green-700 text-white px-4 py-2 rounded-lg">Ver más</a>
</div>
</div>
```

Ambos ejemplos resuelven el mismo problema, pero muestran dos formas distintas de pensar la interfaz. Bootstrap se apoya más en nombres de componentes ya definidos. Tailwind se apoya más en decisiones pequeñas que se van componiendo.

## Validación y recursos recomendados para frameworks CSS

Cuando se trabaja con frameworks CSS conviene revisar no solo si las clases “funcionan”, sino también si el resultado sigue siendo claro, mantenible y coherente con la interfaz.

Algunas preguntas útiles son:

- ¿el framework realmente acelera el trabajo en este proyecto?
- ¿las clases utilizadas siguen siendo legibles?
- ¿la interfaz mantiene coherencia visual?
- ¿la accesibilidad sigue cuidada, especialmente en formularios, contraste y foco?
- ¿se está entendiendo qué resuelve el framework y qué sigue dependiendo del criterio del desarrollador?

Recursos recomendados para profundizar:

- Bootstrap: [https://getbootstrap.com/](https://getbootstrap.com/)
- Tailwind CSS: [https://tailwindcss.com/](https://tailwindcss.com/)
- Documentación del grid de Bootstrap: [https://getbootstrap.com/docs/5.3/layout/grid/](https://getbootstrap.com/docs/5.3/layout/grid/)
- Componentes de Bootstrap: [https://getbootstrap.com/docs/5.3/components/](https://getbootstrap.com/docs/5.3/components/)
- Documentación de utility classes en Tailwind: [https://tailwindcss.com/docs/utility-first](https://tailwindcss.com/docs/utility-first)
- Diseño responsive en Tailwind: [https://tailwindcss.com/docs/responsive-design](https://tailwindcss.com/docs/responsive-design)
- Estados interactivos en Tailwind: [https://tailwindcss.com/docs/hover-focus-and-other-states](https://tailwindcss.com/docs/hover-focus-and-other-states)

Con esto queda cubierto un primer panorama de frameworks CSS. A esta altura, ya debería poder reconocer qué problemas resuelve un framework, qué costo introduce y por qué la elección entre Bootstrap y Tailwind depende más del contexto que de una preferencia abstracta.

El siguiente módulo retomará dos temas que ya aparecieron transversalmente a lo largo del libro y los trabajará de forma específica: accesibilidad y responsive design.

## Ejercicios del capítulo

### Comprensión

1. Explique con sus palabras cuál es la diferencia entre un framework orientado a componentes y un enfoque utility-first.
2. Describa una ventaja y una desventaja de Bootstrap.
3. Describa una ventaja y una desventaja de Tailwind CSS.

### Aplicación

1. Construya una tarjeta simple de producto con Bootstrap usando grilla, imagen, texto y botón.
2. Reproduzca esa misma interfaz con Tailwind CSS e identifique qué diferencias de trabajo encontró entre ambos enfoques.

### Integración

1. Elija una pantalla del proyecto del supermercado y justifique qué enfoque sería más conveniente para desarrollarla: CSS propio, Bootstrap o Tailwind. Argumente su respuesta en términos de tiempo, claridad, mantenimiento y control visual.
