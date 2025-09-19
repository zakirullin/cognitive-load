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

