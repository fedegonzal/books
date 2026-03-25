# Vectorización y broadcasting

En el estudio de sistemas paralelos conviene prestar atención a estrategias que no siempre se presentan como paralelismo explícito, pero que producen mejoras significativas de rendimiento. La vectorización y el broadcasting forman parte de ese conjunto de técnicas, especialmente en entornos de cálculo numérico y procesamiento de datos con arreglos.

## Objetivos del capítulo

- definir vectorización y broadcasting en un nivel introductorio;
- relacionar estas técnicas con SIMD y con bibliotecas como NumPy;
- mostrar por qué resultan importantes en procesamiento de imágenes, datos e inteligencia artificial;
- comparar estas estrategias con bucles explícitos y con formas más tradicionales de paralelización.

## Por qué este capítulo importa

Después de estudiar hilos, procesos y bibliotecas de paralelización en Python, conviene introducir una idea clave: no toda mejora de rendimiento proviene de repartir trabajo entre workers visibles. En muchos problemas numéricos, el cambio decisivo consiste en dejar de pensar el cálculo como una secuencia de iteraciones explícitas y pasar a expresarlo como una operación sobre estructuras completas de datos.

Este cambio de formulación tiene consecuencias importantes. Reduce la sobrecarga del intérprete, aprovecha bibliotecas implementadas en bajo nivel y permite explotar capacidades del hardware que el programador no siempre controla directamente, como SIMD o ciertas optimizaciones de memoria.

## Qué es la vectorización

La vectorización consiste en aplicar operaciones sobre estructuras completas de datos, como vectores o matrices, en lugar de recorrer elemento por elemento mediante bucles explícitos en Python. Esta estrategia suele apoyarse en implementaciones optimizadas de bajo nivel y en capacidades del hardware asociadas a SIMD, es decir, la ejecución de una misma instrucción sobre múltiples datos.

El material de cátedra presenta ejemplos sencillos de suma de vectores para mostrar la diferencia entre una implementación secuencial con bucles y una versión vectorial basada en NumPy.

En términos prácticos, vectorizar significa reemplazar una lógica del tipo "para cada elemento, hacer una operación" por una expresión que opera sobre todo el arreglo de una vez. La operación conceptual puede ser la misma, pero el costo de ejecución cambia porque ya no se depende del intérprete de Python para administrar cada iteración individual.

Una comparación mínima permite verlo con claridad:

```python
result = []
for i in range(len(a)):
	result.append(a[i] + b[i])
```

Frente a una formulación vectorizada:

```python
import numpy as np

result = np.array(a) + np.array(b)
```

La segunda versión no es solo más breve. También suele ser más eficiente porque delega el cálculo a una implementación optimizada.

## SIMD como fundamento

SIMD, sigla de Single Instruction, Multiple Data, permite que una misma operación actúe simultáneamente sobre varios elementos. Esta idea resulta especialmente adecuada para tareas repetitivas sobre grandes conjuntos de datos, como procesamiento de imágenes, audio, video, simulaciones físicas y entrenamiento de modelos de inteligencia artificial.

Conviene notar que SIMD no es lo mismo que vectorización, aunque ambas ideas están muy relacionadas. SIMD es una capacidad de hardware o de bajo nivel. La vectorización es una forma de expresar el cálculo de modo tal que ese hardware pueda aprovecharse. Dicho de otro modo, la vectorización suele ser la puerta de entrada de alto nivel a comportamientos cercanos a SIMD.

Por ese motivo, este capítulo funciona como puente entre dos escalas: la del código Python que escribe quien programa y la del hardware que ejecuta muchas operaciones sobre datos contiguos.

## Qué es el broadcasting

El broadcasting es un conjunto de reglas que permite combinar arreglos de distinto tamaño cuando sus dimensiones son compatibles según ciertos criterios. En lugar de expandir manualmente los datos o escribir bucles adicionales, la biblioteca aplica la operación como si ciertos valores se difundieran sobre la estructura mayor.

El programa muestra ejemplos de suma entre vectores y escalares, y también de operaciones mixtas entre más de una estructura de datos.

Un caso elemental es sumar un escalar a todos los elementos de un vector:

```python
import numpy as np

values = np.array([1, 2, 3])
result = values + 5
```

Aquí el valor `5` actúa como si se replicara sobre todas las posiciones del arreglo, aunque esa expansión no se escriba manualmente. El interés del broadcasting está justamente en evitar código adicional y permitir expresiones compactas sobre estructuras compatibles.

También puede aparecer en operaciones entre matrices y vectores, por ejemplo cuando se desea sumar un vector fila a todas las filas de una matriz. Este patrón es muy frecuente en procesamiento de imágenes, normalización de datos y cálculo científico.

## Relación entre ambas ideas

Vectorización y broadcasting suelen aparecer juntas. La primera se refiere a operar sobre arreglos completos; la segunda, a compatibilizar dimensiones para que esa operación sea posible sin trabajo manual adicional. Aunque se las confunda con frecuencia, conviene distinguirlas porque resuelven problemas diferentes.

La vectorización responde a la pregunta "cómo evitar iterar elemento por elemento desde Python". El broadcasting responde a la pregunta "cómo combinar estructuras de distinta forma sin escribir lógica adicional para expandirlas". En muchos programas ambas ideas aparecen al mismo tiempo, pero no cumplen exactamente la misma función.

## Comparación con bucles explícitos

Desde el punto de vista didáctico, conviene comparar tres opciones frente a un mismo problema numérico sencillo:

- un bucle explícito en Python;
- una estrategia de paralelización explícita con hilos o procesos;
- una formulación vectorizada con NumPy.

