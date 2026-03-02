<!DOCTYPE html>

<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Walletero">
<meta name="theme-color" content="#0a0f1e">
<title>Walletero</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0a0f1e;
  --bg2: #111827;
  --bg3: #1a2235;
  --card: #1e2d45;
  --border: #2a3a55;
  --text: #f0f4ff;
  --text2: #8899bb;
  --text3: #4a5a7a;
  --green: #22d37a;
  --green2: #16a85a;
  --red: #ff4d6a;
  --red2: #cc2244;
  --blue: #3b8bff;
  --blue2: #1a5fd4;
  --yellow: #fbbf24;
  --purple: #a78bfa;
  --accent: #3b8bff;
  --shadow: 0 4px 24px rgba(0,0,0,0.4);
  --radius: 18px;
  --radius-sm: 12px;
}
[data-theme="light"] {
  --bg: #f4f6fb;
  --bg2: #eaecf5;
  --bg3: #dde2ef;
  --card: #ffffff;
  --border: #d0d8ee;
  --text: #0d1829;
  --text2: #4a5a7a;
  --text3: #9aaac8;
  --shadow: 0 4px 24px rgba(0,0,0,0.08);
}
* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
html, body { height:100%; overflow:hidden; }
body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--text);
  transition: background 0.3s, color 0.3s;
  overscroll-behavior: none;
}

/* LAYOUT */
#app { display:flex; flex-direction:column; height:100vh; height:100dvh; }
#header {
padding: 52px 20px 16px;
display: flex;
align-items: center;
justify-content: space-between;
background: var(–bg);
position: relative;
z-index: 10;
}
.app-title { font-size: 22px; font-weight: 700; letter-spacing: -0.5px; }
.app-title span { color: var(–accent); }
.header-actions { display:flex; gap:10px; }
.btn-icon {
width: 38px; height: 38px;
border-radius: 50%;
background: var(–bg3);
border: none;
color: var(–text);
font-size: 16px;
cursor: pointer;
display: flex; align-items: center; justify-content: center;
transition: background 0.2s, transform 0.1s;
}
.btn-icon:active { transform: scale(0.92); }

#content {
flex: 1;
overflow-y: auto;
overflow-x: hidden;
-webkit-overflow-scrolling: touch;
scroll-behavior: smooth;
}
#content::-webkit-scrollbar { display: none; }

/* TABS */
#tabs {
display: flex;
background: var(–bg);
border-top: 1px solid var(–border);
padding: 8px 0 20px;
position: relative;
z-index: 10;
}
.tab {
flex: 1;
display: flex;
flex-direction: column;
align-items: center;
gap: 3px;
padding: 6px 4px;
border: none;
background: none;
color: var(–text3);
font-size: 10px;
font-family: ‘DM Sans’, sans-serif;
font-weight: 500;
cursor: pointer;
transition: color 0.2s;
}
.tab .tab-icon { font-size: 20px; transition: transform 0.2s; }
.tab.active { color: var(–accent); }
.tab.active .tab-icon { transform: scale(1.15); }

/* SCREENS */
.screen { display: none; padding: 16px 16px 24px; }
.screen.active { display: block; }

/* CARDS */
.card {
background: var(–card);
border-radius: var(–radius);
padding: 18px;
border: 1px solid var(–border);
box-shadow: var(–shadow);
margin-bottom: 14px;
}

/* BALANCE CARD */
.balance-card {
background: linear-gradient(135deg, var(–blue2) 0%, var(–blue) 60%, #6ab4ff 100%);
border: none;
padding: 24px 20px;
position: relative;
overflow: hidden;
}
.balance-card::before {
content: ‘’;
position: absolute;
top: -40px; right: -40px;
width: 160px; height: 160px;
border-radius: 50%;
background: rgba(255,255,255,0.07);
}
.balance-card::after {
content: ‘’;
position: absolute;
bottom: -20px; left: 30px;
width: 100px; height: 100px;
border-radius: 50%;
background: rgba(255,255,255,0.05);
}
.balance-label { font-size: 12px; font-weight: 500; opacity: 0.8; margin-bottom: 4px; }
.balance-amount {
font-size: 38px;
font-weight: 700;
letter-spacing: -1px;
color: #fff;
font-family: ‘DM Mono’, monospace;
}
.balance-sub {
display: flex;
gap: 20px;
margin-top: 16px;
}
.balance-sub-item { display: flex; flex-direction: column; gap: 2px; }
.balance-sub-label { font-size: 11px; opacity: 0.75; }
.balance-sub-value { font-size: 16px; font-weight: 600; color: #fff; font-family: ‘DM Mono’, monospace; }

/* QUICK STATS */
.stats-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 14px; }
.stat-card {
background: var(–card);
border-radius: var(–radius-sm);
padding: 14px;
border: 1px solid var(–border);
}
.stat-label { font-size: 11px; color: var(–text2); margin-bottom: 4px; font-weight: 500; }
.stat-value { font-size: 20px; font-weight: 700; font-family: ‘DM Mono’, monospace; }
.stat-value.green { color: var(–green); }
.stat-value.red { color: var(–red); }
.stat-change { font-size: 10px; color: var(–text3); margin-top: 2px; }

/* TRANSACTION LIST */
.section-header {
display: flex;
align-items: center;
justify-content: space-between;
margin-bottom: 10px;
}
.section-title { font-size: 15px; font-weight: 600; }
.see-all { font-size: 12px; color: var(–accent); cursor: pointer; }

.tx-item {
display: flex;
align-items: center;
gap: 12px;
padding: 12px 0;
border-bottom: 1px solid var(–border);
animation: fadeIn 0.3s ease;
}
.tx-item:last-child { border-bottom: none; }
@keyframes fadeIn { from { opacity:0; transform: translateY(6px); } to { opacity:1; transform:none; } }

.tx-icon {
width: 40px; height: 40px;
border-radius: 50%;
display: flex;
align-items: center;
justify-content: center;
font-size: 18px;
flex-shrink: 0;
}
.tx-icon.income { background: rgba(34,211,122,0.15); }
.tx-icon.expense { background: rgba(255,77,106,0.15); }
.tx-info { flex: 1; min-width: 0; }
.tx-desc { font-size: 14px; font-weight: 500; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.tx-meta { font-size: 11px; color: var(–text2); margin-top: 2px; }
.tx-amount {
font-size: 15px;
font-weight: 600;
font-family: ‘DM Mono’, monospace;
flex-shrink: 0;
}
.tx-amount.income { color: var(–green); }
.tx-amount.expense { color: var(–red); }

/* FAB BUTTON */
#fab {
position: fixed;
bottom: 100px;
right: 20px;
width: 56px; height: 56px;
border-radius: 50%;
background: linear-gradient(135deg, var(–blue), var(–blue2));
border: none;
color: #fff;
font-size: 26px;
cursor: pointer;
box-shadow: 0 6px 20px rgba(59,139,255,0.45);
display: flex; align-items: center; justify-content: center;
transition: transform 0.2s, box-shadow 0.2s;
z-index: 100;
}
#fab:active { transform: scale(0.9); }

/* MODAL */
.modal-overlay {
position: fixed;
inset: 0;
background: rgba(0,0,0,0.6);
backdrop-filter: blur(8px);
-webkit-backdrop-filter: blur(8px);
z-index: 200;
display: flex;
align-items: flex-end;
opacity: 0;
pointer-events: none;
transition: opacity 0.3s;
}
.modal-overlay.open { opacity: 1; pointer-events: all; }
.modal {
width: 100%;
background: var(–bg2);
border-radius: 28px 28px 0 0;
padding: 20px 20px 40px;
transform: translateY(100%);
transition: transform 0.4s cubic-bezier(0.34,1.1,0.64,1);
max-height: 92dvh;
overflow-y: auto;
}
.modal-overlay.open .modal { transform: translateY(0); }
.modal-handle {
width: 40px; height: 4px;
background: var(–border);
border-radius: 2px;
margin: 0 auto 20px;
}
.modal-title { font-size: 18px; font-weight: 700; margin-bottom: 20px; text-align: center; }

/* FORM */
.form-group { margin-bottom: 14px; }
.form-label { font-size: 12px; font-weight: 600; color: var(–text2); margin-bottom: 6px; display: block; text-transform: uppercase; letter-spacing: 0.5px; }
.form-input {
width: 100%;
background: var(–bg3);
border: 1.5px solid var(–border);
border-radius: var(–radius-sm);
padding: 13px 14px;
color: var(–text);
font-size: 16px;
font-family: ‘DM Sans’, sans-serif;
outline: none;
transition: border-color 0.2s;
}
.form-input:focus { border-color: var(–accent); }
.form-input::placeholder { color: var(–text3); }
textarea.form-input { resize: none; height: 80px; }

/* TYPE TOGGLE */
.type-toggle {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 8px;
margin-bottom: 14px;
}
.type-btn {
padding: 12px;
border-radius: var(–radius-sm);
border: 2px solid var(–border);
background: var(–bg3);
color: var(–text2);
font-size: 14px;
font-weight: 600;
cursor: pointer;
transition: all 0.2s;
font-family: ‘DM Sans’, sans-serif;
}
.type-btn.active-income { background: rgba(34,211,122,0.15); border-color: var(–green); color: var(–green); }
.type-btn.active-expense { background: rgba(255,77,106,0.15); border-color: var(–red); color: var(–red); }

/* CATEGORIES */
.cats-grid {
display: grid;
grid-template-columns: repeat(4, 1fr);
gap: 8px;
margin-bottom: 14px;
}
.cat-btn {
display: flex; flex-direction: column; align-items: center; gap: 4px;
padding: 10px 4px;
border-radius: 12px;
border: 1.5px solid var(–border);
background: var(–bg3);
cursor: pointer;
transition: all 0.2s;
font-family: ‘DM Sans’, sans-serif;
}
.cat-btn span:first-child { font-size: 22px; }
.cat-btn span:last-child { font-size: 9px; color: var(–text2); font-weight: 500; }
.cat-btn.active { border-color: var(–accent); background: rgba(59,139,255,0.12); }

/* PRIMARY BTN */
.btn-primary {
width: 100%;
padding: 15px;
border-radius: var(–radius-sm);
background: linear-gradient(135deg, var(–blue), var(–blue2));
border: none;
color: #fff;
font-size: 16px;
font-weight: 600;
cursor: pointer;
font-family: ‘DM Sans’, sans-serif;
transition: transform 0.15s, box-shadow 0.15s;
box-shadow: 0 4px 14px rgba(59,139,255,0.4);
}
.btn-primary:active { transform: scale(0.97); }

/* CHART AREA */
.chart-wrap {
position: relative;
height: 200px;
margin: 4px 0 8px;
}
canvas { border-radius: 8px; }

/* DONUT WRAPPER */
.donut-wrap {
display: flex;
align-items: center;
gap: 16px;
}
.donut-canvas { flex-shrink: 0; }
.donut-legend { flex: 1; display: flex; flex-direction: column; gap: 8px; }
.legend-item { display: flex; align-items: center; gap: 8px; }
.legend-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
.legend-label { font-size: 12px; color: var(–text2); flex: 1; }
.legend-value { font-size: 12px; font-weight: 600; font-family: ‘DM Mono’, monospace; }

/* BUDGET BARS */
.budget-item { margin-bottom: 16px; }
.budget-header { display: flex; justify-content: space-between; margin-bottom: 6px; }
.budget-cat { font-size: 13px; font-weight: 500; }
.budget-amounts { font-size: 11px; color: var(–text2); font-family: ‘DM Mono’, monospace; }
.progress-bar {
height: 8px;
background: var(–bg3);
border-radius: 4px;
overflow: hidden;
}
.progress-fill {
height: 100%;
border-radius: 4px;
transition: width 0.6s cubic-bezier(0.34,1.1,0.64,1);
}

/* GOALS */
.goal-card {
background: var(–card);
border-radius: var(–radius);
padding: 16px;
border: 1px solid var(–border);
margin-bottom: 12px;
}
.goal-header { display: flex; align-items: center; gap: 10px; margin-bottom: 12px; }
.goal-icon { font-size: 28px; }
.goal-title { font-size: 15px; font-weight: 600; }
.goal-sub { font-size: 11px; color: var(–text2); margin-top: 2px; }
.goal-progress { margin-bottom: 8px; }
.goal-amounts { display: flex; justify-content: space-between; font-size: 12px; color: var(–text2); margin-top: 4px; }
.goal-pct { font-weight: 700; color: var(–accent); }

/* SEARCH */
.search-wrap { position: relative; margin-bottom: 14px; }
.search-input {
width: 100%;
background: var(–card);
border: 1.5px solid var(–border);
border-radius: 50px;
padding: 12px 16px 12px 42px;
color: var(–text);
font-size: 14px;
font-family: ‘DM Sans’, sans-serif;
outline: none;
transition: border-color 0.2s;
}
.search-input:focus { border-color: var(–accent); }
.search-icon {
position: absolute;
left: 14px; top: 50%;
transform: translateY(-50%);
color: var(–text3);
font-size: 16px;
}
.filter-row { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 4px; margin-bottom: 12px; }
.filter-row::-webkit-scrollbar { display: none; }
.filter-chip {
flex-shrink: 0;
padding: 6px 14px;
border-radius: 50px;
border: 1.5px solid var(–border);
background: var(–bg3);
color: var(–text2);
font-size: 12px;
font-weight: 500;
cursor: pointer;
font-family: ‘DM Sans’, sans-serif;
transition: all 0.2s;
}
.filter-chip.active { background: var(–accent); border-color: var(–accent); color: #fff; }

/* EMPTY STATE */
.empty-state {
text-align: center;
padding: 40px 20px;
color: var(–text3);
}
.empty-state .empty-icon { font-size: 48px; margin-bottom: 12px; }
.empty-state p { font-size: 14px; }

/* NLP RESULT */
.nlp-result {
background: var(–bg3);
border-radius: var(–radius-sm);
padding: 14px;
margin-bottom: 14px;
border: 1.5px solid var(–border);
display: none;
}
.nlp-result.show { display: block; }
.nlp-row { display: flex; justify-content: space-between; align-items: center; padding: 4px 0; }
.nlp-key { font-size: 12px; color: var(–text2); }
.nlp-val { font-size: 13px; font-weight: 600; }

/* TOAST */
.toast {
position: fixed;
top: 60px;
left: 50%;
transform: translateX(-50%) translateY(-80px);
background: var(–card);
border: 1px solid var(–border);
padding: 12px 20px;
border-radius: 50px;
font-size: 13px;
font-weight: 500;
box-shadow: var(–shadow);
z-index: 999;
transition: transform 0.4s cubic-bezier(0.34,1.1,0.64,1);
white-space: nowrap;
}
.toast.show { transform: translateX(-50%) translateY(0); }

/* MONTH SELECTOR */
.month-nav {
display: flex;
align-items: center;
justify-content: center;
gap: 16px;
margin-bottom: 14px;
}
.month-btn {
background: var(–bg3);
border: none;
color: var(–text);
width: 32px; height: 32px;
border-radius: 50%;
font-size: 16px;
cursor: pointer;
display: flex; align-items: center; justify-content: center;
}
.month-label { font-size: 15px; font-weight: 600; }

/* MIC CENTER TAB BUTTON */
#micTab {
width: 58px; height: 58px;
border-radius: 50%;
background: linear-gradient(135deg, #3b8bff, #1a5fd4);
border: none;
cursor: pointer;
position: relative;
margin-top: -18px;
flex-shrink: 0;
box-shadow: 0 4px 20px rgba(59,139,255,0.5);
transition: transform 0.15s, box-shadow 0.15s;
display: flex; align-items: center; justify-content: center;
}
#micTab:active { transform: scale(0.92); }
#micTab.listening {
background: linear-gradient(135deg, #ff4d6a, #cc2244);
box-shadow: 0 4px 24px rgba(255,77,106,0.6);
}
#micInner {
width: 58px; height: 58px;
display: flex; align-items: center; justify-content: center;
position: relative; z-index: 2;
}
#micRings { position: absolute; inset: 0; border-radius: 50%; }
.mic-ring {
position: absolute;
border-radius: 50%;
border: 1.5px solid rgba(255,255,255,0.3);
opacity: 0;
}
#micTab.listening .mic-ring { animation: micPulseRing 1.8s ease-out infinite; }
.mic-ring.r1 { inset: -6px; animation-delay: 0s !important; }
.mic-ring.r2 { inset: -13px; animation-delay: 0.4s !important; }
.mic-ring.r3 { inset: -20px; animation-delay: 0.8s !important; }
@keyframes micPulseRing {
0% { opacity: 0.7; transform: scale(0.95); }
100% { opacity: 0; transform: scale(1.1); }
}

/* MIC OVERLAY */
#micOverlay {
position: fixed; inset: 0;
background: rgba(5,10,20,0.92);
backdrop-filter: blur(20px);
-webkit-backdrop-filter: blur(20px);
z-index: 500;
display: none;
align-items: center;
justify-content: center;
flex-direction: column;
}
#micOverlay.active { display: flex; }
#micOverlayInner { text-align: center; padding: 40px 32px; width: 100%; }
#micPulse {
position: relative;
width: 100px; height: 100px;
margin: 0 auto 28px;
display: flex; align-items: center; justify-content: center;
}
.pulse-ring {
position: absolute;
border-radius: 50%;
border: 1.5px solid rgba(59,139,255,0.4);
animation: overlayPulse 2s ease-out infinite;
}
.pulse-ring.pr1 { inset: 0; animation-delay: 0s; }
.pulse-ring.pr2 { inset: -16px; animation-delay: 0.5s; }
.pulse-ring.pr3 { inset: -32px; animation-delay: 1s; }
@keyframes overlayPulse {
0% { opacity: 0.8; transform: scale(0.95); }
100% { opacity: 0; transform: scale(1.15); }
}
#micOrbBtn {
width: 100px; height: 100px;
border-radius: 50%;
background: linear-gradient(135deg, rgba(59,139,255,0.3), rgba(26,95,212,0.5));
border: 1.5px solid rgba(59,139,255,0.5);
display: flex; align-items: center; justify-content: center;
cursor: pointer;
position: relative; z-index: 2;
transition: background 0.3s;
}
#micOrbBtn.active-listening {
background: linear-gradient(135deg, rgba(255,77,106,0.3), rgba(204,34,68,0.5));
border-color: rgba(255,77,106,0.5);
}
#micStatus {
font-size: 18px;
font-weight: 600;
color: var(–text);
margin-bottom: 12px;
letter-spacing: 0.3px;
}
#micTranscript {
font-size: 14px;
color: var(–text2);
min-height: 44px;
line-height: 1.5;
padding: 0 20px;
margin-bottom: 32px;
font-style: italic;
}
#micCancelBtn {
background: rgba(255,255,255,0.08);
border: 1px solid rgba(255,255,255,0.15);
color: var(–text2);
padding: 12px 32px;
border-radius: 50px;
font-size: 14px;
cursor: pointer;
font-family: ‘DM Sans’, sans-serif;
}

