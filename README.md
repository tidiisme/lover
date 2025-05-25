<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hiệu ứng tình yêu rơi</title>
  <style>
    body {
      margin: 0;
      background: linear-gradient(to bottom, #87CEEB, #E0F6FF);
      overflow: hidden;
      height: 100vh;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      position: relative;
    }
    .rain-container {
      position: relative;
      width: 100%;
      height: 100%;
      z-index: 1;
    }
    .cloud {
      position: absolute;
      opacity: 0.7;
      pointer-events: none;
      z-index: 0;
      animation: drift linear infinite;
    }
    .cloud-1 {
      width: 200px;
      top: 10%;
      left: 5%;
      animation-duration: 30s;
    }
    .cloud-2 {
      width: 150px;
      top: 20%;
      right: 10%;
      animation-duration: 40s;
      animation-direction: reverse;
    }
    .cloud-3 {
      width: 180px;
      top: 40%;
      left: 20%;
      animation-duration: 35s;
    }
    @keyframes drift {
      0% {
        transform: translateX(-20vw);
      }
      100% {
        transform: translateX(120vw);
      }
    }
    .char, .falling-image {
      position: absolute;
      user-select: none;
      opacity: 0.9;
      animation: fall linear infinite;
      z-index: 1;
    }
    .char {
      color: #ffffff;
      text-shadow: 0 0 8px #ff69b4;
      white-space: nowrap;
      font-size: 24px;
    }
    .falling-image {
      width: 60px;
      height: 60px;
    }
    @keyframes fall {
      0% {
        transform: translateY(-100%);
        opacity: 0.3;
      }
      50% {
        opacity: 1;
      }
      100% {
        transform: translateY(100vh);
        opacity: 0.1;
      }
    }
    audio {
      display: none;
    }
  </style>
</head>
<body>
  <audio autoplay loop>
    <source src="https://raw.githubusercontent.com/tidiisme/lover/main/1.mp3" type="audio/mpeg">
    Trình duyệt của bạn không hỗ trợ audio.
  </audio>
  <img src="https://cdn.pixabay.com/photo/2016/03/31/19/05/cloud-1294458_1280.png" class="cloud cloud-1" alt="cloud">
  <img src="https://cdn.pixabay.com/photo/2016/03/31/19/05/cloud-1294458_1280.png" class="cloud cloud-2" alt="cloud">
  <img src="https://cdn.pixabay.com/photo/2016/03/31/19/05/cloud-1294458_1280.png" class="cloud cloud-3" alt="cloud">
  <div class="rain-container" id="rain"></div>
  <script>
    const container = document.getElementById("rain");
    const phrases = ["Vũ Tú Mây", "25/10/2001", "❤️", "我爱你", "宝贝"];
    const imageUrls = [
      "https://cdn-icons-png.flaticon.com/512/833/833472.png"
    ];
    function createChar() {
      const charEl = document.createElement("div");
      charEl.classList.add("char");
      charEl.textContent = phrases[Math.floor(Math.random() * phrases.length)];
      charEl.style.left = Math.random() * (window.innerWidth - 100) + "px";
      charEl.style.animationDuration = (Math.random() * 3 + 3) + "s";
      charEl.style.fontSize = (Math.random() * 10 + 20) + "px";
      container.appendChild(charEl);
      setTimeout(() => {
        if (charEl.parentNode) {
          container.removeChild(charEl);
        }
      }, 6000);
    }
    function createImage() {
      const imgEl = document.createElement("img");
      imgEl.classList.add("falling-image");
      imgEl.src = imageUrls[0];
      imgEl.style.left = Math.random() * (window.innerWidth - 60) + "px";
      imgEl.style.animationDuration = (Math.random() * 3 + 4) + "s";
      container.appendChild(imgEl);
      setTimeout(() => {
        if (imgEl.parentNode) {
          container.removeChild(imgEl);
        }
      }, 7000);
    }
    setInterval(() => {
      for (let i = 0; i < 2; i++) {
        createChar();
      }
      if (Math.random() > 0.9) {
        createImage();
      }
    }, 200);
    window.addEventListener('resize', () => {
      container.style.width = window.innerWidth + 'px';
      container.style.height = window.innerHeight + 'px';
    });
  </script>
</body>
</html>
