<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>CTMP | Cost of Waiting Counter</title>
  <style>
    :root{
      --bg:#000;
      --panel:#0a0a0a;
      --panel2:#1a0000;
      --red:#ff0000;
      --white:#ffffff;
      --muted:#888888;
      --border:#ff0000;
    }

    body{
      font-family:"Courier New", monospace;
      background:var(--bg);
      color:var(--red);
      overflow-x:hidden;
      margin:0;
      padding:0;
    }

    .container{
      max-width:1400px;
      margin:0 auto;
      padding:40px 20px;
    }

    /* Header */
    .header{
      text-align:center;
      margin-bottom:50px;
      border-bottom:2px solid var(--border);
      padding-bottom:30px;
    }
    .header h1{
      font-size:42px;
      margin:0 0 14px 0;
      letter-spacing:2px;
      text-shadow:0 0 10px rgba(255,0,0,0.7);
      color:var(--red);
    }
    .header .subtitle{
      font-size:18px;
      color:var(--white);
      margin-bottom:6px;
    }
    .header .tagline{
      font-size:14px;
      color:var(--muted);
      line-height:1.5;
      max-width:980px;
      margin:0 auto;
    }

    /* Main Counter Section */
    .counter-section{
      background:var(--panel);
      border:3px solid var(--border);
      border-radius:10px;
      padding:34px;
      margin-bottom:26px;
      box-shadow:0 0 20px rgba(255,0,0,0.25);
    }
    .clock-title{
      font-size:22px;
      text-align:center;
      margin-bottom:6px;
      color:var(--white);
      letter-spacing:1px;
    }
    .clock-subtitle{
      font-size:14px;
      text-align:center;
      margin-bottom:22px;
      color:var(--muted);
      line-height:1.5;
    }

    .main-counter{
      display:flex;
      justify-content:center;
      align-items:center;
      gap:16px;
      flex-wrap:wrap;
      margin-bottom:26px;
    }
    .counter-box{
      background:var(--panel2);
      border:2px solid var(--border);
      border-radius:8px;
      padding:24px 30px;
      text-align:center;
      min-width:240px;
    }
    .counter-value{
      font-size:56px;
      font-weight:bold;
      color:var(--red);
      text-shadow:0 0 14px rgba(255,0,0,0.85);
      animation:pulse 2s infinite;
    }
    .counter-label{
      font-size:14px;
      color:var(--white);
      margin-top:8px;
      letter-spacing:1px;
    }
    @keyframes pulse{
      0%,100%{opacity:1}
      50%{opacity:0.75}
    }

    .global-stats{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(240px,1fr));
      gap:14px;
      margin-top:14px;
    }
    .global-stat-box{
      background:var(--panel2);
      border:2px solid var(--border);
      border-radius:8px;
      padding:18px;
      text-align:center;
    }
    .global-stat-number{
      font-size:38px;
      color:var(--red);
      font-weight:bold;
      margin-bottom:8px;
      text-shadow:0 0 10px rgba(255,0,0,0.6);
    }
    .global-stat-label{
      font-size:13px;
      color:var(--white);
    }

    /* Info blocks */
    .info-grid{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(320px,1fr));
      gap:16px;
      margin-bottom:26px;
    }
    .card{
      background:var(--panel);
      border:2px solid var(--border);
      border-radius:8px;
      padding:22px;
    }
    .card h3{
      font-size:18px;
      color:var(--white);
      margin:0 0 12px 0;
      border-bottom:1px solid var(--border);
      padding-bottom:10px;
      letter-spacing:1px;
    }
    .card p{
      margin:10px 0;
      color:var(--muted);
      line-height:1.6;
      font-size:14px;
    }
    .card .emph{
      color:var(--red);
      font-weight:bold;
    }

    /* Settings strip */
    .settings{
      background:var(--panel);
      border:2px solid var(--border);
      border-radius:8px;
      padding:16px 18px;
      margin-bottom:26px;
      display:flex;
      flex-wrap:wrap;
      gap:10px 18px;
      align-items:center;
      justify-content:space-between;
    }
    .settings .left, .settings .right{
      display:flex;
      flex-wrap:wrap;
      gap:10px 16px;
      align-items:center;
    }
    .pill{
      border:1px solid var(--border);
      background:#060606;
      border-radius:999px;
      padding:8px 12px;
      color:var(--white);
      font-size:12px;
      line-height:1;
    }
    .pill strong{ color:var(--red); }

    /* Footer */
    .footer{
      margin-top:20px;
      text-align:center;
      padding:22px 16px;
      border-top:2px solid var(--border);
      color:var(--muted);
      font-size:12px;
      line-height:1.6;
    }
    .footer .statement{
      font-size:15px;
      color:var(--red);
      margin-bottom:10px;
      font-weight:bold;
      text-shadow:0 0 8px rgba(255,0,0,0.6);
    }

    /* Responsive */
    @media (max-width:768px){
      .header h1{ font-size:30px; }
      .counter-value{ font-size:44px; }
      .counter-box{ min-width:190px; padding:18px 20px; }
    }
  </style>
