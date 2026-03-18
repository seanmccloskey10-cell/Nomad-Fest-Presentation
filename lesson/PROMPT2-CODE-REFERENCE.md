# Prompt 2 — Code Reference

This file contains pre-tested, working code for every complex component in the Prompt 2 transformation.
Claude should read this file and use these exact implementations rather than writing them from scratch.
This eliminates the two biggest time/bug risks: the pong game and the marquee.

---

## GOOGLE FONTS — paste in `<head>` before `<style>`

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
```

CSS variables to add to `:root`:
```css
--font-display: 'Barlow Condensed', sans-serif;
--font-body:    'Inter', sans-serif;
```

Apply to headings: `font-family: var(--font-display); font-weight: 700; text-transform: uppercase;`
Apply to body/p/li: `font-family: var(--font-body);`

---

## ANIMATED GRADIENT HERO BACKGROUND

Apply directly to `.hero` — no extra elements needed:

```css
.hero {
  background: linear-gradient(-45deg, #f4511e, #f9a825, #e91e8c, #9c27b0, #0ea5e9, #f4511e);
  background-size: 500% 500%;
  animation: gradient-shift 35s ease infinite;
}

@keyframes gradient-shift {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

Color story: coral-orange → amber-gold → hot pink → deep purple → ocean blue → back. Each colour shares hues with its neighbour — no jarring jumps.

---

## PONG GAME — complete working implementation

### HTML (goes inside the game card, replacing whatever game HTML exists)

```html
<div class="game-card-hero">
  <div class="game-header">
    <div class="game-title">🏓 Rally Challenge</div>
    <div class="round-pips">
      <div class="pip" id="pip1"></div>
      <div class="pip" id="pip2"></div>
      <div class="pip" id="pip3"></div>
      <div class="pip" id="pip4"></div>
      <div class="pip" id="pip5"></div>
    </div>
  </div>
  <div class="court" id="court">
    <canvas id="gameCanvas"></canvas>
  </div>
  <div class="game-status" id="gameStatus"></div>
  <div class="results-row" id="resultsRow">
    <div class="res-block">
      <div class="res-num" id="resScore">—</div>
      <div class="res-label">Rallies Hit</div>
    </div>
    <div class="res-block">
      <div class="res-rating" id="resRating"></div>
    </div>
  </div>
  <div class="game-controls">
    <button class="btn btn-white"  id="playBtn"  onclick="startRally()">▶ Play</button>
    <button class="btn btn-ghost"  id="againBtn" onclick="resetRally()" style="display:none">↺ Again</button>
    <a href="#join" class="btn btn-primary">Join the Club →</a>
  </div>
</div>
```

### CSS (for the game card and court)

```css
.game-card-hero {
  background: rgba(255,255,255,0.18);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255,255,255,0.35);
  border-radius: 20px;
  padding: 24px 28px;
  box-shadow: 0 32px 80px rgba(0,0,0,0.25), inset 0 1px 0 rgba(255,255,255,0.4);
}
.game-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 16px; }
.game-title { font-size: 12px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; color: rgba(255,255,255,0.9); }
.round-pips { display: flex; gap: 8px; }
.pip { width: 28px; height: 6px; border-radius: 3px; background: rgba(255,255,255,0.25); transition: background 0.3s; }
.pip.hit  { background: #fff; }
.pip.miss { background: rgba(255,80,50,0.8); }
.court { width: 100%; height: 200px; border-radius: 12px; overflow: hidden; margin-bottom: 14px; cursor: none; user-select: none; }
#gameCanvas { width: 100%; height: 100%; display: block; border-radius: 12px; }
.game-status { font-size: 13px; color: rgba(255,255,255,0.7); text-align: center; min-height: 18px; margin-bottom: 14px; }
.game-status.good    { color: #fff; font-weight: 700; }
.game-status.warning { color: rgba(255,180,100,0.9); font-weight: 700; }
.results-row { display: none; align-items: center; justify-content: center; gap: 32px; padding: 12px 0; margin-bottom: 14px; }
.results-row.show { display: flex; }
.res-num   { font-family: var(--font-display, sans-serif); font-size: 40px; font-weight: 700; color: #fff; line-height: 1; }
.res-label { font-size: 11px; color: rgba(255,255,255,0.6); text-transform: uppercase; letter-spacing: 0.08em; margin-top: 4px; }
.res-block { text-align: center; }
.res-rating { font-size: 18px; font-weight: 700; color: #fff; }
.game-controls { display: flex; gap: 10px; justify-content: center; }
```

### JavaScript (complete — paste inside `<script>` tag)

```js
// ── CANVAS PONG ──
const canvas     = document.getElementById('gameCanvas');
const ctx        = canvas.getContext('2d');
const courtDiv   = document.getElementById('court');
const gameStatus = document.getElementById('gameStatus');
const playBtn    = document.getElementById('playBtn');
const againBtn   = document.getElementById('againBtn');
const resultsRow = document.getElementById('resultsRow');

let W, H;
const PADDLE_W = 12, PADDLE_H = 64, BALL_R = 9;
const BASE_SPEED = 7;

let running = false, animId = null;
let ballX, ballY, ballDX, ballDY;
let playerY, aiY;
let score = 0;
let mouseY = 0;
let flashTimer = 0, flashColor = '';

function resize() {
  W = courtDiv.offsetWidth; H = courtDiv.offsetHeight;
  canvas.width = W; canvas.height = H;
  playerY = H / 2 - PADDLE_H / 2;
  aiY     = H / 2 - PADDLE_H / 2;
}

function setStatus(msg, cls) {
  gameStatus.textContent = msg;
  gameStatus.className = 'game-status' + (cls ? ' ' + cls : '');
}

function setPip(n, state) {
  const pip = document.getElementById('pip' + n);
  if (pip) pip.className = 'pip' + (state ? ' ' + state : '');
}

courtDiv.addEventListener('mousemove', function(e) {
  const rect = courtDiv.getBoundingClientRect();
  mouseY = e.clientY - rect.top - PADDLE_H / 2;
});

function launch() {
  const angle = (Math.random() * 0.6 - 0.3);
  const spd = BASE_SPEED + score * 0.4;
  ballX = W / 2; ballY = H / 2;
  ballDX = spd * (Math.random() > 0.5 ? 1 : -1);
  ballDY = spd * Math.sin(angle);
}

function startRally() {
  resize();
  playBtn.style.display  = 'none';
  againBtn.style.display = 'none';
  resultsRow.classList.remove('show');
  score = 0;
  [1,2,3,4,5].forEach(n => setPip(n, ''));
  setStatus('Move your mouse to control the paddle →', '');
  running = true; launch(); loop();
}

function loop() { animId = requestAnimationFrame(loop); update(); draw(); }

function update() {
  if (!running) return;
  playerY = Math.max(0, Math.min(H - PADDLE_H, mouseY));
  const aiCenter = aiY + PADDLE_H / 2;
  const aiSpeed = 5;
  if (ballY > aiCenter + 6) aiY = Math.min(H - PADDLE_H, aiY + aiSpeed);
  if (ballY < aiCenter - 6) aiY = Math.max(0, aiY - aiSpeed);
  ballX += ballDX; ballY += ballDY;
  if (ballY - BALL_R < 0) { ballY = BALL_R; ballDY = Math.abs(ballDY); }
  if (ballY + BALL_R > H) { ballY = H - BALL_R; ballDY = -Math.abs(ballDY); }
  const px = W - PADDLE_W - 14;
  if (ballDX > 0 && ballX + BALL_R >= px && ballX + BALL_R <= px + PADDLE_W + 8 &&
      ballY >= playerY - 4 && ballY <= playerY + PADDLE_H + 4) {
    ballX = px - BALL_R;
    ballDX = -Math.abs(ballDX) * 1.06;
    const offset = (ballY - (playerY + PADDLE_H / 2)) / (PADDLE_H / 2);
    ballDY = offset * Math.abs(ballDX) * 0.85;
    score++;
    if (score <= 5) setPip(score, 'hit');
    flashTimer = 8; flashColor = '#ffffff';
    setStatus('Rally ' + score + (score >= 5 ? ' 🔥' : ''), 'good');
    if (score >= 10) { endGame(); return; }
  }
  const ax = 14;
  if (ballDX < 0 && ballX - BALL_R <= ax + PADDLE_W && ballX - BALL_R >= ax - 8 &&
      ballY >= aiY - 4 && ballY <= aiY + PADDLE_H + 4) {
    ballX = ax + PADDLE_W + BALL_R; ballDX = Math.abs(ballDX);
  }
  if (ballX - BALL_R < 0) { ballX = BALL_R; ballDX = Math.abs(ballDX); }
  if (ballX + BALL_R > W) {
    if (score <= 5) setPip(score + 1, 'miss');
    flashTimer = 10; flashColor = '#f97316';
    setStatus('Missed! ❌', 'warning'); endGame();
  }
  if (flashTimer > 0) flashTimer--;
}

function draw() {
  ctx.clearRect(0, 0, W, H);
  ctx.fillStyle = 'rgba(15,23,42,0.85)'; ctx.fillRect(0, 0, W, H);
  if (flashTimer > 0) { ctx.fillStyle = flashColor + '22'; ctx.fillRect(0, 0, W, H); }
  ctx.setLineDash([6, 8]); ctx.strokeStyle = 'rgba(255,255,255,0.07)'; ctx.lineWidth = 2;
  ctx.beginPath(); ctx.moveTo(W/2, 0); ctx.lineTo(W/2, H); ctx.stroke(); ctx.setLineDash([]);
  if (!running && score === 0) {
    ctx.fillStyle = 'rgba(255,255,255,0.4)'; ctx.font = '14px sans-serif'; ctx.textAlign = 'center';
    ctx.fillText('🏓  Move mouse over the court to control your paddle', W/2, H/2); return;
  }
  // AI paddle — white
  const aiGrad = ctx.createLinearGradient(14, aiY, 14 + PADDLE_W, aiY + PADDLE_H);
  aiGrad.addColorStop(0, 'rgba(255,255,255,0.9)'); aiGrad.addColorStop(1, 'rgba(255,255,255,0.6)');
  ctx.fillStyle = aiGrad; ctx.shadowColor = 'rgba(255,255,255,0.4)'; ctx.shadowBlur = 8;
  ctx.beginPath(); ctx.roundRect(14, aiY, PADDLE_W, PADDLE_H, 5); ctx.fill(); ctx.shadowBlur = 0;
  // Player paddle — orange glow
  const pgx = W - PADDLE_W - 14;
  const pGrad = ctx.createLinearGradient(pgx, playerY, pgx + PADDLE_W, playerY + PADDLE_H);
  pGrad.addColorStop(0, '#f97316'); pGrad.addColorStop(1, '#f4511e');
  ctx.fillStyle = pGrad; ctx.shadowColor = '#f97316'; ctx.shadowBlur = 18;
  ctx.beginPath(); ctx.roundRect(pgx, playerY, PADDLE_W, PADDLE_H, 5); ctx.fill(); ctx.shadowBlur = 0;
  // Ball — white to ocean blue
  const bGrad = ctx.createRadialGradient(ballX-3, ballY-3, 1, ballX, ballY, BALL_R);
  bGrad.addColorStop(0, '#ffffff'); bGrad.addColorStop(1, '#0ea5e9');
  ctx.fillStyle = bGrad; ctx.shadowColor = '#0ea5e9'; ctx.shadowBlur = 20;
  ctx.beginPath(); ctx.arc(ballX, ballY, BALL_R, 0, Math.PI * 2); ctx.fill(); ctx.shadowBlur = 0;
  ctx.fillStyle = 'rgba(255,255,255,0.5)'; ctx.font = 'bold 14px sans-serif'; ctx.textAlign = 'center';
  if (score > 0) ctx.fillText('RALLY × ' + score, W / 2, 22);
}

function endGame() {
  running = false; cancelAnimationFrame(animId);
  document.getElementById('resScore').textContent = score;
  const rating = score >= 10 ? 'Unstoppable 🏆' : score >= 7 ? 'Elite Rally ⚡' :
                 score >= 4  ? 'Sharp 🎯'        : score >= 2 ? 'Getting There 👍' : 'Keep Practising 😅';
  document.getElementById('resRating').textContent = rating;
  resultsRow.classList.add('show'); againBtn.style.display = ''; setStatus('', '');
}

function resetRally() {
  cancelAnimationFrame(animId); running = false; score = 0;
  [1,2,3,4,5].forEach(n => setPip(n, ''));
  resultsRow.classList.remove('show'); setStatus('', '');
  againBtn.style.display = 'none'; playBtn.style.display = '';
  resize(); draw();
}

window.addEventListener('resize', () => { if (running || score > 0) resize(); });
resize(); draw();
```

---

## STATS MARQUEE CONVEYOR BELT

### HTML (replaces the static stats div)

```html
<div class="stats-marquee">
  <div class="marquee-wrap">
    <div class="marquee-track">
      <div class="marquee-item">
        <div class="marquee-stat"><span class="m-num">6</span><span class="m-label">Pro Courts</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat ocean"><span class="m-num">320+</span><span class="m-label">Members</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat gold"><span class="m-num">Open</span><span class="m-label">7 Days a Week</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat lime"><span class="m-num">4.9★</span><span class="m-label">Google Rating</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat"><span class="m-num">🌴</span><span class="m-label">Da Nang, Vietnam</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat ocean"><span class="m-num">Book</span><span class="m-label">A Court Today</span></div>
        <span class="marquee-dot">◆</span>
      </div>
      <!-- Duplicate for seamless loop -->
      <div class="marquee-item" aria-hidden="true">
        <div class="marquee-stat"><span class="m-num">6</span><span class="m-label">Pro Courts</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat ocean"><span class="m-num">320+</span><span class="m-label">Members</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat gold"><span class="m-num">Open</span><span class="m-label">7 Days a Week</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat lime"><span class="m-num">4.9★</span><span class="m-label">Google Rating</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat"><span class="m-num">🌴</span><span class="m-label">Da Nang, Vietnam</span></div>
        <span class="marquee-dot">◆</span>
        <div class="marquee-stat ocean"><span class="m-num">Book</span><span class="m-label">A Court Today</span></div>
        <span class="marquee-dot">◆</span>
      </div>
    </div>
  </div>
</div>
```

### CSS

```css
.stats-marquee { background: #1e293b; overflow: hidden; }
.marquee-wrap { display: flex; overflow: hidden; user-select: none; }
.marquee-track { display: flex; flex-shrink: 0; animation: marquee-scroll 28s linear infinite; }
.marquee-track:hover { animation-play-state: paused; }
.marquee-item { display: flex; align-items: center; flex-shrink: 0; }
.marquee-stat { display: inline-flex; align-items: baseline; gap: 8px; padding: 20px 40px; border-right: 1px solid rgba(255,255,255,0.08); }
.marquee-stat .m-num { font-family: var(--font-display, sans-serif); font-size: 28px; font-weight: 700; color: #f4511e; letter-spacing: 0.02em; }
.marquee-stat.ocean .m-num { color: #0ea5e9; }
.marquee-stat.gold  .m-num { color: #f59e0b; }
.marquee-stat.lime  .m-num { color: #22c55e; }
.marquee-stat .m-label { font-size: 12px; font-weight: 600; color: rgba(255,255,255,0.55); text-transform: uppercase; letter-spacing: 0.1em; }
.marquee-dot { padding: 20px 24px; color: rgba(255,255,255,0.18); font-size: 18px; flex-shrink: 0; }
@keyframes marquee-scroll {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}
```

---

## SCROLL REVEAL + UTILITY FUNCTIONS

Paste at the bottom of `<script>`, then call on DOMContentLoaded:

```js
function initReveal() {
  document.querySelectorAll('.reveal').forEach((el, i) => {
    el.style.opacity = '0';
    el.style.transform = 'translateY(28px)';
    el.style.transition =
      `opacity 0.55s cubic-bezier(0.25,0.46,0.45,0.94) ${i * 90}ms,
       transform 0.55s cubic-bezier(0.25,0.46,0.45,0.94) ${i * 90}ms`;
  });
  const obs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.style.opacity = '1'; e.target.style.transform = 'translateY(0)'; }
    });
  }, { threshold: 0.2 });
  document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
}

// Add class="reveal" to: .game-sched-card, .player, #join section
document.addEventListener('DOMContentLoaded', () => { initReveal(); });
```

---

## GLASSMORPHISM (for game card on vivid hero)

```css
/* Apply to any card sitting on top of the animated gradient hero */
.game-card-hero {
  background: rgba(255,255,255,0.18);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255,255,255,0.35);
  border-radius: 20px;
  box-shadow: 0 32px 80px rgba(0,0,0,0.25), inset 0 1px 0 rgba(255,255,255,0.4);
}
```
