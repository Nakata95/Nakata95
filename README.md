<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DRAGON // PROFILE.exe</title>
<style>
  :root{
    --void:#07050c;
    --void-deep:#0d0616;
    --panel:#120a1f;
    --blood:#ff1244;
    --blood-dim:#7a0a26;
    --pink:#ff3d7f;
    --cyan:#2af0e8;
    --purple:#6d1fb8;
    --paper:#e8dfe6;
    --dim:#8a7a92;
    --font-display: 'Press Start 2P', monospace;
    --font-mono: 'Share Tech Mono', monospace;
  }

  @font-face{
    font-family:'Press Start 2P';
    src: local('Press Start 2P');
  }

  *{box-sizing:border-box; margin:0; padding:0;}

  html{scroll-behavior:smooth;}

  body{
    background:var(--void);
    color:var(--paper);
    font-family:var(--font-mono);
    overflow-x:hidden;
    position:relative;
  }

  /* ---------- CRT / scanline / noise layer ---------- */
  .crt{
    pointer-events:none;
    position:fixed; inset:0; z-index:50;
    background:repeating-linear-gradient(
      to bottom,
      rgba(0,0,0,0) 0px,
      rgba(0,0,0,0.15) 1px,
      rgba(0,0,0,0) 2px
    );
    mix-blend-mode:multiply;
  }
  .vignette{
    pointer-events:none;
    position:fixed; inset:0; z-index:49;
    background:radial-gradient(ellipse at center, rgba(0,0,0,0) 40%, rgba(0,0,0,0.65) 100%);
  }

  @media (prefers-reduced-motion: no-preference){
    .glitch-layer::before,
    .glitch-layer::after{ animation-play-state:running; }
  }
  @media (prefers-reduced-motion: reduce){
    *{animation:none !important; transition:none !important;}
  }

  a{color:inherit;}
  :focus-visible{outline:2px solid var(--cyan); outline-offset:3px;}

  /* ---------- shared ---------- */
  .wrap{max-width:1000px; margin:0 auto; padding:0 28px;}
  .eyebrow{
    font-family:var(--font-display);
    font-size:10px;
    letter-spacing:2px;
    color:var(--cyan);
    display:flex;
    align-items:center;
    gap:10px;
    margin-bottom:22px;
  }
  .eyebrow::before{
    content:'';
    width:20px; height:2px;
    background:var(--cyan);
    box-shadow:0 0 8px var(--cyan);
  }

  section{padding:110px 0; position:relative;}

  /* ---------- HERO ---------- */
  .hero{
    min-height:100vh;
    display:flex;
    flex-direction:column;
    justify-content:center;
    position:relative;
    background:
      radial-gradient(ellipse 60% 50% at 50% 20%, rgba(255,18,68,0.18), transparent 60%),
      radial-gradient(ellipse 50% 40% at 80% 80%, rgba(109,31,184,0.25), transparent 60%),
      linear-gradient(180deg, var(--void-deep) 0%, var(--void) 100%);
    border-bottom:1px solid var(--blood-dim);
    overflow:hidden;
  }

  .hero-grid{
    position:absolute; inset:0;
    background-image:
      linear-gradient(rgba(255,61,127,0.06) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,61,127,0.06) 1px, transparent 1px);
    background-size:44px 44px;
    -webkit-mask-image:linear-gradient(180deg, transparent, black 30%, black 70%, transparent);
    mask-image:linear-gradient(180deg, transparent, black 30%, black 70%, transparent);
  }

  .katana{
    position:absolute;
    top:8%; right:-6%;
    width:520px;
    opacity:0.85;
    filter:drop-shadow(0 0 24px rgba(255,18,68,0.35));
    transform:rotate(8deg);
  }

  .hero-inner{position:relative; z-index:2;}

  .codename{
    font-family:var(--font-display);
    font-size:clamp(34px, 7vw, 76px);
    line-height:1.15;
    letter-spacing:1px;
    color:var(--paper);
    text-shadow:
      0 0 18px rgba(255,18,68,0.55);
    position:relative;
    display:inline-block;
  }
  .codename .glitch-layer{position:relative; display:inline-block;}
  .codename .glitch-layer::before,
  .codename .glitch-layer::after{
    content:attr(data-text);
    position:absolute; left:0; top:0;
    width:100%; overflow:hidden;
    background:var(--void);
    clip-path: inset(0 0 0 0);
  }
  .codename .glitch-layer::before{
    color:var(--cyan);
    animation:glitchTop 4.2s infinite steps(1);
    left:2px;
  }
  .codename .glitch-layer::after{
    color:var(--blood);
    animation:glitchBottom 4.2s infinite steps(1);
    left:-2px;
  }
  @keyframes glitchTop{
    0%, 92%, 100%{ clip-path: inset(0 0 100% 0); opacity:0; }
    93%{ clip-path: inset(10% 0 60% 0); opacity:1; }
    95%{ clip-path: inset(60% 0 5% 0); opacity:1; }
    97%{ clip-path: inset(30% 0 40% 0); opacity:1; }
  }
  @keyframes glitchBottom{
    0%, 90%, 100%{ clip-path: inset(100% 0 0 0); opacity:0; }
    91%{ clip-path: inset(70% 0 5% 0); opacity:1; }
    94%{ clip-path: inset(15% 0 65% 0); opacity:1; }
    96.5%{ clip-path: inset(50% 0 20% 0); opacity:1; }
  }

  .subline{
    margin-top:20px;
    font-size:16px;
    color:var(--dim);
    max-width:520px;
    line-height:1.7;
  }
  .subline strong{color:var(--pink); font-weight:400;}

  .hero-meta{
    margin-top:44px;
    display:flex;
    gap:36px;
    flex-wrap:wrap;
    font-size:12px;
    color:var(--dim);
  }
  .hero-meta div span{display:block; color:var(--cyan); font-size:10px; letter-spacing:1px; margin-bottom:6px;}
  .hero-meta div strong{color:var(--paper); font-weight:400; font-size:14px;}

  .cta-row{margin-top:48px; display:flex; gap:16px; flex-wrap:wrap;}
  .btn{
    font-family:var(--font-mono);
    font-size:13px;
    letter-spacing:1px;
    padding:14px 26px;
    border:1px solid var(--blood);
    color:var(--paper);
    text-decoration:none;
    position:relative;
    transition:background .15s, color .15s, box-shadow .15s;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 100%, 12px 100%);
  }
  .btn:hover{ background:var(--blood); box-shadow:0 0 22px rgba(255,18,68,0.6); }
  .btn.alt{border-color:var(--cyan); color:var(--cyan);}
  .btn.alt:hover{ background:var(--cyan); color:var(--void); box-shadow:0 0 22px rgba(42,240,232,0.6); }

  .scroll-hint{
    position:absolute; bottom:36px; left:28px;
    font-size:10px; letter-spacing:2px; color:var(--dim);
    display:flex; align-items:center; gap:10px;
  }
  .scroll-hint .bar{width:1px; height:30px; background:linear-gradient(var(--blood), transparent); animation:pulseBar 2s infinite;}
  @keyframes pulseBar{0%,100%{opacity:.3} 50%{opacity:1}}

  /* ---------- MISSION divider ---------- */
  .mission-tag{
    font-family:var(--font-display);
    font-size:12px;
    color:var(--blood);
    letter-spacing:2px;
    margin-bottom:10px;
  }
  .mission-title{
    font-family:var(--font-display);
    font-size:clamp(22px, 3.4vw, 34px);
    letter-spacing:1px;
    margin-bottom:44px;
    color:var(--paper);
  }

  /* ---------- ABOUT / DOSSIER ---------- */
  .dossier{
    background:var(--panel);
    border:1px solid rgba(255,61,127,0.18);
    padding:36px;
    position:relative;
  }
  .dossier::before{
    content:'CLASSIFIED';
    position:absolute; top:14px; right:18px;
    font-family:var(--font-display);
    font-size:9px;
    color:var(--blood-dim);
    letter-spacing:2px;
  }
  .dossier p{line-height:1.9; color:var(--dim); font-size:14.5px; max-width:640px;}
  .dossier p + p{margin-top:16px;}
  .dossier .highlight{color:var(--pink);}

  /* ---------- STACK / HUD BARS ---------- */
  .stack-grid{
    display:grid;
    grid-template-columns:repeat(2, 1fr);
    gap:34px 60px;
  }
  @media (max-width:640px){ .stack-grid{grid-template-columns:1fr;} }

  .stat-row{margin-bottom:22px;}
  .stat-row .label{
    display:flex; justify-content:space-between;
    font-size:12px; color:var(--paper); margin-bottom:8px; letter-spacing:1px;
  }
  .stat-row .label span:last-child{color:var(--cyan);}
  .meter{
    height:8px;
    background:rgba(255,255,255,0.06);
    position:relative;
    clip-path: polygon(0 0, 100% 0, calc(100% - 6px) 100%, 0% 100%);
  }
  .meter i{
    display:block; height:100%;
    background:linear-gradient(90deg, var(--blood), var(--pink));
    box-shadow:0 0 10px rgba(255,18,68,0.6);
    transform-origin:left;
    transform:scaleX(0);
    animation:fillMeter 1.4s ease-out forwards;
    animation-delay:.2s;
  }
  @keyframes fillMeter{ to{ transform:scaleX(1); } }

  /* ---------- PROJECTS / MISSIONS LIST ---------- */
  .missions{display:flex; flex-direction:column;}
  .mission{
    display:grid;
    grid-template-columns:90px 1fr auto;
    gap:24px;
    align-items:start;
    padding:26px 0;
    border-top:1px solid rgba(255,61,127,0.14);
    transition:background .15s;
  }
  .missions .mission:last-child{border-bottom:1px solid rgba(255,61,127,0.14);}
  .mission:hover{background:rgba(255,18,68,0.04);}
  .mission .num{
    font-family:var(--font-display);
    font-size:11px;
    color:var(--blood-dim);
    padding-top:4px;
  }
  .mission .body h3{
    font-family:var(--font-display);
    font-size:14px;
    letter-spacing:1px;
    margin-bottom:10px;
    color:var(--paper);
  }
  .mission .body p{color:var(--dim); font-size:13.5px; line-height:1.7; max-width:520px;}
  .mission .tags{display:flex; gap:8px; flex-wrap:wrap; margin-top:12px;}
  .mission .tags span{
    font-size:10px; letter-spacing:1px; color:var(--cyan);
    border:1px solid rgba(42,240,232,0.35);
    padding:4px 8px;
  }
  .mission .status{
    font-size:10px; letter-spacing:1px; color:var(--dim); text-align:right; padding-top:6px; white-space:nowrap;
  }
  .mission .status.clear{color:var(--pink);}
  .mission .status.clear::before{content:'● '; color:var(--blood);}
  .mission .status.wip::before{content:'● '; color:var(--cyan);}

  /* ---------- ARSENAL / GITHUB STATS ---------- */
  .arsenal-grid{display:grid; grid-template-columns:1fr 1fr; gap:20px;}
  @media (max-width:640px){ .arsenal-grid{grid-template-columns:1fr;} }
  .arsenal-grid img{ width:100%; display:block; filter:saturate(1.1) contrast(1.05);
    border:1px solid rgba(255,61,127,0.18); background:var(--panel);}

  /* ---------- CONTACT / EXTRACTION ---------- */
  .extraction{
    text-align:center;
    padding:130px 0 100px;
    background:
      radial-gradient(ellipse 70% 60% at 50% 100%, rgba(255,18,68,0.16), transparent 70%),
      var(--void-deep);
    border-top:1px solid var(--blood-dim);
  }
  .extraction .mission-title{margin:0 auto 18px;}
  .extraction p{color:var(--dim); max-width:440px; margin:0 auto 40px; font-size:14px; line-height:1.7;}
  .contact-row{display:flex; gap:16px; justify-content:center; flex-wrap:wrap;}

  footer{
    text-align:center; padding:28px; font-size:10px; color:var(--dim); letter-spacing:1px;
    border-top:1px solid rgba(255,61,127,0.1);
  }
