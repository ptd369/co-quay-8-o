<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Súng Lục Cò Quay</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', sans-serif;
      overflow: hidden;
      background: black;
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
    }
    .cylinder-view.spinning {
      animation: spinEffect 3s ease-out;
    }
    @keyframes spinEffect {
      0% { transform: translate(-50%, -50%) rotate(0deg); }
      100% { transform: translate(-50%, -50%) rotate(1440deg); }
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
    .smoke {
      position: absolute;
      width: 80px;
      height: 80px;
      background: url('assets/smoke.png') center center / contain no-repeat;
      opacity: 0;
      animation: puff 0.5s ease-out forwards;
    }
    .bullet {
      position: absolute;
      width: 20px;
      height: 10px;
      background: gold;
      border-radius: 5px;
      animation: fly 0.5s ease-out forwards;
    }
    @keyframes puff {
      0% { transform: scale(0.5); opacity: 1; }
      100% { transform: scale(1.5); opacity: 0; }
    }
    @keyframes fly {
      0% { left: 50%; top: 50%; transform: translate(-50%, -50%) scale(1); }
      100% { left: 100vw; top: 40%; transform: translate(-50%, -50%) scale(1.2); }
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

    function fire() {
      if (cylinder.style.display !== 'block') {
        const fired = chambers[current];
        if (fired) {
          chambers[current] = false;
          playSound("sfx-fire");
          showSmoke();
          showBullet();
        } else {
          playSound("sfx-click");
        }
        current = (current + 1) % 8;
        updateCylinder();
      }
    }

    function spinCylinder() {
      const shift = Math.floor(Math.random() * 8);
      chambers = rotateArray(chambers, shift);
      current = shift;
      cylinder.classList.add('spinning');
      playSound("sfx-spin");
      spinAudio.onended = () => {
        cylinder.classList.remove('spinning');
      };
      updateCylinder();
    }

    function rotateArray(arr, count) {
      return arr.slice(count).concat(arr.slice(0, count));
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
      if (strength > 15 && now - lastShake > 800) {
        fire();
        lastShake = now;
      }
    });
  </script>
</body>
</html>
