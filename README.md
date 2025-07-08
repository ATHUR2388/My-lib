
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
      text-align: center;
    }
    h1 {
      font-size: 2rem;
      color: #1d4ed8;
    }
    input, button {
      margin: 5px;
      padding: 10px;
      font-size: 1rem;
    }
    .upload-section, .files-section, .admin-section {
      margin-top: 20px;
    }
    a {
      color: #007bff;
      text-decoration: underline;
    }
    .background-books {
      background-image: url('https://images.unsplash.com/photo-1512820790803-83ca734da794');
      background-size: cover;
      background-position: center;
      padding: 40px 20px;
      border-radius: 10px;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <div class="background-books">
    <h1>WELCOME TO MAKUTO'S LIBRARY</h1>
  </div>  <div id="auth-section">
    <input type="email" id="email" placeholder="Email" />
    <input type="password" id="password" placeholder="Password" />
    <input type="password" id="confirmPassword" placeholder="Confirm Password (Sign Up only)" />
    <br />
    <button onclick="signUp()">Sign Up</button>
    <button onclick="signIn()">Sign In</button>
    <button onclick="signOut()">Sign Out</button>
  </div>  <div id="admin-section" class="admin-section hidden">
    <h3>Admin Panel</h3>
    <input type="text" id="unitName" placeholder="Create new unit directory" />
    <button onclick="createUnitDirectory()">Create Unit</button>
    <h4>Registered Users</h4>
    <ul id="userList"></ul>
    <h4>Created Units</h4>
    <ul id="unitList"></ul>
  </div>  <div class="upload-section hidden" id="upload-section">
    <p><strong id="user-email"></strong></p>
    <input type="file" id="fileInput" />
    <input type="text" id="unitFolder" placeholder="Enter Unit Folder Name" />
    <button onclick="uploadFile()">Upload File</button>
    <button onclick="loadFiles()">Load Uploaded Files</button>
  </div>  <div class="files-section">
    <h3>Uploaded Notes</h3>
    <ul id="fileList"></ul>
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
        document.getElementById("admin-section").classList.remove("hidden");
        document.getElementById("upload-section").classList.remove("hidden");
        document.getElementById("user-email").innerText = "Logged in as Admin";
        loadUserList();
        loadUnitList();
        return;
      }

      if (!users[email] || users[email] !== password) {
        alert("Wrong password or user does not exist.");
        return;
      }

      currentUser = email;
      document.getElementById("upload-section").classList.remove("hidden");
      document.getElementById("user-email").innerText = `Logged in as: ${email}`;
    }

    function signOut() {
      currentUser = null;
      document.getElementById("upload-section").classList.add("hidden");
      document.getElementById("admin-section").classList.add("hidden");
      document.getElementById("user-email").innerText = "";
    }

    function loadUserList() {
      const userList = document.getElementById("userList");
      userList.innerHTML = "";
      for (const [email, pwd] of Object.entries(users)) {
        const li = document.createElement("li");
        li.textContent = `${email}`;
        userList.appendChild(li);
      }
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

    function uploadFile() {
      const file = document.getElementById("fileInput").files[0];
      const unitFolder = document.getElementById("unitFolder").value.trim();
      if (!file || !unitFolder) return alert("Select a file and enter unit folder");

      const fakeURL = `https://storage.fake-firebase.com/notes/${unitFolder}/${file.name}`;
      alert(`File '${file.name}' uploaded to '${unitFolder}' (simulated).`);
    }

    function loadFiles() {
      const fileList = document.getElementById("fileList");
      fileList.innerHTML = "Example notes: ";

      const exampleFiles = ["unit1_note.pdf", "unit2_slides.pptx", "unit3_outline.docx"];
      exampleFiles.forEach(file => {
        const li = document.createElement("li");
        li.innerHTML = `<a href="#">${file}</a>`;
        fileList.appendChild(li);
      });
    }
  </script></body>
</html>
