# ES2020: Promise.allSettled

Uma nova adição que chega com o ES2020 é `Promise.allSettled`. Esse novo método chega para resolver um problema que deixava o código muito verboso na utilização de `Promise.all`.

## Recapitulando rapidamente Promises

[Promises](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) é um objeto usado para processamento assíncrono. Uma `Promise` representa um valor que pode estar disponível agora, no futuro ou nunca.

Uma`Promise` pode se encontrar em algum dos estados:

- pending (pendente): Estado inicial, que não foi realizada nem rejeitada.
- fulfilled (realizada): Sucesso na operação.
- rejected (rejeitada): Falha na operação.
- settled (estabelecida): Que foi realizada ou rejeitada.

Uma promessa pendente pode ter seu estado alterado para realizada com um valor ou ser rejeitada com um motivo (erro).

## Recapitulando rapidamente Promise.all e Promise.race

[`Promise.all`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) é um método que recebe um objeto iterável contendo promises. `Promise.all` apenas retorna uma promise `fulfilled` caso todas as promises que foram passadas no objeto sejam também `fulfilled` caso contrário irá retornar uma promise com estado `rejected`.

[`Promise.race`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise/race) funciona de forma similar ao `.all` com a diferença de não esperar que todas as promises sejam estabelecidas. `Promise.race` retorna a primeira promise que for estabelecida, resolvendo ou rejeitando de acordo com o resultado.

## Promise.allSettled

`Promise.allSettled` funciona de forma similar a `Promise.all` com a diferença que a promise resultante nunca é rejeitada caso uma das promises do objeto iterado seja rejeitada. Ao invés disso retorna um array com um objeto para cada promise contendo as propriedades:

- status: `fulfilled` | `rejected`
- value: valor da promise resolvida
- reason: motivo da promise rejeitada

O novo método `Promise.allSettled` é bem útil quando você precisa executar uma operação que deve ser considerada completa independente de suas etapas falharem ou não. Como por exemplo, quando você quer fazer download de multiplos arquivos e ao final executar alguma outra ação.

Usando `Promise.all` você teria que adicionar um `.catch` para cada promise que será executada. Para evitar que o retorno de `Promise.all` seja uma promise rejeitada.

```javascript
const download = async (url) => {/*...*/};
const handleFailedDownload = async url => {/*...*/};

const downloadAllFiles = async () => {
  const urls = [
    "http://example.com/exists.txt",
    "http://example.com/missing-file.txt"
  ];

  await Promise.all(urls.map(url => download(url).catch(handleFailedDownload)));
  doSomethingElse();
};
```

Usando `Promise.allSettled` você não precisa mais se preocupar com promises sendo rejeitadas em um loop. Porém ter

```javascript
const download = async (url) => {/*...*/};

const downloadAllFiles = async () => {
  const urls = [
    'http://example.com/exists.txt',
    'http://example.com/missing-file.txt'
  ];

  await Promise.allSettled(urls.map(url => download(url));
  doSomethingElse();
};
```

## Atenção com os valores retornados

Diferente de `Promise.all` onde em caso de sucesso, os valores são retornados diretamente no array de resultados. Em `Promise.allSettled` o array de resultados retorna contém um `SettlementObject` para cada promise passada no iterável inicial.

Abaixo você encontra uma representação da assinatura dos retornos de `Promise.allSettled`.

```typescript
type SettlementObject<T> = FulFillmentObject<T> | RejectionObject<T>;

interface SettlementObject<T> {
  status: "fulfilled";
  value: T;
}

interface RejectionObject {
  status: "rejected";
  reason: unknown;
}
```

## Exemplo de Promise.allSettled

```javascript
const results = Promise.allSettled([
  Promise.resolve("OK"),
  Promise.reject("ERROR"),
  Promise.resolve("OK TOO")
]);

console.log(results);

/**
Expected output:
[
  { status: 'fulfilled', value: 'OK' },
  { status: 'rejected', reason: 'ERROR' },
  { status: 'fulfilled', value: 'OK TOO'},
]
*/
```
