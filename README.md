<!DOCTYPE html>

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>WhatsApp Work Manager</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gradient-to-br from-purple-700 via-pink-600 to-orange-500 min-h-screen p-4 text-white">  <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-6"><div class="md:col-span-2 bg-white/10 backdrop-blur-xl border border-white/20 rounded-3xl shadow-2xl p-6">

  <div class="flex justify-between items-center mb-6">
    <div>
      <h1 class="text-3xl font-bold">WhatsApp Work Manager</h1>
      <p class="text-white/70 mt-1">Professional Work Tracking System</p>
    </div>

    <div class="relative">
      <button onclick="toggleMenu()"
        class="bg-white/20 text-white px-4 py-2 rounded-xl text-2xl">
        ⋮
      </button>

      <div id="historyMenu"
        class="hidden absolute right-0 top-14 bg-white shadow-2xl rounded-2xl w-64 border z-50 overflow-hidden">

        <div class="p-4 font-bold bg-gray-100 border-b">
          Number Wise History
        </div>

        <div id="numberList" class="max-h-80 overflow-y-auto"></div>
      </div>
    </div>
  </div>

  <div class="space-y-4">

    <div class="relative">
      <button onclick="toggleNameSelector()"
        class="w-full border p-4 rounded-2xl outline-none bg-white text-left flex justify-between items-center">
        <span id="selectedNameText" class="text-gray-700">
          Select Name
        </span>

        <span class="text-2xl">⌄</span>
      </button>

      <div id="nameSelector"
        class="hidden absolute top-16 left-0 w-full bg-white border shadow-2xl rounded-2xl z-50 overflow-hidden">

        <div onclick="selectName('SANAVAJ')"
          class="p-4 border-b cursor-pointer hover:bg-white/10">
          SANAVAJ
        </div>

        <div onclick="selectName('ASHIQ')"
          class="p-4 border-b cursor-pointer hover:bg-white/10">
          ASHIQ
        </div>

        <div onclick="selectName('OVES')"
          class="p-4 border-b cursor-pointer hover:bg-white/10">
          OVES
        </div>

        <div onclick="selectName('TANVEER')"
          class="p-4 cursor-pointer hover:bg-white/10">
          TANVEER
        </div>
      </div>
    </div>

    <div class="relative">
      <button onclick="toggleNumberSelector()"
        class="w-full border p-4 rounded-2xl outline-none bg-white text-left flex justify-between items-center">
        <span id="selectedNumbersText" class="text-gray-700">
          Select WhatsApp Numbers
        </span>

        <span class="text-2xl">⌄</span>
      </button>

      <div id="numberSelector"
        class="hidden absolute top-16 left-0 w-full bg-white border shadow-2xl rounded-2xl z-50 overflow-hidden">

        <label class="flex items-center gap-3 p-4 border-b cursor-pointer hover:bg-white/10">
          <input type="checkbox" value="9588833797" class="phone-checkbox">
          <span>9588833797</span>
        </label>

        <label class="flex items-center gap-3 p-4 border-b cursor-pointer hover:bg-white/10">
          <input type="checkbox" value="8824363410" class="phone-checkbox">
          <span>8824363410</span>
        </label>

        <label class="flex items-center gap-3 p-4 border-b cursor-pointer hover:bg-white/10">
          <input type="checkbox" value="7568617184" class="phone-checkbox">
          <span>7568617184</span>
        </label>

        <label class="flex items-center gap-3 p-4 cursor-pointer hover:bg-white/10">
          <input type="checkbox" value="9530270792" class="phone-checkbox">
          <span>9530270792</span>
        </label>
      </div>
    </div>

    <div class="relative">
      <button onclick="toggleAmountSelector()"
        class="w-full border p-4 rounded-2xl outline-none bg-white text-left flex justify-between items-center">
        <span id="selectedAmountText" class="text-gray-700">
          Select Amount
        </span>

        <span class="text-2xl">⌄</span>
      </button>

      <div id="amountSelector"
        class="hidden absolute top-16 left-0 w-full bg-white border shadow-2xl rounded-2xl z-50 overflow-hidden">

        <div onclick="selectAmount('300')"
          class="p-4 border-b cursor-pointer hover:bg-white/10">
          ₹ 300
        </div>

        <div onclick="selectAmount('400')"
          class="p-4 border-b cursor-pointer hover:bg-white/10">
          ₹ 400
        </div>

        <div onclick="selectAmount('350')"
          class="p-4 border-b cursor-pointer hover:bg-white/10">
          ₹ 350
        </div>

        <div onclick="selectAmount('500')"
          class="p-4 border-b cursor-pointer hover:bg-white/10">
          ₹ 500
        </div>

        <div onclick="selectAmount('600')"
          class="p-4 cursor-pointer hover:bg-white/10">
          ₹ 600
        </div>
      </div>
    </div>

    <textarea id="work"
      placeholder="Enter Work Details"
      class="w-full border border-white/20 bg-white/10 backdrop-blur-md text-white placeholder-white/60 p-4 rounded-2xl h-32 outline-none"></textarea>

    

    <button onclick="saveWork()"
      class="w-full bg-gradient-to-r from-green-400 to-emerald-600 hover:scale-105 transition-all duration-300 text-white shadow-2xl p-4 rounded-2xl text-lg font-bold">
      Save & Send WhatsApp
    </button>
  </div>
