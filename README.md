<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Math</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}

/* ── THEMES ── */
[data-theme="dark"]{
  --bg:#0d0f14;--surface:#13161c;--card:#1a1d25;--border:#252830;
  --text:#e8eaf0;--muted:#7a7f8e;--sub:#444854;
  --acc:#5b8df5;--acc-dim:#172040;--acc-txt:#8db4ff;
  --suc:#2ecc8a;--suc-dim:#0a2518;--suc-txt:#60e8b0;
  --warn:#f0a020;--warn-dim:#281a04;--warn-txt:#ffbe55;
  --dan:#e04f4f;--dan-dim:#280d0d;--dan-txt:#ff8080;
}
[data-theme="midnight"]{
  --bg:#080c14;--surface:#0e1420;--card:#131c2c;--border:#1c2840;
  --text:#c8d8f0;--muted:#5a7090;--sub:#2a3850;
  --acc:#3a7ef5;--acc-dim:#0d1f40;--acc-txt:#70a8ff;
  --suc:#1acc7a;--suc-dim:#062016;--suc-txt:#40e89a;
  --warn:#e09010;--warn-dim:#201604;--warn-txt:#f0b840;
  --dan:#d04040;--dan-dim:#200808;--dan-txt:#f07070;
}
[data-theme="neon"]{
  --bg:#070a0e;--surface:#0d1018;--card:#111520;--border:#1a2030;
  --text:#e0f0ff;--muted:#4a6080;--sub:#283040;
  --acc:#00d4ff;--acc-dim:#001828;--acc-txt:#60e8ff;
  --suc:#00ff88;--suc-dim:#002018;--suc-txt:#40ffaa;
  --warn:#ffaa00;--warn-dim:#201400;--warn-txt:#ffcc40;
  --dan:#ff2244;--dan-dim:#200010;--dan-txt:#ff6080;
}
[data-theme="forest"]{
  --bg:#0a110a;--surface:#0f180f;--card:#141f14;--border:#1e2e1e;
  --text:#d0e8c8;--muted:#5a7850;--sub:#2e4028;
  --acc:#4acc70;--acc-dim:#0a2010;--acc-txt:#80e898;
  --suc:#80e060;--suc-dim:#102008;--suc-txt:#a8f088;
  --warn:#d4a020;--warn-dim:#201800;--warn-txt:#f0c840;
  --dan:#e04040;--dan-dim:#280808;--dan-txt:#ff8080;
}
[data-theme="sunset"]{
  --bg:#120810;--surface:#1a0e18;--card:#221420;--border:#301a2c;
  --text:#f0d8e8;--muted:#906080;--sub:#502840;
  --acc:#e060c0;--acc-dim:#280820;--acc-txt:#f090d8;
  --suc:#60d890;--suc-dim:#082018;--suc-txt:#90f0b0;
  --warn:#f0a030;--warn-dim:#281400;--warn-txt:#ffc860;
  --dan:#f04060;--dan-dim:#280808;--dan-txt:#ff8090;
}
[data-theme="light"]{
  --bg:#f0f2f6;--surface:#ffffff;--card:#ffffff;--border:#dde1ea;
  --text:#1a1d26;--muted:#7a8090;--sub:#b0b5c0;
  --acc:#4a7ef0;--acc-dim:#e8f0ff;--acc-txt:#2a5ed8;
  --suc:#18b870;--suc-dim:#e0f8ee;--suc-txt:#0a8050;
  --warn:#d08010;--warn-dim:#fff4e0;--warn-txt:#a06000;
  --dan:#d83030;--dan-dim:#ffe8e8;--dan-txt:#a01818;
}

html,body{height:100%;background:var(--bg);color:var(--text);font-family:'Segoe UI',system-ui,sans-serif;font-size:14px;transition:background .3s,color .3s;}

#app{display:grid;grid-template-columns:175px 1fr;height:100vh;overflow:hidden;}
.sidebar{background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;padding:16px 0;overflow-y:auto;transition:background .3s,border-color .3s;}
.main{overflow-y:auto;background:var(--bg);padding:20px;transition:background .3s;}

.logo{display:flex;align-items:center;gap:9px;padding:0 13px 15px;border-bottom:1px solid var(--border);margin-bottom:10px;}
.logo-dot{width:30px;height:30px;border-radius:8px;background:var(--acc);display:flex;align-items:center;justify-content:center;font-size:16px;}
.logo-name{font-size:15px;font-weight:700;letter-spacing:-.3px;}
.logo-sub{font-size:10px;color:var(--muted);}
.nav-sec{padding:12px 13px 4px;font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.1em;text-transform:uppercase;}
.nav-item{display:flex;align-items:center;gap:9px;padding:8px 13px;cursor:pointer;color:var(--muted);border-left:2px solid transparent;font-size:13px;transition:all .1s;user-select:none;}
.nav-item:hover{color:var(--text);background:rgba(128,128,128,.05);}
.nav-item.active{color:var(--acc-txt);border-left-color:var(--acc);background:var(--acc-dim);}
.nav-item svg{width:15px;height:15px;flex-shrink:0;}
.sb-bottom{margin-top:auto;padding:12px 13px;border-top:1px solid var(--border);font-size:12px;color:var(--sub);}
.sb-bottom strong{color:var(--warn-txt);}

.view{display:none;}
.view.active{display:block;animation:pop .12s ease;}
@keyframes pop{from{opacity:0;transform:translateY(3px)}to{opacity:1;transform:none}}

