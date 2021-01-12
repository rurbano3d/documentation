# Diferença entre Verificar um erro e lançar uma exceção?

## Exceção
Isto permite que o programador possa incluir código de tratamento das exceções, de forma que, quando a exceção ocorrer, a execução do programa não seja finalizada, mas que a exceção seja tratada adequadamente e o programa prossiga sua execução normalmente.

Exceções são os erros que podem ser verificados, por exemplo, um objeto null, uma entrada de dados errada como um float no lugar de um inteiro.

### Exceções não verificadas
São as execeções que não precisa ser tratadas para o codigo rodar. Por exemplo uma divisão por 0 cujo resultado não existe

Outros exemplos são as NullPointerException, ArrayIndexOutOfBoundsException e IllegalArgumentException.

### Exceções verificadas
São as execeções que precisam ser tratadas para o codígo rodar. Por exemplo receber uma string quando se esperar um number.

Outros exemplos são as IOException, SQLException e ParseException.

“Se for razoável esperar que um cliente se recupere de uma exceção, torne-a uma exceção verificada. Se um cliente não puder fazer nada para se recuperar da exceção, torne-a uma exceção não verificada. ”

[Fonte](https://www.baeldung.com/java-checked-unchecked-exceptions#:~:text=Checked%20Exceptions,-In%20general%2C%20checked&text=For%20example%2C%20the%20constructor%20of,checked%20exceptions%20at%20compile%2Dtime.&text=Some%20common%20checked%20exceptions%20in,IOException%2C%20SQLException%2C%20and%20ParseException.)

## Erros

Já o erros são erros que não podem ser verificados, como erro memoria, erro de conexão, etc.


Michael Feathers diz que:

* É importante utilizar try/catch para tratamento de erros.
* Crie testes que forçam as exceções e depois adicione testes para cumprir suas ações (TDD)
* Use exceções não verificadas.
* Forneça exceções com contexto, mencione a operação que falhou e o tipo da falha.
