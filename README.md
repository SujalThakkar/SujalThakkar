<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Sujal Thakkar — Developer Profile</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=JetBrains+Mono:wght@300;400;700&display=swap" rel="stylesheet"/>
<style>
  /* ═══════════════════ RESET & VARIABLES ═══════════════════ */
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg:        #04010f;
    --bg2:       #080520;
    --surface:   #0d0a26;
    --border:    #1e1a45;
    --accent:    #8b5cf6;
    --accent2:   #a78bfa;
    --accent3:   #c4b5fd;
    --neon:      #7c3aed;
    --gold:      #fbbf24;
    --green:     #10b981;
    --red:       #ef4444;
    --text:      #e2e8f0;
    --muted:     #64748b;
    --font-sans: 'Syne', sans-serif;
    --font-mono: 'JetBrains Mono', monospace;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-sans);
    overflow-x: hidden;
    cursor: none;
  }

  /* ═══════════════════ CUSTOM CURSOR ═══════════════════ */
  #cursor {
    position: fixed; width: 12px; height: 12px;
    background: var(--accent); border-radius: 50%;
    pointer-events: none; z-index: 99999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, background 0.2s;
    mix-blend-mode: screen;
  }
  #cursor-ring {
    position: fixed; width: 36px; height: 36px;
    border: 1px solid var(--accent2); border-radius: 50%;
    pointer-events: none; z-index: 99998;
    transform: translate(-50%, -50%);
    transition: all 0.15s ease;
    opacity: 0.5;
  }

  /* ═══════════════════ CANVAS BACKGROUND ═══════════════════ */
  #bg-canvas {
    position: fixed; inset: 0;
    z-index: 0; pointer-events: none;
  }

  /* ═══════════════════ LAYOUT ═══════════════════ */
  .container { max-width: 1100px; margin: 0 auto; padding: 0 2rem; position: relative; z-index: 1; }

  section { padding: 6rem 0; }

  /* ═══════════════════ HERO ═══════════════════ */
  #hero {
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    flex-direction: column; text-align: center;
    padding: 2rem;
    position: relative;
  }

  .hero-eyebrow {
    font-family: var(--font-mono);
    font-size: 0.75rem; letter-spacing: 0.3em;
    color: var(--accent2); text-transform: uppercase;
    margin-bottom: 1.5rem;
    opacity: 0; animation: fadeUp 0.8s 0.2s forwards;
  }

  .hero-name {
    font-size: clamp(3.5rem, 9vw, 8rem);
    font-weight: 800; line-height: 0.95;
    letter-spacing: -0.02em;
    background: linear-gradient(135deg, #fff 0%, var(--accent3) 50%, var(--accent) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    opacity: 0; animation: fadeUp 0.8s 0.4s forwards;
    position: relative;
  }

  .hero-name .glitch-layer {
    position: absolute; top: 0; left: 0; width: 100%;
    background: linear-gradient(135deg, var(--accent) 0%, #06b6d4 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: glitch 4s infinite;
    clip-path: polygon(0 0, 100% 0, 100% 0, 0 0);
  }

  @keyframes glitch {
    0%,94%,100% { clip-path: polygon(0 0,100% 0,100% 0,0 0); transform: translate(0); }
    95% { clip-path: polygon(0 30%,100% 30%,100% 50%,0 50%); transform: translate(-3px,2px); }
    96% { clip-path: polygon(0 60%,100% 60%,100% 75%,0 75%); transform: translate(3px,-2px); }
    97% { clip-path: polygon(0 15%,100% 15%,100% 25%,0 25%); transform: translate(-2px,1px); }
    98% { clip-path: polygon(0 0,100% 0,100% 0,0 0); transform: translate(0); }
  }

  .hero-title {
    font-family: var(--font-mono);
    font-size: clamp(0.85rem, 2vw, 1.1rem);
    color: var(--muted); margin-top: 1.2rem;
    opacity: 0; animation: fadeUp 0.8s 0.6s forwards;
    letter-spacing: 0.05em;
  }
  .hero-title span { color: var(--accent2); }

  .hero-badge-row {
    display: flex; gap: 0.75rem; flex-wrap: wrap;
    justify-content: center; margin-top: 2.5rem;
    opacity: 0; animation: fadeUp 0.8s 0.8s forwards;
  }

  .badge {
    font-family: var(--font-mono); font-size: 0.72rem;
    padding: 0.4rem 1rem; border-radius: 999px;
    border: 1px solid var(--border);
    background: rgba(139,92,246,0.08);
    color: var(--accent3); letter-spacing: 0.05em;
    transition: all 0.3s; cursor: default;
  }
  .badge:hover {
    background: rgba(139,92,246,0.2);
    border-color: var(--accent);
    transform: translateY(-2px);
    box-shadow: 0 0 20px rgba(139,92,246,0.3);
  }
  .badge.gold { color: var(--gold); border-color: rgba(251,191,36,0.3); background: rgba(251,191,36,0.06); }
  .badge.green { color: var(--green); border-color: rgba(16,185,129,0.3); background: rgba(16,185,129,0.06); }

  .scroll-hint {
    position: absolute; bottom: 2.5rem; left: 50%;
    transform: translateX(-50%);
    font-family: var(--font-mono); font-size: 0.7rem;
    color: var(--muted); letter-spacing: 0.2em;
    animation: bounce 2s infinite;
    opacity: 0; animation: fadeIn 1s 2s forwards, bounce 2s 3s infinite;
  }

  @keyframes bounce {
    0%,100% { transform: translateX(-50%) translateY(0); }
    50% { transform: translateX(-50%) translateY(8px); }
  }
  @keyframes fadeUp { from { opacity:0; transform: translateY(24px); } to { opacity:1; transform: translateY(0); } }
  @keyframes fadeIn { from { opacity:0; } to { opacity:1; } }

  /* ═══════════════════ SECTION TITLES ═══════════════════ */
  .section-label {
    font-family: var(--font-mono); font-size: 0.7rem;
    color: var(--accent); letter-spacing: 0.3em;
    text-transform: uppercase; margin-bottom: 0.75rem;
  }
  .section-title {
    font-size: clamp(2rem, 5vw, 3rem); font-weight: 800;
    line-height: 1.1; margin-bottom: 3rem;
    background: linear-gradient(135deg, #fff 30%, var(--accent3) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  /* ═══════════════════ GAME SECTION ═══════════════════ */
  #game-section { padding: 4rem 0; }

  .game-wrapper {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
    position: relative;
    box-shadow: 0 0 60px rgba(139,92,246,0.1);
  }

  .game-header {
    display: flex; align-items: center; justify-content: space-between;
    padding: 1rem 1.5rem;
    border-bottom: 1px solid var(--border);
    background: rgba(0,0,0,0.3);
  }
  .game-header-left { display: flex; align-items: center; gap: 0.75rem; }
  .game-dot { width: 12px; height: 12px; border-radius: 50%; }
  .game-dot.r { background: #ef4444; }
  .game-dot.y { background: #fbbf24; }
  .game-dot.g { background: #10b981; }
  .game-title-bar {
    font-family: var(--font-mono); font-size: 0.8rem;
    color: var(--muted);
  }
  .game-controls-hint {
    font-family: var(--font-mono); font-size: 0.72rem;
    color: var(--muted);
  }

  .game-stats-bar {
    display: flex; gap: 2rem; padding: 0.75rem 1.5rem;
    border-bottom: 1px solid var(--border);
    background: rgba(0,0,0,0.2);
    font-family: var(--font-mono); font-size: 0.8rem;
  }
  .game-stat { display: flex; flex-direction: column; gap: 0.2rem; }
  .game-stat-label { color: var(--muted); font-size: 0.65rem; letter-spacing: 0.1em; }
  .game-stat-value { color: var(--accent2); font-weight: 700; }

  #game-canvas-wrap {
    position: relative; display: flex;
    justify-content: center; align-items: center;
    background: #03010a;
    padding: 1.5rem;
  }

  #gameCanvas {
    border-radius: 8px;
    border: 1px solid var(--border);
    display: block;
    image-rendering: pixelated;
  }

  #game-overlay {
    position: absolute; inset: 0;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    background: rgba(4,1,15,0.85);
    backdrop-filter: blur(4px);
    border-radius: 8px;
    z-index: 10;
  }

  .overlay-title {
    font-size: 2rem; font-weight: 800;
    background: linear-gradient(135deg, #fff, var(--accent3));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 0.5rem;
  }
  .overlay-sub {
    font-family: var(--font-mono); font-size: 0.8rem;
    color: var(--muted); margin-bottom: 2rem; text-align: center;
    line-height: 1.8;
  }

  .btn-primary {
    font-family: var(--font-mono); font-size: 0.85rem;
    padding: 0.75rem 2rem; border-radius: 8px;
    background: linear-gradient(135deg, var(--neon), var(--accent2));
    color: white; border: none; cursor: pointer;
    font-weight: 700; letter-spacing: 0.05em;
    transition: all 0.3s;
    box-shadow: 0 0 30px rgba(124,58,237,0.4);
  }
  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 50px rgba(124,58,237,0.6);
  }

  /* ═══════════════════ SKILL BARS ═══════════════════ */
  #skills { padding: 5rem 0; }

  .skills-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 2.5rem; }
  @media (max-width: 700px) { .skills-grid { grid-template-columns: 1fr; } }

  .skill-item { margin-bottom: 1.5rem; }
  .skill-header { display: flex; justify-content: space-between; margin-bottom: 0.5rem; }
  .skill-name { font-family: var(--font-mono); font-size: 0.85rem; color: var(--text); }
  .skill-pct  { font-family: var(--font-mono); font-size: 0.8rem; color: var(--accent2); font-weight: 700; }

  .skill-track {
    height: 6px; background: var(--border); border-radius: 999px;
    overflow: visible; position: relative;
  }
  .skill-bar {
    height: 100%; border-radius: 999px;
    background: linear-gradient(90deg, var(--neon), var(--accent2));
    width: 0; transition: width 1.4s cubic-bezier(0.16,1,0.3,1);
    position: relative;
  }
  .skill-bar::after {
    content: '';
    position: absolute; right: -1px; top: 50%;
    transform: translateY(-50%);
    width: 10px; height: 10px; border-radius: 50%;
    background: var(--accent2);
    box-shadow: 0 0 10px var(--accent2);
  }
  .skill-bar.green-bar { background: linear-gradient(90deg, #065f46, var(--green)); }
  .skill-bar.green-bar::after { background: var(--green); box-shadow: 0 0 10px var(--green); }
  .skill-bar.gold-bar { background: linear-gradient(90deg, #78350f, var(--gold)); }
  .skill-bar.gold-bar::after { background: var(--gold); box-shadow: 0 0 10px var(--gold); }

  /* ═══════════════════ PROJECTS ═══════════════════ */
  #projects { padding: 5rem 0; }

  .projects-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
  @media (max-width: 700px) { .projects-grid { grid-template-columns: 1fr; } }

  .project-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 14px; padding: 2rem;
    position: relative; overflow: hidden;
    cursor: pointer; transition: all 0.4s cubic-bezier(0.16,1,0.3,1);
    group: true;
  }
  .project-card::before {
    content: ''; position: absolute; inset: 0;
    background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(139,92,246,0.08) 0%, transparent 60%);
    opacity: 0; transition: opacity 0.3s;
    pointer-events: none;
  }
  .project-card:hover::before { opacity: 1; }
  .project-card:hover {
    transform: translateY(-6px);
    border-color: var(--accent);
    box-shadow: 0 20px 60px rgba(139,92,246,0.2), 0 0 0 1px rgba(139,92,246,0.1);
  }
  .project-card.featured { grid-column: span 2; }
  @media (max-width: 700px) { .project-card.featured { grid-column: span 1; } }

  .card-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 1.25rem; }
  .card-icon { font-size: 2rem; }
  .card-badge {
    font-family: var(--font-mono); font-size: 0.65rem;
    padding: 0.3rem 0.75rem; border-radius: 999px;
    background: rgba(251,191,36,0.1); color: var(--gold);
    border: 1px solid rgba(251,191,36,0.3);
  }
  .card-badge.new { background: rgba(16,185,129,0.1); color: var(--green); border-color: rgba(16,185,129,0.3); }

  .card-title { font-size: 1.3rem; font-weight: 800; margin-bottom: 0.5rem; }
  .card-desc { font-size: 0.9rem; color: var(--muted); line-height: 1.7; margin-bottom: 1.5rem; }

  .card-metrics { display: flex; gap: 1.5rem; margin-bottom: 1.5rem; }
  .metric { font-family: var(--font-mono); }
  .metric-val { font-size: 1.1rem; font-weight: 700; color: var(--accent2); }
  .metric-lbl { font-size: 0.65rem; color: var(--muted); margin-top: 0.1rem; letter-spacing: 0.05em; }

  .card-tags { display: flex; flex-wrap: wrap; gap: 0.5rem; }
  .tag {
    font-family: var(--font-mono); font-size: 0.7rem;
    padding: 0.25rem 0.6rem; border-radius: 6px;
    background: rgba(139,92,246,0.08); color: var(--accent3);
    border: 1px solid rgba(139,92,246,0.15);
  }

  /* ═══════════════════ STATS ═══════════════════ */
  #stats { padding: 5rem 0; }

  .stats-row { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1.5rem; }
  @media (max-width: 700px) { .stats-row { grid-template-columns: repeat(2, 1fr); } }

  .stat-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 12px; padding: 1.75rem;
    text-align: center;
    transition: all 0.3s;
  }
  .stat-card:hover {
    border-color: var(--accent);
    transform: translateY(-4px);
    box-shadow: 0 12px 40px rgba(139,92,246,0.15);
  }
  .stat-number {
    font-size: 2.5rem; font-weight: 800; display: block;
    background: linear-gradient(135deg, #fff, var(--accent3));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .stat-label { font-family: var(--font-mono); font-size: 0.7rem; color: var(--muted); margin-top: 0.4rem; letter-spacing: 0.1em; }

  /* ═══════════════════ GITHUB CARDS ═══════════════════ */
  #github { padding: 5rem 0; }
  .gh-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
  @media (max-width: 700px) { .gh-grid { grid-template-columns: 1fr; } }
  .gh-grid img { width: 100%; border-radius: 12px; display: block; }
  .gh-full { grid-column: span 2; }
  @media (max-width: 700px) { .gh-full { grid-column: span 1; } }

  /* ═══════════════════ CONNECT ═══════════════════ */
  #connect { padding: 5rem 0 8rem; text-align: center; }

  .connect-links { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; margin-top: 2rem; }
  .connect-link {
    display: flex; align-items: center; gap: 0.6rem;
    font-family: var(--font-mono); font-size: 0.85rem;
    padding: 0.8rem 1.75rem; border-radius: 10px;
    background: var(--surface); border: 1px solid var(--border);
    color: var(--text); text-decoration: none;
    transition: all 0.3s;
  }
  .connect-link:hover {
    border-color: var(--accent);
    background: rgba(139,92,246,0.1);
    transform: translateY(-3px);
    box-shadow: 0 8px 30px rgba(139,92,246,0.2);
  }

  /* ═══════════════════ NAV ═══════════════════ */
  nav {
    position: fixed; top: 1.5rem; left: 50%; transform: translateX(-50%);
    z-index: 100;
    background: rgba(4,1,15,0.8); backdrop-filter: blur(16px);
    border: 1px solid var(--border); border-radius: 999px;
    padding: 0.5rem 1.5rem;
    display: flex; gap: 2rem; align-items: center;
  }
  nav a {
    font-family: var(--font-mono); font-size: 0.72rem;
    color: var(--muted); text-decoration: none; letter-spacing: 0.05em;
    transition: color 0.2s;
  }
  nav a:hover { color: var(--accent2); }

  /* ═══════════════════ PARTICLE EFFECTS ═══════════════════ */
  .particle-burst {
    position: fixed; pointer-events: none; z-index: 9999;
  }

  /* ═══════════════════ FOOTER ═══════════════════ */
  footer {
    border-top: 1px solid var(--border);
    padding: 2rem; text-align: center;
    font-family: var(--font-mono); font-size: 0.72rem;
    color: var(--muted);
    position: relative; z-index: 1;
  }

  /* ═══════════════════ ACHIEVEMENTS TOAST ═══════════════════ */
  #toast {
    position: fixed; bottom: 2rem; right: 2rem;
    background: var(--surface); border: 1px solid var(--accent);
    border-radius: 12px; padding: 1rem 1.5rem;
    font-family: var(--font-mono); font-size: 0.8rem;
    color: var(--text); z-index: 9999;
    transform: translateY(120%); opacity: 0;
    transition: all 0.4s cubic-bezier(0.16,1,0.3,1);
    box-shadow: 0 8px 30px rgba(139,92,246,0.3);
    max-width: 280px;
  }
  #toast.show { transform: translateY(0); opacity: 1; }
  #toast-icon { font-size: 1.2rem; margin-bottom: 0.3rem; display: block; }
  #toast-title { color: var(--accent2); font-weight: 700; margin-bottom: 0.2rem; }

  /* ═══════════════════ XP BAR ═══════════════════ */
  #xp-bar-wrap {
    position: fixed; top: 0; left: 0; right: 0;
    height: 3px; z-index: 9999;
    background: rgba(255,255,255,0.03);
  }
  #xp-bar {
    height: 100%;
    background: linear-gradient(90deg, var(--neon), var(--accent2), #06b6d4);
    width: 0; transition: width 0.8s cubic-bezier(0.16,1,0.3,1);
    box-shadow: 0 0 12px var(--accent2);
  }
  #xp-label {
    position: fixed; top: 8px; right: 1rem;
    font-family: var(--font-mono); font-size: 0.65rem;
    color: var(--accent2); z-index: 9999;
    opacity: 0; transition: opacity 0.3s;
  }

  /* ═══════════════════ CODE BLOCK ═══════════════════ */
  .code-block {
    background: rgba(0,0,0,0.4); border: 1px solid var(--border);
    border-radius: 12px; overflow: hidden;
    font-family: var(--font-mono);
  }
  .code-header {
    padding: 0.75rem 1.25rem; border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 0.5rem;
    background: rgba(255,255,255,0.02);
  }
  .code-dot { width: 10px; height: 10px; border-radius: 50%; }
  .code-body { padding: 1.5rem; font-size: 0.85rem; line-height: 2; overflow-x: auto; }
  .kw { color: #c084fc; }
  .str { color: #86efac; }
  .num { color: #fbbf24; }
  .fn  { color: #60a5fa; }
  .cm  { color: var(--muted); }
  .prop { color: var(--accent3); }

  /* animated cursor in code */
  .cursor-blink {
    display: inline-block; width: 2px; height: 1em;
    background: var(--accent2); vertical-align: middle;
    animation: blink 1s step-end infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* ═══════════════════ DIVIDER ═══════════════════ */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border), transparent);
    margin: 0;
  }
</style>
</head>
<body>

<!-- XP BAR -->
<div id="xp-bar-wrap"><div id="xp-bar"></div></div>
<div id="xp-label">XP: <span id="xp-val">0</span></div>

<!-- CURSOR -->
<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- CANVAS BACKGROUND (stars + grid) -->
<canvas id="bg-canvas"></canvas>

<!-- TOAST -->
<div id="toast">
  <span id="toast-icon">🏆</span>
  <div id="toast-title">Achievement Unlocked!</div>
  <div id="toast-body">You discovered the profile</div>
</div>

<!-- NAV -->
<nav>
  <a href="#hero">HOME</a>
  <a href="#game-section">GAME</a>
  <a href="#skills">SKILLS</a>
  <a href="#projects">PROJECTS</a>
  <a href="#stats">STATS</a>
  <a href="#connect">CONNECT</a>
</nav>

<!-- ══════════════════════════ HERO ══════════════════════════ -->
<section id="hero">
  <div class="hero-eyebrow">◈ &nbsp;Full-Stack Engineer &nbsp;·&nbsp; Hackathon Champion &nbsp;·&nbsp; Systems Builder &nbsp;◈</div>
  <h1 class="hero-name">
    SUJAL<br/>THAKKAR
    <span class="glitch-layer" aria-hidden="true">SUJAL<br/>THAKKAR</span>
  </h1>
  <p class="hero-title">
    <span>B.Tech CS</span> @ K.J. Somaiya &nbsp;·&nbsp;
    <span>CGPA 9.27</span> &nbsp;·&nbsp;
    <span>Thane, Maharashtra 🇮🇳</span>
  </p>
  <div class="hero-badge-row">
    <span class="badge gold">🏆 1ST PLACE — PERISCOPE HACKATHON</span>
    <span class="badge green">🟢 OPEN TO INTERNSHIPS</span>
    <span class="badge">⚡ NEXT.JS · PYTHON · JAVA · TYPESCRIPT</span>
    <span class="badge">🌍 BUILT AI FOR 7 INDIAN LANGUAGES</span>
  </div>
  <div class="scroll-hint">▼ &nbsp; SCROLL TO EXPLORE</div>
</section>

<div class="divider"></div>

<!-- ══════════════════════ GAME SECTION ══════════════════════ -->
<section id="game-section">
  <div class="container">
    <div class="section-label">// interactive_01</div>
    <h2 class="section-title">Play My Profile</h2>
    <p style="color:var(--muted);font-family:var(--font-mono);font-size:0.85rem;margin-bottom:2rem;margin-top:-2rem;">
      Collect code snippets to learn about me. Click food items to eat them. Arrow keys / WASD to move.
    </p>

    <div class="game-wrapper">
      <div class="game-header">
        <div class="game-header-left">
          <div class="game-dot r"></div>
          <div class="game-dot y"></div>
          <div class="game-dot g"></div>
          <span class="game-title-bar">sujal@profile:~$ ./snake --bio-mode</span>
        </div>
        <span class="game-controls-hint">↑↓←→ or WASD · Click food to eat · P to pause</span>
      </div>
      <div class="game-stats-bar">
        <div class="game-stat"><span class="game-stat-label">SCORE</span><span class="game-stat-value" id="g-score">0</span></div>
        <div class="game-stat"><span class="game-stat-label">HIGH SCORE</span><span class="game-stat-value" id="g-high">0</span></div>
        <div class="game-stat"><span class="game-stat-label">LENGTH</span><span class="game-stat-value" id="g-len">1</span></div>
        <div class="game-stat"><span class="game-stat-label">LEVEL</span><span class="game-stat-value" id="g-level">1</span></div>
        <div class="game-stat"><span class="game-stat-label">FACT</span><span class="game-stat-value" id="g-fact" style="color:var(--accent3);font-size:0.7rem;max-width:300px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">Start game to learn about Sujal!</span></div>
      </div>
      <div id="game-canvas-wrap">
        <canvas id="gameCanvas" width="700" height="420"></canvas>
        <div id="game-overlay">
          <div class="overlay-title">🐍 BIO SNAKE</div>
          <div class="overlay-sub">
            Eat the food items to collect facts about Sujal.<br/>
            Each item reveals a piece of my story.<br/>
            Can you collect them all?
          </div>
          <button class="btn-primary" id="startBtn">▶ &nbsp; START GAME</button>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════════════════ WHO AM I ══════════════════════ -->
<section id="about">
  <div class="container">
    <div class="section-label">// identity.ts</div>
    <h2 class="section-title">Who Am I</h2>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:3rem;align-items:start;">
      <div class="code-block">
        <div class="code-header">
          <div class="code-dot" style="background:#ef4444"></div>
          <div class="code-dot" style="background:#fbbf24"></div>
          <div class="code-dot" style="background:#10b981"></div>
          <span style="font-size:0.75rem;color:var(--muted);margin-left:0.5rem">identity.ts</span>
        </div>
        <div class="code-body">
<span class="kw">interface</span> <span class="fn">Developer</span> {<br/>
&nbsp;&nbsp;<span class="prop">name</span>:       <span class="str">"Sujal Hitesh Thakkar"</span>;<br/>
&nbsp;&nbsp;<span class="prop">location</span>:   <span class="str">"Thane, Maharashtra 🇮🇳"</span>;<br/>
&nbsp;&nbsp;<span class="prop">university</span>: <span class="str">"K.J. Somaiya SoE"</span>;<br/>
&nbsp;&nbsp;<span class="prop">cgpa</span>:       <span class="num">9.27</span>;<br/>
&nbsp;&nbsp;<span class="prop">grad</span>:       <span class="num">2028</span>;<br/>
&nbsp;&nbsp;<span class="prop">status</span>:     <span class="str">"🟢 Open to Internships"</span>;<br/>
}<br/>
<br/>
<span class="kw">const</span> <span class="fn">sujal</span> = {<br/>
&nbsp;&nbsp;<span class="prop">building</span>:   <span class="str">"Outlier — Productivity OS"</span>,<br/>
&nbsp;&nbsp;<span class="prop">won</span>:        <span class="str">"Periscope Healthcare Hackathon 🏆"</span>,<br/>
&nbsp;&nbsp;<span class="prop">languages</span>: [<span class="str">"Java"</span>, <span class="str">"Python"</span>, <span class="str">"TypeScript"</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">"JavaScript"</span>, <span class="str">"C++"</span>],<br/>
&nbsp;&nbsp;<span class="prop">superpower</span>: <span class="str">"Ships in 42 hrs ⚡"</span>,<br/>
&nbsp;&nbsp;<span class="prop">coffee</span>:     <span class="fn">Infinity</span>,<br/>
}; <span class="cursor-blink"></span>
        </div>
      </div>
      <div>
        <p style="font-size:1.05rem;line-height:1.9;color:var(--muted);margin-bottom:2rem;">
          I'm a second-year CS student who ships production-ready systems. 
          Won 1st place at the Periscope Healthcare Hackathon building an AI doctor 
          that speaks 7 Indian languages — in 42 hours. 
          I build full-stack, I build fast, and I build things that work.
        </p>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:1rem;">
          <div style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:1.25rem;">
            <div style="font-size:1.8rem;margin-bottom:0.4rem;">🏆</div>
            <div style="font-weight:700;font-size:0.95rem;">Hackathon Champion</div>
            <div style="color:var(--muted);font-size:0.8rem;margin-top:0.25rem;">1st Place · Periscope 2025</div>
          </div>
          <div style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:1.25rem;">
            <div style="font-size:1.8rem;margin-bottom:0.4rem;">⚡</div>
            <div style="font-weight:700;font-size:0.95rem;">42-Hour Builder</div>
            <div style="color:var(--muted);font-size:0.8rem;margin-top:0.25rem;">Zero to production AI system</div>
          </div>
          <div style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:1.25rem;">
            <div style="font-size:1.8rem;margin-bottom:0.4rem;">🌍</div>
            <div style="font-weight:700;font-size:0.95rem;">7 Languages Built</div>
            <div style="color:var(--muted);font-size:0.8rem;margin-top:0.25rem;">Hindi, Gujarati, Tamil +4</div>
          </div>
          <div style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:1.25rem;">
            <div style="font-size:1.8rem;margin-bottom:0.4rem;">📜</div>
            <div style="font-weight:700;font-size:0.95rem;">CS50x Certified</div>
            <div style="color:var(--muted);font-size:0.8rem;margin-top:0.25rem;">Harvard University · 2024</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════════════════ SKILLS ══════════════════════ -->
<section id="skills">
  <div class="container">
    <div class="section-label">// skills.json</div>
    <h2 class="section-title">Arsenal</h2>
    <div class="skills-grid">
      <div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">Java</span><span class="skill-pct">95%</span></div><div class="skill-track"><div class="skill-bar" data-w="95"></div></div></div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">TypeScript / JavaScript</span><span class="skill-pct">90%</span></div><div class="skill-track"><div class="skill-bar" data-w="90"></div></div></div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">Python</span><span class="skill-pct">88%</span></div><div class="skill-track"><div class="skill-bar" data-w="88"></div></div></div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">C / C++</span><span class="skill-pct">77%</span></div><div class="skill-track"><div class="skill-bar green-bar" data-w="77"></div></div></div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">SQL / Database Design</span><span class="skill-pct">85%</span></div><div class="skill-track"><div class="skill-bar gold-bar" data-w="85"></div></div></div>
      </div>
      <div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">Next.js / React</span><span class="skill-pct">92%</span></div><div class="skill-track"><div class="skill-bar" data-w="92"></div></div></div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">Flask + SQLAlchemy</span><span class="skill-pct">84%</span></div><div class="skill-track"><div class="skill-bar green-bar" data-w="84"></div></div></div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">Tailwind CSS</span><span class="skill-pct">90%</span></div><div class="skill-track"><div class="skill-bar" data-w="90"></div></div></div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">DSA + Algorithms</span><span class="skill-pct">82%</span></div><div class="skill-track"><div class="skill-bar gold-bar" data-w="82"></div></div></div>
        <div class="skill-item"><div class="skill-header"><span class="skill-name">System Design</span><span class="skill-pct">75%</span></div><div class="skill-track"><div class="skill-bar green-bar" data-w="75"></div></div></div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════════════════ PROJECTS ══════════════════════ -->
<section id="projects">
  <div class="container">
    <div class="section-label">// projects/</div>
    <h2 class="section-title">What I've Shipped</h2>
    <div class="projects-grid">

      <div class="project-card featured" data-xp="50">
        <div class="card-top">
          <span class="card-icon">🏆</span>
          <span class="card-badge">1ST PLACE — HACKATHON</span>
        </div>
        <div class="card-title">AgentFoundry</div>
        <div class="card-desc">An AI doctor that speaks to patients in their native Indian language. Analyzes X-rays, generates structured diagnoses, and delivers voice-based results in real time. Built by a 4-person team in 42 hours — and won.</div>
        <div class="card-metrics">
          <div class="metric"><div class="metric-val">7</div><div class="metric-lbl">LANGUAGES</div></div>
          <div class="metric"><div class="metric-val">42h</div><div class="metric-lbl">BUILD TIME</div></div>
          <div class="metric"><div class="metric-val">&lt;1s</div><div class="metric-lbl">LANG SWITCH</div></div>
          <div class="metric"><div class="metric-val">1st</div><div class="metric-lbl">PLACE</div></div>
        </div>
        <div class="card-tags">
          <span class="tag">Python</span><span class="tag">JavaScript</span><span class="tag">AI/ML</span><span class="tag">Voice Synthesis</span><span class="tag">X-Ray Analysis</span>
        </div>
      </div>

      <div class="project-card" data-xp="30">
        <div class="card-top"><span class="card-icon">⚡</span><span class="card-badge new">FLAGSHIP</span></div>
        <div class="card-title">Outlier</div>
        <div class="card-desc">Dark, gamified productivity OS. Habits, focus sessions, skill tracking, vitality score, and rank progression — from Novice to Outlier.</div>
        <div class="card-metrics">
          <div class="metric"><div class="metric-val">7</div><div class="metric-lbl">MODULES</div></div>
          <div class="metric"><div class="metric-val">5</div><div class="metric-lbl">RANK TIERS</div></div>
        </div>
        <div class="card-tags"><span class="tag">Next.js</span><span class="tag">TypeScript</span><span class="tag">Prisma</span><span class="tag">Tailwind CSS</span></div>
      </div>

      <div class="project-card" data-xp="30">
        <div class="card-top"><span class="card-icon">🛒</span><span class="card-badge">FULL-STACK</span></div>
        <div class="card-title">RetailPulse</div>
        <div class="card-desc">Retail management platform. Weighted Average Cost engine, OCR invoice scanning, role-based access, real-time analytics dashboard.</div>
        <div class="card-metrics">
          <div class="metric"><div class="metric-val">99%+</div><div class="metric-lbl">ACCURACY</div></div>
          <div class="metric"><div class="metric-val">60%</div><div class="metric-lbl">FASTER</div></div>
        </div>
        <div class="card-tags"><span class="tag">Flask</span><span class="tag">MySQL</span><span class="tag">Chart.js</span><span class="tag">OCR</span></div>
      </div>

      <div class="project-card" data-xp="20">
        <div class="card-top"><span class="card-icon">🌍</span><span class="card-badge new">SOCIAL IMPACT</span></div>
        <div class="card-title">ImpactBridge</div>
        <div class="card-desc">Two-sided NGO–volunteer marketplace. QR attendance, auto-certificates, smart re-engagement notifications.</div>
        <div class="card-metrics">
          <div class="metric"><div class="metric-val">100%</div><div class="metric-lbl">VERIFIED</div></div>
        </div>
        <div class="card-tags"><span class="tag">Next.js</span><span class="tag">React</span><span class="tag">PostgreSQL</span></div>
      </div>

      <div class="project-card" data-xp="20">
        <div class="card-top"><span class="card-icon">🔗</span><span class="card-badge">GRAPH THEORY</span></div>
        <div class="card-title">ConnectSphere</div>
        <div class="card-desc">Mutual-friend recommendation engine using Graph Theory and Set Theory. Data Access Object architecture, 40% reduced coupling.</div>
        <div class="card-metrics">
          <div class="metric"><div class="metric-val">40%</div><div class="metric-lbl">LESS COUPLING</div></div>
        </div>
        <div class="card-tags"><span class="tag">Java</span><span class="tag">Swing</span><span class="tag">SQLite</span></div>
      </div>

      <div class="project-card" data-xp="15">
        <div class="card-top"><span class="card-icon">📋</span><span class="card-badge">DESKTOP</span></div>
        <div class="card-title">Trackfolio</div>
        <div class="card-desc">Desktop skill and certificate tracker. Java2D progress visualization, certificate uploads, shareable public portfolio view.</div>
        <div class="card-metrics">
          <div class="metric"><div class="metric-val">80%</div><div class="metric-lbl">TIME SAVED</div></div>
        </div>
        <div class="card-tags"><span class="tag">Java 17</span><span class="tag">Java2D</span><span class="tag">SQLite</span></div>
      </div>

    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════════════════ STATS ══════════════════════ -->
<section id="stats">
  <div class="container">
    <div class="section-label">// metrics.log</div>
    <h2 class="section-title">By The Numbers</h2>
    <div class="stats-row">
      <div class="stat-card"><span class="stat-number" data-count="1">0</span><div class="stat-label">HACKATHON WIN</div></div>
      <div class="stat-card"><span class="stat-number" data-count="6">0</span><div class="stat-label">PROJECTS SHIPPED</div></div>
      <div class="stat-card"><span class="stat-number" data-count="7">0</span><div class="stat-label">LANGUAGES BUILT</div></div>
      <div class="stat-card"><span class="stat-number" data-count="42">0</span><div class="stat-label">HOURS TO WIN</div></div>
    </div>
    <br/><br/>
    <div class="gh-grid">
      <img src="https://github-readme-stats.vercel.app/api?username=SujalThakkar&show_icons=true&theme=midnight-purple&hide_border=true&bg_color=0d0221&title_color=a78bfa&icon_color=a78bfa&text_color=e2e8f0&ring_color=7c3aed&include_all_commits=true&count_private=true" loading="lazy"/>
      <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=SujalThakkar&layout=compact&theme=midnight-purple&hide_border=true&bg_color=0d0221&title_color=a78bfa&text_color=e2e8f0&langs_count=8" loading="lazy"/>
      <img class="gh-full" src="https://streak-stats.demolab.com?user=SujalThakkar&theme=midnight-purple&hide_border=true&background=0d0221&ring=7c3aed&fire=a855f7&currStreakLabel=7c3aed&sideLabels=e2e8f0&dates=94a3b8" loading="lazy"/>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════════════════ CONNECT ══════════════════════ -->
<section id="connect">
  <div class="container">
    <div class="section-label">// contact.sh</div>
    <h2 class="section-title">Let's Build Something</h2>
    <p style="color:var(--muted);max-width:500px;margin:0 auto 2.5rem;line-height:1.8;text-align:center;">
      Open to internships, collabs, and hard problems.<br/>
      Response time under 24 hours. Always.
    </p>
    <div class="connect-links">
      <a class="connect-link" href="https://linkedin.com/in/sujalthakkar" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
      <a class="connect-link" href="mailto:sujal.ht@somaiya.edu">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
        Email
      </a>
      <a class="connect-link" href="https://github.com/SujalThakkar" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
        GitHub
      </a>
    </div>
  </div>
</section>

<footer>
  <div style="margin-bottom:0.5rem">
    ◈ &nbsp; Sujal Hitesh Thakkar &nbsp; · &nbsp; Thane, Maharashtra 🇮🇳 &nbsp; · &nbsp; 2025
  </div>
  <div style="color:var(--border)">Built with obsession. Shipped for real. ⚡</div>
</footer>

<script>
// ═══════════════════════════════════════════════════
//  CURSOR
// ═══════════════════════════════════════════════════
const cursor = document.getElementById('cursor');
const ring   = document.getElementById('cursor-ring');
let mx = 0, my = 0, rx = 0, ry = 0;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx + 'px';
  cursor.style.top  = my + 'px';
});
setInterval(() => {
  rx += (mx - rx) * 0.15;
  ry += (my - ry) * 0.15;
  ring.style.left = rx + 'px';
  ring.style.top  = ry + 'px';
}, 16);

document.querySelectorAll('a, button, .project-card, .badge').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.transform = 'translate(-50%,-50%) scale(2)';
    ring.style.transform   = 'translate(-50%,-50%) scale(1.5)';
    ring.style.opacity     = '1';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.transform = 'translate(-50%,-50%) scale(1)';
    ring.style.transform   = 'translate(-50%,-50%) scale(1)';
    ring.style.opacity     = '0.5';
  });
});

