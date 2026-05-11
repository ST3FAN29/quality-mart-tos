<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EMP Unpanzerforce — Discord Community</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --black:      #010608;
    --dark:       #060d12;
    --dark2:      #091218;
    --dark3:      #0c1820;
    --panel:      #071018;
    --cyan:       #00e5ff;
    --cyan2:      #00bcd4;
    --cyan-dim:   rgba(0,229,255,0.10);
    --cyan-glow:  0 0 8px #00e5ff, 0 0 30px rgba(0,229,255,0.35);
    --cyan-glow2: 0 0 4px #00e5ff, 0 0 14px rgba(0,229,255,0.25);
    --orange:     #ff6d00;
    --orange-glow:0 0 8px #ff6d00, 0 0 28px rgba(255,109,0,0.4);
    --white:      #e8f4ff;
    --text:       #a8c8d8;
    --text-dim:   #3d5a6a;
    --border:     rgba(0,229,255,0.13);
    --border-o:   rgba(255,109,0,0.25);
  }
  *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--black);
    color: var(--text);
    font-family: 'Rajdhani', sans-serif;
    font-weight: 400;
    overflow-x: hidden;
    cursor: crosshair;
  }
  body::after {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.03) 2px,rgba(0,0,0,0.03) 4px);
    pointer-events: none;
    z-index: 9999;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 200;
    display: flex; align-items: center; justify-content: space-between;
    padding: 0.8rem 2.5rem;
    background: rgba(1,6,8,0.9);
    backdrop-filter: blur(14px);
    border-bottom: 1px solid var(--border);
  }
  .nav-brand { display: flex; align-items: center; gap: 0.9rem; text-decoration: none; }
  .nav-logo-img { width: 32px; height: 32px; image-rendering: pixelated; filter: drop-shadow(0 0 6px rgba(255,109,0,0.7)); }
  .nav-title { font-family: 'Orbitron', monospace; font-weight: 900; font-size: 0.95rem; letter-spacing: 0.25em; color: var(--white); }
  .nav-title span { color: var(--cyan); }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a { font-family: 'Share Tech Mono', monospace; font-size: 0.68rem; letter-spacing: 0.2em; color: var(--text-dim); text-decoration: none; text-transform: uppercase; transition: color 0.2s, text-shadow 0.2s; }
  .nav-links a:hover { color: var(--cyan); text-shadow: var(--cyan-glow2); }
  .nav-cta { font-family: 'Share Tech Mono', monospace; font-size: 0.7rem; letter-spacing: 0.15em; color: var(--black); background: var(--cyan); padding: 0.5rem 1.3rem; border: none; cursor: pointer; text-decoration: none; text-transform: uppercase; clip-path: polygon(6px 0%,100% 0%,calc(100% - 6px) 100%,0% 100%); transition: box-shadow 0.25s, transform 0.2s; font-weight: 700; }
  .nav-cta:hover { box-shadow: var(--cyan-glow); transform: translateY(-1px); }

  /* ── HERO ── */
  #hero {
    position: relative; min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    text-align: center; padding: 7rem 2rem 5rem;
    overflow: hidden;
  }
  .hero-grid {
    position: absolute; inset: 0; pointer-events: none;
    background-image: linear-gradient(rgba(0,229,255,0.035) 1px, transparent 1px), linear-gradient(90deg, rgba(0,229,255,0.035) 1px, transparent 1px);
    background-size: 50px 50px;
    mask-image: radial-gradient(ellipse 85% 85% at 50% 50%, black 30%, transparent 100%);
  }
  .hero-glow {
    position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%);
    width: 700px; height: 500px;
    background: radial-gradient(ellipse, rgba(0,229,255,0.06) 0%, transparent 65%);
    pointer-events: none;
  }
  .corner { position: absolute; width: 40px; height: 40px; }
  .corner.tl { top: 90px; left: 20px; border-top: 2px solid var(--cyan); border-left: 2px solid var(--cyan); }
  .corner.tr { top: 90px; right: 20px; border-top: 2px solid var(--cyan); border-right: 2px solid var(--cyan); }
  .corner.bl { bottom: 20px; left: 20px; border-bottom: 2px solid var(--cyan); border-left: 2px solid var(--cyan); }
  .corner.br { bottom: 20px; right: 20px; border-bottom: 2px solid var(--cyan); border-right: 2px solid var(--cyan); }

  .hero-eyebrow { font-family: 'Share Tech Mono', monospace; font-size: 0.66rem; letter-spacing: 0.45em; color: var(--cyan); text-transform: uppercase; margin-bottom: 1.2rem; opacity: 0; animation: fadeUp 0.6s 0.2s forwards; }

  .hero-logos { display: flex; align-items: center; gap: 1.4rem; justify-content: center; margin-bottom: 0.8rem; opacity: 0; animation: fadeUp 0.6s 0.35s forwards; }
  .hero-logo-wrap { display: flex; flex-direction: column; align-items: center; gap: 0.35rem; }
  .hero-logo-img { width: 52px; height: 52px; image-rendering: pixelated; }
  .logo-old .hero-logo-img { filter: drop-shadow(0 0 8px rgba(0,229,255,0.7)); opacity: 0.45; }
  .logo-new .hero-logo-img { filter: drop-shadow(0 0 12px rgba(255,109,0,0.9)); }
  .logo-label { font-family: 'Share Tech Mono', monospace; font-size: 0.52rem; letter-spacing: 0.18em; color: var(--text-dim); text-transform: uppercase; }
  .logo-label.active { color: var(--orange); }
  .logo-divider { display: flex; flex-direction: column; align-items: center; gap: 0.25rem; }
  .logo-divider .ld-txt { font-family: 'Share Tech Mono', monospace; font-size: 0.55rem; color: var(--text-dim); letter-spacing: 0.1em; }
  .logo-arrow { font-size: 1.1rem; color: var(--cyan); text-shadow: var(--cyan-glow2); animation: arrowPulse 2s ease-in-out infinite; }
  @keyframes arrowPulse { 0%,100%{transform:translateX(0);opacity:0.6;} 50%{transform:translateX(4px);opacity:1;} }

  .hero-title {
    font-family: 'Orbitron', monospace; font-size: clamp(4rem,15vw,11rem); font-weight: 900;
    letter-spacing: 0.18em; color: var(--white); position: relative; line-height: 1;
    text-shadow: 0 0 40px rgba(0,229,255,0.2);
    opacity: 0; animation: fadeUp 0.6s 0.5s forwards, glitch 7s 2.5s infinite;
  }
  .hero-title::before, .hero-title::after {
    content: attr(data-text); position: absolute; inset: 0;
    font-family: inherit; font-weight: 900; font-size: inherit; letter-spacing: inherit;
  }
  .hero-title::before { color: var(--cyan); clip-path: polygon(0 25%,100% 25%,100% 42%,0 42%); transform: translateX(-4px); animation: gBefore 7s 2.5s infinite; opacity: 0; }
  .hero-title::after  { color: var(--orange); clip-path: polygon(0 62%,100% 62%,100% 76%,0 76%); transform: translateX(4px); animation: gAfter 7s 2.5s infinite; opacity: 0; }
  @keyframes glitch { 0%,91%,100%{transform:none;} 92%{transform:skewX(-1.5deg) translateX(3px);} 93%{transform:skewX(0.5deg) translateX(-2px);} 94%{transform:none;} }
  @keyframes gBefore { 0%,91%,100%{opacity:0;transform:translateX(-4px);} 92%{opacity:0.9;transform:translateX(-8px);} 93%{opacity:0.9;transform:translateX(-2px);} 94%{opacity:0;} }
  @keyframes gAfter  { 0%,91%,100%{opacity:0;transform:translateX(4px);} 92%{opacity:0.9;transform:translateX(8px);} 93%{opacity:0.9;transform:translateX(2px);} 94%{opacity:0;} }

  .hero-subtitle { font-family: 'Orbitron', monospace; font-size: clamp(0.65rem,2vw,0.95rem); font-weight: 400; letter-spacing: 0.35em; color: var(--text-dim); text-transform: uppercase; margin-top: 0.3rem; margin-bottom: 0.5rem; opacity: 0; animation: fadeUp 0.6s 0.65s forwards; }
  .hero-tagline { font-family: 'Rajdhani', sans-serif; font-size: clamp(0.95rem,2.5vw,1.25rem); font-weight: 300; letter-spacing: 0.12em; color: var(--text); margin-bottom: 2.2rem; opacity: 0; animation: fadeUp 0.6s 0.8s forwards; }
  .hero-tagline .c { color: var(--cyan); font-weight: 600; }
  .hero-tagline .o { color: var(--orange); font-weight: 600; }

  .hero-btns { display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center; opacity: 0; animation: fadeUp 0.6s 1s forwards; }

  .btn-primary { font-family: 'Orbitron', monospace; font-size: 0.82rem; font-weight: 700; letter-spacing: 0.18em; color: var(--black); background: var(--cyan); padding: 0.95rem 2.3rem; border: none; cursor: pointer; text-decoration: none; text-transform: uppercase; clip-path: polygon(10px 0%,100% 0%,calc(100% - 10px) 100%,0% 100%); transition: box-shadow 0.3s, transform 0.2s; display: inline-flex; align-items: center; gap: 0.5rem; }
  .btn-primary:hover { box-shadow: var(--cyan-glow); transform: translateY(-2px); }
  .btn-secondary { font-family: 'Orbitron', monospace; font-size: 0.82rem; font-weight: 700; letter-spacing: 0.18em; color: var(--cyan); background: transparent; padding: 0.95rem 2.3rem; border: 1px solid var(--cyan); cursor: pointer; text-decoration: none; text-transform: uppercase; clip-path: polygon(10px 0%,100% 0%,calc(100% - 10px) 100%,0% 100%); transition: background 0.3s, box-shadow 0.3s, transform 0.2s; }
  .btn-secondary:hover { background: var(--cyan-dim); box-shadow: var(--cyan-glow); transform: translateY(-2px); }

  .hero-games { margin-top: 2.2rem; display: flex; gap: 0.5rem; flex-wrap: wrap; justify-content: center; opacity: 0; animation: fadeUp 0.6s 1.2s forwards; }
  .game-tag { font-family: 'Share Tech Mono', monospace; font-size: 0.58rem; letter-spacing: 0.18em; color: var(--text-dim); text-transform: uppercase; padding: 0.28rem 0.75rem; border: 1px solid rgba(0,229,255,0.1); background: rgba(0,229,255,0.03); clip-path: polygon(4px 0%,100% 0%,calc(100% - 4px) 100%,0% 100%); transition: color 0.2s, border-color 0.2s; cursor: default; }
  .game-tag:hover { color: var(--cyan); border-color: var(--border); }

  .scroll-indicator { position: absolute; bottom: 2rem; left: 50%; transform: translateX(-50%); display: flex; flex-direction: column; align-items: center; gap: 0.4rem; opacity: 0; animation: fadeIn 1s 1.6s forwards; }
  .scroll-indicator span { font-family: 'Share Tech Mono', monospace; font-size: 0.52rem; letter-spacing: 0.35em; color: var(--text-dim); text-transform: uppercase; }
  .scroll-line { width: 1px; height: 34px; background: linear-gradient(var(--cyan), transparent); animation: scrollPulse 1.6s ease-in-out infinite; }
  @keyframes scrollPulse { 0%,100%{opacity:0.3;} 50%{opacity:1;} }

  #particles { position: absolute; inset: 0; pointer-events: none; overflow: hidden; }
  .particle { position: absolute; border-radius: 50%; background: var(--cyan); box-shadow: 0 0 4px var(--cyan); animation: floatUp linear infinite; opacity: 0; }
  @keyframes floatUp { from{transform:translateY(100vh) translateX(0);opacity:0;} 10%{opacity:0.8;} 90%{opacity:0.4;} to{transform:translateY(-40px) translateX(calc(var(--dx,0) * 1px));opacity:0;} }

  /* ── DIVIDER ── */
  .divider { width: 100%; height: 1px; background: linear-gradient(90deg,transparent,var(--border),transparent); }

  /* ── SHARED LAYOUT ── */
  .section-wrap { max-width: 1100px; margin: 0 auto; padding: 6rem 2rem; }
  .full-dark { background: var(--dark); }

  .section-tag { font-family: 'Share Tech Mono', monospace; font-size: 0.62rem; letter-spacing: 0.42em; color: var(--cyan); text-transform: uppercase; margin-bottom: 0.7rem; display: flex; align-items: center; gap: 0.5rem; }
  .section-tag::before { content: '//'; color: var(--text-dim); }

  h2 { font-family: 'Orbitron', monospace; font-size: clamp(1.55rem,4vw,2.5rem); font-weight: 700; color: var(--white); letter-spacing: 0.1em; margin-bottom: 1.1rem; }
  h2 .c { color: var(--cyan); }
  h2 .o { color: var(--orange); }
  .body-p { font-size: 1rem; line-height: 1.8; color: var(--text); max-width: 58ch; font-weight: 300; }

  /* ── LORE BANNER ── */
  #lore-banner { background: linear-gradient(90deg, rgba(255,109,0,0.06) 0%, transparent 60%); border-left: 3px solid var(--orange); border-top: 1px solid var(--border-o); border-bottom: 1px solid var(--border-o); }
  .lore-inner { max-width: 1100px; margin: 0 auto; padding: 3rem 2rem; display: grid; grid-template-columns: 1fr 1fr; gap: 3rem; align-items: center; }
  .lore-eyebrow { font-family: 'Share Tech Mono', monospace; font-size: 0.6rem; letter-spacing: 0.38em; color: var(--orange); text-transform: uppercase; margin-bottom: 0.6rem; }
  .lore-text h3 { font-family: 'Orbitron', monospace; font-size: clamp(1rem,2.5vw,1.45rem); font-weight: 700; color: var(--white); letter-spacing: 0.1em; margin-bottom: 0.8rem; }
  .lore-logos { display: flex; align-items: center; gap: 1.5rem; justify-content: flex-end; background: var(--panel); border: 1px solid var(--border-o); padding: 1.8rem; position: relative; clip-path: polygon(0 0,calc(100% - 14px) 0,100% 14px,100% 100%,14px 100%,0 calc(100% - 14px)); }
  .lore-logos::before { content: 'LORE EVENT'; position: absolute; top: 0.45rem; left: 0.75rem; font-family: 'Share Tech Mono', monospace; font-size: 0.52rem; letter-spacing: 0.18em; color: var(--text-dim); text-transform: uppercase; }
  .lore-logo-item { display: flex; flex-direction: column; align-items: center; gap: 0.5rem; flex: 1; }
  .lore-logo-item img { width: 64px; height: 64px; image-rendering: pixelated; }
  .lore-logo-item.old img { filter: drop-shadow(0 0 7px rgba(0,229,255,0.55)) grayscale(0.3); opacity: 0.5; }
  .lore-logo-item.new img { filter: drop-shadow(0 0 14px rgba(255,109,0,0.9)); }
  .lore-logo-item .tag { font-family: 'Share Tech Mono', monospace; font-size: 0.56rem; letter-spacing: 0.12em; text-transform: uppercase; text-align: center; }
  .lore-logo-item.old .tag { color: var(--text-dim); }
  .lore-logo-item.new .tag { color: var(--orange); }
  .lore-arrow { font-size: 1.4rem; color: var(--orange); text-shadow: var(--orange-glow); flex-shrink: 0; animation: arrowPulse 2s ease-in-out infinite; }

  /* ── ABOUT ── */
  .about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; align-items: center; }
  .about-panel { background: var(--panel); border: 1px solid var(--border); padding: 1.8rem; position: relative; overflow: hidden; clip-path: polygon(0 0,calc(100% - 18px) 0,100% 18px,100% 100%,18px 100%,0 calc(100% - 18px)); }
  .about-panel::before { content: ''; position: absolute; inset: 0; background: radial-gradient(ellipse at 30% 0%,rgba(0,229,255,0.05) 0%,transparent 60%); }
  .about-corner { position: absolute; width: 14px; height: 14px; }
  .about-corner.tl { top: 0; left: 0; border-top: 2px solid var(--cyan); border-left: 2px solid var(--cyan); }
  .about-corner.br { bottom: 0; right: 0; border-bottom: 2px solid var(--cyan); border-right: 2px solid var(--cyan); }
  .panel-header { font-family: 'Share Tech Mono', monospace; font-size: 0.58rem; letter-spacing: 0.22em; color: var(--text-dim); text-transform: uppercase; padding-bottom: 0.75rem; border-bottom: 1px solid var(--border); margin-bottom: 1.1rem; display: flex; justify-content: space-between; }
  .panel-status { color: var(--cyan); text-shadow: var(--cyan-glow2); animation: blink2 2s step-end infinite; }
  @keyframes blink2 { 0%,100%{opacity:1;} 50%{opacity:0.4;} }
  .stat-row { display: flex; justify-content: space-between; align-items: center; padding: 0.65rem 0; border-bottom: 1px solid rgba(0,229,255,0.05); }
  .stat-row:last-child { border-bottom: none; }
  .stat-label { font-family: 'Share Tech Mono', monospace; font-size: 0.62rem; letter-spacing: 0.12em; color: var(--text-dim); text-transform: uppercase; }
  .stat-val { font-family: 'Orbitron', monospace; font-size: 0.75rem; font-weight: 700; color: var(--cyan); letter-spacing: 0.08em; }
  .stat-val.o { color: var(--orange); }
  .stat-val.w { color: var(--white); }

  /* ── RTS ── */
  .rts-grid { display: grid; grid-template-columns: 1fr 1.2fr; gap: 3.5rem; align-items: start; margin-top: 2.5rem; }
  .rts-cards { display: flex; flex-direction: column; gap: 1px; }
  .rts-card { background: var(--panel); border: 1px solid var(--border); border-left: 3px solid var(--cyan); padding: 1.1rem 1.3rem; position: relative; overflow: hidden; transition: background 0.3s; cursor: default; }
  .rts-card:hover { background: var(--dark3); }
  .rts-card.villain { border-left-color: var(--orange); }
  .rts-card-title { font-family: 'Orbitron', monospace; font-size: 0.76rem; font-weight: 700; letter-spacing: 0.15em; text-transform: uppercase; color: var(--white); margin-bottom: 0.35rem; }
  .rts-card.villain .rts-card-title { color: var(--orange); }
  .rts-card-desc { font-size: 0.88rem; line-height: 1.65; color: var(--text-dim); }
  .rts-badge { position: absolute; top: 0.65rem; right: 0.8rem; font-family: 'Share Tech Mono', monospace; font-size: 0.48rem; letter-spacing: 0.18em; text-transform: uppercase; padding: 0.18rem 0.45rem; border: 1px solid var(--border); color: var(--text-dim); }
  .rts-badge.threat { border-color: var(--border-o); color: var(--orange); }

  .rts-world { background: var(--panel); border: 1px solid var(--border); padding: 1.8rem; min-height: 340px; display: flex; flex-direction: column; overflow: hidden; position: relative; }
  .rts-world::before { content: ''; position: absolute; inset: 0; background: radial-gradient(ellipse at 50% 30%,rgba(0,229,255,0.04) 0%,transparent 60%), repeating-linear-gradient(0deg,transparent,transparent 29px,rgba(0,229,255,0.015) 29px,rgba(0,229,255,0.015) 30px), repeating-linear-gradient(90deg,transparent,transparent 29px,rgba(0,229,255,0.015) 29px,rgba(0,229,255,0.015) 30px); }
  .rts-world-label { font-family: 'Share Tech Mono', monospace; font-size: 0.56rem; letter-spacing: 0.28em; color: var(--text-dim); text-transform: uppercase; margin-bottom: 1rem; position: relative; }
  .territory-map { flex: 1; position: relative; display: grid; grid-template-columns: repeat(4,1fr); grid-template-rows: repeat(3,1fr); gap: 3px; }
  .territory { background: rgba(0,229,255,0.035); border: 1px solid rgba(0,229,255,0.07); display: flex; align-items: center; justify-content: center; transition: background 0.25s; cursor: default; }
  .territory:hover { background: rgba(0,229,255,0.07); }
  .territory.contested { background: rgba(255,109,0,0.04); border-color: rgba(255,109,0,0.12); }
  .territory.contested:hover { background: rgba(255,109,0,0.08); }
  .territory.center { grid-column: 2/4; grid-row: 1/3; background: rgba(0,229,255,0.07); border-color: var(--border); }
  .territory span { font-family: 'Share Tech Mono', monospace; font-size: 0.46rem; letter-spacing: 0.08em; color: var(--text-dim); text-transform: uppercase; text-align: center; padding: 0.2rem; }
  .territory.center span { font-size: 0.58rem; color: var(--cyan); text-shadow: var(--cyan-glow2); }
  .territory.contested span { color: var(--orange); }
  .map-legend { margin-top: 0.9rem; display: flex; gap: 1rem; flex-wrap: wrap; position: relative; }
  .map-key { display: flex; align-items: center; gap: 0.35rem; }
  .map-swatch { width: 9px; height: 9px; }
  .map-key span { font-family: 'Share Tech Mono', monospace; font-size: 0.5rem; color: var(--text-dim); letter-spacing: 0.1em; text-transform: uppercase; }
  .map-note { margin-top: 0.9rem; padding: 0.7rem; background: rgba(255,109,0,0.04); border: 1px solid var(--border-o); border-left: 2px solid var(--orange); position: relative; }
  .map-note span { font-family: 'Share Tech Mono', monospace; font-size: 0.55rem; color: var(--orange); letter-spacing: 0.12em; text-transform: uppercase; }

  /* ── FEATURES ── */
  .features-grid { display: grid; grid-template-columns: repeat(auto-fill,minmax(260px,1fr)); gap: 1px; border: 1px solid var(--border); margin-top: 2.2rem; overflow: hidden; }
  .feat-card { padding: 1.7rem; background: var(--panel); position: relative; overflow: hidden; transition: background 0.3s; cursor: default; }
  .feat-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; background: var(--cyan); transform: scaleX(0); transform-origin: left; transition: transform 0.4s; }
  .feat-card:hover { background: var(--dark3); }
  .feat-card:hover::before { transform: scaleX(1); }
  .feat-card:hover .feat-icon { transform: scale(1.15); text-shadow: var(--cyan-glow); }
  .feat-icon { font-size: 1.45rem; margin-bottom: 0.85rem; display: block; transition: transform 0.3s, text-shadow 0.3s; }
  .feat-num { position: absolute; top: 0.9rem; right: 1.1rem; font-family: 'Share Tech Mono', monospace; font-size: 0.52rem; color: var(--text-dim); }
  .feat-title { font-family: 'Orbitron', monospace; font-size: 0.74rem; font-weight: 700; letter-spacing: 0.14em; color: var(--white); text-transform: uppercase; margin-bottom: 0.45rem; }
  .feat-desc { font-size: 0.88rem; color: var(--text-dim); line-height: 1.7; }

  /* ── WHY JOIN ── */
  .why-grid { display: grid; grid-template-columns: 1fr 1.4fr; gap: 5rem; align-items: center; }
  .why-items { display: flex; flex-direction: column; }
  .why-item { display: flex; gap: 1.1rem; align-items: flex-start; padding: 1.2rem 0; border-bottom: 1px solid var(--border); transition: padding-left 0.3s; cursor: default; }
  .why-item:first-child { border-top: 1px solid var(--border); }
  .why-item:hover { padding-left: 0.5rem; }
  .why-item:hover .why-bullet { text-shadow: var(--cyan-glow2); }
  .why-bullet { font-family: 'Share Tech Mono', monospace; font-size: 0.68rem; color: var(--cyan); flex-shrink: 0; margin-top: 0.1rem; transition: text-shadow 0.2s; }
  .why-text strong { display: block; font-family: 'Rajdhani', sans-serif; font-weight: 700; color: var(--white); font-size: 0.98rem; margin-bottom: 0.15rem; }
  .why-text p { font-size: 0.86rem; line-height: 1.65; color: var(--text-dim); }

  /* ── RULES ── */
  .rules-grid { display: grid; grid-template-columns: repeat(auto-fill,minmax(220px,1fr)); gap: 1rem; margin-top: 2.2rem; }
  .rule-card { background: var(--panel); border: 1px solid var(--border); padding: 1.3rem; position: relative; overflow: hidden; clip-path: polygon(0 0,calc(100% - 11px) 0,100% 11px,100% 100%,11px 100%,0 calc(100% - 11px)); transition: border-color 0.3s, box-shadow 0.3s; cursor: default; }
  .rule-card:hover { border-color: rgba(0,229,255,0.3); box-shadow: 0 0 18px rgba(0,229,255,0.04); }
  .rule-num { font-family: 'Share Tech Mono', monospace; font-size: 1.3rem; color: rgba(0,229,255,0.06); position: absolute; top: 0.65rem; right: 0.85rem; }
  .rule-title { font-family: 'Orbitron', monospace; font-size: 0.7rem; font-weight: 700; letter-spacing: 0.18em; color: var(--cyan); text-transform: uppercase; margin-bottom: 0.4rem; }
  .rule-desc { font-size: 0.84rem; color: var(--text-dim); line-height: 1.65; }

  /* ── CTA ── */
  #cta { text-align: center; padding: 8rem 2rem; position: relative; overflow: hidden; }
  #cta::before { content: ''; position: absolute; inset: 0; background: radial-gradient(ellipse 70% 70% at 50% 50%,rgba(0,229,255,0.04) 0%,transparent 70%), repeating-linear-gradient(0deg,transparent,transparent 49px,rgba(0,229,255,0.012) 49px,rgba(0,229,255,0.012) 50px), repeating-linear-gradient(90deg,transparent,transparent 49px,rgba(0,229,255,0.012) 49px,rgba(0,229,255,0.012) 50px); }
  .cta-inner { position: relative; max-width: 700px; margin: 0 auto; }
  .cta-logo { display: flex; justify-content: center; margin-bottom: 1.8rem; }
  .cta-logo img { width: 76px; height: 76px; image-rendering: pixelated; filter: drop-shadow(0 0 16px rgba(255,109,0,0.9)) drop-shadow(0 0 38px rgba(255,109,0,0.35)); animation: logoPulse 3s ease-in-out infinite; }
  @keyframes logoPulse { 0%,100%{filter:drop-shadow(0 0 16px rgba(255,109,0,0.9)) drop-shadow(0 0 38px rgba(255,109,0,0.35));} 50%{filter:drop-shadow(0 0 26px rgba(255,109,0,1)) drop-shadow(0 0 56px rgba(255,109,0,0.55));} }
  .cta-eyebrow { font-family: 'Share Tech Mono', monospace; font-size: 0.65rem; letter-spacing: 0.38em; color: var(--cyan); text-transform: uppercase; margin-bottom: 1.1rem; }
  .cta-title { font-family: 'Orbitron', monospace; font-size: clamp(1.7rem,5vw,3rem); font-weight: 900; color: var(--white); letter-spacing: 0.08em; margin-bottom: 0.9rem; line-height: 1.1; }
  .cta-sub { color: var(--text-dim); font-size: 1rem; margin-bottom: 2.6rem; line-height: 1.7; }
  .btn-large { font-family: 'Orbitron', monospace; font-size: 0.92rem; font-weight: 900; letter-spacing: 0.22em; color: var(--black); background: var(--cyan); padding: 1.2rem 3.2rem; border: none; cursor: pointer; text-decoration: none; text-transform: uppercase; clip-path: polygon(13px 0%,100% 0%,calc(100% - 13px) 100%,0% 100%); transition: box-shadow 0.3s, transform 0.2s; display: inline-flex; align-items: center; gap: 0.7rem; }
  .btn-large:hover { box-shadow: var(--cyan-glow), 0 0 70px rgba(0,229,255,0.18), 0 18px 36px rgba(0,229,255,0.1); transform: translateY(-3px); }
  .btn-large::after { content: '→'; transition: transform 0.2s; }
  .btn-large:hover::after { transform: translateX(5px); }

  /* ── FOOTER ── */
  footer { border-top: 1px solid var(--border); padding: 1.7rem 2.5rem; display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 1rem; background: var(--dark); }
  .footer-brand { display: flex; align-items: center; gap: 0.65rem; }
  .footer-brand img { width: 24px; height: 24px; image-rendering: pixelated; filter: drop-shadow(0 0 4px rgba(255,109,0,0.6)); }
  .footer-brand-text { font-family: 'Orbitron', monospace; font-weight: 900; font-size: 0.8rem; letter-spacing: 0.28em; color: var(--white); }
  .footer-text { font-family: 'Share Tech Mono', monospace; font-size: 0.58rem; letter-spacing: 0.14em; color: var(--text-dim); text-transform: uppercase; }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp { from{opacity:0;transform:translateY(22px);} to{opacity:1;transform:none;} }
  @keyframes fadeIn { from{opacity:0;} to{opacity:1;} }
  .reveal { opacity: 0; transform: translateY(26px); transition: opacity 0.7s, transform 0.7s; }
  .reveal.visible { opacity: 1; transform: none; }

  /* ── MOBILE ── */
  @media (max-width: 768px) {
    nav { padding: 0.8rem 1.2rem; }
    .nav-links { display: none; }
    .about-grid, .why-grid, .rts-grid, .lore-inner { grid-template-columns: 1fr; gap: 2rem; }
    .lore-logos { justify-content: center; }
    .section-wrap { padding: 4rem 1.2rem; }
    #cta { padding: 5rem 1.2rem; }
    footer { padding: 1.4rem 1.2rem; }
  }
