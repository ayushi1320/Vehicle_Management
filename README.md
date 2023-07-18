# Vehicle_Management
Admin Login Portal:
<?php
session_start();
require 'update_slots.php';
require 'mysqlConnect.php';
?>
<!DOCTYPE html>
<html lang="en">
 <head>
 <meta charset="utf-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <meta name="description" content="">
 <meta name="author" content="Dashboard">
 <title>Admin</title>
 <!-- Bootstrap core CSS -->
 <link href="assets/css/bootstrap.css" rel="stylesheet">
 <!--external css-->
 <link href="assets/font-awesome/css/font-awesome.css" rel="stylesheet" />
 <!-- Custom styles for this template -->
 <link href="assets/css/style.css" rel="stylesheet">
 <link href="assets/css/style-responsive.css" rel="stylesheet">
 </head>
 <body>
 <div id="login-page">
 <div class="container">
 <form class="form-login" action="admin_login.php" method="post">
 <h2 class="form-login-heading">sign in</h2>
 <div class="login-wrap">
 <input type="text" name="email" class="form-control" 
placeholder="email" autofocus>
 <br>
 <input type="password" name="password" class="form-control" 
placeholder="Password">
 </br>
 </br>
 <button class="btn btn-theme btn-block" href="user_login.php" 
name='admin_login' type="submit"><i class="fa fa-lock"></i> SIGN IN</button>
 <!-- Modal -->
 <div aria-hidden="true" aria-labelledby="myModalLabel" role="dialog" 
tabindex="-1" id="myModal" class="modal fade">
 <div class="modal-dialog">
 <div class="modal-content">
 <div class="modal-header">
 <button type="button" class="close" data-dismiss="modal" 
aria-hidden="true">&times;</button>
 </div>
 <div class="modal-footer">
 <button data-dismiss="modal" class="btn btn-default" 
type="button">Cancel</button>
 <button class="btn btn-theme" 
type="button">Submit</button>
 </div>
 </div>
 </div>
 </div>
 <!-- modal -->
 </form>
 </div>
 </div>
 <!-- js placed at the end of the document so the pages load faster -->
 <script src="assets/js/jquery.js"></script>
 <script src="assets/js/bootstrap.min.js"></script>
 <!--BACKSTRETCH-->
 <!-- You can use an image of whatever size. This script will stretch to fit in any screen size.-
->
 <script type="text/javascript" src="assets/js/jquery.backstretch.min.js"></script>
 <script>
 $.backstretch("assets/img/admin0000.jpg", {speed: 500});
 </script>
 <?php
 if(isset($_POST['admin_login'])){
 $password=mysqli_real_escape_string($con,$_POST['password']);
 $email=mysqli_real_escape_string($con,$_POST['email']);
 $sel="select * from admin where email='$email' AND password='$password'";
 $run=mysqli_query($con,$sel);
 $check=mysqli_num_rows($run);
 if($check==0)
 {
 echo"<script>alert('password or email is not correct,try again!')</script>";
 exit();
 }
 else{
 $_SESSION['email']=$email;
 echo"<script>window.open('admin.php','_self')</script>";
 }
 }
 ?>
 </body>
</html>
ATTENDANT LOGIN PORTAL :
<?php
session_start();
require 'mysqlConnect.php';
?>
<!DOCTYPE html>
<html lang="en">
 <head>
 <meta charset="utf-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <meta name="description" content="">
 <meta name="author" content="Dashboard">
 <meta name="keyword" content="Dashboard, Bootstrap, Admin, Template, Theme, 
Responsive, Fluid, Retina">
 <title>Attendant</title>
 <!-- Bootstrap core CSS -->
 <link href="assets/css/bootstrap.css" rel="stylesheet">
 <!--external css-->
 <link href="assets/font-awesome/css/font-awesome.css" rel="stylesheet" />
 <!-- Custom styles for this template -->
 <link href="assets/css/style.css" rel="stylesheet">
 <link href="assets/css/style-responsive.css" rel="stylesheet">
 </head>
 <body>
 <div id="login-page">
 <div class="container">
 <form class="form-login" action="attendant_login.php" method="post">
 <h2 class="form-login-heading">sign in now</h2>
 <div class="login-wrap">
 <input type="text" name="username" class="form-control" 
placeholder="Username" autofocus>
 <br>
 <input type="password" name="password" class="form-control" 
placeholder="Password">
 </br>
 </br>
 <button class="btn btn-theme btn-block" href="user_login.php" 
name='attendant_login' type="submit"><i class="fa fa-lock"></i> SIGN IN</button>
 <!-- Modal -->
 <div aria-hidden="true" aria-labelledby="myModalLabel" role="dialog" 
tabindex="-1" id="myModal" class="modal fade">
 <div class="modal-dialog">
 <div class="modal-content">
 <div class="modal-header">
 <button type="button" class="close" data-dismiss="modal" 