</head>
<body>
  <div class="container">

    <div class="header">
      <h1>COST OF WAITING COUNTER</h1>
      <div class="subtitle">A modeled estimate of preventable loss during avoidable delay</div>
      <div class="tagline">
        This page does not record individual deaths in real time. It is a time-based counter derived from a fixed start date and a configurable daily rate.
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
      <div class="clock-title">MODELED PREVENTABLE LOSS SINCE CTMP READINESS DATE</div>
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
          A <span class="emph">modeled counter</span> that converts time elapsed since a fixed reference date into a running estimate using a configured daily rate.
        </p>
        <p>
          If you refresh the page, the displayed value updates only because time has advanced. It does not restart from zero.
        </p>
      </div>

      <div class="card">
        <h3>WHAT THIS IS NOT</h3>
        <p>
          It is <span class="emph">not</span> a live mortality feed. It does not claim a specific person died at a specific moment. It does not generate fabricated locations or causes.
        </p>
        <p>
          It is a clock that quantifies delay using a defined model, nothing more.
        </p>
      </div>

      <div class="card">
        <h3>MODEL ASSUMPTION</h3>
        <p>
          Daily rate used here: <span class="emph" id="rateInline">1,382</span> per day.
          Derived: <span class="emph" id="perMinute">0</span> per minute and <span class="emph" id="msPerOne">0</span> ms per 1.
        </p>
        <p>
          If you change the daily rate, all derived values update consistently.
        </p>
      </div>

      <div class="card">
        <h3>FRAMING</h3>
        <p class="emph">
          From this point on, delay is not confusion. It is consent.
        </p>
        <p>
          This page is intended to communicate the cost of delay in clear arithmetic, without pretending to be a real-time death tracker.
        </p>
      </div>

    </div>

    <div class="footer">
      <div class="statement">CTMP: Living proof that scarcity is a choice.</div>
      <div>
        Counter basis: fixed reference date + configured daily rate. This is a modeled estimate, not a real-time mortality registry.
      </div>
      <div>
        Suggested sources to document separately (if you publish a rate): WHO Global Health Estimates; UNICEF/WHO Joint Monitoring Programme; peer-reviewed health impact methodology.
      </div>
    </div>

  </div>

  <script>
    /***********************
     * CONFIG (EDIT HERE)
     ***********************/
    const REFERENCE_DATE_UTC = '2025-08-24T00:00:00Z'; // fixed start date in UTC
    const RATE_PER_DAY = 1382; // modeled preventable loss per day

    /***********************
     * DERIVED CONSTANTS
     ***********************/
    const MS_PER_DAY = 86400000;
    const referenceDate = new Date(REFERENCE_DATE_UTC);

    const ratePerHour = RATE_PER_DAY / 24;
    const ratePerMinute = RATE_PER_DAY / 1440;
    const msPerOne = MS_PER_DAY / RATE_PER_DAY;

    function fmt(n) { return Math.floor(n).toLocaleString(); }

    function utcStartOfToday(now) {
      return new Date(Date.UTC(now.getUTCFullYear(), now.getUTCMonth(), now.getUTCDate()));
    }

    function utcStartOfYear(now) {
      return new Date(Date.UTC(now.getUTCFullYear(), 0, 1));
    }

    function nonNegative(n) { return n < 0 ? 0 : n; }

    function totalSinceReference(nowMs) {
      const msSince = nowMs - referenceDate.getTime();
      const daysSince = msSince / MS_PER_DAY;
      return nonNegative(daysSince * RATE_PER_DAY);
    }

    function todayCount(now) {
      const start = utcStartOfToday(now);
      const ms = now.getTime() - start.getTime();
      return nonNegative((ms / MS_PER_DAY) * RATE_PER_DAY);
    }

    function yearCount(now) {
      const start = utcStartOfYear(now);
      const ms = now.getTime() - start.getTime();
      return nonNegative((ms / MS_PER_DAY) * RATE_PER_DAY);
    }

    function daysSinceReference(nowMs) {
      const msSince = nowMs - referenceDate.getTime();
      return nonNegative(Math.floor(msSince / MS_PER_DAY));
    }

    function bootLabels() {
      document.getElementById('refDateText').textContent = REFERENCE_DATE_UTC.slice(0,10);
      document.getElementById('ratePerDayText').textContent = RATE_PER_DAY.toLocaleString();

      const refPretty = referenceDate.toLocaleDateString('en-US', { year:'numeric', month:'long', day:'numeric', timeZone:'UTC' });
      document.getElementById('referenceLabel').textContent = refPretty;

      document.getElementById('rateInline').textContent = RATE_PER_DAY.toLocaleString();
      document.getElementById('perHour').textContent = fmt(ratePerHour);
      document.getElementById('perMinute').textContent = (ratePerMinute).toFixed(3);
      document.getElementById('msPerOne').textContent = Math.round(msPerOne).toLocaleString();
    }

    function tick() {
      const now = new Date();
      const nowMs = now.getTime();

      document.getElementById('totalCounter').textContent = fmt(totalSinceReference(nowMs));
      document.getElementById('todayCounter').textContent = fmt(todayCount(now));
      document.getElementById('yearCounter').textContent = fmt(yearCount(now));
      document.getElementById('daysDelayed').textContent = daysSinceReference(nowMs).toLocaleString();
    }

    bootLabels();
    tick();

    // Smooth enough without being wasteful
    setInterval(tick, 250);
  </script>
</body>
</html>
