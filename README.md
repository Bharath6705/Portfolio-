<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Bharath G — ECE Engineer</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #0a0a0f;
      --surface: #111118;
      --card: #16161f;
      --border: #2a2a3a;
      --accent: #00e5c3;
      --accent2: #7c5cfc;
      --text: #e8e8f0;
      --muted: #7070a0;
      --font-display: 'Syne', sans-serif;
      --font-mono: 'DM Mono', monospace;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-display);
      overflow-x: hidden;
    }

    /* ── NOISE OVERLAY ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='1'/%3E%3C/svg%3E");
      opacity: 0.03;
      pointer-events: none;
      z-index: 9999;
    }

    /* ── GRID BACKGROUND ── */
    .grid-bg {
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(0,229,195,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,229,195,0.03) 1px, transparent 1px);
      background-size: 60px 60px;
      pointer-events: none;
      z-index: 0;
    }

    /* ── GLOW BLOBS ── */
    .blob {
      position: fixed;
      border-radius: 50%;
      filter: blur(120px);
      pointer-events: none;
      z-index: 0;
    }
    .blob-1 {
      width: 500px; height: 500px;
      background: rgba(0,229,195,0.07);
      top: -100px; left: -100px;
      animation: drift 14s ease-in-out infinite alternate;
    }
    .blob-2 {
      width: 400px; height: 400px;
      background: rgba(124,92,252,0.08);
      bottom: -80px; right: -80px;
      animation: drift 18s ease-in-out infinite alternate-reverse;
    }
    @keyframes drift {
      from { transform: translate(0,0) scale(1); }
      to   { transform: translate(40px, 30px) scale(1.1); }
    }

    /* ── LAYOUT ── */
    main { position: relative; z-index: 1; }

    section { max-width: 960px; margin: 0 auto; padding: 80px 24px; }

    /* ── NAV ── */
    nav {
      position: fixed; top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 18px 40px;
      background: rgba(10,10,15,0.75);
      backdrop-filter: blur(18px);
      border-bottom: 1px solid var(--border);
    }
    .nav-logo {
      font-size: 1rem;
      font-weight: 800;
      letter-spacing: 0.08em;
      color: var(--accent);
      font-family: var(--font-mono);
    }
    .nav-links { display: flex; gap: 32px; }
    .nav-links a {
      text-decoration: none;
      font-size: 0.78rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
      transition: color 0.2s;
      font-weight: 600;
    }
    .nav-links a:hover { color: var(--accent); }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding-top: 100px;
      max-width: 960px;
      margin: 0 auto;
      padding-left: 24px;
      padding-right: 24px;
    }
    .hero-label {
      font-family: var(--font-mono);
      font-size: 0.75rem;
      letter-spacing: 0.2em;
      color: var(--accent);
      text-transform: uppercase;
      margin-bottom: 20px;
      opacity: 0;
      animation: fadeUp 0.6s ease 0.2s forwards;
    }
    .hero-name {
      font-size: clamp(3.5rem, 9vw, 7rem);
      font-weight: 800;
      line-height: 0.95;
      letter-spacing: -0.03em;
      margin-bottom: 24px;
      opacity: 0;
      animation: fadeUp 0.7s ease 0.4s forwards;
    }
    .hero-name span {
      display: block;
      background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    .hero-bio {
      font-family: var(--font-mono);
      font-size: 0.95rem;
      line-height: 1.8;
      color: var(--muted);
      max-width: 580px;
      margin-bottom: 40px;
      opacity: 0;
      animation: fadeUp 0.7s ease 0.6s forwards;
    }
    .hero-links {
      display: flex; gap: 16px; flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.7s ease 0.8s forwards;
    }
    .btn {
      display: inline-flex; align-items: center; gap: 8px;
      padding: 12px 28px;
      border-radius: 4px;
      font-family: var(--font-mono);
      font-size: 0.8rem;
      font-weight: 500;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      text-decoration: none;
      transition: all 0.2s;
      cursor: pointer;
    }
    .btn-primary {
      background: var(--accent);
      color: #000;
    }
    .btn-primary:hover { background: #00ffd5; transform: translateY(-2px); box-shadow: 0 8px 30px rgba(0,229,195,0.25); }
    .btn-ghost {
      border: 1px solid var(--border);
      color: var(--text);
    }
    .btn-ghost:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

    .hero-stats {
      display: flex; gap: 40px; margin-top: 64px;
      padding-top: 40px;
      border-top: 1px solid var(--border);
      opacity: 0;
      animation: fadeUp 0.7s ease 1s forwards;
    }
    .stat-num {
      font-size: 2rem;
      font-weight: 800;
      color: var(--accent);
      line-height: 1;
    }
    .stat-label {
      font-family: var(--font-mono);
      font-size: 0.72rem;
      color: var(--muted);
      text-transform: uppercase;
      letter-spacing: 0.1em;
      margin-top: 4px;
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ── SECTION HEADING ── */
    .section-tag {
      font-family: var(--font-mono);
      font-size: 0.72rem;
      color: var(--accent);
      letter-spacing: 0.2em;
      text-transform: uppercase;
      margin-bottom: 12px;
    }
    .section-title {
      font-size: clamp(2rem, 5vw, 3.2rem);
      font-weight: 800;
      letter-spacing: -0.02em;
      margin-bottom: 48px;
      line-height: 1.1;
    }

    /* ── SKILLS ── */
    .skills-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 16px;
    }
    .skill-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 24px;
      transition: all 0.25s;
      position: relative;
      overflow: hidden;
    }
    .skill-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 2px;
      background: linear-gradient(90deg, var(--accent), var(--accent2));
      transform: scaleX(0);
      transition: transform 0.3s;
    }
    .skill-card:hover::before { transform: scaleX(1); }
    .skill-card:hover { border-color: rgba(0,229,195,0.3); transform: translateY(-3px); }
    .skill-icon {
      font-size: 1.6rem;
      margin-bottom: 12px;
    }
    .skill-category {
      font-family: var(--font-mono);
      font-size: 0.68rem;
      color: var(--accent);
      letter-spacing: 0.15em;
      text-transform: uppercase;
      margin-bottom: 8px;
    }
    .skill-items {
      font-family: var(--font-mono);
      font-size: 0.82rem;
      color: var(--muted);
      line-height: 1.7;
    }

    /* ── PROJECTS ── */
    .projects-grid {
      display: grid;
      gap: 20px;
    }
    .project-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 32px;
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 16px;
      align-items: start;
      transition: all 0.25s;
      position: relative;
      overflow: hidden;
    }
    .project-card::after {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, rgba(0,229,195,0.03), rgba(124,92,252,0.03));
      opacity: 0;
      transition: opacity 0.3s;
    }
    .project-card:hover { border-color: rgba(0,229,195,0.25); transform: translateX(4px); }
    .project-card:hover::after { opacity: 1; }
    .project-num {
      font-family: var(--font-mono);
      font-size: 0.68rem;
      color: var(--accent2);
      letter-spacing: 0.15em;
      margin-bottom: 8px;
    }
    .project-title {
      font-size: 1.1rem;
      font-weight: 700;
      margin-bottom: 8px;
      letter-spacing: -0.01em;
    }
    .project-desc {
      font-family: var(--font-mono);
      font-size: 0.8rem;
      color: var(--muted);
      line-height: 1.7;
    }
    .project-arrow {
      font-size: 1.2rem;
      color: var(--muted);
      transition: color 0.2s, transform 0.2s;
      margin-top: 4px;
    }
    .project-card:hover .project-arrow { color: var(--accent); transform: translate(4px, -4px); }

    /* ── EDUCATION ── */
    .edu-list { display: flex; flex-direction: column; gap: 20px; }
    .edu-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 28px 32px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 20px;
      transition: border-color 0.25s;
    }
    .edu-card:hover { border-color: rgba(124,92,252,0.4); }
    .edu-degree {
      font-size: 1rem;
      font-weight: 700;
      margin-bottom: 4px;
    }
    .edu-school {
      font-family: var(--font-mono);
      font-size: 0.8rem;
      color: var(--muted);
    }
    .edu-badge {
      text-align: right;
      flex-shrink: 0;
    }
    .edu-score {
      font-size: 1.4rem;
      font-weight: 800;
      color: var(--accent2);
      line-height: 1;
    }
    .edu-year {
      font-family: var(--font-mono);
      font-size: 0.7rem;
      color: var(--muted);
      margin-top: 4px;
    }

    /* ── CERTS ── */
    .certs-list { display: flex; flex-direction: column; gap: 16px; }
    .cert-item {
      display: flex;
      align-items: flex-start;
      gap: 16px;
      padding: 20px 24px;
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 8px;
      transition: border-color 0.25s;
    }
    .cert-item:hover { border-color: rgba(0,229,195,0.3); }
    .cert-icon {
      font-size: 1.3rem;
      flex-shrink: 0;
      margin-top: 2px;
    }
    .cert-text {
      font-family: var(--font-mono);
      font-size: 0.83rem;
      color: var(--muted);
      line-height: 1.65;
    }

    /* ── CONTACT ── */
    #contact {
      border-top: 1px solid var(--border);
      text-align: center;
    }
    .contact-links {
      display: flex;
      justify-content: center;
      gap: 24px;
      flex-wrap: wrap;
      margin-top: 40px;
    }
    .contact-link {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      padding: 14px 28px;
      border: 1px solid var(--border);
      border-radius: 6px;
      font-family: var(--font-mono);
      font-size: 0.8rem;
      color: var(--muted);
      text-decoration: none;
      transition: all 0.2s;
    }
    .contact-link:hover {
      border-color: var(--accent);
      color: var(--accent);
      transform: translateY(-3px);
      box-shadow: 0 8px 24px rgba(0,229,195,0.1);
    }

    /* ── FOOTER ── */
    footer {
      position: relative; z-index: 1;
      text-align: center;
      padding: 32px 24px;
      border-top: 1px solid var(--border);
      font-family: var(--font-mono);
      font-size: 0.72rem;
      color: var(--muted);
    }

    /* ── REVEAL ANIMATION ── */
    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }
  </style>
