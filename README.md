<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Súng Lục – Chạm Để Bắt Đầu</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: black;
      font-family: 'Segoe UI', sans-serif;
    }
    body.landscape {
      background: url('assets/background.jpg') center center / cover no-repeat;
    }
    .start-screen {
      position: fixed;
      inset: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      background: black;
      color: white;
      font-size: 24px;
      z-index: 9999;
    }
    .container {
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      width: 100vw;
      text-align: center;
      position: relative;
    }
    .gun-image {
      width: 60vw;
      max-width: 400px;
      transition: transform 0.1s ease;
    }
    .controls {
      margin-top: 12px;
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
      transition: transform 3s ease-out;
    }
    .cylinder-view.spin {
      transform: translate(-50%, -50%) rotate(1440deg);
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
    @media screen and (orientation: portrait) {
      body.landscape::before {
        content: 'Vui lòng xoay ngang màn hình để chơi';
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: rgba(0,0,0,0.85);
        color: white;
        padding: 20px;
        font-size: 18px;
        border-radius: 10px;
        z-index: 10000;
      }
    }
  </style>
</head>
<body>
  <div class="start-screen" id="startScreen">Chạm để bắt đầu</div>
  <div class="container" id="gameContainer">
    <img src="assets/gun.png" class="gun-image" id="gun">
    <div class="controls">
      <button onclick="spinCylinder()">🌀 Xoay ổ</button>
      <button onclick="toggleCylinderView()">🔄 Nạp đạn</button>
    </div>
  </div>

  <div class="cylinder-view" id="cylinderView"></div>

  <audio id="sfx-load" src="assets/reload.mp3"></audio>
  <audio id="sfx-spin" src="assets/spin.mp3"></audio>
  <audio id="sfx-fire" src="assets/gunshot.mp3"></audio>
  <audio id="sfx-click" src="assets/click.mp3"></audio>

  <script>
    const gun = document.getElementById('gun');
    const container = document.getElementById('gameContainer');
    const startScreen = document.getElementById('startScreen');
    const cylinder = document.getElementById('cylinderView');
    const spinAudio = document.getElementById('sfx-spin');
    let chambers = Array(8).fill(false);
    let current = 0;
    let lastShake = 0;

    window.onload = () => {
      ['sfx-load','sfx-spin','sfx-fire','sfx-click'].forEach(id => {
        document.getElementById(id).load();
      });
    }

    startScreen.addEventListener('click', () => {
      startScreen.style.display = 'none';
      container.style.display = 'flex';
      document.body.classList.add('landscape');
    });

    function playSound(id) {
      const audio = document.getElementById(id);
      if (audio) {
        audio.currentTime = 0;
        audio.play();
      }
    }

    function spinCylinder() {
      const shift = Math.floor(Math.random() * 8);
      chambers = rotateArray(chambers, shift);
      current = shift;
      cylinder.classList.add('spin');
      playSound("sfx-spin");
      spinAudio.onended = () => {
        cylinder.classList.remove('spin');
      };
      updateCylinder();
    }

    function rotateArray(arr, count) {
      return arr.slice(count).concat(arr.slice(0, count));
    }

    function fire() {
      if (cylinder.style.display !== 'block') {
        const fired = chambers[current];
        if (fired) {
          chambers[current] = false;
          playSound("sfx-fire");
        } else {
          playSound("sfx-click");
        }
        current = (current + 1) % 8;
        updateCylinder();
      }
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
        div.onclick = () => {
          const wasLoaded = chambers[i];
          chambers[i] = !chambers[i];
          if (!wasLoaded && chambers[i]) playSound("sfx-load");
          updateCylinder();
        };
        cylinder.appendChild(div);
      }
    }

    window.addEventListener("devicemotion", function(e) {
      const acc = e.accelerationIncludingGravity;
      const strength = Math.abs(acc.x) + Math.abs(acc.y) + Math.abs(acc.z);
      const now = Date.now();
      if (strength > 25 && now - lastShake > 1000) {
        fire();
        lastShake = now;
      }
    });
  </script>
</body>
</html>
