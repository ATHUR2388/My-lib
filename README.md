<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Makuto's Library</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #dbeafe, #eff6ff);
      color: #222;
      margin: 0;
      padding: 20px;
    }
    h1, h2, h3, h4 {
      text-align: center;
      color: #1d4ed8;
    }
    input, button, select {
      margin: 5px;
      padding: 10px;
      font-size: 1rem;
      border-radius: 8px;
      border: 1px solid #ccc;
    }
    button {
      background-color: #3b82f6;
      color: white;
      border: none;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #2563eb;
    }
    .upload-section, .files-section, .admin-section, .dashboard {
      margin-top: 20px;
    }
    .background-books {
      background-image: url('https://images.unsplash.com/photo-1512820790803-83ca734da794');
      background-size: cover;
      background-position: center;
      padding: 40px 20px;
      border-radius: 10px;
      text-align: center;
    }
    .hidden {
      display: none;
    }
    .dashboard {
      background-color: #fef9c3;
      border-radius: 10px;
      padding: 20px;
    }
    #searchInput {
      width: 100%;
      max-width: 400px;
      margin: 10px auto;
      padding: 10px;
      display: block;
    }
    .unit-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 8px;
      border-bottom: 1px solid #ccc;
    }
    .unit-actions button, .note-actions button {
      margin-left: 5px;
    }
    .notes-section {
      background-color: #f0fdf4;
      border-radius: 10px;
      padding: 15px;
      margin-top: 15px;
    }
    .notes-section ul {
      list-style-type: none;
      padding: 0;
    }
    .notes-section li {
      padding: 8px;
      margin: 5px 0;
      background-color: #ffffff;
      border: 1px solid #ddd;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .preview-img {
      width: 40px;
      height: 40px;
      object-fit: cover;
      margin-right: 10px;
    }
  </style>
</head>
<body>
  <div class="background-books" id="homepage">
    <h1>WELCOME TO MAKUTO'S LIBRARY</h1>
    <button onclick="showLogin()">Log In</button>
    <button onclick="showRegister()">Register</button>
  </div>  <div class="hidden" id="login-section">
    <h2>Login</h2>
    <input type="email" id="login-email" placeholder="Email" />
    <input type="password" id="login-password" placeholder="Password" />
    <br />
    <button onclick="signIn()">Login</button>
    <button onclick="backHome()">Back</button>
  </div>  <div class="hidden" id="register-section">
    <h2>Register</h2>
    <input type="email" id="register-email" placeholder="Email" />
    <input type="password" id="register-password" placeholder="Password" />
    <input type="password" id="register-confirm" placeholder="Confirm Password" />
    <br />
    <button onclick="registerUser()">Register</button>
    <button onclick="backHome()">Back</button>
  </div>  <!-- Dashboard and other content stay unchanged -->  <script>
    const ADMIN_EMAIL = "athur2388@gmail.com";
    const ADMIN_PASSWORD = "Makuto2388";
    const users = JSON.parse(localStorage.getItem("users")) || {};
    const unitFolders = JSON.parse(localStorage.getItem("unitFolders")) || [];
    const unitFiles = JSON.parse(localStorage.getItem("unitFiles")) || {};
    let currentUser = null;
    let selectedUnit = null;

    function showLogin() {
      document.getElementById("homepage").classList.add("hidden");
      document.getElementById("login-section").classList.remove("hidden");
    }

    function showRegister() {
      document.getElementById("homepage").classList.add("hidden");
      document.getElementById("register-section").classList.remove("hidden");
    }

    function backHome() {
      document.getElementById("homepage").classList.remove("hidden");
      document.getElementById("login-section").classList.add("hidden");
      document.getElementById("register-section").classList.add("hidden");
    }

    function registerUser() {
      const email = document.getElementById("register-email").value;
      const password = document.getElementById("register-password").value;
      const confirm = document.getElementById("register-confirm").value;

      if (!email || !password || !confirm) return alert("Please fill all fields.");
      if (password !== confirm) return alert("Passwords do not match.");
      if (users[email]) return alert("Email already registered.");

      users[email] = password;
      localStorage.setItem("users", JSON.stringify(users));
      alert("Registration successful. Please log in.");
      backHome();
    }

    function signIn() {
      const email = document.getElementById("login-email").value;
      const password = document.getElementById("login-password").value;

      if (email === ADMIN_EMAIL && password === ADMIN_PASSWORD) {
        currentUser = email;
        document.getElementById("login-section").classList.add("hidden");
        document.getElementById("dashboard").classList.remove("hidden");
        document.getElementById("admin-section").classList.remove("hidden");
        document.getElementById("welcome-text").innerText = `Welcome Admin: ${email}`;
        loadUserList();
        loadUnitList();
        return;
      }

      if (users[email] && users[email] === password) {
        currentUser = email;
        document.getElementById("login-section").classList.add("hidden");
        document.getElementById("dashboard").classList.remove("hidden");
        document.getElementById("admin-section").classList.add("hidden");
        document.getElementById("welcome-text").innerText = `Welcome: ${email}`;
        loadUnitList();
      } else {
        alert("Wrong email or password");
      }
    }
  </script></body>
</html>
