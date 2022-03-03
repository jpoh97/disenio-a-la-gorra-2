# Diseño a la gorra - temporada 2
## Episodio 1 - "Errores" históricos de los Lenguajes de Programación - Parte I

Cuando encontramos errores buscamos en los puntos que menos conocemos.

Para evitar errores al diseñar solucaciones, debemos seguir el principio del menor asombro (Principle Of Least Astonishment): El resultado de realizar alguna operación debe ser obvio, consistente y predecible, según el nombre de la operación y otras pistas. Cuando no se cumple tenemos Complejidad Accidental, Confusión, Errores, etc.

### "Feature" Nro 1: Definición Automática de Variables

* Definición/Declaración de Variable: Se indica al compilador que se define una variable para su uso.
* Inicialización de Variable: Asignación inicial de un valor a una variable
* Definición Automática: Definición + Inicialización. Poco cohesivo

Closure (funciones anonimas, funciones lambda, etc) es un objeto que representa codigo. No se le da nombre a ese objeto. Son metodos que no estan asociados a una clase. Se bindean al contexto de ejecucion en el cual se instancia. Nos permite en programacion funcional, pasar funcionalidad como parametro.

Con los closures toca tener variables con definicion explicita y no implicita para evitar problemas de contexto. Se evita complejidad accidental.

Solución: Definición explícita de variable

* Definición Automática de Variables:
  * Pros:
    * Escribir menos
  * Cons:
    * Propenso a error por errores de tipeo
    * Complejidad accidental al momento de combinarlo con closures
    * Definición dependiente de flujo de ejecución
    * Pensado para escribir menor no para leer menos -> Bueno para scripting, no para sistemas grandes
  * Importancia de soporte del IDE
  * Impotancia de tener tests que cubran todo el código

* Definición Explícita de Variables:
  * Pros:
    * No hay posibilidad de error por errores de tipeo
    * Sin complejidaad accidental cuando se usa con closures
    * La definición no depende del flujo de ejecución
  * Cons:
    * Hay que tipear más (No con IDE)
    * Acordarse de borrar definición cuando no se use más (No con IDE)

### "Feature" Nro 2: Binding Dinámico de Variable

El binding dinamico es una muy mala idea porque se ejecuta en el orden en que se definen. Con el binding lexicográfico se soluciono este error.

### Error (no feature) Nro 3: this en JavaScript

El this en javascript no se bindea con lo que uno espera (en las inner function). Si se utiliza el "use strict" varia su comportamiento (sin este, el this se vuelve global). Se solucionó con las arrow functions.

### "Feature" Nro 4: (ab)Uso de diccionarios/hashes/etc

Cuando se definen objetos como maps o diccionarios, se pierden las ventajas del mundo de objetos. Primitive obsetion. Se vuelve programacion estructurada, se rompe el encapsulamiento. El principal problema es que no se le asigna un nombre, no se conceptualiza (falta de concepto y abstracción) y cada desarrollador termina asignando su nombre. La ventaja principal del encapsulamiento es que se limita el error a los objetos. Evitar los nameless objects.

* Motivación: Poder "Scriptear rápidamente"
* Nuevamente se prioriza "escribir rápido" sobre lectura y comprensión
* No es un error nuevo: Ver "Don't use arrays?" Mayo 1993 Smalltalk Report
* Cons:
  * Dificulta la comunicación
  * Dificulta el pensamiento
  * Genera código repetido
  * Se pueden generar fácilmente objetos distintos por errores de tipeo
  * No soporta correctamente herramientas de refactoring como rename
  * Hace la programación y mantenimiento más difícil
  * En definitiva, cuesta más dinero

### "Feature" Nro 5: No chequeo de Acceso a Arrays

Un error que viene derivado de C es el no chequeo de bounds de arrays. Se hizo para reducir runtime. El error de C (busca al siguiente puntero en ciclos) ocurre solo en lenguajes que no tienen un garbage collector.

* Motivación: Performance (hay que situarse en la década del 60/70)
* ¿Actualmente es realmente un problema el performance?
* Imposible de mantener en un lenguaje con "con memoria administrada"

### Conclusiones

* Los lenguajes de programación son hechos por seres humanos, por lo tanto tienen errores
* Cambiar un lenguaje de programación es muy difícil por la compatibilidad hacia atrás
* Hay temas de ego en la modificación de los lenguajes de programación ("prefiero seguir con mi idea hasta el final!")
* Los lenguajes de programación son un sistema complejo con mucho acoplamiento. Cambios que pueden parecer features suelen terminar generando más problemas que soluciones
* Hay que ser crítico con los features que aparecen constantemente
* Los lenguajes de programación "tienen" que estar sacando nuevos features constantemente porque sino no venden
* Es un tema comercial no técnico generalmente

Alan Kay no queria que Smalltalk se hiciera publico para que no se viera como un producto (comercial). Evitar problemas de mantener compatibilidad hacia atrás.

"Premature optimization is the root of all evil" Donald Knuth

"Premature optimization is the root of all evil in programming" Tony Hoose

Cuanto mas simple sea el lenguaje es mas facil hacer la evolución. Que el core sea pequeño y las funcionalidades se agreguen como librerias.

Somos los seres humanos los que mas nos cuesta cambiar!

El software es un modelo, el desarrollo de software es el proceso de modelar. Lo mas importante en ese proceso es el aprendizaje y lo importante es que las herramientas que utilicemos nos ayuden a aprender.

Cambiar de un lenguaje no es solo sintaxis, es sintaxis y semantica!