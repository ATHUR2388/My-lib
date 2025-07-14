<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Welcome to My Library</title>
  <link rel="stylesheet" href="assets/css/style.css" />
</head>
<body>
  <header>
    <h1>WELCOME TO MY LIBRARY</h1>
    <nav>
      <a href="admin/login.php" target="_blank">Admin Login</a>
      <a href="members/signup.php" target="_blank">Member Signup/Login</a>
    </nav>
  </header>

  <div class="search-bar">
    <input type="text" placeholder="Search..." />
  </div>

  <footer>
    <p>Created by Athur @2024</p>
  </footer>

  <script src="assets/js/main.js"></script>
</body>
</html>
body {
  font-family: 'Segoe UI', sans-serif;
  margin: 0;
  background: #f4f6fc;
  color: #333;
}

header {
  background-color: #004aad;
  color: #fff;
  padding: 20px;
  text-align: center;
  animation: fadeIn 1s ease-in;
}

nav a {
  margin: 0 10px;
  padding: 10px 15px;
  background: #f6ba35;
  border-radius: 5px;
  color: #000;
  text-decoration: none;
  transition: background 0.3s ease;
}

nav a:hover {
  background: #ffd676;
}

.search-bar {
  margin: 30px auto;
  text-align: center;
}

.search-bar input {
  padding: 10px;
  width: 50%;
  border: 2px solid #004aad;
  border-radius: 5px;
  transition: width 0.3s ease;
}

.search-bar input:focus {
  width: 60%;
}

footer {
  background: #004aad;
  color: white;
  text-align: center;
  padding: 15px;
  position: fixed;
  width: 100%;
  bottom: 0;
}

@keyframes fadeIn {
  from {opacity: 0;}
  to {opacity: 1;}
}
<?php
session_start();
if ($_SERVER["REQUEST_METHOD"] === "POST") {
  $email = $_POST["email"];
  $password = $_POST["password"];

  // Simple hardcoded login
  if ($email === "athur2388@gmail.com" && $password === "Makuto2388") {
    $_SESSION["admin"] = true;
    header("Location: dashboard.php");
    exit;
  } else {
    $error = "Invalid login.";
  }
}
<?php
session_start();
if ($_SERVER["REQUEST_METHOD"] === "POST") {
  $email = $_POST["email"];
  $password = $_POST["password"];

  // Simple hardcoded login
  if ($email === "athur2388@gmail.com" && $password === "Makuto2388") {
    $_SESSION["admin"] = true;
    header("Location: dashboard.php");
    exit;
  } else {
    $error = "Invalid login.";
  }
}
?>

<!DOCTYPE html>
<html>
<head>
  <title>Admin Login</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
</head>
<body>
  <div class="login-box">
    <h2>Admin Login</h2>
    <form method="post">
      <input type="email" name="email" placeholder="Email" required />
      <input type="password" name="password" placeholder="Password" required />
      <button type="submit">Log In</button>
    </form>
    <?php if (isset($error)) echo "<p style='color:red;'>$error</p>"; ?>
  </div>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION["admin"])) {
  header("Location: login.php");
  exit;
}
?>

<!DOCTYPE html>
<html>
<head>
  <title>Admin Dashboard</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
</head>
<body>
  <header>
    <h2>Admin Dashboard</h2>
    <div class="profile-box">
      <img src="../assets/icons/default_profile.png" class="circle" alt="Admin Photo" />
      <p>Name: <strong>Athur Makuto</strong></p>
      <p>Email: athur2388@gmail.com</p>
      <p>Contact: +254XXXXXXX</p>
    </div>
  </header>

  <main>
    <section>
      <h3>Create Academic Folders</h3>
      <a href="create_units.php">Create Years → Units → Semesters</a>
    </section>

    <section>
      <h3>Manage Notes</h3>
      <a href="upload_notes.php">Upload & Edit Notes</a>
    </section>

    <section>
      <h3>Member Query List</h3>
      <a href="members_list.php">View Member Info</a>
    </section>

    <section>
      <h3>Educational Links</h3>
      <a href="external_links.php">Add/View Site Links</a>
    </section>
  </main>

  <footer>
    <p>Created by Athur @2024</p>
  </footer>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION["admin"])) {
  header("Location: login.php");
  exit;
}
?>