</style>
</head>
<body>

<!-- LOGOS AS DATA URLS (embedded) -->
<script>
const LOGO_OLD = "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/4gHYSUNDX1BST0ZJTEUAAQEAAAHIAAAAAAQwAABtbnRyUkdCIFhZWiAH4AABAAEAAAAAAABhY3NwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAA9tYAAQAAAADTLQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAlkZXNjAAAA8AAAACRyWFlaAAABFAAAABRnWFlaAAABKAAAABRiWFlaAAABPAAAABR3dHB0AAABUAAAABRyVFJDAAABZAAAAChnVFJDAAABZAAAAChiVFJDAAABZAAAAChjcHJ0AAABjAAAADxtbHVjAAAAAAAAAAEAAAAMZW5VUwAAAAgAAAAcAHMAUgBHAEJYWVogAAAAAAAAb6IAADj1AAADkFhZWiAAAAAAAABimQAAt4UAABjaWFlaIAAAAAAAACSgAAAPhAAAts9YWVogAAAAAAAA9tYAAQAAAADTLXBhcmEAAAAAAAQAAAACZmYAAPKnAAANWQAAE9AAAApbAAAAAAAAAABtbHVjAAAAAAAAAAEAAAAMZW5VUwAAACAAAAAcAEcAbwBvAGcAbABlACAASQBuAGMALgAgADIAMAAxADb/2wBDAAUDBAQEAwUEBAQFBQUGBwwIBwcHBw8LCwkMEQ8SEhEPERETFhwXExQaFRERGCEYGh0dHx8fExciJCIeJBweHx7/2wBDAQUFBQcGBw4ICA4eFBEUHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh7/wAARCAAoAC0DASIAAhEBAxEB/8QAGwAAAQUBAQAAAAAAAAAAAAAAAAUGBwgJAQL/xAAsEAABAwQBAwIGAgMAAAAAAAABAgMEAAUGERIHCCETQRQVIjEyYSORQkNx/8QAGAEAAwEBAAAAAAAAAAAAAAAAAwQFAAb/xAAiEQABBAEDBQEAAAAAAAAAAAABAAIDEQQFEiETIkFRYUL/2gAMAwEAAhEDEQA/AKZUUU9Lf0n6m3CBHnwcCyOTFktJeYeat7ikOIUNpUkgeQQQQayyf/b92+XDqTY05XOu0aHjyZDkVwMrJl+olII0koKOO1D/AC296VeufbTMwjEp2Z2K9MTLDbmmvi0TFkSi6t0NjglKOJT9aD5UD+X6qw3aBjt9xjoG7bMitE20zTeXnAxLZU0vgUo0rR86Oj/VL3cVZ7rf+3LLbTZLdKuNwfVG9GNGbLji+MllR0keToAn/gNMBjeiXVzajvyJRqYhvt23X3lZqVynyvo/1UQgrV08yZKUjZJtrugP6pjkHeqXVhKmJNQncptLVxLXwS5zKZHqK4o9MrHLkfYa3s1qVji1x8etzFkUTam4rSIJY+tssBADfBQ3tPHWjs7FZQ1Lli7kusljscGy2zLUMQYEZuLGb+WxVcG20hKU7U2SdAAbJJo0UoZdi1PzsF2UQRIW16Whcp64ONakF709+eSNDdeYjs5CVCIXeO9ngnY3Ua9ruc5R1C6JSL9ltyFwuCbu7HDoYba/jSlsgcW0pH3UfOt0tdc8ovmGdAsoyXG5ohXWEuOWHy0hzhzfZQr6VgpO0qUPI96bEwMW7auddprhqDYeqbIu/Kej790Uy4l4yPTKSF7QQNa81mD1djWWJ1MyCNjhi/KG5q0xPhnAtr0/bioE7H72afb/AHQ9cHWVtOZmgoWkpUPlUTyCNH/VUMk7O6UllDxwKXQYWA7GeXGQuv2uUUUUFUlYzto7grZ08xI4VfLM6q3OzHZi7gy5ycSpSUgJDevI2geeXv8AalruA7k7BlnTy64JjlmlPxbq2yty4SF+kplaHkOcQ3o8hpseeQ/L9eSiiCQhhb4Spw4zkDI/QFfFVmiiihppf//Z";
const LOGO_NEW = "data:image/jpeg;base64,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";
</script>

