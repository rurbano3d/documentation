# Observer

Observer é um padrão comportamental ( Behavioral Pattern), que se preocupa com a implementação do algoritmo e com a separação de responsabilidades entre os objetos.

O Observer observa um objeto e notifica outros objetos quando houver um evento.
>Por meio de um mecanismo de assinatura de eventos.

Ao contrário de você fazer uma chamada a cada tempo para verificar se o objeto observado emitiu algum evento ou que o objeto observado envie um evento para todos os observadores. O Observer cria uma lista com os observadores que o objeto observado precisa enviar o evento, poupando tempo.

O Observer é chamado de Publisher
A lista de observadores é chamada de Subscriber

O Publisher possui dois métodos
 * um para adicionar um novo subscriber
 * outro para remover um subscriber

