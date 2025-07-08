
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
  </style>
</head>
<body>
  <div class="background-books" id="homepage">
    <h1>WELCOME TO MAKUTO'S LIBRARY</h1>
    <button onclick="showLogin()">Log In</button>
    <button onclick="showSignUp()">Sign Up</button>
  </div>  <div class="hidden" id="login-section">
    <h2>Login</h2>
    <input type="email" id="login-email" placeholder="Email" />
    <input type="password" id="login-password" placeholder="Password" />
    <br />
    <button onclick="signIn()">Login</button>
    <button onclick="backHome()">Back</button>
  </div>  <div class="hidden" id="signup-section">
    <h2>Sign Up</h2>
    <input type="email" id="signup-email" placeholder="Email" />
    <input type="password" id="signup-password" placeholder="Password" />
    <input type="password" id="signup-confirm" placeholder="Confirm Password" />
    <br />
    <button onclick="signUp()">Register</button>
    <button onclick="backHome()">Back</button>
  </div>  <div id="dashboard" class="dashboard hidden">
    <h2 id="welcome-text"></h2>
    <button onclick="signOut()">Log Out</button>
    <input type="text" id="searchInput" onkeyup="searchUnits()" placeholder="Search for a unit..." /><div id="admin-section" class="admin-section hidden">
  <h3>Admin Panel</h3>
  <input type="text" id="unitName" placeholder="Create new unit directory" />
  <button onclick="createUnitDirectory()">Create Unit</button>
  <h4>Registered Users</h4>
  <ul id="userList"></ul>
</div>

<h3>Available Units (<span id="unitCount"></span>)</h3>
<ul id="unitList"></ul>

  </div>  <div id="unitView" class="dashboard hidden">
    <h3 id="selectedUnitTitle"></h3>
    <div id="uploadControls" class="hidden">
      <input type="file" id="fileInput" />
      <button onclick="uploadFile()">Upload File</button>
    </div>
    <button onclick="signOut()">Log Out</button>
    <button onclick="backToDashboard()">Back to Units</button><div class="notes-section">
  <h4>Uploaded Notes (<span id="notesCount"></span>)</h4>
  <ul id="uploadedFiles"></ul>
