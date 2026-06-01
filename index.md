<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2026 Match Planner</title>
    <style>
        /* 2002 Brazil Away Kit Inspired Palette: Royal Blue, Neon Yellow, White */
        :root {
            --brazil-blue: #0541a6;
            --brazil-yellow: #ccff00; 
            --bg-dark-blue: #032b70;
            --card-white: #ffffff;
            --text-dark: #111111;
        }

        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
            max-width: 600px; 
            margin: 0 auto; 
            padding: 15px; 
            background-color: var(--bg-dark-blue); 
            color: white;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 3px solid var(--brazil-yellow);
            padding-bottom: 10px;
            margin-bottom: 20px;
        }

        h2 { margin: 0; color: white; text-transform: uppercase; font-style: italic; font-size: 20px; }

        .lang-btn {
            background: transparent;
            border: 2px solid var(--brazil-yellow);
            color: var(--brazil-yellow);
            padding: 5px 12px;
            font-weight: bold;
            border-radius: 20px;
            cursor: pointer;
            transition: 0.2s;
        }
        .lang-btn:hover {
            background: var(--brazil-yellow);
            color: var(--bg-dark-blue);
        }

        .intro-text { color: #d0e0ff; font-size: 14px; margin-bottom: 20px; }

        .match-card { 
            background: var(--card-white); 
            color: var(--text-dark);
            padding: 15px; 
            margin: 12px 0; 
            border-radius: 10px; 
            display: flex; 
            align-items: center; 
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
            border-left: 6px solid var(--brazil-blue);
        }

        .match-card input[type="checkbox"] { 
            margin-right: 15px; 
            transform: scale(1.4); 
            cursor: pointer;
            accent-color: var(--brazil-blue);
        }

        .match-info { flex-grow: 1; }
        
        .teams { font-size: 18px; font-weight: bold; color: var(--brazil-blue); }
        
        .meta-data { 
            font-size: 13px; 
            color: #555; 
            margin-top: 4px;
            line-height: 1.4;
        }

        .badge-group {
            display: inline-block;
            background: #e1ecf4;
            color: #032b70;
            padding: 2px 6px;
            border-radius: 4px;
            font-size: 11px;
            font-weight: bold;
        }

        button.action-btn { 
            background: var(--brazil-yellow); 
            color: var(--bg-dark-blue); 
            border: none; 
            padding: 15px 20px; 
            font-size: 16px; 
            font-weight: bold;
            border-radius: 8px; 
            cursor: pointer; 
            width: 100%; 
            margin-top: 20px; 
            box-shadow: 0 4px 6px rgba(0,0,0,0.2);
            text-transform: uppercase;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        button.action-btn:hover { opacity: 0.9; }
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
        <button class="action-btn" onclick="shareOnWhatsApp()" id="shareBtn">
            🟢 Share on WhatsApp
        </button>
    </div>

    <script>
        // ⚠️ CUSTOM CONFIGURATIONS
        const API_URL = "YOUR_APPS_SCRIPT_URL_HERE"; 
        const GITHUB_PAGES_URL = "YOUR_GITHUB_PAGES_URL_HERE"; 

        let allMatches = [];
        let currentLang = 'en'; 

        const dictionary = {
            en: {
                title: "🏆 2026 Match Planner",
                editIntro: "Select the matches you plan to watch, then share the schedule with your friends on WhatsApp.",
                loading: "⚽ Loading schedule...",
                alertSelect: "Please select at least one match first!",
                wpGreeting: "Hello! Let's watch these matches?\n",
                wpFooter: "\nPlan yours here: "
            },
            pt: {
                title: "🏆 Agenda Copa 2026",
                editIntro: "Selecione os jogos que você quer assistir e envie a lista organizada para seus amigos no WhatsApp.",
                loading: "⚽ Carregando jogos...",
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
                document.getElementById('matchList').innerText = "Error loading schedule data.";
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
            document.getElementById('shareBtn').innerText = currentLang === 'en' ? "🟢 Share on WhatsApp" : "🟢 Compartilhar no WhatsApp";
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
                                📅 <strong>${timeData.weekday}</strong>, ${timeData.localDate}<br>
                                ⏰ ${timeData.localTime} | 📍 ${m.stadium} <span class="badge-group">${m.group}</span>
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

            // Start parsing message string
            let message = dictionary[currentLang].wpGreeting;

            checkboxes.forEach(cb => {
                const matchId = cb.value;
                const match = allMatches.find(m => String(m.id) === String(matchId));
                if (match) {
                    const home = currentLang === 'en' ? match.team1_en : match.team1_pt;
                    const away = currentLang === 'en' ? match.team2_en : match.team2_pt;
                    const timeData = getLocalTimeData(match.datetime_utc);
                    
                    // Format row text
                    message += `• ${timeData.weekday}, ${timeData.localDate} @ ${timeData.localTime} - ${home} vs ${away}\n`;
                }
            });

            message += dictionary[currentLang].wpFooter + GITHUB_PAGES_URL;

            // URL Encode text string safely and execute redirect
            const encodedMessage = encodeURIComponent(message);
            const whatsappUrl = `https://api.whatsapp.com/send?text=${encodedMessage}`;
            
            window.open(whatsappUrl, '_blank');
        }

        window.onload = init;
    </script>
</body>
</html>
