<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WELCOME TO MY LIBRARY</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { font-family: Arial, sans-serif; background-color: #f4f4f4; }
    header {
      background-color: #003366;
      color: #fff;
      text-align: center;
      padding: 2rem;
      border-bottom: 4px solid #0055a5;
    }
    header h1 {
      font-size: 2.5rem;
    }
    nav {
      display: flex;
      justify-content: center;
      gap: 1rem;
      margin: 1rem;
    }
    nav a {
      background-color: #0055a5;
      color: #fff;
      padding: 0.75rem 1.5rem;
      border-radius: 5px;
      text-decoration: none;
      border: 1px solid #003366;
      font-weight: bold;
    }
    nav a:hover {
      background-color: #003366;
    }
    .footer {
      text-align: center;
      padding: 2rem;
      background-color: #003366;
      color: white;
      border-top: 4px solid #0055a5;
      margin-top: 2rem;
    }
    .search-bar {
      display: flex;
      justify-content: flex-end;
      padding: 1rem;
    }
    .search-bar input {
      padding: 0.5rem;
      width: 250px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    .arrows {
      position: fixed;
      bottom: 20px;
      right: 20px;
      display: flex;
      gap: 10px;
    }
    .arrows button {
      padding: 0.5rem 0.8rem;
      border: none;
      background: #0055a5;
      color: white;
      border-radius: 50%;
      font-size: 1.2rem;
      cursor: pointer;
    }
    .section {
      max-width: 800px;
      margin: 2rem auto;
      padding: 1rem;
      border: 1px solid #ccc;
      border-radius: 8px;
      background-color: white;
    }
    .section h2 {
      margin-bottom: 1rem;
      color: #003366;
    }
    .button {
      background-color: #0055a5;
      color: white;
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 5px;
      margin-top: 1rem;
      cursor: pointer;
    }
    .button:hover {
      background-color: #003366;
    }
    .profile-pic {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      object-fit: cover;
      border: 2px solid #003366;
    }
    .top-right {
      position: absolute;
      top: 1rem;
      right: 1rem;
      text-align: right;
    }
  </style>
</head>
<body>
  <header>
    <h1>WELCOME TO MY LIBRARY</h1>
  </header>  <div class="top-right" id="user-info">
    <!-- Admin or Member info shown here -->
  </div>  <div class="search-bar">
    <input type="text" placeholder="Search...">
  </div>  <nav>
    <a href="admin-login.html">Admin Sign In</a>
    <a href="member-signup.html">Member Sign Up</a>
  </nav>  <div class="section">
    <h2>Library Features</h2>
    <ul>
      <li>Admin login with fixed credentials</li>
      <li>Admin creates member accounts (picture, name, contact, email)</li>
      <li>Members sign up with email, password, optional circular photo</li>
      <li>Admin dashboard: create folders by year → semester → unit</li>
      <li>Upload and manage notes: PDF, DOC, PPT, TXT</li>
      <li>Notes editable by admin, downloadable/readable by members</li>
      <li>Search available on all pages</li>
      <li>Cloud/online-only file storage and educational links section</li>
      <li>Registered member list with full account details</li>
      <li>Navigation using ← × → buttons</li>
    </ul>
    <button class="button" onclick="alert('Coming soon: Full functionality')">Explore Dashboard</button>
  </div>  <div class="footer">
    created by athur @2024
  </div>  <div class="arrows">
    <button onclick="history.back()">←</button>
    <button onclick="window.close()">×</button>
    <button onclick="history.forward()">→</button>
  </div>
</body>
</html>
