[index.html](https://github.com/user-attachments/files/27624558/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no"/>
<meta name="apple-mobile-web-app-capable" content="yes"/>
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"/>
<meta name="apple-mobile-web-app-title" content="OB Planner"/>
<meta name="theme-color" content="#1a0f0a"/>
<title>OB Care Planner</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Nunito:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
/* ═══════════════════════════════════════
   ROOT & RESET
═══════════════════════════════════════ */
:root {
  --bg: #0e0a08;
  --surface: #1c1410;
  --surface2: #241a15;
  --surface3: #2e221b;
  --border: rgba(255,255,255,0.08);
  --border2: rgba(255,255,255,0.12);
  --rose: #e8876a;
  --rose-light: #f4a98e;
  --rose-muted: rgba(232,135,106,0.15);
  --sage: #7ec8a8;
  --sage-muted: rgba(126,200,168,0.15);
  --gold: #d4a855;
  --gold-muted: rgba(212,168,85,0.15);
  --text: #f0e8e0;
  --text2: #a8978a;
  --text3: #6b5c52;
  --safe-top: env(safe-area-inset-top, 44px);
  --safe-bottom: env(safe-area-inset-bottom, 34px);
  --safe-left: env(safe-area-inset-left, 0px);
  --safe-right: env(safe-area-inset-right, 0px);
}
* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
html {
  width: 100%; height: 100%;
  background: var(--bg);
}
body {
  width: 100%; height: 100%;
  background: var(--bg);
  color: var(--text);
  font-family: 'Nunito', sans-serif;
  overflow: hidden;
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  -webkit-text-size-adjust: 100%;
}

/* ═══════════════════════════════════════
   APP SHELL
═══════════════════════════════════════ */
#app {
  width: 100vw;
  height: 100vh;
  height: 100dvh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* ═══════════════════════════════════════
   STATUS BAR SPACER
═══════════════════════════════════════ */
.status-bar {
  height: var(--safe-top);
  background: var(--bg);
  flex-shrink: 0;
}

/* ═══════════════════════════════════════
   TOP NAV
═══════════════════════════════════════ */
.top-nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 20px;
  background: var(--bg);
  border-bottom: 1px solid var(--border);
  flex-shrink: 0;
  position: relative;
}
.nav-title {
  font-family: 'Playfair Display', serif;
  font-size: 20px;
  font-weight: 600;
  background: linear-gradient(135deg, var(--rose-light), var(--gold));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.nav-subtitle { font-size: 10px; color: var(--text3); letter-spacing: 1.2px; text-transform: uppercase; margin-top: 1px; }
.nav-icon { font-size: 22px; }
.nav-back {
  font-size: 14px; color: var(--rose); font-weight: 500;
  background: none; border: none; cursor: pointer; padding: 4px 0;
  display: flex; align-items: center; gap: 4px;
}
.nav-back-placeholder { width: 60px; }

/* ═══════════════════════════════════════
   SCROLL AREA
═══════════════════════════════════════ */
.scroll-area {
  flex: 1;
  overflow-y: auto;
  overflow-x: hidden;
  -webkit-overflow-scrolling: touch;
  overscroll-behavior-y: contain;
  min-height: 0;
}
.scroll-area::-webkit-scrollbar { display: none; }

/* ═══════════════════════════════════════
   BOTTOM TAB BAR
═══════════════════════════════════════ */
.tab-bar {
  display: none;
  background: rgba(14,10,8,0.95);
  border-top: 1px solid var(--border);
  padding-bottom: var(--safe-bottom);
  flex-shrink: 0;
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
}
.tab-bar.visible { display: flex; }
.tab-item {
  flex: 1;
  display: flex; flex-direction: column; align-items: center;
  padding: 10px 0 6px;
  cursor: pointer;
  background: none; border: none;
  transition: opacity 0.15s;
  position: relative;
}
.tab-item.active .tab-icon { color: var(--rose); }
.tab-item.active .tab-label { color: var(--rose); }
.tab-icon { font-size: 20px; color: var(--text3); transition: color 0.15s; }
.tab-label { font-size: 9px; color: var(--text3); margin-top: 3px; letter-spacing: 0.5px; font-weight: 500; transition: color 0.15s; }
.tab-badge {
  position: absolute; top: 7px; right: calc(50% - 16px);
  background: var(--rose); color: white;
  font-size: 9px; font-weight: 700;
  width: 16px; height: 16px;
  border-radius: 50%;
  display: none; align-items: center; justify-content: center;
}
.tab-badge.show { display: flex; }

/* ═══════════════════════════════════════
   SCREENS
═══════════════════════════════════════ */
.screen { display: none; height: 100%; flex-direction: column; min-height: 0; overflow: hidden; }
.screen.active { display: flex; }

/* ═══════════════════════════════════════
   SCREEN 1 — FORM
═══════════════════════════════════════ */
.form-scroll { padding: 20px 16px; padding-bottom: 24px; }

.hero-card {
  background: linear-gradient(135deg, #2a1510 0%, #1c1018 100%);
  border: 1px solid rgba(232,135,106,0.2);
  border-radius: 20px;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.hero-card::before {
  content: '';
  position: absolute; inset: 0;
  background: radial-gradient(ellipse at 50% 0%, rgba(232,135,106,0.12), transparent 60%);
}
.hero-emoji { font-size: 36px; display: block; margin-bottom: 8px; }
.hero-title {
  font-family: 'Playfair Display', serif;
  font-size: 22px; font-style: italic; font-weight: 400;
  color: var(--rose-light);
  line-height: 1.3;
}
.hero-sub { font-size: 12px; color: var(--text2); margin-top: 6px; line-height: 1.5; }

.section-label {
  font-size: 11px; font-weight: 600;
  text-transform: uppercase; letter-spacing: 1.5px;
  color: var(--text3);
  margin: 20px 0 10px 4px;
}

.input-group {
  background: var(--surface);
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid var(--border);
  margin-bottom: 12px;
}
.input-row {
  display: flex; align-items: center;
  padding: 0 16px;
  min-height: 52px;
  border-bottom: 1px solid var(--border);
  gap: 12px;
}
.input-row:last-child { border-bottom: none; }
.input-icon { font-size: 18px; flex-shrink: 0; width: 24px; text-align: center; }
.input-inner { flex: 1; display: flex; flex-direction: column; padding: 10px 0; }
.input-lbl { font-size: 10px; color: var(--text3); letter-spacing: 0.8px; text-transform: uppercase; margin-bottom: 2px; font-weight: 600; }
input[type="text"], input[type="email"], input[type="tel"], input[type="date"], select {
  background: none; border: none; outline: none;
  font-family: 'Nunito', sans-serif;
  font-size: 15px; color: var(--text);
  width: 100%;
  -webkit-appearance: none;
  appearance: none;
}
input[type="date"] { color-scheme: dark; }
select { color: var(--text); }
select option { background: #2a1a12; }
input::placeholder { color: var(--text3); }
.input-hint { font-size: 10px; color: var(--text3); margin-top: 1px; }

.rh-selector {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 14px 16px;
  margin-bottom: 12px;
}
.rh-label-top { font-size: 11px; color: var(--text3); text-transform: uppercase; letter-spacing: 1px; font-weight: 600; margin-bottom: 10px; display: flex; align-items: center; gap: 6px; }
.rh-options { display: flex; gap: 8px; }
.rh-opt {
  flex: 1; padding: 10px; border-radius: 12px;
  border: 1.5px solid var(--border);
  background: none; cursor: pointer;
  font-family: 'Nunito', sans-serif;
  font-size: 13px; font-weight: 500;
  color: var(--text2);
  text-align: center;
  transition: all 0.2s;
}
.rh-opt.selected-pos { border-color: var(--sage); background: var(--sage-muted); color: var(--sage); }
.rh-opt.selected-neg { border-color: var(--rose); background: var(--rose-muted); color: var(--rose); }
.rh-opt.selected-unk { border-color: var(--gold); background: var(--gold-muted); color: var(--gold); }

.generate-btn {
  width: 100%;
  padding: 17px;
  background: linear-gradient(135deg, var(--rose), #c96a4a);
  border: none; border-radius: 16px;
  font-family: 'Nunito', sans-serif;
  font-size: 16px; font-weight: 600;
  color: white; cursor: pointer;
  margin-top: 8px;
  display: flex; align-items: center; justify-content: center; gap: 8px;
  box-shadow: 0 8px 30px rgba(232,135,106,0.3);
  transition: transform 0.1s, box-shadow 0.1s;
  -webkit-appearance: none;
}
.generate-btn:active { transform: scale(0.97); box-shadow: 0 4px 15px rgba(232,135,106,0.2); }

.error-banner {
  background: rgba(220,60,60,0.15);
  border: 1px solid rgba(220,60,60,0.3);
  border-radius: 12px;
  padding: 12px 14px;
  font-size: 13px; color: #f08080;
  margin-bottom: 12px;
  display: none;
}

/* ═══════════════════════════════════════
   SCREEN 2 — SUMMARY
═══════════════════════════════════════ */
.summary-scroll { padding: 20px 16px 24px; }

.patient-hero {
  background: linear-gradient(160deg, #2a1510, #141020);
  border: 1px solid rgba(232,135,106,0.25);
  border-radius: 24px;
  padding: 24px 20px;
  margin-bottom: 16px;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.patient-hero::before {
  content: '';
  position: absolute; top: -40px; left: 50%; transform: translateX(-50%);
  width: 200px; height: 200px;
  background: radial-gradient(circle, rgba(232,135,106,0.15), transparent);
  pointer-events: none;
}
.patient-avatar {
  width: 60px; height: 60px;
  background: linear-gradient(135deg, var(--rose-muted), var(--sage-muted));
  border: 2px solid rgba(232,135,106,0.3);
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 26px;
  margin: 0 auto 14px;
}
.patient-name {
  font-family: 'Playfair Display', serif;
  font-size: 22px; font-weight: 600;
  color: var(--text);
  margin-bottom: 4px;
}
.edd-line { font-size: 13px; color: var(--text2); margin-bottom: 16px; }
.edd-date { color: var(--rose-light); font-weight: 600; }

.ga-display {
  background: rgba(255,255,255,0.05);
  border-radius: 14px;
  padding: 14px 16px;
  margin-bottom: 12px;
}
.ga-top { display: flex; justify-content: space-between; align-items: flex-end; margin-bottom: 10px; }
.ga-weeks { font-size: 28px; font-weight: 600; color: var(--rose-light); font-family: 'Playfair Display', serif; }
.ga-label { font-size: 11px; color: var(--text3); text-transform: uppercase; letter-spacing: 1px; }
.ga-days-badge { font-size: 13px; color: var(--text2); }
.progress-track { background: rgba(255,255,255,0.08); border-radius: 99px; height: 6px; overflow: hidden; }
.progress-fill { height: 100%; border-radius: 99px; background: linear-gradient(90deg, var(--rose), var(--sage)); transition: width 1s cubic-bezier(0.4, 0, 0.2, 1); }
.days-left { font-size: 11px; color: var(--text3); margin-top: 6px; text-align: right; }

.info-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 16px; }
.info-tile {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 14px;
}
.info-tile-icon { font-size: 20px; margin-bottom: 6px; }
.info-tile-label { font-size: 10px; color: var(--text3); text-transform: uppercase; letter-spacing: 0.8px; font-weight: 600; margin-bottom: 3px; }
.info-tile-value { font-size: 14px; font-weight: 600; color: var(--text); }

.rh-alert {
  background: linear-gradient(135deg, rgba(232,135,106,0.12), rgba(212,168,85,0.08));
  border: 1.5px solid rgba(232,135,106,0.3);
  border-radius: 16px;
  padding: 14px 16px;
  margin-bottom: 16px;
  display: none;
}
.rh-alert.show { display: block; }
.rh-alert-title { font-size: 13px; font-weight: 600; color: var(--rose-light); margin-bottom: 4px; display: flex; align-items: center; gap: 6px; }
.rh-alert-text { font-size: 12px; color: var(--text2); line-height: 1.5; }

.action-row { display: flex; gap: 10px; margin-bottom: 12px; }
.action-btn {
  flex: 1; padding: 14px 10px;
  border: none; border-radius: 16px;
  font-family: 'Nunito', sans-serif;
  font-size: 13px; font-weight: 600;
  cursor: pointer;
  display: flex; flex-direction: column; align-items: center; gap: 4px;
  transition: transform 0.1s;
  -webkit-appearance: none;
}
.action-btn:active { transform: scale(0.95); }
.action-btn .btn-ico { font-size: 22px; }
.btn-email { background: var(--sage-muted); border: 1.5px solid rgba(126,200,168,0.3); color: var(--sage); }
.btn-wa { background: rgba(37,211,102,0.12); border: 1.5px solid rgba(37,211,102,0.3); color: #25d366; }
.btn-view { background: var(--rose-muted); border: 1.5px solid rgba(232,135,106,0.3); color: var(--rose-light); }
.btn-print { background: rgba(212,168,85,0.12); border: 1.5px solid rgba(212,168,85,0.3); color: var(--gold); }

/* ═══════════════════════════════════════
   SCREEN 3 — SCHEDULE
═══════════════════════════════════════ */
.schedule-scroll { padding: 16px 16px 24px; }

.trimester-header {
  display: flex; align-items: center; gap: 10px;
  margin: 20px 0 12px;
}
.trimester-header:first-child { margin-top: 0; }
.trim-line { flex: 1; height: 1px; background: var(--border); }
.trim-pill {
  font-size: 10px; font-weight: 700;
  text-transform: uppercase; letter-spacing: 1.2px;
  padding: 4px 12px; border-radius: 99px;
}
.trim-pill.t1 { background: rgba(232,135,106,0.15); color: var(--rose-light); border: 1px solid rgba(232,135,106,0.25); }
.trim-pill.t2 { background: rgba(126,200,168,0.15); color: var(--sage); border: 1px solid rgba(126,200,168,0.25); }
.trim-pill.t3 { background: rgba(212,168,85,0.15); color: var(--gold); border: 1px solid rgba(212,168,85,0.25); }

.visit-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 20px;
  margin-bottom: 12px;
  overflow: hidden;
  transition: border-color 0.2s;
}
.visit-card.current {
  border-color: rgba(232,135,106,0.5);
  box-shadow: 0 0 0 1px rgba(232,135,106,0.2), 0 8px 30px rgba(232,135,106,0.1);
}
.visit-card.t2 { border-color: var(--border); }
.visit-card.t2.current { border-color: rgba(126,200,168,0.5); box-shadow: 0 0 0 1px rgba(126,200,168,0.2), 0 8px 30px rgba(126,200,168,0.1); }
.visit-card.t3 { border-color: var(--border); }
.visit-card.t3.current { border-color: rgba(212,168,85,0.5); box-shadow: 0 0 0 1px rgba(212,168,85,0.2), 0 8px 30px rgba(212,168,85,0.1); }

.visit-header {
  padding: 16px 16px 12px;
  cursor: pointer;
  user-select: none;
  -webkit-user-select: none;
}
.visit-top-row { display: flex; align-items: flex-start; justify-content: space-between; gap: 8px; }
.visit-week-badge {
  font-size: 10px; font-weight: 700;
  padding: 3px 10px; border-radius: 99px;
  white-space: nowrap; flex-shrink: 0;
}
.week-t1 { background: rgba(232,135,106,0.15); color: var(--rose-light); }
.week-t2 { background: rgba(126,200,168,0.15); color: var(--sage); }
.week-t3 { background: rgba(212,168,85,0.15); color: var(--gold); }
.visit-title-text {
  font-family: 'Playfair Display', serif;
  font-size: 16px; font-weight: 600;
  color: var(--text); line-height: 1.3;
  flex: 1;
}
.visit-date-text { font-size: 11px; color: var(--text3); margin-top: 4px; }
.current-badge {
  display: inline-block;
  background: var(--rose); color: white;
  font-size: 9px; font-weight: 700;
  padding: 2px 8px; border-radius: 99px;
  letter-spacing: 0.5px;
  margin-top: 5px;
}
.t2 .current-badge { background: var(--sage); }
.t3 .current-badge { background: var(--gold); color: #1a0f0a; }
.visit-chevron { color: var(--text3); font-size: 16px; margin-left: 4px; transition: transform 0.3s; flex-shrink: 0; }
.visit-chevron.open { transform: rotate(90deg); }

.visit-body {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}
.visit-body.open { max-height: 2000px; }
.visit-body-inner { padding: 0 16px 16px; border-top: 1px solid var(--border); padding-top: 14px; }

.test-item {
  display: flex; gap: 10px;
  margin-bottom: 12px;
}
.test-item:last-of-type { margin-bottom: 0; }
.test-dot-wrap { padding-top: 4px; flex-shrink: 0; }
.test-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--rose); }
.test-dot.sage { background: var(--sage); }
.test-dot.gold { background: var(--gold); }
.test-name { font-size: 13px; font-weight: 600; color: var(--text); margin-bottom: 2px; }
.test-info { font-size: 12px; color: var(--text2); line-height: 1.55; }

.visit-note {
  background: var(--surface2);
  border-left: 3px solid var(--rose);
  border-radius: 0 10px 10px 0;
  padding: 10px 12px;
  margin-top: 14px;
  font-size: 11px; color: var(--text2);
  line-height: 1.6;
}
.visit-note.sage-note { border-left-color: var(--sage); }
.visit-note.gold-note { border-left-color: var(--gold); }

/* ═══════════════════════════════════════
   BOTTOM SHEET (SHARE)
═══════════════════════════════════════ */
.sheet-overlay {
  position: fixed; inset: 0;
  background: rgba(0,0,0,0.7);
  z-index: 100;
  display: none;
  align-items: flex-end;
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
}
.sheet-overlay.open { display: flex; }
.bottom-sheet {
  width: 100%;
  background: var(--surface);
  border-radius: 24px 24px 0 0;
  padding: 0 20px;
  padding-bottom: calc(20px + var(--safe-bottom));
  transform: translateY(100%);
  transition: transform 0.35s cubic-bezier(0.4, 0, 0.2, 1);
  border-top: 1px solid var(--border2);
}
.sheet-overlay.open .bottom-sheet { transform: translateY(0); }
.sheet-handle { width: 36px; height: 4px; background: var(--text3); border-radius: 99px; margin: 12px auto 20px; }
.sheet-title { font-family: 'Playfair Display', serif; font-size: 20px; margin-bottom: 6px; }
.sheet-sub { font-size: 12px; color: var(--text2); margin-bottom: 20px; line-height: 1.5; }
.sheet-link {
  display: block;
  background: var(--surface2);
  border: 1px solid var(--border2);
  border-radius: 12px;
  padding: 12px 14px;
  font-size: 11px; color: var(--text2);
  word-break: break-all;
  margin-bottom: 14px;
  text-decoration: none;
  line-height: 1.5;
}
.sheet-btn {
  width: 100%; padding: 15px;
  border: none; border-radius: 14px;
  font-family: 'Nunito', sans-serif;
  font-size: 15px; font-weight: 600;
  cursor: pointer; margin-bottom: 10px;
  -webkit-appearance: none;
  transition: transform 0.1s;
}
.sheet-btn:active { transform: scale(0.97); }
.sheet-btn-primary { background: var(--rose); color: white; }
.sheet-btn-secondary { background: var(--surface2); color: var(--text); }

/* ═══════════════════════════════════════
   INSTALL HINT
═══════════════════════════════════════ */
.install-hint {
  background: rgba(126,200,168,0.08);
  border: 1px solid rgba(126,200,168,0.2);
  border-radius: 14px;
  padding: 12px 14px;
  margin-bottom: 16px;
  font-size: 12px;
  color: var(--text2);
  line-height: 1.55;
  display: flex; gap: 10px; align-items: flex-start;
}
.install-hint .ih-icon { font-size: 20px; flex-shrink: 0; }

/* ═══════════════════════════════════════
   ANIMATIONS
═══════════════════════════════════════ */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(16px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-in { animation: fadeUp 0.4s ease both; }
.delay-1 { animation-delay: 0.05s; }
.delay-2 { animation-delay: 0.10s; }
.delay-3 { animation-delay: 0.15s; }
.delay-4 { animation-delay: 0.20s; }

/* iOS standalone full-screen feel */
@media (display-mode: standalone) {
  .install-hint { display: none; }
}

/* ═══════════════════════════════════════
   DATE PICKER WHEEL
═══════════════════════════════════════ */
.picker-overlay {
  position: fixed; inset: 0;
  background: rgba(0,0,0,0.72);
  z-index: 200;
  display: none;
  align-items: flex-end;
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
}
.picker-overlay.open { display: flex; }
.picker-sheet {
  width: 100%;
  background: #1e1510;
  border-radius: 24px 24px 0 0;
  border-top: 1px solid rgba(255,255,255,0.1);
  padding-bottom: calc(16px + env(safe-area-inset-bottom, 34px));
  transform: translateY(100%);
  transition: transform 0.35s cubic-bezier(0.4,0,0.2,1);
}
.picker-overlay.open .picker-sheet { transform: translateY(0); }
.picker-toolbar {
  display: flex; justify-content: space-between; align-items: center;
  padding: 14px 20px 10px;
  border-bottom: 1px solid rgba(255,255,255,0.07);
}
.picker-toolbar-title { font-size: 15px; font-weight: 600; color: var(--text); }
.picker-btn {
  font-family: 'Nunito', sans-serif;
  font-size: 15px; font-weight: 600;
  background: none; border: none; cursor: pointer; padding: 4px 8px;
}
.picker-btn-cancel { color: var(--text3); }
.picker-btn-done { color: var(--rose-light); }

.picker-wheels {
  display: flex;
  height: 220px;
  position: relative;
  overflow: hidden;
}
/* Selection highlight bar */
.picker-wheels::before,
.picker-wheels::after {
  content: '';
  position: absolute; left: 10px; right: 10px;
  height: 44px;
  top: 50%; transform: translateY(-50%);
  pointer-events: none;
  z-index: 2;
}
.picker-wheels::before {
  background: rgba(232,135,106,0.1);
  border-top: 1px solid rgba(232,135,106,0.3);
  border-bottom: 1px solid rgba(232,135,106,0.3);
  border-radius: 10px;
}
/* Fade top & bottom */
.picker-wheels::after {
  height: 100%;
  top: 0; transform: none;
  background: linear-gradient(
    to bottom,
    #1e1510 0%,
    transparent 30%,
    transparent 70%,
    #1e1510 100%
  );
}

.picker-col {
  flex: 1;
  overflow-y: scroll;
  -webkit-overflow-scrolling: touch;
  scroll-snap-type: y mandatory;
  scrollbar-width: none;
  -ms-overflow-style: none;
  padding: 88px 0; /* (220 - 44) / 2 */
}
.picker-col::-webkit-scrollbar { display: none; }

.picker-item {
  height: 44px;
  display: flex; align-items: center; justify-content: center;
  font-size: 20px; font-weight: 500;
  color: var(--text2);
  scroll-snap-align: center;
  cursor: pointer;
  transition: color 0.15s;
  user-select: none;
  -webkit-user-select: none;
}
.picker-item.selected { color: var(--text); font-weight: 600; }

/* column width hints */
.picker-col-day { flex: 0.8; }
.picker-col-month { flex: 1.4; }
.picker-col-year { flex: 1; }
</style>
</head>
<body>
<div id="app">
  <div class="status-bar"></div>

  <!-- TOP NAV -->
  <div class="top-nav" id="topNav">
    <div class="nav-back-placeholder"></div>
    <div style="text-align:center;">
      <div class="nav-title">OB Care Planner</div>
      <div class="nav-subtitle">Prenatal Schedule</div>
    </div>
    <div class="nav-icon">🌸</div>
  </div>

  <!-- ═══ SCREEN: FORM ═══ -->
  <div class="screen active" id="screenForm">
    <div class="scroll-area">
      <div class="form-scroll">

        <div class="install-hint animate-in">
          <span class="ih-icon">📲</span>
          <div>
            <strong style="color:var(--sage);display:block;margin-bottom:4px;">How to install this as a real app:</strong>
            1. Go to <strong>github.com</strong> on your laptop → sign up free<br/>
            2. New repository → name it <strong>ob-planner</strong> → Public → Create<br/>
            3. Upload this HTML file → Commit changes<br/>
            4. Settings → Pages → Branch: main → Save<br/>
            5. Open the <strong>github.io</strong> URL in Safari on iPhone<br/>
            6. Tap <strong>Share ⬆ → Add to Home Screen → Add</strong><br/>
            <span style="color:var(--gold);margin-top:4px;display:block;">✓ Free forever · No password · Works offline · Real app icon</span>
          </div>
        </div>

        <div class="hero-card animate-in delay-1">
          <span class="hero-emoji">🤰</span>
          <div class="hero-title">Welcome to your<br/>prenatal journey</div>
          <div class="hero-sub">Enter your patient's details to generate a complete, personalised prenatal care schedule.</div>
        </div>

        <div id="errorBanner" class="error-banner">⚠️ Please fill in all required fields.</div>

        <div class="section-label animate-in delay-2">Patient Identity</div>
        <div class="input-group animate-in delay-2">
          <div class="input-row">
            <div class="input-icon">👤</div>
            <div class="input-inner">
              <div class="input-lbl">First Name *</div>
              <input type="text" id="fFirstName" placeholder="e.g. Maria" autocomplete="given-name"/>
            </div>
          </div>
          <div class="input-row">
            <div class="input-icon">👤</div>
            <div class="input-inner">
              <div class="input-lbl">Family Name *</div>
              <input type="text" id="fLastName" placeholder="e.g. Khoury" autocomplete="family-name"/>
            </div>
          </div>
          <div class="input-row" onclick="openDatePicker('dob')" style="cursor:pointer;">
            <div class="input-icon">🎂</div>
            <div class="input-inner">
              <div class="input-lbl">Date of Birth</div>
              <div id="fDobDisplay" style="font-size:15px;color:var(--text3);padding:2px 0;">Tap to select</div>
            </div>
            <div style="color:var(--text3);font-size:18px;margin-left:4px;">›</div>
          </div>
        </div>

        <div class="section-label animate-in delay-3">Pregnancy Dates</div>
        <div class="input-group animate-in delay-3">
          <div class="input-row" onclick="openDatePicker('lmp')" style="cursor:pointer;">
            <div class="input-icon">📅</div>
            <div class="input-inner">
              <div class="input-lbl">Last Menstrual Period (LMP) *</div>
              <div id="fLmpDisplay" style="font-size:15px;color:var(--text3);padding:2px 0;">Tap to select</div>
              <div class="input-hint">First day of last period</div>
            </div>
            <div style="color:var(--text3);font-size:18px;margin-left:4px;">›</div>
          </div>
        </div>

        <div class="section-label animate-in delay-3">Blood Group</div>
        <div class="rh-selector animate-in delay-3">
          <div class="rh-label-top"><span>🩸</span> Rhesus Factor</div>
          <div class="rh-options">
            <button class="rh-opt" id="rhPos" onclick="setRh('positive')">Rh + Positive</button>
            <button class="rh-opt" id="rhNeg" onclick="setRh('negative')">Rh − Negative</button>
            <button class="rh-opt" id="rhUnk" onclick="setRh('unknown')">Unknown</button>
          </div>
        </div>

        <div class="section-label animate-in delay-4">Contact Details</div>
        <div class="input-group animate-in delay-4">
          <div class="input-row">
            <div class="input-icon">📧</div>
            <div class="input-inner">
              <div class="input-lbl">Email Address</div>
              <input type="email" id="fEmail" placeholder="patient@email.com" autocomplete="email" inputmode="email"/>
            </div>
          </div>
          <div class="input-row">
            <div class="input-icon">📱</div>
            <div class="input-inner">
              <div class="input-lbl">Mobile / WhatsApp</div>
              <input type="tel" id="fPhone" placeholder="+961 70 000 000" inputmode="tel"/>
              <div class="input-hint">Include country code for WhatsApp</div>
            </div>
          </div>
        </div>

        <div style="height: 8px;"></div>

      </div>
    </div>
    <!-- STICKY GENERATE BUTTON — outside scroll so it's always reachable -->
    <div style="
      padding: 12px 16px;
      padding-bottom: calc(12px + env(safe-area-inset-bottom, 20px));
      background: var(--bg);
      border-top: 1px solid var(--border);
      flex-shrink: 0;
    ">
      <button class="generate-btn" onclick="generate()">
        <span>✦</span> Generate Prenatal Schedule
      </button>
    </div>
  </div>

  <!-- ═══ SCREEN: SUMMARY ═══ -->
  <div class="screen" id="screenSummary">
    <div class="scroll-area">
      <div class="summary-scroll" id="summaryContent"></div>
    </div>
  </div>

  <!-- ═══ SCREEN: SCHEDULE ═══ -->
  <div class="screen" id="screenSchedule">
    <div class="scroll-area">
      <div class="schedule-scroll" id="scheduleContent"></div>
    </div>
  </div>

  <!-- TAB BAR -->
  <div class="tab-bar">
    <button class="tab-item active" id="tab0" onclick="switchTab(0)">
      <div class="tab-icon">✏️</div>
      <div class="tab-label">Patient</div>
    </button>
    <button class="tab-item" id="tab1" onclick="switchTab(1)">
      <div class="tab-icon">📊</div>
      <div class="tab-label">Summary</div>
      <div class="tab-badge" id="badge1">!</div>
    </button>
    <button class="tab-item" id="tab2" onclick="switchTab(2)">
      <div class="tab-icon">📋</div>
      <div class="tab-label">Schedule</div>
      <div class="tab-badge" id="badge2">!</div>
    </button>
  </div>
</div>

<!-- DATE PICKER WHEEL -->
<div class="picker-overlay" id="datePickerOverlay" onclick="cancelDatePicker()">
  <div class="picker-sheet" onclick="event.stopPropagation()">
    <div class="picker-toolbar">
      <button class="picker-btn picker-btn-cancel" onclick="cancelDatePicker()">Cancel</button>
      <div class="picker-toolbar-title" id="pickerTitle">Date of Birth</div>
      <button class="picker-btn picker-btn-done" onclick="confirmDatePicker()">Done</button>
    </div>
    <div class="picker-wheels">
      <div class="picker-col picker-col-day" id="pickerDay"></div>
      <div class="picker-col picker-col-month" id="pickerMonth"></div>
      <div class="picker-col picker-col-year" id="pickerYear"></div>
    </div>
  </div>
</div>

<!-- BOTTOM SHEET: EMAIL -->
<div class="sheet-overlay" id="emailSheet" onclick="closeSheet('emailSheet')">
  <div class="bottom-sheet" onclick="event.stopPropagation()">
    <div class="sheet-handle"></div>
    <div class="sheet-title">✉️ Email via Outlook</div>
    <div class="sheet-sub">Opens Microsoft Outlook with the patient's email and full schedule pre-filled. Outlook must be installed on your iPhone.</div>
    <div id="emailSheetLink" class="sheet-link">—</div>
    <button id="emailSheetBtn" class="sheet-btn sheet-btn-primary" style="border:none;cursor:pointer;font-family:inherit;">Open Outlook</button>
    <button class="sheet-btn sheet-btn-secondary" onclick="closeSheet('emailSheet')">Cancel</button>
  </div>
</div>

<!-- BOTTOM SHEET: WHATSAPP -->
<div class="sheet-overlay" id="waSheet" onclick="closeSheet('waSheet')">
  <div class="bottom-sheet" onclick="event.stopPropagation()">
    <div class="sheet-handle"></div>
    <div class="sheet-title">📱 WhatsApp Patient</div>
    <div class="sheet-sub">Opens WhatsApp with the patient's number and a complete schedule summary ready to send.</div>
    <a id="waSheetLink" class="sheet-link" href="#">—</a>
    <a id="waSheetBtn" class="sheet-btn sheet-btn-primary" href="#" style="display:block;text-align:center;text-decoration:none;padding:15px;border-radius:14px;background:#25d366;color:white;">Open WhatsApp</a>
    <button class="sheet-btn sheet-btn-secondary" onclick="closeSheet('waSheet')">Cancel</button>
  </div>
</div>

<script>
// ─────────────────────────────────────
// STATE
// ─────────────────────────────────────
let state = {
  firstName:'', lastName:'', dob:'', lmp:null,
  edd:null, ga:{weeks:0,days:0,total:0},
  rhesus:'', phone:'', email:'',
  generated: false
};
let rhSelected = '';

// ─────────────────────────────────────
// SCHEDULE DATA
// ─────────────────────────────────────
const SCHEDULE = [
  {
    id:'v1', trim:1,
    title:'First Prenatal Visit — Dating & Baseline Blood Work',
    wFrom:6, wTo:7,
    note:'Come fasting (nothing to eat 8 hours before) so all blood tests can be done in one session. This is your most important first appointment.',
    tests:[
      {name:'Complete Blood Count (CBC)', info:'Checks for anaemia, platelet count, and general blood health — the baseline for the whole pregnancy.', dot:'rose'},
      {name:'HbA1c (Glycated Haemoglobin)', info:'Screens for pre-existing diabetes before pregnancy significantly alters blood sugar levels.', dot:'rose'},
      {name:'Iron Studies & Ferritin', info:'Measures your iron stores. Deficiency is very common in pregnancy and needs early treatment.', dot:'rose'},
      {name:'Folic Acid Level', info:'Confirms adequate folate, which is essential to prevent neural tube defects in the baby.', dot:'rose'},
      {name:'Blood Group & Rhesus Factor', info:'Determines your blood type and Rh status — critical for anti-D planning.', dot:'rose'},
      {name:'Toxoplasmosis IgG & IgM', info:'Checks immunity to a parasite found in undercooked meat and cat faeces that can harm the baby.', dot:'rose'},
      {name:'Rubella IgG & IgM', info:'Rubella in early pregnancy can cause severe birth defects — this confirms your immunity status.', dot:'rose'},
      {name:'CMV (Cytomegalovirus) IgG & IgM', info:'Screens for CMV infection, which can affect fetal development if acquired during pregnancy.', dot:'rose'},
      {name:'HIV Test', info:'Routine confidential screening — if positive, treatment virtually eliminates transmission to your baby.', dot:'rose'},
      {name:'VDRL (Syphilis Serology)', info:'Syphilis is easily treated but causes serious harm if missed. This is a standard screen.', dot:'rose'},
      {name:'HBsAg (Hepatitis B Surface Antigen)', info:'Determines if you carry Hepatitis B so your baby can receive protective vaccination at birth.', dot:'rose'},
      {name:'Transvaginal Ultrasound (Dating Scan)', info:'Confirms the pregnancy is inside the uterus, measures the embryo, and sets the accurate due date.', dot:'sage'},
    ]
  },
  {
    id:'v2', trim:1,
    title:'Heartbeat Confirmation Visit',
    wFrom:8, wTo:9,
    note:'A short but deeply reassuring visit. Hearing your baby\'s heartbeat for the first time is a very special milestone that also significantly reduces miscarriage risk.',
    tests:[
      {name:'Ultrasound — Fetal Heartbeat', info:'At 8 weeks the heartbeat is clearly visible and audible on ultrasound. We confirm embryonic growth and cardiac activity.', dot:'sage'},
    ]
  },
  {
    id:'v3', trim:1,
    title:'NIPT — Non-Invasive Prenatal Testing',
    wFrom:10, wTo:13,
    note:'NIPT is optional but highly recommended. It is completely safe — only a maternal blood draw is needed, with no risk to the baby. Results take 7–10 days.',
    tests:[
      {name:'NIPT Blood Test (Cell-Free DNA)', info:'Analyses baby\'s DNA fragments in your blood. Screens for Down syndrome (Trisomy 21), Trisomy 18, Trisomy 13, and sex chromosome anomalies with over 99% sensitivity.', dot:'rose'},
    ]
  },
  {
    id:'v4', trim:1,
    title:'First Trimester Serological Screening',
    wFrom:11, wTo:13,
    note:'This blood test is timed to work together with the NT ultrasound (next visit). The combination gives a personalised chromosomal risk score.',
    tests:[
      {name:'Free β-hCG & PAPP-A Blood Test', info:'Two pregnancy hormones measured in your blood. Combined with the NT measurement, they calculate a personal risk score for chromosomal abnormalities — the standard first-trimester screening protocol.', dot:'rose'},
    ]
  },
  {
    id:'v5', trim:1,
    title:'First Trimester Ultrasound — NT Scan',
    wFrom:12, wTo:13,
    note:'The NT scan must be done within a precise window (11w 3d – 13w 6d). Please book in advance as the timing is critical and cannot be delayed.',
    tests:[
      {name:'Nuchal Translucency (NT) Measurement', info:'Measures fluid at the back of the baby\'s neck. Increased NT can suggest chromosomal or cardiac issues. Combined with blood tests, it gives a chromosomal risk estimate.', dot:'sage'},
      {name:'Nasal Bone Assessment', info:'Absence of the nasal bone adds important information to the chromosomal risk calculation.', dot:'sage'},
      {name:'Early Fetal Anatomy Overview', info:'We can already see the baby\'s developing brain, spine, and limbs. Number of babies is confirmed (twins check).', dot:'sage'},
    ]
  },
  {
    id:'v6', trim:2,
    title:'Second Trimester Serological Screening (Triple Test)',
    wFrom:15, wTo:17,
    note:'If you already had NIPT and first-trimester combined screening, discuss with your doctor whether this test adds further value in your specific case.',
    tests:[
      {name:'Triple Test (AFP, β-hCG, uE3)', info:'Measures three markers — Alpha-Fetoprotein, human chorionic gonadotropin, and unconjugated Estriol — to reassess risk for Down syndrome and neural tube defects in the second trimester.', dot:'rose'},
    ]
  },
  {
    id:'v7', trim:2,
    title:'Morphology Ultrasound — Detailed Anatomy Scan',
    wFrom:20, wTo:24,
    note:'This is the most comprehensive ultrasound of the pregnancy. Allow 45–60 minutes. The baby\'s sex can be revealed at this scan if you wish.',
    tests:[
      {name:'Fetal Morphology / Anomaly Scan', info:'A detailed head-to-toe examination: brain, face, heart (4 chambers), lungs, abdomen, kidneys, limbs, and spine. Detects the majority of major structural abnormalities.', dot:'sage'},
      {name:'Placenta Localisation', info:'Confirms the placenta is not covering the cervix (placenta praevia), which would affect delivery planning.', dot:'sage'},
      {name:'Cervical Length Measurement', info:'Assesses risk of preterm labour. A short cervix may require preventive treatment.', dot:'sage'},
    ]
  },
  {
    id:'v8', trim:2,
    title:'Glucose Tolerance Test — Gestational Diabetes Screening',
    wFrom:24, wTo:28,
    note:'Come FASTING — nothing to eat or drink except water from midnight. The test takes about 2 hours at the laboratory. Gestational diabetes is very manageable when detected early.',
    tests:[
      {name:'Oral Glucose Tolerance Test (OGTT 75g)', info:'You drink a glucose solution; blood is taken at 0, 1, and 2 hours. Screens for gestational diabetes, which — if undetected — can cause a large baby, difficult delivery, and metabolic problems.', dot:'rose'},
    ]
  },
  {
    id:'v8b', trim:2, rhesusOnly:true,
    title:'Anti-D Immunoglobulin Injection',
    wFrom:28, wTo:28,
    note:'THIS APPOINTMENT IS MANDATORY for Rh Negative mothers. Missing this injection puts future pregnancies at serious risk. The injection is completely safe for you and your baby.',
    tests:[
      {name:'Anti-D Immunoglobulin Injection (300 mcg)', info:'Prevents your immune system from forming antibodies against your baby\'s blood cells (Rh sensitisation). Without this, future pregnancies with Rh Positive babies could be endangered by haemolytic disease of the newborn.', dot:'rose'},
    ]
  },
  {
    id:'v9', trim:3,
    title:'Third Trimester Growth Ultrasound',
    wFrom:30, wTo:34,
    note:'Growth scans may be repeated every 3–4 weeks if a concern is found. One scan in this window is the standard of care for uncomplicated pregnancies.',
    tests:[
      {name:'Fetal Biometry (Head, Abdomen, Femur)', info:'Precise measurements plotted on growth curves confirm the baby is growing appropriately.', dot:'sage'},
      {name:'Estimated Fetal Weight (EFW)', info:'Calculated from biometry measurements. Alerts to both growth restriction (too small) and macrosomia (too large).', dot:'sage'},
      {name:'Amniotic Fluid Assessment', info:'Too little (oligohydramnios) or too much (polyhydramnios) fluid can indicate placental or fetal issues.', dot:'sage'},
      {name:'Doppler Blood Flow Studies', info:'Measures blood flow in the umbilical artery and fetal brain to assess placental function and oxygenation.', dot:'sage'},
      {name:'Placenta Position Reassessment', info:'A low-lying placenta seen at 20 weeks is re-evaluated to confirm it has migrated clear of the cervix.', dot:'sage'},
    ]
  },
  {
    id:'v10', trim:3,
    title:'Group B Streptococcus Vaginal Screening',
    wFrom:36, wTo:37,
    note:'A quick and painless vaginal swab. If positive, you will receive IV antibiotics during labour — this is very effective at fully protecting your baby.',
    tests:[
      {name:'GBS Vaginal & Rectal Swab', info:'GBS is carried by ~25% of women without causing them harm, but can cause serious newborn infection if passed during birth. Knowing your status lets us give antibiotics in labour and completely protect your baby.', dot:'rose'},
    ]
  },
  {
    id:'v11', trim:3,
    title:'Final Pre-Delivery Consultation',
    wFrom:36, wTo:38,
    note:'Come with all your questions about labour, delivery, and postpartum care. We will review your full pregnancy file and discuss your birth plan together.',
    tests:[
      {name:'Clinical Examination & Baby Position', info:'Confirms whether the baby is head-down or breech. If breech, options including external cephalic version (ECV) or planned caesarean will be discussed.', dot:'gold'},
      {name:'Birth Plan Review & Labour Counselling', info:'Review of all pregnancy results, discussion of mode of delivery, signs of labour to watch for, when to go to hospital, pain relief options, and postpartum care.', dot:'gold'},
      {name:'Post-Delivery Anti-D (Rh Negative)', info:'A final anti-D dose will be given after delivery if your baby proves to be Rh Positive.', dot:'rose'},
    ]
  },
];

// ─────────────────────────────────────
// HELPERS
// ─────────────────────────────────────
function fmt(d) {
  if (!d) return '—';
  return d.toLocaleDateString('en-GB', {day:'2-digit', month:'long', year:'numeric'});
}
function fmtShort(d) {
  if (!d) return '—';
  return d.toLocaleDateString('en-GB', {day:'2-digit', month:'short', year:'numeric'});
}
function addDays(d, n) { const r=new Date(d); r.setDate(r.getDate()+n); return r; }
function addWeeks(d, w) { return addDays(d, w*7); }
function calcGA(lmp, today) {
  const diff = Math.floor((today - lmp) / 86400000);
  return { weeks: Math.floor(diff/7), days: diff%7, total: diff };
}

// ─────────────────────────────────────
// RH SELECTOR
// ─────────────────────────────────────
function setRh(val) {
  rhSelected = val;
  document.getElementById('rhPos').className = 'rh-opt' + (val==='positive' ? ' selected-pos' : '');
  document.getElementById('rhNeg').className = 'rh-opt' + (val==='negative' ? ' selected-neg' : '');
  document.getElementById('rhUnk').className = 'rh-opt' + (val==='unknown' ? ' selected-unk' : '');
}

// ─────────────────────────────────────
// TAB SWITCHING
// ─────────────────────────────────────
const screens = ['screenForm','screenSummary','screenSchedule'];
let activeTab = 0;
function switchTab(i) {
  if (i > 0 && !state.generated) { showError('Please generate a schedule first.'); return; }
  screens.forEach((s,idx) => {
    document.getElementById(s).classList.toggle('active', idx===i);
    document.getElementById('tab'+idx).classList.toggle('active', idx===i);
  });
  activeTab = i;
  if (i===1) { document.getElementById('badge1').classList.remove('show'); }
  if (i===2) { document.getElementById('badge2').classList.remove('show'); }
  // Show tab bar only on summary/schedule screens
  document.querySelector('.tab-bar').classList.toggle('visible', i > 0);
}

// ─────────────────────────────────────
// GENERATE
// ─────────────────────────────────────
function generate() {
  const fn = document.getElementById('fFirstName').value.trim();
  const ln = document.getElementById('fLastName').value.trim();
  if (!fn || !ln) { showError('Please fill in First Name and Family Name.'); return; }
  if (!pickerValues.lmp) { showError('Please select the Last Menstrual Period (LMP) date.'); return; }
  document.getElementById('errorBanner').style.display='none';

  const lmp = pickerValues.lmp;
  const today = new Date(); today.setHours(0,0,0,0);
  const edd = addDays(lmp, 280);
  const ga = calcGA(lmp, today);
  const dob = pickerValues.dob || null;
  const phone = document.getElementById('fPhone').value.trim();
  const email = document.getElementById('fEmail').value.trim();

  state = { firstName:fn, lastName:ln, dob, lmp, edd, ga, rhesus:rhSelected, phone, email, generated:true };

  buildSummary();
  buildSchedule();

  document.getElementById('badge1').classList.add('show');
  document.getElementById('badge2').classList.add('show');
  document.querySelector('.tab-bar').classList.add('visible');
  switchTab(1);
}

function showError(msg) {
  const el = document.getElementById('errorBanner');
  el.textContent = '⚠️ ' + msg;
  el.style.display = 'block';
}

// ─────────────────────────────────────
// BUILD SUMMARY
// ─────────────────────────────────────
function buildSummary() {
  const { firstName, lastName, dob, lmp, edd, ga, rhesus } = state;
  const pct = Math.min(100, Math.max(0, (ga.total / 280) * 100));
  const daysLeft = Math.max(0, Math.floor((edd - new Date().setHours(0,0,0,0)) / 86400000));
  const trimester = ga.weeks <= 13 ? '1st Trimester' : ga.weeks <= 27 ? '2nd Trimester' : '3rd Trimester';

  document.getElementById('summaryContent').innerHTML = `
    <div class="patient-hero animate-in">
      <div class="patient-avatar">🤰</div>
      <div class="patient-name">${firstName} ${lastName}</div>
      <div class="edd-line">Estimated Due Date: <span class="edd-date">${fmt(edd)}</span></div>
      <div class="ga-display">
        <div class="ga-top">
          <div>
            <div class="ga-label">Gestational Age Today</div>
            <div class="ga-weeks">${ga.weeks}<span style="font-size:16px;color:var(--text2)"> wks</span></div>
          </div>
          <div class="ga-days-badge">${ga.days} day${ga.days!==1?'s':''} extra<br/><span style="color:var(--text3);font-size:10px;">${trimester}</span></div>
        </div>
        <div class="progress-track">
          <div class="progress-fill" style="width:${pct}%"></div>
        </div>
        <div class="days-left">${ga.total > 280 ? 'Past estimated due date' : daysLeft + ' days until EDD'}</div>
      </div>
    </div>

    <div class="info-grid animate-in delay-1">
      <div class="info-tile">
        <div class="info-tile-icon">📅</div>
        <div class="info-tile-label">LMP</div>
        <div class="info-tile-value">${fmtShort(lmp)}</div>
      </div>
      <div class="info-tile">
        <div class="info-tile-icon">🎯</div>
        <div class="info-tile-label">Due Date</div>
        <div class="info-tile-value">${fmtShort(edd)}</div>
      </div>
      <div class="info-tile">
        <div class="info-tile-icon">🎂</div>
        <div class="info-tile-label">Date of Birth</div>
        <div class="info-tile-value">${dob ? fmtShort(new Date(dob)) : 'Not set'}</div>
      </div>
      <div class="info-tile">
        <div class="info-tile-icon">🩸</div>
        <div class="info-tile-label">Rhesus</div>
        <div class="info-tile-value" style="color:${rhesus==='negative'?'var(--rose)':rhesus==='positive'?'var(--sage)':'var(--gold)'}">
          ${rhesus==='positive'?'Rh Positive (+)':rhesus==='negative'?'Rh Negative (−)':rhesus==='unknown'?'Unknown':'Not set'}
        </div>
      </div>
    </div>

    <div class="rh-alert ${rhesus==='negative'?'show':''} animate-in delay-2">
      <div class="rh-alert-title">⚠️ Rhesus Negative — Important</div>
      <div class="rh-alert-text">As your blood group is Rh Negative, you require Anti-D immunoglobulin injections at specific points in your pregnancy. These are included in your schedule and are essential to protect future pregnancies.</div>
    </div>

    <div class="action-row animate-in delay-2">
      <button class="action-btn btn-view" onclick="switchTab(2)">
        <span class="btn-ico">📋</span>
        View Schedule
      </button>
      <button class="action-btn btn-email" onclick="openEmailSheet()">
        <span class="btn-ico">✉️</span>
        Email
      </button>
      <button class="action-btn btn-wa" onclick="openWaSheet()">
        <span class="btn-ico">📱</span>
        WhatsApp
      </button>
      <button class="action-btn btn-print" onclick="openPrintSheet()">
        <span class="btn-ico">🖨️</span>
        Print
      </button>
    </div>
  `;
}

// ─────────────────────────────────────
// BUILD SCHEDULE
// ─────────────────────────────────────
function buildSchedule() {
  const { lmp, ga, rhesus } = state;
  const container = document.getElementById('scheduleContent');
  container.innerHTML = '';

  // Add share row at top
  container.innerHTML = `
    <div class="action-row" style="margin-bottom:8px;">
      <button class="action-btn btn-email" onclick="openEmailSheet()"><span class="btn-ico">✉️</span>Email</button>
      <button class="action-btn btn-wa" onclick="openWaSheet()"><span class="btn-ico">📱</span>WhatsApp</button>
      <button class="action-btn btn-print" onclick="openPrintSheet()"><span class="btn-ico">🖨️</span>Print</button>
    </div>
  `;

  let currentTrim = 0;
  const trimLabels = {1:'🌱 First Trimester', 2:'🌿 Second Trimester', 3:'🌳 Third Trimester'};
  const trimClasses = {1:'t1', 2:'t2', 3:'t3'};

  SCHEDULE.forEach((v, idx) => {
    if (v.rhesusOnly && rhesus !== 'negative') return;

    if (v.trim !== currentTrim) {
      currentTrim = v.trim;
      const sep = document.createElement('div');
      sep.className = 'trimester-header';
      sep.innerHTML = `<div class="trim-line"></div><div class="trim-pill ${trimClasses[currentTrim]}">${trimLabels[currentTrim]}</div><div class="trim-line"></div>`;
      container.appendChild(sep);
    }

    const dateFrom = addWeeks(lmp, v.wFrom);
    const dateTo = v.wTo !== v.wFrom ? addWeeks(lmp, v.wTo) : null;
    const dateLabel = dateTo ? `${fmtShort(dateFrom)} – ${fmtShort(dateTo)}` : fmtShort(dateFrom);
    const weekLabel = v.wTo !== v.wFrom ? `Weeks ${v.wFrom}–${v.wTo}` : `Week ${v.wFrom}`;
    const isCurrent = ga.weeks >= v.wFrom - 1 && ga.weeks <= (v.wTo + 1);

    const tClass = trimClasses[v.trim];
    const wkBadgeClass = `week-${tClass}`;
    const noteClass = v.trim===2 ? 'sage-note' : v.trim===3 ? 'gold-note' : '';

    let testsHTML = v.tests.map(t => `
      <div class="test-item">
        <div class="test-dot-wrap"><div class="test-dot ${t.dot}"></div></div>
        <div>
          <div class="test-name">${t.name}</div>
          <div class="test-info">${t.info}</div>
        </div>
      </div>
    `).join('');

    const card = document.createElement('div');
    card.className = `visit-card ${tClass}${isCurrent?' current':''}`;
    card.innerHTML = `
      <div class="visit-header" onclick="toggleCard('body_${v.id}', 'chev_${v.id}')">
        <div class="visit-top-row">
          <div style="flex:1">
            <div class="visit-title-text">${v.title}</div>
            <div class="visit-date-text">${dateLabel}</div>
            ${isCurrent ? '<div class="current-badge">Current Period</div>' : ''}
          </div>
          <div style="display:flex;flex-direction:column;align-items:flex-end;gap:6px;flex-shrink:0;">
            <span class="visit-week-badge ${wkBadgeClass}">${weekLabel}</span>
            <span class="visit-chevron" id="chev_${v.id}">›</span>
          </div>
        </div>
      </div>
      <div class="visit-body${isCurrent?' open':''}" id="body_${v.id}">
        <div class="visit-body-inner">
          ${testsHTML}
          ${v.note ? `<div class="visit-note ${noteClass}">📌 ${v.note}</div>` : ''}
        </div>
      </div>
    `;
    if (isCurrent) {
      card.querySelector('.visit-chevron').classList.add('open');
    }
    container.appendChild(card);
  });
}

function toggleCard(bodyId, chevId) {
  const body = document.getElementById(bodyId);
  const chev = document.getElementById(chevId);
  const isOpen = body.classList.contains('open');
  body.classList.toggle('open', !isOpen);
  chev.classList.toggle('open', !isOpen);
}

// ─────────────────────────────────────
// MESSAGE BUILDER
// ─────────────────────────────────────
function buildMessage() {
  const { firstName, lastName, lmp, edd, ga, rhesus } = state;
  const rh = rhesus==='negative' ? '\n💉 28 Weeks — Anti-D Injection (MANDATORY — Rh Negative)' : '';
  return [
    `🌸 Prenatal Care Plan — ${firstName} ${lastName}`,
    ``,
    `📅 LMP: ${fmt(lmp)}`,
    `🎯 Estimated Due Date: ${fmt(edd)}`,
    `📊 Gestational Age: ${ga.weeks} weeks ${ga.days} days`,
    ``,
    `📋 YOUR PRENATAL SCHEDULE:`,
    ``,
    `1. ✅ 6–7 Weeks — First visit: CBC, HbA1c, Iron, Folic Acid, Blood Group, Toxoplasmosis, Rubella, CMV, HIV, VDRL, HBsAg + Dating Ultrasound`,
    `2. 💓 8 Weeks — Heartbeat confirmation ultrasound`,
    `3. 🧬 10–13 Weeks — NIPT (cell-free DNA screening)`,
    `4. 🔬 11–13 Weeks — First trimester serology (PAPP-A & β-hCG)`,
    `5. 📡 12–13 Weeks — NT Ultrasound (Nuchal Translucency)`,
    `6. 🔬 15–17 Weeks — Triple Test (second trimester serology)`,
    `7. 🔍 20–24 Weeks — Full morphology / anomaly ultrasound`,
    `8. 🍬 24–28 Weeks — Glucose Tolerance Test (come FASTING)`,
    rh,
    `9. 📈 30–34 Weeks — Growth ultrasound with Doppler`,
    `10. 🦠 36 Weeks — Group B Streptococcus vaginal swab`,
    `11. 🏁 36–38 Weeks — Final consultation & birth plan`,
    ``,
    `Please contact the clinic with any questions. Take good care! 💙`,
  ].filter(l => l !== null && l !== '').join('\n');
}

// ─────────────────────────────────────
// SHARE SHEETS
// ─────────────────────────────────────
function openEmailSheet() {
  const { email } = state;
  const subj = encodeURIComponent(`Your Prenatal Care Schedule — ${state.firstName} ${state.lastName}`);
  const body = encodeURIComponent(buildMessage());
  // ms-outlook:// deep link opens Outlook directly on iOS instead of Apple Mail
  const outlookHref = `ms-outlook://compose?to=${encodeURIComponent(email||'')}&subject=${subj}&body=${body}`;
  const fallbackHref = `mailto:${email||''}?subject=${subj}&body=${body}`;
  document.getElementById('emailSheetLink').textContent = email || '(no email entered — will open Outlook compose)';
  document.getElementById('emailSheetLink').href = outlookHref;
  // Primary button tries Outlook; if Outlook not installed it falls back to mailto
  document.getElementById('emailSheetBtn').onclick = function(e) {
    e.preventDefault();
    // Try Outlook deep link first
    window.location.href = outlookHref;
    // After 1.5s, if nothing happened (Outlook not installed), fall back to mailto
    setTimeout(() => { window.location.href = fallbackHref; }, 1500);
  };
  openSheet('emailSheet');
}
function openWaSheet() {
  const phone = state.phone.replace(/[^0-9]/g,'');
  const msg = encodeURIComponent(buildMessage());
  const href = phone ? `https://wa.me/${phone}?text=${msg}` : `https://wa.me/?text=${msg}`;
  document.getElementById('waSheetLink').textContent = phone ? `wa.me/${phone}` : 'No number entered (will open WhatsApp without pre-filled contact)';
  document.getElementById('waSheetLink').href = href;
  document.getElementById('waSheetBtn').href = href;
  openSheet('waSheet');
}
function openSheet(id) {
  document.getElementById(id).classList.add('open');
}
function closeSheet(id) {
  document.getElementById(id).classList.remove('open');
}

// ─────────────────────────────────────
// PRINT → PDF → SHARPDESK
// ─────────────────────────────────────
function openPrintSheet() {
  if (!state.generated) { showError('Please generate a schedule first.'); return; }
  document.getElementById('printProgress').style.display = 'none';
  document.getElementById('printGenerateBtn').style.display = 'block';
  document.getElementById('printSheetSub').style.display = 'block';
  openSheet('printSheet');
}

function generateAndSharePDF() {
  document.getElementById('printGenerateBtn').style.display = 'none';
  document.getElementById('printSheetSub').style.display = 'none';
  document.getElementById('printProgress').style.display = 'block';

  // Build a clean print-friendly HTML page as a Blob, then open it
  // Safari on iOS: opening a blob URL and using window.print() triggers
  // the native iOS print/share sheet where SharpDesk Mobile appears
  const html = buildPrintHTML();
  const blob = new Blob([html], { type: 'text/html' });
  const url = URL.createObjectURL(blob);

  // Open in new tab — iOS Safari will show the print-ready page
  // User can then tap Share ⬆ → SharpDesk Mobile, OR use the print icon
  const win = window.open(url, '_blank');

  // Fallback: if popup blocked, create a download link instead
  setTimeout(() => {
    document.getElementById('printProgress').style.display = 'none';
    document.getElementById('printGenerateBtn').style.display = 'block';
    document.getElementById('printSheetSub').style.display = 'block';

    if (!win || win.closed) {
      // Popup was blocked — offer direct download
      const a = document.createElement('a');
      a.href = url;
      a.download = `prenatal_schedule_${state.firstName}_${state.lastName}.html`.replace(/\s/g,'_');
      a.click();
    }
    closeSheet('printSheet');
  }, 800);
}

function buildPrintHTML() {
  const { firstName, lastName, dob, lmp, edd, ga, rhesus } = state;
  const SCHEDULE_PRINT = SCHEDULE.filter(v => !(v.rhesusOnly && rhesus !== 'negative'));

  const trimNames = {1:'First Trimester', 2:'Second Trimester', 3:'Third Trimester'};
  let currentTrim = 0;
  let visitsHTML = '';

  SCHEDULE_PRINT.forEach(v => {
    if (v.trim !== currentTrim) {
      currentTrim = v.trim;
      if (visitsHTML) visitsHTML += '</div>';
      visitsHTML += `<div class="trim-section">
        <div class="trim-header">${trimNames[currentTrim]}</div>`;
    }
    const dateFrom = addWeeks(lmp, v.wFrom);
    const dateTo = v.wTo !== v.wFrom ? addWeeks(lmp, v.wTo) : null;
    const dateLabel = dateTo ? `${fmtShort(dateFrom)} – ${fmtShort(dateTo)}` : fmtShort(dateFrom);
    const weekLabel = v.wTo !== v.wFrom ? `Weeks ${v.wFrom}–${v.wTo}` : `Week ${v.wFrom}`;

    let testsHTML = v.tests.map(t =>
      `<div class="test-row">
        <div class="test-bullet"></div>
        <div><strong>${t.name}</strong><br/><span class="test-desc">${t.info}</span></div>
      </div>`
    ).join('');

    visitsHTML += `
      <div class="visit-block">
        <div class="visit-top-row">
          <div class="visit-head">${v.title}</div>
          <div class="visit-badge">${weekLabel} · ${dateLabel}</div>
        </div>
        <div class="tests">${testsHTML}</div>
        ${v.note ? `<div class="note">📌 ${v.note}</div>` : ''}
      </div>`;
  });
  visitsHTML += '</div>';

  const rhBanner = rhesus === 'negative'
    ? `<div class="rh-banner">⚠️ <strong>Rhesus Negative:</strong> Anti-D immunoglobulin injections are required at 28 weeks and after delivery. These are included in your schedule below and are mandatory for your safety.</div>`
    : '';

  return `<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Prenatal Schedule — ${firstName} ${lastName}</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600&family=Nunito:wght@400;500;600&display=swap');
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'Nunito', sans-serif; background: #fff; color: #1a1210; font-size: 13px; line-height: 1.5; }
  .page { max-width: 780px; margin: 0 auto; padding: 28px 24px; }

  .doc-header { display: flex; align-items: center; justify-content: space-between; border-bottom: 2px solid #c9806a; padding-bottom: 14px; margin-bottom: 18px; }
  .doc-header h1 { font-family: 'Playfair Display', serif; font-size: 22px; font-weight: 600; color: #a5604e; }
  .doc-header .clinic-label { font-size: 10px; color: #888; letter-spacing: 1px; text-transform: uppercase; margin-top: 2px; }
  .doc-header .logo { font-size: 32px; }

  .patient-bar { background: #faf3ef; border: 1px solid #e8d0c4; border-radius: 10px; padding: 12px 16px; margin-bottom: 14px; display: flex; flex-wrap: wrap; gap: 16px; }
  .patient-bar .pfield { flex: 1; min-width: 140px; }
  .patient-bar .pfield label { font-size: 9px; text-transform: uppercase; letter-spacing: 1px; color: #999; display: block; }
  .patient-bar .pfield span { font-size: 13px; font-weight: 600; color: #2c1a14; }
  .pfield .edd-val { color: #c9806a; font-size: 15px; }

  .ga-row { background: #2c1a14; color: white; border-radius: 10px; padding: 10px 16px; margin-bottom: 14px; display: flex; align-items: center; gap: 16px; }
  .ga-row .ga-weeks { font-size: 22px; font-weight: 700; color: #f4a98e; font-family: 'Playfair Display', serif; }
  .ga-row .ga-label { font-size: 10px; text-transform: uppercase; letter-spacing: 1px; color: #9e8070; }
  .ga-bar-outer { flex:1; background: rgba(255,255,255,0.12); border-radius: 99px; height: 6px; }
  .ga-bar-inner { height: 100%; border-radius: 99px; background: linear-gradient(90deg, #e8876a, #7ec8a8); }

  .rh-banner { background: #fff8e1; border: 1.5px solid #ffc107; border-radius: 8px; padding: 10px 14px; margin-bottom: 14px; font-size: 12px; color: #7a5a00; }

  .trim-header { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 2px; color: #999; margin: 18px 0 8px; padding-left: 4px; border-left: 3px solid #e8876a; padding: 4px 0 4px 10px; }

  .visit-block { border: 1px solid #e8d5c4; border-radius: 10px; margin-bottom: 10px; overflow: hidden; break-inside: avoid; }
  .visit-top-row { background: #faf3ef; padding: 10px 14px; display: flex; align-items: flex-start; justify-content: space-between; gap: 12px; border-bottom: 1px solid #e8d5c4; }
  .visit-head { font-family: 'Playfair Display', serif; font-size: 14px; font-weight: 600; color: #2c1a14; }
  .visit-badge { font-size: 10px; background: #fff; border: 1px solid #e8d5c4; border-radius: 6px; padding: 3px 8px; color: #7a6055; white-space: nowrap; flex-shrink: 0; }
  .tests { padding: 10px 14px; display: flex; flex-direction: column; gap: 7px; }
  .test-row { display: flex; gap: 8px; align-items: flex-start; }
  .test-bullet { width: 7px; height: 7px; background: #c9806a; border-radius: 50%; margin-top: 4px; flex-shrink: 0; }
  .test-desc { color: #7a6055; font-size: 11px; }
  .note { background: #faf3ef; border-left: 3px solid #c9806a; padding: 8px 12px; font-size: 11px; color: #7a6055; margin: 0 14px 10px; border-radius: 0 6px 6px 0; }

  .footer { text-align: center; margin-top: 24px; padding-top: 14px; border-top: 1px solid #e8d5c4; font-size: 10px; color: #aaa; }

  @media print {
    body { -webkit-print-color-adjust: exact; print-color-adjust: exact; }
    .visit-block { break-inside: avoid; }
    .no-print { display: none; }
  }
</style>
</head>
<body>
<div class="page">
  <div class="doc-header">
    <div>
      <h1>Prenatal Care Schedule</h1>
      <div class="clinic-label">Personalised Obstetric Plan</div>
    </div>
    <div class="logo">🌸</div>
  </div>

  <div class="patient-bar">
    <div class="pfield"><label>Patient Name</label><span>${firstName} ${lastName}</span></div>
    ${dob ? `<div class="pfield"><label>Date of Birth</label><span>${fmtShort(new Date(dob))}</span></div>` : ''}
    <div class="pfield"><label>Last Menstrual Period</label><span>${fmtShort(lmp)}</span></div>
    <div class="pfield"><label>Estimated Due Date</label><span class="edd-val">${fmtShort(edd)}</span></div>
    <div class="pfield"><label>Rhesus</label><span>${rhesus==='positive'?'Rh Positive (+)':rhesus==='negative'?'Rh Negative (−)':'Unknown'}</span></div>
  </div>

  <div class="ga-row">
    <div><div class="ga-label">Gestational Age Today</div><div class="ga-weeks">${ga.weeks} wks ${ga.days} days</div></div>
    <div class="ga-bar-outer"><div class="ga-bar-inner" style="width:${Math.min(100,(ga.total/280)*100).toFixed(1)}%"></div></div>
    <div style="font-size:11px;color:#9e8070;white-space:nowrap;">${Math.max(0,Math.floor((edd-new Date())/86400000))} days to EDD</div>
  </div>

  ${rhBanner}
  ${visitsHTML}

  <div class="footer">Generated by OB Care Planner · ${new Date().toLocaleDateString('en-GB',{day:'2-digit',month:'long',year:'numeric'})}</div>
</div>
<script>
  // Auto-trigger print dialog so user can share to SharpDesk Mobile immediately
  window.onload = function() { setTimeout(function(){ window.print(); }, 600); };
<\/script>
</body>
</html>`;
}


// ─────────────────────────────────────
// DATE PICKER ENGINE
// ─────────────────────────────────────
const MONTHS = ['January','February','March','April','May','June',
                'July','August','September','October','November','December'];

const pickerValues = { dob: null, lmp: null };
let pickerTarget = 'dob';
let pickerTempDay = 1, pickerTempMonth = 0, pickerTempYear = 2000;
let scrollTimers = {};

function daysInMonth(month, year) {
  return new Date(year, month + 1, 0).getDate();
}

function openDatePicker(field) {
  pickerTarget = field;
  document.getElementById('pickerTitle').textContent =
    field === 'dob' ? 'Date of Birth' : 'Last Menstrual Period';

  const existing = pickerValues[field];
  const now = new Date();
  if (existing) {
    pickerTempDay   = existing.getDate();
    pickerTempMonth = existing.getMonth();
    pickerTempYear  = existing.getFullYear();
  } else if (field === 'dob') {
    pickerTempDay = 1; pickerTempMonth = 0;
    pickerTempYear = now.getFullYear() - 28;
  } else {
    const lmpDefault = new Date(now.getTime() - 56 * 86400000);
    pickerTempDay   = lmpDefault.getDate();
    pickerTempMonth = lmpDefault.getMonth();
    pickerTempYear  = lmpDefault.getFullYear();
  }

  buildPickerColumns();
  document.getElementById('datePickerOverlay').classList.add('open');

  requestAnimationFrame(() => {
    setTimeout(() => {
      scrollPickerTo('pickerDay',   pickerTempDay - 1);
      scrollPickerTo('pickerMonth', pickerTempMonth);
      const yearIdx = getYearItems().indexOf(pickerTempYear);
      scrollPickerTo('pickerYear', yearIdx < 0 ? 0 : yearIdx);
    }, 60);
  });
}

function getYearItems() {
  const now = new Date().getFullYear();
  if (pickerTarget === 'dob') {
    return Array.from({length: now - 1929}, (_, i) => now - i);
  } else {
    return Array.from({length: now - 2018}, (_, i) => now - i);
  }
}

function buildPickerColumns() {
  // Days 1–31
  const dayCol = document.getElementById('pickerDay');
  dayCol.innerHTML = '';
  for (let d = 1; d <= 31; d++) {
    const el = document.createElement('div');
    el.className = 'picker-item' + (d === pickerTempDay ? ' selected' : '');
    el.textContent = String(d).padStart(2,'0');
    el.dataset.val = d;
    dayCol.appendChild(el);
  }

  // Months
  const monCol = document.getElementById('pickerMonth');
  monCol.innerHTML = '';
  MONTHS.forEach((m, i) => {
    const el = document.createElement('div');
    el.className = 'picker-item' + (i === pickerTempMonth ? ' selected' : '');
    el.textContent = m;
    el.dataset.val = i;
    monCol.appendChild(el);
  });

  // Years
  const yearItems = getYearItems();
  const yrCol = document.getElementById('pickerYear');
  yrCol.innerHTML = '';
  yearItems.forEach(y => {
    const el = document.createElement('div');
    el.className = 'picker-item' + (y === pickerTempYear ? ' selected' : '');
    el.textContent = y;
    el.dataset.val = y;
    yrCol.appendChild(el);
  });

  attachScrollListener('pickerDay',   'day');
  attachScrollListener('pickerMonth', 'month');
  attachScrollListener('pickerYear',  'year');
}

function scrollPickerTo(colId, index) {
  const col = document.getElementById(colId);
  if (!col || index < 0) return;
  col.scrollTop = index * 44;
}

function attachScrollListener(colId, type) {
  const col = document.getElementById(colId);
  if (!col) return;
  col.onscroll = function() {
    clearTimeout(scrollTimers[colId]);
    scrollTimers[colId] = setTimeout(() => snapAndRead(col, type), 100);
  };
}

function snapAndRead(col, type) {
  const index = Math.round(col.scrollTop / 44);
  col.scrollTop = index * 44;
  const items = col.querySelectorAll('.picker-item');
  items.forEach(el => el.classList.remove('selected'));
  if (items[index]) {
    items[index].classList.add('selected');
    const val = parseInt(items[index].dataset.val);
    if (type === 'day')   { pickerTempDay   = val; }
    if (type === 'month') { pickerTempMonth = val; rebuildDays(); }
    if (type === 'year')  { pickerTempYear  = val; rebuildDays(); }
  }
}

function rebuildDays() {
  const maxDay = daysInMonth(pickerTempMonth, pickerTempYear);
  if (pickerTempDay > maxDay) pickerTempDay = maxDay;
  const dayCol = document.getElementById('pickerDay');
  dayCol.innerHTML = '';
  for (let d = 1; d <= 31; d++) {
    const el = document.createElement('div');
    el.className = 'picker-item' + (d === pickerTempDay ? ' selected' : '');
    el.textContent = String(d).padStart(2,'0');
    el.dataset.val = d;
    dayCol.appendChild(el);
  }
  dayCol.scrollTop = (pickerTempDay - 1) * 44;
  attachScrollListener('pickerDay', 'day');
}

function confirmDatePicker() {
  const maxDay = daysInMonth(pickerTempMonth, pickerTempYear);
  const safeDay = Math.min(pickerTempDay, maxDay);
  const date = new Date(pickerTempYear, pickerTempMonth, safeDay);
  pickerValues[pickerTarget] = date;
  const displayId = pickerTarget === 'dob' ? 'fDobDisplay' : 'fLmpDisplay';
  const el = document.getElementById(displayId);
  el.textContent = fmt(date);
  el.style.color = 'var(--text)';
  document.getElementById('datePickerOverlay').classList.remove('open');
}

function cancelDatePicker() {
  document.getElementById('datePickerOverlay').classList.remove('open');
}

document.querySelectorAll('.scroll-area').forEach(el => {
  el.addEventListener('touchstart', e => {}, { passive: true });
});
</script>
<!-- BOTTOM SHEET: PRINT → SHARPDESK -->
<div class="sheet-overlay" id="printSheet" onclick="closeSheet('printSheet')">
  <div class="bottom-sheet" onclick="event.stopPropagation()">
    <div class="sheet-handle"></div>
    <div class="sheet-title">🖨️ Print via SharpDesk</div>
    <div class="sheet-sub" id="printSheetSub">Tap below to generate the patient schedule as a PDF. iOS will show the Share Sheet — choose <strong style="color:var(--gold)">SharpDesk Mobile</strong> from the list to send it to your Sharp printer.</div>
    <div id="printProgress" style="display:none;text-align:center;padding:16px 0;">
      <div style="font-size:28px;margin-bottom:8px;">⏳</div>
      <div style="font-size:13px;color:var(--text2);">Building PDF…</div>
    </div>
    <button id="printGenerateBtn" class="sheet-btn" style="background:var(--gold-muted);border:1.5px solid rgba(212,168,85,0.4);color:var(--gold);font-family:inherit;cursor:pointer;" onclick="generateAndSharePDF()">
      Generate PDF &amp; Open Share Sheet
    </button>
    <button class="sheet-btn sheet-btn-secondary" onclick="closeSheet('printSheet')">Cancel</button>
  </div>
</div>

</body>
</html>
