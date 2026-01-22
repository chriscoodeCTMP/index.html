<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>CTMP | Cost of Waiting Counter</title>

  <style>
    :root{
      --bg:#000;
      --panel:#0a0a0a;
      --panel2:#120000;
      --red:#ff0000;
      --white:#ffffff;
      --muted:#bbbbbb;
      --muted2:#8a8a8a;
      --border:#330000;
      --shadow: 0 10px 30px rgba(0,0,0,0.5);
      --radius: 16px;
      --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
      --sans: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Noto Sans", "Liberation Sans", sans-serif;
    }

    html,body{height:100%}
    body{
      margin:0;
      background: radial-gradient(1200px 800px at 20% 0%, #120000 0%, #000 60%);
      color:var(--white);
      font-family:var(--sans);
    }

    .wrap{
      max-width: 1050px;
      margin: 0 auto;
      padding: 22px 16px 40px;
    }

    .header{
      background: linear-gradient(180deg, rgba(255,0,0,0.09), rgba(0,0,0,0.2));
      border: 1px solid rgba(255,0,0,0.25);
      border-radius: var(--radius);
      padding: 18px 18px;
      box-shadow: var(--shadow);
    }
    .header h1{
      margin:0 0 6px;
      letter-spacing: 0.08em;
      font-size: 20px;
      font-family: var(--mono);
      color: var(--white);
    }
    .subtitle{
      margin: 0 0 10px;
      color: var(--muted);
      font-size: 14px;
    }
    .tagline{
      margin:0;
      color: var(--muted2);
      font-size: 13px;
      line-height: 1.35;
    }

    .settings{
      margin-top: 14px;
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      justify-content:space-between;
    }
    .left,.right{display:flex; gap:10px; flex-wrap:wrap}
    .pill{
      background: rgba(255,255,255,0.03);
      border: 1px solid rgba(255,0,0,0.18);
      border-radius: 999px;
      padding: 8px 12px;
      font-family: var(--mono);
      font-size: 12px;
      color: var(--muted);
      white-space: nowrap;
    }
    .pill strong{color: var(--white); font-weight: 700;}

    .counter-section{
      margin-top: 16px;
      background: linear-gradient(180deg, rgba(255,0,0,0.06), rgba(0,0,0,0.25));
      border: 1px solid rgba(255,0,0,0.22);
      border-radius: var(--radius);
      padding: 16px;
      box-shadow: var(--shadow);
    }

    .clock-title{
      font-family: var(--mono);
      letter-spacing: 0.08em;
      color: var(--white);
      font-size: 12px;
      text-transform: uppercase;
      margin-bottom: 6px;
    }
    .clock-subtitle{
      color: var(--muted2);
      font-size: 13px;
      margin-bottom: 14px;
    }

    .main-counter{
      display:flex;
      justify-content:center;
      margin: 10px 0 12px;
    }
    .counter-box{
      width: min(680px, 100%);
      background: rgba(0,0,0,0.35);
      border: 1px solid rgba(255,0,0,0.28);
      border-radius: var(--radius);
      padding: 16px 14px;
      text-align:center;
    }
    .counter-value{
      font-family: var(--mono);
      font-size: clamp(34px, 6vw, 64px);
      color: var(--red);
      font-weight: 800;
      letter-spacing: 0.02em;
      line-height: 1.05;
    }
    .counter-label{
      margin-top: 6px;
      font-family: var(--mono);
      color: var(--muted2);
      font-size: 12px;
      letter-spacing: 0.08em;
    }

    .global-stats{
      display:grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 10px;
    }
    @media (max-width: 860px){
      .global-stats{grid-template-columns: repeat(2, minmax(0, 1fr));}
    }
    .global-stat-box{
      background: rgba(255,255,255,0.03);
      border: 1px solid rgba(255,0,0,0.16);
      border-radius: 14px;
      padding: 12px 12px;
    }
    .global-stat-number{
      font-family: var(--mono);
      font-size: 20px;
      color: var(--white);
      font-weight: 700;
    }
    .global-stat-label{
      margin-top: 4px;
      color: var(--muted2);
      font-size: 12px;
    }

    .info-grid{
      margin-top: 16px;
      display:grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 12px;
    }
    @media (max-width: 860px){
      .info-grid{grid-template-columns: 1fr;}
    }

    .card{
      background: rgba(0,0,0,0.28);
      border: 1px solid rgba(255,0,0,0.16);
      border-radius: var(--radius);
      padding: 14px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.35);
    }
    .card h3{
      margin: 0 0 8px;
      font-family: var(--mono);
      letter-spacing: 0.08em;
      font-size: 12px;
      text-transform: uppercase;
      color: var(--white);
    }
    .card p{
      margin: 0 0 10px;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.45;
    }
    .card p:last-child{margin-bottom:0;}
    .emph{color: var(--white); font-weight: 700;}

    .footer{
      margin-top: 16px;
      border-top: 1px solid rgba(255,0,0,0.18);
      padding-top: 14px;
      color: var(--muted2);
      font-size: 12px;
      line-height: 1.45;
    }
    .statement{
      font-family: var(--mono);
      color: var(--white);
      margin-bottom: 6px;
    }
    .sources{
      margin-top: 10px;
      background: rgba(255,255,255,0.02);
      border: 1px solid rgba(255,0,0,0.14);
      border-radius: 14px;
      padding: 10px 12px;
    }
    .sources-title{margin-bottom: 6px; color: var(--white); font-family: var(--mono);}
    .sources ul{margin: 0; padding-left: 18px;}
    .sources li{margin: 6px 0;}
    .sources a{color: #ff6666; text-decoration: none;}
    .sources a:hover{text-decoration: underline;}
  </style>
</head>

<body>
  <div class="wrap">
    <div class="header">
      <h1>COST OF WAITING COUNTER</h1>
      <div class="subtitle">A modeled estimate of delay cost using a fixed start date and a stated daily rate</div>
      <div class="tagline">
        This page does not report real-time events or identify individuals. It displays a time-based estimate derived from a fixed start date and a stated daily rate.
      </div>
    </div>

    <div class="settings">
      <div class="left">
        <div class="pill">Start date (UTC): <strong id="refDateText">2025-08-24</strong></div>
        <div class="pill">Rate: <strong id="ratePerDayText">1,382</strong> per day</div>
      </div>
      <div class="right">
        <div class="pill">Model type: <strong>Reference-date only</strong></div>
        <div class="pill">Refresh behavior: <strong>No reset</strong></div>
      </div>
    </div>

    <div class="counter-section">
      <div class="clock-title">MODELED DELAY COST SINCE CTMP READINESS DATE</div>
      <div class="clock-subtitle">
        Reference: <span id="referenceLabel">August 24, 2025</span> to present (UTC basis)
      </div>

      <div class="main-counter">
        <div class="counter-box">
          <div class="counter-value" id="totalCounter">0</div>
          <div class="counter-label">TOTAL (MODELED)</div>
        </div>
      </div>

      <div class="global-stats">
        <div class="global-stat-box">
          <div class="global-stat-number" id="todayCounter">0</div>
          <div class="global-stat-label">Modeled Today (UTC)</div>
        </div>

        <div class="global-stat-box">
          <div class="global-stat-number" id="yearCounter">0</div>
          <div class="global-stat-label">Modeled This Year (UTC)</div>
        </div>

        <div class="global-stat-box">
          <div class="global-stat-number" id="perHour">0</div>
          <div class="global-stat-label">Per Hour (Derived)</div>
        </div>

        <div class="global-stat-box">
          <div class="global-stat-number" id="daysDelayed">0</div>
          <div class="global-stat-label">Days Since Reference</div>
        </div>
      </div>
    </div>

    <div class="info-grid">
      <div class="card">
        <h3>WHAT THIS IS</h3>
        <p>
          A <span class="emph">modeled counter</span> that converts time elapsed since a fixed reference date into a running estimate using a stated daily rate.
        </p>
        <p>
          Refreshing the page does not restart anything. The value changes only because time has moved forward.
        </p>
      </div>

      <div class="card">
        <h3>WHAT THIS IS NOT</h3>
        <p>
          It is <span class="emph">not</span> a live feed of incidents or outcomes. It does not report real-time events. It does not identify individuals.
        </p>
        <p>
          It is simple arithmetic: <span class="emph">elapsed time × stated rate</span>.
        </p>
      </div>

      <div class="card">
        <h3>MODEL ASSUMPTION</h3>
        <p>
          Daily rate used here: <span class="emph" id="rateInline">1,382</span> per day.
          Derived: <span class="emph" id="perMinute">0</span> per minute and <span class="emph" id="msPerOne">0</span> ms per 1.
        </p>
        <p>
          If the daily rate changes, all derived values update consistently.
        </p>
      </div>

      <div class="card">
        <h3>FRAMING</h3>
        <p class="emph">From this point on, delay is not confusion. It is consent.</p>
        <p>
          This page communicates the cost of delay in plain arithmetic, without presenting itself as a live registry.
        </p>
      </div>
    </div>

    <div class="footer">
      <div class="statement">CTMP: Living proof that scarcity is a choice.</div>
      <div>
        Counter basis: fixed reference date + stated daily rate. This is a modeled estimate, not a real-time registry.
      </div>

      <div class="sources">
        <div class="sources-title"><strong>Sources</strong></div>
        <ul>
          <li>WHO Global Health Estimates (GHE): Mortality and Global Health Estimates. <a href="https://www.who.int/data/gho/data/themes/mortality-and-global-health-estimates" target="_blank" rel="noopener">WHO</a></li>
          <li>WHO GHE methods: Methods and data sources (technical methods PDF). <a href="https://cdn.who.int/media/docs/default-source/gho-documents/global-health-estimates/ghe2021_daly_methods.pdf" target="_blank" rel="noopener">WHO (PDF)</a></li>
          <li>WHO/UNICEF Joint Monitoring Programme (JMP): Global WASH data. <a href="https://washdata.org/" target="_blank" rel="noopener">JMP</a></li>
          <li>UN IGME: Levels and Trends in Child Mortality. <a href="https://data.unicef.org/resources/levels-and-trends-in-child-mortality-2024/" target="_blank" rel="noopener">UNICEF Data</a></li>
          <li>GATHER Statement (2016): Reporting guideline for health estimates. <a href="https://www.healthdata.org/sites/default/files/files/GATHER-statement_2016.pdf" target="_blank" rel="noopener">GATHER (PDF)</a></li>
        </ul>
      </div>
    </div>
  </div>

  <script>
    // ---------------------------
    // CONFIG (edit only these)
    // ---------------------------
    const REF_DATE_UTC = "2025-08-24T00:00:00Z"; // fixed start date (UTC)
    const RATE_PER_DAY = 1382;                  // stated daily rate (number)

    // ---------------------------
    // Helpers
    // ---------------------------
    const fmtInt = new Intl.NumberFormat(undefined, { maximumFractionDigits: 0 });
    const MS_PER_DAY = 24 * 60 * 60 * 1000;

    function el(id){
      const node = document.getElementById(id);
      if(!node) throw new Error("Missing element id: " + id);
      return node;
    }

    function setText(id, value){
      el(id).textContent = value;
    }

    function startOfUtcDay(ts){
      const d = new Date(ts);
      return Date.UTC(d.getUTCFullYear(), d.getUTCMonth(), d.getUTCDate(), 0, 0, 0, 0);
    }

    function startOfUtcYear(ts){
      const d = new Date(ts);
      return Date.UTC(d.getUTCFullYear(), 0, 1, 0, 0, 0, 0);
    }

    // ---------------------------
    // Init visible config fields
    // ---------------------------
    const ref = new Date(REF_DATE_UTC);
    if (Number.isNaN(ref.getTime())) throw new Error("Bad REF_DATE_UTC: " + REF_DATE_UTC);
    if (!Number.isFinite(RATE_PER_DAY) || RATE_PER_DAY <= 0) throw new Error("Bad RATE_PER_DAY: " + RATE_PER_DAY);

    setText("refDateText", "2025-08-24");
    setText("ratePerDayText", fmtInt.format(RATE_PER_DAY));
    setText("rateInline", fmtInt.format(RATE_PER_DAY));

    const perMinute = RATE_PER_DAY / 1440;
    const msPerOne = (MS_PER_DAY / RATE_PER_DAY);

    setText("perMinute", perMinute.toFixed(3));
    setText("msPerOne", fmtInt.format(Math.round(msPerOne)));

    // ---------------------------
    // Main update loop
    // ---------------------------
    function update(){
      const now = Date.now();

      const elapsedMs = now - ref.getTime();
      const elapsedDays = Math.max(0, elapsedMs / MS_PER_DAY);

      const total = elapsedDays * RATE_PER_DAY;

      const todayStart = startOfUtcDay(now);
      const todayMs = now - todayStart;
      const today = Math.max(0, (todayMs / MS_PER_DAY) * RATE_PER_DAY);

      const yearStart = startOfUtcYear(now);
      const yearMs = now - yearStart;
      const year = Math.max(0, (yearMs / MS_PER_DAY) * RATE_PER_DAY);

      setText("totalCounter", fmtInt.format(Math.floor(total)));
      setText("todayCounter", fmtInt.format(Math.floor(today)));
      setText("yearCounter", fmtInt.format(Math.floor(year)));
      setText("perHour", fmtInt.format(Math.round(RATE_PER_DAY / 24)));
      setText("daysDelayed", fmtInt.format(Math.floor(elapsedDays)));
    }

    // Run once immediately, then smoothly.
    update();
    setInterval(update, 250);
  </script>
</body>
</html>
