# Computación con GPU

En las últimas décadas, las unidades de procesamiento gráfico dejaron de ser dispositivos dedicados exclusivamente al renderizado visual y pasaron a ocupar un lugar central en la computación paralela. Su arquitectura, pensada para ejecutar una gran cantidad de operaciones similares sobre muchos datos, las volvió especialmente valiosas en simulación, procesamiento multimedia e inteligencia artificial.

## Objetivos del capítulo

- introducir el papel de las GPU en la computación paralela contemporánea;
- presentar de manera general el modelo de ejecución de CUDA;
- vincular GPU, Numba y deep learning dentro del recorrido de la materia;
- incorporar PyTorch como vía de acceso de alto nivel a CPU y GPU;
- explicar los principales factores que influyen en el rendimiento de un kernel;
- introducir tipos de memoria y conceptos como coalescing, occupancy y warp divergence;
- incorporar criterios básicos de debugging y profiling para kernels GPU.

## Por qué las GPU ocupan un lugar central

Las GPU se volvieron especialmente relevantes porque permiten ejecutar una enorme cantidad de operaciones similares sobre grandes volúmenes de datos. Esta característica las hace adecuadas para problemas donde el paralelismo de datos es dominante, por ejemplo procesamiento de imágenes, simulaciones numéricas y entrenamiento de redes neuronales.

Conviene notar que esta ventaja no proviene solo de tener muchos núcleos. También depende de una arquitectura orientada a ocultar latencias, sostener alto ancho de banda de memoria y ejecutar miles de hilos ligeros sobre un mismo dispositivo. Esa lógica es diferente de la de una CPU generalista, que suele dedicar más recursos a la ejecución rápida de unos pocos hilos complejos.

## Qué caracteriza a una GPU

Una GPU dispone de una gran cantidad de núcleos especializados y de un ancho de banda de memoria muy elevado en comparación con la memoria RAM convencional. Estas características la hacen especialmente apta para tareas masivas y repetitivas sobre grandes volúmenes de datos.

El material de cátedra utiliza ejemplos concretos, como la referencia a una GPU NVIDIA GeForce RTX 4090, para ilustrar la magnitud de este tipo de hardware. Más allá del modelo puntual, lo importante es comprender el principio general: la GPU ofrece paralelismo masivo, aunque bajo reglas de programación distintas de las de una CPU tradicional.

En términos generales, una CPU optimiza latencia y control. Una GPU optimiza throughput, es decir, la cantidad total de trabajo completado sobre un gran conjunto de datos. Por ese motivo, una GPU no siempre es la mejor elección para cualquier algoritmo. Su ventaja aparece cuando el problema contiene muchas operaciones similares e independientes.

## CUDA como modelo de programación

CUDA, sigla de Compute Unified Device Architecture, es el modelo desarrollado por NVIDIA para utilizar GPU en cálculos de propósito general. En el material se explica que la ejecución se organiza mediante tres conceptos centrales: grid, block y thread.

Los hilos se agrupan en bloques y los bloques en grillas. Esta organización permite distribuir el trabajo sobre el dispositivo y adaptar la ejecución al problema planteado. La elección de dimensiones adecuadas para bloques y grillas constituye una parte importante del diseño y del análisis de rendimiento.

Un modo simple de leer esta estructura es el siguiente:

- cada `thread` ejecuta el mismo kernel sobre una parte del problema;
- varios `threads` se agrupan en un `block`, que comparte ciertos recursos del hardware;
- el conjunto de bloques forma el `grid`, que representa la ejecución total del kernel.

Desde el punto de vista conceptual, esta organización se parece a una versión masiva del paralelismo de datos estudiado en el capítulo 08, Modelos de programación paralela. La diferencia es que aquí la cantidad de hilos puede ser muy grande y la memoria del dispositivo introduce reglas específicas de rendimiento.

## Un kernel mínimo con Numba

La materia introduce el uso de GPU desde Python mediante Numba. Esta estrategia resulta especialmente adecuada para el enfoque didáctico del curso, ya que permite acercarse a conceptos de GPU sin abandonar el lenguaje principal de trabajo.

Un ejemplo mínimo de transformación elemento a elemento puede verse así:

```python
from numba import cuda


@cuda.jit
def add_one(values):
	index = cuda.grid(1)
	if index < len(values):
		values[index] += 1
```

