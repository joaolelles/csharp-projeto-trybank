# Trybank

Boas-vindas ao repositório do projeto `Trybank`

Aqui, você vai encontrar os detalhes de como estruturar o desenvolvimento do seu projeto a partir desse repositório, utilizando uma branch específica e um _Pull Request_ para colocar seus códigos.
  
<details>
<summary><strong>🧑‍💻 O que foi desenvolvido</strong></summary>

Já pensou em criar um sistema de um banco? Nesse projeto, eu criei uma aplicação para controlar contas bancárias bem como realizar as suas operações básicas de checar um saldo, depositar, sacar e transferir dinheiro.
Além disso, eu permiti com que nessa aplicação, você cadastre novas contas, faça login e logout no seu sistema.

</details>
  
<details>
  <summary><strong>:memo: Habilidades trabalhadas </strong></summary>

- Entender sobre as estruturas de array
- Realizar a conversão e manipulação de variáveis de diversos tipos
- Realizar operações aritméticas
- Construir algorítmos que implementem estruturas de controle
- Lançar exceções controladas.
</details>

## Orientações

<details>
  <summary><strong>‼️ Antes de começar a desenvolver</strong></summary><br />

  1. Clone o repositório

  2. Instale as dependências
  
  - Entre na pasta `src/`.
  - Execute o comando: `dotnet restore`.
  
  3. Crie uma branch a partir da branch `master`

  4. Adicione as mudanças ao _stage_ do Git e faça um `commit`

  5. Adicione a sua branch com o novo `commit` ao repositório remoto

  6. Crie um novo `Pull Request` _(PR)_

</details>