/* ANIMATIONS */
@keyframes slideUp { from { transform: translateY(20px); opacity:0; } to { transform:none; opacity:1; } }
.slide-up { animation: slideUp 0.4s ease forwards; }

/* UNDO TOAST - swipeable */
.undo-toast {
position: fixed;
bottom: 110px;
left: 16px; right: 16px;
background: rgba(20,30,50,0.82);
backdrop-filter: blur(20px);
-webkit-backdrop-filter: blur(20px);
border: 1px solid rgba(255,255,255,0.10);
padding: 14px 16px;
border-radius: 20px;
display: flex;
align-items: center;
gap: 12px;
box-shadow: 0 8px 32px rgba(0,0,0,0.5);
z-index: 998;
opacity: 0;
transform: translateY(20px);
transition: opacity 0.3s, transform 0.35s cubic-bezier(0.34,1.1,0.64,1);
pointer-events: none;
touch-action: pan-y;
cursor: grab;
}
.undo-toast.show { opacity:1; transform: translateY(0); pointer-events:all; }
.undo-toast.swiping { transition: transform 0.1s linear; }
.undo-label { font-size:13px; color:var(–text); flex:1; line-height:1.3; }
.undo-timer {
width: 28px; height: 28px;
border-radius: 50%;
background: conic-gradient(var(–red) 100%, var(–bg3) 100%);
display: flex; align-items: center; justify-content: center;
font-size: 11px; font-weight: 700; color: var(–text);
flex-shrink: 0;
}
.undo-btn {
background: var(–blue);
border: none;
color: #fff;
padding: 8px 16px;
border-radius: 50px;
font-size: 13px;
font-weight: 600;
cursor: pointer;
font-family: ‘DM Sans’, sans-serif;
white-space: nowrap;
}

/* TRASH SCREEN */
.trash-item {
display: flex;
align-items: center;
gap: 12px;
padding: 12px;
background: var(–bg3);
border-radius: 12px;
margin-bottom: 8px;
opacity: 0.75;
}
.trash-expiry { font-size: 10px; color: var(–red); margin-top: 2px; }
.restore-btn {
background: rgba(34,211,122,0.15);
border: 1.5px solid var(–green);
color: var(–green);
padding: 6px 12px;
border-radius: 8px;
font-size: 12px;
font-weight: 600;
cursor: pointer;
font-family: ‘DM Sans’, sans-serif;
flex-shrink: 0;
}
.perm-del-btn {
background: rgba(255,77,106,0.12);
border: 1.5px solid var(–red);
color: var(–red);
padding: 6px 10px;
border-radius: 8px;
font-size: 12px;
cursor: pointer;
font-family: ‘DM Sans’, sans-serif;
flex-shrink: 0;
}

/* EYE BUTTON */
.eye-btn {
position: absolute;
right: 14px; bottom: 14px;
width: 32px; height: 32px;
background: rgba(255,255,255,0.12);
border: 1px solid rgba(255,255,255,0.22);
border-radius: 50%;
color: rgba(255,255,255,0.75);
font-size: 15px;
cursor: pointer;
display: flex; align-items: center; justify-content: center;
backdrop-filter: blur(6px);
-webkit-backdrop-filter: blur(6px);
transition: background 0.2s;
line-height: 1;
}
.eye-btn:active { background: rgba(255,255,255,0.22); }
.balance-hidden { filter: blur(9px); user-select: none; pointer-events:none; }

