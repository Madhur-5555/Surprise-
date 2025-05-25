<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Surprise for Khushi</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: #000;
      color: white;
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding-top: 50px;
    }

    #heart-container, #fireworks {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 1;
    }

    .heart {
      position: absolute;
      font-size: 24px;
      animation: fall 3s linear forwards;
      user-select: none;
    }

    @keyframes fall {
      0% { transform: translateY(0); opacity: 1; }
      100% { transform: translateY(100vh); opacity: 0; }
    }

    #surprise-content {
      position: relative;
      z-index: 2;
      margin-top: 50px;
      display: none;
    }

    #message {
      font-size: 20px;
      margin: 20px auto;
      max-width: 600px;
      white-space: pre-wrap;
      min-height: 150px;
    }

    button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 18px;
      background: gold;
      color: black;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    #gift-box {
      display: none;
      animation: pop 1s ease;
      margin-top: 20px;
    }

    @keyframes pop {
      0% { transform: scale(0.5); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    .slideshow {
      max-width: 300px;
      margin: 20px auto;
      border-radius: 12px;
      box-shadow: 0 0 10px gold;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 1;
      pointer-events: none;
    }

    audio {
      display: none;
    }
  </style>
</head>
<body>

  <!-- Background Music -->
  <audio id="bg-music" loop>
    <source src="https://dl.sndup.net/8cbq/music-khushi.mp3" type="audio/mpeg">
  </audio>

  <div id="heart-container"></div>
  <canvas id="fireworks"></canvas>

  <div id="surprise-content">
    <h1>Hey Khushi!</h1>
    <div id="message"></div>
    <button onclick="playMusic()">Play Music</button>
    <button onclick="revealGift()">Click to See Your Smile</button>

    <div id="gift-box">
      <img class="slideshow" src="https://i.imgur.com/F3KVuYA.jpg" alt="Khushi Surprise Image" />
    </div>
  </div>

  <script>
    // Hearts animation
    function createHeart() {
      const heart = document.createElement("div");
      heart.classList.add("heart");
      heart.textContent = "❤️";
      heart.style.left = Math.random() * window.innerWidth + "px";
      heart.style.top = "-20px";
      document.getElementById("heart-container").appendChild(heart);
      setTimeout(() => heart.remove(), 3000);
    }

    let heartInterval = setInterval(createHeart, 150);

    // Show message and content after hearts
    setTimeout(() => {
      clearInterval(heartInterval);
      document.getElementById("surprise-content").style.display = "block";
      typeMessage();
    }, 4000);

    // Typewriter effect
    const msg = `Tere jaise dost ho toh zindagi mein har din special lagta hai.
Na tu bhai hai, na behen, par tu hai meri sabse khaas friend.
Teri yaari hi meri smile ki wajah hai!

Stay happy and awesome always!`;
    let index = 0;

    function typeMessage() {
      const messageEl = document.getElementById("message");
      const typing = setInterval(() => {
        if (index < msg.length) {
          messageEl.textContent += msg[index++];
        } else {
          clearInterval(typing);
        }
      }, 50);
    }

    // Music play
    function playMusic() {
      const music = document.getElementById("bg-music");
      music.play();
    }

    // Reveal gift and launch fireworks
    function revealGift() {
      document.getElementById("gift-box").style.display = "block";
      launchFireworks();
    }

    // Fireworks Canvas
    const canvas = document.getElementById('fireworks');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const fireworks = [];

    function launchFireworks() {
      setInterval(() => {
        const x = Math.random() * canvas.width;
        const y = Math.random() * canvas.height / 2;
        for (let i = 0; i < 100; i++) {
          fireworks.push({
            x, y,
            radius: Math.random() * 2,
            dx: (Math.random() - 0.5) * 5,
            dy: (Math.random() - 0.5) * 5,
            alpha: 1
          });
        }
      }, 600);
    }

    function drawFireworks() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      fireworks.forEach((f, index) => {
        f.x += f.dx;
        f.y += f.dy;
        f.alpha -= 0.01;
        ctx.beginPath();
        ctx.arc(f.x, f.y, f.radius, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(255, ${Math.random()*255}, ${Math.random()*255}, ${f.alpha})`;
        ctx.fill();
        if (f.alpha <= 0) fireworks.splice(index, 1);
      });
      requestAnimationFrame(drawFireworks);
    }
    drawFireworks();
  </script>

</body>
</html>
