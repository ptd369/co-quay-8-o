<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ổ Quay Súng – Mô phỏng đẹp & mobile</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom, #2d2d2d, #1a1a1a);
      color: #fefefe;
      text-align: center;
      padding: 20px;
    }
    h1 {
      color: #ff5252;
      margin-bottom: 10px;
    }
    #revolver {
      margin: 30px auto;
      position: relative;
      width: 240px;
      height: 240px;
      background: radial-gradient(circle at center, #3a3a3a, #111);
      border-radius: 50%;
      box-shadow: inset 0 0 30px #000;
    }
    .chamber {
      width: 48px;
      height: 48px;
      background: #444;
      border: 3px solid #aaa;
      border-radius: 50%;
      position: absolute;
      transform-origin: center center;
      transition: background 0.3s;
    }
    .loaded {
      background: red;
      box-shadow: 0 0 8px #ff0000;
    }
    .fire-position {
      width: 60px;
      height: 60px;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 50%;
      position: absolute;
      top: 90px;
      left: 90px;
      border: 2px dashed #fff;
    }
    button {
      padding: 12px 24px;
      margin: 10px;
      font-weight: bold;
      font-size: 1rem;
      background: #ff5252;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background 0.2s;
    }
    button:hover {
      background: #ff7373;
    }
    .log {
      margin-top: 20px;
      background: #222;
      padding: 12px;
      border-radius: 6px;
      height: 140px;
      overflow-y: auto;
      font-size: 0.95rem;
      width: 90%;
      max-width: 500px;
      margin-left: auto;
      margin-right: auto;
      box-shadow: inset 0 0 5px #000;
    }
    @media (max-width: 500px) {
      #revolver {
        width: 180px;
        height: 180px;
      }
      .chamber {
        width: 36px;
        height: 36px;
      }
      .fire-position {
        width: 48px;
        height: 48px;
        top: 66px;
        left: 66px;
      }
    }
  </style>
</head>
<body>
  <h1>🔫 Ổ Quay Súng (8 lỗ)</h1>
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
        const radius = 80;
        div.style.top = 90 + radius * Math.sin((angle * Math.PI) / 180) + "px";
        div.style.left = 90 + radius * Math.cos((angle * Math.PI) / 180) + "px";
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
        chambers[current] = false;
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
