---
title: '💧Drops: Javascript Reduce'
date: 2016-09-10 10:24:46

tags: drops
---

<!--- Invisible Char: > < --->

Com certeza você sabe fazer um __loop__ em uma collection.
Mas você sabe o que significa **reduzir** uma collection??

Não? Isso te soa estranho? Calma, é bem simples, tenho certeza que você já fez isso:

<!-- more -->
```javascript
let total = 0;
const numbers = [1, 5, 7, 3, 8, 9];
for ( let i = 0; i < numbers.length; i++ ){
    total += numbers[i];
}
```

Pronto! Você **reduziu** a collection de numbers dentro de uma variável total. 😃
Vamos ver outro exemplo:

```javascript
let message = "";
const words = ["reducing", "is", "simple"];
for ( let i = 0; i < words.length; i++ ){
  message += words[i];
}
```

Agora você **reduziu** a collection words dentro da variável message.

Acho que você deve ter notado a semelhança entre os dois códigos.
Iniciamos com uma **collection** (numbers, words) e uma **variável** (total, message) com um **valor inicial** (0, "").
Depois iteramos na collection para alterar o valor da variável.

>*Tá mas é só isso? um *`for`*?* 🤔

Vamos lá! Veja esse código:

```javascript
const numbers = [1,5,7,3,8,9];
const sum = numbers.reduce(function(total, number) {
  return total + number;
}, 0)

// sum = 33
 
// Você também pode usar Arrow Function do ES6
const sum = numbers.reduce((total, number) => total + number, 0)
```

>*Wow. Então o objeto Array já sabe reduzir??* 😮

**Exatamente!** Sempre que você quiser iterar em uma collection a fim de criar um novo valor pergunte a si mesmo se você pode considerar o uso da função `Array.prototype.reduce`.

## Sintaxe

```javascript
array.reduce(callback, [initialValue]);
array.reduce(function(previousValue, currentValue, index, array){
  // do stuff
}, [initialValue]);
```

O reduce recebe dois parâmetros:

1. *callback* : Uma função de callback (que explicarei logo em seguida).
2. *initialValue* : (opcional): Um valor inicial para o retorno que pode ser qualquer dado. Se esse parâmetro não for informado, o valor inicial padrão é o primeiro item do array a ser iterado.

O reduce executa a função de callback uma vez para cada elemento presente no array, excluindo furos (valores indefinidos) , recebendo quatro argumentos: o valor inicial (ou o valor do callback anterior, *previousValue*), o valor do elemento corrente (*currentValue*), o índice (*index*) corrente e o próprio *array* onde a iteração está ocorrendo. - *MDN*

Você pode reduzir a qualquer tipo de dado. Não apenas soma ou concatenação, exemplo:

```javascript
const people = [
  { name: 'João', age: 32},
  { name: 'Maria', age: 22},
  { name: 'José', age: 13},
  { name: 'Francisco', age: 56},
  { name: 'Mariana', age: 49},
  { name: 'Marcos', age: 26},
];
 
// Retorna a pessoa mais velha da lista
let oldest = people.reduce(function (prev, curr) {
  if (curr.age > prev.age) {
    return curr;
  } else {
    return prev;
  }
})

// oldest = {name: "Francisco", age: 56}
 
// Com Arrow function
const oldest = people.reduce((prev, curr) => (curr.age > prev.age) ? curr : prev )
```

Parabéns! Agora você sabe o que é e como usar o Reduce! 🤘🏻

Você também pode ler a [Documentação do Reduce no MDN]( https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) para ir mais afundo

<img src="https://i.giphy.com/7rj2ZgttvgomY.gif"/>