</head>
<body>

<div class="grid-bg"></div>
<div class="blob blob-1"></div>
<div class="blob blob-2"></div>

<nav>
  <div class="nav-logo">BHARATH.G</div>
  <div class="nav-links">
    <a href="#skills">Skills</a>
    <a href="#projects">Projects</a>
    <a href="#education">Education</a>
    <a href="#contact">Contact</a>
  </div>
</nav>

<main>

  <!-- HERO -->
  <section id="hero">
    <div class="hero-label">// ECE Engineer & IoT Developer</div>
    <h1 class="hero-name">
      Bharath<span>G.</span>
    </h1>
    <p class="hero-bio">
      Electronics & Communication Engineering student skilled in IoT systems,
      embedded programming, and PCB design. Building real-world engineering
      applications with sensors, microcontrollers & simulation tools.
    </p>
    <div class="hero-links">
      <a href="mailto:bharathg2805@gmail.com" class="btn btn-primary">✉ Email Me</a>
      <a href="https://linkedin.com/in/bharath-g-006272392" target="_blank" class="btn btn-ghost">LinkedIn ↗</a>
      <a href="https://github.com/Bharath6705" target="_blank" class="btn btn-ghost">GitHub ↗</a>
    </div>
    <div class="hero-stats">
      <div>
        <div class="stat-num">5+</div>
        <div class="stat-label">Projects</div>
      </div>
      <div>
        <div class="stat-num">7.59</div>
        <div class="stat-label">CGPA</div>
      </div>
      <div>
        <div class="stat-num">2nd</div>
        <div class="stat-label">IIoT Prize</div>
      </div>
      <div>
        <div class="stat-num">2027</div>
        <div class="stat-label">Graduation</div>
      </div>
    </div>
  </section>

  <!-- SKILLS -->
  <section id="skills">
    <div class="reveal">
      <div class="section-tag">// 01 — Technical Arsenal</div>
      <h2 class="section-title">Skills &amp; Tools</h2>
      <div class="skills-grid">
        <div class="skill-card">
          <div class="skill-icon">⚡</div>
          <div class="skill-category">Programming</div>
          <div class="skill-items">C<br>Python (Basics)</div>
        </div>
        <div class="skill-card">
          <div class="skill-icon">🔌</div>
          <div class="skill-category">IoT & Embedded</div>
          <div class="skill-items">Arduino<br>ESP32<br>Sensor Interfacing</div>
        </div>
        <div class="skill-card">
          <div class="skill-icon">🔧</div>
          <div class="skill-category">Electronics</div>
          <div class="skill-items">Digital Electronics<br>Basic Circuit Design</div>
        </div>
        <div class="skill-card">
          <div class="skill-icon">🛠</div>
          <div class="skill-category">Tools</div>
          <div class="skill-items">Arduino IDE<br>LT Spice · Keil<br>Thinkspeak · Tinkercad<br>GitHub</div>
        </div>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects">
    <div class="reveal">
      <div class="section-tag">// 02 — Selected Work</div>
      <h2 class="section-title">Projects</h2>
      <div class="projects-grid">

        <div class="project-card">
          <div>
            <div class="project-num">PROJECT 01</div>
            <div class="project-title">Patch Antenna with Metamaterial Superstrate</div>
            <div class="project-desc">Simulation and design of a patch antenna enhanced with a metamaterial superstrate layer, analysing gain improvement and radiation characteristics.</div>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card">
          <div>
            <div class="project-num">PROJECT 02</div>
            <div class="project-title">Packet Sniffing & Traffic Analysis</div>
            <div class="project-desc">Network monitoring system for capturing and analysing data packets to identify traffic patterns, anomalies, and security vulnerabilities.</div>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card">
          <div>
            <div class="project-num">PROJECT 03</div>
            <div class="project-title">Smart Logistics Monitoring System</div>
            <div class="project-desc">IoT-based logistics platform with real-time tracking, environmental monitoring, and automated alerting to streamline supply-chain operations.</div>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card">
          <div>
            <div class="project-num">PROJECT 04</div>
            <div class="project-title">Smart Low-Power 12-bit Multiplexer</div>
            <div class="project-desc">Ultrasonic-sensor–driven 12-bit multiplexer design focused on minimising power consumption while maintaining high signal fidelity.</div>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card">
          <div>
            <div class="project-num">PROJECT 05</div>
            <div class="project-title">AI-Powered Disease Prediction</div>
            <div class="project-desc">Healthcare application that leverages machine-learning models trained on patient data to predict diseases and support early diagnosis.</div>
          </div>
          <div class="project-arrow">↗</div>
        </div>

      </div>
    </div>
  </section>

  <!-- EDUCATION -->
  <section id="education">
    <div class="reveal">
      <div class="section-tag">// 03 — Academic Background</div>
      <h2 class="section-title">Education</h2>
      <div class="edu-list">
        <div class="edu-card">
          <div>
            <div class="edu-degree">B.E. Electronics & Communication Engineering</div>
            <div class="edu-school">Anna University Regional Campus, Coimbatore</div>
          </div>
          <div class="edu-badge">
            <div class="edu-score">7.59</div>
            <div class="edu-year">2023 – 2027</div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- CERTIFICATIONS -->
  <section id="certifications">
    <div class="reveal">
      <div class="section-tag">// 04 — Recognition & Workshops</div>
      <h2 class="section-title">Achievements</h2>
      <div class="certs-list">
        <div class="cert-item">
          <div class="cert-icon">🏆</div>
          <div class="cert-text">
            Won <strong style="color:var(--text)">2nd Prize</strong> in the IIoT Innovation Contest conducted by <strong style="color:var(--text)">TEKTORK Pvt Ltd</strong> at Anna University, Coimbatore.
          </div>
        </div>
        <div class="cert-item">
          <div class="cert-icon">🎓</div>
          <div class="cert-text">
            Attended Workshop on <strong style="color:var(--text)">VLSI: SoC Design Flow and Verification Methodologies</strong> at TICEL BIOPARK.
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact">
    <div class="reveal">
      <div class="section-tag">// 05 — Get In Touch</div>
      <h2 class="section-title">Let's Connect</h2>
      <p style="font-family:var(--font-mono);font-size:0.9rem;color:var(--muted);max-width:480px;margin:0 auto;line-height:1.8;">
        Open to internships, collaborations, and interesting engineering challenges.
        Reach out via any of the channels below.
      </p>
      <div class="contact-links">
        <a href="mailto:bharathg2805@gmail.com" class="contact-link">✉ bharathg2805@gmail.com</a>
        <a href="tel:+916380082810" class="contact-link">📞 +91 6380082810</a>
        <a href="https://linkedin.com/in/bharath-g-006272392" target="_blank" class="contact-link">in LinkedIn</a>
        <a href="https://github.com/Bharath6705" target="_blank" class="contact-link">⌥ GitHub</a>
      </div>
    </div>
  </section>

</main>

<footer>
  Built from resume · Bharath G · ECE '27 · Chennai, India
</footer>

<script>
  // Scroll-reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });
  reveals.forEach(el => observer.observe(el));
</script>

</body>
</html>
