<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Space+Mono:wght@400;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --neon-cyan: #00f5ff;
    --neon-purple: #b44bff;
    --neon-pink: #ff2d78;
    --neon-green: #00ff94;
    --neon-orange: #ff6b35;
    --dark-bg: #05060f;
    --dark-card: #0d0f1e;
    --dark-border: rgba(0, 245, 255, 0.15);
    --text-primary: #e8eaf6;
    --text-muted: #8892b0;
  }

  body {
    background: var(--dark-bg);
    color: var(--text-primary);
    font-family: 'Space Mono', monospace;
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* Animated starfield */
  .starfield {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    pointer-events: none;
    z-index: 0;
    overflow: hidden;
  }
  .star {
    position: absolute;
    background: white;
    border-radius: 50%;
    animation: twinkle var(--dur, 3s) ease-in-out infinite alternate;
  }
  @keyframes twinkle {
    from { opacity: 0.1; transform: scale(0.8); }
    to { opacity: 0.9; transform: scale(1.2); }
  }

  /* Grid lines background */
  .grid-bg {
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,245,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,245,255,0.03) 1px, transparent 1px);
    background-size: 50px 50px;
    pointer-events: none;
    z-index: 0;
  }

  .page-wrapper {
    position: relative;
    z-index: 1;
    max-width: 860px;
    margin: 0 auto;
    padding: 0 20px 60px;
  }

  /* ===== HEADER ===== */
  header {
    background: linear-gradient(135deg, #070b1a 0%, #0d0f2b 50%, #07111a 100%);
    border-bottom: 1px solid var(--dark-border);
    padding: 0;
    position: relative;
    overflow: hidden;
  }
  .header-aurora {
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse 80% 60% at 50% -20%, rgba(180,75,255,0.25) 0%, transparent 70%),
                radial-gradient(ellipse 60% 40% at 80% 50%, rgba(0,245,255,0.12) 0%, transparent 60%),
                radial-gradient(ellipse 50% 50% at 20% 80%, rgba(255,45,120,0.10) 0%, transparent 60%);
    animation: aurora-shift 8s ease-in-out infinite alternate;
  }
  @keyframes aurora-shift {
    from { opacity: 0.7; transform: scale(1); }
    to { opacity: 1; transform: scale(1.05); }
  }
  .header-content {
    position: relative;
    z-index: 2;
    max-width: 860px;
    margin: 0 auto;
    padding: 28px 20px 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 16px;
    flex-wrap: wrap;
  }
  .header-brand {
    display: flex;
    align-items: center;
    gap: 14px;
  }
  .header-avatar {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--neon-purple), var(--neon-cyan));
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Orbitron', monospace;
    font-weight: 900;
    font-size: 18px;
    color: #fff;
    animation: avatar-pulse 3s ease-in-out infinite;
    flex-shrink: 0;
  }
  @keyframes avatar-pulse {
    0%, 100% { box-shadow: 0 0 0 0 rgba(180,75,255,0.4), 0 0 20px rgba(0,245,255,0.3); }
    50% { box-shadow: 0 0 0 8px rgba(180,75,255,0), 0 0 40px rgba(0,245,255,0.5); }
  }
  .header-title {
    font-family: 'Orbitron', monospace;
    font-size: clamp(14px, 3vw, 20px);
    font-weight: 700;
    background: linear-gradient(90deg, var(--neon-cyan), var(--neon-purple));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    letter-spacing: 1px;
  }
  .header-subtitle {
    font-size: 11px;
    color: var(--text-muted);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-top: 2px;
  }
  .header-nav {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  .nav-btn {
    padding: 7px 14px;
    border-radius: 6px;
    font-size: 11px;
    font-family: 'Space Mono', monospace;
    font-weight: 700;
    text-decoration: none;
    letter-spacing: 1px;
    text-transform: uppercase;
    transition: all 0.25s ease;
    cursor: pointer;
    border: none;
  }
  .nav-btn-outline {
    background: transparent;
    border: 1px solid var(--dark-border);
    color: var(--text-muted);
  }
  .nav-btn-outline:hover {
    border-color: var(--neon-cyan);
    color: var(--neon-cyan);
    box-shadow: 0 0 12px rgba(0,245,255,0.2);
  }
  .nav-btn-filled {
    background: linear-gradient(135deg, var(--neon-purple), var(--neon-pink));
    color: white;
    border: 1px solid transparent;
  }
  .nav-btn-filled:hover {
    box-shadow: 0 0 20px rgba(180,75,255,0.5);
    transform: translateY(-1px);
  }

  /* ===== HERO SECTION ===== */
  .hero {
    padding: 70px 0 50px;
    text-align: center;
    position: relative;
  }
  .hero-badge {
    display: inline-block;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--neon-cyan);
    border: 1px solid rgba(0,245,255,0.3);
    border-radius: 100px;
    padding: 5px 16px;
    margin-bottom: 28px;
    animation: badge-glow 2s ease-in-out infinite alternate;
  }
  @keyframes badge-glow {
    from { box-shadow: 0 0 8px rgba(0,245,255,0.2); }
    to { box-shadow: 0 0 20px rgba(0,245,255,0.5); }
  }
  .hero-emoji {
    font-size: 56px;
    display: block;
    animation: wave 2.5s ease-in-out infinite;
    margin-bottom: 16px;
  }
  @keyframes wave {
    0%, 100% { transform: rotate(0deg); }
    20% { transform: rotate(20deg); }
    40% { transform: rotate(-10deg); }
    60% { transform: rotate(16deg); }
    80% { transform: rotate(-8deg); }
  }
  .hero-name {
    font-family: 'Orbitron', monospace;
    font-size: clamp(28px, 6vw, 52px);
    font-weight: 900;
    background: linear-gradient(135deg, #fff 0%, var(--neon-cyan) 40%, var(--neon-purple) 70%, var(--neon-pink) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1.1;
    margin-bottom: 10px;
    animation: name-shimmer 4s linear infinite;
    background-size: 200% auto;
  }
  @keyframes name-shimmer {
    from { background-position: 0% center; }
    to { background-position: 200% center; }
  }
  .hero-role {
    font-family: 'Syne', sans-serif;
    font-size: clamp(14px, 2.5vw, 20px);
    font-weight: 600;
    color: var(--text-muted);
    letter-spacing: 2px;
    margin-bottom: 20px;
  }
  .hero-role span {
    color: var(--neon-purple);
  }
  .hero-tagline {
    font-size: 14px;
    color: var(--text-muted);
    line-height: 1.8;
    max-width: 520px;
    margin: 0 auto 36px;
  }
  .hero-tagline strong {
    color: var(--neon-cyan);
  }
  .hero-cta {
    display: flex;
    gap: 12px;
    justify-content: center;
    flex-wrap: wrap;
  }
  .cta-btn {
    padding: 11px 24px;
    border-radius: 8px;
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 1px;
    text-decoration: none;
    text-transform: uppercase;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .cta-primary {
    background: linear-gradient(135deg, var(--neon-purple), var(--neon-cyan));
    color: #fff;
    border: none;
  }
  .cta-primary:hover {
    box-shadow: 0 0 30px rgba(0,245,255,0.4), 0 0 60px rgba(180,75,255,0.2);
    transform: translateY(-2px);
  }
  .cta-secondary {
    background: transparent;
    border: 1px solid var(--dark-border);
    color: var(--text-muted);
  }
  .cta-secondary:hover {
    border-color: var(--neon-green);
    color: var(--neon-green);
    box-shadow: 0 0 16px rgba(0,255,148,0.2);
    transform: translateY(-2px);
  }

  /* ===== TYPING ANIMATION ===== */
  .typing-text {
    display: inline;
    color: var(--neon-green);
  }
  .cursor {
    display: inline-block;
    width: 2px;
    height: 1em;
    background: var(--neon-green);
    margin-left: 2px;
    vertical-align: middle;
    animation: blink 1s step-end infinite;
  }
  @keyframes blink { 50% { opacity: 0; } }

  /* ===== SECTION STYLES ===== */
  .section {
    margin: 60px 0;
    animation: section-fade-up 0.6s ease both;
  }
  @keyframes section-fade-up {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }
  .section-header {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 28px;
  }
  .section-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--dark-border), transparent);
  }
  .section-label {
    font-family: 'Orbitron', monospace;
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--neon-cyan);
  }
  .section-num {
    color: var(--neon-purple);
    margin-right: 6px;
  }

  /* ===== SKILLS GRID ===== */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 12px;
  }
  .skill-pill {
    background: var(--dark-card);
    border: 1px solid var(--dark-border);
    border-radius: 10px;
    padding: 14px 12px;
    text-align: center;
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 0.5px;
    transition: all 0.3s ease;
    cursor: default;
    position: relative;
    overflow: hidden;
  }
  .skill-pill::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--skill-color, var(--neon-cyan));
    opacity: 0;
    transition: opacity 0.3s ease;
    border-radius: inherit;
  }
  .skill-pill:hover::before { opacity: 0.08; }
  .skill-pill:hover {
    border-color: var(--skill-color, var(--neon-cyan));
    transform: translateY(-3px);
    box-shadow: 0 8px 24px rgba(0,0,0,0.4);
  }
  .skill-icon { font-size: 22px; display: block; margin-bottom: 6px; }
  .skill-name { color: var(--text-primary); position: relative; z-index: 1; }

  /* ===== BADGES ROW ===== */
  .badges-row {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  .badge {
    padding: 8px 16px;
    border-radius: 8px;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 1px;
    text-transform: uppercase;
    border: 1px solid transparent;
    animation: badge-float 4s ease-in-out infinite;
  }
  .badge:nth-child(2) { animation-delay: 0.5s; }
  .badge:nth-child(3) { animation-delay: 1s; }
  .badge:nth-child(4) { animation-delay: 1.5s; }
  .badge:nth-child(5) { animation-delay: 2s; }
  .badge:nth-child(6) { animation-delay: 2.5s; }
  @keyframes badge-float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-4px); }
  }
  .badge-frontend { background: rgba(0,245,255,0.08); border-color: rgba(0,245,255,0.3); color: var(--neon-cyan); }
  .badge-backend { background: rgba(0,255,148,0.08); border-color: rgba(0,255,148,0.3); color: var(--neon-green); }
  .badge-db { background: rgba(255,107,53,0.08); border-color: rgba(255,107,53,0.3); color: var(--neon-orange); }
  .badge-ai { background: rgba(255,45,120,0.08); border-color: rgba(255,45,120,0.3); color: var(--neon-pink); }
  .badge-mobile { background: rgba(180,75,255,0.08); border-color: rgba(180,75,255,0.3); color: var(--neon-purple); }
  .badge-tools { background: rgba(14,165,233,0.08); border-color: rgba(14,165,233,0.3); color: #38bdf8; }

  /* ===== STAT CARDS ===== */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 14px;
  }
  .stat-card {
    background: var(--dark-card);
    border: 1px solid var(--dark-border);
    border-radius: 12px;
    padding: 20px 16px;
    text-align: center;
    position: relative;
    overflow: hidden;
    transition: all 0.3s ease;
  }
  .stat-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--card-color, var(--neon-cyan)), transparent);
  }
  .stat-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 30px rgba(0,0,0,0.5);
    border-color: var(--card-color, var(--neon-cyan));
  }
  .stat-value {
    font-family: 'Orbitron', monospace;
    font-size: 28px;
    font-weight: 900;
    color: var(--card-color, var(--neon-cyan));
    display: block;
    margin-bottom: 6px;
    animation: count-up 1s ease both;
  }
  .stat-label {
    font-size: 11px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  /* ===== ABOUT ===== */
  .about-card {
    background: var(--dark-card);
    border: 1px solid var(--dark-border);
    border-radius: 16px;
    padding: 32px;
    position: relative;
    overflow: hidden;
  }
  .about-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--neon-purple), var(--neon-cyan), var(--neon-pink));
    animation: gradient-flow 3s linear infinite;
    background-size: 200% auto;
  }
  @keyframes gradient-flow {
    from { background-position: 0% center; }
    to { background-position: 200% center; }
  }
  .about-text {
    font-size: 14px;
    line-height: 1.9;
    color: var(--text-muted);
  }
  .about-text em {
    color: var(--neon-cyan);
    font-style: normal;
    font-weight: 700;
  }
  .about-text .highlight {
    color: var(--neon-purple);
  }

  /* ===== STREAK / GITHUB ===== */
  .github-section {
    background: var(--dark-card);
    border: 1px solid var(--dark-border);
    border-radius: 16px;
    padding: 24px;
    text-align: center;
    overflow: hidden;
  }
  .github-section img {
    max-width: 100%;
    border-radius: 8px;
  }

  /* ===== CONTACT ===== */
  .contact-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 14px;
  }
  .contact-card {
    background: var(--dark-card);
    border: 1px solid var(--dark-border);
    border-radius: 12px;
    padding: 20px;
    display: flex;
    align-items: center;
    gap: 16px;
    text-decoration: none;
    color: inherit;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  .contact-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--c-color);
    opacity: 0;
    transition: opacity 0.3s;
    border-radius: inherit;
  }
  .contact-card:hover::before { opacity: 0.06; }
  .contact-card:hover {
    border-color: var(--c-color);
    transform: translateY(-3px);
    box-shadow: 0 10px 28px rgba(0,0,0,0.4);
  }
  .contact-icon {
    width: 44px;
    height: 44px;
    border-radius: 10px;
    background: var(--c-bg);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 22px;
    flex-shrink: 0;
    position: relative;
    z-index: 1;
  }
  .contact-info { position: relative; z-index: 1; }
  .contact-label {
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 4px;
  }
  .contact-value {
    font-size: 13px;
    font-weight: 700;
    color: var(--c-color);
    word-break: break-all;
  }

  /* ===== FOOTER ===== */
  footer {
    background: linear-gradient(135deg, #070b1a 0%, #0b0d26 50%, #070c1a 100%);
    border-top: 1px solid var(--dark-border);
    position: relative;
    overflow: hidden;
  }
  .footer-aurora {
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse 80% 80% at 50% 120%, rgba(0,245,255,0.08) 0%, transparent 70%),
                radial-gradient(ellipse 50% 50% at 10% 50%, rgba(180,75,255,0.06) 0%, transparent 60%);
    pointer-events: none;
  }
  .footer-content {
    position: relative;
    z-index: 1;
    max-width: 860px;
    margin: 0 auto;
    padding: 40px 20px;
  }
  .footer-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 20px;
    margin-bottom: 32px;
  }
  .footer-brand {
    font-family: 'Orbitron', monospace;
    font-size: 20px;
    font-weight: 900;
    background: linear-gradient(90deg, var(--neon-cyan), var(--neon-purple));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .footer-links {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
  }
  .footer-link {
    padding: 7px 14px;
    border-radius: 6px;
    font-size: 11px;
    letter-spacing: 1px;
    text-transform: uppercase;
    text-decoration: none;
    border: 1px solid var(--dark-border);
    color: var(--text-muted);
    transition: all 0.25s ease;
  }
  .footer-link:hover {
    color: var(--neon-cyan);
    border-color: rgba(0,245,255,0.4);
    box-shadow: 0 0 12px rgba(0,245,255,0.15);
  }
  .footer-divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--dark-border), transparent);
    margin-bottom: 24px;
  }
  .footer-bottom {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 12px;
  }
  .footer-copy {
    font-size: 12px;
    color: var(--text-muted);
  }
  .footer-copy span { color: var(--neon-pink); }
  .footer-tagline {
    font-size: 12px;
    color: var(--text-muted);
    letter-spacing: 1px;
  }
  .footer-tagline em {
    color: var(--neon-green);
    font-style: normal;
  }

  /* ===== SCROLL PROGRESS ===== */
  .scroll-bar {
    position: fixed;
    top: 0; left: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--neon-purple), var(--neon-cyan), var(--neon-pink));
    z-index: 9999;
    transition: width 0.1s linear;
    width: 0%;
  }

  /* ===== FUN SECTION ===== */
  .fun-card {
    background: var(--dark-card);
    border: 1px solid var(--dark-border);
    border-radius: 16px;
    padding: 24px;
    text-align: center;
    overflow: hidden;
  }
  .fun-card img { max-width: 100%; border-radius: 8px; margin-top: 16px; }

  /* ===== ORBIT ===== */
  .orbit-container {
    position: relative;
    width: 180px;
    height: 180px;
    margin: 0 auto 30px;
  }
  .orbit-center {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    font-family: 'Orbitron', monospace;
    font-size: 13px;
    font-weight: 900;
    color: var(--neon-cyan);
    text-align: center;
    line-height: 1.3;
  }
  .orbit-ring {
    position: absolute;
    inset: 0;
    border: 1px dashed rgba(0,245,255,0.15);
    border-radius: 50%;
    animation: orbit-spin var(--speed, 8s) linear infinite;
  }
  .orbit-ring-2 {
    inset: 20px;
    border-color: rgba(180,75,255,0.15);
    animation-direction: reverse;
    animation-duration: 12s;
  }
  @keyframes orbit-spin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

  /* Reveal animation */
  .reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .reveal.visible { opacity: 1; transform: none; }
