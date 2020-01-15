# ES2020: Nullish coalescing operator (`??`)

O [*operador de coalescência nula* (`??`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) é um operador lógico que retorna o operando do lado direito caso o valor do operando do lado esquerdo seja `null` ou `undefined`. Caso contrário, retorna o operando do lando esquerdo.

Diferente do [operador lógico OR (`||`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Logical_OR_2), o operando do lado esquerdo é retornado caso seja um valor [falsy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Description) que não seja `null` ou `undefined`.

## Atribuindo valor padrão à uma variável

Antes, quando você queria atribuir um valor padrão à uma variável, era comum se deparar com algum código como esse:

```javascript
let foo = 0;

...

const defaultNumber = 42;
console.log(output || defaultNumber); // expected output: 42
```

O problema com essa abordagem é que caso você considere zero (`0`) ou uma string vazia (`''`) como válidos, você terminaria com um comportamento indesejado aqui.

Utilizando o operador de coalescência nula, a história muda.

```javascript
let foo = 0;
let bar;

...
const defaultNumber = 42;

console.log(foo ?? defaultNumber); // expected output: 0
console.log(bar ?? defaultNumber); // expected output: 42
```

## Encadeando com os operadores OR (`||`) e AND (`&&`)

O operador `??` não pode ser encadeado diretamente com os operadores `||` e `&&`. Caso isso aconteça, você vai terminar com um `SyntaxError` sendo lançado:

```javascript
null || undefined ?? 'default'; // lança um SyntaxError
```

Para corrigir isso você deve envolver a expressão em parênteses para explicitamente indicar a precedência:

```javascript
(null || undefined) ?? 'default'; // 'default'
```

## Relação com o operador de encadeamento opcional (`?.`)

O operador `??` trata os especificamente os valores `null` e `undefined`, assim como o [operador de encadeamento opcional (`?.`)](https://www.linkedin.com/pulse/es2020-optional-chaining-operator-mesaque-do-nascimento-francisco/), que é usado para acessar propriedades de um objeto que podem ser `null` ou `undefined`.