<!DOCTYPE html>
<html>
<head>
  <title>Create Unit Structure</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
  <style>
    .unit-form {
      margin: 20px auto;
      padding: 20px;
      border: 2px solid #004aad;
      background: #fff;
      border-radius: 10px;
      width: 70%;
    }
    select, input[type="text"] {
      padding: 10px;
      margin: 10px 0;
      width: 100%;
      border: 2px solid #ccc;
      border-radius: 5px;
    }
    .submit-btn {
      padding: 10px 20px;
      background: #004aad;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .submit-btn:hover {
      background: #003080;
    }
  </style>
</head>
<body>
  <h2 style="text-align:center;">Create Unit Folder</h2>
  <div class="unit-form">
    <form method="post" action="create_units.php">
      <label>Choose Year:</label>
      <select name="year" required>
        <option value="">Select Year</option>
        <option value="Year1">Year 1</option>
        <option value="Year2">Year 2</option>
        <option value="Year3">Year 3</option>
      </select>

      <label>Unit Name:</label>
      <input type="text" name="unit_name" placeholder="Enter Unit Name" required />

      <label>Semester:</label>
      <select name="semester" required>
        <option value="">Select Semester</option>
        <option value="Semester1">Semester 1</option>
        <option value="Semester2">Semester 2</option>
        <option value="Semester3">Semester 3</option>
      </select>

      <button class="submit-btn" type="submit">Create Folder</button>
    </form>
  </div>

  <?php
  if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $year = $_POST["year"];
    $unit = $_POST["unit_name"];
    $semester = $_POST["semester"];

    $path = "../assets/notes/$year/$unit/$semester";

    if (!file_exists($path)) {
      mkdir($path, 0777, true);
      echo "<p style='text-align:center; color:green;'>Folder created at: $path</p>";
    } else {
      echo "<p style='text-align:center; color:red;'>Folder already exists.</p>";
    }
  }
  ?>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION["admin"])) {
  header("Location: login.php");
  exit;
}

$basePath = "../assets/notes/";
$success = "";

if ($_SERVER["REQUEST_METHOD"] === "POST") {
  $year = $_POST["year"];
  $unit = $_POST["unit"];
  $semester = $_POST["semester"];
  $file = $_FILES["note_file"];

  $targetDir = $basePath . "$year/$unit/$semester/";
  if (!is_dir($targetDir)) mkdir($targetDir, 0777, true);

  $filename = basename($file["name"]);
  $targetPath = $targetDir . $filename;

  if (move_uploaded_file($file["tmp_name"], $targetPath)) {
    $success = "Note uploaded successfully to: $targetPath";
  } else {
    $success = "Upload failed.";
  }
}
?>

<!DOCTYPE html>
<html>
<head>
  <title>Upload Notes</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
</head>
<body>
  <h2 style="text-align:center;">Upload Notes to Unit</h2>
  <div class="unit-form">
    <form method="post" enctype="multipart/form-data">
      <label>Year:</label>
      <select name="year" required>
        <option value="Year1">Year 1</option>
        <option value="Year2">Year 2</option>
        <option value="Year3">Year 3</option>
      </select>

      <label>Unit Name:</label>
      <input type="text" name="unit" placeholder="Enter Unit Name" required />

      <label>Semester:</label>
      <select name="semester" required>
        <option value="Semester1">Semester 1</option>
        <option value="Semester2">Semester 2</option>
        <option value="Semester3">Semester 3</option>
      </select>

      <label>Upload Note:</label>
      <input type="file" name="note_file" accept=".pdf,.doc,.ppt,.txt" required />

      <button class="submit-btn" type="submit">Upload Note</button>
    </form>
    <?php if ($success) echo "<p style='color:green; text-align:center;'>$success</p>"; ?>
  </div>