</style>
</head>
<body>

<div class="crt"></div>
<div class="vignette"></div>

<!-- ============ HERO ============ -->
<header class="hero">
  <div class="hero-grid" aria-hidden="true"></div>

  <svg class="katana" viewBox="0 0 400 400" aria-hidden="true">
    <g transform="rotate(-15 200 200)">
      <rect x="60" y="190" width="260" height="6" fill="#e8dfe6" opacity="0.9"/>
      <rect x="60" y="190" width="260" height="2" fill="#2af0e8" opacity="0.5"/>
      <rect x="20" y="182" width="45" height="22" fill="#ff1244"/>
      <rect x="0" y="178" width="24" height="30" fill="#120a1f" stroke="#ff1244" stroke-width="2"/>
      <polygon points="320,190 360,193 320,196" fill="#e8dfe6" opacity="0.6"/>
    </g>
  </svg>

  <div class="wrap hero-inner">
    <div class="eyebrow">FICHIER OUVERT // 2026</div>
    <h1 class="codename">
      <span class="glitch-layer" data-text="DRAGON">DRAGON</span>
    </h1>
    <p class="subline">
      Développeur — je répare des systèmes cassés à <strong>3h du matin</strong> et je commit avant le générique de fin.
      Remplace "DRAGON" par ton pseudo, et le reste par ta vraie histoire.
    </p>

    <div class="hero-meta">
      <div><span>RÔLE</span><strong>Full-Stack Dev</strong></div>
      <div><span>BASE</span><strong>Paris, FR</strong></div>
      <div><span>STATUT</span><strong>Disponible</strong></div>
    </div>

    <div class="cta-row">
      <a class="btn" href="#missions">VOIR LES PROJETS</a>
      <a class="btn alt" href="#contact">CONTACT</a>
    </div>
  </div>

  <div class="scroll-hint"><div class="bar"></div>DÉFILER</div>
