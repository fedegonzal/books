# Modelos de programación paralela

Disponer de hardware paralelo no garantiza por sí mismo una solución eficiente. También es necesario decidir cómo descomponer el problema, cómo distribuir tareas y cómo coordinar resultados. Los modelos de programación paralela ofrecen justamente marcos de organización para pensar estas decisiones.

## Objetivos del capítulo

- presentar algunos paradigmas clásicos de programación paralela;
- describir el tipo de problemas para los que cada modelo puede resultar útil;
- vincular cada paradigma con las nociones de comunicación, sincronización y distribución del trabajo.

## Por qué trabajar con modelos

Los modelos de programación paralela funcionan como esquemas conceptuales y prácticos. Permiten reconocer patrones recurrentes en problemas distintos y facilitan la elección de una estrategia de implementación. En lugar de empezar desde cero ante cada desafío, conviene apoyarse en estructuras conocidas que ya organizan la coordinación entre procesos o tareas.

También conviene evitar un error frecuente: pensar que un modelo es equivalente a una biblioteca o a una API concreta. Un modelo describe una forma de organizar el problema. Luego esa idea puede implementarse con herramientas diferentes según la arquitectura disponible, el lenguaje elegido y el costo aceptable de sincronización o comunicación.

## Criterios para elegir un modelo

Antes de revisar cada paradigma, conviene identificar algunas preguntas guía:

- ¿el problema puede dividirse en subtareas relativamente independientes o requiere una coordinación central fuerte?;
- ¿el trabajo se parece más a una secuencia de etapas, a una descomposición recursiva o a una aplicación repetida de la misma operación sobre muchos datos?;
- ¿la comunicación entre tareas será frecuente o esporádica?;
- ¿interesa más maximizar rendimiento, simplificar implementación o facilitar escalabilidad distribuida?;
- ¿el problema tiene una estructura estable y regular, o cambia dinámicamente durante la ejecución?

Estas preguntas no producen una respuesta automática, pero permiten justificar mejor por qué un modelo resulta más adecuado que otro.

## Vista comparativa

La siguiente tabla resume el rasgo dominante de cada modelo y el tipo de problema en el que suele resultar más útil.

| Modelo | Idea central | Conviene usarlo cuando | Caso reconocible |
|---|---|---|---|
| Maestro-esclavo | un coordinador reparte trabajo y reúne resultados | hay una lógica central clara de asignación y control | procesamiento de lotes independientes |
| Divide and conquer | el problema se divide recursivamente y luego se combinan resultados | la tarea admite particiones naturales y balanceadas | suma recursiva, ordenamiento, matrices |
| Pipelining | el trabajo se organiza en etapas consecutivas | los datos fluyen por fases con operaciones diferenciadas | procesamiento de imágenes o streaming |
| MapReduce | se aplica una función a muchos datos y luego se agregan resultados | hay grandes volúmenes de datos con operaciones homogéneas | conteo de palabras, agregaciones masivas |
| Actores | componentes autónomos intercambian mensajes | el sistema requiere desacoplamiento, concurrencia y evolución dinámica | servicios distribuidos o sistemas reactivos |

## Modelo maestro-esclavo

El modelo maestro-esclavo, también llamado master-slave, organiza la ejecución a partir de un proceso principal que distribuye trabajo a varios procesos secundarios. El maestro coordina, asigna tareas y reúne resultados. Este enfoque resulta claro cuando existe una lógica central de reparto y control.

El material de cátedra lo presenta junto con ejemplos basados en colas y procesos, destacando la importancia de un mecanismo de comunicación eficiente entre quien coordina y quienes ejecutan.

Este modelo conviene cuando las tareas son muchas, relativamente similares entre sí y pueden asignarse desde un punto central sin excesivo costo. Un caso típico es el procesamiento por lotes de archivos, imágenes o registros, donde un proceso maestro reparte unidades de trabajo independientes a varios workers.

Su ventaja principal es la claridad organizativa. Su riesgo principal es que el maestro se convierta en cuello de botella o en punto único de falla si concentra demasiadas decisiones o demasiada comunicación.

## Divide and conquer

El modelo divide and conquer resuelve un problema descomponiéndolo en subproblemas más pequeños, que a su vez pueden dividirse de forma recursiva. Luego se combinan los resultados parciales para obtener la solución final. Ejemplos clásicos son QuickSort y ciertas estrategias de multiplicación de matrices.

Este paradigma es útil cuando el problema admite una descomposición natural y relativamente equilibrada.

Un ejemplo mínimo es la suma recursiva de un vector. En lugar de recorrer todos los elementos en una sola secuencia, el vector puede partirse en dos mitades, sumar cada mitad por separado y luego combinar ambos subtotales. Esa misma idea puede repetirse sobre particiones cada vez más pequeñas.

Un esquema mínimo de pseudocódigo puede escribirse así:

```text
funcion suma_recursiva(datos):
	if longitud(datos) == 1:
		return datos[0]

	mitad = longitud(datos) // 2
	izquierda = suma_recursiva(datos[:mitad])
	derecha = suma_recursiva(datos[mitad:])
	return izquierda + derecha
```

En una implementación paralela, las llamadas `izquierda` y `derecha` podrían ejecutarse al mismo tiempo mientras el costo de combinación queda concentrado en la suma final.

Conviene usar este modelo cuando la división del problema produce subproblemas de tamaño semejante y con poca dependencia entre sí. Si las particiones quedan muy desbalanceadas o si la fase de combinación resulta costosa, la ventaja del modelo disminuye.

## Pipelining

