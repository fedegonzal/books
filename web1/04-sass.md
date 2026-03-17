# Preprocesadores para CSS (SASS)

Cuando un proyecto crece, escribir CSS plano sigue siendo posible, pero no siempre resulta cómodo ni sostenible. Los preprocesadores aparecen para ordenar mejor la hoja de estilos, evitar repeticiones y escalar el trabajo sin perder legibilidad. En este capítulo se presenta SASS como una herramienta complementaria, no como un reemplazo de los fundamentos de CSS.

## Objetivos del capítulo

- comprender qué problemas de organización resuelve SASS sobre una base previa de CSS;
- usar variables, nesting, partials y mixins en ejemplos simples;
- reconocer el flujo entre archivos fuente `.scss`, compilación y CSS final;
- evaluar cuándo SASS aporta orden real y cuándo solo agrega complejidad innecesaria.

## Qué problema resuelve SASS

A medida que un proyecto crece, también crecen sus hojas de estilo. Empiezan a repetirse colores, tamaños, familias tipográficas, sombras, espaciados y bloques enteros de reglas. CSS permite resolver muchas de estas situaciones, pero cuando el proyecto gana complejidad, el mantenimiento puede volverse lento y propenso a errores.

SASS surge justamente para ayudar en ese escenario. Es un preprocesador de CSS: una herramienta que agrega capacidades extra para escribir estilos de una forma más organizada y luego convertir ese código en CSS estándar, que es lo que finalmente entiende el navegador.

Esto significa que el navegador no interpreta SASS directamente. Lo que se hace es escribir archivos `.scss` o `.sass`, y después compilarlos para obtener archivos `.css` normales.

Entre las ventajas principales de SASS se encuentran:

- reutilizar valores con variables;
- agrupar mejor reglas relacionadas;
- crear fragmentos reutilizables con mixins;
- dividir el código en varios archivos sin perder organización;
- facilitar el mantenimiento del proyecto cuando crece.

SASS no reemplaza los fundamentos de CSS. Si la base de CSS está desordenada, SASS no la arregla por sí solo. Su valor aparece cuando ya se entiende bien CSS y se necesita escribirlo de forma más escalable.

En una Web 1 conviene pensarlo como una herramienta de organización posible, no como un paso obligatorio después de aprender CSS. De hecho, CSS moderno ya resuelve parte de estos problemas con variables nativas, mejores estrategias de layout y otras capacidades del lenguaje. Aun así, SASS sigue siendo útil para introducir la idea de preprocesamiento, organización modular y reutilización de estilos.

## Sintaxis básica y flujo de trabajo

En la práctica actual, la sintaxis más común es SCSS. Se parece mucho a CSS tradicional, pero permite sumar herramientas extra como variables, nesting y mixins.

Existe también una sintaxis `.sass`, más compacta y basada en indentación, pero en este libro se trabajará con `.scss` porque resulta más cercana a CSS y suele ser más amigable para estudiantes que todavía están consolidando la lectura del lenguaje base.

Por ejemplo, este fragmento sigue siendo muy parecido a CSS:

```scss
$color-principal: #2f6b2f;

.boton {
background-color: $color-principal;
color: white;
}
```

Para usar SASS es necesario convertir el archivo fuente en un archivo CSS final. Esto puede hacerse de varias maneras:

- mediante línea de comandos;
- mediante una extensión o integración en el editor;
- mediante herramientas de build del proyecto.

En esta materia alcanza con comprender la lógica del proceso y, si se desea practicar, usar una variante simple de compilación asistida por editor o línea de comandos. La configuración profunda de tooling no es el objetivo central de Web 1.

En un flujo simple de aprendizaje, alcanza con compilar un archivo `estilos.scss` hacia un archivo `estilos.css` y luego enlazar ese CSS desde el HTML como siempre.

Lo importante es entender el recorrido:

```text
estilos.scss -> compilacion -> estilos.css -> navegador
```

Es importante no perder de vista esta secuencia: el navegador nunca interpreta directamente SASS. Lo que finalmente llega al navegador es siempre CSS compilado. Por eso conviene revisar tanto el archivo fuente `.scss` como el resultado que se genera después de la compilación.

## Variables

Las variables son uno de los usos más claros de SASS. Permiten guardar valores que se repiten muchas veces, como colores, tamaños o tipografías.

Ejemplo:

```scss
$color-primario: #2f6b2f;
$color-secundario: #f7f4ea;
$radio-base: 8px;
```

```scss
.tarjeta {
background-color: $color-secundario;
border: 1px solid $color-primario;
border-radius: $radio-base;
}
```

La gran ventaja es que, si el proyecto cambia de paleta o de escala visual, alcanza con modificar el valor de la variable en un solo lugar.

En proyectos como el sistema de supermercado, esto resulta muy útil para unificar colores de botones, tarjetas, encabezados y tablas.

## Nesting

El nesting permite anidar reglas de forma más cercana a la estructura lógica de los componentes. Esto puede hacer que el código sea más fácil de leer, siempre que se use con moderación.

Ejemplo:

```scss
.producto {
padding: 1rem;
border: 1px solid #ddd;

  h2 {
    margin-bottom: 0.5rem;
  }

  p {
    color: #555;
  }
}
```

