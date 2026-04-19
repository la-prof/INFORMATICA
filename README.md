<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Corso AI per Docenti</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=DM+Sans:wght@300;400;500&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}

:root{
  --ink:#0f1117;
  --ink-mid:#1c2030;
  --gold:#c9a84c;
  --gold-pale:#e8cc80;
  --cream:#f5f0e6;
  --cream-dim:rgba(245,240,230,.7);
  --muted:#8a8d99;
  --border:rgba(201,168,76,.18);
  --border-dim:rgba(201,168,76,.09);
}

html{scroll-behavior:smooth}
body{font-family:'DM Sans',sans-serif;font-weight:300;background:var(--ink);color:var(--cream);min-height:100vh;overflow-x:hidden}

/* NAV */
nav{
  position:fixed;top:0;left:0;right:0;z-index:100;
  display:flex;align-items:center;justify-content:space-between;
  padding:16px 48px;
  background:rgba(15,17,23,.88);
  backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);
  border-bottom:1px solid rgba(201,168,76,.1);
}
.nav-brand{font-family:'Playfair Display',serif;font-size:1rem;font-weight:700;color:var(--gold)}
.nav-brand span{color:var(--cream);font-style:italic;font-weight:400}
.nav-meta{font-family:'DM Mono',monospace;font-size:.68rem;letter-spacing:.12em;color:var(--muted)}

/* HERO */
.hero{
  min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;
  text-align:center;padding:120px 24px 80px;position:relative;overflow:hidden;
}
.hero-grid{position:absolute;inset:0;background-image:linear-gradient(rgba(201,168,76,.045) 1px,transparent 1px),linear-gradient(90deg,rgba(201,168,76,.045) 1px,transparent 1px);background-size:60px 60px;pointer-events:none}
.hero::before{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 80% 55% at 50% 0%,rgba(201,168,76,.11) 0%,transparent 70%);pointer-events:none}
.hero-content{position:relative;z-index:1;max-width:780px}

.hero-eyebrow{
  display:inline-flex;align-items:center;gap:10px;
  font-family:'DM Mono',monospace;font-size:.7rem;letter-spacing:.2em;text-transform:uppercase;
  color:var(--gold);background:rgba(201,168,76,.09);border:1px solid rgba(201,168,76,.22);
  padding:6px 16px;border-radius:2px;margin-bottom:32px;
  animation:fadeUp .6s ease both;
}
.eyebrow-dot{width:6px;height:6px;border-radius:50%;background:var(--gold);animation:pulse 2s ease infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.35;transform:scale(.75)}}

.hero-headline{
  font-family:'Playfair Display',serif;font-size:clamp(2.6rem,6.5vw,4.8rem);
  font-weight:900;line-height:1.06;letter-spacing:-.02em;color:var(--cream);
  margin-bottom:12px;animation:fadeUp .6s .1s ease both;
}
.hero-headline em{font-style:italic;color:var(--gold)}
.hero-sub{
  font-size:1.05rem;color:var(--muted);line-height:1.75;max-width:540px;
  margin:22px auto 40px;font-weight:300;animation:fadeUp .6s .2s ease both;
}
.hero-sub strong{color:var(--cream);font-weight:400}

.hero-meta{
  display:flex;align-items:center;justify-content:center;gap:28px;flex-wrap:wrap;
  animation:fadeUp .6s .3s ease both;
  font-family:'DM Mono',monospace;font-size:.72rem;letter-spacing:.1em;color:var(--muted);
  text-transform:uppercase;
}
.hero-meta-dot{width:4px;height:4px;border-radius:50%;background:var(--gold);opacity:.5}

.scroll-cue{
  position:absolute;bottom:32px;left:50%;transform:translateX(-50%);
  display:flex;flex-direction:column;align-items:center;gap:8px;
  font-family:'DM Mono',monospace;font-size:.58rem;letter-spacing:.18em;text-transform:uppercase;color:var(--muted);
  animation:fadeUp 1s .8s ease both;
}
.scroll-line{width:1px;height:32px;background:linear-gradient(to bottom,var(--gold),transparent);animation:scrollPulse 2.2s ease infinite}
@keyframes scrollPulse{0%,100%{opacity:.35}50%{opacity:1}}
@keyframes fadeUp{from{opacity:0;transform:translateY(18px)}to{opacity:1;transform:translateY(0)}}

/* SECTION SHARED */
section{padding:72px 24px}
.section-inner{max-width:900px;margin:0 auto}
.section-eyebrow{font-family:'DM Mono',monospace;font-size:.66rem;letter-spacing:.2em;text-transform:uppercase;color:var(--gold);display:block;margin-bottom:14px}
.section-title{font-family:'Playfair Display',serif;font-size:clamp(1.7rem,3.5vw,2.4rem);font-weight:700;color:var(--cream);line-height:1.2;margin-bottom:14px}
.section-sub{font-size:.95rem;color:var(--muted);line-height:1.7}

