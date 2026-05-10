<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Naddiya Sheraz — Frontend Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Fira+Code:wght@400;500&display=swap" rel="stylesheet" />
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
 
  body {
    background: #0a0a0f;
    color: #e8e6ff;
    font-family: 'Space Grotesk', sans-serif;
    overflow-x: hidden;
    min-height: 100vh;
  }
 
  .noise {
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.6;
  }
 
  .grid-bg {
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(120,80,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(120,80,255,0.04) 1px, transparent 1px);
    background-size: 48px 48px;
    pointer-events: none;
    z-index: 0;
  }
 
  .glow-orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(100px);
    pointer-events: none;
    z-index: 0;
  }
  .orb1 { width: 500px; height: 500px; background: rgba(99,60,255,0.12); top: -200px; left: -150px; }
  .orb2 { width: 400px; height: 400px; background: rgba(0,200,160,0.08); bottom: 200px; right: -100px; }
  .orb3 { width: 300px; height: 300px; background: rgba(255,80,120,0.07); top: 50%; left: 50%; transform: translate(-50%,-50%); }
 
  .container {
    position: relative;
    z-index: 1;
    max-width: 900px;
    margin: 0 auto;
    padding: 0 24px 80px;
  }
 
  /* HERO */
  .hero {
    padding: 80px 0 60px;
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 40px;
    align-items: center;
    opacity: 0;
    transform: translateY(24px);
    animation: fadeUp 0.8s ease 0.1s forwards;
  }
 
  .hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(99,60,255,0.15);
    border: 1px solid rgba(99,60,255,0.3);
    border-radius: 100px;
    padding: 6px 14px;
    font-size: 12px;
    font-family: 'Fira Code', monospace;
    color: #a78bfa;
    margin-bottom: 20px;
  }
 
  .status-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: #00d4a0;
    animation: pulse 2s ease-in-out infinite;
  }
 
  .hero h1 {
    font-size: clamp(38px, 5vw, 62px);
    font-weight: 700;
    line-height: 1.1;
    letter-spacing: -2px;
    color: #fff;
  }
 
  .hero h1 .accent {
    background: linear-gradient(135deg, #7b4fff 0%, #00d4a0 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
 
  .hero-subtitle {
    margin-top: 16px;
    font-size: 16px;
    color: rgba(232,230,255,0.5);
    font-weight: 300;
    max-width: 480px;
    line-height: 1.7;
  }
 
  .hero-subtitle .highlight { color: #00d4a0; font-weight: 500; }
 
  .avatar-wrapper {
    position: relative;
    width: 140px;
    height: 140px;
    flex-shrink: 0;
    animation: float 4s ease-in-out infinite;
  }
 
  .avatar-ring {
    position: absolute;
    inset: -6px;
    border-radius: 50%;
    background: conic-gradient(from 0deg, #7b4fff, #00d4a0, #ff5080, #7b4fff);
    animation: spin 6s linear infinite;
  }
 
  .avatar-inner {
    position: absolute;
    inset: 3px;
    border-radius: 50%;
    background: #0a0a0f;
    display: flex;
    align-items: center;
    justify-content: center;
  }
 
  .avatar-initials {
    background: linear-gradient(135deg, #7b4fff, #00d4a0);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    font-size: 42px;
    font-weight: 700;
  }
 
  /* QUICK INFO */
  .quick-info {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    margin-top: 28px;
    opacity: 0;
    transform: translateY(20px);
    animation: fadeUp 0.8s ease 0.25s forwards;
  }
 
  .info-chip {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 8px 16px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 100px;
    font-size: 13px;
    color: rgba(232,230,255,0.65);
    transition: all 0.25s ease;
    cursor: default;
    text-decoration: none;
  }
 
  .info-chip:hover {
    background: rgba(123,79,255,0.12);
    border-color: rgba(123,79,255,0.4);
    color: #e8e6ff;
    transform: translateY(-2px);
  }
 
  /* SECTIONS */
  .section {
    margin-top: 64px;
    opacity: 0;
    transform: translateY(20px);
  }
 
  .section.visible {
    animation: fadeUp 0.7s ease forwards;
  }
 
  .section-label {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 28px;
  }
 
  .section-label span {
    font-family: 'Fira Code', monospace;
    font-size: 11px;
    color: #7b4fff;
    letter-spacing: 2px;
    text-transform: uppercase;
  }
 
  .section-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, rgba(123,79,255,0.3), transparent);
  }
 
  /* TECH GRID */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
    gap: 10px;
  }
 
  .tech-pill {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    padding: 16px 10px;
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 12px;
    font-size: 12px;
    color: rgba(232,230,255,0.6);
    transition: all 0.3s cubic-bezier(0.34,1.56,0.64,1);
    cursor: default;
  }
 
  .tech-pill:hover {
    transform: translateY(-4px) scale(1.04);
    border-color: rgba(123,79,255,0.35);
    color: #fff;
    background: rgba(123,79,255,0.08);
  }
 
  .tech-pill:hover .tech-icon-circle {
    box-shadow: 0 0 16px var(--tp, rgba(123,79,255,0.4));
  }
 
  .tech-icon-circle {
    width: 38px; height: 38px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(255,255,255,0.1);
    transition: box-shadow 0.3s ease;
    font-size: 20px;
  }
 
  .tech-name { font-size: 11px; font-weight: 500; text-align: center; }
 
  /* STATS */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }
 
  .stat-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 16px;
    padding: 24px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s ease;
  }
 
  .stat-card::after {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(123,79,255,0.5), transparent);
    opacity: 0;
    transition: opacity 0.3s ease;
  }
 
  .stat-card:hover {
    border-color: rgba(123,79,255,0.2);
    background: rgba(123,79,255,0.06);
    transform: translateY(-2px);
  }
 
  .stat-card:hover::after { opacity: 1; }
 
  .stat-num {
    font-size: 36px;
    font-weight: 700;
    letter-spacing: -2px;
    background: linear-gradient(135deg, #fff, rgba(255,255,255,0.6));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
  }
 
  .stat-label {
    margin-top: 8px;
    font-size: 12px;
    color: rgba(232,230,255,0.4);
    font-family: 'Fira Code', monospace;
    letter-spacing: 0.5px;
  }
 
  .stat-icon {
    position: absolute;
    top: 20px; right: 20px;
    font-size: 18px;
    opacity: 0.25;
  }
 
  /* COURSES */
  .courses-list { display: flex; flex-direction: column; gap: 12px; }
 
  .course-item {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 20px 24px;
    background: rgba(255,255,255,0.025);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 12px;
    transition: all 0.3s ease;
    cursor: default;
  }
 
  .course-item:hover {
    background: rgba(0,212,160,0.05);
    border-color: rgba(0,212,160,0.2);
    transform: translateX(4px);
  }
 
  .course-num {
    font-family: 'Fira Code', monospace;
    font-size: 11px;
    color: #7b4fff;
    min-width: 24px;
  }
 
  .course-title {
    font-size: 14px;
    font-weight: 500;
    color: rgba(232,230,255,0.85);
    flex: 1;
  }
 
  .course-tag {
    font-size: 11px;
    padding: 4px 10px;
    background: rgba(0,212,160,0.1);
    border: 1px solid rgba(0,212,160,0.2);
    border-radius: 100px;
    color: #00d4a0;
    font-family: 'Fira Code', monospace;
    white-space: nowrap;
  }
 
  /* CONNECT */
  .connect-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }
 
  .connect-card {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 20px 24px;
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 14px;
    text-decoration: none;
    transition: all 0.3s cubic-bezier(0.34,1.56,0.64,1);
    color: inherit;
  }
 
  .connect-card:hover {
    transform: translateY(-3px);
    border-color: var(--c);
    background: rgba(var(--cr), 0.06);
    box-shadow: 0 8px 32px rgba(var(--cr), 0.12);
  }
 
  .connect-icon {
    width: 40px; height: 40px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    flex-shrink: 0;
    background: rgba(var(--cr), 0.12);
    border: 1px solid rgba(var(--cr), 0.2);
  }
 
  .connect-label {
    font-size: 11px;
    color: rgba(232,230,255,0.4);
    font-family: 'Fira Code', monospace;
    margin-bottom: 2px;
  }
 
  .connect-value {
    font-size: 13px;
    font-weight: 500;
    color: rgba(232,230,255,0.85);
  }
 
  /* QUOTE */
  .quote-block {
    position: relative;
    padding: 32px 36px;
    background: rgba(123,79,255,0.06);
    border: 1px solid rgba(123,79,255,0.15);
    border-radius: 16px;
    overflow: hidden;
  }
 
  .quote-block::before {
    content: '"';
    position: absolute;
    top: -20px; left: 20px;
    font-size: 120px;
    color: rgba(123,79,255,0.1);
    font-family: Georgia, serif;
    line-height: 1;
    pointer-events: none;
  }
 
  .quote-text {
    font-size: 17px;
    font-style: italic;
    color: rgba(232,230,255,0.7);
    line-height: 1.7;
    position: relative;
    z-index: 1;
  }
 
  .quote-author {
    margin-top: 12px;
    font-size: 12px;
    font-family: 'Fira Code', monospace;
    color: #7b4fff;
  }
 
  /* FOOTER */
  .footer {
    margin-top: 80px;
    padding-top: 32px;
    border-top: 1px solid rgba(255,255,255,0.06);
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 16px;
  }
 
  .footer-sig {
    font-family: 'Fira Code', monospace;
    font-size: 12px;
    color: rgba(232,230,255,0.25);
  }
 
  .footer-sig span { color: #ff5080; }
 
  .footer-links { display: flex; gap: 8px; }
 
  .footer-links a {
    width: 36px; height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 8px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.08);
    color: rgba(232,230,255,0.5);
    text-decoration: none;
    font-size: 15px;
    transition: all 0.25s ease;
  }
 
  .footer-links a:hover {
    background: rgba(123,79,255,0.15);
    border-color: rgba(123,79,255,0.3);
    color: #7b4fff;
    transform: translateY(-2px);
  }
 
  /* ANIMATIONS */
  @keyframes fadeUp { to { opacity: 1; transform: translateY(0); } }
  @keyframes spin { to { transform: rotate(360deg); } }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.6; transform: scale(0.85); }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-8px); }
  }
 
  @media (max-width: 600px) {
    .hero { grid-template-columns: 1fr; }
    .avatar-wrapper { margin: 0 auto; }
    .stats-row { grid-template-columns: 1fr; }
    .connect-grid { grid-template-columns: 1fr; }
    .course-tag { display: none; }
  }
