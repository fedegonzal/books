# DOM y debugging

Una vez que JavaScript puede procesar datos, el paso siguiente es conectarlo con la página cargada en el navegador. El DOM es el puente entre el documento HTML y el código que lo modifica. En este capítulo se trabaja esa relación: cómo seleccionar elementos, cómo cambiar contenido, cómo crear nodos y cómo empezar a depurar problemas reales durante la ejecución.

## Objetivos del capítulo

- comprender qué es el DOM y cómo se diferencia del HTML fuente;
- seleccionar, inspeccionar y modificar nodos con métodos frecuentes del navegador;
- crear, insertar y eliminar elementos de forma controlada;
- incorporar primeras prácticas de debugging usando consola e inspector.

## Qué es el DOM

El DOM, sigla de Document Object Model, es la representación que el navegador construye de un documento HTML una vez que la página fue cargada. No es simplemente el archivo fuente tal como fue escrito: es una estructura de objetos que el navegador organiza en memoria para poder interpretarla, mostrarla y permitir su manipulación.

Dicho de otro modo, cuando JavaScript interactúa con una página, no trabaja directamente “sobre el texto del HTML”, sino sobre esa representación del documento. Gracias a eso puede leer contenido, cambiar atributos, agregar clases, crear elementos nuevos o eliminar nodos existentes.

Esta idea es central para el desarrollo frontend. HTML define la estructura inicial, pero el DOM es la estructura activa sobre la que JavaScript puede operar una vez que el navegador ya interpretó el documento.

## Seleccionar elementos del documento

Para trabajar con el DOM primero hay que poder localizar elementos. Existen varios métodos, pero en la práctica conviene dominar sobre todo estos:

- `document.getElementById()`;
- `document.querySelector()`;
- `document.querySelectorAll()`.

Ejemplos:

```js
const titulo = document.getElementById('titulo-principal');
const tarjeta = document.querySelector('.tarjeta-producto');
const botones = document.querySelectorAll('.boton-comprar');
```

La diferencia principal entre ellos es esta:

- `getElementById` busca por un `id` exacto;
- `querySelector` devuelve el primer elemento que coincide con un selector CSS;
- `querySelectorAll` devuelve todos los elementos que coinciden.

En código actual, `querySelector` y `querySelectorAll` suelen resultar especialmente cómodos porque reutilizan la lógica de selectores que ya se conoce desde CSS.

## Leer y modificar contenido, atributos y estilos

Una vez obtenido un elemento, JavaScript puede inspeccionarlo o cambiarlo.

Por ejemplo, si se quiere modificar el texto de un título:

```js
const titulo = document.querySelector('#titulo-principal');
titulo.textContent = 'Ofertas de la semana';
```

`textContent` es una forma clara y segura de reemplazar texto dentro de un elemento.

También pueden leerse o modificarse atributos:

```js
const imagen = document.querySelector('.producto img');
imagen.setAttribute('alt', 'Paquete de arroz integral');
const ruta = imagen.getAttribute('src');
```

Para trabajar con clases CSS, una herramienta especialmente útil es `classList`:

```js
const tarjeta = document.querySelector('.producto');
tarjeta.classList.add('destacado');
tarjeta.classList.remove('agotado');
tarjeta.classList.toggle('seleccionado');
```

También es posible modificar estilos desde JavaScript:

```js
tarjeta.style.borderColor = 'green';
```

Sin embargo, en la mayoría de los casos conviene cambiar clases y dejar que el CSS resuelva la presentación visual. Eso mantiene mejor separadas las responsabilidades del código.

## Crear y eliminar elementos

Manipular el DOM no consiste solo en cambiar lo que ya existe. También se pueden crear elementos nuevos y agregarlos al documento.

Ejemplo:

```js
const lista = document.querySelector('#lista-productos');
const item = document.createElement('li');
item.textContent = 'Azucar';
lista.appendChild(item);
```

En este caso se crea un nuevo `li`, se le asigna contenido y luego se lo inserta dentro de una lista existente.

También puede eliminarse un nodo:

```js
item.remove();
```

Estas operaciones son la base de muchas interfaces dinámicas. Más adelante aparecerán combinadas con eventos y datos, pero ya en este punto conviene entender que el documento no es estático: puede crecer, reorganizarse o simplificarse durante la ejecución.

## Recorrer colecciones del DOM

Cuando `querySelectorAll` devuelve varios elementos, el resultado puede recorrerse para aplicar una misma lógica a todos.

Por ejemplo:

```js
const precios = document.querySelectorAll('.precio');

precios.forEach((elemento) => {
  console.log(elemento.textContent);
});
```

Esto resulta útil para leer información repetida, agregar clases a varios nodos o aplicar transformaciones consistentes.

Al trabajar con colecciones conviene recordar que no se está operando sobre un único elemento sino sobre un conjunto. Muchos errores de principiantes aparecen justamente por intentar usar propiedades de un elemento individual sobre una lista completa.

## Debugging básico en el navegador

Debugging significa inspeccionar y corregir problemas durante la ejecución de un programa. En JavaScript del lado del navegador, eso implica aprender a observar qué valores existen, en qué momento se ejecuta el código y qué errores informa la consola.

La herramienta más inmediata sigue siendo `console.log()`:

```js
console.log(productos);
console.log(titulo);
console.log(precios.length);
```