Al compilarse, esto se transforma en selectores CSS completos para `.producto h2` y `.producto p`.

El nesting es cómodo, pero conviene no exagerarlo. Si la anidación se vuelve muy profunda, el código pierde claridad y los selectores resultantes pueden volverse demasiado específicos.

Como criterio práctico para una materia inicial, conviene mantener anidaciones cortas. Si una regla necesita demasiados niveles para entenderse, probablemente sea una señal de que la estructura puede escribirse de una manera más clara.

## Partials y organización de archivos

Cuando una hoja de estilos empieza a crecer, conviene dividirla. En SASS esto suele hacerse mediante partials: archivos parciales que ayudan a separar responsabilidades.

Por ejemplo, una estructura simple podría ser:

- `_variables.scss`
- `_base.scss`
- `_layout.scss`
- `_components.scss`
- `main.scss`

Los archivos parciales suelen comenzar con guion bajo porque no están pensados para compilarse de forma independiente. Su contenido se centraliza luego desde un archivo principal.

En la sintaxis moderna de SASS se recomienda usar `@use` para importar módulos:

```scss
@use 'variables';
@use 'components';
```

Esto ayuda a mantener una organización más clara que la vieja estrategia basada en `@import`.

## Mixins

Los mixins permiten definir bloques reutilizables de reglas CSS, incluso con parámetros. Son especialmente útiles cuando se repiten patrones más complejos que una sola línea de estilo.

Ejemplo:

```scss
@mixin boton-base($fondo, $texto) {
background-color: $fondo;
color: $texto;
padding: 0.75rem 1rem;
border: none;
border-radius: 8px;
}
```

```scss
.boton-primario {
@include boton-base(#2f6b2f, white);
}
```

```scss
.boton-secundario {
@include boton-base(#d9d3c3, #222);
}
```

En la cursada, una aplicación muy útil de mixins es generar degradados o centralizar estilos repetidos de tipografía, botones o tarjetas.

## Proyecto guiado: refactor del integrador con SASS

Una buena forma de introducir SASS no es empezar un proyecto nuevo, sino tomar el integrador ya trabajado con HTML y CSS y reorganizarlo.

Una secuencia razonable para el sistema de supermercado podría ser esta:

- definir dos colores base de la interfaz, por ejemplo uno primario y otro secundario;
- extraer esos valores a variables;
- crear un mixin para degradados de header y footer;
- separar estilos generales, layout y componentes en archivos parciales;
- reutilizar mixins en botones, tarjetas y bloques repetidos.

Por ejemplo, si el sitio ya tiene una portada con header, cuerpo y footer, SASS puede ayudar a que esas secciones compartan reglas consistentes sin duplicar código.

El objetivo no es complicar el proyecto, sino mostrar que SASS se vuelve útil cuando el CSS empieza a repetirse y hace falta mantener más orden.

## Validación y recursos recomendados para SASS

Al trabajar con SASS conviene revisar dos cosas distintas: la calidad del código fuente `.scss` y el CSS compilado que finalmente recibirá el navegador.

Algunas preguntas útiles para revisar el propio trabajo son:

- ¿las variables realmente reducen repetición?
- ¿los mixins encapsulan patrones útiles o solo agregan complejidad?
- ¿la anidación sigue siendo legible?
- ¿la división en archivos mejora la organización del proyecto?
- ¿el CSS compilado sigue siendo claro y razonable?

Recursos recomendados para profundizar:

- Sitio oficial de Sass: [https://sass-lang.com/](https://sass-lang.com/)
- Documentación de `@use`: [https://sass-lang.com/documentation/at-rules/use/](https://sass-lang.com/documentation/at-rules/use/)
- Sass Guidelines: [https://sass-guidelin.es/](https://sass-guidelin.es/)
- Guía general de Sass en MDN: [https://developer.mozilla.org/en-US/docs/Glossary/Sass](https://developer.mozilla.org/en-US/docs/Glossary/Sass)

Con esto queda presentado el primer nivel de herramientas que permiten escalar mejor una hoja de estilos. A esta altura, ya debería poder reconocer cuándo un CSS empieza a volverse repetitivo y cómo SASS puede ayudar a reorganizarlo sin ocultar los fundamentos del lenguaje.

El próximo paso será estudiar frameworks CSS, que ofrecen componentes y convenciones listas para acelerar el desarrollo.

## Ejercicios del capítulo

### Comprensión

1. Explique cuál es la diferencia entre CSS y SASS, y por qué el navegador no interpreta directamente archivos `.scss`.
2. Describa para qué sirven variables, partials y mixins dentro de un proyecto de estilos.
3. Explique por qué el nesting puede ser útil, pero también problemático si se usa sin criterio.

### Aplicación

1. Convierta una hoja de estilos simple a SCSS extrayendo al menos tres variables y un mixin reutilizable.
2. Reorganice un pequeño conjunto de estilos en partials separados por responsabilidad, por ejemplo variables, layout y componentes.

### Integración

1. Tome una parte del proyecto del supermercado ya estilizada en CSS y refactorícela con SASS. Documente qué valores extrajo a variables, qué patrones convirtió en mixins y qué mejoras obtuvo en legibilidad u organización.