<!-- NAV -->
<nav>
  <a class="nav-brand" href="#">
    <img class="nav-logo-img" id="nav-logo-img" src="" alt="EMP logo">
    <span class="nav-title">EMP <span>Unpanzerforce</span></span>
  </a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#rts">RTS Universe</a></li>
    <li><a href="#features">Features</a></li>
    <li><a href="#rules">Rules</a></li>
  </ul>
  <a class="nav-cta" href="https://discord.gg/k6f2NS4Bg8" target="_blank">Join Discord</a>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-grid"></div>
  <div class="hero-glow"></div>
  <div id="particles"></div>
  <div class="corner tl"></div><div class="corner tr"></div>
  <div class="corner bl"></div><div class="corner br"></div>

  <div class="hero-eyebrow">// Active Discord Community · EMP Universe</div>

  <div class="hero-logos">
    <div class="hero-logo-wrap logo-old">
      <img class="hero-logo-img" id="hero-logo-old" src="" alt="EMP Panzerforce (old)">
      <span class="logo-label">Panzerforce (old)</span>
    </div>
    <div class="logo-divider">
      <span class="ld-txt">LORE</span>
      <div class="logo-arrow">→</div>
      <span class="ld-txt">EVENT</span>
    </div>
    <div class="hero-logo-wrap logo-new">
      <img class="hero-logo-img" id="hero-logo-new" src="" alt="EMP Unpanzerforce (current)">
      <span class="logo-label active">Unpanzerforce (now)</span>
    </div>
  </div>

  <h1 class="hero-title" data-text="EMP">EMP</h1>
  <div class="hero-subtitle">Unpanzerforce</div>
  <p class="hero-tagline">
    A community for <span class="c">War Thunder</span> · <span class="c">Minecraft</span> · <span class="c">Sprocket</span> · <span class="c">Chill</span><br>
    and an ever-evolving <span class="o">RTS universe</span> unlike anything else
  </p>

  <div class="hero-btns">
    <a class="btn-primary" href="https://discord.gg/k6f2NS4Bg8" target="_blank">⚡ Join Discord</a>
    <a class="btn-secondary" href="#rts">Explore the Universe</a>
  </div>

  <div class="hero-games">
    <span class="game-tag">⚔️ War Thunder Events</span>
    <span class="game-tag">🧱 Minecraft</span>
    <span class="game-tag">🛡️ Sprocket RTS</span>
    <span class="game-tag">🌍 Custom Nations</span>
    <span class="game-tag">🕹️ Chill Sessions</span>
    <span class="game-tag">⚙️ Tank Engineering</span>
    <span class="game-tag">👑 Faction Politics</span>
  </div>

  <div class="scroll-indicator">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<div class="divider"></div>