.topbar{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:18px;gap:12px;}
.topbar h1{font-size:20px;font-weight:700;letter-spacing:-.3px;}
.topbar-sub{font-size:12px;color:var(--muted);margin-top:2px;}
.badge{display:inline-block;padding:3px 9px;border-radius:6px;font-size:11px;font-weight:700;}
.badge-suc{background:var(--suc-dim);color:var(--suc-txt);}
.badge-dan{background:var(--dan-dim);color:var(--dan-txt);}
.badge-warn{background:var(--warn-dim);color:var(--warn-txt);}
.badge-acc{background:var(--acc-dim);color:var(--acc-txt);}
.btn{padding:7px 13px;border-radius:6px;border:1px solid var(--border);background:var(--card);color:var(--muted);font-size:12px;cursor:pointer;font-family:inherit;transition:all .1s;display:inline-flex;align-items:center;gap:5px;}
.btn:hover{color:var(--text);border-color:var(--muted);}
.btn-acc{background:var(--acc);color:#fff;border-color:var(--acc);}
.btn-acc:hover{opacity:.88;color:#fff;}
.btn-lg{padding:11px 20px;font-size:14px;font-weight:600;border-radius:8px;}
.card{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:15px;transition:background .3s,border-color .3s;}
.card-title{font-size:13px;font-weight:700;margin-bottom:12px;display:flex;align-items:center;justify-content:space-between;}
.card-title span{font-size:11px;color:var(--muted);font-weight:400;}
.metrics{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:13px;}
.metric{background:var(--card);border:1px solid var(--border);border-radius:9px;padding:12px;transition:background .3s,border-color .3s;}
.metric-label{font-size:10px;color:var(--muted);margin-bottom:4px;font-weight:600;text-transform:uppercase;letter-spacing:.05em;}
.metric-value{font-size:22px;font-weight:700;}
.metric-sub{font-size:11px;color:var(--muted);margin-top:3px;}
.g2{display:grid;grid-template-columns:1fr 1fr;gap:11px;margin-bottom:11px;}
.g32{display:grid;grid-template-columns:2fr 1fr;gap:11px;margin-bottom:11px;}
.bar-row{display:flex;align-items:center;gap:9px;margin-bottom:8px;}
.bar-label{font-size:12px;color:var(--muted);width:70px;flex-shrink:0;text-align:right;}
.bar-track{flex:1;height:5px;background:var(--border);border-radius:99px;overflow:hidden;}
.bar-fill{height:100%;border-radius:99px;}
.bar-pct{font-size:11px;width:30px;text-align:right;}
.sw-row{display:flex;align-items:center;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);}
.sw-row:last-child{border-bottom:none;}
.sw-left{display:flex;align-items:center;gap:8px;}
.sw-icon{width:26px;height:26px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:14px;}
.tabs{display:flex;gap:3px;margin-bottom:13px;background:var(--surface);border-radius:7px;padding:3px;flex-wrap:wrap;}
.tab{padding:6px 13px;border-radius:5px;font-size:12px;cursor:pointer;color:var(--muted);transition:all .1s;}
.tab:hover{color:var(--text);}
.tab.active{background:var(--card);color:var(--text);font-weight:600;}
.hist-table{width:100%;border-collapse:collapse;}
.hist-table th{font-size:10px;color:var(--sub);font-weight:700;text-align:left;padding:0 9px 7px;text-transform:uppercase;letter-spacing:.06em;}
.hist-table td{font-size:12px;color:var(--muted);padding:8px 9px;border-top:1px solid var(--border);}
.hist-table tr:hover td{background:rgba(128,128,128,.04);}
.pill{display:inline-block;padding:2px 7px;border-radius:5px;font-size:11px;font-weight:600;}
.setting-row{display:flex;align-items:center;justify-content:space-between;padding:12px 0;border-bottom:1px solid var(--border);}
.setting-row:last-child{border-bottom:none;}
.setting-label{font-size:13px;font-weight:500;}
.setting-sub{font-size:11px;color:var(--muted);margin-top:2px;}
.toggle{width:36px;height:20px;border-radius:99px;background:var(--border);position:relative;cursor:pointer;transition:background .18s;flex-shrink:0;}
.toggle.on{background:var(--acc);}
.toggle-knob{width:14px;height:14px;border-radius:50%;background:#fff;position:absolute;top:3px;left:3px;transition:left .18s;}
.toggle.on .toggle-knob{left:19px;}
.sel{background:var(--surface);border:1px solid var(--border);color:var(--text);border-radius:5px;padding:5px 8px;font-size:12px;font-family:inherit;cursor:pointer;}
.inp{background:var(--surface);border:1px solid var(--border);color:var(--text);border-radius:6px;padding:7px 11px;font-size:13px;font-family:inherit;width:100%;outline:none;}
.inp:focus{border-color:var(--acc);}

#toast{position:fixed;bottom:18px;right:18px;background:var(--card);border:1px solid var(--border);border-radius:8px;padding:9px 15px;font-size:13px;opacity:0;pointer-events:none;transition:opacity .2s;z-index:999;max-width:260px;}
#toast.show{opacity:1;}

/* ══ PLAY ══ */
#view-play{padding:0;}
#game-wrap{height:100%;display:flex;flex-direction:column;}
#menu-screen{padding:20px;animation:pop .12s ease;}
#menu-screen h1{font-size:24px;font-weight:800;letter-spacing:-.5px;margin-bottom:3px;}
.mode-grid{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:16px;}
.mode-card{background:var(--card);border:2px solid var(--border);border-radius:10px;padding:14px;cursor:pointer;transition:all .12s;text-align:left;}
.mode-card:hover{border-color:var(--acc-txt);background:var(--acc-dim);}
.mode-card.sel{border-color:var(--acc);background:var(--acc-dim);}
.mode-icon{font-size:22px;margin-bottom:7px;}
.mode-name{font-size:14px;font-weight:700;color:var(--text);}
.mode-desc{font-size:11px;color:var(--muted);margin-top:2px;}
.diff-chips{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:13px;}
.diff-chip{padding:5px 12px;border-radius:6px;border:1px solid var(--border);background:var(--card);color:var(--muted);font-size:12px;cursor:pointer;transition:all .1s;}
.diff-chip:hover{border-color:var(--acc-txt);color:var(--acc-txt);}
.diff-chip.sel{border-color:var(--acc);color:var(--acc-txt);background:var(--acc-dim);font-weight:700;}
.diff-info{background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:11px 14px;margin-bottom:16px;font-size:12px;color:var(--muted);line-height:1.6;}

#countdown-screen{display:none;flex:1;align-items:center;justify-content:center;flex-direction:column;gap:6px;}
#countdown-num{font-size:100px;font-weight:800;color:var(--acc-txt);letter-spacing:-4px;}

#game-screen{display:none;flex-direction:column;padding:16px;flex:1;}
.match-timer-wrap{position:relative;height:10px;background:var(--border);border-radius:99px;margin-bottom:16px;overflow:hidden;}
#match-bar{height:100%;border-radius:99px;background:var(--suc);transition:width .25s linear,background .4s;}
.match-timer-label{position:absolute;right:0;top:-18px;font-size:11px;color:var(--muted);}
#match-time-left{font-weight:700;color:var(--text);}
.game-hud{display:flex;align-items:center;gap:8px;margin-bottom:10px;flex-wrap:wrap;}
.hud-pill{background:var(--surface);border:1px solid var(--border);border-radius:6px;padding:3px 10px;font-size:12px;color:var(--muted);}
.hud-pill strong{color:var(--text);}
.strikes-wrap{display:flex;gap:5px;align-items:center;margin-left:auto;}
.strike-dot{width:12px;height:12px;border-radius:50%;border:1.5px solid var(--dan);background:transparent;transition:background .15s;}
.strike-dot.filled{background:var(--dan);}
.scoreboard{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:12px;}
.score-box{background:var(--surface);border:1px solid var(--border);border-radius:9px;padding:11px;text-align:center;}
.score-box.you{border-color:var(--acc-dim);}
.score-box .slabel{font-size:11px;color:var(--muted);margin-bottom:3px;font-weight:600;}
.score-box .sval{font-size:28px;font-weight:800;}
.bot-race{margin-bottom:12px;}
.bot-race-label{display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin-bottom:4px;}
.bot-race-label .bot-name{display:flex;align-items:center;gap:5px;}
.bot-pulse{width:7px;height:7px;border-radius:50%;background:var(--suc);animation:pulse 1s infinite;}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.25}}
.bot-track{height:5px;background:var(--border);border-radius:99px;overflow:hidden;}
#bot-progress{height:100%;border-radius:99px;background:var(--dan);transition:width .3s ease;}
#question{font-size:38px;font-weight:800;text-align:center;padding:14px 0 6px;letter-spacing:-1px;min-height:74px;}
#hint{text-align:center;font-size:12px;color:var(--sub);margin-bottom:8px;min-height:18px;}
#feedback{height:24px;text-align:center;font-size:13px;font-weight:600;margin-bottom:8px;}
#answer-input{display:block;width:100%;padding:10px 15px;font-size:22px;font-family:inherit;font-weight:700;border-radius:8px;border:2px solid var(--border);background:var(--surface);color:var(--text);text-align:center;outline:none;margin-bottom:10px;transition:border-color .12s,box-shadow .12s;}
#answer-input:focus{border-color:var(--acc);box-shadow:0 0 0 3px rgba(91,141,245,.12);}
#answer-input.wrong{border-color:var(--dan);box-shadow:0 0 0 3px rgba(224,79,79,.12);animation:shake .28s;}
#answer-input.right{border-color:var(--suc);box-shadow:0 0 0 3px rgba(46,204,138,.12);}
@keyframes shake{0%,100%{transform:translateX(0)}25%{transform:translateX(-6px)}75%{transform:translateX(6px)}}
.game-btns{display:flex;gap:8px;}

#result-screen{display:none;padding:20px;animation:pop .18s ease;}
.result-big{font-size:44px;font-weight:800;text-align:center;margin:8px 0 3px;letter-spacing:-1px;}
.result-sub{text-align:center;color:var(--muted);font-size:14px;margin-bottom:18px;}
.res-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:14px;}
.res-stat{background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:11px;text-align:center;}
.res-stat .rl{font-size:10px;color:var(--muted);font-weight:700;text-transform:uppercase;letter-spacing:.05em;}
.res-stat .rv{font-size:22px;font-weight:800;margin-top:3px;}
.res-btns{display:flex;gap:8px;margin-bottom:14px;}
.pb-flash{background:linear-gradient(135deg,var(--warn-dim),rgba(40,26,4,.8));border:1px solid var(--warn);border-radius:8px;padding:10px 14px;text-align:center;font-size:13px;color:var(--warn-txt);font-weight:600;margin-bottom:14px;animation:glow 1.5s ease infinite alternate;}
@keyframes glow{from{box-shadow:0 0 6px rgba(240,160,32,.2)}to{box-shadow:0 0 16px rgba(240,160,32,.5)}}

.breakdown-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.breakdown-card{background:var(--surface);border:1px solid var(--border);border-radius:9px;padding:12px;}
.breakdown-title{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.07em;margin-bottom:10px;display:flex;align-items:center;gap:6px;}
.qrow{display:flex;align-items:center;justify-content:space-between;padding:6px 0;border-bottom:1px solid var(--border);gap:8px;}
.qrow:last-child{border-bottom:none;}
.qrow-q{font-size:13px;font-weight:700;color:var(--text);flex:1;}
.qrow-badge{font-size:11px;font-weight:700;padding:2px 7px;border-radius:5px;flex-shrink:0;}
.qrow-missed{background:var(--dan-dim);color:var(--dan-txt);}
.qrow-fast{background:var(--suc-dim);color:var(--suc-txt);}

/* discord webhook status */
.webhook-status{display:flex;align-items:center;gap:6px;font-size:11px;margin-top:8px;}
.webhook-dot{width:7px;height:7px;border-radius:50%;background:var(--sub);}
.webhook-dot.ok{background:var(--suc);}
.webhook-dot.err{background:var(--dan);}

/* theme swatches */
.theme-grid{display:flex;flex-wrap:wrap;gap:8px;margin-top:6px;}
.theme-swatch{width:32px;height:32px;border-radius:8px;cursor:pointer;border:2px solid transparent;transition:all .12s;position:relative;}
.theme-swatch:hover{transform:scale(1.1);}
.theme-swatch.active{border-color:var(--text);box-shadow:0 0 0 2px var(--acc);}

/* analytics question heatmap */
.qheat-row{display:flex;align-items:center;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--border);gap:8px;}
.qheat-row:last-child{border-bottom:none;}
.qheat-q{font-size:13px;font-weight:700;flex:1;}
.qheat-bar-wrap{width:80px;height:5px;background:var(--border);border-radius:99px;overflow:hidden;}
.qheat-bar{height:100%;border-radius:99px;}
.qheat-count{font-size:11px;width:28px;text-align:right;}
</style>
</head>
<body>
<div id="toast"></div>
<div id="app">

