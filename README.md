<!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<title>Ultra Hisab WhatsApp</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0"><style>
body {
  font-family: Arial;
  background: linear-gradient(135deg,#1f1c2c,#928dab);
  padding:20px;
  color:white;
}

.container {
  max-width:420px;
  margin:auto;
  background:#ffffff10;
  backdrop-filter: blur(10px);
  padding:20px;
  border-radius:20px;
  position:relative;
}

.menu {
  position:absolute;
  top:10px;
  right:15px;
  cursor:pointer;
  font-size:20px;
}

.dropdown {
  display:none;
  position:absolute;
  top:40px;
  right:10px;
  background:#000;
  border-radius:10px;
  padding:10px;
}

.hidden { display:none; }

input, button {
  width:100%;
  padding:12px;
  margin:8px 0;
  border:none;
  border-radius:10px;
}

button {
  background:#25D366;
  color:white;
}

.history {
  margin-top:20px;
  background:#00000030;
  padding:10px;
  border-radius:10px;
  max-height:250px;
  overflow:auto;
}

.entry { font-size:13px; margin:5px 0; }
.total { text-align:center; margin-top:10px; }

.backBtn {
  background:#ff4757;
}

</style></head><body>
<div class="container"><div class="menu" onclick="toggleMenu()">⋮</div><div class="dropdown" id="menuBox">
  <input type="number" id="searchPhone" placeholder="Number daalo">
  <button onclick="openHistoryPage()">History Dekho</button>
</div><!-- MAIN PAGE --><div id="mainPage">
  <h1>🔥 Ultra Hisab</h1>  <input type="text" id="name" placeholder="Naam">
  <input type="text" id="work" placeholder="Kaam">
  <input type="number" id="amount" placeholder="Paise ₹">
  <input type="number" id="phone" placeholder="Phone (91xxxxxxxxxx)" oninput="loadHistoryByPhone()"><button onclick="sendNow()">Send WhatsApp 🚀</button>

  <div class="total">Total: ₹<span id="total">0</span></div>  <div class="history" id="history"></div>
</div><!-- HISTORY PAGE --><div id="historyPage" class="hidden">
  <h2>📜 Full History</h2>
  <button class="backBtn" onclick="goBack()">⬅ Back</button>
  <div class="total">Total: ₹<span id="historyTotal">0</span></div>
  <div class="history" id="historyBox"></div>
</div></div><script>
let allData = {};

function toggleMenu() {
  const menu = document.getElementById('menuBox');
  menu.style.display = menu.style.display === 'block' ? 'none' : 'block';
}

function openHistoryPage() {
  const phone = val('searchPhone');
  if (!phone) return alert('Number daalo');

  document.getElementById('menuBox').style.display = 'none';

  document.getElementById('mainPage').classList.add('hidden');
  document.getElementById('historyPage').classList.remove('hidden');

  showFullHistory(phone);
}

function goBack() {
  document.getElementById('historyPage').classList.add('hidden');
  document.getElementById('mainPage').classList.remove('hidden');
}

function showFullHistory(phone) {
  const box = document.getElementById('historyBox');
  box.innerHTML = '';

  if (!allData[phone]) {
    box.innerHTML = 'No history found';
    document.getElementById('historyTotal').innerText = 0;
    return;
  }

  allData[phone].history.forEach(item => {
    const div = document.createElement('div');
    div.className = 'entry';
    div.innerText = item;
    box.appendChild(div);
  });

  document.getElementById('historyTotal').innerText = allData[phone].total;
}

function sendNow() {
  const name = val('name');
  const work = val('work');
  const amount = val('amount');
  const phone = val('phone');

  if (!name || !work || !amount || !phone) {
    alert('Sab fill karo');
    return;
  }

  const now = new Date();
  const date = now.toLocaleDateString();
  const time = now.toLocaleTimeString();

  if (!allData[phone]) allData[phone] = { history: [], total: 0 };

  allData[phone].history.push(`${name} - ${work} - ₹${amount}`);
  allData[phone].total += Number(amount);

  renderHistory(phone);
  saveData();

  const message = `🔥 HISAB 🔥%0A%0ANaam: ${name}%0AKaam: ${work}%0APaise: ₹${amount}%0ADate: ${date}%0ATime: ${time}%0A%0ATotal: ₹${allData[phone].total}`;

  window.open(`https://wa.me/${phone}?text=${message}`, '_blank');
}

function renderHistory(phone) {
  const box = document.getElementById('history');
  box.innerHTML = '';

  if (!allData[phone]) {
    box.innerHTML = 'No history';
    document.getElementById('total').innerText = 0;
    return;
  }

  allData[phone].history.forEach(item => {
    const div = document.createElement('div');
    div.className = 'entry';
    div.innerText = item;
    box.appendChild(div);
  });

  document.getElementById('total').innerText = allData[phone].total;
}

function loadHistoryByPhone() {
  const phone = val('phone');
  renderHistory(phone);
}

function saveData() {
  localStorage.setItem('hisabAllData', JSON.stringify(allData));
}

function loadData() {
  allData = JSON.parse(localStorage.getItem('hisabAllData')) || {};
}

function val(id){return document.getElementById(id).value.trim();}

loadData();
</script></body>
</html>