aria-hidden="true">&times;</button>
 </div>
 <div class="modal-footer">
 <button data-dismiss="modal" class="btn btn-default" 
type="button">Cancel</button>
 <button class="btn btn-theme" 
type="button">Submit</button>
 </div>
 </div>
 </div>
 </div>
 <!-- modal -->
 </form>
 </div>
 </div>
 <!-- js placed at the end of the document so the pages load faster -->
 <script src="assets/js/jquery.js"></script>
 <script src="assets/js/bootstrap.min.js"></script>
 <!--BACKSTRETCH-->
 <!-- You can use an image of whatever size. This script will stretch to fit in any screen size.-
->
 <script type="text/javascript" src="assets/js/jquery.backstretch.min.js"></script>
 <script>
 $.backstretch("assets/img/atten000.jpg", {speed: 500});
 </script>
 
 <?php
if(isset($_POST['attendant_login'])){
$password=mysqli_real_escape_string($con,$_POST['password']);
$username=mysqli_real_escape_string($con,$_POST['username']);
$sel="select * from attendant where username='$username'";
$result=mysqli_query($con,$sel);
if(mysqli_num_rows($result) > 0)
{
 while($row = mysqli_fetch_array($result))
 {
 if(password_verify($password, $row["password"]))
 {
 //return true
 $_SESSION['username']=$username;
 echo"<script>window.open('attendant_portal.php','_self')</script>";
 }
 else
 {
 //return false
 echo"<script>alert('wrong user details,try again!')</script>";
 echo"<script>window.open('attendant_login.php','_self')</script>";
 exit();
 }
 }
}
else{
 echo"<script>alert('wrong user details,try again!')</script>";
 echo"<script>window.open('attendant_login.php','_self')</script>";
 exit();
}
}
?>
 </body>
</html>
USER LOGIN PORTAL :
<?php
session_start();
require 'mysqlConnect.php';
require 'update_slots.php';
?>
<!DOCTYPE html>
<html lang="en">
 <head>
 <meta charset="utf-8">
 <meta http-equiv="X-UA-Compatible" content="IE=edge">
 <meta name="viewport" content="width=device-width, initial-scale=1">
 <!-- The above 3 meta tags *must* come first in the head; any other head content must 
come *after* these tags -->
 <title>Smart Parking Web Portal</title>
 <meta charset="utf-8">
 <meta name="viewport" content="width=device-width, initial-scale=1">
 <link rel="stylesheet" 
href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
 <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.0/jquery.min.js"></script>
 <script 
src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
 <link href="assets/css/bootstrap.css" rel="stylesheet">
 <link href="custom.css" rel="stylesheet">
<style>
/* .modal-fullscreen size: we use Bootstrap media query breakpoints */
.modal-fullscreen .modal-dialog {
 margin: 0;
 margin-right: auto;
 margin-left: auto;
 width: 100%;
}
@media (min-width: 768px) {
 .modal-fullscreen .modal-dialog {
 width: 750px;
 }
}
@media (min-width: 992px) {
Page | 28
 .modal-fullscreen .modal-dialog {
 width: 970px;
 }
}
@media (min-width: 1200px) {
 .modal-fullscreen .modal-dialog {
 width: 1170px;
 }
}
/* .modal-transparent */
#regForm label{
color: #000 !important; /* makes the text-black */
}
</style>
<script type="text/javascript">
function checkPass()
{
 //Store the password field objects into variables ...
 var pass1 = document.getElementById('password');
 var pass2 = document.getElementById('password_confirm');
 //Store the Confimation Message Object ...
 var message = document.getElementById('confirmMessage');
 //Set the colors we will be using ...
 var goodColor = "#66cc66";
 var badColor = "#ff6666";
 //Compare the values in the password field
 //and the confirmation field
 if(pass1.value == pass2.value){
 //The passwords match.
 //Set the color to the good color and inform
 //the user that they have entered the correct password
 pass2.style.backgroundColor = goodColor;
 $('#regBtn').prop('disabled', false);
 $('#regOwner').prop('disabled', false);
 }else{
 //The passwords do not match.
 //Set the color to the bad color and
 //notify the user.
 $('#regBtn').prop('disabled', true);
 $('#regOwner').prop('disabled', true);
 pass2.style.backgroundColor = badColor;
 message.style.color = badColor;
 message.innerHTML = "Passwords Do Not Match!"
 }
}
// validate email
function email_validate(email)
{
var regMail = /^([_a-zA-Z0-9-]+)(\.[_a-zA-Z0-9-]+)*@([a-zA-Z0-9-]+\.)+([a-zA-Z]{2,3})$/;
 var status = document.getElementById("emailstatus");
 if(regMail.test(email) == false)
 {
 document.getElementById("emailstatus").innerHTML = "<span class='warning'>Email 
address is not valid.</span>";
 status.style.color = "#f44336";
 $('#regBtn').prop('disabled', true);
 $('#regOwner').prop('disabled', true);
 }
 else
 {
 document.getElementById("emailstatus").innerHTML = "<span class='valid'>Email 
address is Valid!</span>";
 status.style.color = "#00838f ";
 $('#regBtn').prop('disabled', false);
 $('#regOwner').prop('disabled', false);
 }
}
$(".modal-fullscreen").on('show.bs.modal', function () {
 setTimeout( function() {
 $(".modal-backdrop").addClass("modal-backdrop-fullscreen");
 }, 0);
});
$(".modal-fullscreen").on('hidden.bs.modal', function () {
 $(".modal-backdrop").addClass("modal-backdrop-fullscreen");
});
$(".modal-transparent").on('show.bs.modal', function () {
 setTimeout( function() {
 $(".modal-backdrop").addClass("modal-backdrop-transparent");
 }, 0);
});
$(".modal-transparent").on('hidden.bs.modal', function () {
 $(".modal-backdrop").addClass("modal-backdrop-transparent");
});
</script>
 </head>
 <body>
 <div class="overlay">
 <div class="row">
 <div class="container">
 <div class="col-md-4"></div>
 <div class="col-md-4">
 <div class="page-header">
 <center><h1 class="colors">SMART PARKING Portal</h1></center>
 </div>
 </div>
 <div class="col-md-4"></div>
 </div>
 </div>
 <!-- Modal -->
 <div class="modal modal-fullscreen fade modal-transparent" id="myModal" role="dialog" 
