<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Abhinav Sharma — Full Stack MERN Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;600;700;800&family=JetBrains+Mono:wght@300;400;600&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #070b14;
    --surface: #0d1424;
    --surface2: #111827;
    --teal: #38b2ac;
    --teal2: #4fd1c5;
    --cyan: #67e8f9;
    --purple: #818cf8;
    --pink: #f472b6;
    --yellow: #fbbf24;
    --green: #34d399;
    --text: #e2e8f0;
    --muted: #64748b;
    --border: rgba(56,178,172,0.15);
    --glow: rgba(56,178,172,0.4);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* ── Custom Cursor ── */
  #cursor {
    position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9999;
    width: 12px; height: 12px;
    background: var(--teal);
    border-radius: 50%;
    transform: translate(-50%,-50%);
    transition: transform .1s, background .2s;
    mix-blend-mode: screen;
  }
  #cursor-trail {
    position: fixed; top: 0; left: 0; pointer-events: none; z-index: 9998;
    width: 32px; height: 32px;
    border: 1px solid var(--teal);
    border-radius: 50%;
    transform: translate(-50%,-50%);
    opacity: .4;
    transition: transform .25s ease, opacity .2s;
  }

  /* ── Canvas bg ── */
  #bg-canvas {
    position: fixed; inset: 0; z-index: 0;
    pointer-events: none;
  }

  /* ── Layout ── */
  .wrapper {
    position: relative; z-index: 1;
    max-width: 920px;
    margin: 0 auto;
    padding: 0 24px 80px;
  }

  /* ── Hero ── */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 80px 0 40px;
    position: relative;
  }

  .hero-badge {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--teal);
    border: 1px solid var(--border);
    padding: 6px 18px;
    border-radius: 100px;
    margin-bottom: 32px;
    animation: fadeSlideDown .8s ease both;
    background: rgba(56,178,172,.05);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(52px, 10vw, 96px);
    font-weight: 800;
    line-height: .95;
    letter-spacing: -2px;
    animation: fadeSlideDown .9s .1s ease both;
    background: linear-gradient(135deg, #fff 0%, var(--teal2) 50%, var(--cyan) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-title {
    font-family: 'Space Mono', monospace;
    font-size: clamp(14px, 2.5vw, 20px);
    color: var(--muted);
    margin-top: 16px;
    animation: fadeSlideDown 1s .2s ease both;
    letter-spacing: 1px;
  }

  .hero-title span { color: var(--teal); }

  .type-line {
    font-family: 'JetBrains Mono', monospace;
    font-size: clamp(13px, 2vw, 16px);
    color: var(--teal2);
    margin-top: 28px;
    height: 24px;
    animation: fadeSlideDown 1s .4s ease both;
  }

  .type-cursor {
    display: inline-block;
    width: 2px; height: 1.1em;
    background: var(--teal);
    vertical-align: middle;
    margin-left: 3px;
    animation: blink 1s step-end infinite;
  }

  .hero-cta {
    display: flex; gap: 16px; margin-top: 40px;
    flex-wrap: wrap; justify-content: center;
    animation: fadeSlideDown 1s .5s ease both;
  }

  .btn {
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    letter-spacing: 1px;
    padding: 12px 28px;
    border-radius: 6px;
    cursor: pointer;
    text-decoration: none;
    transition: all .25s;
    display: inline-flex; align-items: center; gap: 8px;
  }
  .btn-primary {
    background: var(--teal);
    color: #000;
    font-weight: 700;
  }
  .btn-primary:hover { background: var(--teal2); transform: translateY(-2px); box-shadow: 0 8px 24px var(--glow); }
  .btn-outline {
    border: 1px solid var(--border);
    color: var(--text);
    background: transparent;
  }
  .btn-outline:hover { border-color: var(--teal); color: var(--teal); transform: translateY(-2px); }

  .scroll-hint {
    position: absolute; bottom: 32px; left: 50%; transform: translateX(-50%);
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px; color: var(--muted);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    animation: fadeIn 1s 1.5s ease both;
  }
  .scroll-hint span { animation: bounceY 1.5s ease-in-out infinite; }

  /* ── Section ── */
  section {
    padding: 80px 0;
    opacity: 0; transform: translateY(40px);
    transition: opacity .7s ease, transform .7s ease;
  }
  section.visible { opacity: 1; transform: none; }

  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px; letter-spacing: 3px;
    text-transform: uppercase; color: var(--teal);
    margin-bottom: 12px;
  }

  .section-title {
    font-size: clamp(28px, 5vw, 44px);
    font-weight: 800; letter-spacing: -1px;
    margin-bottom: 48px;
    line-height: 1.1;
  }

  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--teal), transparent);
    margin: 0 0 80px;
    opacity: .3;
  }

  /* ── About ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    align-items: start;
  }

  .about-facts {
    display: flex; flex-direction: column; gap: 14px;
  }

  .fact-item {
    display: flex; align-items: flex-start; gap: 14px;
    padding: 16px 20px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    transition: border-color .3s, transform .3s;
    cursor: default;
  }
  .fact-item:hover { border-color: var(--teal); transform: translateX(6px); }
  .fact-emoji { font-size: 18px; flex-shrink: 0; margin-top: 2px; }
  .fact-text { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: var(--text); line-height: 1.5; }
  .fact-text strong { color: var(--teal); }

  .about-terminal {
    background: #0a0f1a;
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    font-family: 'JetBrains Mono', monospace;
  }
  .terminal-bar {
    background: var(--surface2);
    padding: 10px 16px;
    display: flex; align-items: center; gap: 8px;
    border-bottom: 1px solid var(--border);
  }
  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot-r { background: #ff5f57; }
  .dot-y { background: #ffbd2e; }
  .dot-g { background: #28ca41; }
  .terminal-title { font-size: 11px; color: var(--muted); margin-left: auto; }
  .terminal-body { padding: 20px; font-size: 12px; line-height: 1.8; }
  .t-line { display: block; }
  .t-prompt { color: var(--teal); }
  .t-cmd { color: var(--cyan); }
  .t-out { color: var(--muted); padding-left: 16px; }
  .t-out .hi { color: var(--text); }
  .t-out .accent { color: var(--teal2); }
  .t-cursor-inline { display: inline-block; width: 8px; height: 14px; background: var(--teal); vertical-align: middle; animation: blink 1s step-end infinite; }

  /* ── Connect ── */
  .connect-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 12px;
  }

  .social-card {
    display: flex; align-items: center; gap: 12px;
    padding: 14px 18px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    text-decoration: none; color: var(--text);
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    transition: all .25s;
    position: relative; overflow: hidden;
  }
  .social-card::before {
    content: '';
    position: absolute; inset: 0;
    background: var(--card-color, var(--teal));
    opacity: 0;
    transition: opacity .25s;
  }
  .social-card:hover::before { opacity: .08; }
  .social-card:hover { border-color: var(--card-color, var(--teal)); transform: translateY(-3px); box-shadow: 0 8px 20px rgba(0,0,0,.3); color: var(--card-color, var(--teal)); }
  .social-icon { font-size: 18px; z-index: 1; }
  .social-name { z-index: 1; }

  /* ── Tech Stack ── */
  .stack-section { margin-bottom: 40px; }
  .stack-category {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px; letter-spacing: 2px;
    text-transform: uppercase; color: var(--muted);
    margin-bottom: 14px;
    display: flex; align-items: center; gap: 10px;
  }
  .stack-category::after { content: ''; flex: 1; height: 1px; background: var(--border); }

  .tech-grid { display: flex; flex-wrap: wrap; gap: 10px; }

  .tech-pill {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 8px 14px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    font-family: 'Space Mono', monospace;
    font-size: 11px; color: var(--text);
    cursor: default;
    transition: all .2s;
    position: relative;
  }
  .tech-pill:hover {
    border-color: var(--pill-color, var(--teal));
    color: var(--pill-color, var(--teal));
    transform: translateY(-3px) scale(1.04);
    box-shadow: 0 6px 16px rgba(0,0,0,.4);
  }
  .tech-pill img { width: 16px; height: 16px; object-fit: contain; }

  /* ── Stats ── */
  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }
  .stat-img {
    border-radius: 12px;
    overflow: hidden;
    border: 1px solid var(--border);
    transition: border-color .3s, transform .3s;
  }
  .stat-img:hover { border-color: var(--teal); transform: scale(1.01); }
  .stat-img img { width: 100%; display: block; }
  .stat-img.full { grid-column: 1 / -1; }

  /* ── Currently Working ── */
  .work-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }

  .work-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 22px 24px;
    display: flex; align-items: flex-start; gap: 16px;
    transition: all .3s;
    position: relative; overflow: hidden;
  }
  .work-card::before {
    content: '';
    position: absolute; left: 0; top: 0; bottom: 0; width: 3px;
    background: var(--accent, var(--teal));
    transform: scaleY(0);
    transition: transform .3s;
    transform-origin: top;
  }
  .work-card:hover::before { transform: scaleY(1); }
  .work-card:hover { border-color: var(--accent, var(--teal)); transform: translateY(-3px); }
  .work-icon { font-size: 28px; flex-shrink: 0; }
  .work-title { font-size: 12px; font-family: 'JetBrains Mono', monospace; color: var(--accent, var(--teal)); margin-bottom: 4px; letter-spacing: 1px; text-transform: uppercase; }
  .work-desc { font-size: 13px; color: var(--text); line-height: 1.6; }

  /* ── Contribution ── */
  .contrib-wrap {
    border-radius: 12px; overflow: hidden;
    border: 1px solid var(--border);
    transition: border-color .3s;
  }
  .contrib-wrap:hover { border-color: var(--teal); }
  .contrib-wrap img { width: 100%; display: block; }

  /* ── Quote ── */
  .quote-box {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 40px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .quote-box::before {
    content: '"';
    position: absolute; top: -20px; left: 20px;
    font-size: 140px; color: var(--teal);
    opacity: .06;
    font-family: Georgia, serif;
    line-height: 1;
  }
  .quote-text {
    font-family: 'Syne', sans-serif;
    font-size: clamp(22px, 4vw, 36px);
    font-weight: 700;
    letter-spacing: -0.5px;
    color: var(--text);
    line-height: 1.3;
    position: relative; z-index: 1;
  }
  .quote-text span { color: var(--teal); }
  .quote-sub {
    margin-top: 16px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px; color: var(--muted);
    letter-spacing: 2px;
  }

  /* ── Footer ── */
  footer {
    text-align: center;
    padding: 48px 0 24px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px; color: var(--muted);
    border-top: 1px solid var(--border);
  }
  footer strong { color: var(--teal); }

  /* ── Floating badges ── */
  .badge-row {
    display: flex; gap: 10px; flex-wrap: wrap; justify-content: center;
    margin-bottom: 24px;
    animation: fadeSlideDown 1s .3s ease both;
  }
  .badge-item {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px; color: var(--muted);
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 4px 12px; border-radius: 100px;
    display: flex; align-items: center; gap: 6px;
  }
  .badge-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--teal); animation: pulse 2s ease-in-out infinite; }

  /* ── Animations ── */
  @keyframes fadeSlideDown {
    from { opacity: 0; transform: translateY(-20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; } to { opacity: 1; }
  }
  @keyframes blink {
    0%, 100% { opacity: 1; } 50% { opacity: 0; }
  }
  @keyframes bounceY {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(8px); }
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: .5; transform: scale(1.3); }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0) rotate(0deg); }
    50% { transform: translateY(-18px) rotate(3deg); }
  }
  @keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
  }

  /* ── LeetCode Section ── */
  .lc-hero {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin-bottom: 28px;
  }

  .lc-profile-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 28px;
    display: flex; flex-direction: column; align-items: center;
    text-align: center; gap: 12px;
    position: relative; overflow: hidden;
    transition: border-color .3s, transform .3s;
  }
  .lc-profile-card:hover { border-color: var(--yellow); transform: translateY(-3px); }
  .lc-profile-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 3px;
    background: linear-gradient(90deg, #fbbf24, #f97316, #ef4444);
  }

  .lc-avatar {
    width: 64px; height: 64px; border-radius: 50%;
    border: 2px solid var(--yellow);
    display: flex; align-items: center; justify-content: center;
    font-size: 28px;
    background: rgba(251,191,36,.1);
  }
  .lc-username {
    font-family: 'Syne', sans-serif;
    font-weight: 700; font-size: 18px; color: var(--yellow);
  }
  .lc-rank {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px; color: var(--muted);
    background: rgba(251,191,36,.08);
    padding: 4px 14px; border-radius: 100px;
    border: 1px solid rgba(251,191,36,.2);
  }
  .lc-rank span { color: var(--yellow); }

  .lc-donut-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 28px;
    display: flex; align-items: center; gap: 24px;
    position: relative; overflow: hidden;
    transition: border-color .3s, transform .3s;
  }
  .lc-donut-card:hover { border-color: var(--teal); transform: translateY(-3px); }
  .lc-donut-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 3px;
    background: linear-gradient(90deg, #38b2ac, #818cf8);
  }

  .lc-donut-wrap {
    position: relative; flex-shrink: 0;
    width: 110px; height: 110px;
  }
  .lc-donut-wrap svg { transform: rotate(-90deg); }
  .lc-donut-center {
    position: absolute; inset: 0;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
  }
  .lc-donut-num {
    font-family: 'Syne', sans-serif; font-weight: 800; font-size: 22px; color: var(--text);
    line-height: 1;
  }
  .lc-donut-label {
    font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--muted);
    letter-spacing: 1px; text-transform: uppercase;
  }

  .lc-breakdown { flex: 1; display: flex; flex-direction: column; gap: 10px; }
  .lc-diff-row { display: flex; align-items: center; gap: 10px; }
  .lc-diff-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
  .lc-diff-info { flex: 1; }
  .lc-diff-name {
    font-family: 'JetBrains Mono', monospace; font-size: 10px;
    letter-spacing: 1px; text-transform: uppercase;
  }
  .lc-diff-bar-wrap {
    height: 4px; background: rgba(255,255,255,.05); border-radius: 2px; margin-top: 4px;
    overflow: hidden;
  }
  .lc-diff-bar {
    height: 100%; border-radius: 2px;
    width: 0%;
    transition: width 1.4s cubic-bezier(.4,0,.2,1);
  }
  .lc-diff-count {
    font-family: 'JetBrains Mono', monospace; font-size: 12px; font-weight: 600;
    flex-shrink: 0;
  }

  .lc-stats-row {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
    margin-bottom: 20px;
  }
  .lc-stat-box {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 18px 16px;
    text-align: center;
    transition: all .3s;
    cursor: default;
  }
  .lc-stat-box:hover { transform: translateY(-4px); border-color: var(--stat-color, var(--teal)); box-shadow: 0 8px 20px rgba(0,0,0,.3); }
  .lc-stat-val {
    font-family: 'Syne', sans-serif; font-weight: 800;
    font-size: 26px; color: var(--stat-color, var(--teal));
    line-height: 1;
  }
  .lc-stat-lbl {
    font-family: 'JetBrains Mono', monospace; font-size: 10px;
    color: var(--muted); letter-spacing: 1px; text-transform: uppercase;
    margin-top: 4px;
  }

  .lc-link-btn {
    display: inline-flex; align-items: center; gap: 8px;
    font-family: 'Space Mono', monospace; font-size: 12px;
    color: var(--yellow); text-decoration: none;
    border: 1px solid rgba(251,191,36,.3);
    padding: 10px 22px; border-radius: 8px;
    background: rgba(251,191,36,.05);
    transition: all .25s;
    margin-top: 4px;
  }
  .lc-link-btn:hover { background: rgba(251,191,36,.12); border-color: var(--yellow); transform: translateY(-2px); }

  .lc-loading {
    display: flex; flex-direction: column; align-items: center; gap: 16px;
    padding: 60px 0; color: var(--muted);
    font-family: 'JetBrains Mono', monospace; font-size: 13px;
  }
  .lc-spinner {
    width: 36px; height: 36px; border-radius: 50%;
    border: 3px solid rgba(251,191,36,.15);
    border-top-color: var(--yellow);
    animation: spin .8s linear infinite;
  }
  .lc-error {
    text-align: center; padding: 40px;
    font-family: 'JetBrains Mono', monospace; font-size: 13px; color: var(--muted);
  }
  .lc-error a { color: var(--yellow); }

  /* ── Responsive ── */
  @media (max-width: 640px) {
    .about-grid, .stats-grid, .work-grid { grid-template-columns: 1fr; }
    .stat-img.full { grid-column: 1; }
    .lc-hero { grid-template-columns: 1fr; }
    .lc-stats-row { grid-template-columns: repeat(2, 1fr); }
  }