<nav class="sidebar">
  <div class="logo">
    <div class="logo-dot">⚡</div>
    <div><div class="logo-name">MathBattle</div><div class="logo-sub">vs the bot</div></div>
  </div>
  <div class="nav-sec">Play</div>
  <div class="nav-item active" data-view="play">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polygon points="5 3 19 12 5 21 5 3"/></svg>Play
  </div>
  <div class="nav-sec">Stats</div>
  <div class="nav-item" data-view="dashboard">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>Dashboard
  </div>
  <div class="nav-item" data-view="analytics">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg>Analytics
  </div>
  <div class="nav-item" data-view="history">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="9"/><polyline points="12 7 12 12 15 15"/></svg>History
  </div>
  <div class="nav-sec">Other</div>
  <div class="nav-item" data-view="settings">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l-.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>Settings
  </div>
  <div class="sb-bottom">🏆 Best: <strong id="sb-best">—</strong> pts</div>
</nav>

<main class="main">

  <!-- PLAY -->
  <div class="view active" id="view-play">
    <div id="game-wrap">
      <div id="menu-screen">
        <h1>⚡ Math Battle</h1>
        <p style="font-size:13px;color:var(--muted);margin-bottom:18px;">45 seconds. 3 strikes. Beat the bot or go home.</p>
        <div style="font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.09em;text-transform:uppercase;margin-bottom:7px;">Mode</div>
        <div class="mode-grid">
          <div class="mode-card sel" data-mode="addition"><div class="mode-icon">➕</div><div class="mode-name">Addition</div><div class="mode-desc">Fast arithmetic</div></div>
          <div class="mode-card" data-mode="multiplication"><div class="mode-icon">✖️</div><div class="mode-name">Multiplication</div><div class="mode-desc">Times tables & beyond</div></div>
          <div class="mode-card" data-mode="fractions"><div class="mode-icon">➗</div><div class="mode-name">Fractions</div><div class="mode-desc">Simplify, add, divide</div></div>
          <div class="mode-card" data-mode="variation"><div class="mode-icon">🎲</div><div class="mode-name">Variation</div><div class="mode-desc">Everything mixed</div></div>
        </div>
        <div style="font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.09em;text-transform:uppercase;margin-bottom:7px;">Difficulty</div>
        <div class="diff-chips" id="diff-chips"></div>
        <div class="diff-info" id="diff-info"></div>
        <button class="btn btn-acc btn-lg" style="width:100%;" id="start-btn">
          <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polygon points="5 3 19 12 5 21 5 3"/></svg>Start match
        </button>
      </div>

      <div id="countdown-screen" style="display:none;flex:1;align-items:center;justify-content:center;flex-direction:column;gap:5px;">
        <div style="font-size:14px;color:var(--muted);font-weight:600;">GET READY</div>
        <div id="countdown-num"></div>
        <div id="countdown-bot-warn" style="font-size:12px;color:var(--dan-txt);margin-top:4px;"></div>
      </div>

      <div id="game-screen" style="display:none;flex-direction:column;flex:1;">
        <div class="game-hud">
          <div class="hud-pill"><strong id="hud-mode"></strong></div>
          <div class="hud-pill"><strong id="hud-diff"></strong></div>
          <div class="hud-pill">Q#<strong id="hud-q">1</strong></div>
          <div class="strikes-wrap" id="strikes-wrap"></div>
        </div>
        <div class="match-timer-wrap">
          <div class="match-timer-label"><span id="match-time-left">45</span>s left</div>
          <div id="match-bar" style="width:100%;"></div>
        </div>
        <div class="scoreboard">
          <div class="score-box"><div class="slabel">🤖 Bot</div><div class="sval" id="bot-score">0</div></div>
          <div class="score-box you"><div class="slabel">⚡ You</div><div class="sval" id="player-score">0</div></div>
        </div>
        <div class="bot-race">
          <div class="bot-race-label">
            <div class="bot-name"><div class="bot-pulse" id="bot-pulse"></div><span id="bot-status">Bot solving…</span></div>
            <span id="bot-speed-label" style="color:var(--dan-txt);"></span>
          </div>
          <div class="bot-track"><div id="bot-progress" style="width:0%;"></div></div>
        </div>
        <div id="question"></div>
        <div id="hint"></div>
        <div id="feedback"></div>
        <input type="text" id="answer-input" placeholder="answer…" autocomplete="off" inputmode="decimal"/>
        <div class="game-btns">
          <button class="btn btn-acc" style="flex:1;justify-content:center;font-size:14px;font-weight:700;" onclick="submitAnswer()">Submit</button>
          <button class="btn" onclick="endGame('quit')" style="color:var(--muted);">Quit</button>
        </div>
        <div style="text-align:center;font-size:11px;color:var(--sub);margin-top:7px;">Enter to submit</div>
      </div>

      <div id="result-screen" style="display:none;">
        <div class="result-big" id="res-title"></div>
        <div class="result-sub" id="res-sub"></div>
        <div id="pb-banner" style="display:none;" class="pb-flash">🔥 New personal best!</div>
        <div class="res-stats">
          <div class="res-stat"><div class="rl">Your score</div><div class="rv" id="rs-player"></div></div>
          <div class="res-stat"><div class="rl">Bot score</div><div class="rv" id="rs-bot"></div></div>
          <div class="res-stat"><div class="rl">Accuracy</div><div class="rv" id="rs-acc"></div></div>
          <div class="res-stat"><div class="rl">Questions</div><div class="rv" id="rs-q"></div></div>
          <div class="res-stat"><div class="rl">Avg speed</div><div class="rv" id="rs-speed"></div></div>
          <div class="res-stat"><div class="rl">Strikes</div><div class="rv" id="rs-strikes"></div></div>
        </div>
        <div class="res-btns">
          <button class="btn btn-acc btn-lg" style="flex:1;justify-content:center;" onclick="playAgain()">Play again</button>
          <button class="btn btn-lg" style="flex:1;justify-content:center;" onclick="showMenu()">Change mode</button>
        </div>
        <div id="discord-result" style="font-size:11px;color:var(--muted);text-align:center;margin-bottom:10px;"></div>
        <div class="breakdown-grid" id="breakdown-grid"></div>
      </div>
    </div>
  </div>

  <!-- DASHBOARD -->
  <div class="view" id="view-dashboard">
    <div class="topbar"><div><h1>Dashboard</h1><div class="topbar-sub">Your numbers, all time</div></div><span class="badge badge-warn" id="db-streak">—</span></div>
    <div class="metrics">
      <div class="metric"><div class="metric-label">Games</div><div class="metric-value" id="stat-total">0</div><div class="metric-sub">all time</div></div>
      <div class="metric"><div class="metric-label">Win rate</div><div class="metric-value" id="stat-winrate" style="color:var(--suc-txt);">—</div><div class="metric-sub">vs bot</div></div>
      <div class="metric"><div class="metric-label">Best score</div><div class="metric-value" id="stat-best" style="color:var(--warn-txt);">—</div><div class="metric-sub">questions won</div></div>
      <div class="metric"><div class="metric-label">Accuracy</div><div class="metric-value" id="stat-acc">—</div><div class="metric-sub">correct answers</div></div>
    </div>
    <div class="g32">
      <div class="card"><div class="card-title">Accuracy by mode</div><div id="mode-acc-bars"><div style="color:var(--muted);font-size:13px;">Play a game to see stats.</div></div></div>
      <div class="card"><div class="card-title">Quick facts</div>
        <div class="sw-row"><div>Best score</div><div id="qs-best" style="font-weight:700;color:var(--warn-txt);">—</div></div>
        <div class="sw-row"><div>Bot beaten</div><div id="qs-wins" style="font-weight:700;color:var(--suc-txt);">—</div></div>
        <div class="sw-row"><div>Fastest ans</div><div id="qs-fastest" style="font-weight:700;color:var(--acc-txt);">—</div></div>
        <div class="sw-row"><div>Fav mode</div><div id="qs-fav" style="font-weight:700;">—</div></div>
      </div>
    </div>
    <div class="g2">
      <div class="card"><div class="card-title">Strengths</div><div id="strengths-list"><div style="color:var(--muted);font-size:13px;">Play more to find out.</div></div></div>
      <div class="card"><div class="card-title">Weaknesses</div><div id="weaknesses-list"><div style="color:var(--muted);font-size:13px;">Play more to find out.</div></div></div>
    </div>
  </div>

  <!-- ANALYTICS -->
  <div class="view" id="view-analytics">
    <div class="topbar"><div><h1>Analytics</h1><div class="topbar-sub">Deep dive into your data</div></div></div>
    <div class="tabs">
      <div class="tab active" data-tab="by-mode">By mode</div>
      <div class="tab" data-tab="by-diff">By difficulty</div>
      <div class="tab" data-tab="questions">Questions</div>
      <div class="tab" data-tab="recent">Recent</div>
    </div>
    <div id="tab-by-mode">
      <div class="g2">
        <div class="card"><div class="card-title">Win rate by mode</div><div id="an-winrate"><div style="color:var(--muted);font-size:13px;">No data yet.</div></div></div>
        <div class="card"><div class="card-title">Accuracy by mode</div><div id="an-acc"><div style="color:var(--muted);font-size:13px;">No data yet.</div></div></div>
      </div>
      <div class="card"><div class="card-title">Games played per mode</div><div id="an-games"></div></div>
    </div>
    <div id="tab-by-diff" style="display:none;">
      <div class="g2">
        <div class="card"><div class="card-title">Accuracy by difficulty</div><div id="an-diff-acc"></div></div>
        <div class="card"><div class="card-title">Avg speed by difficulty</div><div id="an-diff-speed"></div></div>
      </div>
    </div>
    <div id="tab-questions" style="display:none;">
      <div class="g2">
        <div class="card"><div class="card-title">Most missed questions <span>all time</span></div><div id="an-most-missed"><div style="color:var(--muted);font-size:13px;">No data yet — go play!</div></div></div>
        <div class="card"><div class="card-title">Most answered correctly <span>all time</span></div><div id="an-most-correct"><div style="color:var(--muted);font-size:13px;">No data yet — go play!</div></div></div>
      </div>
    </div>
    <div id="tab-recent" style="display:none;">
      <div class="card"><div class="card-title">Last 10 matches</div><div id="an-recent"></div></div>
    </div>
  </div>

  <!-- HISTORY -->
  <div class="view" id="view-history">
    <div class="topbar">
      <div><h1>History</h1><div class="topbar-sub" id="history-count">—</div></div>
      <select class="sel" onchange="renderHistory(this.value)">
        <option value="all">All modes</option>
        <option value="addition">Addition</option>
        <option value="multiplication">Multiplication</option>
        <option value="fractions">Fractions</option>
        <option value="variation">Variation</option>
      </select>
    </div>
    <div class="card"><div style="overflow-x:auto;"><table class="hist-table">
      <thead><tr><th>Result</th><th>Mode</th><th>Diff</th><th>Score</th><th>Acc</th><th>Speed</th><th>When</th></tr></thead>
      <tbody id="hist-body"></tbody>
    </table></div></div>
  </div>

  <!-- SETTINGS -->
  <div class="view" id="view-settings">
    <div class="topbar"><div><h1>Settings</h1></div></div>
    <div class="g2">
      <div>
        <div class="card" style="margin-bottom:11px;">
          <div class="card-title">Game</div>
          <div class="setting-row"><div><div class="setting-label">Fraction hints</div><div class="setting-sub">Show hint during fraction questions</div></div><div class="toggle on" id="toggle-hints" onclick="this.classList.toggle('on')"><div class="toggle-knob"></div></div></div>
          <div class="setting-row"><div><div class="setting-label">Bot difficulty scaling</div><div class="setting-sub">Bot speeds up as your best score climbs</div></div><div class="toggle on" onclick="this.classList.toggle('on')"><div class="toggle-knob"></div></div></div>
          <div class="setting-row"><div><div class="setting-label">Match length</div><div class="setting-sub">Seconds per match</div></div>
            <select class="sel" id="match-len-sel"><option value="30">30s</option><option value="45" selected>45s</option><option value="60">60s</option><option value="90">90s</option></select>
          </div>
        </div>
        <div class="card">
          <div class="card-title">Theme</div>
          <div class="theme-grid" id="theme-grid"></div>
        </div>
      </div>
      <div>
        <div class="card" style="margin-bottom:11px;">
          <div class="card-title">Discord Webhook</div>
          <div style="font-size:12px;color:var(--muted);margin-bottom:8px;">Paste your Discord webhook URL to send match results to a channel automatically after every game.</div>
          <div class="form-row" style="margin-bottom:8px;">
            <input class="inp" id="webhook-url" placeholder="https://discord.com/api/webhooks/..." />
          </div>
          <div style="display:flex;gap:7px;">
            <button class="btn btn-acc" style="flex:1;justify-content:center;" onclick="saveWebhook()">Save webhook</button>
            <button class="btn" onclick="testWebhook()">Test</button>
          </div>
          <div class="webhook-status"><div class="webhook-dot" id="webhook-dot"></div><span id="webhook-label">No webhook set</span></div>
        </div>
        <div class="card">
          <div class="card-title">Data</div>
          <div class="setting-row"><div><div class="setting-label">Export stats</div><div class="setting-sub">Download history as CSV</div></div><button class="btn" onclick="exportCSV()">Export</button></div>
          <div class="setting-row"><div><div class="setting-label">Reset all stats</div><div class="setting-sub">Clears everything — can't undo</div></div><button class="btn" style="color:var(--dan-txt);border-color:var(--dan-dim);" onclick="resetStats()">Reset</button></div>
        </div>
      </div>
    </div>
  </div>

