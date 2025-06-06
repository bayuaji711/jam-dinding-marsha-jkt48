<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>Jam Dinding Marsha JKT48</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Sacramento&family=Poppins:wght@600&display=swap');
    body {
      background: linear-gradient(135deg, #fcd5ce, #f8edeb);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      font-family: 'Poppins', sans-serif;
      user-select: none;
    }
    .clock {
      position: relative;
      width: 340px;
      height: 340px;
      background: radial-gradient(circle, #fff9f9, #f8d7da);
      border: 14px solid #f67280;
      border-radius: 50%;
      box-shadow: 0 0 25px rgba(246, 114, 128, 0.7);
    }
    .number {
      position: absolute;
      width: 38px;
      height: 38px;
      text-align: center;
      font-weight: 700;
      font-size: 20px;
      color: #a62d41;
      transform: translate(-50%, -50%);
      font-family: 'Sacramento', cursive;
      text-shadow: 1px 1px 2px #f6b6bd;
    }
    .hand {
      position: absolute;
      bottom: 50%;
      left: 50%;
      transform-origin: bottom center;
      border-radius: 7px;
      cursor: grab;
      transition: transform 0.1s ease-out;
      box-shadow: 0 0 6px rgba(166, 45, 65, 0.8);
    }
    .hour {
      width: 12px;
      height: 85px;
      background: #a62d41;
    }
    .minute {
      width: 7px;
      height: 125px;
      background: #f67280;
    }
    .center-dot {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 20px;
      height: 20px;
      background: #fff;
      border: 4px solid #a62d41;
      border-radius: 50%;
      transform: translate(-50%, -50%);
      z-index: 10;
      box-shadow: 0 0 10px #f67280;
    }
    .logo {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, 140%);
      font-size: 28px;
      font-weight: 700;
      color: #a62d41;
      text-shadow: 2px 2px 6px #f6b6bd;
      font-family: 'Sacramento', cursive;
      letter-spacing: 3px;
    }
  </style>
</head>
<body>
  <div class="clock" id="clock">
    <div class="hand hour" id="hour"></div>
    <div class="hand minute" id="minute"></div>
    <div class="center-dot"></div>
    <div class="logo">Marsha</div>
  </div>

  <script>
    const clock = document.getElementById("clock");

    // Buat angka 1 sampai 12 dengan posisi melingkar
    for (let i = 1; i <= 12; i++) {
      const angle = (i - 3) * 30 * Math.PI / 180;
      const x = 170 + 130 * Math.cos(angle);
      const y = 170 + 130 * Math.sin(angle);
      const num = document.createElement("div");
      num.className = "number";
      num.style.left = x + "px";
      num.style.top = y + "px";
      num.textContent = i;
      clock.appendChild(num);
    }

    // Fungsi supaya jarum bisa digeser bebas
    function enableDrag(hand) {
      let isDragging = false;

      hand.addEventListener("mousedown", (e) => {
        isDragging = true;
        e.preventDefault();
      });

      document.addEventListener("mousemove", (e) => {
        if (isDragging) {
          const rect = clock.getBoundingClientRect();
          const cx = rect.left + rect.width / 2;
          const cy = rect.top + rect.height / 2;
          const angle = Math.atan2(e.clientY - cy, e.clientX - cx) * 180 / Math.PI;
          const deg = (angle + 90 + 360) % 360;
          hand.style.transform = `rotate(${deg}deg)`;
        }
      });

      document.addEventListener("mouseup", () => {
        isDragging = false;
      });
    }

    enableDrag(document.getElementById("hour"));
    enableDrag(document.getElementById("minute"));
  </script>
</body>
</html>
