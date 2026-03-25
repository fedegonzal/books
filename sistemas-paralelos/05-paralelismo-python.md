# Paralelismo en Python

En esta materia, Python funciona como lenguaje de trabajo para experimentar con conceptos de programación paralela. La elección tiene un sentido pedagógico claro: se trata de un entorno accesible, ampliamente utilizado y relevante en ámbitos profesionales y académicos. Sin embargo, trabajar con Python también exige comprender ciertas limitaciones y estrategias específicas.

## Objetivos del capítulo

- presentar herramientas de Python útiles para explorar paralelismo;
- comparar enfoques basados en hilos, procesos, vectorización y compilación JIT;
- ubicar bibliotecas de tensores como PyTorch dentro del ecosistema de CPU y GPU;
- relacionar cada estrategia con el tipo de problema que conviene resolver;
- señalar las limitaciones del lenguaje y sus implicancias prácticas;
- introducir errores frecuentes de concurrencia y criterios básicos de diagnóstico.

## Por qué Python

El material de cátedra explica que, aunque Python presenta limitaciones para la ejecución en paralelo, se elige por su amplia adopción y por su utilidad profesional inmediata. Esta decisión no implica desconocer otras opciones más cercanas al hardware, sino priorizar una plataforma que permita concentrarse en los fundamentos sin elevar innecesariamente la barrera de entrada.

Python también tiene una ventaja didáctica importante: permite comparar con relativa facilidad una versión secuencial, una versión con hilos, otra con procesos y otra más optimizada mediante bibliotecas numéricas. Ese contraste ayuda a ver que el paralelismo no es una única técnica, sino una familia de estrategias con costos y beneficios diferentes.

## Un mapa inicial de herramientas

Entre las herramientas disponibles aparecen `threading`, `multiprocessing`, NumPy, Numba, PyTorch, JAX, TensorFlow y otras bibliotecas afines. No todas cumplen el mismo papel.

- `threading` y sus variantes permiten trabajar con concurrencia basada en hilos;
- `multiprocessing` crea procesos independientes y evita la restricción principal del GIL para tareas intensivas de CPU;
- NumPy ofrece vectorización y broadcasting, que en muchos casos resultan más eficaces que paralelizar bucles explícitos;
- Numba compila funciones Python y puede acercar el rendimiento al de implementaciones más cercanas al hardware, tanto en CPU como en GPU;
- bibliotecas como PyTorch o JAX combinan operaciones vectorizadas, aceleración y acceso a GPU en contextos más amplios de cálculo científico y aprendizaje automático.

Esta variedad es valiosa porque muestra que el paralelismo en Python no depende de una sola biblioteca. La decisión correcta depende del tipo de problema, del tamaño de los datos y del costo de coordinación.

## El Global Interpreter Lock

Uno de los puntos centrales de esta unidad es el Global Interpreter Lock, conocido como GIL. Se trata de una limitación relevante en la implementación tradicional de Python, ya que condiciona la ejecución simultánea de hilos dentro de un mismo intérprete. Por ese motivo, no siempre alcanza con crear múltiples threads para obtener una mejora real en tareas intensivas de CPU.

En términos prácticos, esto significa que los hilos en Python suelen ser adecuados para tareas I/O-bound, como leer archivos, esperar respuestas de red o interactuar con dispositivos. En cambio, para tareas CPU-bound, como sumar grandes arreglos, procesar imágenes o calcular modelos, el GIL limita la ganancia esperable si se usan hilos convencionales.

Comprender esta limitación es fundamental para interpretar correctamente los resultados experimentales. Un programa con muchos threads puede parecer más complejo o más paralelo y, sin embargo, rendir igual o peor que una versión secuencial si el problema está dominado por cálculo puro.

## Cómo elegir una estrategia

Antes de escribir código conviene responder una pregunta simple: ¿el problema está limitado por entrada y salida o por cálculo?

- si el problema es I/O-bound, los hilos suelen ser una opción razonable;
- si el problema es CPU-bound, los procesos o herramientas como Numba suelen ser mejores alternativas;
- si el trabajo consiste en aplicar operaciones repetitivas sobre arreglos numéricos, conviene evaluar primero vectorización con NumPy;
- si se necesita acelerar código Python sin reescribir todo el algoritmo en otro lenguaje, Numba funciona como un puente especialmente útil.

Este criterio evita una decisión ingenua muy frecuente: elegir la herramienta por familiaridad en lugar de elegirla según la estructura real del problema.

## Patrones para paralelizar loops en Python

Uno de los usos más comunes del paralelismo en Python consiste en transformar un loop secuencial en una ejecución repartida entre workers. El extracto revisado del material complementario resulta especialmente útil para ordenar esos patrones.

