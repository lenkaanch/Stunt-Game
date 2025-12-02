<!-- Stunt Runner — готовый код для вставки в Tilda (T123 -> HTML) -->
<style>
  .sr-container { max-width:900px; margin:20px auto; text-align:center; font-family:Arial, sans-serif; }
  #game { background:#111; border-radius:12px; border:3px solid #222; display:block; margin:10px auto; touch-action:none; }
  .controls { margin:8px 0; display:flex; gap:10px; justify-content:center; align-items:center; flex-wrap:wrap; }
  .btn { padding:8px 12px; border-radius:8px; background:#222; color:#fff; border:1px solid #444; cursor:pointer; }
  .bigbtn { padding:12px 18px; font-weight:600; }
  #mobileJump { position:fixed; right:18px; bottom:18px; z-index:9999; border-radius:50%; width:76px; height:76px; font-size:18px; display:none; align-items:center; justify-content:center; }
  #soundToggle.active { background:#2a7; color:#022; }
  #hud { color:#fff; text-shadow:0 1px 2px rgba(0,0,0,0.7); }
  .picker { display:inline-block; padding:6px 8px; background:#fff; border-radius:8px; color:#111; }
  @media (max-width:700px){ #game{ width:95%; } #mobileJump{ display:flex; } }
</style>

<div class="sr-container">
  <h2>Stunt Runner — Прыгай через препятствия</h2>
  <div style="margin-bottom:6px;">
    <label class="picker">Выбери персонажа:
      <select id="charSelect" style="margin-left:8px;">
        <option value="man">Мужчина — джинсы + грубая куртка</option>
        <option value="woman">Женщина — Lara Croft style</option>
      </select>
    </label>

    <label class="picker" style="margin-left:12px;">Уровень:
      <select id="levelSelect" style="margin-left:8px;">
        <option value="1">1 — Площадка каскадёров</option>
        <option value="2">2 — Город</option>
        <option value="3">3 — Съёмочная площадка</option>
        <option value="4">4 — Ночной город</option>
        <option value="5">5 — Лес (финал вертолёт)</option>
      </select>
    </label>
  </div>

  <div class="controls">
    <button id="startBtn" class="btn bigbtn">Старт</button>
    <button id="restartBtn" class="btn">Рестарт</button>
    <button id="soundToggle" class="btn">Включить звук</button>
    <div id="hud" style="margin-left:8px;">Счёт: <span id="score">0</span></div>
  </div>

  <canvas id="game" width="860" height="320"></canvas>
</div>

<!-- мобильная кнопка прыжка (показывается на мобильных) -->
<button id="mobileJump" class="btn" aria-label="Прыжок">Прыжок</button>

<script>
/* ============================
   Stunt Runner — Canvas game
   - 5 levels with different backgrounds
   - 2 stylized characters
   - mobile button + swipe up
   - sounds via button (replace URLs below)
   ============================ */

const canvas = document.getElementById('game');
const ctx = canvas.getContext('2d');

let W = canvas.width, H = canvas.height;

// HUD
const scoreEl = document.getElementById('score');
const startBtn = document.getElementById('startBtn');
const restartBtn = document.getElementById('restartBtn');
const soundToggle = document.getElementById('soundToggle');
const charSelect = document.getElementById('charSelect');
const levelSelect = document.getElementById('levelSelect');
const mobileJump = document.getElementById('mobileJump');

let game = {
  running: false,
  score: 0,
  level: 1,
  speed: 5,
  spawnRate: 1400,
  obstacles: [],
  gravity: 1.2,
  lastSpawn: 0,
  tick: 0,
  frames: 0
};

// ----- Sounds (замени URL'ы на свои файлы если нужно) -----
const soundEnabledState = { enabled: false };
const snd = {
  jump: new Audio("https://cdn.pixabay.com/download/audio/2021/08/04/audio_3d1f6a1e1c.mp3?filename=jump-01-6293.mp3"), // placeholder
  hit: new Audio("https://cdn.pixabay.com/download/audio/2022/03/15/audio_0b6cf9a1d8.mp3?filename=impact-2-6597.mp3"), // placeholder
  bgMusic: new Audio(""), // optional bg music
  helicopter: new Audio("") // optional helicopter sound
};
// Предупреждение: некоторые браузеры блокируют автоплеер, поэтому звук включаем только по кнопке.

// ----- Responsive mobile button visibility -----
function updateMobileUI(){
  if(window.innerWidth <= 700) mobileJump.style.display = 'flex';
  else mobileJump.style.display = 'none';
}
window.addEventListener('resize', updateMobileUI);
updateMobileUI();

// ----- Stylized character sprites drawn to offscreen canvases -----
function makeCharacterSprites(){
  // returns two Image objects (man, woman) as canvas->image
  function drawMan(ctx, scale){
    // body
    ctx.fillStyle = '#2b2b2b'; // jacket (dark denim)
    ctx.fillRect(0, 20*scale, 34*scale, 44*scale);
    // torso inner (shirt)
    ctx.fillStyle = '#bfbfbf';
    ctx.fillRect(8*scale, 32*scale, 18*scale, 18*scale);
    // legs (jeans)
    ctx.fillStyle = '#101019';
    ctx.fillRect(6*scale, 58*scale, 10*scale, 22*scale);
    ctx.fillRect(18*scale, 58*scale, 10*scale, 22*scale);
    // head
    ctx.fillStyle = '#f1c8a0';
    ctx.beginPath(); ctx.ellipse(17*scale, 8*scale, 11*scale, 11*scale, 0, 0, Math.PI*2); ctx.fill();
    // hair
    ctx.fillStyle = '#222';
    ctx.fillRect(6*scale, -2*scale, 22*scale, 10*scale);
    // simple face features
    ctx.fillStyle = '#000'; ctx.fillRect(12*scale,6*scale,3*scale,2*scale); ctx.fillRect(21*scale,6*scale,3*scale,2*scale);
  }
  function drawWoman(ctx, scale){
    // torso (tank top / Lara style)
    ctx.fillStyle = '#2f5b6e'; // teal top
    ctx.fillRect(6*scale, 28*scale, 30*scale, 28*scale);
    // shorts
    ctx.fillStyle = '#1f2b3a';
    ctx.fillRect(10*scale, 56*scale, 10*scale, 20*scale);
    ctx.fillRect(22*scale, 56*scale, 10*scale, 20*scale);
    // legs
    ctx.fillStyle = '#f1c8a0';
    ctx.fillRect(10*scale, 76*scale, 10*scale, 22*scale);
    ctx.fillRect(22*scale, 76*scale, 10*scale, 22*scale);
    // head
    ctx.fillStyle = '#f1c8a0';
    ctx.beginPath(); ctx.ellipse(20*scale, 8*scale, 10*scale, 10*scale, 0, 0, Math.PI*2); ctx.fill();
    // hair long blonde
    ctx.fillStyle = '#caa068';
    ctx.beginPath(); ctx.ellipse(20*scale, 18*scale, 14*scale, 18*scale, 0, 0, Math.PI*2); ctx.fill();
    // face eyes
    ctx.fillStyle = '#000'; ctx.fillRect(14*scale,6*scale,3*scale,2*scale); ctx.fillRect(23*scale,6*scale,3*scale,2*scale);
  }

  function canvasToImg(drawFn, w, h, scale){
    const c = document.createElement('canvas');
    c.width = w*scale; c.height = h*scale;
    const g = c.getContext('2d');
    drawFn(g, scale);
    const img = new Image();
    img.src = c.toDataURL();
    return img;
  }
  return {
    man: canvasToImg(drawMan, 40, 110, 2),
    woman: canvasToImg(drawWoman, 40, 110, 2)
  };
}

const sprites = makeCharacterSprites();

// ----- Background drawing per level (parallax layers) -----
function drawBackground(level, tick){
  // base sky
  if(level===1){ // stunt area (mats, boxes, rails)
    ctx.fillStyle = '#cfe8ff'; ctx.fillRect(0,0,W,H);
    // ground
    ctx.fillStyle = '#3a3a3a'; ctx.fillRect(0,H-70,W,70);
    // mats boxes
    for(let i=0;i<10;i++){
      ctx.fillStyle = i%2? '#b33':'#d44';
      ctx.fillRect((i*120 + (tick*0.5)%120)-120, H-80 - (i%3)*6, 100, 24);
      // rails
      ctx.fillStyle='#999'; ctx.fillRect((i*260 + (tick*0.9)%260)-260, H-150, 120, 6);
    }
  } else if(level===2){ // city
    ctx.fillStyle = '#9cc7ff'; ctx.fillRect(0,0,W,H);
    // skyline
    for(let i=0;i<12;i++){
      const bw = 50 + (i%3)*20;
      const bh = 80 + (i*20%(H-120));
      ctx.fillStyle = '#2b2b2b';
      ctx.fillRect(i*(W/12) + Math.sin((tick+i)*0.02)*6, H-70-bh, bw, bh);
      // windows
      ctx.fillStyle='#ffd';
      for(let y=H-70-bh+8;y<H-70-8;y+=16){
        for(let x=i*(W/12)+6;x<i*(W/12)+bw-6;x+=12){
          if(Math.random()>0.6) ctx.fillRect(x+Math.sin((tick+i)*0.01)*4, y, 6, 8);
        }
      }
    }
    // street
    ctx.fillStyle = '#222'; ctx.fillRect(0,H-70,W,70);
    // road stripe
    ctx.fillStyle='#fff'; for(let x=0;x<W;x+=60) ctx.fillRect(x+((tick*speed)%60), H-35, 30, 4);
  } else if(level===3){ // film set
    ctx.fillStyle = '#eef6ff'; ctx.fillRect(0,0,W,H);
    // lights and tripods
    for(let i=0;i<8;i++){
      const x = (i*150 + (tick*0.7)%150)-150;
      ctx.strokeStyle='#333'; ctx.lineWidth=3;
      ctx.beginPath(); ctx.moveTo(x+100,H-120); ctx.lineTo(x+100,H-40); ctx.stroke();
      ctx.fillStyle = '#222'; ctx.fillRect(x+92,H-140,16,20);
      // fake camera
      ctx.fillStyle='#333'; ctx.fillRect(x+60,H-150,40,20);
      ctx.fillStyle='#ffeb3b'; ctx.beginPath(); ctx.arc(x+80,H-140,8,0,Math.PI*2); ctx.fill();
    }
    ctx.fillStyle='#2a2a2a'; ctx.fillRect(0,H-70,W,70);
  } else if(level===4){ // night neon
    // gradient sky
    const g = ctx.createLinearGradient(0,0,0,H);
    g.addColorStop(0,'#021028'); g.addColorStop(1,'#0a1b2b');
    ctx.fillStyle = g; ctx.fillRect(0,0,W,H);
    // neon buildings
    for(let i=0;i<10;i++){
      const x = i*(W/10) + Math.sin((tick+i)*0.03)*8;
      const wB = 60;
      const hB = 120 + (i%3)*50;
      ctx.fillStyle = '#041a2b';
      ctx.fillRect(x, H-70-hB, wB, hB);
      // neon lines
      ctx.strokeStyle = (i%2? '#ff2d95' : '#3df0ff');
      ctx.lineWidth = 3;
      for(let y=H-70-hB+10;y<H-70;y+=20) {
        ctx.beginPath(); ctx.moveTo(x+6,y+Math.sin((tick+i)*0.02)*2); ctx.lineTo(x+wB-6,y+Math.sin((tick+i)*0.02)*2); ctx.stroke();
      }
    }
    // ground
    ctx.fillStyle = '#06121a'; ctx.fillRect(0,H-70,W,70);
  } else if(level===5){ // forest + lake
    ctx.fillStyle = '#bde7d7'; ctx.fillRect(0,0,W,H);
    // distant hills
    ctx.fillStyle = '#8fcf9a'; ctx.beginPath(); ctx.ellipse(120,120,220,90,0,0,Math.PI*2); ctx.fill();
    ctx.fillStyle = '#7ec07f'; ctx.beginPath(); ctx.ellipse(620,110,240,110,0,0,Math.PI*2); ctx.fill();
    // trees
    for(let i=0;i<12;i++){
      const x = (i*90 + (tick*0.2)%90)-90;
      ctx.fillStyle = '#3b5f36';
      ctx.beginPath(); ctx.moveTo(x, H-70-30); ctx.lineTo(x+20, H-70-30-60); ctx.lineTo(x+40, H-70-30); ctx.closePath(); ctx.fill();
      ctx.fillStyle = '#6b3b1d'; ctx.fillRect(x+16, H-70-10, 8, 30);
    }
    // lake left
    ctx.fillStyle = '#4aa3c8'; ctx.beginPath(); ctx.ellipse(W-220,H-110,120,50,0,0,Math.PI*2); ctx.fill();
    ctx.fillStyle = '#3a7f9a'; ctx.globalAlpha = 0.4; ctx.fillRect(0,H-70,W,70); ctx.globalAlpha = 1.0;
  }
}

/* --------- Obstacles definitions --------- 
   Drawn shapes for: table, chair, wall, rock, bench, viking (cartoon helmet)
*/
function drawObstacleShape(ctx, type, x, y, w, h){
  if(type==='table'){
    ctx.fillStyle = '#8b5a2b'; ctx.fillRect(x,y-10,w,h-10);
    // legs
    ctx.fillRect(x+4,y+h-6,6,6); ctx.fillRect(x+w-10,y+h-6,6,6);
  } else if(type==='chair'){
    ctx.fillStyle = '#a05a2e'; ctx.fillRect(x,y,w*0.6,h*0.6);
    ctx.fillRect(x,y-18,w*0.2,18);
  } else if(type==='wall'){
    ctx.fillStyle = '#b33'; ctx.fillRect(x,y-40,w,40);
    ctx.fillStyle='#8b0000';
    for(let by=y-40;by<y;by+=10) for(let bx=x;bx<x+w;bx+=20) ctx.fillRect(bx+2,by+2,16,6);
  } else if(type==='rock'){
    ctx.fillStyle = '#8a8a8a'; ctx.beginPath(); ctx.ellipse(x+w/2, y-8, w*0.6, h*0.6, 0, 0, Math.PI*2); ctx.fill();
  } else if(type==='bench'){
    ctx.fillStyle = '#9b6b3a'; ctx.fillRect(x,y-10,w,10); ctx.fillRect(x+6,y,6,10); ctx.fillRect(x+w-12,y,6,10);
  } else if(type==='viking'){
    ctx.fillStyle='#c2a56b'; ctx.fillRect(x,y-22,w,18); // body
    ctx.fillStyle='#999'; ctx.beginPath(); ctx.arc(x+w/2,y-28,12,0,Math.PI,true); ctx.fill(); // helmet
    // horns
    ctx.fillStyle='#fff'; ctx.beginPath(); ctx.ellipse(x+w/2-16,y-28,6,4,0,0,Math.PI*2); ctx.fill();
    ctx.beginPath(); ctx.ellipse(x+w/2+16,y-28,6,4,0,0,Math.PI*2); ctx.fill();
  }
}

/* --------- Player object --------- */
function makePlayer(which){
  return {
    type: which,
    x: 80,
    y: H-70 - 110, // base y
    w: 40,
    h: 90,
    vy: 0,
    onGround: true,
    frame:0,
    dustTimer:0
  };
}

let player = makePlayer('man');

/* --------- Spawn obstacles according to level --------- */
function spawnObstacleForLevel(level){
  const typesByLevel = {
    1: ['table','chair','rock'],
    2: ['wall','rock','bench'],
    3: ['chair','table','viking','bench'],
    4: ['wall','rock','viking'],
    5: ['rock','bench','table','chair']
  };
  const arr = typesByLevel[level];
  const t = arr[Math.floor(Math.random()*arr.length)];
  const w = 40 + Math.random()*40;
  const h = 30 + Math.random()*40;
  return { type: t, x: W + 40, y: H-70, w: w, h: h };
}

/* --------- Particles (dust) --------- */
let particles = [];
function spawnDust(x,y,amount){
  for(let i=0;i<amount;i++){
    particles.push({
      x: x + (Math.random()-0.5)*10,
      y: y + (Math.random()-0.5)*6,
      vx: (Math.random()-0.5)*1.2,
      vy: -1 - Math.random()*1,
      life: 30 + Math.random()*30,
      size: 3 + Math.random()*3
    });
  }
}

/* --------- Game loop --------- */
function resetGame(){
  game.running = false; game.score = 0; game.obstacles = []; game.tick = 0; player = makePlayer(charSelect.value);
  scoreEl.textContent = game.score;
}
resetGame();

function setLevelFromSelect(){
  const lvl = parseInt(levelSelect.value);
  game.level = lvl;
  // tweak speed & spawnRate by level
  switch(lvl){
    case 1: game.speed = 4; game.spawnRate = 1600; break;
    case 2: game.speed = 6; game.spawnRate = 1400; break;
    case 3: game.speed = 8; game.spawnRate = 1200; break;
    case 4: game.speed = 11; game.spawnRate = 1000; break;
    case 5: game.speed = 9; game.spawnRate = 1000; break;
  }
}
setLevelFromSelect();
levelSelect.addEventListener('change', ()=> { setLevelFromSelect(); });

startBtn.addEventListener('click', ()=>{
  if(!game.running){
    setLevelFromSelect();
    player = makePlayer(charSelect.value);
    game.running = true;
    game.lastSpawn = performance.now();
    game.score = 0;
    scoreEl.textContent = game.score;
    // Attempt to unlock sounds if user enabled them earlier (some browsers require interaction)
    if(soundEnabledState.enabled) {
      Object.values(snd).forEach(s => { try{ s.play().then(()=>s.pause(), ()=>{}); s.currentTime=0;}catch(e){} });
    }
  }
});

restartBtn.addEventListener('click', ()=>{ resetGame(); setLevelFromSelect(); });

soundToggle.addEventListener('click', ()=>{
  soundEnabledState.enabled = !soundEnabledState.enabled;
  if(soundEnabledState.enabled) {
    soundToggle.classList.add('active'); soundToggle.textContent = 'Звук включён';
    // Unblock audio by playing a tiny silent buffer or playing one sound once
    try { snd.jump.volume = 0.8; } catch(e){}
  } else { soundToggle.classList.remove('active'); soundToggle.textContent='Включить звук'; }
});

/* Keyboard control: space to jump */
window.addEventListener('keydown', (e)=>{
  if(e.code === 'Space' && game.running && player.onGround){
    player.vy = -16; player.onGround = false; player.dustTimer = 6;
    if(soundEnabledState.enabled) { try{ snd.jump.currentTime=0; snd.jump.play(); }catch(e){} }
  }
  // start on Enter
  if(e.code==='Enter' && !game.running) startBtn.click();
});

/* Mobile: jump button */
mobileJump.addEventListener('touchstart', (ev)=>{ ev.preventDefault(); if(game.running && player.onGround){ player.vy=-16; player.onGround=false; spawnDust(player.x+player.w/2, player.y+player.h, 8); if(soundEnabledState.enabled) try{ snd.jump.currentTime=0; snd.jump.play(); }catch(e){} } });

/* Mobile: swipe up */
let touchStartY = null;
canvas.addEventListener('touchstart', (e)=>{ if(e.touches && e.touches[0]) touchStartY = e.touches[0].clientY; }, {passive:true});
canvas.addEventListener('touchend', (e)=>{
  if(!touchStartY) return;
  const ty = e.changedTouches[0].clientY;
  if(touchStartY - ty > 60 && game.running && player.onGround){
    player.vy=-16; player.onGround=false; spawnDust(player.x+player.w/2, player.y+player.h, 8);
    if(soundEnabledState.enabled) try{ snd.jump.currentTime=0; snd.jump.play(); }catch(e){}
  }
  touchStartY = null;
}, {passive:true});

/* Mouse / Click on canvas for jump (desktop) */
canvas.addEventListener('mousedown', (e)=>{ if(game.running && player.onGround){ player.vy=-16; player.onGround=false; spawnDust(player.x+player.w/2, player.y+player.h, 6); if(soundEnabledState.enabled) try{ snd.jump.currentTime=0; snd.jump.play(); }catch(e){} } });

/* Main animation frame */
let lastTime = performance.now();
function loop(now){
  const dt = now - lastTime;
  lastTime = now;
  if(game.running){
    game.tick += dt;
    // spawn obstacles
    if(now - game.lastSpawn > game.spawnRate){
      game.obstacles.push(spawnObstacleForLevel(game.level));
      // small random jitter on spawnRate
      game.lastSpawn = now - Math.random()*200;
    }
    // update player
    player.vy += game.gravity;
    player.y += player.vy;
    if(player.y >= H-70 - player.h){
      if(!player.onGround) {
        // landed
        spawnDust(player.x + player.w/2, player.y+player.h, 8);
      }
      player.y = H-70 - player.h; player.vy = 0; player.onGround = true;
    } else { player.onGround = false; }

    // move obstacles
    for(let i=game.obstacles.length-1;i>=0;i--){
      const o = game.obstacles[i];
      o.x -= game.speed;
      // collision check (AABB)
      if(player.x < o.x + o.w && player.x + player.w > o.x && player.y + player.h > o.y - o.h/2){
        // hit
        if(soundEnabledState.enabled) try{ snd.hit.currentTime=0; snd.hit.play(); }catch(e){}
        game.running = false;
        alert('Поражение! Твой счёт: ' + game.score);
        break;
      }
      // passed
      if(o.x + o.w < 0){ game.obstacles.splice(i,1); game.score++; scoreEl.textContent = game.score; }
    }

    // particles
    for(let i=particles.length-1;i>=0;i--){
      const p = particles[i];
      p.x += p.vx; p.y += p.vy; p.vy += 0.15; p.life--;
      if(p.life<=0) particles.splice(i,1);
    }

    // automatic level progression option: if you want to increase level on certain score, you can implement here.
    // finish sequence on level 5 when score hit threshold (e.g., 15)
    if(game.level === 5 && game.score >= 15 && game.running){
      // trigger helicopter sequence
      game.running = false;
      flyHelicopterFinish();
    }
  }

  // draw
  ctx.clearRect(0,0,W,H);
  drawBackground(game.level, game.tick);

  // draw ground line
  ctx.fillStyle = '#0a0a0a'; ctx.fillRect(0,H-70,W,4);

  // draw obstacles
  for(let o of game.obstacles){
    drawObstacleShape(ctx, o.type, Math.floor(o.x), o.y - o.h, o.w, o.h);
  }

  // draw player (using sprite)
  const sprite = (player.type === 'woman') ? sprites.woman : sprites.man;
  // bobbing while running
  const bob = (player.onGround ? Math.sin(game.tick*0.02)*2 : 0);
  ctx.drawImage(sprite, player.x, player.y + bob, player.w, player.h);

  // draw dust particles
  for(let p of particles){
    ctx.globalAlpha = Math.max(0, p.life/60);
    ctx.fillStyle = 'rgba(160,120,80,0.9)';
    ctx.beginPath(); ctx.ellipse(p.x, p.y, p.size, p.size*0.6, 0, 0, Math.PI*2); ctx.fill();
    ctx.globalAlpha = 1.0;
  }

  // HUD overlay (level label)
  ctx.fillStyle = 'rgba(0,0,0,0.4)'; ctx.fillRect(8,8,170,28);
  ctx.fillStyle = '#fff'; ctx.font = '16px Arial'; ctx.fillText('Уровень: ' + game.level, 16, 28);

  requestAnimationFrame(loop);
}
requestAnimationFrame(loop);

/* -------- Helicopter finish on level 5 -------- */
function flyHelicopterFinish(){
  // simple animation: helicopter flies in from right, lifts player up and off-screen
  const heli = { x: W + 40, y: 60, vx: -5 };
  const startPlayerY = player.y;
  let phase = 0; // 0 fly in, 1 attach + lift, 2 done
  const heliLoop = () => {
    ctx.clearRect(0,0,W,H);
    drawBackground(5, game.tick);

    // draw obstacles remaining as dim
    for(let o of game.obstacles){ ctx.globalAlpha = 0.4; drawObstacleShape(ctx, o.type, Math.floor(o.x), o.y - o.h, o.w, o.h); ctx.globalAlpha = 1; }

    // heli
    ctx.fillStyle = '#333'; ctx.fillRect(heli.x, heli.y, 80, 24); // body
    ctx.fillStyle = '#666'; ctx.fillRect(heli.x+32, heli.y-18, 36,6); // rotor
    // rotor
    ctx.fillStyle = '#222'; ctx.fillRect(heli.x+22+Math.sin(performance.now()*0.02)*10, heli.y-22, 60,4);

    if(phase===0){
      heli.x += heli.vx;
      if(heli.x < W-260){ phase = 1; }
    } else if(phase===1){
      // lift player gradually to helicopter y - attach rope
      player.x = heli.x - 20;
      player.y -= 1.6;
      // draw rope
      ctx.strokeStyle = '#222'; ctx.beginPath(); ctx.moveTo(heli.x+12, heli.y+24); ctx.lineTo(player.x+player.w/2, player.y); ctx.stroke();
      if(player.y + player.h < 30){ phase = 2; if(soundEnabledState.enabled && snd.helicopter) try{ snd.helicopter.play(); }catch(e){} }
    } else { // done - fly away
      heli.x += -8;
      player.x = heli.x - 20;
      player.y -= 1.2;
      if(heli.x < -200){ // finished
        alert('Поздравляем! Уровень пройден. Твой счёт: ' + game.score);
        resetGame();
        return;
      }
    }

    // draw player attached
    const sprite = (player.type === 'woman') ? sprites.woman : sprites.man;
    ctx.drawImage(sprite, player.x, player.y, player.w, player.h);

    requestAnimationFrame(heliLoop);
  };
  heliLoop();
}

/* ======= Notes for deployment in Tilda =======
1) Если хочешь заменить звуки на свои файлы — загрузи их в Tilda и вставь прямые ссылки в snd.jump.src и snd.hit.src.
2) Можно заменить спрайты персонажей на готовые PNG — заменив sprites.man.src / sprites.woman.src.
3) При желании можно увеличить порог для "финала" level 5 (game.score >= 15) на другой порог.
4) Этот файл не использует внешние изображения кроме placeholder audio; всё рисуется на canvas — будет работать в Tilda.
============================================== */

</script>
