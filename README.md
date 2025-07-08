<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Makuto's Library</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #dbeafe, #eff6ff);
      color: #222;
      margin: 0;
      padding: 20px;
    }
    h1 {
      font-size: 2rem;
      color: #1d4ed8;
      text-align: center;
    }
    input, button {
      margin: 5px;
      padding: 10px;
      font-size: 1rem;
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
  </style>
</head>
<body>
  <div class="background-books" id="homepage">
    <h1>WELCOME TO MAKUTO'S LIBRARY</h1>
    <div id="auth-section">
      <input type="email" id="email" placeholder="Email" />
      <input type="password" id="password" placeholder="Password" />
      <input type="password" id="confirmPassword" placeholder="Confirm Password (Sign Up only)" />
      <br />
      <button onclick="signUp()">Sign Up</button>
      <button onclick="signIn()">Sign In</button>
    </div>
  </div>  <div id="dashboard" class="dashboard hidden">
    <h2 id="welcome-text"></h2>
    <input type="text" id="searchInput" onkeyup="searchUnits()" placeholder="Search for a unit..." /><div id="admin-section" class="admin-section hidden">
  <h3>Admin Panel</h3>
  <input type="text" id="unitName" placeholder="Create new unit directory" />
  <button onclick="createUnitDirectory()">Create Unit</button>
  <h4>Registered Users</h4>
  <ul id="userList"></ul>
</div>

<h3>Available Units</h3>
<ul id="unitList"></ul>

  </div>  <script>
    const ADMIN_EMAIL = "athur2388@gmail.com";
    const ADMIN_PASSWORD = "Makuto2388";

    const users = JSON.parse(localStorage.getItem("users")) || {};
    const unitFolders = JSON.parse(localStorage.getItem("unitFolders")) || [];

    let currentUser = null;

    function saveUsers() {
      localStorage.setItem("users", JSON.stringify(users));
    }

    function saveUnits() {
      localStorage.setItem("unitFolders", JSON.stringify(unitFolders));
    }

    function signUp() {
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;
      const confirmPassword = document.getElementById("confirmPassword").value;

      if (users[email]) {
        alert("User already exists. Please sign in.");
        return;
      }
      if (password !== confirmPassword) {
        alert("Passwords do not match.");
        return;
      }
      users[email] = password;
      saveUsers();
      alert("Sign up successful. Please sign in.");
    }

    function signIn() {
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;

      if (email === ADMIN_EMAIL && password === ADMIN_PASSWORD) {
        currentUser = email;
        document.getElementById("homepage").classList.add("hidden");
        document.getElementById("dashboard").classList.remove("hidden");
        document.getElementById("admin-section").classList.remove("hidden");
        document.getElementById("welcome-text").innerText = `Welcome Admin: ${email}`;
        loadUserList();
        loadUnitList();
        return;
      }

      if (!users[email] || users[email] !== password) {
        alert("Wrong password or user does not exist.");
        return;
      }

      currentUser = email;
      document.getElementById("homepage").classList.add("hidden");
      document.getElementById("dashboard").classList.remove("hidden");
      document.getElementById("welcome-text").innerText = `Welcome: ${email}`;
      loadUnitList();
    }

    function createUnitDirectory() {
      const unitName = document.getElementById("unitName").value.trim();
      if (!unitName) return alert("Enter a valid unit name");
      if (!unitFolders.includes(unitName)) {
        unitFolders.push(unitName);
        saveUnits();
        loadUnitList();
        alert(`Unit folder '${unitName}' created.`);
      } else {
        alert("This unit already exists.");
      }
    }

    function loadUnitList() {
      const unitList = document.getElementById("unitList");
      unitList.innerHTML = "";
      unitFolders.forEach(folder => {
        const li = document.createElement("li");
        li.textContent = folder;
        unitList.appendChild(li);
      });
    }

    function loadUserList() {
      const userList = document.getElementById("userList");
      userList.innerHTML = "";
      for (const email in users) {
        const li = document.createElement("li");
        li.textContent = email;
        userList.appendChild(li);
      }
    }

    function searchUnits() {
      const input = document.getElementById("searchInput").value.toLowerCase();
      const list = document.getElementById("unitList").getElementsByTagName("li");
      for (let i = 0; i < list.length; i++) {
        const item = list[i];
        const text = item.textContent.toLowerCase();
        item.style.display = text.includes(input) ? "" : "none";
      }
    }
  </script></body>
</html>
