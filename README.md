<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard de Vendas Avançado</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"> 
    <!-- CSS Embutido -->
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        :root {
            --bg-dark: #0f172a;
            --card-dark: #1e293b;
            --text-dark: #e2e8f0;
            --border-dark: #334155;
            --shadow-dark: rgba(0, 0, 0, 0.4);
            --primary-color: #3b82f6;
            --success-color: #10b981;
            --danger-color: #ef4444;
            --bg-light: #f1f5f9;
            --card-light: #ffffff;
            --text-light: #1e293b;
            --border-light: #cbd5e1;
            --shadow-light: rgba(0, 0, 0, 0.1);
        }
        html, body {
            height: 100%;
            font-family: 'Inter', sans-serif;
        }
        body {
            background: linear-gradient(135deg, var(--bg-dark), var(--card-dark));
            color: var(--text-dark);
            padding: 2rem;
            transition: background 0.4s, color 0.4s;
        }
        body.light {
            background: linear-gradient(135deg, var(--bg-light), var(--card-light));
            color: var(--text-light);
        }
        body.light .dashboard-header {
            background: rgba(255, 255, 255, 0.8);
            box-shadow: 0 4px 10px var(--shadow-light);
        }
        body.light .card {
            background: rgba(255, 255, 255, 0.9);
            box-shadow: 0 4px 12px var(--shadow-light);
            border: 1px solid var(--border-light);
        }
        body.light .input-field, body.light select {
            background: var(--bg-light);
            color: var(--text-light);
            border: 1px solid var(--border-light);
        }
        body.light table th {
            background: rgba(226, 232, 240, 0.9);
            color: var(--text-light);
        }
        body.light .list-container li {
            background: rgba(241, 245, 249, 0.9);
            border-bottom: 1px solid var(--border-light);
        }
        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 1.5rem;
            border-radius: 16px;
            background: rgba(30, 41, 59, 0.8);
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 10px var(--shadow-dark);
            margin-bottom: 2rem;
            transition: background 0.4s, box-shadow 0.4s;
        }
        .dashboard-header h1 {
            font-size: 2rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .dashboard-main {
            max-width: 1200px;
            margin: 0 auto;
        }
        .summary-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 2rem;
        }
        .content-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }
        .content-grid .full-width {
            grid-column: 1 / -1;
        }
        .card {
            background: rgba(30, 41, 59, 0.85);
            backdrop-filter: blur(10px);
            padding: 25px;
            border-radius: 16px;
            box-shadow: 0 4px 12px var(--shadow-dark);
            transition: background 0.4s, transform 0.2s;
            border: 1px solid transparent;
        }
        .card:hover {
            transform: translateY(-5px);
        }
        .summary-cards .card {
            text-align: center;
        }
        .summary-value {
            font-size: 2.2rem;
            font-weight: 700;
            margin-top: 10px;
            color: var(--primary-color);
        }
        h2 {
            font-size: 1.4rem;
            margin-bottom: 1.2rem;
            color: var(--primary-color);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .btn {
            border: none;
            color: #fff;
            padding: 10px 18px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 0.95rem;
            font-weight: 600;
            transition: transform 0.2s, background 0.3s, box-shadow 0.2s;
        }
        .btn:hover {
            transform: scale(1.05);
        }
        .btn-primary {
            background: linear-gradient(135deg, var(--primary-color), #2563eb);
        }
        .btn-success {
            background: linear-gradient(135deg, var(--success-color), #059669);
        }
        .btn-danger {
            background: linear-gradient(135deg, var(--danger-color), #b91c1c);
        }
        .btn-icon {
            background: none;
            border: 1px solid var(--border-dark);
            color: var(--text-dark);
            padding: 10px;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .btn-icon:hover {
            background: rgba(255, 255, 255, 0.1);
        }
        .input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        .input-group input {
            flex-grow: 1;
        }
        .input-field {
            width: 100%;
            padding: 12px;
            margin-bottom: 12px;
            border: 1px solid var(--border-dark);
            border-radius: 10px;
            font-size: 1rem;
            background: rgba(15, 23, 42, 0.7);
            color: var(--text-dark);
            transition: border-color 0.3s, transform 0.2s, box-shadow 0.2s;
        }
        .input-field:focus {
            border-color: var(--primary-color);
            outline: none;
            transform: scale(1.01);
            box-shadow: 0 0 8px rgba(59, 130, 246, 0.5);
        }
        .list-container {
            list-style: none;
            padding: 0;
            margin-top: 15px;
        }
        .list-container li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 15px;
            margin-bottom: 8px;
            border-radius: 10px;
            background: rgba(15, 23, 42, 0.8);
            font-size: 0.95rem;
            border-left: 4px solid var(--primary-color);
            transition: transform 0.2s;
        }
        .list-container li:hover {
            transform: translateX(5px);
        }
        .table-container {
            overflow-x: auto;
        }
        #salesTable {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            margin-top: 15px;
            font-size: 0.95rem;
            border-radius: 10px;
            overflow: hidden;
        }
        #salesTable th, #salesTable td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid var(--border-dark);
        }
        #salesTable th {
            background: rgba(30, 41, 59, 0.9);
            color: #93c5fd;
            font-weight: 600;
        }
        #salesTable tbody tr:last-child td {
            border-bottom: none;
        }
        .chart-card {
            height: 400px; /* Altura fixa para os gráficos */
            display: flex;
            flex-direction: column;
        }
        .chart-card canvas {
            flex-grow: 1;
        }
        @media (max-width: 1024px) {
            .content-grid {
                grid-template-columns: 1fr;
            }
        }
        @media (max-width: 768px) {
            body {
                padding: 1rem;
            }
            .dashboard-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
            }
            .header-actions {
                display: flex;
                width: 100%;
                justify-content: space-between;
            }
        }
    </style>
