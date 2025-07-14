<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Library Members</title>
  <style>
    table {
      width: 100%;
      border-collapse: collapse;
    }
    th, td {
      padding: 10px;
      border: 1px solid #ddd;
      text-align: center;
    }
    .circle {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      object-fit: cover;
    }
  </style>
</head>
<body>

  <h2>Registered Members</h2>

  <table>
    <thead>
      <tr>
        <th>Photo</th>
        <th>Name</th>
        <th>Email</th>
        <th>Contact</th>
      </tr>
    </thead>
    <tbody>
      <?php
        // Sample data if $members is not set
        $members = $members ?? [
          "John Doe|john@example.com|0712345678|john.jpg",
          "Jane Smith|jane@example.com|0798765432|",
          "Bob Lee|bob@example.com|0788001122|bob.jpg"
        ];

        foreach ($members as $member):
          $parts = explode("|", trim($member));
          $name = $parts[0] ?? 'Unknown';
          $email = $parts[1] ?? 'No Email';
          $contact = $parts[2] ?? 'No Contact';
          $photo = $parts[3] ?? '';
      ?>
        <tr>
          <td>
            <?php if (!empty($photo)): ?>
              <img src="../assets/uploads/<?php echo htmlspecialchars($photo); ?>" class="circle" alt="Photo" />
            <?php else: ?>
              <span>No Photo</span>
            <?php endif; ?>
          </td>
          <td><?php echo htmlspecialchars($name); ?></td>
          <td><?php echo htmlspecialchars($email); ?></td>
          <td><?php echo htmlspecialchars($contact); ?></td>
        </tr>
      <?php endforeach; ?>
    </tbody>
  </table>

</body>
</html>
