# portfoliodev
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Tapon Kumer Ray — Research Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;600;700;800&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet" />

<style>
  :root {
    --bg: #07080d;
    --bg2: #0c0e18;
    --bg3: #111428;
    --card: #0f1120;
    --border: rgba(99, 139, 255, 0.18);
    --accent: #638bff;
    --accent2: #a78bfa;
    --accent3: #34d399;
    --amber: #fbbf24;
    --text: #e2e8f8;
    --muted: #7280a8;
    --dim: #3d4a6b;
    --glow: rgba(99,139,255,0.3);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Syne', sans-serif;
    background: var(--bg);
    color: var(--text);
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s ease;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid rgba(99,139,255,0.5);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%,-50%);
    transition: all 0.18s ease;
  }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.035'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1;
    opacity: 0.6;
  }

  /* Grid background */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(99,139,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(99,139,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
  }

  /* NAVIGATION */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.4rem 3rem;
    background: rgba(7,8,13,0.7);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }
  .nav-logo {
    font-family: 'Space Mono', monospace;
    font-size: 0.78rem;
    color: var(--accent);
    letter-spacing: 0.15em;
    text-transform: uppercase;
  }
  .nav-links {
    display: flex;
    gap: 2.5rem;
    list-style: none;
  }
  .nav-links a {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--accent); }

  .nav-status {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    color: var(--accent3);
    letter-spacing: 0.1em;
  }
  .status-dot {
    width: 6px; height: 6px;
    background: var(--accent3);
    border-radius: 50%;
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.7); }
  }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 8rem 3rem 4rem;
    position: relative;
    z-index: 2;
    max-width: 1300px;
    margin: 0 auto;
  }

  .hero-tag {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    color: var(--accent);
    letter-spacing: 0.25em;
    text-transform: uppercase;
    margin-bottom: 2rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.2s forwards;
  }

  .hero-name {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(3.5rem, 8vw, 7.5rem);
    line-height: 0.92;
    color: var(--text);
    margin-bottom: 1rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.35s forwards;
  }

  .hero-name span {
    display: block;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-desc {
    max-width: 560px;
    margin: 2rem 0 3rem;
    font-size: 1.05rem;
    line-height: 1.75;
    color: var(--muted);
    opacity: 0;
    animation: fadeUp 0.8s 0.5s forwards;
  }

  .hero-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
    margin-bottom: 3.5rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.65s forwards;
  }
  .tag {
    font-family: 'Space Mono', monospace;
    font-size: 0.68rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    padding: 0.4rem 1rem;
    border: 1px solid var(--border);
    border-radius: 2px;
    color: var(--muted);
    background: rgba(99,139,255,0.04);
    transition: all 0.2s;
  }
  .tag:hover { border-color: var(--accent); color: var(--accent); background: rgba(99,139,255,0.1); }

  .hero-cta {
    display: flex;
    gap: 1.5rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
  }
  .btn-primary {
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    padding: 1rem 2.2rem;
    background: var(--accent);
    color: var(--bg);
    border: none;
    border-radius: 2px;
    cursor: none;
    text-decoration: none;
    transition: all 0.2s;
    font-weight: 700;
  }
  .btn-primary:hover { background: var(--accent2); transform: translateY(-2px); box-shadow: 0 8px 30px var(--glow); }

  .btn-ghost {
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    padding: 1rem 2.2rem;
    background: transparent;
    color: var(--accent);
    border: 1px solid var(--border);
    border-radius: 2px;
    cursor: none;
    text-decoration: none;
    transition: all 0.2s;
  }
  .btn-ghost:hover { border-color: var(--accent); background: rgba(99,139,255,0.08); }

  /* floating decorators */
  .hero-deco {
    position: absolute;
    right: 3rem;
    top: 50%;
    transform: translateY(-50%);
    width: 400px;
    height: 400px;
    opacity: 0;
    animation: fadeIn 1.5s 1s forwards;
  }
  .hero-deco svg { width: 100%; height: 100%; }

  .orbital-ring {
    animation: rotate 20s linear infinite;
    transform-origin: center;
  }
  .orbital-ring2 {
    animation: rotate 14s linear infinite reverse;
    transform-origin: center;
  }
  @keyframes rotate {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  /* SECTION BASE */
  section {
    position: relative;
    z-index: 2;
    max-width: 1300px;
    margin: 0 auto;
    padding: 6rem 3rem;
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 1.5rem;
    margin-bottom: 4rem;
  }
  .section-num {
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    color: var(--accent);
    letter-spacing: 0.2em;
  }
  .section-line {
    width: 60px;
    height: 1px;
    background: var(--border);
  }
  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1.8rem, 4vw, 3rem);
    font-weight: 800;
    color: var(--text);
    letter-spacing: -0.02em;
  }
  .section-divider {
    border: none;
    border-top: 1px solid var(--border);
    max-width: 1300px;
    margin: 0 auto;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; } to { opacity: 1; }
  }

  /* ABOUT / STATS */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1.5px;
    margin-bottom: 4rem;
    border: 1.5px solid var(--border);
    overflow: hidden;
    border-radius: 4px;
  }
  .stat-card {
    background: var(--card);
    padding: 2.5rem 2rem;
    border-right: 1.5px solid var(--border);
    position: relative;
    overflow: hidden;
    transition: background 0.3s;
  }
  .stat-card:last-child { border-right: none; }
  .stat-card:hover { background: rgba(99,139,255,0.06); }
  .stat-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transition: transform 0.3s;
  }
  .stat-card:hover::after { transform: scaleX(1); }
  .stat-num {
    font-family: 'DM Serif Display', serif;
    font-size: 3.2rem;
    color: var(--accent);
    line-height: 1;
    margin-bottom: 0.5rem;
  }
  .stat-label {
    font-family: 'Space Mono', monospace;
    font-size: 0.68rem;
    color: var(--muted);
    letter-spacing: 0.12em;
    text-transform: uppercase;
  }

  /* RESEARCH EXPERIENCE */
  .timeline {
    display: flex;
    flex-direction: column;
    gap: 0;
    position: relative;
  }
  .timeline::before {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    width: 1px;
    background: linear-gradient(to bottom, var(--accent), var(--accent2), transparent);
  }
  .timeline-item {
    padding: 0 0 3.5rem 3rem;
    position: relative;
  }
  .timeline-item::before {
    content: '';
    position: absolute;
    left: -4.5px;
    top: 6px;
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    border: 2px solid var(--bg);
    box-shadow: 0 0 12px var(--glow);
  }
  .timeline-date {
    font-family: 'Space Mono', monospace;
    font-size: 0.68rem;
    color: var(--accent);
    letter-spacing: 0.15em;
    margin-bottom: 0.75rem;
  }
  .timeline-role {
    font-family: 'Syne', sans-serif;
    font-size: 1.25rem;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 0.25rem;
  }
  .timeline-org {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    color: var(--muted);
    margin-bottom: 1.25rem;
    letter-spacing: 0.08em;
  }
  .timeline-bullets {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  .timeline-bullets li {
    font-size: 0.9rem;
    color: var(--muted);
    line-height: 1.65;
    padding-left: 1.2rem;
    position: relative;
  }
  .timeline-bullets li::before {
    content: '→';
    position: absolute;
    left: 0;
    color: var(--accent);
    font-size: 0.75rem;
  }

  /* PUBLICATIONS */
  .pub-grid {
    display: flex;
    flex-direction: column;
    gap: 1.5px;
    border: 1.5px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .pub-card {
    background: var(--card);
    padding: 2rem 2.5rem;
    border-bottom: 1px solid var(--border);
    display: grid;
    grid-template-columns: auto 1fr auto;
    gap: 2rem;
    align-items: start;
    transition: background 0.3s;
    position: relative;
  }
  .pub-card:last-child { border-bottom: none; }
  .pub-card:hover { background: rgba(99,139,255,0.05); }
  .pub-card::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 3px;
    background: linear-gradient(to bottom, var(--accent), var(--accent2));
    transform: scaleY(0);
    transition: transform 0.3s;
  }
  .pub-card:hover::before { transform: scaleY(1); }
  .pub-num {
    font-family: 'DM Serif Display', serif;
    font-size: 2.2rem;
    color: var(--dim);
    line-height: 1;
    min-width: 40px;
  }
  .pub-title {
    font-family: 'Syne', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 0.4rem;
    line-height: 1.4;
  }
  .pub-venue {
    font-family: 'Space Mono', monospace;
    font-size: 0.68rem;
    color: var(--muted);
    letter-spacing: 0.1em;
  }
  .pub-badge {
    font-family: 'Space Mono', monospace;
    font-size: 0.62rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.3rem 0.8rem;
    border-radius: 2px;
    white-space: nowrap;
    align-self: center;
  }
  .badge-review {
    background: rgba(251,191,36,0.1);
    color: var(--amber);
    border: 1px solid rgba(251,191,36,0.3);
  }
  .badge-published {
    background: rgba(52,211,153,0.1);
    color: var(--accent3);
    border: 1px solid rgba(52,211,153,0.3);
  }
  .badge-presented {
    background: rgba(167,139,250,0.1);
    color: var(--accent2);
    border: 1px solid rgba(167,139,250,0.3);
  }

  /* PROJECTS */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5px;
    border: 1.5px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .project-card {
    background: var(--card);
    padding: 2.5rem 2rem;
    position: relative;
    overflow: hidden;
    transition: background 0.3s;
  }
  .project-card:hover { background: rgba(99,139,255,0.06); }
  .project-card::after {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s;
  }
  .project-card:hover::after { transform: scaleX(1); }
  .project-icon {
    width: 48px; height: 48px;
    border: 1px solid var(--border);
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 1.5rem;
    font-size: 1.4rem;
    background: rgba(99,139,255,0.06);
  }
  .project-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.05rem;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 0.75rem;
    line-height: 1.35;
  }
  .project-desc {
    font-size: 0.85rem;
    color: var(--muted);
    line-height: 1.7;
    margin-bottom: 1.5rem;
  }
  .tech-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
  }
  .tech-chip {
    font-family: 'Space Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.08em;
    padding: 0.2rem 0.6rem;
    border: 1px solid var(--border);
    border-radius: 2px;
    color: var(--dim);
    text-transform: uppercase;
  }
  .project-card:nth-child(3n+2) { border-left: 1.5px solid var(--border); border-right: 1.5px solid var(--border); }

  /* SKILLS */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5px;
    border: 1.5px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .skill-group {
    background: var(--card);
    padding: 2.5rem 2rem;
    border-right: 1.5px solid var(--border);
  }
  .skill-group:nth-child(2n) { border-right: none; }
  .skill-group:nth-last-child(-n+2) { border-top: 1.5px solid var(--border); }
  .skill-group-title {
    font-family: 'Space Mono', monospace;
    font-size: 0.68rem;
    color: var(--accent);
    letter-spacing: 0.18em;
    text-transform: uppercase;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }
  .skill-group-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }
  .skill-chips {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }
  .skill-chip {
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    padding: 0.45rem 0.9rem;
    border: 1px solid var(--border);
    border-radius: 2px;
    color: var(--muted);
    background: rgba(99,139,255,0.03);
    transition: all 0.2s;
    letter-spacing: 0.06em;
  }
  .skill-chip:hover { border-color: var(--accent); color: var(--accent); background: rgba(99,139,255,0.1); }

  /* AWARDS */
  .awards-list {
    display: flex;
    flex-direction: column;
    gap: 1.5px;
    border: 1.5px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .award-item {
    background: var(--card);
    padding: 1.75rem 2.5rem;
    display: flex;
    align-items: center;
    gap: 2rem;
    border-bottom: 1px solid var(--border);
    transition: background 0.3s;
  }
  .award-item:last-child { border-bottom: none; }
  .award-item:hover { background: rgba(99,139,255,0.05); }
  .award-year {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    color: var(--dim);
    min-width: 40px;
    letter-spacing: 0.08em;
  }
  .award-icon { font-size: 1.3rem; }
  .award-text {
    font-size: 0.95rem;
    color: var(--text);
    line-height: 1.5;
    flex: 1;
  }
  .award-badge {
    font-family: 'Space Mono', monospace;
    font-size: 0.62rem;
    padding: 0.25rem 0.7rem;
    border-radius: 2px;
    background: rgba(99,139,255,0.1);
    color: var(--accent);
    border: 1px solid var(--border);
    letter-spacing: 0.08em;
    text-transform: uppercase;
    white-space: nowrap;
  }

  /* CONTACT SECTION */
  .contact-block {
    border: 1.5px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    background: var(--card);
    padding: 4rem;
    text-align: center;
    position: relative;
  }
  .contact-block::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at center, rgba(99,139,255,0.06) 0%, transparent 70%);
    pointer-events: none;
  }
  .contact-title {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(2rem, 5vw, 4rem);
    color: var(--text);
    margin-bottom: 1rem;
    position: relative;
  }
  .contact-sub {
    font-family: 'Space Mono', monospace;
    font-size: 0.78rem;
    color: var(--muted);
    letter-spacing: 0.12em;
    margin-bottom: 3rem;
    position: relative;
  }
  .contact-links {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
    position: relative;
  }
  .contact-link {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    padding: 0.9rem 2rem;
    border: 1px solid var(--border);
    border-radius: 2px;
    color: var(--muted);
    text-decoration: none;
    transition: all 0.2s;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .contact-link:hover { border-color: var(--accent); color: var(--accent); background: rgba(99,139,255,0.08); }

  /* FOOTER */
  footer {
    position: relative;
    z-index: 2;
    border-top: 1px solid var(--border);
    padding: 2rem 3rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1300px;
    margin: 0 auto;
  }
  footer span {
    font-family: 'Space Mono', monospace;
    font-size: 0.65rem;
    color: var(--dim);
    letter-spacing: 0.1em;
  }

  /* SCROLL ANIMATIONS */
  .reveal {
    opacity: 0;
    transform: translateY(28px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--dim); border-radius: 4px; }
  ::-webkit-scrollbar-thumb:hover { background: var(--accent); }

  /* GLOW BLOB */
  .glow-blob {
    position: fixed;
    border-radius: 50%;
    filter: blur(100px);
    pointer-events: none;
    z-index: 1;
    opacity: 0.18;
  }
  .glow-blob-1 {
    width: 600px; height: 600px;
    background: var(--accent);
    top: -200px; right: -200px;
  }
  .glow-blob-2 {
    width: 500px; height: 500px;
    background: var(--accent2);
    bottom: -100px; left: -150px;
  }

  @media (max-width: 900px) {
    nav { padding: 1.2rem 1.5rem; }
    .hero { padding: 7rem 1.5rem 3rem; }
    .hero-deco { display: none; }
    section { padding: 4rem 1.5rem; }
    .stats-grid { grid-template-columns: repeat(2,1fr); }
    .projects-grid { grid-template-columns: 1fr; }
    .skills-grid { grid-template-columns: 1fr; }
    .pub-card { grid-template-columns: 1fr; }
    .pub-num { font-size: 1.5rem; }
    footer { padding: 1.5rem; flex-direction: column; gap: 0.5rem; text-align: center; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- Glow blobs -->
<div class="glow-blob glow-blob-1"></div>
<div class="glow-blob glow-blob-2"></div>

<!-- NAVIGATION -->
<nav>
  <div class="nav-logo">TK Ray // Portfolio</div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#research">Research</a></li>
    <li><a href="#publications">Papers</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="nav-status">
    <span class="status-dot"></span>
    Open to Opportunities
  </div>
</nav>

<!-- HERO -->
<div class="hero" id="about">
  <div class="hero-tag">// Researcher · Builder · Collaborator</div>
  <h1 class="hero-name">
    Tapon<br />
    <span>Kumer Ray</span>
  </h1>
  <p class="hero-desc">
    Final-year CSE undergraduate at VIT-AP, India. Focused on Human-Computer Interaction, AR Interfaces, and Intelligent Agents. Publishing in multimodal AI, context-aware systems, and adaptive UX.
  </p>
  <div class="hero-tags">
    <span class="tag">Human-Computer Interaction</span>
    <span class="tag">AR Interfaces</span>
    <span class="tag">Multimodal AI</span>
    <span class="tag">Reinforcement Learning</span>
    <span class="tag">User-Centered Design</span>
    <span class="tag">Intelligent Agents</span>
  </div>
  <div class="hero-cta">
    <a href="#publications" class="btn-primary">View Publications</a>
    <a href="#contact" class="btn-ghost">Get in Touch</a>
  </div>

  <!-- Decorative SVG orbital -->
  <div class="hero-deco">
    <svg viewBox="0 0 400 400" fill="none" xmlns="http://www.w3.org/2000/svg">
      <circle cx="200" cy="200" r="140" stroke="rgba(99,139,255,0.12)" stroke-width="1"/>
      <circle cx="200" cy="200" r="100" stroke="rgba(167,139,250,0.1)" stroke-width="1"/>
      <circle cx="200" cy="200" r="60" stroke="rgba(52,211,153,0.1)" stroke-width="1"/>
      <circle cx="200" cy="200" r="20" fill="rgba(99,139,255,0.15)" stroke="rgba(99,139,255,0.4)" stroke-width="1.5"/>

      <g class="orbital-ring">
        <circle cx="340" cy="200" r="7" fill="#638bff" opacity="0.8"/>
        <circle cx="60" cy="200" r="4" fill="#638bff" opacity="0.4"/>
      </g>
      <g class="orbital-ring2">
        <circle cx="200" cy="100" r="5" fill="#a78bfa" opacity="0.7"/>
        <circle cx="200" cy="300" r="3" fill="#a78bfa" opacity="0.35"/>
        <circle cx="130" cy="270" r="5" fill="#34d399" opacity="0.6"/>
      </g>

      <!-- grid lines -->
      <line x1="200" y1="0" x2="200" y2="400" stroke="rgba(99,139,255,0.05)" stroke-width="1"/>
      <line x1="0" y1="200" x2="400" y2="200" stroke="rgba(99,139,255,0.05)" stroke-width="1"/>
      <line x1="58" y1="58" x2="342" y2="342" stroke="rgba(99,139,255,0.04)" stroke-width="1"/>
      <line x1="342" y1="58" x2="58" y2="342" stroke="rgba(99,139,255,0.04)" stroke-width="1"/>
    </svg>
  </div>
</div>

<hr class="section-divider" />

<!-- STATS -->
<section class="reveal">
 <div class="stat-card">
  <div class="stat-card">
    <div class="stat-card">
      <div class="stat-num">7</div>
      <div class="stat-label">Research Papers</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">8.2</div>
      <div class="stat-label">GPA / 10.0</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">2+</div>
      <div class="stat-label">Years Research Exp.</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">3</div>
      <div class="stat-label">Intl. Conferences</div>
    </div>
  </div>
 </div>
</section>

<hr class="section-divider" />

<!-- RESEARCH EXPERIENCE -->
<section id="research" class="reveal">
  <div class="section-header">
    <span class="section-num">01</span>
    <div class="section-line"></div>
    <h2 class="section-title">Research Experience</h2>
  </div>

  <div class="timeline">
    <div class="timeline-item">
      <div class="timeline-date">MAY 2024 – DECEMBER 2025</div>
      <div class="timeline-role">Undergraduate Research Assistant</div>
      <div class="timeline-org">AIR Center · VIT-AP University, Amaravati — Advisor: Dr. Rajkumar Yesuraj</div>
      <ul class="timeline-bullets">
        <li>Implemented AR-based simulation frameworks in Unity + ROS + OpenCV to support experiments on context-aware adaptive interfaces.</li>
        <li>Developed data pipelines for multimodal input (speech, gesture, visual signals) and performed statistical analysis using Python/SPSS.</li>
        <li>Integrated prototype adaptive decision-making models with reinforcement learning and rule-based policies for proof-of-concept testing.</li>
      </ul>
    </div>

    <div class="timeline-item">
      <div class="timeline-date">AUGUST 2023 – JULY 2024</div>
      <div class="timeline-role">Project Assistant</div>
      <div class="timeline-org">IIEC Center · VIT-AP University, Amaravati — Advisor: Dr. Guruprakash Jayabalasamy</div>
      <ul class="timeline-bullets">
        <li>Investigated adaptive user interface models in AR-supported human-robot collaboration environments.</li>
        <li>Conducted a structured literature review for a survey on vision-language interaction models in HCI.</li>
        <li>Collaborated on experiment design for evaluating multimodal adaptive systems.</li>
      </ul>
    </div>
  </div>
</section>

<hr class="section-divider" />

<!-- PUBLICATIONS -->
<section id="publications" class="reveal">
  <div class="section-header">
    <span class="section-num">02</span>
    <div class="section-line"></div>
    <h2 class="section-title">Publications</h2>
  </div>

  <div class="pub-grid">
    <div class="pub-card">
      <div class="pub-num">01</div>
      <div>
        <div class="pub-title">Synchronous Emotional Dynamics in Human-AI Collaborative Networks: A Temporal Graph Neural Network Approach</div>
        <div class="pub-venue">IEEE CICN · Conference Proceedings · 2025</div>
      </div>
      <div class="pub-badge badge-published">Published</div>
    </div>

    <div class="pub-card">
      <div class="pub-num">02</div>
      <div>
        <div class="pub-title">XMACNet: An Explainable Lightweight Attention based CNN with Multi-Modal Fusion for Chili Disease Classification</div>
        <div class="pub-venue">Springer LNICST · Conference Proceedings · 2025</div>
      </div>
      <div class="pub-badge badge-published">Published</div>
    </div>

    <div class="pub-card">
      <div class="pub-num">03</div>
      <div>
        <div class="pub-title">Segment-Based Dynamic Programming for Optimal Binary Search Trees: A Sub-Cubic Algorithm (NCUR 2026)</div>
        <div class="pub-venue">National Conference on Undergraduate Research (NCUR) · Presentation · 2026</div>
      </div>
      <div class="pub-badge badge-presented">Presented</div>
    </div>

    <div class="pub-card">
      <div class="pub-num">04</div>
      <div>
        <div class="pub-title">A Comprehensive Survey on Human Behavior Prediction by Speech, Emotion and Gesture using Deep Learning</div>
        <div class="pub-venue">Journal of Ambient Intelligence and Humanized Computing · Under Review</div>
      </div>
      <div class="pub-badge badge-review">Under Review</div>
    </div>

    <div class="pub-card">
      <div class="pub-num">05</div>
      <div>
        <div class="pub-title">Context-Aware Emotionally Adaptive Voice Assistants: A Multi-Modal Framework for Empathetic Human-Agent Interaction</div>
        <div class="pub-venue">Journal of Automation and Intelligence · Under Review</div>
      </div>
      <div class="pub-badge badge-review">Under Review</div>
    </div>

    <div class="pub-card">
      <div class="pub-num">06</div>
      <div>
        <div class="pub-title">Interactive Ethical Constraint Specification for LLM Decision Support: A Human-Centered Algorithmic Framework</div>
        <div class="pub-venue">Autonomous Agents and Multi-Agent Systems · Under Review</div>
      </div>
      <div class="pub-badge badge-review">Under Review</div>
    </div>

    <div class="pub-card">
      <div class="pub-num">07</div>
      <div>
        <div class="pub-title">Segment-Based Dynamic Programming for Optimal Binary Search Trees: A Sub-Cubic Algorithm with Hierarchical Weight Partitioning</div>
        <div class="pub-venue">Springer Algorithmica · Under Review · 2026</div>
      </div>
      <div class="pub-badge badge-review">Under Review</div>
    </div>
  </div>
</section>

<hr class="section-divider" />

<!-- PROJECTS -->
<section id="projects" class="reveal">
  <div class="section-header">
    <span class="section-num">03</span>
    <div class="section-line"></div>
    <h2 class="section-title">Projects</h2>
  </div>

  <div class="projects-grid">
    <div class="project-card">
      <div class="project-icon">🧠</div>
      <div class="project-title">Context-Aware Decision Making Agent for Smart Assistants</div>
      <p class="project-desc">Capstone project deploying multimodal signal fusion (voice, wearables) with on-device processing and RL-based adaptive policies, ensuring real-time, privacy-preserving smart assistant interactions.</p>
      <div class="tech-stack">
        <span class="tech-chip">PyTorch</span>
        <span class="tech-chip">RL</span>
        <span class="tech-chip">On-Device AI</span>
        <span class="tech-chip">Multimodal</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">🤖</div>
      <div class="project-title">AR-Enhanced Human-Robot Collaboration Interface</div>
      <p class="project-desc">Multimodal interface design using Unity and ROS to support spatial collaboration and task-switching with context-aware feedback in AR-supported environments.</p>
      <div class="tech-stack">
        <span class="tech-chip">Unity</span>
        <span class="tech-chip">ROS</span>
        <span class="tech-chip">OpenCV</span>
        <span class="tech-chip">AR</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">👁</div>
      <div class="project-title">Machine Vision-Based Third Eye for Safe Driving</div>
      <p class="project-desc">Non-invasive eye-tracking interaction model using WebGazer.js and OpenCV to enable navigation in constrained environments, developed as part of Engineering Clinics.</p>
      <div class="tech-stack">
        <span class="tech-chip">WebGazer.js</span>
        <span class="tech-chip">OpenCV</span>
        <span class="tech-chip">Eye-Tracking</span>
        <span class="tech-chip">HCI</span>
      </div>
    </div>
  </div>
</section>

<hr class="section-divider" />

<!-- SKILLS -->
<section id="skills" class="reveal">
  <div class="section-header">
    <span class="section-num">04</span>
    <div class="section-line"></div>
    <h2 class="section-title">Technical Skills</h2>
  </div>

  <div class="skills-grid">
    <div class="skill-group">
      <div class="skill-group-title">Languages</div>
      <div class="skill-chips">
        <span class="skill-chip">Python</span>
        <span class="skill-chip">Java</span>
        <span class="skill-chip">R</span>
        <span class="skill-chip">JavaScript</span>
        <span class="skill-chip">MATLAB</span>
        <span class="skill-chip">SQL</span>
      </div>
    </div>
    <div class="skill-group">
      <div class="skill-group-title">Frameworks</div>
      <div class="skill-chips">
        <span class="skill-chip">PyTorch</span>
        <span class="skill-chip">TensorFlow</span>
        <span class="skill-chip">Keras</span>
        <span class="skill-chip">Scikit-learn</span>
        <span class="skill-chip">Hugging Face</span>
        <span class="skill-chip">StyleGAN</span>
      </div>
    </div>
    <div class="skill-group">
      <div class="skill-group-title">Tools & Platforms</div>
      <div class="skill-chips">
        <span class="skill-chip">NumPy</span>
        <span class="skill-chip">Pandas</span>
        <span class="skill-chip">SciPy</span>
        <span class="skill-chip">SPSS</span>
        <span class="skill-chip">RStudio</span>
        <span class="skill-chip">Unity</span>
        <span class="skill-chip">OpenCV</span>
        <span class="skill-chip">ROS</span>
      </div>
    </div>
    <div class="skill-group">
      <div class="skill-group-title">Design & Workflow</div>
      <div class="skill-chips">
        <span class="skill-chip">Figma</span>
        <span class="skill-chip">Adobe XD</span>
        <span class="skill-chip">Tableau</span>
        <span class="skill-chip">Git</span>
        <span class="skill-chip">LaTeX</span>
        <span class="skill-chip">Jupyter</span>
        <span class="skill-chip">Mendeley</span>
        <span class="skill-chip">Zotero</span>
      </div>
    </div>
  </div>
</section>

<hr class="section-divider" />

<!-- AWARDS -->
<section class="reveal">
  <div class="section-header">
    <span class="section-num">05</span>
    <div class="section-line"></div>
    <h2 class="section-title">Awards & Recognition</h2>
  </div>

  <div class="awards-list">
    <div class="award-item">
      <div class="award-year">2026</div>
      <div class="award-icon">🌎</div>
      <div class="award-text">Selected — <strong>Student Mentoring Workshop (SMeW), ICSE 2026</strong> · Rio de Janeiro, Brazil</div>
      <div class="award-badge">International</div>
    </div>
    <div class="award-item">
      <div class="award-year">2026</div>
      <div class="award-icon">✏️</div>
      <div class="award-text">Student Volunteer — <strong>POPL 2026</strong> (Principles of Programming Languages) · Rennes, France</div>
      <div class="award-badge">Volunteer</div>
    </div>
    <div class="award-item">
      <div class="award-year">2023</div>
      <div class="award-icon">🏆</div>
      <div class="award-text">Finalist — <strong>National Level MARK-XXIV Hackathon</strong> · Woxsen University, India</div>
      <div class="award-badge">Finalist</div>
    </div>
    <div class="award-item">
      <div class="award-year">2022</div>
      <div class="award-icon">🎓</div>
      <div class="award-text">Merit-Based — <strong>International Scholarship for Education & Enrichment (I-SEE)</strong> · VIT University, India</div>
      <div class="award-badge">Scholarship</div>
    </div>
  </div>
</section>

<hr class="section-divider" />

<!-- CONTACT -->
<section id="contact" class="reveal">
  <div class="contact-block">
    <h2 class="contact-title">Let's Collaborate</h2>
    <p class="contact-sub">// Open to research collaborations, internships &amp; PhD positions</p>
    <div class="contact-links">
      <a href="mailto:tapon.22bce20245@vitapstudent.ac.in" class="contact-link">
        ✉ Email
      </a>
      <a href="https://github.com/tapon22bce" class="contact-link" target="_blank">
        ⌥ GitHub
      </a>
      <a href="https://linkedin.com" class="contact-link" target="_blank">
        ↗ LinkedIn
      </a>
      <a href="https://x.com" class="contact-link" target="_blank">
        ✕ X / Twitter
      </a>
    </div>
  </div>
</section>

<footer>
  <span>© 2026 TAPON KUMER RAY · VIT-AP, INDIA</span>
  <span>CSE · HCI · MULTIMODAL AI · AR</span>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const cursorRing = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    cursorRing.style.left = rx + 'px';
    cursorRing.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .tag, .skill-chip, .tech-chip, .pub-card').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(2.5)';
      cursorRing.style.transform = 'translate(-50%,-50%) scale(1.5)';
      cursorRing.style.borderColor = 'rgba(99,139,255,0.8)';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(1)';
      cursorRing.style.transform = 'translate(-50%,-50%) scale(1)';
      cursorRing.style.borderColor = 'rgba(99,139,255,0.5)';
    });
  });

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });
  reveals.forEach(r => observer.observe(r));

  // Smooth nav highlight
  const sections = document.querySelectorAll('section[id], div[id="about"]');
  const navLinks = document.querySelectorAll('.nav-links a');
  window.addEventListener('scroll', () => {
    let current = '';
    sections.forEach(s => {
      if (window.scrollY >= s.offsetTop - 200) current = s.id;
    });
    navLinks.forEach(a => {
      a.style.color = a.getAttribute('href') === '#'+current ? 'var(--accent)' : '';
    });
  });
</script>

</body>
</html>