### Creación manual de workers

La forma más explícita consiste en crear un hilo o un proceso por tarea. Este enfoque es pedagógicamente útil porque muestra con claridad qué significa lanzar trabajo independiente, iniciar workers y esperar su finalización.

Un patrón mínimo con hilos podría escribirse así:

```python
from threading import Thread


def task(value):
	print(value * value)


if __name__ == "__main__":
	threads = [Thread(target=task, args=(i,)) for i in range(4)]

	for thread in threads:
		thread.start()

	for thread in threads:
		thread.join()
```

Y un patrón equivalente con procesos podría expresarse de este modo:

```python
from multiprocessing import Process


def task(value):
	print(value * value, flush=True)


if __name__ == "__main__":
	processes = [Process(target=task, args=(i,)) for i in range(4)]

	for process in processes:
		process.start()

	for process in processes:
		process.join()
```

Estas versiones son claras, pero no escalan bien cuando hay muchas tareas pequeñas. Crear un worker por iteración introduce un overhead considerable y, además, dificulta la recuperación ordenada de resultados.

### Pools y executors

Cuando la tarea consiste en aplicar la misma función muchas veces con diferentes entradas, conviene reutilizar un conjunto fijo de workers. Ahí aparecen los pools y los executors.

Un ejemplo con `ProcessPoolExecutor` permite ver el patrón moderno más útil para tareas CPU-bound:

```python
from concurrent.futures import ProcessPoolExecutor


def task(value):
	return value * value


if __name__ == "__main__":
	with ProcessPoolExecutor() as executor:
		results = list(executor.map(task, range(8)))

	print(results)
```

Para tareas I/O-bound, una estructura análoga con `ThreadPoolExecutor` suele ser más natural. La diferencia importante no está solo en la sintaxis, sino en el tipo de problema para el cual cada executor resulta apropiado.

En términos prácticos, los executors suelen ser preferibles a la creación manual masiva porque reutilizan workers, simplifican la recolección de resultados y expresan mejor la intención del programa.

## Secuencial, threads, procesos y Numba sobre un mismo problema

Para comparar estrategias conviene partir de un problema pequeño y homogéneo. Un ejemplo típico es recorrer un vector y acumular resultados. En versión secuencial, el patrón es simple:

```python
def sum_elements(values):
	total = 0
	for value in values:
		total += value
	return total
```

Si se intenta resolver este mismo problema con `threading`, puede que el rendimiento no mejore en tareas CPU-bound debido al GIL. Con `multiprocessing`, en cambio, es posible repartir bloques entre procesos distintos y combinar subtotales. Una versión conceptual mínima podría verse así:

```python
from multiprocessing import Pool


def partial_sum(values):
	total = 0
	for value in values:
		total += value
	return total


if __name__ == "__main__":
	chunks = [list(range(0, 250000)), list(range(250000, 500000))]

	with Pool(processes=2) as pool:
		partials = pool.map(partial_sum, chunks)

	print(sum(partials))
```

La idea importante es que la ganancia no proviene solo de usar una biblioteca diferente, sino de haber repartido los datos y de aceptar el costo de serialización y sincronización entre procesos.

Con Numba, el mismo problema puede atacarse desde otra lógica: en lugar de coordinar múltiples procesos desde Python, se compila el cálculo y se deja que la biblioteca optimice la ejecución.

```python
from numba import njit, prange


@njit(parallel=True)
def sum_numba(values):
	total = 0.0
	for index in prange(len(values)):
		total += values[index]
	return total
```

Este enfoque es especialmente importante en el libro porque conecta con OpenMP a nivel conceptual y prepara el camino hacia vectorización y GPU.

## El lugar de NumPy

Antes de paralelizar bucles en Python, conviene considerar una alternativa muchas veces más efectiva: eliminar el bucle explícito. NumPy permite expresar operaciones sobre arreglos completos mediante vectorización. En problemas numéricos regulares, esta estrategia suele superar a muchas soluciones basadas en threads o procesos, justamente porque reduce la sobrecarga del intérprete y aprovecha implementaciones de bajo nivel optimizadas.

Por ejemplo, si el objetivo es sumar dos vectores, una formulación vectorizada como la siguiente suele ser preferible a un loop Python paralelizado manualmente:

```python
import numpy as np


a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
c = a + b
```

Esta observación es central para la materia: no todo problema repetitivo debe resolverse con hilos o procesos. En muchos casos, la optimización correcta consiste en cambiar el nivel de abstracción del cálculo.

## PyTorch dentro del ecosistema Python