// ═══════════════════════════════════════════════════
//  BACKGROUND CANVAS — STARS + GRID + NEBULA
// ═══════════════════════════════════════════════════
const bgCanvas = document.getElementById('bg-canvas');
const bgCtx = bgCanvas.getContext('2d');
let W, H, stars = [];

function initBg() {
  W = bgCanvas.width  = window.innerWidth;
  H = bgCanvas.height = window.innerHeight;
  stars = Array.from({length: 180}, () => ({
    x: Math.random() * W, y: Math.random() * H,
    r: Math.random() * 1.2 + 0.2,
    a: Math.random(), speed: Math.random() * 0.003 + 0.001,
    drift: (Math.random() - 0.5) * 0.1
  }));
}
window.addEventListener('resize', initBg);
initBg();

let bgFrame = 0;
function drawBg() {
  bgCtx.clearRect(0, 0, W, H);
  bgFrame++;

  // Grid
  bgCtx.strokeStyle = 'rgba(139,92,246,0.03)';
  bgCtx.lineWidth = 1;
  const gridSize = 60;
  for (let x = 0; x < W; x += gridSize) {
    bgCtx.beginPath(); bgCtx.moveTo(x,0); bgCtx.lineTo(x,H); bgCtx.stroke();
  }
  for (let y = 0; y < H; y += gridSize) {
    bgCtx.beginPath(); bgCtx.moveTo(0,y); bgCtx.lineTo(W,y); bgCtx.stroke();
  }

  // Stars
  stars.forEach(s => {
    s.a += s.speed; if (s.a > 1) s.a = 0;
    s.x += s.drift;
    if (s.x < 0) s.x = W; if (s.x > W) s.x = 0;
    const pulse = 0.3 + 0.7 * Math.abs(Math.sin(s.a * Math.PI));
    bgCtx.beginPath();
    bgCtx.arc(s.x, s.y, s.r, 0, Math.PI*2);
    bgCtx.fillStyle = `rgba(196,181,253,${pulse * 0.8})`;
    bgCtx.fill();
  });

  // Nebula glow
  const t = bgFrame * 0.003;
  const gx = W * 0.5 + Math.sin(t) * W * 0.15;
  const gy = H * 0.4 + Math.cos(t * 0.7) * H * 0.1;
  const grad = bgCtx.createRadialGradient(gx, gy, 0, gx, gy, W * 0.4);
  grad.addColorStop(0, 'rgba(124,58,237,0.04)');
  grad.addColorStop(1, 'transparent');
  bgCtx.fillStyle = grad;
  bgCtx.fillRect(0, 0, W, H);

  requestAnimationFrame(drawBg);
}
drawBg();