</div>

<div class="bg-white/10 backdrop-blur-xl border border-white/20 rounded-3xl shadow-2xl p-6">
  <div class="flex justify-between items-center mb-5">
    <div>
      <h2 class="text-2xl font-bold">History</h2>
      <p class="text-white/70 text-sm">Permanent Saved Records</p>
    </div>

    <button onclick="resetFilter()"
      class="bg-white/20 text-white px-3 py-2 rounded-xl text-sm">
      Reset
    </button>
  </div>

  <div id="historyBox" class="space-y-4 max-h-[700px] overflow-y-auto"></div>

  <div class="mt-5 bg-gradient-to-r from-cyan-400 to-blue-600 text-white p-4 rounded-2xl text-sm font-semibold cursor-pointer" onclick="showAllHistory()">
    📂 Permanent All History
  </div>

  <div class="mt-3 bg-gradient-to-r from-red-500 to-pink-600 text-white p-4 rounded-2xl text-sm font-semibold cursor-pointer" onclick="deleteAllHistory()">
    🗑️ Permanent Delete All History
  </div>

  <div class="mt-3 bg-gradient-to-r from-orange-500 to-red-600 text-white p-4 rounded-2xl text-sm">
    Permanent history protection enabled. Delete option working disabled forever.
  </div>
</div>

  </div><script>

let selectedNumber = null;

function getHistory() {
  return JSON.parse(localStorage.getItem('workHistory')) || [];
}

function saveHistory(data) {
  localStorage.setItem('workHistory', JSON.stringify(data));
}

function toggleAmountSelector() {
  document.getElementById('amountSelector').classList.toggle('hidden');
}

function selectAmount(amount) {
  document.getElementById('selectedAmountText').innerText = `₹ ${amount}`;
  document.getElementById('amountSelector').classList.add('hidden');
}

function toggleNameSelector() {
  document.getElementById('nameSelector').classList.toggle('hidden');
}

function selectName(name) {
  document.getElementById('selectedNameText').innerText = name;
  document.getElementById('nameSelector').classList.add('hidden');
}

function toggleNumberSelector() {
  document.getElementById('numberSelector').classList.toggle('hidden');
}

function toggleMenu() {
  document.getElementById('historyMenu').classList.toggle('hidden');
}

document.addEventListener('change', function () {

  const checked = [...document.querySelectorAll('.phone-checkbox:checked')]
    .map(cb => cb.value);

  document.getElementById('selectedNumbersText').innerText =
    checked.length > 0
      ? checked.join(', ')
      : 'Select WhatsApp Numbers';
});

