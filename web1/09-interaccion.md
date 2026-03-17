# Interacción con el usuario

El capítulo anterior mostró cómo leer y modificar el documento. Ahora el problema cambia: ya no alcanza con alterar el DOM de forma estática, hace falta responder a acciones reales. En esta etapa se incorporan eventos, validación de formularios, feedback visual, asincronía y generación dinámica de contenido como parte del comportamiento cotidiano de una interfaz.

## Objetivos del capítulo

- comprender cómo se modela la interacción con eventos y respuestas visuales en una interfaz web;
- usar `addEventListener`, `event.target` y `preventDefault()` en casos frecuentes;
- validar formularios y comunicar estados de interfaz con mayor claridad;
- integrar eventos, DOM y asincronía en mejoras concretas del proyecto del supermercado.

## Qué significa interactuar en una interfaz web

Una interfaz deja de ser solamente informativa cuando empieza a reaccionar a lo que hace una persona usuaria. Esa reacción puede ser muy simple, como mostrar un mensaje al hacer click, o más compleja, como validar un formulario, filtrar productos, cargar datos externos o actualizar una sección sin recargar toda la página.

En desarrollo frontend, la interacción con el usuario se construye combinando varias piezas: HTML para ofrecer controles, CSS para expresar estados visuales y JavaScript para escuchar acciones, procesarlas y responder de manera coherente.

Este módulo se apoya en todo lo visto antes. El lenguaje ya fue presentado, el DOM ya puede leerse y modificarse; ahora el paso siguiente es responder a acciones reales del usuario y construir comportamientos más dinámicos.

## Eventos del navegador

Un evento es algo que ocurre en la interfaz o en el navegador y que puede ser detectado por JavaScript. Muchos de esos eventos están ligados directamente a acciones del usuario.

Algunos de los más habituales son:

- `click`, cuando se activa un botón o un enlace;
- `input`, cuando cambia el valor de un campo mientras se escribe;
- `change`, cuando un control cambia su valor y confirma ese cambio;
- `submit`, cuando se intenta enviar un formulario;
- `keydown` o `keyup`, cuando se presiona o suelta una tecla.

Pensar en eventos ayuda a dejar atrás una lógica puramente lineal. El código ya no se ejecuta solo de arriba hacia abajo, sino que también espera acciones y responde cuando algo sucede.

## Escuchar eventos con addEventListener

La forma más clara y flexible de trabajar con eventos es `addEventListener()`.

Por ejemplo:

```js
const boton = document.querySelector('#boton-oferta');

boton.addEventListener('click', () => {
  console.log('Se hizo click en el boton');
});
```

Con este patrón se selecciona un elemento y luego se asocia una función que se ejecutará cuando ocurra el evento indicado.

También puede usarse una función con nombre:

```js
function mostrarMensaje() {
  console.log('Accion ejecutada');
}
```

```js
boton.addEventListener('click', mostrarMensaje);
```

En general, esta estrategia es preferible a usar atributos HTML como `onclick`, porque mantiene mejor separadas la estructura y la lógica del comportamiento.

## El objeto event y preventDefault

Cuando ocurre un evento, JavaScript puede recibir un objeto con información sobre lo sucedido. Ese objeto suele llamarse `event` o simplemente `e`.

Ejemplo:

```js
const campo = document.querySelector('#busqueda');

campo.addEventListener('input', (event) => {
  console.log(event.target.value);
});
```

Aquí `event.target` refiere al elemento que disparó el evento. En formularios y entradas de texto, esa propiedad resulta especialmente útil para leer el valor actual.

Otro método fundamental es `preventDefault()`, que sirve para impedir el comportamiento automático del navegador cuando hace falta controlarlo con JavaScript.

Por ejemplo, al enviar un formulario:

```js
const formulario = document.querySelector('#form-producto');

formulario.addEventListener('submit', (event) => {
  event.preventDefault();
  console.log('Formulario interceptado por JavaScript');
});
```

Sin esa línea, el navegador intentaría enviar el formulario y probablemente recargaría la página. Con `preventDefault()`, el programa puede validar, procesar o mostrar mensajes antes de decidir qué hacer.

## Interacción en formularios

Los formularios son uno de los espacios más frecuentes de interacción. Allí JavaScript puede validar datos, completar mensajes de ayuda, mostrar errores o preparar información antes del envío.

