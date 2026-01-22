<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>CTMP | Cost of Waiting Counter</title>

  <style>
    :root{
      --bg:#000;
      --panel:#0b0b0b;
      --panel2:#111;
      --text:#fff;
      --muted:#b6b6b6;
      --line:#222;
      --accent:#ff2a2a;
    }

    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Noto Sans", "Helvetica Neue", sans-serif;
      background: radial-gradient(1200px 600px at 50% -10%, #220000 0%, #000 60%);
      color:var(--text);
    }

    .wrap{
      max-width: 980px;
      margin: 0 auto;
      padding: 28px 16px 40px;
    }

    .header{
      display:flex;
      flex-direction:column;
      gap:10px;
      padding: 18px 18px;
      border: 1px solid var(--line);
      border-radius: 16px;
      background: linear-gradient(180deg, rgba(255,42,42,.08), rgba(0,0,0,0));
    }

    h1{
      margin:0;
      letter-spacing: 1px;
      font-size: 22px;
    }

    .subtitle{
      color:var(--muted);
      line-height: 1.35;
      font-size: 14px;
    }

    .keyline{
      margin-top:6px;
      font-size: 15px;
      line-height: 1.45;
    }
    .keyline strong{ color:#fff; }
    .keyline .accent{ color:var(--accent); font-weight:700; }

    .grid{
      display:grid;
      grid-template-columns: 1.6fr 1fr;
      gap: 14px;
      margin-top: 14px;
    }

    @media (max-width: 820px){
      .grid{ grid-template-columns: 1fr; }
    }

    .big{
      border: 1px solid var(--line);
      border-radius: 16px;
      background: rgba(11,11,11,.78);
      padding: 18px;
      overflow:hidden;
      position:relative;
    }

    .big .label{
      color:var(--muted);
      font-size: 13px;
      letter-spacing: .8px;
      text-transform: uppercase;
    }

    .big .value{
      margin-top: 10px;
      font-size: clamp(44px, 6vw, 68px);
      line-height: 1.05;
      font-weight: 800;
      letter-spacing: 1px;
    }

    .metaRow{
      margin-top: 12px;
      display:flex;
      flex-wrap:wrap;
      gap: 10px;
      color:var(--muted);
      font-size: 13px;
    }

    .pill{
      border: 1px solid var(--line);
      border-radius: 999px;
      padding: 6px 10px;
      background: rgba(17,17,17,.7);
    }
    .pill strong{ color:#fff; font-weight:700; }

    .side{
      border: 1px solid var(--line);
      border-radius: 16px;
      background: rgba(11,11,11,.78);
      padding: 14px;
      display:grid;
      gap: 10px;
    }

    .stat{
      border: 1px solid var(--line);
      border-radius: 14px;
      padding: 12px;
      background: rgba(17,17,17,.65);
    }

    .stat .num{
      font-size: 28px;
      font-weight: 800;
      line-height: 1.1;
    }

    .stat .name{
      margin-top: 6px;
      color:var(--muted);
      font-size: 12px;
      letter-spacing: .6px;
      text-transform: uppercase;
    }

    .cards{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 14px;
      margin-top: 14px;
    }

    @media (max-width: 820px){
      .cards{ grid-template-columns: 1fr; }
    }

    .card{
      border: 1px solid var(--line);
      border-radius: 16px;
      padding: 14px 14px;
      background: rgba(11,11,11,.78);
    }

    .card h3{
      margin:0 0 8px 0;
      font-size: 14px;
      letter-spacing: .6px;
      text-transform: uppercase;
    }

    .card p{
      margin: 0 0 8px 0;
      color: var(--muted);
      line-height: 1.5;
      font-size: 14px;
    }

    .card p:last-child{ margin-bottom:0; }

    .footer{
      margin-top: 16px;
      border: 1px solid var(--line);
      border-radius: 16px;
      padding: 14px;
      background: rgba(11,11,11,.78);
      color: var(--muted);
      font-size: 13px;
      line-height: 1.55;
    }

    .footer .sources-title{
      color:#fff;
      font-weight:700;
      margin-bottom: 8px;
    }

    .footer ul{
      margin: 8px 0 0 18px;
      padding: 0;
    }
    .footer a{
      color:#fff;
      text-decoration: underline;
      text-underline-offset: 2px;
    }
  </style>
</head>

<body>
  <div class="wrap">

    <div class="header">
      <h1>COST OF WAITING COUNTER</h1>
      <div class="subtitle">
        A simple model that turns delay into a number you can see.
      </div>

      <div class="keyline">
        <strong>How it works:</strong> time since <span class="accent" id="refHuman">August 24, 2025</span>
        multiplied by a stated rate of <span class="accent" id="rateHuman">1,382 per day</span>.
        <br />
        This is an estimate. It is not a live registry of real-time events.
      </div>
    </div>

    <div class="grid">
      <div class="big">
        <div class="label">Total since reference date (modeled)</div>
        <div class="value" id="totalCounter">0</div>

        <div class="metaRow">
          <div class="pill">Start (UTC): <strong id="refDateText">2025-08-24</strong></div>
          <div class="pill">Rate: <strong id="ratePerDayText">1,382</strong> per day</div>
          <div class="pill">Per hour (derived): <strong id="perHourText">0</strong></div>
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
          A clock that shows a running estimate based on elapsed time.
        </p>
        <p>
          Refreshing the page does not reset it. Time keeps moving, so the number keeps moving.
        </p>
      </div>

      <div class="card">
        <h3>What this is not</h3>
        <p>
          Not a live feed. Not real-time reporting. Not individual records.
        </p>
        <p>
          Just a model: elapsed time multiplied by a stated rate.
        </p>
      </div>

      <div class="card">
        <h3>The rate</h3>
        <p>
          The daily rate is a published assumption.
          If you change it, every number updates automatically.
        </p>
        <p>
          The point is clarity: people can see what delay costs under the stated assumption.
        </p>
      </div>
    </div>

    <div class="footer">
      <div class="sources-title">Sources (for documenting the underlying rate)</div>
      <div>
        Use these to justify whatever daily rate you choose to publish, and to document methods transparently.
      </div>
      <ul>
        <li>WHO Global Health Estimates (GHE): Mortality and global health estimates. <a href="https://www.who.int/data/gho/data/themes/mortality-and-global-health-estimates" target="_blank" rel="noopener">WHO</a></li>
        <li>WHO GHE methods (technical): “Methods and data sources for global burden of disease estimates 2000–2021”. <a href="https://cdn.who.int/media/docs/default-source/gho-documents/global-health-estimates/ghe2021_daly_methods.pdf" target="_blank" rel="noopener">WHO (PDF)</a></li>
        <li>WHO/UNICEF Joint Monitoring Programme (JMP): Global WASH data. <a href="https://washdata.org/" target="_blank" rel="noopener">JMP</a></li>
        <li>UN IGME: Levels and Trends in Child Mortality report page. <a href="https://data.unicef.org/resources/levels-and-trends-in-child-mortality-2024/" target="_blank" rel="noopener">UNICEF Data</a></li>
        <li>GATHER Statement (2016): Reporting standard for health estimates transparency. <a href="https://www.healthdata.org/sites/default/files/files/GATHER-statement_2016.pdf" target="_blank" rel="noopener">GATHER (PDF)</a></li>
      </ul>
    </div>

  </div>

  <script>
    // --------- CONFIG (simple, visible, editable) ----------
    const REF_DATE_UTC = "2025-08-24T00:00:00Z";
    const RATE_PER_DAY = 1382;

    // --------- HELPERS ----------
    const nf0 = new Intl.NumberFormat("en-US", { maximumFractionDigits: 0 });
    const nf2 = new Intl.NumberFormat("en-US", { minimumFractionDigits: 2, maximumFractionDigits: 2 });

    function $(id){ return document.getElementById(id); }

    function startOfUtcDay(d){
      return new Date(Date.UTC(d.getUTCFullYear(), d.getUTCMonth(), d.getUTCDate(), 0,0,0,0));
    }
    function startOfUtcYear(d){
      return new Date(Date.UTC(d.getUTCFullYear(), 0, 1, 0,0,0,0));
    }

    function toHumanDate(iso){
      const d = new Date(iso);
      const months = ["January","February","March","April","May","June","July","August","September","October","November","December"];
      return months[d.getUTCMonth()] + " " + d.getUTCDate() + ", " + d.getUTCFullYear();
    }

    // --------- INIT STATIC TEXT ----------
    $("refDateText").textContent = REF_DATE_UTC.slice(0,10);
    $("ratePerDayText").textContent = nf0.format(RATE_PER_DAY);
    $("refHuman").textContent = toHumanDate(REF_DATE_UTC);
    $("rateHuman").textContent = nf0.format(RATE_PER_DAY) + " per day";
    $("perHourText").textContent = nf2.format(RATE_PER_DAY / 24);

    // --------- UPDATE LOOP ----------
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
      const days = Math.floor(elapsedDays);

      $("totalCounter").textContent = nf0.format(Math.floor(total));
      $("todayCounter").textContent = nf0.format(Math.floor(today));
      $("yearCounter").textContent = nf0.format(Math.floor(year));
      $("daysDelayed").textContent = nf0.format(days);
    }

    update();
    setInterval(update, 250);
  </script>
</body>
</html>