</header>

<!-- ============ ABOUT ============ -->
<section id="about">
  <div class="wrap">
    <div class="mission-tag">MISSION 00</div>
    <h2 class="mission-title">DOSSIER</h2>
    <div class="dossier">
      <p>
        Je construis des produits <span class="highlight">rapides, précis</span>, sans fioritures inutiles —
        un peu comme un bon combat au katana : chaque mouvement compte, pas de temps mort.
      </p>
      <p>
        Actuellement concentré sur des projets web et des outils internes. Toujours partant pour
        un défi technique tordu ou une refonte impossible.
      </p>
    </div>
  </div>
</section>

<!-- ============ STACK ============ -->
<section id="stack">
  <div class="wrap">
    <div class="mission-tag">MISSION 01</div>
    <h2 class="mission-title">ARSENAL TECHNIQUE</h2>
    <div class="stack-grid">
      <div>
        <div class="stat-row">
          <div class="label"><span>JavaScript / TypeScript</span><span>92%</span></div>
          <div class="meter"><i style="width:92%"></i></div>
        </div>
        <div class="stat-row">
          <div class="label"><span>React / Next.js</span><span>88%</span></div>
          <div class="meter"><i style="width:88%"></i></div>
        </div>
        <div class="stat-row">
          <div class="label"><span>Node.js</span><span>80%</span></div>
          <div class="meter"><i style="width:80%"></i></div>
        </div>
      </div>
      <div>
        <div class="stat-row">
          <div class="label"><span>Python</span><span>75%</span></div>
          <div class="meter"><i style="width:75%"></i></div>
        </div>
        <div class="stat-row">
          <div class="label"><span>SQL / PostgreSQL</span><span>70%</span></div>
          <div class="meter"><i style="width:70%"></i></div>
        </div>
        <div class="stat-row">
          <div class="label"><span>Docker / CI-CD</span><span>65%</span></div>
          <div class="meter"><i style="width:65%"></i></div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ============ MISSIONS / PROJECTS ============ -->