En este kernel, cada hilo calcula su índice global dentro del grid y modifica un único elemento del arreglo. El interés del ejemplo no está en la operación elegida, sino en mostrar el patrón más básico de programación en GPU: un gran conjunto de hilos ejecuta el mismo código sobre datos distintos.

Cuando se lanza el kernel, también debe decidirse la configuración de ejecución:

```python
threads_per_block = 256
blocks_per_grid = (n + threads_per_block - 1) // threads_per_block
add_one[blocks_per_grid, threads_per_block](values)
```

Esta decisión influye directamente en el rendimiento. Elegirla bien es parte del problema de programación, no un detalle accesorio.

## Tipos de memoria en GPU

Uno de los motivos por los que dos kernels correctos pueden rendir de forma muy distinta es la jerarquía de memoria del dispositivo. En un nivel introductorio, conviene distinguir al menos estas regiones:

- memoria global: es la memoria principal de la GPU. Tiene gran capacidad, pero también una latencia relativamente alta;
- memoria compartida: es una memoria pequeña y rápida, visible para los hilos de un mismo bloque;
- memoria local: corresponde a datos privados de cada hilo, aunque puede terminar respaldada en memoria global según el uso de registros;
- memoria constante: está pensada para datos de solo lectura que se reutilizan de manera uniforme por muchos hilos.

En términos generales, una estrategia eficiente intenta minimizar accesos costosos a memoria global y reutilizar datos cuando sea posible mediante registros o memoria compartida. Esta observación conecta directamente con la jerarquía de memoria estudiada en CPU, aunque aquí adquiere todavía mayor relevancia.

## Coalescing

El coalescing describe una situación en la que hilos cercanos acceden a posiciones de memoria global cercanas entre sí. Cuando esto ocurre, el hardware puede agrupar esos accesos y utilizarlos de manera más eficiente.

Si, en cambio, cada hilo accede a posiciones dispersas o poco regulares, la GPU necesita más transacciones de memoria y el kernel pierde rendimiento. Por eso, no basta con que el trabajo esté paralelizado: también importa cómo se recorren y se distribuyen los datos.

Un ejemplo conceptual ayuda a verlo. Si el hilo `i` accede al elemento `values[i]`, el patrón suele ser favorable. Si el hilo `i` accede a `values[i * stride]` con un salto grande, el acceso puede volverse menos eficiente. El cálculo puede ser correcto en ambos casos, pero el comportamiento de memoria cambia de manera significativa.

## Warp divergence

En muchas GPU, los hilos se ejecutan internamente en grupos llamados warps. En términos simples, un warp es un conjunto de hilos que avanza de manera coordinada. Si todos siguen el mismo camino de ejecución, el hardware trabaja de forma eficiente. Si distintas ramas condicionales hacen que algunos hilos tomen un camino y otros otro, aparece la llamada warp divergence.

La divergencia no significa que el kernel esté mal, pero sí que parte del paralelismo efectivo se pierde porque el warp debe resolver caminos distintos en momentos diferentes. Por eso, en GPU conviene prestar atención a condiciones muy irregulares o a kernels donde los hilos de un mismo grupo no realizan operaciones similares.

## Occupancy

La occupancy puede entenderse, en este nivel, como la relación entre la cantidad de hilos activos en un multiprocesador de la GPU y la cantidad máxima que ese multiprocesador podría sostener. Una occupancy alta suele ayudar a ocultar latencias de memoria, porque mientras algunos hilos esperan datos otros pueden seguir ejecutándose.

Sin embargo, una occupancy alta no garantiza por sí sola un mejor rendimiento. Si el kernel usa demasiados registros, demasiada memoria compartida o presenta malos accesos a memoria, el desempeño puede seguir siendo pobre. Por ese motivo, la occupancy debe leerse como un indicador útil, pero no como un objetivo absoluto.

## Configuración del kernel y rendimiento observado

Uno de los problemas prácticos más importantes al trabajar con GPU consiste en elegir la configuración de `threadsperblock` y `blockspergrid`. Si el bloque es demasiado pequeño, puede desaprovechar recursos. Si es demasiado grande, puede limitar la cantidad de bloques activos o generar presión excesiva sobre registros y memoria compartida.

Por ese motivo, dos decisiones de configuración pueden producir tiempos muy distintos aun cuando el kernel sea exactamente el mismo. Esto explica por qué el ajuste de parámetros forma parte del análisis de performance y no debe tratarse como una elección arbitraria.

