
Neste capítulo Uncle Bob diz que é importante utilizar a abstração, ou seja, não expor o tipo e a implementação. 

Mas o que é implementação?
Implementação é a ação de inserir uma coisa dentro de outra.

"Uma classe não passa suas variáveis simplesmente por meio de métodos de escrita ou leitura. Em vez disso, ela expõe interfaces abstratas que permite aos usuários manipular a essência dos dados, sem precisar conhecer a implementação."

Ou seja, quando expomos nossa implementação estamos dando acesso a forma de como criamos os comportamentos, isso deve ser abstrato.

" Queremos expressar nossos dados de forma abstrata. Isso não se consegue meramente através de interfaces e/ou métodos de escrita e leitura. É preciso pensar bastante na melhor maneira de representar os dados que um objeto contenha. A pior opção é adicionar levianamente métodos de escrita e leitura.

# data/Objeto

São conceitos antissimétricos, ou seja, são opostos.

## Objetos
* usam abstrações para esconder os seus dados, e expõem as funções que operam tais dados.
* O codigo OO facilita a adiçao de novas classes sem precisar alterar as funçoes existentes.
* O codigo OO dificulta a adição de novas funçoes, pois todas as classes teriam de ser alteradas.

## Dados
* Expõem seus dados e não possuem funções significativas.
* O codigo procedural facilita adiçao de novas funçoes sem precisar alterar as estruturas de dados existentes.
* O codigo procedural dificulta a adiçao de novas estruturas de dados, pois todas as funçoes teriam de ser alteradas.

# Explicação simplista sobre Procedural e OO.

Vamos simplificar toda a programação baseado em estado e comportamento.

Estado, é nossa estrutura de dados do programa
* Arrays
* Variavéis

Comportamento, é a nossa lógica.
* funções
* métodos

A Programação Procedural passa o estado para o comportamento para produzir a saída. Utiliza a ramificação (if/else) como forma de seleção.

A Programação Orientada a Objetos produz a saída de um objeto sem a necessidade de passar um estado. Utiliza o polimorfismo como forma de seleção.
