aria-hidden="true">
 <div class="modal-dialog">
 <!-- Modal content-->
 <div class="modal-content">
 <div class="modal-header">
 <button type="button" class="close" data-dismiss="modal">&times;</button>
 <center><h4 class="modal-title" style="color:#225556;">All form fields are 
required.</h4></center>
 </div>
 <div class="modal-body">
 <form id="regForm" action="register.php" method="POST" enctype="multipart/formdata">
 <div class="form-group">
 <label for="name" >Name:</label>
 <input type="text" name="name" id="name" class="text ui-widget-content ui-cornerall">
 </div> 
 <div class="form-group">
 <label for="email">Email</label>
 <input type="email" id="email" name="email" placeholder="" class="text ui-widgetcontent ui-corner-all" onchange="email_validate(this.value);" required>
 <p id="emailstatus"></p>
 </div> 
 <div class="form-group">
 <label for="password">Password</label>
 <input type="password" id="password" name="password" placeholder="" class="text uiwidget-content ui-corner-all" required>
 </div> 
 <div class="form-group">
 <label for="password">Confirm Password</label>
 <input type="password" class="text ui-widget-content ui-corner-all" 
id="password_confirm" name="password_confirm" placeholder="" onkeyup="checkPass(); 
return false;" required>
 </div> 
<button type="submit" id="regBtn" class="form-control" name="register">create 
account</button>
 </div>
 </form>
 </div>
 </div>
 </div>
 <div class="row">
 <div class="container">
 <div class="col-md-4"></div>
 <div class="col-md-4">
 <form enctype="multipart/form" action="user_login.php" method="POST" id="">
 <div class="page-header">
 <center><h3 class="colors">Login</h3></center>
 </div>
 <label for=""></label>
 <input type="text" name="email" id="" placeholder="email" class="email">
 <label for=""></label>
 <input type="password" name="password" id="" placeholder="password" 
class="pass">
 <button type="submit" name="login">login</button>
 <label for=""></label>
 <button type="button" data-toggle="modal" data-target="#myModal">Sign 
Up</button>
 </form>
 </div>
 <div class="col-md-4"> </div>
 </div>
 </div>
</div>
<?php
if(isset($_POST['login'])){
$password=mysqli_real_escape_string($con,$_POST['password']);
$email=mysqli_real_escape_string($con,$_POST['email']);
$sel="select * from users where email='$email'";
$result=mysqli_query($con,$sel);
if(mysqli_num_rows($result) > 0)
{
 while($row = mysqli_fetch_array($result))
 {
 if(password_verify($password, $row["password"]))
 {
 //return true
 $_SESSION['driver_email']=$email;
 echo"<script>window.open('home.php','_self')</script>";
 }
 else
 {
 //return false
 echo"<script>alert('wrong user details,try again!')</script>";

 echo"<script>window.open('user_login.php','_self')</script>";
 exit();
 }
 }
}
else{
 echo"<script>alert('wrong user details,try again!')</script>";
 echo"<script>window.open('user_login.php','_self')</script>";
 exit();
}
}
?>
 <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
 <script src="assets/js/jquery-1.8.3.min.js"></script>
 <!-- Include all compiled plugins (below), or include individual files as needed -->
 <script src="assets/js/bootstrap.min.js"></script>
 </body>
</html>