// ═══════════════════════════════════════════════════
//  XP SYSTEM
// ═══════════════════════════════════════════════════
let xp = 0, maxXP = 300;
const xpBar   = document.getElementById('xp-bar');
const xpVal   = document.getElementById('xp-val');
const xpLabel = document.getElementById('xp-label');

function addXP(amount) {
  xp = Math.min(xp + amount, maxXP);
  const pct = (xp / maxXP) * 100;
  xpBar.style.width = pct + '%';
  xpVal.textContent = xp;
  xpLabel.style.opacity = '1';
  setTimeout(() => { xpLabel.style.opacity = '0'; }, 2000);
}

// ═══════════════════════════════════════════════════
//  TOAST ACHIEVEMENT SYSTEM
// ═══════════════════════════════════════════════════
const toast = document.getElementById('toast');
let toastTimeout;
const achievements = {
  visited:  { icon: '👀', title: 'Explorer', body: 'You opened my profile!' },
  game:     { icon: '🎮', title: 'Gamer', body: 'You played Bio Snake!' },
  score50:  { icon: '🏆', title: 'Snake Master', body: 'Scored 50+ in Bio Snake!' },
  project:  { icon: '🚀', title: 'Curious Mind', body: 'You explored a project!' },
  scrolled: { icon: '🌊', title: 'Deep Diver', body: 'You scrolled the whole page!' },
};
const unlocked = new Set();

