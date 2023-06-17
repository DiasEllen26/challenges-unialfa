# Desafio 8
## BindParam

O bindParam já é embutido no PHP, e que é utilizado para realizar a definição do valor de um parâmetro. Um método que liga as variáveis e nela passa o seu valor como entrada e caso houver um marcador de parâmetro associado, ele recebe o valor de saída. 
Veja no exemplo a seguir: 

```php 
$con = new PDO("mysql:dbname=ex8;host=localhost", "root", "root");
$config = $con->prepare("INSERT INTO tabela_users (nomeUser, senhaUser) VALUES(:userNome, :userIdade)");
```
No código acima foi criado uma váriavel $con que possui nela a conexão com o banco de dados. Logo após criado a variavel chamado $dados onde nela insere uma query no banco de dados e ali também é inserido dois parâmetros: **:userNome** **userIdade**.
```php
$config->bindParam(':userNome', "Romero Britto");
$config->bindParam(':userIdade', "18");
$config->execute();
echo "Dados inseridos com sucesso!";
```

Neste trecho foi utilizado o método bindParam duas vezes, onde nele logo após usa o execute onde realmente é responsável pela query do banco de dados. 

Entretanto, caso realizar o código dessa forma irá retornar um erro, pois o parametro foi realizado em texto puro, via string. Desta forma, irá retornar um erro onde não consegue encontrar o parâmetro, pois precisa de uma referência para funcionar. 

```php 
$userNome = "Romero Britto";
$userIdade = "18";

$config->bindParam(':userNome', $userNome);
$config->bindParam(':userIdade', $idade);
$config->execute();
echo "Dados inseridos com sucesso!";
```
Desta forma já foi inserido dados a variável e também informado essa váriavel no bindParam. Sendo realizado desta forma, é realizado a query 