<!-- LORE BANNER -->
<div id="lore-banner">
  <div class="lore-inner">
    <div class="lore-text reveal">
      <div class="lore-eyebrow">⚠ Lore Event · Server History</div>
      <h3>The Fall of Panzerforce<br>— Rise of Unpanzerforce</h3>
      <p class="body-p" style="font-size:0.93rem;">
        EMP was once known as <strong style="color:var(--cyan)">EMP Panzerforce</strong>, a name bound to a chapter now defined by its most notorious figure: <strong style="color:var(--orange)">Panzermaker</strong> — a godlike entity and the primary villain of the EMP universe. Following in-universe events tied to Panzermaker's rise, the server underwent a canonical rebirth. The orange gear now marks the new era: <strong style="color:var(--orange)">EMP Unpanzerforce</strong>.
      </p>
    </div>
    <div class="lore-logos reveal">
      <div class="lore-logo-item old">
        <img id="lore-logo-old" src="" alt="EMP Panzerforce old logo">
        <div class="tag">EMP Panzerforce<br><span style="color:var(--text-dim);font-size:0.48rem;">DEPRECATED BY LORE</span></div>
      </div>
      <div class="lore-arrow">→</div>
      <div class="lore-logo-item new">
        <img id="lore-logo-new" src="" alt="EMP Unpanzerforce current logo">
        <div class="tag">EMP Unpanzerforce<br><span style="color:var(--orange);font-size:0.48rem;">CURRENT ERA</span></div>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- ABOUT -->