</style>
</head>
<body>

<canvas id="bg-canvas"></canvas>
<div id="cursor"></div>
<div id="cursor-trail"></div>

<div class="wrapper">

  <!-- ── HERO ── -->
  <section class="hero" style="opacity:1;transform:none;">
    <div class="hero-badge">🚀 Available for Opportunities</div>
    <h1 class="hero-name">Abhinav<br/>Sharma</h1>
    <p class="hero-title">Full Stack <span>MERN</span> Developer</p>
    <div class="type-line">
      <span id="typewriter"></span><span class="type-cursor"></span>
    </div>
    <div class="badge-row" style="margin-top:32px;">
      <div class="badge-item"><span class="badge-dot"></span> React</div>
      <div class="badge-item"><span class="badge-dot"></span> Node.js</div>
      <div class="badge-item"><span class="badge-dot"></span> MongoDB</div>
      <div class="badge-item"><span class="badge-dot"></span> Express</div>
      <div class="badge-item"><span class="badge-dot"></span> Socket.io</div>
    </div>
    <div class="hero-cta">
      <a href="https://www.linkedin.com/in/abhinav-sharma-56131135a" class="btn btn-primary" target="_blank">Connect on LinkedIn ↗</a>
      <a href="mailto:abhinavsharma3614@gmail.com" class="btn btn-outline">📧 Say Hello</a>
      <a href="https://github.com/AbhinavSharma0188" class="btn btn-outline" target="_blank">⭐ GitHub</a>
    </div>
    <div class="scroll-hint">
      <span>↓</span>
      <span style="font-family:'JetBrains Mono',monospace;font-size:10px;letter-spacing:2px;">SCROLL</span>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── ABOUT ── -->
  <section id="about">
    <div class="section-label">// 01 — about_me</div>
    <h2 class="section-title">Who Am I?</h2>
    <div class="about-grid">
      <div class="about-facts">
        <div class="fact-item"><span class="fact-emoji">🚀</span><div class="fact-text">Full Stack Web Developer specializing in the <strong>MERN Stack</strong></div></div>
        <div class="fact-item"><span class="fact-emoji">💻</span><div class="fact-text">Proficient in <strong>React · Node.js · MongoDB · JavaScript</strong></div></div>
        <div class="fact-item"><span class="fact-emoji">📚</span><div class="fact-text">Currently strengthening <strong>DSA & Backend Architecture</strong></div></div>
        <div class="fact-item"><span class="fact-emoji">🎯</span><div class="fact-text">Goal: Build <strong>scalable, production-ready</strong> web applications</div></div>
        <div class="fact-item"><span class="fact-emoji">🔥</span><div class="fact-text">Passionate about <strong>performance optimization & clean UI/UX</strong></div></div>
        <div class="fact-item"><span class="fact-emoji">⚡</span><div class="fact-text">Fun fact: <em>I debug with console.log and I'm not ashamed</em></div></div>
      </div>
      <div class="about-terminal">
        <div class="terminal-bar">
          <div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div>
          <div class="terminal-title">abhinav@portfolio ~ zsh</div>
        </div>
        <div class="terminal-body">
          <span class="t-line"><span class="t-prompt">➜</span> <span class="t-cmd">whoami</span></span>
          <span class="t-line t-out"><span class="hi">Abhinav Sharma</span></span>
          <span class="t-line" style="margin-top:8px;"><span class="t-prompt">➜</span> <span class="t-cmd">cat role.txt</span></span>
          <span class="t-line t-out"><span class="accent">Full Stack MERN Developer</span></span>
          <span class="t-line" style="margin-top:8px;"><span class="t-prompt">➜</span> <span class="t-cmd">cat status.json</span></span>
          <span class="t-line t-out">{ <span class="accent">"open_to_work"</span>: true,</span>
          <span class="t-line t-out">&nbsp;&nbsp;<span class="accent">"location"</span>: "India",</span>
          <span class="t-line t-out">&nbsp;&nbsp;<span class="accent">"building"</span>: "MERN + Socket.io app",</span>
          <span class="t-line t-out">&nbsp;&nbsp;<span class="accent">"learning"</span>: ["DSA", "AWS", "Docker"] }</span>
          <span class="t-line" style="margin-top:8px;"><span class="t-prompt">➜</span> <span class="t-cursor-inline"></span></span>
        </div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── CONNECT ── -->
  <section id="connect">
    <div class="section-label">// 02 — connect_with_me</div>
    <h2 class="section-title">Let's Talk 👋</h2>
    <div class="connect-grid">
      <a href="https://www.linkedin.com/in/abhinav-sharma-56131135a" class="social-card" style="--card-color:#0077B5" target="_blank"><span class="social-icon">💼</span><span class="social-name">LinkedIn</span></a>
      <a href="mailto:abhinavsharma3614@gmail.com" class="social-card" style="--card-color:#D14836"><span class="social-icon">📧</span><span class="social-name">Gmail</span></a>
      <a href="https://www.behance.net/abhinavsharma224" class="social-card" style="--card-color:#1769ff" target="_blank"><span class="social-icon">🎨</span><span class="social-name">Behance</span></a>
      <a href="https://discord.gg/7EDnJMRy" class="social-card" style="--card-color:#7289DA" target="_blank"><span class="social-icon">🎮</span><span class="social-name">Discord</span></a>
      <a href="https://stackoverflow.com/users/32224723/abhinav-sharma" class="social-card" style="--card-color:#FE7A16" target="_blank"><span class="social-icon">📚</span><span class="social-name">Stack Overflow</span></a>
      <a href="https://www.reddit.com/user/DanceConscious9855/" class="social-card" style="--card-color:#FF4500" target="_blank"><span class="social-icon">🤖</span><span class="social-name">Reddit</span></a>
      <a href="https://in.pinterest.com/abhinavsharma3614/" class="social-card" style="--card-color:#E60023" target="_blank"><span class="social-icon">📌</span><span class="social-name">Pinterest</span></a>
      <a href="https://www.quora.com/profile/Abhinav-Sharma-4709" class="social-card" style="--card-color:#B92B27" target="_blank"><span class="social-icon">❓</span><span class="social-name">Quora</span></a>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── TECH STACK ── -->
  <section id="stack">
    <div class="section-label">// 03 — tech_stack</div>
    <h2 class="section-title">My Arsenal 🧠</h2>

    <div class="stack-section">
      <div class="stack-category">💻 Languages</div>
      <div class="tech-grid">
        <div class="tech-pill" style="--pill-color:#F7DF1E"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" alt="JS"/>JavaScript</div>
        <div class="tech-pill" style="--pill-color:#ED8B00"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" alt="Java"/>Java</div>
        <div class="tech-pill" style="--pill-color:#3670A0"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" alt="Python"/>Python</div>
        <div class="tech-pill" style="--pill-color:#00599C"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/c/c-original.svg" alt="C"/>C</div>
      </div>
    </div>

    <div class="stack-section">
      <div class="stack-category">🌐 Frontend</div>
      <div class="tech-grid">
        <div class="tech-pill" style="--pill-color:#61DAFB"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg" alt="React"/>React</div>
        <div class="tech-pill" style="--pill-color:#646CFF"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vite/vite-original.svg" alt="Vite"/>Vite</div>
        <div class="tech-pill" style="--pill-color:#38B2AC">🌊 TailwindCSS</div>
        <div class="tech-pill" style="--pill-color:#8511FA"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bootstrap/bootstrap-original.svg" alt="Bootstrap"/>Bootstrap</div>
        <div class="tech-pill" style="--pill-color:#E34F26"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg" alt="HTML5"/>HTML5</div>
        <div class="tech-pill" style="--pill-color:#1572B6"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg" alt="CSS3"/>CSS3</div>
      </div>
    </div>

    <div class="stack-section">
      <div class="stack-category">⚙️ Backend</div>
      <div class="tech-grid">
        <div class="tech-pill" style="--pill-color:#6DA55F"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg" alt="Node"/>Node.js</div>
        <div class="tech-pill" style="--pill-color:#aaa">🚂 Express.js</div>
        <div class="tech-pill" style="--pill-color:#fff">🔌 Socket.io</div>
        <div class="tech-pill" style="--pill-color:#FF6C37">📮 REST API</div>
      </div>
    </div>

    <div class="stack-section">
      <div class="stack-category">🗄️ Databases</div>
      <div class="tech-grid">
        <div class="tech-pill" style="--pill-color:#4EA94B"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mongodb/mongodb-original.svg" alt="MongoDB"/>MongoDB</div>
        <div class="tech-pill" style="--pill-color:#4479A1"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg" alt="MySQL"/>MySQL</div>
        <div class="tech-pill" style="--pill-color:#316192"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg" alt="Postgres"/>PostgreSQL</div>
      </div>
    </div>

    <div class="stack-section">
      <div class="stack-category">🚀 DevOps & Hosting</div>
      <div class="tech-grid">
        <div class="tech-pill" style="--pill-color:#0DB7ED"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" alt="Docker"/>Docker</div>
        <div class="tech-pill" style="--pill-color:#FF9900">☁️ AWS</div>
        <div class="tech-pill" style="--pill-color:#FFCA28">🔥 Firebase</div>
        <div class="tech-pill" style="--pill-color:#fff">▲ Vercel</div>
        <div class="tech-pill" style="--pill-color:#00C7B7">🟢 Netlify</div>
        <div class="tech-pill" style="--pill-color:#46E3B7">🎯 Render</div>
      </div>
    </div>

    <div class="stack-section">
      <div class="stack-category">🛠 Tools</div>
      <div class="tech-grid">
        <div class="tech-pill" style="--pill-color:#F05033"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" alt="Git"/>Git</div>
        <div class="tech-pill" style="--pill-color:#fff"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" alt="GitHub"/>GitHub</div>
        <div class="tech-pill" style="--pill-color:#FF6C37">📮 Postman</div>
        <div class="tech-pill" style="--pill-color:#fff">📝 Notion</div>
        <div class="tech-pill" style="--pill-color:#0078D4"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg" alt="VSCode"/>VS Code</div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── GITHUB STATS ── -->
  <section id="stats">
    <div class="section-label">// 04 — github_stats</div>
    <h2 class="section-title">By the Numbers 📊</h2>
    <div class="stats-grid">
      <div class="stat-img">
        <img src="https://github-readme-stats.vercel.app/api?username=AbhinavSharma0188&show_icons=true&theme=tokyonight&hide_border=true&include_all_commits=true&count_private=true" alt="GitHub Stats"/>
      </div>
      <div class="stat-img">
        <img src="https://streak-stats.demolab.com?user=AbhinavSharma0188&theme=tokyonight&hide_border=true" alt="Streak Stats"/>
      </div>
      <div class="stat-img full">
        <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=AbhinavSharma0188&theme=tokyonight&hide_border=true&layout=compact&langs_count=8" alt="Top Languages"/>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── CONTRIBUTION ── -->
  <section id="contrib">
    <div class="section-label">// 05 — contribution_graph</div>
    <h2 class="section-title">Activity Graph 📈</h2>
    <div class="contrib-wrap">
      <img src="https://github-readme-activity-graph.vercel.app/graph?username=AbhinavSharma0188&bg_color=1a1b27&color=38b2ac&line=38b2ac&point=ffffff&area=true&hide_border=true" alt="Contribution Graph"/>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── LEETCODE ── -->
  <section id="leetcode">
    <div class="section-label">// 05b — leetcode_stats</div>
    <h2 class="section-title">LeetCode Grind 🧩</h2>
    <div id="lc-content">
      <div class="lc-loading">
        <div class="lc-spinner"></div>
        <span>Fetching live LeetCode data...</span>
      </div>
    </div>
    <div style="text-align:center;margin-top:20px;">
      <a href="https://leetcode.com/u/Abhinav3614/" target="_blank" class="lc-link-btn">
        🔗 View Full LeetCode Profile ↗
      </a>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── CURRENTLY WORKING ── -->
  <section id="working">
    <div class="section-label">// 06 — currently_working_on</div>
    <h2 class="section-title">What I'm Up To 🎯</h2>
    <div class="work-grid">
      <div class="work-card" style="--accent:#38b2ac">
        <div class="work-icon">🔨</div>
        <div>
          <div class="work-title">Building</div>
          <div class="work-desc">A full-stack scalable web app with MERN + Socket.io real-time features</div>
        </div>
      </div>
      <div class="work-card" style="--accent:#818cf8">
        <div class="work-icon">📖</div>
        <div>
          <div class="work-title">Learning</div>
          <div class="work-desc">Advanced DSA, System Design & AWS Architecture patterns</div>
        </div>
      </div>
      <div class="work-card" style="--accent:#f472b6">
        <div class="work-icon">🎯</div>
        <div>
          <div class="work-title">Goal</div>
          <div class="work-desc">Land a Full Stack Developer role at a top product company</div>
        </div>
      </div>
      <div class="work-card" style="--accent:#fbbf24">
        <div class="work-icon">💡</div>
        <div>
          <div class="work-title">Exploring</div>
          <div class="work-desc">Docker, CI/CD Pipelines & Microservices architecture</div>
        </div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── QUOTE ── -->
  <section id="quote">
    <div class="quote-box">
      <div class="quote-text">
        <span>"</span>Code. Break. <span>Learn.</span><br/>Improve. <span>Repeat.</span><span>"</span>
      </div>
      <div class="quote-sub">— Abhinav's Dev Mantra ⚡</div>
    </div>
  </section>

