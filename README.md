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



## Episodio 2 - "Errores" históricos de los Lenguajes de Programación - Parte II

### "Error" Nro 1: Null - The Billion Dollar Mistake

Dijkstra le dijo a Tony Hoare que no incluyera null en Algol-60 porque cada soltero pasara a estar casado con la misma persona. Todas las referencias van a la misma bolsa (null).

Dejemos de rompernos las pelotas con tanta optimización. No estamos en los 60.

Las opciones para evitar el null:

* Optional<T> / Maybe
  * Funciona muy bien en Lenguajes Estáticamente tipados
  * No tan bien en Lenguajes Dinámicamente tipados
* Null Object
  * Sirve para ambos tipos de lenguajes
  * Hay que crear jerarquía de Existencia / No Existencia
* Encapsular null/nil y ofrecer mensajes de "control de flujo" particulares
  * Solo válido para lenguajes dinámicamente tipados con full closures
* GenericNil?? (No tan buena opción)
  * Si se le envía un mensaje, se devuelve el mismo
  * Utilizado en Objective-C
  * Oculta "problemas"

### "Error" Nro 2: Falta de closures /  lambdas / etc

El concepto de "función lambda" está implementado desde 1958, en Lisp.

El concepto de bloque ejecutable existe desde Agol-60 y la implementación de Dijkstra. En lenguajes bien diseñados, un bloque y un closure tienen la misma sintaxis. En lenguajes como java la sintaxis debe ser diferente.

No tener closures implica:

* Tener código repetido
* No identificar que el código es también un objeto
* No poder parametrizar código

Recordar: Closure != Puntero a Función (ejemplo C).

### "Error" Nro 3: Sintaxis distinta para Closure y Bloque

Lenguajes sin closures desde su concepción adolecen de sintaxis distinta para closures y bloques.

Problemas:

* Incosistencia
* Mayor complejidad accidental
* Los "bloques" no son objetos
* Nos acostumbramos a esta diferencia!

### "Error" Nro 4: Weak Typing

Los chequeos de tipos se categorizan en Fuerte vs Debil y Estáticamente vs Dinámicamente:

* Fuerte (Strong)
  * Estáticamente: Java, C#, Haskell
  * Dinámicamente: Smalltalk, Ruby
* Débil (Weak):
  * Estáticamente: C, C++
  * Dinámicamente: VB6, JavaScript

Hay que tener cuidado con la conversión de tipos en lenguajes estáticamente tipados débiles.

En C++ usar dynamic_cast, que es lo que Java/C# implementan por default.

La conversión explícita de tipos es "peligrosa":

* Puede generar pérdida de información
* Suele ser inconsistente
* Genera resultados inesperados

### "Error" Nro 5: Sobrecarga de Métodos a partir del tipo de Parámetros

Tener cuidado con este "feature", puede generar comportamiento inesperado y errores de compilación difíciles de entender. En Java, el no toma el tipo del objeto sino el tipo con el cual se declaro. Por ejemplo con Address y DefaultAddress, el tomaría el metodo Address si declaro la variable con el tipo del padre, a pesar de que se instancia con el hijo.

### Conclusión

Hay que mantener los lenguajes de programación simples y minimales.

Seguir el principio del menor asombro (Principle of Least Astonishment): El resultado de realizar alguna "operación" debe ser obvio, consistente y predecible, según el nombre de la "operación" y otras pistas.

Si nos equivocamos, quiero saberlo rápidamente y claramente (Que la computadora nos enseñe). Cuando no se cumple lleva a: Complejidad accidental, confusión, errores, etc.


## Episodio 3 - Nombramiento

Una medida importante para evaluar la complejidad accidental de un sistema es su simplicidad. Una persona inteligente debe ser capaz de entender el sistema en escencia.

El desarrollo de software es un trabajo de equipo. Debemos aprender a trabajar en equipo.

Malos nombres conocidos vs buenos nombres por conocer.