<div id="about" class="full-dark">
  <div class="section-wrap">
    <div class="about-grid">
      <div class="reveal">
        <div class="section-tag">About EMP</div>
        <h2>More Than a <span class="c">Server.</span></h2>
        <p class="body-p" style="margin-bottom:1rem;">EMP Unpanzerforce is a one-of-a-kind Discord built around gaming, community, and a living universe. Whether you're rolling into War Thunder operations, engineering tanks in Sprocket, surviving Minecraft, or just chilling — there's a place for you.</p>
        <p class="body-p">The community is active, the voice chats are alive, and the lore runs extraordinarily deep. EMP isn't just a server — it's a world with its own gods, history, factions, wars, and political drama.</p>
      </div>
      <div class="reveal">
        <div class="about-panel">
          <div class="about-corner tl"></div>
          <div class="about-corner br"></div>
          <div class="panel-header">
            <span>SYS::EMP-STATUS</span>
            <span class="panel-status">● ONLINE</span>
          </div>
          <div class="stat-row"><span class="stat-label">Status</span><span class="stat-val">ACTIVE</span></div>
          <div class="stat-row"><span class="stat-label">Current Era</span><span class="stat-val o">UNPANZERFORCE</span></div>
          <div class="stat-row"><span class="stat-label">Games</span><span class="stat-val w">WT · MC · Sprocket</span></div>
          <div class="stat-row"><span class="stat-label">RTS Universe</span><span class="stat-val">OPERATIONAL</span></div>
          <div class="stat-row"><span class="stat-label">Panzermaker Threat</span><span class="stat-val o">CONTAINED</span></div>
          <div class="stat-row"><span class="stat-label">War Thunder Events</span><span class="stat-val">ONGOING</span></div>
          <div class="stat-row"><span class="stat-label">Lore Depth</span><span class="stat-val">IMMEASURABLE</span></div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- RTS UNIVERSE -->
