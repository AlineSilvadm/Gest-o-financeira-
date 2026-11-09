<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestão Financeira - Controle Pessoal</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons & Chart.js -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            dark: '#1E293B',
                            light: '#F8FAFC',
                            accent: '#B0E635',
                            accentHover: '#98CD24'
                        }
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
        }
        /* Custom scrollbars */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
        .dark ::-webkit-scrollbar-thumb {
            background: #334155;
        }
    </style>
</head>
<body class="bg-slate-100 dark:bg-slate-950 text-slate-800 dark:text-slate-100 min-h-screen flex flex-col md:flex-row overflow-x-hidden transition-colors duration-200">

    <!-- SIDEBAR -->
    <aside class="w-full md:w-64 bg-white dark:bg-slate-900 border-b md:border-b-0 md:border-r border-slate-200 dark:border-slate-800 p-5 flex flex-col justify-between shrink-0">
        <div>
            <!-- LOGO -->
            <div class="flex items-center gap-3 text-xl font-bold text-slate-900 dark:text-white mb-8">
                <div class="w-9 h-9 bg-slate-900 dark:bg-brand-accent text-brand-accent dark:text-slate-900 rounded-xl flex items-center justify-center font-extrabold shadow-sm">
                    <i data-lucide="wallet" class="w-5 h-5"></i>
                </div>
                <span>Gestão Financeira</span>
            </div>

            <!-- NAVIGATION LINKS -->
            <nav class="space-y-1">
                <a href="#" class="flex items-center gap-3 px-3 py-2.5 rounded-xl bg-brand-accent text-slate-900 font-semibold text-sm transition-all shadow-sm">
                    <i data-lucide="layout-dashboard" class="w-4 h-4"></i> Dashboard
                </a>
                <a href="#transacoes" class="flex items-center gap-3 px-3 py-2.5 rounded-xl text-slate-600 dark:text-slate-400 hover:bg-slate-100 dark:hover:bg-slate-800 hover:text-slate-900 dark:hover:text-white font-medium text-sm transition-all">
                    <i data-lucide="arrow-left-right" class="w-4 h-4"></i> Transações
                </a>
                <a href="#metas" class="flex items-center gap-3 px-3 py-2.5 rounded-xl text-slate-600 dark:text-slate-400 hover:bg-slate-100 dark:hover:bg-slate-800 hover:text-slate-900 dark:hover:text-white font-medium text-sm transition-all">
                    <i data-lucide="target" class="w-4 h-4"></i> Metas
                </a>
                <a href="#cartoes" class="flex items-center gap-3 px-3 py-2.5 rounded-xl text-slate-600 dark:text-slate-400 hover:bg-slate-100 dark:hover:bg-slate-800 hover:text-slate-900 dark:hover:text-white font-medium text-sm transition-all">
                    <i data-lucide="credit-card" class="w-4 h-4"></i> Cartões
                </a>
            </nav>
        </div>

        <!-- APP INFO CARD -->
        <div class="mt-6 p-4 rounded-2xl bg-slate-900 dark:bg-slate-800 text-white space-y-2">
            <div class="flex items-center gap-2 text-brand-accent font-bold text-xs">
                <i data-lucide="shield-check" class="w-4 h-4"></i> Versão Gratuita & Ilimitada
            </div>
            <p class="text-xs text-slate-300">Todos os seus dados são salvos localmente em seu navegador com privacidade total.</p>
        </div>
    </aside>

    <!-- MAIN CONTENT AREA -->
    <main class="flex-1 flex flex-col h-screen overflow-y-auto">
        
        <!-- HEADER -->
        <header class="bg-white dark:bg-slate-900 border-b border-slate-200 dark:border-slate-800 px-6 py-4 flex items-center justify-between sticky top-0 z-10">
            <div>
                <h1 class="text-xl font-bold text-slate-900 dark:text-white">Dashboard Financeiro</h1>
                <p class="text-xs text-slate-500 dark:text-slate-400">Gerencie e edite suas finanças em um só lugar</p>
            </div>

            <div class="flex items-center gap-3">
                <!-- Theme Toggle -->
                <button onclick="toggleTheme()" class="p-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:text-slate-900 dark:hover:text-white transition">
                    <i data-lucide="sun" class="w-5 h-5 hidden dark:block"></i>
                    <i data-lucide="moon" class="w-5 h-5 block dark:hidden"></i>
                </button>

                <!-- Nova Transação BTN -->
                <button onclick="openTxModal()" class="flex items-center gap-2 bg-slate-900 dark:bg-brand-accent text-white dark:text-slate-900 px-4 py-2 rounded-xl font-bold text-sm hover:opacity-90 transition shadow-sm">
                    <i data-lucide="plus" class="w-4 h-4"></i>
                    <span>Nova Transação</span>
                </button>
            </div>
        </header>

        <!-- DASHBOARD CONTAINER -->
        <div class="p-6 grid grid-cols-1 lg:grid-cols-3 gap-6">

            <!-- COLUNA ESQUERDA + CENTRO (2 colunas em telas grandes) -->
            <div class="lg:col-span-2 space-y-6">

                <!-- CARDS DE MÉTRICAS EDITÁVEIS -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    
                    <!-- ENTRADAS -->
                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800 relative group">
                        <div class="flex justify-between items-center text-xs text-slate-500 dark:text-slate-400 font-medium">
                            <span>Entradas</span>
                            <button onclick="editMetric('income')" class="opacity-0 group-hover:opacity-100 text-slate-400 hover:text-slate-700 dark:hover:text-white transition">
                                <i data-lucide="pencil" class="w-3.5 h-3.5"></i>
                            </button>
                        </div>
                        <div class="text-xl font-bold text-emerald-600 dark:text-emerald-400 mt-1" id="metric-income">R$ 0,00</div>
                        <div class="text-[11px] text-emerald-500 mt-1 font-semibold flex items-center gap-1">
                            <i data-lucide="arrow-down-left" class="w-3 h-3"></i> Receitas totais
                        </div>
                    </div>

                    <!-- SAÍDAS -->
                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800 relative group">
                        <div class="flex justify-between items-center text-xs text-slate-500 dark:text-slate-400 font-medium">
                            <span>Saídas / Despesas</span>
                            <button onclick="editMetric('expense')" class="opacity-0 group-hover:opacity-100 text-slate-400 hover:text-slate-700 dark:hover:text-white transition">
                                <i data-lucide="pencil" class="w-3.5 h-3.5"></i>
                            </button>
                        </div>
                        <div class="text-xl font-bold text-rose-600 dark:text-rose-400 mt-1" id="metric-expense">R$ 0,00</div>
                        <div class="text-[11px] text-rose-500 mt-1 font-semibold flex items-center gap-1">
                            <i data-lucide="arrow-up-right" class="w-3 h-3"></i> Gastos do mês
                        </div>
                    </div>

                    <!-- POUPANÇA -->
                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800 relative group">
                        <div class="flex justify-between items-center text-xs text-slate-500 dark:text-slate-400 font-medium">
                            <span>Poupança</span>
                            <button onclick="editMetric('savings')" class="opacity-0 group-hover:opacity-100 text-slate-400 hover:text-slate-700 dark:hover:text-white transition">
                                <i data-lucide="pencil" class="w-3.5 h-3.5"></i>
                            </button>
                        </div>
                        <div class="text-xl font-bold text-slate-900 dark:text-white mt-1" id="metric-savings">R$ 0,00</div>
                        <div class="text-[11px] text-blue-500 mt-1 font-semibold flex items-center gap-1">
                            <i data-lucide="piggy-bank" class="w-3 h-3"></i> Reserva guardada
                        </div>
                    </div>

                    <!-- INVESTIMENTOS -->
                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800 relative group">
                        <div class="flex justify-between items-center text-xs text-slate-500 dark:text-slate-400 font-medium">
                            <span>Investimentos</span>
                            <button onclick="editMetric('investment')" class="opacity-0 group-hover:opacity-100 text-slate-400 hover:text-slate-700 dark:hover:text-white transition">
                                <i data-lucide="pencil" class="w-3.5 h-3.5"></i>
                            </button>
                        </div>
                        <div class="text-xl font-bold text-slate-900 dark:text-white mt-1" id="metric-investment">R$ 0,00</div>
                        <div class="text-[11px] text-purple-500 mt-1 font-semibold flex items-center gap-1">
                            <i data-lucide="line-chart" class="w-3 h-3"></i> Aplicações ativas
                        </div>
                    </div>

                </div>

                <!-- GRÁFICO DE FLUXO DE CAIXA -->
                <div class="bg-white dark:bg-slate-900 p-5 rounded-2xl border border-slate-200 dark:border-slate-800">
                    <div class="flex justify-between items-center mb-4">
                        <div>
                            <h3 class="font-bold text-slate-900 dark:text-white text-base">Fluxo de Caixa</h3>
                            <p class="text-xs text-slate-500">Comparativo visual de Entradas vs Saídas</p>
                        </div>
                        <span class="text-xs bg-slate-100 dark:bg-slate-800 px-3 py-1 rounded-full text-slate-600 dark:text-slate-300 font-medium">Visualização Semanal</span>
                    </div>
                    <div class="h-60 w-full">
                        <canvas id="cashflowChart"></canvas>
                    </div>
                </div>

                <!-- TABELA DE TRANSAÇÕES RECENTES COM EDIÇÃO E EXCLUSÃO -->
                <div id="transacoes" class="bg-white dark:bg-slate-900 p-5 rounded-2xl border border-slate-200 dark:border-slate-800">
                    <div class="flex justify-between items-center mb-4">
                        <div>
                            <h3 class="font-bold text-slate-900 dark:text-white text-base">Transações Recentes</h3>
                            <p class="text-xs text-slate-500">Adicione, edite ou remova qualquer lançamento</p>
                        </div>
                        <button onclick="openTxModal()" class="text-xs text-slate-700 dark:text-brand-accent font-semibold hover:underline">
                            + Adicionar Registro
                        </button>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs">
                            <thead class="text-slate-400 border-b border-slate-100 dark:border-slate-800 font-medium">
                                <tr>
                                    <th class="py-2.5">Descrição</th>
                                    <th class="py-2.5">Categoria</th>
                                    <th class="py-2.5">Data</th>
                                    <th class="py-2.5">Valor</th>
                                    <th class="py-2.5 text-right">Ações</th>
                                </tr>
                            </thead>
                            <tbody id="tx-table-body" class="divide-y divide-slate-100 dark:divide-slate-800">
                                <!-- Transações renderizadas via JS -->
                            </tbody>
                        </table>
                    </div>
                </div>

            </div>

            <!-- COLUNA DIREITA -->
            <div class="space-y-6">

                <!-- SCORE FINANCEIRO & SALDO -->
                <div class="bg-white dark:bg-slate-900 p-5 rounded-2xl border border-slate-200 dark:border-slate-800">
                    <div class="flex justify-between items-center mb-2">
                        <h3 class="font-bold text-slate-900 dark:text-white text-sm">Saldo da Conta</h3>
                        <span class="text-xs font-semibold px-2.5 py-0.5 rounded-full bg-emerald-100 text-emerald-700 dark:bg-emerald-950 dark:text-emerald-300">Saúde Financeira: Excelente</span>
                    </div>
                    <div class="text-2xl font-extrabold text-slate-900 dark:text-white mb-4" id="total-balance-display">R$ 0,00</div>

                    <!-- DISTRIBUIÇÃO DE GASTOS (GRÁFICO ROSCA) -->
                    <div class="pt-2 border-t border-slate-100 dark:border-slate-800">
                        <h4 class="font-semibold text-xs text-slate-700 dark:text-slate-300 mb-2">Distribuição por Categoria</h4>
                        <div class="h-44 relative">
                            <canvas id="expenseCategoryChart"></canvas>
                        </div>
                    </div>
                </div>

                <!-- METAS DE POUPANÇA EDITÁVEIS -->
                <div id="metas" class="bg-white dark:bg-slate-900 p-5 rounded-2xl border border-slate-200 dark:border-slate-800">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="font-bold text-slate-900 dark:text-white text-sm">Metas de Poupança</h3>
                        <button onclick="addGoalPrompt()" class="text-xs text-emerald-600 dark:text-brand-accent font-semibold hover:underline">+ Nova Meta</button>
                    </div>
                    <div id="goals-list" class="space-y-4">
                        <!-- Metas inseridas dinamicamente -->
                    </div>
                </div>

                <!-- CARTÕES VIRTUAIS -->
                <div id="cartoes" class="bg-white dark:bg-slate-900 p-5 rounded-2xl border border-slate-200 dark:border-slate-800 space-y-3">
                    <h3 class="font-bold text-slate-900 dark:text-white text-sm mb-2">Meus Cartões</h3>
                    
                    <div class="p-4 rounded-xl bg-gradient-to-tr from-slate-900 to-slate-800 text-white shadow-md relative">
                        <div class="text-[10px] opacity-75 font-semibold">Platinum Plus • VISA</div>
                        <div class="text-lg font-bold my-2">R$ 4.500,00</div>
                        <div class="text-xs opacity-60 tracking-wider">•••• •••• •••• 9967</div>
                    </div>

                    <div class="p-4 rounded-xl bg-gradient-to-tr from-emerald-900 to-slate-900 text-white shadow-md relative">
                        <div class="text-[10px] opacity-75 font-semibold">Freedom • Mastercard</div>
                        <div class="text-lg font-bold my-2">R$ 2.320,00</div>
                        <div class="text-xs opacity-60 tracking-wider">•••• •••• •••• 5487</div>
                    </div>
                </div>

            </div>

        </div>
    </main>

    <!-- MODAL ADICIONAR / EDITAR TRANSAÇÃO -->
    <div id="tx-modal" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm hidden items-center justify-center z-50 p-4">
        <div class="bg-white dark:bg-slate-900 w-full max-w-md rounded-2xl p-6 shadow-xl border border-slate-200 dark:border-slate-800">
            <div class="flex justify-between items-center mb-4">
                <h3 class="font-bold text-lg text-slate-900 dark:text-white" id="modal-title">Adicionar Transação</h3>
                <button onclick="closeTxModal()" class="text-slate-400 hover:text-slate-600"><i data-lucide="x" class="w-5 h-5"></i></button>
            </div>
            
            <form id="tx-form" onsubmit="saveTx(event)" class="space-y-4">
                <input type="hidden" id="tx-id">
                
                <div>
                    <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300 mb-1">Descrição</label>
                    <input type="text" id="tx-desc" required placeholder="Ex: Supermercado, Salário..." class="w-full px-3 py-2 rounded-xl border border-slate-200 dark:border-slate-700 dark:bg-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-accent">
                </div>

                <div>
                    <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300 mb-1">Categoria</label>
                    <input type="text" id="tx-cat" required placeholder="Ex: Alimentação, Lazer, Moradia" class="w-full px-3 py-2 rounded-xl border border-slate-200 dark:border-slate-700 dark:bg-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-accent">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300 mb-1">Valor (R$)</label>
                        <input type="number" step="0.01" id="tx-val" required placeholder="0.00" class="w-full px-3 py-2 rounded-xl border border-slate-200 dark:border-slate-700 dark:bg-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-accent">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300 mb-1">Tipo</label>
                        <select id="tx-type" class="w-full px-3 py-2 rounded-xl border border-slate-200 dark:border-slate-700 dark:bg-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-accent">
                            <option value="income">Entrada (+)</option>
                            <option value="expense">Saída (-)</option>
                        </select>
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300 mb-1">Data</label>
                    <input type="date" id="tx-date" required class="w-full px-3 py-2 rounded-xl border border-slate-200 dark:border-slate-700 dark:bg-slate-800 text-sm focus:outline-none focus:ring-2 focus:ring-brand-accent">
                </div>

                <div class="pt-2 flex gap-3">
                    <button type="button" onclick="closeTxModal()" class="flex-1 py-2.5 rounded-xl border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 text-sm font-semibold hover:bg-slate-100 dark:hover:bg-slate-800">Cancelar</button>
                    <button type="submit" class="flex-1 py-2.5 rounded-xl bg-slate-900 dark:bg-brand-accent text-white dark:text-slate-900 text-sm font-bold hover:opacity-90">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- JAVASCRIPT APP LOGIC -->
    <script>
        // ESTADO INICIAL DA APLICAÇÃO (Salvo no LocalStorage)
        const DEFAULT_DATA = {
            metrics: {
                income: 8500.00,
                expense: 4900.00,
                savings: 2000.00,
                investment: 1600.00
            },
            transactions: [
                { id: '1', desc: 'Salário Mensal', cat: 'Renda', val: 5000.00, type: 'income', date: '2026-11-01' },
                { id: '2', desc: 'Rendimento Investimento', cat: 'Investimentos', val: 200.00, type: 'income', date: '2026-11-05' },
                { id: '3', desc: 'Supermercado', cat: 'Alimentação', val: 450.20, type: 'expense', date: '2026-11-06' },
                { id: '4', desc: 'Conta de Luz', cat: 'Despesas Fixas', val: 120.75, type: 'expense', date: '2026-11-07' },
                { id: '5', desc: 'Assinaturas Streaming', cat: 'Lazer', val: 71.90, type: 'expense', date: '2026-11-08' }
            ],
            goals: [
                { id: '1', name: 'Reserva de Emergência', current: 4500, target: 10000 },
                { id: '2', name: 'Fundo de Aposentadoria', current: 5000, target: 20000 },
                { id: '3', name: 'Viagem & Lazer', current: 2500, target: 5000 }
            ]
        };

        // Carregar do localStorage ou usar padrão
        let appData = JSON.parse(localStorage.getItem('GESTAVO_FINANCEIRA_DATA')) || DEFAULT_DATA;

        function saveData() {
            localStorage.setItem('GESTAVO_FINANCEIRA_DATA', JSON.stringify(appData));
            renderAll();
        }

        // FORMATADORES DE MOEDA
        const formatBRL = (val) => Number(val).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });

        // INICIALIZAÇÃO DE GRÁFICOS
        let cashflowChartInstance = null;
        let expenseChartInstance = null;

        function renderAll() {
            renderMetrics();
            renderTransactions();
            renderGoals();
            renderCharts();
            lucide.createIcons();
        }

        // 1. RENDERIZAR MÉTRICAS
        function renderMetrics() {
            document.getElementById('metric-income').innerText = formatBRL(appData.metrics.income);
            document.getElementById('metric-expense').innerText = formatBRL(appData.metrics.expense);
            document.getElementById('metric-savings').innerText = formatBRL(appData.metrics.savings);
            document.getElementById('metric-investment').innerText = formatBRL(appData.metrics.investment);

            // Calcular Saldo Total (Entradas - Saídas + Poupança + Investimentos)
            const balance = (appData.metrics.income - appData.metrics.expense);
            document.getElementById('total-balance-display').innerText = formatBRL(balance);
        }

        // EDITAR MÉTRICA VIA PROMPT
        function editMetric(key) {
            const labels = {
                income: 'Entradas',
                expense: 'Saídas / Despesas',
                savings: 'Poupança',
                investment: 'Investimentos'
            };
            const newVal = prompt(`Informe o novo valor para ${labels[key]}:`, appData.metrics[key]);
            if (newVal !== null && !isNaN(parseFloat(newVal))) {
                appData.metrics[key] = parseFloat(newVal);
                saveData();
            }
        }

        // 2. RENDERIZAR TRANSAÇÕES
        function renderTransactions() {
            const tbody = document.getElementById('tx-table-body');
            tbody.innerHTML = '';

            if (appData.transactions.length === 0) {
                tbody.innerHTML = `<tr><td colspan="5" class="py-4 text-center text-slate-400">Nenhuma transação cadastrada.</td></tr>`;
                return;
            }

            appData.transactions.forEach((tx) => {
                const tr = document.createElement('tr');
                const isIncome = tx.type === 'income';
                const valClass = isIncome ? 'text-emerald-600 dark:text-emerald-400 font-bold' : 'text-rose-600 dark:text-rose-400 font-bold';
                const sign = isIncome ? '+' : '-';

                tr.innerHTML = `
                    <td class="py-3 font-semibold text-slate-800 dark:text-white">${tx.desc}</td>
                    <td class="py-3 text-slate-500">${tx.cat}</td>
                    <td class="py-3 text-slate-400">${tx.date}</td>
                    <td class="py-3 ${valClass}">${sign} ${formatBRL(tx.val)}</td>
                    <td class="py-3 text-right space-x-1">
                        <button onclick="editTx('${tx.id}')" class="p-1 text-slate-400 hover:text-slate-700 dark:hover:text-white transition"><i data-lucide="pencil" class="w-3.5 h-3.5"></i></button>
                        <button onclick="deleteTx('${tx.id}')" class="p-1 text-slate-400 hover:text-rose-600 transition"><i data-lucide="trash-2" class="w-3.5 h-3.5"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        // MODAL TRANSAÇÃO
        function openTxModal(txId = null) {
            document.getElementById('tx-modal').classList.remove('hidden');
            document.getElementById('tx-modal').classList.add('flex');
            
            if (txId) {
                const tx = appData.transactions.find(t => t.id === txId);
                document.getElementById('modal-title').innerText = 'Editar Transação';
                document.getElementById('tx-id').value = tx.id;
                document.getElementById('tx-desc').value = tx.desc;
                document.getElementById('tx-cat').value = tx.cat;
                document.getElementById('tx-val').value = tx.val;
                document.getElementById('tx-type').value = tx.type;
                document.getElementById('tx-date').value = tx.date;
            } else {
                document.getElementById('modal-title').innerText = 'Adicionar Transação';
                document.getElementById('tx-form').reset();
                document.getElementById('tx-id').value = '';
                document.getElementById('tx-date').value = new Date().toISOString().split('T')[0];
            }
        }

        function closeTxModal() {
            document.getElementById('tx-modal').classList.add('hidden');
            document.getElementById('tx-modal').classList.remove('flex');
        }

        function saveTx(e) {
            e.preventDefault();
            const id = document.getElementById('tx-id').value;
            const desc = document.getElementById('tx-desc').value;
            const cat = document.getElementById('tx-cat').value;
            const val = parseFloat(document.getElementById('tx-val').value);
            const type = document.getElementById('tx-type').value;
            const date = document.getElementById('tx-date').value;

            if (id) {
                // Editar existente
                const index = appData.transactions.findIndex(t => t.id === id);
                if (index !== -1) {
                    appData.transactions[index] = { id, desc, cat, val, type, date };
                }
            } else {
                // Criar nova
                const newTx = { id: Date.now().toString(), desc, cat, val, type, date };
                appData.transactions.unshift(newTx);
            }

            closeTxModal();
            saveData();
        }

        function editTx(id) {
            openTxModal(id);
        }

        function deleteTx(id) {
            if (confirm('Tem certeza de que deseja excluir esta transação?')) {
                appData.transactions = appData.transactions.filter(t => t.id !== id);
                saveData();
            }
        }

        // 3. RENDERIZAR METAS
        function renderGoals() {
            const container = document.getElementById('goals-list');
            container.innerHTML = '';

            appData.goals.forEach(goal => {
                const percent = Math.min(100, Math.round((goal.current / goal.target) * 100));
                const div = document.createElement('div');
                div.className = "group border-b border-slate-100 dark:border-slate-800 pb-3 last:border-none";
                div.innerHTML = `
                    <div class="flex justify-between items-center text-xs font-semibold text-slate-800 dark:text-white mb-1">
                        <span>${goal.name}</span>
                        <div class="flex items-center gap-1">
                            <span>${percent}%</span>
                            <button onclick="editGoal('${goal.id}')" class="opacity-0 group-hover:opacity-100 text-slate-400 hover:text-slate-700 dark:hover:text-white transition ml-1">
                                <i data-lucide="pencil" class="w-3 h-3"></i>
                            </button>
                        </div>
                    </div>
                    <div class="w-full bg-slate-100 dark:bg-slate-800 h-2 rounded-full overflow-hidden">
                        <div class="bg-brand-accent h-full rounded-full" style="width: ${percent}%;"></div>
                    </div>
                    <div class="flex justify-between text-[11px] text-slate-400 mt-1">
                        <span>Guardado: ${formatBRL(goal.current)}</span>
                        <span>Meta: ${formatBRL(goal.target)}</span>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function editGoal(id) {
            const goal = appData.goals.find(g => g.id === id);
            const newCurrent = prompt(`Atualizar valor poupado para "${goal.name}":`, goal.current);
            if (newCurrent !== null && !isNaN(parseFloat(newCurrent))) {
                goal.current = parseFloat(newCurrent);
                saveData();
            }
        }

        function addGoalPrompt() {
            const name = prompt('Nome da nova meta:');
            if (!name) return;
            const target = prompt('Valor da meta final (R$):');
            if (!target || isNaN(parseFloat(target))) return;

            appData.goals.push({
                id: Date.now().toString(),
                name,
                current: 0,
                target: parseFloat(target)
            });
            saveData();
        }

        // 4. GRÁFICOS DINÂMICOS
        function renderCharts() {
            // Chart 1: Cashflow Line Chart
            const ctxCashflow = document.getElementById('cashflowChart').getContext('2d');
            if (cashflowChartInstance) cashflowChartInstance.destroy();

            cashflowChartInstance = new Chart(ctxCashflow, {
                type: 'line',
                data: {
                    labels: ['Sem 1', 'Sem 2', 'Sem 3', 'Sem 4'],
                    datasets: [
                        {
                            label: 'Entradas',
                            data: [appData.metrics.income * 0.4, appData.metrics.income * 0.2, appData.metrics.income * 0.3, appData.metrics.income * 0.1],
                            borderColor: '#B0E635',
                            backgroundColor: 'rgba(176, 230, 53, 0.15)',
                            fill: true,
                            tension: 0.4
                        },
                        {
                            label: 'Saídas',
                            data: [appData.metrics.expense * 0.2, appData.metrics.expense * 0.3, appData.metrics.expense * 0.25, appData.metrics.expense * 0.25],
                            borderColor: '#EF4444',
                            borderDash: [4, 4],
                            tension: 0.4
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        x: { grid: { display: false } },
                        y: { grid: { color: 'rgba(200, 200, 200, 0.1)' } }
                    }
                }
            });

            // Chart 2: Expense Categories Donut Chart
            const ctxExpense = document.getElementById('expenseCategoryChart').getContext('2d');
            if (expenseChartInstance) expenseChartInstance.destroy();

            // Agrupar despesas por categoria das transações
            const expensesByCat = {};
            appData.transactions.filter(t => t.type === 'expense').forEach(t => {
                expensesByCat[t.cat] = (expensesByCat[t.cat] || 0) + t.val;
            });

            const labels = Object.keys(expensesByCat).length ? Object.keys(expensesByCat) : ['Outros'];
            const dataVals = Object.keys(expensesByCat).length ? Object.values(expensesByCat) : [1];

            expenseChartInstance = new Chart(ctxExpense, {
                type: 'doughnut',
                data: {
                    labels,
                    datasets: [{
                        data: dataVals,
                        backgroundColor: ['#10B981', '#6366F1', '#F59E0B', '#EF4444', '#8B5CF6'],
                        borderWidth: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    cutout: '70%',
                    plugins: { legend: { position: 'bottom', labels: { boxWidth: 10, font: { size: 10 } } } }
                }
            });
        }

        // MODO CLARO / ESCURO TOGGLE
        function toggleTheme() {
            document.documentElement.classList.toggle('dark');
        }

        // CARREGAR APLICAÇÃO NA INICIALIZAÇÃO
        window.onload = function() {
            renderAll();
        };
    </script>
</body>
</html>
