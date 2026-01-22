<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>CTMP | Cost of Waiting Counter</title>

  <style>
    :root{
      --bg:#000000;
      --panel:#070000;
      --panel2:#0d0000;

      /* all-red theme */
      --text:#ff2a2a;
      --muted:#ff6b6b;
      --line:#ff2a2a;
      --accent:#ff2a2a;
      --softglow: rgba(255,42,42,.22);
      --hardglow: rgba(255,42,42,.55);
    }

    *{ box-sizing:border-box; }

    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Noto Sans", "Helvetica Neue", sans-serif;
      background:
        radial-gradient(1200px 700px at 50% -10%, rgba(255,42,42,.18) 0%, rgba(0,0,0,1) 55%),
        radial-gradient(900px 450px at 10% 20%, rgba(255,42,42,.06) 0%, rgba(0,0,0,0) 60%),
        #000;
      color: var(--text);
    }

    a{
      color: var(--text);
      text-decoration: underline;
      text-underline-offset: 2px;
    }

    .wrap{
      max-width: 980px;
      margin: 0 auto;
      padding: 22px 14px 40px;
    }

    .header{
      border: 1px solid var(--line);
      border-radius: 16px;
      background: linear-gradient(180deg, rgba(255,42,42,.10), rgba(0,0,0,0));
      padding: 18px 18px 16px;
      box-shadow: 0 0 30px rgba(255,42,42,.08);
    }

    h1{
      margin:0;
      font-size: 22px;
      letter-spacing: 1px;
      text-transform: uppercase;
    }

    .subtitle{
      margin-top: 8px;
      color: var(--muted);
      font-size: 14px;
      line-height: 1.45;
      display:flex;
      flex-wrap:wrap;
      align-items:center;
      gap:10px;
    }

    .live{
      display:inline-flex;
      align-items:center;
      gap:8px;
      font-size: 12px;
      letter-spacing: .4px;
      color: var(--muted);
      white-space: nowrap;
      padding: 4px 10px;
      border: 1px solid rgba(255,42,42,.35);
      border-radius: 999px;
      background: rgba(255,42,42,.06);
    }

    .dot{
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: var(--accent);
      box-shadow: 0 0 12px rgba(255,42,42,.9);
      animation: pulse 1.4s infinite;
    }

    @keyframes pulse{
      0%{ transform: scale(1); opacity: .55; }
      50%{ transform: scale(1.45); opacity: 1; }
      100%{ transform: scale(1); opacity: .55; }
    }

    .keyline{
      margin-top: 10px;
      font-size: 14px;
      line-height: 1.55;
      color: var(--muted);
    }
    .keyline strong{ color: var(--text); }

    .grid{
      display:grid;
      grid-template-columns: 1.6fr 1fr;
      gap: 12px;
      margin-top: 12px;
    }

    @media (max-width: 820px){
      .grid{ grid-template-columns: 1fr; }
    }

    .big{
      border: 1px solid var(--line);
      border-radius: 16px;
      background: rgba(7,0,0,.78);
      padding: 16px;
      box-shadow: 0 0 26px rgba(255,42,42,.08);
    }

    .label{
      color: var(--muted);
      font-size: 12px;
      letter-spacing: .9px;
      text-transform: uppercase;
    }

    .value{
      margin-top: 10px;
      font-size: clamp(44px, 6vw, 72px);
      line-height: 1.05;
      font-weight: 850;
      letter-spacing: 1px;
      text-shadow: 0 0 18px var(--softglow);
      cursor: help;
      user-select: none;
    }

    .metaRow{
      margin-top: 12px;
      display:flex;
      flex-wrap:wrap;
      gap: 8px;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.4;
    }

    .pill{
      border: 1px solid rgba(255,42,42,.45);
      border-radius: 999px;
      padding: 6px 10px;
      background: rgba(255,42,42,.05);
    }
    .pill strong{ color: var(--text); font-weight: 750; }

    .side{
      border: 1px solid var(--line);
      border-radius: 16px;
      background: rgba(7,0,0,.78);
      padding: 12px;
      display:grid;
      gap: 10px;
      box-shadow: 0 0 26px rgba(255,42,42,.08);
    }

    .stat{
      border: 1px solid rgba(255,42,42,.45);
      border-radius: 14px;
      padding: 12px;
      background: rgba(255,42,42,.04);
    }

    .stat .num{
      font-size: 28px;
      font-weight: 850;
      line-height: 1.1;
      text-shadow: 0 0 14px var(--softglow);
    }

    .stat .name{
      margin-top: 6px;
      color: var(--muted);
      font-size: 11px;
      letter-spacing: .8px;
      text-transform: uppercase;
    }

    .cards{
      display:grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 12px;
      margin-top: 12px;
    }

    @media (max-width: 820px){
      .cards{ grid-template-columns: 1fr; }
    }

    .card{
      border: 1px solid var(--line);
      border-radius: 16px;
      padding: 14px 14px;
      background: rgba(7,0,0,.78);
      box-shadow: 0 0 22px rgba(255,42,42,.06);
    }

    .card h3{
      margin:0 0 8px 0;
      font-size: 13px;
      letter-spacing: .8px;
      text-transform: uppercase;
    }

    .card p{
      margin: 0 0 10px 0;
      color: var(--muted);
      line-height: 1.55;
      font-size: 14px;
    }

    .card p:last-child{ margin-bottom:0; }

    .rule{
      height:1px;
      width:100%;
      background: rgba(255,42,42,.35);
      margin: 10px 0;
    }

    .callout{
      margin-top: 12px;
      border: 1px solid rgba(255,42,42,.55);
      border-radius: 16px;
      padding: 14px;
      background: rgba(255,42,42,.05);
      box-shadow: 0 0 26px rgba(255,42,42,.07);
    }

    .callout .title{
      font-weight: 850;
      letter-spacing: .7px;
      text-transform: uppercase;
      margin-bottom: 8px;
    }

    .callout .text{
      color: var(--muted);
      line-height: 1.6;
      font-size: 14px;
    }

    .footer{
      margin-top: 12px;
      border: 1px solid var(--line);
      border-radius: 16px;
      padding: 14px;
      background: rgba(7,0,0,.78);
      color: var(--muted);
      font-size: 13px;
      line-height: 1.6;
    }

    .footer .sources-title{
      color: var(--text);
      font-weight: 850;
      letter-spacing: .7px;
      text-transform: uppercase;
      margin-bottom: 6px;
    }

    .footer ul{
      margin: 8px 0 0 18px;
      padding: 0;
    }

    .tiny{
      font-size: 12px;
      color: rgba(255,107,107,.95);
    }

    .mono{
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
      letter-spacing: .2px;
    }
  </style>
