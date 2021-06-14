<?php
if($_POST) {

$message=$_POST['name'];
$message .=$_POST['firstname'];
$message .=$_POST['user_mail'];
$message .=$_POST['user_mail'];


mail ($message .=$_POST['champtexte2'], "Confirmation of your inscription", $message, "From: contact@taxiteam.com") ; 

}
?>


<form class = "contact" action="/profile page" method="post">
    <div class = "contact" >
        <label  class = "contact" for="name">Name : </label>
        <input type="text" id="name" name="name">
    </div>
     <div class = "contact" >
        <label  class = "contact" for="firstname">Firstname : </label>
        <input type="text" id="firstname" name="firstname">
    </div>
    <div class = "contact" >
<input type="file" name="photo" id="photo" /> 
     </div>
     <div class = "contact" >
<input type="submit" class="btn" value="envoyer" /> 
     </div>
    <div class = "contact" >
        <label  class = "contact" for="mail">e-mail :</label>
        <input type="email" id="mail" name="user_mail">
    </div>
    <div class = "contact" >
        <label  class = "contact" for="phone">phone number: </label>
        <input type="text " id="phone" name="phone_number">
    </div>
<div class = "contact" >
        <label  class = "contact" for="city">City : </label>
        <input type="text" id="city" name=”city">
    </div>
<div class = "contact" >
        <label  class = "contact" for="adress">Adress : </label>
        <input type="text" id="adress" name=“address”>
    </div>
</form>



form.contact {
  /* Uniquement centrer le formulaire sur la page */
  margin: 0 auto;
  width: 400px;
  /* Encadré pour voir les limites du formulaire */
  padding: 1em;
  border: 1px solid #CCC;
  border-radius: 1em;
}

div.contact {
  margin-top: 1em;
}

label.contact {
  /* Pour être sûrs que toutes les étiquettes ont même taille et sont correctement alignées */
  display: inline-block;
  width: 90px;
  text-align: right;
}