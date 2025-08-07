<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dashboard de Vendas Avançado 2.0</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"> 
<style>
:root {
    --primary: #3b82f6;
    --success: #10b981;
    --danger: #ef4444;
    --bg-dark: #0f172a;
    --bg-light: #f1f5f9;
    --card-dark: rgba(30,41,59,0.85);
    --card-light: rgba(255,255,255,0.85);
    --text-dark: #e2e8f0;
    --text-light: #1e293b;
    --shadow-dark: rgba(0,0,0,0.4);
    --shadow-light: rgba(0,0,0,0.1);
    --blur: blur(12px);
}
* {
    margin: 0; padding: 0; box-sizing: border-box;
}
body {
    font-family: 'Inter', sans-serif;
    min-height: 100vh;
    background: linear-gradient(135deg, var(--bg-dark), #1e293b);
    color: var(--text-dark);
    padding: 2rem;
    transition: background 0.4s, color 0.4s;
}
body.light {
    background: linear-gradient(135deg, var(--bg-light), #e2e8f0);
    color: var(--text-light);
}
.dashboard-header {
    display: flex; justify-content: space-between; align-items: center;
    background: var(--card-dark);
    backdrop-filter: var(--blur);
    padding: 1rem 1.5rem;
    border-radius: 16px;
    box-shadow: 0 4px 12px var(--shadow-dark);
    margin-bottom: 2rem;
    transition: background 0.4s, box-shadow 0.4s;
}
body.light .dashboard-header {
    background: var(--card-light);
    box-shadow: 0 4px 12px var(--shadow-light);
}
h1 {
    font-size: 1.8rem;
    display: flex;
    align-items: center;
    gap: 10px;
}
.btn {
    padding: 10px 16px;
    border: none;
    border-radius: 10px;
    font-weight: 600;
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s;
}
.btn:hover { transform: scale(1.05); }
.btn-primary { background: var(--primary); color: white; }
.btn-success { background: var(--success); color: white; }
.btn-danger { background: var(--danger); color: white; }
.btn-icon {
    background: none; border: 1px solid currentColor;
    border-radius: 50%; width: 42px; height: 42px;
    display: flex; align-items: center; justify-content: center;
}
.summary-cards {
    display: grid; gap: 20px;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    margin-bottom: 2rem;
}
.card {
    background: var(--card-dark);
    backdrop-filter: var(--blur);
    padding: 20px;
    border-radius: 16px;
    box-shadow: 0 4px 12px var(--shadow-dark);
    transition: background 0.4s, transform 0.2s;
}
body.light .card {
    background: var(--card-light);
    box-shadow: 0 4px 12px var(--shadow-light);
}
.card:hover { transform: translateY(-4px); }
.summary-value {
    font-size: 2rem;
    font-weight: bold;
    margin-top: 8px;
    color: var(--primary);
}
.content-grid {
    display: grid;
    gap: 20px;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}
.input-field {
    width: 100%;
    padding: 12px;
    border-radius: 10px;
    border: 1px solid rgba(255,255,255,0.2);
    background: rgba(15,23,42,0.5);
    color: inherit;
    margin-bottom: 12px;
    transition: border 0.3s, background 0.3s;
}
body.light .input-field {
    background: rgba(255,255,255,0.5);
    border: 1px solid rgba(0,0,0,0.1);
}
.input-field:focus {
    border-color: var(--primary);
    outline: none;
    box-shadow: 0 0 8px rgba(59,130,246,0.5);
}
.list-container {
    list-style: none;
    max-height: 200px;
    overflow-y: auto;
}
.list-container li {
    background: rgba(255,255,255,0.05);
    padding: 10px;
    border-radius: 8px;
    margin-bottom: 6px;
    display: flex;
    justify-content: space-between;
}
.table-container {
    overflow-x: auto;
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    padding: 12px;
    border-bottom: 1px solid rgba(255,255,255,0.1);
}
th { text-align: left; }
.chart-card { height: 350px; }
</style>
</head>
<body>
<header class="dashboard-header">
    <h1><i class="fas fa-chart-line"></i> Dashboard Avançado</h1>
    <div>
        <button id="toggleTheme" class="btn btn-icon"><i class="fas fa-sun"></i></button>
        <button id="exportCSV" class="btn btn-primary"><i class="fas fa-download"></i> CSV</button>
    </div>
</header>

<main>
    <section class="summary-cards">
        <div class="card"><h3>Total de Vendas</h3><p id="totalSales" class="summary-value">R$ 0,00</p></div>
        <div class="card"><h3>Usuários</h3><p id="totalUsers" class="summary-value">0</p></div>
        <div class="card"><h3>Média por Venda</h3><p id="averageSale" class="summary-value">R$ 0,00</p></div>
    </section>
    <section class="content-grid">
        <div class="card">
            <h2><i class="fas fa-users-cog"></i> Usuários</h2>
            <input type="text" id="userName" class="input-field" placeholder="Nome do usuário">
            <button id="addUserBtn" class="btn btn-success">Adicionar</button>
            <ul id="userList" class="list-container"></ul>
        </div>
        <div class="card">
            <h2><i class="fas fa-cash-register"></i> Registrar Venda</h2>
            <select id="userSelect" class="input-field"></select>
            <input type="number" id="saleAmount" class="input-field" placeholder="Valor da venda (R$)">
            <input type="date" id="saleDate" class="input-field">
            <button id="addSaleBtn" class="btn btn-primary">Adicionar Venda</button>
        </div>
        <div class="card" style="grid-column:1/-1;">
            <h2><i class="fas fa-table"></i> Vendas</h2>
            <div class="table-container">
                <table id="salesTable">
                    <thead><tr><th>Usuário</th><th>Valor</th><th>Data</th><th>Ações</th></tr></thead>
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
const state = {
    users: JSON.parse(localStorage.getItem('users')) || [],
    sales: JSON.parse(localStorage.getItem('sales')) || []
};
const DOM = {
    totalSales: document.getElementById('totalSales'),
    totalUsers: document.getElementById('totalUsers'),
    averageSale: document.getElementById('averageSale'),
    userName: document.getElementById('userName'),
    addUserBtn: document.getElementById('addUserBtn'),
    userList: document.getElementById('userList'),
    userSelect: document.getElementById('userSelect'),
    saleAmount: document.getElementById('saleAmount'),
    saleDate: document.getElementById('saleDate'),
    addSaleBtn: document.getElementById('addSaleBtn'),
    salesTableBody: document.querySelector('#salesTable tbody'),
    toggleTheme: document.getElementById('toggleTheme')
};
function save() {
    localStorage.setItem('users', JSON.stringify(state.users));
    localStorage.setItem('sales', JSON.stringify(state.sales));
}
function renderUsers() {
    DOM.userSelect.innerHTML = '';
    DOM.userList.innerHTML = '';
    state.users.forEach((u,i)=>{
        DOM.userSelect.innerHTML += `<option value="${i}">${u}</option>`;
        DOM.userList.innerHTML += `<li>${u} <button onclick="deleteUser(${i})" class="btn btn-danger btn-sm">Excluir</button></li>`;
    });
    DOM.totalUsers.textContent = state.users.length;
}
function renderSales() {
    DOM.salesTableBody.innerHTML = '';
    let total = 0;
    state.sales.forEach((s,i)=>{
        total += s.value;
        DOM.salesTableBody.innerHTML += `
            <tr>
                <td>${s.user}</td>
                <td>R$ ${s.value.toFixed(2)}</td>
                <td>${s.date}</td>
                <td><button onclick="deleteSale(${i})" class="btn btn-danger btn-sm">Excluir</button></td>
            </tr>`;
    });
    DOM.totalSales.textContent = `R$ ${total.toFixed(2)}`;
    DOM.averageSale.textContent = `R$ ${(total/(state.sales.length||1)).toFixed(2)}`;
    updateCharts();
}
function addUser() {
    if(!DOM.userName.value.trim()) return;
    state.users.push(DOM.userName.value.trim());
    DOM.userName.value = '';
    save();
    renderUsers();
}
function addSale() {
    if(DOM.userSelect.value==='' || !DOM.saleAmount.value) return;
    const sale = {
        user: state.users[DOM.userSelect.value],
        value: parseFloat(DOM.saleAmount.value),
        date: DOM.saleDate.value || new Date().toISOString().split('T')[0]
    };
    state.sales.push(sale);
    DOM.saleAmount.value = '';
    DOM.saleDate.value = '';
    save();
    renderSales();
}
function deleteUser(i) {
    state.users.splice(i,1);
    save();
    renderUsers();
    renderSales();
}
function deleteSale(i) {
    state.sales.splice(i,1);
    save();
    renderSales();
}
let salesChart = new Chart(document.getElementById('salesChart'), {
    type: 'line',
    data: { labels: [], datasets: [{ label:'Vendas', data: [], borderColor: '#3b82f6', backgroundColor:'rgba(59,130,246,0.3)', fill:true }] },
    options: { responsive:true }
});
let pieChart = new Chart(document.getElementById('userPieChart'), {
    type: 'pie',
    data: { labels: [], datasets: [{ data: [], backgroundColor:['#3b82f6','#10b981','#f59e0b','#ef4444','#8b5cf6'] }] }
});
function updateCharts() {
    const byDate={}, byUser={};
    state.sales.forEach(s=>{
        byDate[s.date]=(byDate[s.date]||0)+s.value;
        byUser[s.user]=(byUser[s.user]||0)+s.value;
    });
    salesChart.data.labels = Object.keys(byDate);
    salesChart.data.datasets[0].data = Object.values(byDate);
    pieChart.data.labels = Object.keys(byUser);
    pieChart.data.datasets[0].data = Object.values(byUser);
    salesChart.update(); pieChart.update();
}
DOM.addUserBtn.onclick = addUser;
DOM.addSaleBtn.onclick = addSale;
renderUsers();
renderSales();
DOM.toggleTheme.onclick = ()=>{
    document.body.classList.toggle('light');
    localStorage.setItem('theme', document.body.classList.contains('light')?'light':'dark');
};
if(localStorage.getItem('theme')==='light') document.body.classList.add('light');
</script>
</body>
</html>