function unlock(key) {
  if (unlocked.has(key)) return;
  unlocked.add(key);
  const a = achievements[key];
  if (!a) return;
  document.getElementById('toast-icon').textContent  = a.icon;
  document.getElementById('toast-title').textContent = a.title;
  document.getElementById('toast-body').textContent  = a.body;
  toast.classList.add('show');
  clearTimeout(toastTimeout);
  toastTimeout = setTimeout(() => toast.classList.remove('show'), 3500);
  addXP(25);
}

setTimeout(() => unlock('visited'), 1500);

// ═══════════════════════════════════════════════════
//  PARTICLE BURST ON CLICK
// ═══════════════════════════════════════════════════
function burst(x, y, color = '#a78bfa') {
  const canvas = document.createElement('canvas');
  canvas.className = 'particle-burst';
  canvas.width = 200; canvas.height = 200;
  canvas.style.left = (x - 100) + 'px';
  canvas.style.top  = (y - 100) + 'px';
  document.body.appendChild(canvas);
  const ctx = canvas.getContext('2d');
  const particles = Array.from({length: 18}, () => ({
    x: 100, y: 100,
    vx: (Math.random() - 0.5) * 12,
    vy: (Math.random() - 0.5) * 12,
    r: Math.random() * 4 + 2,
    a: 1,
    hue: color
  }));
  let frame = 0;
  function animate() {
    ctx.clearRect(0, 0, 200, 200);
    particles.forEach(p => {
      p.x += p.vx; p.y += p.vy;
      p.vy += 0.3; p.a -= 0.035;
      if (p.a <= 0) return;
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI*2);
      ctx.fillStyle = p.hue + Math.floor(p.a * 255).toString(16).padStart(2,'0');
      ctx.fill();
    });
    frame++;
    if (frame < 45) requestAnimationFrame(animate);
    else canvas.remove();
  }
  animate();
}