<section id="missions">
  <div class="wrap">
    <div class="mission-tag">MISSION 02</div>
    <h2 class="mission-title">OPÉRATIONS ACHEVÉES</h2>
    <div class="missions">
      <div class="mission">
        <div class="num">01</div>
        <div class="body">
          <h3>NOM_DU_PROJET</h3>
          <p>Description courte : ce que fait le projet, le problème résolu, et ce qui le rend intéressant techniquement.</p>
          <div class="tags"><span>React</span><span>Node.js</span><span>PostgreSQL</span></div>
        </div>
        <div class="status clear">TERMINÉ</div>
      </div>
      <div class="mission">
        <div class="num">02</div>
        <div class="body">
          <h3>AUTRE_PROJET</h3>
          <p>Une deuxième mission — remplace par un vrai repo GitHub avec un lien vers le code.</p>
          <div class="tags"><span>Python</span><span>API</span></div>
        </div>
        <div class="status wip">EN COURS</div>
      </div>
      <div class="mission">
        <div class="num">03</div>
        <div class="body">
          <h3>PROJET_SECRET</h3>
          <p>Un projet en cours de développement, encore classifié.</p>
          <div class="tags"><span>TypeScript</span><span>Docker</span></div>
        </div>
        <div class="status wip">EN COURS</div>
      </div>
    </div>
  </div>