</main>
</div>

<script>
// ── store ──
const store = {
  get matches(){ try{ return JSON.parse(localStorage.getItem('mb_matches')||'[]'); }catch(e){ return []; } },
  save(m){ const ms=this.matches; ms.unshift(m); localStorage.setItem('mb_matches', JSON.stringify(ms.slice(0,300))); },
  get bestScore(){ try{ return parseInt(localStorage.getItem('mb_best')||'0'); }catch(e){ return 0; } },
  setBest(n){ localStorage.setItem('mb_best', String(n)); },
  get webhook(){ return localStorage.getItem('mb_webhook')||''; },
  setWebhook(u){ localStorage.setItem('mb_webhook',u); },
  // persist all-time question stats
  get qStats(){ try{ return JSON.parse(localStorage.getItem('mb_qstats')||'{}'); }catch(e){ return {}; } },
  saveQStats(s){ localStorage.setItem('mb_qstats', JSON.stringify(s)); }
};

// ── modes ──
const MODES = {
  addition:{ label:'Addition', diffs:[
    {name:'Kindergarten',desc:'Single digits · e.g. 3 + 5',bot:5},
    {name:'Easy',desc:'Up to 20 · e.g. 13 + 7',bot:4},
    {name:'Medium',desc:'Two-digit · e.g. 47 + 36',bot:3},
    {name:'Hard',desc:'Three-digit · e.g. 384 + 219',bot:2.2},
    {name:'Expert',desc:'Four-digit · e.g. 4732 + 2891',bot:1.8},
    {name:'Master',desc:'Triple addend with large numbers',bot:1.3},
  ]},
  multiplication:{ label:'Multiply', diffs:[
    {name:'Kindergarten',desc:'Times 1–2 tables · e.g. 3 × 2',bot:6},
    {name:'Easy',desc:'Times 1–5 tables · e.g. 4 × 5',bot:4.5},
    {name:'Medium',desc:'Times 1–12 tables · e.g. 7 × 9',bot:3},
    {name:'Hard',desc:'Two-digit × one-digit · e.g. 23 × 7',bot:2.2},
    {name:'Expert',desc:'Two-digit × two-digit · e.g. 34 × 27',bot:1.8},
    {name:'Master',desc:'Three-digit × two-digit · e.g. 142 × 38',bot:1.3},
  ]},
  fractions:{ label:'Fractions', diffs:[
    {name:'Kindergarten',desc:'Simple halves and quarters',bot:7},
    {name:'Easy',desc:'Same denominator addition',bot:5},
    {name:'Medium',desc:'Different denominators',bot:3.5},
    {name:'Hard',desc:'Mixed numbers',bot:2.8},
    {name:'Expert',desc:'Multiply fractions',bot:2.2},
    {name:'Master',desc:'Divide fractions and mixed numbers',bot:1.8},
  ]},
  variation:{ label:'Variation', diffs:[
    {name:'Kindergarten',desc:'Simple mix of all types',bot:6},
    {name:'Easy',desc:'Easy mix — all modes',bot:4.5},
    {name:'Medium',desc:'Moderate mix of all operations',bot:3},
    {name:'Hard',desc:'Hard mix — everything',bot:2.2},
    {name:'Expert',desc:'Expert-level mix',bot:1.8},
    {name:'Master',desc:'Master all — anything goes',bot:1.3},
  ]}
};

function r(a,b){ return Math.floor(Math.random()*(b-a+1))+a; }
function gcd(a,b){ return b===0?a:gcd(b,a%b); }

