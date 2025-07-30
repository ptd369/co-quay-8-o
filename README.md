<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
  <title>Trò Chơi Súng Lục – Xoay Chuẩn + Màn Hình Ngang</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: url('assets/background.jpg') center center / cover no-repeat;
      font-family: 'Segoe UI', sans-serif;
      transform: rotate(90deg); /* Màn hình ngang trên điện thoại */
      transform-origin: center center;
      height: 100vw;
      width: 100vh;
    }
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }
    .container {
      text-align: center;
      width: 100vh;
      position: relative;
      z-index: 1;
    }
    .gun-image {
      width: 50vh;
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
      transition: transform 3s cubic-bezier(0.1, 0.9, 0.5, 1.5);
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
  </style>
</head>
<body>
  <div class="container">
    <img src="assets/gun.png" alt="Khẩu súng" class="gun-image" id="gun">
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
    const cylinder = document.getElementById('cylinderView');
    let chambers = Array(8).fill(false);
    let current = 0;
    let lastShake = 0;

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
      current = 0;
      cylinder.classList.add('spin');
      setTimeout(() => cylinder.classList.remove('spin'), 3000);
      playSound("sfx-spin");
      updateCylinder();
    }

    function rotateArray(arr, count) {
      return arr.slice(count).concat(arr.slice(0, count));
    }

    function fire() {
      if (!cylinder.style.display || cylinder.style.display === 'none') {
        const fired = chambers[current];
        if (fired) {
          chambers[current] = false;
          playSound("sfx-fire");
          showSmoke();
          showBullet();
          shakeGun();
        } else {
          playSound("sfx-click");
        }
        current = (current + 1) % 8;
        updateCylinder();
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
      if (strength > 25 && now - lastShake > 1200) {
        fire();
        lastShake = now;
      }
    });
  </script>
</body>
</html>