</div>

<!-- ── FOOTER ── -->
<footer>
  <p>⭐ If you find my work useful, <strong>star my repos!</strong> &nbsp;|&nbsp; Built with ❤️ by <strong>Abhinav Sharma</strong></p>
  <p style="margin-top:8px;">
    <a href="https://github.com/AbhinavSharma0188" style="color:var(--teal);text-decoration:none;" target="_blank">@AbhinavSharma0188</a>
  </p>
</footer>

<script>
/* ── Cursor ── */
const cursor = document.getElementById('cursor');
const trail = document.getElementById('cursor-trail');
let mx = 0, my = 0, tx = 0, ty = 0;
document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; cursor.style.left = mx+'px'; cursor.style.top = my+'px'; });
setInterval(() => {
  tx += (mx - tx) * .12; ty += (my - ty) * .12;
  trail.style.left = tx+'px'; trail.style.top = ty+'px';
}, 16);

/* ── Canvas particles ── */
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H, stars = [];
function resize() { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; }
resize(); window.addEventListener('resize', resize);
for (let i = 0; i < 120; i++) {
  stars.push({ x: Math.random()*1920, y: Math.random()*1080, r: Math.random()*1.2+.3, speed: Math.random()*.4+.1, alpha: Math.random() });
}
function drawCanvas() {
  ctx.clearRect(0,0,W,H);
  stars.forEach(s => {
    s.alpha += .005 * (Math.random()>.5?1:-1);
    s.alpha = Math.max(.1, Math.min(.8, s.alpha));
    s.y -= s.speed;
    if (s.y < 0) { s.y = H; s.x = Math.random()*W; }
    ctx.beginPath();
    ctx.arc(s.x%W, s.y%H, s.r, 0, Math.PI*2);
    ctx.fillStyle = `rgba(56,178,172,${s.alpha})`;
    ctx.fill();
  });
  requestAnimationFrame(drawCanvas);
}
drawCanvas();

