<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<title>Glass Overlay</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
<style>
  /* THE IMPORTANT PART: no background color anywhere, so the host
     (OBS Browser Source, an Electron transparent window, etc.) can
     actually punch through to whatever sits underneath it. */
  html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    background: transparent;
    font-family: 'Space Grotesk', sans-serif;
    overflow: hidden;
  }

  /* Glass panel — the blur only does anything when there's real
     transparency behind it (a game capture, desktop, video, etc). */
  .glass {
    position: absolute;
    background: rgba(255, 255, 255, 0.08);
    backdrop-filter: blur(16px) saturate(140%);
    -webkit-backdrop-filter: blur(16px) saturate(140%);
    border: 1px solid rgba(255, 255, 255, 0.25);
    border-radius: 16px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.25);
    color: #fff;
    text-shadow: 0 1px 4px rgba(0, 0, 0, 0.4);
  }

  /* --- Example widget 1: a clock --- */
  #clockWidget {
    top: 24px;
    right: 24px;
    padding: 14px 20px;
    text-align: right;
  }
  #clockTime {
    font-family: 'JetBrains Mono', monospace;
    font-size: 28px;
    font-weight: 500;
    letter-spacing: 1px;
  }
  #clockDate {
    font-size: 11px;
    opacity: 0.75;
    margin-top: 2px;
  }

  /* --- Example widget 2: a label / caption bar --- */
  #labelWidget {
    bottom: 24px;
    left: 24px;
    padding: 10px 18px;
    font-size: 13px;
    letter-spacing: 0.5px;
  }
  #labelWidget b { font-weight: 700; }
</style>
</head>
<body>

  <div class="glass" id="clockWidget">
    <div id="clockTime">--:--</div>
    <div id="clockDate"></div>
  </div>

  <div class="glass" id="labelWidget">
    <b>● LIVE</b> — edit or delete this widget, it's just an example
  </div>

  <script>
    function tick() {
      const d = new Date();
      document.getElementById('clockTime').textContent =
        d.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', second: '2-digit' });
      document.getElementById('clockDate').textContent =
        d.toLocaleDateString([], { weekday: 'long', month: 'short', day: 'numeric' });
    }
    tick();
    setInterval(tick, 1000);
  </script>

</body>
</html>