</div>

  </div>  <script>
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

    function showSignUp() {
      document.getElementById("homepage").classList.add("hidden");
      document.getElementById("signup-section").classList.remove("hidden");
    }

    function backHome() {
      document.getElementById("homepage").classList.remove("hidden");
      document.getElementById("login-section").classList.add("hidden");
      document.getElementById("signup-section").classList.add("hidden");
    }

    function saveUsers() { localStorage.setItem("users", JSON.stringify(users)); }
    function saveUnits() { localStorage.setItem("unitFolders", JSON.stringify(unitFolders)); }
    function saveFiles() { localStorage.setItem("unitFiles", JSON.stringify(unitFiles)); }

    function signUp() {
      const email = document.getElementById("signup-email").value;
      const password = document.getElementById("signup-password").value;
      const confirmPassword = document.getElementById("signup-confirm").value;
      if (users[email]) return alert("User already exists.");
      if (password !== confirmPassword) return alert("Passwords do not match.");
      users[email] = password;
      saveUsers();
      alert("Sign up successful. Please login.");
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
      if (!users[email] || users[email] !== password) return alert("Wrong password or user does not exist.");
      currentUser = email;
      document.getElementById("login-section").classList.add("hidden");
      document.getElementById("dashboard").classList.remove("hidden");
      document.getElementById("welcome-text").innerText = `Welcome: ${email}`;
      document.getElementById("admin-section").classList.add("hidden");
      loadUnitList();
    }

    function signOut() {
      currentUser = null;
      selectedUnit = null;
      document.getElementById("dashboard").classList.add("hidden");
      document.getElementById("unitView").classList.add("hidden");
      document.getElementById("homepage").classList.remove("hidden");
    }

    function backToDashboard() {
      document.getElementById("unitView").classList.add("hidden");
      document.getElementById("dashboard").classList.remove("hidden");
      loadUnitList();
    }

    function createUnitDirectory() {
      const unitName = document.getElementById("unitName").value.trim();
      if (!unitName) return alert("Enter a valid unit name");
      if (!unitFolders.includes(unitName)) {
        unitFolders.push(unitName);
        saveUnits();
        loadUnitList();
        alert(`Unit '${unitName}' created.`);
      } else alert("Unit already exists.");
    }

    function deleteUnit(folder) {
      if (!confirm(`Delete '${folder}'?`)) return;
      const index = unitFolders.indexOf(folder);
      if (index > -1) {
        unitFolders.splice(index, 1);
        delete unitFiles[folder];
        saveUnits();
        saveFiles();
        loadUnitList();
      }
    }

    function loadUnitList() {
      const unitList = document.getElementById("unitList");
      unitList.innerHTML = "";
      unitFolders.forEach((folder, i) => {
        const li = document.createElement("li");
        li.classList.add("unit-item");
        const span = document.createElement("span");
        span.textContent = `${i + 1}. ${folder}`;
        span.style.cursor = "pointer";
        span.onclick = () => openUnit(folder);
        const actionDiv = document.createElement("div");
        actionDiv.classList.add("unit-actions");
        if (currentUser === ADMIN_EMAIL) {
          const delBtn = document.createElement("button");
          delBtn.textContent = "Delete";
          delBtn.onclick = () => deleteUnit(folder);
          actionDiv.appendChild(delBtn);
        }
        li.appendChild(span);
        li.appendChild(actionDiv);
        unitList.appendChild(li);
      });
      document.getElementById("unitCount").innerText = unitFolders.length;
    }

    function openUnit(unitName) {
      selectedUnit = unitName;
      document.getElementById("dashboard").classList.add("hidden");
      document.getElementById("unitView").classList.remove("hidden");
      document.getElementById("selectedUnitTitle").innerText = `Unit: ${unitName}`;
      document.getElementById("uploadControls").classList.toggle("hidden", currentUser !== ADMIN_EMAIL);
      loadUploadedFiles();
    }

    function uploadFile() {
      const file = document.getElementById("fileInput").files[0];
      if (!file || !selectedUnit) return alert("Select file and unit.");
      const timestamp = new Date().toISOString();
      if (!unitFiles[selectedUnit]) unitFiles[selectedUnit] = [];
      unitFiles[selectedUnit].unshift({ name: file.name, timestamp, url: URL.createObjectURL(file) });
      saveFiles();
      loadUploadedFiles();
      alert(`Uploaded '${file.name}' to ${selectedUnit}`);
    }

    function deleteNote(index) {
      if (!selectedUnit || !confirm("Delete this note?")) return;
      unitFiles[selectedUnit].splice(index, 1);
      saveFiles();
      loadUploadedFiles();
    }

    function loadUploadedFiles() {
      const ul = document.getElementById("uploadedFiles");
      ul.innerHTML = "";
      const files = unitFiles[selectedUnit] || [];
      document.getElementById("notesCount").innerText = files.length;
      files.forEach((file, index) => {
        const li = document.createElement("li");
        const a = document.createElement("a");
        a.href = file.url;
        a.target = "_blank";
        a.textContent = `${index + 1}. ${file.timestamp} - ${file.name}`;

        li.appendChild(a);

        const actions = document.createElement("div");
        const downloadBtn = document.createElement("button");
        downloadBtn.textContent = "Download";
        downloadBtn.onclick = () => {
          const link = document.createElement('a');
          link.href = file.url;
          link.download = file.name;
          link.click();
        };
        actions.appendChild(downloadBtn);

        if (currentUser === ADMIN_EMAIL) {
          const delBtn = document.createElement("button");
          delBtn.textContent = "Delete";
          delBtn.onclick = () => deleteNote(index);
          actions.appendChild(delBtn);
        }

        li.appendChild(actions);
        ul.appendChild(li);
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
