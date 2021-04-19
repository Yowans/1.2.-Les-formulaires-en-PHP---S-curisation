# 1.2.-Les-formulaires-en-PHP---S-curisation
form.php

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">

             <title>Formulaire</title>
</head>
<body>


<?php
    if($_POST){
        require_once ('controller.php');
    }
?>

<form action="form.php" method="POST">
    <div>
        <label for="firstname">Nom</label><br>
        <input type="text"  ="name" name="firstname" value="<?=$firstname?>"><br><br>
    </div>
    <div>
        <label for="lastname">Prénom</label><br>
        <input type="text" id="lastname" name="lastname" value="<?=$lastname?>"><br><br>
    </div>
    <div>
        <label for="mail">Email</label><br>
         <input type="email" id="mail" name="mail" value="<?=$mail?>"><br><br>
    </div>
    <div>
        <label for="phone">Téléphone</label><br>
        <input type="text"  id="phone" name="phone" placeholder="0607080910" value="<?=$phone?>"><br><br>
    </div>
    <div>
        <label for="subject">Sujet</label><br>
        <select id="subject"  name="subject" value="<?=$subject?>">
            <option value="">Choisir un onglet</option>
            <option value="achats">Achats</option>
            <option value="maintenance">Maintenance</option>
            <option value="oders">Commandes</option>
            <option value="other">Autre</option>
        </select><br><br>

        <label for="message">Message</label><br>
        <textarea id="message" name="message" value="<?=$message?>"></textarea><br><br>
    </div>
    <div class="button">
        <button type="submit"> Submit your message</button>
    </div>
   </form>

<?php

?>


</body>
</html>



controller.php

<?php

$firstnameError = '';
$lastnameError  = '';
$subjectError   = '';
$mailError      = '';
$phoneError     = '';
$messageError   = '';
$nbError        = 0;




if (empty($_POST['firstname'])) {
    $nbError++;
    $firstname      = $_POST['firstname'];
    $firstnameError = 'Vous devez entrer un nom.';
}
if (empty($_POST['lastname'])) {
    $nbError++;
    $lastname      = $_POST['lastname'];
    $lastnameError = 'Vous devez entrer un prénom.';
}
if (empty($_POST['subject'])) {
    $nbError++;
    $subject      = $_POST['subject'];
    $subjectError = 'Vous devez sélectionner un sujet.';
}
if (!filter_var ($_POST['mail'], FILTER_VALIDATE_EMAIL)) {
    $nbError++;
    $mail         = $_POST['mail'];
    $mailError    = 'Vous devez saisir un email au format demandé.';
}
if (empty($_POST['phone'])) {
    $nbError++;
    $phone        = $_POST['phone'];
    $phoneError   = 'Vous devez saisir un numéro de téléphone au format demandé.';
}
if (empty($_POST['message'])) {
    $nbError++;
    $message       = $_POST['message'];
    $messageError  = 'Vous devez saisir un message.';
}


echo $firstnameError.'<br>';
echo $lastnameError.'<br>';
echo $subjectError.'<br>';
echo $mailError.'<br>';
echo $phoneError.'<br>';
echo $messageError.'<br>';

if ($nbError === 0){
    header('Location:thanks.php?lastname=' . $_POST['lastname'] .' '. '&firstname=' . $_POST['firstname'] .' '. '&subject=' . $_POST['subject'] .' '. '&mail=' . $_POST['mail'] .' '. '&phone=' . $_POST['phone'] .' '. '&message=' . $_POST['message']);

}


thanks.php


<?php


echo 'Merci ' . $_GET['lastname']. '' .$_GET['firstname'] . ' de nous avoir contacté à propos de '. ''.$_GET['subject'];
echo '<br>';
echo 'Un de nos conseiller vous contactera soit à l\'adresse suivante ' . $_GET['mail']. ' ou par téléphone au ' . $_GET['phone'] . ' dans les plus brefs délais pour traiter votre demande: ' . $_GET['message'];