</style>
</head>
<body>
 
<div class="noise"></div>
<div class="grid-bg"></div>
<div class="glow-orb orb1"></div>
<div class="glow-orb orb2"></div>
<div class="glow-orb orb3"></div>
 
<div class="container">
 
  <!-- HERO -->
  <div class="hero">
    <div>
      <div class="hero-badge">
        <span class="status-dot"></span>
        <span>available for collaborations</span>
      </div>
      <h1>Naddiya<br><span class="accent">Sheraz</span></h1>
      <p class="hero-subtitle">
        Frontend Developer &amp; Instructor turning
        <span class="highlight">☕ coffee</span> into clean, maintainable code —
        mentoring the next generation of developers.
      </p>
    </div>
    <div class="avatar-wrapper">
      <div class="avatar-ring"></div>
      <div class="avatar-inner">
        <span class="avatar-initials">NS</span>
      </div>
    </div>
  </div>
 
  <!-- QUICK INFO -->
  <div class="quick-info">
    <a class="info-chip" href="mailto:naddiyasheraz18@gmail.com">
      <span>✉</span> naddiyasheraz18@gmail.com
    </a>
    <a class="info-chip" href="https://linkedin.com/in/naddiya-sheraz-771978310" target="_blank">
      <span>💼</span> LinkedIn
    </a>
    <span class="info-chip"><span>📍</span> Open Source Contributor</span>
    <span class="info-chip"><span>🎓</span> Instructor</span>
  </div>
 
  <!-- STATS -->
  <div class="section" id="s1">
    <div class="section-label">
      <span>// at a glance</span>
      <div class="section-line"></div>
    </div>
    <div class="stats-row">
      <div class="stat-card">
        <span class="stat-icon">⚡</span>
        <div class="stat-num">10+</div>
        <div class="stat-label">technologies</div>
      </div>
      <div class="stat-card">
        <span class="stat-icon">📚</span>
        <div class="stat-num">3</div>
        <div class="stat-label">courses &amp; bootcamps</div>
      </div>
      <div class="stat-card">
        <span class="stat-icon">🚀</span>
        <div class="stat-num">∞</div>
        <div class="stat-label">lines of clean code</div>
      </div>
    </div>
  </div>
 
  <!-- TECH STACK -->
  <div class="section" id="s2">
    <div class="section-label">
      <span>// tech stack</span>
      <div class="section-line"></div>
    </div>
    <div class="tech-grid">
      <div class="tech-pill" style="--tp:#e34c26"><div class="tech-icon-circle">🟠</div><span class="tech-name">HTML5</span></div>
      <div class="tech-pill" style="--tp:#1572b6"><div class="tech-icon-circle">🔵</div><span class="tech-name">CSS3</span></div>
      <div class="tech-pill" style="--tp:#f7df1e"><div class="tech-icon-circle">🟡</div><span class="tech-name">JavaScript</span></div>
      <div class="tech-pill" style="--tp:#3178c6"><div class="tech-icon-circle">💙</div><span class="tech-name">TypeScript</span></div>
      <div class="tech-pill" style="--tp:#61dafb"><div class="tech-icon-circle">⚛️</div><span class="tech-name">React</span></div>
      <div class="tech-pill" style="--tp:#6da55f"><div class="tech-icon-circle">🟢</div><span class="tech-name">Node.js</span></div>
      <div class="tech-pill" style="--tp:#e0234e"><div class="tech-icon-circle">🔴</div><span class="tech-name">NestJS</span></div>
      <div class="tech-pill" style="--tp:#4ea94b"><div class="tech-icon-circle">🍃</div><span class="tech-name">MongoDB</span></div>
      <div class="tech-pill" style="--tp:#039be5"><div class="tech-icon-circle">🔥</div><span class="tech-name">Firebase</span></div>
      <div class="tech-pill" style="--tp:#8511fa"><div class="tech-icon-circle">🟣</div><span class="tech-name">Bootstrap</span></div>
      <div class="tech-pill" style="--tp:#646cff"><div class="tech-icon-circle">⚡</div><span class="tech-name">Vite</span></div>
      <div class="tech-pill" style="--tp:#ff6c37"><div class="tech-icon-circle">🟠</div><span class="tech-name">Postman</span></div>
    </div>
  </div>
 
  <!-- COURSES -->
  <div class="section" id="s3">
    <div class="section-label">
      <span>// courses &amp; workshops</span>
      <div class="section-line"></div>
    </div>
    <div class="courses-list">
      <div class="course-item">
        <span class="course-num">01</span>
        <span class="course-title">Frontend Development Bootcamp</span>
        <span class="course-tag">HTML · CSS · JS · React</span>
      </div>
      <div class="course-item">
        <span class="course-num">02</span>
        <span class="course-title">Advanced JavaScript &amp; TypeScript Training</span>
        <span class="course-tag">Advanced</span>
      </div>
      <div class="course-item">
        <span class="course-num">03</span>
        <span class="course-title">Open-Source Contribution Workshops</span>
        <span class="course-tag">OSS</span>
      </div>
    </div>
  </div>
 
  <!-- QUOTE -->
  <div class="section" id="s4">
    <div class="section-label">
      <span>// dev philosophy</span>
      <div class="section-line"></div>
    </div>
    <div class="quote-block">
      <p class="quote-text">
        Clean code is not written by following rules. You know you are working on clean code
        when each function you read turns out to be pretty much what you expected.
      </p>
      <p class="quote-author">— Robert C. Martin</p>
    </div>
  </div>
 
  <!-- CONNECT -->
  <div class="section" id="s5">
    <div class="section-label">
      <span>// let's connect</span>
      <div class="section-line"></div>
    </div>
    <div class="connect-grid">
      <a class="connect-card" href="mailto:naddiyasheraz18@gmail.com"
         style="--c:rgba(255,80,120,0.4);--cr:255,80,120;">
        <div class="connect-icon" style="--cr:255,80,120;">✉️</div>
        <div>
          <div class="connect-label">email</div>
          <div class="connect-value">naddiyasheraz18@gmail.com</div>
        </div>
      </a>
      <a class="connect-card" href="https://linkedin.com/in/naddiya-sheraz-771978310" target="_blank"
         style="--c:rgba(0,119,181,0.4);--cr:0,119,181;">
        <div class="connect-icon" style="--cr:0,119,181;">💼</div>
        <div>
          <div class="connect-label">linkedin</div>
          <div class="connect-value">Naddiya Sheraz</div>
        </div>
      </a>
      <div class="connect-card" style="--c:rgba(123,79,255,0.4);--cr:123,79,255;cursor:default;">
        <div class="connect-icon" style="--cr:123,79,255;">🤝</div>
        <div>
          <div class="connect-label">open to</div>
          <div class="connect-value">Mentorship &amp; Freelance</div>
        </div>
      </div>
      <div class="connect-card" style="--c:rgba(0,212,160,0.4);--cr:0,212,160;cursor:default;">
        <div class="connect-icon" style="--cr:0,212,160;">🌐</div>
        <div>
          <div class="connect-label">open to</div>
          <div class="connect-value">Collaborations &amp; OSS</div>
        </div>
      </div>
    </div>
  </div>
 
  <!-- FOOTER -->
  <div class="footer">
    <span class="footer-sig">crafted with <span>♥</span> &amp; too much coffee — naddiyasheraz</span>
    <div class="footer-links">
      <a href="mailto:naddiyasheraz18@gmail.com" title="Email">✉</a>
      <a href="https://linkedin.com/in/naddiya-sheraz-771978310" target="_blank" title="LinkedIn">in</a>
      <a href="https://github.com/NaddiyaSheraz" target="_blank" title="GitHub">⌥</a>
    </div>
  </div>
 
</div>
 
<script>
  const sections = document.querySelectorAll('.section');
  const io = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        io.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });
  sections.forEach(s => io.observe(s));
</script>
 
</body>
</html>
<!-- Proudly built with GPRM -->