Usado con criterio, permite verificar si una variable contiene lo que se espera. No resuelve por sí solo todos los problemas, pero ayuda a ubicar dónde empieza a desviarse la ejecución.

Además de la consola, el navegador ofrece herramientas de desarrollo muy valiosas:

- la pestaña Elements o Inspector, para ver el DOM resultante;
- la pestaña Console, para revisar errores y ejecutar pruebas rápidas;
- la pestaña Sources o Debugger, para colocar breakpoints y avanzar paso a paso.

Los breakpoints permiten pausar la ejecución en una línea determinada y examinar el valor real de las variables en ese instante. Ese recurso se vuelve especialmente importante cuando el código deja de ser lineal o cuando varias funciones interactúan entre sí.

## Errores frecuentes al trabajar con DOM

Hay algunos problemas que aparecen muy seguido al empezar:

- intentar seleccionar un elemento que todavía no existe en la página;
- escribir mal un selector;
- olvidar que `querySelectorAll` devuelve una colección y no un único nodo;
- modificar `innerHTML` sin necesidad, mezclando estructura y lógica de forma confusa;
- asumir que una variable tiene contenido sin verificarlo antes.

Un error clásico sería este:

```
const titulo = document.querySelector('#titulo-principal');
titulo.textContent = 'Nuevo titulo';
```

Si ese selector no encuentra nada, `titulo` será `null` y la segunda línea generará un error.

Una alternativa defensiva puede ser:

```
const titulo = document.querySelector('#titulo-principal');
if (titulo) {
  titulo.textContent = 'Nuevo titulo';
}
```

Esto no reemplaza a una buena estructura del programa, pero ayuda a leer mejor qué está ocurriendo y a evitar fallos innecesarios durante la práctica.

## Proyecto guiado: renderizar productos en el supermercado

Este módulo puede aplicarse al proyecto del supermercado sin introducir todavía interacción compleja. La idea es usar un array de productos y reflejar esa información dentro del HTML.

Por ejemplo, se puede partir de una estructura como esta:

```
const productos = [
  { nombre: 'Leche', precio: 1500 },
  { nombre: 'Pan', precio: 900 },
  { nombre: 'Cafe', precio: 4300 }
];
```

Y una lista vacía en HTML:

```
<ul id="lista-productos"></ul>
```

Luego, desde JavaScript:

```
const lista = document.querySelector('#lista-productos');

productos.forEach((producto) => {
  const item = document.createElement('li');
  item.textContent = producto.nombre + ' - $' + producto.precio;
  lista.appendChild(item);
});
```

Este ejercicio permite conectar varias ideas del libro:

- arrays de objetos;
- recorridos con `forEach`;
- selección de nodos del documento;
- creación e inserción de elementos;
- verificación del resultado en el inspector del navegador.

Pedagógicamente es un paso importante, porque el estudiante deja de pensar JavaScript solo como cálculo abstracto y empieza a verlo como una herramienta para transformar la interfaz real.

## Validación y recursos recomendados para DOM y debugging

Al cerrar este módulo conviene revisar algunas preguntas básicas:

- ¿se entiende la diferencia entre HTML fuente y DOM cargado en navegador?
- ¿los selectores usados realmente apuntan a los elementos esperados?
- ¿se distingue cuándo un método devuelve un nodo y cuándo devuelve una colección?
- ¿las modificaciones visuales se resuelven preferentemente con clases y CSS?
- ¿se está usando la consola para comprobar valores reales?
- ¿se probaron las herramientas del navegador más allá de `console.log()`?

Recursos recomendados para profundizar:

- MDN sobre DOM: [https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model](https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model)
- Introducción al DOM en MDN: [https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
- MDN sobre querySelector: [https://developer.mozilla.org/es/docs/Web/API/Document/querySelector](https://developer.mozilla.org/es/docs/Web/API/Document/querySelector)
- MDN sobre classList: [https://developer.mozilla.org/es/docs/Web/API/Element/classList](https://developer.mozilla.org/es/docs/Web/API/Element/classList)
- Guía de Chrome DevTools: [https://developer.chrome.com/docs/devtools/](https://developer.chrome.com/docs/devtools/)
- Depuración de JavaScript con Chrome DevTools: [https://developer.chrome.com/docs/devtools/javascript/](https://developer.chrome.com/docs/devtools/javascript/)

Con este capítulo queda resuelto el paso desde la lógica básica del lenguaje hacia la manipulación del documento. A esta altura, ya debería poder leer el DOM con más criterio, seleccionar nodos, modificar contenido y usar las herramientas del navegador para ubicar errores con mayor precisión.

El próximo módulo se concentrará en la interacción con el usuario, incorporando eventos, formularios, respuestas visuales y comportamientos más dinámicos.

## Ejercicios del capítulo

### Comprensión

1. Explique con sus palabras qué diferencia hay entre el HTML fuente y el DOM que construye el navegador.
2. Describa qué diferencia hay entre `querySelector()` y `querySelectorAll()`.
3. Explique por qué, en general, conviene modificar clases antes que estilos en línea desde JavaScript.

### Aplicación

1. Seleccione un elemento de una página HTML y cambie su texto, una clase y un atributo.
2. Construya una lista vacía en HTML y complétela desde JavaScript creando nodos con `createElement()` y `appendChild()`.

### Integración

1. Renderice en pantalla un array de productos del supermercado dentro de una lista o grilla HTML. Luego verifique el resultado en el inspector del navegador y registre qué problemas encontró al depurar el proceso.
