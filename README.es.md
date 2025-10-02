# Cognitive load is what matters

[Prompt](https://github.com/zakirullin/cognitive-load/blob/main/README.prompt.md) | [Blog version](https://minds.md/zakirullin/cognitive) | [Chinese](https://github.com/zakirullin/cognitive-load/blob/main/README.zh-cn.md) | [Korean](README.ko.md) | [Turkish](README.tr.md) | [Japanese](README.ja.md)  | [Spanish](README.es.md)

<!-- *It is a living document, last update: **September 2025.** Your contributions are welcome!* -->

*Este es un domento vivo, ultima actualizacion: **Septiembre 2025**.  ¡Tus contribuciones son bienbenidas!*

<!-- ## Introduction  -->

## Introduccion

<!-- There are so many buzzwords and best practices out there, but most of them have failed. They failed because they were imagined, not real. These ideas were based on aesthetics and subjective judgments. We need **something** more fundamental, something that can't be wrong. -->

Existen numerosos términos y prácticas que se ponen de moda, pero la gran mayoría de ellos fracasan en su cometido. Fallan porque son concebidos como imaginarios, no como reales. Estas ideas están basadas en juicios estéticos y subjetivos. Por ello, se hace necesario algo más fundamental, algo que no pueda estar errado

<!-- Sometimes we feel confusion going through the code. Confusion costs time and money. Confusion is caused by high *cognitive load*. It's not some fancy abstract concept, but rather **a fundamental human constraint.** It's not imagined, it's there and we can feel it. -->

A veces podemos sentir mucha confusion mientras leemos codigo. Confuncion que cuesta tiempo y dinero. Confusin causado por la *carga cognitiva.* No se trata de algun concepto bastracto y/o sofisticado, sino mas bien un **limite muy humano.** Y no es imaginario, es algo que realmente podemos sentir.

A veces, al revisar el código, se puede sentir mucha confusión. Esta confusión, que cuesta tiempo y dinero, es causada por la alta *carga cognitiva*. No se trata de un concepto abstracto y/o sofisticado, sino más bien de un **límite muy humano.** La carga cognitiva no es imaginaria; es algo que realmente se puede sentir.

<!-- Since we spend far more time reading and understanding code than writing it, we should constantly ask ourselves whether we are embedding excessive cognitive load into our code. -->

Dado que se invierte más tiempo leyendo y tratando de entender el código del que se emplea escribiéndolo, se debería cuestionar constantemente si se está generando una carga cognitiva excesiva en el código que se desarrolla.

<!-- ## Cognitive load  -->

## La Carga Cognitiva

<!-- > Cognitive load is how much a developer needs to think in order to complete a task. -->
> La carga cognitiva se refiere a la cantidad de esfuerzo mental que un desarrollador necesita para completar una tarea.

<!-- When reading code, you put things like values of variables, control flow logic and call sequences into your head. The average person can hold roughly [four such chunks](https://github.com/zakirullin/cognitive-load/issues/16) in working memory. Once the cognitive load reaches this threshold, it becomes much harder to understand things. -->

Cuando se lee el código, se colocan elementos como valores, variables, controles de flujo, lógica y llamados de secuencia en la mente. La persona promedio puede retener aproximadamente unos [c](https://github.com/zakirullin/cognitive-load/issues/16)[cuatro elementos ](https://github.com/zakirullin/cognitive-load/issues/16) en su memoria de trabajo. Una vez que la carga cognitiva excede un determinado límite, se vuelve muy difícil entender ciertas cosas.

<!-- *Let's say we have been asked to make some fixes to a completely unfamiliar project. We were told that a really smart developer had contributed to it. Lots of cool architectures, fancy libraries and trendy technologies were used. In other words, **the author had created a high cognitive load for us.*** -->

*Digamos que se solicita realizar correcciones a un proyecto con el que no se está familiarizado. Se informa que un desarrollador realmente inteligente ha contribuido al mismo. Se utilizaron una gran cantidad de arquitecturas geniales, librerías sofisticadas y tecnologías de punta. En síntesis, **el autor ha creado una enorme carga cognitiva para nosotros.***

<div align="center">
  <img src="/img/cognitiveloadv6.png" alt="Cognitive load" width="750">
</div>

<!-- We should reduce the cognitive load in our projects as much as possible. -->

Deberíamos reducir la carga cognitiva en nuestros proyectos en la medida posible.

<!-- <details>
  <summary><b>Cognitive load and interruptions | Carga cognitiva e interrupciones</b></summary>
  <div align="center">
    <img src="img/interruption.jpeg" width="480">
  </div>
</details> -->

<details>
  <summary><b>Carga cognitiva e interrupciones</b></summary>
  <div align="center">
    <img src="img/interruption.jpeg" width="480">
  </div>
</details>

<!-- > We are going to use "cognitive load" in an informal sense; sometimes it lines up with the specific scientific concept of Cognitive Load, but we don't know enough about where it does and doesn't match. -->

> Vamos a utilizar el término "carga cognitiva" en un sentido informal; a veces coincide con el concepto científico específico de Carga Cognitiva, pero no conocemos con precisión en qué aspectos coinciden y en cuáles no.
>

<!-- ## Types of cognitive load  -->

## Tipos de carga cognitiva

<!-- **Intrinsic** - caused by the inherent difficulty of a task. It can't be reduced, it's at the very heart of software development. -->

**Intinseca** - causada por la dificultad inherente a la tarea. No puede ser reducida, ya que constituye el núcleo fundamental del trabajo de un ingeniero de software

<!-- **Extraneous** - created by the way the information is presented. Caused by factors not directly relevant to the task, such as smart author's quirks. Can be greatly reduced. We will focus on this type of cognitive load. -->

**Extrinseca** - creada por la forma en que la información es presentada. Es causada por factores que no están directamente relacionados con la tarea, como los caprichos de un autor que se siente particularmente inteligente. Puede reducirse considerablemente. Nos enfocaremos en este tipo de carga cognitiva.

<!-- <div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="Intrinsic vs Extraneous | Intinseca vs Extrinseca" width="600">
</div> -->

<div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="Intinseca vs Extrinseca" width="600">
</div>

<!-- Let's jump straight to the concrete practical examples of extraneous cognitive load. -->

Vamos directamente a ejemplos concretos de Carga Cognitiva Extrínseca

---

<!-- We will refer to the level of cognitive load as follows:`🧠`: fresh working memory, zero cognitive load `🧠++`: two facts in our working memory, cognitive load increased `🤯`: cognitive overload, more than 4 facts -->

Nos vamos a referir a los niveles de carga cognitiva como sigue: `🧠`: memoria de trabajo fresca, sin carga cognitiva `🧠++`: al menos dos datos en nuestra memoria de trabajo, carga cognitiva moderada `🤯`: sobrecarga cognitiva, más de 4 datos

Nos vamos a referir a los niveles de carga cognitiva como sigue: `🧠`: memoria de trabajo fresca, sin carga cognitiva`🧠++`: al menos dos datos en nuestra memoria de trabajo, carga cognitiva moderada`🤯`: sobrecarga cognitiva, más de 4 datos.

<!-- > Our brain is much more complex and unexplored, but we can go with this simplistic model. -->

> Nuestro cerebro es mucho más complejo de lo que creemos y está, en su mayoría, inexplorado, pero podemos trabajar con este modelo simplista.

**Nota sobre los ejemplos de Código**: En los ejemplos de código, se mantendrá la convención de nombres de variables, funciones, métodos, etc., en inglés, mientras que los comentarios explicativos sí serán traducidos al español.

<!-- ## Complex conditionals -->

## Condicionales complejas

<!-- ```go
if val > someConstant // 🧠+
    && (condition2 || condition3) // 🧠+++, prev cond should be true, one of c2 or c3 has to be true
    && (condition4 && !condition5) { // 🤯, we are messed up by this point
    ...
}
``` -->

```go
if val > someConstant // 🧠+
    && (condition2 || condition3) // 🧠+++, la condición anterior debe ser verdadera, y una de las condiciones C2 o C3 también debe ser verdadera
    && (condition4 && !condition5) { // 🤯, Estamos completamente perdidos en este punto.
    ...
}
```

<!-- Introduce intermediate variables with meaningful names: -->

Utilice variables intermedias con nombres descriptivos:

<!-- ```go
isValid = val > someConstant
isAllowed = condition2 || condition3
isSecure = condition4 && !condition5
// 🧠, we don't need to remember the conditions, there are descriptive variables
if isValid && isAllowed && isSecure {
    ...
}
``` -->

```go
isValid = val > someConstant
isAllowed = condition2 || condition3
isSecure = condition4 && !condition5
// 🧠 No necesitamos memorizar las condiciones, existen variables descriptivas de la evaluacion.
if isValid && isAllowed && isSecure {
    ...
}
```

<!-- ## Nested ifs  -->

## Ifs Anidados

<!--
```go
if isValid { // 🧠+, okay nested code applies to valid input only
    if isSecure { // 🧠++, we do stuff for valid and secure input only
        stuff // 🧠+++
    }
}
``` -->

```go
if isValid { // 🧠+, el código anidado solo se aplica a entradas válidas
    if isSecure { // 🧠++, solo realizamos acciones con entradas de datos válidas y seguras
        stuff // 🧠+++ [1]
    }
}
```

<!-- Compare it with the early returns: -->

Comparemos con el código anterior:

<!-- ```go
if !isValid
    return

if !isSecure
    return

// 🧠, we don't really care about earlier returns, if we are here then all good

stuff // 🧠+
``` -->

```go
if !isValid
    return

if !isSecure
    return

// 🧠, ya no nos importa la logica previa de validacion; si estamos aquí, todo está bien.

stuff // 🧠+
```

<!-- We can focus on the happy path only, thus freeing our working memory from all sorts of preconditions. -->

De este modo nos enfocamos únicamente en el escenario ideal, liberando así nuestra memoria de trabajo de todo tipo de condicionamientos previos.

<!-- ## Inheritance nightmare -->

## La Pesadilla de la Herencia

<!-- We are asked to change a few things for our admin users: `🧠` -->

Digamos que nos solicitan algunos cambios para nuestros usuarios administradores: 🧠

`AdminController extends UserController extends GuestController extends BaseController`

<!-- Ohh, part of the functionality is in `BaseController`, let's have a look: `🧠+` -->

¡Ah!, parte de nuestra funcionalidad está en `BaseController`,echemos un vistazo: `🧠+`

<!-- Basic role mechanics got introduced in `GuestController`: 🧠++ -->

Las mecánicas básicas de los roles se introdujeron en `GuestController`: 🧠++

<!-- Things got partially altered in `UserController`: `🧠+++ ` -->

Las cosas cambiaron parcialmente en UserController: `🧠+++`
<!-- Finally we are here, `AdminController`, let's code stuff! `🧠++++` -->
Finalmente estamos aquí, `AdminController`, ¡vamos a codear! 🧠++++

<!-- Oh, wait, there's `SuperuserController` which extends `AdminController`. By modifying `AdminController` we can break things in the inherited class, so let's dive in `SuperuserController` first: `🤯 ` -->

¡Un momento!, existe el controlador `SuperuserController` que hereda de `AdminController`. Si modificamos `AdminController`, podríamos causar problemas en la clase heredada, así que primero analicemos `SuperuserController`: 🤯

<!-- Prefer composition over inheritance. We won't go into detail - there's [plenty of material](https://www.youtube.com/watch?v=hxGOiiR9ZKg) out there. -->

Es preferible utilizar la composición en lugar de la herencia. No vamos a entrar en detalles; hay mucha información disponible [aquí](https://www.youtube.com/watch?v=hxGOiiR9ZKg).

<!-- ## Too many small methods, classes or modules -->

## Demasiados métodos, clases y/o módulos pequeños

<!-- > Method, class and module are interchangeable in this context -->

> En este contexto, los términos método, clase y módulo son intercambiables.

<!-- Mantras like "methods should be shorter than 15 lines of code" or "classes should be small" turned out to be somewhat wrong. -->

Resultó que principios como "los métodos deben tener menos de 15 líneas de código" o "las clases deben ser pequeñas", eran en cierto modo erróneos.

<!-- **Deep module** - simple interface, complex functionality -->

**Modulo Profundo** - interfaz simple, funcionalidad compleja.

<!-- **Shallow module** - interface is relatively complex compared to the small functionality it provides -->

**Modulo de funcionalidad limitada** - la interfaz es relativamente compleja comparada a la funcionalidad relativamente simple que provee.

<div align="center">
  <img src="/img/deepmodulev8.png" alt="Deep module" width="700">
</div>

<!-- Having too many shallow modules can make it difficult to understand the project. **Not only do we have to keep in mind each module's responsibilities, but also all their interactions.** To understand the purpose of a shallow module, we first need to look at the functionality of all the related modules. Jumping between such shallow components is mentally exhausting, `<a target="_blank" href="https://blog.separateconcerns.com/2023-09-11-linear-code.html">`linear thinking `</a>` is more natural to us humans. -->

El tener muchos pequeños módulos puede dificultar el entender un proyecto. **No solo tenemos que mantener en mente cada una de las responsabilidades, sino además cada una de sus interacciones.** Para poder entender el propósito de un módulo con poca funcionalidad necesitamos mirar todas las funcionalidades asociadas de todos los módulos asociados. Navegar entre tantos módulos pequeños puede resultar mentalmente agotador, el <a target="_blank" href="https://blog.separateconcerns.com/2023-09-11-linear-code.html">pensamiento lineal </a> nos resulta más cómodo y natural.

<!-- > Information hiding is paramount, and we don't hide as much complexity in shallow modules. -->

> La encapsulacion de información es fundamental, y no intentamos ocultar mucha complejidad en módulos más simples.

<!-- I have two pet projects, both of them are somewhat 5K lines of code. The first one has 80 shallow classes, whereas the second one has only 7 deep classes. I haven't been maintaining any of these projects for one year and a half. -->

Tenía dos proyectos personales, ambos con aproximadamente 5k líneas de código. El primero tenía unas 80 clases sencillas, mientras que el segundo solo tenía 7 clases complejas. No había realizado ningún mantenimiento en ninguno de estos proyectos durante el último año y medio.

<!-- Once I came back, I realised that it was extremely difficult to untangle all the interactions between those 80 classes in the first project. I would have to rebuild an enormous amount of cognitive load before I could start coding. On the other hand, I was able to grasp the second project quickly, because it had only a few deep classes with a simple interface. -->

Una vez que los retomó, se dio cuenta de que era extremadamente difícil comprender todas las interacciones entre las 80 clases del primer proyecto. Tendría que volver a aprender una gran cantidad de conceptos antes de poder empezar a programar. Por otro lado, el segundo proyecto fue fácil de entender, ya que solo tenía unas pocas clases complejas con una interfaz sencilla.

> Los mejores componentes son aquellos que ofrecen una funcionalidad potente pero con una interfaz sencilla.
>
> *John Ousterhout, A Philosophy of Software Design (Una filosofía del diseño de software)*

<!-- The interface of the UNIX I/O is very simple. It has only five basic calls: -->

La interfaz de I/O de UNIX es muy simple. Solo tiene cinco llamadas básicas:

```python
open(path, flags, permissions)
read(fd, buffer, count)
write(fd, buffer, count)
lseek(fd, offset, referencePosition)
close(fd)
```

<!-- A modern implementation of this interface has **hundreds of thousands of lines of code.** Lots of complexity is hidden under the hood. Yet it is easy to use due to its simple interface. -->

Una implementación moderna de esta interfaz cuenta con **cientos de miles de líneas de código**. A pesar de su gran complejidad interna, su interfaz sencilla la hace muy fácil de usar.

<!-- > This deep module example is taken from the book [A Philosophy of Software Design](https://web.stanford.edu/~ouster/cgi-bin/book.php) by John Ousterhout. Not only does this book cover the very essence of complexity in software development, but it also has the greatest interpretation of Parnas' influential paper [On the Criteria To Be Used in Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf). Both are essential reads. Other related readings: [A Philosophy of Software Design vs Clean Code](https://github.com/johnousterhout/aposd-vs-clean-code), [It's probably time to stop recommending Clean Code](https://qntm.org/clean), [Small Functions considered Harmful](https://copyconstruct.medium.com/small-functions-considered-harmful-91035d316c29). -->

<!-- Nota interna: Seria bueno tener titulo de traducciones de los recusos de abajo o en su defecto una traduccion de los titulos -->

> El ejemplo de módulo complejo es extraído del libro  [A Philosophy of Software Design](https://web.stanford.edu/~ouster/cgi-bin/book.php) por John Ousterhout. No solo aborda la esencia de la complejidad en el desarrollo de software, sino que ofrece la mejor interpretacion del influyente artículo de Parnas titulado [On the Criteria To Be Used in Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf). Ambas son lecturas escenciales.Otras lecturas relacionada pueden ser: [A Philosophy of Software Design vs Clean Code](https://github.com/johnousterhout/aposd-vs-clean-code), [It&#39;s probably time to stop recommending Clean Code](https://qntm.org/clean), [Small Functions considered Harm](https://copyconstruct.medium.com/small-functions-considered-harmful-91035d316c29)

<!-- <details>
    <summary><b>Important things should be big, examples</b></summary>
    <br>
    <div align="center">
        <img src="/img/dirty.png" alt="Clean vs Dirty" width="600">
    </div>
    <blockquote>If you allow your important "crux" functions to be larger ("dirty") it is easier to pick them out from the sea of functions, they are obviously important: just look at them, they are big!</blockquote>
    This picture is taken from <a href="https://htmx.org/essays/codin-dirty/" target="_blank">Codin' Dirty</a> article by Carson Gross. You'll find <a href="https://htmx.org/essays/codin-dirty/#real-world-examples" target="_blank">real world examples</a> of deep functions there.
</details> -->

<details>
    <summary><b>Las cosas importantes deben ser grandes: ejemplos</b></summary>
    <br>
    <div align="center">
        <img src="/img/dirty.png" alt="Limpio vs Sucio" width="600">
    </div>
    <blockquote>Si permitimos que las funciones "centrales" importantes sean más grandes ("sucias"), es más fácil distinguirlas en el mar de funciones; son obviamente importantes: ¡solo míralas!</blockquote>
    Esta imagen ha sido tomada del artículo <a href="https://htmx.org/essays/codin-dirty/" target="_blank">Codin' Dirty</a> de Carson Gross. Allí encontrarás <a href="https://htmx.org/essays/codin-dirty/#real-world-examples" target="_blank">ejemplos reales</a> de funciones profundas.
</details>

<!-- P.S. If you think we are rooting for bloated God objects with too many responsibilities, you got it wrong. -->

PD: Si crees que defendemos los 'God objects'/'Objeto Todopoderoso' sobrecargados y con demasiadas responsabilidades, estás equivocado.".

<!-- ## Responsible for one thing -->

## Responsables de una unica funcion

<!-- All too often, we end up creating lots of shallow modules, following some vague "a module should be responsible for one, and only one, thing" principle. What is this blurry one thing? Instantiating an object is one thing, right? So [MetricsProviderFactoryFactory](https://minds.md/benji/frameworks) seems to be just fine. **The names and interfaces of such classes tend to be more mentally taxing than their entire implementations, what kind of abstraction is that?** Something went wrong. -->

Muy frecuentemente, terminamos creado numeroso modulos simplistas, siguiendo el principio ambiguo de "un modulo debe ser responsable por una, y solo una funcion" ¿Pero qué significa exactamente esa "única función"? ¿Acaso instanciar un objeto es una función? Entonces, [MetricsProviderFactoryFactory](https://minds.md/benji/frameworks) parece estar bien. **Sin embargo, los nombres e interfaces de estas clases suelen ser más difíciles de comprender que su implementación completa. ¿Qué tipo de abstracción es esa?** Algo falla en este enfoque.

<!-- We make changes to our systems to satisfy our users and stakeholders. We are responsible to them. -->

Realizamos mejoras en nuestros sistemas para satisfacer las necesidades de nuestros usuarios y demás partes interesadas. Somos responsables ante ellos.

<!-- esta nota debe estar visible al publico -->

> *Nota del traductor*: stakeholders normalmente se usa en el ambito de las inversiones y refiere al inversionanista o tambien traducido como accionista (posee acciones de una empresa), quien posee poder de voto en la toma de deciciones de una empresa, el mismo es la parte interesada en el correcto funcionamiento de la inversion. En nuestro caso y contexto solo refiere a una parte interesada por el funcionamiento esperado del codigo, al no encontrar una palabra que pueda sustituir directamente esta idea la hemos dejado como 'parte interesada'.

<!-- 
> A module should be responsible to one, and only one, user or stakeholder.
> -->

> Un módulo debe ser responsable ante un único usuario o interesado.

<!-- This is what this Single Responsibility Principle is all about. Simply put, if we introduce a bug in one place, and then two different business people come to complain, we've violated the principle. It has nothing to do with the number of things we do in our module. -->

De eso se trata el Principio de Responsabilidad única. En pocas palabras, si introducimos un error en un punto concreto y dos personas de diferentes departamentos se quejan por ello, estamos violando dicho principio. Esto no tiene nada que ver con la cantidad de funciones que incluimos en nuestro módulo.

<!-- But even now, this rule can do more harm than good. This principle can be understood in as many different ways as there are individuals. A better approach would be to look at how much cognitive load it all creates. It's mentally demanding to remember that change in one place can trigger a chain of reactions across different business streams. And that's about it, no fancy terms to learn. -->

Pero incluso hoy en día, esta regla puede generar más mal que bien. Este principio puede interpretarse de muchas maneras, dependiendo de cada persona. Un enfoque más acertado sería analizar la carga cognitiva que implica. Es difícil recordar mentalmente que un cambio en un área puede desencadenar una serie de reacciones en diferentes procesos de la empresa. Y eso es todo; no hace falta aprender términos complicados.

<!-- ## Too many shallow microservices -->

## Demasiados microservicios superficiales

<!-- This shallow-deep module principle is scale-agnostic, and we can apply it to microservices architecture. Too many shallow microservices won't do any good - the industry is heading towards somewhat "macroservices", i.e., services that are not so shallow (=deep). One of the worst and hardest to fix phenomena is so-called distributed monolith, which is often the result of this overly granular shallow separation. -->

Este principio de módulo superficial-profundo es independiente de la escala, y podemos aplicarlo a la arquitectura de microservicios. Demasiados microservicios superficiales no servirán de nada; la industria se está moviendo hacia "macroservicios", es decir, servicios que no son tan superficiales (= profundos). Uno de los peores fenomenos y ademas, más difíciles de corregir es el llamado monolito distribuido, que a menudo es el resultado de esta separación superficial excesivamente granular.

<!-- I once consulted a startup where a team of five developers introduced 17(!) microservices. They were 10 months behind schedule and appeared nowhere close to the public release. Every new requirement led to changes in 4+ microservices. It took an enormous amount of time to reproduce and debug an issue in such a distributed system. Both time to market and cognitive load were unacceptably high. `🤯` -->

Una vez fui consultado por una *startup* donde un equipo de cinco desarrolladores crearon 17(!) microservicios. Tenian un atraso de 10 meses y no parecia estar cerca del lamzamiento. Cada nuevo rquerimiento llevaba a cambios en 4 o mas microservicios. Tomaba mucho tiempo  reproducir un bug un problemas en estos servicios distribuidos. Tanto el tiempo como el mercado y la carga cognitiva estaban en un estado inaceptablemente altos.  `🤯`

<!-- Is this the right way to approach the uncertainty of a new system? It's enormously difficult to elicit the right logical boundaries in the beginning. The key is to make decisions as late as you can responsibly wait, because that is when you have the most information at hand. By introducing a network layer up front, we make our design decisions hard to revert right from the start. The team's only justification was: "The FAANG companies proved microservices architecture to be effective". *Hello, you got to stop dreaming big.* -->

Acaso es esta la mejor manera de abordar la incertidumbre de un nuevo sistema? Es bastante dificil dar con los  limites logicos correctos al principio de un proyecto. La clave esta en tomar desiciones tan tarde como sea responsablemente posible dado que cuando se tiene la mayor cantidad de informacion posible. Al introducir capas de interconexiones en los servicios desde un principio, nuestras desiciones se vuelven mas dificiles de revertir. La unica justificacion que encontro el equipo de desarrollo era: "Las FAANG han provado que la arquitectura de microservicios es efectiva". *Hola, tienes que dejar de soñar en grande.*

<!-- The [Tanenbaum-Torvalds debate](https://en.wikipedia.org/wiki/Tanenbaum%E2%80%93Torvalds_debate) argued that Linux's monolithic design was flawed and obsolete, and that a microkernel architecture should be used instead. Indeed, the microkernel design seemed to be superior "from a theoretical and aesthetical" point of view. On the practical side of things - three decades on, microkernel-based GNU Hurd is still in development, and monolithic Linux is everywhere. This page is powered by Linux, your smart teapot is powered by Linux. By monolithic Linux. -->

En el [debate Tanenbaum-Torvalds](https://en.wikipedia.org/wiki/Tanenbaum%E2%80%93Torvalds_debate), Tanenbaum mantiene que el disenno monolitico de kernel Linux era un defecto de disenno y ademas obsoleto, en cambio debio haberse usado la arquitectura de micro-kernel. Ciertamente, el disenno de micro-kernel desde un punto de vista "teorico y estetico". En la practica, tres decadas despues, el micro-kernell de GNU Hurd sigue en fase de desarrollo y el monolitico Linux esta en todas partes. Esta misma pagina en impulsada por Linux, tu dispositivos smarth son corren en Linux. Por un Linux monolitico.

A well-crafted monolith with truly isolated modules is often much more flexible than a bunch of microservices. It also requires far less cognitive effort to maintain. It's only when the need for separate deployments becomes crucial, such as scaling the development team, that you should consider adding a network layer between the modules, future microservices.

Un monolito bien construido con modulos verdaderamente aislados es, muchas veces, mas flexible que un monton de microservicios. Tambien requiere mucho menos efuerzo cognitivo. Es solo cuando se requieres despliegues separados cuando los microservicios son cruciales, asi como escalar el equipo de desarrollo, deberian considerar annadir una capa de interconexion ente los modulos de los futuros microservicis.

## Feature-rich languages

## Lenguages ricos en caracteristicas

We feel excited when new features got released in our favourite language. We spend some time learning these features, we build code upon them.

Tendemos a emocionarnos cuando se lanzan nuevas caracteristicas en nuestro lenguaje favorito. Invertimos cierta cantidad de tiempo aprendiendo esas nuevas posibilidades y creamos cosdigo en base a ellas.

If there are lots of features, we may spend half an hour playing with a few lines of code, to use one or another feature. And it's kind of a waste of time. But what's worse, **when you come back later, you would have to recreate that thought process!**

Si hay muchas caracteristicas puede que pasemos al menos media hora jugando con ellas escribiendo un par de lineas de codigo para poder usar luego alguna u otra caracteristica. Pero lo peors, **cuando regresamos luego, tenemos que recrear todo el proceso de pensamiento!**

**You not only have to understand this complicated program, you have to understand why a programmer decided this was the way to approach a problem from the features that are available.** `🤯`

**No solo tenemos que entender un programa complicado, tenemos que entender por que un programado decidio tomar dicho enfoque para abordar el problema con las caractericticas disponibles. `🤯`**

These statements are made by none other than Rob Pike.
Esta es la famosa declaracion por no menos que Rob Pike.

> Reduce cognitive load by limiting the number of choices.
> Reduzca la carga cognitiva limitando el numero de opciones.

Language features are OK, as long as they are orthogonal to each other.

Las nuevas características de un lenguaje son aceptables, siempre y cuando sean mutuamente independientes (ortogonnales).

<details>
  <summary><b>Thoughts from an engineer with 20 years of C++ experience ⭐️</b></summary>
  <br>
  I was looking at my RSS reader the other day and noticed that I have somewhat three hundred unread articles under the "C++" tag. I haven't read a single article about the language since last summer, and I feel great!<br><br>
  I've been using C++ for 20 years for now, that's almost two-thirds of my life. Most of my experience lies in dealing with the darkest corners of the language (such as undefined behaviours of all sorts). It's not a reusable experience, and it's kind of creepy to throw it all away now.<br><br>
  Like, can you imagine, the token <code>||</code> has a different meaning in <code>requires ((!P<T> || !Q<T>))</code> and in <code>requires (!(P<T> || Q<T>))</code>. The first is the constraint disjunction, the second is the good-old logical OR operator, and they behave differently.<br><br>
  You can't allocate space for a trivial type and just <code>memcpy</code> a set of bytes there without extra effort - that won't start the lifetime of an object. This was the case before C++20. It was fixed in C++20, but the cognitive load of the language has only increased.<br><br>
  Cognitive load is constantly growing, even though things got fixed. I should know what was fixed, when it was fixed, and what it was like before. I am a professional after all. Sure, C++ is good at legacy support, which also means that you <b>will face</b> that legacy. For example, last month a colleague of mine asked me about some behaviour in C++03. <code>🤯</code><br><br>
  There were 20 ways of initialization. Uniform initialization syntax has been added. Now we have 21 ways of initialization. By the way, does anyone remember the rules for selecting constructors from the initializer list? Something about implicit conversion with the least loss of information, <i>but if</i> the value is known statically, then... <code>🤯</code><br><br>
  <b>This increased cognitive load is not caused by a business task at hand. It is not an intrinsic complexity of the domain. It is just there due to historical reasons</b> (<i>extraneous cognitive load</i>).<br><br>
  I had to come up with some rules. Like, if that line of code is not as obvious and I have to remember the standard, I better not write it that way. The standard is somewhat 1500 pages long, by the way.<br><br>
  <b>By no means I am trying to blame C++.</b> I love the language. It's just that I am tired now.<br><br>
  <p>Thanks to <a href="https://0xd34df00d.me" target="_blank">0xd34df00d</a> for writing.</p>
</details>

<details>
  <summary><b>Reflexiones de un ingeniero con 20 años de experiencia en C++ ⭐️</b></summary>
  <br>
  El otro día estaba mirando mi lector de RSS y me di cuenta de que tengo unos trescientos artículos sin leer bajo la etiqueta "C++". No he leído un solo artículo sobre el lenguaje desde el verano pasado, ¡y me siento genial!<br><br>
  Llevo usando C++ desde hace 20 años, eso es casi dos tercios de mi vida. La mayor parte de mi experiencia reside en lidiar con los rincones más oscuros del lenguaje (como comportamientos indefinidos de todo tipo). No es una experiencia reutilizable, y es un poco desolador desecharlo todo ahora.<br><br>
  Por ejemplo, ¿te imaginas?, el token <code>||</code> tiene un significado diferente en <code>requires ((!P<T> || !Q<T>))</code> y en <code>requires (!(P<T> || Q<T>))</code>. El primero es la disyunción de restricciones, el segundo es el viejo y conocido operador OR lógico, y se comportan de manera diferente.<br><br>
  No puedes reservar espacio para un tipo trivial y simplemente hacer <code>memcpy</code> de un conjunto de bytes ahí sin un esfuerzo adicional; eso no iniciará el tiempo de vida de un objeto. Así era antes de C++20. Se corrigió en C++20, pero la carga cognitiva del lenguaje no ha hecho más que aumentar.<br><br>
  La carga cognitiva crece constantemente, aunque se hayan arreglado cosas. Debo saber qué se arregló, cuándo se arregló y cómo era antes. Después de todo, soy un profesional. Claro, C++ es bueno con el soporte de código heredado (legacy), lo que también significa que <b>te enfrentarás</b> a ese legado. Por ejemplo, el mes pasado un colega me preguntó sobre un comportamiento en C++03. <code>🤯</code><br><br>
  Había 20 formas de inicialización. Se ha añadido la sintaxis de inicialización uniforme. Ahora tenemos 21 formas de inicialización. Por cierto, ¿alguien recuerda las reglas para seleccionar constructores a partir de la lista de inicializadores? Algo sobre la conversión implícita con la menor pérdida de información, <i>pero si</i> el valor se conoce estáticamente, entonces... <code>🤯</code><br><br>
  <b>Este aumento de la carga cognitiva no está causado por una tarea de negocio. No es una complejidad intrínseca del dominio. Simplemente está ahí por razones históricas</b> (<i>carga cognitiva ajena</i>).<br><br>
  Tuve que idear algunas reglas. Por ejemplo, si esa línea de código no es tan obvia y tengo que recordar el estándar, es mejor que no la escriba de esa manera. Por cierto, el estándar tiene unas 1500 páginas.<br><br>
  <b>De ninguna manera estoy tratando de culpar a C++.</b> Amo el lenguaje. Es solo que ahora estoy cansado.<br><br>
  <p>Gracias a <a href="https://0xd34df00d.me" target="_blank">0xd34df00d</a> por escribirlo.</p>
</details>

## Business logic and HTTP status codes

## Logica de Negocia y Estados HTTP

On the backend we return:
`401` for expired JWT token
`403` for not enough access
`418` for banned users

Desde el backend retornan:
`401` para un Token JWT que ha expirado
`403` no posee los accesos adecuados
`418` para usuarios prohibidos (esto es segun el autor pero 418 es 'Soy una tetera')

The engineers on the frontend use backend API to implement login functionality. They would have to temporarily create the following cognitive load in their brains:
`401` is for expired JWT token // `🧠+`, ok just temporarily remember it
`403` is for not enough access // `🧠++`
`418` is for banned users // `🧠+++`

Los ingenieros del frontend que utilizan la API del backend para implementar la funcionalidad de inicio de sesión. Ellos tendran que crear temporalmente la siguiente carga cognitiva en sus cerebros:
`401` para un Token JWT que ha expirado // `🧠+`, ok lo voy a recordar temporalmente
`403` no posee los accesos adecuados // `🧠++`
`418` para usuarios prohibidos // `🧠+++`

Frontend developers would (hopefully) introduce some kind `numeric status -> meaning` dictionary on their side, so that subsequent generations of contributors wouldn't have to recreate this mapping in their brains.

Los ingenieros frontend introduciran (si Dios quiere) algun tipo de diccionatio `estado numeroc -> significado` , de manera que los subsequentes contribuidores no tengan que recrear el mapa en sus mentes.

Then QA engineers come into play:
"Hey, I got `403` status, is that expired token or not enough access?"
**QA engineers can't jump straight to testing, because first they have to recreate the cognitive load that the engineers on the backend once created.**

Luego entran los ingeniero de QA:
"Hola!, tengo un estado `403`, es que ha expirado el token o no tengo acceso?
**Los QA no puede ir directamente al testing porque primero tienen que recrear la carga cognitiva que los ingenieros del backend crearon.**

¿Por qué mantener este mapeo personalizado en nuestra memoria de trabajo? Es mejor abstraer los detalles de negocio del protocolo de transferencia HTTP y devolver códigos autodescriptivos directamente en el cuerpo de la respuesta:

```json
{
    "code": "jwt_has_expired"
}
```

Cognitive load on the frontend side: `🧠` (fresh, no facts are held in mind)
Cognitive load on the QA side: `🧠`

La carga cognitiva del ingeniero Frontend: `🧠` (fresca, no hay que mantener informacion en mente)
Carga cognitiva del QA: `🧠`

The same rule applies to all sorts of numeric statuses (in the database or wherever) - **prefer self-describing strings.** We are not in the era of 640K computers to optimise for memory.

La misma regla aplica para todo tipo de estados numericos (en bases de datos o donde sea) **hay que preferir cadenas de texto descriptivas.**  No estamos en la era de las computadoras de 640KB para vernos obligados a optimizar la memoria.

> People spend time arguing between `401` and `403`, making decisions based on their own mental models. New developers are coming in, and they need to recreate that thought process. You may have documented the "whys" (ADRs) for your code, helping newcomers to understand the decisions made. But in the end it just doesn't make any sense. We can separate errors into either user-related or server-related, but apart from that, things are kind of blurry.
>
> Los programadors pasan tiempo dicutiendo entre 401 y 403, tomando deciciones en base a sus propio modelos mentales. Nuevos desarrolladores estan llegando y necesitan recrear los procesos de pensamiento. Puede que se haya documentado el "por que" (ADRs) en el codigo, ayudando a los recien llegados a entender las deciciones tomadas. PEro al fenal no tiene ningun sentido. Podemos separar los errores en los *relaciondo al usuario* y lo *relacionado al servido*r, pero aparte de eso, los limites tienden a ser algo borrosos.

P.S. It's often mentally taxing to distinguish between "authentication" and "authorization". We can use simpler terms like [&#34;login&#34; and &#34;permissions&#34;](https://ntietz.com/blog/lets-say-instead-of-auth/) to reduce the cognitive load.

PD: Usuarlmente es mentalmente agotador el distinguir entre autenticacion y autorizacion. Podemos usar terminso mas simples como [&#34;login&#34;&#34; y &#34;&#34;permisos&#34;&#34;](https://ntietz.com/blog/lets-say-instead-of-auth/) para reducir la carga cognitiva.

## Abusing DRY principle

## Abusando del principio DRY (No te repitas)

Do not repeat yourself - that is one of the first principles you are taught as a software engineer. It is so deeply embedded in ourselves that we can not stand the fact of a few extra lines of code. Although in general a good and fundamental rule, when overused it leads to the cognitive load we can not handle

No te repitas (tu mismo) es uno de los primeros principios que son enseñados a un ingeniero de software. Esta profundamente incrustado en nosotros y no podemos soportar el hecho de incluir alguna lineas de codigo extra. Aunque en general, es un buen fundamento, cuando hacemos un sobre uso de esta regla el mismo lleva a una sobrecarga cognitiva que no podemos manejar.

Nowadays, everyone builds software based on logically separated components. Often those are distributed among multiple codebases representing separate services. When you strive to eliminate any repetition, you might end up creating tight coupling between unrelated components. As a result, changes in one part may have unintended consequences in other seemingly unrelated areas. It can also hinder the ability to replace or modify individual components without impacting the entire system. `🤯`

Hoy en dia, todos contruyen software en base a componentes logicamente separados. A menudo, dichos sistemas estan distribuidos entre muchso repositoriso de codigo representado diferetes servicios independientes unos de otros. Cuando luchas por eliminar cada repeticion puedes terminan creado un *acoplamiento fuerte* entre distintos servicio no relacionados. Como resultado, los cambios enm una parte del codigo puede tener efectos no intencionados  en otra area que aprecia no relacionada. Además, puede dificultar la posibilidad de reemplazar o modificar componentes individuales sin afectar al sistema en su totalidad. 🤯

In fact, the same problem arises even within a single module. You might extract common functionality too early, based on perceived similarities that might not actually exist in the long run. This can result in unnecessary abstractions that are difficult to modify or extend.

De hecho, el mismo problema surge en un unico modulo. Puedes abstraer funcionalidades de manera muy temprana en el codigo basado en similaridades que pueden no existir a largo plazo. Esto resulta en abtracciones innecesarias que son dificiles de modificar o extender.

Rob Pike once said:
Rob Pike dijo una vez:

> A little copying is better than a little dependency.
> Copiar un poco es mejor que una pequeña dependencia.

We are tempted to not reinvent the wheel so strongly that we are ready to import large, heavy libraries to use a small function that we could easily write by ourselves.

Estamos tan tentados a no reinventar la rueda que estamos listo para imprtar una enorme y pesada libreria para usar una pequeña duncion que facilmente podriamos escribir nosotros.

**All your dependencies are your code.** Going through 10+ levels of stack trace of some imported library and figuring out what went wrong (*because things go wrong*) is painful.

**Todas tus dependencias son tu código.** Recorrer más de 10 niveles de la traza de la pila de alguna librería importada y averiguar qué salió mal (*porque las cosas salen mal*) es doloroso.

## Tight coupling with a framework

## Acoplamiento fuerte con un framework

There's a lot of "magic" in frameworks. By relying too heavily on a framework, **we force all upcoming developers to learn that "magic" first.** It can take months. Even though frameworks enable us to launch MVPs in a matter of days, in the long run they tend to add unnecessary complexity and cognitive load.

Hay mucha "magia" en los frameworks. Al depender casi exclusivamente de un framework **forzamos a los recien llegados  a aprender la "magia" primero.** Y puede que tome meses. Aun cuando muchos framework nos permita lanzar MVPs (productos minimo viable) en cuestion de dias, al largo plazo tienden a añadir una complejidad innecesaria y carga cognitiva.

Worse yet, at some point frameworks can become a significant constraint when faced with a new requirement that just doesn't fit the architecture. From here onwards people end up forking a framework and maintaining their own custom version. Imagine the amount of cognitive load a newcomer would have to build (i.e. learn this custom framework) in order to deliver any value. `🤯`

Peor aun, en algun punto los frameworks se vuelven un probelma importante cuando tenemos un requerimiento que no calza en su arquitectura. De aqui en adelante los profesionales  tienden a tener un fork del framework con  sus propias customizaciones. Imagina la carga cognitiva de un recien llegado que debe contruir (y por ende aprender este cframnework perzonalizado) para poder realizar una entrega. `🤯`

**By no means do we advocate to invent everything from scratch!**

**En ningún caso estamos a favor de (re)inventar todo desde cero.**

We can write code in a somewhat framework-agnostic way. The business logic should not reside within a framework; rather, it should use the framework's components. Put a framework outside of your core logic. Use the framework in a library-like fashion. This would allow new contributors to add value from day one, without the need of going through debris of framework-related complexity first.

Podemos escribir codigo que sea lo mas independiente del framework posible (framework-agnostic). La logica de negocio no deberia depender del framework, deberia encambio, usar los componentes que framework posee. Pongamos el framework fuera de la logica central. Usemos el framework como si fuera una libreria.

> [Why I Hate Frameworks (Por que Odio los Framewworks)](https://minds.md/benji/frameworks)

## Layered architecture

## Arquitectura por capas

There is a certain engineering excitement about all this stuff.

Esto despierta un cierto entusiasmo entre los ingenieros.

I myself was a passionate advocate of Hexagonal/Onion Architecture for years. I used it here and there and encouraged other teams to do so. The complexity of our projects went up, the sheer number of files alone had doubled. It felt like we were writing a lot of glue code. On ever changing requirements we had to make changes across multiple layers of abstractions, it all became tedious. `🤯`

Yo mismo  soy un apacionado de la Arquitectura Hexagonal/Cebolla por años. La uso aqui y alla y motivo a los equipos que hagan lo mismo. La complejidad de nuestros proyectos se disparo, el solo numero total de archivos se habia duplicado.

**Abstraction is supposed to hide complexity, here it just adds [indirection](https://fhur.me/posts/2024/thats-not-an-abstraction).** Jumping from call to call to read along and figure out what goes wrong and what is missing is a vital requirement to quickly solve a problem. With this architecture’s layer uncoupling it requires an exponential factor of extra, often disjointed, traces to get to the point where the failure occurs. Every such trace takes space in our limited working memory. `🤯`

**Se supone que la complejidad debe estar oculta en la Abstraccion,  pero en este caso solo añade [confusion](https://fhur.me/posts/2024/thats-not-an-abstraction).** Pasar de una invocacion a otra para determinar que es lo que ha salido mal y que falta por hacer es un requisito fundamental para solucionar un problema.Con la arquitecura por capas el desacoplamiento requiere un factor exponencial extra, muchas veces inconexas, la traza llega al punto donde la falla ocurre.  Cada traza ocupa un espacion en nuestra limitada memoria de trabajo. `🤯`

This architecture was something that made intuitive sense at first, but every time we tried applying it to projects it did more harm than good. We spent years on unnecessary mental activity and writing useless glue code with no clear business value. On the contrary, we made things worse for the business by forcing newcomers to learn our approaches (mental models) first. The time to market has worsened. In the end, we gave it all up in favour of the good old dependency inversion principle. **No port/adapter terms to learn, no unnecessary layers of horizontal abstractions, no extraneous cognitive load.**

Esta arquiotectura parecia tener snetido de manera intuitiva al principio, pero cada que tratamos de aplicarla a proyectos hacia mas mal que bien. Pasamos años con acitividad mental innencesaria y escribiendo codigo pegamento inutil sin un valor de negocio claro. Al contrario, hicimos las cosas peor para la logica de negocio al forzar al los recien llegados a aprender nuestros enfoques (modelos mentales). El tiempo de comercialización ha empeorado. Al final lo dejamos todo en favor del buen y viejo principio de inversión de dependencias.  **No es necesario aprender términos relacionados con puertos/adaptadores, ni capas innecesarias de abstracción, ni carga cognitiva adicional.**

<details>
    <summary><b>Coding principles and experience</b></summary>
    <div align="center">
        <img src="img/complexity.png" alt="Super simple code" width="500">
    </div>
    <a href="https://twitter.com/flaviocopes">@flaviocopes</a>
</details>

<details>
    <summary><b>Principios de programación y experiencia</b></summary>
    <div align="center">
        <img src="img/complexity.png" alt="Código súper simple" width="500">
    </div>
    <a href="https://twitter.com/flaviocopes">@flaviocopes</a>
</details>

If you think that such layering will allow you to quickly replace a database or other dependencies, you're mistaken. Changing the storage causes lots of problems, and believe us, having some abstractions for the data access layer is the least of your worries. At best, abstractions can save somewhat 10% of your migration time (if any), the real pain is in data model incompatibilities, communication protocols, distributed systems challenges, and [implicit interfaces](https://www.hyrumslaw.com).

Si piensa que esta organizacion por capas le permite reemplazar una base de datos por otra dependencia, esta equivocado. Cambiar el almacenamiento causa muchos problemas, y creanos, tener algunas abtracciones para la capa de acceso de datos es la menor de sus preocupaciones. En el mejor de los casos, las abstracciones pueden salvar alrededor del 10% de su tiempo de migracion (si acaso), el verdadero dolor esta en la incompatibilidad de los modelos de datos, protocolos de comunicacion, desafios de los sistemas distribuidos y las [iinterfaces implicitas](https://www.hyrumslaw.com).

> With a sufficient number of users of an API,
> it does not matter what you promise in the contract:
> all observable behaviours of your system
> will be depended on by somebody.
>
> Con un numero suficiente de usuarios de una API,
> no importa lo que haya prometido en el contrato:
> todos los comportamientos observables de su sistema
> van a depender de alguien.

We did a storage migration, and that took us about 10 months. The old system was single-threaded, so the exposed events were sequential. All our systems depended on that observed behaviour. This behaviour was not part of the API contract, it was not reflected in the code. A new distributed storage didn't have that guarantee - the events came out-of-order. We spent only a few hours coding a new storage adapter, thanks to an abstraction. **We spent the next 10 months on dealing with out-of-order events and other challenges.** It's now funny to say that abstractions help us replace components quickly.

Hicimos algo de migracion de almacenamiento, nos tomo unos 10 meses. El viejo sistema era mono-hilo, por tanto, los eventos eran expuestos de manera secuencial. Todos nuestros sistemas dependen en ese comportamiento observado. Dicho comportamiento no era parte del contrato de la API y no fue reflejada en el codigo. Un nuevo almacenamiento distribuido no tiene las garantias de que los eventos lleguen en orden. Solo usamos algunas hora ecribiendo el nuevo adaptador del amacenamient, gracias a la abtraccion. **Pasamos los siguientes 10 meses lidiando con los eventos fuera de orden y otros desafios.** Ahora resulta gracioso decir que la abtraccion nos ayuda reemplazar los componentes de manera rapida.

**So, why pay the price of high cognitive load for such a layered architecture, if it doesn't pay off in the future?** Plus, in most cases, that future of replacing some core component never happens.

**Entonces, porque pagar el precio de una alta carga cognitiva por una arquitectura por capas si no da beneficios futuros?** sumando ademas, que en la mayoria de los casos ese futuro de reemplazar componentes casi nunca pasa.

These architectures are not fundamental, they are just subjective, biased consequences of more fundamental principles. Why rely on those subjective interpretations? Follow the fundamental rules instead: dependency inversion principle, single source of truth, cognitive load and information hiding. Your business logic should not depend on low-level modules like database, UI or framework. We should be able to write tests for our core logic without worrying about the infrastructure, and that's it. [Discuss](https://github.com/zakirullin/cognitive-load/discussions/24).

Estas arquitecturas no son fundamentales, solo son subjetivas, consecuencias sesgadas de principios más fundamentales. Porque confiar unicamente en esas interpretaciones subjetivas? Sigamos mejor las reglas fundamentales: el principio de inversion de dependencias, una sola fuente de la verdad, carga cognitiva y abstraccion de la informacion. SU logica de negocio no debe depender de modulos de bajo nivel com una base de datos, la UI o un framework. Deberiamos ser capaces de escribir test para nuestra logica central sin preocuparnos por la infraestructura, y eso es todo! [Discucion](https://github.com/zakirullin/cognitive-load/discussions/24)

Do not add layers of abstractions for the sake of an architecture. Add them whenever you need an extension point that is justified for practical reasons.

No añada capas de abtraccion por el amor a la arquitectura. Añadala cuando necesita una extension al pinta que se justifique por razones practicas.

**[Layers of abstraction aren&#39;t free of charge](https://blog.jooq.org/why-you-should-not-implement-layered-architecture), they are to be held in our limited working memory.**

**[Los niveles de abstracción no son gratuitos](https://blog.jooq.org/why-you-should-not-implement-layered-architecture), requieren recursos de nuestra memoria de trabajo, que es limitada.**

<div align="center">
  <img src="/img/layers.png" alt="Layers" width="400">
</div>

## Domain Driven Design

Domain-driven design has some great points, although it is often misinterpreted. People say, "We write code in DDD", which is a bit strange, because DDD is more about the problem space rather than the solution space.

El Domain-Driven Design (Diseño Guiado por el Dominio) tiene grandes puntos a su favor, aunque frecuentemente es mal interpretado. Las personas dicen "escribo codigo en DDD", lo cual es un poco extraño, porque el DDD es mas sobre el espacio del problema que la solucion al espacio.

Ubiquitous language, domain, bounded context, aggregate, event storming are all about problem space. They are meant to help us learn the insights about the domain and extract the boundaries. DDD enables developers, domain experts and business people to communicate effectively using a single, unified language. Rather than focusing on these problem space aspects of DDD, we tend to emphasise particular folder structures, services, repositories, and other solution space techniques.

El Lenguaje Ubicuo, el Dominio, el Contexto Delimitado, el Agregado y el Event Storming son conceptos que pertenecen al espacio del problema (problem space). Su objetivo es ayudarnos a obtener una comprensión profunda del dominio y a delimitar sus fronteras. DDD facilita que desarrolladores, expertos del dominio y responsables de negocio se comuniquen eficazmente utilizando un lenguaje único y unificado. Sin embargo, en lugar de centrarnos en estos aspectos de DDD del espacio del problema, solemos poner el énfasis en estructuras de carpetas, servicios, repositorios y otras técnicas del espacio de la solución (solution space).

Chances are that the way we interpret DDD is likely to be unique and subjective. And if we build code upon this understanding, i.e., if we create a lot of extraneous cognitive load - future developers are doomed. `🤯`

Lo mas problable es que la manera en que cada uno interpreta el DDD sea unica y subjetiva. Y si escribimos codigo sobre estas conclusiones, por ejemplo, creamos muchas carga cognitiva externa, los programadores que aborde este codigo en el futuro estan perdidos! `🤯`

Team Topologies provides a much better, easier to understand framework that helps us split the cognitive load across teams. Engineers tend to develop somewhat similar mental models after learning about Team Topologies. DDD, on the other hand, seems to be creating 10 different mental models for 10 different readers. Instead of being common ground, it becomes a battleground for unnecessary debates.

LaTopologia de Equipo provee una mejor y mas facil manera de entender el conexto que nos ayuda a dividir la carga cognitiva entre equipos. Los ingenieros tienden a desarrollar del algun modo, modelos mentales siimilar al aprender sobre Topologia de Equipos. DDD, por otro lado, parece crear 10 diferentes modelos mentales para 10 lectores diferentes. En ves de ser un terrene comun, se combierte en un campo de batalla para debates innecesarios.

## Cognitive load in familiar projects

## La Carga Cognitiva en proyectos que nos son familiares

> The problem is that **familiarity is not the same as simplicity.** They *feel* the same — that same ease of moving through a space without much mental effort — but for very different reasons. Every “clever” (read: “self-indulgent”) and non-idiomatic trick you use incurs a learning penalty for everyone else. Once they have done that learning, then they will find working with the code less difficult. So it is hard to recognise how to simplify code that you are already familiar with. This is why I try to get “the new kid” to critique the code before they get too institutionalised!
>
> El problema es que **la familiaridad no es igual a simplicidad.** Se *sienten* iguales, esa misma facilidad para moverse por un espacio sin tener que hacer un gran esfuerzo mental, pero por muy diferentes razones. Cada solucion "ingeniosa" (o mas bien "caprichosa") y no idiomatica que se utilice supone un obstaculo para el aprendizaje de los demas. Una vez que terminen de aprender, se encontraran con codigo menos dificil. Entonces, es dificil reconocer como el simplicar el codigo con el que estamos familiarizados. Es por qesto que tratamso que el "chco nuevo" critique el codigo antes de que este muy institucionalizado.
>
> It is likely that the previous author(s) created this huge mess one tiny increment at a time, not all at once. So you are the first person who has ever had to try to make sense of it all at once.
>
> Es proables que el(los) autor(es) anterior(es) crearan un enorme desastre con un pequeño incremento a la vez , no de un golpe. Por lo tanto, usted es la primera persona que ha tenido que intentar comprenderlo todo de una vez.
>
> In my class I describe a sprawling SQL stored procedure we were looking at one day, with hundreds of lines of conditionals in a huge WHERE clause. Someone asked how anyone could have let it get this bad. I told them: “When there are only 2 or 3 conditionals, adding another one doesn’t make any difference. By the time there are 20 or 30 conditionals, adding another one doesn’t make any difference!”
>
> En nuestras clases describimos un extenso procedimiento almacenado de SQL que estuvimos analizando un día, con cientos de líneas de condicionales en una cláusula WHERE enorme. Alguien preguntó cómo era posible que hubieran permitido que llegara a tal extremo. Les respondí: “Cuando solo hay 2 o 3 condicionales, añadir uno más no supone ninguna diferencia. Para cuando ya hay 20 o 30, ¡añadir uno más tampoco supone ninguna diferencia!”.
>
> There is no “simplifying force” acting on the code base other than deliberate choices that you make. Simplifying takes effort, and people are too often in a hurry.
>
> No existe ninguna "fuerza simplificadora" que actúe sobre la base de código, más allá de las decisiones deliberadas que se toman. Simplificar requiere esfuerzo y, con demasiada frecuencia, la gente tiene prisa
>
> *Thanks to [Dan North](https://dannorth.net) for his comment*.
> *Gracias a [Dan North](https://dannorth.net) por este comentario*.

If you've internalized the mental models of the project into your long-term memory, you won't experience a high cognitive load.

Si has internalizado los modelos mentales del proyecto en tu memoria a largo plazo, no experimentarás una gran carga cognitiva.

<div align="center">
  <img src="/img/mentalmodelsv15.png" alt="Mental models" width="700">
</div>

The more mental models there are to learn, the longer it takes for a new developer to deliver value.

Cuantos más modelos mentales haya que aprender, más tiempo le tomará a un nuevo desarrollador aportar valor.

Once you onboard new people on your project, try to measure the amount of confusion they have (pair programming may help). If they're confused for more than ~40 minutes in a row - you've got things to improve in your code.

Cuando incorpores a gente nueva a tu proyecto, intenta medir su nivel de confusión (el pair programming puede ayudar). Si están confundidos durante más de ~40 minutos seguidos, tienes aspectos que mejorar en tu código.

If you keep the cognitive load low, people can contribute to your codebase within the first few hours of joining your company.

Si mantienes la carga cognitiva baja, la gente puede contribuir a la base de código en sus primeras horas tras unirse a la empresa.

## Examples

## Ejemplos

- Our architecture is a standard CRUD app architecture, [a Python monolith on top of Postgres](https://danluu.com/simple-architectures/)
- How Instagram scaled to 14 million users with [only 3 engineers](https://read.engineerscodex.com/p/how-instagram-scaled-to-14-million)
- The companies where we were like ”woah, these folks are [smart as hell](https://kenkantzer.com/learnings-from-5-years-of-tech-startup-code-audits/)” for the most part failed
- One function that wires up the entire system. If you want to know how the system works - [go read it](https://www.infoq.com/presentations/8-lines-code-refactoring)

* Nuestra arquitectura es la de una aplicación CRUD estándar, [un monolito de Python sobre Postgres](https://www.google.com/url?sa=E&q=https%3A%2F%2Fdanluu.com%2Fsimple-architectures%2F).
* Cómo Instagram escaló a 14 millones de usuarios con [solo 3 ingenieros](https://www.google.com/url?sa=E&q=https%3A%2F%2Fread.engineerscodex.com%2Fp%2Fhow-instagram-scaled-to-14-million).
* La mayoría de las empresas sobre las que pensábamos «guau, esta gente es [increíblemente lista](https://www.google.com/url?sa=E&q=https%3A%2F%2Fkenkantzer.com%2Flearnings-from-5-years-of-tech-startup-code-audits%2F)» fracasaron.
* Una única función que orquesta todo el sistema. Si quieres saber cómo funciona, [ve y léela](https://www.google.com/url?sa=E&q=https%3A%2F%2Fwww.infoq.com%2Fpresentations%2F8-lines-code-refactoring) .

These architectures are quite boring and easy to understand. Anyone can grasp them without much mental effort.

Estas arquitecturas son aburridas y faciles de entender. Cualquier puede entenderlas sin mucho esfuerzo mental.

Involve junior developers in architecture reviews, they will help you to identify the mentally demanding areas.

Involucrar a los desarrolladores junior en la revision de arquitecturas, te ayudaran a identificar la areas metalmente demadantes.

> Software systems are perhaps the most intricate and complex (in terms of number of distinct kinds of parts) of the things humanity makes.
>
> Los sistemas de software so quizas lo mas intricados y complejos (en el sentido de los distitos numeros de partes) que la humanidad puede hacer.
>
> *Fred Brooks, The Mythical Man-Month
> Fred Brooks, The Mythical Man-Month (El mito del hombre mes)*

**Maintaining software is hard**, things break and we would need every bit of mental effort we can save. The fewer components there are in the system, the fewer issues there will be. Debugging will also be less mentally taxing.

**Mantener software es dificil,** las caracteriticas tienden a rompeser y necesitamos ahorrar cada gramo de energia mental que podamos. Mientras menos componentes tenga el sistema, menos problemas vamos a tener. Depurrar tambien se vuelve menos agotador.

> Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.
>
> Depurar es el doble de dificil que escribir codigo en un primer momento. Por tanto, si es escribes el codigo mas brillante posibñle, tu eres por definicion, no lo suficientementwe listo para depurarlo.
>
> *Brian Kernighan*

In general, the mindset "Wow, this architecture sure feels good!" is misleading. That's "a point in time" subjective feeling, and it says nothing about the reality. A far better approach is to observe the consequences in the long run:

En general, la mentalidad "Wao!, esta arquitectura seguramente es la mejor" es engañosa, Esto es "en cierto punto en el tiempo" un sentimiento subjetivo y no dice nada sobre la realidad.  Un abordaje mucho mejor seria observar las consecuencia a largo plazo:

- Is it easy to reproduce and debug an issue? Or do you have to jump across the call stacks or distributed components, trying to make sense of everything in your head?
- Es facil reproducir un bug o un problema? O debe ir de un lado a otro en la pila de invocaciones o componente distribuidos, tratando de darle sentido a todo en su cabeza.
- Can we make changes quickly, or are there a lot of unknown unknowns, and people are afraid to touch things?
- Podemos hacer cambios rapidamente, o hay un monto de desconocido y los desarrolladores tienen miedo de tocar el codigo.
- Can new people add features quickly? Are there some unique mental models to learn?
- Pueden lo recien llegados añadir nuevas caracteristica rapidamente? Hay algun modelo mental unico que aprender?

> What are those unique mental models? It's some set of rules, usually a mixture of DDD/CQRS/Clean Architecture/Event Driven Architecture. This is an author's own interpretation of the things that excite him the most. His own subjective mental models. **Extraneous cognitive load that others have to internalize.**
>
> Que son esos modelos mentales tan unicos? Es un conjunto de reglas, usualmente DDD/CQRS/Arquitectura Limpia/Arquitectura por Eventos. Esta es la interpretacion del autor en cuanto a las cosas que mas le emocionan. Son sus propios modelos subjetivos. **Cargas cognitiva extrañas que otros deben internalizar.**

These questions are far harder to track, and people often don't like to answer them directly. Look at some of the most complex software systems in the world, the ones that have stood the test of time - Linux, Kubernetes, Chrome and Redis (see comments below). You will not find anything fancy there, it's boring for the most part, and that's a good thing.

Estas preguntas son algo dificil de seguire, y normalmente las personas no les gusta responder de manera concreta. Si miramos algunos de los sistemas de software mas  complejos del mundos, aquellos que han soportado la prueba del tiempo (eje: Linux, Kubernetes, Chrome, Redis (ver comentatios mas abajo)).  No encontrara nada esplendoroso, es aburrido en su mayopr parte, y eso es bueno.

## Conclusion 

## Conclusiones

Imagine for a moment that what we inferred in the second chapter isn’t actually true. If that’s the case, then the conclusion we just negated, along with the conclusions in the previous chapter that we had accepted as valid, might not be correct either. `🤯`

Imagina por un momento que lo que inferimos en el segundo capítulo no es realmente cierto. Si ese es el caso, entonces la conclusión que acabamos de negar, junto con las conclusiones del capítulo anterior que habíamos aceptado como válidas, tampoco podrían ser correctas. 🤯

Do you feel it? Not only do you have to jump all over the article to get the meaning (shallow modules!), but the paragraph in general is difficult to understand. We have just created an unnecessary cognitive load in your head. **Do not do this to your colleagues.**

¿Lo notas? No solo tienes que saltar por todo el artículo para entender el significado (¡módulos poco profundos!), sino que el párrafo en general es difícil de comprender. Acabamos de crear una carga cognitiva innecesaria en tu cabeza. **No le hagas esto a tus colegas.**

<div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="Smart author" width="600">
</div>

We should reduce any cognitive load above and beyond what is intrinsic to the work we do.

Deberíamos reducir cualquier carga cognitiva que vaya más allá de lo que es intrínseco al trabajo que realizamos.

```

```

---

[LinkedIn](https://www.linkedin.com/in/zakirullin/), [X](https://twitter.com/zakirullin), [GitHub](https://github.com/zakirullin), artemzr(аt)g-yоu-knоw-com

<details>
    <summary><b>Comments</b></summary>
    <br>
    <p><strong>Rob Pike</strong> <i>(Unix, Golang)</i><br>Nice article.</p>
    <p><strong><a href="https://x.com/karpathy/status/1872038630405054853" target="_blank">Andrej Karpathy</a></strong> <i>(ChatGPT, Tesla)</i><br>Nice post on software engineering. Probably the most true, least practiced viewpoint.</p>
    <p><strong><a href="https://x.com/elonmusk/status/1872346903792566655" target="_blank">Elon Musk</a></strong> <i>(Rockets)</i><br>True.</p>
    <p><strong><a href="https://www.linkedin.com/feed/update/urn:li:activity:7277757844970520576/" target="_blank">Addy Osmani</a></strong> <i>(Chrome, the most complex software system in the world)</i><br>I've seen countless projects where smart developers created impressive architectures using the latest design patterns and microservices. But when new team members tried to make changes, they spent weeks just trying to understand how everything fits together. The cognitive load was so high that productivity plummeted and bugs multiplied.</p>
    <p>The irony? Many of these complexity-inducing patterns were implemented in the name of "clean code."</p>
    <p>What really matters is reducing unnecessary cognitive burden. Sometimes this means fewer, deeper modules instead of many shallow ones. Sometimes it means keeping related logic together instead of splitting it into tiny functions.</p>
    <p>And sometimes it means choosing boring, straightforward solutions over clever ones. The best code isn't the most elegant or sophisticated - it's the code that future developers (including yourself) can understand quickly.</p>
    <p>Your article really resonates with the challenges we face in browser development. You're absolutely right about modern browsers being among the most complex software systems. Managing that complexity in Chromium is a constant challenge that aligns perfectly with many of the points you made about cognitive load.</p>
    <p>One way we try to handle this in Chromium is through careful component isolation and well-defined interfaces between subsystems (like rendering, networking, JavaScript execution, etc.). Similar to your deep modules example with Unix I/O - we aim for powerful functionality behind relatively simple interfaces. For instance, our rendering pipeline handles incredible complexity (layout, compositing, GPU acceleration) but developers can interact with it through clear abstraction layers.</p>
    <p>Your points about avoiding unnecessary abstractions really hit home too. In browser development, we constantly balance between making the codebase approachable for new contributors while handling the inherent complexity of web standards and compatibility. </p>
    <p>Sometimes the simplest solution is the best one, even in a complex system.</p>
    <p><strong><a href="https://x.com/antirez" target="_blank">antirez</a></strong> <i>(Redis)</i><br>Totally agree about it :) Also, what I believe is missing from mentioned "A Philosophy of Software Design" is the concept of "design sacrifice". That is, sometimes you sacrifice something and get back simplicity, or performances, or both. I apply this idea continuously, but often is not understood.</p>
    <p>A good example is the fact that I always refused to have hash items expires. This is a design sacrifice because if you have certain attributes only in the top-level items (the keys themselves), the design is simpler, values will just be objects. When Redis got hash expires, it was a nice feature but required (indeed) many changes to many parts, raising the complexity.</p>
    <p>Another example is what I'm doing right now, Vector Sets, the new Redis data type. I decided that Redis would not be the source of truth about vectors, but that it can just take an approximate version of them, so I was able to do on-insert normalization, quantization without trying to retain the large floats vector on disk, and so forth. Many vector DBs don't sacrifice the fact of remembering what the user put inside (the full precision vector).</p>
    <p>These are just two random examples, but I apply this idea everywhere. Now the thing is: of course one must sacrifice the right things. Often, there are 5% features that account for a very large amount of complexity: that is a good thing to kill :D</p>
    <p><strong><a href="https://working-for-the-future.medium.com/about" target="_blank">A developer from the internet</a></strong><br>You would not hire me... I sell myself on my track record of released enterprise projects.</p>
    <p>I worked with a guy that could speak design patterns. I could never speak that way, though I was one of the few that could well understand him. The managers loved him and he could dominate any development conversation. The people working around him said he left a trail of destruction behind him. I was told that I was the first person that could understand his projects. Maintainability matters. I care most about TCO. For some firms, that's what matters.</p>
    <p>I logged into Github after not being there for a while and for some reason it took me to an article in a repository by someone that seemed random. I was thinking "what is this" and had some trouble getting to my home page, so I read it. I didn't really register it at the time, but it was amazing. Every developer should read it. It largely said that almost everything we've been told about programming best practices leads to excessive "cognitive load", meaning our minds are getting kicked by the intellectual demands. I've known this for a while, especially with the demands of cloud, security and DevOps.</p>
    <p>I also liked it because it described practices I have done for decades, but never much admit to because they are not popular... I write really complicated stuff and need all the help I can get.</p>
    <p>Consider, if I'm right, it popped up because the Github folks, very smart people, though that developers should see it. I agree.</p>
    <p><a href="https://news.ycombinator.com/item?id=45074248" target="_blank">Comments on Hacker News</a> (<a href="https://news.ycombinator.com/item?id=42489645" target="_blank">2</a>)</p>
</details>