document.addEventListener('click', e => {
  burst(e.clientX, e.clientY);
});

// Project cards XP
document.querySelectorAll('.project-card').forEach(card => {
  card.addEventListener('click', () => {
    const xpAmt = parseInt(card.dataset.xp || '10');
    addXP(xpAmt);
    unlock('project');
    burst(
      card.getBoundingClientRect().left + card.offsetWidth/2,
      card.getBoundingClientRect().top  + card.offsetHeight/2,
      '#fbbf24'
    );
  });
  // Mouse move glow effect
  card.addEventListener('mousemove', e => {
    const r = card.getBoundingClientRect();
    const x = ((e.clientX - r.left) / r.width  * 100).toFixed(1);
    const y = ((e.clientY - r.top)  / r.height * 100).toFixed(1);
    card.style.setProperty('--mx', x + '%');
    card.style.setProperty('--my', y + '%');
  });
});

// ═══════════════════════════════════════════════════
//  SKILL BARS ANIMATION ON SCROLL
// ═══════════════════════════════════════════════════
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.querySelectorAll('.skill-bar').forEach(bar => {
        bar.style.width = bar.dataset.w + '%';
      });
      e.target.querySelectorAll('[data-count]').forEach(el => {
        const target = parseInt(el.dataset.count);
        let current = 0;
        const step = Math.ceil(target / 40);
        const timer = setInterval(() => {
          current = Math.min(current + step, target);
          el.textContent = current;
          if (current >= target) clearInterval(timer);
        }, 40);
      });
    }
  });
}, { threshold: 0.3 });

