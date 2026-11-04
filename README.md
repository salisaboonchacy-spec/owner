[fing.biston.html](https://github.com/user-attachments/files/34363288/fing.biston.html)
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>ศึกยักษ์ 2 ผู้เล่น</title><img width="455" height="452" alt="images" src="https://github.com/user-attachments/assets/983a5b60-6b39-4c52-9144-f4ec2ab986d3" />

<style>
  * { box-sizing: border-box; }
  html, body {
    touch-action: manipulation;
    -webkit-user-select: none;
    user-select: none;
    -webkit-tap-highlight-color: transparent;
    overscroll-behavior: none;
  }
  body {
    margin: 0;
    padding: 16px 12px;
    background: #f4f3ef;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    display: flex;
    justify-content: center;
    min-height: 100vh;
  }
  .wrap { max-width: 520px; width: 100%; }
  h1 { font-size: 17px; font-weight: 600; text-align: center; margin: 0 0 14px; color: #222; }
  h2 { font-size: 15px; font-weight: 600; text-align: center; margin: 0 0 16px; color: #222; }
  .bars { display: flex; justify-content: space-between; gap: 12px; margin-bottom: 8px; }
  .bar-col { flex: 1; }
  .bar-label { font-size: 13px; color: #666; margin-bottom: 5px; font-weight: 500; display: flex; justify-content: space-between; }
  .bar-label.right { flex-direction: row-reverse; }
  .bar-track { height: 22px; background: #e3e1d9; border-radius: 8px; overflow: hidden; border: 1px solid #d5d3c9; }
  .bar-fill { height: 100%; width: 100%; transition: width 0.2s; }
  #sceneWrap { overflow: hidden; border-radius: 12px; }
  svg { width: 100%; background: #efeee7; display: block; touch-action: none; }
  #log { margin: 10px 0; font-size: 13px; color: #666; min-height: 34px; text-align: center; line-height: 1.4; }
  .controls { display: flex; justify-content: space-between; gap: 10px; align-items: flex-start; flex-wrap: wrap; }
  .grp { display: flex; gap: 8px; flex: 1; min-width: 200px; flex-wrap: wrap; }
  .grp.p2 { justify-content: flex-end; }
  button {
    height: 46px;
    min-width: 44px;
    padding: 0 12px;
    border-radius: 10px;
    border: 0.5px solid #ccc;
    background: #fff;
    font-size: 14px;
    cursor: pointer;
    color: #222;
    touch-action: manipulation;
  }
  .grp button.dir { flex: 0 0 44px; padding: 0; font-size: 18px; }
  button.atk { flex: 1; min-width: 80px; font-weight: 500; }
  button:hover { background: #f0f0ec; }
  button:active { transform: scale(0.96); background: #e8e7e1; }
  button:disabled { opacity: 0.5; cursor: default; }
  #restart { width: 100%; margin-top: 10px; display: none; height: 44px; }
  .hint { font-size: 12px; color: #999; text-align: center; margin-top: 10px; }
  @media (max-width: 460px) {
    .controls { flex-direction: column; gap: 8px; }
    .grp.p2 { justify-content: flex-start; }
  }
  .pickRow { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; margin-bottom: 20px; }
  .pickCol { flex: 1; min-width: 140px; max-width: 200px; }
  .pickTitle { font-size: 13px; color: #666; text-align: center; margin-bottom: 8px; }
  .pick { width: 100%; margin-bottom: 8px; text-align: left; padding: 10px 14px; height: auto; display: flex; align-items: center; gap: 8px; }
  .pick .dot { width: 14px; height: 14px; border-radius: 50%; flex: none; }
  .pick.selected { border: 2px solid #222; background: #eee; }
  #startBtn { display: block; margin: 0 auto; padding: 0 28px; }
</style>
</head>
<body>
<div class="wrap">
  <h1>ศึกยักษ์ 2 ผู้เล่น</h1>

  <div id="titleScreen" style="text-align:center; padding: 40px 0;">
    <div style="font-size:40px; margin-bottom:8px;">⚔️</div>
    <h2 style="font-size:20px; margin-bottom:6px;">ศึกยักษ์ 2 ผู้เล่น</h2>
    <p style="font-size:13px; color:#888; margin-bottom:24px;">เลือกตัวละครแล้วต่อสู้กับเพื่อนบนเครื่องเดียวกัน</p>
    <button id="playBtn" style="padding:0 40px; height:50px; font-size:16px; font-weight:600; background:#222; color:#fff; border:none;">เล่นเลย</button>
  </div>

  <div id="modeScreen" style="display:none; text-align:center; padding: 20px 0;">
    <h2>เลือกโหมดการเล่น</h2>
    <div style="display:flex; gap:14px; justify-content:center; flex-wrap:wrap; max-width:360px; margin:0 auto;">
      <button class="modeBtn" data-mode="bot" style="flex:1; min-width:140px; height:64px; font-size:15px; font-weight:600;">🤖<br>เล่นกับบอท</button>
      <button class="modeBtn" data-mode="friend" style="flex:1; min-width:140px; height:64px; font-size:15px; font-weight:600;">🧑‍🤝‍🧑<br>เล่นกับเพื่อน</button>
    </div>
  </div>

  <div id="selectScreen" style="display:none;">
    <h2>เลือกตัวละครของแต่ละฝ่าย</h2>
    <div class="pickRow">
      <div class="pickCol">
        <div class="pickTitle">ผู้เล่น 1</div>
        <button class="pick" data-p="p1" data-c="knight"><span class="dot" style="background:#1A1A1A"></span>อัศวิน</button>
        <button class="pick" data-p="p1" data-c="catfish"><span class="dot" style="background:#534AB7"></span>ปลาดุก</button>
        <button class="pick" data-p="p1" data-c="horse"><span class="dot" style="background:#8A5A2E"></span>ม้า</button>
        <button class="pick" data-p="p1" data-c="gunner"><span class="dot" style="background:#E8E4DA"></span>มนุษย์</button>
        <button class="pick" data-p="p1" data-c="hero"><span class="dot" style="background:#2F6FE0"></span>นักรบแสง</button>
      </div>
      <div class="pickCol">
        <div class="pickTitle" id="p2title">ผู้เล่น 2</div>
        <button class="pick" data-p="p2" data-c="knight"><span class="dot" style="background:#1A1A1A"></span>อัศวิน</button>
        <button class="pick" data-p="p2" data-c="catfish"><span class="dot" style="background:#534AB7"></span>ปลาดุก</button>
        <button class="pick" data-p="p2" data-c="horse"><span class="dot" style="background:#8A5A2E"></span>ม้า</button>
        <button class="pick" data-p="p2" data-c="gunner"><span class="dot" style="background:#E8E4DA"></span>มนุษย์</button>
        <button class="pick" data-p="p2" data-c="hero"><span class="dot" style="background:#2F6FE0"></span>นักรบแสง</button>
      </div>
    </div>
    <button id="startBtn" disabled>ต่อไป</button>
  </div>

  <div id="stageScreen" style="display:none; text-align:center; padding: 20px 0;">
    <h2>เลือกด่าน</h2>
    <div style="display:flex; gap:14px; justify-content:center; flex-wrap:wrap;">
      <button class="pick stageBtn" data-stage="forest" style="max-width:220px; justify-content:center; font-size:15px;">🌲 ป่า</button>
      <button class="pick stageBtn" data-stage="city" style="max-width:220px; justify-content:center; font-size:15px;">🏙️ เมือง</button>
    </div>
  </div>

  <div id="gameScreen" style="display:none;">
    <div class="bars">
      <div class="bar-col">
        <div class="bar-label"><span id="p1label">P1</span><span id="p1hpnum">300</span></div>
        <div class="bar-track"><div id="hp_p1" class="bar-fill"></div></div>
        <div class="bar-track" style="height:8px;margin-top:3px;"><div id="stg_p1" class="bar-fill" style="background:#E24B4A;width:0%;"></div></div>
      </div>
      <div class="bar-col">
        <div class="bar-label right"><span id="p2label">P2</span><span id="p2hpnum">300</span></div>
        <div class="bar-track"><div id="hp_p2" class="bar-fill"></div></div>
        <div class="bar-track" style="height:8px;margin-top:3px;"><div id="stg_p2" class="bar-fill" style="background:#E24B4A;width:0%;"></div></div>
      </div>
    </div>

    <div id="sceneWrap">
    <svg id="scene" viewBox="0 0 400 220">
      <rect id="skyRect" x="0" y="0" width="400" height="180" fill="#efeee7"/>
      <g id="bgDecor"></g>
      <rect id="groundRect" x="0" y="180" width="400" height="40" fill="#e3e1d9"/>
      <line id="beam" x1="0" y1="0" x2="0" y2="0" stroke="#ffffff" stroke-width="7" opacity="0" stroke-linecap="round"/>
      <circle id="charge" cx="0" cy="0" r="0" fill="#ffffff" opacity="0"/>
      <g id="fx"></g>
      <g id="p1" transform="translate(80,130)"></g>
      <g id="p2" transform="translate(300,130) scale(-1,1)"></g>
    </svg>
    </div>

    <div id="log">พร้อมสู้!</div>

    <div class="controls">
      <div class="grp">
        <button id="p1left" class="dir" aria-label="P1 เดินซ้าย">←</button>
        <button id="p1right" class="dir" aria-label="P1 เดินขวา">→</button>
        <button id="p1m" class="atk"></button>
        <button id="p1s" class="atk"></button>
      </div>
      <div class="grp p2">
        <button id="p2s" class="atk"></button>
        <button id="p2m" class="atk"></button>
        <button id="p2left" class="dir" aria-label="P2 เดินซ้าย">←</button>
        <button id="p2right" class="dir" aria-label="P2 เดินขวา">→</button>
      </div>
    </div>
    <button id="restart">เริ่มใหม่</button>
    <div class="hint">P1: A/D เดิน, G โจมตีประชิด, F ท่าไม้ตาย — P2: ลูกศร เดิน, Enter โจมตีประชิด, Shift ท่าไม้ตาย</div>
  </div>
</div>

<script>
(function(){
  window.addEventListener('error', function(e){
    const logEl = document.getElementById('log');
    if(logEl) logEl.textContent = 'เกิดข้อผิดพลาด: ' + e.message;
    console.error(e);
  });
  const svgNS = "http://www.w3.org/2000/svg";

  function buildKnight(p){ return `
    <g id="${p}back"><path d="M -12 4 Q -26 26 -20 54 L -10 54 L -6 30 L -2 54 L 6 40 Z" fill="#0D0D0D"/></g>
    <g id="${p}legBack"><rect x="-9" y="24" width="18" height="34" rx="4" fill="#1A1A1A"/><rect x="-12" y="52" width="10" height="8" rx="2" fill="#000"/></g>
    <g id="${p}legFront"><rect x="-9" y="24" width="18" height="34" rx="4" fill="#1A1A1A"/><rect x="2" y="52" width="10" height="8" rx="2" fill="#000"/></g>
    <g id="${p}torso"><path d="M -14 -6 L 14 -6 L 12 22 L -12 22 Z" fill="#1A1A1A"/><path d="M 0 0 L 6 8 L 0 20 L -6 8 Z" fill="#000" stroke="#444441" stroke-width="1"/></g>
    <path d="M -14 -10 L -22 -2 L -14 2 Z" fill="#000"/><path d="M 14 -10 L 22 -2 L 14 2 Z" fill="#000"/>
    <circle cx="-15" cy="-5" r="6" fill="#1A1A1A"/><circle cx="15" cy="-5" r="6" fill="#1A1A1A"/>
    <g id="${p}armL"><rect x="-19" y="-4" width="7" height="18" rx="2" fill="#1A1A1A"/><rect x="-20" y="12" width="9" height="7" rx="2" fill="#000"/></g>
    <g id="${p}armR"><rect x="12" y="-4" width="7" height="18" rx="2" fill="#1A1A1A"/><rect x="11" y="12" width="9" height="7" rx="2" fill="#000"/></g>
    <rect x="-4" y="-12" width="8" height="8" fill="#0D0D0D"/>
    <g id="${p}head"><ellipse cx="0" cy="-20" rx="13" ry="14" fill="#000"/><path d="M -10 -30 L -18 -42 L -8 -32 Z" fill="#0D0D0D"/><path d="M 10 -30 L 18 -42 L 8 -32 Z" fill="#0D0D0D"/><path id="${p}mouth" d="M -6 -22 L 0 -14 L 6 -22" fill="none" stroke="#fff" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/></g>
  `; }

  function buildCatfish(p){ return `
    <g id="${p}back"><path d="M 12 6 Q 28 2 32 -10 Q 30 4 20 10 Q 30 14 32 26 Q 26 16 12 14 Z" fill="#3C3489"/></g>
    <g id="${p}legBack"><rect x="-9" y="24" width="18" height="32" rx="6" fill="#3C3489"/><path d="M -13 52 L -5 52 L -9 60 Z" fill="#26215C"/></g>
    <g id="${p}legFront"><rect x="-9" y="24" width="18" height="32" rx="6" fill="#3C3489"/><path d="M 5 52 L 13 52 L 9 60 Z" fill="#26215C"/></g>
    <g id="${p}torso"><ellipse cx="0" cy="6" rx="15" ry="20" fill="#534AB7"/><ellipse cx="0" cy="12" rx="9" ry="10" fill="#AFA9EC"/></g>
    <g id="${p}armL"><path d="M -13 -2 L -26 6 L -14 10 Z" fill="#3C3489"/></g>
    <g id="${p}armR"><path d="M 13 -2 L 26 6 L 14 10 Z" fill="#3C3489"/></g>
    <g id="${p}head"><ellipse cx="0" cy="-20" rx="13" ry="13" fill="#534AB7"/>
      <path d="M -12 -18 Q -24 -20 -30 -28" stroke="#26215C" stroke-width="2" fill="none" stroke-linecap="round"/>
      <path d="M -12 -13 Q -24 -10 -30 -6" stroke="#26215C" stroke-width="2" fill="none" stroke-linecap="round"/>
      <circle cx="-5" cy="-22" r="3" fill="#fff"/><circle cx="5" cy="-22" r="3" fill="#fff"/>
      <circle cx="-5" cy="-22" r="1.4" fill="#000"/><circle cx="5" cy="-22" r="1.4" fill="#000"/>
      <path id="${p}mouth" d="M -7 -14 Q 0 -9 7 -14" fill="none" stroke="#26215C" stroke-width="2.5" stroke-linecap="round"/>
    </g>
  `; }

  function buildHorse(p){ return `
    <g id="${p}back"><path d="M -8 -18 Q -4 -34 6 -30 Q 0 -22 -4 -14 Z" fill="#5C3B1E"/><path d="M -14 6 Q -28 10 -24 24 Q -20 12 -10 12 Z" fill="#5C3B1E"/></g>
    <g id="${p}legBack"><rect x="-9" y="24" width="18" height="34" rx="4" fill="#8A5A2E"/><rect x="-12" y="52" width="10" height="8" rx="2" fill="#3B2711"/></g>
    <g id="${p}legFront"><rect x="-9" y="24" width="18" height="34" rx="4" fill="#8A5A2E"/><rect x="2" y="52" width="10" height="8" rx="2" fill="#3B2711"/></g>
    <g id="${p}torso"><path d="M -14 -6 L 14 -6 L 12 22 L -12 22 Z" fill="#8A5A2E"/><ellipse cx="0" cy="8" rx="7" ry="9" fill="#D9A066"/></g>
    <g id="${p}armL"><rect x="-19" y="-4" width="7" height="18" rx="2" fill="#8A5A2E"/><rect x="-20" y="12" width="9" height="7" rx="2" fill="#3B2711"/></g>
    <g id="${p}armR"><rect x="12" y="-4" width="7" height="18" rx="2" fill="#8A5A2E"/><rect x="11" y="12" width="9" height="7" rx="2" fill="#3B2711"/></g>
    <g id="${p}head"><path d="M -8 -32 Q 8 -34 10 -18 Q 8 -6 -2 -8 Q -12 -10 -12 -22 Z" fill="#8A5A2E"/>
      <path d="M -6 -34 L -4 -44 L 0 -34 Z" fill="#5C3B1E"/><path d="M 2 -34 L 4 -44 L 6 -34 Z" fill="#5C3B1E"/>
      <circle cx="-4" cy="-24" r="3" fill="#fff"/><circle cx="-4" cy="-24" r="1.4" fill="#000"/>
      <path id="${p}mouth" d="M 2 -12 L 10 -14 L 8 -8 Z" fill="#3B2711"/>
    </g>
  `; }

  function buildGunner(p){ return `
    <g id="${p}back"></g>
    <g id="${p}legBack"><rect x="-9" y="24" width="18" height="34" rx="4" fill="#141414"/><rect x="-12" y="52" width="10" height="8" rx="2" fill="#000"/></g>
    <g id="${p}legFront"><rect x="-9" y="24" width="18" height="34" rx="4" fill="#141414"/><rect x="2" y="52" width="10" height="8" rx="2" fill="#000"/></g>
    <g id="${p}torso"><path d="M -13 -6 L 13 -6 L 11 22 L -11 22 Z" fill="#6B4226"/><path d="M -4 -6 L -4 20 M 4 -6 L 4 20" stroke="#9B9B93" stroke-width="2" opacity="0.85"/><path d="M -13 -6 L -9 -3 L -13 2 Z" fill="#9B9B93"/><path d="M 13 -6 L 9 -3 L 13 2 Z" fill="#9B9B93"/></g>
    <circle cx="-14" cy="-4" r="5" fill="#6B4226"/><circle cx="14" cy="-4" r="5" fill="#6B4226"/>
    <g id="${p}armL"><rect x="-18" y="-4" width="7" height="17" rx="2" fill="#6B4226"/><rect x="-19" y="11" width="9" height="7" rx="2" fill="#D9A066"/></g>
    <g id="${p}armR"><rect x="11" y="-4" width="7" height="17" rx="2" fill="#6B4226"/><rect x="10" y="11" width="9" height="7" rx="2" fill="#D9A066"/>
      <g id="${p}axe" opacity="0"><g transform="translate(20,10)"><rect x="-9" y="-6" width="18" height="13" rx="2" fill="#2E2E2E"/><circle cx="0" cy="0" r="5" fill="#1A1A1A"/><circle cx="0" cy="0" r="3" fill="#7FA8D9"/><rect x="4" y="-9" width="6" height="4" rx="1" fill="#2E2E2E"/></g></g>
    </g>
    <rect x="-4" y="-12" width="8" height="8" fill="#D9A066"/>
    <g id="${p}head"><ellipse cx="0" cy="-20" rx="12" ry="13" fill="#D9A066"/>
      <path d="M -12 -16 Q -14 -4 -10 2 L -8 -12 Z" fill="#2E2118"/>
      <path d="M 12 -16 Q 14 -4 10 2 L 8 -12 Z" fill="#2E2118"/>
      <path d="M -12 -14 Q -13 -30 0 -31 Q 13 -30 12 -14 Q 12 -19 9 -18 Q 6 -22 3 -16 Q 0 -23 -3 -16 Q -6 -22 -9 -18 Q -12 -19 -12 -14 Z" fill="#241A12"/>
      <path d="M -7 -23 L -3 -20" stroke="#5C3B1E" stroke-width="2" stroke-linecap="round"/>
      <path d="M 7 -23 L 3 -20" stroke="#5C3B1E" stroke-width="2" stroke-linecap="round"/>
    </g>
  `; }

  function buildHero(p){ return `
    <g id="${p}back"></g>
    <g id="${p}legBack"><rect x="-9" y="24" width="18" height="34" rx="4" fill="#14203A"/><rect x="-9" y="24" width="18" height="6" fill="#E8792E"/><rect x="-12" y="52" width="10" height="8" rx="2" fill="#0A1226"/></g>
    <g id="${p}legFront"><rect x="-9" y="24" width="18" height="34" rx="4" fill="#14203A"/><rect x="-9" y="24" width="18" height="6" fill="#E8792E"/><rect x="2" y="52" width="10" height="8" rx="2" fill="#0A1226"/></g>
    <g id="${p}torso"><path d="M -13 -6 L 13 -6 L 11 22 L -11 22 Z" fill="#14203A"/><path d="M -10 -6 L 0 10 L 10 -6 Z" fill="#E8792E"/></g>
    <path d="M -13 -8 Q -23 -8 -22 2 Q -18 -3 -12 0 Z" fill="#14203A"/>
    <path d="M 13 -8 Q 23 -8 22 2 Q 18 -3 12 0 Z" fill="#14203A"/>
    <g id="${p}armL"><rect x="-18" y="-4" width="7" height="17" rx="2" fill="#14203A"/><rect x="-19" y="11" width="9" height="7" rx="2" fill="#2F6FE0"/></g>
    <g id="${p}armR"><rect x="11" y="-4" width="7" height="17" rx="2" fill="#14203A"/><rect x="10" y="11" width="9" height="7" rx="2" fill="#2F6FE0"/></g>
    <rect x="-4" y="-12" width="8" height="8" fill="#14203A"/>
    <g id="${p}head"><ellipse cx="0" cy="-20" rx="12" ry="13" fill="#14203A"/>
      <path d="M -7 -27 Q 0 -22 7 -27 Q 3 -34 0 -38 Q -3 -34 -7 -27 Z" fill="#E8792E"/>
      <path d="M -9 -22 Q 0 -18 9 -22 L 9 -18 Q 0 -14 -9 -18 Z" fill="#2F6FE0"/>
      <path id="${p}mouth" d="M -6 -22 L 0 -14 L 6 -22" fill="none" stroke="#E8792E" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
    </g>
  `; }

  const CHARS = {
    knight: { name:'อัศวิน', hp:'#444441', melee:'หมัดมืด', special:'ลำแสงมืด', beamColor:'#ffffff', fxColor:'#AFA9EC', dmgMelee:[8,14], dmgSpecial:[12,22], svg:buildKnight,
      mouthDefault:'M -6 -22 L 0 -14 L 6 -22', mouthOpen:'M -7 -19 L 0 -16 L 7 -19' },
    catfish: { name:'ปลาดุก', hp:'#0F6E56', melee:'ฟาดหนวด', special:'พ่นน้ำแรงดัน', beamColor:'#7FE0C0', fxColor:'#5DCAA5', dmgMelee:[8,14], dmgSpecial:[12,22], svg:buildCatfish,
      mouthDefault:'M -7 -14 Q 0 -9 7 -14', mouthOpen:'M -8 -14 Q 0 -5 8 -14' },
    horse: { name:'ม้า', hp:'#8A5A2E', melee:'เตะกีบ', special:'เสียงร้องกัมปนาท', beamColor:'#F0997B', fxColor:'#D9A066', dmgMelee:[9,15], dmgSpecial:[13,23], svg:buildHorse },
    gunner: { name:'มนุษย์', hp:'#6B4226', melee:'ตีด้วยกล้อง', special:'ถ่ายภาพ', beamColor:'#FFF7D6', fxColor:'#FFE9A3', dmgMelee:[7,12], dmgSpecial:[20,20], rangeSpecial:260, svg:buildGunner },
    hero: { name:'นักรบแสง', hp:'#2F6FE0', melee:'หมัดพลังงาน', special:'ลำแสงพิฆาต', beamColor:'#E8792E', fxColor:'#2F6FE0', dmgMelee:[8,14], dmgSpecial:[14,24], svg:buildHero,
      mouthDefault:'M -6 -22 L 0 -14 L 6 -22', mouthOpen:'M -7 -19 L 0 -16 L 7 -19' }
  };


  const MELEE_RANGE = 100, SPECIAL_RANGE = 140, MIN_GAP = 75;
  const scene = document.getElementById('scene');
  const beam = document.getElementById('beam');
  const charge = document.getElementById('charge');
  const fx = document.getElementById('fx');
  const log = document.getElementById('log');
  const restart = document.getElementById('restart');
  const selectScreen = document.getElementById('selectScreen');
  const gameScreen = document.getElementById('gameScreen');
  const titleScreen = document.getElementById('titleScreen');
  const modeScreen = document.getElementById('modeScreen');
  const startBtn = document.getElementById('startBtn');
  let gameMode = 'friend';
  let aiTimer = null;

  document.getElementById('playBtn').addEventListener('click', function(){
    titleScreen.style.display = 'none';
    modeScreen.style.display = 'block';
  });

  document.querySelectorAll('.modeBtn').forEach(function(btn){
    btn.addEventListener('click', function(){
      gameMode = btn.dataset.mode;
      document.getElementById('p2title').textContent = gameMode === 'bot' ? 'บอท (คู่ต่อสู้)' : 'ผู้เล่น 2';
      modeScreen.style.display = 'none';
      selectScreen.style.display = 'block';
    });
  });

  let sel = { p1:null, p2:null };
  document.querySelectorAll('.pick').forEach(btn=>{
    btn.addEventListener('click', function(){
      const pl = btn.dataset.p, c = btn.dataset.c;
      sel[pl] = c;
      document.querySelectorAll('.pick[data-p="'+pl+'"]').forEach(b=>b.classList.remove('selected'));
      btn.classList.add('selected');
      startBtn.disabled = !(sel.p1 && sel.p2);
    });
  });

  let P = null, over = true, moving = { p1:0, p2:0 };
  let hitFlag = { p1:0, p2:0 };
  let shakeT = 0, shakeMag = 0;
  let loopStarted = false;

  function el(id){ return document.getElementById(id); }

  function buildSlot(pl){
    document.getElementById(pl).innerHTML = CHARS[P[pl].char].svg(pl);
  }

  const MAX_HP = 300, MAX_STAGGER = 100;

  function setHp(){
    el('hp_p1').style.width = Math.max(P.p1.hp,0)/MAX_HP*100 + '%';
    el('hp_p2').style.width = Math.max(P.p2.hp,0)/MAX_HP*100 + '%';
    el('p1hpnum').textContent = Math.max(Math.round(P.p1.hp),0);
    el('p2hpnum').textContent = Math.max(Math.round(P.p2.hp),0);
  }

  function setStagger(){
    el('stg_p1').style.width = Math.min(P.p1.stagger,MAX_STAGGER) + '%';
    el('stg_p2').style.width = Math.min(P.p2.stagger,MAX_STAGGER) + '%';
  }

  function updateButtons(){
    el('p1m').disabled = over || P.p1.mcool || P.p1.cool;
    el('p1s').disabled = over || P.p1.cool || P.p1.mcool;
    el('p2m').disabled = over || P.p2.mcool || P.p2.cool;
    el('p2s').disabled = over || P.p2.cool || P.p2.mcool;
  }

  const stageScreen = document.getElementById('stageScreen');
  let selectedStage = 'forest';

  const STAGES = {
    forest: { sky:'#DCE8D5', ground:'#8FA876',
      decor:'<path d="M 30 180 L 40 130 L 50 180 Z" fill="#5C7A4A"/><path d="M 30 180 L 40 148 L 50 180 Z" fill="#6F9058"/><circle cx="40" cy="122" r="10" fill="#4A6339"/>' +
            '<path d="M 90 180 L 98 140 L 106 180 Z" fill="#5C7A4A"/><circle cx="98" cy="134" r="8" fill="#4A6339"/>' +
            '<path d="M 340 180 L 350 128 L 360 180 Z" fill="#5C7A4A"/><circle cx="350" cy="120" r="11" fill="#4A6339"/>' +
            '<path d="M 300 180 L 308 145 L 316 180 Z" fill="#5C7A4A"/><circle cx="308" cy="139" r="8" fill="#4A6339"/>' },
    city: { sky:'#D8DEE4', ground:'#A9A9A4',
      decor:'<rect x="14" y="20" width="34" height="160" fill="#8C8C90"/><rect x="20" y="30" width="7" height="7" fill="#D8DEE4"/><rect x="34" y="30" width="7" height="7" fill="#D8DEE4"/><rect x="20" y="46" width="7" height="7" fill="#D8DEE4"/><rect x="34" y="46" width="7" height="7" fill="#D8DEE4"/><rect x="20" y="62" width="7" height="7" fill="#D8DEE4"/><rect x="34" y="62" width="7" height="7" fill="#D8DEE4"/>' +
            '<rect x="58" y="70" width="26" height="110" fill="#9B9B95"/><rect x="64" y="80" width="6" height="6" fill="#D8DEE4"/><rect x="76" y="80" width="6" height="6" fill="#D8DEE4"/><rect x="64" y="94" width="6" height="6" fill="#D8DEE4"/><rect x="76" y="94" width="6" height="6" fill="#D8DEE4"/>' +
            '<rect x="316" y="10" width="38" height="170" fill="#8C8C90"/><rect x="323" y="20" width="7" height="7" fill="#D8DEE4"/><rect x="337" y="20" width="7" height="7" fill="#D8DEE4"/><rect x="323" y="36" width="7" height="7" fill="#D8DEE4"/><rect x="337" y="36" width="7" height="7" fill="#D8DEE4"/><rect x="323" y="52" width="7" height="7" fill="#D8DEE4"/><rect x="337" y="52" width="7" height="7" fill="#D8DEE4"/>' +
            '<rect x="286" y="60" width="24" height="120" fill="#9B9B95"/><rect x="292" y="70" width="6" height="6" fill="#D8DEE4"/><rect x="304" y="70" width="6" height="6" fill="#D8DEE4"/>' }
  };

  function applyStage(stage){
    const s = STAGES[stage] || STAGES.forest;
    el('skyRect').setAttribute('fill', s.sky);
    el('groundRect').setAttribute('fill', s.ground);
    el('bgDecor').innerHTML = s.decor;
  }

  document.querySelectorAll('.stageBtn').forEach(function(btn){
    btn.addEventListener('click', function(){
      selectedStage = btn.dataset.stage;
      stageScreen.style.display = 'none';
      startGame();
    });
  });

  startBtn.addEventListener('click', function(){
    selectScreen.style.display = 'none';
    stageScreen.style.display = 'block';
  });

  function startGame(){
    const charKeys = Object.keys(CHARS);
    if(!sel.p1) sel.p1 = charKeys[Math.floor(Math.random()*charKeys.length)];
    if(!sel.p2) sel.p2 = charKeys[Math.floor(Math.random()*charKeys.length)];
    el('p1').style.transform = ''; el('p1').style.opacity = '';
    el('p2').style.transform = ''; el('p2').style.opacity = '';
    applyStage(selectedStage);
    P = {
      p1: { x:80, hp:300, stagger:0, facing:1, char:sel.p1, cool:false, mcool:false },
      p2: { x:300, hp:300, stagger:0, facing:-1, char:sel.p2, cool:false, mcool:false }
    };
    try {
      buildSlot('p1'); buildSlot('p2');
    } catch(err) {
      console.error('buildSlot failed', err);
      if(!el('p1').innerHTML.trim()){ P.p1.char = 'knight'; buildSlot('p1'); }
      if(!el('p2').innerHTML.trim()){ P.p2.char = 'knight'; buildSlot('p2'); }
    }
    sel.p1 = P.p1.char; sel.p2 = P.p2.char;
    el('p1label').textContent = 'P1 ' + CHARS[sel.p1].name;
    el('p2label').textContent = 'P2 ' + CHARS[sel.p2].name;
    el('hp_p1').style.background = CHARS[sel.p1].hp;
    el('hp_p2').style.background = CHARS[sel.p2].hp;
    el('p1m').textContent = CHARS[sel.p1].melee;
    el('p1s').textContent = CHARS[sel.p1].special;
    el('p2m').textContent = CHARS[sel.p2].melee;
    el('p2s').textContent = CHARS[sel.p2].special;
    el('p1').setAttribute('transform','translate(80,130)');
    el('p2').setAttribute('transform','translate(300,130) scale(-1,1)');
    over = false;
    hitFlag = { p1:0, p2:0 };
    restart.style.display = 'none';
    log.textContent = 'เริ่ม! ' + CHARS[sel.p1].name + ' ปะทะ ' + CHARS[sel.p2].name;
    setHp(); setStagger(); updateButtons();
    selectScreen.style.display = 'none';
    stageScreen.style.display = 'none';
    gameScreen.style.display = 'block';
    document.querySelector('.grp.p2').style.display = gameMode === 'bot' ? 'none' : 'flex';
    document.querySelector('.hint').textContent = gameMode === 'bot'
      ? 'P1: A/D เดิน, G โจมตีประชิด, F ท่าไม้ตาย — บอทควบคุมฝั่งตรงข้ามเอง'
      : 'P1: A/D เดิน, G โจมตีประชิด, F ท่าไม้ตาย — P2: ลูกศร เดิน, Enter โจมตีประชิด, Shift ท่าไม้ตาย';
    if(aiTimer) { clearInterval(aiTimer); aiTimer = null; }
    if(gameMode === 'bot'){
      aiTimer = setInterval(aiTick, 450);
    }
    if(!loopStarted){ loopStarted = true; requestAnimationFrame(loop); }
  }

  function aiTick(){
    if(over || !P) return;
    const dist = Math.abs(P.p1.x - P.p2.x);
    const myRange = CHARS[P.p2.char].rangeSpecial || SPECIAL_RANGE;
    const canMelee = !P.p2.mcool && !P.p2.cool && dist <= MELEE_RANGE;
    const canSpecial = !P.p2.mcool && !P.p2.cool && dist <= myRange;
    if(canMelee && Math.random() < 0.55){ moving.p2 = 0; meleeAttack('p2'); return; }
    if(canSpecial && Math.random() < 0.5){ moving.p2 = 0; specialAttack('p2'); return; }
    if(dist > MELEE_RANGE - 15){
      moving.p2 = P.p1.x < P.p2.x ? -1 : 1;
    } else {
      moving.p2 = Math.random() < 0.35 ? (P.p1.x < P.p2.x ? 1 : -1) : 0;
    }
  }

  function burst(x, y, color, n){
    n = n || 8;
    for(let i=0;i<n;i++){
      const angle = (Math.PI*2/n)*i + Math.random()*0.3;
      const line = document.createElementNS(svgNS,'line');
      line.setAttribute('x1', x); line.setAttribute('y1', y);
      line.setAttribute('x2', x); line.setAttribute('y2', y);
      line.setAttribute('stroke', color); line.setAttribute('stroke-width', '3'); line.setAttribute('stroke-linecap', 'round');
      fx.appendChild(line);
      const dx = Math.cos(angle)*22, dy = Math.sin(angle)*22;
      let prog = 0;
      const anim = setInterval(function(){
        prog += 0.09;
        if(prog >= 1){ clearInterval(anim); if(fx.contains(line)) fx.removeChild(line); return; }
        line.setAttribute('x1', x + dx*prog*0.5); line.setAttribute('y1', y + dy*prog*0.5);
        line.setAttribute('x2', x + dx*prog); line.setAttribute('y2', y + dy*prog);
        line.setAttribute('opacity', 1-prog);
      }, 16);
    }
  }
  function slash(x, y, dir, color){
    const path = document.createElementNS(svgNS,'path');
    path.setAttribute('d', 'M ' + (x-14*dir) + ' ' + (y-10) + ' Q ' + x + ' ' + y + ' ' + (x+14*dir) + ' ' + (y+10));
    path.setAttribute('stroke', color); path.setAttribute('stroke-width', '4'); path.setAttribute('fill', 'none'); path.setAttribute('stroke-linecap', 'round');
    fx.appendChild(path);
    let op = 1;
    const anim = setInterval(function(){
      op -= 0.08;
      if(op <= 0){ clearInterval(anim); if(fx.contains(path)) fx.removeChild(path); return; }
      path.setAttribute('opacity', op);
    }, 16);
  }
  function impactStar(x, y, color){
    const star = document.createElementNS(svgNS,'path');
    const pts = [];
    for(let i=0;i<8;i++){ const a=(Math.PI*2/8)*i, r=i%2===0?10:4; pts.push((x+Math.cos(a)*r)+' '+(y+Math.sin(a)*r)); }
    star.setAttribute('d', 'M ' + pts.join(' L ') + ' Z');
    star.setAttribute('fill', color); star.setAttribute('opacity', '0.9');
    fx.appendChild(star);
    let s = 1, op = 0.9;
    const anim = setInterval(function(){
      s += 0.15; op -= 0.12;
      star.setAttribute('transform', 'translate(' + x + ',' + y + ') scale(' + s + ') translate(' + (-x) + ',' + (-y) + ')');
      star.setAttribute('opacity', Math.max(op,0));
      if(op <= 0){ clearInterval(anim); if(fx.contains(star)) fx.removeChild(star); }
    }, 16);
  }
  function shake(mag, dur){ shakeMag = mag; shakeT = dur; }

  function loop(t){
    if(!over && P){
      ['p1','p2'].forEach(function(pl){
        const other = pl==='p1' ? 'p2' : 'p1';
        const dir = moving[pl];
        const group = el(pl);
        const legBack = el(pl+'legBack'), legFront = el(pl+'legFront');
        const armL = el(pl+'armL'), armR = el(pl+'armR');
        const back = el(pl+'back'), torso = el(pl+'torso'), head = el(pl+'head');
        if(dir !== 0){
          let nx = P[pl].x + dir*2.2;
          if(pl==='p1') nx = Math.max(20, Math.min(nx, P.p2.x - MIN_GAP));
          else nx = Math.max(P.p1.x + MIN_GAP, Math.min(nx, 380));
          P[pl].x = nx;
          P[pl].facing = dir;
          const bob = Math.abs(Math.sin(t/90))*3;
          group.setAttribute('transform','translate(' + P[pl].x + ',' + (130-bob) + ') scale(' + dir + ',1)');
          const step = Math.sin(t/80);
          if(legBack) legBack.setAttribute('transform', 'rotate(' + (step*22) + ' 0 24)');
          if(legFront) legFront.setAttribute('transform', 'rotate(' + (-step*22) + ' 0 24)');
          if(!P[pl].mcool){
            if(armL) armL.setAttribute('transform', 'rotate(' + (-step*18) + ' -16 -4)');
            if(armR) armR.setAttribute('transform', 'rotate(' + (step*18) + ' 16 -4)');
          }
          if(back) back.setAttribute('transform', 'skewX(' + (-step*6-4) + ')');
        } else {
          if(legBack) legBack.removeAttribute('transform');
          if(legFront) legFront.removeAttribute('transform');
          const idle = Math.sin(t/500)*1.5;
          group.setAttribute('transform','translate(' + P[pl].x + ',' + (130+idle) + ') scale(' + P[pl].facing + ',1)');
          if(head) head.setAttribute('transform', 'translate(0,' + (Math.sin(t/700)*0.8) + ') rotate(' + (Math.sin(t/1100)*2) + ' 0 -14)');
          if(torso) torso.setAttribute('transform', 'scale(1,' + (1+Math.sin(t/450)*0.03) + ')');
          if(!P[pl].mcool){
            if(armL) armL.setAttribute('transform', 'rotate(' + (Math.sin(t/480)*4) + ' -16 -4)');
            if(armR) armR.setAttribute('transform', 'rotate(' + (-Math.sin(t/480)*4) + ' 16 -4)');
          }
          if(back) back.setAttribute('transform', 'skewX(' + (Math.sin(t/650)*3) + ')');
        }
        if(hitFlag[pl] > 0){ hitFlag[pl] -= 1; group.querySelector('#'+pl+'torso') && group.setAttribute('data-hit','1'); }
      });
      if(shakeT > 0){ shakeT -= 1; scene.style.transform = 'translate(' + (Math.random()*shakeMag-shakeMag/2) + 'px,' + (Math.random()*shakeMag-shakeMag/2) + 'px)'; }
      else scene.style.transform = 'translate(0,0)';
    }
    requestAnimationFrame(loop);
  }

  ['p1left','p1right','p2left','p2right'].forEach(function(id){
    document.getElementById(id).addEventListener('pointerdown', function(){
      if(over) return;
      if(id==='p1left') moving.p1=-1; if(id==='p1right') moving.p1=1;
      if(id==='p2left') moving.p2=-1; if(id==='p2right') moving.p2=1;
    });
    ['pointerup','pointerleave'].forEach(ev=>document.getElementById(id).addEventListener(ev, function(){
      if(id==='p1left'||id==='p1right') moving.p1=0;
      if(id==='p2left'||id==='p2right') moving.p2=0;
    }));
  });

  window.addEventListener('keydown', function(e){
    if(over || !P) return;
    const k = e.key.toLowerCase();
    if(k==='a') moving.p1=-1;
    if(k==='d') moving.p1=1;
    if(k==='g') meleeAttack('p1');
    if(k==='f') specialAttack('p1');
    if(gameMode === 'bot') return;
    if(k==='arrowleft') moving.p2=-1;
    if(k==='arrowright') moving.p2=1;
    if(k==='enter') meleeAttack('p2');
    if(e.key==='Shift') specialAttack('p2');
  });
  window.addEventListener('keyup', function(e){
    const k = e.key.toLowerCase();
    if(k==='a'||k==='d') moving.p1=0;
    if(k==='arrowleft'||k==='arrowright') moving.p2=0;
  });

  function playerFall(pl, dir){
    const group = el(pl);
    let ang = 0;
    const anim = setInterval(function(){
      ang += 6;
      group.style.transformOrigin = 'center';
      group.style.transform = 'rotate(' + (ang*dir) + 'deg)';
      group.style.opacity = Math.max(0.4, 1 - ang/150);
      if(ang >= 90) clearInterval(anim);
    }, 16);
  }
  function winPose(pl){
    const group = el(pl);
    let s = 0;
    const anim = setInterval(function(){
      s += 1;
      group.style.transform = 'translateY(' + (-Math.abs(Math.sin(s/8))*8) + 'px)';
      if(s >= 60){ clearInterval(anim); group.style.transform=''; }
    }, 16);
  }

  function endCheck(){
    if(P.p2.hp <= 0){ over = true; if(aiTimer){clearInterval(aiTimer); aiTimer=null;} log.textContent = 'P1 (' + CHARS[P.p1.char].name + ') ชนะ!'; playerFall('p2',1); winPose('p1'); shake(6,20); updateButtons(); restart.style.display='block'; return true; }
    if(P.p1.hp <= 0){ over = true; if(aiTimer){clearInterval(aiTimer); aiTimer=null;} log.textContent = (gameMode==='bot' ? 'บอท' : 'P2') + ' (' + CHARS[P.p2.char].name + ') ชนะ!'; playerFall('p1',-1); winPose('p2'); shake(6,20); updateButtons(); restart.style.display='block'; return true; }
    return false;
  }

  function meleeAttack(pl){
    if(over || P[pl].mcool || P[pl].cool) return;
    const other = pl==='p1' ? 'p2' : 'p1';
    const dist = Math.abs(P[other].x - P[pl].x);
    if(dist > MELEE_RANGE){ log.textContent = (pl==='p1'?'P1':'P2') + ': เข้าใกล้อีกนิดถึงจะโจมตีโดน'; return; }
    P[pl].mcool = true; updateButtons();
    const armR = el(pl+'armR'), mouth = el(pl+'mouth'), axe = el(pl+'axe');
    const facing = P[pl].facing;
    const cdef = CHARS[P[pl].char];
    if(armR) armR.setAttribute('transform','translate(' + (facing*14) + ',0) rotate(' + (facing*-8) + ' ' + (facing>0?16:-16) + ' -4)');
    if(mouth && cdef.mouthOpen) mouth.setAttribute('d', cdef.mouthOpen);
    if(axe) axe.setAttribute('opacity','1');
    setTimeout(function(){
      if(armR) armR.removeAttribute('transform');
      if(mouth && cdef.mouthDefault) mouth.setAttribute('d', cdef.mouthDefault);
      const hitX = P[pl].x + facing*40;
      slash(hitX, 122, facing, '#ffffff');
      impactStar(hitX, 122, CHARS[P[pl].char].fxColor);
      shake(3,8);
      const dmg = 1;
      P[other].hp -= dmg; hitFlag[other] = 12;
      const wasFull = P[other].stagger >= MAX_STAGGER;
      if(wasFull){
        P[other].stagger = 0;
        P[pl].cool = false;
        knockdown(other);
        log.textContent = (pl==='p1'?'P1 ':'P2 ') + CHARS[P[pl].char].name + ' ทำให้คู่ต่อสู้ล้ม! ใช้ท่าไม้ตายได้ทันที';
      } else {
        P[other].stagger = Math.min(P[other].stagger + 2, MAX_STAGGER);
        log.textContent = (pl==='p1'?'P1 ':'P2 ') + CHARS[P[pl].char].name + ' ใช้' + CHARS[P[pl].char].melee + '! -' + dmg;
      }
      setHp(); setStagger();
      if(endCheck()) return;
      setTimeout(function(){ P[pl].mcool = false; updateButtons(); if(axe) axe.setAttribute('opacity','0'); }, 380);
    }, 140);
  }

  function knockdown(pl){
    const group = el(pl);
    let ang = 0;
    const anim = setInterval(function(){
      ang += 8;
      group.style.transformOrigin = 'center';
      group.style.transform = 'rotate(' + (ang*P[pl].facing*-1) + 'deg) translateY(' + Math.min(ang*0.3,14) + 'px)';
      if(ang >= 80) clearInterval(anim);
    }, 16);
    setTimeout(function(){
      group.style.transform = '';
    }, 900);
  }

  function specialAttack(pl){
    if(over || P[pl].cool || P[pl].mcool) return;
    const other = pl==='p1' ? 'p2' : 'p1';
    const dist = Math.abs(P[other].x - P[pl].x);
    const myRange = CHARS[P[pl].char].rangeSpecial || SPECIAL_RANGE;
    if(dist > myRange){ log.textContent = (pl==='p1'?'P1':'P2') + ': เข้าใกล้อีกนิดถึงจะใช้ท่าไม้ตายโดน'; return; }
    P[pl].cool = true; updateButtons();
    const armL = el(pl+'armL'), armR = el(pl+'armR'), mouth = el(pl+'mouth'), gun = el(pl+'gun'), axe = el(pl+'axe');
    const facing = P[pl].facing;
    const cdef = CHARS[P[pl].char];
    if(mouth && cdef.mouthOpen) mouth.setAttribute('d', cdef.mouthOpen);
    if(gun) gun.setAttribute('opacity','1');
    if(axe) axe.setAttribute('opacity','1');
    if(armL) armL.setAttribute('transform','translate(' + (-2*facing) + ',-6) rotate(' + (-20*facing) + ')');
    if(armR) armR.setAttribute('transform','translate(' + (2*facing) + ',-6) rotate(' + (20*facing) + ')');
    charge.setAttribute('cx', P[pl].x); charge.setAttribute('cy', 120); charge.setAttribute('fill', CHARS[P[pl].char].fxColor); charge.setAttribute('opacity','0.85');
    let r = 0;
    const gi = setInterval(function(){ r += 1; charge.setAttribute('r', r); }, 15);
    setTimeout(function(){
      clearInterval(gi);
      charge.setAttribute('opacity','0'); charge.setAttribute('r','0');
      if(armL) armL.removeAttribute('transform');
      if(armR) armR.removeAttribute('transform');
      if(mouth && cdef.mouthDefault) mouth.setAttribute('d', cdef.mouthDefault);
      beam.setAttribute('stroke', CHARS[P[pl].char].beamColor);
      beam.setAttribute('x1', P[pl].x); beam.setAttribute('y1', 120);
      beam.setAttribute('x2', P[other].x); beam.setAttribute('y2', 130);
      beam.setAttribute('opacity','1');
      setTimeout(function(){
        beam.setAttribute('opacity','0');
        burst(P[other].x, 128, CHARS[P[pl].char].fxColor, 10);
        impactStar(P[other].x, 128, '#ffffff');
        shake(4,10);
        const [lo,hi] = CHARS[P[pl].char].dmgSpecial;
        const dmg = Math.round(lo + Math.random()*(hi-lo));
        P[other].hp -= dmg; hitFlag[other] = 12;
        setHp();
        log.textContent = (pl==='p1'?'P1 ':'P2 ') + CHARS[P[pl].char].name + ' ใช้' + CHARS[P[pl].char].special + '! -' + dmg;
        if(endCheck()) return;
        setTimeout(function(){ P[pl].cool = false; updateButtons(); if(gun) gun.setAttribute('opacity','0'); if(axe) axe.setAttribute('opacity','0'); }, 500);
      }, 200);
    }, 450);
  }

  el('p1m').addEventListener('click', ()=>meleeAttack('p1'));
  el('p1s').addEventListener('click', ()=>specialAttack('p1'));
  el('p2m').addEventListener('click', ()=>meleeAttack('p2'));
  el('p2s').addEventListener('click', ()=>specialAttack('p2'));

  restart.addEventListener('click', function(){
    if(aiTimer){ clearInterval(aiTimer); aiTimer = null; }
    modeScreen.style.display = 'block';
    selectScreen.style.display = 'none';
    gameScreen.style.display = 'none';
    over = true;
    el('p1').style.transform=''; el('p1').style.opacity='';
    el('p2').style.transform=''; el('p2').style.opacity='';
  });
})();
</script>
</body>
</html>