Antes de sumar lógica con JavaScript, conviene recordar que HTML ya ofrece validaciones nativas con atributos como `required`, `min`, `max`, `minlength`, `maxlength` o tipos específicos como `email`. JavaScript suele complementar esa base cuando hace falta una respuesta más personalizada o una regla de negocio más específica.

Un ejemplo sencillo sería verificar que un campo no esté vacío:

```js
const formulario = document.querySelector('#form-producto');
const nombreInput = document.querySelector('#nombre-producto');
const mensaje = document.querySelector('#mensaje-formulario');
```

```js
formulario.addEventListener('submit', (event) => {
  event.preventDefault();

  if (nombreInput.value.trim() === '') {
    mensaje.textContent = 'El nombre del producto es obligatorio';
    return;
  }

  mensaje.textContent = 'Formulario listo para enviarse';
});
```

Además del evento `submit`, suele ser útil trabajar con `input` o `change` para responder mientras el usuario escribe, selecciona o activa opciones.

La validación visual debe seguir siendo clara y accesible: no conviene depender solo del color, y los mensajes deberían poder entenderse sin ambigüedad.

## Feedback visual y estados de interfaz

Interacción no significa solo capturar acciones. También significa devolver señales claras. Si un usuario presiona un botón, completa un campo o dispara una búsqueda, la interfaz debería mostrar de alguna manera qué está ocurriendo.

Ese feedback puede tomar distintas formas:

- mensajes de éxito o error;
- clases visuales como `activo`, `error`, `cargando` o `oculto`;
- deshabilitar temporalmente un botón durante una operación;
- mostrar resultados parciales a medida que el usuario escribe.

Ejemplo:

```js
const boton = document.querySelector('#guardar');

boton.addEventListener('click', () => {
  boton.classList.add('cargando');
  boton.textContent = 'Guardando...';
});
```

Este tipo de gesto mejora la comprensión de la interfaz porque evita que la acción quede “silenciosa”. En experiencias reales, una parte importante de la calidad percibida depende justamente de estas respuestas intermedias.

## Fetch como interacción asincrónica

No toda interacción se resuelve con datos ya presentes en la página. Muchas veces una acción del usuario requiere consultar un recurso externo, como una API o un archivo JSON. Para eso JavaScript ofrece `fetch()`.

Ejemplo básico:

```js
fetch('https://apis.datos.gob.ar/georef/api/provincias')
  .then((response) => {
    if (!response.ok) {
      throw new Error('No se pudo obtener la informacion');
    }

    return response.json();
  })
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

Esto introduce una idea clave: hay respuestas que llegan más tarde. El programa hace una solicitud y continúa; cuando los datos llegan, recién entonces ejecuta la lógica asociada.

En una interfaz, esto puede usarse para autocompletar, cargar listados, filtrar recursos, mostrar resultados remotos o enriquecer formularios sin recargar toda la página.

Aunque `fetch` no siempre implica una acción visible del usuario en sí misma, en muchos casos forma parte del circuito de interacción: el usuario solicita algo y la interfaz responde trayendo información nueva.

Cuando se trabaja con `fetch`, también conviene pensar qué va a pasar si la respuesta tarda, falla o devuelve un resultado inesperado. En una interfaz real, estados como `cargando`, `error` o `sin resultados` son parte del diseño de interacción, no simples detalles técnicos.

En JavaScript moderno también es frecuente resolver este mismo problema con `async/await`. En este libro no será un tema central, pero conviene reconocer que existe como otra forma de escribir lógica asincrónica sobre promesas.

## Template strings para respuestas dinámicas

Cuando una interacción genera contenido nuevo, las template strings ayudan a construir texto o fragmentos HTML de manera más legible.

Por ejemplo:

```js
function plantillaProducto(producto) {
  return `
    <article class="producto">
      <h3>${producto.nombre}</h3>
      <p>Precio: $${producto.precio}</p>
    </article>
  `;
}
```

Con esa técnica se pueden generar tarjetas, filas de tabla, mensajes o pequeños bloques reutilizables a partir de datos variables.

Esto conecta muy bien con `fetch`, porque permite transformar datos recibidos desde una API o desde un archivo local en contenido visible dentro de la interfaz.

En esta etapa conviene mantener el criterio: las templates son útiles cuando simplifican la lectura del código, no cuando convierten cada interacción en una cadena larga y difícil de mantener.

## Proyecto guiado: búsqueda y carga interactiva en el supermercado

Para cerrar el libro, este módulo puede aplicarse al proyecto del supermercado de dos maneras complementarias.

La primera es agregar una búsqueda simple sobre el listado de productos:

```js
const inputBusqueda = document.querySelector('#busqueda');
const items = document.querySelectorAll('.producto');