<div id="rts">
  <div class="section-wrap">
    <div class="reveal">
      <div class="section-tag">Sprocket RTS Universe</div>
      <h2>Build. Rule. <span class="o">Conquer.</span></h2>
      <p class="body-p">EMP hosts a fully community-driven RTS universe built inside Sprocket. Design your own tanks, forge your nation, build political alliances — and watch the world shift in real time. The roles, factions, and power structures run so deep that even veterans are still discovering new layers.</p>
    </div>
    <div class="rts-grid">
      <div class="rts-cards">
        <div class="rts-card reveal">
          <span class="rts-badge">CORE MECHANIC</span>
          <div class="rts-card-title">🏗️ Tank Engineering</div>
          <p class="rts-card-desc">Players design custom tanks from scratch using Sprocket's in-depth tools. Every nation has its own armored doctrine and design philosophy.</p>
        </div>
        <div class="rts-card reveal">
          <span class="rts-badge">WORLD SYSTEM</span>
          <div class="rts-card-title">🌍 Nation Building</div>
          <p class="rts-card-desc">Form your own country, expand your territory, and establish political relations with other player-run factions across the EMP world.</p>
        </div>
        <div class="rts-card reveal">
          <span class="rts-badge">DEEP LORE</span>
          <div class="rts-card-title">⚖️ Faction Politics</div>
          <p class="rts-card-desc">Alliances, betrayals, trade pacts, proxy wars. EMP's political landscape is shaped entirely by its members — no scripted events, pure player agency.</p>
        </div>
        <div class="rts-card villain reveal">
          <span class="rts-badge threat">⚠ THREAT: GOD-TIER</span>
          <div class="rts-card-title">☠ Panzermaker</div>
          <p class="rts-card-desc">The primary antagonist of the EMP universe. A godlike entity whose influence caused the collapse of the Panzerforce era and the rebirth of EMP as Unpanzerforce. His shadow still looms over server lore.</p>
        </div>
        <div class="rts-card reveal">
          <span class="rts-badge">ONGOING</span>
          <div class="rts-card-title">🎖️ Massive Role System</div>
          <p class="rts-card-desc">Dozens of unique roles tied to the RTS universe — factions, titles, ranks, lore positions. Even long-time members are still discovering new layers. The system is that deep.</p>
        </div>
      </div>

      <div class="rts-world reveal">
        <div class="rts-world-label">// EMP WORLD MAP · TERRITORY OVERVIEW</div>
        <div class="territory-map">
          <div class="territory"><span>Nordvik</span></div>
          <div class="territory center"><span>[ EMP CORE ]<br>Unpanzerforce<br>Territory</span></div>
          <div class="territory contested"><span>⚠ Contested</span></div>
          <div class="territory"><span>Kalmar</span></div>
          <div class="territory contested"><span>⚠ Panzer Ruins</span></div>
          <div class="territory"><span>Ironveld</span></div>
          <div class="territory"><span>Estmark</span></div>
          <div class="territory contested"><span>⚠ No Man's Land</span></div>
          <div class="territory"><span>Drakholm</span></div>
          <div class="territory"><span>Verath</span></div>
        </div>
        <div class="map-legend">
          <div class="map-key"><div class="map-swatch" style="background:rgba(0,229,255,0.04);border:1px solid rgba(0,229,255,0.08);"></div><span>Neutral Zone</span></div>
          <div class="map-key"><div class="map-swatch" style="background:rgba(255,109,0,0.04);border:1px solid rgba(255,109,0,0.12);"></div><span style="color:var(--orange)">Contested</span></div>
          <div class="map-key"><div class="map-swatch" style="background:rgba(0,229,255,0.07);border:1px solid var(--border);"></div><span style="color:var(--cyan)">EMP Core</span></div>
        </div>
        <div class="map-note">
          <span>⚠ Placeholder map · The real universe is shaped entirely by YOU and your fellow members</span>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- FEATURES -->
