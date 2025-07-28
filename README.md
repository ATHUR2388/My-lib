<?php
session_start();
$conn = new mysqli("localhost", "root", "", "notehub");
if ($conn->connect_error) die("DB Connection failed: " . $conn->connect_error);

// LOGIN
if (isset($_POST['login'])) {
    $email = $_POST['email'];
    $pass = $_POST['password'];
    $stmt = $conn->prepare("SELECT * FROM users WHERE email=? AND password=?");
    $stmt->bind_param("ss", $email, $pass);
    $stmt->execute();
    $res = $stmt->get_result();
    if ($res->num_rows == 1) {
        $_SESSION['user'] = $email;
        header("Location: notehub.php");
        exit();
    } else {
        $error = "Invalid login!";
    }
}

// LOGOUT
if (isset($_GET['logout'])) {
    session_destroy();
    header("Location: notehub.php");
    exit();
}

// ADD YEAR
if (isset($_POST['add_year'])) {
    $name = $_POST['year_name'];
    $conn->query("INSERT INTO years (name) VALUES ('$name')");
}

// ADD SEMESTER
if (isset($_POST['add_semester'])) {
    $name = $_POST['semester_name'];
    $year_id = $_POST['year_id'];
    $conn->query("INSERT INTO semesters (year_id, name) VALUES ('$year_id', '$name')");
}

// ADD NOTE
if (isset($_POST['add_note'])) {
    $unit = $_POST['unit'];
    $title = $_POST['title'];
    $content = $_POST['content'];
    $semester_id = $_POST['semester_id'];
    $conn->query("INSERT INTO notes (semester_id, unit_name, title, content) 
                  VALUES ('$semester_id', '$unit', '$title', '$content')");
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>NoteHub</title>
    <style>
        body { font-family: sans-serif; margin: 20px; }
        input, textarea, select { margin: 5px; padding: 8px; width: 300px; }
        button { padding: 8px 15px; }
        .box { border: 1px solid #ccc; padding: 15px; margin-bottom: 20px; }
        h2 { margin-top: 40px; }
    </style>
</head>
<body>

<?php if (!isset($_SESSION['user'])): ?>
    <h2>Login to NoteHub</h2>
    <form method="POST">
        <input type="text" name="email" placeholder="Email" required><br>
        <input type="password" name="password" placeholder="Password" required><br>
        <button name="login">Login</button>
    </form>
    <?php if (isset($error)) echo "<p style='color:red;'>$error</p>"; ?>
<?php else: ?>
    <h2>Welcome, <?=$_SESSION['user']?> | <a href="?logout=1">Logout</a></h2>

    <!-- Add Year -->
    <div class="box">
        <h3>Add Study Year</h3>
        <form method="POST">
            <input type="text" name="year_name" placeholder="e.g. Year 1" required>
            <button name="add_year">Add Year</button>
        </form>
    </div>

    <!-- Show Years and Semesters -->
    <div class="box">
        <h3>Your Years & Semesters</h3>
        <?php
        $years = $conn->query("SELECT * FROM years");
        while ($y = $years->fetch_assoc()):
            echo "<strong>".$y['name']."</strong><br>";
            $yid = $y['id'];
            $semesters = $conn->query("SELECT * FROM semesters WHERE year_id=$yid");
            echo "<ul>";
            while ($s = $semesters->fetch_assoc()) {
                echo "<li>".$s['name']." <a href='?show_notes=1&sid=".$s['id']."'>[View/Add Notes]</a></li>";
            }
            echo "</ul>";
        ?>
        <form method="POST">
            <input type="hidden" name="year_id" value="<?=$y['id']?>">
            <input type="text" name="semester_name" placeholder="Add Semester" required>
            <button name="add_semester">Add Semester</button>
        </form>
        <hr>
        <?php endwhile; ?>
    </div>

    <!-- Add / View Notes -->
    <?php if (isset($_GET['show_notes'])):
        $sid = $_GET['sid'];
        $notes = $conn->query("SELECT * FROM notes WHERE semester_id=$sid");
    ?>
    <div class="box">
        <h3>Notes for Semester ID <?=$sid?></h3>

        <form method="POST">
            <input type="hidden" name="semester_id" value="<?=$sid?>">
            <input type="text" name="unit" placeholder="Unit Name" required><br>
            <input type="text" name="title" placeholder="Note Title" required><br>
            <textarea name="content" rows="5" placeholder="Write note here..."></textarea><br>
            <button name="add_note">Save Note</button>
        </form>

        <hr>
        <h4>Saved Notes:</h4>
        <?php while ($n = $notes->fetch_assoc()): ?>
            <div style="border:1px solid #999; padding:10px; margin-bottom:10px;">
                <strong>Unit:</strong> <?=$n['unit_name']?><br>
                <strong>Title:</strong> <?=$n['title']?><br>
                <p><?=$n['content']?></p>
            </div>
        <?php endwhile; ?>
    </div>
    <?php endif; ?>

<?php endif; ?>
</body>
</html>
