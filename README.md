# ThreadEverest
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>ThreadEverest — Custom Sportswear Manufacturer</title>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --black: #0a0a0a;
      --white: #f5f2ee;
      --red: #d42b2b;
      --red-dark: #a01f1f;
      --gray: #1a1a1a;
      --gray-mid: #2e2e2e;
      --text-muted: #888;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--black);
      color: var(--white);
      font-family: 'DM Sans', sans-serif;
      font-weight: 300;
      overflow-x: hidden;
    }

    /* NOISE OVERLAY */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 999;
      opacity: 0.4;
    }

    /* NAV */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.4rem 4rem;
      background: rgba(10,10,10,0.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid rgba(255,255,255,0.05);
    }

    .nav-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.6rem;
      letter-spacing: 0.1em;
      color: var(--white);
      text-decoration: none;
    }

    .nav-logo span { color: var(--red); }

    nav ul {
      list-style: none;
      display: flex;
      gap: 2.5rem;
    }

    nav ul a {
      color: var(--text-muted);
      text-decoration: none;
      font-size: 0.85rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      transition: color 0.2s;
    }

    nav ul a:hover { color: var(--white); }

    .nav-cta {
      background: var(--red);
      color: var(--white) !important;
      padding: 0.5rem 1.2rem;
      border-radius: 2px;
    }

    .nav-cta:hover { background: var(--red-dark); color: var(--white) !important; }

    /* HERO */
    #hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 10rem 4rem 6rem;
      position: relative;
      overflow: hidden;
    }

    #hero::after {
      content: 'TE';
      position: absolute;
      right: -2rem;
      bottom: -4rem;
      font-family: 'Bebas Neue', sans-serif;
      font-size: 30vw;
      color: rgba(255,255,255,0.02);
      line-height: 1;
      pointer-events: none;
      user-select: none;
    }

    .hero-tag {
      font-size: 0.75rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--red);
      margin-bottom: 1.5rem;
      opacity: 0;
      animation: fadeUp 0.8s ease forwards 0.2s;
    }

    h1 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(4rem, 10vw, 9rem);
      line-height: 0.95;
      letter-spacing: 0.02em;
      max-width: 900px;
      opacity: 0;
      animation: fadeUp 0.9s ease forwards 0.4s;
    }

    h1 em {
      font-style: normal;
      color: var(--red);
    }

    .hero-sub {
      margin-top: 2rem;
      font-size: 1.05rem;
      color: var(--text-muted);
      max-width: 520px;
      line-height: 1.7;
      opacity: 0;
      animation: fadeUp 0.9s ease forwards 0.6s;
    }

    .hero-btns {
      margin-top: 3rem;
      display: flex;
      gap: 1rem;
      opacity: 0;
      animation: fadeUp 0.9s ease forwards 0.8s;
    }

    .btn {
      display: inline-block;
      padding: 0.85rem 2rem;
      font-size: 0.85rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      text-decoration: none;
      border-radius: 2px;
      transition: all 0.2s;
      font-family: 'DM Sans', sans-serif;
      font-weight: 500;
    }

    .btn-primary {
      background: var(--red);
      color: var(--white);
    }

    .btn-primary:hover { background: var(--red-dark); transform: translateY(-2px); }

    .btn-outline {
      border: 1px solid rgba(255,255,255,0.2);
      color: var(--white);
    }

    .btn-outline:hover { border-color: var(--white); transform: translateY(-2px); }

    /* MARQUEE */
    .marquee-wrap {
      background: var(--red);
      padding: 0.9rem 0;
      overflow: hidden;
      white-space: nowrap;
    }

    .marquee-track {
      display: inline-block;
      animation: marquee 20s linear infinite;
    }

    .marquee-track span {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1rem;
      letter-spacing: 0.15em;
      margin: 0 2rem;
      color: rgba(255,255,255,0.9);
    }

    @keyframes marquee {
      from { transform: translateX(0); }
      to { transform: translateX(-50%); }
    }

    /* SECTIONS */
    section {
      padding: 7rem 4rem;
    }

    .section-label {
      font-size: 0.7rem;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: var(--red);
      margin-bottom: 1rem;
    }

    h2 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(2.5rem, 5vw, 4.5rem);
      letter-spacing: 0.04em;
      line-height: 1;
      margin-bottom: 1rem;
    }

    /* SPORTS GRID */
    #sports { background: var(--gray); }

    .sports-intro {
      max-width: 500px;
      color: var(--text-muted);
      line-height: 1.7;
      margin-bottom: 4rem;
    }

    .sports-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 1px;
      background: rgba(255,255,255,0.05);
      border: 1px solid rgba(255,255,255,0.05);
    }

    .sport-card {
      background: var(--gray);
      padding: 2rem 1.8rem;
      transition: background 0.2s;
      cursor: default;
    }

    .sport-card:hover { background: var(--gray-mid); }

    .sport-icon {
      font-size: 1.8rem;
      margin-bottom: 1rem;
    }

    .sport-card h3 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.3rem;
      letter-spacing: 0.06em;
      margin-bottom: 0.4rem;
    }

    .sport-card p {
      font-size: 0.8rem;
      color: var(--text-muted);
      line-height: 1.6;
    }

    /* CAPABILITIES */
    #capabilities { background: var(--black); }

    .cap-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 4rem;
      margin-top: 4rem;
    }

    .cap-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 0;
    }

    .cap-list li {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.2rem 0;
      border-bottom: 1px solid rgba(255,255,255,0.07);
      font-size: 0.9rem;
    }

    .cap-list li span:first-child {
      color: var(--text-muted);
      text-transform: uppercase;
      font-size: 0.75rem;
      letter-spacing: 0.1em;
    }

    .cap-list li span:last-child {
      color: var(--white);
      font-weight: 500;
      text-align: right;
      max-width: 60%;
    }

    .cap-highlight {
      background: var(--gray);
      padding: 3rem;
      border-left: 3px solid var(--red);
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    .cap-highlight blockquote {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 2.2rem;
      line-height: 1.1;
      letter-spacing: 0.04em;
      margin-bottom: 1.5rem;
    }

    .cap-highlight p {
      color: var(--text-muted);
      font-size: 0.85rem;
      line-height: 1.7;
    }

    /* WHY */
    #why { background: var(--gray); }

    .why-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 2rem;
      margin-top: 4rem;
    }

    .why-card {
      padding: 2.5rem 2rem;
      border: 1px solid rgba(255,255,255,0.07);
      transition: border-color 0.2s, transform 0.2s;
    }

    .why-card:hover {
      border-color: var(--red);
      transform: translateY(-4px);
    }

    .why-num {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 3rem;
      color: var(--red);
      opacity: 0.4;
      line-height: 1;
      margin-bottom: 1rem;
    }

    .why-card h3 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.4rem;
      letter-spacing: 0.06em;
      margin-bottom: 0.7rem;
    }

    .why-card p {
      font-size: 0.85rem;
      color: var(--text-muted);
      line-height: 1.7;
    }

    /* CONTACT */
    #contact {
      background: var(--black);
      text-align: center;
    }

    #contact h2 { margin-bottom: 1rem; }

    #contact p {
      color: var(--text-muted);
      max-width: 480px;
      margin: 0 auto 3rem;
      line-height: 1.7;
    }

    .contact-links {
      display: flex;
      justify-content: center;
      gap: 1.5rem;
      flex-wrap: wrap;
      margin-top: 2rem;
    }

    .contact-link {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      color: var(--text-muted);
      text-decoration: none;
      font-size: 0.85rem;
      letter-spacing: 0.05em;
      transition: color 0.2s;
      padding: 0.8rem 1.5rem;
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 2px;
    }

    .contact-link:hover { color: var(--white); border-color: rgba(255,255,255,0.2); }

    /* FOOTER */
    footer {
      padding: 2rem 4rem;
      border-top: 1px solid rgba(255,255,255,0.05);
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 0.75rem;
      color: var(--text-muted);
    }

    .footer-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.2rem;
      letter-spacing: 0.1em;
      color: var(--white);
    }

    .footer-logo span { color: var(--red); }

    /* ANIMATIONS */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* RESPONSIVE */
    @media (max-width: 768px) {
      nav { padding: 1.2rem 1.5rem; }
      nav ul { display: none; }
      #hero { padding: 8rem 1.5rem 4rem; }
      section { padding: 5rem 1.5rem; }
      .cap-grid { grid-template-columns: 1fr; gap: 2rem; }
      .why-grid { grid-template-columns: 1fr; }
      footer { flex-direction: column; gap: 1rem; text-align: center; }
    }
  </style>
