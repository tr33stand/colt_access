<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Signup, Login & Profile</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; background-color: maroon; margin: 0; padding: 0; }
        .container { width: 700px; margin: 50px auto; padding: 20px; border: 1px solid #ccc; background: white; display: none; }
        input, button { width: 100%; padding: 7px; margin: 5px 0; }
        button { background: blue; color: ivory; border: none; cursor: pointer; }
        a { cursor: pointer; color: blue; text-decoration: underline; }

        /* Profile Page Styles */
        .navbar { border: 10px solid green; font-family: courier; background-color: green; padding: 10px; color: ivory; display: flex; justify-content: space-between; align-items: center; }
        .navbar h1 { margin: 0; font-size: 20px; }
        .navbar input { padding: 5px; border-radius: 15px; width: 200px; }
        .profile-container { width: 90%; max-width: 600px; margin: 20px auto; background: green; border-radius: 8px; overflow: hidden; }
        .cover-photo { width: 100%; height: 200px; background: url('https://via.placeholder.com/800x200') center/cover no-repeat; }
        .profile-info { padding: 20px; text-align: center; position: relative; }
        .profile-pic { box-shadow: 15px 20px orange; width: 100px; height: 100px; border-radius: 50%; border: 4px solid ivory; position: absolute; top: -50px; left: 50%; transform: translateX(-50%); }
        .profile-info h1 { margin-top: 50px; font-size: 22px; }
        .profile-nav { border: 20px solid cyan; display: flex; justify-content: space-around; background: green; padding: 10px; }
        .profile-nav a { text-decoration: none; color: black; font-weight: bold; }
        .main-content { box-shadow: 15px 20px orange; width: 90%; max-width: 600px; margin: 20px auto; text-align: left; }
        .section { background: green; padding: 15px; margin-bottom: 10px; border-radius: 8px; }
    </style>

</head>
<body>

    <!-- Signup Page -->
    <div id="signup" class="container">
        <h2>Signup</h2>
        <input type="text" id="signupUsername" placeholder="Username">
        <input type="email" id="signupEmail" placeholder="Email">
        <input type="password" id="signupPassword" placeholder="Password">
        <input type="password" id="signupConfirmPassword" placeholder="Confirm Password">
        <button onclick="signup()">Signup</button>
        <p>Already have an account? <a onclick="showLogin()">Login here</a></p>
    </div>

    <!-- Login Page -->
    <div id="login" class="container">
        <h2>Login</h2>
        <input type="email" id="loginEmail" placeholder="Email">
        <input type="password" id="loginPassword" placeholder="Password">
        <button onclick="login()">Login</button>
        <p>Don't have an account? <a onclick="showSignup()">Signup here</a></p>
    </div>

    <!-- Profile Page -->
    <div id="profile" style="display: none;">
        <div class="navbar">
            <h1>ColinaTube</h1>
            <input type="text" placeholder="Search...">
            <button onclick="logout()" style="background: red;">Logout</button>
        </div>

        <div class="profile-container">
            <div class="cover-photo"></div>
            <div class="profile-info">
                <img src="https://via.placeholder.com/100" class="profile-pic" id="profilePic" alt="Profile Picture">
                <h1 id="profileName">Trestan James Colina</h1>
                <p id="profileUsername">@tjlovessaji99</p>
                <button class="edit-profile">Edit Profile</button>
            </div>

            <!-- Navigation Tabs -->
            <div class="profile-nav">
                <a href="#">Posts</a>
                <a href="#">Friends</a>
                <a href="#">Photos</a>
            </div>
        </div>

        <div class="main-content">
            <div class="section">
                <h2>About Me</h2>
                <p>Hello my Name is Trestan James Colina I am an Indie Game Developer and former 2D animator.</p>
            </div>

            <div class="section interests">
                <h2>Interests</h2>
                <ul>
                    <li>🎮 Game Development</li>
                    <li>📚 Animation</li>
                    <li>🎵 Electronic Music</li>
                </ul>
            </div>

            <div class="section contact">
                <h2>Contact Info</h2>
                <p>Email: <a href="mailto:trestan2005@gmail.com">trestan2005@gmail.com</a></p>
                <p>Phone: +097 492 9381</p>
            </div>
        </div>
    </div>

    <script>
        function showSignup() {
            document.getElementById("signup").style.display = "block";
            document.getElementById("login").style.display = "none";
            document.getElementById("profile").style.display = "none";
        }

        function showLogin() {
            document.getElementById("signup").style.display = "none";
            document.getElementById("login").style.display = "block";
            document.getElementById("profile").style.display = "none";
        }

        function showProfile() {
            let username = localStorage.getItem("username");
            let email = localStorage.getItem("email");

            if (username && email) {
                document.getElementById("profileName").textContent = username;
                document.getElementById("profileUsername").textContent = "@" + username.toLowerCase();
                document.getElementById("profilePic").src = "FXOC5636.JPEG";

                document.getElementById("signup").style.display = "none";
                document.getElementById("login").style.display = "none";
                document.getElementById("profile").style.display = "block";
            } else {
                showLogin();
            }
        }

        function signup() {
            let username = document.getElementById("signupUsername").value;
            let email = document.getElementById("signupEmail").value;
            let password = document.getElementById("signupPassword").value;
            let confirmPassword = document.getElementById("signupConfirmPassword").value;

            if (password !== confirmPassword) {
                alert("Passwords do not match!");
                return;
            }

            localStorage.setItem("username", username);
            localStorage.setItem("email", email);
            localStorage.setItem("password", password);

            alert("Signup successful! Redirecting to login.");
            showLogin();
        }

        function login() {
            let email = document.getElementById("loginEmail").value;
            let password = document.getElementById("loginPassword").value;

            if (email === localStorage.getItem("email") && password === localStorage.getItem("password")) {
                alert("Login successful!");
                showProfile();
            } else {
                alert("Invalid email or password!");
            }
        }

        function logout() {
            alert("Logged out!");
            showLogin();
        }
        window.onload = function() {
            let username = localStorage.getItem("username");
            username ? showLogin() : showSignup();
        };
    </script>
</body>
</html>