</style>
</head>
<body>

<div class="scroll-bar" id="scrollBar"></div>

<!-- Starfield -->
<div class="starfield" id="starfield"></div>
<div class="grid-bg"></div>

<!-- ===== HEADER ===== -->
<header>
  <div class="header-aurora"></div>
  <div class="header-content">
    <div class="header-brand">
      <div class="header-avatar">WY</div>
      <div>
        <div class="header-title">WAHAJ YASIN</div>
        <div class="header-subtitle">Software Engineer &amp; AI Explorer</div>
      </div>
    </div>
    <div class="header-nav">
      <a href="wahajportfolio.pages.dev" class="nav-btn nav-btn-outline">Portfolio ↗</a>
      <a href="https://www.linkedin.com/in/m-wahaj-yasin/" class="nav-btn nav-btn-outline">LinkedIn ↗</a>
      <a href="mailto:wahajrajpoot987654@gmail.com" class="nav-btn nav-btn-filled">Hire Me</a>
    </div>
  </div>
</header>

<!-- ===== PAGE CONTENT ===== -->
<div class="page-wrapper">

  <!-- HERO -->
  <section class="hero">
    <div class="hero-badge">✦ Available for Opportunities</div>
    <span class="hero-emoji">👋</span>
    <h1 class="hero-name">WAHAJ YASIN</h1>
    <p class="hero-role">
      <span id="typed-role"></span><span class="cursor"></span>
    </p>
    <p class="hero-tagline">
      Turning ideas into <strong>scalable products</strong>, intelligent systems &amp; smooth user experiences 🚀<br/>
      I build things that <strong>solve real problems</strong>, automate boring stuff 🤖, and look clean while doing it ✨
    </p>
    <div class="hero-cta">
      <a href="https://wahajportfolio.pages.dev/" class="cta-btn cta-primary">🌐 View Portfolio</a>
      <a href="mailto:wahajrajpoot987654@gmail.com" class="cta-btn cta-secondary">✉ Email Me</a>
    </div>
  </section>

  <!-- TECH BADGES -->
  <section class="section reveal">
    <div class="section-header">
      <span class="section-label"><span class="section-num">01.</span>Tech Stack</span>
      <div class="section-line"></div>
    </div>
    <div class="badges-row" style="margin-bottom: 20px;">
      <span class="badge badge-frontend">Frontend: React · Tailwind · Bootstrap</span>
      <span class="badge badge-backend">Backend: Node.js · Laravel · Express</span>
      <span class="badge badge-db">Databases: MySQL · MongoDB</span>
      <span class="badge badge-ai">AI/ML: YOLO · OpenCV · Python</span>
      <span class="badge badge-mobile">Mobile: Flutter · Firebase</span>
      <span class="badge badge-tools">Tools: Git · GitHub · AWS</span>
    </div>
  </section>

  <!-- SKILLS ICONS -->
  <section class="section reveal">
    <div class="section-header">
      <span class="section-label"><span class="section-num">02.</span>Skills</span>
      <div class="section-line"></div>
    </div>
    <div class="skills-grid" id="skillsGrid"></div>
  </section>

  <!-- ABOUT -->
  <section class="section reveal">
    <div class="section-header">
      <span class="section-label"><span class="section-num">03.</span>About Me</span>
      <div class="section-line"></div>
    </div>
    <div class="about-card">
      <p class="about-text">
        Hey! I'm <em>Wahaj</em> — a passionate <em>Full-Stack Developer</em> and <em>AI Explorer</em> based in <span class="highlight">Pakistan 🇵🇰</span>. I enjoy building things that solve real problems — from <em>scalable web applications</em> to <em>intelligent ML systems</em>.<br/><br/>
        Sometimes I train models 🧠, sometimes I break builds 💥 — but I'm <em>always learning</em>. My stack spans React, Node.js, Laravel, Flutter, Python, and more. Whether it's a <span class="highlight">sleek frontend</span>, a <span class="highlight">robust API</span>, or a <span class="highlight">computer vision pipeline</span>, I bring it to life with clean, purposeful code.<br/><br/>
        <em>Code • Learn • Build • Repeat ⚡</em>
      </p>
    </div>
  </section>

  <!-- STATS -->
  <section class="section reveal">
    <div class="section-header">
      <span class="section-label"><span class="section-num">04.</span>At a Glance</span>
      <div class="section-line"></div>
    </div>
    <div class="stats-grid">
      <div class="stat-card" style="--card-color: var(--neon-cyan);">
        <span class="stat-value" data-target="16">0</span>
        <span class="stat-label">Technologies</span>
      </div>
      <div class="stat-card" style="--card-color: var(--neon-purple);">
        <span class="stat-value" data-target="3">0</span>
        <span class="stat-label">Years Experience</span>
      </div>
      <div class="stat-card" style="--card-color: var(--neon-green);">
        <span class="stat-value" data-target="20">0</span>+
        <span class="stat-label">Projects Built</span>
      </div>
      <div class="stat-card" style="--card-color: var(--neon-pink);">
        <span class="stat-value" data-target="100">0</span>%
        <span class="stat-label">Passion for Code</span>
      </div>
    </div>
  </section>

  <!-- GITHUB STREAK -->
  <section class="section reveal">
    <div class="section-header">
      <span class="section-label"><span class="section-num">05.</span>GitHub Activity</span>
      <div class="section-line"></div>
    </div>
    <div class="github-section">
      <img src="https://github-readme-streak-stats.herokuapp.com/?user=WahajYasin&theme=dracula&hide_border=true" alt="GitHub Streak Stats" loading="lazy"/>
    </div>
  </section>

  <!-- FUN SECTION -->
  <section class="section reveal">
    <div class="section-header">
      <span class="section-label"><span class="section-num">06.</span>Just for Fun 🎮</span>
      <div class="section-line"></div>
    </div>
    <div class="fun-card">
      <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 16px;">Watch the snake eat my contributions 🐍</p>
      <img src="https://github.com/Platane/snk/raw/output/github-contribution-grid-snake.svg" alt="Contribution Snake" loading="lazy"/>
    </div>
  </section>

  <!-- CONTACT -->
  <section class="section reveal">
    <div class="section-header">
      <span class="section-label"><span class="section-num">07.</span>Let's Connect</span>
      <div class="section-line"></div>
    </div>
    <div class="contact-grid">
      <a href="mailto:wahajrajpoot987654@gmail.com" class="contact-card" style="--c-color: #ea4335; --c-bg: rgba(234,67,53,0.1);">
        <div class="contact-icon">📧</div>
        <div class="contact-info">
          <div class="contact-label">Email</div>
          <div class="contact-value">wahajrajpoot987654</div>
        </div>
      </a>
      <a href="https://www.linkedin.com/in/m-wahaj-yasin/" class="contact-card" style="--c-color: #0077b5; --c-bg: rgba(0,119,181,0.1);" target="_blank">
        <div class="contact-icon">💼</div>
        <div class="contact-info">
          <div class="contact-label">LinkedIn</div>
          <div class="contact-value">m-wahaj-yasin</div>
        </div>
      </a>
      <a href="https://wahajportfolio.pages.dev/" class="contact-card" style="--c-color: var(--neon-purple); --c-bg: rgba(180,75,255,0.1);" target="_blank">
        <div class="contact-icon">🌐</div>
        <div class="contact-info">
          <div class="contact-label">Portfolio</div>
          <div class="contact-value">wahajportfolio.pages.dev</div>
        </div>
      </a>
    </div>
  </section>

