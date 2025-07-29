<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
  <title>Trò Chơi Súng Lục – Mobile + Ổ Đạn Tròn Chuẩn</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: url('assets/background.jpg') center center / cover no-repeat;
      font-family: 'Segoe UI', sans-serif;
    }
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    .container {
      text-align: center;
      width: 100vw;
      position: relative;
      z-index: 1;
    }
    .gun-image {
      width: 55vw;
      max-width: 400px;
      height: auto;
      pointer-events: none;
      transition: transform 0.1s ease;
    }
    .smoke {
      position: absolute;
      width: 80px;
      height: 80px;
      background: url('assets/smoke.png') center center / contain no-repeat;
      opacity: 0;
      animation: puff 0.5s ease-out forwards;
    }
    @keyframes puff {
      0% { transform: scale(0.5); opacity: 1; }
      100% { transform: scale(1.5); opacity: 0; }
    }
    .bullet {
      position: absolute;
      width: 20px;
      height: 10px;
      background: gold;
      border-radius: 5px;
      animation: fly 0.5s ease-out forwards;
    }
    @keyframes fly {
      0% { left: 50%; top: 50%; transform: translate(-50%, -50%) scale(1); }
      100% { left: 100vw; top: 40%; transform: translate(-50%, -50%) scale(1.2); }
    }
    .controls {
      margin-top: 10px;
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      justify-content: center;
    }
    .controls button {
      padding: 10px 18px;
      font-size: 0.9rem;
      font-weight: bold;
      border: none;
      border-radius: 6px;
      background-color: #ff5252;
      color: white;
      cursor: pointer;
    }
    .log {
      background: rgba(0,0,0,0.6);
      color: white;
      padding: 6px;
      margin-top: 8px;
      height: 80px;
      overflow-y: auto;
      font-size: 0.8rem;
      width: 90vw;
      max-width: 420px;
    }
    .cylinder-view {
      display: none;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 220px;
      height: 220px;
      border-radius: 50%;
      background: rgba(0, 0, 0, 0.6);
      z-index: 2;
    }
    .chamber {
      position: absolute;
      width: 40px;
      height: 40px;
      background: #444;
      border: 2px solid #aaa;
      border-radius: 50%;
      cursor: pointer;
    }
    .chamber.loaded {
      background: red;
    }
  </style>
</head>
<body>
  <div class="container">
    <img src="assets/gun.png" alt="Khẩu súng" class="gun-image" id="gun">
    <div class="controls">
      <button onclick="loadBullet()">🔄 Nạp đạn</button>
      <button onclick="spinCylinder()">🌀 Xoay ổ</button>
      <button onclick="toggleCylinderView()">🔍 Xem ổ đạn</button>
    </div>
    <div class="log" id="log"></div>
  </div>

  <div class="cylinder-view" id="cylinderView"></div>

  <audio id="sfx-load" src="assets/reload.mp3"></audio>
  <audio id="sfx-spin" src="assets/spin.mp3"></audio>
  <audio id="sfx-fire" src="assets/gunshot.mp3"></audio>
  <audio id="sfx-click" src="assets/click.mp3"></audio>

  <script>
    const gun = document.getElementById('gun');
    const logBox = document.getElementById('log');
    const cylinder = document.getElementById('cylinderView');
    let chambers = Array(8).fill(false);
    let current = 0;

    function log(msg) {
      logBox.innerHTML += `> ${msg}<br>`;
      logBox.scrollTop = logBox.scrollHeight;
    }

    function playSound(id) {
      const audio = document.getElementById(id);
      if (audio) {
        audio.currentTime = 0;
        audio.play();
      }
    }

    function loadBullet() {
      const empty = chambers.map((v, i) => (!v ? i : -1)).filter(i => i !== -1);
      if (!empty.length) return log("❗Ổ đã đầy!");
      const index = empty[Math.floor(Math.random() * empty.length)];
      chambers[index] = true;
      playSound("sfx-load");
      updateCylinder();
      log(`🔫 Nạp đạn vào ổ số ${index + 1}`);
    }

    function spinCylinder() {
      current = Math.floor(Math.random() * 8);
      playSound("sfx-spin");
      log("🌀 Xoay ổ quay...");
    }

    function fire() {
      const fired = chambers[current];
      if (fired) {
        chambers[current] = false;
        playSound("sfx-fire");
        log("💥 BANG! Trúng đạn!");
        showSmoke();
        showBullet();
        shakeGun();
      } else {
        playSound("sfx-click");
        log("✅ Click! Không có đạn.");
      }
      current = (current + 1) % 8;
      updateCylinder();
    }

    function showSmoke() {
      const smoke = document.createElement('div');
      smoke.className = 'smoke';
      document.body.appendChild(smoke);
      setTimeout(() => smoke.remove(), 600);
    }

    function showBullet() {
      const bullet = document.createElement('div');
      bullet.className = 'bullet';
      document.body.appendChild(bullet);
      setTimeout(() => bullet.remove(), 600);
    }

    function shakeGun() {
      gun.style.transform = 'rotate(-2deg)';
      setTimeout(() => gun.style.transform = 'rotate(2deg)', 60);
      setTimeout(() => gun.style.transform = 'rotate(0)', 120);
    }

    function toggleCylinderView() {
      cylinder.style.display = cylinder.style.display === 'block' ? 'none' : 'block';
      updateCylinder();
    }

    function updateCylinder() {
      cylinder.innerHTML = '';
      const radius = 80;
      const centerX = 110;
      const centerY = 110;
      for (let i = 0; i < 8; i++) {
        const angle = (360 / 8) * i * Math.PI / 180;
        const x = centerX + radius * Math.cos(angle);
        const y = centerY + radius * Math.sin(angle);
        const div = document.createElement('div');
        div.className = 'chamber' + (chambers[i] ? ' loaded' : '');
        div.style.left = `${x - 20}px`;
        div.style.top = `${y - 20}px`;
        div.title = `Ổ số ${i + 1}`;
        div.onclick = () => {
          chambers[i] = !chambers[i];
          updateCylinder();
        };
        cylinder.appendChild(div);
      }
    }

    window.addEventListener("devicemotion", function(e) {
      const acc = e.accelerationIncludingGravity;
      const strength = Math.abs(acc.x) + Math.abs(acc.y) + Math.abs(acc.z);
      if (strength > 30) fire();
    });
  </script>
</body>
</html>