Muchas veces utilizamos nombramientos de una sola letra porque venimos influenciados por las matemáticas. Lo importante es que el equipo de trabajo tenga un entendimiento de los conceptos de negocio y que cada miembro nuevo pueda entender la solución por si mismo. El código debe mostrar su intención y en esto ayuda el nombramiento.

¿Qué decisión tomamos? Siempre favorecer al más débil en vez de al más inteligente. Un desarrollador inteligente quiza es capaz de deducir la intención aún si los nombres no son los mejores, pero las personas del común no. Modelar debe revelar la intención.

Cuando no sabes que nombre ponerle a algo, es porque no sabes muy bien de que estas hablando.

Estos problemas vienen de los filósofos griegos que solo diferencian entre verdad y mentira, sin embargo existen muchas verdades y muchos niveles de falsedad. Existen multiples maneras de nombrar variables correctamente.

¿Por qué pasa esto? No se hace por mala intención, sino que nos acostumbramos a los malos nombres.

Existe un code smell llamado "too clever programer" en donde algunos desarrolladores intentan que el código se vea complicado solo por ahorrarse unas lineas, pero inyectan complejidad accidental al código.

Debemos respetar los nombres del negocio. Los nombres deben mostrar su objetivo. Deben resolver una necesidad, no crearla.

“El mundo era tan reciente que muchas cosas carecían de nombre, y para nombrarlas había que señalarlas con el dedo". Gabriel Garcí­a Márquez, Cien años de soledad.

Mejor poner nombres sin significado que malos nombres.

No hablemos de buenos o malos nombres. Hablemos que mejores y peores nombres. Mejores/más utiles/descriptivos que otros.

Debemos nombrar las cosas para coincidir con el concepto. Hay nombres que capturan algo que ya existia y otros que proyectan lo que vamos a construir.

Programar es un acto lingüístico, más allá de lo técnico y tecnólogico. Constantemente nos estamos comunicando al programar. Tiene caracteristicas lingüísticas que se viven cotidianamente.

Hay un factor super importante que es el tiempo. En un momento de la historia un nombre puede ser bueno y en otro malo. Debemos hacer explicito el paso en el tiempo.

Un nombre puede ser bueno en una comunidad y en un contexto especifico. Debe permitir comunicarnos de manera clara. No necesariamente es el mejor nombre pero si puede ser bueno.

El nombramiento es fundamental en el proceso de aprendizaje que se realiza en conjunto (en equipo).

Nietzsche ya lo dijo en más allá del bien y del mal, construimos nuestra propia moral y la plasmamos a la hora de nombrar variables.

Criterios para saber un buen nombre:
* La palabra utilizada debe ser neutra. No localizado (no programar en Colombiano). Obviamente depende del dominio. Programar un software para la legislación colombiana en inglés no tiene sentido. 
* No debe ser excesivamente largo. Puede ocurrir typos al escribirlo. Si es largo, ya no es una sintesis. No es un problema con los IDEs actuales. Una cosa es un texto largo y otra cosa es un texto que acople 3 o 4 conceptos. Evitar: AgendaControllerManagerUtil... etc.
* No extiende excesivamente el léxico. Debe hacer match con el dominio. No extenderlo mas allá del dominio.

Las cosas no son solo blanco o negro.

Cuando agregamos capas de abastracción se vuelve complejo mantener la representatividad. Una sobre-generalización.

Algunas escuelas filosoficas mencionan que no solo nombrando conoces, nombrando creas/descubres, expandes el mundo. Cada que crear un nombre construimos la realidad. En software quizá no es tan así porque estamos modelando.

Si no encontramos el nombre de negocio ideal para una variable, debemos usar metaforas o analogias para nombrar los objetos del dominio, mapear los conceptos del dominio. Evitar siempre los Service, Manager, Util, Controller, Helper, etc.

Usar un idioma que no domino para programar representa un reto cultural grande.

