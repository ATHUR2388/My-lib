<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WELCOME TO MY LIBRARY</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
    }
    header {
      background-color: #003366;
      color: #fff;
      text-align: center;
      padding: 2rem 1rem;
      border-bottom: 4px solid #0055a5;
    }
    header h1 {
      font-size: 2.5rem;
      margin-bottom: 0.5rem;
    }
    nav {
      display: flex;
      justify-content: center;
      margin: 1.5rem 0;
      gap: 1rem;
    }
    nav a {
      padding: 0.75rem 1.5rem;
      background-color: #0055a5;
      color: #fff;
      text-decoration: none;
      border-radius: 5px;
      border: 1px solid #003366;
      font-weight: bold;
    }
    nav a:hover {
      background-color: #003366;
    }
    .footer {
      text-align: center;
      padding: 2rem;
      margin-top: 4rem;
      background-color: #003366;
      color: white;
      border-top: 4px solid #0055a5;
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
      padding: 0.5rem;
      border: none;
      background: #0055a5;
      color: white;
      border-radius: 50%;
      font-size: 1.2rem;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <header>
