# Conclusión general

Este libro recorrió una idea central del desarrollo web frontend: una interfaz no aparece resuelta de una sola vez, sino por capas que se apoyan entre sí. Primero fue necesario comprender qué es la web, cómo circula la información y por qué los estándares importan. Luego apareció HTML como estructura del contenido, CSS como herramienta para construir presentación visual, responsive design y accesibilidad como criterios de calidad, y JavaScript como lenguaje para incorporar lógica, manipulación del documento e interacción.

## Objetivos de cierre e integración

- revisar el recorrido completo como un sistema articulado y no como una lista de temas aislados;
- identificar qué capacidades mínimas debería consolidar una primera cursada de frontend;
- integrar estructura, estilos, accesibilidad, lógica, DOM e interacción en un proyecto breve;
- reconocer próximos temas de estudio sin perder de vista la base construida.

Visto en conjunto, el recorrido no trata solamente de aprender etiquetas, propiedades o métodos aislados. El objetivo de fondo es adquirir una manera de pensar problemas frontend. Eso implica tomar decisiones de estructura, nombrar con claridad, separar responsabilidades, detectar repeticiones, validar supuestos, observar el comportamiento real de una interfaz y corregirla cuando algo falla.

También importa sostener una mirada amplia sobre la diversidad de la web. Las personas no navegan todas de la misma manera, no usan los mismos dispositivos ni las mismas condiciones de acceso. Por eso desarrollar bien no es solo “hacer que funcione” en una situación ideal, sino construir soluciones suficientemente claras, robustas y adaptables para distintos contextos.

El proyecto del supermercado funcionó como hilo conductor porque permitió pasar de la teoría a un problema concreto: estructurar páginas, darles estilo, mejorar accesibilidad, reorganizar código, procesar datos, renderizar contenido y responder a acciones del usuario. Ese tipo de práctica es importante porque acerca el aprendizaje a la forma en que realmente se trabaja en desarrollo web.

Con esta base ya debería ser posible leer y producir pequeños proyectos frontend con más criterio, entender mejor qué hace cada tecnología y seguir avanzando hacia temas más complejos. Esa base no convierte automáticamente a nadie en especialista, pero sí ofrece un punto de partida sólido para encarar problemas reales con un lenguaje técnico más preciso y una mejor capacidad de análisis.

En términos curriculares, este recorrido corresponde a una primera etapa. Aquí el foco estuvo en comprender cómo se construye una interfaz desde sus fundamentos: estructura, presentación, accesibilidad, lógica básica e interacción en el navegador.

Un paso siguiente natural, ya fuera del alcance de esta etapa, sería profundizar en consumo de APIs, almacenamiento local, organización modular del código, herramientas de build y enfoques más avanzados de desarrollo frontend. También sería razonable avanzar hacia prácticas más sistemáticas de validación, debugging y mantenimiento. En otras palabras: este libro no agota el campo del frontend, pero sí busca dejar una plataforma confiable para seguir aprendiendo y continuar el recorrido en una materia posterior.

## Rúbrica orientativa para el proyecto integrador

La siguiente rúbrica sirve como guía para evaluar una primera versión del proyecto del supermercado. No reemplaza la devolución docente cualitativa, pero ayuda a explicitar qué dimensiones conviene observar al revisar una entrega.

| Criterio | Logro inicial | Logro esperado | Logro sólido |
| :---- | :---- | :---- | :---- |
| Estructura HTML | La página funciona, pero la estructura es confusa o poco semántica. | La estructura principal está bien resuelta y usa etiquetas adecuadas en la mayor parte del documento. | La estructura es clara, semántica y consistente en todas las pantallas. |
| CSS y presentación | Hay estilos básicos, pero con poca jerarquía visual o baja consistencia. | La interfaz presenta una identidad visual reconocible, ordenada y legible. | La interfaz es consistente, clara, responsive y con buen criterio de organización del CSS. |
| Accesibilidad y responsive | Hay intentos parciales, pero persisten problemas de foco, contraste o adaptación. | La interfaz funciona razonablemente bien en pantallas pequeñas y contempla criterios básicos de accesibilidad. | La interfaz integra de forma sólida accesibilidad, foco visible, labels correctos, contraste y adaptación responsive. |
| JavaScript y lógica | Hay interacciones mínimas, con errores de organización o poca claridad. | El código resuelve validaciones, renderizado o eventos de forma comprensible. | El código está bien nombrado, separado por responsabilidades y resuelve interacciones con mayor robustez. |
| Integración general | Las partes existen, pero se perciben desconectadas entre sí. | HTML, CSS y JavaScript se articulan correctamente en una experiencia coherente. | La integración es consistente, justificada y muestra criterio técnico en las decisiones tomadas. |

## Criterios mínimos de entrega del integrador

Como referencia práctica, una entrega inicial del proyecto debería incluir al menos:

- una página de carga de producto con formulario legible;
- una ficha de producto con estructura clara y contenido relevante;
- una página de listado con más de un producto visible;
- estilos consistentes entre las tres pantallas;
- al menos una mejora responsive y una mejora explícita de accesibilidad;
- una interacción en JavaScript, por ejemplo validación, búsqueda o renderizado de datos.

## Ejercicios finales de integración

### Comprensión

1. Explique cómo se relacionan HTML, CSS y JavaScript dentro de una interfaz web.
2. Describa por qué accesibilidad y responsive design no deberían tratarse como agregados posteriores.
3. Explique qué aprendizaje le parece más importante del recorrido general del libro y por qué.

### Aplicación

1. Revise un pequeño proyecto propio o de práctica y describa qué decisiones corresponden a estructura, cuáles a presentación y cuáles a interacción.
2. Escriba una autoevaluación breve indicando qué temas del libro maneja con más seguridad y cuáles necesitaría practicar más.

### Integración

1. Diseñe y construya una versión inicial del proyecto del supermercado que combine una página de listado, una ficha de producto y un formulario de carga. El objetivo no es resolver un sistema completo, sino integrar con criterio estructura HTML, estilos CSS, validaciones básicas, manipulación del DOM y respuesta a eventos.