En términos introductorios, conviene quedarse con esta idea: el rendimiento en GPU depende de la interacción entre cómputo, memoria y configuración de ejecución. No alcanza con que el código "corra en la GPU".

## Uso de GPU con Numba y acceso práctico

La elección de Numba como puerta de entrada resulta especialmente útil porque permite experimentar con kernels, bloques y grillas sin abandonar Python. Desde el punto de vista didáctico, esto reduce barreras de entrada y ayuda a concentrarse en los conceptos fundamentales.

Además, cuando no se dispone de GPU local, herramientas como Google Colab permiten acceder a un entorno razonable para realizar pruebas. Esa disponibilidad es importante porque en GPU la experimentación resulta parte esencial del aprendizaje: conviene observar cómo cambian los resultados al modificar tamaño de datos, configuración del kernel o patrón de acceso a memoria.

## PyTorch como acceso de alto nivel a CPU y GPU

Numba no es la única forma de trabajar con GPU desde Python. En contextos prácticos, especialmente cuando el problema ya está formulado en términos de tensores, PyTorch ofrece una vía más directa. En lugar de escribir kernels explícitos, quien programa opera sobre tensores y decide en qué dispositivo quiere ejecutar el cálculo.

Ese cambio de nivel de abstracción es importante. Con Numba, el foco está puesto en cómo se organiza un kernel, cómo se calcula un índice y cómo se configura un grid. Con PyTorch, el foco se desplaza hacia operaciones sobre tensores y movimiento de datos entre CPU y GPU. Ambos enfoques son valiosos, pero responden a necesidades distintas.

Un ejemplo mínimo permite ver esa continuidad entre CPU y GPU:

```python
import torch

device = "cuda" if torch.cuda.is_available() else "cpu"

values = torch.tensor([1.0, 2.0, 3.0, 4.0], device=device)
result = values * 2 + 1
```

La operación es la misma tanto si `device` vale `"cpu"` como si vale `"cuda"`. Desde el punto de vista didáctico, esto resulta especialmente útil porque permite trabajar con el mismo código básico incluso en entornos donde no siempre hay GPU disponible.

También puede escribirse de forma más explícita el movimiento entre dispositivos:

```python
import torch

values = torch.tensor([1.0, 2.0, 3.0, 4.0])
cpu_result = values * 2 + 1

if torch.cuda.is_available():
	gpu_values = values.to("cuda")
	gpu_result = gpu_values * 2 + 1
	result_back_on_cpu = gpu_result.to("cpu")
```

Aquí aparecen con claridad tres momentos: datos en CPU, cómputo en GPU y devolución del resultado al host. Esa secuencia retoma una idea ya señalada en la sección de debugging y profiling: medir una ejecución GPU exige distinguir cálculo y transferencia.

## Numba y PyTorch: dos puertas de entrada distintas

Conviene comparar brevemente ambos enfoques para no confundir sus papeles dentro del libro.

| Herramienta | Nivel de abstracción | Conviene usarla cuando | Lo que deja ver con más claridad |
|---|---|---|---|
| Numba | más cercano al kernel y a CUDA | interesa entender cómo se distribuye trabajo en threads, blocks y grids | organización interna de la ejecución GPU |
| PyTorch | más cercano a tensores y operaciones de alto nivel | el problema ya se expresa como cálculo sobre tensores y se quiere trabajar en CPU o GPU con una interfaz uniforme | continuidad entre vectorización, tensores y aceleración |

Esta comparación ayuda a ubicar mejor el sentido pedagógico del capítulo. Numba permite entender cómo funciona la GPU más de cerca. PyTorch muestra cómo muchas aplicaciones reales acceden a ese hardware sin escribir kernels manuales.

## Importancia para deep learning

Uno de los motivos por los que las GPU ganaron tanta relevancia es su papel en el entrenamiento y la inferencia de modelos de aprendizaje profundo. Redes neuronales con millones de parámetros requieren una enorme cantidad de operaciones numéricas, y las GPU permiten ejecutarlas de manera mucho más eficiente que una CPU generalista en muchos casos.

La razón profunda de esta ventaja no es solo la cantidad de núcleos. También influye que muchas operaciones de deep learning, como productos matriciales, convoluciones y transformaciones sobre tensores, tienen una estructura muy regular y altamente paralelizable. En ese sentido, las GPU representan una continuidad natural de las ideas de vectorización y paralelismo de datos desarrolladas en el capítulo 12, Vectorización y broadcasting.