document.querySelectorAll('#skills, #stats').forEach(s => observer.observe(s));

// Scroll achievements
const scrollObserver = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting && e.target.id === 'connect') {
      unlock('scrolled');
    }
  });
}, { threshold: 0.5 });
const connectSec = document.getElementById('connect');
if (connectSec) scrollObserver.observe(connectSec);

// ═══════════════════════════════════════════════════
//  BIO SNAKE GAME
// ═══════════════════════════════════════════════════
const gameCanvas  = document.getElementById('gameCanvas');
const gCtx        = gameCanvas.getContext('2d');
const overlay     = document.getElementById('game-overlay');
const startBtn    = document.getElementById('startBtn');

const CELL  = 20;
const COLS  = Math.floor(gameCanvas.width  / CELL);
const ROWS  = Math.floor(gameCanvas.height / CELL);

const FACTS = [
  { emoji: '🏆', text: '1st Place — Periscope Healthcare Hackathon 2025!', color: '#fbbf24', pts: 15 },
  { emoji: '🌍', text: 'Built AI that speaks 7 Indian languages!', color: '#34d399', pts: 12 },
  { emoji: '⚡', text: 'Shipped a production AI system in just 42 hours!', color: '#a78bfa', pts: 12 },
  { emoji: '📜', text: 'Completed Harvard CS50x — all 10 modules!', color: '#60a5fa', pts: 10 },
  { emoji: '⭐', text: 'CGPA 9.48 in Semester 2!', color: '#fbbf24', pts: 10 },
  { emoji: '🛒', text: 'RetailPulse: 99%+ profit accuracy with WAC algorithm!', color: '#f87171', pts: 10 },
  { emoji: '🔗', text: 'ConnectSphere uses Graph Theory for recommendations!', color: '#c084fc', pts: 8 },
  { emoji: '🚀', text: 'ImpactBridge connects NGOs with volunteers via QR!', color: '#34d399', pts: 8 },
  { emoji: '💜', text: 'From Thane, Maharashtra 🇮🇳', color: '#a78bfa', pts: 5 },
  { emoji: '☕', text: 'Coffee consumed: Infinity. No upper bound detected.', color: '#fbbf24', pts: 5 },
];

