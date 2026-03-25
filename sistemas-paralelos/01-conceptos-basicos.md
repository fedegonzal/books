# Conceptos básicos

Antes de analizar arquitecturas o escribir código paralelo, conviene comprender con precisión los conceptos básicos que organizan el campo. En esta unidad se distinguen distintos modos de ejecución, se revisan límites históricos de la computación secuencial y se introducen ideas centrales como núcleo de procesamiento, sincronización y niveles de paralelismo.

La computación paralela ocupa hoy un lugar central en la informática porque muchos problemas actuales ya no pueden resolverse de manera eficiente confiando solo en el aumento de la frecuencia de reloj. Procesamiento de imágenes y video, simulaciones, análisis de grandes volúmenes de datos, inteligencia artificial y servicios distribuidos exigen aprovechar mejor los recursos de hardware disponibles. Por ese motivo, conviene estudiar el paralelismo no como un tema aislado, sino como una respuesta técnica a necesidades concretas de rendimiento.

También es importante notar que el problema involucra al mismo tiempo hardware y software. No alcanza con disponer de múltiples núcleos, clústeres o GPU: es necesario diseñar algoritmos capaces de dividir el trabajo, coordinar tareas y sincronizar resultados. Dicho de forma simple, los sistemas paralelos se ubican en la intersección entre arquitectura de cómputo, modelos de programación y análisis de performance.

## Objetivos del capítulo

- distinguir computación secuencial, concurrente, paralela y distribuida;
- explicar de manera introductoria cómo ejecuta instrucciones un procesador;
- relacionar la evolución del hardware con la necesidad de paralelizar;
- presentar los principales niveles de paralelismo.

## Por qué estudiar paralelismo

El paralelismo ya forma parte del hardware cotidiano. Computadoras personales, notebooks, teléfonos móviles y placas de video incorporan distintos niveles de ejecución simultánea. En consecuencia, incluso en desarrollos que no pertenecen a la computación de alto rendimiento, conviene entender cómo se reparten tareas, qué costos introduce la sincronización y qué límites aparecen cuando se busca acelerar un programa.

Además, el área no se reduce a un conjunto de bibliotecas o trucos de implementación. Estudiar sistemas paralelos implica construir criterios para distinguir cuándo un problema puede beneficiarse del paralelismo, qué arquitectura resulta más adecuada y cómo evaluar si la mejora obtenida justifica los recursos empleados.

Por ese motivo, conviene pensar el paralelismo también como una forma de analizar problemas. Antes de escribir una implementación paralela, suele ser necesario preguntarse qué partes del trabajo pueden ejecutarse de manera independiente, cuáles dependen de resultados previos y en qué momento será necesario recombinar los resultados parciales. Esa mirada de descomposición es tan importante como la herramienta elegida para programar.

## Computación secuencial

La computación secuencial es la forma tradicional de ejecución de programas. Las instrucciones se realizan una tras otra, en un orden determinado, y en cada instante solo una rama de ejecución avanza efectivamente. Aunque existan estructuras condicionales o repetitivas, el programa sigue un recorrido único en cada paso.

Comprender esta modalidad es importante porque el paralelismo no reemplaza por completo a la ejecución secuencial. Más bien se construye sobre ella, identificando qué partes de un problema pueden descomponerse y cuáles deben mantenerse en orden.

Un ejemplo simple ayuda a ver esta diferencia. Si se desea sumar los valores `40 + 20 + 10 + 60`, una implementación secuencial realiza una acumulación lineal: primero suma `40 + 20`, luego agrega `10` y finalmente `60`. En cambio, una descomposición paralela puede organizar el mismo cálculo en dos sumas parciales independientes, por ejemplo `40 + 20` y `10 + 60`, para luego combinar ambos resultados. El problema es el mismo, pero cambia la forma de organizar el trabajo.

Un pseudocódigo mínimo permite ver con más claridad esa reorganización:

```text
total = 40 + 20
total = total + 10
total = total + 60
```

Frente a una descomposición en árbol de dos etapas:

```text
parcial_1 = 40 + 20
parcial_2 = 10 + 60
total = parcial_1 + parcial_2
```

En la segunda formulación, `parcial_1` y `parcial_2` podrían calcularse de manera simultánea. La sincronización aparece en el momento de combinar ambos resultados para producir el valor final.

Esta observación parece menor, aunque en realidad introduce una idea central: paralelizar no consiste únicamente en ejecutar más cosas al mismo tiempo, sino en reorganizar un problema para exponer partes independientes sin perder corrección.

## Velocidad de ejecución y ciclo del procesador

El material de cátedra introduce la idea de ciclo de reloj para explicar cómo la CPU sincroniza sus operaciones básicas. También presenta, de forma simplificada, el ciclo de ejecución mediante las etapas fetch, decode, execute y write. Esta descripción permite entender que el rendimiento no depende solo de la cantidad de instrucciones, sino también de cómo las ejecuta el hardware.

Durante décadas, el incremento de la frecuencia de reloj fue una estrategia central para mejorar la performance. Sin embargo, el aumento del calor y del consumo energético llevó a buscar otras alternativas. Ese cambio histórico abrió paso a la popularización de procesadores multicore.