El punto importante es que la tercera opción muchas veces gana sin necesidad de lanzar workers visibles. Esto ocurre porque el costo de iterar en Python suele ser alto, mientras que una operación vectorizada delega el trabajo a rutinas optimizadas que recorren memoria de forma más eficiente.

Por ese motivo, en problemas de arreglos regulares conviene evaluar primero la vectorización antes de introducir coordinación entre procesos o hilos. Esa recomendación no elimina el valor del paralelismo explícito, pero sí ayuda a elegir el primer enfoque razonable.

## Relación con el ancho de banda de memoria

La mejora de rendimiento asociada con vectorización no depende solo de hacer varias operaciones a la vez. También influye el modo en que los datos se organizan y se recorren en memoria. Cuando un arreglo está dispuesto de forma contigua y la operación recorre los datos con regularidad, el hardware puede aprovechar mejor la jerarquía de caché y reducir accesos costosos a memoria principal.

Aquí vuelve a aparecer una idea del capítulo 07, Arquitectura y métricas: muchas tareas con arreglos grandes están limitadas por memoria más que por cálculo puro. En esos casos, escribir el problema de forma vectorizada puede mejorar tanto la expresión del cálculo como el patrón de acceso a memoria.

Esto explica por qué una implementación vectorizada puede superar a otra más "paralela" en apariencia. Si la segunda introduce overhead de coordinación o recorre peor los datos, la ventaja de tener más workers puede evaporarse rápidamente.

## Importancia práctica

Estas técnicas son centrales en dispositivos y plataformas actuales. El material menciona explícitamente procesadores Intel, AMD y ARM, además de su relevancia en computación móvil. En el contexto de la materia, su estudio funciona como puente entre paralelismo de CPU, procesamiento numérico eficiente y preparación para el trabajo con GPU.

También son especialmente importantes en inteligencia artificial y procesamiento de imágenes, donde gran parte del trabajo consiste en aplicar transformaciones repetitivas sobre tensores, matrices o arreglos multidimensionales. En ese tipo de problemas, vectorización y broadcasting no son una optimización menor, sino una forma natural de expresar el cálculo.

## Criterios para el análisis práctico

Para estudiar estas técnicas con mayor profundidad conviene comparar implementaciones con bucles explícitos frente a versiones vectorizadas, observar cómo cambian las dimensiones de los arreglos en operaciones con broadcasting y relacionar esas transformaciones con los tiempos de ejecución obtenidos.

En particular, conviene revisar al menos estas preguntas:

- ¿la operación puede escribirse sobre arreglos completos o depende de lógica muy irregular?;
- ¿los datos tienen una forma compatible con broadcasting o requieren reestructuración previa?;
- ¿la ganancia observada proviene de menos iteraciones en Python, de mejor acceso a memoria o de ambas cosas?;
- ¿una versión paralela explícita aporta algo adicional o introduce más overhead que beneficio?

Un ejemplo algo más cercano a usos reales aparece al normalizar columnas de una matriz. Si se quiere restar a cada columna su media, puede escribirse:

```python
import numpy as np

matrix = np.array([
	[1.0, 10.0, 100.0],
	[2.0, 20.0, 200.0],
	[3.0, 30.0, 300.0],
])

column_means = matrix.mean(axis=0)
centered = matrix - column_means
```

Aquí no hace falta expandir manualmente `column_means` para cada fila. El broadcasting aplica la resta como si ese vector se replicara sobre toda la matriz. Este tipo de operación aparece con frecuencia en análisis de datos y aprendizaje automático.

Estas preguntas permiten leer los resultados con más cuidado y evitar la idea simplista de que cualquier paralelización explícita será superior a una formulación vectorizada.

## Una tabla de orientación rápida

| Estrategia | Conviene usarla cuando | Ventaja principal | Límite principal |
|---|---|---|---|
| Bucle explícito en Python | el problema es pequeño o muy irregular | simplicidad conceptual | alto costo por iteración |
| Vectorización con NumPy | la operación es regular sobre arreglos | gran reducción de overhead y buen uso de memoria | menos natural para lógica irregular |
| Broadcasting | hay que combinar estructuras compatibles de distinta forma | evita expansión manual y simplifica expresiones | requiere comprender reglas de dimensiones |
| Paralelismo explícito | el trabajo no puede resolverse solo con operaciones vectoriales | control sobre reparto de trabajo | comunicación y sincronización adicionales |

Con este marco, el siguiente paso será estudiar el paralelismo con GPU, donde estas ideas adquieren todavía mayor importancia.

## Ejercicios del capítulo

### Comprensión

1. Defina vectorización con sus palabras.
2. Explique qué problema resuelve el broadcasting.
3. Indique por qué SIMD resulta relevante para estas técnicas.
4. Explique por qué vectorización y broadcasting no son exactamente lo mismo.
5. Justifique por qué una operación vectorizada puede superar a un loop explícito en Python.

### Aplicación

1. Proponga un ejemplo sencillo en el que una operación sobre arreglos pueda expresarse con vectorización en lugar de un bucle explícito.
2. Describa una situación en la que el broadcasting facilite una operación entre estructuras de distinto tamaño.
3. Compare conceptualmente una versión con loop explícito y una versión vectorizada de una misma transformación sobre un arreglo.

### Integración

1. Elija una tarea numérica simple y justifique si conviene resolverla con un loop explícito, con vectorización o con paralelismo explícito.
2. Redacte una explicación breve sobre la relación entre vectorización, acceso a memoria y rendimiento observado.