function generateQ(mode,di){
  if(mode==='variation'){ const m=['addition','multiplication','fractions'][r(0,2)]; return generateQ(m,Math.min(di,MODES[m].diffs.length-1)); }
  if(mode==='addition'){
    if(di===0){const a=r(1,9),b=r(1,9);return{q:`${a} + ${b}`,ans:String(a+b)};}
    if(di===1){const a=r(1,20),b=r(1,20);return{q:`${a} + ${b}`,ans:String(a+b)};}
    if(di===2){const a=r(10,99),b=r(10,99);return{q:`${a} + ${b}`,ans:String(a+b)};}
    if(di===3){const a=r(100,999),b=r(100,999);return{q:`${a} + ${b}`,ans:String(a+b)};}
    if(di===4){const a=r(1000,9999),b=r(1000,9999);return{q:`${a} + ${b}`,ans:String(a+b)};}
    if(di===5){const a=r(100,999),b=r(100,999),c=r(100,999);return{q:`${a} + ${b} + ${c}`,ans:String(a+b+c)};}
  }
  if(mode==='multiplication'){
    if(di===0){const a=r(1,5),b=r(1,2);return{q:`${a} × ${b}`,ans:String(a*b)};}
    if(di===1){const a=r(1,9),b=r(1,5);return{q:`${a} × ${b}`,ans:String(a*b)};}
    if(di===2){const a=r(1,12),b=r(1,12);return{q:`${a} × ${b}`,ans:String(a*b)};}
    if(di===3){const a=r(12,99),b=r(2,9);return{q:`${a} × ${b}`,ans:String(a*b)};}
    if(di===4){const a=r(12,99),b=r(12,99);return{q:`${a} × ${b}`,ans:String(a*b)};}
    if(di===5){const a=r(100,999),b=r(12,99);return{q:`${a} × ${b}`,ans:String(a*b)};}
  }
  if(mode==='fractions'){
    if(di===0){const opts=[{q:'1/2 + 1/2',a:'1'},{q:'1/4 + 3/4',a:'1'},{q:'1/3 + 1/3',a:'2/3'},{q:'3/4 – 1/4',a:'1/2'}];const o=opts[r(0,opts.length-1)];return{q:o.q,ans:o.a,hint:'Answer as a fraction or whole number'};}
    if(di===1){const den=[4,6,8,10][r(0,3)];const a=r(1,den-2),b=r(1,den-a-1);const s=a+b,g2=gcd(s,den);const ans=g2===den?String(s/g2):`${s/g2}/${den/g2}`;return{q:`${a}/${den} + ${b}/${den}`,ans,hint:'Same denominator — add the tops'};}
    if(di===2){const pairs=[[2,3],[2,4],[3,4],[4,5],[2,5]];const[d1,d2]=pairs[r(0,pairs.length-1)];const n1=r(1,d1-1),n2=r(1,d2-1);const cd=d1*d2,s=n1*d2+n2*d1,g2=gcd(s,cd);const ans=g2===cd?String(s/g2):`${s/g2}/${cd/g2}`;return{q:`${n1}/${d1} + ${n2}/${d2}`,ans,hint:'Find a common denominator first'};}
    if(di===3){const w1=r(1,4),n1=r(1,2),w2=r(1,4),n2=r(1,2),den=4;const tot=w1+w2+(n1+n2)/den;const wh=Math.floor(tot),fr=Math.round((tot-wh)*den);let ans;if(fr===0)ans=String(wh);else if(fr===den)ans=String(wh+1);else{const g2=gcd(fr,den);ans=`${wh} ${fr/g2}/${den/g2}`;}return{q:`${w1} ${n1}/4 + ${w2} ${n2}/4`,ans,hint:'e.g. answer as: 3 1/2'};}
    if(di===4){const n1=r(1,5),d1=[2,3,4,5][r(0,3)],n2=r(1,5),d2=[2,3,4,5][r(0,3)];const rn=n1*n2,rd=d1*d2,g2=gcd(rn,rd);const ans=g2===rd?String(rn/g2):`${rn/g2}/${rd/g2}`;return{q:`${n1}/${d1} × ${n2}/${d2}`,ans,hint:'Multiply tops together, bottoms together'};}
    if(di===5){const n1=r(2,7),d1=[2,3,4][r(0,2)],n2=r(2,7),d2=[2,3,4][r(0,2)];const rn=n1*d2,rd=d1*n2,g2=gcd(rn,rd);const ans=g2===rd?String(rn/g2):`${rn/g2}/${rd/g2}`;return{q:`${n1}/${d1} ÷ ${n2}/${d2}`,ans,hint:'Flip the second fraction, then multiply'};}
  }
  return{q:'1 + 1',ans:'2'};
}

// ── themes ──
const THEMES=[
  {id:'dark',   label:'Dark',    bg:'#0d0f14', acc:'#5b8df5'},
  {id:'midnight',label:'Midnight',bg:'#080c14',acc:'#3a7ef5'},
  {id:'neon',   label:'Neon',    bg:'#070a0e', acc:'#00d4ff'},
  {id:'forest', label:'Forest',  bg:'#0a110a', acc:'#4acc70'},
  {id:'sunset', label:'Sunset',  bg:'#120810', acc:'#e060c0'},
  {id:'light',  label:'Light',   bg:'#f0f2f6', acc:'#4a7ef0'},
];

function buildThemeGrid(){
  const saved=localStorage.getItem('mb_theme')||'dark';
  const grid=document.getElementById('theme-grid');
  grid.innerHTML='';
  THEMES.forEach(t=>{
    const s=document.createElement('div');
    s.className='theme-swatch'+(t.id===saved?' active':'');
    s.title=t.label;
    s.style.cssText=`background:${t.bg};border-color:${t.acc};`;
    s.innerHTML=`<div style="position:absolute;bottom:3px;right:3px;width:10px;height:10px;border-radius:50%;background:${t.acc};"></div>`;
    s.addEventListener('click',()=>{
      applyTheme(t.id);
      document.querySelectorAll('.theme-swatch').forEach(x=>x.classList.remove('active'));
      s.classList.add('active');
    });
    grid.appendChild(s);
    const lbl=document.createElement('div');
    lbl.style.cssText='font-size:10px;color:var(--muted);text-align:center;width:32px;';
    lbl.textContent=t.label;
    grid.appendChild(lbl);
  });
}

function applyTheme(id){
  document.documentElement.setAttribute('data-theme',id);
  localStorage.setItem('mb_theme',id);
}

// ── nav ──
function nav(id){
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  const el=document.querySelector(`.nav-item[data-view="${id}"]`);
  if(el) el.classList.add('active');
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.getElementById('view-'+id).classList.add('active');
  if(id==='dashboard') refreshDashboard();
  if(id==='analytics') refreshAnalytics();
  if(id==='history') renderHistory('all');
  if(id==='settings'){ loadWebhookUI(); buildThemeGrid(); }
}
document.querySelectorAll('.nav-item[data-view]').forEach(n=>{
  n.addEventListener('click',()=>nav(n.dataset.view));
});

// ── menu ──
let selMode='addition', selDiff=0;
function buildMenu(){
  document.querySelectorAll('.mode-card').forEach(c=>{
    c.addEventListener('click',()=>{
      document.querySelectorAll('.mode-card').forEach(x=>x.classList.remove('sel'));
      c.classList.add('sel'); selMode=c.dataset.mode; selDiff=0; buildDiffChips();
    });
  });
  buildDiffChips();
  updateSbBest();
}
function buildDiffChips(){
  const diffs=MODES[selMode].diffs;
  const wrap=document.getElementById('diff-chips');
  wrap.innerHTML='';
  diffs.forEach((d,i)=>{
    const ch=document.createElement('div');
    ch.className='diff-chip'+(i===selDiff?' sel':'');
    ch.textContent=d.name;
    ch.addEventListener('click',()=>{
      document.querySelectorAll('.diff-chip').forEach(x=>x.classList.remove('sel'));
      ch.classList.add('sel'); selDiff=i; updateDiffInfo();
    });
    wrap.appendChild(ch);
  });
  updateDiffInfo();
}
function updateDiffInfo(){
  const d=MODES[selMode].diffs[selDiff];
  const best=store.bestScore;
  const botSpd=getBotSpeed(d.bot);
  document.getElementById('diff-info').innerHTML=
    `<strong style="color:var(--text);">${d.name}</strong> — ${d.desc}<br>
     <span style="font-size:11px;color:var(--sub);margin-top:3px;display:block;">Bot: ~${botSpd}s/q${best>0?` · Best: <strong style="color:var(--warn-txt);">${best} pts</strong>`:''} · Match: <strong>${getMatchLen()}s</strong></span>`;
}
function getMatchLen(){ return parseInt(document.getElementById('match-len-sel')?.value||'45'); }
function getBotSpeed(base){
  const best=store.bestScore;
  const red=Math.min(best*0.033,base*0.6);
  return parseFloat(Math.max(base-red,base*0.4).toFixed(2));
}

document.getElementById('start-btn').addEventListener('click',startCountdown);

function startCountdown(){
  document.getElementById('menu-screen').style.display='none';
  const cs=document.getElementById('countdown-screen');
  cs.style.display='flex';
  const el=document.getElementById('countdown-num');
  const botSpd=getBotSpeed(MODES[selMode].diffs[selDiff].bot);
  const best=store.bestScore;
  document.getElementById('countdown-bot-warn').textContent=
    best>0?`Bot: ~${botSpd}s/q (your best: ${best} pts)`:`Bot: ~${MODES[selMode].diffs[selDiff].bot}s/q`;
  let n=3;
  el.textContent=n;
  const iv=setInterval(()=>{
    n--;
    if(n<=0){ clearInterval(iv); cs.style.display='none'; startGame(); }
    else el.textContent=n;
  },800);
}

// ── game ──
let G={}, matchIv=null, botTo=null, qStart=0;

function startGame(){
  const matchLen=getMatchLen();
  G={ mode:selMode, diff:selDiff, pScore:0, bScore:0, strikes:0,
      total:0, correct:0, speeds:[], timeLeft:matchLen, matchLen, cur:null,
      questionLog:[], missedLog:{} };
  document.getElementById('game-screen').style.display='flex';
  document.getElementById('hud-mode').textContent=MODES[selMode].label;
  document.getElementById('hud-diff').textContent=MODES[selMode].diffs[selDiff].name;
  updateStrikes();
  const bar=document.getElementById('match-bar');
  bar.style.width='100%'; bar.style.background='var(--suc)';
  matchIv=setInterval(()=>{
    G.timeLeft-=0.1;
    const pct=Math.max(0,G.timeLeft/G.matchLen*100);
    bar.style.width=pct+'%';
    bar.style.background=pct<20?'var(--dan)':pct<40?'var(--warn)':'var(--suc)';
    document.getElementById('match-time-left').textContent=Math.ceil(G.timeLeft);
    if(G.timeLeft<=0){ clearInterval(matchIv); matchIv=null; endGame('time'); }
  },100);
  nextQ();
}

