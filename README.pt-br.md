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

## Linguagem rica de recursos

Sentimos ansiosos por novos recursos lançados em nossas linguagem favoritas. Gastamos certo tempo para aprender esses recursos, e construímos código em cima disso.

Se existem vários recursos, podemos gastar meia hora brincando com alguma slinhas de código para usar um ou outro recurso. E isso é meio que perda de tempo. Mas o que é pior, **quando retornar depois, você poderia ter de recriar todo o processo de pensamento!**

**Você não apenas tem de compreender esse programa complicado, como tem de compreender porque um programador decidiu essa forma de resolver o problem com os recursos disponíveis**. `🤯`

Essas afirmações foram feitas por ninguém menos que Rob Pike.

> Reduza a carga cognitiva pelo número de escolhas.

Recursos de linguagem são OK, contanto que sejam ortoginais entre si.

<details>
  <summary><b>Pensamentos de um engenheiro com 20 anos de experiência em C++ ⭐️</b></summary>
  <br>
  Eu estava procurando em meu leitor de RSS outro dia e notei que eu tenho algo entre trezentos artigos sobre linguagens desde o último verão, e eu me sinto bem!
  <br><br>
  Eu tenho usado C++ por 20 anos, o que são quase dois terços de minha vida. Maior parte de minha experiência deriva dos cantos mais obscuros da linguagem (como *undefined behavior* de todos os tipos). Isso não é apenas uma experiência reusável, commo é o tipo de coisa assustadora para se jogar fora.
  <br><br>
  Tipo, você pode imaginar, o token <code>||</code> tem significado distinto em <code>requires ((!P&lt;T&gt; || !Q&lt;T&gt;))</code> e em <code>requires (!(P&lt;T&gt; || Q&lt;T&gt;))</code>. A primeira é a disjunção de restrição, a segunda é o bom e velho operador lógico OR, e elas se comportam de maneira diferente.<br><br>
  Você não consegue alocar espaço para um tipo trivial e apenas <code>memcpy</code> um conjunto de bytes sem esforço extra - isso não iniciará o ciclo-de-vida do objeto. Este foi o caso antes do C++20. E foi consertado no C++20, mas a carga cognitiva da linguagem tem apenas aumentado.<br><br>
  A carga cognitiva está constantemente crescendo, mesmo quando as coisas são consertadas. Eu deveria saber o que foi consertado, quando isso foi consertado e como era antes. Eu sou um profissional afinal de contas. Certo, C++ é bom para suporte legado, o que significa que você <b>irá enfrentar</b> o legado. Por exemplo, último mês um colega meu me perguntou sobre o comportamento em C++03. <code>🤯</code><br><br>
  Existiram 20 formas de inicialização. A sintaxe uniforme de inicialização foi adicionado. Agora temos 21 formas de inicialização. De qualquer forma, alguém lembra as regras para selecionar construtores de uma lista inicializadora? Algo sobre conversão implícita com o mínimo de perda de informação <i>mas se</i> o valor é conhecido estaticamente, então... <code>🤯</code><br><br>
  <b>
  Esse aumento na carga cognitiva não é causado pela tarefa do negócio em mãos. E não é uma complexidade intrínseca do domínio. É apenas algo que está lá devido a questões históricas</b> (<i>Carga cognitiva extrínseca</i>).<br><br>
  Eu tive de vir com algumas regras. Assim, se aquela linha de código não fosse óbvia e eu tivesse de lembrar do *Standard*, melhor não escrever dessa forma. O *Standard* é longo, de 1500 páginas, a propósito.<br><br>
  <b>De nenhuma forma estou tentando julgar C++.</b> Amo a linguagem. Mas estou apenas cansado por agora.<br><br>
  <p>Obrigado ao <a href="https://0xd34df00d.me" target="_blank">0xd34df00d</a> por escrever.</p>
</details>

## Lógica de negócios e código de status HTTP

No backend, retornamos:
`401` para tokens JWT expirados
`403` para acesso insuficiente
`418` para usuários banidos

