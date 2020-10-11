# Testes automatizados.

Os teste garatem que a nossa aplicação continue funcionando independente do número de novas funcionalidades e do número de devs no time.

#### Teste Unitários (TDD - Test Driven Development)
Testam funcionalidades específicas da nossa aplicação (precisam ser funções puras)

###### Funções puras
Funcções que jamais fazem chamada à uma API e não possui efeito colateral, ou seja dão sempre o mesmo resultado.

#### Teste de integração
Testam funcionalidades completas, passando por várias camadas da aplicação.

#### Teste E2E
Testes que simulam a ação do usuário dentro da nossa aplicação.

  1. Clique no input de email
  2. Preencha com rurbano3d@gmail.com
  3. Clique no input de senha
  4. Preencha com 123456
  5. Clique no botão logar
  6. Espero que a página tenha enviado o usuário para o dashboard