function nextQ(){
  if(botTo){ clearTimeout(botTo); botTo=null; }
  G.total++;
  G.cur=generateQ(G.mode,G.diff);
  qStart=Date.now();
  document.getElementById('question').textContent=G.cur.q+' = ?';
  const showHints=document.getElementById('toggle-hints').classList.contains('on');
  document.getElementById('hint').textContent=(showHints&&G.cur.hint)?G.cur.hint:'';
  document.getElementById('feedback').textContent='';
  document.getElementById('answer-input').value='';
  document.getElementById('answer-input').className='';
  document.getElementById('hud-q').textContent=G.total;
  document.getElementById('answer-input').focus();
  const base=MODES[G.mode].diffs[G.diff].bot;
  const botSpd=getBotSpeed(base);
  const jitter=botSpd*(0.1+Math.random()*0.2)*(Math.random()<.5?1:-1);
  const delay=Math.max(botSpd+jitter,0.5)*1000;
  document.getElementById('bot-speed-label').textContent=`~${botSpd.toFixed(1)}s/q`;
  const prog=document.getElementById('bot-progress');
  prog.style.transition='none'; prog.style.width='0%';
  document.getElementById('bot-pulse').style.background='var(--warn)';
  document.getElementById('bot-status').textContent='Bot solving…';
  requestAnimationFrame(()=>requestAnimationFrame(()=>{
    prog.style.transition=`width ${delay/1000}s linear`; prog.style.width='100%';
  }));
  botTo=setTimeout(()=>{
    if(G.cur&&G.timeLeft>0){ G.bScore++; document.getElementById('bot-score').textContent=G.bScore;
      document.getElementById('bot-pulse').style.background='var(--suc)';
      document.getElementById('bot-status').textContent='Bot got it ✓'; }
  },delay);
}

function updateStrikes(){
  const wrap=document.getElementById('strikes-wrap');
  wrap.innerHTML='';
  for(let i=0;i<3;i++){
    const d=document.createElement('div');
    d.className='strike-dot'+(i<G.strikes?' filled':'');
    wrap.appendChild(d);
  }
  const rem=document.createElement('span');
  rem.style.cssText='font-size:10px;color:var(--sub);margin-left:4px;';
  rem.textContent=`${3-G.strikes} left`;
  wrap.appendChild(rem);
}

function normalizeAns(s){ return s.trim().replace(/\s+/g,' ').toLowerCase(); }
function checkAns(inp){
  const cor=String(G.cur.ans).trim().toLowerCase();
  if(normalizeAns(inp)===cor) return true;
  const ni=parseFloat(inp),nc=parseFloat(cor);
  if(!isNaN(ni)&&!isNaN(nc)&&Math.abs(ni-nc)<0.001) return true;
  return false;
}

function submitAnswer(){
  const inp=document.getElementById('answer-input').value;
  if(!inp.trim()||!G.cur) return;
  const elapsed=(Date.now()-qStart)/1000;
  if(botTo){ clearTimeout(botTo); botTo=null; }
  const prog=document.getElementById('bot-progress');
  prog.style.transition='none'; prog.style.width='0%';
  if(checkAns(inp)){
    G.correct++; G.pScore++; G.speeds.push(elapsed);
    G.questionLog.push({q:G.cur.q,ans:G.cur.ans,result:'correct',elapsed});
    document.getElementById('answer-input').className='right';
    document.getElementById('feedback').textContent=`✓  ${elapsed.toFixed(1)}s`;
    document.getElementById('player-score').textContent=G.pScore;
    if(G.timeLeft>0) setTimeout(nextQ,400);
  } else {
    G.strikes++;
    const key=G.cur.q;
    if(!G.missedLog[key]) G.missedLog[key]={q:G.cur.q,ans:G.cur.ans,count:0};
    G.missedLog[key].count++;
    G.questionLog.push({q:G.cur.q,ans:G.cur.ans,result:'wrong',elapsed});
    document.getElementById('answer-input').className='wrong';
    document.getElementById('feedback').textContent=`✗  Answer: ${G.cur.ans}`;
    updateStrikes();
    if(G.strikes>=3){ setTimeout(()=>endGame('strikes'),800); return; }
    if(G.timeLeft>0) setTimeout(nextQ,900);
  }
}

document.getElementById('answer-input').addEventListener('keydown',e=>{ if(e.key==='Enter') submitAnswer(); });

function endGame(reason){
  if(matchIv){ clearInterval(matchIv); matchIv=null; }
  if(botTo){ clearTimeout(botTo); botTo=null; }
  G.cur=null;
  document.getElementById('game-screen').style.display='none';
  const win=G.pScore>G.bScore, tie=G.pScore===G.bScore;
  let title,sub;
  if(reason==='strikes'){ title='💥 Knocked out'; sub='3 strikes and you\'re done.'; }
  else if(reason==='time'){
    if(win){ title='🏆 You win!'; sub='You scored more than the bot!'; }
    else if(tie){ title='🤝 Tie game'; sub='Dead even with the bot.'; }
    else{ title='🤖 Bot wins'; sub='The bot outscored you this time.'; }
  } else { title='👋 Quit'; sub='Better luck next time.'; }
  const acc=G.total>0?Math.round(G.correct/G.total*100):0;
  const avgSpeed=G.speeds.length>0?(G.speeds.reduce((a,b)=>a+b,0)/G.speeds.length).toFixed(1)+'s':'—';
  document.getElementById('res-title').textContent=title;
  document.getElementById('res-sub').textContent=sub;
  document.getElementById('rs-player').textContent=G.pScore;
  document.getElementById('rs-bot').textContent=G.bScore;
  document.getElementById('rs-acc').textContent=acc+'%';
  document.getElementById('rs-q').textContent=G.total;
  document.getElementById('rs-speed').textContent=avgSpeed;
  document.getElementById('rs-strikes').textContent=G.strikes+'/3';
  const prev=store.bestScore;
  const isPB=G.pScore>prev;
  if(isPB){ store.setBest(G.pScore); updateSbBest(); }
  document.getElementById('pb-banner').style.display=isPB?'block':'none';

  // breakdown panels
  const missed=Object.values(G.missedLog).sort((a,b)=>b.count-a.count).slice(0,5);
  const fastQ=G.questionLog.filter(l=>l.result==='correct').sort((a,b)=>a.elapsed-b.elapsed).slice(0,5);
  document.getElementById('breakdown-grid').innerHTML=`
    <div class="breakdown-card">
      <div class="breakdown-title" style="color:var(--dan-txt);">💀 Most missed</div>
      ${missed.length?missed.map(m=>`<div class="qrow"><div class="qrow-q">${m.q} = <span style="color:var(--suc-txt);">${m.ans}</span></div><div class="qrow-badge qrow-missed">✗ ×${m.count}</div></div>`).join(''):'<div style="color:var(--muted);font-size:13px;padding:6px 0;">No wrong answers! 🎉</div>'}
    </div>
    <div class="breakdown-card">
      <div class="breakdown-title" style="color:var(--suc-txt);">⚡ Fastest answers</div>
      ${fastQ.length?fastQ.map(l=>`<div class="qrow"><div class="qrow-q">${l.q} = <span style="color:var(--acc-txt);">${l.ans}</span></div><div class="qrow-badge qrow-fast">⚡ ${l.elapsed.toFixed(2)}s</div></div>`).join(''):'<div style="color:var(--muted);font-size:13px;padding:6px 0;">No correct answers yet.</div>'}
    </div>`;

  document.getElementById('result-screen').style.display='block';

  // persist all-time question stats
  const qs=store.qStats;
  G.questionLog.forEach(l=>{
    if(!qs[l.q]) qs[l.q]={q:l.q,ans:l.ans,correct:0,wrong:0};
    if(l.result==='correct') qs[l.q].correct++;
    else qs[l.q].wrong++;
  });
  store.saveQStats(qs);

  // save match
  const matchData={
    result: reason==='strikes'?'loss':reason==='quit'?'quit':win?'win':tie?'tie':'loss',
    mode:G.mode, diff:MODES[G.mode].diffs[G.diff].name,
    pScore:G.pScore, bScore:G.bScore, acc,
    avgSpeed:G.speeds.length>0?parseFloat((G.speeds.reduce((a,b)=>a+b,0)/G.speeds.length).toFixed(1)):null,
    total:G.total, strikes:G.strikes,
    fastest:G.speeds.length>0?Math.min(...G.speeds):null,
    date:new Date().toISOString(),
    missedLog:G.missedLog, questionLog:G.questionLog
  };
  store.save(matchData);

  // discord webhook
  sendToDiscord(matchData, missed, fastQ, isPB);
}