function saveWork() {

  const name = document.getElementById('selectedNameText').innerText;
  const selectedPhones = [...document.querySelectorAll('.phone-checkbox:checked')].map(cb => cb.value);

  const phone = selectedPhones.join(',');
  const amount = document.getElementById('selectedAmountText').innerText.replace('₹ ', '');
  const work = document.getElementById('work').value;
  const now = new Date();

  const date = now.toLocaleDateString();
  const time = now.toLocaleTimeString();

  if (name === 'Select Name' || selectedPhones.length === 0 || amount === 'Select Amount' || !work) {
    alert('Please fill all details');
    return;
  }

  const history = getHistory();

  const mainPhone = phone.split(',')[0].trim();

  const entry = {
    id: Date.now(),
    name,
    phone: mainPhone,
    work,
    date,
    time,
    amount,
    createdAt: new Date().toLocaleString()
  };

  history.unshift(entry);

  saveHistory(history);

  const phoneList = phone.split(',').map(num => num.trim());

  const userHistory = history.filter(item => phoneList.includes(item.phone));

  const historyText = userHistory.map((item, index) =>
    `${index + 1}. Name: ${item.name}
Amount: ₹${item.amount}
Work: ${item.work}\nDate: ${item.date}\nTime: ${item.time}`
  ).join('\n\n----------------\n\n');

  const historyLink = `${window.location.origin}${window.location.pathname}?history=${mainPhone}`;

  const message = `Hello ${name}

Your work saved successfully.

Complete History:

${historyText}

👇 CLICK HISTORY LINK 👇

${historyLink}`;

  phoneList.forEach(number => {
    window.open(`https://wa.me/91${number}?text=${encodeURIComponent(message)}`, '_blank');
  });

  document.getElementById('selectedNameText').innerText = 'Select Name';
  document.querySelectorAll('.phone-checkbox').forEach(cb => cb.checked = false);
  document.getElementById('selectedNumbersText').innerText = 'Select WhatsApp Numbers';
  document.getElementById('selectedAmountText').innerText = 'Select Amount';
  document.getElementById('work').value = '';
  

  openHistoryFromURL();



renderHistory();
renderNumbers();
}

function renderNumbers() {

  const history = getHistory();
  const numbers = [...new Set(history.map(item => item.phone))];

  const numberList = document.getElementById('numberList');

  numberList.innerHTML = '';

  if (numbers.length === 0) {
    numberList.innerHTML = '<div class="p-4 text-white/70">No History</div>';
    return;
  }

  numbers.forEach(number => {

    const btn = document.createElement('button');

    btn.className = 'w-full text-left p-4 border-b hover:bg-gray-100';

    btn.innerHTML = `
      <div class="font-bold">${number}</div>
      <div class="text-sm text-white/70">View History</div>
    `;

    btn.onclick = () => {
      selectedNumber = number;
      renderHistory();
      toggleMenu();
    };

    numberList.appendChild(btn);
  });
}

function openHistoryFromURL() {

  const params = new URLSearchParams(window.location.search);
  const historyNumber = params.get('history');

  if (historyNumber) {
    selectedNumber = historyNumber;
  }
}

function renderHistory() {

  const historyBox = document.getElementById('historyBox');
  const history = getHistory();

  const filtered = selectedNumber
    ? history.filter(item => item.phone === selectedNumber)
    : history;

  historyBox.innerHTML = '';

  if (filtered.length === 0) {
    historyBox.innerHTML = '<div class="text-center text-white/70 py-10">No History Found</div>';
    return;
  }

  filtered.forEach(item => {

    const card = document.createElement('div');

    card.className = 'bg-white/10 backdrop-blur-md border border-white/20 rounded-3xl p-5 shadow-xl';

    card.innerHTML = `
      <div class="flex justify-between items-start mb-3">
        <div>
          <h3 class="font-bold text-lg">${item.name}</h3>
          <p class="text-white/70 text-sm">${item.phone}</p>
        </div>

        <div class="bg-white border px-3 py-1 rounded-full text-xs">
          ${item.date}
        </div>
      </div>

      <div class="mb-3 inline-block bg-gradient-to-r from-yellow-400 to-orange-500 text-white px-4 py-2 rounded-full text-sm font-bold">
        ₹ ${item.amount}
      </div>

      <div class="bg-black/20 backdrop-blur-md p-4 rounded-2xl border border-white/10 text-sm leading-6 text-white">
        ${item.work}
      </div>

      <div class="flex justify-between mt-4 text-xs text-white/70">
        <span>${item.time}</span>
        <span>${item.createdAt}</span>
      </div>
    `;

    historyBox.appendChild(card);
  });
}



function showAllHistory() {
  selectedNumber = null;
  renderHistory();
}

function deleteAllHistory() {

  const confirmDelete = confirm('Are you sure you want to permanently delete all history?');

  if (!confirmDelete) {
    return;
  }

  localStorage.removeItem('workHistory');

  selectedNumber = null;

  renderHistory();
  renderNumbers();

  alert('All history deleted permanently');
}

function resetFilter() {
  selectedNumber = null;
  renderHistory();
}

renderHistory();
renderNumbers();

</script></body>
</html>
