# Cognitive load is what matters

[Prompt](https://github.com/zakirullin/cognitive-load/blob/main/README.prompt.md) | [Blog version](https://minds.md/zakirullin/cognitive) | [Chinese](https://github.com/zakirullin/cognitive-load/blob/main/README.zh-cn.md) | [Korean](README.ko.md) | [Turkish](README.tr.md) | [Japanese](README.ja.md) 

*It is a living document, last update: **September 2025.** Your contributions are welcome!*

*Este es un domento vivo, ultima actualizacion: **Septiembre 2025**.  ¡Tus contribuciones son bienbenidas!*

## Introduction 

## Introduccion

There are so many buzzwords and best practices out there, but most of them have failed. They failed because they were imagined, not real. These ideas were based on aesthetics and subjective judgments. We need something more fundamental, something that can't be wrong.

Hay muchos terminos y practicas que se ponen de moda, pero la gran mayortia de ellos fallan en su cometido. Fallan porque eran imaginarios, no reales. Esta ideas estaban basadas en juicios esteticos y subjetivos. Se hace necesario alfo mas fundamental, algo que no pueda estar errado.

Sometimes we feel confusion going through the code. Confusion costs time and money. Confusion is caused by high *cognitive load*. It's not some fancy abstract concept, but rather **a fundamental human constraint.** It's not imagined, it's there and we can feel it.

A veces podemos sentir mucha confusion mientras leemos codigo. Confuncion que cuesta tiempo y dinero. Confusin causado por la *carga cognitiva.* No se trata de algun concepto bastracto y/o sofisticado, sino mas bien un **limite muy humano.** Y no es imaginario, es algo que realmente podemos sentir.

Since we spend far more time reading and understanding code than writing it, we should constantly ask ourselves whether we are embedding excessive cognitive load into our code.

Dado que pasamos mas tiempo leyendo y tratando de entender el coodigo del que pasamos escribiendo, deberiamos preguntarnos constantemente si estamos colocando una excesiva carga cognitiva en el codigo que escribimos.

## Cognitive load 

## La Carga Cognitiva

> Cognitive load is how much a developer needs to think in order to complete a task.
>
> La carga cognitiva se refiere a la cantidad de esfuerzo mental que un desarrollador necesita para completar una tarea.

When reading code, you put things like values of variables, control flow logic and call sequences into your head. The average person can hold roughly [four such chunks](https://github.com/zakirullin/cognitive-load/issues/16) in working memory. Once the cognitive load reaches this threshold, it becomes much harder to understand things.

Cuando leemos el codigo colocamos cosas como valores, variables, controles de flujo, logica y llamados de secuencia en nuestra mente. La persona promedio puede colocar unos [c](https://github.com/zakirullin/cognitive-load/issues/16)[uato elementos ](https://github.com/zakirullin/cognitive-load/issues/16)en nuestra memmoria de trabajo. Una vez que la carga cognitiva pasa ciertto limite se vueleve muy dificil entender ciertas cosas.

*Let's say we have been asked to make some fixes to a completely unfamiliar project. We were told that a really smart developer had contributed to it. Lots of cool architectures, fancy libraries and trendy technologies were used. In other words, **the author had created a high cognitive load for us.***

*Digamos que nos solicitan realizar correciones a un projecto con el que no estamos familiarizados. Nos dicen que un desarrollador realmente inteligente ha contribuido al mismo. Un monton de arquitecturas geniales, librerias sofisticadas y tecnologias de punta fueron usadas. En sintesis, **el autor a creado una enorme carga cognitiva para nosotros.***


<div align="center">
  <img src="/img/cognitiveloadv6.png" alt="Cognitive load" width="750">
</div>

We should reduce the cognitive load in our projects as much as possible.

Deberíamos reducir la carga cognitiva en nuestros proyectos en medida posible.

<details>
  <summary><b>Cognitive load and interruptions | Carga cognitiva e interrupciones</b></summary>
  <div align="center">
    <img src="img/interruption.jpeg" width="480">
  </div>
</details>


> We are going to use "cognitive load" in an informal sense; sometimes it lines up with the specific scientific concept of Cognitive Load, but we don't know enough about where it does and doesn't match.
>
> Vamos a utilizar el término "carga cognitiva" en un sentido informal; a veces coincide con el concepto científico específico de Carga Cognitiva, pero no conocemos con precisión en qué aspectos coinciden y en cuáles no.

## Types of cognitive load 

## Tipos de carga cognitiva

**Intrinsic** - caused by the inherent difficulty of a task. It can't be reduced, it's at the very heart of software development.

**Intinseca** - causada por la dificultad inherente a la tarea. Puede ser reducida, es el nucleo fundamental de un ingeniero de software.

**Extraneous** - created by the way the information is presented. Caused by factors not directly relevant to the task, such as smart author's quirks. Can be greatly reduced. We will focus on this type of cognitive load.

**Extrinseca** - creada por la forma en que la informacion es presentada. Es causada por dactores que no son directamente relacionado a la tarea, como los caprichos de un autor que se siente particularmente inteligente. Puede reducirse considerablemente. Nos enfoccaremos en este tipo de carga cognitiva.

<div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="Intrinsic vs Extraneous | Intinseca vs Extrinseca" width="600">
</div>

Let's jump straight to the concrete practical examples of extraneous cognitive load.

Vamos directamente a ejemploc concretos  de Carga Cognotiva Extrinseca.

---

We will refer to the level of cognitive load as follows:`🧠`: fresh working memory, zero cognitive load `🧠++`: two facts in our working memory, cognitive load increased `🤯`: cognitive overload, more than 4 facts

Nos vamos a referir a los niveles de carga cognitiva como sigue: `🧠`: memoria de trabajo fresca, sin carga cognitiva `🧠++`: al menos dos datos en nuestra memoria de trabajo, carga cognitiva moderada `🤯`: sobrecarga cognitiva, más de 4 datos

> Our brain is much more complex and unexplored, but we can go with this simplistic model.

**Nota**: En los ejemplos de codigo mantendremos la convencion de nombres de variables, funciones, metodos etc. en ingles, lo comentarios explicativos si los traduciremos.

## Complex conditionals

## Condicionales complejas

```go
if val > someConstant // 🧠+
    && (condition2 || condition3) // 🧠+++, prev cond should be true, one of c2 or c3 has to be true
				  // 🧠+++, la condición anterior debe ser verdadera, y una de las condiciones C2 o C3 también debe ser verdadera
    && (condition4 && !condition5) { // 🤯, we are messed up by this point
				     // 🤯, Estamos completamente perdidos en este punto.
    ...
}
```

Introduce intermediate variables with meaningful names:

Utilice variables intermedias con nombres descriptivos:

```go
isValid = val > someConstant
isAllowed = condition2 || condition3
isSecure = condition4 && !condition5 
// 🧠, we don't need to remember the conditions, there are descriptive variables
// 🧠 No necesitamos memorizar las condiciones, existen variables descriptivas de la evaluacion.
if isValid && isAllowed && isSecure {
    ...
}
```

## Nested ifs Ifs Anidados

```go
if isValid { // 🧠+, okay nested code applies to valid input only
	     // 🧠+, el código anidado solo se aplica a entradas válidas
    if isSecure { // 🧠++, we do stuff for valid and secure input only
		  // 🧠++, solo realizamos acciones con entradas de datos válidas y seguras
        stuff // 🧠+++
    }
} 
```

Compare it with the early returns:

Comparemos con el codigo anterior::

```go
if !isValid
    return
 
if !isSecure
    return

// 🧠, we don't really care about earlier returns, if we are here then all good
// 🧠, no nos importa si hubo devoluciones anteriores; si estamos aquí, todo está bien.

stuff // 🧠+
```

We can focus on the happy path only, thus freeing our working memory from all sorts of preconditions.

De este modo nos enfocamos únicamente en el escenario ideal, liberando así nuestra memoria de trabajo de todo tipo de condicionamientos previos.

## Inheritance nightmare 

## La Pesadilla de la Herencia

We are asked to change a few things for our admin users: `🧠`

Se nos ha solicitado realizar algunos cambios para nuestros usuarios administradores: 🧠

`AdminController extends UserController extends GuestController extends BaseController`

Ohh, part of the functionality is in `BaseController`, let's have a look: `🧠+`

Oh!, parte de nuestra funcionalidad esta en `BaseController`, echemeos un vistazo: `🧠+`
Basic role mechanics got introduced in `GuestController`: 🧠++ 
Las mecánicas básicas de los roles se introdujeron en  `GuestController`: `🧠++`

Las mecánicas básicas de los roles se introdujeron en  `GuestController`: `🧠++`
Things got partially altered in `UserController`: `🧠+++ `
Las cosas cambiaron parcialmente en `UserController`: `🧠+++ `
Finally we are here, `AdminController`, let's code stuff! `🧠++++`
Oh, wait, there's `SuperuserController` which extends `AdminController`. By modifying `AdminController` we can break things in the inherited class, so let's dive in `SuperuserController` first: `🤯 `
¡Un momento!, existe el controlador `SuperuserController` que hereda de `AdminController`. Si modificamos `AdminController`, podríamos causar problemas en la clase heredada, así que primero analicemos `SuperuserController`: `🤯`

Prefer composition over inheritance. We won't go into detail - there's [plenty of material](https://www.youtube.com/watch?v=hxGOiiR9ZKg) out there. 

**Es preferible utilizar la composición en lugar de la herencia.**No vamos a entrar en detalles; hay mucha información disponible [aquí](https://www.youtube.com/watch?v=hxGOiiR9ZKg).

## Too many small methods, classes or modules 

## Demasiados métodos, clases y/o módulos pequeños.

> Method, class and module are interchangeable in this context
>
> En este contexto, los términos método, clase y módulo son intercambiables.

Mantras like "methods should be shorter than 15 lines of code" or "classes should be small" turned out to be somewhat wrong.

Resultó que principios como "los métodos deben tener menos de 15 líneas de código" o "las clases deben ser pequeñas", eran en cierto modo erróneos.

**Deep module** - simple interface, complex functionality
**Modulo Profundo** - interfaz simple, funcionalidad compleja
**Shallow module** - interface is relatively complex compared to the small functionality it provides
**Modulo de funcionalidad limitada** - la intyerfaz es relativamente compleja comparada a la funcionalidad relativamente simple que provee.

<div align="center">
  <img src="/img/deepmodulev8.png" alt="Deep module" width="700">
</div>

Having too many shallow modules can make it difficult to understand the project. **Not only do we have to keep in mind each module's responsibilities, but also all their interactions.** To understand the purpose of a shallow module, we first need to look at the functionality of all the related modules. Jumping between such shallow components is mentally exhausting, `<a target="_blank" href="https://blog.separateconcerns.com/2023-09-11-linear-code.html">`linear thinking `</a>` is more natural to us humans.

El tener muchos peuqeños modulos puede dificultar el entender un proyecto. **No solo tenemos que mantener en mente cada una de las responsabilidades, sino ademas sus interacciones.** Para poder entender el proposito de un modulo con poca funcionalidad necesitamos mirar tofdas las funcionalidades asociadas de todos los modulos asociados. Navegar ente tantos modulos pequeños puede resultar mentalmente agotador, el  `<a target="_blank" href="https://blog.separateconcerns.com/2023-09-11-linear-code.html">`pensamiento lineas `</a>` nos resulta mas comodo y natural.

> Information hiding is paramount, and we don't hide as much complexity in shallow modules.
>
>
> La encapsulacion de información es fundamental, y no intentamos ocultar mucha complejidad en los módulos más simples.

I have two pet projects, both of them are somewhat 5K lines of code. The first one has 80 shallow classes, whereas the second one has only 7 deep classes. I haven't been maintaining any of these projects for one year and a half.

Tengo dos proyectos personales, ambos con aproximadamente 5k líneas de código. El primero tiene unas 80 clases sencillas, mientras que el segundo solo tiene 7 clases complejas. No he realizado ningún mantenimiento en ninguno de estos proyectos durante el último año y medio.

Once I came back, I realised that it was extremely difficult to untangle all the interactions between those 80 classes in the first project. I would have to rebuild an enormous amount of cognitive load before I could start coding. On the other hand, I was able to grasp the second project quickly, because it had only a few deep classes with a simple interface.

Una vez que  los retome, me di cuenta de que era extremadamente difícil comprender todas las interacciones entre las 80 clases del primer proyecto. Tendría que volver a aprender una gran cantidad de conceptos antes de poder empezar a programar. Por otro lado, el segundo proyecto fue fácil de entender, ya que solo tenía unas pocas clases complejas con una interfaz sencilla.

> Los mejores componentes son aquellos que ofrecen una funcionalidad potente pero con una interfaz sencilla.
>
> *John Ousterhout, A Philosophy of Software Design (Una filosofía del diseño de software)*

The interface of the UNIX I/O is very simple. It has only five basic calls:

La interfaz de I/O de UNIX es muy simple. Solo tiene cinco llamadas básicas:

```python
open(path, flags, permissions)
read(fd, buffer, count)
write(fd, buffer, count)
lseek(fd, offset, referencePosition)
close(fd)
```

A modern implementation of this interface has **hundreds of thousands of lines of code.** Lots of complexity is hidden under the hood. Yet it is easy to use due to its simple interface.

Una implementación moderna de esta interfaz cuenta con **cientos de miles de líneas de código**. A pesar de su gran complejidad interna, su interfaz sencilla la hace muy fácil de usar.

> This deep module example is taken from the book [A Philosophy of Software Design](https://web.stanford.edu/~ouster/cgi-bin/book.php) by John Ousterhout. Not only does this book cover the very essence of complexity in software development, but it also has the greatest interpretation of Parnas' influential paper [On the Criteria To Be Used in Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf). Both are essential reads. Other related readings: [A Philosophy of Software Design vs Clean Code](https://github.com/johnousterhout/aposd-vs-clean-code), [It&#39;s probably time to stop recommending Clean Code](https://qntm.org/clean), [Small Functions considered Harmful](https://copyconstruct.medium.com/small-functions-considered-harmful-91035d316c29).
>
> El ejemplo de modulo complejo es extraido del libro  [A Philosophy of Software Design](https://web.stanford.edu/~ouster/cgi-bin/book.php) por John Ousterhout. No solo aborda la esencia de la complejidad en el desarrollo de software, sino que ofrece la mejor interpretacion del influyente artioculo de Parnas titulado [On the Criteria To Be Used in Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf). Ambas son lecturas escenciales.Otras lecturas relacionada pueden ser: [A Philosophy of Software Design vs Clean Code](https://github.com/johnousterhout/aposd-vs-clean-code), [It&#39;s probably time to stop recommending Clean Code](https://qntm.org/clean), [Small Functions considered Harm](https://copyconstruct.medium.com/small-functions-considered-harmful-91035d316c29)

<details>
    <summary><b>Important things should be big, examples</b></summary>
    <br>
    <div align="center">
        <img src="/img/dirty.png" alt="Clean vs Dirty" width="600">
    </div>
    <blockquote>If you allow your important "crux" functions to be larger ("dirty") it is easier to pick them out from the sea of functions, they are obviously important: just look at them, they are big!</blockquote>
    This picture is taken from <a href="https://htmx.org/essays/codin-dirty/" target="_blank">Codin' Dirty</a> article by Carson Gross. You'll find <a href="https://htmx.org/essays/codin-dirty/#real-world-examples" target="_blank">real world examples</a> of deep functions there.
</details>



<details>
    <summary><b>Las cosas importantes deben ser grandes: ejemplos</b></summary>
    <br>
    <div align="center">
        <img src="/img/dirty.png" alt="Limpio vs Sucio" width="600">
    </div>
    <blockquote>Si permitimos que las funciones "centrales" importantes sean más grandes ("sucias"), es más fácil distinguirlas del mar de funciones; son obviamente importantes: ¡solo míralas!</blockquote>
    Esta imagen ha sido tomada del artículo <a href="https://htmx.org/essays/codin-dirty/" target="_blank">Codin' Dirty</a> de Carson Gross. Allí encontrarás <a href="https://htmx.org/essays/codin-dirty/#real-world-examples" target="_blank">ejemplos reales</a> de funciones profundas.
</details>


P.S. If you think we are rooting for bloated God objects with too many responsibilities, you got it wrong.

PD: Si crees que estamos defendiendo la idea de clases con una funcionalidad excesiva y demasiadas responsabilidades, estás equivocado.

## Responsible for one thing 

## Responsables de una funcion

All too often, we end up creating lots of shallow modules, following some vague "a module should be responsible for one, and only one, thing" principle. What is this blurry one thing? Instantiating an object is one thing, right? So [MetricsProviderFactoryFactory](https://minds.md/benji/frameworks) seems to be just fine. **The names and interfaces of such classes tend to be more mentally taxing than their entire implementations, what kind of abstraction is that?** Something went wrong.

Muy frecuentemente, terminamos crado numeroso modulos simplistas, siguien el principio ambiguo de "un modulo debe ser responsable por uno, y solo una funcion" ¿Pero qué significa exactamente esa "única función"? ¿Acaso instanciar un objeto es una función?Entonces, [MetricsProviderFactoryFactory](https://minds.md/benji/frameworks)MetricsProviderFactoryFactoryparece estar bien. **Sin embargo, los nombres e interfaces de estas clases suelen ser más difíciles de comprender que su implementación completa. ¿Qué tipo de abstracción es esa?** Algo falla en este enfoque.

We make changes to our systems to satisfy our users and stakeholders. We are responsible to them.

Realizamos mejoras en nuestros sistemas para satisfacer las necesidades de nuestros usuarios y demás partes interesadas. Somos responsables ante ellos.

Nota: stakeholders normalmente se usa en el ambito de las ibersiones y refiere al inversionanista, el mismo es la parte interesada en el funcionamiento de la inversion. En nuestro caso y contexto solo refiere a una parte interesada por el funcionamiento del codigo, al no encontrar una palabra que pueda sustituir directamente esta idea la hemos dejado como 'parte interesada'.

> A module should be responsible to one, and only one, user or stakeholder.
>
> Un módulo debe ser responsable ante un único usuario o interesado.

This is what this Single Responsibility Principle is all about. Simply put, if we introduce a bug in one place, and then two different business people come to complain, we've violated the principle. It has nothing to do with the number of things we do in our module.

De eso se trata el Principio de Responsabilidad única. En pocas palabras, si introducimos un error en un punto concreto y dos personas de diferentes departamentos se quejan por ello, estamos violando dicho principio. Esto no tiene nada que ver con la cantidad de funciones que incluimos en nuestro módulo.

But even now, this rule can do more harm than good. This principle can be understood in as many different ways as there are individuals. A better approach would be to look at how much cognitive load it all creates. It's mentally demanding to remember that change in one place can trigger a chain of reactions across different business streams. And that's about it, no fancy terms to learn.

Pero incluso hoy en día, esta regla puede generar más mal que bien. Este principio puede interpretarse de muchas maneras, dependiendo de cada persona. Un enfoque más acertado sería analizar la carga cognitiva que implica. Es difícil recordar mentalmente que un cambio en un área puede desencadenar una serie de reacciones en diferentes procesos de la empresa. Y eso es todo; no hace falta aprender términos complicados.

## Too many shallow microservices

This shallow-deep module principle is scale-agnostic, and we can apply it to microservices architecture. Too many shallow microservices won't do any good - the industry is heading towards somewhat "macroservices", i.e., services that are not so shallow (=deep). One of the worst and hardest to fix phenomena is so-called distributed monolith, which is often the result of this overly granular shallow separation.

I once consulted a startup where a team of five developers introduced 17(!) microservices. They were 10 months behind schedule and appeared nowhere close to the public release. Every new requirement led to changes in 4+ microservices. It took an enormous amount of time to reproduce and debug an issue in such a distributed system. Both time to market and cognitive load were unacceptably high. `🤯`

Is this the right way to approach the uncertainty of a new system? It's enormously difficult to elicit the right logical boundaries in the beginning. The key is to make decisions as late as you can responsibly wait, because that is when you have the most information at hand. By introducing a network layer up front, we make our design decisions hard to revert right from the start. The team's only justification was: "The FAANG companies proved microservices architecture to be effective". *Hello, you got to stop dreaming big.*

The [Tanenbaum-Torvalds debate](https://en.wikipedia.org/wiki/Tanenbaum%E2%80%93Torvalds_debate) argued that Linux's monolithic design was flawed and obsolete, and that a microkernel architecture should be used instead. Indeed, the microkernel design seemed to be superior "from a theoretical and aesthetical" point of view. On the practical side of things - three decades on, microkernel-based GNU Hurd is still in development, and monolithic Linux is everywhere. This page is powered by Linux, your smart teapot is powered by Linux. By monolithic Linux.

A well-crafted monolith with truly isolated modules is often much more flexible than a bunch of microservices. It also requires far less cognitive effort to maintain. It's only when the need for separate deployments becomes crucial, such as scaling the development team, that you should consider adding a network layer between the modules, future microservices.

## Feature-rich languages

We feel excited when new features got released in our favourite language. We spend some time learning these features, we build code upon them.

If there are lots of features, we may spend half an hour playing with a few lines of code, to use one or another feature. And it's kind of a waste of time. But what's worse, **when you come back later, you would have to recreate that thought process!**

**You not only have to understand this complicated program, you have to understand why a programmer decided this was the way to approach a problem from the features that are available.** `🤯`

These statements are made by none other than Rob Pike.

> Reduce cognitive load by limiting the number of choices.

Language features are OK, as long as they are orthogonal to each other.

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

## Business logic and HTTP status codes

On the backend we return:
`401` for expired JWT token
`403` for not enough access
`418` for banned users

The engineers on the frontend use backend API to implement login functionality. They would have to temporarily create the following cognitive load in their brains:
`401` is for expired JWT token // `🧠+`, ok just temporarily remember it
`403` is for not enough access // `🧠++`
`418` is for banned users // `🧠+++`

Frontend developers would (hopefully) introduce some kind `numeric status -> meaning` dictionary on their side, so that subsequent generations of contributors wouldn't have to recreate this mapping in their brains.

Then QA engineers come into play:
"Hey, I got `403` status, is that expired token or not enough access?"
**QA engineers can't jump straight to testing, because first they have to recreate the cognitive load that the engineers on the backend once created.**

Why hold this custom mapping in our working memory? It's better to abstract away your business details from the HTTP transfer protocol, and return self-descriptive codes directly in the response body:

```json
{
    "code": "jwt_has_expired"
}
```

Cognitive load on the frontend side: `🧠` (fresh, no facts are held in mind)
Cognitive load on the QA side: `🧠`

The same rule applies to all sorts of numeric statuses (in the database or wherever) - **prefer self-describing strings.** We are not in the era of 640K computers to optimise for memory.

> People spend time arguing between `401` and `403`, making decisions based on their own mental models. New developers are coming in, and they need to recreate that thought process. You may have documented the "whys" (ADRs) for your code, helping newcomers to understand the decisions made. But in the end it just doesn't make any sense. We can separate errors into either user-related or server-related, but apart from that, things are kind of blurry.

P.S. It's often mentally taxing to distinguish between "authentication" and "authorization". We can use simpler terms like [&#34;login&#34; and &#34;permissions&#34;](https://ntietz.com/blog/lets-say-instead-of-auth/) to reduce the cognitive load.

## Abusing DRY principle

Do not repeat yourself - that is one of the first principles you are taught as a software engineer. It is so deeply embedded in ourselves that we can not stand the fact of a few extra lines of code. Although in general a good and fundamental rule, when overused it leads to the cognitive load we can not handle.

Nowadays, everyone builds software based on logically separated components. Often those are distributed among multiple codebases representing separate services. When you strive to eliminate any repetition, you might end up creating tight coupling between unrelated components. As a result, changes in one part may have unintended consequences in other seemingly unrelated areas. It can also hinder the ability to replace or modify individual components without impacting the entire system. `🤯`

In fact, the same problem arises even within a single module. You might extract common functionality too early, based on perceived similarities that might not actually exist in the long run. This can result in unnecessary abstractions that are difficult to modify or extend.

Rob Pike once said:

> A little copying is better than a little dependency.

We are tempted to not reinvent the wheel so strongly that we are ready to import large, heavy libraries to use a small function that we could easily write by ourselves.

**All your dependencies are your code.** Going through 10+ levels of stack trace of some imported library and figuring out what went wrong (*because things go wrong*) is painful.

## Tight coupling with a framework

There's a lot of "magic" in frameworks. By relying too heavily on a framework, **we force all upcoming developers to learn that "magic" first.** It can take months. Even though frameworks enable us to launch MVPs in a matter of days, in the long run they tend to add unnecessary complexity and cognitive load.

Worse yet, at some point frameworks can become a significant constraint when faced with a new requirement that just doesn't fit the architecture. From here onwards people end up forking a framework and maintaining their own custom version. Imagine the amount of cognitive load a newcomer would have to build (i.e. learn this custom framework) in order to deliver any value. `🤯`

**By no means do we advocate to invent everything from scratch!**

We can write code in a somewhat framework-agnostic way. The business logic should not reside within a framework; rather, it should use the framework's components. Put a framework outside of your core logic. Use the framework in a library-like fashion. This would allow new contributors to add value from day one, without the need of going through debris of framework-related complexity first.

> [Why I Hate Frameworks](https://minds.md/benji/frameworks)

## Layered architecture

There is a certain engineering excitement about all this stuff.

I myself was a passionate advocate of Hexagonal/Onion Architecture for years. I used it here and there and encouraged other teams to do so. The complexity of our projects went up, the sheer number of files alone had doubled. It felt like we were writing a lot of glue code. On ever changing requirements we had to make changes across multiple layers of abstractions, it all became tedious. `🤯`

**Abstraction is supposed to hide complexity, here it just adds [indirection](https://fhur.me/posts/2024/thats-not-an-abstraction).** Jumping from call to call to read along and figure out what goes wrong and what is missing is a vital requirement to quickly solve a problem. With this architecture’s layer uncoupling it requires an exponential factor of extra, often disjointed, traces to get to the point where the failure occurs. Every such trace takes space in our limited working memory. `🤯`

This architecture was something that made intuitive sense at first, but every time we tried applying it to projects it did more harm than good. We spent years on unnecessary mental activity and writing useless glue code with no clear business value. On the contrary, we made things worse for the business by forcing newcomers to learn our approaches (mental models) first. The time to market has worsened. In the end, we gave it all up in favour of the good old dependency inversion principle. **No port/adapter terms to learn, no unnecessary layers of horizontal abstractions, no extraneous cognitive load.**

<details>
    <summary><b>Coding principles and experience</b></summary>
    <div align="center">
        <img src="img/complexity.png" alt="Super simple code" width="500">
    </div>
    <a href="https://twitter.com/flaviocopes">@flaviocopes</a>
</details>

If you think that such layering will allow you to quickly replace a database or other dependencies, you're mistaken. Changing the storage causes lots of problems, and believe us, having some abstractions for the data access layer is the least of your worries. At best, abstractions can save somewhat 10% of your migration time (if any), the real pain is in data model incompatibilities, communication protocols, distributed systems challenges, and [implicit interfaces](https://www.hyrumslaw.com).

> With a sufficient number of users of an API,
> it does not matter what you promise in the contract:
> all observable behaviours of your system
> will be depended on by somebody.

We did a storage migration, and that took us about 10 months. The old system was single-threaded, so the exposed events were sequential. All our systems depended on that observed behaviour. This behaviour was not part of the API contract, it was not reflected in the code. A new distributed storage didn't have that guarantee - the events came out-of-order. We spent only a few hours coding a new storage adapter, thanks to an abstraction. **We spent the next 10 months on dealing with out-of-order events and other challenges.** It's now funny to say that abstractions help us replace components quickly.

**So, why pay the price of high cognitive load for such a layered architecture, if it doesn't pay off in the future?** Plus, in most cases, that future of replacing some core component never happens.

These architectures are not fundamental, they are just subjective, biased consequences of more fundamental principles. Why rely on those subjective interpretations? Follow the fundamental rules instead: dependency inversion principle, single source of truth, cognitive load and information hiding. Your business logic should not depend on low-level modules like database, UI or framework. We should be able to write tests for our core logic without worrying about the infrastructure, and that's it. [Discuss](https://github.com/zakirullin/cognitive-load/discussions/24).

Do not add layers of abstractions for the sake of an architecture. Add them whenever you need an extension point that is justified for practical reasons.

**[Layers of abstraction aren&#39;t free of charge](https://blog.jooq.org/why-you-should-not-implement-layered-architecture), they are to be held in our limited working memory.**

<div align="center">
  <img src="/img/layers.png" alt="Layers" width="400">
</div>

## Domain-driven design

Domain-driven design has some great points, although it is often misinterpreted. People say, "We write code in DDD", which is a bit strange, because DDD is more about the problem space rather than the solution space.

Ubiquitous language, domain, bounded context, aggregate, event storming are all about problem space. They are meant to help us learn the insights about the domain and extract the boundaries. DDD enables developers, domain experts and business people to communicate effectively using a single, unified language. Rather than focusing on these problem space aspects of DDD, we tend to emphasise particular folder structures, services, repositories, and other solution space techniques.

Chances are that the way we interpret DDD is likely to be unique and subjective. And if we build code upon this understanding, i.e., if we create a lot of extraneous cognitive load - future developers are doomed. `🤯`

Team Topologies provides a much better, easier to understand framework that helps us split the cognitive load across teams. Engineers tend to develop somewhat similar mental models after learning about Team Topologies. DDD, on the other hand, seems to be creating 10 different mental models for 10 different readers. Instead of being common ground, it becomes a battleground for unnecessary debates.

## Cognitive load in familiar projects

> The problem is that **familiarity is not the same as simplicity.** They *feel* the same — that same ease of moving through a space without much mental effort — but for very different reasons. Every “clever” (read: “self-indulgent”) and non-idiomatic trick you use incurs a learning penalty for everyone else. Once they have done that learning, then they will find working with the code less difficult. So it is hard to recognise how to simplify code that you are already familiar with. This is why I try to get “the new kid” to critique the code before they get too institutionalised!
>
> It is likely that the previous author(s) created this huge mess one tiny increment at a time, not all at once. So you are the first person who has ever had to try to make sense of it all at once.
>
> In my class I describe a sprawling SQL stored procedure we were looking at one day, with hundreds of lines of conditionals in a huge WHERE clause. Someone asked how anyone could have let it get this bad. I told them: “When there are only 2 or 3 conditionals, adding another one doesn’t make any difference. By the time there are 20 or 30 conditionals, adding another one doesn’t make any difference!”
>
> There is no “simplifying force” acting on the code base other than deliberate choices that you make. Simplifying takes effort, and people are too often in a hurry.
>
> *Thanks to [Dan North](https://dannorth.net) for his comment*.

If you've internalized the mental models of the project into your long-term memory, you won't experience a high cognitive load.

<div align="center">
  <img src="/img/mentalmodelsv15.png" alt="Mental models" width="700">
</div>

The more mental models there are to learn, the longer it takes for a new developer to deliver value.

Once you onboard new people on your project, try to measure the amount of confusion they have (pair programming may help). If they're confused for more than ~40 minutes in a row - you've got things to improve in your code.

If you keep the cognitive load low, people can contribute to your codebase within the first few hours of joining your company.

## Examples

- Our architecture is a standard CRUD app architecture, [a Python monolith on top of Postgres](https://danluu.com/simple-architectures/)
- How Instagram scaled to 14 million users with [only 3 engineers](https://read.engineerscodex.com/p/how-instagram-scaled-to-14-million)
- The companies where we were like ”woah, these folks are [smart as hell](https://kenkantzer.com/learnings-from-5-years-of-tech-startup-code-audits/)” for the most part failed
- One function that wires up the entire system. If you want to know how the system works - [go read it](https://www.infoq.com/presentations/8-lines-code-refactoring)

These architectures are quite boring and easy to understand. Anyone can grasp them without much mental effort.

Involve junior developers in architecture reviews, they will help you to identify the mentally demanding areas.

> Software systems are perhaps the most intricate and complex (in terms of number of distinct kinds of parts) of the things humanity makes.
>
> *Fred Brooks, The Mythical Man-Month*

**Maintaining software is hard**, things break and we would need every bit of mental effort we can save. The fewer components there are in the system, the fewer issues there will be. Debugging will also be less mentally taxing.

> Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.
>
> *Brian Kernighan*

In general, the mindset "Wow, this architecture sure feels good!" is misleading. That's "a point in time" subjective feeling, and it says nothing about the reality. A far better approach is to observe the consequences in the long run:

- Is it easy to reproduce and debug an issue? Or do you have to jump across the call stacks or distributed components, trying to make sense of everything in your head?
- Can we make changes quickly, or are there a lot of unknown unknowns, and people are afraid to touch things?
- Can new people add features quickly? Are there some unique mental models to learn?

> What are those unique mental models? It's some set of rules, usually a mixture of DDD/CQRS/Clean Architecture/Event Driven Architecture. This is an author's own interpretation of the things that excite him the most. His own subjective mental models. **Extraneous cognitive load that others have to internalize.**

These questions are far harder to track, and people often don't like to answer them directly. Look at some of the most complex software systems in the world, the ones that have stood the test of time - Linux, Kubernetes, Chrome and Redis (see comments below). You will not find anything fancy there, it's boring for the most part, and that's a good thing.

## Conclusion

Imagine for a moment that what we inferred in the second chapter isn’t actually true. If that’s the case, then the conclusion we just negated, along with the conclusions in the previous chapter that we had accepted as valid, might not be correct either. `🤯`

Do you feel it? Not only do you have to jump all over the article to get the meaning (shallow modules!), but the paragraph in general is difficult to understand. We have just created an unnecessary cognitive load in your head. **Do not do this to your colleagues.**

<div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="Smart author" width="600">
</div>

We should reduce any cognitive load above and beyond what is intrinsic to the work we do.

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
