# pdo1
   <?php

require 'connect.php';

$pdo = new PDO(DSN, USER, PASS) ;
var_dump($pdo);


$errors =[] ;
if ($_SERVER ["REQUEST_METHOD"] ==='POST') {

    if(!empty($_POST['firstname']) &&  !empty($_POST['lastname'])) {
        //Faire une insert into(préparer) en base de donnée  INSERT INTO  story(title , content ,autor )Values(:title , :content , ;autor)
          $statement=$pdo->prepare("INSERT INTO friend (firstname , lastname) Values (:firstname , :lastname )") ;
          //IL faut binder tous les parametre 
          $statement->bindValue(":firstname", $_POST['firstname'] ,PDO::PARAM_STR) ;
          $statement->bindValue(":lastname", $_POST['lastname'],PDO::PARAM_STR) ;
          //IL faut executer la requete 
          $statement->execute() ;
           //Permet de la redirigé 
          header('Location: /') ;
    } else {
        $errors[]="tous les champs sont requis " ; //La gestion d'eerreur se mets apres la method post  qui est <?php if (!empty ($errors)) {echo ""le champs est requi ;}
    }
}
$statement=$pdo->query ("SELECT * FROM story") ;
$articles=$statement->fetchAll(PDO::FETCH_ASSOC) ;
var_dump($articles) ;
?>

?>

<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    
    <title>Checkpoint PHP 1</title>
</head>
<body>
<form method="POST" action="">

<?php if (!empty ($errors)){
                            foreach ($errors as $error){ //prends l'erreur en valu du tableau pour aller decrire
                                echo $error ."\n" ; 
                            }
                        }
                        ?>

    <div class="mb-3">
                <label for="lastname" class="form-label">lastname</label>
                <input type="text" name="lastname" class="form-control" id="lastname" >
            </div>
            <div class="mb-3">
                <label for="firstname" class="form-label">firstname</label>
                <input type="text" name="firstname" class="form-control" id="firstname">
            </div>
            
            <button type="submit" value="Démarrer la machine" accesskey="s"></button>
</form>

</body>
