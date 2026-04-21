<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Eiker — Music Producer</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Mono:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
 
  :root {
    --bg: #080808;
    --bg2: #111111;
    --bg3: #181818;
    --border: rgba(255,255,255,0.07);
    --text: #f0ede8;
    --muted: rgba(240,237,232,0.45);
    --accent: #c8f060;
    --accent2: #60d0f0;
    --accent-dim: rgba(200,240,96,0.12);
  }
 
  html { scroll-behavior: smooth; }
 
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }
 
  /* Grain overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    opacity: 0.35;
    pointer-events: none;
    z-index: 999;
  }
 
  .container {
    max-width: 680px;
    margin: 0 auto;
    padding: 0 24px;
  }
 
  /* ── HERO ── */
  .hero {
    padding: 100px 0 80px;
    position: relative;
  }
 
  .hero-eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.18em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 28px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.1s;
  }
 
  .hero-name {
    font-size: clamp(64px, 15vw, 96px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.03em;
    margin-bottom: 28px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.2s;
  }
 
  .hero-name span {
    display: block;
    color: var(--accent);
  }
 
  .hero-tagline {
    font-size: 17px;
    font-weight: 400;
    color: var(--muted);
    line-height: 1.6;
    max-width: 420px;
    margin-bottom: 40px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.3s;
  }
 
  /* Credential badge */
  .credential {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    background: var(--accent-dim);
    border: 1px solid rgba(200,240,96,0.25);
    border-radius: 4px;
    padding: 10px 16px;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.4s;
  }
 
  .credential-dot {
    width: 7px;
    height: 7px;
    background: var(--accent);
    border-radius: 50%;
    flex-shrink: 0;
    animation: pulse 2s ease infinite;
  }
 
  .credential-text {
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--accent);
    letter-spacing: 0.02em;
  }
 
  .cta-row {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.5s;
  }
 
  .btn-primary {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: var(--accent);
    color: #080808;
    font-family: 'Syne', sans-serif;
    font-size: 14px;
    font-weight: 700;
    letter-spacing: 0.02em;
    padding: 14px 24px;
    border-radius: 4px;
    text-decoration: none;
    transition: transform 0.15s, box-shadow 0.15s;
  }
 
  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 32px rgba(200,240,96,0.25);
  }
 
  .btn-ghost {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: transparent;
    color: var(--text);
    font-family: 'Syne', sans-serif;
    font-size: 14px;
    font-weight: 500;
    padding: 14px 24px;
    border: 1px solid var(--border);
    border-radius: 4px;
    text-decoration: none;
    transition: border-color 0.15s, background 0.15s;
  }
 
  .btn-ghost:hover {
    border-color: rgba(255,255,255,0.2);
    background: rgba(255,255,255,0.04);
  }
 
  /* ── DIVIDER ── */
  .divider {
    height: 1px;
    background: var(--border);
    margin: 0;
  }
 
  /* ── SECTION ── */
  section {
    padding: 72px 0;
  }
 
  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.18em;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 36px;
  }
 
  /* ── TRACKS ── */
  .tracks { display: flex; flex-direction: column; gap: 2px; }
 
  .track {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 20px 22px;
    cursor: pointer;
    transition: border-color 0.15s, background 0.15s;
    position: relative;
    overflow: hidden;
  }
 
  .track:hover {
    border-color: rgba(255,255,255,0.14);
    background: var(--bg3);
  }
 
  .track-top {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 12px;
    margin-bottom: 8px;
  }
 
  .track-name {
    font-size: 15px;
    font-weight: 600;
    letter-spacing: -0.01em;
  }
 
  .track-tag {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 3px 8px;
    border-radius: 20px;
    flex-shrink: 0;
  }
 
  .tag-commercial { background: rgba(200,240,96,0.12); color: var(--accent); border: 1px solid rgba(200,240,96,0.2); }
  .tag-ghost { background: rgba(96,208,240,0.1); color: var(--accent2); border: 1px solid rgba(96,208,240,0.2); }
  .tag-brand { background: rgba(255,160,80,0.1); color: #ffa050; border: 1px solid rgba(255,160,80,0.2); }
 
  .track-desc {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.5;
    margin-bottom: 16px;
  }
 
  /* Fake waveform */
  .waveform {
    display: flex;
    align-items: center;
    gap: 2px;
    height: 32px;
    margin-bottom: 12px;
  }
 
  .waveform-bar {
    width: 3px;
    border-radius: 2px;
    background: rgba(255,255,255,0.12);
    transition: background 0.2s;
  }
 
  .track:hover .waveform-bar { background: rgba(255,255,255,0.2); }
  .track.playing .waveform-bar { background: var(--accent); animation: wave 0.8s ease infinite alternate; }
 
  .track-footer {
    display: flex;
    align-items: center;
    gap: 10px;
  }
 
  .play-btn {
    width: 28px;
    height: 28px;
    border-radius: 50%;
    border: 1px solid var(--border);
    background: transparent;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    color: var(--text);
    flex-shrink: 0;
    transition: border-color 0.15s, background 0.15s;
  }
 
  .track.playing .play-btn {
    background: var(--accent);
    border-color: var(--accent);
    color: #080808;
  }
 
  .track-meta {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
  }
 
  /* ── SERVICES ── */
  .services { display: flex; flex-direction: column; gap: 2px; }
 
  .service {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 16px;
    padding: 22px 0;
    border-bottom: 1px solid var(--border);
    transition: opacity 0.15s;
  }
 
  .service:first-child { border-top: 1px solid var(--border); }
 
  .service:hover { opacity: 0.75; }
 
  .service-left { flex: 1; }
 
  .service-name {
    font-size: 16px;
    font-weight: 600;
    letter-spacing: -0.01em;
    margin-bottom: 4px;
  }
 
  .service-desc {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.5;
  }
 
  .service-price {
    text-align: right;
    flex-shrink: 0;
  }
 
  .price-from {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.1em;
    color: var(--muted);
    text-transform: uppercase;
    display: block;
    margin-bottom: 2px;
  }
 
  .price-amount {
    font-size: 18px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: -0.02em;
  }
 
  .service-delivery {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    margin-top: 2px;
  }
 
  /* ── CONTACT ── */
  .contact-block {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 48px 40px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
 
  .contact-block::before {
    content: '';
    position: absolute;
    top: -60px;
    left: 50%;
    transform: translateX(-50%);
    width: 300px;
    height: 300px;
    background: radial-gradient(circle, rgba(200,240,96,0.06) 0%, transparent 70%);
    pointer-events: none;
  }
 
  .contact-title {
    font-size: clamp(28px, 6vw, 40px);
    font-weight: 800;
    letter-spacing: -0.03em;
    margin-bottom: 12px;
    line-height: 1.1;
  }
 
  .contact-sub {
    font-size: 14px;
    color: var(--muted);
    margin-bottom: 32px;
    line-height: 1.6;
  }
 
  .contact-note {
    margin-top: 20px;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.05em;
  }
 
  /* ── FOOTER ── */
  footer {
    padding: 32px 0;
    border-top: 1px solid var(--border);
  }
 
  .footer-inner {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 12px;
    flex-wrap: wrap;
  }
 
  .footer-name {
    font-size: 13px;
    font-weight: 600;
    color: var(--muted);
  }
 
  .footer-copy {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: rgba(240,237,232,0.2);
  }
 
  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }
 
  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50%       { opacity: 0.4; }
  }
 
  @keyframes wave {
    from { transform: scaleY(0.4); }
    to   { transform: scaleY(1); }
  }
 
  /* Staggered wave animation */
  .track.playing .waveform-bar:nth-child(1)  { animation-delay: 0.0s; }
  .track.playing .waveform-bar:nth-child(2)  { animation-delay: 0.05s; }
  .track.playing .waveform-bar:nth-child(3)  { animation-delay: 0.1s; }
  .track.playing .waveform-bar:nth-child(4)  { animation-delay: 0.15s; }
  .track.playing .waveform-bar:nth-child(5)  { animation-delay: 0.2s; }
  .track.playing .waveform-bar:nth-child(6)  { animation-delay: 0.1s; }
  .track.playing .waveform-bar:nth-child(7)  { animation-delay: 0.05s; }
  .track.playing .waveform-bar:nth-child(8)  { animation-delay: 0.0s; }
  .track.playing .waveform-bar:nth-child(9)  { animation-delay: 0.15s; }
  .track.playing .waveform-bar:nth-child(10) { animation-delay: 0.2s; }
  .track.playing .waveform-bar:nth-child(11) { animation-delay: 0.08s; }
  .track.playing .waveform-bar:nth-child(12) { animation-delay: 0.03s; }
  .track.playing .waveform-bar:nth-child(13) { animation-delay: 0.18s; }
  .track.playing .waveform-bar:nth-child(14) { animation-delay: 0.12s; }
  .track.playing .waveform-bar:nth-child(15) { animation-delay: 0.07s; }
  .track.playing .waveform-bar:nth-child(16) { animation-delay: 0.02s; }
  .track.playing .waveform-bar:nth-child(17) { animation-delay: 0.16s; }
  .track.playing .waveform-bar:nth-child(18) { animation-delay: 0.09s; }
  .track.playing .waveform-bar:nth-child(19) { animation-delay: 0.04s; }
  .track.playing .waveform-bar:nth-child(20) { animation-delay: 0.14s; }
 
  @media (max-width: 480px) {
    .hero { padding: 72px 0 56px; }
    .contact-block { padding: 36px 24px; }
    .service { flex-direction: column; align-items: flex-start; }
    .service-price { text-align: left; }
  }
