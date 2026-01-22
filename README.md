<div class="header">
  <h1>COST OF WAITING COUNTER</h1>
  <div class="subtitle">A modeled estimate of delay cost using a fixed start date and a stated daily rate</div>
  <div class="tagline">
    This page does not report real-time events or identify individuals. It displays a time-based estimate derived from a fixed start date and a configurable daily rate.
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
      A <span class="emph">modeled counter</span> that converts time elapsed since a fixed reference date into a running estimate using a configured daily rate.
    </p>
    <p>
      If you refresh the page, the displayed value updates only because time has advanced. It does not restart from zero.
    </p>
  </div>

  <div class="card">
    <h3>WHAT THIS IS NOT</h3>
    <p>
      It is <span class="emph">not</span> a live feed of incidents or outcomes. It does not report real-time events. It does not identify individuals. It does not claim “this happened at this moment.”
    </p>
    <p>
      It is a simple model: <span class="emph">elapsed time × stated rate</span>.
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
      This page is intended to communicate the cost of delay in clear arithmetic, without presenting itself as a live registry.
    </p>
  </div>

</div>

<div class="footer">
  <div class="statement">CTMP: Living proof that scarcity is a choice.</div>
  <div>
    Counter basis: fixed reference date + configured daily rate. This is a modeled estimate, not a real-time registry.
  </div>

  <div class="sources">
    <div class="sources-title"><strong>Sources</strong></div>
    <ul>
      <li>WHO Global Health Estimates (GHE): Mortality and global health estimates (downloads, 2000–2021). <a href="https://www.who.int/data/gho/data/themes/mortality-and-global-health-estimates" target="_blank" rel="noopener">WHO</a></li>
      <li>WHO GHE 2021 methods: “Methods and data sources for global burden of disease estimates 2000–2021” (technical methods PDF). <a href="https://cdn.who.int/media/docs/default-source/gho-documents/global-health-estimates/ghe2021_daly_methods.pdf" target="_blank" rel="noopener">WHO (PDF)</a></li>
      <li>WHO/UNICEF Joint Monitoring Programme (JMP): Global WASH data and reporting. <a href="https://washdata.org/" target="_blank" rel="noopener">JMP</a></li>
      <li>UN IGME: Levels and Trends in Child Mortality (latest annual estimates and report page). <a href="https://data.unicef.org/resources/levels-and-trends-in-child-mortality-2024/" target="_blank" rel="noopener">UNICEF Data</a></li>
      <li>Reporting standard for health estimates transparency: GATHER Statement (2016). <a href="https://www.healthdata.org/sites/default/files/files/GATHER-statement_2016.pdf" target="_blank" rel="noopener">GATHER (PDF)</a></li>
    </ul>
  </div>
</div>