/* ── Typewriter ── */
const lines = [
  "Hey there! I'm Abhinav Sharma 👋",
  "Full Stack MERN Developer 🚀",
  "Building Scalable & Production-Ready Apps",
  "Open to Exciting Opportunities 💼",
  "Let's Build Something Amazing Together!"
];
let li = 0, ci = 0, deleting = false;
const el = document.getElementById('typewriter');
function type() {
  const current = lines[li];
  if (!deleting) {
    el.textContent = current.slice(0, ++ci);
    if (ci === current.length) { deleting = true; setTimeout(type, 1800); return; }
  } else {
    el.textContent = current.slice(0, --ci);
    if (ci === 0) { deleting = false; li = (li+1)%lines.length; }
  }
  setTimeout(type, deleting ? 40 : 60);
}
type();

/* ── Scroll reveal ── */
const sections = document.querySelectorAll('section:not(.hero)');
const io = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); } });
}, { threshold: .12 });
sections.forEach(s => io.observe(s));

/* ── LeetCode Live Data ── */
async function fetchLeetCode() {
  const username = 'Abhinav3614';
  const container = document.getElementById('lc-content');

  try {
    // Use LeetCode GraphQL API via a public proxy
    const res = await fetch(`https://leetcode-stats-api.herokuapp.com/${username}`);
    let data = null;
    if (res.ok) {
      data = await res.json();
    }

    // Fallback: try tashif API
    if (!data || data.status === 'error') {
      const res2 = await fetch(`https://leetcode-stats.tashif.codes/${username}`);
      if (res2.ok) data = await res2.json();
    }

    if (!data || data.status === 'error') throw new Error('API unavailable');

    renderLeetCode(data, container, username);
  } catch(e) {
    // Render with placeholder/static data gracefully
    renderLeetCode({
      totalSolved: '—', totalQuestions: 3000,
      easySolved: '—', totalEasy: 800,
      mediumSolved: '—', totalMedium: 1600,
      hardSolved: '—', totalHard: 600,
      acceptanceRate: '—', ranking: '—',
      contributionPoints: '—', reputation: '—',
      _fallback: true
    }, container, username);
  }
}