/* SECTION DIVIDER */
.section-rule{height:1px;background:var(--border-dim);max-width:900px;margin:0 auto}

/* CARDS GRID */
.cards-section{background:var(--ink)}
.cards-grid{
  display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));
  gap:2px;margin-top:48px;
}
.material-card{
  background:var(--ink-mid);border:1px solid var(--border-dim);
  text-decoration:none;display:block;
  transition:border-color .3s,background .3s,transform .2s;
  position:relative;overflow:hidden;
}
.material-card::before{
  content:'';position:absolute;top:0;left:0;right:0;height:2px;
  background:var(--card-accent,var(--gold));
  transform:scaleX(0);transform-origin:left;transition:transform .3s;
}
.material-card:hover{border-color:var(--border);background:#1a1d28;transform:translateY(-2px)}
.material-card:hover::before{transform:scaleX(1)}
.card-top{padding:24px 22px 18px}
.card-tag{
  font-family:'DM Mono',monospace;font-size:.62rem;letter-spacing:.16em;text-transform:uppercase;
  color:var(--gold);margin-bottom:10px;display:block;
}
.card-title{font-family:'Playfair Display',serif;font-size:1.15rem;font-weight:700;color:var(--cream);margin-bottom:8px;line-height:1.25}
.card-desc{font-size:.82rem;color:var(--muted);line-height:1.6}
.card-bottom{
  padding:12px 22px;border-top:1px solid var(--border-dim);
  display:flex;justify-content:space-between;align-items:center;
}
.card-duration{font-family:'DM Mono',monospace;font-size:.68rem;letter-spacing:.06em;color:var(--muted)}
.card-arrow{color:var(--gold);font-size:.95rem;font-weight:500;transition:transform .2s}
.material-card:hover .card-arrow{transform:translateX(4px)}

/* COMING SOON CARD */
.card-coming{opacity:.45;pointer-events:none}
.card-coming .card-tag{color:var(--muted)}
.card-coming .card-arrow{color:var(--muted)}

/* INFO BOXES */
.info-section{background:#13151e}
.info-grid{
  display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
  gap:16px;margin-top:40px;
}
.info-card{
  background:var(--ink-mid);border:1px solid var(--border-dim);
  border-radius:2px;padding:22px;
  transition:border-color .3s,transform .2s;
}
.info-card:hover{border-color:var(--border);transform:translateY(-2px)}
.info-card-label{
  font-family:'DM Mono',monospace;font-size:.62rem;letter-spacing:.16em;text-transform:uppercase;
  color:var(--gold);margin-bottom:10px;display:block;
}
.info-card h4{font-size:.95rem;font-weight:500;color:var(--cream);margin-bottom:8px}
.info-card p{font-size:.8rem;color:var(--muted);line-height:1.65}

/* FOOTER */
footer{
  background:#090b10;border-top:1px solid rgba(201,168,76,.08);
  padding:32px 24px;text-align:center;
}
.footer-brand{font-family:'Playfair Display',serif;font-size:.95rem;color:var(--gold);margin-bottom:8px}
.footer-meta{font-size:.75rem;color:var(--muted)}
.footer-meta a{color:var(--gold);text-decoration:none}
.footer-meta a:hover{color:var(--gold-pale)}

@media(max-width:600px){
  nav{padding:14px 20px}
  .nav-meta{display:none}
}
</style>
</head>
<body>

<nav>
  <div class="nav-brand">Corso AI <span>per Docenti</span></div>
  <div class="nav-meta">Prof.ssa Elisabetta Chiurco · 2025</div>
</nav>

<section class="hero">
  <div class="hero-grid"></div>
  <div class="hero-content">

    <div class="hero-eyebrow">
      <span class="eyebrow-dot"></span>
      Formazione Docenti · AI nella Didattica
    </div>

    <h1 class="hero-headline">
      L'intelligenza artificiale<br>
      <em>al servizio di chi insegna.</em>
    </h1>

    <p class="hero-sub">
      Materiali per la lezione laboratoriale sull'utilizzo dell'AI nella
      <strong>scuola secondaria di secondo grado</strong>.
      Strumenti pratici, guide e laboratori per integrare l'AI nella pratica didattica quotidiana.
    </p>

    <div class="hero-meta">
      <span>Scuola sec. 2° grado</span>
      <span class="hero-meta-dot"></span>
      <span>Lezione laboratoriale </span>
      <span class="hero-meta-dot"></span>
      <span>A cura di Prof.ssa Chiurco Elisabetta</span>
    </div>

  </div>
  <div class="scroll-cue">
    <div class="scroll-line"></div>
    Materiali
  </div>
</section>

<!-- MATERIALI -->
<section class="cards-section">
  <div class="section-inner">
    <span class="section-eyebrow">// Materiali del corso</span>
    <h2 class="section-title">Tutto il necessario per iniziare.</h2>
    <p class="section-sub">Dalla lezione introduttiva alle guide pratiche per ogni strumento, fino al laboratorio di prompt engineering.</p>

    <div class="cards-grid">

      <a class="material-card" href="lezione.html" style="--card-accent:#7090e8">
        <div class="card-top">
          <span class="card-tag">Modulo 01 · Lezione</span>
          <div class="card-title">Lezione Laboratoriale</div>
          <div class="card-desc">Panoramica completa degli strumenti AI per la didattica: chatbot generalisti, strumenti specializzati, etica e quiz finale.</div>
        </div>
        <div class="card-bottom">
          <span class="card-duration">2 ore · 6 moduli</span>
          <span class="card-arrow">→</span>
        </div>
      </a>

      <a class="material-card" href="guida.html" style="--card-accent:var(--gold)">
        <div class="card-top">
          <span class="card-tag">Guida di Riferimento</span>
          <div class="card-title">Guida Pratica a Claude</div>
          <div class="card-desc">Come usare Claude in modo efficace: chat, Projects, funzionalità chiave, prompt pronti e confronto tra piani.</div>
        </div>
        <div class="card-bottom">
          <span class="card-duration">7 sezioni · con esempi</span>
          <span class="card-arrow">→</span>
        </div>
      </a>

      <a class="material-card" href="guida_gemini.html" style="--card-accent:#70a8f0">
        <div class="card-top">
          <span class="card-tag">Guida di Riferimento</span>
          <div class="card-title">Guida Pratica a Gemini</div>
          <div class="card-desc">Come usare Gemini in modo efficace: integrazione Google Workspace, Gems, NotebookLM, prompt pronti e confronto tra piani.</div>
        </div>
        <div class="card-bottom">
          <span class="card-duration">7 sezioni · con esempi</span>
          <span class="card-arrow">→</span>
        </div>
      </a>

      <a class="material-card" href="prompt-lab.html" style="--card-accent:#b070e8">
        <div class="card-top">
          <span class="card-tag">Strumento Pratico</span>
          <div class="card-title">Prompt Engineering Lab</div>
          <div class="card-desc">Costruisci prompt efficaci con il framework R·C·T·F: compila i quattro campi e ottieni il prompt pronto da copiare.</div>
        </div>
        <div class="card-bottom">
          <span class="card-duration">4 componenti · prompt pronto</span>
          <span class="card-arrow">→</span>
        </div>
      </a>

      <a class="material-card" href="lezione_finale.html" style="--card-accent:#70c8a8">
        <div class="card-top">
          <span class="card-tag">Modulo 06 · Lezione Finale</span>
          <div class="card-title">Strumenti Specializzati per Docenti</div>
          <div class="card-desc">Laboratorio conclusivo: Magic School AI, Diffit e Curipod. Dal prompting generalista ai tool pensati specificamente per chi insegna.</div>
        </div>
        <div class="card-bottom">
          <span class="card-duration">2 ore · 6 sezioni</span>
          <span class="card-arrow">→</span>
        </div>
      </a>

    </div>
  </div>
</section>

<div class="section-rule"></div>

<!-- INFO -->
<section class="info-section">
  <div class="section-inner">
    <span class="section-eyebrow">// Informazioni utili</span>
    <h2 class="section-title">Il corso in sintesi.</h2>

    <div class="info-grid">
      <div class="info-card">
        <span class="info-card-label">Strumenti trattati</span>
        <p>Claude · ChatGPT · Gemini · Perplexity · Poe · Mizou · SchoolAI · Magic School AI · Botsonic · Synthesia · Gamma</p>
      </div>
      <div class="info-card">
        <span class="info-card-label">Obiettivi</span>
        <p>Conoscere i principali strumenti AI, saper creare prompt efficaci, integrare l'AI nella propria pratica didattica in modo consapevole.</p>
      </div>
      <div class="info-card">
        <span class="info-card-label">Prerequisiti</span>
        <p>Nessuna conoscenza tecnica richiesta. È sufficiente saper usare un browser e avere un account email per la registrazione agli strumenti.</p>
      </div>
      <div class="info-card">
        <span class="info-card-label">Come usare i materiali</span>
        <p>I materiali sono pensati per essere proiettati durante la lezione. Ogni sezione include esempi pratici e prompt pronti da copiare.</p>
      </div>
    </div>
  </div>
</section>

<footer>
  <div class="footer-brand">Corso AI per Docenti</div>
  <p class="footer-meta">Materiali a cura di Prof.ssa Chiurco Elisabetta · Aggiornato 2025 · <a href="https://la-prof.github.io/CORSO-AI/">la-prof.github.io/CORSO-AI</a></p>
</footer>

</body>
</html>