</section>

<!-- ============ GITHUB STATS ============ -->
<section id="stats">
  <div class="wrap">
    <div class="mission-tag">MISSION 03</div>
    <h2 class="mission-title">RAPPORT DE COMBAT</h2>
    <div class="arsenal-grid">
      <img src="https://github-readme-stats.vercel.app/api?username=octocat&show_icons=true&theme=radical&hide_border=true&bg_color=120a1f&title_color=ff1244&icon_color=2af0e8&text_color=e8dfe6" alt="Statistiques GitHub" loading="lazy">
      <img src="https://github-readme-streak-stats.herokuapp.com/?user=octocat&theme=radical&hide_border=true&background=120a1f&ring=ff1244&fire=ff1244&currStreakLabel=2af0e8" alt="Streak GitHub" loading="lazy">
    </div>
    <p style="margin-top:16px; font-size:11px; color:var(--dim); letter-spacing:0.5px;">
      Remplace "octocat" par ton propre nom d'utilisateur GitHub dans les deux URLs ci-dessus.
    </p>
  </div>
</section>

<!-- ============ CONTACT ============ -->
<section id="contact" class="extraction">
  <div class="wrap">
    <div class="mission-tag" style="text-align:center;">MISSION FINALE</div>
    <h2 class="mission-title">POINT D'EXTRACTION</h2>
    <p>Un projet en tête, une idée un peu folle, ou juste envie de parler code ? Le canal est ouvert.</p>
    <div class="contact-row">
      <a class="btn" href="mailto:ton.email@exemple.com">EMAIL</a>
      <a class="btn alt" href="https://github.com/octocat" target="_blank" rel="noopener">GITHUB</a>
      <a class="btn alt" href="https://linkedin.com" target="_blank" rel="noopener">LINKEDIN</a>
    </div>
  </div>
</section>

<footer>DOSSIER_FERMÉ // GÉNÉRÉ POUR GITHUB PAGES</footer>

</body>
</html>