</style>
</head>
<body>
 
<div class="container">
 
  <!-- HERO -->
  <div class="hero">
    <p class="hero-eyebrow">Music Producer · Sync Licensing</p>
    <h1 class="hero-name">
      Eiker<span>.</span>
    </h1>
    <p class="hero-tagline">
      Music for brands and content creators. Commercial-ready tracks, fast delivery, no label middlemen.
    </p>
    <div class="credential">
      <span class="credential-dot"></span>
      <span class="credential-text">Work licensed for Twix — international advertising campaign</span>
    </div>
    <div class="cta-row">
      <a href="https://wa.me/549TUNUMERO" class="btn-primary">
        Work with me →
      </a>
      <a href="#tracks" class="btn-ghost">Listen</a>
    </div>
  </div>
 
  <div class="divider"></div>
 
  <!-- TRACKS -->
  <section id="tracks">
    <p class="section-label">// Selected work</p>
    <div class="tracks">
 
      <!-- Track 1 -->
      <div class="track" onclick="togglePlay(this)">
        <div class="track-top">
          <span class="track-name">Untitled Commercial 01</span>
          <span class="track-tag tag-commercial">Commercial</span>
        </div>
        <p class="track-desc">Produced for brand advertising. High-energy, radio-ready arrangement. Sync license available.</p>
        <div class="waveform" id="wf1"></div>
        <div class="track-footer">
          <button class="play-btn" aria-label="Play track">
            <svg width="10" height="12" viewBox="0 0 10 12" fill="currentColor"><path d="M0 0l10 6-10 6z"/></svg>
          </button>
          <span class="track-meta">Replace with your SoundCloud embed · 3:24</span>
        </div>
      </div>
 
      <!-- Track 2 -->
      <div class="track" onclick="togglePlay(this)">
        <div class="track-top">
          <span class="track-name">Ghost Beat 07</span>
          <span class="track-tag tag-ghost">Ghost Production</span>
        </div>
        <p class="track-desc">Full exclusive beat. Mixed and mastered, vocal-ready. Delivered without credit.</p>
        <div class="waveform" id="wf2"></div>
        <div class="track-footer">
          <button class="play-btn" aria-label="Play track">
            <svg width="10" height="12" viewBox="0 0 10 12" fill="currentColor"><path d="M0 0l10 6-10 6z"/></svg>
          </button>
          <span class="track-meta">Replace with your SoundCloud embed · 2:58</span>
        </div>
      </div>
 
      <!-- Track 3 -->
      <div class="track" onclick="togglePlay(this)">
        <div class="track-top">
          <span class="track-name">Brand Intro Pack — Sample</span>
          <span class="track-tag tag-brand">Brand Sound</span>
        </div>
        <p class="track-desc">Jingle + intro + two background variations. Built for content creators with a defined identity.</p>
        <div class="waveform" id="wf3"></div>
        <div class="track-footer">
          <button class="play-btn" aria-label="Play track">
            <svg width="10" height="12" viewBox="0 0 10 12" fill="currentColor"><path d="M0 0l10 6-10 6z"/></svg>
          </button>
          <span class="track-meta">Replace with your SoundCloud embed · 1:40</span>
        </div>
      </div>
 
    </div>
  </section>
 
  <div class="divider"></div>
 
  <!-- SERVICES -->
  <section id="services">
    <p class="section-label">// Services</p>
    <div class="services">
 
      <div class="service">
        <div class="service-left">
          <p class="service-name">Commercial Music Production</p>
          <p class="service-desc">Original track for advertising, brand content, or campaigns. Sync licensing included.</p>
          <p class="service-delivery">Delivery: 5–7 days</p>
        </div>
        <div class="service-price">
          <span class="price-from">from</span>
          <span class="price-amount">$350</span>
        </div>
      </div>
 
      <div class="service">
        <div class="service-left">
          <p class="service-name">Ghost Production</p>
          <p class="service-desc">Complete exclusive beat. Mixed, mastered, vocal-ready. No credit to producer.</p>
          <p class="service-delivery">Delivery: 3–5 days</p>
        </div>
        <div class="service-price">
          <span class="price-from">from</span>
          <span class="price-amount">$200</span>
        </div>
      </div>
 
      <div class="service">
        <div class="service-left">
          <p class="service-name">Brand Sound Package</p>
          <p class="service-desc">Jingle + intro/outro + 2 background variations. Built for YouTubers, podcasters, streamers.</p>
          <p class="service-delivery">Delivery: 5 days</p>
        </div>
        <div class="service-price">
          <span class="price-from">from</span>
          <span class="price-amount">$450</span>
        </div>
      </div>
 
    </div>
  </section>
 
  <div class="divider"></div>
 
  <!-- CONTACT -->
  <section>
    <div class="contact-block">
      <h2 class="contact-title">Ready to work?</h2>
      <p class="contact-sub">
        Tell me what you need. I'll tell you if I can deliver it and at what price.<br>
        No agencies, no waitlists. Direct.
      </p>
      <a href="https://wa.me/549TUNUMERO" class="btn-primary" style="font-size:15px; padding:16px 32px;">
        Write me on WhatsApp →
      </a>
      <p class="contact-note">50% upfront · Secure delivery · Commercial rights included</p>
    </div>
  </section>
 
  <!-- FOOTER -->
  <footer>
    <div class="footer-inner">
      <span class="footer-name">Eiker — Music Producer</span>
      <span class="footer-copy">Sync licensing verified · International credits</span>
    </div>
  </footer>
 
</div>
 
<script>
  // Generate waveform bars
  ['wf1','wf2','wf3'].forEach(id => {
    const el = document.getElementById(id);
    const heights = [18,28,22,36,24,40,30,20,38,26,32,18,42,28,36,22,30,24,38,20];
    heights.forEach(h => {
      const bar = document.createElement('div');
      bar.className = 'waveform-bar';
      bar.style.height = h + 'px';
      el.appendChild(bar);
    });
  });
 
  // Play toggle (visual only — replace with actual audio embed)
  let current = null;
  function togglePlay(track) {
    if (current && current !== track) {
      current.classList.remove('playing');
      current.querySelector('.play-btn svg').innerHTML = '<path d="M0 0l10 6-10 6z"/>';
    }
    if (track.classList.contains('playing')) {
      track.classList.remove('playing');
      track.querySelector('.play-btn svg').innerHTML = '<path d="M0 0l10 6-10 6z"/>';
      current = null;
    } else {
      track.classList.add('playing');
      track.querySelector('.play-btn svg').innerHTML = '<rect x="0" y="0" width="4" height="12"/><rect x="6" y="0" width="4" height="12"/>';
      current = track;
    }
  }
</script>
 
</body>
</html>
 
