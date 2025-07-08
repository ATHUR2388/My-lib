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
    <button onclick="showSignUp()">Sign Up (Admin Only)</button>
  </div>  <div class="hidden" id="login-section">
    <h2>Login</h2>
    <input type="email" id="login-email" placeholder="Email" />
    <input type="password" id="login-password" placeholder="Password" />
    <br />
    <button onclick="signIn()">Login</button>
    <button onclick="backHome()">Back</button>
  </div>  <div class="hidden" id="signup-section">
    <h2>Admin Sign Up</h2>
    <input type="email" id="signup-email" placeholder="Email" />
    <input type="password" id="signup-password" placeholder="Password" />
    <input type="password" id="signup-confirm" placeholder="Confirm Password" />
    <br />
    <button onclick="signUp()">Register</button>
    <button onclick="backHome()">Back</button>
  </div>  <!-- (The rest of the code stays the same) --></body>
</html>
