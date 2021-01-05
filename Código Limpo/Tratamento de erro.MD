# Diferença entre Verificar um erro e lançar uma exceção?

## Exceção
Isto permite que o programador possa incluir código de tratamento das exceções, de forma que, quando a exceção ocorrer, a execução do programa não seja finalizada, mas que a exceção seja tratada adequadamente e o programa prossiga sua execução normalmente.

Exceções são os erros que podem ser verificados, por exemplo, um objeto null, uma entrada de dados errada como um float no lugar de um inteiro.

## Erros

Já o erros são erros que não podem ser verificados, como erro memoria, erro de conexão, etc.


Michael Feathers diz que:

* É importante utilizar try/catch para tratamento de erros.
* Crie testes que forçam as exceções e depois adicione testes para cumprir suas ações (TDD)
* Forneça exceções com contexto, mencione a operação que falhou e o tipo da falha.