</head>
<body>
    <header class="dashboard-header">
        <h1><i class="fas fa-chart-line"></i> Dashboard de Vendas</h1>
        <div class="header-actions">
            <button id="toggleTheme" class="btn btn-icon" title="Alternar Tema">
                <i class="fas fa-sun"></i>
            </button>
            <button id="exportCSV" class="btn btn-primary">
                <i class="fas fa-download"></i> Exportar CSV
            </button>
        </div>
    </header>
    <main class="dashboard-main">
        <section class="summary-cards">
            <div class="card">
                <h3>Total de Vendas</h3>
                <p id="totalSales" class="summary-value">R$ 0,00</p>
            </div>
            <div class="card">
                <h3>Usuários Cadastrados</h3>
                <p id="totalUsers" class="summary-value">0</p>
            </div>
            <div class="card">
                <h3>Média por Venda</h3>
                <p id="averageSale" class="summary-value">R$ 0,00</p>
            </div>
        </section>
        <section class="content-grid">
            <!-- Gerenciar Usuários -->
            <div class="card form-card">
                <h2><i class="fas fa-users-cog"></i> Gerenciar Usuários</h2>
                <div class="input-group">
                    <input type="text" id="userName" placeholder="Nome do usuário">
                    <button id="addUserBtn" class="btn btn-success">Adicionar</button>
                </div>
                <ul id="userList" class="list-container"></ul>
            </div>
            <div class="card form-card">
                <h2><i class="fas fa-cash-register"></i> Registrar Venda</h2>
                <select id="userSelect" class="input-field"></select>
                <input type="number" id="saleAmount" placeholder="Valor da venda (R$)" class="input-field">
                <input type="date" id="saleDate" class="input-field">
                <button id="addSaleBtn" class="btn btn-primary">Adicionar Venda</button>
            </div>
            <div class="card full-width">
                <h2><i class="fas fa-table"></i> Vendas Registradas</h2>
                <div class="filter-controls">
                    <select id="filterUser" class="input-field">
                        <option value="">Todos os Usuários</option>
                    </select>
                    <input type="date" id="filterStart" class="input-field">
                    <input type="date" id="filterEnd" class="input-field">
                    <button id="resetFilters" class="btn btn-danger">Limpar Filtros</button>
                </div>
                <div class="table-container">
                    <table id="salesTable">
                        <thead>
                            <tr>
                                <th>Usuário</th>
                                <th>Valor (R$)</th>
                                <th>Data</th>
                                <th>Ações</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>
            <div class="card chart-card">
                <h2><i class="fas fa-chart-bar"></i> Vendas por Data</h2>
                <canvas id="salesChart"></canvas>
            </div>
            <div class="card chart-card">
                <h2><i class="fas fa-chart-pie"></i> Vendas por Usuário</h2>
                <canvas id="userPieChart"></canvas>
            </div>
        </section>
    </main>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const DOM = {
                userName: document.getElementById('userName'),
                addUserBtn: document.getElementById('addUserBtn'),
                userList: document.getElementById('userList'),
                userSelect: document.getElementById('userSelect'),
                saleAmount: document.getElementById('saleAmount'),
                saleDate: document.getElementById('saleDate'),
                addSaleBtn: document.getElementById('addSaleBtn'),
                filterUser: document.getElementById('filterUser'),
                filterStart: document.getElementById('filterStart'),
                filterEnd: document.getElementById('filterEnd'),
                salesTableBody: document.getElementById('salesTable').querySelector('tbody'),
                totalSalesEl: document.getElementById('totalSales'),
                totalUsersEl: document.getElementById('totalUsers'),
                averageSaleEl: document.getElementById('averageSale'),
                toggleThemeBtn: document.getElementById('toggleTheme'),
                exportCSVBtn: document.getElementById('exportCSV'),
                resetFiltersBtn: document.getElementById('resetFilters')
            };
            // Estado da Aplicação (Dados)
            let users = JSON.parse(localStorage.getItem('users')) || [];
            let sales = JSON.parse(localStorage.getItem('sales')) || [];
            const ctxSales = document.getElementById('salesChart').getContext('2d');
            let salesChart = createSalesChart(ctxSales);
            const ctxPie = document.getElementById('userPieChart').getContext('2d');
            let userPieChart = createUserPieChart(ctxPie);
            init();
            DOM.addUserBtn.addEventListener('click', addUser);
            DOM.addSaleBtn.addEventListener('click', addSale);
            DOM.filterUser.addEventListener('change', renderSales);
            DOM.filterStart.addEventListener('change', renderSales);
            DOM.filterEnd.addEventListener('change', renderSales);
            DOM.toggleThemeBtn.addEventListener('click', toggleTheme);
            DOM.exportCSVBtn.addEventListener('click', exportCSV);
            DOM.resetFiltersBtn.addEventListener('click', resetFilters);
            function init() {
                updateUserSelects();
                renderSales();
                setInitialTheme();
            }
            function saveData() {
                localStorage.setItem('users', JSON.stringify(users));
                localStorage.setItem('sales', JSON.stringify(sales));
            }
            function addUser() {
                const name = DOM.userName.value.trim();
                if (!name) {
                    // Substitua o 'alert' por uma mensagem na tela para uma melhor experiência do usuário
                    // alert('Por favor, digite um nome de usuário.');
                    console.log('Por favor, digite um nome de usuário.');
                    return;
                }
                users.push(name);
                DOM.userName.value = '';
                saveData();
                updateUserSelects();
            }
            function deleteUser(index) {
                // Substitua o 'confirm' por uma caixa de diálogo personalizada
                // if (!confirm('Tem certeza que deseja excluir este usuário? As vendas dele permanecerão registradas.')) return;
                if (!window.confirm('Tem certeza que deseja excluir este usuário? As vendas dele permanecerão registradas.')) return;
                users.splice(index, 1);
                saveData();
                updateUserSelects();
                renderSales();
            }
            function updateUserSelects() {
                DOM.userSelect.innerHTML = '';
                DOM.filterUser.innerHTML = '<option value="">Todos os Usuários</option>';
                DOM.userList.innerHTML = '';
                if (users.length === 0) {
                    const emptyOption = document.createElement('option');
                    emptyOption.textContent = 'Nenhum usuário cadastrado';
                    DOM.userSelect.appendChild(emptyOption);
                    DOM.userSelect.disabled = true;
                    DOM.addSaleBtn.disabled = true;
                } else {
                    DOM.userSelect.disabled = false;
                    DOM.addSaleBtn.disabled = false;
                }
                users.forEach((user, index) => {
                    const opt1 = document.createElement('option');
                    opt1.value = index;
                    opt1.textContent = user;
                    DOM.userSelect.appendChild(opt1);
                    const opt2 = document.createElement('option');
                    opt2.value = user;
                    opt2.textContent = user;
                    DOM.filterUser.appendChild(opt2);
                    const li = document.createElement('li');
                    li.innerHTML = `${user} <button class="btn btn-danger btn-sm" onclick="deleteUser(${index})">Excluir</button>`;
                    DOM.userList.appendChild(li);
                });
                DOM.totalUsersEl.innerText = users.length;
            }
            function addSale() {
                const userIndex = DOM.userSelect.value;
                const amount = parseFloat(DOM.saleAmount.value);
                const date = DOM.saleDate.value || new Date().toISOString().slice(0, 10);
                if (userIndex === '' || isNaN(amount) || amount <= 0) {
                    // Substitua o 'alert' por uma mensagem na tela
                    // alert('Por favor, preencha os campos corretamente.');
                    console.log('Por favor, preencha os campos corretamente.');
                    return;
                }
                sales.push({ user: users[userIndex], value: amount, date });
                DOM.saleAmount.value = '';
                DOM.saleDate.value = '';
                saveData();
                renderSales();
            }
            function deleteSale(index) {
                // Substitua o 'confirm' por uma caixa de diálogo personalizada
                // if (!confirm('Tem certeza que deseja excluir esta venda?')) return;
                if (!window.confirm('Tem certeza que deseja excluir esta venda?')) return;
                sales.splice(index, 1);
                saveData();
                renderSales();
            }
            function renderSales() {
                DOM.salesTableBody.innerHTML = '';
                let total = 0;
                const filterU = DOM.filterUser.value;
                const filterStart = DOM.filterStart.value;
                const filterEnd = DOM.filterEnd.value;
                const filteredSales = sales.filter(s => {
                    if (filterU && s.user !== filterU) return false;
                    if (filterStart && s.date < filterStart) return false;
                    if (filterEnd && s.date > filterEnd) return false;
                    return true;
                });
                filteredSales.forEach((sale, index) => {
                    total += sale.value;
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${sale.user}</td>
                        <td>R$ ${sale.value.toFixed(2)}</td>
                        <td>${sale.date}</td>
                        <td><button class="btn btn-danger btn-sm" onclick="deleteSale(${index})">Excluir</button></td>
                    `;
                    DOM.salesTableBody.appendChild(row);
                });
                DOM.totalSalesEl.innerText = `R$ ${total.toFixed(2)}`;
                DOM.averageSaleEl.innerText = `R$ ${(total / (filteredSales.length || 1)).toFixed(2)}`;
                updateCharts(filteredSales);
            }
            function exportCSV() {
                let csv = 'Usuário,Valor,Data\n';
                sales.forEach(s => {
                    csv += `${s.user},${s.value},${s.date}\n`;
                });
                const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
                const link = document.createElement('a');
                link.href = URL.createObjectURL(blob);
                link.download = 'vendas.csv';
                link.click();
            }
            function resetFilters() {
                DOM.filterUser.value = '';
                DOM.filterStart.value = '';
                DOM.filterEnd.value = '';
                renderSales();
            }
            function createSalesChart(ctx) {
                return new Chart(ctx, {
                    type: 'line',
                    data: { labels: [], datasets: [{ label: 'Vendas (R$)', data: [], borderColor: '#3b82f6', fill: true, backgroundColor: 'rgba(59,130,246,0.2)', tension: 0.4 }] },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { labels: { color: 'var(--text-dark)' } } },
                        scales: {
                            x: { ticks: { color: 'var(--text-dark)' } },
                            y: { ticks: { color: 'var(--text-dark)' } }
                        }
                    }
                });
            }
            function createUserPieChart(ctx) {
                return new Chart(ctx, {
                    type: 'pie',
                    data: { labels: [], datasets: [{ data: [], backgroundColor: ['#3b82f6', '#10b981', '#f59e0b', '#ef4444', '#8b5cf6'] }] },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { labels: { color: 'var(--text-dark)' } } }
                    }
                });
            }
            function updateCharts(filteredSales) {
                const totalPerUser = {};
                const salesByDate = {};
                filteredSales.forEach(sale => {
                    totalPerUser[sale.user] = (totalPerUser[sale.user] || 0) + sale.value;
                    salesByDate[sale.date] = (salesByDate[sale.date] || 0) + sale.value;
                });
                const sortedDates = Object.keys(salesByDate).sort();
                const salesData = sortedDates.map(date => salesByDate[date]);
                salesChart.data.labels = sortedDates;
                salesChart.data.datasets[0].data = salesData;
                salesChart.update();
                userPieChart.data.labels = Object.keys(totalPerUser);
                userPieChart.data.datasets[0].data = Object.values(totalPerUser);
                userPieChart.update();
            }
            function setInitialTheme() {
                const savedTheme = localStorage.getItem('theme');
                if (savedTheme === 'light') {
                    document.body.classList.add('light');
                    DOM.toggleThemeBtn.innerHTML = '<i class="fas fa-moon"></i>';
                } else {
                    DOM.toggleThemeBtn.innerHTML = '<i class="fas fa-sun"></i>';
                }
                updateChartTheme();
            }
            function toggleTheme() {
                document.body.classList.toggle('light');
                const isLight = document.body.classList.contains('light');
                localStorage.setItem('theme', isLight ? 'light' : 'dark');
                DOM.toggleThemeBtn.innerHTML = isLight ? '<i class="fas fa-moon"></i>' : '<i class="fas fa-sun"></i>';
                updateChartTheme();
            }
            function updateChartTheme() {
                const isLight = document.body.classList.contains('light');
                const color = isLight ? '#222' : '#fff';
                salesChart.options.plugins.legend.labels.color = color;
                salesChart.options.scales.x.ticks.color = color;
                salesChart.options.scales.y.ticks.color = color;
                salesChart.options.plugins.legend.labels.font = { weight: 'bold' };
                userPieChart.options.plugins.legend.labels.color = color;
                userPieChart.options.plugins.legend.labels.font = { weight: 'bold' };
                salesChart.update();
                userPieChart.update();
            }
            window.deleteUser = deleteUser;
            window.deleteSale = deleteSale;
        });
    </script>
</body>
</html>
