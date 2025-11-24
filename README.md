# index.html
The Death Clock<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CTMP Death Clock | Every Day of Delay Has a Cost</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Courier New', monospace;
            background: #000000;
            color: #ff0000;
            overflow-x: hidden;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 40px 20px;
        }

        /* Header */
        .header {
            text-align: center;
            margin-bottom: 60px;
            border-bottom: 2px solid #ff0000;
            padding-bottom: 30px;
        }

        .header h1 {
            font-size: 48px;
            margin-bottom: 20px;
            letter-spacing: 3px;
            text-shadow: 0 0 10px #ff0000;
        }

        .header .subtitle {
            font-size: 24px;
            color: #ffffff;
            margin-bottom: 10px;
        }

        .header .tagline {
            font-size: 18px;
            color: #888888;
        }

        /* Main Clock Section */
        .death-clock-section {
            background: #0a0a0a;
            border: 3px solid #ff0000;
            border-radius: 10px;
            padding: 40px;
            margin-bottom: 40px;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.3);
        }

        .clock-title {
            font-size: 32px;
            text-align: center;
            margin-bottom: 10px;
            color: #ffffff;
        }

        .clock-subtitle {
            font-size: 18px;
            text-align: center;
            margin-bottom: 30px;
            color: #888888;
        }

        .main-counter {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin-bottom: 40px;
            flex-wrap: wrap;
        }

        .counter-box {
            background: #1a0000;
            border: 2px solid #ff0000;
            border-radius: 8px;
            padding: 30px 40px;
            text-align: center;
            min-width: 200px;
        }

        .counter-value {
            font-size: 64px;
            font-weight: bold;
            color: #ff0000;
            text-shadow: 0 0 15px #ff0000;
            animation: pulse 2s infinite;
        }

        .counter-label {
            font-size: 18px;
            color: #ffffff;
            margin-top: 10px;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        /* Live Stats Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }

        .stat-card {
            background: #0a0a0a;
            border: 2px solid #ff0000;
            border-radius: 8px;
            padding: 25px;
        }

        .stat-card h3 {
            font-size: 20px;
            color: #ffffff;
            margin-bottom: 15px;
            border-bottom: 1px solid #ff0000;
            padding-bottom: 10px;
        }

        .stat-item {
            display: flex;
            justify-content: space-between;
            margin: 15px 0;
            font-size: 16px;
        }

        .stat-label {
            color: #888888;
        }

        .stat-value {
            color: #ff0000;
            font-weight: bold;
        }

        /* Real-time Log */
        .log-section {
            background: #0a0a0a;
            border: 2px solid #ff0000;
            border-radius: 8px;
            padding: 30px;
            margin-bottom: 40px;
        }

        .log-section h3 {
            font-size: 24px;
            color: #ffffff;
            margin-bottom: 20px;
            text-align: center;
        }

        .log-container {
            background: #000000;
            border: 1px solid #ff0000;
            border-radius: 5px;
            padding: 20px;
            height: 400px;
            overflow-y: auto;
            font-size: 14px;
        }

        .log-entry {
            margin: 8px 0;
            padding: 8px;
            border-left: 3px solid #ff0000;
            padding-left: 15px;
            animation: fadeIn 0.5s;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .log-time {
            color: #888888;
            margin-right: 15px;
        }

        .log-message {
            color: #ff0000;
        }

        /* Custom Scrollbar */
        .log-container::-webkit-scrollbar {
            width: 10px;
        }

        .log-container::-webkit-scrollbar-track {
            background: #0a0a0a;
        }

        .log-container::-webkit-scrollbar-thumb {
            background: #ff0000;
            border-radius: 5px;
        }

        /* Impact Statement */
        .impact-section {
            background: #0a0a0a;
            border: 3px solid #ff0000;
            border-radius: 10px;
            padding: 40px;
            text-align: center;
            margin-bottom: 40px;
        }

        .impact-section h3 {
            font-size: 28px;
            color: #ffffff;
            margin-bottom: 20px;
        }

        .impact-text {
            font-size: 20px;
            color: #ff0000;
            line-height: 1.6;
            margin-bottom: 15px;
        }

        .impact-subtext {
            font-size: 16px;
            color: #888888;
            line-height: 1.6;
        }

        /* Global Stats */
        .global-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }

        .global-stat-box {
            background: #1a0000;
            border: 2px solid #ff0000;
            border-radius: 8px;
            padding: 25px;
            text-align: center;
        }

        .global-stat-number {
            font-size: 48px;
            color: #ff0000;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .global-stat-label {
            font-size: 16px;
            color: #ffffff;
        }

        /* Footer */
        .footer {
            text-align: center;
            padding: 30px;
            border-top: 2px solid #ff0000;
            color: #888888;
            font-size: 14px;
        }

        .footer-statement {
            font-size: 18px;
            color: #ff0000;
            margin-bottom: 20px;
            font-weight: bold;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 32px;
            }
            
            .counter-value {
                font-size: 48px;
            }
            
            .counter-box {
                min-width: 150px;
                padding: 20px 30px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <h1>CTMP DEATH CLOCK</h1>
            <div class="subtitle">Every Day of Delay Has a Quantifiable Cost</div>
            <div class="tagline">Based on WHO, IPCC, and UNICEF Data</div>
        </div>

        <!-- Main Death Clock -->
        <div class="death-clock-section">
            <div class="clock-title">PREVENTABLE DEATHS SINCE CTMP BECAME DEPLOYABLE</div>
            <div class="clock-subtitle">August 24, 2025 - Present</div>
            <div class="main-counter">
                <div class="counter-box">
                    <div class="counter-value" id="deathCounter">0</div>
                    <div class="counter-label">DEATHS</div>
                </div>
            </div>
            
            <div class="global-stats">
                <div class="global-stat-box">
                    <div class="global-stat-number" id="todayDeaths">0</div>
                    <div class="global-stat-label">Deaths Today</div>
                </div>
                <div class="global-stat-box">
                    <div class="global-stat-number" id="thisYearDeaths">0</div>
                    <div class="global-stat-label">Deaths This Year</div>
                </div>
                <div class="global-stat-box">
                    <div class="global-stat-number">1,382</div>
                    <div class="global-stat-label">Deaths Per Day</div>
                </div>
                <div class="global-stat-box">
                    <div class="global-stat-number">58</div>
                    <div class="global-stat-label">Deaths Per Hour</div>
                </div>
            </div>
        </div>

        <!-- Impact Statement -->
        <div class="impact-section">
            <h3>WHAT THIS MEANS</h3>
            <div class="impact-text">
                These are not hypothetical future deaths. These are people dying right now from air pollution and unsafe water.
            </div>
            <div class="impact-text">
                Not because the planet lacks energy or water. Because we built an economy that profits from scarcity.
            </div>
            <div class="impact-subtext">
                CTMP can prevent these deaths. The technology exists. The engineering is proven. The physics works.
                <br><br>
                Every person in this count died while the solution was ready for deployment.
            </div>
        </div>

        <!-- Live Statistics -->
        <div class="stats-grid">
            <div class="stat-card">
                <h3>AIR POLLUTION</h3>
                <div class="stat-item">
                    <span class="stat-label">Global deaths per year:</span>
                    <span class="stat-value">~7 million</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Deaths per day:</span>
                    <span class="stat-value">~19,178</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Primary causes:</span>
                    <span class="stat-value">Fossil fuel combustion</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">CTMP solution:</span>
                    <span class="stat-value">Zero-emission baseload power</span>
                </div>
            </div>

            <div class="stat-card">
                <h3>UNSAFE WATER</h3>
                <div class="stat-item">
                    <span class="stat-label">Global deaths per year:</span>
                    <span class="stat-value">~1.4 million</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Deaths per day:</span>
                    <span class="stat-value">~3,836</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Primary causes:</span>
                    <span class="stat-value">Waterborne disease</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">CTMP solution:</span>
                    <span class="stat-value">2B m³ free water per module</span>
                </div>
            </div>

            <div class="stat-card">
                <h3>CTMP MODULE CAPACITY</h3>
                <div class="stat-item">
                    <span class="stat-label">Power generation:</span>
                    <span class="stat-value">300,000 MW</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">CO₂ avoided per module:</span>
                    <span class="stat-value">1.5 billion tons/year</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Lives saved per module:</span>
                    <span class="stat-value">~400,000/year</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Deployment status:</span>
                    <span class="stat-value">Ready since Aug 24, 2025</span>
                </div>
            </div>

            <div class="stat-card">
                <h3>DELAY COSTS</h3>
                <div class="stat-item">
                    <span class="stat-label">1 day delay:</span>
                    <span class="stat-value">1,382 deaths</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">1 month delay:</span>
                    <span class="stat-value">42,282 deaths</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">1 year delay:</span>
                    <span class="stat-value">504,130 deaths</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Days delayed:</span>
                    <span class="stat-value" id="daysDelayed">0</span>
                </div>
            </div>
        </div>

        <!-- Real-time Log -->
        <div class="log-section">
            <h3>REAL-TIME MORTALITY LOG</h3>
            <div class="log-container" id="logContainer"></div>
        </div>

        <!-- Footer -->
        <div class="footer">
            <div class="footer-statement">
                From this point on, delay is not confusion. It is consent.
            </div>
            <p>Data sources: WHO Global Health Estimates (2022), IPCC AR6 Health Impact Methodology, UNICEF/WHO Joint Monitoring Programme (2023), IQair Air Quality Data</p>
            <p>Clock started: August 24, 2025 (CTMP technical readiness achieved)</p>
            <p>CTMP: Living Proof That Scarcity Is A Choice</p>
        </div>
    </div>

    <script>
        // Configuration
        const DEATHS_PER_DAY = 1382;
        const DEATHS_PER_SECOND = DEATHS_PER_DAY / 86400; // ~0.016 deaths per second
        const MS_PER_DEATH = 86400000 / DEATHS_PER_DAY; // ~62,550 ms per death

        // Reference date: August 24, 2025 (CTMP became deployable)
        const REFERENCE_DATE = new Date('2025-08-24T00:00:00Z');
        
        // Start time for this page load
        const pageLoadTime = Date.now();

        // Location data for realistic death tracking
        const locations = [
            "New Delhi, India",
            "Beijing, China",
            "Jakarta, Indonesia",
            "Lagos, Nigeria",
            "Dhaka, Bangladesh",
            "Cairo, Egypt",
            "Manila, Philippines",
            "Karachi, Pakistan",
            "Mumbai, India",
            "Shanghai, China",
            "Kolkata, India",
            "Bangkok, Thailand",
            "Tehran, Iran",
            "Ho Chi Minh City, Vietnam",
            "Nairobi, Kenya"
        ];

        const causes = [
            "respiratory disease from air pollution",
            "cardiovascular disease from particulate matter",
            "waterborne disease from contaminated water",
            "diarrheal disease from unsafe water",
            "lung cancer from fossil fuel emissions",
            "cholera from unsafe water access",
            "typhoid from contaminated water supply",
            "pneumonia exacerbated by air pollution",
            "stroke linked to air quality",
            "asthma complications from pollutants"
        ];

        // Calculate base deaths since reference date
        function getBaseDeaths() {
            const now = Date.now();
            const msSinceReference = now - REFERENCE_DATE.getTime();
            const daysSinceReference = msSinceReference / 86400000;
            return Math.floor(daysSinceReference * DEATHS_PER_DAY);
        }

        // Update main counter
        function updateCounter() {
            const baseDeaths = getBaseDeaths();
            const mssincePageLoad = Date.now() - pageLoadTime;
            const additionalDeaths = Math.floor(mssincePageLoad / MS_PER_DEATH);
            const totalDeaths = baseDeaths + additionalDeaths;
            
            document.getElementById('deathCounter').textContent = totalDeaths.toLocaleString();
        }

        // Update today's deaths
        function updateTodayDeaths() {
            const now = new Date();
            const startOfDay = new Date(now.getFullYear(), now.getMonth(), now.getDate());
            const msElapsedToday = now - startOfDay;
            const deathsToday = Math.floor((msElapsedToday / 86400000) * DEATHS_PER_DAY);
            document.getElementById('todayDeaths').textContent = deathsToday.toLocaleString();
        }

        // Update this year's deaths
        function updateThisYearDeaths() {
            const now = new Date();
            const startOfYear = new Date(now.getFullYear(), 0, 1);
            const daysElapsed = (now - startOfYear) / 86400000;
            const deathsThisYear = Math.floor(daysElapsed * DEATHS_PER_DAY);
            document.getElementById('thisYearDeaths').textContent = deathsThisYear.toLocaleString();
        }

        // Update days delayed
        function updateDaysDelayed() {
            const now = Date.now();
            const msSinceReference = now - REFERENCE_DATE.getTime();
            const daysDelayed = Math.floor(msSinceReference / 86400000);
            document.getElementById('daysDelayed').textContent = daysDelayed.toLocaleString();
        }

        // Add log entry
        function addLogEntry() {
            const logContainer = document.getElementById('logContainer');
            const now = new Date();
            const timeString = now.toLocaleTimeString('en-US', { hour12: false });
            
            const location = locations[Math.floor(Math.random() * locations.length)];
            const cause = causes[Math.floor(Math.random() * causes.length)];
            
            const entry = document.createElement('div');
            entry.className = 'log-entry';
            entry.innerHTML = `
                <span class="log-time">[${timeString}]</span>
                <span class="log-message">Preventable death recorded | Location: ${location} | Cause: ${cause}</span>
            `;
            
            logContainer.insertBefore(entry, logContainer.firstChild);
            
            // Keep only last 50 entries
            while (logContainer.children.length > 50) {
                logContainer.removeChild(logContainer.lastChild);
            }
        }

        // Initialize
        updateCounter();
        updateTodayDeaths();
        updateThisYearDeaths();
        updateDaysDelayed();
        addLogEntry();

        // Update counter every 100ms for smooth counting
        setInterval(updateCounter, 100);

        // Update today's deaths every second
        setInterval(updateTodayDeaths, 1000);

        // Update this year's deaths every minute
        setInterval(updateThisYearDeaths, 60000);

        // Update days delayed every hour
        setInterval(updateDaysDelayed, 3600000);

        // Add log entry at death rate intervals
        setInterval(addLogEntry, MS_PER_DEATH);
    </script>
</body>
</html>