<details>
  <summary><strong>🎛 Linter</strong></summary><br />

  Usaremos o [NetAnalyzer](https://docs.microsoft.com/pt-br/dotnet/fundamentals/code-analysis/overview) para fazer a análise estática do seu código.

  Este projeto já vem com as dependências relacionadas ao _linter_ configuradas no arquivo `.csproj`.

  O analisador já é instalado pelo plugin da `Microsoft C#` no `VSCode`. Para isso, basta fazer o download do [plugin](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) e instalá-lo.
</details>

<details>
  <summary><strong>🛠 Testes</strong></summary><br />

  O .NET já possui sua própria plataforma de testes.
  
  Este projeto já vem configurado e com suas dependências.

  ### Executando todos os testes

  Para executar os testes com o .NET, execute o comando dentro do diretório do seu projeto `src/`.

  ```
  dotnet test
  ```

  ### Executando um teste específico

  Para executar um teste expecífico, basta executar o comando `dotnet test --filter Name~TestMethod1`.

  :warning: **Importante:** o comando irá executar testes cujo nome contém `TestMethod1`.

  :warning: **O avaliador automático não necessariamente avalia seu projeto na ordem em que os requisitos aparecem no readme. Isso acontece para deixar o processo de avaliação mais rápido. Então, não se assuste se isso acontecer, ok?**

  ### Outras opções para testes
  - Algumas opções que podem lhe ajudar são:
    -  `-?|-h|--help`: exibem a descrição completa de como utilizar o comando.
    -  `-t|--list-tests`: lista todos os testes, ao invés de executá-los.
    -  `-v|--verbosity <LEVEL>`: define o nível de detalhe na resposta dos testes.
      - `q | quiet`
      - `m | minimal`
      - `n | normal`
      - `d | detailed`
      - `diag | diagnostic`
      - Exemplo de uso: 
         ```
           dotnet test -v diag
         ```
         ou
         ```            
           dotnet test --verbosity=diagnostic
         ``` 
</details>


# Requisitos do Projeto

Boas-vindas ao TryBank, uma iniciativa de implementar um serviço de banco financeiro para sua instituição do coração.💚

Você recebeu a demanda de criar a versão inicial do TryBank. Nesse projeto, você tem como objetivo construir um banco que contenha contas. Além disso, deve criar e validar os processos de cadastro, login, saque, depósito e transferência do saldo dessas contas. 

Como ainda não aprendemos a persistir dados, este projeto irá armazenar os dados em um array. Como os dados do array estarão sempre em memória, toda vez que reiniciar o programa a memória do apagar e você terá os dados do array zerados.

Os dados da conta bancária ficará armazenado em um array multidimensional. Cada array que irá armazenar os dados tem na posição 0 o número da conta, na posição 1, a agencia, na posição 2 a senha de acesso e na posição 3 o saldo da conta. Por exemplo, para cadastro das seguintes contas:

Conta 1: Agência 1, Número da conta: 1234, Senha: 987, Saldo: 0
Conta 2: Agência 2, Número da conta: 5678, Senha: 765, Saldo: 0

O array multidimensional ficaria:

```csharp
    int[] conta1 = new int[4] {1234, 1, 987, 0};
    int[] conta2 = new int[4] {5678, 2, 765, 0};

    int[][] Bank = new int[50][conta1, conta2]; <-- arruma isso, pq não sei como faz.
```

De olho na dica👀: Faça uma boa separação de responsabilidades garantindo assim que a evolução desse sistema ocorra facilmente. Construa os requisitos em ordem para que os testes utilizem os métodos implementados por você corretamente.
 

## 1. Construa a funcionalidade de cadastrar novas contas

Crie a lógica do seu requisito no arquivo src/trybank/Trybank.cs.

<details>
  <summary>O programa deve permitir o cadastro de novas contas</summary><br />

Crie esse requisito na função `RegisterAccount()`

Se essa combinação de **número e agência** já existir, você deverá lançar uma exceção do tipo `ArgumentException` com a mensagem `A conta já está sendo usada!`.

Caso contrário, a função deve armazenar os dados no array `Bank` na próxima posição disponível marcada por `registeredAccounts` com saldo 0;

Caso tudo corra bem, a função deve incrementar a variável registeredAccounts;

**O que será testado:**

Será testado que ao chamar o método implementado, o mesmo registre uma conta nova no array e incremente a variável `registeredAccounts`.


</details>

## 2. Construa a funcionalidade de fazer Login

Crie a lógica do seu requisito no arquivo src/trybank/Trybank.cs.

<details>
  <summary>O programa deve permitir o Login da pessoa usuária</summary><br />

Crie esse requisito na função `Login()`

O estado de pessoa usuária logada é controlado pela variável `Logged`


- **Se já houver uma pessoa usuária logada**, você deverá lançar uma exceção do tipo `AccessViolationException` com a mensagem `Usuário já está logado`


 **Caso contrário**, a função deve procurar por essa combinação de número e agência.

-   **Se encontrado e a senha for correta**, a função deve alterar o estado da variável `Logged` e armazenar a posição da pessoa usuária logada na variável `loggedUser` (será útil futuramente para as próximas funções, fica a dica!)

-   **Se encontrado e a senha for incorreta**, você deve lançar uma exceção do tipo `ArgumentException` com a mensagem `Senha incorreta`

-   Se não for encontrada a combinação de `número e agência`, você deve lançar uma exceção do tipo `ArgumentException`com a mensagem `Agência + Conta não encontrada`

**O que será testado:**

Será testado que ao chamar o método implementado, o mesmo registre o login caso o usuário exista e a senha esteja correta e lance os erros caso a senha esteja incorreta ou caso a combinação de agência e conta não exista.

</details>

## 3. Construa a funcionalidade de fazer Logout

Crie a lógica do seu requisito no arquivo src/trybank/Trybank.cs.

<details>
  <summary>O programa deve permitir o Logout do usário</summary><br />

Crie esse requisito na função `Logout()`

O estado de pessoa usuária logada é controlado pela variável `Logged`

**Se não houver uma pessoa usuária logada**, você deverá lançar uma exceção do tipo `AccessViolationException` com a mensagem `Usuário não está logado`

**Caso contrário**, a função deve alterar o estado da variável `Logged` e o índice de pessoa usuária `loggedUser` de volta para `-99`


**O que será testado:**

Será testado que ao chamar o método implementado, o mesmo faça o logout do usuário logado e lance um erro caso o usuário em questão não esteja logado.

</details>


## 4. Construa a funcionalidade de checar o saldo

Crie a lógica do seu requisito no arquivo src/trybank/Trybank.cs.

<details>
  <summary>O programa deve permitir verificar o saldo na conta da pessoa usária logada</summary><br />

Crie esse requisito na função `CheckBalance()`

**Se não houver uma pessoa usuária logada**, você deverá lançar uma exceção do tipo `AccessViolationException` com a mensagem `Usuário não está logado`

**Caso contrário**, a função deve retornar o saldo na conta da pessoa usuária logada.


**O que será testado:**

Será testado que ao chamar o método implementado, o mesmo mostre o saldo da conta e lance um erro caso o usuário em questão não esteja logado.

</details>

## 5. Construa a funcionalidade de depositar dinheiro

Crie a lógica do seu requisito no arquivo src/trybank/Trybank.cs.

<details>
  <summary>O programa deve permitir o depósito de um valor na conta da pessoa usária logada</summary><br />

Crie esse requisito na função `Deposit()`

**Se não houver uma pessoa usuária logada**, você deverá lançar uma exceção do tipo `AccessViolationException` com a mensagem `Usuário não está logado`

**Caso contrário**, a função deve adicionar o valor passado por parâmetro para o saldo da pessoa usuária logada.


**O que será testado:**

Será testado que ao chamar o método implementado, o mesmo aumente o saldo da conta e lance um erro caso o usuário em questão não esteja logado.


</details>

## 6. Construa a funcionalidade de sacar dinheiro

Crie a lógica do seu requisito no arquivo src/trybank/Trybank.cs.

<details>
  <summary>O programa deve permitir o saque de um valor na conta da pessoa usuária logada</summary><br />

Crie esse requisito na função `Withdraw()`

**Se não houver uma pessoa usuária logada**, você deverá lançar uma exceção do tpo `AccessViolationException`, com a mensagem `Usuário não está logado`

**Caso contrário**, a função deve retirar o valor passado por parâmetro para o saldo da pessoa usuária logada.
  Se o saldo da conta da pessoa usuária logada for insuficiente para fazer o saque, você deve lançar uma exceção do tipo `InvalidOperationException` com a mensagem `Saldo insuficiente`


**O que será testado:**

Será testado que ao chamar o método implementado, o mesmo diminua o saldo da conta e lance um erro caso o usuário em questão não esteja logado ou caso o saldo seja insuficiente.

</details>


## 7. Construa a funcionalidade de transferir dinheiro entre contas

Crie a lógica do seu requisito no arquivo src/trybank/Trybank.cs.

<details>
  <summary>O programa deve permitir a transferência de saldo entre uma pessoa usuária logada e uma conta existente</summary><br />

Crie esse requisito na função `Transfer(int destinationNumber, int destinationAgency, int value)()`

**Se não houver uma pessoa usuária logada**, você deverá lançar uma exceção do tipo `AccessViolationException`, com a mensagem `Usuário já está logado`

Se o saldo da conta da pessoa usuária logada for insuficiente para fazer a transferência, você deve lançar uma exceção do tipo `InvalidOperationException` com a mensagem `Saldo insuficiente`

**Caso contrário**, a função deve transferir o valor passado por parâmetro do saldo da pessoa usuária logada para o saldo da conta passada por parâmetro.


**O que será testado:**

Será testado que ao chamar o método implementado, o mesmo diminua o saldo da conta origem e aumente o saldo da conta destino no mesmo valor. Também será testado que o software lance um erro caso o usuário em questão não esteja logado ou caso o saldo seja insuficiente.

</details>

---

<!-- mdi versão 1.1 projeto ⚠️ não exclua esse comentário -->
