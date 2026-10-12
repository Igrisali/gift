<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Sorry</title>
<style>
  html, body { margin:0; height:100%; }
  body {
    background: #ffe4ec;
    background: radial-gradient(circle at 50% 20%, #fff0f5 0%, #ffe4ec 60%, #ffd6e4 100%);
    font-family: Georgia, "Times New Roman", serif;
    overflow:hidden;
    position:relative;
  }
  svg.scene { position:absolute; inset:0; width:100%; height:100%; }
  .hint {
    position:absolute; top:6%; width:100%; text-align:center;
    color:#c2185b; font-size:1.1rem; letter-spacing:.05em;
  }
  .magic { cursor:pointer; transform-box:fill-box; transform-origin:center bottom; animation:float 2.4s ease-in-out infinite; }
  .magic:hover { filter:drop-shadow(0 0 14px #ff4f9a); }
  @keyframes float { 0%,100%{transform:translateY(0) scale(1)} 50%{transform:translateY(-6px) scale(1.06)} }

  #overlay {
    position:fixed; inset:0; display:none; align-items:center; justify-content:center;
    background:rgba(255,182,210,.55); backdrop-filter:blur(3px); z-index:10;
  }
  #overlay.show { display:flex; }
  .card {
    background:#fff7fa; border:3px solid #ff9ec4; border-radius:28px;
    padding:36px 48px; text-align:center; max-width:80vw;
    box-shadow:0 12px 40px rgba(194,24,91,.3);
    animation:pop .5s cubic-bezier(.2,1.4,.4,1);
  }
  @keyframes pop { from{transform:scale(.2) rotate(-8deg);opacity:0} to{transform:scale(1) rotate(0);opacity:1} }
  .card h1 { margin:0; font-size:clamp(2.5rem,10vw,4.5rem); color:#d81b60; }
  .card p { color:#ad1457; margin:10px 0 18px; font-size:1.1rem; }
  .card button {
    border:0; background:#ff80ab; color:#fff; padding:10px 24px; border-radius:20px;
    font-size:1rem; cursor:pointer;
  }
  .petal-fall { position:absolute; top:-30px; font-size:20px; animation:fall linear forwards; pointer-events:none; z-index:11; }
  @keyframes fall { to { transform:translateY(110vh) rotate(360deg); } }
</style>
</head>
<body>

<div class="hint">🌸 Click the glowing lotus 🌸</div>

<svg class="scene" viewBox="0 0 800 600" preserveAspectRatio="xMidYMid slice" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <!-- Lotus -->
    <symbol id="lotus" viewBox="-60 -60 120 90" overflow="visible">
      <g stroke="#e91e63" stroke-width="1.5">
        <ellipse cx="0" cy="-22" rx="11" ry="26" fill="#f8bbd0" transform="rotate(-70)"/>
        <ellipse cx="0" cy="-22" rx="11" ry="26" fill="#f8bbd0" transform="rotate(70)"/>
        <ellipse cx="0" cy="-22" rx="11" ry="28" fill="#f48fb1" transform="rotate(-40)"/>
        <ellipse cx="0" cy="-22" rx="11" ry="28" fill="#f48fb1" transform="rotate(40)"/>
        <ellipse cx="0" cy="-24" rx="12" ry="30" fill="#ff80ab" transform="rotate(-15)"/>
        <ellipse cx="0" cy="-24" rx="12" ry="30" fill="#ff80ab" transform="rotate(15)"/>
        <ellipse cx="0" cy="-26" rx="12" ry="32" fill="#ff4081"/>
      </g>
      <circle cx="0" cy="-4" r="6" fill="#ffd54f"/>
    </symbol>
    <!-- Strawberry -->
    <symbol id="berry" viewBox="-20 -30 40 55" overflow="visible">
      <path d="M0 22 C-22 8 -20 -14 0 -16 C20 -14 22 8 0 22Z" fill="#e53935" stroke="#b71c1c" stroke-width="1"/>
      <g fill="#ffeb3b">
        <circle cx="-8" cy="-4" r="1.3"/><circle cx="6" cy="-6" r="1.3"/><circle cx="-2" cy="2" r="1.3"/>
        <circle cx="9" cy="3" r="1.3"/><circle cx="-10" cy="8" r="1.3"/><circle cx="2" cy="11" r="1.3"/>
        <circle cx="-3" cy="-11" r="1.3"/><circle cx="8" cy="12" r="1.3"/>
      </g>
      <path d="M0 -16 L-10 -22 L-4 -15 L-12 -14 L-2 -13 L0 -6 L2 -13 L12 -14 L4 -15 L10 -22Z" fill="#43a047"/>
    </symbol>
  </defs>

  <!-- Mountains -->
  <polygon points="0,420 150,230 280,400 400,260 540,420 660,240 800,400 800,600 0,600" fill="#d1a3c4" opacity=".7"/>
  <polygon points="0,470 120,330 240,450 380,310 520,460 680,320 800,460 800,600 0,600" fill="#b57bb0" opacity=".85"/>
  <polygon points="150,230 128,262 150,252 170,266" fill="#fff"/>
  <polygon points="660,240 640,270 660,262 680,274" fill="#fff"/>
  <polygon points="400,260 382,288 400,280 418,290" fill="#fff"/>

  <!-- Pond -->
  <rect x="0" y="470" width="800" height="130" fill="#f8bbd0"/>
  <ellipse cx="400" cy="540" rx="380" ry="50" fill="#f48fb1" opacity=".45"/>

  <!-- Lily pads -->
  <ellipse cx="130" cy="545" rx="42" ry="12" fill="#81c784"/>
  <ellipse cx="670" cy="548" rx="42" ry="12" fill="#81c784"/>
  <ellipse cx="400" cy="570" rx="48" ry="13" fill="#81c784"/>

  <!-- Normal lotuses -->
  <use href="#lotus" x="70"  y="465" width="120" height="90"/>
  <use href="#lotus" x="620" y="468" width="120" height="90"/>

  <!-- Special clickable lotus -->
  <g class="magic" id="magicLotus">
    <use href="#lotus" x="320" y="480" width="160" height="120"/>
  </g>

  <!-- Strawberries -->
  <use href="#berry" x="60"  y="110" width="50" height="68"/>
  <use href="#berry" x="690" y="140" width="50" height="68"/>
  <use href="#berry" x="200" y="60"  width="40" height="55"/>
  <use href="#berry" x="560" y="70"  width="44" height="60"/>
  <use href="#berry" x="110" y="400" width="46" height="62"/>
  <use href="#berry" x="650" y="395" width="46" height="62"/>
  <use href="#berry" x="370" y="150" width="38" height="52"/>
</svg>

<div id="overlay">
  <div class="card">
    <h1>Sorry 🥺</h1>
    <p>🌸 🍓 🌸</p>
    <button id="closeBtn">Close</button>
  </div>
</div>

<script>
  const overlay = document.getElementById('overlay');
  function petals() {
    for (let i = 0; i < 25; i++) {
      const p = document.createElement('div');
      p.className = 'petal-fall';
      p.textContent = ['🌸','🍓','💗'][i % 3];
      p.style.left = Math.random() * 100 + 'vw';
      p.style.animationDuration = (3 + Math.random() * 3) + 's';
      p.style.animationDelay = (Math.random() * 1.5) + 's';
      document.body.appendChild(p);
      setTimeout(() => p.remove(), 8000);
    }
  }
  document.getElementById('magicLotus').addEventListener('click', () => {
    overlay.classList.add('show');
    petals();
  });
  document.getElementById('closeBtn').addEventListener('click', () => overlay.classList.remove('show'));
</script>
</body>
</html>
