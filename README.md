<!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ultra Hisab App</title><style>
body {
  font-family: Arial;
  margin:0;
  background: linear-gradient(135deg,#1f1c2c,#928dab);
  color:white;
}

.container {
  max-width:420px;
  margin:auto;
  padding:15px;
}

.card {
  background:#ffffff10;
  backdrop-filter: blur(10px);
  padding:20px;
  border-radius:15px;
  position:relative;
}

.menu {
  position:absolute;
  top:10px;
  right:15px;
  font-size:22px;
  cursor:pointer;
}

.dropdown {
  display:none;
  position:absolute;
  top:40px;
  right:10px;
  background:#000;
  padding:8px;
  border-radius:10px;
}

.dropdown input {
  width:100%;
  padding:12px;
  margin:6px 0;
  border:none;
  border-radius:10px;
}
  display:none;
  position:absolute;
  top:40px;
  right:10px;
  background:#000;
  padding:10px;
  border-radius:10px;
}

input, button {
  width:100%;
  padding:20px !important;
  margin:14px 0;
  border:none;
  border-radius:16px;
  font-size:20px;
  box-sizing:border-box;
}

button {
  background:#25D366;
  color:white;
  font-weight:bold;
}

.history {
  margin-top:10px;
  max-height:200px;
  overflow:auto;
  background:#00000030;
  padding:10px;
  border-radius:10px;
}

.hidden { display:none; }
.backBtn { background:red; }

</style></head><body>
<div class="container"><div class="card"><div class="menu" onclick="toggleMenu()">⋮</div><div class="dropdown" id="menuBox">
  <input id="searchPhone" placeholder="Number">
  <button onclick="openHistoryPage()">History Dekho</button>
</div><!-- MAIN PAGE --><div id="mainPage">
<h2>🔥 Hisab App</h2><input id="name" placeholder="Naam">
<input id="work" placeholder="Kaam">
<input id="amount" type="number" placeholder="Paise">
<input id="phone" placeholder="Phone">
<button onclick="sendNow()">Send WhatsApp</button><div>Total: ₹<span id="total">0</span></div>
<div class="history" id="history"></div>
</div><!-- HISTORY PAGE --><div id="historyPage" class="hidden">
<h3>📜 History</h3>
<button class="backBtn" onclick="goBack()">⬅ Back</button>
<div>Total: ₹<span id="historyTotal">0</span></div>
<div class="history" id="historyBox"></div>
</div></div>
</div><script>
let allData = JSON.parse(localStorage.getItem('hisabAllData')) || {};

function toggleMenu(){
  let m=document.getElementById('menuBox');
  m.style.display=m.style.display==='block'?'none':'block';
}

function sendNow(){
  let name=v('name'),work=v('work'),amount=v('amount'),phone=v('phone');

  if(!name||!work||!amount||!phone){alert('Fill all');return;}

  if(!allData[phone]) allData[phone]={history:[],total:0};

  allData[phone].history.push(`${name} - ${work} - ₹${amount}`);
  allData[phone].total+=Number(amount);

  localStorage.setItem('hisabAllData',JSON.stringify(allData));

  render(phone);

  let d=new Date();
  let msg=`Naam:${name}%0AKaam:${work}%0APaise:₹${amount}%0ADate:${d.toLocaleDateString()}%0ATime:${d.toLocaleTimeString()}%0ATotal:₹${allData[phone].total}`;

  window.open(`https://wa.me/${phone}?text=${msg}`,'_blank');
}

function render(phone){
  let box=document.getElementById('history');
  box.innerHTML='';

  if(!allData[phone]) return;

  allData[phone].history.forEach(i=>{
    let d=document.createElement('div');
    d.innerText=i;
    box.appendChild(d);
  });

  document.getElementById('total').innerText=allData[phone].total;
}

function openHistoryPage(){
  let phone=v('searchPhone');
  if(!phone) return alert('Enter number');

  document.getElementById('mainPage').classList.add('hidden');
  document.getElementById('historyPage').classList.remove('hidden');

  let box=document.getElementById('historyBox');
  box.innerHTML='';

  if(!allData[phone]){
    box.innerText='No data';
    return;
  }

  allData[phone].history.forEach(i=>{
    let d=document.createElement('div');
    d.innerText=i;
    box.appendChild(d);
  });

  document.getElementById('historyTotal').innerText=allData[phone].total;
}

function goBack(){
  document.getElementById('historyPage').classList.add('hidden');
  document.getElementById('mainPage').classList.remove('hidden');
}

function v(id){return document.getElementById(id).value.trim();}
</script></body>
</html>