<div id="features" class="full-dark">
  <div class="section-wrap">
    <div class="reveal">
      <div class="section-tag">What We Offer</div>
      <h2>Server <span class="c">Features</span></h2>
    </div>
    <div class="features-grid">
      <div class="feat-card reveal"><span class="feat-num">01</span><span class="feat-icon">🟢</span><div class="feat-title">Always Active</div><p class="feat-desc">Real members, real conversations around the clock. EMP never goes quiet.</p></div>
      <div class="feat-card reveal"><span class="feat-num">02</span><span class="feat-icon">🎙️</span><div class="feat-title">Voice Chats</div><p class="feat-desc">Dedicated VC channels for gaming sessions, squad ops, and casual hangouts at any hour.</p></div>
      <div class="feat-card reveal"><span class="feat-num">03</span><span class="feat-icon">⚔️</span><div class="feat-title">War Thunder Events</div><p class="feat-desc">Organized community War Thunder events and competitive operations. Rally the squadron.</p></div>
      <div class="feat-card reveal"><span class="feat-num">04</span><span class="feat-icon">🛡️</span><div class="feat-title">Safe & Moderated</div><p class="feat-desc">Active moderation keeps EMP welcoming. Zero tolerance for harassment or toxicity.</p></div>
      <div class="feat-card reveal"><span class="feat-num">05</span><span class="feat-icon">⚙️</span><div class="feat-title">Custom Roles & Bots</div><p class="feat-desc">An enormous role ecosystem — from RTS universe titles to game-specific ranks. Layers within layers.</p></div>
      <div class="feat-card reveal"><span class="feat-num">06</span><span class="feat-icon">🌍</span><div class="feat-title">Living RTS Universe</div><p class="feat-desc">The Sprocket-based nation builder — design tanks, forge nations, shape history.</p></div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- WHY JOIN -->