// ── discord webhook ──
async function sendToDiscord(match, missed, fastQ, isPB){
  const url=store.webhook;
  const el=document.getElementById('discord-result');
  if(!url){ el.textContent=''; return; }
  const resultEmoji={win:'🏆',loss:'💥',tie:'🤝',quit:'👋'}[match.result]||'🎮';
  const missedTxt=missed.length?missed.map(m=>`\`${m.q} = ${m.ans}\` ×${m.count}`).join('\n'):'None! Perfect match 🎉';
  const fastTxt=fastQ.length?fastQ.map(l=>`\`${l.q} = ${l.ans}\` — ${l.elapsed.toFixed(2)}s`).join('\n'):'No correct answers';
  const embed={
    title:`${resultEmoji} Math Battle Result`,
    color: match.result==='win'?0x2ecc8a:match.result==='loss'?0xe04f4f:match.result==='tie'?0xf0a020:0x5b8df5,
    fields:[
      {name:'Result',value:`**${match.result.toUpperCase()}** — ${match.pScore} vs ${match.bScore} (bot)`,inline:false},
      {name:'Mode',value:`${MODES[match.mode]?.label||match.mode} · ${match.diff}`,inline:true},
      {name:'Accuracy',value:`${match.acc}%`,inline:true},
      {name:'Avg Speed',value:match.avgSpeed?`${match.avgSpeed}s`:'—',inline:true},
      {name:'💀 Most Missed',value:missedTxt,inline:false},
      {name:'⚡ Fastest Answers',value:fastTxt,inline:false},
    ],
    footer:{text:`${isPB?'🔥 NEW PERSONAL BEST! · ':''}`+'MathBattle · '+new Date().toLocaleString()},
  };
  try {
    el.textContent='Sending to Discord…';
    const resp=await fetch(url,{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({embeds:[embed]})});
    if(resp.ok){ el.style.color='var(--suc-txt)'; el.textContent='✓ Sent to Discord!'; }
    else{ el.style.color='var(--dan-txt)'; el.textContent=`Discord error: ${resp.status}`; }
  } catch(e){ el.style.color='var(--dan-txt)'; el.textContent='Discord send failed (check webhook URL)'; }
}

function loadWebhookUI(){
  const url=store.webhook;
  document.getElementById('webhook-url').value=url;
  const dot=document.getElementById('webhook-dot');
  const lbl=document.getElementById('webhook-label');
  if(url){ dot.className='webhook-dot ok'; lbl.textContent='Webhook saved'; }
  else{ dot.className='webhook-dot'; lbl.textContent='No webhook set'; }
}

function saveWebhook(){
  const url=document.getElementById('webhook-url').value.trim();
  store.setWebhook(url);
  loadWebhookUI();
  toast(url?'Webhook saved!':'Webhook cleared');
}

async function testWebhook(){
  const url=store.webhook||document.getElementById('webhook-url').value.trim();
  if(!url){ toast('Paste a webhook URL first'); return; }
  try{
    const resp=await fetch(url,{method:'POST',headers:{'Content-Type':'application/json'},
      body:JSON.stringify({embeds:[{title:'⚡ Math Battle — Test Message',description:'Your webhook is working! Game results will appear here after each match.',color:0x5b8df5,footer:{text:'MathBattle test'}}]})});
    if(resp.ok){ toast('✓ Test sent to Discord!'); document.getElementById('webhook-dot').className='webhook-dot ok'; document.getElementById('webhook-label').textContent='Webhook working'; }
    else toast(`Discord error: ${resp.status}`);
  } catch(e){ toast('Send failed — check the URL'); }
}

function updateSbBest(){ const b=store.bestScore; document.getElementById('sb-best').textContent=b>0?b+'pts':'—'; }

function showMenu(){
  document.getElementById('result-screen').style.display='none';
  document.getElementById('game-screen').style.display='none';
  document.getElementById('menu-screen').style.display='block';
  updateDiffInfo();
}
function playAgain(){ document.getElementById('result-screen').style.display='none'; startCountdown(); }

// ── dashboard ──
function refreshDashboard(){
  const ms=store.matches; const best=store.bestScore;
  document.getElementById('stat-best').textContent=best>0?best:'—';
  document.getElementById('qs-best').textContent=best>0?best+'pts':'—';
  if(!ms.length){ ['stat-total','stat-winrate','stat-acc'].forEach(id=>document.getElementById(id).textContent='0'); return; }
  const wins=ms.filter(m=>m.result==='win').length;
  const total=ms.length;
  const accs=ms.map(m=>m.acc).filter(a=>a!=null);
  const avgAcc=accs.length?Math.round(accs.reduce((a,b)=>a+b,0)/accs.length):null;
  const allFastest=ms.flatMap(m=>m.fastest!=null?[m.fastest]:[]);
  document.getElementById('stat-total').textContent=total;
  document.getElementById('stat-winrate').textContent=Math.round(wins/total*100)+'%';
  document.getElementById('stat-acc').textContent=avgAcc!=null?avgAcc+'%':'—';
  document.getElementById('qs-wins').textContent=wins;
  document.getElementById('qs-fastest').textContent=allFastest.length?Math.min(...allFastest).toFixed(1)+'s':'—';
  document.getElementById('db-streak').textContent='7d streak 🔥';
  const modeCounts={};
  ms.forEach(m=>{modeCounts[m.mode]=(modeCounts[m.mode]||0)+1;});
  const favMode=Object.keys(modeCounts).sort((a,b)=>modeCounts[b]-modeCounts[a])[0];
  document.getElementById('qs-fav').textContent=favMode?MODES[favMode].label:'—';
  const modeLabels={addition:'Addition',multiplication:'Multiply',fractions:'Fractions',variation:'Variation'};
  let barsHtml='',strengths=[],weaknesses=[];
  Object.keys(modeLabels).forEach(mode=>{
    const mms=ms.filter(m=>m.mode===mode);
    if(!mms.length) return;
    const acc=Math.round(mms.reduce((a,m)=>a+m.acc,0)/mms.length);
    const col=acc>=80?'var(--suc)':acc>=65?'var(--warn)':'var(--dan)';
    const colTxt=acc>=80?'var(--suc-txt)':acc>=65?'var(--warn-txt)':'var(--dan-txt)';
    barsHtml+=`<div class="bar-row"><div class="bar-label">${modeLabels[mode]}</div><div class="bar-track"><div class="bar-fill" style="width:${acc}%;background:${col};"></div></div><div class="bar-pct" style="color:${colTxt};">${acc}%</div></div>`;
    if(acc>=80) strengths.push({name:modeLabels[mode],acc});
    else if(acc<68) weaknesses.push({name:modeLabels[mode],acc});
  });
  document.getElementById('mode-acc-bars').innerHTML=barsHtml||'<div style="color:var(--muted);font-size:13px;">Play a game first!</div>';
  strengths.sort((a,b)=>b.acc-a.acc); weaknesses.sort((a,b)=>a.acc-b.acc);
  document.getElementById('strengths-list').innerHTML=strengths.length?strengths.map(s=>`<div class="sw-row"><div class="sw-left"><div class="sw-icon" style="background:var(--suc-dim);">✓</div><div style="font-size:13px;">${s.name}</div></div><div style="font-weight:700;color:var(--suc-txt);">${s.acc}%</div></div>`).join(''):'<div style="color:var(--muted);font-size:13px;">Keep playing!</div>';
  document.getElementById('weaknesses-list').innerHTML=weaknesses.length?weaknesses.map(w=>`<div class="sw-row"><div class="sw-left"><div class="sw-icon" style="background:var(--dan-dim);">✗</div><div style="font-size:13px;">${w.name}</div></div><div style="font-weight:700;color:var(--dan-txt);">${w.acc}%</div></div>`).join(''):'<div style="color:var(--muted);font-size:13px;">No weak spots yet!</div>';
}

