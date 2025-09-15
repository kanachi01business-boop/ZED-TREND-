<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>My Telegram Mini App</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <style>
    body{font-family:system-ui,Segoe UI,Roboto; padding:18px;}
    button{padding:12px 18px;font-size:16px;border-radius:8px;}
  </style>
</head>
<body>
  <h2 id="greet">Hello!</h2>
  <p id="info">Waiting for Telegram...</p>
  <button id="sendBtn">Send data to bot</button>

  <script>
    const tg = window.Telegram?.WebApp;
    if(!tg){ document.getElementById('info').innerText = 'Open this inside Telegram to test the mini app.'; }
    else {
      tg.ready();
      const u = tg.initDataUnsafe?.user;
      document.getElementById('greet').innerText = u ? `Hi, ${u.first_name || 'friend'}!` : 'Hi!';
      document.getElementById('info').innerText = 'Tap "Send data to bot" to deliver a message to your bot (keyboard-launched apps only).';

      document.getElementById('sendBtn').addEventListener('click', () => {
        // sendData sends a string back to the bot as a service message:
        const payload = { fromMiniApp: true, time: Date.now() };
        tg.sendData(JSON.stringify(payload));   // bot receives it as service message (web_app_data)
        tg.close(); // optional: closes the mini app UI
      });
    }
  </script>
</body>
</html>
