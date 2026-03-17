# Introducción a JavaScript - ECMAScript

Hasta este punto, el recorrido del libro trabajó sobre estructura y presentación. El paso siguiente es incorporar lógica. JavaScript permite procesar datos, tomar decisiones, automatizar comportamientos y, más adelante, responder a acciones del usuario modificando la interfaz. En este capítulo se presenta la base del lenguaje con foco en lectura de código, resolución de problemas simples y construcción de funciones con sentido.

## Objetivos del capítulo

- reconocer los conceptos básicos del lenguaje y su lugar dentro del frontend;
- trabajar con variables, tipos, arrays, objetos, condicionales y funciones simples;
- leer y escribir pequeñas transformaciones de datos con mayor seguridad;
- modelar información del proyecto integrador antes de llevarla al DOM.

## Qué es JavaScript y qué es ECMAScript

JavaScript es el lenguaje de programación que los navegadores entienden de forma nativa. Mientras HTML estructura el contenido y CSS define la presentación visual, JavaScript permite incorporar lógica, cálculos, decisiones e interactividad.

Cuando se habla de ECMAScript, se está nombrando el estándar sobre el que se basa JavaScript. Dicho de forma simple: ECMAScript define reglas y características del lenguaje, y JavaScript es la implementación más conocida de ese estándar. Por eso a veces se usan ambos nombres casi como sinónimos, aunque no son exactamente lo mismo.

En este libro vamos a trabajar con JavaScript moderno, priorizando la sintaxis y las prácticas más habituales hoy: `let`, `const`, funciones claras, arrays, objetos y un uso progresivo del lenguaje. La idea es comprender primero cómo piensa JavaScript antes de llevarlo al DOM o a la interacción con eventos.

## Cómo incorporar JavaScript en HTML

JavaScript puede escribirse dentro del propio documento HTML o en un archivo externo. En proyectos reales conviene usar archivos externos, porque eso facilita el mantenimiento, la organización y la reutilización.

Una forma habitual es esta:

```html
<script src="script.js" defer></script>
```

El atributo `defer` indica que el archivo se descargue mientras se procesa el HTML, pero que su ejecución espere hasta que el documento haya sido interpretado. Para los primeros ejemplos del libro, esa práctica ayuda a evitar errores producidos por intentar usar elementos que todavía no existen en la página.

También puede usarse un script interno:

```html
<script>
  console.log('Hola desde JavaScript');
</script>
```

Aunque esto sirve para pruebas pequeñas, conviene no abusar de esa modalidad cuando el código empieza a crecer.

## Variables y constantes

Las variables permiten guardar información para usarla más adelante. En JavaScript moderno se trabaja principalmente con `let` y `const`.

```js
let precio = 1200;
const IVA = 0.21;
```

La diferencia principal es esta:

- `let` permite reasignar el valor más adelante;
- `const` define una referencia que no debería cambiar.

Por ejemplo:

```js
let stock = 10;
stock = stock - 1;
```

En cambio, una constante suele representar datos estables dentro de un contexto, como una tasa, un nombre de configuración o un selector que no va a cambiar durante la ejecución.

En materiales más antiguos aparece también `var`, pero hoy conviene evitarlo en ejemplos introductorios porque su alcance y su comportamiento suelen generar más confusión que claridad. Para empezar, `let` y `const` son mejores herramientas.

Como criterio práctico, conviene usar `const` por defecto y reservar `let` para los casos en los que el valor realmente vaya a cambiar. Esa decisión vuelve el código más claro y ayuda a detectar mejor dónde hay cambios de estado.

## Tipos de datos básicos

JavaScript es un lenguaje de tipado dinámico. Eso significa que una variable no queda atada de manera rígida a un único tipo. Aun así, hay tipos básicos que es importante reconocer:

- `string`: textos, como `'Harina integral'`;
- `number`: números enteros o decimales, como `12` o `19.99`;
- `boolean`: valores lógicos, `true` o `false`;
- `undefined`: valor que suele aparecer cuando algo todavía no fue definido;
- `null`: valor vacío asignado de forma explícita.

Ejemplos simples:

```js
let producto = 'Yerba';
let precio = 2500;
let disponible = true;
let descripcion;
let descuento = null;
```

Una operación importante para empezar a leer código es `typeof`, que permite consultar el tipo de un valor:

```js
typeof precio; // 'number'
```

