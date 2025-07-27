<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Ổ Quay Súng – Mô phỏng đơn giản</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #1c1c1c;
      color: white;
      text-align: center;
      padding: 30px;
    }
    h1 {
      color: #ff5252;
    }
    #revolver {
      margin: 40px auto;
      position: relative;
      width: 200px;
      height: 200px;
    }
    .chamber {
      width: 40px;
      height: 40px;
      background: #333;
      border: 2px solid #aaa;
      border-radius: 50%;
      position: absolute;
      transform-origin: center center;
    }
    .loaded {
      background: red;
    }
    .fire-position {
      width: 50px;
      height: 50px;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 50%;
      position: absolute;
      top: 75px;
      left: 75px;
      border: 2px dashed #fff;
    }
    button {
      padding: 10px 20px;
      margin: 10px;
      font-weight: bold;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .log {
      margin-top: 20px;
      background: #222;
      padding: 10px;
      border-radius: 5px;
      height: 120px;
      overflow-y: auto;
    }
  </style>
</head>
<body>
  <h1>🔫 Mô phỏng ổ quay – 8 lỗ</h1>
  <div id="revolver">
    <div class="fire-position"></div>
  </div>

  <button onclick="loadBullet()">🔄 Nạp đạn</button>
  <button onclick="spinCylinder()">🌀 Xoay ổ</button>
  <button onclick="fire()">🔥 Bóp cò</button>

  <div class="log" id="log"></div>

  <script>
    const revolver = document.getElementById("revolver");
    const logBox = document.getElementById("log");
    const chambers = [];
    const total = 8;
    let current = 0;

    function createChambers() {
      revolver.querySelectorAll(".chamber").forEach(e => e.remove());
      for (let i = 0; i < total; i++) {
        const angle = (360 / total) * i;
        const div = document.createElement("div");
        div.className = "chamber";
        div.style.top = 80 + 70 * Math.sin((angle * Math.PI) / 180) + "px";
        div.style.left = 80 + 70 * Math.cos((angle * Math.PI) / 180) + "px";
        chambers[i] = false;
        revolver.appendChild(div);
      }
      updateChambers();
    }

    function updateChambers() {
      const all = revolver.querySelectorAll(".chamber");
      all.forEach((div, i) => {
        div.classList.toggle("loaded", chambers[i]);
      });
    }

    function loadBullet() {
      const empty = chambers.map((v, i) => (!v ? i : -1)).filter(i => i !== -1);
      if (empty.length === 0) return log("❗Ổ đã đầy!");
      const randomIndex = empty[Math.floor(Math.random() * empty.length)];
      chambers[randomIndex] = true;
      updateChambers();
      log(`🔫 Nạp đạn vào ổ số ${randomIndex + 1}`);
    }

    function spinCylinder() {
      current = Math.floor(Math.random() * total);
      log("🌀 Đã xoay ổ quay.");
    }

    function fire() {
      const result = chambers[current];
      if (result) {
        log("💥 BANG! Trúng đạn!");
        chambers[current] = false; // bóp xong trúng thì hết đạn
      } else {
        log("✅ Click! Không có đạn.");
      }
      current = (current + 1) % total;
      updateChambers();
    }

    function log(msg) {
      logBox.innerHTML += `> ${msg}<br>`;
      logBox.scrollTop = logBox.scrollHeight;
    }

    createChambers();
  </script>
</body>
</html>
