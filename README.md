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

    #surprise-content {
      margin-top: 50px;
      display: none;
    }

    .sparkle {
      position: absolute;
      width: 5px;
      height: 5px;
      background: gold;
      border-radius: 50%;
      animation: fall 2s linear forwards;
    }

    @keyframes fall {
      0% { transform: translateY(0); opacity: 1; }
      100% { transform: translateY(100vh); opacity: 0; }
    }

    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 18px;
      background: gold;
      color: black;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    #gift-box {
      margin-top: 30px;
      display: none;
      animation: pop 1s ease;
    }

    @keyframes pop {
      0% { transform: scale(0.5); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    img {
      max-width: 300px;
      margin-top: 20px;
      border-radius: 12px;
      box-shadow: 0 0 10px gold;
    }

    audio {
      display: none;
    }
  </style>
</head>
<body>

  <audio autoplay loop>
    <source src="https://www.youtube.com/embed/0pWsCiBvLOk" type="audio/mpeg">
  </audio>

  <div id="sparkle-container"></div>

  <div id="surprise-content">
    <h1>Hey Khushi!</h1>
    <p style="white-space: pre-wrap;">
Tere jaise dost ho toh zindagi mein har din special lagta hai.
Na tu bhai hai, na behen, par tu hai meri sabse khaas friend.
Teri yaari hi meri smile ki wajah hai!

Stay happy and awesome always!
    </p>
    <button onclick="revealGift()">Click to See Your Smile</button>
    
    <div id="gift-box">
      <img src="file-3wuZ6f6qpG1PdsVshzVWmU" alt="Khushi Surprise Image" />
    </div>
  </div>

  <script>
    function createSparkle() {
      const sparkle = document.createElement("div");
      sparkle.classList.add("sparkle");
      sparkle.style.left = Math.random() * window.innerWidth + "px";
      document.getElementById("sparkle-container").appendChild(sparkle);
      setTimeout(() => sparkle.remove(), 2000);
    }

    let interval = setInterval(createSparkle, 100);
    setTimeout(() => {
      clearInterval(interval);
      document.getElementById("surprise-content").style.display = "block";
    }, 3000);

    function revealGift() {
      document.getElementById("gift-box").style.display = "block";
    }
  </script>

</body>
</html>