<div id="why">
  <div class="section-wrap">
    <div class="why-grid">
      <div class="reveal">
        <div class="section-tag">Why EMP?</div>
        <h2>Join the <span class="c">Pulse.</span></h2>
        <p class="body-p">EMP isn't another dead Discord. It's a growing, living community with genuine depth — games, lore, politics, and people who actually show up every day.</p>
      </div>
      <div class="why-items">
        <div class="why-item reveal"><span class="why-bullet">[ 01 ]</span><div class="why-text"><strong>Always Online</strong><p>Find someone to play or chat with at any hour. The server never sleeps.</p></div></div>
        <div class="why-item reveal"><span class="why-bullet">[ 02 ]</span><div class="why-text"><strong>Unique RTS Experience</strong><p>No other Discord has a Sprocket-powered nation builder with this depth of lore and community-driven politics.</p></div></div>
        <div class="why-item reveal"><span class="why-bullet">[ 03 ]</span><div class="why-text"><strong>Multi-Game Community</strong><p>War Thunder, Minecraft, Sprocket, chill — all under one roof, all active, all welcoming.</p></div></div>
        <div class="why-item reveal"><span class="why-bullet">[ 04 ]</span><div class="why-text"><strong>Deep Lore to Explore</strong><p>A universe with gods, factions, wars, and history shaped entirely by members. You'll still be discovering things months in.</p></div></div>
        <div class="why-item reveal"><span class="why-bullet">[ 05 ]</span><div class="why-text"><strong>Real Community</strong><p>People who genuinely care about the server, the games, and each other.</p></div></div>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- RULES -->
<div id="rules" class="full-dark">
  <div class="section-wrap">
    <div class="reveal">
      <div class="section-tag">Community Standards</div>
      <h2>The <span class="c">Rules.</span></h2>
      <p class="body-p">EMP runs on mutual respect. Simple standards, consistently enforced.</p>
    </div>
    <div class="rules-grid">
      <div class="rule-card reveal"><div class="rule-num">01</div><div class="rule-title">Respect Everyone</div><p class="rule-desc">Treat all members with respect. No harassment, hate speech, or targeted negativity of any kind.</p></div>
      <div class="rule-card reveal"><div class="rule-num">02</div><div class="rule-title">No Spam</div><p class="rule-desc">Keep conversations meaningful. No flooding, repeated posts, or unsolicited self-promotion.</p></div>
      <div class="rule-card reveal"><div class="rule-num">03</div><div class="rule-title">Follow Discord ToS</div><p class="rule-desc">All standard Discord Terms of Service and Community Guidelines apply within EMP at all times.</p></div>
      <div class="rule-card reveal"><div class="rule-num">04</div><div class="rule-title">Keep It Clean</div><p class="rule-desc">Maintain a friendly, inclusive atmosphere. EMP is for everyone — keep it welcoming.</p></div>
    </div>
  </div>
</div>

<!-- FINAL CTA -->
<div id="cta">
  <div class="cta-inner">
    <div class="cta-logo reveal"><img id="cta-logo" src="" alt="EMP Unpanzerforce"></div>
    <div class="cta-eyebrow reveal">// Ready to Join the Universe?</div>
    <h2 class="cta-title reveal">Join <span class="c">EMP</span><br><span style="color:var(--orange);font-size:0.68em;letter-spacing:0.12em;">Unpanzerforce</span></h2>
    <p class="cta-sub reveal">The universe is alive. The maps are shifting. The tanks are rolling. Don't just watch — be part of it.</p>
    <a class="btn-large reveal" href="https://discord.gg/k6f2NS4Bg8" target="_blank">Join EMP Discord</a>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <div class="footer-brand">
    <img id="footer-logo" src="" alt="EMP logo">
    <span class="footer-brand-text">EMP Unpanzerforce</span>
  </div>
  <div class="footer-text">© 2026 EMP Community · All rights reserved</div>
  <div class="footer-text">War Thunder · Minecraft · Sprocket · Chill</div>
</footer>

<script>
  // Inject logos
  document.addEventListener('DOMContentLoaded', () => {
    ['nav-logo-img','hero-logo-new','lore-logo-new','cta-logo','footer-logo'].forEach(id => {
      const el = document.getElementById(id);
      if (el) el.src = LOGO_NEW;
    });
    ['hero-logo-old','lore-logo-old'].forEach(id => {
      const el = document.getElementById(id);
      if (el) el.src = LOGO_OLD;
    });
  });

  // Particles
  const pc = document.getElementById('particles');
  for (let i = 0; i < 25; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    const s = Math.random() > 0.8 ? 2 : 1;
    p.style.cssText = `left:${Math.random()*100}%;width:${s}px;height:${s}px;animation-duration:${7+Math.random()*10}s;animation-delay:${Math.random()*10}s;--dx:${(Math.random()-0.5)*80};`;
    pc.appendChild(p);
  }

  // Reveal on scroll
  const reveals = document.querySelectorAll('.reveal');
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) { setTimeout(() => e.target.classList.add('visible'), 60); obs.unobserve(e.target); }
    });
  }, { threshold: 0.1 });
  reveals.forEach(r => obs.observe(r));

  // Stagger delays
  document.querySelectorAll('.features-grid .feat-card').forEach((el,i) => { el.style.transitionDelay = `${i*70}ms`; });
  document.querySelectorAll('.rules-grid .rule-card').forEach((el,i) => { el.style.transitionDelay = `${i*70}ms`; });
  document.querySelectorAll('.rts-cards .rts-card').forEach((el,i) => { el.style.transitionDelay = `${i*75}ms`; });
</script>
</body>
</html>
