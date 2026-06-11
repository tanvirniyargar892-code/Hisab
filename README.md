<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kaam Hisab WhatsApp Scheduler</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial,sans-serif;
}

body{
background:#f2f2f2;
padding:20px;
}

.container{
max-width:500px;
margin:auto;
background:#fff;
padding:20px;
border-radius:12px;
box-shadow:0 0 10px rgba(0,0,0,.1);
}

h2{
text-align:center;
margin-bottom:20px;
color:#25D366;
}

label{
font-weight:bold;
display:block;
margin-top:10px;
}

input{
width:100%;
padding:12px;
margin-top:5px;
border:1px solid #ccc;
border-radius:8px;
}

button{
width:100%;
padding:14px;
border:none;
border-radius:8px;
margin-top:15px;
font-size:16px;
cursor:pointer;
}

.saveBtn{
background:#007bff;
color:white;
}

.whatsappBtn{
background:#25D366;
color:white;
}

.scheduleBtn{
background:#ff9800;
color:white;
}

#status{
margin-top:15px;
font-weight:bold;
text-align:center;
color:green;
}

table{
width:100%;
margin-top:20px;
border-collapse:collapse;
}

table th,
table td{
border:1px solid #ddd;
padding:8px;
text-align:center;
}

table th{
background:#25D366;
color:white;
}
</style>
</head>

<body>

<div class="container">

<h2>Kaam Hisab WhatsApp Scheduler</h2>

<label>Naam</label>
<input type="text" id="name" placeholder="Naam">

<label>Mobile Number</label>
<input type="tel" id="mobile" placeholder="Mobile Number">

<label>Paise (₹)</label>
<input type="text" id="paise" placeholder="Paise">

<label>Kaam Ka Naam</label>
<input type="text" id="work" placeholder="Kaam Ka Naam">

<label>Tarikh</label>
<input type="text" id="date" readonly>

<label>Schedule Date & Time</label>
<input type="datetime-local" id="scheduleTime">

<button class="saveBtn" onclick="saveData()">
Save Record
</button>

<button class="scheduleBtn" onclick="scheduleMessage()">
Schedule WhatsApp
</button>

<button class="whatsappBtn" onclick="sendNow()">
Send WhatsApp Now
</button>

<div id="status"></div>

<table id="recordsTable">
<tr>
<th>Naam</th>
<th>Mobile</th>
<th>Paise</th>
<th>Kaam</th>
</tr>
</table>

</div>

<script>

document.getElementById("date").value =
new Date().toLocaleDateString("hi-IN");

function getMessage(){

let name=document.getElementById("name").value;
let amount=document.getElementById("paise").value;
let work=document.getElementById("work").value;
let date=document.getElementById("date").value;

return `Namaste ${name},

Kaam: ${work}

Rakam: ₹${amount}

Tarikh: ${date}

Dhanyavaad`;
}

function sendNow(){

let mobile=document.getElementById("mobile").value.trim();

if(!mobile){
alert("Mobile Number Daaliye");
return;
}

let url =
"https://wa.me/91" + mobile +
"?text=" + encodeURIComponent(getMessage());

window.location.href = url;
}

function scheduleMessage(){

let scheduleInput =
document.getElementById("scheduleTime").value;

if(!scheduleInput){
alert("Schedule Time Select Karein");
return;
}

let scheduleDate = new Date(scheduleInput);
let now = new Date();

let delay = scheduleDate - now;

if(delay <= 0){
alert("Future Time Select Karein");
return;
}

document.getElementById("status").innerHTML =
"Schedule Save Ho Gaya";

setTimeout(function(){

let mobile =
document.getElementById("mobile").value.trim();

if(!mobile){
alert("Mobile Number Daaliye");
return;
}

let url =
"https://wa.me/91" + mobile +
"?text=" + encodeURIComponent(getMessage());

window.location.href = url;

}, delay);
}

function saveData(){

let name=document.getElementById("name").value;
let mobile=document.getElementById("mobile").value;
let amount=document.getElementById("paise").value;
let work=document.getElementById("work").value;

let table=document.getElementById("recordsTable");

let row=table.insertRow(-1);

row.insertCell(0).innerHTML=name;
row.insertCell(1).innerHTML=mobile;
row.insertCell(2).innerHTML="₹"+amount;
row.insertCell(3).innerHTML=work;

document.getElementById("status").innerHTML =
"Record Save Ho Gaya";
}

</script>

</body>
</html>
function scheduleMessage(){

let scheduleInput=
document.getElementById("scheduleTime").value;

if(!scheduleInput){
alert("Schedule Time Select Karein");
return;
}

let scheduleDate=new Date(scheduleInput);
let now=new Date();

let delay=scheduleDate-now;

if(delay<=0){
alert("Future Time Select Karein");
return;
}

document.getElementById("status").innerHTML=
"Schedule Save Ho Gaya";

setTimeout(function(){

let mobile=
document.getElementById("mobile").value;

let url=
`https://wa.me/91${mobile}?text=${encodeURIComponent(getMessage())}`;

window.open(url,"_blank");

},delay);

}

function saveData(){

let name=document.getElementById("name").value;
let mobile=document.getElementById("mobile").value;
let amount=document.getElementById("amount").value;
let work=document.getElementById("work").value;

let table=
document.getElementById("recordsTable");

let row=table.insertRow(-1);

row.insertCell(0).innerHTML=name;
row.insertCell(1).innerHTML=mobile;
row.insertCell(2).innerHTML="₹"+amount;
row.insertCell(3).innerHTML=work;

document.getElementById("status").innerHTML=
"Record Save Ho Gaya";
}

</script>

</body>
</html>
