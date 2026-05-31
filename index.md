<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>My World Cup Games / Meus Jogos da Copa</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Ajuste fino para evitar que o clique selecione texto no mobile */
        .card-jogo {
            -webkit-tap-highlight-color: transparent;
        }

        /* Marca d'água do número 11 inspirada na tipografia da camisa de 2002 */
        .jersey-number {
            font-family: 'Impact', 'Arial Black', sans-serif;
            font-size: 24rem;
            line-height: 1;
            font-weight: 900;
            letter-spacing: -0.05em;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-900 min-h-screen">

    <div class="fixed inset-0 flex items-center justify-center pointer-events-none select-none z-0 overflow-hidden">
        <div class="jersey-number text-blue-600/[0.06] transform -rotate-6 select-none">11</div>
    </div>

    <header class="bg-blue-700 text-white shadow-lg sticky top-0 z-50 border-b-4 border-white">
        <div class="max-w-md mx-auto px-4 py-4 flex items-center justify-between">
            <div>
                <h1 id="txt-title" class="text-xl font-black tracking-wider uppercase">🗓️ Meus Jogos</h1>
                <p id="txt-subtitle" class="text-xs opacity-80 mt-0.5 font-medium">Monte suas partidas imperdíveis e compartilhe no WhatsApp</p>
            </div>
            
            <div class="relative inline-block text-left">
                <select id="select-lang" class="bg-white/10 text-white text-xs font-bold rounded-xl px-3 py-2 border border-white/20 focus:outline-none focus:ring-2 focus:ring-yellow-400 cursor-pointer appearance-none pr-7 bg-[url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23fbbf24%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%27style%3E')] bg-[length:8px_auto] bg-[right_10px_center] bg-no-repeat">
                    <option value="pt" class="text-slate-800">PT 🇧🇷</option>
                    <option value="en" class="text-slate-800">EN 🇺🇸</option>
                </select>
            </div>
        </div>
    </header>

    <main class="max-w-md mx-auto p-4 relative z-10">
        
        <div id="txt-instruction" class="mb-5 text-xs font-bold tracking-wide uppercase text-blue-800 text-center bg-white py-3 px-4 rounded-2xl shadow-sm border border-slate-200/60">
            selecione os jogos que você quer parar para ver
        </div>

        <div id="lista-jogos" class="space-y-3.5 pb-28">
            </div>

    </main>

    <div class="fixed bottom-0 left-0 right-0 bg-white/95 backdrop-blur-md p-4 border-t-2 border-slate-200 shadow-xl z-50">
        <div class="max-w-md mx-auto">
            <button id="btn-compartilhar" class="w-full bg-blue-700 hover:bg-blue-800 text-white font-black uppercase tracking-wider py-4 px-4 rounded-2xl shadow-lg shadow-blue-700/20 transition-all duration-200 active:scale-[0.98] flex items-center justify-center gap-2.5 text-sm disabled:opacity-40 disabled:cursor-not-allowed">
                <span class="text-yellow-400">💬</span>
                <span id="txt-btn-text">Compartilhar Agenda</span>
            </button>
        </div>
    </div>

    <script>
        // Dicionário de Idiomas
        const i18n = {
            pt: {
                title: "🗓️ Meus Jogos",
                subtitle: "Monte suas partidas imperdíveis e compartilhe no WhatsApp",
                instruction: "selecione os jogos que você quer parar para ver",
                btnText: "Compartilhar Agenda",
                whatsappHeader: "👋 Olha só os jogos da Copa que eu vou assistir! Bora ver juntos?\n\n",
                whatsappFooter: "\nQuais desses você vai ver também?",
                days: { "Seg": "Segunda", "Ter": "Terça", "Qua": "Quarta", "Qui": "Quinta", "Sex": "Sexta", "Sáb": "Sábado", "Dom": "Domingo" }
            },
            en: {
                title: "⚽ My Matchday",
                subtitle: "Build your schedule and share it on WhatsApp",
                instruction: "Select the matches you plan to watch:",
                btnText: "Share Schedule",
                whatsappHeader: "👋 Check out the World Cup matches I'm planning to watch! Let's watch together?\n\n",
                whatsappFooter: "\nWhich of these are you watching too?",
                days: { "Seg": "Monday", "Ter": "Tuesday", "Qua": "Wednesday", "Qui": "Thursday", "Sex": "Friday", "Sáb": "Saturday", "Dom": "Sunday" }
            }
        };

        let currentLang = 'pt';
        const jogosSelecionados = new Set(); // Armazena os IDs dos jogos

        // Dados dos Jogos (MVP - fixos por enquanto)
        const jogos = [
            { id: 1, data: "08/06", diaSemana: "Seg", hora: "11:00", selecao1: { pt: "Brasil", en: "Brazil" }, selecao2: { pt: "Croácia", en: "Croatia" } },
            { id: 2, data: "08/06", diaSemana: "Seg", hora: "16:00", selecao1: { pt: "França", en: "France" }, selecao2: { pt: "Marrocos", en: "Morocco" } },
            { id: 3, data: "09/06", diaSemana: "Ter", hora: "13:00", selecao1: { pt: "Argentina", en: "Argentina" }, selecao2: { pt: "Japão", en: "Japan" } },
            { id: 4, data: "10/06", diaSemana: "Qua", hora: "09:00", selecao1: { pt: "Espanha", en: "Spain" }, selecao2: { pt: "Canadá", en: "Canada" } },
            { id: 5, data: "11/06", diaSemana: "Qui", hora: "16:00", selecao1: { pt: "Alemanha", en: "Germany" }, selecao2: { pt: "Portugal", en: "Portugal" } }
        ];

        // Elementos do DOM
        const elTitle = document.getElementById('txt-title');
        const elSubtitle = document.getElementById('txt-subtitle');
        const elInstruction = document.getElementById('txt-instruction');
        const elBtnText = document.getElementById('txt-btn-text');
        const elSelectLang = document.getElementById('select-lang');
        const elListaJogos = document.getElementById('lista-jogos');
        const elBtnCompartilhar = document.getElementById('btn-compartilhar');

        // Função para atualizar os textos da interface
        function atualizarIdiomaInterface() {
            const textos = i18n[currentLang];
            elTitle.innerText = textos.title;
            elSubtitle.innerText = textos.subtitle;
            elInstruction.innerText = textos.instruction;
            atualizarBotao();
            renderizarJogos();
        }

        // Função para criar o HTML dos cards de jogos
        function renderizarJogos() {
            elListaJogos.innerHTML = '';
            const textos = i18n[currentLang];

            jogos.forEach(jogo => {
                const isSelected = jogosSelecionados.has(jogo.id);
                const card = document.createElement('div');
                
                // Estilização inspirada nas cores azul e branco de 2002
                card.className = `card-jogo p-4 rounded-2xl border transition-all duration-200 cursor-pointer flex items-center justify-between select-none ${
                    isSelected 
                    ? 'bg-blue-700 text-white border-blue-800 shadow-md transform -translate-y-0.5' 
                    : 'bg-white text-slate-800 border-slate-200 hover:border-slate-300'
                }`;
                
                const diaTraduzido = textos.days[jogo.diaSemana] || jogo.diaSemana;

                card.innerHTML = `
                    <div class="flex-1">
                        <div class="text-[10px] font-black tracking-widest uppercase flex items-center gap-2 ${isSelected ? 'text-white/80' : 'text-slate-400'}">
                            <span>📅 ${diaTraduzido}, ${jogo.data}</span>
                            <span>•</span>
                            <span>⏰ ${jogo.hora}</span>
                        </div>
                        <div class="text-base font-extrabold mt-1.5 flex items-center gap-2.5">
                            <span>${jogo.selecao1[currentLang]}</span>
                            <span class="${isSelected ? 'text-yellow-400' : 'text-blue-700/20'} font-medium text-xs">×</span>
                            <span>${jogo.selecao2[currentLang]}</span>
                        </div>
                    </div>
                    <div class="ml-4 flex items-center justify-center">
                        <div class="w-6 h-6 rounded-lg border-2 flex items-center justify-center transition-all duration-200 ${
                            isSelected 
                            ? 'bg-white border-white text-blue-700' 
                            : 'border-slate-200 bg-slate-50'
                        }">
                            ${isSelected ? '<svg class="w-4 h-4 text-blue-700" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="4" d="M5 13l4 4L19 7"></path></svg>' : ''}
                        </div>
                    </div>
                `;

                // Evento de clique para selecionar/deselecionar
                card.addEventListener('click', () => alternarSelecao(jogo.id));
                elListaJogos.appendChild(card);
            });
        }

        // Função para adicionar/remover da lista de selecionados
        function alternarSelecao(id) {
            if (jogosSelecionados.has(id)) {
                jogosSelecionados.delete(id);
            } else {
                jogosSelecionados.add(id);
            }
            renderizarJogos();
            atualizarBotao();
        }

        // Função para atualizar o contador e estado do botão
        function atualizarBotao() {
            const qtd = jogosSelecionados.size;
            const textos = i18n[currentLang];
            elBtnText.innerText = `${textos.btnText} (${qtd})`;
            elBtnCompartilhar.disabled = qtd === 0;
        }

        // Função para gerar e abrir o link do WhatsApp
        elBtnCompartilhar.addEventListener('click', () => {
            if (jogosSelecionados.size === 0) return;

            const textos = i18n[currentLang];
            let mensagem = textos.whatsappHeader;
            
            jogos.forEach(jogo => {
                if (jogosSelecionados.has(jogo.id)) {
                    const diaTraduzido = textos.days[jogo.diaSemana] || jogo.diaSemana;
                    const s1 = jogo.selecao1[currentLang];
                    const s2 = jogo.selecao2[currentLang];
                    
                    // Formatação da mensagem para o WhatsApp
                    mensagem += `📅 *${diaTraduzido}, ${jogo.data} - ${jogo.hora}*\n⚽ ${s1} × ${s2}\n\n`;
                }
            });

            mensagem += textos.whatsappFooter;

            const urlMensagem = encodeURIComponent(mensagem);
            window.open(`https://api.whatsapp.com/send?text=${urlMensagem}`, '_blank');
        });

        // Evento de troca de idioma
        elSelectLang.addEventListener('change', (e) => {
            currentLang = e.target.value;
            atualizarIdiomaInterface();
        });

        // Inicialização
        atualizarIdiomaInterface();
    </script>
</body>
</html>
