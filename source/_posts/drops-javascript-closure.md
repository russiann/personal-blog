---
title: '💧Javascript Drops: Scopes, Let & Closures'
date: 2016-09-11 11:40:44
tags:
---
<!--- Invisible Char: > < --->

Para tabalhar com Javascript eficientemente, uma das primeiras coisas que você deve entender é o conceito de Escopo. As regras de escopo variam de linguagem em linguagem e esse artigo aborda especificamente o Javascript.

<!-- more -->

## Scopes
O escopo de uma variável determina em que partes do programa essa variável pode ser acessada. O JavaScript tem dois escopos: **global** e **local**.

Uma variável declarada fora de uma `function` pertence ao escopo **global**, portanto, ela se torna uma **variável global**, e seu valor será acessível e modificável em todo o seu programa.

Toda `function` possui seu próprio escopo, e qualquer variável declarada dentro de uma `function`

Uma variável declarada dentro de uma `function` pertence ao escope é local. Por exemplo:

```javascript
var x = 10; // x é global
function foo() {
  var y = 20; // y é local e seu acesso é limitado dentro do escopo de foo
  console.log(x); // mas como x é global, temos acesso a ela aqui dentro também
}
foo(); // -> 10
```

Quando o `console.log(x)` é executado, o Javascript primeiro procura qualquer variável `x` definida dentro do scopo de `foo()`, para depois procura-lo no escopo global (ou por closure da qual explicarei depois). No caso como não existe nenhum `x` definido dentro do escopo de `foo()` ele captura o `x` definido no escopo global.

> *Então se houver outro `x` definido no escopo de `foo()` ele irá usa-lo?*

Reposta: Sim

```javascript
var x = 10; // x global
function foo() {
  var y = 20; // y local
  var x = 30; // x local
  console.log(x); // agora que há um x local, ele será usado.
}
foo(); // -> 30
```

Vamos a outro exemplo agora:

```javascript
function foo() {
  if (true) {
    var x = 5;
  }
  console.log(x)
}
// result -> 5
```

<!-- E cada novo scopo criado dentro de um escopo já existente tem acesso a todas as variáveis definidas no(s) "de fora":
```javascript
function x() {          // "x" tem acesso a "a"
    var a;
    function y() {      // "y" tem acesso a "a" e "b"
        var b;
        function z() {  // "z" tem acesso a "a", "b", e "c"
            var c;
```

Alias, esse código a cima também mostra o nosso próximo tema... -->

## Closures
Closure se refere a forma como funçòes definidas dentro de um "escopo léxico" (i.e. o corpo de uma função, um bloco, um arquivo fonte) acessam dados (variáveis, parâmentros) definidas nesse contexto.