Hasta aquí el capítulo presentó herramientas orientadas a hilos, procesos, vectorización y compilación. Conviene agregar una pieza importante del ecosistema actual: PyTorch. Esta biblioteca trabaja con tensores y permite ejecutar muchas operaciones numéricas tanto en CPU como en GPU, manteniendo una interfaz relativamente uniforme.

Desde el punto de vista pedagógico, PyTorch ocupa un lugar intermedio entre NumPy y Numba. Como NumPy, permite expresar operaciones sobre estructuras completas de datos. Como Numba, abre una puerta hacia aceleración y hardware más especializado. Sin embargo, su foco principal no está en escribir kernels de bajo nivel, sino en operar con tensores y delegar buena parte de la ejecución a bibliotecas optimizadas.

Un ejemplo mínimo sobre CPU puede verse así:

```python
import torch

t1 = torch.tensor([1.0, 2.0, 3.0])
t2 = torch.tensor([4.0, 5.0, 6.0])
result = t1 + t2
```

La idea general se parece a una operación vectorizada con NumPy. La diferencia importante es que PyTorch permite mover esos tensores a GPU cuando el entorno lo soporta. Por ese motivo, resulta especialmente útil en flujos de aprendizaje automático y cálculo numérico donde interesa conservar un mismo modelo de programación sobre CPU o GPU.

En esta etapa conviene leer PyTorch como una herramienta de más alto nivel que `threading`, `multiprocessing` o incluso Numba. No reemplaza el análisis del problema ni elimina la necesidad de medir, pero sí muestra que parte del paralelismo contemporáneo en Python se expresa mediante operaciones sobre tensores y no solo mediante workers explícitos.

## Errores frecuentes al paralelizar en Python

Hasta aquí el capítulo se concentró en elegir bibliotecas y patrones. Sin embargo, al trabajar con concurrencia y paralelismo también aparecen errores específicos que conviene reconocer desde una etapa introductoria.

Uno de los más conocidos es la race condition. Aparece cuando varios hilos o procesos acceden a un mismo dato compartido sin coordinación suficiente y el resultado depende del orden efectivo de ejecución. En esos casos, el programa puede producir salidas distintas entre una corrida y otra, incluso si el código fuente no cambia.

En memoria compartida, una actualización aparentemente simple como incrementar un contador puede volverse problemática si no se protege adecuadamente. Conceptualmente, el problema no está en la suma en sí, sino en que leer, modificar y escribir no siempre constituye una operación atómica.

Otro riesgo importante es el deadlock. Ocurre cuando dos o más tareas quedan esperando recursos entre sí y ninguna puede avanzar. En Python, este problema puede aparecer al combinar locks, colas, joins o recursos compartidos en un orden incorrecto.

En un nivel introductorio, conviene quedarse con tres señales de alerta:

- resultados no deterministas cuando se reutilizan datos compartidos;
- programas que terminan más lentamente de lo esperado sin mejorar con más workers;
- ejecuciones que quedan bloqueadas o no finalizan.

Reconocer estos síntomas es importante porque no todo problema de paralelismo es un problema de rendimiento. A veces el código falla primero en corrección y solo después en velocidad.

## Una mirada inicial al debugging y profiling

Debuggear programas paralelos exige observar más que el resultado final. En Python conviene empezar por preguntas sencillas:

- ¿los workers están haciendo trabajo real o permanecen ociosos?;
- ¿el tiempo se va en cómputo o en crear procesos, mover datos y sincronizar?;
- ¿el uso de CPU se distribuye entre varios cores o sigue concentrado en uno solo?;
- ¿las salidas cambian entre ejecuciones equivalentes?

En esta etapa del libro no hace falta incorporar herramientas avanzadas. Una primera aproximación razonable consiste en medir tiempos con cuidado, observar la carga de CPU del sistema y contrastar resultados entre distintas configuraciones. Ese tipo de observación ya alcanza para detectar muchos errores de diseño, por ejemplo tareas demasiado pequeñas para justificar procesos o uso de threads en problemas claramente CPU-bound.

Por ese motivo, profiling y debugging deben leerse aquí como prácticas de observación básica: medir, comparar, repetir y buscar explicaciones consistentes para el comportamiento del programa.

## Una tabla de decisión inicial

La siguiente tabla resume el criterio básico de elección para esta unidad.

