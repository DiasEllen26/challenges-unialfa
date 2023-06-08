# Desafio 7 

## config.php
```php 
<?php 
$servidor = "localhost";
$banco = "pesquisa";
$user = "root";
$password = "root";

    try { 
        $con = new PDO("mysql:host={$servidor};dbname={$banco};port=8889;charset=utf8", $user, $password);
    }

    catch(PDOException $e){
        echo "erro ao conectar no banco" . $e->getMessage();
    }
````

## pesquisa.php
```php 
<?php 
    require "./config.php";

    $sql = "SELECT * FROM dados";
    $consulta = $con->prepare($sql);


    $true = "true";
    if(isset($_GET["status"])) {
        $true = $_GET["status"];   
        $sql = "SELECT * FROM dados WHERE status = :true ";
        $consulta = $con->prepare($sql);
        $consulta->bindParam(":true", $true);
    }
    
    $consulta->execute();
    $dados = $consulta->fetchAll(PDO::FETCH_OBJ);

    //print_r($dados);
    
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pesquisa</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
</head>
<body>
    <table class="table table-hover table-dark">
        <thead>
            <tr>
                <td scope="col">Id</th>
                <td scope="col">Região</th>
                <td scope="col">Descrição</th>
                <td scope="col">Status</th>
            </tr>
        </thead>
        <tbody>

        <?php 
            foreach ($dados as $pesquisa) { 
        ?>
            <tr>
                <th><?=$pesquisa->id?></th>
                <td><?=$pesquisa->regiao?></td>
                <td><?=$pesquisa->descricao?></td>
                <td><?=$pesquisa->status?></td>
            </tr>
            <?php 
        }
    ?>
        </tbody>
    </table>
    
    <a href="pesquisa.php?status=false" class="btn btn-danger">False</a>
    <a href="pesquisa.php?status=true" class="btn btn-success">True</a>
    <a href="pesquisa.php" class="btn btn-warning">Todos</a>
</body>
</html>