Comprender estos tipos ayuda a evitar errores frecuentes, especialmente cuando se comparan valores o se espera un número y se recibe texto.

También conviene recordar que JavaScript puede convertir valores de manera implícita en algunas operaciones. En una etapa inicial, lo más prudente es trabajar con comparaciones estrictas, tipos bien identificados y nombres de variables suficientemente claros.

## Arrays y objetos

Los arrays y los objetos son dos estructuras fundamentales en JavaScript.

Un array es una colección ordenada de valores:

```js
const categorias = ['almacen', 'bebidas', 'limpieza'];
```

Cada elemento tiene una posición, llamada índice, que comienza en `0`.

```js
categorias[0]; // 'almacen'
```

Un objeto, en cambio, organiza información en pares clave-valor:

```js
const producto = {
  nombre: 'Galletitas',
  precio: 1800,
  stock: 12,
  oferta: true
};
```

Aquí no se accede por posición sino por nombre de propiedad:

```js
producto.nombre; // 'Galletitas'
producto.precio; // 1800
```

En desarrollo web es muy común trabajar con arrays de objetos, porque ese formato representa colecciones de datos con bastante naturalidad:

```js
const productos = [
  { nombre: 'Leche', precio: 1500 },
  { nombre: 'Pan', precio: 900 },
  { nombre: 'Cafe', precio: 4300 }
];
```

Ese tipo de estructura va a reaparecer más adelante cuando el libro trabaje con DOM, eventos y datos externos.

Además de guardar datos, en JavaScript es muy común transformarlos. Métodos como `map()`, `filter()` y `find()` permiten trabajar con arrays de manera muy expresiva cuando lo que se necesita es derivar información, filtrar elementos o localizar un caso específico.

Por ejemplo:

```js
const nombres = productos.map((producto) => producto.nombre);
const economicos = productos.filter((producto) => producto.precio <
2000);
const pan = productos.find((producto) => producto.nombre === 'Pan');
```

## Operadores y estructuras de control

JavaScript permite comparar valores y tomar decisiones usando operadores y estructuras de control.

Algunos operadores frecuentes son:

- `===`: igualdad estricta;
- `!==`: desigualdad estricta;
- `>` y `<`: mayor y menor;
- `>=` y `<=`: mayor o igual, menor o igual;
- `&&`: y lógico;
- `||`: o lógico.

La igualdad estricta `===` es preferible a `==` en la mayoría de los casos, porque compara también el tipo del valor y evita conversiones implícitas que pueden resultar confusas.

La estructura condicional más habitual es `if`:

```js
if (producto.stock > 0) {
  console.log('Hay stock disponible');
} else {
  console.log('Producto agotado');
}
```

Para repetir acciones, pueden usarse bucles como `for` o `while`.

Ejemplo con `for`:

```js
for (let indice = 0; indice < productos.length; indice++) {
  console.log(productos[indice].nombre);
}
```

Ejemplo con `while`:

```js
let indice = 0;
while (indice < 3) {
  console.log(indice);
  indice++;
}
```

Estas estructuras permiten recorrer datos, filtrar información o decidir qué camino sigue la ejecución del programa.

## Funciones

Una función es un bloque de código que encapsula una tarea. Puede recibir parámetros, procesar información y devolver un resultado.

Esto permite evitar repeticiones, mejorar la legibilidad y dividir problemas grandes en partes más manejables.

Ejemplo simple:

```js
function calcularPrecioConIVA(precio) {
  return precio * 1.21;
}
```

```js
const precioFinal = calcularPrecioConIVA(1000);
```

Las funciones también pueden validar datos recibidos:

```js
function sumarDosNumeros(num1, num2) {
  if (typeof num1 === 'number' && typeof num2 === 'number') {
    return num1 + num2;
  }
  return undefined;
}
```

Ese patrón muestra algo importante: una función no solo “hace algo”, también expresa una intención y permite concentrar una regla en un solo lugar.

En proyectos más grandes, escribir funciones pequeñas y con nombres claros suele ser una de las formas más efectivas de mantener el código entendible.

## Parámetros por defecto, rest y arrow functions

JavaScript moderno ofrece algunas herramientas muy útiles para escribir funciones con mayor flexibilidad.

Los parámetros por defecto permiten definir un valor inicial cuando no se recibe uno explícito:

```js
function aplicarDescuento(precio, porcentaje = 10) {
  return precio - (precio * porcentaje) / 100;
}
```