/* LIQUID GLASS ICONS - used in tx list, categories, etc */
.lg-icon {
width: 40px; height: 40px;
border-radius: 50%;
display: flex; align-items: center; justify-content: center;
flex-shrink: 0;
position: relative;
overflow: hidden;
}
.lg-icon::before {
content: ‘’;
position: absolute; inset: 0;
border-radius: 50%;
backdrop-filter: blur(8px);
-webkit-backdrop-filter: blur(8px);
border: 1px solid rgba(255,255,255,0.18);
}
.lg-icon svg {
width: 20px; height: 20px;
position: relative; z-index: 1;
stroke-width: 1.8;
stroke-linecap: round;
stroke-linejoin: round;
fill: none;
}
.lg-icon.income { background: rgba(34,211,122,0.18); }
.lg-icon.income svg { stroke: #22d37a; }
.lg-icon.expense { background: rgba(255,77,106,0.18); }
.lg-icon.expense svg { stroke: #ff4d6a; }

/* Category liquid glass icons */
.cat-lg {
width: 38px; height: 38px;
border-radius: 50%;
display: flex; align-items: center; justify-content: center;
flex-shrink: 0;
position: relative;
overflow: hidden;
}
.cat-lg::before {
content: ‘’;
position: absolute; inset: 0;
border-radius: 50%;
border: 1.5px solid rgba(255,255,255,0.15);
}
.cat-lg svg {
width: 18px; height: 18px;
position: relative; z-index: 1;
stroke-width: 1.8;
stroke-linecap: round;
stroke-linejoin: round;
fill: none;
}

/* Tab bar icons - SVG based */
.tab-svg {
width: 22px; height: 22px;
stroke-width: 1.8;
stroke-linecap: round;
stroke-linejoin: round;
fill: none;
stroke: currentColor;
}

/* Trash icon in corner of presupuesto/metas */
.corner-trash {
position: absolute;
top: 14px; right: 14px;
width: 30px; height: 30px;
background: rgba(255,77,106,0.12);
border: 1px solid rgba(255,77,106,0.25);
border-radius: 8px;
display: flex; align-items: center; justify-content: center;
cursor: pointer;
}
.corner-trash svg { width:14px; height:14px; stroke: var(–red); stroke-width:1.8; fill:none; stroke-linecap:round; stroke-linejoin:round; }
</style>

</head>
<body data-theme="dark">
<div id="app">

  <!-- HEADER -->

  <div id="header">
    <div class="app-title">Wallet<span>ero</span></div>
    <div class="header-actions">
      <button class="btn-icon" id="themeToggle" title="Tema">
        <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/></svg>
      </button>
      <button class="btn-icon" onclick="switchTab('trash')" title="Papelera" style="position:relative;" id="trashHeaderBtn">
        <svg viewBox="0 0 24 24" width="17" height="17" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14H6L5 6"/><path d="M10 11v6M14 11v6"/><path d="M9 6V4h6v2"/></svg>
        <span id="trashBadge" style="display:none;position:absolute;top:4px;right:4px;width:8px;height:8px;background:var(--red);border-radius:50%;"></span>
      </button>
    </div>
  </div>

  <!-- CONTENT -->

  <div id="content">

```
<!-- HOME SCREEN -->
<div class="screen active" id="screen-home">
  <div class="balance-card card slide-up" style="position:relative">
    <div class="balance-label">Balance total</div>
    <div id="balanceWrap">
      <div class="balance-amount" id="balanceAmount">$0.00</div>
      <div class="balance-sub">
        <div class="balance-sub-item">
          <div class="balance-sub-label">↑ Ingresos</div>
          <div class="balance-sub-value" id="totalIncome">$0.00</div>
        </div>
        <div class="balance-sub-item">
          <div class="balance-sub-label">↓ Gastos</div>
          <div class="balance-sub-value" id="totalExpense">$0.00</div>
        </div>
      </div>
    </div>
    <button class="eye-btn" id="eyeBtn" onclick="toggleBalance()" aria-label="Ocultar balance">
      <svg id="eyeIcon" viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="rgba(255,255,255,0.8)" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/></svg>
    </button>
  </div>

  <div class="stats-row">
    <div class="stat-card">
      <div class="stat-label">Este mes</div>
      <div class="stat-value red" id="monthExpense">$0</div>
      <div class="stat-change">en gastos</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Movimientos</div>
      <div class="stat-value" id="txCount" style="color:var(--blue)">0</div>
      <div class="stat-change">registrados</div>
    </div>
  </div>

  <div class="card">
    <div class="section-header">
      <div class="section-title">Recientes</div>
      <div class="see-all" onclick="switchTab('historial')">Ver todo</div>
    </div>
    <div id="recentList">
      <div class="empty-state">
        <p>Toca + para agregar tu primer movimiento</p>
      </div>
    </div>
  </div>

  <!-- METAS EN INICIO -->
  <div class="card">
    <div class="section-header">
      <div class="section-title">Metas de ahorro</div>
      <div class="see-all" onclick="showAddGoal()">+ Nueva</div>
    </div>
    <div id="goalsHome">
      <div class="empty-state" style="padding:12px 0;">
        <p style="font-size:13px;">Sin metas activas</p>
      </div>
    </div>
  </div>
</div>

<!-- GRAFICAS SCREEN -->
<div class="screen" id="screen-graficas">
  <div class="month-nav">
    <button class="month-btn" onclick="changeMonth(-1)">‹</button>
    <div class="month-label" id="monthLabel">Marzo 2026</div>
    <button class="month-btn" onclick="changeMonth(1)">›</button>
  </div>

  <div class="card">
    <div class="section-title" style="margin-bottom:12px">Flujo mensual</div>
    <div class="chart-wrap">
      <canvas id="barChart"></canvas>
    </div>
  </div>

  <div class="card">
    <div class="section-title" style="margin-bottom:14px">Gastos por categoria</div>
    <div class="donut-wrap">
      <canvas class="donut-canvas" id="donutChart" width="130" height="130"></canvas>
      <div class="donut-legend" id="donutLegend"></div>
    </div>
  </div>

  <div class="card">
    <div class="section-title" style="margin-bottom:14px">Linea de tiempo</div>
    <div class="chart-wrap">
      <canvas id="lineChart"></canvas>
    </div>
  </div>
</div>

<!-- PRESUPUESTO SCREEN -->
<div class="screen" id="screen-presupuesto">
  <div class="card" style="position:relative">
    <div class="section-header">
      <div class="section-title">Presupuesto mensual</div>
      <div style="display:flex;gap:8px;align-items:center;">
        <div class="see-all" onclick="showBudgetModal()">Editar</div>
        <button class="corner-trash" onclick="switchTab('trash')" title="Papelera" style="position:static;width:26px;height:26px;">
          <svg viewBox="0 0 24 24"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14H6L5 6"/><path d="M10 11v6M14 11v6"/><path d="M9 6V4h6v2"/></svg>
        </button>
      </div>
    </div>
    <div id="budgetList">
      <div class="empty-state">
        <p>Configura tu presupuesto por categoria</p>
      </div>
    </div>
  </div>

  <div class="card" id="savingsCard" style="display:none">
    <div class="section-title" style="margin-bottom:12px">Resumen del mes</div>
    <div id="budgetSummary"></div>
  </div>
</div>

<!-- METAS SCREEN -->
<div class="screen" id="screen-metas">
  <div style="margin-bottom:14px;">
    <button class="btn-primary" onclick="showAddGoal()">+ Nueva meta de ahorro</button>
  </div>
  <div id="goalsList">
    <div class="empty-state">
      <p>Crea una meta para empezar a ahorrar</p>
    </div>
  </div>
</div>

<!-- HISTORIAL SCREEN -->
<div class="screen" id="screen-historial">
  <div class="search-wrap">
    <span class="search-icon">🔍</span>
    <input type="text" class="search-input" placeholder="Buscar movimiento..." id="searchInput" oninput="filterTx()">
  </div>
  <div class="filter-row" id="filterRow">
    <button class="filter-chip active" onclick="setFilter('todos',this)">Todos</button>
    <button class="filter-chip" onclick="setFilter('ingreso',this)">Ingresos</button>
    <button class="filter-chip" onclick="setFilter('gasto',this)">Gastos</button>
    <button class="filter-chip" onclick="setFilter('Comida',this)">Comida</button>
    <button class="filter-chip" onclick="setFilter('Transporte',this)">Transporte</button>
    <button class="filter-chip" onclick="setFilter('Trabajo',this)">Trabajo</button>
    <button class="filter-chip" onclick="setFilter('Salud',this)">Salud</button>
    <button class="filter-chip" onclick="setFilter('Venta',this)">Venta</button>
  </div>
  <div class="card" id="historialList"></div>
</div>

<!-- TRASH SCREEN -->
<div class="screen" id="screen-trash">
  <div style="display:flex;align-items:center;gap:10px;margin-bottom:14px;">
    <button onclick="history.back()||switchTab('home')" style="background:var(--bg3);border:none;color:var(--text);width:34px;height:34px;border-radius:50%;cursor:pointer;display:flex;align-items:center;justify-content:center;" id="trashBackBtn">
      <svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="15 18 9 12 15 6"/></svg>
    </button>
    <div style="font-size:16px;font-weight:600;">Papelera</div>
  </div>
  <div class="card" style="margin-bottom:14px;">
    <div style="font-size:13px;color:var(--text2);line-height:1.5;">
      Los elementos eliminados se borran permanentemente despues de <strong style="color:var(--red)">24 horas</strong>.
    </div>
  </div>
  <div id="trashList">
    <div class="empty-state"><p>La papelera esta vacia</p></div>
  </div>
</div>
```

  </div><!-- end content -->

  <!-- TABS -->

  <div id="tabs">
    <button class="tab active" onclick="switchTab('home')" id="tab-home">
      <svg class="tab-svg" viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>
      <span>Inicio</span>
    </button>
    <button class="tab" onclick="switchTab('graficas')" id="tab-graficas">
      <svg class="tab-svg" viewBox="0 0 24 24"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg>
      <span>Graficas</span>
    </button>

```
<!-- MIC CENTER BUTTON -->
<button id="micTab" onclick="activateMic()">
  <div id="micRings">
    <div class="mic-ring r1"></div>
    <div class="mic-ring r2"></div>
    <div class="mic-ring r3"></div>
  </div>
  <div id="micInner">
    <svg viewBox="0 0 24 24" width="22" height="22" fill="none" stroke="white" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
      <rect x="9" y="2" width="6" height="12" rx="3"/>
      <path d="M19 10a7 7 0 0 1-14 0"/><line x1="12" y1="19" x2="12" y2="22"/><line x1="8" y1="22" x2="16" y2="22"/>
    </svg>
  </div>
</button>

<button class="tab" onclick="switchTab('presupuesto')" id="tab-presupuesto">
  <svg class="tab-svg" viewBox="0 0 24 24"><rect x="2" y="3" width="20" height="14" rx="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></svg>
  <span>Presupuesto</span>
</button>
<button class="tab" onclick="switchTab('historial')" id="tab-historial">
  <svg class="tab-svg" viewBox="0 0 24 24"><line x1="8" y1="6" x2="21" y2="6"/><line x1="8" y1="12" x2="21" y2="12"/><line x1="8" y1="18" x2="21" y2="18"/><line x1="3" y1="6" x2="3.01" y2="6"/><line x1="3" y1="12" x2="3.01" y2="12"/><line x1="3" y1="18" x2="3.01" y2="18"/></svg>
  <span>Historial</span>
</button>
```

  </div>

  <!-- tab-metas dummy for switchTab compatibility -->

  <div id="tab-metas" style="display:none"></div>
  <div id="tab-trash" style="display:none"></div>

  <!-- MIC OVERLAY -->

  <div id="micOverlay">
    <div id="micOverlayInner">
      <div id="micPulse">
        <div class="pulse-ring pr1"></div>
        <div class="pulse-ring pr2"></div>
        <div class="pulse-ring pr3"></div>
        <div id="micOrbBtn" onclick="stopMic()">
          <svg viewBox="0 0 24 24" width="28" height="28" fill="none" stroke="white" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
            <rect x="9" y="2" width="6" height="12" rx="3"/>
            <path d="M19 10a7 7 0 0 1-14 0"/><line x1="12" y1="19" x2="12" y2="22"/><line x1="8" y1="22" x2="16" y2="22"/>
          </svg>
        </div>
      </div>
      <div id="micStatus">Escuchando...</div>
      <div id="micTranscript"></div>
      <button id="micCancelBtn" onclick="cancelMic()">Cancelar</button>
    </div>
  </div>

</div><!-- end app -->

<!-- FAB -->

<button id="fab" onclick="showAddModal()">+</button>

<!-- TOAST -->

<div class="toast" id="toast"></div>

<!-- UNDO TOAST -->

<div class="undo-toast" id="undoToast">
  <div class="undo-label" id="undoLabel">Eliminado</div>
  <div class="undo-timer" id="undoTimer">5</div>
  <button class="undo-btn" onclick="undoDelete()">Devolver</button>
</div>

<!-- ADD TRANSACTION MODAL -->

<div class="modal-overlay" id="addModal">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-title">Nuevo movimiento</div>

```
<div class="type-toggle">
  <button class="type-btn active-expense" id="btnGasto" onclick="setType('gasto')">↓ Gasto</button>
  <button class="type-btn" id="btnIngreso" onclick="setType('ingreso')">↑ Ingreso</button>
</div>

<div class="form-group">
  <label class="form-label">Descripcion en lenguaje natural</label>
  <input type="text" class="form-input" id="nlpInput" placeholder="Describir..." oninput="runNLP()">
  <div style="font-size:11px;color:var(--text3);margin-top:5px;">Puedes escribir varios items separados por "y" o comas</div>
</div>

<!-- MULTI ITEM PREVIEW -->
<div id="multiPreview" style="display:none;margin-bottom:14px;">
  <div style="font-size:12px;font-weight:600;color:var(--text2);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:8px;">Items detectados</div>
  <div id="multiItems"></div>
  <div style="display:flex;justify-content:space-between;align-items:center;margin-top:10px;padding:10px 12px;background:var(--bg3);border-radius:10px;">
    <span style="font-size:13px;color:var(--text2);">Total</span>
    <span style="font-size:16px;font-weight:700;font-family:'DM Mono',monospace;color:var(--accent);" id="multiTotal">$0.00</span>
  </div>
</div>

<!-- SINGLE ITEM PREVIEW -->
<div class="nlp-result" id="nlpResult">
  <div class="nlp-row">
    <span class="nlp-key">Detectado</span>
    <span class="nlp-val" id="nlpType"></span>
  </div>
  <div class="nlp-row">
    <span class="nlp-key">Monto</span>
    <span class="nlp-val" id="nlpMonto"></span>
  </div>
  <div class="nlp-row">
    <span class="nlp-key">Categoria</span>
    <span class="nlp-val" id="nlpCat"></span>
  </div>
</div>

<!-- SINGLE ITEM FIELDS -->
<div id="singleFields">
  <div class="form-group">
    <label class="form-label">Descripcion</label>
    <input type="text" class="form-input" id="txDesc" placeholder="Descripcion del movimiento">
  </div>
  <div class="form-group">
    <label class="form-label">Monto (MXN)</label>
    <input type="number" class="form-input" id="txAmount" placeholder="0.00" step="0.01" inputmode="decimal">
  </div>
  <div class="form-group">
    <label class="form-label">Categoria</label>
    <div class="cats-grid" id="catsGrid"></div>
  </div>
</div>

<button class="btn-primary" id="saveBtn" onclick="saveTx()">Guardar movimiento</button>
<br><br>
<button style="width:100%;padding:12px;background:none;border:none;color:var(--text2);font-size:14px;cursor:pointer;font-family:'DM Sans',sans-serif;" onclick="closeModal('addModal')">Cancelar</button>
```

  </div>
</div>

<!-- BUDGET MODAL -->

<div class="modal-overlay" id="budgetModal">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-title">Presupuesto por categoria</div>
    <div id="budgetInputs"></div>
    <button class="btn-primary" onclick="saveBudget()">Guardar presupuesto</button>
    <br><br>
    <button style="width:100%;padding:12px;background:none;border:none;color:var(--text2);font-size:14px;cursor:pointer;font-family:'DM Sans',sans-serif;" onclick="closeModal('budgetModal')">Cancelar</button>
  </div>
</div>

<!-- GOAL MODAL -->

<div class="modal-overlay" id="goalModal">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-title">Nueva meta de ahorro</div>
    <div class="form-group">
      <label class="form-label">Nombre de la meta</label>
      <input type="text" class="form-input" id="goalName" placeholder="ej: Vacaciones, iPhone, Carro...">
    </div>
    <div class="form-group">
      <label class="form-label">Monto objetivo (MXN)</label>
      <input type="number" class="form-input" id="goalTarget" placeholder="0.00" inputmode="decimal">
    </div>
    <div class="form-group">
      <label class="form-label">Monto ahorrado actual (MXN)</label>
      <input type="number" class="form-input" id="goalCurrent" placeholder="0.00" inputmode="decimal">
    </div>
    <div class="form-group">
      <label class="form-label">Emoji / Icono</label>
      <input type="text" class="form-input" id="goalEmoji" placeholder="🎯" maxlength="2">
    </div>
    <button class="btn-primary" onclick="saveGoal()">Crear meta</button>
    <br><br>
    <button style="width:100%;padding:12px;background:none;border:none;color:var(--text2);font-size:14px;cursor:pointer;font-family:'DM Sans',sans-serif;" onclick="closeModal('goalModal')">Cancelar</button>
  </div>
</div>

<script>
// =====================================================
// DATA LAYER
// =====================================================
var DB = {
  load: function() {
    try {
      var d = JSON.parse(localStorage.getItem('walletero_v1') || 'null');
      if(!d) d = JSON.parse(localStorage.getItem('finanzaspro_v1') || 'null'); // migrate
      return d || {txs:[],budgets:{},goals:[],trash:[]};
    } catch(e) { return {txs:[],budgets:{},goals:[],trash:[]}; }
  },
  save: function(data) {
    localStorage.setItem('walletero_v1', JSON.stringify(data));
  }
};

var state = DB.load();
if(!state.trash) state.trash=[];
var currentType = 'gasto';
var selectedCat = 'Otro';
var currentFilter = 'todos';
var viewMonth = new Date();
var balanceHidden = false;
var nlpTimer = null;
var pendingMultiItems = null;
var isMultiMode = false;
var undoQueue = null;
var undoInterval = null;

// =====================================================
// BALANCE EYE TOGGLE
// =====================================================
function toggleBalance() {
  balanceHidden = !balanceHidden;
  var wrap = document.getElementById('balanceWrap');
  var icon = document.getElementById('eyeIcon');
  wrap.classList.toggle('balance-hidden', balanceHidden);
  if(balanceHidden) {
    icon.innerHTML='<path d="M17.94 17.94A10.07 10.07 0 0 1 12 20c-7 0-11-8-11-8a18.45 18.45 0 0 1 5.06-5.94"/><path d="M9.9 4.24A9.12 9.12 0 0 1 12 4c7 0 11 8 11 8a18.5 18.5 0 0 1-2.16 3.19"/><line x1="1" y1="1" x2="23" y2="23"/>';
  } else {
    icon.innerHTML='<path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/>';
  }
}

// =====================================================
// UNDO / TRASH SYSTEM
// =====================================================
function softDelete(item, type) {
  // Cancel any pending undo first
  if(undoQueue) commitDelete();

  var trashItem = {
    item: item,
    type: type, // 'tx' or 'goal'
    deletedAt: Date.now(),
    expiresAt: Date.now() + 24*60*60*1000
  };
  state.trash.push(trashItem);
  DB.save(state);

  undoQueue = trashItem;
  showUndoToast(item, type);
}

function showUndoToast(item, type) {
  clearInterval(undoInterval);
  var label = type==='tx' ? (item.desc||'Movimiento') : (item.name||'Meta');
  document.getElementById('undoLabel').textContent = '"'+label+'" eliminado';
  var timeLeft = 5;
  document.getElementById('undoTimer').textContent = timeLeft;
  updateTimerRing(timeLeft);

  var toast = document.getElementById('undoToast');
  toast.classList.add('show');

  undoInterval = setInterval(function(){
    timeLeft--;
    document.getElementById('undoTimer').textContent = timeLeft;
    updateTimerRing(timeLeft);
    if(timeLeft <= 0) {
      clearInterval(undoInterval);
      toast.classList.remove('show');
      undoQueue = null;
      renderTrash();
    }
  }, 1000);
}

function updateTimerRing(t) {
  var pct = (t/5)*100;
  document.getElementById('undoTimer').style.background =
    'conic-gradient(var(--red) '+pct+'%, var(--bg3) '+pct+'%)';
}

function undoDelete() {
  if(!undoQueue) return;
  clearInterval(undoInterval);
  // Remove from trash
  state.trash = state.trash.filter(function(ti){ return ti !== undoQueue; });
  // Restore
  if(undoQueue.type === 'tx') {
    state.txs.push(undoQueue.item);
    renderHome(); renderHistorial();
  } else {
    state.goals.push(undoQueue.item);
    renderGoals();
  }
  DB.save(state);
  undoQueue = null;
  document.getElementById('undoToast').classList.remove('show');
  showToast('Movimiento restaurado');
}

function commitDelete() {
  clearInterval(undoInterval);
  document.getElementById('undoToast').classList.remove('show');
  undoQueue = null;
  renderTrash();
}

// =====================================================
// TRASH SCREEN
// =====================================================
function renderTrash() {
  // Purge items older than 24h
  var now = Date.now();
  state.trash = state.trash.filter(function(ti){ return ti.expiresAt > now; });
  DB.save(state);
  updateTrashBadge();

  var list = document.getElementById('trashList');
  if(!state.trash.length){
    list.innerHTML='<div class="empty-state"><div class="empty-icon">🗑️</div><p>La papelera esta vacia</p></div>';
    // Update trash tab badge
    document.getElementById('tab-trash').querySelector('.tab-icon').textContent='🗑️';
    return;
  }

  // Show badge if items
  document.getElementById('tab-trash').querySelector('.tab-icon').textContent='🗑️';
  list.innerHTML='';

  state.trash.slice().reverse().forEach(function(ti){
    var item = ti.item;
    var hoursLeft = Math.max(0, Math.floor((ti.expiresAt - now)/(1000*60*60)));
    var minsLeft  = Math.max(0, Math.floor((ti.expiresAt - now)/(1000*60)) % 60);
    var timeStr = hoursLeft > 0 ? hoursLeft+'h '+minsLeft+'m' : minsLeft+'m';

    var isTx = ti.type==='tx';
    var svgPath = isTx ? getCatSvg(item.cat||'Otro') : '<circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="6"/><circle cx="12" cy="12" r="2"/>';
    var strokeColor = isTx ? (item.tipo==='ingreso'?'#22d37a':'#ff4d6a') : '#a78bfa';
    var bgColor = isTx ? (item.tipo==='ingreso'?'rgba(34,211,122,0.15)':'rgba(255,77,106,0.15)') : 'rgba(167,139,250,0.15)';
    var label = isTx
      ? (item.tipo==='ingreso'?'+':'-')+fmt(item.monto)+' · '+item.desc
      : item.name+' · Meta '+fmt(item.target);

    var div=document.createElement('div');
    div.className='trash-item';
    div.innerHTML=
      '<div style="width:38px;height:38px;border-radius:50%;background:'+bgColor+';border:1px solid '+strokeColor.replace(')',',0.3)').replace('rgb','rgba')+';display:flex;align-items:center;justify-content:center;flex-shrink:0;">'+
        '<svg viewBox="0 0 24 24" width="17" height="17" fill="none" stroke="'+strokeColor+'" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">'+svgPath+'</svg>'+
      '</div>'+
      '<div style="flex:1;min-width:0;">'+
        '<div style="font-size:13px;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">'+label+'</div>'+
        '<div class="trash-expiry">Se borra en '+timeStr+'</div>'+
      '</div>'+
      '<button class="restore-btn" onclick="restoreFromTrash(\''+ti.deletedAt+'\')">Restaurar</button>'+
      '<button class="perm-del-btn" onclick="permanentDelete(\''+ti.deletedAt+'\')">'+
        '<svg viewBox="0 0 24 24" width="12" height="12" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>'+
      '</button>';
    list.appendChild(div);
  });
}

function restoreFromTrash(deletedAt) {
  var idx = state.trash.findIndex(function(ti){ return String(ti.deletedAt)===String(deletedAt); });
  if(idx===-1) return;
  var ti = state.trash[idx];
  state.trash.splice(idx,1);
  if(ti.type==='tx'){ state.txs.push(ti.item); renderHome(); renderHistorial(); }
  else { state.goals.push(ti.item); renderGoals(); }
  DB.save(state);
  renderTrash();
  showToast('Restaurado correctamente');
}

function permanentDelete(deletedAt) {
  state.trash = state.trash.filter(function(ti){ return String(ti.deletedAt)!==String(deletedAt); });
  DB.save(state);
  renderTrash();
  showToast('Eliminado permanentemente');
}

// =====================================================
// CATEGORIES CONFIG
// =====================================================
var CATS = [
  {id:'Comida',       emoji:'🍔', color:'#f97316'},
  {id:'Transporte',   emoji:'🚗', color:'#3b82f6'},
  {id:'Super',        emoji:'🛒', color:'#10b981'},
  {id:'Hogar',        emoji:'🏠', color:'#8b5cf6'},
  {id:'Salud',        emoji:'💊', color:'#ef4444'},
  {id:'Servicios',    emoji:'📱', color:'#06b6d4'},
  {id:'Compras',      emoji:'👗', color:'#ec4899'},
  {id:'Trabajo',      emoji:'💼', color:'#22d37a'},
  {id:'Venta',        emoji:'💰', color:'#fbbf24'},
  {id:'Transferencia',emoji:'↔️', color:'#94a3b8'},
  {id:'Entretenimiento',emoji:'🎬',color:'#a78bfa'},
  {id:'Otro',         emoji:'📌', color:'#64748b'}
];

function getCat(id) {
  return CATS.find(function(c){ return c.id===id; }) || CATS[CATS.length-1];
}

// =====================================================
// NLP ENGINE
// =====================================================
// Numero regex que preserva decimales con punto O coma
var NUM_RE = /\d{1,3}(?:,\d{3})*(?:[.,]\d{1,2})?|\d+(?:[.,]\d{1,2})?/g;

function parseNum(s) {
  // Si tiene coma de miles: 1,500 o 1,500.50
  if(/^\d{1,3}(?:,\d{3})+(?:\.\d{1,2})?$/.test(s)) return parseFloat(s.replace(/,/g,''));
  // Si tiene punto decimal: 2781.18
  if(/^\d+\.\d{1,2}$/.test(s)) return parseFloat(s);
  // Si tiene coma decimal: 2781,18
  if(/^\d+,\d{1,2}$/.test(s)) return parseFloat(s.replace(',','.'));
  return parseFloat(s.replace(/,/g,''));
}

// Detecta si el texto tiene MULTIPLES items con precios
// ej: "dona 12 y sabritas 18 y coca 23"
// Retorna array de {desc, monto} o null si es item unico
function extractMultiItems(input) {
  var t = input.toLowerCase();
  // Separadores: "y", "e", ",", "tambien", "ademas", "mas"
  // Ahora coma sola también funciona como separador
  var separators = /\s*,\s*|\s+(?:y|e|tambien|ademas|mas una?|mas un?)\s+/gi;
  var parts = t.split(separators);
  if(parts.length < 2) return null;

  var items = [];
  parts.forEach(function(part) {
    part = part.trim();
    // Buscar numero en esta parte
    NUM_RE.lastIndex = 0;
    var nums = [];
    var m;
    while((m = NUM_RE.exec(part)) !== null) {
      var n = parseNum(m[0]);
      var isYear = n>=1900&&n<=2099;
      if(!isYear && n>=1 && n<=999999) nums.push({val:n, idx:m.index, raw:m[0]});
    }
    if(!nums.length) return;
    // Tomar el numero mas grande como precio
    nums.sort(function(a,b){return b.val-a.val;});
    var precio = nums[0];
    // Descripcion: todo lo que no es el numero ni palabras conectoras
    var stopSmall = ['una','un','de','en','por','a','las','los','le','me','la','el','unas','unos'];
    var words = part.replace(precio.raw,'').replace(/[0-9.,]/g,'').trim().split(/\s+/);
    var descWords = words.filter(function(w){
      return w.length>1 && stopSmall.indexOf(w)===-1;
    });
    var desc = descWords.join(' ');
    if(!desc) desc = 'Item';
    desc = desc.charAt(0).toUpperCase() + desc.slice(1);
    items.push({desc: desc, monto: precio.val});
  });

  return items.length >= 2 ? items : null;
}

function extractMonto(input) {
  var t = input.toLowerCase();
  var products = ['omega 3','omega3','b12','b6','xbox 360','xbox 720','ps4','ps5','ps3',
    'iphone 15','iphone 14','iphone 13','iphone 12','iphone 11','galaxy s23','covid 19'];
  var tClean = t;
  for(var i=0;i<products.length;i++) tClean = tClean.replace(products[i],' PROD ');

  // Patron: X mil / Xk
  var mMil = tClean.match(/(\d+(?:[.,]\d+)?)\s*(?:mil|k)\b/i);
  if(mMil) return parseFloat(mMil[1].replace(',','.')) * 1000;

  // Patron: $1,500.50 o $2781.18
  var mPesos = tClean.match(/\$\s*(\d{1,3}(?:,\d{3})*(?:\.\d{1,2})?|\d+(?:[.,]\d{1,2})?)/);
  if(mPesos) return parseNum(mPesos[1]);

  // Patron: "pague 2781.18", "nomina 2781.18", "en 350.50"
  // CLAVE: el regex ahora captura decimales con punto explicitamente
  var keywords = ['pague','gaste','compre','vendi','cobre','cobro','deposito','nomina',
    'sueldo','quincena','monto','precio','total','costo','por','de','en','vale'];
  for(var k=0;k<keywords.length;k++){
    // Regex mejorado: captura numero con decimales OBLIGATORIO
    var re = new RegExp(keywords[k]+'\\s+(?:[a-z]+\\s+){0,2}(\\d+(?:[.,]\\d{1,2})?)(?:\\s|$)','i');
    var mm = tClean.match(re);
    if(mm){
      var v = parseNum(mm[1]);
      if(v>=1&&v<=9999999) return v;
    }
  }

  // Fallback: todos los numeros, tomar el mayor
  var nums = [];
  NUM_RE.lastIndex = 0;
  var m2;
  while((m2=NUM_RE.exec(tClean))!==null){
    var n=parseNum(m2[0]);
    var isYear=n>=1900&&n<=2099;
    var isTiny=n<5;
    if(!isYear&&!isTiny&&n<=9999999) nums.push(n);
  }
  if(!nums.length) return 0;
  nums.sort(function(a,b){return b-a;});
  return nums[0];
}

function nlpDetect(input) {
  var t = input.toLowerCase().replace(/[.,!?;:]/g,' ').replace(/\s+/g,' ').trim();
  var monto = extractMonto(input);

  var ventaWords = ['vendi','vendido','venta','vende'];
  var objetos = ['xbox','playstation','ps4','ps5','laptop','computadora','celular',
    'iphone','samsung','tablet','ipad','auto','carro','moto','bici','silla','mesa',
    'sofa','mueble','reloj','camara','drone','consola'];
  var tieneVenta=false, tieneObjeto=false;
  for(var v=0;v<ventaWords.length;v++) if(t.indexOf(ventaWords[v])!==-1){tieneVenta=true;break;}
  for(var o=0;o<objetos.length;o++) if(t.indexOf(objetos[o])!==-1){tieneObjeto=true;break;}

  var ingPats=[
    {p:['vendi','vendido','venta de','vente'],w:10},
    {p:['me depositaron','depositaron','me deposito'],w:10},
    {p:['me pagaron','me pago','me transfirieron','me mandaron'],w:10},
    {p:['cobro','cobre','cobrar'],w:9},
    {p:['recibi','recibo'],w:8},
    {p:['sueldo','salario','quincena','nomina'],w:10},
    {p:['aguinaldo','bono','utilidades'],w:10},
    {p:['freelance','honorarios','facture'],w:9},
    {p:['prestaron','me prestaron'],w:8},
    {p:['devolvieron','reembolso'],w:9},
    {p:['gane','premio','loteria'],w:9},
    {p:['trabajo','trabo'],w:5}
  ];
  var gasPats=[
    {p:['pague','pago de','pagar'],w:9},
    {p:['gaste','gasto','me costo'],w:9},
    {p:['compre','compra de'],w:9},
    {p:['uber','didi','taxi','cabify'],w:8},
    {p:['gasolina','gas lp'],w:8},
    {p:['renta','mensualidad'],w:9},
    {p:['comida','comer','restaurant','tacos','pizza'],w:7},
    {p:['super','walmart','soriana','oxxo'],w:8},
    {p:['farmacia','medicamento','doctor','consulta'],w:8},
    {p:['luz','agua','internet','telefono'],w:7},
    {p:['netflix','spotify','suscripcion'],w:8},
    {p:['deuda','tarjeta'],w:8}
  ];

  var sIng=0,sGas=0;
  for(var i=0;i<ingPats.length;i++) for(var j=0;j<ingPats[i].p.length;j++) if(t.indexOf(ingPats[i].p[j])!==-1){sIng+=ingPats[i].w;break;}
  for(var i=0;i<gasPats.length;i++) for(var j=0;j<gasPats[i].p.length;j++) if(t.indexOf(gasPats[i].p[j])!==-1){sGas+=gasPats[i].w;break;}
  if(tieneVenta&&tieneObjeto) sIng+=20;
  if(tieneVenta&&!tieneObjeto) sIng+=10;

  var tipo = sIng>=sGas ? 'ingreso' : 'gasto';

  var catMap = {
    'Transporte':['uber','didi','taxi','gasolina','camion','metro','bus','caseta'],
    'Comida':['comida','comer','restaurant','cafe','pizza','tacos','sushi','taqueria'],
    'Super':['super','supermercado','walmart','soriana','chedraui','costco','oxxo'],
    'Hogar':['renta','hipoteca','mantenimiento','luz','agua'],
    'Salud':['farmacia','medicamento','doctor','hospital','consulta','dentista','omega','vitamina'],
    'Servicios':['internet','telefono','netflix','spotify','suscripcion','streaming'],
    'Compras':['ropa','zapatos','tienda','liverpool','shein'],
    'Trabajo':['sueldo','salario','quincena','nomina','freelance','honorarios','bono','aguinaldo','trabo','trabajo'],
    'Venta':['vendi','vendido','venta'],
    'Transferencia':['transferencia','deposito','spei'],
    'Entretenimiento':['cine','concierto','evento','boleto','teatro','gym']
  };
  var cat='Otro';
  for(var clave in catMap){
    var pals=catMap[clave];
    for(var k=0;k<pals.length;k++) if(t.indexOf(pals[k])!==-1){cat=clave;break;}
    if(cat!=='Otro') break;
  }
  if(tieneVenta&&tieneObjeto) cat='Venta';

  var prio=objetos.concat(['sueldo','quincena','nomina','freelance','gasolina','uber','didi',
    'renta','farmacia','doctor','luz','agua','internet','netflix','spotify','super','walmart',
    'pizza','tacos','cafe','vitamina','omega','consulta','honorarios']);
  var stop=['pague','gaste','compre','vendi','me','el','la','de','en','un','una','que','por',
    'con','los','las','del','al','lo','mi','su','se','para','como','mas','ya','si','no',
    'hoy','ayer','pesos','mxn','dinero','trabo'];
  var desc='';
  for(var p=0;p<prio.length;p++) if(t.indexOf(prio[p])!==-1){desc=prio[p].charAt(0).toUpperCase()+prio[p].slice(1);break;}
  if(!desc){
    var words=t.split(' ');
    for(var p=0;p<words.length;p++){
      var pal=words[p].replace(/[^a-z]/g,'');
      if(pal.length>3&&stop.indexOf(pal)===-1&&isNaN(pal)){desc=pal.charAt(0).toUpperCase()+pal.slice(1);break;}
    }
  }
  if(!desc) desc=tipo==='ingreso'?'Ingreso':'Gasto';

  return {tipo:tipo, monto:monto, desc:desc, cat:cat};
}

// =====================================================
// UI HELPERS
// =====================================================
function fmt(n) {
  var num = parseFloat(n)||0;
  var parts = num.toFixed(2).split('.');
  parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g,',');
  return '$'+parts[0]+'.'+parts[1];
}

function fmtShort(n) {
  var num = parseFloat(n)||0;
  if(num>=1000) return '$'+(num/1000).toFixed(1)+'k';
  return '$'+Math.round(num);
}

function todayStr() {
  var d=new Date();
  return d.getDate()+'/'+(d.getMonth()+1)+'/'+d.getFullYear();
}

function monthStr(d) {
  var months=['Enero','Febrero','Marzo','Abril','Mayo','Junio',
    'Julio','Agosto','Septiembre','Octubre','Noviembre','Diciembre'];
  return months[d.getMonth()]+' '+d.getFullYear();
}

function showToast(msg) {
  var t=document.getElementById('toast');
  t.textContent=msg;
  t.classList.add('show');
  setTimeout(function(){t.classList.remove('show');},2500);
}

function switchTab(name) {
  document.querySelectorAll('.screen').forEach(function(s){s.classList.remove('active');});
  document.querySelectorAll('#tabs .tab').forEach(function(t){t.classList.remove('active');});
  document.getElementById('screen-'+name).classList.add('active');
  var tabEl = document.getElementById('tab-'+name);
  if(tabEl && tabEl.classList.contains('tab')) tabEl.classList.add('active');
  if(name==='graficas') renderCharts();
  if(name==='presupuesto') renderBudget();
  if(name==='metas') renderGoals();
  if(name==='historial') renderHistorial();
  if(name==='trash') renderTrash();
  document.getElementById('content').scrollTo(0,0);
}

// Trash back button
document.getElementById('trashBackBtn').addEventListener('click', function(){
  switchTab('home');
});

function closeModal(id) {
  document.getElementById(id).classList.remove('open');
}

function openModal(id) {
  document.getElementById(id).classList.add('open');
}

// Close modals on backdrop click
document.querySelectorAll('.modal-overlay').forEach(function(overlay){
  overlay.addEventListener('click',function(e){
    if(e.target===overlay) overlay.classList.remove('open');
  });
});

// Theme toggle - SVG swap
document.getElementById('themeToggle').addEventListener('click',function(){
  var isDark = document.body.getAttribute('data-theme')==='dark';
  document.body.setAttribute('data-theme', isDark?'light':'dark');
  // Swap moon/sun icon
  var svg = this.querySelector('svg path');
  if(!isDark) {
    // show moon
    this.innerHTML='<svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/></svg>';
  } else {
    // show sun
    this.innerHTML='<svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/></svg>';
  }
  renderCharts();
});

// Swipe down to dismiss undo toast
(function(){
  var el = document.getElementById('undoToast');
  var startY = 0, curY = 0, dragging = false;
  el.addEventListener('touchstart', function(e){
    startY = e.touches[0].clientY;
    dragging = true;
    el.classList.add('swiping');
  }, {passive:true});
  el.addEventListener('touchmove', function(e){
    if(!dragging) return;
    curY = e.touches[0].clientY - startY;
    if(curY > 0) el.style.transform = 'translateY('+curY+'px)';
  }, {passive:true});
  el.addEventListener('touchend', function(){
    dragging = false;
    el.classList.remove('swiping');
    if(curY > 50) {
      el.style.transform = 'translateY(100px)';
      el.style.opacity = '0';
      setTimeout(function(){
        el.classList.remove('show');
        el.style.transform = '';
        el.style.opacity = '';
        commitDelete();
      }, 200);
    } else {
      el.style.transform = '';
    }
    curY = 0;
  });
})();

// =====================================================
// ADD TRANSACTION
// =====================================================
function showAddModal() {
  currentType='gasto';
  selectedCat='Otro';
  document.getElementById('nlpInput').value='';
  document.getElementById('txDesc').value='';
  document.getElementById('txAmount').value='';
  document.getElementById('nlpResult').classList.remove('show');
  updateTypeButtons();
  renderCatsGrid();
  openModal('addModal');
  setTimeout(function(){document.getElementById('nlpInput').focus();},400);
}

function setType(type) {
  currentType=type;
  updateTypeButtons();
}

function updateTypeButtons() {
  var bg=document.getElementById('btnGasto');
  var bi=document.getElementById('btnIngreso');
  bg.className='type-btn'+(currentType==='gasto'?' active-expense':'');
  bi.className='type-btn'+(currentType==='ingreso'?' active-income':'');
}

function renderCatsGrid() {
  var grid=document.getElementById('catsGrid');
  grid.innerHTML='';
  CATS.forEach(function(cat){
    var btn=document.createElement('button');
    btn.className='cat-btn'+(selectedCat===cat.id?' active':'');
    var svgPath=getCatSvg(cat.id);
    btn.innerHTML=
      '<div style="width:26px;height:26px;display:flex;align-items:center;justify-content:center;">'+
        '<svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">'+svgPath+'</svg>'+
      '</div>'+
      '<span>'+cat.id+'</span>';
    btn.onclick=function(){selectedCat=cat.id;renderCatsGrid();};
    grid.appendChild(btn);
  });
}

function renderMultiItems(items, totalEl, saveBtn) {
  var total=0;
  var html='';
  items.forEach(function(item,i){
    total+=item.monto;
    var svgPath = getCatSvg(item.cat||'Otro');
    var strokeColor = currentType==='ingreso'?'#22d37a':'#ff4d6a';
    var bgColor = currentType==='ingreso'?'rgba(34,211,122,0.15)':'rgba(255,77,106,0.15)';
    var borderColor = currentType==='ingreso'?'rgba(34,211,122,0.3)':'rgba(255,77,106,0.3)';
    html+=
      '<div style="display:flex;align-items:center;gap:10px;padding:10px 12px;background:var(--bg3);border-radius:12px;margin-bottom:6px;border:1px solid var(--border);">'+
        '<div style="width:34px;height:34px;border-radius:50%;background:'+bgColor+';border:1px solid '+borderColor+';display:flex;align-items:center;justify-content:center;flex-shrink:0;">'+
          '<svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="'+strokeColor+'" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">'+svgPath+'</svg>'+
        '</div>'+
        '<div style="flex:1;min-width:0;">'+
          '<div style="font-size:13px;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">'+item.desc+'</div>'+
          '<div style="font-size:10px;color:var(--text3);margin-top:1px;">'+item.cat+'</div>'+
        '</div>'+
        '<div style="font-size:13px;font-weight:700;font-family:\'DM Mono\',monospace;color:'+(currentType==='ingreso'?'var(--green)':'var(--red)')+';">'+(currentType==='ingreso'?'+':'-')+fmt(item.monto)+'</div>'+
        '<button onclick="removeMultiItem('+i+')" style="background:none;border:none;color:var(--text3);cursor:pointer;padding:4px;margin-left:4px;display:flex;align-items:center;justify-content:center;">'+
          '<svg viewBox="0 0 24 24" width="13" height="13" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>'+
        '</button>'+
      '</div>';
  });
  document.getElementById('multiItems').innerHTML=html;
  document.getElementById('multiTotal').textContent=fmt(total);
  if(saveBtn) document.getElementById('saveBtn').textContent='Guardar '+items.length+' movimientos ('+fmt(total)+')';
}

// Per-item category detection
function detectItemCat(desc) {
  var t = desc.toLowerCase();
  var catMap = {
    'Transporte':['uber','didi','taxi','gasolina','camion','metro','bus','caseta','autobus'],
    'Comida':['taco','tacos','pizza','burger','hamburgesa','torta','dona','donas','pan','cafe','restaurant','fonda','chettos','cheetos','sabritas','frituras','papas','palomitas','chocolate','dulce','refresco','coca','pepsi','sprite','comida','comer'],
    'Super':['super','supermercado','walmart','soriana','chedraui','costco','oxxo','seven','tiendita'],
    'Hogar':['renta','hipoteca','mantenimiento','luz','agua','gas','plomero','electricista'],
    'Salud':['farmacia','medicamento','doctor','hospital','consulta','dentista','omega','vitamina','medicina','pastilla'],
    'Servicios':['internet','telefono','netflix','spotify','suscripcion','streaming','cable'],
    'Compras':['ropa','zapatos','tienda','liverpool','shein','camisa','pantalon','vestido','celular','iphone','samsung','laptop','computadora','tablet','televisor','audifonos','bocina'],
    'Trabajo':['sueldo','salario','quincena','nomina','freelance','honorarios','bono','aguinaldo'],
    'Venta':['vendi','vendido','venta'],
    'Transferencia':['transferencia','deposito','spei'],
    'Entretenimiento':['cine','concierto','evento','boleto','teatro','gym','juego','videojuego']
  };
  for(var cat in catMap){
    var words=catMap[cat];
    for(var k=0;k<words.length;k++) if(t.indexOf(words[k])!==-1) return cat;
  }
  return 'Otro';
}

function runNLP() {
  clearTimeout(nlpTimer);
  nlpTimer=setTimeout(function(){
    var txt=document.getElementById('nlpInput').value.trim();
    if(txt.length<4){
      document.getElementById('nlpResult').classList.remove('show');
      document.getElementById('multiPreview').style.display='none';
      document.getElementById('singleFields').style.display='block';
      document.getElementById('saveBtn').textContent='Guardar movimiento';
      pendingMultiItems=null; isMultiMode=false;
      return;
    }
    var multi = extractMultiItems(txt);
    if(multi && multi.length>=2) {
      // Detect category per item
      multi.forEach(function(item){ item.cat = detectItemCat(item.desc); });
      isMultiMode=true;
      pendingMultiItems=multi;
      document.getElementById('nlpResult').classList.remove('show');
      document.getElementById('singleFields').style.display='none';
      document.getElementById('multiPreview').style.display='block';
      renderMultiItems(multi, true, true);
    } else {
      isMultiMode=false;
      pendingMultiItems=null;
      document.getElementById('multiPreview').style.display='none';
      document.getElementById('singleFields').style.display='block';
      var res=nlpDetect(txt);
      if(res.monto>0){
        document.getElementById('nlpType').textContent=res.tipo.toUpperCase();
        document.getElementById('nlpType').style.color=res.tipo==='ingreso'?'var(--green)':'var(--red)';
        document.getElementById('nlpMonto').textContent=fmt(res.monto);
        document.getElementById('nlpCat').textContent=res.cat;
        document.getElementById('nlpResult').classList.add('show');
        document.getElementById('txDesc').value=res.desc;
        document.getElementById('txAmount').value=res.monto;
        currentType=res.tipo;
        selectedCat=res.cat;
        updateTypeButtons();
        renderCatsGrid();
        document.getElementById('saveBtn').textContent='Guardar movimiento';
      }
    }
  },400);
}

function removeMultiItem(idx) {
  if(!pendingMultiItems) return;
  pendingMultiItems.splice(idx,1);
  if(pendingMultiItems.length<2){
    isMultiMode=false;
    document.getElementById('multiPreview').style.display='none';
    document.getElementById('singleFields').style.display='block';
    document.getElementById('saveBtn').textContent='Guardar movimiento';
    pendingMultiItems=null;
    return;
  }
  renderMultiItems(pendingMultiItems, true, true);
}

function saveTx() {
  if(isMultiMode && pendingMultiItems && pendingMultiItems.length>=1) {
    var total=0;
    pendingMultiItems.forEach(function(item){
      var tx={id:Date.now()+Math.random(), tipo:currentType, monto:item.monto,
        desc:item.desc, cat:item.cat||selectedCat, fecha:todayStr(), ts:Date.now()};
      state.txs.push(tx);
      total+=item.monto;
    });
    DB.save(state);
    closeModal('addModal');
    renderHome();
    showToast(pendingMultiItems.length+' movimientos guardados - '+fmt(total));
    return;

  }

  // Modo single
  var desc=document.getElementById('txDesc').value.trim();
  var amount=parseFloat(document.getElementById('txAmount').value)||0;
  if(!desc){showToast('Agrega una descripcion');return;}
  if(amount<=0){showToast('El monto debe ser mayor a 0');return;}
  var tx={id:Date.now(), tipo:currentType, monto:amount, desc:desc,
    cat:selectedCat, fecha:todayStr(), ts:Date.now()};
  state.txs.push(tx);
  DB.save(state);
  closeModal('addModal');
  renderHome();
  showToast((currentType==='ingreso'?'+ ':'- ')+fmt(amount)+' guardado');
}

// =====================================================
// HOME RENDER
// =====================================================
function renderHome() {
  var ing=0,gas=0,monthGas=0;
  var m=new Date().getMonth(), y=new Date().getFullYear();
  state.txs.forEach(function(t){
    if(t.tipo==='ingreso') ing+=t.monto;
    else gas+=t.monto;
    var parts=t.fecha.split('/');
    if(parseInt(parts[1])-1===m&&parseInt(parts[2])===y&&t.tipo==='gasto') monthGas+=t.monto;
  });
  var bal=ing-gas;
  document.getElementById('balanceAmount').textContent=(bal>=0?'+':'')+fmt(bal);
  document.getElementById('balanceAmount').style.color='#fff';
  document.getElementById('totalIncome').textContent=fmt(ing);
  document.getElementById('totalExpense').textContent=fmt(gas);
  document.getElementById('monthExpense').textContent=fmtShort(monthGas);
  document.getElementById('txCount').textContent=state.txs.length;

  var recent=state.txs.slice(-8).reverse();
  var list=document.getElementById('recentList');
  if(!recent.length){
    list.innerHTML='<div class="empty-state"><p>Toca + para agregar tu primer movimiento</p></div>';
  } else {
    list.innerHTML='';
    recent.forEach(function(t){ list.appendChild(makeTxItem(t)); });
  }

  // Goals widget
  renderGoals();
}

// SVG paths per category for liquid glass icons
var CAT_SVG = {
  'Comida':    '<path d="M18 8h1a4 4 0 0 1 0 8h-1"/><path d="M2 8h16v9a4 4 0 0 1-4 4H6a4 4 0 0 1-4-4V8z"/><line x1="6" y1="1" x2="6" y2="4"/><line x1="10" y1="1" x2="10" y2="4"/><line x1="14" y1="1" x2="14" y2="4"/>',
  'Transporte':'<rect x="1" y="3" width="15" height="13" rx="2"/><polygon points="16 8 20 8 23 11 23 16 16 16 16 8"/><circle cx="5.5" cy="18.5" r="2.5"/><circle cx="18.5" cy="18.5" r="2.5"/>',
  'Super':     '<circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/>',
  'Hogar':     '<path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/>',
  'Salud':     '<path d="M22 12h-4l-3 9L9 3l-3 9H2"/>',
  'Servicios': '<rect x="5" y="2" width="14" height="20" rx="2" ry="2"/><line x1="12" y1="18" x2="12.01" y2="18"/>',
  'Compras':   '<path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/><line x1="3" y1="6" x2="21" y2="6"/><path d="M16 10a4 4 0 0 1-8 0"/>',
  'Trabajo':   '<rect x="2" y="7" width="20" height="14" rx="2" ry="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/>',
  'Venta':     '<line x1="12" y1="1" x2="12" y2="23"/><path d="M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/>',
  'Transferencia':'<polyline points="17 1 21 5 17 9"/><path d="M3 11V9a4 4 0 0 1 4-4h14"/><polyline points="7 23 3 19 7 15"/><path d="M21 13v2a4 4 0 0 1-4 4H3"/>',
  'Entretenimiento':'<polygon points="23 7 16 12 23 17 23 7"/><rect x="1" y="5" width="15" height="14" rx="2" ry="2"/>',
  'Otro':      '<circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/>'
};

function getCatSvg(catId) {
  return CAT_SVG[catId] || CAT_SVG['Otro'];
}

function makeTxItem(t, showDelete) {
  var cat = getCat(t.cat);
  var svgPath = getCatSvg(t.cat);
  var isInc = t.tipo === 'ingreso';
  var div = document.createElement('div');
  div.className = 'tx-item';

  // Liquid glass icon
  var bgColor = isInc ? 'rgba(34,211,122,0.15)' : 'rgba(255,77,106,0.15)';
  var strokeColor = isInc ? '#22d37a' : '#ff4d6a';

  div.innerHTML =
    '<div style="width:40px;height:40px;border-radius:50%;background:'+bgColor+';display:flex;align-items:center;justify-content:center;flex-shrink:0;border:1px solid '+(isInc?'rgba(34,211,122,0.3)':'rgba(255,77,106,0.3)')+';">'+
      '<svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="'+strokeColor+'" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">'+svgPath+'</svg>'+
    '</div>'+
    '<div class="tx-info">'+
      '<div class="tx-desc">'+t.desc+'</div>'+
      '<div class="tx-meta">'+t.cat+' · '+t.fecha+'</div>'+
    '</div>'+
    '<div class="tx-amount '+(isInc?'income':'expense')+'">'+(isInc?'+':'-')+fmt(t.monto)+'</div>'+
    (showDelete?'<button onclick="deleteTx('+t.id+')" style="background:rgba(255,77,106,0.12);border:1px solid rgba(255,77,106,0.3);color:var(--red);width:28px;height:28px;border-radius:50%;cursor:pointer;font-size:13px;margin-left:6px;flex-shrink:0;display:flex;align-items:center;justify-content:center;">'+
      '<svg viewBox="0 0 24 24" width="12" height="12" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>'+
    '</button>':'');
  return div;
}

function deleteTx(id) {
  var tx = state.txs.find(function(t){return t.id===id;});
  if(!tx) return;
  state.txs = state.txs.filter(function(t){return t.id!==id;});
  DB.save(state);
  softDelete(tx, 'tx');
  renderHistorial();
  renderHome();
}

// =====================================================
// HISTORIAL
// =====================================================
function filterTx() {
  renderHistorial();
}
function setFilter(f, el) {
  currentFilter=f;
  document.querySelectorAll('.filter-chip').forEach(function(c){c.classList.remove('active');});
  el.classList.add('active');
  renderHistorial();
}

function renderHistorial() {
  var q=document.getElementById('searchInput').value.toLowerCase();
  var list=state.txs.filter(function(t){
    var matchFilter=currentFilter==='todos'||t.tipo===currentFilter||t.cat===currentFilter;
    var matchSearch=!q||t.desc.toLowerCase().indexOf(q)!==-1||t.cat.toLowerCase().indexOf(q)!==-1||t.fecha.indexOf(q)!==-1;
    return matchFilter&&matchSearch;
  }).reverse();

  var container=document.getElementById('historialList');
  if(!list.length){
    container.innerHTML='<div class="empty-state"><div class="empty-icon">🔍</div><p>No se encontraron movimientos</p></div>';
    return;
  }
  container.innerHTML='';
  list.forEach(function(t){container.appendChild(makeTxItem(t,true));});
}

// =====================================================
// CHARTS
// =====================================================
function getMonthTxs(d) {
  return state.txs.filter(function(t){
    var p=t.fecha.split('/');
    return parseInt(p[1])-1===d.getMonth()&&parseInt(p[2])===d.getFullYear();
  });
}

function changeMonth(dir) {
  viewMonth=new Date(viewMonth.getFullYear(), viewMonth.getMonth()+dir, 1);
  document.getElementById('monthLabel').textContent=monthStr(viewMonth);
  renderCharts();
}

function getThemeColors() {
  var isDark=document.body.getAttribute('data-theme')==='dark';
  return {
    grid: isDark?'rgba(255,255,255,0.06)':'rgba(0,0,0,0.08)',
    text: isDark?'#64748b':'#9aaac8',
    tooltip: isDark?'#1e2d45':'#ffffff'
  };
}

function renderCharts() {
  document.getElementById('monthLabel').textContent=monthStr(viewMonth);
  var txs=getMonthTxs(viewMonth);
  renderBarChart(txs);
  renderDonutChart(txs);
  renderLineChart(txs);
}

function renderBarChart(txs) {
  var canvas=document.getElementById('barChart');
  var ctx=canvas.getContext('2d');
  var dpr=window.devicePixelRatio||1;
  var W=canvas.parentElement.offsetWidth-2;
  var H=200;
  canvas.width=W*dpr; canvas.height=H*dpr;
  canvas.style.width=W+'px'; canvas.style.height=H+'px';
  ctx.scale(dpr,dpr);
  ctx.clearRect(0,0,W,H);

  var tc=getThemeColors();
  var days={};
  var daysInMonth=new Date(viewMonth.getFullYear(),viewMonth.getMonth()+1,0).getDate();
  for(var i=1;i<=daysInMonth;i++) days[i]={ing:0,gas:0};
  txs.forEach(function(t){
    var d=parseInt(t.fecha.split('/')[0]);
    if(t.tipo==='ingreso') days[d].ing+=t.monto;
    else days[d].gas+=t.monto;
  });

  var labels=Object.keys(days).map(Number);
  var vals=labels.map(function(d){return days[d];});
  var maxVal=Math.max.apply(null,vals.map(function(v){return Math.max(v.ing,v.gas);}),1);

  var pad={l:8,r:8,t:16,b:24};
  var chartW=W-pad.l-pad.r;
  var chartH=H-pad.t-pad.b;
  var barW=Math.max(2, chartW/labels.length - 3);

  // Grid lines
  ctx.strokeStyle=tc.grid; ctx.lineWidth=1;
  for(var g=0;g<=4;g++){
    var y=pad.t+chartH*(1-g/4);
    ctx.beginPath(); ctx.moveTo(pad.l,y); ctx.lineTo(W-pad.r,y); ctx.stroke();
  }

  labels.forEach(function(day,i){
    var x=pad.l+(chartW/labels.length)*i+(chartW/labels.length-barW*2-2)/2;
    var gasH=(vals[i].gas/maxVal)*chartH;
    var ingH=(vals[i].ing/maxVal)*chartH;

    if(vals[i].gas>0){
      ctx.fillStyle='rgba(255,77,106,0.8)';
      ctx.beginPath();
      ctx.roundRect(x, pad.t+chartH-gasH, barW, gasH, [3,3,0,0]);
      ctx.fill();
    }
    if(vals[i].ing>0){
      ctx.fillStyle='rgba(34,211,122,0.8)';
      ctx.beginPath();
      ctx.roundRect(x+barW+2, pad.t+chartH-ingH, barW, ingH, [3,3,0,0]);
      ctx.fill();
    }
  });

  // Legend
  ctx.font='10px DM Sans';
  ctx.fillStyle='rgba(255,77,106,0.9)'; ctx.fillRect(pad.l,H-10,8,8);
  ctx.fillStyle=tc.text; ctx.fillText('Gastos',pad.l+10,H-3);
  ctx.fillStyle='rgba(34,211,122,0.9)'; ctx.fillRect(pad.l+55,H-10,8,8);
  ctx.fillStyle=tc.text; ctx.fillText('Ingresos',pad.l+65,H-3);
}

function renderDonutChart(txs) {
  var canvas=document.getElementById('donutChart');
  var ctx=canvas.getContext('2d');
  var dpr=window.devicePixelRatio||1;
  canvas.width=130*dpr; canvas.height=130*dpr;
  canvas.style.width='130px'; canvas.style.height='130px';
  ctx.scale(dpr,dpr);
  ctx.clearRect(0,0,130,130);

  var gastos=txs.filter(function(t){return t.tipo==='gasto';});
  var byCat={};
  gastos.forEach(function(t){
    byCat[t.cat]=(byCat[t.cat]||0)+t.monto;
  });

  var cats=Object.keys(byCat);
  var total=cats.reduce(function(s,c){return s+byCat[c];},0);

  if(!total){
    ctx.fillStyle='var(--bg3)';
    ctx.beginPath(); ctx.arc(65,65,50,0,Math.PI*2); ctx.fill();
    ctx.fillStyle='rgba(100,116,139,0.3)';
    ctx.beginPath(); ctx.arc(65,65,30,0,Math.PI*2); ctx.fill();

    document.getElementById('donutLegend').innerHTML=
      '<p style="color:var(--text3);font-size:12px">Sin gastos este mes</p>';
    return;
  }

  var angle=-Math.PI/2;
  var legend=document.getElementById('donutLegend');
  legend.innerHTML='';

  cats.sort(function(a,b){return byCat[b]-byCat[a];}).slice(0,6).forEach(function(cat,i){
    var pct=byCat[cat]/total;
    var catInfo=getCat(cat);
    var arc=pct*Math.PI*2;

    ctx.beginPath();
    ctx.moveTo(65,65);
    ctx.arc(65,65,56,angle,angle+arc);
    ctx.closePath();
    ctx.fillStyle=catInfo.color;
    ctx.fill();
    angle+=arc;

    // Legend item
    var item=document.createElement('div');
    item.className='legend-item';
    item.innerHTML=
      '<div class="legend-dot" style="background:'+catInfo.color+'"></div>'+
      '<div class="legend-label">'+cat+'</div>'+
      '<div class="legend-value">'+fmtShort(byCat[cat])+'</div>';
    legend.appendChild(item);
  });

  // Donut hole
  var isDark=document.body.getAttribute('data-theme')==='dark';
  ctx.beginPath(); ctx.arc(65,65,30,0,Math.PI*2);
  ctx.fillStyle=isDark?'#111827':'#eaecf5';
  ctx.fill();
}

function renderLineChart(txs) {
  var canvas=document.getElementById('lineChart');
  var ctx=canvas.getContext('2d');
  var dpr=window.devicePixelRatio||1;
  var W=canvas.parentElement.offsetWidth-2;
  var H=200;
  canvas.width=W*dpr; canvas.height=H*dpr;
  canvas.style.width=W+'px'; canvas.style.height=H+'px';
  ctx.scale(dpr,dpr);
  ctx.clearRect(0,0,W,H);

  var tc=getThemeColors();
  var daysInMonth=new Date(viewMonth.getFullYear(),viewMonth.getMonth()+1,0).getDate();
  var cumIncome=Array(daysInMonth).fill(0);
  var cumExpense=Array(daysInMonth).fill(0);

  txs.forEach(function(t){
    var d=parseInt(t.fecha.split('/')[0])-1;
    if(t.tipo==='ingreso') cumIncome[d]+=t.monto;
    else cumExpense[d]+=t.monto;
  });

  // Make cumulative
  for(var i=1;i<daysInMonth;i++){
    cumIncome[i]+=cumIncome[i-1];
    cumExpense[i]+=cumExpense[i-1];
  }

  var maxVal=Math.max.apply(null,cumIncome.concat(cumExpense).concat([1]));
  var pad={l:8,r:8,t:16,b:24};
  var chartW=W-pad.l-pad.r;
  var chartH=H-pad.t-pad.b;

  // Grid
  ctx.strokeStyle=tc.grid; ctx.lineWidth=1;
  for(var g=0;g<=4;g++){
    var y=pad.t+chartH*(1-g/4);
    ctx.beginPath(); ctx.moveTo(pad.l,y); ctx.lineTo(W-pad.r,y); ctx.stroke();
  }

  function drawLine(data, color) {
    ctx.beginPath();
    ctx.strokeStyle=color; ctx.lineWidth=2.5;
    ctx.lineJoin='round'; ctx.lineCap='round';
    data.forEach(function(v,i){
      var x=pad.l+(chartW/(daysInMonth-1))*i;
      var y=pad.t+chartH*(1-v/maxVal);
      if(i===0) ctx.moveTo(x,y); else ctx.lineTo(x,y);
    });
    ctx.stroke();

    // Fill area
    ctx.beginPath();
    data.forEach(function(v,i){
      var x=pad.l+(chartW/(daysInMonth-1))*i;
      var y=pad.t+chartH*(1-v/maxVal);
      if(i===0) ctx.moveTo(x,y); else ctx.lineTo(x,y);
    });
    ctx.lineTo(W-pad.r, pad.t+chartH);
    ctx.lineTo(pad.l, pad.t+chartH);
    ctx.closePath();
    ctx.fillStyle=color.replace(')',',0.1)').replace('rgb','rgba');
    ctx.fill();
  }

  drawLine(cumExpense,'rgb(255,77,106)');
  drawLine(cumIncome,'rgb(34,211,122)');
}

// =====================================================
// BUDGET
// =====================================================
function showBudgetModal() {
  var inputs=document.getElementById('budgetInputs');
  inputs.innerHTML='';
  var expenseCats=CATS.filter(function(c){return c.id!=='Trabajo'&&c.id!=='Venta'&&c.id!=='Transferencia';});
  expenseCats.forEach(function(cat){
    var g=document.createElement('div');
    g.className='form-group';
    g.innerHTML=
      '<label class="form-label">'+cat.id+'</label>'+
      '<input type="number" class="form-input" id="budget_'+cat.id+'" placeholder="0.00" value="'+(state.budgets[cat.id]||'')+'" inputmode="decimal">';
    inputs.appendChild(g);
  });
  openModal('budgetModal');
}

function saveBudget() {
  var expenseCats=CATS.filter(function(c){return c.id!=='Trabajo'&&c.id!=='Venta'&&c.id!=='Transferencia';});
  expenseCats.forEach(function(cat){
    var val=parseFloat(document.getElementById('budget_'+cat.id).value)||0;
    if(val>0) state.budgets[cat.id]=val;
    else delete state.budgets[cat.id];
  });
  DB.save(state);
  closeModal('budgetModal');
  renderBudget();
  showToast('Presupuesto guardado');
}

function renderBudget() {
  var txs=getMonthTxs(viewMonth);
  var spent={};
  txs.filter(function(t){return t.tipo==='gasto';}).forEach(function(t){
    spent[t.cat]=(spent[t.cat]||0)+t.monto;
  });

  var list=document.getElementById('budgetList');
  var budgetCats=Object.keys(state.budgets);

  if(!budgetCats.length){
    list.innerHTML='<div class="empty-state"><div class="empty-icon">📊</div><p>Configura tu presupuesto por categoria</p></div>';
    document.getElementById('savingsCard').style.display='none';
    return;
  }

  list.innerHTML='';
  var totalBudget=0, totalSpent=0;

  budgetCats.forEach(function(cat){
    var budget=state.budgets[cat];
    var s=spent[cat]||0;
    var pct=Math.min(s/budget,1);
    totalBudget+=budget; totalSpent+=s;

    var color = pct<0.6?'var(--green)':pct<0.85?'var(--yellow)':'var(--red)';
    var div=document.createElement('div');
    div.className='budget-item';
    var catInfo=getCat(cat);
    div.innerHTML=
      '<div class="budget-header">'+
      '<div class="budget-cat"><svg viewBox="0 0 24 24" width="14" height="14" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" style="margin-right:5px;vertical-align:middle;">'+getCatSvg(cat)+'</svg>'+cat+'</div>'+
        '<div class="budget-amounts">'+fmtShort(s)+' / '+fmtShort(budget)+'</div>'+
      '</div>'+
      '<div class="progress-bar">'+
        '<div class="progress-fill" style="width:'+(pct*100)+'%;background:'+color+'"></div>'+
      '</div>';
    list.appendChild(div);
  });

  // Summary
  var saved=totalBudget-totalSpent;
  var card=document.getElementById('savingsCard');
  card.style.display='block';
  var pctTotal=totalBudget>0?Math.min(totalSpent/totalBudget,1):0;
  var colorTotal=pctTotal<0.6?'var(--green)':pctTotal<0.85?'var(--yellow)':'var(--red)';
  document.getElementById('budgetSummary').innerHTML=
    '<div class="budget-item">'+
      '<div class="budget-header">'+
        '<div class="budget-cat">Total presupuesto</div>'+
        '<div class="budget-amounts">'+fmtShort(totalSpent)+' / '+fmtShort(totalBudget)+'</div>'+
      '</div>'+
      '<div class="progress-bar"><div class="progress-fill" style="width:'+(pctTotal*100)+'%;background:'+colorTotal+'"></div></div>'+
    '</div>'+
    '<div style="margin-top:12px;padding:12px;background:var(--bg3);border-radius:12px;display:flex;justify-content:space-between;align-items:center;">'+
      '<div style="font-size:13px;color:var(--text2);">'+(saved>=0?'Disponible restante':'Excedido en')+'</div>'+
      '<div style="font-size:16px;font-weight:700;font-family:\'DM Mono\',monospace;color:'+(saved>=0?'var(--green)':'var(--red)')+';">'+(saved>=0?'+':'')+fmt(Math.abs(saved))+'</div>'+
    '</div>';
}

// =====================================================
// GOALS
// =====================================================
function showAddGoal() {
  document.getElementById('goalName').value='';
  document.getElementById('goalTarget').value='';
  document.getElementById('goalCurrent').value='';
  document.getElementById('goalEmoji').value='';
  openModal('goalModal');
}

function saveGoal() {
  var name=document.getElementById('goalName').value.trim();
  var target=parseFloat(document.getElementById('goalTarget').value)||0;
  var current=parseFloat(document.getElementById('goalCurrent').value)||0;
  var emoji=document.getElementById('goalEmoji').value.trim()||'🎯';
  if(!name){showToast('Agrega un nombre');return;}
  if(target<=0){showToast('El objetivo debe ser mayor a 0');return;}

  state.goals.push({
    id: Date.now(),
    name: name,
    target: target,
    current: Math.min(current,target),
    emoji: emoji,
    createdAt: todayStr()
  });
  DB.save(state);
  closeModal('goalModal');
  renderGoals();
  showToast('Meta creada: '+name);
}

function addToGoal(id, amount) {
  state.goals=state.goals.map(function(g){
    if(g.id===id) g.current=Math.min(g.current+amount,g.target);
    return g;
  });
  DB.save(state);
  renderGoals();
}

function deleteGoal(id) {
  var goal = state.goals.find(function(g){return g.id===id;});
  if(!goal) return;
  state.goals = state.goals.filter(function(g){return g.id!==id;});
  DB.save(state);
  softDelete(goal, 'goal');
  renderGoals();
}

function renderGoals() {
  var list=document.getElementById('goalsList');
  var homeWidget=document.getElementById('goalsHome');

  if(!state.goals.length){
    if(list) list.innerHTML='<div class="empty-state"><p>Crea una meta para empezar a ahorrar</p></div>';
    if(homeWidget) homeWidget.innerHTML='<div class="empty-state" style="padding:12px 0;"><p style="font-size:13px;">Sin metas activas</p></div>';
    return;
  }

  var html = buildGoalsHTML();
  if(list) list.innerHTML = html;
  if(homeWidget) homeWidget.innerHTML = html;
}

function buildGoalsHTML() {
  var html = '';
  state.goals.forEach(function(g){
    var pct=g.target>0?g.current/g.target:0;
    var pctInt=Math.round(pct*100);
    var color=pct<0.4?'var(--blue)':pct<0.7?'var(--yellow)':'var(--green)';
    var done=pct>=1;
    html+=
      '<div class="goal-card">'+
        '<div class="goal-header">'+
          '<div style="width:42px;height:42px;border-radius:50%;background:rgba(167,139,250,0.15);border:1px solid rgba(167,139,250,0.3);display:flex;align-items:center;justify-content:center;flex-shrink:0;">'+
            '<svg viewBox="0 0 24 24" width="20" height="20" fill="none" stroke="#a78bfa" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="6"/><circle cx="12" cy="12" r="2"/></svg>'+
          '</div>'+
          '<div style="flex:1;margin-left:10px;">'+
            '<div class="goal-title">'+(done?'Completada - ':'')+g.name+'</div>'+
            '<div class="goal-sub">Desde '+g.createdAt+'</div>'+
          '</div>'+
          '<div class="goal-pct">'+pctInt+'%</div>'+
        '</div>'+
        '<div class="progress-bar" style="height:8px;margin:10px 0;">'+
          '<div class="progress-fill" style="width:'+(pct*100)+'%;background:'+color+'"></div>'+
        '</div>'+
        '<div class="goal-amounts">'+
          '<span>Ahorrado: <strong style="color:var(--green)">'+fmt(g.current)+'</strong></span>'+
          '<span>Meta: <strong>'+fmt(g.target)+'</strong></span>'+
        '</div>'+
        '<div style="margin-top:10px;">'+
          '<button onclick="deleteGoal('+g.id+')" style="width:100%;padding:9px;background:rgba(255,77,106,0.08);border:1px solid rgba(255,77,106,0.25);color:var(--red);border-radius:10px;font-size:13px;font-weight:500;cursor:pointer;font-family:\'DM Sans\',sans-serif;display:flex;align-items:center;justify-content:center;gap:6px;">'+
            '<svg viewBox="0 0 24 24" width="13" height="13" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14H6L5 6"/></svg>'+
            'Eliminar meta'+
          '</button>'+
        '</div>'+
      '</div>';
  });
  return html;
}

function promptAddToGoal(id) {
  var amount=parseFloat(prompt('Cuanto quieres abonar?'))||0;
  if(amount>0){
    addToGoal(id,amount);
    showToast(fmt(amount)+' abonado a la meta');
  }
}

// =====================================================
// VOICE RECOGNITION
// =====================================================
var micRecognition = null;
var micActive = false;

function activateMic() {
  var SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
  if(!SpeechRecognition) {
    // Fallback: just open the modal
    showToast('Voz no disponible, escribe tu movimiento');
    showAddModal();
    return;
  }

  try {
    micRecognition = new SpeechRecognition();
  } catch(e) {
    showToast('Voz no disponible en este navegador');
    showAddModal();
    return;
  }

  micRecognition.lang = 'es-MX';
  micRecognition.interimResults = true;
  micRecognition.maxAlternatives = 1;
  micRecognition.continuous = false;

  micActive = true;
  document.getElementById('micOverlay').classList.add('active');
  document.getElementById('micTab').classList.add('listening');
  document.getElementById('micOrbBtn').classList.add('active-listening');
  document.getElementById('micStatus').textContent = 'Escuchando...';
  document.getElementById('micTranscript').textContent = '';

  var finalTranscript = '';

  micRecognition.onresult = function(e) {
    var interim = '';
    finalTranscript = '';
    for(var i = 0; i < e.results.length; i++) {
      if(e.results[i].isFinal) finalTranscript += e.results[i][0].transcript;
      else interim += e.results[i][0].transcript;
    }
    var shown = finalTranscript || interim;
    document.getElementById('micTranscript').textContent = shown ? '"' + shown + '"' : '';
    if(finalTranscript) {
      document.getElementById('micStatus').textContent = 'Procesando...';
    }
  };

  micRecognition.onerror = function(e) {
    var msg = {
      'not-allowed': 'Permiso denegado. Ve a Ajustes > Safari > Microfono',
      'no-speech': 'No se escucho nada, intenta de nuevo',
      'network': 'Error de red',
      'audio-capture': 'Microfono no disponible'
    }[e.error] || ('Error: ' + e.error);
    document.getElementById('micStatus').textContent = msg;
    document.getElementById('micTab').classList.remove('listening');
    document.getElementById('micOrbBtn').classList.remove('active-listening');
    setTimeout(function() {
      if(e.error === 'not-allowed') {
        cancelMic();
      }
    }, 2500);
  };

  micRecognition.onend = function() {
    document.getElementById('micTab').classList.remove('listening');
    document.getElementById('micOrbBtn').classList.remove('active-listening');
    if(micActive && finalTranscript) {
      setTimeout(function() { applyVoiceInput(finalTranscript); }, 300);
    } else if(micActive && !finalTranscript) {
      document.getElementById('micStatus').textContent = 'No se escucho nada';
      setTimeout(cancelMic, 1500);
    }
  };

  try {
    micRecognition.start();
  } catch(e) {
    cancelMic();
    showToast('No se pudo iniciar el microfono');
  }
}

function stopMic() {
  if(micRecognition) { try { micRecognition.stop(); } catch(e) {} }
}

function cancelMic() {
  micActive = false;
  if(micRecognition) { try { micRecognition.abort(); } catch(e) {} }
  micRecognition = null;
  document.getElementById('micOverlay').classList.remove('active');
  document.getElementById('micTab').classList.remove('listening');
  var orb = document.getElementById('micOrbBtn');
  if(orb) orb.classList.remove('active-listening');
}

function applyVoiceInput(transcript) {
  cancelMic();
  setTimeout(function() {
    showAddModal();
    setTimeout(function() {
      var inp = document.getElementById('nlpInput');
      if(inp) { inp.value = transcript; runNLP(); }
    }, 500);
  }, 100);
}

function updateTrashBadge() {
  var badge = document.getElementById('trashBadge');
  if(!badge) return;
  var now = Date.now();
  var count = (state.trash||[]).filter(function(ti){ return ti.expiresAt > now; }).length;
  badge.style.display = count > 0 ? 'block' : 'none';
}

// =====================================================
// INIT
// =====================================================
if(!state.trash) state.trash=[];
renderHome();
renderHistorial();
updateTrashBadge();
document.getElementById('monthLabel').textContent=monthStr(viewMonth);
</script>

</body>
</html>
