# ES2020: Promise.allSettled

Uma nova adição que chega com o ES2020 é `Promise.allSettled`. Esse novo método chega para resolver um problema que deixava o código muito verboso na utilização de `Promise.all`.

## Recapitulando rapidamente Promises

[Promises](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) é um objeto usado para processamento assíncrono. Uma `Promise` representa um valor que pode estar disponível agora, no futuro ou nunca.

Uma`Promise` pode se encontrar em algum dos estados:

* pending (pendente): Estado inicial, que não foi realizada nem rejeitada.
* fulfilled (realizada): Sucesso na operação.
* rejected (rejeitada): Falha na operação.
* settled (estabelecida): Que foi realizada ou rejeitada.

Uma promessa pendente pode ter seu estado alterado para realizada com um valor ou ser rejeitada com um motivo (erro).

## Recapitulando rapidamente Promise.all e Promise.race

[`Promise.all`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) é um método que recebe um objeto iterável contendo promises. `Promise.all` apenas retorna uma promise `fulfilled` caso todas as promises que foram passadas no objeto sejam também `fulfilled` caso contrário irá retornar uma promise com estado `rejected`.

[`Promise.race`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise/race) funciona de forma similar ao `.all` com a diferença de não esperar que todas as promises sejam estabelecidas. `Promise.race` retorna a primeira promise que for estabelecida, resolvendo ou rejeitando de acordo com o resultado.

## Promise.allSettled


