<!DOCTYPE html>
<html lang="vi">
<head><meta charset="UTF‑8"><meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Súng Lục Revolver – Logic Chuẩn</title>
  <style>/*... giữ nguyên CSS từ bản trước ...*/</style>
</head>
<body>
  <div id="startScreen">Chạm để bắt đầu</div>
  <div id="gameContainer">
    <img id="gun" src="assets/gun.png">
    <button onclick="spinCylinder()">🌀 Xoay ổ</button>
    <button onclick="toggleCylinderView()">🔄 Nạp đạn</button>
  </div>
  <div id="cylinderView"></div>
  <audio id="sfx-load" src="assets/reload.mp3"></audio>
  <audio id="sfx-spin" src="assets/spin.mp3"></audio>
  <audio id="sfx-fire" src="assets/gunshot.mp3"></audio>
  <audio id="sfx-click" src="assets/click.mp3"></audio>
  <script>
    let chambers = Array(8).fill(false);
    let current = 0, lastShake = 0;
    const spinAudio = document.getElementById('sfx-spin');

    function spinCylinder() {
      const shift = Math.floor(Math.random()*8);
      chambers = chambers.slice(shift).concat(chambers.slice(0, shift));
      document.getElementById('cylinderView').classList.add('spinning');
      spinAudio.currentTime = 0;
      spinAudio.play();
      spinAudio.onended = () => document.getElementById('cylinderView').classList.remove('spinning');
      updateCylinder();
    }

    function fire() {
      if (document.getElementById('cylinderView').style.display === 'block') return;
      if (chambers[current]) {
        chambers[current] = false;
        playSound('sfx-fire');
        showSmoke(); showBullet();
      } else playSound('sfx-click');
      current = (current + 1) % 8;
      updateCylinder();
    }

    window.addEventListener('devicemotion', e => {
      const acc = e.accelerationIncludingGravity;
      const strength = Math.abs(acc.x)+Math.abs(acc.y)+Math.abs(acc.z);
      const now = Date.now();
      if (strength > 25 && now - lastShake > 800) { fire(); lastShake = now; }
    });

    // Các hàm còn lại như playSound, updateCylinder, showSmoke, showBullet giữ nguyên như bản trước
  </script>
</body>
</html>