## Qué conviene observar al analizar una implementación GPU

Al estudiar o medir un kernel, conviene observar al menos estas cuestiones:

- si el problema tiene suficiente paralelismo de datos como para justificar el uso de la GPU;
- si los accesos a memoria global son regulares o dispersos;
- si los hilos de un mismo warp siguen trayectorias de ejecución similares;
- si la configuración de bloques e hilos parece razonable para el tamaño del problema;
- si el costo de copiar datos entre CPU y GPU no anula la mejora obtenida en el cómputo.

Estas preguntas ayudan a interpretar resultados experimentales y a evitar una expectativa ingenua según la cual cualquier cálculo será automáticamente más rápido por ejecutarse en GPU.

## Debugging y profiling en GPU

En GPU, una parte importante del trabajo consiste en distinguir entre un kernel incorrecto y un kernel correcto pero ineficiente. Ese diagnóstico requiere una forma de observación algo diferente de la que se usa en CPU, porque aquí intervienen también copias de datos entre host y dispositivo, configuración de ejecución y patrones de acceso a memoria.

Una primera recomendación consiste en separar conceptualmente tres tiempos distintos:

- el tiempo de preparación y copia de datos hacia la GPU;
- el tiempo de ejecución del kernel;
- el tiempo de devolución de resultados al host.

Si no se distinguen estas etapas, una medición puede llevar a conclusiones engañosas. Un kernel muy rápido puede parecer lento si el volumen de transferencia domina el tiempo total.

En una medición básica con Numba, además, conviene sincronizar explícitamente antes de detener el reloj, ya que la ejecución puede ser asincrónica:

```python
import time
from numba import cuda


start = time.time()
kernel[blocks_per_grid, threads_per_block](values)
cuda.synchronize()
elapsed = time.time() - start
```

Sin esa sincronización, el tiempo medido puede no reflejar la ejecución real del kernel.

Desde el punto de vista del debugging, conviene observar al menos estos síntomas:

- resultados incorrectos por índices mal calculados o límites mal controlados;
- kernels que funcionan pero rinden poco por accesos no coalesced;
- configuraciones de bloques que reducen occupancy o desaprovechan el dispositivo;
- tiempos dominados por copia de datos en lugar de por cómputo.

En un nivel introductorio, profiling y debugging en GPU no requieren todavía herramientas sofisticadas. Lo importante es aprender a formular buenas preguntas: si el cuello de botella está en memoria, en configuración, en divergencia o en transferencia, la estrategia de mejora será distinta.

## Cierre de la unidad

Este capítulo permitió introducir la GPU como una plataforma de paralelismo masivo orientada a throughput, con una organización de hilos y una jerarquía de memoria propias. También mostró que el rendimiento no depende solo de escribir un kernel correcto, sino de comprender cómo interactúan bloques, warps, memoria global, memoria compartida y configuración de ejecución.

Con este marco, el capítulo final del libro reunirá algunas líneas de proyección para seguir profundizando el estudio del paralelismo, incluyendo temas avanzados de rendimiento, profiling, GPU y memoria.

## Ejercicios del capítulo

### Comprensión

1. Explique por qué una GPU resulta adecuada para tareas altamente paralelizables.
2. Describa la función de los conceptos grid, block y thread en CUDA.
3. Indique qué relación existe entre GPU y deep learning.
4. Distinga memoria global y memoria compartida en una GPU.
5. Explique con sus palabras qué significan coalescing, occupancy y warp divergence.
6. Justifique por qué conviene separar tiempo de transferencia y tiempo de kernel al medir rendimiento.

### Aplicación

1. Justifique por qué Google Colab puede ser una herramienta útil para esta unidad.
2. Proponga una tarea que podría beneficiarse del uso de GPU y explique brevemente por qué.
3. Describa un caso en el que una mala elección de `threadsperblock` podría degradar el rendimiento.
4. Proponga un ejemplo conceptual de acceso coalesced y otro de acceso no coalesced.
5. Explique qué error puede cometerse al medir un kernel si no se sincroniza la GPU antes de registrar el tiempo final.

### Integración

1. Explique por qué dos kernels correctos pueden rendir de forma muy distinta en una misma GPU.
2. Relacione las ideas de vectorización, paralelismo de datos y GPU dentro del recorrido del libro.
3. Describa qué observaría primero para diagnosticar una implementación GPU correcta que no muestra mejora de rendimiento.