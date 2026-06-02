# 🌍 2026 Match Planner - Prompt Master (Serverless Stack)

This file contains the perfect engineering prompts to replicate the "2026 World Cup Match Planner" project in both Portuguese and English.

---

## 🇧🇷 Versão em Português

Atue como um desenvolvedor Full-Stack sênior e UI/UX Designer especialista. Preciso construir um MVP para um aplicativo "Match Planner da Copa do Mundo 2026". O objetivo é permitir que os usuários escolham seus times ou jogadores favoritos através de uma busca unificada e gerem instantaneamente uma lista de jogos formatada para compartilhar com os amigos diretamente pelo WhatsApp.

O app deve ser 100% gratuito para rodar, leve e serverless, utilizando apenas Google Sheets (Banco de dados), Google Apps Script (API/Backend) e GitHub Pages (Hospedagem estática do Frontend). Não deve exigir login, autenticação ou criação de contas de usuário.

Forneça o código pronto para produção seguindo estas especificações exatas:

### 1. Estrutura do Banco de Dados (Google Sheets)
O arquivo deve conter uma aba chamada "app". As colunas obrigatórias são:
- ID (Número)
- DateTime_UTC (String no formato ISO 8601: YYYY-MM-DDTHH:MM:SSZ)
- Stadium (Texto)
- Team1_EN / Team1_PT (Texto)
- Team2_EN / Team2_PT (Texto)
- Group (Texto)
- has_player (Número: 0 ou 1)
- filter_especial (Texto: nome de um jogador estrela caso has_player = 1)

### 2. API Backend (Google Apps Script)
Forneça um script `doGet()` robusto que leia a aba "app", limpe strings contra espaços extras, trate valores nulos, converta datas em strings ISO padronizadas e retorne um array JSON com os cabeçalhos CORS corretos.

### 3. Interface do Usuário (Single index.html com JS e CSS)
A experiência deve ser dividida em duas telas consecutivas dentro de um único arquivo:

- **Tela 1 (Filtros Preferenciais):** Apresenta uma grade unificada contendo exatamente 18 opções fixas de cartões (Países principais e nomes das estrelas da coluna 'filter_especial'). O usuário clica para selecionar (múltipla escolha livre). Um segundo clique no mesmo cartão o desmarca. O botão inferior "partidas" inicia desabilitado e só deve ser ativado se houver pelo menos uma opção selecionada.
- **Tela 2 (Seleção de Jogos):** Ao avançar, o JavaScript faz uma busca cruzada inteligente baseada na seleção. Se o usuário escolheu uma estrela (ex: "HAALAND"), o sistema filtra as partidas onde o valor consta na coluna 'filter_especial'. Se escolheu um país (ex: "BRASIL"), o sistema filtra pelas colunas de times. Os jogos correspondentes são listados em formato de cards contendo checkbox para a seleção final dos jogos.

### 4. Design Visual e Layout Moderno
- O layout deve ser inspirado nas cores do uniforme reserva do Brasil na Copa de 2002 (Base em Azul Marinho profundo/Gradient e detalhes em Amarelo/Verde limão neon para botões e estados ativos).
- Os cards de jogos e botões devem possuir bordas arredondadas modernas (`border-radius: 12px`) e sombras suaves.
- A tipografia deve ser limpa (Inter), removendo excessos de negrito. Use pesos leves para metadados e destaque em negrito apenas para os nomes dos times.
- Os cards na Tela 2 devem exibir o dia da semana abreviado, data e o horário local convertido.

### 5. Mecânica de Fuso Horário e Idioma
- Inclua um botão de alternância de idioma no topo ("PT 🇧🇷" / "EN 🇺🇸"). Mudar o idioma deve traduzir instantaneamente os botões de países e metadados da interface sem dar refresh na página.
- O JavaScript deve capturar a data UTC do Sheets e convertê-la nativamente para o fuso horário e horário local do dispositivo do usuário que abrir o site.

### 6. Formatação do WhatsApp
Ao clicar em "enviar por whatsapp", o JS gera um link da API do WhatsApp contendo os jogos selecionados organizados exatamente com esta estrutura de quebras e emojis:

"Olá! Vamos assistir a esses jogos?
📅 [Dia da Semana], [Data Local] - [Horário Local]
⚽ [Time 1] × [Time 2]

Monte a sua programação aqui: https://pages.github.com/"

---

## 🇺🇸 English Version

Act as a Senior Full-Stack Developer and Expert UI/UX Designer. I need to build an MVP for a "2026 World Cup Match Planner" web app. The goal is to allow users to pick their favorite teams or players through a single unified screen and instantly generate a beautiful text schedule to share with friends directly via WhatsApp.

The app must be 100% free to run, lightweight, and serverless, built entirely using Google Sheets (Database), Google Apps Script (API/Backend), and GitHub Pages (Static Frontend Hosting). It must not require logins, authentication, or user accounts.

Please provide the production-ready code based on these exact specifications:

### 1. Database Layout (Google Sheets)
The sheet must have a tab named exactly "app". Required columns:
- ID (Number)
- DateTime_UTC (ISO 8601 String format: YYYY-MM-DDTHH:MM:SSZ)
- Stadium (Text)
- Team1_EN / Team1_PT (Text)
- Team2_EN / Team2_PT (Text)
- Group (Text)
- has_player (Number: 0 or 1)
- filter_especial (Text: star player's name if has_player = 1)

### 2. Backend API (Google Apps Script)
Provide a clean `doGet()` script that reads the "app" tab, trims whitespace, handles null values safely, converts native dates to standardized ISO strings, and returns a clean JSON array with proper CORS headers.

### 3. Frontend UI (Single index.html with JS and CSS)
The user experience must be split into two sequential screens within a single self-contained file:

- **Screen 1 (Preferences Filter):** Displays a single unified grid containing exactly 18 fixed preference cards (Top countries and star player names from the 'filter_especial' column). Users can multi-select freely. Clicking an active card deselects it. The bottom action button ("view matches") must start disabled and only enable when at least one card is selected.
- **Screen 2 (Match Selection):** When advancing, JavaScript runs a cross-reference search. If a user picked a player (e.g., "HAALAND"), it filters rows matching the 'filter_especial' column. If they picked a country (e.g., "BRAZIL"), it filters matching team columns. The corresponding games are listed as sleek cards with checkboxes for the final schedule selection.

### 4. Visual Design & Modern Layout
- The styling must be heavily inspired by the iconic 2002 Brazil World Cup away kit (Deep navy blue background gradient with luminous neon yellow/green accents for primary actions and active states).
- All buttons and match cards must feature smooth modern rounded corners (`border-radius: 12px`) and soft drop shadows.
- Typography must use a modern sans-serif font (Inter), avoiding an overly bold or blocky look. Use regular font weights for metadata (stadium, date) and keep bold weights strictly for team names.
- Match cards on Screen 2 must clearly display the abbreviated weekday, local date, and converted local kickoff time.

### 5. Localization & Timezone Mechanics
- Include a fixed language toggle at the top right ("PT 🇧🇷" / "EN 🇺🇸"). Clicking it must instantly translate country button names and UI text without refreshing the page.
- JavaScript must parse the UTC timestamp from the database and automatically convert it using the browser's native locale settings so that the user sees and shares the exact kickoff time for their specific device timezone.

### 6. WhatsApp Formatting
Clicking the share action button must open a WhatsApp API link with the checked matches formatted exactly like this with emojis and clean line breaks:

"Hello! Let's watch these matches?
📅 [Weekday], [Local Date] - [Local Time]
⚽ [Team 1] × [Team 2]

Plan yours here: [GitHub Pages URL]"