## Los límites de la computación secuencial

La llamada ley de Moore permitió durante muchos años sostener un crecimiento notable en la capacidad de cómputo. No obstante, el aumento de frecuencia comenzó a mostrar límites prácticos. La respuesta de la industria fue diseñar procesadores con varios núcleos, capaces de ejecutar múltiples tareas simultáneamente.

Este cambio no solo afectó al hardware. También obligó a repensar el software, ya que el rendimiento adicional dejó de depender exclusivamente del fabricante del procesador y pasó a exigir programas capaces de aprovechar esos recursos.

Sin embargo, disponer de más núcleos no implica automáticamente una aceleración proporcional. En muchos problemas siempre existe una parte del trabajo que debe mantenerse secuencial o que introduce costos de coordinación. Más adelante se verá que esta restricción impone límites teóricos y prácticos al speed-up, incluso cuando el hardware disponible es abundante.

## Concurrencia, paralelismo y distribución

La concurrencia se refiere a la coexistencia de varias tareas en ejecución o en progreso, aun cuando no siempre se resuelva un mismo problema. El paralelismo, en cambio, apunta específicamente a dividir un problema en partes que puedan ejecutarse simultáneamente para obtener un resultado común.

La computación distribuida agrega otra dimensión: los procesadores o nodos pueden encontrarse físicamente separados y cooperar mediante intercambio de datos. En la práctica contemporánea, estos enfoques suelen combinarse. Por ese motivo, conviene distinguir sus diferencias conceptuales sin perder de vista que en sistemas reales aparecen mezclados.

Una comparación breve permite aclarar la distinción. Si en una computadora se descarga un archivo mientras se reproduce música y se edita un documento, hay concurrencia: varias tareas avanzan en el mismo intervalo, aunque no cooperan para resolver un único problema. En cambio, si una suma grande de datos se divide en bloques para que varios núcleos calculen subtotales y luego se integren en un único resultado, hay paralelismo. En ambos casos puede haber actividad simultánea, pero solo en el segundo existe cooperación directa sobre una misma tarea.

## Niveles de paralelismo

El programa también menciona distintos niveles de paralelismo. Algunos son transparentes para quien programa, como el paralelismo a nivel de bit o de instrucción. Otros requieren decisiones explícitas, como el paralelismo de tareas, el paralelismo de datos y la vectorización.

El paralelismo de tareas divide un problema en subtareas que pueden asignarse a distintas unidades de procesamiento. El paralelismo de datos aplica la misma operación sobre particiones independientes de un conjunto de entrada. La vectorización, por su parte, aprovecha operaciones repetitivas sobre estructuras de datos para ejecutarlas de forma más eficiente.

Distinguir estos niveles es importante porque no todo paralelismo se expresa del mismo modo. A veces la mejora proviene de dividir tareas diferentes entre varios workers; en otros casos, de aplicar la misma operación sobre grandes volúmenes de datos; y en otros, de mecanismos internos del hardware que resultan casi invisibles para quien programa. Reconocer esas diferencias ayuda a elegir mejor las herramientas y también a interpretar los resultados de rendimiento.

## Observación del uso de CPU

Una idea práctica que aparece en el material consiste en observar la carga de cada core y no solo un porcentaje global de CPU. Esta recomendación será útil en los trabajos prácticos, ya que permite analizar si un programa efectivamente distribuye su carga de trabajo o si mantiene un uso predominantemente secuencial.

## Cierre de la unidad

Con este marco ya se cuenta con una base conceptual suficiente para avanzar hacia el análisis de plataformas y métricas. En particular, el capítulo permitió distinguir tipos de ejecución, entender por qué el multicore modificó el problema del rendimiento y ver que paralelizar exige descomponer, coordinar y sincronizar trabajo.

En el próximo capítulo se estudiarán clasificaciones de arquitecturas paralelas y medidas de rendimiento como speed-up y eficiencia. Ese paso permitirá no solo describir plataformas, sino también analizar por qué una implementación paralela puede rendir mucho mejor, apenas mejor o incluso peor de lo esperado.

## Ejercicios del capítulo

### Comprensión

1. Distinga computación secuencial, concurrente, paralela y distribuida.
2. Explique por qué la aparición de procesadores multicore modificó las exigencias sobre el software.
3. Describa la diferencia entre paralelismo de tareas y paralelismo de datos.
4. Explique por qué conviene entender el paralelismo también como una forma de descomponer problemas.

### Aplicación

1. Proponga un ejemplo cotidiano de tarea concurrente y otro de tarea paralela.
2. Observe el monitor de actividad de su sistema y describa qué información ofrece sobre el uso de los distintos cores.
3. Reescriba conceptualmente una suma secuencial de cuatro valores como una suma en árbol de dos etapas e indique dónde aparece la sincronización.

### Integración

1. Redacte un texto breve en el que relacione límites de la computación secuencial, multicore y necesidad de paralelización.
2. Justifique por qué disponer de más cores no garantiza, por sí solo, una mejora lineal del rendimiento.