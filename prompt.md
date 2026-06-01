Act as an expert full-stack developer and UI designer. Help me build a Minimum Viable Product (MVP) for a 2026 World Cup Match Planner app. The objective is to make it easy for users to pick the matches they want to watch and instantly share the actual list of games with friends directly via WhatsApp as a clean text message.

The app must be 100% free to run, lightweight, and buildable using only Google Sheets (Database), Google Apps Script (API), and GitHub Pages (Frontend Hosting). It must not require user accounts, logins, or authentication.

Please provide the step-by-step implementation guide and full production-ready code based on these exact specifications:

### 1. Database Layout (Google Sheets)
The Google Sheet tab must be named "Matches". It needs to process dates and times using UTC ISO format so that the frontend can automatically shift kickoff times to the reader's local device time (e.g., displaying the correct relative time for the user).
Columns:
- ID (Number)
- DateTime_UTC (ISO String format: YYYY-MM-DDTHH:MM:SSZ)
- Stadium (Text)
- Team1_EN (Text)
- Team1_PT (Text)
- Team2_EN (Text)
- Team2_PT (Text)
- Group (Text)

### 2. Backend API (Google Apps Script)
Provide a `doGet()` script that reads the Google Sheet data, maps the columns into a clean JSON array of objects, and returns it with the correct JSON MIME type so the frontend can safely fetch it.

### 3. Frontend UI & The WhatsApp Sharing Feature (Single index.html)
Provide a complete, self-contained `index.html` file that includes CSS styling and JavaScript. 
- The app will load all matches from the API chronologically.
- Users can check boxes next to the games they want to watch.
- There must be a prominent "Share on WhatsApp" action button. 
- When clicked, JavaScript must loop through the checked matches, format them into a clean, readable text message, and open a WhatsApp API link (`https://api.whatsapp.com/send?text=...`).

The pre-formatted WhatsApp message must look exactly like this:
"Hello! Let's watch these matches?
• [Weekday], [Date] at [Time] - [Team 1] vs [Team 2]
• [Weekday], [Date] at [Time] - [Team 1] vs [Team 2]

Plan yours here: [Your GitHub Pages URL]"

### 4. Visual Design & Branding
The UI must be heavily inspired by the iconic 2002 Brazil World Cup away kit (the royal blue shirt). 
- Primary Background: Deep, rich sport/navy blue.
- Content Cards: Crisp white background with dark readable text, sharp edges, and a thick royal blue left border.
- Accents & Call-to-Actions: Luminous neon-yellow/green color for primary buttons, highlights, and borders.
- Typography: Modern, clean, sans-serif font family with stylized uppercase headers to give it a premium sports-app feel.

### 5. Localization & Time Mechanics (EN / PT-BR)
- Include a fixed language toggle button at the top right of the screen ("PT 🇧🇷" / "EN 🇺🇸"). Clicking it must instantly translate all UI text, card metadata, team names, and the final generated WhatsApp text message without reloading the page.
- The JavaScript must parse the `DateTime_UTC` field from the Google Sheet and automatically convert it using the browser's native locale settings so the user sees and shares the matches in their exact local phone time.
- Each match card on the site must explicitly display: The correct localized Day of the Week (e.g., "Monday" or "Segunda-feira"), the localized date, the localized 24-hour kickoff time, the stadium name, and the group badge.

Please output the steps clearly, ensuring there are clear placeholders in the HTML where I need to paste my live Google Apps Script Web App URL and my GitHub Pages URL.