Nombramos objetos y utilizamos variables para representarlos.

Debemos evitar poner el nombre del patron de diseño al nombrar. Muchas veces los patrones son conceptos de implmentación, no del dominio. Los patrones son propuestas abstractas y la implementación se la damos nosotros. No debemos guiar nuestro diseño a partir del patrón. Debemos capturar la intención del patrón porque hay muchos que son muy parecidos. Nos dieron un nuevo vocabulario, podemos hablar de manera más abstracta de las soluciones que estamos creando.

Al nombrar con el patron de diseño, este estructura nuestro código. Muchos lenguajes de programación cometen este error y terminando adaptandonos a lo técnico y no al dominio. Lo técnico termina influyendo nuestro modelo e incluso crea conceptos que no representan nada: POJO, DTO, Bean, etc.

Nos concentramos en hablar de los patrones y de como implementarlos en lugar de hablar del dominio y de como modelarlo.

Las interfaces es más facil nombrarlas con el Rol que representa.

### Conclusión

* Nombrar los objetos en base al rol que tienen en el contexto en el que se los esta nombrando
* Usar nombres de dominio del problema
* Evitar nombres técnicos o basados en el tipo del objeto
* Evitar nombres de mensajes basados en la implementación


## Episodio 4 - Default Parameters o un poco de diversión

Todos los parámetros deben ser explícitos. El problema con los parámetros defaults es que no se sabe de manera explícita cuales son los valores por default y te obliga a cambiar de contexto. Crea mucho acoplamiento.

### Errores históricos: Clases que no son objetos

Los métodos de clase (estáticos) en Java son meramente funciones, se sale del mundo de objetos. Para tratar clases como objetos, solo se puede mediante vía meta-programación y sigue sin estar en el mundo de objetos.

Las clases no solo sirven para crear instancias, también debe representar comportamientos asociados al concepto que no pertenecen a una única instancia.

A veces se escoge conocimiento de palabra sobre semántica.

* No puedo usar polimorfismo a nivel clase
* No hay self/this
* No hay super
* Método static no es objetos!!
* Puedo simularlo con Meta-programación, pero todo es un lio

### Acoplamiento con Clases

Los parámetros no deben estar acoplados a un tipo sino a los mensajes que deben responder. Es una forma de romper acoplamiento.

En java, cuando tengo un acoplamiento debo crear una nueva abstracción (ejemplo LocalDate vs Clock).

* Referencias a clases generan acoplamiento
  * A la implementación
  * A un recurso externo
* En lenguajes estáticos es peor aún si las clases no son objetos.

¿Por qué en Java las clases no son objetos? Seguramente no entendían el metamodelo de Smalltalk.

### Singleton

Cumple 2 funciones: Asegurar una única instancia y Proveer un punto global de acceso a este (tomado del libro de patrones).

La mayoría de veces se usa solo como punto de acceso porque no existe un contexto global.

¿Por qué pretendemos una única instancia de una clase? En la realidad no existen cosas únicas, por lo que el Singleton en realidad no tiene mucho sentido.

* Si es Singleton, que no se note (a la Smalltalk, modificar el new)
* No hay que confundir Singleton con "variables globales"
* Un Singleton no me permite usar objetos polimórficos
* Si existe el mensaje "setInstance" no es Singleton
* Dependency Injection
  * Problema forzado por frameworks
  * No tiene ningún sentido usar frameworks de dependency injection

La inyección de dependencias es una solución a un problema inexistente. ¡El problema es absurdo! ¡¡Al final es solo parametrizar!! 

La gente descubre el martillo y piensa que todos los problemas son clavos. Debemos evitar ser víctimas de las modas.

Debemos evitar los Singleton siempre que podamos.

### Métodos largos

Dificultan la comprensión y el mantenimiento.

Es muy importante conocer las herramientas de refactoring automatizado que provee el IDE para mejorar el código. Correr los test en los refactors manuales.

