<!-- Full updated HTML with shake sensitivity = 20 -->
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Súng Lục – Shake Fix</title>
  <!-- styles remain unchanged -->
  <style>/* ... giữ nguyên CSS từ phiên bản trước ... */</style>
</head>
<body>
  <!-- giữ nguyên HTML phần giao diện -->

  <!-- âm thanh -->
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
      console.log("Lắc điện thoại: ", strength);
      if (strength > 20 && now - lastShake > 800) {
        fire();
        lastShake = now;
      }
    });
  </script>
</body>
</html>
