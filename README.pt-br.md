# Carga Cognitiva é o que importa

[Versão Legível](https://minds.md/zakirullin/cognitive) | [Original](README.md)

*Este é um documento vivo, última atualização da tradução: **Setembro de 2025**. Contribuições são bem vindas!*

## Introdução

Extistem muitas palavras na moda e melhores práticas por aí, mas maior parte delas tem falhado. Elas falharam porque foram imaginadas, ao invés de se basearem na realidade. Essas ideias foram baseadas na estética e julgamentos subjetivos. Precisamos de algo mais fundamental, algo que não possa estar errado.

Algumas vezes sentimos uma confusão ocorrendo no código. Confusão que custa tempo e dinheiro. Confusão esta, causada pela *alta carga cognitiva*. Este não é apenas algum conceito abstrato chique, mas uma **limitação fundamental humana**. Não é imaginado, é algo que está lá e podemos sentir.

Já que gastamos muito mais tempo lendo e compreendendo código que escrevendo, poderíamos constantemente nos questionar se estamos embarcando carga cognitiva excessiva em nosso código.

## Carga Cognitiva
> Carga cognitiva é o quanto um desenvolvedor precisa pensar para completar uma tarefa.

Quando lê-se o código, você coloca coisas como valores de variáveis, controles de fluxo e sequências de chamadas em sua cabeça. A pessoa média consegue guardar aproximadamente [quatro desses blocos](https://github.com/zakirullin/cognitive-load/issues/16) em sua memória de trabalho. Uma vez que a carga cognitiva atinge tal limite, se torna muito mais difícil de compreender as coisas.

*Digamos que fomos pedidos para fazer alguns consertos em um projeto completamente não-familiar. Disseram-nos que um desenvolvedor realmente inteligente tem contribuído para o mesmo. Muitas arquiteturas legais, bibliotecas fantásticas e tecnologias novas e da moda foram usadas. Em outras palavras, **O autor criou uma alta carga cognitiva deixada para nós.***

<div align="center">
  <img src="/img/cognitiveloadv6.png" alt="Cognitive load" width="750">
</div>

Deveríamos reduzir a carga cognitiva em nossos projetos o máximo possível.

<details>
  <summary><b>Carga cognitiva e interrupções</b></summary>
  <img src="img/interruption.jpeg"><br>
</details>

> Usaremos "carga cognitiva" de maneira informal; por vezes alinhará com o conceito científico específico de Carga Cognitiva, mas não sabemos o suficiente quando alinhará ou não.

## Tipos de carga cognitiva
**Intrínseca** - causada pela dificuldade inerente da tarefa. Não pode ser reduzido, já que se está na cerne do desenvolvimento do *software*.

**Extrínseca** - criada pela forma que a informação é apresentada. Causada por fatores não diretamente relevantes à tarefa, como as peculiaridades do autor inteligente. Pode ser grandemente reduzida. Focaremos nesse tipo de carga cognitiva.

<div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="Intrínseca vs Extrínseca" width="600">
</div>

Pularemos direto aos exemplos práticos e concretos de carga cognitiva extrínseca.

---

Referiremos ao nível de carga coginitiva como a seguinte:
`🧠`: memória de trabalho fresca, nenhuma carga coginitiva  
`🧠++`: dois fatos em nossa memória de trabalho, carga cognitiva aumentada
`🤯`: sobrecarga cognitiva, mais de 4 fatos

> Nosso cérebro é muito mais complexo e não explorado, mas podemos seguir neste modelo simplístico.

## Condicionais complexas
```go
if val > someConstant // 🧠+
    && (condition2 || condition3) // 🧠+++, condição prévia deve ser verdadeira, uma de c2 ou c3 tem de ser verdadeira
    && (condition4 && !condition5) { // 🤯, estamos confusos neste momento
    ...
}
```

Introduza variáveis intermediárias com nomes significativos:
```go
isValid = val > someConstant
isAllowed = condition2 || condition3
isSecure = condition4 && !condition5 
// 🧠, não precisamos lembrar as condições, elas são variáveis descritivas
if isValid && isAllowed && isSecure {
    ...
}
```

## Ifs aninhados
```go
if isValid { // 🧠+, ok, código aninhado se aplica a entradas válidas apenas
    if isSecure { // 🧠++, fazemos a tarefa apenas para entradas válidas e seguras 
        stuff // 🧠+++
    }
}
```

Compare agora com *early returns*:
```go
if !isValid
    return
 
if !isSecure
    return

// 🧠, não realmente ligamos para retornos breves, se estamos aqui, então tudo certo

stuff // 🧠+
```

Podemos focar no caminho feliz apenas, liberando nossa memória de trabalho de todos esses tipos de pré-condições.

## Pesadelo de herança

Fomos pedidos para mudar algumas coisas para nossos usuários administradores: `🧠`

`AdminController extends UserController extends GuestController extends BaseController`

Ahh, parte da functionalidade está em `BaseControler`, vamos dar uma olhada: `🧠+`
O mecanismo básico foi introduzido em `GuestController`: `🧠++`
Algumas coisas foram parcialmente alteradas em `UserController`: `🧠+++`
Finalmente, estamos aqui, `AdminController`, vamos programar nossa tarefa! `🧠++++`

Ei, espera! Existe um `SuperuserController` que extende `AdminController`. Ao modificar `AdminController`, podemos quebrar partes da classe herdeira, vamos mergulhar em `SuperuserController` primeiro: `🤯`

Prefira composição à herança. Não vamos entrar em muitos detalhes - existem uma [variedade de materiais](https://www.youtube.com/watch?v=hxGOiiR9ZKg) por aí.

## Pequenos métodos, classes ou módulos demasiados

> Método, classes e módulos são intercambiáveis neste contexto.

Mantras como "métodos deveriam ser menores que 15 linhas de código" ou "classes deveriam ser pequenas" se tornaram em algo errado.

**Módulo profundo** - interface simples, funcionalidade complexa
**Módulo raso** - interface relativamente complexa comparada à pequena funcionalidade que isso provê.

<div align="center">
  <img src="/img/deepmodulev8.png" alt="Módulo Profundo" width="700">
</div>

Ter muitos módulos rasos pode tornar o projeto difícil de compreender. **Não apenas temos de manter em mente a responsabilidade de cada módulo, como também suas interações**. Para compreender o propósito de um módulo raso vamos precisar olhar para a funcionalidade de todos os módulos relacionados. Pular entre cada componente raso é mentalmente exaustivo <a target="_blank" href="https://blog.separateconcerns.com/2023-09-11-linear-code.html">pensamento linear</a> é mais natural para nós, humanos.

> Ocultar informação é fundamental, não precisamos ocultar tanto a complexidade em módulos rasos.

Eu tenho dois projetos pet. Ambos com algo entre 5 mil linhas de código. O primeiro tem 80 classes rasas, enquanto o segundo tem apenas 7 classes profundas. Eu não tenho mantido nenhum dos dois projetos por um ano e meio.

Ao retornar, eu percebi o quão extremamente difícil é para desembaraçar todas as interações entre essas 80 classes do primeiro projeto. Eu teria de reconstruir a quantidade enorme de carga coginitiva antes que pudesse começar a programar. Por outro lado, eu fui capaz de compreender o segundo projeto rapidamente, já que tinham apenas algumas classes profundas com interfaces simples.

> Os melhores componentes são aqueles que provém funcionalidades poderosas enquanto mantém interfaces simples.
> 
> *John Ousterhout, Um Filósofo de Deisgn de Software*

A interface do *UNIX I/O* é bastante simples. Ele tem apenas cinco básicas chamadas.

```py
open(caminho, bandeiras, permissões)
read(da, buffer, contagem)
read(da, buffer, contagem)
lseek(da, desvio, posiçãoDeReferencia)
close(da)
```

Uma implementação moderna dessa interface tem **centeras de milhares de linhas de código**. Muitas das complexidades estão ocultas por debaixo do capô. Ainda assim, é fácil de usar devido a sua simples interface.

> Esse exemplo de módulo profundo é tirado do livro *[A Philosophy of Software Design](https://web.stanford.edu/~ouster/cgi-bin/book.php)* por John Ousterhout. Não apenas este livro cobre bastante a essência da complexidade no desenvolvimento de *Software*, mas também tem a melhor interpretação do artigo influencial de Parnas *[On the Criteria To Be Used In Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf)*. Ambos são essenciais de ler. Outras leituras relacionadas: *[A Philosophy of Software Design vs Clean Code](https://github.com/johnousterhout/aposd-vs-clean-code)*, *[It's probably time to stop recommending Clean Code](https://qntm.org/clean)*, *[Small Functions considered Harmful](https://copyconstruct.medium.com/small-functions-considered-harmful-91035d316c29)*.

<details>
    <summary><b>Coisas importantes deviam ser grandes, exemplos</b></summary>
    <br>
    <div align="center">
        <img src="/img/dirty.png" alt="Clean vs Dirty" width="600">
    </div>
    <blockquote>
      Se você permitir seu "crux" importante de funções serem maiores, sujas ("dirty"), será mais fácil de escolhê-las dentro de um mar de funções, elas serão obviamente importantes: apenas olhe para elas, elas são grandes!
    </blockquote>

  Esta imagem foi tiradas de <a href="https://htmx.org/essays/codin-dirty/" target="_blank">Codin' Dirty</a>, artigo por Carson Gross. Você encontrará <a href="https://htmx.org/essays/codin-dirty/#real-world-examples" target="_blank"> exemplos do mundo real</a> de funções profundas aí.
</details>

P.S. Caso pense que estamos enraizando objetos divinos inchados com muitas responsabilidades, você compreendeu errado.

## Responsável por uma única coisa

Frequentemente, acabamos por criar muitos módulos rasos, seguindo vagos princípios como "um módulo deveria ser responsável por uma coisa, e apenas uma única coisa". O que seria esse borrão? Instanciar um objeto é uma coisa, correto? Então [MetricsProviderFactoryFactory](https://minds.md/benji/frameworks) parece ser correto. **Os nomes e interfaces destas classes tendem a ser mentalmente desgastantes. Mais que sua implementação completa. Que tipo de abstração é essa?** Algo está errado.

Fazemos mudanças em nossos sistemas para satisfazer nossos usuários e *Stakeholders*. Somos responsáveis por eles.

> Um módulo deveria ser responsável por um, e apenas um, usuário ou *Stakeholder*.

Isso é o que o *Princípio da Responsabilidade Única* (*Single Responsibility Principle*) é sobre. Em termos simples, se introduzirmos um bug em um lugar e, em seguida, dois profissionais de negócios diferentes vierem reclamar, teremos violado o princípio. Isso não tem nada a ver com o número de coisas que fazemos em nosso módulo.

Mas ainda assim, esta regras pode ser mais danosa que boa. Esse princípio pode ser compreendido de múltiplas formas como há de pessoas na terra. Uma forma melhor seria a de olhar para a quantidade de carga cognitiva que ele pode criar. Esta é a demanda mental para lembrar que mudar em um lugar pode ativar uma cadeia de reações em diferentes fluxos de negócios.

## Muitos microsserviços rasos

Esse princípio de módulo raso-profundo é agnóstico à escala, e podemos aplicá-lo à arquitetura de microsserviços. Uma quantidade excessiva de microsserviços rasos não traz nenhum benefício - a indústria tem caminhado em direção a "macrosserviços", exemplo, serviços que não são tão rasos (=profundos). Um dos piores fenômenos e mais dificéis de consertar é o chamado monolito distribuído, o qual é frequentemente resultado de uma separação rasa excessivamente granular.

Certa vez eu consultei uma *Startup* onde um time de cinco desenvolvedores introduziram 17 (!) microsserviços. Eles estavam 10 meses atrasados e nem um pouco próximo do lançamento público. Cada novo requisito levava a mudanças em mais de 4 microsserviços. Isso levou uma quantidade enorme de tempo para reproduzir e depurar um problema como um sistema distribuído. Ambos, o tempo de lançamento e a carga coginitiva estavam inaceitavelmente altos. `🤯`

Esta é a forma correta de lidar com a incerteza de um novo sistema? É extremamente difícil eleger os limites lógicos no início. A chave é tomar decições o mais tarde que você responsavelmente possa esperar, pois terá a informação nas mãos. Ao introduzir uma camada de network logo de cara, fazemos nossa decisão de *design* difícil de reverter logo do início. A única justificativa do time foi: "Empresas FAANG provaram que a arquitetura de microsserviços é efetiva". *Olá, você precisa parar de sonhar alto.*

O [debate Tanenbaum-Torvalds](https://en.wikipedia.org/wiki/Tanenbaum%E2%80%93Torvalds_debate) argumentou que o design monolítico do Linux era falho e obsoleto, e que a arquitetura de *microkernel* deveria ser usada ao invés. De fato, o *design* de *microkernel* parecia ser superior do ponto de vista "teorético e estético". No lado prático das coisas - três décadas depois, o GNU Hurn baseado em *microkernel* continua em desenvolvimento, e o Linux monolítico está em todo canto. Essa página é entregue por um Linux, seu bule inteligente utiliza Linux. Linux monolito.

Um monolito bem-feito com módulos verdadeiramente isolados é frequentemente muito mais flexível que um monte de microsserviços. Ele requer muito menos esfoço cognitivo para manter. Apenas quando precisamos de separar *deployments* se torna crucial, como escalar o desenvolvimento de time, que devemos considerar adicionar uma camada de *network* entre os módulos, futuro microsserviços.