let snake, dir, nextDir, foods, score, highScore = 0, level, gameInterval, paused, gameOver, collected;

function initGame() {
  const cx = Math.floor(COLS / 2), cy = Math.floor(ROWS / 2);
  snake = [{ x: cx, y: cy }, { x: cx-1, y: cy }, { x: cx-2, y: cy }];
  dir = { x: 1, y: 0 }; nextDir = { x: 1, y: 0 };
  score = 0; level = 1; paused = false; gameOver = false; collected = new Set();
  foods = [];
  spawnFood();
  updateStats();
}

function spawnFood() {
  if (foods.length >= 3) return;
  const remaining = FACTS.filter((_, i) => !collected.has(i));
  if (!remaining.length) return;
  const idx = FACTS.indexOf(remaining[Math.floor(Math.random() * remaining.length)]);
  let pos;
  let tries = 0;
  do {
    pos = { x: Math.floor(Math.random() * COLS), y: Math.floor(Math.random() * ROWS) };
    tries++;
  } while (tries < 100 && (
    snake.some(s => s.x === pos.x && s.y === pos.y) ||
    foods.some(f => f.x === pos.x && f.y === pos.y)
  ));
  foods.push({ ...pos, factIdx: idx, pulse: 0 });
}

function updateStats() {
  document.getElementById('g-score').textContent = score;
  document.getElementById('g-high').textContent  = highScore;
  document.getElementById('g-len').textContent   = snake.length;
  document.getElementById('g-level').textContent = level;
}

function step() {
  if (paused || gameOver) return;
  dir = { ...nextDir };

  const head = { x: snake[0].x + dir.x, y: snake[0].y + dir.y };

  // Wall collision
  if (head.x < 0 || head.x >= COLS || head.y < 0 || head.y >= ROWS) {
    endGame(); return;
  }
  // Self collision
  if (snake.some(s => s.x === head.x && s.y === head.y)) {
    endGame(); return;
  }

  snake.unshift(head);

  // Check food
  const fi = foods.findIndex(f => f.x === head.x && f.y === head.y);
  if (fi !== -1) {
    const food = foods[fi];
    const fact = FACTS[food.factIdx];
    score += fact.pts;
    if (score > highScore) highScore = score;
    collected.add(food.factIdx);
    foods.splice(fi, 1);

    document.getElementById('g-fact').textContent = fact.emoji + ' ' + fact.text;

    // Particle burst on eat
    const px = (food.x * CELL + CELL/2) + gameCanvas.getBoundingClientRect().left;
    const py = (food.y * CELL + CELL/2) + gameCanvas.getBoundingClientRect().top;
    burst(px, py, fact.color);

    addXP(fact.pts);
    level = Math.floor(score / 50) + 1;

    // Speed up
    clearInterval(gameInterval);
    gameInterval = setInterval(step, Math.max(80, 200 - (level - 1) * 15));

    if (score >= 50) unlock('score50');
    spawnFood();
  } else {
    snake.pop();
  }

  if (foods.length < 2) spawnFood();
  updateStats();
  draw();
}

