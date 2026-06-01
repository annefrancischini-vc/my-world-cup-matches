<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2026 Match Planner</title>
    <style>
        /* Modern 2026 Premium Sports UI Palette */
        :root {
            --brazil-blue-glow: #0a58ca;
            --neon-lime: #ccff00; 
            --bg-gradient: linear-gradient(135deg, #020b18 0%, #051d3b 100%);
            --glass-card: rgba(255, 255, 255, 0.06);
            --glass-border: rgba(255, 255, 255, 0.1);
            --text-primary: #ffffff;
            --text-secondary: #a0aec0;
        }

        body { 
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            max-width: 500px; 
            margin: 0 auto; 
            padding: 20px 16px; 
            background: var(--bg-gradient);
            background-attachment: fixed;
            color: var(--text-primary);
            -webkit-font-smoothing: antialiased;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 16px;
            margin-bottom: 24px;
            border-bottom: 1px solid var(--glass-border);
        }

        h2 { 
            margin: 0; 
            font-size: 22px; 
            font-weight: 800;
            letter-spacing: -0.5px;
            background: linear-gradient(90deg, #ffffff, var(--neon-lime));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .lang-btn {
            background: rgba(255, 255, 255, 0.08);
            border: 1px solid var(--glass-border);
            color: var(--text-primary);
            padding: 6px 14px;
            font-size: 13px;
            font-weight: 600;
            border-radius: 99px;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .lang-btn:hover {
            background: var(--neon-lime);
            color: #020b18;
            border-color: var(--neon-lime);
        }

        .intro-text { 
            color: var(--text-secondary); 
            font-size: 14px; 
            line-height: 1.5;
            margin-bottom: 24px; 
        }

        #matchList {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 90px; /* Space for the fixed bottom floating button */
        }

        .match-card { 
            background: var(--glass-card);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            padding: 16px; 
            border-radius: 16px; 
            display: flex; 
            align-items: center; 
            border: 1px solid var(--glass-border);
            transition: transform 0.2s ease, border-color 0.2s ease;
        }

        .match-card:style-within, .match-card:hover {
            border-color: rgba(10, 88, 202, 0.5);
        }

        /* Custom Modern Checkbox styling */
        .match-card input[type="checkbox"] { 
            margin-right: 16px; 
            width: 22px;
            height: 22px;
            border-radius: 6px;
            cursor: pointer;
            accent-color: var(--neon-lime);
        }

        .match-info { flex-grow: 1; }
        
        .teams { 
            font-size: 16px; 
            font-weight: 700; 
            color: var(--text-primary);
            margin-bottom: 6px;
        }
        
        .meta-data { 
            font-size: 12px; 
            color: var(--text-secondary);
            line-height: 1.6;
            display: flex;
            flex-direction: column;
            gap: 2px;
        }

        .meta-row {
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .badge-group {
            align-self: flex-start;
            background: rgba(10, 88, 202, 0.2);
            color: #79a6ff;
            padding: 2px 8px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 700;
            margin-top: 4px;
            border: 1px solid rgba(10, 88, 202, 0.3);
        }

        /* Fixed modern floating WhatsApp CTA button */
        .action-btn-container {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(transparent, #020b18 30%);
            padding: 24px 16px;
            display: flex;
            justify-content: center;
            max-width: 500px;
            margin: 0 auto;
            box-sizing: border-box;
            z-index: 100;
        }

        button.action-btn { 
            background: #25D366; /* Official WhatsApp Green */
            color: white; 
            border: none; 
            padding: 14px 28px; 
            font-size: 16px; 
            font-weight: 700;
            border-radius: 99px; 
            cursor: pointer; 
            width: 100%; 
            box-shadow: 0 8px 24px rgba(37, 211, 102, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }
        button.action-btn:hover { 
            transform: translateY(-2px);
            box-shadow: 0 12px 28px rgba(37, 211, 102, 0.4);
        }
        button.action-btn img {
            width: 22px;
            height: 22px;
        }
    </style>
</head>
<body>

    <header>
        <h2 id="appTitle">🏆 2026 Match Planner</h2>
        <button class="lang-btn" onclick="toggleLanguage()" id="langBtn">PT 🇧🇷</button>
    </header>

    <div id="mainContainer">
        <p class="intro-text" id="editIntro">Select the matches you plan to watch, then share the schedule with your friends on WhatsApp.</p>
        <div id="matchList">⚽ Loading schedule...</div>
    </div>

    <div class="action-btn-container">
        <button class="action-btn" onclick="shareOnWhatsApp()" id="shareBtn">
            <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" alt="WhatsApp">
            <span id="btnText">Share on WhatsApp</span>
        </button>
    </div>

    <script>
        // ⚠️ CUSTOM CONFIGURATIONS (Update these!)
        const API_URL = "YOUR_APPS_SCRIPT_URL_HERE"; 
        const GITHUB_PAGES_URL = "YOUR_GITHUB_PAGES_URL_HERE"; 

        let allMatches = [];
        let currentLang = 'en'; 

        const dictionary = {
            en: {
                title: "🏆 2026 Match Planner",
                editIntro: "Select the matches you plan to watch, then share the schedule with your friends on WhatsApp.",
                loading: "⚽ Loading schedule...",
                btnText: "Share on WhatsApp",
                alertSelect: "Please select at least one match first!",
                wpGreeting: "Hello! Let's watch these matches?\n",
                wpFooter: "\nPlan yours here: "
            },
            pt: {
                title: "🏆 Agenda Copa 2026",
                editIntro: "Selecione os jogos que você quer assistir e envie a lista organizada para seus amigos no WhatsApp.",
                loading: "⚽ Carregando jogos...",
                btnText: "Compartilhar no WhatsApp",
                alertSelect: "Por favor, selecione pelo menos um jogo!",
                wpGreeting: "Olá! Bora assistir a esses jogos?\n",
                wpFooter: "\nMonte sua agenda aqui: "
            }
        };

        const weekdays = {
            en: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
            pt: ["Domingo", "Segunda-feira", "Terça-feira", "Quarta-feira", "Quinta-feira", "Sexta-feira", "Sábado"]
        };

        async function init() {
            updateUI();
            try {
                const response = await fetch(API_URL);
                allMatches = await response.json();
                renderSchedule();
            } catch (error) {
                document.getElementById('matchList').innerHTML = `<div style="color:#ff4a4a; text-align:center; padding: 20px;">⚠️ Error loading schedule data. Check your Google Script configuration.</div>`;
                console.error(error);
            }
        }

        function toggleLanguage() {
            currentLang = currentLang === 'en' ? 'pt' : 'en';
            document.getElementById('langBtn').innerText = currentLang === 'en' ? "PT 🇧🇷" : "EN 🇺🇸";
            updateUI();
            renderSchedule();
        }

        function updateUI() {
            document.getElementById('appTitle').innerText = dictionary[currentLang].title;
            document.getElementById('editIntro').innerText = dictionary[currentLang].editIntro;
            document.getElementById('btnText').innerText = dictionary[currentLang].btnText;
        }

        function getLocalTimeData(isoString) {
            const dateObj = new Date(isoString);
            const weekday = weekdays[currentLang][dateObj.getDay()];
            const localDate = dateObj.toLocaleDateString(currentLang === 'en' ? 'en-US' : 'pt-BR', {
                month: 'numeric', day: 'numeric', year: 'numeric'
            });
            const localTime = dateObj.toLocaleTimeString([], {
                hour: '2-digit', minute: '2-digit', hour12: false
            });
            return { weekday, localDate, localTime };
        }

        function renderSchedule() {
            let html = '';
            allMatches.forEach(m => {
                const home = currentLang === 'en' ? m.team1_en : m.team1_pt;
                const away = currentLang === 'en' ? m.team2_en : m.team2_pt;
                const timeData = getLocalTimeData(m.datetime_utc);

                html += `
                    <div class="match-card">
                        <input type="checkbox" value="${m.id}" class="match-cb" id="match-${m.id}">
                        <div class="match-info">
                            <div class="teams">${home} × ${away}</div>
                            <div class="meta-data">
                                <div class="meta-row">📅 <strong>${timeData.weekday}</strong>, ${timeData.localDate}</div>
                                <div class="meta-row">⏰ ${timeData.localTime} | 📍 ${m.stadium}</div>
                                <span class="badge-group">${m.group}</span>
                            </div>
                        </div>
                    </div>`;
            });
            document.getElementById('matchList').innerHTML = html;
        }

        function shareOnWhatsApp() {
            const checkboxes = document.querySelectorAll('.match-cb:checked');
            if (checkboxes.length === 0) {
                alert(dictionary[currentLang].alertSelect);
                return;
            }

            let message = dictionary[currentLang].wpGreeting;

            checkboxes.forEach(cb => {
                const matchId = cb.value;
                const match = allMatches.find(m => String(m.id) === String(matchId));
                if (match) {
                    const home = currentLang === 'en' ? match.team1_en : match.team1_pt;
                    const away = currentLang === 'en' ? match.team2_en : match.team2_pt;
                    const timeData = getLocalTimeData(match.datetime_utc);
                    
                    message += `• ${timeData.weekday}, ${timeData.localDate} @ ${timeData.localTime} - ${home} vs ${away}\n`;
                }
            });

            message += dictionary[currentLang].wpFooter + GITHUB_PAGES_URL;

            const encodedMessage = encodeURIComponent(message);
            const whatsappUrl = `https://api.whatsapp.com/send?text=${encodedMessage}`;
            
            window.open(whatsappUrl, '_blank');
        }

        window.onload = init;
    </script>
</body>
</html>