**Al darle significado a cada una de las partes se obtiene algo más abstracto que es fácil de entender**. Se oculta información que impide ser reutilizada (Por ejemplo, con un template method).

Refactorizar sirve para descubrir semánticamente que hace un método.

Un método debe tener pocas líneas, no debe tener tantas colaboraciones.

* Dificultan la comprensión
* No me dejan ver el QUÉ
* No me dejan ver la posibilidad de reúso

### Conclusiones

* No acoplarse a clases
* No usar Singletons
* No usar frameworks de Dependency Inyection, modelar bien!
* Tener métodos cortos y bien declarativos

## Episodio 5 - Testing en la UI

Normalmente los frameworks de frontend tienen ejemplos en donde nos venden la herramienta. No se preocupan por el diseño del software, solo por mostrar las características que tiene. Como consecuencia, muchos desarrolladores en frontend terminan creando código con mucha complejidad accidental.

El principal problema que tiene el código que se acopla al framework es la testeabilidad. La lógica de negocio debe ser independiente y fácil de testear.

Debemos buscar nombres a los objetos que vamos a utilizar, no implementar objetos in the fly (jsons) también llamados nameless objects. Porque si no no podemos nombrarlos y reflexionar sobre ellos.

Evitemos el acoplamiento al framework, quizá algún día necesitemos cambiar el framework o la librería.

Que el lenguaje te permita romper el encapsulamiento no significa que debamos hacerlo.

NO estamos obligados a cometer los mismos errores que otros

Debemos modelar nuestro negocio siempre. Eso marca la diferencia entre aplicar scripting y crear un sistema mantenible.

RES, del latín: cosa. Reificar darle a algo entidad de cosa. En objetos, hacer objeto una cosa de la realidad.

Debemos hacer cosas que nos causen placer estético. Ayuda para la creatividad y motivación. El admirar lo que uno hace te hace trabajar mejor y nos ayuda en la métrica de belleza.

La belleza se puede entender con la habitabilidad del software. Que tan fácil y simple es convivir con este. No estar peleando con el sistema.

Pensar en cuanta disonancia cognitiva me produce mirar el código (qué tan difícil es mirarlo un rato y entender que hace sin que te canse mentalmente).

Mientras menos código tenga en la configuración del framework, mejor. Menos errores, más fácil de testear.

Si un framework te limita en algo, no lo uses. Vas a terminar agregando complejidades. No podemos reducir la calidad del diseño solo por limitaciones tecnológicas. En caso de que sea obligatorio, podemos agregar otra capa de abstracción (quizá un proxy) que permita la comunicación con la librería.

En vez de usar DTOs, podemos mandar objetos sobre la red. Se puede tener el mismo objeto distribuido (replicado) en varios servidores y en el front.

Un objeto debe ser inmutable si lo que está representando es inmutable. Normalmente debemos preferir los objetos inmutables. Este no es un concepto de la programación funcional, objetos puede trabajar de manera inmutable (lo aconsejable).

Debemos modelar el negocio y desacoplar todo de la UI. Programar en back y front es igual!! Solo debemos diseñar bien el código. 

El dominio periférico (técnico) se modela diferente en front y back ya que cada uno tiene sus conjuntos de problemas a resolver. Es importante saber el dominio en el cual estoy para saber que voy a programar.

Debemos separar el dominio de objetos con las bases de datos. Son completamente distintos. Empezando porque las relaciones son inversas. En objetos, un carrito conoce sus productos, en el mundo de DB relacional, un producto conoce a cuál carrito pertenece.

### Conclusiones

* El problema de testear en la UI es conceptualmente el mismo que testear en el back
* La diferencia es que la UI "se ve", el back "no se ve"
* Otra diferencia es el uso de frameworks. Los frameworks de UI son más intrusivos que los del back
* La solución es la misma: No dejar que el framework se meta en tu modelo de negocio