</body>
</html>
<?php
session_start();
if ($_SERVER["REQUEST_METHOD"] === "POST") {
  $email = $_POST["email"];
  $password = password_hash($_POST["password"], PASSWORD_DEFAULT);
  $photo = $_FILES["photo"];
  $contact = $_POST["contact"];
  $name = $_POST["name"];

  $photoName = $photo["name"] ? uniqid() . "_" . $photo["name"] : "";
  $photoPath = "../assets/uploads/" . $photoName;

  if ($photo["tmp_name"]) {
    move_uploaded_file($photo["tmp_name"], $photoPath);
  }

  $data = "$name|$email|$contact|$photoName\n";
  file_put_contents("../assets/members.txt", $data, FILE_APPEND);

  $_SESSION["member"] = $email;
  header("Location: dashboard.php");
  exit;
}
?>

<!DOCTYPE html>
<html>
<head>
  <title>Member Sign-Up</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
</head>
<body>
  <h2 style="text-align:center;">Register as a Member</h2>
  <div class="unit-form">
    <form method="post" enctype="multipart/form-data">
      <input type="text" name="name" placeholder="Full Name" required />
      <input type="email" name="email" placeholder="Email Address" required />
      <input type="text" name="contact" placeholder="Phone Number" required />
      <input type="password" name="password" placeholder="Set Password" required />
      <label>Upload Profile Photo (Optional)</label>
      <input type="file" name="photo" accept="image/*" />
      <button class="submit-btn" type="submit">Sign Up</button>
    </form>
  </div>
</body>
  <?php
session_start();
$members = file("../assets/members.txt");

if ($_SERVER["REQUEST_METHOD"] === "POST") {
  $email = $_POST["email"];
  $password = $_POST["password"];

  foreach ($members as $member) {
    list($name, $mem_email, $contact, $photo) = explode("|", trim($member));
    if ($email === $mem_email) {
      $_SESSION["member"] = $email;
      header("Location: dashboard.php");
      exit;
    }
  }
  $error = "Invalid login.";
}
?>

<!DOCTYPE html>
<html>
<head>
  <title>Member Login</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
</head>
<body>
  <div class="login-box">
    <h2>Member Login</h2>
    <form method="post">
      <input type="email" name="email" placeholder="Email" required />
      <input type="password" name="password" placeholder="Password" required />
      <button type="submit">Log In</button>
    </form>
    <?php if (isset($error)) echo "<p style='color:red;'>$error</p>"; ?>
  </div>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION["member"])) {
  header("Location: login.php");
  exit;
}

$email = $_SESSION["member"];
$members = file("../assets/members.txt");

foreach ($members as $member) {
  list($name, $mem_email, $contact, $photo) = explode("|", trim($member));
  if ($email === $mem_email) {
    $user = ["name" => $name, "email" => $email, "contact" => $contact, "photo" => $photo];
    break;
  }
}
?>

<!DOCTYPE html>
<html>
<head>
  <title>Member Dashboard</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
</head>
<body>
  <header>
    <h2>Welcome, <?php echo $user["name"]; ?></h2>
    <?php if ($user["photo"]) { ?>
      <img src="../assets/uploads/<?php echo $user["photo"]; ?>" class="circle" style="width:60px; border-radius:50%;" alt="Profile" />
    <?php } ?>
    <p>Email: <?php echo $user["email"]; ?></p>
    <p>Contact: <?php echo $user["contact"]; ?></p>
  </header>

  <main>
    <section>
      <h3>Read & Download Notes</h3>
      <p><a href="../assets/notes/">Access Notes</a></p>
    </section>

    <section>
      <h3>Explore External Books</h3>
      <p><a href="external_links.php">Educational Links</a></p>
    </section>

    <section>
      <h3>Edit Profile</h3>
      <p><a href="edit_profile.php">Update Info</a></p>
    </section>
  </main>

  <footer>
    <p>Created by Athur @2024</p>
  </footer>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION["admin"])) {
  header("Location: login.php");
  exit;
}