</div>

<!-- ===== FOOTER ===== -->
<footer>
  <div class="footer-aurora"></div>
  <div class="footer-content">
    <div class="footer-top">
      <div class="footer-brand">WAHAJ YASIN</div>
      <div class="footer-links">
        <a href="https://wahajportfolio.pages.dev/" class="footer-link" target="_blank">Portfolio</a>
        <a href="https://www.linkedin.com/in/m-wahaj-yasin/" class="footer-link" target="_blank">LinkedIn</a>
        <a href="mailto:wahajrajpoot987654@gmail.com" class="footer-link">Email</a>
        <a href="https://github.com/WahajYasin" class="footer-link" target="_blank">GitHub</a>
      </div>
    </div>
    <div class="footer-divider"></div>
    <div class="footer-bottom">
      <p class="footer-copy">© 2025 Wahaj Yasin. Crafted with <span>♥</span> and caffeine.</p>
      <p class="footer-tagline">⚡ Code · Learn · Build · <em>Repeat</em></p>
    </div>
  </div>
</footer>

<script>
// Starfield
const sf = document.getElementById('starfield');
for (let i = 0; i < 120; i++) {
  const s = document.createElement('div');
  s.className = 'star';
  const size = Math.random() * 2.5 + 0.5;
  s.style.cssText = `width:${size}px;height:${size}px;left:${Math.random()*100}%;top:${Math.random()*100}%;--dur:${2+Math.random()*4}s;animation-delay:${Math.random()*4}s`;
  sf.appendChild(s);
}