| Estrategia | Conviene usarla cuando | Ventaja principal | Límite principal |
|---|---|---|---|
| `threading` | la tarea espera entrada/salida | bajo costo y buena respuesta concurrente | no acelera bien tareas CPU-bound por el GIL |
| `multiprocessing` | la tarea es CPU-bound y puede repartirse en bloques | evita el GIL | serialización y comunicación entre procesos |
| NumPy | el problema es numérico y regular sobre arreglos | vectorización eficiente | menor flexibilidad para lógica irregular |
| Numba | se quiere acelerar Python numérico sin abandonar el lenguaje | compilación JIT y paralelismo cercano al hardware | requiere código compatible y cierto cuidado con tipos y estructuras |
| PyTorch | se trabaja con tensores y se quiere conservar una vía clara hacia CPU o GPU | misma lógica general sobre distintos dispositivos | mayor peso conceptual si solo se necesita cálculo numérico simple |

Esta tabla no reemplaza la medición, pero sirve como primer filtro razonable para elegir herramientas.

## Suma paralela de un vector como caso de estudio

El programa propone la suma en paralelo de un vector como ejercicio de esta unidad. Se trata de un caso especialmente valioso porque permite comparar una versión secuencial, una versión con threads, otra con procesos y eventualmente una variante con Numba.

La importancia pedagógica del ejercicio no está solo en obtener un resultado correcto. También obliga a registrar tiempos, calcular speed-up, medir eficiencia e interpretar por qué una estrategia mejora y otra no. Precisamente ahí aparece uno de los aprendizajes más importantes del capítulo: en Python, elegir bien la herramienta suele ser más decisivo que paralelizar de manera indiscriminada.

## Criterios para interpretar resultados

Al trabajar con Python conviene mirar más que el tiempo final. Si una versión con threads no mejora, puede ser una consecuencia natural del GIL. Si una versión con procesos mejora poco, tal vez el problema sea demasiado pequeño para compensar el costo de crear procesos y mover datos. Si una versión vectorizada o compilada con Numba supera a una solución con workers explícitos, eso no contradice el paralelismo: muestra que la forma de expresar el cálculo también importa.

También conviene prestar atención a síntomas de debugging. Si los resultados cambian entre corridas, si el programa queda esperando indefinidamente o si el tiempo crece al agregar workers, es probable que el problema no sea solo de elección de biblioteca, sino de coordinación, granularidad o acceso a recursos compartidos.

Por ese motivo, este capítulo debe leerse como una preparación para el trabajo experimental del resto del libro. Lo importante no es memorizar nombres de bibliotecas, sino aprender a justificar por qué cierta estrategia resulta adecuada para cierto tipo de tarea. En ese mapa, PyTorch aparece como una vía especialmente relevante cuando el problema ya se formula en términos de tensores y cuando interesa mantener abierta la posibilidad de ejecutar sobre CPU o GPU.

El siguiente capítulo retoma este marco desde otra perspectiva: en lugar de coordinar workers explícitos, estudiará cómo la vectorización y el broadcasting permiten reformular muchos problemas numéricos para ejecutarlos de manera más eficiente. Más adelante, en el capítulo de GPU, esta línea volverá a aparecer con PyTorch y Numba como dos formas distintas de acceso a aceleración sobre dispositivo.

## Ejercicios del capítulo

### Comprensión

1. Explique por qué Python sigue siendo útil para esta materia a pesar de sus limitaciones.
2. Describa qué papel cumple el GIL en la interpretación de resultados de rendimiento.
3. Compare tareas I/O-bound y CPU-bound en relación con `threading` y `multiprocessing`.
4. Indique por qué NumPy puede ser una mejor opción que paralelizar un loop explícito en ciertos problemas.
5. Explique qué papel cumple Numba dentro del recorrido de la materia.
6. Distinga una race condition de un problema de rendimiento.
7. Explique por qué PyTorch puede leerse como una herramienta orientada a tensores y no solo como una biblioteca de aprendizaje automático.

### Aplicación

1. Diseñe una tabla de resultados para comparar una versión secuencial, una versión con threads, una versión con procesos y una versión con Numba de un mismo problema.
2. Proponga un problema I/O-bound y otro CPU-bound, e indique qué estrategia usaría en cada caso.
3. Reescriba conceptualmente un loop numérico simple en una versión vectorizada con NumPy.
4. Describa una situación en la que un programa paralelo en Python podría quedar bloqueado o producir resultados no deterministas.
5. Describa un caso en el que elegiría PyTorch en lugar de `multiprocessing` o Numba.

### Integración

1. Justifique cuál de las siguientes estrategias elegiría para un problema de suma de grandes arreglos numéricos: `threading`, `multiprocessing`, NumPy o Numba.
2. Redacte una reflexión breve sobre por qué una implementación más paralela en apariencia puede no ser la más rápida en Python.
3. Explique qué observaría primero para diagnosticar por qué una versión paralela no mejora respecto de la secuencial.