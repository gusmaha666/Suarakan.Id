<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Suarakan.id</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      padding: 0;
      background: #f9f9f9;
    }
    .landing {
      height: 100vh;
      background: linear-gradient(to right, #0077cc, #00aaff);
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 2rem;
    }
    .landing h1 {
      font-size: 3rem;
      margin-bottom: 1rem;
    }
    .landing p {
      font-size: 1.3rem;
      margin-bottom: 2rem;
      max-width: 600px;
    }
    .landing button {
      padding: 0.8rem 2rem;
      font-size: 1rem;
      border: none;
      background: white;
      color: #0077cc;
      border-radius: 30px;
      cursor: pointer;
      transition: 0.3s;
    }
    .landing button:hover {
      background: #e0e0e0;
    }
    .main-app {
      display: none;
    }
    header {
      background: #0077cc;
      color: white;
      padding: 1rem;
      text-align: center;
    }
    nav {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 1rem;
      background: #eee;
      padding: 0.5rem;
    }
    nav button {
      padding: 0.5rem 1rem;
      border: none;
      background: #ddd;
      cursor: pointer;
      text-align: left;
      max-width: 200px;
    }
    nav button.active {
      background: #0077cc;
      color: white;
    }
    nav button small {
      display: block;
      font-size: 0.75rem;
      color: #444;
    }
    nav button.active small {
      color: #fff;
    }
    .content {
      padding: 1rem;
      max-width: 800px;
      margin: auto;
    }
    .message-form {
      margin-bottom: 2rem;
    }
    textarea {
      width: 100%;
      height: 80px;
      padding: 0.5rem;
      font-size: 1rem;
    }
    .message {
      border-bottom: 1px solid #ccc;
      padding: 0.5rem 0;
    }
    .like-button, .comment-button {
      background: none;
      border: none;
      color: #0077cc;
      cursor: pointer;
      margin-right: 10px;
    }
    .comment-section {
      margin-left: 1rem;
      font-size: 0.9rem;
    }
    .login-box {
      padding: 1rem;
      background: #eee;
      text-align: center;
    }
    .login-box input {
      padding: 0.4rem;
      margin: 0.2rem;
    }
  </style>
</head>
<body>
  <!-- Landing Page -->
  <section class="landing" id="landing">
    <h1>Selamat Datang di Suarakan.id</h1>
    <p>Platform untuk menyuarakan pendapatmu, berbagi cerita, dan menyampaikan kritik serta saran dengan aman — anonim atau tidak, kamu bebas bicara.</p>
    <button onclick="enterApp()">Mulai</button>
  </section>

  <!-- Main App -->
  <div class="main-app" id="app">
    <header>
      <h1>Suarakan.id</h1>
    </header>

    <div class="login-box">
      <label>Nama: <input type="text" id="nameInput"></label>
      <label>Asal: <input type="text" id="originInput"></label>
      <button onclick="simpleLogin()">Login</button>
      <button onclick="logout()">Logout</button>
      <div><strong id="user-info">Belum login</strong></div>
    </div>

    <nav>
      <button onclick="switchTab('berani')" class="active">
        #SuaraBerani<br>
        <small>Lawan Bullying, curhatkan isi hati dan beri dukungan pada sesama!</small>
      </button>
      <button onclick="switchTab('aspirasi')">
        #SuaraAspirasi<br>
        <small>Sampaikan kritik dan saran untuk perubahan yang lebih baik!</small>
      </button>
      <button onclick="switchTab('cerita')">
        #SuaraCerita<br>
        <small>Bagikan pengalaman positif dan inspiratif!</small>
      </button>
    </nav>

    <div class="content">
      <div class="message-form">
        <h2>Tulis Suaramu</h2>
        <p id="formDescription" style="font-style: italic; color: #555;">
          Lawan Bullying, curhatkan isi hati dan beri dukungan pada sesama!
        </p>
        <textarea id="userInput" placeholder="Tulis pesanmu di sini..."></textarea>
        <br>
        <label><input type="checkbox" id="anon"> Kirim secara anonim</label>
        <br><br>
        <button onclick="submitMessage()">Kirim</button>
      </div>
      <div id="messages"></div>
    </div>
  </div>

  <script>
    let currentTab = 'berani';
    let userData = JSON.parse(localStorage.getItem('suarakan_user') || 'null');

    function enterApp() {
      document.getElementById('landing').style.display = 'none';
      document.getElementById('app').style.display = 'block';
    }

    function updateUserDisplay() {
      const info = document.getElementById('user-info');
      if (userData) {
        info.textContent = `Login sebagai: ${userData.name} dari ${userData.origin}`;
      } else {
        info.textContent = 'Belum login';
      }
    }

    function simpleLogin() {
      const name = document.getElementById('nameInput').value.trim();
      const origin = document.getElementById('originInput').value.trim();
      if (name && origin) {
        userData = { name, origin };
        localStorage.setItem('suarakan_user', JSON.stringify(userData));
        updateUserDisplay();
      } else {
        alert("Harap isi nama dan asal.");
      }
    }

    function logout() {
      userData = null;
      localStorage.removeItem('suarakan_user');
      updateUserDisplay();
    }

    function getMessages() {
      return JSON.parse(localStorage.getItem('suarakan_messages') || '{}');
    }

    function saveMessages(messages) {
      localStorage.setItem('suarakan_messages', JSON.stringify(messages));
    }

    function switchTab(tab) {
      currentTab = tab;
      document.querySelectorAll('nav button').forEach(btn => btn.classList.remove('active'));
      document.querySelector(`nav button[onclick="switchTab('${tab}')"]`).classList.add('active');

      // Ubah deskripsi di bawah "Tulis Suaramu"
      const formDesc = document.getElementById('formDescription');
      if (tab === 'berani') {
        formDesc.textContent = 'Lawan Bullying, curhatkan isi hati dan beri dukungan pada sesama!';
      } else if (tab === 'aspirasi') {
        formDesc.textContent = 'Sampaikan kritik dan saran untuk perubahan yang lebih baik pada komunitasmu!';
      } else if (tab === 'cerita') {
        formDesc.textContent = 'Bagikan pengalaman positif dan inspiratif yang kamu miliki bersama orang-orang dilingkunganmu!';
      }

      displayMessages();
    }

    function submitMessage() {
      const input = document.getElementById('userInput');
      const isAnon = document.getElementById('anon').checked;
      const username = isAnon || !userData ? 'Anonim' : `${userData.name} (${userData.origin})`;
      const text = input.value.trim();
      if (text) {
        const allMessages = getMessages();
        if (!allMessages[currentTab]) allMessages[currentTab] = [];
        allMessages[currentTab].unshift({ text, user: username, likes: 0, comments: [] });
        saveMessages(allMessages);
        input.value = '';
        displayMessages();
      }
    }

    function likeMessage(index) {
      const allMessages = getMessages();
      allMessages[currentTab][index].likes++;
      saveMessages(allMessages);
      displayMessages();
    }

    function addComment(index) {
      const comment = prompt("Tulis komentar Anda:");
      if (comment) {
        const username = userData ? `${userData.name} (${userData.origin})` : 'Anonim';
        const allMessages = getMessages();
        allMessages[currentTab][index].comments.push({ user: username, text: comment });
        saveMessages(allMessages);
        displayMessages();
      }
    }

    function displayMessages() {
      const allMessages = getMessages();
      const container = document.getElementById('messages');
      container.innerHTML = '';
      const tabMessages = allMessages[currentTab] || [];
      tabMessages.forEach((msg, index) => {
        const div = document.createElement('div');
        div.className = 'message';
        div.innerHTML = `<strong>${msg.user}:</strong> <p>${msg.text}</p>
          <button class="like-button" onclick="likeMessage(${index})">&#128077; ${msg.likes}</button>
          <button class="comment-button" onclick="addComment(${index})">Komentar</button>`;

        if (msg.comments && msg.comments.length > 0) {
          const commentDiv = document.createElement('div');
          commentDiv.className = 'comment-section';
          msg.comments.forEach(c => {
            const p = document.createElement('p');
            p.innerHTML = `<strong>${c.user}:</strong> ${c.text}`;
            commentDiv.appendChild(p);
          });
          div.appendChild(commentDiv);
        }

        container.appendChild(div);
      });
    }

    updateUserDisplay();
    displayMessages();
  </script>
</body>
</html>
