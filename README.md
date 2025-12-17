<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Your Spirit Emoji ✨</title>

  <style>
    body {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #fdfbfb, #ebedee);
      font-family: Arial, sans-serif;
      margin: 0;
      text-align: center;
      overflow: hidden;
    }

    h1 {
      font-size: 28px;
      margin-bottom: 20px;
      opacity: 0;
      animation: fadeIn 1.2s forwards;
    }

    #emoji {
      font-size: 120px;
      opacity: 0;
      animation: popIn 0.8s ease-out forwards;
      animation-delay: 0.5s; /* Slightly faster feel */
    }

    @keyframes fadeIn {
      to { opacity: 1; }
    }

    @keyframes popIn {
      0% { transform: scale(0); opacity: 0; }
      70% { transform: scale(1.2); }
      100% { transform: scale(1); opacity: 1; }
    }
  </style>
</head>
<body>

  <h1>Your spirit emoji is…</h1>
  <div id="emoji"></div>

  <script>
    const emojis = [
      "😃","😆","😁","😉","😗","🤪","😏",
      "🙂‍↕️","🙂‍↔️","☹️","😭","😠",
      "🫣","🫡","🤔","🫢","🤫","🤥",
      "😮","🥱","🤮","🥳","😎","🤖","🌈"
    ];

    // 1. Check if the URL contains "?scan=true"
    const params = new URLSearchParams(window.location.search);
    const isNewScan = params.has("scan");

    // 2. Try to get a previously saved emoji
    let emoji = localStorage.getItem("spiritEmoji");

    // 3. Logic: If it's a new scan (from QR) OR no emoji exists yet, pick a new one
    if (isNewScan || !emoji) {
      emoji = emojis[Math.floor(Math.random() * emojis.length)];
      localStorage.setItem("spiritEmoji", emoji);
      
      // 4. Clean the URL: Removes "?scan=true" from the address bar 
      // so that hitting 'Refresh' doesn't generate a new emoji again.
      if (isNewScan) {
        const cleanURL = window.location.protocol + "//" + window.location.host + window.location.pathname;
        window.history.replaceState({}, document.title, cleanURL);
      }
    }

    // 5. Display the emoji
    document.getElementById("emoji").textContent = emoji;
  </script>

</body>

</html>