$linkFile = "../assets/links.txt";
if ($_SERVER["REQUEST_METHOD"] === "POST") {
  $title = $_POST["title"];
  $url = $_POST["url"];
  $entry = "$title|$url\n";
  file_put_contents($linkFile, $entry, FILE_APPEND);
}

$links = file_exists($linkFile) ? file($linkFile) : [];
?>

<!DOCTYPE html>
<html>
<head>
  <title>Manage Educational Links</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
</head>
<body>
  <h2 style="text-align:center;">Add Educational Links</h2>
  <div class="unit-form">
    <form method="post">
      <input type="text" name="title" placeholder="Site Title" required />
      <input type="url" name="url" placeholder="https://example.com" required />
      <button class="submit-btn" type="submit">Add Link</button>
    </form>
  </div>

  <h3 style="text-align:center;">Available Links</h3>
  <ul style="width:60%; margin:auto;">
    <?php foreach ($links as $link) {
      list($title, $url) = explode("|", trim($link));
      echo "<li><a href='$url' target='_blank'>$title</a></li>";
    } ?>
  </ul>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION["member"])) {
  header("Location: login.php");
  exit;
}

$links = file_exists("../assets/links.txt") ? file("../assets/links.txt") : [];
?>

<!DOCTYPE html>
<html>
<head>
  <title>Educational Links</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
</head>
<body>
  <h2 style="text-align:center;">Educational Resources</h2>
  <ul style="width:60%; margin:auto;">
    <?php foreach ($links as $link) {
      list($title, $url) = explode("|", trim($link));
      echo "<li><a href='$url' target='_blank'>$title</a></li>";
    } ?>
  </ul>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION["admin"])) {
  header("Location: login.php");
  exit;
}

$members = file_exists("../assets/members.txt") ? file("../assets/members.txt") : [];
?>

<!DOCTYPE html>
<html>
<head>
  <title>Registered Members</title>
  <link rel="stylesheet" href="../assets/css/style.css" />
  <style>
    .search-bar input {
      padding: 10px;
      width: 50%;
      border: 2px solid #004aad;
      margin: 20px auto;
      display: block;
      border-radius: 5px;
    }
    table {
      width: 80%;
      margin: auto;
      border-collapse: collapse;
    }
    th, td {
      border: 1px solid #004aad;
      padding: 10px;
      text-align: center;
    }
    img.circle {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      object-fit: cover;
    }
  </style>
  <script>
    function searchMembers() {
      let input = document.getElementById("searchInput").value.toLowerCase();
      let rows = document.querySelectorAll("table tbody tr");
      rows.forEach(row => {
        row.style.display = row.textContent.toLowerCase().includes(input) ? "" : "none";
      });
    }
  </script>
</head>
<body>
  <h2 style="text-align:center;">Registered Members</h2>
  <div class="search-bar">
    <input type="text" id="searchInput" placeholder="Search members..." onkeyup="searchMembers()" />
  </div>

  <table>
    <thead>
      <tr>
        <th>Photo</th>
        <th>Full Name</th>
        <th>Email</th>
        <th>Contact</th>
      </tr>
    </thead>
    <tbody>
      <?php foreach ($members as $member): 
        list($name, $email, $contact, $photo) = explode("|", trim($member)); ?>
        <tr>
          <td>
            <?php if ($photo): ?>
              <img src="../assets/uploads/<?php echo $photo; ?>" class="circle" alt="Member Photo" />
            <?php else: ?>
              <span>No Photo</span>
            <?php endif; ?>
          </td>
          <td><?php echo $name; ?></td>
          <td><?php echo $email; ?></td>
          <td><?php echo $contact; ?></td>
        </tr>
      <?php endforeach; ?>
    </tbody>
  </table>
</body>
</html>
</html>