Os engenheiros no frontend usam a API para implementar a funcionalidade de login. Eles precisariam de temporariamente criar a seguinte carga cognitiva em suas cabeças:
`401` para tokens JWT expirados // `🧠+`, ok  vamos temporariamente lembrar disso
`403` para acesso insuficiente // `🧠++`
`418` para usuários banidos // `🧠+++`

Desenvolvedores frontend deveriam (com sorte) introduzir algum tipo de dicionário `status numérico -> significado` em seus lados, então as gerações subsequentes de contribuidores não precisaram ter de recirar esse mapa em seus cérebros.

Então os engenheiros QA entram na jogada:
"Ei, eu tenho um status `403`, isso seria o token expirado ou acesso insuficiente?"
**Engenheiros QA não conseguem pular direto aos testes, pois eles primeiro têm de recriar a carga cognitiva que os engenheiros backend uma vez criaram**

Por que guardar esse mapa customizado em nossa memória de trabalho? É melhor abstrair os nossos detalhes de negócio do protocolo de transferência HTTP e retornar códigos auto-descritíveis no corpo da resposta:

```json
{
  "código": "jwt-expirado"
}
```

Carga cognitiva do lado do *front-end*: `🧠` (fresco, nenhum fato é guardado em mente)
Carga cognitiva do lado do *QA*: `🧠`

As mesmas regras se aplicam a todos os tipos de status numéricos (em bancos de dados ou qualquer outra coisa) - **prefira *strings* auto-descritíveis**. Não estamos em uma era de computadores com 640K de memória para otimizar.

> Pessoas gastam tempo argumentando entre `401` e `403`, tomando decisões baseadas em seus próprios modelos mentais. Novos desenvolvedores estão chegando, e eles precisam de recriar esse processo de pensamento. Você pode ter documentado os Porquês (ADRs) para o seu código, ajudando novatos a compreender as decisões feitas. Mas no final apenas não fazem sentido. Nós podemos separar erros entre ambos, relacionados-ao-usuário ou relacionados-ao-servidor, mas além disso, as coisas são muito foscas.

