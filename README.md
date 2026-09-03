<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Funny Monkey 🐒</title>

  <style>
    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: Arial, sans-serif;
      background:
        radial-gradient(circle at center, #00bfff 0%, #0066ff 35%, #001b5e 100%);
      color: white;
      padding-bottom: 70px;
    }

    .card {
      width: 90%;
      max-width: 500px;
      padding: 25px;
      text-align: center;
      background: rgba(0, 10, 40, 0.8);
      border: 2px solid #00eaff;
      border-radius: 25px;
      box-shadow:
        0 0 15px #00eaff,
        0 0 40px #008cff,
        0 0 80px #0055ff;
    }

    h1 {
      font-size: 32px;
      text-shadow:
        0 0 5px #00eaff,
        0 0 15px #00eaff,
        0 0 30px #008cff;
    }

    .monkey {
      width: 100%;
      max-width: 420px;
      border-radius: 20px;
      display: block;
      margin: 20px auto;
      box-shadow:
        0 0 10px #00eaff,
        0 0 25px #008cff;
    }

    #caption {
      font-size: 20px;
      font-weight: bold;
      min-height: 30px;
      text-shadow: 0 0 8px #00eaff;
    }

    button {
      border: 2px solid #00eaff;
      background: #006eff;
      color: white;
      padding: 14px 25px;
      border-radius: 30px;
      font-size: 17px;
      font-weight: bold;
      cursor: pointer;
      box-shadow:
        0 0 10px #00eaff,
        0 0 25px #008cff;
    }

    button:hover {
      background: #00c8ff;
      transform: scale(1.07);
    }

    /* Bottom marquee */
    .marquee {
      position: fixed;
      bottom: 0;
      left: 0;
      width: 100%;
      overflow: hidden;
      background: #00133d;
      border-top: 2px solid #00eaff;
      border-bottom: 2px solid #00eaff;
      box-shadow: 0 0 20px #00eaff;
      padding: 12px 0;
      white-space: nowrap;
    }

    .marquee span {
      display: inline-block;
      padding-left: 100%;
      font-size: 18px;
      font-weight: bold;
      color: #ffffff;
      text-shadow:
        0 0 5px #00eaff,
        0 0 15px #00eaff;
      animation: scroll 12s linear infinite;
    }

    @keyframes scroll {
      from {
        transform: translateX(0);
      }
      to {
        transform: translateX(-100%);
      }
    }
  </style>
</head>

<body>

  <div class="card">
    <h1>🐒 Funny Monkey!</h1>

    <img
      class="monkey"
      src="https://images.unsplash.com/photo-1540573133985-87b6da6d54a9?auto=format&fit=crop&w=800&q=80"
      alt="Funny monkey">

    <p id="caption">
      "When you hear someone say there are no bananas left..." 🍌
    </p>

    <button onclick="changeCaption()">
      Make Monkey Talk 😂
    </button>
  </div>

  <div class="marquee">
    <span>
      THIS WEB HAS BEEN CLOSED TO LET ADMIN TAKE CONTROL OF RESULTS 🚨
    </span>
  </div>

  <script>
    const captions = [
      '"When you hear someone say there are no bananas left..." 🍌',
      '"I definitely did NOT eat the last banana." 😇',
      '"Bro, why are you looking at me?" 👀',
      '"Monday again? Seriously?" 😭',
      '"I came here for bananas, not responsibilities." 😂',
      '"This is my serious face." 🐒'
    ];

    function changeCaption() {
      const random = Math.floor(Math.random() * captions.length);
      document.getElementById("caption").textContent = captions[random];
    }
  </script>

</body>
</html>
