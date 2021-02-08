// php_login page

<?php
session_start(); // start session

// Here is your connection file

include ('YOUR CONNECTION FILE');

$msg = "";
$msg1 = "";

// Here we check the submit btn is clicked then we have to run this code

if(isset($_POST['register'])){

 $email = $_POST['email'];
 $pass = $_POST['password'];
	

 $sel = " SELECT * FROM `TABLE_NAME` WHERE email='$MAIL' ";
 $query = mysqli_query($con, $sel);

   $row = mysqli_num_rows($query);  
     if($row){
         $token = mysqli_fetch_assoc($query);
         $passfatch = $token['password'];
         
         $dpass = password_verify($pass, $passfatch);
         if($dpass){ //match password with hashed password
           
             echo "<script>alert('login success\nYou are Manager.')</script>";
             echo "<script> location.href='panadmn.php'</script>";
           }
           else{
             echo "<script>alert('Please Make Payment to login.')</script>";
             echo "<script> location.href='active.php'</script>";}
        } 
        else { $msg = "Wrong password";}
    } 
    else { $msg1 = "Invalid E-Mail!!!";}
}
?>
<html>
  <head>
    <title>Login Page</title>
  </head>
  <body>
    <style>
    html {
        font-size: 62.5%;
    }
    body {
        margin: 0rem;
        font-size: 2rem;
		padding:0rem;
    }
 .first {
      /* background-color: rgb(240, 234, 234);*/
        text-align: center;
        padding: 2rem;
        font-size: 1.5rem;
        width: 30rem;
        height: 50rem;
        margin: auto;
	 border:.1rem solid red;
        border-radius: 1rem;
    }
 .second {
        padding: 1rem;
        line-height: 3rem;
        text-align: center;
    }
 .second input {
        padding: 1rem 4rem;
    }
 .third {
        background-color: brown;
        border-radius: .5rem;
        width: 20rem;
        height: 4rem;
        color: white;
        font-size: 2rem;
        margin-top: 3rem;
    }
 	 
 @media(max-width:769px) {
	 html{
		 font-size:62.5%;
		 }
        body {
            margin: 0rem;
           padding:0rem;
        }
 .first{
         /*  background-color: rgb(240, 234, 234);*/
            text-align: center;
            padding: 2rem;
            width: 30rem;
            height: 50rem;
            margin: auto;
	  border:.1rem solid red;
           border-radius: 1rem;
        }
 .second {
            padding: 1rem;
            line-height: 3rem;
            text-align: center;
        }
 .second input {
            padding: 1rem 4rem;
        }
 .third {
            background-color: brown;
            border-radius: .5rem;
            width: 20rem;
            height: 4rem;
            margin-top: 3rem;
	 }   
 }
    </style>
    <form method="post" action="<?php echo htmlentities($_SERVER['PHP_SELF']); ?>">
        <div class="first">
            <h1>SIGN IN NOW</h1>
            <hr>
            <div class="second">
                <label><b>E-MAIL ID</b></label><br>
                <input type="email" name="email" placeholder="<?= $msg1; ?>"><br>
                <label><b>Password</b></label><br>
                <input type="password" name="password" id="inputPassword0" placeholder="<?= $msg; ?>"><br>
                <input type="checkbox" onclick="showpass()"> Show Password

                <input type="submit" name="register" class="third" value="Login">
            </div>
           <p>Don't Have an Account?<a href="register.php">Create an Account</a></p>
			<p><a href="#">Forget Password<!--- page link --></a></p>
        </div>
    </form>
    
</body>

</html>
