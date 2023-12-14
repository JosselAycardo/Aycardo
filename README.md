<?php
    session_start();
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="Style.css">
    <title>Login</title>
</head>
<body>
    <div class="container">
        <div class="box form-box">
            <?php
                include("php/config.php");

                if(isset($_POST['submit'])){
                    $email = mysqli_real_escape_string($con, $_POST['Email']);
                    $password = mysqli_real_escape_string($con, $_POST['Password']);

                    $result = mysqli_query($con, "SELECT * FROM users WHERE Email='$email' AND Password='$password'") or die("Select Error");
                    $row = mysqli_fetch_assoc($result);

                    if(is_array($row) && !empty($row)){
                        $_SESSION['valid'] = $row['EMAIL'];
                        $_SESSION['Username'] = $row['USERNAME'];
                        $_SESSION['Age'] = $row['AGE'];
                        $_SESSION['Id'] = $row['Id'];
                        header("Location: Example.html");
                        exit(); // Ensure that the script stops execution after redirecting
                    } else {
                        echo "<div class='message'>
                                <p>Wrong Email or Password</p>
                              </div><br>";
                    }
                }
            ?>
            <header>Login</header>
            <form action="" method="post">
                <div class="field input">
                    <label for="Email">Email</label>
                    <input type="text" name="Email" id="Email" autocomplete="off" required>
                </div>
                <div class="field input">
                    <label for="Password">Password</label>
                    <input type="password" name="Password" id="Password" autocomplete="off" required>
                </div>
                <div class="field">
                    <input type="submit" class="btn" name="submit" value="Login" required>
                </div>
                <div class="links">
                    Don't have an account? <a href="Register.php">Create now</a>
                </div>
            </form>
        </div>
    </div>
</body>
</html>