inputBusqueda.addEventListener('input', (event) => {
  const texto = event.target.value.toLowerCase();

  items.forEach((item) => {
    const nombre = item.textContent.toLowerCase();
    item.classList.toggle('oculto', !nombre.includes(texto));
  });
});
```

La segunda es interceptar el formulario de carga para validar campos y mostrar una confirmación en pantalla antes de cualquier envío real:

```js
const formulario = document.querySelector('#form-producto');
const estado = document.querySelector('#estado-envio');

formulario.addEventListener('submit', (event) => {
  event.preventDefault();
  estado.textContent = 'Producto cargado correctamente';
});
```

Si se quisiera dar un paso más, también podría consultarse una API o un archivo local para completar listados dinámicos y luego renderizarlos con templates. Eso no es obligatorio para comprender la materia, pero muestra hacia dónde evoluciona naturalmente el trabajo frontend.

## Validación y recursos recomendados para interacción con el usuario

Antes de cerrar este módulo conviene revisar:

- ¿los eventos están asociados a los elementos correctos?
- ¿se entiende qué papel cumple `event.target`?
- ¿se usa `preventDefault()` cuando realmente hace falta?
- ¿los formularios muestran mensajes claros al usuario?
- ¿las respuestas visuales expresan estados como error, carga o éxito?
- ¿se comprende la idea de asincronía cuando se usa `fetch()`?
- ¿las templates mejoran la legibilidad en lugar de complicarla?

Recursos recomendados:

- MDN sobre eventos: [https://developer.mozilla.org/es/docs/Learn/JavaScript/Building_blocks/Events](https://developer.mozilla.org/es/docs/Learn/JavaScript/Building_blocks/Events)
- Referencia de eventos en MDN: [https://developer.mozilla.org/en-US/docs/Web/Events](https://developer.mozilla.org/en-US/docs/Web/Events)
- MDN sobre validación de formularios: [https://developer.mozilla.org/es/docs/Learn/Forms/Form_validation](https://developer.mozilla.org/es/docs/Learn/Forms/Form_validation)
- Constraint validation en HTML: [https://developer.mozilla.org/en-US/docs/Web/HTML/Constraint_validation](https://developer.mozilla.org/en-US/docs/Web/HTML/Constraint_validation)
- MDN sobre Fetch API: [https://developer.mozilla.org/es/docs/Web/API/Fetch_API](https://developer.mozilla.org/es/docs/Web/API/Fetch_API)

Con este capítulo queda cerrada la secuencia principal del libro sobre fundamentos de desarrollo web frontend. A esta altura, ya debería poder reconocer cómo se conectan los tres lenguajes principales de la web: HTML ofrece estructura, CSS comunica estados visuales y JavaScript responde a acciones, modifica la interfaz y procesa información.

A partir de aquí, una siguiente etapa natural sería profundizar en consumo de APIs, almacenamiento local, componentes reutilizables o frameworks de JavaScript, pero esa ya es una expansión propia de un curso posterior.

## Ejercicios del capítulo

### Comprensión

1. Explique qué es un evento y por qué `addEventListener()` suele ser preferible a `onclick`.
2. Describa para qué sirve `event.target` y en qué casos resulta útil.
3. Explique con sus palabras qué problema resuelve `preventDefault()` en formularios u otras interacciones.

### Aplicación

1. Implemente un botón que, al hacer click, cambie su texto y agregue o quite una clase visual.
2. Construya una validación simple de formulario que muestre un mensaje claro si un campo obligatorio quedó vacío.

### Integración

1. Implemente una búsqueda en tiempo real sobre una lista de productos del supermercado y sume una confirmación visual al enviar un formulario de carga. Si usa datos remotos o locales con `fetch`, registre también qué estado mostraría mientras la información está cargando.
