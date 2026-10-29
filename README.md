<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#111216">
  <meta name="description" content="PHISHGUARD — ferramenta defensiva para análise de URLs, indicadores suspeitos e inteligência de ameaças.">
  <title>PHISHGUARD — URL Threat Intelligence</title>
  <style>
    :root {
      color-scheme: dark;
      --bg: #0b0c10;
      --panel: #12141a;
      --panel-2: #191b22;
      --line: #30333d;
      --text: #f3f4f6;
      --muted: #a4a8b3;
      --red: #f04452;
      --red-dark: #b92335;
      --red-soft: rgba(240, 68, 82, .12);
      --green: #62dfa0;
      --max: 1160px;
    }
    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin: 0;
      background: radial-gradient(ellipse at 75% 0%, rgba(240,68,82,.13), transparent 36rem), linear-gradient(180deg, #111216 0%, var(--bg) 70%);
      color: var(--text);
      font: 16px/1.6 Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }
    a { color: inherit; }
    .container { width: min(var(--max), calc(100% - 40px)); margin: 0 auto; }
    .topline { height: 3px; background: linear-gradient(90deg, transparent, var(--red), #ff8a92, transparent); }
    header { position: sticky; top: 0; z-index: 10; background: rgba(11,12,16,.88); backdrop-filter: blur(18px); border-bottom: 1px solid rgba(255,255,255,.08); }
    .nav { min-height: 76px; display:flex; align-items:center; justify-content:space-between; gap:20px; }
    .brand { display:flex; align-items:center; gap:12px; text-decoration:none; font-weight:900; letter-spacing:.12em; }
    .brand-mark { width:40px; height:40px; display:grid; place-items:center; border:1px solid rgba(240,68,82,.6); border-radius:12px; color:var(--red); background:var(--red-soft); font-size:22px; box-shadow:0 0 26px rgba(240,68,82,.12); }
    .brand small { display:block; color:var(--muted); font-size:10px; letter-spacing:.18em; font-weight:600; }
    .nav-links { display:flex; align-items:center; gap:24px; }
    .nav-links a { color:var(--muted); text-decoration:none; font-size:14px; }
    .nav-links a:hover { color:var(--text); }
    .btn { display:inline-flex; align-items:center; justify-content:center; gap:10px; min-height:48px; padding:0 20px; border:1px solid var(--line); border-radius:10px; text-decoration:none; font-weight:750; cursor:pointer; transition:transform .18s ease, border-color .18s ease, background .18s ease; }
    .btn:hover { transform:translateY(-2px); }
    .btn-primary { background:var(--red); border-color:var(--red); color:#fff; box-shadow:0 8px 30px rgba(240,68,82,.2); }
    .btn-primary:hover { background:#ff5360; }
    .btn-secondary { background:#1b1d24; color:var(--text); }
    .btn-secondary:hover { border-color:#656a78; }
    .hero { padding:88px 0 68px; overflow:hidden; }
    .hero-grid { display:grid; grid-template-columns:1.15fr .85fr; align-items:center; gap:56px; }
    .eyebrow { display:inline-flex; align-items:center; gap:9px; color:#ff8790; text-transform:uppercase; letter-spacing:.16em; font-size:12px; font-weight:800; }
    .dot { width:7px; height:7px; border-radius:50%; background:var(--red); box-shadow:0 0 14px var(--red); }
    h1 { margin:18px 0 18px; font-size:clamp(42px,6vw,72px); line-height:1.02; letter-spacing:-.055em; }
    h1 span { color:var(--red); }
    .lead { max-width:650px; color:#c1c4ce; font-size:18px; line-height:1.75; }
    .hero-actions { display:flex; flex-wrap:wrap; gap:12px; margin-top:28px; }
    .microcopy { color:var(--muted); font-size:12px; margin-top:15px; }
    .visual { position:relative; min-height:370px; display:grid; place-items:center; border:1px solid rgba(240,68,82,.25); border-radius:26px; overflow:hidden; background:linear-gradient(rgba(255,255,255,.025) 1px, transparent 1px), linear-gradient(90deg, rgba(255,255,255,.025) 1px, transparent 1px), radial-gradient(circle at 50% 40%, rgba(240,68,82,.2), transparent 54%), #101116; background-size:28px 28px,28px 28px,auto,auto; box-shadow:0 24px 80px rgba(0,0,0,.28), inset 0 0 50px rgba(240,68,82,.05); }
    .visual:before,.visual:after { content:""; position:absolute; border:1px solid rgba(240,68,82,.2); border-radius:50%; width:280px; height:280px; }
    .visual:after { width:215px; height:215px; border-style:dashed; animation:spin 38s linear infinite; }
    .shield { z-index:1; width:142px; height:166px; display:grid; place-items:center; color:var(--red); filter:drop-shadow(0 0 25px rgba(240,68,82,.45)); }
    .shield svg { width:100%; height:100%; }
    .scan-label { position:absolute; z-index:2; bottom:24px; left:24px; right:24px; padding:13px 15px; border:1px solid var(--line); border-radius:10px; background:rgba(10,11,15,.86); display:flex; justify-content:space-between; gap:12px; font-size:12px; }
    .scan-label strong { color:var(--green); letter-spacing:.08em; }
    @keyframes spin { to { transform:rotate(360deg); } }
    section { padding:58px 0; }
    .section-head { max-width:720px; margin-bottom:28px; }
    .section-head h2 { margin:8px 0 10px; font-size:clamp(28px,4vw,42px); line-height:1.15; letter-spacing:-.035em; }
    .section-head p { color:var(--muted); margin:0; }
    .cards { display:grid; grid-template-columns:repeat(3,1fr); gap:16px; }
    .card { padding:24px; border:1px solid var(--line); border-radius:16px; background:linear-gradient(145deg,rgba(255,255,255,.035),rgba(255,255,255,.012)); }
    .card-icon { width:44px; height:44px; display:grid; place-items:center; border-radius:12px; background:var(--red-soft); color:#ff6875; font-size:21px; margin-bottom:18px; }
    .card h3 { margin:0 0 8px; font-size:18px; }
    .card p { margin:0; color:var(--muted); font-size:14px; }
    .download-panel { border:1px solid rgba(240,68,82,.4); border-radius:22px; background:linear-gradient(120deg,rgba(240,68,82,.12),rgba(255,255,255,.02) 60%); padding:32px; display:grid; grid-template-columns:1fr auto; align-items:center; gap:24px; }
    .download-panel h2 { margin:0 0 8px; font-size:clamp(26px,4vw,38px); }
    .download-panel p { margin:0; color:var(--muted); }
    .platforms { display:flex; flex-wrap:wrap; gap:10px; margin-top:20px; }
    .platform { padding:7px 10px; border:1px solid var(--line); border-radius:7px; color:#d5d7de; font-size:12px; }
    .steps { display:grid; grid-template-columns:repeat(3,1fr); gap:16px; counter-reset:step; }
    .step { border-top:2px solid var(--red); padding:20px 4px 0; }
    .step:before { counter-increment:step; content:"0" counter(step); display:block; color:var(--red); font-weight:900; letter-spacing:.12em; margin-bottom:10px; }
    .step h3 { margin:0 0 8px; }
    .step p { margin:0; color:var(--muted); font-size:14px; }
    .notice { border-left:3px solid #e5a642; padding:14px 18px; color:#c9cbd2; background:rgba(229,166,66,.07); border-radius:0 8px 8px 0; font-size:13px; }
    footer { margin-top:30px; border-top:1px solid var(--line); padding:28px 0 40px; color:var(--muted); font-size:13px; }
    .footer-row { display:flex; justify-content:space-between; align-items:center; gap:16px; flex-wrap:wrap; }
    footer a { color:#d9dbe2; text-decoration:none; }
    @media (max-width:850px) { .hero-grid { grid-template-columns:1fr; gap:30px; } .visual { min-height:300px; } .cards { grid-template-columns:1fr 1fr; } .download-panel { grid-template-columns:1fr; } .nav-links { gap:12px; } }
    @media (max-width:580px) { .container { width:min(100% - 28px,var(--max)); } .nav { min-height:66px; } .nav-links a:not(.nav-download) { display:none; } .hero { padding:58px 0 38px; } .cards,.steps { grid-template-columns:1fr; } .download-panel { padding:23px; } .btn { width:100%; } .hero-actions { display:grid; } }
    @media (prefers-reduced-motion: reduce) { *,*::before,*::after { animation:none!important; scroll-behavior:auto!important; transition:none!important; } }
  </style>
</head>
<body>
  <div class="topline"></div>
  <header>
    <div class="container nav">
      <a class="brand" href="#"><span class="brand-mark">⛨</span><span>PHISHGUARD<small>URL THREAT INTELLIGENCE</small></span></a>
      <nav class="nav-links" aria-label="Navegação principal">
        <a href="#recursos">Recursos</a><a href="#download">Download</a><a href="#instalacao">Instalação</a>
        <a href="https://github.com/john-root-opsec/phishguard">Código-fonte</a>
        <a class="btn btn-primary nav-download" href="https://github.com/john-root-opsec/phishguard/releases/latest">Baixar agora ↗</a>
      </nav>
    </div>
  </header>
  <main>
    <section class="hero"><div class="container hero-grid"><div>
      <div class="eyebrow"><span class="dot"></span> Ferramenta de segurança defensiva</div>
      <h1>Investigue URLs.<br><span>Encontre sinais.</span></h1>
      <p class="lead">Analise a estrutura de endereços, investigue indicadores suspeitos e organize evidências técnicas em uma interface desktop desenvolvida para análise defensiva.</p>
      <div class="hero-actions"><a class="btn btn-primary" href="#download">⬇ &nbsp; Download do PHISHGUARD</a><a class="btn btn-secondary" href="https://github.com/john-root-opsec/phishguard">⌘ &nbsp; Ver código-fonte</a></div>
      <p class="microcopy">Projeto open source · Python · Linux e Windows em desenvolvimento</p>
    </div><div class="visual" aria-label="Ilustração abstrata de um escudo de segurança"><div class="shield"><svg viewBox="0 0 120 140" fill="none" aria-hidden="true"><path d="M60 7 106 24v37c0 32-19 54-46 70C33 115 14 93 14 61V24L60 7Z" stroke="currentColor" stroke-width="4"/><path d="M60 22 91 34v27c0 22-12 38-31 50C41 99 29 83 29 61V34L60 22Z" stroke="currentColor" stroke-width="1.5" opacity=".5"/><path d="m43 67 11 11 25-28" stroke="currentColor" stroke-width="5" stroke-linecap="round" stroke-linejoin="round"/></svg></div><div class="scan-label"><span>PHISHGUARD / SECURITY ENGINE</span><strong>● READY</strong></div></div></div></section>
    <section id="recursos"><div class="container"><div class="section-head"><div class="eyebrow">Capacidades principais</div><h2>Inteligência técnica. Evidências organizadas.</h2><p>Uma base modular para investigar URLs suspeitas e apoiar fluxos de trabalho de segurança defensiva.</p></div>
      <div class="cards">
        <article class="card"><div class="card-icon">⌕</div><h3>Análise de URL</h3><p>Inspecione a estrutura do endereço e extraia hostname, domínio e outros componentes relevantes.</p></article>
        <article class="card"><div class="card-icon">◈</div><h3>Indicadores de ameaça</h3><p>Organize sinais técnicos e resultados disponíveis para apoiar uma investigação.</p></article>
        <article class="card"><div class="card-icon">◎</div><h3>Threat intelligence</h3><p>Consulte fontes públicas compatíveis quando a integração estiver configurada e disponível.</p></article>
        <article class="card"><div class="card-icon">⌘</div><h3>Pesquisa de domínio</h3><p>Módulos dedicados a consultas DNS e dados de registro de domínio via RDAP.</p></article>
        <article class="card"><div class="card-icon">▤</div><h3>Relatórios técnicos</h3><p>Organize os resultados e exporte dados estruturados em formato JSON.</p></article>
        <article class="card"><div class="card-icon">▦</div><h3>Aplicação desktop</h3><p>Interface gráfica em Python com PySide6, desenvolvida para evoluir em Linux e Windows.</p></article>
      </div></div></section>
    <section id="download"><div class="container"><div class="download-panel"><div><div class="eyebrow">Obtenha o projeto</div><h2>Pronto para investigar?</h2><p>Consulte a versão mais recente e baixe os arquivos publicados na página oficial de Releases.</p><div class="platforms"><span class="platform">Windows · pacote a publicar</span><span class="platform">Linux · pacote a publicar</span><span class="platform">Código-fonte disponível</span></div></div><div><a class="btn btn-primary" href="https://github.com/john-root-opsec/phishguard/releases/latest">Ver downloads ↗</a><p class="microcopy">Abre a página oficial de Releases do GitHub.</p></div></div>
      <p class="notice" style="margin-top:18px"><strong>Disponibilidade:</strong> os instaladores para Windows e Linux só poderão ser baixados depois que os respectivos arquivos forem compilados, testados e anexados a uma Release. Até lá, o repositório contém o código-fonte.</p>
    </div></section>
    <section id="instalacao"><div class="container"><div class="section-head"><div class="eyebrow">Comece pelo código-fonte</div><h2>Instalação para desenvolvedores</h2><p>Enquanto os pacotes instaláveis não estiverem publicados, você pode executar o projeto a partir do código-fonte, conforme as dependências da versão atual.</p></div>
      <div class="steps"><article class="step"><h3>Clone o repositório</h3><p>Obtenha o código-fonte pelo GitHub e entre na pasta do projeto.</p></article><article class="step"><h3>Instale as dependências</h3><p>Crie um ambiente virtual e instale os pacotes definidos em <code>requirements.txt</code>.</p></article><article class="step"><h3>Execute e teste</h3><p>Siga as instruções do README e execute os testes automatizados disponíveis.</p></article></div>
      <div class="card" style="margin-top:22px"><pre style="margin:0;white-space:pre-wrap;overflow-wrap:anywhere;color:#e9eaf0"><code>git clone https://github.com/john-root-opsec/phishguard.git
cd phishguard
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python desktop.py</code></pre></div>
    </div></section>
    <section><div class="container"><div class="section-head"><div class="eyebrow">Uso responsável</div><h2>Feito para análise defensiva.</h2><p>PHISHGUARD auxilia a investigação, mas não substitui um antivírus, uma solução EDR ou uma plataforma de proteção em tempo real. Resultados dependem dos métodos implementados e das fontes consultadas.</p></div><a class="btn btn-secondary" href="https://github.com/john-root-opsec/phishguard">Explorar o projeto no GitHub ↗</a></div></section>
  </main>
  <footer><div class="container footer-row"><div><strong style="color:var(--text);letter-spacing:.1em">PHISHGUARD</strong><br>URL Threat Intelligence · Defensive Security</div><div>Desenvolvido por <a href="https://github.com/john-root-opsec">john-root-opsec</a> · <a href="https://github.com/john-root-opsec/phishguard">GitHub</a></div></div></footer>
</body>
</html>
