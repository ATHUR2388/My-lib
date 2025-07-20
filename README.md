<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Notes Portfolio</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f9ff;
      margin: 0;
      padding: 0;
    }
    header {
      background: #4a90e2;
      color: white;
      padding: 1em;
      text-align: center;
      font-size: 24px;
      font-weight: bold;
    }
    .container {
      padding: 2em;
    }
    .section {
      margin: 1em 0;
      border: 2px solid #4a90e2;
      border-radius: 15px;
      padding: 1em;
      background: #ffffff;
    }
    button {
      background-color: #4a90e2;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 10px;
      cursor: pointer;
      margin-right: 10px;
    }
    button:hover {
      background-color: #357ab8;
    }
    input, select {
      padding: 0.5em;
      margin: 0.5em 0;
      width: 100%;
      border: 1px solid #ccc;
      border-radius: 10px;
    }
    .folder-button {
      display: inline-block;
      margin: 5px 5px 0 0;
      padding: 8px 12px;
      background-color: #6cbf84;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }
    .folder-button:hover {
      background-color: #57a36f;
    }
    iframe.viewer {
      width: 100%;
      height: 600px;
      border: 2px solid #ccc;
      margin-top: 10px;
      border-radius: 10px;
    }
    .note-item {
      margin-bottom: 10px;
    }
    .nav-arrows {
      display: flex;
      justify-content: space-between;
      margin: 1em 0;
    }
    .nav-arrows button {
      font-size: 20px;
      padding: 10px;
      width: 60px;
    }
  </style>
</head>
<body>
  <header>My Notes Portfolio</header>
  <div class="container" id="mainContainer"></div>

  <script>
    const container = document.getElementById('mainContainer');
    const historyStack = [];

    function navigate(callback) {
      historyStack.push(container.innerHTML);
      callback();
    }

    function goBack() {
      if (historyStack.length > 0) {
        container.innerHTML = historyStack.pop();
      }
    }

    function loadYearSelection() {
      container.innerHTML = `
        <div class="section" id="yearSection">
          <label for="year">Select Year:</label>
          <select id="year">
            <option>Year 1</option>
            <option>Year 2</option>
            <option>Year 3</option>
          </select>
          <button onclick="navigate(goToSemesterPage)">Open Year Folder</button>
          <div id="savedYears"></div>
        </div>`;
    }

    function goToSemesterPage() {
      const year = document.getElementById('year').value;
      const semesters = ['Semester 1', 'Semester 2', 'Semester 3'];
      container.innerHTML = `
        <div class="nav-arrows">
          <button onclick="goBack()">⬅️</button>
          <button onclick="loadYearSelection()">🏠</button>
        </div>
        <div class="section">
          <h2>${year}</h2>
          ${semesters.map(s => `<button class='folder-button' onclick="navigate(() => goToUnitPage('${year}', '${s}'))">${s}</button>`).join('')}
        </div>`;
    }

    function goToUnitPage(year, semester) {
      const keyPrefix = `${year}_${semester}_`;
      const savedUnits = JSON.parse(localStorage.getItem('savedUnits')) || [];
      const filtered = savedUnits.filter(k => k.startsWith(keyPrefix));
      container.innerHTML = `
        <div class="nav-arrows">
          <button onclick="goBack()">⬅️</button>
          <button onclick="loadYearSelection()">🏠</button>
        </div>
        <div class="section">
          <h2>${year} - ${semester}</h2>
          <label for="unit">Enter Unit Name:</label>
          <input type="text" id="unit" placeholder="e.g. Anatomy">
          <button onclick="navigate(() => openUnit('${year}', '${semester}'))">Open Unit Folder</button>
          <h3>Existing Unit Folders:</h3>
          ${filtered.map(k => `<button class='folder-button' onclick="navigate(() => showUnitInterface('${k}'))">${k.split('_')[2]}</button> <button onclick="deleteFolder('${k}')">🗑️</button>`).join('<br>')}
        </div>`;
    }

    function openUnit(year, semester) {
      const unit = document.getElementById('unit').value.trim();
      if (!unit) {
        alert('Please enter a unit name.');
        return;
      }
      const key = `${year}_${semester}_${unit}`;
      const savedUnits = JSON.parse(localStorage.getItem('savedUnits')) || [];
      const notesByFolder = JSON.parse(localStorage.getItem('notesByFolder')) || {};
      if (!savedUnits.includes(key)) {
        savedUnits.push(key);
        localStorage.setItem('savedUnits', JSON.stringify(savedUnits));
        notesByFolder[key] = [];
        localStorage.setItem('notesByFolder', JSON.stringify(notesByFolder));
      }
      showUnitInterface(key);
    }

    function showUnitInterface(folderKey) {
      container.innerHTML = `
        <div class="nav-arrows">
          <button onclick="goBack()">⬅️</button>
          <button onclick="loadYearSelection()">🏠</button>
        </div>
        <div class="section">
          <h2>Folder: ${folderKey}</h2>
          <input type="file" id="fileUpload" />
          <button onclick="uploadNotes('${folderKey}')">Upload Notes</button>
        </div>
        <div class="section">
          <h3>Notes in Folder</h3>
          <div id="notesDisplay">Loading...</div>
          <iframe id="viewer" class="viewer" style="display:none;"></iframe>
        </div>`;
      displayNotes(folderKey);
    }

    function uploadNotes(folderKey) {
      const fileInput = document.getElementById('fileUpload');
      const file = fileInput.files[0];
      if (!file) {
        alert('Please select a file to upload.');
        return;
      }
      const reader = new FileReader();
      reader.onload = function(e) {
        const notesByFolder = JSON.parse(localStorage.getItem('notesByFolder')) || {};
        const fileData = {
          name: file.name,
          content: e.target.result,
          type: file.type
        };
        if (!notesByFolder[folderKey]) {
          notesByFolder[folderKey] = [];
        }
        notesByFolder[folderKey].push(fileData);
        localStorage.setItem('notesByFolder', JSON.stringify(notesByFolder));
        displayNotes(folderKey);
      };
      reader.readAsDataURL(file);
    }

    function displayNotes(folderKey) {
      const notesByFolder = JSON.parse(localStorage.getItem('notesByFolder')) || {};
      const notes = notesByFolder[folderKey] || [];
      const container = document.getElementById('notesDisplay');
      const viewer = document.getElementById('viewer');
      if (notes.length === 0) {
        container.innerHTML = 'No notes uploaded in this folder.';
        viewer.style.display = 'none';
        return;
      }
      container.innerHTML = '<ul>' + notes.map((note, index) => {
        const blob = dataURLtoBlob(note.content);
        const blobURL = URL.createObjectURL(blob);
        return `<li class="note-item">
            <strong>${note.name}</strong><br>
            <a href="#" onclick="showViewer('${folderKey}', ${index}); return false;">📖 Read Online</a> |
            <a href="${blobURL}" download="${note.name}">⬇️ Download</a> |
            <a href="#" onclick="deleteNote('${folderKey}', ${index}); return false;">🗑️ Delete</a>
          </li>`;
      }).join('') + '</ul>';
    }

    function deleteNote(folderKey, index) {
      const notesByFolder = JSON.parse(localStorage.getItem('notesByFolder')) || {};
      if (notesByFolder[folderKey]) {
        notesByFolder[folderKey].splice(index, 1);
        localStorage.setItem('notesByFolder', JSON.stringify(notesByFolder));
        displayNotes(folderKey);
      }
    }

    function deleteFolder(folderKey) {
      let savedUnits = JSON.parse(localStorage.getItem('savedUnits')) || [];
      let notesByFolder = JSON.parse(localStorage.getItem('notesByFolder')) || {};
      savedUnits = savedUnits.filter(unit => unit !== folderKey);
      delete notesByFolder[folderKey];
      localStorage.setItem('savedUnits', JSON.stringify(savedUnits));
      localStorage.setItem('notesByFolder', JSON.stringify(notesByFolder));
      goToUnitPage(...folderKey.split('_').slice(0, 2));
    }

    function showViewer(folderKey, index) {
      const notesByFolder = JSON.parse(localStorage.getItem('notesByFolder')) || {};
      const viewer = document.getElementById('viewer');
      const notes = notesByFolder[folderKey];
      const note = notes[index];
      if (!note || !note.type) {
        alert('Invalid note.');
        viewer.style.display = 'none';
        return;
      }
      if (note.type.startsWith('application/pdf') ||
          note.type.includes('presentation') ||
          note.type.includes('msword') ||
          note.type.includes('text')) {
        viewer.src = note.content;
        viewer.style.display = 'block';
      } else {
        alert('Preview not supported for this file type. Please download to view.');
        viewer.style.display = 'none';
      }
    }

    function dataURLtoBlob(dataurl) {
      const parts = dataurl.split(',');
      const mime = parts[0].match(/:(.*?);/)[1];
      const bstr = atob(parts[1]);
      let n = bstr.length;
      const u8arr = new Uint8Array(n);
      while (n--) {
        u8arr[n] = bstr.charCodeAt(n);
      }
      return new Blob([u8arr], { type: mime });
    }

    loadYearSelection();
  </script>
</body>
</html>