</head>
<body>

  <!-- NAV -->
  <nav>
    <a href="#" class="nav-logo">Thread<span>Everest</span></a>
    <ul>
      <li><a href="#sports">Sports</a></li>
      <li><a href="#capabilities">Capabilities</a></li>
      <li><a href="#why">Why Us</a></li>
      <li><a href="#contact" class="nav-cta">Get a Quote</a></li>
    </ul>
  </nav>

  <!-- HERO -->
  <section id="hero">
    <p class="hero-tag">Custom Sportswear Manufacturer — Pakistan → Worldwide</p>
    <h1>Built For <em>Performance.</em> Made To Order.</h1>
    <p class="hero-sub">Full-custom uniforms and jerseys for teams, coaches, and brands. Sublimation printing, low MOQs, worldwide shipping.</p>
    <div class="hero-btns">
      <a href="#contact" class="btn btn-primary">Get a Quote</a>
      <a href="#sports" class="btn btn-outline">View Sports</a>
    </div>
  </section>

  <!-- MARQUEE -->
  <div class="marquee-wrap">
    <div class="marquee-track">
      <span>Football</span><span>•</span>
      <span>Baseball</span><span>•</span>
      <span>Basketball</span><span>•</span>
      <span>Soccer</span><span>•</span>
      <span>Ice Hockey</span><span>•</span>
      <span>Lacrosse</span><span>•</span>
      <span>Wrestling</span><span>•</span>
      <span>Volleyball</span><span>•</span>
      <span>Softball</span><span>•</span>
      <span>Paintball</span><span>•</span>
      <span>Martial Arts</span><span>•</span>
      <span>Football</span><span>•</span>
      <span>Baseball</span><span>•</span>
      <span>Basketball</span><span>•</span>
      <span>Soccer</span><span>•</span>
      <span>Ice Hockey</span><span>•</span>
      <span>Lacrosse</span><span>•</span>
      <span>Wrestling</span><span>•</span>
      <span>Volleyball</span><span>•</span>
      <span>Softball</span><span>•</span>
      <span>Paintball</span><span>•</span>
      <span>Martial Arts</span><span>•</span>
    </div>
  </div>

  <!-- SPORTS -->
  <section id="sports">
    <p class="section-label">What We Make</p>
    <h2>Every Sport.<br>Every Position.</h2>
    <p class="sports-intro">From full uniform sets to individual jerseys — fully customized with your colors, logos, names, and numbers.</p>

    <div class="sports-grid">
      <div class="sport-card">
        <div class="sport-icon">🏈</div>
        <h3>Football Uniforms</h3>
        <p>Full sets for tackle and 7v7 — jerseys, pants, and complete kits</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">⚾</div>
        <h3>Baseball Uniforms</h3>
        <p>Jerseys, pants, and full team sets — pro-style cuts and custom graphics</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">🏀</div>
        <h3>Basketball Uniforms</h3>
        <p>Jerseys and shorts, reversible options available for full teams</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">⚽</div>
        <h3>Soccer Uniforms</h3>
        <p>Jerseys, shorts, socks, and complete kits for any club or league</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">🏒</div>
        <h3>Ice Hockey Jerseys</h3>
        <p>Pro-style cuts with custom sublimation graphics and team branding</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">🥍</div>
        <h3>Lacrosse Uniforms</h3>
        <p>Jerseys, shorts, and protective gear covers — fully customized</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">🤼</div>
        <h3>Wrestling Singlets</h3>
        <p>Custom sublimation, all cuts — built for performance and comfort</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">🏐</div>
        <h3>Volleyball Jerseys</h3>
        <p>Men's and women's cuts, full team sets with custom design</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">🥎</div>
        <h3>Softball Uniforms</h3>
        <p>Jerseys, pants, and complete kits for teams and leagues</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">🎽</div>
        <h3>Paintball Jerseys</h3>
        <p>Custom sublimation with padded options for competitive play</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">🥋</div>
        <h3>Martial Arts Gis</h3>
        <p>BJJ, Judo, Karate — custom patches, embroidery, and branding</p>
      </div>
      <div class="sport-card">
        <div class="sport-icon">👟</div>
        <h3>Training Gear</h3>
        <p>Compression wear, training tops, and warm-up suits for any sport</p>
      </div>
    </div>
  </section>

  <!-- CAPABILITIES -->
  <section id="capabilities">
    <p class="section-label">Our Capabilities</p>
    <h2>Full Custom.<br>Start to Finish.</h2>

    <div class="cap-grid">
      <ul class="cap-list">
        <li>
          <span>Printing Method</span>
          <span>Sublimation, Screen Print, Embroidery, Heat Transfer</span>
        </li>
        <li>
          <span>MOQ</span>
          <span>Flexible — Low MOQs Available</span>
        </li>
        <li>
          <span>Customization</span>
          <span>Full Custom Design, Logos, Names & Numbers</span>
        </li>
        <li>
          <span>Production</span>
          <span>OEM & Private Label</span>
        </li>
        <li>
          <span>Shipping</span>
          <span>Worldwide</span>
        </li>
        <li>
          <span>Market Focus</span>
          <span>US Market & Global</span>
        </li>
      </ul>

      <div class="cap-highlight">
        <blockquote>"Direct Manufacturer. No Middlemen. Better Pricing."</blockquote>
        <p>We handle everything in-house — from design and fabric to printing and shipping. That means faster turnaround, tighter quality control, and pricing that works for teams of any size.</p>
      </div>
    </div>
  </section>

  <!-- WHY -->
  <section id="why">
    <p class="section-label">Why ThreadEverest</p>
    <h2>What Sets<br>Us Apart.</h2>

    <div class="why-grid">
      <div class="why-card">
        <div class="why-num">01</div>
        <h3>Direct Manufacturer</h3>
        <p>No middlemen. You work directly with the factory — better pricing, faster communication, full control.</p>
      </div>
      <div class="why-card">
        <div class="why-num">02</div>
        <h3>Low MOQ</h3>
        <p>Accessible for small teams and growing brands. You don't need a massive order to get quality gear.</p>
      </div>
      <div class="why-card">
        <div class="why-num">03</div>
        <h3>Full Customization</h3>
        <p>Your colors, your logos, your names and numbers. Every detail built exactly to your spec.</p>
      </div>
      <div class="why-card">
        <div class="why-num">04</div>
        <h3>Worldwide Shipping</h3>
        <p>We ship to the US and globally. Reliable logistics with tracking and on-time delivery.</p>
      </div>
      <div class="why-card">
        <div class="why-num">05</div>
        <h3>US Market Experience</h3>
        <p>We understand US quality standards, sizing, and team requirements — built into every order.</p>
      </div>
      <div class="why-card">
        <div class="why-num">06</div>
        <h3>OEM & Private Label</h3>
        <p>Launching your own brand? We handle full private label production from fabric to finished product.</p>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact">
    <p class="section-label">Get In Touch</p>
    <h2>Ready to Order?<br>Let's Talk.</h2>
    <p>Send us your requirements and we'll get back to you with a quote — fast. Whether it's 10 jerseys or 1000, we've got you covered.</p>
    <a href="https://instagram.com/threadeverest" class="btn btn-primary" target="_blank">DM Us on Instagram</a>

    <div class="contact-links">
      <a href="https://instagram.com/threadeverest" class="contact-link" target="_blank">
        📸 @threadeverest
      </a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <div class="footer-logo">Thread<span>Everest</span></div>
    <div>© 2025 ThreadEverest. All rights reserved.</div>
    <div>Pakistan → Worldwide</div>
  </footer>

</body>
</html>