function renderLeetCode(d, container, username) {
  const total = d.totalSolved;
  const totalQ = d.totalQuestions || 3000;
  const easy = d.easySolved;
  const easyT = d.totalEasy || 800;
  const med = d.mediumSolved;
  const medT = d.totalMedium || 1600;
  const hard = d.hardSolved;
  const hardT = d.totalHard || 600;
  const acc = typeof d.acceptanceRate === 'number' ? d.acceptanceRate.toFixed(1)+'%' : '—';
  const rank = d.ranking ? '#' + Number(d.ranking).toLocaleString() : '—';
  const contrib = d.contributionPoints || '—';

  const pct = typeof total === 'number' ? Math.round((total / totalQ) * 100) : 0;
  const easyPct = typeof easy === 'number' && easyT ? Math.round((easy/easyT)*100) : 0;
  const medPct  = typeof med  === 'number' && medT  ? Math.round((med/medT)*100)  : 0;
  const hardPct = typeof hard === 'number' && hardT ? Math.round((hard/hardT)*100): 0;

  // Donut SVG
  const R = 46, CX = 55, CY = 55, circ = 2 * Math.PI * R;
  const filledLen = circ * (pct / 100);

  const noteHtml = d._fallback
    ? `<p style="font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--muted);text-align:center;margin-top:8px;">⚠️ Live API unavailable. Stats shown are placeholders.</p>`
    : '';

  container.innerHTML = `
    ${noteHtml}
    <div class="lc-hero">
      <!-- Profile card -->
      <div class="lc-profile-card">
        <div class="lc-avatar">⚡</div>
        <div class="lc-username">${username}</div>
        <div class="lc-rank">Global Rank: <span>${rank}</span></div>
        <div style="font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--muted);margin-top:4px;">Acceptance Rate</div>
        <div style="font-family:'Syne',sans-serif;font-weight:800;font-size:28px;color:var(--teal);">${acc}</div>
        <div style="width:100%;height:1px;background:var(--border);margin:4px 0;"></div>
        <div style="font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--muted);">Contribution Points</div>
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:20px;color:var(--purple);">${contrib}</div>
      </div>

      <!-- Donut card -->
      <div class="lc-donut-card">
        <div class="lc-donut-wrap">
          <svg width="110" height="110" viewBox="0 0 110 110">
            <circle cx="${CX}" cy="${CY}" r="${R}" fill="none" stroke="rgba(255,255,255,.05)" stroke-width="10"/>
            <circle id="lc-donut-arc" cx="${CX}" cy="${CY}" r="${R}" fill="none"
              stroke="url(#lcGrad)" stroke-width="10"
              stroke-dasharray="${circ}"
              stroke-dashoffset="${circ}"
              stroke-linecap="round"/>
            <defs>
              <linearGradient id="lcGrad" x1="0%" y1="0%" x2="100%" y2="0%">
                <stop offset="0%" stop-color="#38b2ac"/>
                <stop offset="100%" stop-color="#818cf8"/>
              </linearGradient>
            </defs>
          </svg>
          <div class="lc-donut-center">
            <div class="lc-donut-num" id="lc-solved-num">0</div>
            <div class="lc-donut-label">solved</div>
          </div>
        </div>
        <div class="lc-breakdown">
          <div class="lc-diff-row">
            <div class="lc-diff-dot" style="background:#34d399;"></div>
            <div class="lc-diff-info">
              <div class="lc-diff-name" style="color:#34d399;">Easy</div>
              <div class="lc-diff-bar-wrap"><div class="lc-diff-bar" id="bar-easy" style="background:#34d399;"></div></div>
            </div>
            <div class="lc-diff-count" style="color:#34d399;">${easy}<span style="color:var(--muted);font-size:10px;">/${easyT}</span></div>
          </div>
          <div class="lc-diff-row">
            <div class="lc-diff-dot" style="background:#fbbf24;"></div>
            <div class="lc-diff-info">
              <div class="lc-diff-name" style="color:#fbbf24;">Medium</div>
              <div class="lc-diff-bar-wrap"><div class="lc-diff-bar" id="bar-med" style="background:#fbbf24;"></div></div>
            </div>
            <div class="lc-diff-count" style="color:#fbbf24;">${med}<span style="color:var(--muted);font-size:10px;">/${medT}</span></div>
          </div>
          <div class="lc-diff-row">
            <div class="lc-diff-dot" style="background:#f87171;"></div>
            <div class="lc-diff-info">
              <div class="lc-diff-name" style="color:#f87171;">Hard</div>
              <div class="lc-diff-bar-wrap"><div class="lc-diff-bar" id="bar-hard" style="background:#f87171;"></div></div>
            </div>
            <div class="lc-diff-count" style="color:#f87171;">${hard}<span style="color:var(--muted);font-size:10px;">/${hardT}</span></div>
          </div>
          <div style="margin-top:8px;font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--muted);">
            <span style="color:var(--teal);">${pct}%</span> of total problems cracked
          </div>
        </div>
      </div>
    </div>

    <!-- Stats row -->
    <div class="lc-stats-row">
      <div class="lc-stat-box" style="--stat-color:#34d399;">
        <div class="lc-stat-val" style="color:#34d399;">${easy}</div>
        <div class="lc-stat-lbl">Easy</div>
      </div>
      <div class="lc-stat-box" style="--stat-color:#fbbf24;">
        <div class="lc-stat-val" style="color:#fbbf24;">${med}</div>
        <div class="lc-stat-lbl">Medium</div>
      </div>
      <div class="lc-stat-box" style="--stat-color:#f87171;">
        <div class="lc-stat-val" style="color:#f87171;">${hard}</div>
        <div class="lc-stat-lbl">Hard</div>
      </div>
      <div class="lc-stat-box" style="--stat-color:#818cf8;">
        <div class="lc-stat-val" style="color:#818cf8;">${total}</div>
        <div class="lc-stat-lbl">Total</div>
      </div>
    </div>
  `;

  // Animate donut
  requestAnimationFrame(() => {
    const arc = document.getElementById('lc-donut-arc');
    if (arc) {
      setTimeout(() => {
        arc.style.transition = 'stroke-dashoffset 1.6s cubic-bezier(.4,0,.2,1)';
        arc.style.strokeDashoffset = circ - filledLen;
      }, 300);
    }

    // Animate bars
    setTimeout(() => {
      const be = document.getElementById('bar-easy');
      const bm = document.getElementById('bar-med');
      const bh = document.getElementById('bar-hard');
      if (be) be.style.width = easyPct + '%';
      if (bm) bm.style.width = medPct + '%';
      if (bh) bh.style.width = hardPct + '%';
    }, 400);

    // Count-up animation for total
    const numEl = document.getElementById('lc-solved-num');
    if (numEl && typeof total === 'number') {
      let count = 0;
      const step = Math.ceil(total / 60);
      const interval = setInterval(() => {
        count = Math.min(count + step, total);
        numEl.textContent = count;
        if (count >= total) clearInterval(interval);
      }, 25);
    }
  });
}

// Kick off fetch
fetchLeetCode();
</script>
</body>
</html>
