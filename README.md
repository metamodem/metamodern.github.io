<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Portfolio — AI Designer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Mono:wght@300;400&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #F5F3EF;
      --ink: #1A1916;
      --muted: #9A9690;
      --accent: #C8B89A;
      --line: #E2DED8;
      --serif: 'DM Serif Display', Georgia, serif;
      --mono: 'DM Mono', monospace;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--ink);
      font-family: var(--mono);
      font-weight: 300;
      font-size: 13px;
      letter-spacing: 0.02em;
    }

    /* ── NAV ── */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      display: flex; justify-content: space-between; align-items: center;
      padding: 20px 40px;
      background: rgba(245,243,239,0.88);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--line);
    }
    .nav-logo {
      font-family: var(--serif);
      font-size: 18px;
      letter-spacing: 0;
      color: var(--ink);
      text-decoration: none;
    }
    .nav-links { display: flex; gap: 36px; }
    .nav-links a {
      color: var(--muted);
      text-decoration: none;
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      transition: color 0.2s;
    }
    .nav-links a:hover { color: var(--ink); }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: flex; flex-direction: column; justify-content: flex-end;
      padding: 0 40px 60px;
      border-bottom: 1px solid var(--line);
    }
    .hero-tag {
      font-size: 11px; letter-spacing: 0.12em; text-transform: uppercase;
      color: var(--muted); margin-bottom: 20px;
    }
    .hero-title {
      font-family: var(--serif);
      font-size: clamp(52px, 8vw, 110px);
      line-height: 0.95;
      font-weight: 400;
      max-width: 900px;
    }
    .hero-title em {
      font-style: italic;
      color: var(--accent);
    }
    .hero-sub {
      margin-top: 32px;
      color: var(--muted);
      max-width: 340px;
      line-height: 1.8;
      font-size: 12px;
    }
    .hero-scroll {
      margin-top: 60px;
      font-size: 11px; letter-spacing: 0.1em;
      text-transform: uppercase; color: var(--muted);
      display: flex; align-items: center; gap: 12px;
    }
    .hero-scroll::before {
      content: '';
      display: block; width: 40px; height: 1px;
      background: var(--accent);
    }

    /* ── SECTION WRAPPER ── */
    section { padding: 100px 40px; border-bottom: 1px solid var(--line); }
    .section-header {
      display: flex; justify-content: space-between; align-items: baseline;
      margin-bottom: 60px;
    }
    .section-title {
      font-family: var(--serif);
      font-size: clamp(28px, 4vw, 48px);
      font-weight: 400;
    }
    .section-count {
      font-size: 11px; color: var(--muted); letter-spacing: 0.1em;
    }

    /* ── FILTER TABS ── */
    .filter-bar {
      display: flex; gap: 4px;
      margin-bottom: 48px;
    }
    .filter-btn {
      padding: 7px 18px;
      background: transparent;
      border: 1px solid var(--line);
      color: var(--muted);
      font-family: var(--mono);
      font-size: 11px; letter-spacing: 0.08em;
      text-transform: uppercase;
      cursor: pointer;
      transition: all 0.2s;
    }
    .filter-btn:hover { border-color: var(--accent); color: var(--ink); }
    .filter-btn.active {
      background: var(--ink); border-color: var(--ink);
      color: var(--bg);
    }

    /* ── GRID ── */
    .works-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
      gap: 2px;
    }

    .work-item {
      position: relative; overflow: hidden;
      background: var(--line);
      cursor: pointer;
      transition: opacity 0.3s;
    }
    .work-item.hidden { display: none; }

    .work-media {
      width: 100%; aspect-ratio: 4/3;
      object-fit: cover;
      display: block;
      transition: transform 0.6s cubic-bezier(0.25,0,0,1);
    }

    /* video embed wrapper */
    .work-video-wrap {
      width: 100%; aspect-ratio: 4/3;
      background: #000; position: relative;
    }
    .work-video-wrap iframe,
    .work-video-wrap video {
      width: 100%; height: 100%;
      object-fit: cover; border: none;
    }

    .work-overlay {
      position: absolute; inset: 0;
      background: rgba(26,25,22,0);
      display: flex; flex-direction: column;
      justify-content: flex-end;
      padding: 24px;
      transition: background 0.35s;
    }
    .work-item:hover .work-overlay { background: rgba(26,25,22,0.72); }
    .work-item:hover .work-media { transform: scale(1.04); }

    .work-caption {
      transform: translateY(10px); opacity: 0;
      transition: all 0.3s 0.05s;
    }
    .work-item:hover .work-caption { transform: translateY(0); opacity: 1; }

    .work-title {
      font-family: var(--serif); font-size: 22px;
      color: #F5F3EF; line-height: 1.1;
    }
    .work-desc {
      margin-top: 6px; font-size: 11px; color: rgba(245,243,239,0.65);
      line-height: 1.6; letter-spacing: 0.04em;
    }
    .work-type-badge {
      position: absolute; top: 16px; right: 16px;
      font-size: 9px; letter-spacing: 0.12em; text-transform: uppercase;
      padding: 4px 9px;
      background: rgba(245,243,239,0.15);
      backdrop-filter: blur(6px);
      border: 1px solid rgba(245,243,239,0.25);
      color: rgba(245,243,239,0.8);
    }

    /* ── LIGHTBOX ── */
    .lightbox {
      display: none; position: fixed; inset: 0; z-index: 200;
      background: rgba(26,25,22,0.95);
      align-items: center; justify-content: center;
      padding: 40px;
    }
    .lightbox.open { display: flex; }
    .lb-inner {
      max-width: 1000px; width: 100%;
      display: flex; flex-direction: column; align-items: center;
    }
    .lb-media { max-width: 100%; max-height: 72vh; object-fit: contain; }
    .lb-video { width: 100%; aspect-ratio: 16/9; }
    .lb-caption {
      margin-top: 24px; text-align: center;
      color: rgba(245,243,239,0.7); font-size: 12px;
      line-height: 1.8;
    }
    .lb-title {
      font-family: var(--serif); font-size: 26px;
      color: #F5F3EF; margin-bottom: 6px;
    }
    .lb-close {
      position: fixed; top: 28px; right: 36px;
      background: none; border: none; color: var(--muted);
      font-size: 28px; cursor: pointer; line-height: 1;
      transition: color 0.2s;
    }
    .lb-close:hover { color: #F5F3EF; }
    .lb-nav {
      display: flex; gap: 16px; margin-top: 20px;
    }
    .lb-btn {
      background: none; border: 1px solid rgba(245,243,239,0.2);
      color: rgba(245,243,239,0.5); font-family: var(--mono);
      font-size: 11px; letter-spacing: 0.1em; text-transform: uppercase;
      padding: 8px 20px; cursor: pointer;
      transition: all 0.2s;
    }
    .lb-btn:hover { border-color: rgba(245,243,239,0.6); color: #F5F3EF; }

    /* ── ABOUT ── */
    #about .about-grid {
      display: grid; grid-template-columns: 1fr 1fr; gap: 80px;
      align-items: start;
    }
    .about-text h2 {
      font-family: var(--serif); font-size: clamp(26px, 3vw, 42px);
      font-weight: 400; line-height: 1.15; margin-bottom: 28px;
    }
    .about-text p {
      color: var(--muted); line-height: 1.9; margin-bottom: 16px;
      font-size: 13px;
    }
    .about-tools {
      margin-top: 40px;
      display: flex; flex-wrap: wrap; gap: 8px;
    }
    .tool-tag {
      padding: 5px 14px; border: 1px solid var(--line);
      font-size: 11px; letter-spacing: 0.06em;
      color: var(--muted);
    }
    .about-stats {
      display: flex; flex-direction: column; gap: 32px;
      padding-top: 8px;
    }
    .stat-item { border-top: 1px solid var(--line); padding-top: 20px; }
    .stat-num {
      font-family: var(--serif); font-size: 48px;
      line-height: 1; margin-bottom: 6px;
    }
    .stat-label { font-size: 11px; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; }

    /* ── CONTACT ── */
    #contact { background: var(--ink); border: none; }
    #contact .section-title { color: var(--bg); }
    #contact .section-count { color: var(--muted); }
    .contact-grid {
      display: grid; grid-template-columns: 1fr 1fr; gap: 80px;
      margin-top: 60px;
    }
    .contact-intro {
      font-family: var(--serif); font-size: clamp(22px, 3vw, 36px);
      color: var(--bg); font-weight: 400; line-height: 1.3;
    }
    .contact-intro em { font-style: italic; color: var(--accent); }
    .contact-links { display: flex; flex-direction: column; gap: 0; }
    .contact-link {
      display: flex; justify-content: space-between; align-items: center;
      padding: 20px 0;
      border-bottom: 1px solid rgba(245,243,239,0.1);
      text-decoration: none;
      color: var(--muted);
      font-size: 12px; letter-spacing: 0.08em;
      text-transform: uppercase;
      transition: color 0.2s;
    }
    .contact-link:hover { color: var(--bg); }
    .contact-link span:last-child { font-size: 18px; }

    /* ── FOOTER ── */
    footer {
      background: var(--ink); padding: 24px 40px;
      display: flex; justify-content: space-between; align-items: center;
      border-top: 1px solid rgba(245,243,239,0.08);
    }
    footer span { font-size: 11px; color: rgba(245,243,239,0.3); letter-spacing: 0.06em; }

    /* ── ANIMATIONS ── */
    .fade-in { opacity: 0; transform: translateY(24px); transition: opacity 0.7s, transform 0.7s; }
    .fade-in.visible { opacity: 1; transform: translateY(0); }

    /* ── RESPONSIVE ── */
    @media (max-width: 768px) {
      nav { padding: 16px 20px; }
      .nav-links { gap: 20px; }
      section { padding: 70px 20px; }
      #hero { padding: 0 20px 50px; }
      .about-grid, .contact-grid { grid-template-columns: 1fr; gap: 48px; }
      .works-grid { grid-template-columns: 1fr 1fr; }
      footer { padding: 20px; }
    }
    @media (max-width: 480px) {
      .works-grid { grid-template-columns: 1fr; }
      .hero-title { font-size: 44px; }
    }
  </style>
</head>
<body>

<!-- NAV -->
<nav>
  <a href="#hero" class="nav-logo">A. I.</a>
  <div class="nav-links">
    <a href="#works">Works</a>
    <a href="#about">About</a>
    <a href="#contact">Contact</a>
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <p class="hero-tag">AI Designer · AI Research · Visual Research</p>
  <h1 class="hero-title">
    Design at the edge<br>of <em>human</em><br>& machine
  </h1>
  <p class="hero-sub">
    Exploring the space between intention and algorithm —
    images, motion, and forms that emerge from both.
  </p>
  <div class="hero-scroll">scroll to works</div>
</section>

<!-- WORKS -->
<section id="works">
  <div class="section-header fade-in">
    <h2 class="section-title">Selected Works</h2>
    <span class="section-count" id="work-count"></span>
  </div>

  <div class="filter-bar fade-in">
    <button class="filter-btn active" data-filter="all">All</button>
    <button class="filter-btn" data-filter="image">Images</button>
    <button class="filter-btn" data-filter="video">Video</button>
    <button class="filter-btn" data-filter="gif">Animation</button>
  </div>

  <div class="works-grid" id="works-grid">
    <!--
      ═══════════════════════════════════════════════════════
      КАК ДОБАВЛЯТЬ РАБОТЫ:

      ── ИЗОБРАЖЕНИЕ ──────────────────────────────────────
      <div class="work-item" data-type="image"
           data-src="works/bhudda.jpg"
           data-title="Сход снега"
           data-desc="Ретушь, 2024, DALL-E">
        <img class="work-media" src="works/bhudda.jpg" alt="..." />
        <div class="work-type-badge">Image</div>
        <div class="work-overlay">
          <div class="work-caption">
            <div class="work-title">Название</div>
            <div class="work-desc">Описание · 2024 · Midjourney</div>
          </div>
        </div>
      </div>

      ── ВИДЕО (локальный файл) ────────────────────────────
      <div class="work-item" data-type="video"
           data-src="vorkuta_2.mp4"
           data-title="Название" data-desc="...">
        <div class="work-video-wrap">
          <video class="work-media" src="works/cats_2.mp4" muted autoplay loop playsinline></video>
        </div>
        <div class="work-type-badge">Video</div>
        <div class="work-overlay">
          <div class="work-caption">
            <div class="work-title">Название</div>
            <div class="work-desc">Описание · 2024 · Runway</div>
          </div>
        </div>
      </div>

      ── ВИДЕО (YouTube/Vimeo embed) ───────────────────────
      <div class="work-item" data-type="video"
           data-embed="https://www.youtube.com/embed/VIDEO_ID"
           data-title="Название" data-desc="...">
        <div class="work-video-wrap">
          <iframe src="https://www.youtube.com/embed/VIDEO_ID?mute=1&autoplay=0"
                  allow="autoplay; fullscreen" allowfullscreen></iframe>
        </div>
        <div class="work-type-badge">Video</div>
        <div class="work-overlay">
          <div class="work-caption">
            <div class="work-title">Название</div>
            <div class="work-desc">...</div>
          </div>
        </div>
      </div>

      ── GIF / АНИМАЦИЯ ───────────────────────────────────
      <div class="work-item" data-type="gif"
           data-src="works/anim.gif"
           data-title="Название" data-desc="...">
        <img class="work-media" src="works/anim.gif" alt="..." />
        <div class="work-type-badge">Animation</div>
        <div class="work-overlay">
          <div class="work-caption">
            <div class="work-title">Название</div>
            <div class="work-desc">Описание · 2024 · ComfyUI</div>
          </div>
        </div>
      </div>
      ═══════════════════════════════════════════════════════
    -->

    <!-- ПРИМЕРЫ-ЗАГЛУШКИ (замените реальными работами) -->

    <div class="work-item" data-type="image"
         data-src="works/bhudda.jpg"
         data-title="Сход снега"
         data-desc="Abstracts · 2024 · DALL-E + Photoshop">
      <img class="work-media"
           src="works/bhudda.jpg"
           alt="Сход снега" loading="lazy" />
      <div class="work-type-badge">Image</div>
      <div class="work-overlay">
        <div class="work-caption">
          <div class="work-title">Сход снега</div>
          <div class="work-desc">Abstracts · 2024 · DALL-E + Photoshop</div>
        </div>
      </div>
    </div>

    <div class="work-item" data-type="image"
         data-src="https://images.unsplash.com/photo-1617791160505-6f00504e3519?w=800"
         data-title="Texture Study"
         data-desc="Material exploration · 2024 · Stable Diffusion">
      <img class="work-media"
           src="https://images.unsplash.com/photo-1617791160505-6f00504e3519?w=800"
           alt="Texture Study" loading="lazy" />
      <div class="work-type-badge">Image</div>
      <div class="work-overlay">
        <div class="work-caption">
          <div class="work-title">Texture Study</div>
          <div class="work-desc">Material exploration · 2024 · SD</div>
        </div>
      </div>
    </div>

    <div class="work-item" data-type="video"
         data-embed="https://www.youtube.com/embed/dQw4w9WgXcQ"
         data-title="Motion Loop 001"
         data-desc="Looping video study · 2024 · Runway Gen-2">
      <div class="work-video-wrap">
        <video class="work-media" muted autoplay loop playsinline
               poster="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800">
          <!-- Замените src на реальный файл или уберите видео, оставив poster -->
        </video>
      </div>
      <div class="work-type-badge">Video</div>
      <div class="work-overlay">
        <div class="work-caption">
          <div class="work-title">Motion Loop 001</div>
          <div class="work-desc">Looping study · 2024 · Runway</div>
        </div>
      </div>
    </div>

    <div class="work-item" data-type="gif"
         data-src="https://images.unsplash.com/photo-1531297484001-80022131f5a1?w=800"
         data-title="Pulse"
         data-desc="Animation loop · 2024 · ComfyUI">
      <img class="work-media"
           src="https://images.unsplash.com/photo-1531297484001-80022131f5a1?w=800"
           alt="Pulse" loading="lazy" />
      <div class="work-type-badge">Animation</div>
      <div class="work-overlay">
        <div class="work-caption">
          <div class="work-title">Pulse</div>
          <div class="work-desc">Animation loop · 2024 · ComfyUI</div>
        </div>
      </div>
    </div>

    <div class="work-item" data-type="image"
         data-src="https://images.unsplash.com/photo-1635070041078-e363dbe005cb?w=800"
         data-title="Geometric Drift"
         data-desc="Abstract series · 2024 · DALL·E + Illustrator">
      <img class="work-media"
           src="https://images.unsplash.com/photo-1635070041078-e363dbe005cb?w=800"
           alt="Geometric Drift" loading="lazy" />
      <div class="work-type-badge">Image</div>
      <div class="work-overlay">
        <div class="work-caption">
          <div class="work-title">Geometric Drift</div>
          <div class="work-desc">Abstract series · 2024 · DALL·E</div>
        </div>
      </div>
    </div>

    <div class="work-item" data-type="gif"
         data-src="https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=800"
         data-title="Frequency"
         data-desc="Generative animation · 2024 · Processing + SD">
      <img class="work-media"
           src="https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=800"
           alt="Frequency" loading="lazy" />
      <div class="work-type-badge">Animation</div>
      <div class="work-overlay">
        <div class="work-caption">
          <div class="work-title">Frequency</div>
          <div class="work-desc">Generative animation · 2024</div>
        </div>
      </div>
    </div>

  </div><!-- /works-grid -->
</section>

<!-- LIGHTBOX -->
<div class="lightbox" id="lightbox">
  <button class="lb-close" id="lb-close">×</button>
  <div class="lb-inner">
    <div id="lb-media-wrap"></div>
    <div class="lb-caption">
      <div class="lb-title" id="lb-title"></div>
      <div id="lb-desc"></div>
    </div>
    <div class="lb-nav">
      <button class="lb-btn" id="lb-prev">← Prev</button>
      <button class="lb-btn" id="lb-next">Next →</button>
    </div>
  </div>
</div>

<!-- ABOUT -->
<section id="about">
  <div class="section-header fade-in">
    <h2 class="section-title">About</h2>
  </div>
  <div class="about-grid fade-in">
    <div class="about-text">
      <h2>
        Working at the intersection of design,<br>
        <em style="font-style:italic; color: var(--accent)">code, and imagination.</em>
      </h2>
      <!-- Замените на свой текст -->
      <p>
        I'm an AI-assisted designer exploring generative imagery, motion, and visual systems.
        My practice blends traditional design craft with emerging generative tools —
        creating work that feels both considered and unpredictable.
      </p>
      <p>
        Available for editorial commissions, art direction,
        and experimental collaborations.
      </p>
      <div class="about-tools">
        <span class="tool-tag">Midjourney</span>
        <span class="tool-tag">Stable Diffusion</span>
        <span class="tool-tag">ComfyUI</span>
        <span class="tool-tag">Runway</span>
        <span class="tool-tag">DALL·E</span>
        <span class="tool-tag">After Effects</span>
        <span class="tool-tag">Photoshop</span>
      </div>
    </div>
    <div class="about-stats">
      <div class="stat-item">
        <div class="stat-num">3+</div>
        <div class="stat-label">Years in AI design</div>
      </div>
      <div class="stat-item">
        <div class="stat-num">40+</div>
        <div class="stat-label">Projects completed</div>
      </div>
      <div class="stat-item">
        <div class="stat-num">∞</div>
        <div class="stat-label">Iterations per day</div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-header fade-in">
    <h2 class="section-title">Contact</h2>
    <span class="section-count">Open for commissions</span>
  </div>
  <div class="contact-grid fade-in">
    <p class="contact-intro">
      Let's make something<br><em>strange</em><br>and beautiful.
    </p>
    <div class="contact-links">
      <!-- Замените ссылки на реальные -->
      <a href="mailto:hello@example.com" class="contact-link">
        <span>Email</span>
        <span>↗</span>
      </a>
      <a href="https://instagram.com/" target="_blank" class="contact-link">
        <span>Instagram</span>
        <span>↗</span>
      </a>
      <a href="https://behance.net/" target="_blank" class="contact-link">
        <span>Behance</span>
        <span>↗</span>
      </a>
      <a href="https://twitter.com/" target="_blank" class="contact-link">
        <span>Twitter / X</span>
        <span>↗</span>
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <span id="footer-year"></span>
  <span>Built with intention</span>
</footer>

<script>
  // ── Year ──
  document.getElementById('footer-year').textContent =
    '© ' + new Date().getFullYear();

  // ── Work count ──
  const items = document.querySelectorAll('.work-item');
  document.getElementById('work-count').textContent =
    items.length + ' works';

  // ── Filter ──
  document.querySelectorAll('.filter-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      const f = btn.dataset.filter;
      items.forEach(item => {
        item.classList.toggle('hidden', f !== 'all' && item.dataset.type !== f);
      });
      const visible = document.querySelectorAll('.work-item:not(.hidden)').length;
      document.getElementById('work-count').textContent = visible + ' works';
    });
  });

  // ── Lightbox ──
  let visibleItems = [];
  let currentIdx = 0;

  function openLightbox(idx) {
    visibleItems = [...document.querySelectorAll('.work-item:not(.hidden)')];
    currentIdx = idx;
    renderLB();
    document.getElementById('lightbox').classList.add('open');
    document.body.style.overflow = 'hidden';
  }

  function renderLB() {
    const item = visibleItems[currentIdx];
    const wrap = document.getElementById('lb-media-wrap');
    const type = item.dataset.type;
    const src = item.dataset.src;
    const embed = item.dataset.embed;

    wrap.innerHTML = '';

    if (type === 'video' && embed) {
      const iframe = document.createElement('iframe');
      iframe.src = embed + '?autoplay=1';
      iframe.className = 'lb-video';
      iframe.allow = 'autoplay; fullscreen';
      iframe.allowFullscreen = true;
      wrap.appendChild(iframe);
    } else if (type === 'video' && src) {
      const vid = document.createElement('video');
      vid.src = src; vid.controls = true; vid.autoplay = true;
      vid.className = 'lb-video'; wrap.appendChild(vid);
    } else if (src) {
      const img = document.createElement('img');
      img.src = src; img.className = 'lb-media'; img.alt = item.dataset.title;
      wrap.appendChild(img);
    }

    document.getElementById('lb-title').textContent = item.dataset.title || '';
    document.getElementById('lb-desc').textContent = item.dataset.desc || '';
  }

  function closeLightbox() {
    document.getElementById('lightbox').classList.remove('open');
    document.getElementById('lb-media-wrap').innerHTML = '';
    document.body.style.overflow = '';
  }

  items.forEach((item, i) => {
    item.addEventListener('click', () => {
      const vis = [...document.querySelectorAll('.work-item:not(.hidden)')];
      openLightbox(vis.indexOf(item));
    });
  });

  document.getElementById('lb-close').addEventListener('click', closeLightbox);
  document.getElementById('lb-prev').addEventListener('click', () => {
    currentIdx = (currentIdx - 1 + visibleItems.length) % visibleItems.length;
    renderLB();
  });
  document.getElementById('lb-next').addEventListener('click', () => {
    currentIdx = (currentIdx + 1) % visibleItems.length;
    renderLB();
  });
  document.getElementById('lightbox').addEventListener('click', e => {
    if (e.target === e.currentTarget) closeLightbox();
  });
  document.addEventListener('keydown', e => {
    if (e.key === 'Escape') closeLightbox();
    if (e.key === 'ArrowLeft') { currentIdx = (currentIdx - 1 + visibleItems.length) % visibleItems.length; renderLB(); }
    if (e.key === 'ArrowRight') { currentIdx = (currentIdx + 1) % visibleItems.length; renderLB(); }
  });

  // ── Fade-in on scroll ──
  const observer = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 80);
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));
</script>
</body>
</html>
