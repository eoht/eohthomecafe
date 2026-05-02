<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Eunice Home Café</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --cream: #F5EDD8;
    --caramel: #C17F3A;
    --gold: #D4A853;
    --matcha: #7A9E5F;
    --midnight: #160F06;
    --surface: #1E1509;
    --surface2: #261B0A;
    --border: rgba(212,168,83,0.15);
    --text-dim: rgba(245,237,216,0.4);
    --text-mid: rgba(245,237,216,0.65);
  }
  * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
  html, body {
    height: 100%;
    background: var(--midnight);
    font-family: 'DM Sans', sans-serif;
    color: var(--cream);
    overflow-x: hidden;
  }
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 70% 40% at 15% 5%, rgba(193,127,58,0.2) 0%, transparent 55%),
      radial-gradient(ellipse 50% 35% at 85% 90%, rgba(122,158,95,0.1) 0%, transparent 50%);
    pointer-events: none;
    z-index: 0;
  }
  .app {
    position: relative;
    z-index: 1;
    max-width: 430px;
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    padding-bottom: 40px;
  }
  .header { padding: 52px 24px 20px; text-align: center; }
  .logo-mark { display: flex; align-items: center; justify-content: center; gap: 10px; margin-bottom: 14px; }
  .logo-line { flex: 1; height: 1px; background: var(--border); }
  .logo-icon { width: 36px; height: 36px; background: rgba(212,168,83,0.12); border: 1px solid var(--border); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 16px; }
  .header h1 { font-family: 'Cormorant Garamond', serif; font-size: 42px; font-weight: 700; color: var(--cream); line-height: 1; margin-bottom: 4px; }
  .header h1 span { font-style: italic; color: var(--gold); }
  .header-sub { font-size: 11px; font-weight: 400; letter-spacing: 2.5px; text-transform: uppercase; color: var(--text-dim); margin-top: 8px; }
  .steps-wrap { padding: 0 16px; display: flex; flex-direction: column; gap: 12px; }
  .step-card { background: var(--surface); border: 1px solid rgba(245,237,216,0.07); border-radius: 20px; overflow: hidden; transition: border-color 0.3s; }
  .step-card.active { border-color: rgba(212,168,83,0.3); }
  .step-card.done { border-color: rgba(122,158,95,0.25); }
  .step-header { display: flex; align-items: center; gap: 12px; padding: 16px 18px; cursor: pointer; user-select: none; }
  .step-num { width: 26px; height: 26px; border-radius: 50%; border: 1.5px solid var(--border); display: flex; align-items: center; justify-content: center; font-size: 11px; font-weight: 600; color: var(--text-dim); flex-shrink: 0; transition: all 0.3s; }
  .step-card.active .step-num { background: var(--gold); border-color: var(--gold); color: var(--midnight); }
  .step-card.done .step-num { background: var(--matcha); border-color: var(--matcha); color: white; font-size: 13px; }
  .step-card.done .step-num::before { content: '✓'; }
  .step-title-wrap { flex: 1; }
  .step-title { font-size: 14px; font-weight: 600; color: var(--cream); }
  .step-card.done .step-title { color: var(--text-mid); }
  .step-summary { font-size: 11px; color: var(--gold); margin-top: 2px; display: none; }
  .step-card.done .step-summary { display: block; }
  .step-chevron { color: var(--text-dim); font-size: 12px; transition: transform 0.3s; }
  .step-card.active .step-chevron { transform: rotate(180deg); color: var(--gold); }
  .step-body { display: none; padding: 0 18px 18px; animation: slideDown 0.25s ease; }
  .step-card.active .step-body { display: block; }
  @keyframes slideDown { from { opacity: 0; transform: translateY(-8px); } to { opacity: 1; transform: translateY(0); } }
  .option-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  .option-grid.three { grid-template-columns: 1fr 1fr 1fr; }
  .opt-btn { padding: 14px 10px; border-radius: 14px; border: 1.5px solid rgba(245,237,216,0.1); background: rgba(245,237,216,0.03); color: var(--text-mid); font-family: 'DM Sans', sans-serif; font-size: 12px; font-weight: 500; cursor: pointer; text-align: center; transition: all 0.2s; display: flex; flex-direction: column; align-items: center; gap: 7px; line-height: 1.3; }
  .opt-btn .opt-icon { font-size: 22px; }
  .opt-btn:active { transform: scale(0.97); }
  .opt-btn.selected { border-color: var(--gold); background: rgba(212,168,83,0.1); color: var(--gold); }
  .opt-btn.full { grid-column: 1 / -1; flex-direction: row; gap: 12px; padding: 13px 16px; }
  .opt-btn.full .opt-icon { font-size: 18px; }
  .ingr-section { display: flex; flex-direction: column; gap: 12px; }
  .selected-ingr-wrap { background: rgba(245,237,216,0.03); border: 1px dashed rgba(245,237,216,0.12); border-radius: 14px; padding: 12px 14px; min-height: 50px; }
  .selected-ingr-label { font-size: 10px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--text-dim); margin-bottom: 8px; }
  .selected-tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .sel-tag { display: flex; align-items: center; gap: 5px; padding: 5px 10px; background: rgba(212,168,83,0.15); border-radius: 10px; font-size: 12px; color: var(--gold); }
  .sel-tag button { background: none; border: none; color: rgba(212,168,83,0.6); font-size: 14px; line-height: 1; cursor: pointer; padding: 0; }
  .no-ingr { font-size: 12px; color: var(--text-dim); font-style: italic; }
  .ingr-tabs { display: flex; gap: 6px; overflow-x: auto; -ms-overflow-style: none; scrollbar-width: none; padding-bottom: 2px; }
  .ingr-tabs::-webkit-scrollbar { display: none; }
  .ingr-tab { flex-shrink: 0; padding: 6px 14px; border-radius: 20px; border: 1px solid rgba(245,237,216,0.1); background: transparent; color: var(--text-dim); font-size: 11px; font-weight: 500; cursor: pointer; transition: all 0.2s; white-space: nowrap; }
  .ingr-tab.active { background: rgba(212,168,83,0.12); border-color: var(--gold); color: var(--gold); }
  .ingr-chips { display: flex; flex-wrap: wrap; gap: 7px; min-height: 40px; }
  .ingr-chip { padding: 8px 14px; border-radius: 20px; border: 1.5px solid rgba(245,237,216,0.1); background: rgba(245,237,216,0.04); color: var(--text-mid); font-size: 12px; cursor: pointer; transition: all 0.2s; }
  .ingr-chip.picked { border-color: var(--gold); background: rgba(212,168,83,0.12); color: var(--gold); }
  .ingr-chip.picked::after { content: ' ✓'; font-size: 11px; }
  .custom-ingr-row { display: flex; gap: 8px; align-items: center; }
  .custom-ingr-input { flex: 1; padding: 10px 14px; background: rgba(245,237,216,0.05); border: 1.5px solid rgba(245,237,216,0.1); border-radius: 12px; font-family: 'DM Sans', sans-serif; font-size: 13px; color: var(--cream); outline: none; }
  .custom-ingr-input::placeholder { color: var(--text-dim); }
  .add-ingr-btn { padding: 10px 16px; border-radius: 12px; border: none; background: rgba(212,168,83,0.15); color: var(--gold); font-size: 13px; font-weight: 600; cursor: pointer; white-space: nowrap; }
  .next-btn { width: 100%; margin-top: 14px; padding: 14px; border-radius: 14px; border: none; background: linear-gradient(135deg, var(--caramel), var(--gold)); color: var(--midnight); font-family: 'DM Sans', sans-serif; font-size: 14px; font-weight: 600; cursor: pointer; transition: all 0.25s; }
  .next-btn:disabled { opacity: 0.4; cursor: not-allowed; }
  .generate-btn { margin: 16px 16px 0; padding: 20px; border-radius: 20px; border: none; background: linear-gradient(135deg, var(--caramel) 0%, var(--gold) 100%); color: var(--midnight); font-family: 'Cormorant Garamond', serif; font-size: 20px; font-weight: 700; cursor: pointer; transition: all 0.3s; overflow: hidden; letter-spacing: 0.3px; }
  .generate-btn:hover { transform: translateY(-2px); box-shadow: 0 10px 36px rgba(193,127,58,0.35); }
  .generate-btn:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }
  .results-section { margin: 20px 16px 0; display: none; animation: fadeUp 0.5s ease; }
  .results-section.visible { display: block; }
  @keyframes fadeUp { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: translateY(0); } }
  .results-label { display: flex; justify-content: space-between; align-items: baseline​​​​​​​​​​​​​​​​