El modelo de pipelining divide el procesamiento en etapas. Cada etapa realiza una parte del trabajo y pasa el resultado a la siguiente. Mientras una etapa procesa un nuevo elemento, otra puede estar terminando el elemento anterior. Se genera así un flujo continuo, similar a una línea de producción.

Su principal desafío consiste en gestionar correctamente las dependencias entre etapas para evitar cuellos de botella.

Este paradigma resulta especialmente útil cuando el trabajo puede describirse como una secuencia estable de transformaciones. Un caso reconocible es el procesamiento de datos provenientes de sensores, video o registros: una etapa lee, otra limpia, otra transforma y una última almacena o visualiza resultados.

Conviene distinguir este modelo de divide and conquer. En un pipeline, los datos atraviesan etapas diferentes. En divide and conquer, el mismo problema se subdivide en partes del mismo tipo y luego se recompone. Esa diferencia organizativa produce necesidades de sincronización muy distintas.

## MapReduce

MapReduce organiza el cálculo en dos grandes fases: una etapa de mapeo, que aplica una operación sobre múltiples elementos, y una etapa de reducción, que combina los resultados parciales. Se trata de un modelo muy asociado al procesamiento distribuido de grandes volúmenes de datos y a herramientas como Hadoop o Apache Spark.

Aunque en esta materia se presenta de forma introductoria, su valor conceptual es grande porque muestra una estrategia de paralelización centrada en datos y agregación de resultados.

Un ejemplo clásico es el conteo de palabras en una gran colección de documentos. La fase de map produce pares del tipo palabra, frecuencia parcial. La fase de reduce agrega las ocurrencias de cada palabra y construye el total final. Más allá de la herramienta concreta, lo importante es observar que el modelo organiza con claridad la relación entre paralelismo de datos y agregación.

Conviene usar este enfoque cuando la tarea puede expresarse como una operación repetida sobre muchas entradas independientes seguida de una combinación de resultados. No suele ser la mejor opción cuando existen dependencias complejas, interacción frecuente entre tareas o estructuras de datos muy cambiantes.

## Modelo de actores

En el modelo de actores, cada proceso o componente se entiende como una entidad independiente con estado propio, que se comunica con otros actores mediante mensajes. No se basa necesariamente en una jerarquía fija, sino en interacciones coordinadas entre componentes autónomos. Este enfoque resulta especialmente relevante para sistemas concurrentes y distribuidos.

Un caso reconocible es una plataforma compuesta por servicios que reciben eventos, procesan pedidos y envían respuestas sin compartir memoria directamente. Cada actor mantiene su estado local y responde a mensajes, lo que favorece desacoplamiento y escalabilidad.

Este modelo conviene cuando interesa reducir acoplamiento entre componentes y tolerar mejor la complejidad de la concurrencia. A cambio, obliga a pensar cuidadosamente el diseño de mensajes, la coordinación entre actores y el seguimiento del estado distribuido.

## Comparación conceptual entre modelos

Si se observa el conjunto, maestro-esclavo y divide and conquer son modelos orientados con más claridad al reparto del trabajo. Pipelining organiza una cadena de etapas. MapReduce enfatiza transformación de datos y agregación. Actores privilegia interacción entre componentes autónomos.

Ningún modelo resuelve por sí solo todos los problemas. En sistemas reales es frecuente combinar varios. Por ejemplo, un clúster puede usar un esquema maestro-esclavo para distribuir bloques de datos y, dentro de cada bloque, aplicar una estrategia divide and conquer o un pipeline de procesamiento.

## Dificultades de la computación paralela

El programa subraya un punto decisivo: programar algoritmos paralelos suele ser más difícil que programar algoritmos secuenciales. La sincronización, la comunicación entre procesos y la necesidad de evitar errores como esperas innecesarias o incoherencias de datos introducen complejidad adicional.

Por ese motivo, los modelos no solo ayudan a organizar soluciones, sino también a razonar sobre sus riesgos y limitaciones.

En este sentido, elegir un modelo adecuado no es solo una cuestión de estilo. Una buena elección puede reducir comunicación, simplificar sincronización y mejorar la escalabilidad. Una mala elección puede producir cuellos de botella, tareas desbalanceadas o una implementación innecesariamente difícil de mantener.

## Cierre de la unidad

Con estos paradigmas ya es posible pasar de la discusión arquitectónica a una discusión de diseño. El capítulo mostró que programar en paralelo no consiste solo en lanzar hilos o procesos, sino en decidir cómo se estructura el trabajo y cómo se relacionan las tareas entre sí.

En el próximo capítulo estas ideas se traducirán a APIs clásicas de programación paralela. Allí se verá cómo modelos como memoria compartida, memoria distribuida y reparto de tareas se concretan en herramientas específicas de implementación.

## Ejercicios del capítulo

### Comprensión

1. Describa las características básicas del modelo maestro-esclavo.
2. Explique en qué se diferencia un pipeline de una estrategia divide and conquer.
3. Indique qué papel cumplen los mensajes en el modelo de actores.
4. Justifique por qué MapReduce se asocia especialmente con problemas de gran volumen de datos.

### Aplicación

1. Proponga un problema que podría resolverse con MapReduce y justifique su elección.
2. Elija uno de los modelos presentados y describa qué tipo de sincronización requeriría.
3. Proponga un caso en el que maestro-esclavo sea una mejor elección que actores y explique por qué.

### Integración

1. Compare dos de los modelos estudiados y explique qué cambiaría en la organización del trabajo si un mismo problema se resolviera con uno u otro.
2. Elija un problema de procesamiento de datos, imágenes o servicios distribuidos e indique qué modelo considera más adecuado, con una justificación breve.