P.S. Muitas vezes, é mentalmente cansativo distinguir entre “autenticação” e “autorização”. Podemos usar termos mais simples, como [“login” e “permissões”](https://ntietz.com/blog/lets-say-instead-of-auth/), para reduzir a carga cognitiva.

## Abusando do princípio DRY

Não se repita (Don't Repeat Yourself, DRY) - é um dos primeiros princípios que você é ensinado como um engenheiro de *software*. Está tão profundamente embarcado em nós que não podemos aguentar o fato de algumas linhas extras de código. A pesar de ser, em geral, uma regra boa e fundamental, quando sobre-usada, leva a uma carga cognitiva que não poodemos suportar.

Hoje em dia, todo mundo contrói *software* baseado em componentes logicamente separados, Frequentemente, esses são distribuídos entre múltiplas bases de código representando serviços separados. Quando você tenta eliminar qualquer repetição, você pode acabar por criar um acoplamento estreito entre componentes não relacionados. Como resultado, mudanças em uma parte pode levar a consequências não intencionais em outras áreas aparentemente não relacionadas. Isso também pode atrapalhar a capacidade de trocar ou modificar compoenentes individuais sem impactar em sistemas completos. `🤯`

De fato, o mesmo problema surge mesmo dentro de um único módulo. Você pode extraur funcionalidades comuns muito cedo, baseado em similaridades pecebidas que podem não realmente existir no longo prazo. Isso pode resultar em abstrações desnecessárias que são difíceis de estender ou modificar.

Rob Pike disse, certa vez:

> Uma pequena cópia é melhor que uma pequena dependência.

Somos tentados a não re-inventar a roda tão fortemente que estamos prontos para importar biliotecas garndes, e pesadas para usar pequenas funções que poderíamos escrever nós mesmos.

**Todas as suas dependências são seu código**. Indo através de mais de 10 níveis de *Stack Trace* de alguma biblioteca importada e interpretar o que está de errado (*porque as coisas dão errado*) é doloroso.

## Estreitamente acoplado a um *Framework*

Existem várias mágicas em *frameworks*. Ao depender muito de *frameworks*, **nós forçamos todos os desenvolvedores a aprender essa "mágica" primeiro**. Isso pode levar meses. A pesar disso, *frameworks* nos permitem criar Produtos Mínimos Viáveis (Minimal Viable Products, MVP) em poucos dias, no longo prazo eles tendem a adicionar complexidade desnecessária e carga cognitiva.

Pior ainda, a algum ponto os *frameworks* podem se tornar uma retrição significativa quando encarar um novo requerimento que não se encaixa na arquitetura. Até que as pessoas acabem por bifurcar um *framework* e manter suas próprias versões customizadas. Imagine a quantidade de carga cognitiva que um novato teria de construir (por exemplo, aprender esse *framework* customizado) para que possa entregar algum valor. `🤯`

**De nenhuma forma eu advogo em pró de inventar tudo do zero!**

Podemos programar de uma forma agnóstica à *frameworks*. A regra de negócios não deveriam residir dentro de um *framework*; ao invés disso, deveriamos usar os componentes do *framework*. Use *framework* no estilo de bibliotecas. Dessa forma, permitimos que novos contribuidores adicionem valor do dia um, sem necessidade de mergulhar em detritos de complexidade relacionadas ao *framework* primeiro.

> [Why I Hate Frameworks](https://minds.md/benji/frameworks)

## Arquitetura em camadas

Há uma certa emoção de engenharia em tudo isso.

Eu era um apaixonado advogado de arquitetura Hexagonal/Onion por anos. Usei aqui e encorajei outros times a usar também. A complexidade de nossos projetos aumentaram, a quantidade de arquivos sozinhos dobraram. Parece como se eu estivesse escrevendo um monte de código-cola. A cada mudança de requerimento, temos de fazer mudanças entre múltiplas camadas de abstração, o que se torna tedioso. `🤯`

**Abstrações são supostamente para ocultar complexidade, não adicionar [indireção](https://fhur.me/posts/2024/thats-not-an-abstraction)**. Pulando de chamada em chamada para ler e compreender o que há de errado e qual é o requerimento vital para rapidamente resolver o problema. Com essa arquitetura em camada, desacoplar requer um fator extra exponencial, frequentemente dearticulado, rastros para chegat ao ponto onde a falha ocorre. Cada rastro ocupa espaço em nossa limitada memória de trabalho. `🤯`

Essa arquitetura foi algo que fez senso intuitivo de primeira, mas cada vez que tentamos aplicá-la a projetos, isso fez mais mal que bem. Gastamos anos em atividade mental desnecessária e escrevemos código-cola inútil sem valor de negócios claro. Ao contrário, tornamos as coisas piores para os negócios ao forçar novatos a aprender nossas escolhas (modelos mentais) primeiro. O tempo de mercado tem piorado. E no final, desistimos em favor do bom e velho princípio de inversão de dependência. **Nenhum termo de porta ou adaptador para aprender, nenhuma camada horizontal de abstração, nenhuma carga coginitiva extrínseca**.

<details>
  <summary><b>Princípios de programação e experiência</b></summary>
  <img src="img/complexity.png"><br>
  <a href="https://twitter.com/flaviocopes">@flaviocopes</a>
</details>

Se você pensa que tal camadas irão te permitir rapidamente trocar o banco de dados ou quaisquer outras dependências, você está enganado. Mudar o armazenamento causa vários problemas, e acredite em nós, ter algumas abstrações para acessar a camada de dado é a última de suas preocupações. Ao menos, abstrações podem salvar algo entre 10% do nosso tempo de migração (se houver), a dor real está em incompatibilidades do modelo de dado, protocolo de comunicações, desafios de sistemas distrbuídos e [interfaces implícitas](https://www.hyrumslaw.com).

> Com um número suficiente de usuários de uma API,
> não importa qual a sua promessa no contrato:
> todos os comportamentos de seu sistema
> será dependente de alguém.

Fazemos uma migração de armazenamento, e levamos algo entre 10 meses. O sistema legado era *single-thread*, então os eventos expostos eram sequenciais. Todos os nossos sistemas dependem naquele comportamento observado. Esse comportamento não era parte de nosso contrato de API, e não refletia em nosso código. Um novo armazenamento distribuído não nos garantiu isso - os eventos chegam fora-de-ordem. Gastamos apenas algumas horas programando o novo adaptador do armazenamento, agradecimentos a uma abstração. **Gastamos os próximos 10 meses lidando com eventos fora-de-ordem e outros desafios**. Agora é engraçado dizer que abstrações nos ajudam a trocar componentes rapidamente.

**Então, porque pagar o preço de carga cognitiva como uma arquitetura em camadas, se podemos não pagar no futuro?** Adicionalmente, na maioria dos casos, o futuro de trocar algum componente principal nunca acontece.

Essas arquiteturas não são fundamentais, elas são apenas subjetivas, com consequências enviesadas de princípios mais fundamentais. Por que confiar nessas interpretações subjetivas? Siga regras fundamentais ao invés disso: princípio de invesão de dependência, única fonte de verdade, carga cognitiva e ocultação de informação. Nossa lógica de negócios não deveriam depender de módulos de baixo-nível, como banco de dados, interfaces de usuário ou *frameworks*. Deveriamos ser capazes de escrever testes para nossa lógica principal sem ter de nos perocupar com infraestrutura, e é isso. [Dicussão](https://github.com/zakirullin/cognitive-load/discussions/24)

Não adicione camadas de abstração por conta da arquitetura. Adicione-as quando precisar de uma extensão a algum ponto como é justificável por razões práticas.

**[Camadas de abstrações não são livres de mudanças](https://blog.jooq.org/why-you-should-not-implement-layered-architecture), elas são gurdadas em nossa limitada memória de trabalho.**

<div align="center">
  <img src="/img/layers.png" alt="Camadas" width="400">
</div>

## *Domain-drive design*

*Domain-driven design* (DDD) tem alguns pontos positivos, apesar disso, é frequentemente mal-interpretado. Pessoas dizem "Nós escrevemos código DDD", o qual é um pouco estranho, já que DDD é mais sobre o espaço do problema que o espaço de solução.

Linguagem ubíqua, domínio, contexto adjunto, agregado, tempestade de evento são todos espaços de problemas. Eles são para nos ajudar a aprender os *insights* sobre o domínio e extrarir seus limites. DDD permite desenvolvedores, especialistas de domínio e pessoas de negócios se comunicarem de forma efetiva ao utilizar uma linguagem unificada e singular. Ao invés de focar nesses aspectos do DDD sobre o espaço do problrma, tendemos a dar ênfase em estruturas de arquivos em particular, serviços, repositórios e outras técnicas de solução de espaço.

Chances são que a forma como interpretamos DDD é única e subjetiva. E se construirmos código em cima dessa compreensão, por exemplo, se criamos uma carga cognitiva extrínseca - desenvolvedores futuros estão condenados. `🤯`

*Team Topologies* provê um *framework* muito melhor e fácil de compreender que nos permite dividir a carga cognitiva entre times. Engenheiros tendem a desenvolver modelos mentais similares depois de aprender sobre *Team Topologies*. DDD, por outro lado, parece estar criando 10 modelos mentais diferentes para 10 leitores distintos. Ao invés de um chão comum, isso se torna um campo de batalha para debates desnecessários.


## Carga Cognitiva em projetos familiares

> O problema está no fato que **familiaridade não é o mesmo que simplicidade.** Eles *parecem* a mesma coisa — mesma facilidade de se mover no espaço sem muito esforço mental — mas por razões muito diferentes. Cada truque “inteligente” (leia-se: “autoindulgente”) e não idiomático que você usa acarreta uma penalidade de aprendizagem para todos os outros. Uma vez que eles aprendido, é mais fácil trabalhar com o código. Então é difícil reconhecer como é difícil simplificar um código já familiarizado. É por isso que eu peço aos "novatos" que critiquem o código antes que fiquem muito institucionalizados!
>
> É como se o(s) autor(es) anterior(res) tivesse(m) criado essa grande bagunça um incremento por vez, e não tudo de uma só vez. Então você é a primeira pessoa que tentou encontrar sentido nisso tudo de uma só vez.
>
> Em minha aula, eu descrevo um extenso procedimento SQL armazenado onde estávamos analisando um dia, com centenas de linhas de condicionais em uma grande cláusula WHERE. Alguém me perguntou como eu pude deixar isso ficar assim tão ruim. E disse: "Quando há apenas 2 ou 3 condicionais, adicionar mais uma não faz qualquer diferença. Mas com o tempo, você terá 20 ou 30 condicionais, e adicionar outras não fará nenhuma diferença!"
>
> Não existe "força de simplificação" atuando no código-base outras além de escolhas deliberadas que você faz. Simplificar demanda esforço, e pessoas, muitas vezes, estão com pressa.
>
>*Obrigado ao [Dan North](https://dannorth.net) por seu comentário*.  

Se você tem internalizado os modelos mentais do projeto em sua memória de longo-termo, você não irá experienciar a carga cognitiva.

<div align="center">
  <img src="/img/mentalmodelsv15.png" alt="Modelos mentais" width="700">
</div>

Quanto mais modelos mentais tiver de aprender, mais tempo levará para um novo desenvolvedor entregar valor.

Uma vez que você embarca novas pessoas em seu projeto, tente medir a quantidade de confusão que eles têm (pair programming pode ajudar). Caso eles estejam confusos por mais de, mais ou menos, 40 minutos de uma só vez, você tem coisas a melhorar em seu código.

Se você mantiver a carga cognitiva baixa, pessoas podem contribuir para seu código-base dentro de algumas poucas horas ao entrar na empresa.

## Exemplos

- Nossa arquitetura é uma aplicação CRUD padrão, [Um monolito Python em cima de Postgres](https://danluu.com/simple-architectures/).
- Como o Instagram escalou para 14 milhões de usuários com [apenas 3 engenheiros](https://read.engineerscodex.com/p/how-instagram-scaled-to-14-million).
- As empresas que nos deixaram tipo "Nossa! Esses caras são [inteligentes para caramba](https://kenkantzer.com/learnings-from-5-years-of-tech-startup-code-audits/)" acabaram, na sua maioria, fracassando.
- Uma função que liga todo o sistema. Se você quiser como o sistema funciona, [leia isso](https://www.infoq.com/presentations/8-lines-code-refactoring).

Essas arquiteturas são bastante chatas e fáceis de compreender. Qualquer um pode compreendê-las sem muito esforço mental.

Envolva desenvolvedores júniors em suas reviews de arquitetura, eles podem te ajudar a identificar áreas mentalmente exaustivas.

> Sistemas de software são talvez os mais intricados e complexos (em termos de número de tipos distintos de peças) entre as coisas que a humanidade cria.  
> 
> *Fred Brooks, The Mythical Man-Month*

**Manter software é difícil**, as coisas quebram e precisamos de todo o esforço mental que pudermos economizar. Quanto menos componentes houver no sistema, menos problemas haverá. A depuração também será menos desgastante mentalmente.

> Depurar é duas vezes mais difícil do que escrever o código, em primeiro lugar. Portanto, se você escrever o código da forma mais esperta possível, você, por definição, não será inteligente o suficiente para depurá-lo.  
>
> *Brian Kernighan*

Em geral, a mentalidade de "Uau, essa arquitetura parece ótima!" é enganosa. Essa é uma sensação subjetiva de um determinado momento e não diz nada sobre a realidade. Uma abordagem muito melhor é observar as consequências a longo prazo:

- É fácil reproduzir e depurar um problema? Ou você precisa pular entre *call stacks* ou componentes distribuídos, tentando entender tudo na sua cabeça?
- Podemos fazer alterações rapidamente ou há muitas incógnitas e as pessoas têm medo de mexer nas coisas?
- Os novos funcionários podem adicionar recursos rapidamente? Há alguns modelos mentais únicos a serem aprendidos?

> O que são esses modelos mentais únicos? É um conjunto de regras, geralmente uma mistura de DDD/CQRS/Arquitetura Limpa/Arquitetura Orientada a Eventos. Essa é a interpretação do autor sobre as coisas que mais o entusiasmam. Seus próprios modelos mentais subjetivos. 

**Carga cognitiva estranha que os outros têm de internalizar.**

Essas questões são muito mais difíceis de rastrear, e as pessoas geralmente não gostam de respondê-las diretamente. Veja alguns dos sistemas de software mais complexos do mundo, aqueles que resistiram ao teste do tempo — Linux, Kubernetes, Chrome e Redis (veja os comentários abaixo). Você não encontrará nada sofisticado neles, são em sua maioria enfadonhos, e isso é bom.

## Conclusão

Imagine por um momento que o que inferimos no segundo capítulo não seja realmente verdade. Se for este o caso, então a conclusão que acabamos de negar, juntamente com as conclusões do capítulo anterior que aceitamos como válidas, também podem não estar corretas.

Você percebeu? Não só você precisa pular de um lado para outro no artigo para entender o significado (módulos superficiais!), como o parágrafo em geral é difícil de entender. Acabamos de criar uma carga cognitiva desnecessária na sua cabeça. **Não faça isso com seus colegas.**

<div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="O autor espeto" width="600">
</div>

Deveríamos reduzir qualquer carga cognitiva acima. É algo além de instrínseco para o trabalho que fazemos.

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
    <p>Another example is what I'm doing right now, Vector Sets, the new Redis data type. I decided that Redis would not be the source of truth about vectors, but that it can just take an approximate version of them, so I was able to do on-insert normalization, quantization without trying to retain the large floats vector on disk, and so forth. May vector DBs don't sacrifice the fact of remembering what the user put inside (the full precision vector).</p>
    <p>These are just two random examples, but I apply this idea everywhere. Now the thing is: of course one must sacrifice the right things. Often, there are 5% features that account for a very large amount of complexity: that is a good thing to kill :D</p>
    <p><strong><a href="https://working-for-the-future.medium.com/about" target="_blank">A developer from the internet</a></strong><br>You would not hire me... I sell myself on my track record of released enterprise projects.</p>
    <p>I worked with a guy that could speak design patterns. I could never speak that way, though I was one of the few that could well understand him. The managers loved him and he could dominate any development conversation. The people working around him said he left a trail of destruction behind him. I was told that I was the first person that could understand his projects. Maintainability matters. I care most about TCO. For some firms, that's what matters.</p>
    <p>I logged into Github after not being there for a while and for some reason it took me to an article in a repository by someone that seemed random. I was thinking "what is this" and had some trouble getting to my home page, so I read it. I didn't really register it at the time, but it was amazing. Every developer should read it. It largely said that almost everything we've been told about programming best practices leads to excessive "cognitive load", meaning our minds are getting kicked by the intellectual demands. I've known this for a while, especially with the demands of cloud, security and DevOps.</p>
    <p>I also liked it because it described practices I have done for decades, but never much admit to because they are not popular... I write really complicated stuff and need all the help I can get.</p>
    <p>Consider, if I'm right, it popped up because the Github folks, very smart people, though that developers should see it. I agree.</p>
    <p><a href="https://news.ycombinator.com/item?id=45074248" target="_blank">Comments on Hacker News</a> (<a href="https://news.ycombinator.com/item?id=42489645" target="_blank">2</a>)</p>
</details>
