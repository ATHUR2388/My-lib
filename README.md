<!DOCTYPE html><html lang="en">
<head>
  <!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Admin Dashboard</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background-color: #f8f9fa;
    }
    header {
      background-color: #007bff;
      color: white;
      padding: 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 2px solid #0056b3;
    }
    .admin-info {
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .admin-info img {
      width: 50px;
      height: 50px;
      object-fit: cover;
      border-radius: 50%;
      border: 2px solid white;
    }
    main {
      padding: 20px;
    }
    form {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      max-width: 500px;
      margin-bottom: 30px;
    }
    input, button {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      margin-bottom: 15px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      background-color: #007bff;
      color: white;
      border: none;
    }
    button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
  <header>
    <h2>Admin Dashboard</h2>
    <div class="admin-info" id="adminDisplay">
      <!-- Will be filled with admin details -->
    </div>
  </header>  <main>
    <form id="adminProfileForm">
      <h3>Create Your Admin Account</h3>
      <input type="text" id="name1" placeholder="First Name" required />
      <input type="text" id="name2" placeholder="Last Name" required />
      <input type="text" id="contact" placeholder="Contact" required />
      <input type="email" id="email" placeholder="Email" required />
      <input type="file" id="photo" accept="image/*" />
      <button type="submit">Save Profile</button>
    </form>
  </main>  <script>
    const form = document.getElementById('adminProfileForm');
    const display = document.getElementById('adminDisplay');

    form.addEventListener('submit
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WELCOME TO MY LIBRARY</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header class="main-header">
    <h1>WELCOME TO MY LIBRARY</h1>
    <nav>
      <button onclick="location.href='admin-login.html'">Admin Login</button>
      <button onclick="location.href='member-signup.html'">Member Sign Up</button>
      <input type="search" placeholder="Search...">
    </nav>
  </header>  <main>
    <section>
      <h2>Explore Educational Resources</h2>
      <p>Sign in as an admin or register as a member to access and upload course notes.</p>
    </section>
  </main>  <footer>
    <p>Created by athur @2024</p>
  </footer>

</html>
