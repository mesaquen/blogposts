# Optional chaining operator

Muitas novidades são esperadas com a chegada das especificações para o ES2020. Uma delas que veio para simplificar a vida e diminuir a quantidade de código que temos que escrever é o [operador de encadeamento opcional][Optional chaining operator] `?.` - Optional chaining em inglês.

O funcionamento dele é similar ao do `.` operador de encadeamento, exceto que ao invés de causar um erro ao tentar acessar uma propriedade de uma referência vazia (`null` ou `undefined`), a expressão irá retornar undefined.

Isso pode ser muito util ao explorar conteúdo de um objeto onde não se tem garantia de que as propriedades são obrigatórias.

## Exemplo

```javascript
const player = {
  name: 'John',
  weapon: {
    name: 'sword',
  },
};

// Correto, porém verboso
let clothingName;
if (player != null && player.clothing != null) {
  clothingName = player.clothing.name;
}
console.log(cloathingName);

// Usando optional chaining
const clothingName = player.clothing?.name;
console.log(cloathingName); // expected output: undefined


// Correto, porém verboso
let value;
if (player != null && typeof player.someNonExistentMethod === 'function') {
 value = player.someNonExistentMethod();
}
console.log(value);

// Usando optional chaining
console.log(player.someNonExistentMethod?.()) // expected output: undefined
```

## Sintaxe

```javascript
object?.prop
object?.[expression]
arr?.[index]
func?.(args)
```

O novo operador de encadeamento opcional ajuda reduzir a quantidade de código escrita, simplificando a leitura e manutenção.

Junto com o optional chaining operator receberemos o [Nullish coalescing operator][Nullish coalescing operator], mas isso é assunto para um post futuro.


[Optional chaining operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining
[Nullish coalescing operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_Coalescing_Operator