// ── analytics ──
function refreshAnalytics(){
  const ms=store.matches;
  const modes={addition:'Addition',multiplication:'Multiply',fractions:'Fractions',variation:'Variation'};
  const diffs=['Kindergarten','Easy','Medium','Hard','Expert','Master'];
  function barHtml(label,pct,col,colTxt,val){
    return `<div class="bar-row"><div class="bar-label">${label}</div><div class="bar-track"><div class="bar-fill" style="width:${pct}%;background:${col};"></div></div><div class="bar-pct" style="color:${colTxt};">${val}</div></div>`;
  }
  let wrH='',accH='',gH='';
  const maxG=Math.max(...Object.keys(modes).map(m=>ms.filter(x=>x.mode===m).length),1);
  Object.keys(modes).forEach(m=>{
    const mms=ms.filter(x=>x.mode===m);
    if(!mms.length){wrH+=barHtml(modes[m],0,'var(--border)','var(--muted)','—');accH+=barHtml(modes[m],0,'var(--border)','var(--muted)','—');gH+=barHtml(modes[m],0,'var(--border)','var(--muted)','0');return;}
    const wr=Math.round(mms.filter(x=>x.result==='win').length/mms.length*100);
    const acc=Math.round(mms.reduce((a,x)=>a+x.acc,0)/mms.length);
    const gc=mms.length;
    const wc=wr>=70?'var(--suc)':wr>=50?'var(--warn)':'var(--dan)';
    const wt=wr>=70?'var(--suc-txt)':wr>=50?'var(--warn-txt)':'var(--dan-txt)';
    const ac=acc>=80?'var(--suc)':acc>=65?'var(--warn)':'var(--dan)';
    const at=acc>=80?'var(--suc-txt)':acc>=65?'var(--warn-txt)':'var(--dan-txt)';
    wrH+=barHtml(modes[m],wr,wc,wt,wr+'%');
    accH+=barHtml(modes[m],acc,ac,at,acc+'%');
    gH+=barHtml(modes[m],Math.round(gc/maxG*100),'var(--acc)','var(--acc-txt)',gc);
  });
  document.getElementById('an-winrate').innerHTML=wrH||'<div style="color:var(--muted);font-size:13px;">No data.</div>';
  document.getElementById('an-acc').innerHTML=accH||'<div style="color:var(--muted);font-size:13px;">No data.</div>';
  document.getElementById('an-games').innerHTML=gH||'<div style="color:var(--muted);font-size:13px;">No data.</div>';
  let dAccH='',dSpdH='';
  diffs.forEach(d=>{
    const dms=ms.filter(x=>x.diff===d);
    if(!dms.length){dAccH+=barHtml(d,0,'var(--border)','var(--muted)','—');dSpdH+=barHtml(d,0,'var(--border)','var(--muted)','—');return;}
    const acc=Math.round(dms.reduce((a,x)=>a+x.acc,0)/dms.length);
    const spds=dms.filter(x=>x.avgSpeed!=null).map(x=>x.avgSpeed);
    const spd=spds.length?(spds.reduce((a,b)=>a+b,0)/spds.length).toFixed(1):null;
    const ac=acc>=80?'var(--suc)':acc>=65?'var(--warn)':'var(--dan)';
    const at=acc>=80?'var(--suc-txt)':acc>=65?'var(--warn-txt)':'var(--dan-txt)';
    dAccH+=barHtml(d,acc,ac,at,acc+'%');
    const maxSpd=8;
    const spdPct=spd?Math.min(Math.round(parseFloat(spd)/maxSpd*100),100):0;
    const sc=spdPct>70?'var(--dan)':spdPct>40?'var(--warn)':'var(--suc)';
    const st=spdPct>70?'var(--dan-txt)':spdPct>40?'var(--warn-txt)':'var(--suc-txt)';
    dSpdH+=barHtml(d,spdPct,sc,st,spd?spd+'s':'—');
  });
  document.getElementById('an-diff-acc').innerHTML=dAccH||'<div style="color:var(--muted);font-size:13px;">No data.</div>';
  document.getElementById('an-diff-speed').innerHTML=dSpdH||'<div style="color:var(--muted);font-size:13px;">No data.</div>';

  // all-time question stats
  const qs=store.qStats;
  const qArr=Object.values(qs);
  if(qArr.length){
    // most missed (by wrong count)
    const mostMissed=qArr.filter(q=>q.wrong>0).sort((a,b)=>b.wrong-a.wrong).slice(0,10);
    const maxMissed=Math.max(...mostMissed.map(q=>q.wrong),1);
    document.getElementById('an-most-missed').innerHTML=mostMissed.length?mostMissed.map(q=>`
      <div class="qheat-row">
        <div class="qheat-q" style="color:var(--dan-txt);">${q.q} = <span style="color:var(--suc-txt);">${q.ans}</span></div>
        <div class="qheat-bar-wrap"><div class="qheat-bar" style="width:${Math.round(q.wrong/maxMissed*100)}%;background:var(--dan);"></div></div>
        <div class="qheat-count" style="color:var(--dan-txt);">✗${q.wrong}</div>
      </div>`).join(''):'<div style="color:var(--muted);font-size:13px;">No wrong answers yet!</div>';
    // most correct
    const mostCorrect=qArr.filter(q=>q.correct>0).sort((a,b)=>b.correct-a.correct).slice(0,10);
    const maxCorrect=Math.max(...mostCorrect.map(q=>q.correct),1);
    document.getElementById('an-most-correct').innerHTML=mostCorrect.length?mostCorrect.map(q=>`
      <div class="qheat-row">
        <div class="qheat-q" style="color:var(--suc-txt);">${q.q} = <span style="color:var(--acc-txt);">${q.ans}</span></div>
        <div class="qheat-bar-wrap"><div class="qheat-bar" style="width:${Math.round(q.correct/maxCorrect*100)}%;background:var(--suc);"></div></div>
        <div class="qheat-count" style="color:var(--suc-txt);">✓${q.correct}</div>
      </div>`).join(''):'<div style="color:var(--muted);font-size:13px;">No correct answers yet!</div>';
  } else {
    document.getElementById('an-most-missed').innerHTML='<div style="color:var(--muted);font-size:13px;">Play more games to see your question history!</div>';
    document.getElementById('an-most-correct').innerHTML='<div style="color:var(--muted);font-size:13px;">Play more games to see your question history!</div>';
  }

  const recent=ms.slice(0,10);
  document.getElementById('an-recent').innerHTML=recent.length?recent.map(m=>{
    const rc=m.result==='win'?'badge-suc':m.result==='loss'?'badge-dan':'badge-warn';
    const mS={addition:'Add',multiplication:'Mult',fractions:'Frac',variation:'Var'}[m.mode]||m.mode;
    const when=new Date(m.date).toLocaleDateString(undefined,{month:'short',day:'numeric'});
    return `<div style="display:flex;align-items:center;gap:10px;padding:7px 0;border-bottom:1px solid var(--border);">
      <span class="pill ${rc}" style="min-width:40px;text-align:center;">${m.result}</span>
      <span style="font-size:12px;color:var(--muted);flex:1;">${mS} · ${m.diff} · ${m.pScore}–${m.bScore}</span>
      <span style="font-size:12px;color:var(--muted);">${m.acc}%</span>
      <span style="font-size:11px;color:var(--sub);">${when}</span>
    </div>`;
  }).join(''):'<div style="color:var(--muted);font-size:13px;padding:8px 0;">No recent matches.</div>';
}

document.querySelectorAll('.tab').forEach(t=>{
  t.addEventListener('click',()=>{
    const parent=t.closest('.view');
    parent.querySelectorAll('.tab').forEach(x=>x.classList.remove('active'));
    t.classList.add('active');
    ['by-mode','by-diff','questions','recent'].forEach(id=>{
      const el=document.getElementById('tab-'+id);
      if(el) el.style.display='none';
    });
    document.getElementById('tab-'+t.dataset.tab).style.display='block';
  });
});

// ── history ──
function renderHistory(filter){
  const ms=store.matches;
  const filtered=filter==='all'?ms:ms.filter(m=>m.mode===filter);
  document.getElementById('history-count').textContent=`${filtered.length} match${filtered.length!==1?'es':''}`;
  const mS={addition:'Addition',multiplication:'Multiply',fractions:'Fractions',variation:'Variation'};
  if(!filtered.length){ document.getElementById('hist-body').innerHTML='<tr><td colspan="7" style="text-align:center;padding:22px;color:var(--muted);">No matches yet. Go play!</td></tr>'; return; }
  document.getElementById('hist-body').innerHTML=filtered.map(m=>{
    const rc=m.result==='win'?'badge-suc':m.result==='loss'?'badge-dan':'badge-warn';
    const when=new Date(m.date).toLocaleDateString(undefined,{month:'short',day:'numeric'});
    return `<tr>
      <td><span class="pill ${rc}">${m.result}</span></td>
      <td style="color:var(--text);">${mS[m.mode]||m.mode}</td>
      <td>${m.diff}</td>
      <td style="font-weight:700;">${m.pScore}–${m.bScore}</td>
      <td>${m.acc}%</td>
      <td>${m.avgSpeed?m.avgSpeed+'s':'—'}</td>
      <td>${when}</td>
    </tr>`;
  }).join('');
}

// ── settings / data ──
function exportCSV(){
  const ms=store.matches;
  if(!ms.length){ toast('No matches to export.'); return; }
  const rows=[['Result','Mode','Diff','Your Score','Bot Score','Acc','Avg Speed','Date'],...ms.map(m=>[m.result,m.mode,m.diff,m.pScore,m.bScore,m.acc+'%',m.avgSpeed?m.avgSpeed+'s':'',m.date])];
  const a=document.createElement('a');
  a.href='data:text/csv;charset=utf-8,'+encodeURIComponent(rows.map(r=>r.join(',')).join('\n'));
  a.download='math-battle-stats.csv'; a.click();
  toast('Exported!');
}
function resetStats(){
  if(!confirm('Reset all stats? This cannot be undone.')) return;
  ['mb_matches','mb_best','mb_qstats'].forEach(k=>localStorage.removeItem(k));
  updateSbBest(); toast('Stats cleared.');
}

// ── toast ──
let toastT=null;
function toast(msg){
  const el=document.getElementById('toast');
  el.textContent=msg; el.classList.add('show');
  clearTimeout(toastT);
  toastT=setTimeout(()=>el.classList.remove('show'),2400);
}

// ── init ──
applyTheme(localStorage.getItem('mb_theme')||'dark');
buildMenu();
</script>

<!-- Added by ChatGPT -->
<script>
/* Placeholder hooks for streaks/reset.
   Integrate with your existing game-end logic by calling updateDailyStreak()
   after a completed match. */
function updateDailyStreak(){
  const today=new Date().toISOString().slice(0,10);
  const last=localStorage.getItem("mb_lastPlayed");
  let streak=+(localStorage.getItem("mb_streak")||0);
  let best=+(localStorage.getItem("mb_bestStreak")||0);
  if(last!==today){
    if(last){
      const diff=(new Date(today)-new Date(last))/86400000;
      streak = diff===1 ? streak+1 : 1;
    }else streak=1;
    best=Math.max(best,streak);
    localStorage.setItem("mb_lastPlayed",today);
    localStorage.setItem("mb_streak",streak);
    localStorage.setItem("mb_bestStreak",best);
  }
}
function resetAllProgress(){
  if(!confirm("Reset all progress?")) return;
  Object.keys(localStorage).filter(k=>k.startsWith("mb_")).forEach(k=>localStorage.removeItem(k));
  location.reload();
}
</script>

</body>
</html>