Si se llama a `aplicarDescuento(2000)`, el porcentaje será `10`.

El operador `...` en parámetros, conocido como rest, permite reunir una cantidad indefinida de argumentos en un array:

```js
function armarMensaje(...palabras) {
  return palabras.join(' ');
}
```

Por otra parte, las arrow functions son una forma abreviada de escribir funciones:

```js
const duplicar = (numero) => {
  return numero * 2;
}
```

Cuando la función tiene una sola expresión, puede resumirse aún más:

```js
const obtenerNombres = (items) => items.map((item) => item.nombre);
```

No hace falta usar arrow functions en todos lados. Lo importante, en una etapa inicial, es poder reconocerlas y leerlas con naturalidad, porque aparecen mucho en código actual.

## Proyecto guiado: primeras funciones para el supermercado

Antes de trabajar con el DOM, JavaScript puede usarse para modelar y procesar información del proyecto del supermercado. Eso permite practicar lógica sin mezclar todavía manipulación de interfaz.

Por ejemplo, se puede definir una colección de productos:

```js
const productos = [
  { nombre: 'Leche', precio: 1500, stock: 8 },
  { nombre: 'Pan lactal', precio: 2200, stock: 3 },
  { nombre: 'Yerba', precio: 4800, stock: 0 }
];
```

Y luego escribir funciones simples para operar con esos datos:

```js
function obtenerProductosConStock(items) {
  return items.filter((item) => item.stock > 0);
}
```

```js
function obtenerNombres(items) {
  return items.map((item) => item.nombre);
}
```

```js
function calcularTotal(precios) {
  let acumulado = 0;
  for (let indice = 0; indice < precios.length; indice++) {
    acumulado = acumulado + precios[indice];
  }
  return acumulado;
}
```

Con ejercicios así se puede practicar:

- definición de variables y constantes;
- arrays de objetos;
- condicionales;
- recorridos con `for`;
- funciones que devuelven resultados.

La ventaja pedagógica es que el estudiante empieza a pensar en datos y reglas del problema antes de pasar a modificar la página visualmente.

## Validación y recursos recomendados para JavaScript

Al terminar este módulo conviene revisar si los ejemplos y ejercicios cumplen con algunos criterios básicos:

- ¿se distingue claramente cuándo usar `let` y cuándo usar `const`?
- ¿los valores de entrada y salida de cada función están claros?
- ¿los nombres de variables y funciones describen bien su propósito?
- ¿las estructuras de datos elegidas tienen sentido para el problema?
- ¿los condicionales y bucles se usan de forma comprensible?
- ¿las funciones resuelven tareas concretas en lugar de mezclar demasiadas responsabilidades?

En esta etapa también es útil apoyarse en `console.log()` para inspeccionar valores y entender qué está pasando durante la ejecución. Más adelante ese hábito se complementará con herramientas específicas de debugging en el navegador.

Recursos recomendados para profundizar:

- javascript.info: [https://javascript.info/](https://javascript.info/)
- MDN JavaScript Guide: [https://developer.mozilla.org/es/docs/Web/JavaScript/Guide](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide)
- MDN JavaScript Reference: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
- Eloquent JavaScript: [https://eloquentjavascript.net/](https://eloquentjavascript.net/)

Con este capítulo queda presentada la base del lenguaje. A esta altura, ya debería poder leer variables, funciones, condicionales, recorridos y estructuras de datos con mayor criterio, y escribir pequeñas soluciones ligadas a un problema concreto.

El próximo módulo se apoyará sobre estas herramientas para trabajar con el DOM, inspeccionar documentos cargados en el navegador y empezar a depurar problemas de ejecución de manera más sistemática.

## Ejercicios del capítulo

### Comprensión

1. Explique la diferencia entre `let` y `const`, e indique en qué situación elegiría cada una.
2. Describa qué diferencia hay entre un array y un objeto.
3. Explique por qué conviene usar `===` en lugar de `==` en una etapa inicial.

### Aplicación

1. Defina un array de productos del supermercado y escriba una función que devuelva únicamente los nombres de esos productos.
2. Escriba una función que reciba un precio y un porcentaje de descuento, y retorne el valor final usando un parámetro por defecto.

### Integración

1. Modele un carrito de compras sencillo con un array de objetos y escriba funciones para calcular total, listar nombres y filtrar productos disponibles. Registre qué decisiones tomó sobre nombres de variables y estructuras de datos.
