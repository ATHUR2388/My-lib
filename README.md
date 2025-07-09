<!DOCTYPE html><html lang="en"><head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Admin Login</title>
  <link rel="stylesheet" href="styles.css">
  <script type="module">
    import { signInWithEmailAndPassword } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";
    import { auth } from "./firebase.js";window.addEventListener("DOMContentLoaded", () => {
  const form = document.getElementById("adminLoginForm");
  form.addEventListener("submit", async (e) => {
    e.preventDefault();
    const email = document.getElementById("adminEmail").value;
    const password = document.getElementById("adminPassword").value;

    if (email !== "athur2388@gmail.com" || password !== "Makuto2388") {
      alert("Incorrect admin credentials.");
      return;
    }

    try {
      await signInWithEmailAndPassword(auth, email, password);
      window.location.href = "admin-dashboard.html";
    } catch (error) {
      alert("Login failed: " + error.message);
    }
  });
});

  </script>
</head><body>
  <main>
    <h2>Admin Login</h2>
    <form id="adminLoginForm">
      <input type="email" id="adminEmail" placeholder="Admin Email" required />
      <input type="password" id="adminPassword" placeholder="Admin Password" required />
      <button type="submit">Login</button>
    </form>
  </main>
</body></html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>WELCOME TO MY LIBRARY</title>
  <link rel="stylesheet" href="styles.css" />
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
    import {
      getAuth,
      onAuthStateChanged,
      signInWithEmailAndPassword,
      createUserWithEmailAndPassword,
      signOut
    } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";
    import {
      getFirestore,
      doc,
      setDoc,
      getDoc,
      collection,
      addDoc,
      getDocs
    } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";
    import {
      getStorage,
      ref,
      uploadBytes,
      getDownloadURL
    } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-storage.js";

    // ✅ Replace these with your actual Firebase project config
    const firebaseConfig = {
      apiKey: "AIzaSyDExampleKey1234567890abcdef",
      authDomain: "your-library-project.firebaseapp.com",
      projectId: "your-library-project",
      storageBucket: "your-library-project.appspot.com",
      messagingSenderId: "123456789012",
      appId: "1:123456789012:web:abc123def456ghi789"
    };

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);
    const storage = getStorage(app);

    // 🔐 Protect dashboard pages
    onAuthStateChanged(auth, (user) => {
      const protectedPages = ["admin-dashboard.html", "member-dashboard.html"];
      const currentPage = window.location.pathname.split("/").pop();

      if (protectedPages.includes(currentPage) && !user) {
        alert("You must be logged in to access this page.");
        window.location.href = "index.html";
      }
    });

    // 🔗 Make Firebase accessible globally
    window.firebaseApp = {
      auth, db, storage,
      onAuthStateChanged,
      signInWithEmailAndPassword,
      createUserWithEmailAndPassword,
      signOut,
      setDoc, getDoc, doc, collection, addDoc, getDocs,
      ref, uploadBytes, getDownloadURL
    };
  </script>
</head>

<body>
  <header>
    <h1>WELCOME TO MY LIBRARY</h1>
    <nav>
      <a href="admin-login.html">Admin Login</a>
      <a href="member-signup.html">Member Sign Up</a>
      <input type="text" placeholder="Search..." class="search-box" />
    </nav>
  </header>

  <main>
    <section class="info">
      <h2>Explore Notes, Study Materials & More</h2>
      <p>Created by Athur @2024</p>
    </section>
  </main>

  <footer>
    <p>&copy; 2024 Created by Athur @2024</p>
  </footer>
</body>

</html>