</head>

<body>
  <div class="wrap">

    <div class="header">
      <h1>COST OF WAITING COUNTER</h1>
      <div class="subtitle">
        A simple model that turns delay into a number you can see.
        <span class="live"><span class="dot" aria-hidden="true"></span> Updates automatically</span>
      </div>

      <div class="keyline">
        <strong>How it works:</strong> time since <span id="refHuman"></span> (UTC) multiplied by a stated rate of
        <span id="rateHuman"></span>.
        This is a model, not a live registry.
      </div>
    </div>

    <div class="grid">
      <div class="big">
        <div class="label">Total since reference date (modeled)</div>
        <div
          class="value"
          id="totalCounter"
          title="Modeled estimate: elapsed time multiplied by the stated daily rate. This does not identify individuals or report real-time events."
        >0</div>

        <div class="metaRow">
          <div class="pill">Start (UTC): <strong id="refDateText">2025-08-24</strong></div>
          <div class="pill">Rate: <strong id="ratePerDayText">1,382</strong> per day</div>
          <div class="pill">Per hour (derived): <strong id="perHourText">0</strong></div>
          <div class="pill">Mode: <strong>Reference-date only</strong></div>
        </div>

        <div class="rule"></div>

        <div class="tiny">
          Tip: you can override the rate for transparency using <span class="mono">?rate=1500</span>
        </div>
      </div>

      <div class="side">
        <div class="stat">
          <div class="num" id="todayCounter">0</div>
          <div class="name">Modeled today (UTC)</div>
        </div>
        <div class="stat">
          <div class="num" id="yearCounter">0</div>
          <div class="name">Modeled this year (UTC)</div>
        </div>
        <div class="stat">
          <div class="num" id="daysDelayed">0</div>
          <div class="name">Days since reference</div>
        </div>
      </div>
    </div>

    <div class="cards">
      <div class="card">
        <h3>What this is</h3>
        <p>
          This page is a clock.
          It converts elapsed time into a running estimate using one stated rate.
        </p>
        <p>
          If you refresh the page, it does not reset.
          Time keeps moving, so the number keeps moving.
        </p>
      </div>

      <div class="card">
        <h3>What this is not</h3>
        <p>
          This is not a live feed of incidents.
          It does not report real-time events or identify individuals.
        </p>
        <p>
          It is simple arithmetic:
          elapsed time multiplied by a stated daily rate.
        </p>
      </div>
    </div>

    <div class="callout">
      <div class="title">Why this is on the website</div>
      <div class="text">
        Most people can feel delay, but they cannot measure it.
        This counter makes delay legible.
        It turns waiting into clear arithmetic so the public can see what “later” costs under a stated assumption.
        <br /><br />
        CTMP exists to remove structural delay by making abundant baseload power available at a posted tariff of 2.5 cents per kWh.
        This page is here to hold time accountable, in plain sight.
      </div>
    </div>

    <div class="footer">
      <div class="sources-title">Sources (to document the rate you choose)</div>
      <div>
        Pick a rate you can defend publicly, and cite the basis.
        These references are here to support transparent, method-based estimates.
      </div>
      <ul>
        <li>WHO Global Health Estimates (GHE): Mortality and global health estimates. <a href="https://www.who.int/data/gho/data/themes/mortality-and-global-health-estimates" target="_blank" rel="noopener">WHO</a></li>
        <li>WHO GHE methods (technical): Methods and data sources for global burden of disease estimates 2000–2021. <a href="https://cdn.who.int/media/docs/default-source/gho-documents/global-health-estimates/ghe2021_daly_methods.pdf" target="_blank" rel="noopener">WHO (PDF)</a></li>
        <li>WHO/UNICEF Joint Monitoring Programme (JMP): Global WASH data. <a href="https://washdata.org/" target="_blank" rel="noopener">JMP</a></li>
        <li>UN IGME: Levels and Trends in Child Mortality report page. <a href="https://data.unicef.org/resources/levels-and-trends-in-child-mortality-2024/" target="_blank" rel="noopener">UNICEF Data</a></li>
        <li>GATHER Statement (2016): Reporting standard for health estimates transparency. <a href="https://www.healthdata.org/sites/default/files/files/GATHER-statement_2016.pdf" target="_blank" rel="noopener">GATHER (PDF)</a></li>
      </ul>
      <div class="tiny" style="margin-top:10px;">
        Counter basis: fixed reference date plus stated daily rate. Modeled estimate only.
      </div>
    </div>

  </div>

  <script>
    // -----------------------------
    // CONFIG
    // -----------------------------
    const REF_DATE_UTC = "2025-08-24T00:00:00Z";

    let RATE_PER_DAY = 1382;

    // Optional URL override: ?rate=1500
    const params = new URLSearchParams(window.location.search);
    const rateParam = params.get("rate");
    if (rateParam) {
      const n = Number(rateParam);
      // sanity bounds: positive, not absurd
      if (Number.isFinite(n) && n > 0 && n < 1000000) RATE_PER_DAY = n;
    }

    // -----------------------------
    // HELPERS
    // -----------------------------
    const nf0 = new Intl.NumberFormat("en-US", { maximumFractionDigits: 0 });
    const nf2 = new Intl.NumberFormat("en-US", { minimumFractionDigits: 2, maximumFractionDigits: 2 });

    function $(id){ return document.getElementById(id); }

    function startOfUtcDay(d){
      return new Date(Date.UTC(d.getUTCFullYear(), d.getUTCMonth(), d.getUTCDate(), 0,0,0,0));
    }

    function startOfUtcYear(d){
      return new Date(Date.UTC(d.getUTCFullYear(), 0, 1, 0,0,0,0));
    }

    function toHumanUtcDate(iso){
      const d = new Date(iso);
      const months = ["January","February","March","April","May","June","July","August","September","October","November","December"];
      return months[d.getUTCMonth()] + " " + d.getUTCDate() + ", " + d.getUTCFullYear();
    }

    function safeFloor(n){
      // guard against NaN and negative
      if (!Number.isFinite(n) || n < 0) return 0;
      return Math.floor(n);
    }

    // -----------------------------
    // INIT STATIC TEXT
    // -----------------------------
    $("refDateText").textContent = REF_DATE_UTC.slice(0,10);
    $("ratePerDayText").textContent = nf0.format(RATE_PER_DAY);
    $("perHourText").textContent = nf2.format(RATE_PER_DAY / 24);
    $("refHuman").textContent = toHumanUtcDate(REF_DATE_UTC);
    $("rateHuman").textContent = nf0.format(RATE_PER_DAY) + " per day";

    // -----------------------------
    // UPDATE LOOP
    // -----------------------------
    function update(){
      const now = new Date();
      const ref = new Date(REF_DATE_UTC);

      const elapsedMs = Math.max(0, now.getTime() - ref.getTime());
      const elapsedDays = elapsedMs / 86400000;

      const total = elapsedDays * RATE_PER_DAY;

      // Today (UTC)
      const dayStart = startOfUtcDay(now);
      const todayMs = Math.max(0, now.getTime() - dayStart.getTime());
      const today = (todayMs / 86400000) * RATE_PER_DAY;

      // This year (UTC)
      const yearStart = startOfUtcYear(now);
      const yearMs = Math.max(0, now.getTime() - yearStart.getTime());
      const year = (yearMs / 86400000) * RATE_PER_DAY;

      // Days since reference
      const days = safeFloor(elapsedDays);

      $("totalCounter").textContent = nf0.format(safeFloor(total));
      $("todayCounter").textContent = nf0.format(safeFloor(today));
      $("yearCounter").textContent = nf0.format(safeFloor(year));
      $("daysDelayed").textContent = nf0.format(days);
    }

    update();
    setInterval(update, 250);
  </script>
</body>
</html>
