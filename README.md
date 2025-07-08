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
    .upload-section, .files-section {
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
  </style>  <!-- Firebase Scripts -->  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-storage-compat.js"></script></head>
<body>  <div class="background-books">
    <h1>WELCOME TO MAKUTO'S LIBRARY</h1>
  </div>  <div class="upload-section" id="upload-section">
    <input type="file" id="fileInput" />
    <button onclick="uploadFile()">Upload File</button>
    <button onclick="loadFiles()">Load Uploaded Files</button>
  </div>  <div class="files-section">
    <h3>Uploaded Notes</h3>
    <ul id="fileList"></ul>
  </div>  <script>
    const firebaseConfig = {
      apiKey: "AIzaSyDRkd0dWqI4fiTa-KQDt3ldfe4Wi75A6-A",
      authDomain: "clinical-medicine-2fc52.firebaseapp.com",
      projectId: "clinical-medicine-2fc52",
      storageBucket: "clinical-medicine-2fc52.appspot.com",
      messagingSenderId: "924963533641",
      appId: "1:924963533641:android:88286d9ff4c0f89b652098"
    };

    firebase.initializeApp(firebaseConfig);
    const storage = firebase.storage();

    function uploadFile() {
      const file = document.getElementById("fileInput").files[0];
      if (!file) return alert("Please select a file");
      const storageRef = storage.ref("notes/" + file.name);
      storageRef.put(file).then(() => {
        alert("File uploaded successfully!");
      }).catch(err => alert(err.message));
    }

    function loadFiles() {
      const listRef = storage.ref("notes/");
      const fileList = document.getElementById("fileList");
      fileList.innerHTML = "Loading...";

      listRef.listAll()
        .then(res => {
          fileList.innerHTML = "";
          res.items.forEach(itemRef => {
            itemRef.getDownloadURL().then(url => {
              const li = document.createElement("li");
              li.innerHTML = `<a href="${url}" target="_blank">${itemRef.name}</a>`;
              fileList.appendChild(li);
            });
          });
        })
        .catch(err => alert("Failed to list files: " + err.message));
    }
  </script></body>
</html>