// Scroll progress
window.addEventListener('scroll', () => {
  const pct = window.scrollY / (document.body.scrollHeight - window.innerHeight) * 100;
  document.getElementById('scrollBar').style.width = pct + '%';
});

// Reveal on scroll
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver(entries => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 80);
      observer.unobserve(e.target);
    }
  });
}, { threshold: 0.1 });
reveals.forEach(r => observer.observe(r));

// Typing animation
const roles = [
  'Software Engineer 💻',
  'Full-Stack Developer 🌐',
  'AI Explorer 🤖',
  'Problem Solver 🧩',
  'Flutter Dev 📱',
];
let roleIdx = 0, charIdx = 0, deleting = false;
const typedEl = document.getElementById('typed-role');
function type() {
  const current = roles[roleIdx];
  if (!deleting) {
    typedEl.textContent = current.slice(0, charIdx + 1);
    charIdx++;
    if (charIdx === current.length) { deleting = true; setTimeout(type, 2000); return; }
  } else {
    typedEl.textContent = current.slice(0, charIdx - 1);
    charIdx--;
    if (charIdx === 0) { deleting = false; roleIdx = (roleIdx + 1) % roles.length; }
  }
  setTimeout(type, deleting ? 60 : 90);
}
type();

// Skills data
const skills = [
  { name: 'React', icon: '⚛️', color: '#61dafb' },
  { name: 'Node.js', icon: '🟢', color: '#68a063' },
  { name: 'Laravel', icon: '🔴', color: '#ff2d20' },
  { name: 'Flutter', icon: '💙', color: '#54c5f8' },
  { name: 'Python', icon: '🐍', color: '#ffd43b' },
  { name: 'JavaScript', icon: '🟡', color: '#f7df1e' },
  { name: 'TypeScript', icon: '🔷', color: '#3178c6' },
  { name: 'MongoDB', icon: '🍃', color: '#4db33d' },
  { name: 'MySQL', icon: '🐬', color: '#4479a1' },
  { name: 'AWS', icon: '☁️', color: '#ff9900' },
  { name: 'Git', icon: '🔀', color: '#f05032' },
  { name: 'GitHub', icon: '🐙', color: '#e0e0e0' },
  { name: 'Tailwind', icon: '🎨', color: '#38bdf8' },
  { name: 'Bootstrap', icon: '🅱️', color: '#7952b3' },
  { name: 'OpenCV', icon: '👁️', color: '#5c3ee8' },
  { name: 'Firebase', icon: '🔥', color: '#ffca28' },
];
const grid = document.getElementById('skillsGrid');
skills.forEach((sk, i) => {
  const d = document.createElement('div');
  d.className = 'skill-pill';
  d.style.setProperty('--skill-color', sk.color);
  d.style.animationDelay = (i * 0.05) + 's';
  d.innerHTML = `<span class="skill-icon">${sk.icon}</span><span class="skill-name">${sk.name}</span>`;
  grid.appendChild(d);
});

// Counter animation
const counters = document.querySelectorAll('.stat-value[data-target]');
const counterObserver = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const target = parseInt(e.target.dataset.target);
      let current = 0;
      const step = Math.ceil(target / 30);
      const interval = setInterval(() => {
        current = Math.min(current + step, target);
        e.target.textContent = current;
        if (current >= target) clearInterval(interval);
      }, 40);
      counterObserver.unobserve(e.target);
    }
  });
}, { threshold: 0.5 });
counters.forEach(c => counterObserver.observe(c));
</script>
</body>
</html>
