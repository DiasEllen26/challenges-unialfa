# Desafio 6 
```php 
<?php 
$servidor = "localhost";
$banco = "ex6";
$user = "root";
$password = "root";

    try { 
        $con = new PDO("mysql:host={$servidor};dbname=${$banco};port=8889;charset=utf8", $user, $password);
    }

    catch(PDOException $e){
        echo "erro ao conectar no banco" . $e->getMessage();
    }