function endGame() {
  gameOver = true;
  clearInterval(gameInterval);
  if (score > highScore) highScore = score;
  updateStats();

  // Show game over
  gCtx.fillStyle = 'rgba(4,1,15,0.85)';
  gCtx.fillRect(0, 0, gameCanvas.width, gameCanvas.height);

  gCtx.textAlign = 'center';
  gCtx.font = 'bold 36px Syne, sans-serif';
  gCtx.fillStyle = '#ef4444';
  gCtx.fillText('GAME OVER', gameCanvas.width/2, gameCanvas.height/2 - 50);

  gCtx.font = 'bold 20px JetBrains Mono, monospace';
  gCtx.fillStyle = '#a78bfa';
  gCtx.fillText(`Score: ${score}  |  High: ${highScore}  |  Facts: ${collected.size}/${FACTS.length}`, gameCanvas.width/2, gameCanvas.height/2);

  gCtx.font = '14px JetBrains Mono, monospace';
  gCtx.fillStyle = '#64748b';
  gCtx.fillText('Click START to play again', gameCanvas.width/2, gameCanvas.height/2 + 50);

  overlay.style.display = 'flex';
  overlay.querySelector('.overlay-title').textContent = '💀 GAME OVER';
  overlay.querySelector('.overlay-sub').textContent = `Score: ${score} · Facts collected: ${collected.size}/${FACTS.length}\nClick to play again!`;
  startBtn.textContent = '↩ PLAY AGAIN';
}

function draw() {
  // Background
  gCtx.fillStyle = '#03010a';
  gCtx.fillRect(0, 0, gameCanvas.width, gameCanvas.height);

  // Grid
  gCtx.strokeStyle = 'rgba(139,92,246,0.04)';
  gCtx.lineWidth = 1;
  for (let x = 0; x <= COLS; x++) {
    gCtx.beginPath(); gCtx.moveTo(x*CELL,0); gCtx.lineTo(x*CELL, gameCanvas.height); gCtx.stroke();
  }
  for (let y = 0; y <= ROWS; y++) {
    gCtx.beginPath(); gCtx.moveTo(0,y*CELL); gCtx.lineTo(gameCanvas.width, y*CELL); gCtx.stroke();
  }

  // Foods — pulsing emoji
  foods.forEach(f => {
    f.pulse = (f.pulse || 0) + 0.05;
    const scale = 1 + Math.sin(f.pulse) * 0.15;
    const fact = FACTS[f.factIdx];

    // Glow
    gCtx.save();
    gCtx.shadowColor = fact.color;
    gCtx.shadowBlur  = 18;
    gCtx.translate(f.x * CELL + CELL/2, f.y * CELL + CELL/2);
    gCtx.scale(scale, scale);
    gCtx.font = `${CELL * 0.9}px serif`;
    gCtx.textAlign = 'center';
    gCtx.textBaseline = 'middle';
    gCtx.fillText(fact.emoji, 0, 0);
    gCtx.restore();
  });

  // Snake
  snake.forEach((seg, i) => {
    const t = i / snake.length;
    const r = i === 0 ? 8 : 5;

    // Gradient color head→tail
    const hue = 260 + t * 40;
    const light = 70 - t * 30;
    gCtx.save();
    gCtx.shadowColor = `hsl(${hue},80%,${light}%)`;
    gCtx.shadowBlur  = i === 0 ? 16 : 6;
    gCtx.fillStyle   = `hsl(${hue},80%,${light}%)`;
    roundRect(gCtx, seg.x * CELL + 2, seg.y * CELL + 2, CELL - 4, CELL - 4, r);
    gCtx.fill();
    gCtx.restore();

    // Eyes on head
    if (i === 0) {
      gCtx.fillStyle = 'white';
      const ex = dir.x === 0 ? CELL*0.3 : (dir.x > 0 ? CELL*0.65 : CELL*0.25);
      const ey = dir.y === 0 ? CELL*0.3 : (dir.y > 0 ? CELL*0.65 : CELL*0.25);
      gCtx.beginPath(); gCtx.arc(seg.x*CELL+ex, seg.y*CELL+ey, 2.5, 0, Math.PI*2); gCtx.fill();
      const ex2 = dir.x === 0 ? CELL*0.7 : ex;
      const ey2 = dir.y === 0 ? CELL*0.7 : ey;
      gCtx.beginPath(); gCtx.arc(seg.x*CELL+ex2, seg.y*CELL+ey2, 2.5, 0, Math.PI*2); gCtx.fill();
    }
  });
}

function roundRect(ctx, x, y, w, h, r) {
  ctx.beginPath();
  ctx.moveTo(x+r, y);
  ctx.lineTo(x+w-r, y); ctx.arcTo(x+w, y, x+w, y+r, r);
  ctx.lineTo(x+w, y+h-r); ctx.arcTo(x+w, y+h, x+w-r, y+h, r);
  ctx.lineTo(x+r, y+h); ctx.arcTo(x, y+h, x, y+h-r, r);
  ctx.lineTo(x, y+r); ctx.arcTo(x, y, x+r, y, r);
  ctx.closePath();
}

// Controls
document.addEventListener('keydown', e => {
  const map = {
    ArrowUp:'u', ArrowDown:'d', ArrowLeft:'l', ArrowRight:'r',
    w:'u', s:'d', a:'l', d:'r', W:'u', S:'d', A:'l', D:'r'
  };
  const m = map[e.key];
  if (m) {
    e.preventDefault();
    if (m==='u' && dir.y !== 1)  nextDir = {x:0,y:-1};
    if (m==='d' && dir.y !== -1) nextDir = {x:0,y:1};
    if (m==='l' && dir.x !== 1)  nextDir = {x:-1,y:0};
    if (m==='r' && dir.x !== -1) nextDir = {x:1,y:0};
  }
  if (e.key === 'p' || e.key === 'P') {
    paused = !paused;
  }
});

// Click-to-eat: click on canvas where food is
gameCanvas.addEventListener('click', e => {
  if (gameOver) return;
  const rect = gameCanvas.getBoundingClientRect();
  const cx = Math.floor((e.clientX - rect.left) / CELL);
  const cy = Math.floor((e.clientY - rect.top)  / CELL);
  const fi = foods.findIndex(f => f.x === cx && f.y === cy);
  if (fi !== -1) {
    const food = foods[fi];
    const fact = FACTS[food.factIdx];
    score += Math.floor(fact.pts / 2); // half points for clicking
    collected.add(food.factIdx);
    foods.splice(fi, 1);
    document.getElementById('g-fact').textContent = '👆 ' + fact.emoji + ' ' + fact.text;
    burst(e.clientX, e.clientY, fact.color);
    addXP(fact.pts);
    spawnFood();
    updateStats();
    draw();
  }
});

startBtn.addEventListener('click', () => {
  overlay.style.display = 'none';
  initGame();
  clearInterval(gameInterval);
  gameInterval = setInterval(step, 175);
  draw();
  unlock('game');
  addXP(10);
});

// Initial draw
initGame();
draw();
</script>
</body>
</html>
READMEEOF
echo "Done"
