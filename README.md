<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>WELCOME TO MY LIBRARY</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>WELCOME TO MY LIBRARY</h1>
    <nav>
      <input type="search" placeholder="Search..." />
      <button onclick="showPage('home')">Home</button>
      <button onclick="showPage('adminLogin')">Admin Login</button>
      <button onclick="showPage('memberSignup')">Member Sign Up</button>
    </nav>
  </header>
  <div class="container">
    <!-- HOME -->
    <div id="home">
      <h2>Explore Educational Resources</h2>
      <p>Sign in as an admin or register as a member to access and upload course notes.</p>
    </div><!-- ADMIN LOGIN -->
<div id="adminLogin" class="hidden">
  <h2>Admin Login</h2>
  <form onsubmit="adminLogin(event)">
    <input type="email" id="adminEmail" placeholder="Email" required />
    <input type="password" id="adminPassword" placeholder="Password" required />
    <div id="adminError" class="error"></div>
    <button type="submit">Login</button>
  </form>
</div>

<!-- ADMIN DASHBOARD -->
<div id="adminDashboard" class="hidden">
  <div class="admin-info" id="adminTopRight"></div>
  <h3>Create Admin Account</h3>
  <form onsubmit="saveAdminProfile(event)">
    <input type="text" id="name1" placeholder="First Name" required />
    <input type="text" id="name2" placeholder="Last Name" required />
    <input type="text" id="contact" placeholder="Contact" required />
    <input type="email" id="profileEmail" placeholder="Email" required />
    <input type="file" id="photo" accept="image/*" />
    <button type="submit">Save Profile</button>
  </form>

  <div class="unit-section">
    <h3>Create Unit Folders</h3>
    <select id="year">
      <option>1st Year</option>
      <option>2nd Year</option>
      <option>3rd Year</option>
    </select>
    <input type="text" id="unitName" placeholder="Unit Name" required />
    <select id="semester">
      <option>Semester 1</option>
      <option>Semester 2</option>
      <option>Semester 3</option>
    </select>
    <input type="file" id="unitFile" accept=".pdf,.doc,.ppt,.txt" />
    <button type="button" onclick="uploadNote()">Upload Note</button>
    <ul id="noteList"></ul>
  </div>

  <div class="unit-section">
    <h3>Educational Resources (External Links)</h3>
    <textarea placeholder="Paste educational website links here..."></textarea>
    <button onclick="alert('Link saved successfully (mock)!')">Save Link</button>
  </div>

  <div class="unit-section">
    <h3>Registered Members</h3>
    <table>
      <thead>
        <tr><th>Name</th><th>Email</th><th>Contact</th><th>Edit</th></tr>
      </thead>
      <tbody id="memberTable">
        <tr><td>Jane Doe</td><td>jane@example.com</td><td>0712345678</td><td><button onclick="editMember(this)">Edit</button></td></tr>
        <tr><td>John Smith</td><td>john@example.com</td><td>0700111222</td><td><button onclick="editMember(this)">Edit</button></td></tr>
      </tbody>
    </table>
  </div>
</div>

<!-- MEMBER SIGNUP -->
<div id="memberSignup" class="hidden">
  <h2>Member Sign Up</h2>
  <form onsubmit="registerMember(event)">
    <input type="text" id="memberName" placeholder="Full Name" required />
    <input type="email" id="memberEmail" placeholder="Email" required />
    <input type="text" id="memberContact" placeholder="Contact" required />
    <input type="password" placeholder="Password" required />
    <input type="file" accept="image/*" class="circle" />
    <button type="submit">Register</button>
  </form>
</div>

  </div>
  <footer>Created by athur @2024</footer>
  <script src="script.js"></script>
</body>
</html>
