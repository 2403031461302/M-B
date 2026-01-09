<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title> M B Finance </title>
<style>
  
  :root{
    --green-600:#27ae60;
    --green-500:#2ecc71;
    --green-400:#58d68d;
    --muted:#f5f5f5;
    --panel:#ffffff;
    --border:#dcdcdc;
  }

  /* Page */
  body{
    
    margin:0;
    padding:20px;
    background:    font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size:17px;
    -webkit-font-smoothing:antialiased;
  }
  .container{
    position:relative;
    max-width:900px;
    margin:0 auto;
    background:var(--panel);
    padding:20px;
    border-radius:8px;
    box-shadow:0 6px 18px rgba(0,0,0,0.06);
  }

  h1{
    margin:0 0 16px;
    text-align:center;
    font-family:Georgia, 'Times New Roman', serif;
    color:#21323a;
    font-size:2.2rem;
  }
  h1 .finance{
    display:block;
    font-size:2.8rem;
    color:#e67e22;
    font-weight:800;
    letter-spacing:1px;
  }

  /* Top-right menu icon */
  .menu-icon{
    position:absolute;
    top:16px;
    right:18px;
    cursor:pointer;
    user-select:none;
    font-size:20px;
    padding:6px;
    border-radius:6px;
    background:var(--green-500);
    color:#fff;
  }
  .menu-icon:hover{ background:var(--green-600); }

  .menu-popup{
    position:absolute;
    top:52px;
    right:18px;
    display:none;
    width:180px;
    background:linear-gradient(0deg, rgba(255,255,255,0.98), rgba(255,255,255,0.98));
    border-radius:8px;
    border:1px solid var(--border);
    box-shadow:0 8px 24px rgba(0,0,0,0.12);
    z-index:200;
  }
  .menu-popup button{
    display:block;
    width:100%;
    padding:10px 12px;
    border:none;
    background:transparent;
    text-align:left;
    cursor:pointer;
    font-size:0.97rem;
  }
  .menu-popup button:hover{ background:#f0fff3; }

  /* Form */
  form{
    display:flex;
    flex-wrap:wrap;
    gap:10px;
    margin-bottom:12px;
  }
  input, button{
    padding:12px;
    border-radius:6px;
    border:1px solid var(--border);
    font-size:17px;
    box-sizing:border-box;
  }
  input[type="date"], input[type="text"], input[type="number"]{
    flex:1 1 150px;
  }
  button.primary{
    background:var(--green-500);
    color:#fff;
    border:none;
    cursor:pointer;
    flex:1 1 100px;
  }
  button.primary:hover{ background:var(--green-600); }
 backdrop-filter: blur(14px);

  /* Table */
  table{
    width:100%;
    border-collapse:collapse;
    margin-top:6px;
    font-size:17px;
  }
  th, td{
    padding:10px;
    border:1px solid var(--border);
    text-align:right;
    vertical-align:middle;
  }
  th{ background:#fafafa; text-align:center; font-size:18px; }
  td.description{ text-align:left; }

  td.total-pos{ color:green; font-weight:700; }
  td.total-neg{ color:red; font-weight:700; }

  #summary-bar{
    margin-top:12px;
    text-align:right;
    font-weight:700;
    color:#21323a;
    font-size:1.05rem;
  }

  /* action-menu (per row) same style */
  .action-menu{ position:relative; display:inline-block; }
  .action-menu-content{
    display:none;
    position:absolute;
    right:0;
    background:#fff;
    border:1px solid var(--border);
    border-radius:6px;
    box-shadow:0 6px 20px rgba(0,0,0,0.08);
    z-index:50;
    min-width:120px;
    overflow:hidden;
  }
  .action-menu-content button{
    display:block;
    width:100%;
    padding:10px;
    border:none;
    background:transparent;
    text-align:left;
    cursor:pointer;
    font-size:15px;
  }
  .action-menu-content button:hover{ background:#f6fff6; }
  .action-menu:hover .action-menu-content{ display:block; }

  /* centered popups (draggable) */
  .popup-centered{
    position:fixed;
    left:50%;
    top:50%;
    transform:translate(-50%,-50%);
    background:#fff;
    border:1px solid var(--border);
    border-radius:8px;
    padding:14px;
    box-shadow:0 18px 40px rgba(0,0,0,0.18);
    display:none;
    z-index:500;
    width:320px;
    max-width:calc(100% - 40px);
    cursor:default;
  }

  .popup-header{ font-weight:700; margin-bottom:8px; display:flex; justify-content:space-between; align-items:center; cursor:move; }
  .popup-close{ cursor:pointer; border:none; background:transparent; font-size:16px; }

  /* Calculator (bottom-right initial) */
  .calc-box{
    position:fixed;
    left:50%;
    top:50%;
    transform:translate(-50%,-50%);
    width:250px;
    background:#fff;
    border:1px solid var(--border);
    border-radius:10px;
    padding:12px;
    box-shadow:0 18px 40px rgba(0,0,0,0.16);
    z-index:600;
    display:none;
    cursor:default;
  }
  .calc-header{ display:flex; justify-content:space-between; align-items:center; margin-bottom:8px; font-weight:700; cursor:move; }
  .calc-display{
    width:100%;
    height:44px;
    border-radius:6px;
    border:1px solid #bbb;
    margin-bottom:10px;
    padding:8px 10px;
    text-align:right;
    font-size:1.15rem;
    background:#fafafa;
    box-sizing:border-box;
    white-space:nowrap;
    overflow:hidden;
    text-overflow:ellipsis;
  }
  .calc-grid{ display:grid; grid-template-columns:repeat(4,1fr); gap:8px; }
  .calc-btn{ padding:10px; border-radius:6px; border:1px solid #d0d0d0; background:#f2f6f2; cursor:pointer; font-size:1rem; }
  .calc-btn.op{ background:var(--green-400); color:#fff; font-weight:700; }

  /* Recently deleted (centered popup) */
  .deleted-list{ max-height:320px; overflow:auto; padding-right:6px; }
  .deleted-item{ padding:8px; border-bottom:1px solid #eee; font-size:0.95rem; }
  .deleted-item .restore-btn{ margin-top:8px; display:inline-block; padding:6px 8px; border-radius:6px; border:none; background:var(--green-500); color:white; cursor:pointer; font-size:0.9rem; }
  .clear-deleted{ display:block; width:100%; margin-top:8px; padding:8px; border-radius:6px; border:none; background:#e74c3c; color:white; cursor:pointer; font-size:0.95rem; }

  /* small responsive */
  @media (max-width:520px){
    .calc-box{ right:12px; left:12px; width:auto; }
    .popup-centered{ width:92%; }
  }
</style>
</head>
<body>

<div class="container">
  <div class="menu-icon" id="topMenuBtn" title="Menu">⋮</div>

  <div class="menu-popup" id="menuPopup">
    <button id="openCalcBtn">Calculator</button>
    <button id="openDeletedBtn">Recently Deleted</button>
  </div>

  <h1>M B <span class="finance">Finance</span></h1>

  <form id="transaction-form" autocomplete="off">
    <input type="date" id="date" required />
    <input type="text" id="description" placeholder="Names" required />
    <input type="number" id="income" placeholder="Amount (₹)" min="0" step="0.01" />
    <input type="number" id="interest" placeholder="Interest (₹)" min="0" step="0.01" />
    <input type="number" id="expense" placeholder="Returns (₹)" min="0" step="0.01" />
    <input type="number" id="days" placeholder="Days" min="0" step="1" />
    <button class="primary" type="submit">Add</button>
  </form>

  <table>
    <thead>
      <tr>
        <th>Date</th>
        <th>Names</th>
        <th>Amount (₹)</th>
        <th>Interest (₹)</th>
        <th>Returns (₹)</th>
        <th>Total (₹)</th>
        <th>Days</th>
        <th>Options</th>
      </tr>
    </thead>
    <tbody id="transaction-list"></tbody>
  </table>

  <div id="summary-bar"></div>
</div>

<!-- Calculator box (starts bottom-right) -->
<div class="calc-box" id="calcBox" aria-hidden="true">
  <div class="calc-header" id="calcHeader">
    <div>Calculator</div>
    <button class="popup-close" id="closeCalcBtn" title="Close">✖</button>
  </div>
  <div id="calcDisplay" class="calc-display">0</div>
  <div class="calc-grid" id="calcGrid">
    <button class="calc-btn">7</button>
    <button class="calc-btn">8</button>
    <button class="calc-btn">9</button>
    <button class="calc-btn op">÷</button>

    <button class="calc-btn">4</button>
    <button class="calc-btn">5</button>
    <button class="calc-btn">6</button>
    <button class="calc-btn op">×</button>

    <button class="calc-btn">1</button>
    <button class="calc-btn">2</button>
    <button class="calc-btn">3</button>
    <button class="calc-btn op">−</button>

    <button class="calc-btn">0</button>
    <button class="calc-btn" id="calcClear">C</button>
    <button class="calc-btn" id="calcEquals">=</button>
    <button class="calc-btn op">+</button>
  </div>
</div>

<!-- Recently Deleted centered popup (draggable too) -->
<div class="popup-centered" id="deletedBox" aria-hidden="true">
  <div class="popup-header" id="deletedHeader">
    <div>Recently Deleted</div>
    <button class="popup-close" id="closeDeletedBtn" title="Close">✖</button>
  </div>
  <div class="deleted-list" id="deletedList"></div>
  <button class="clear-deleted" id="clearDeletedBtn">Clear All Deleted Items</button>
</div>

<script>
/* ---------------- refs ---------------- */
const topMenuBtn = document.getElementById('topMenuBtn');
const menuPopup = document.getElementById('menuPopup');
const openCalcBtn = document.getElementById('openCalcBtn');
const openDeletedBtn = document.getElementById('openDeletedBtn');

const calcBox = document.getElementById('calcBox');
const calcHeader = document.getElementById('calcHeader');
const calcDisplay = document.getElementById('calcDisplay');
const calcGrid = document.getElementById('calcGrid');
const calcClear = document.getElementById('calcClear');
const calcEquals = document.getElementById('calcEquals');
const closeCalcBtn = document.getElementById('closeCalcBtn');

const deletedBox = document.getElementById('deletedBox');
const deletedList = document.getElementById('deletedList');
const deletedHeader = document.getElementById('deletedHeader');
const closeDeletedBtn = document.getElementById('closeDeletedBtn');
const clearDeletedBtn = document.getElementById('clearDeletedBtn');

const form = document.getElementById('transaction-form');
const dateInput = document.getElementById('date');
const descriptionInput = document.getElementById('description');
const incomeInput = document.getElementById('income');
const interestInput = document.getElementById('interest');
const expenseInput = document.getElementById('expense');
const daysInput = document.getElementById('days');
const transactionList = document.getElementById('transaction-list');
const summaryBar = document.getElementById('summary-bar');

/* ---------------- data ---------------- */
let transactions = JSON.parse(localStorage.getItem('transactions')) || [];
let deletedItems = JSON.parse(localStorage.getItem('deletedItems')) || [];
let editId = null;

function saveAll(){
  localStorage.setItem('transactions', JSON.stringify(transactions));
  localStorage.setItem('deletedItems', JSON.stringify(deletedItems));
}

/* ---------------- utilities ---------------- */
function formatDateIsoToDmy(d){
  if(!d) return '';
  const [y,m,day] = d.split('-');
  return `${day}-${m}-${y}`;
}
function escapeHtml(s){
  if(s==null) return '';
  return String(s).replace(/[&<>"'`]/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;','`':'&#96;'}[c]));
}

/* ---------------- render ---------------- */
function renderTransactions(){
  transactions.sort((a,b) => new Date(b.date) - new Date(a.date));
  transactionList.innerHTML = '';
  let sumIncome=0, sumInterest=0, sumNet=0;

  transactions.forEach(t=>{
    const income = Number(t.income)||0;
    const interest = Number(t.interest)||0;
    const expense = Number(t.expense)||0;
    const total = income + interest - expense;

    sumIncome += income;
    sumInterest += interest;
    sumNet += total;

    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${formatDateIsoToDmy(t.date)}</td>
      <td class="description">${escapeHtml(t.description)}</td>
      <td>${income.toFixed(2)}</td>
      <td>${interest.toFixed(2)}</td>
      <td>${expense.toFixed(2)}</td>
      <td class="${total>=0? 'total-pos':'total-neg'}">${total.toFixed(2)}</td>
      <td>${t.days}</td>
      <td>
        <div class="action-menu">
          <button style="cursor:pointer;">⋮</button
>
          <div class="action-menu-content">
            <button onclick="handleEdit(${t.id})">Edit</button>
            <button onclick="handleDelete(${t.id})">Delete</button>
          </div>
        </div>
      </td>
    `;
    transactionList.appendChild(tr);
  });

  summaryBar.textContent = `Total Income: ₹${sumIncome.toFixed(2)} | Total Interest: ₹${sumInterest.toFixed(2)} | Total Amount: ₹${sumNet.toFixed(2)}`;
}

/* ---------------- CRUD ---------------- */
function handleDelete(id){
  const idx = transactions.findIndex(x=>x.id===id);
  if(idx===-1) return;
  const item = transactions.splice(idx,1)[0];
  deletedItems.push(item);
  saveAll();
  renderTransactions();
}
function handleEdit(id){
  const item = transactions.find(x=>x.id===id);
  if(!item) return;
  dateInput.value = item.date;
  descriptionInput.value = item.description;
  incomeInput.value = item.income;
  interestInput.value = item.interest;
  expenseInput.value = item.expense;
  daysInput.value = item.days;
  editId = id;
}
form.addEventListener('submit', e=>{
  e.preventDefault();
  const data = {
    id: editId ?? Date.now(),
    date: dateInput.value,
    description: descriptionInput.value.trim(),
    income: Number(incomeInput.value) || 0,
    interest: Number(interestInput.value) || 0,
    expense: Number(expenseInput.value) || 0,
    days: Number(daysInput.value) || 0
  };
  if(editId){
    transactions = transactions.map(t=> t.id===editId ? data : t);
    editId = null;
  } else {
    transactions.push(data);
  }
  saveAll();
  renderTransactions();
  form.reset();
  setDefaultDate();
});
function setDefaultDate(){
  const today = new Date().toISOString().slice(0,10);
  if(!dateInput.value) dateInput.value = today;
}
setDefaultDate();

/* ---------------- Recently Deleted UI ---------------- */
function openDeletedPopup(){
  deletedList.innerHTML = '';
  if(deletedItems.length===0){
    deletedList.innerHTML = '<div style="padding:8px;color:#666">No deleted items</div>';
  } else {
    deletedItems.forEach((item,idx)=>{
      const income = Number(item.income)||0;
      const interest = Number(item.interest)||0;
      const expense = Number(item.expense)||0;
      const total = income + interest - expense;

      const div = document.createElement('div');
      div.className = 'deleted-item';
      div.innerHTML = `
        <div><strong>Name:</strong> ${escapeHtml(item.description)}</div>
        <div><strong>Date:</strong> ${formatDateIsoToDmy(item.date)}</div>
        <div><strong>Amount:</strong> ₹${income.toFixed(2)}</div>
        <div><strong>Interest:</strong> ₹${interest.toFixed(2)}</div>
        <div><strong>Returns:</strong> ₹${expense.toFixed(2)}</div>
        <div><strong>Total:</strong> ₹${total.toFixed(2)}</div>
        <div><strong>Days:</strong> ${item.days}</div>
      `;
      const btn = document.createElement('button');
      btn.className = 'restore-btn';
      btn.textContent = 'Restore';
      btn.onclick = () => {
        const restored = deletedItems.splice(idx,1)[0];
        transactions.push(restored);
        saveAll();
        renderTransactions();
        openDeletedPopup();
      };
      div.appendChild(btn);
      deletedList.appendChild(div);
    });
  }
  deletedBox.style.display = 'block';
}
function clearAllDeleted(){
  if(!confirm('Clear all deleted items?')) return;
  deletedItems = [];
  saveAll();
  openDeletedPopup();
}

/* ---------------- Menu & popups behavior ---------------- */
topMenuBtn.addEventListener('click', e=>{
  e.stopPropagation();
  const shown = menuPopup.style.display === 'block';
  hideAll();
  menuPopup.style.display = shown ? 'none' : 'block';
});
openCalcBtn.addEventListener('click', e=>{
  e.stopPropagation();
  menuPopup.style.display = 'none';
  calcBox.style.display = 'block';
  deletedBox.style.display = 'none';
});
openDeletedBtn.addEventListener('click', e=>{
  e.stopPropagation();
  menuPopup.style.display = 'none';
  openDeletedPopup();
  calcBox.style.display = 'none';
});

document.addEventListener('click', e=>{
  if(!e.target.closest('.menu-popup') && !e.target.closest('.menu-icon')){
    menuPopup.style.display = 'none';
  }
  // click outside closes centered popup and calc if click outside
  if(!e.target.closest('.calc-box') && !e.target.closest('.popup-centered') && !e.target.closest('.menu-popup') && !e.target.closest('.menu-icon')){
    // don't auto-close calc if user dragged it or positioned it; but we'll close it on outside click to keep behavior consistent
    calcBox.style.display = 'none';
    deletedBox.style.display = 'none';
  }
});

// close buttons
closeCalcBtn.addEventListener('click', ()=> calcBox.style.display='none');
closeDeletedBtn.addEventListener('click', ()=> deletedBox.style.display='none');
clearDeletedBtn.addEventListener('click', clearAllDeleted);

/* ---------------- Calculator logic ---------------- */
let calcExpr = '';
function updateCalcUI(){
  if(calcExpr.length > 30) {
    calcDisplay.textContent = '...' + calcExpr.slice(-30);
  } else {
    calcDisplay.textContent = calcExpr || '0';
  }
}
calcGrid.addEventListener('click', (e)=>{
  const btn = e.target;
  if(!btn.classList.contains('calc-btn')) return;
  const v = btn.textContent.trim();
  if(v === 'C'){ calcExpr=''; updateCalcUI(); return; }
  if(v === '='){ evaluateCalc(); return; }
  // append as symbol (buttons show ÷ × − +)
  calcExpr += v;
  updateCalcUI();
});
calcClear.addEventListener('click', ()=>{ calcExpr=''; updateCalcUI(); });
calcEquals.addEventListener('click', evaluateCalc);

function evaluateCalc(){
  if(!calcExpr) return;
  // map symbols to JS ops
  let expr = calcExpr.replace(/×/g,'*').replace(/÷/g,'/').replace(/−/g,'-');
  if(!/^[0-9+\-*/().\s]+$/.test(expr)){
    calcDisplay.textContent = 'Error';
    calcExpr = '';
    return;
  }
  try{
    const result = Function('"use strict";return (' + expr + ')')();
    calcExpr = String(Number(result));
    updateCalcUI();
  }catch(err){
    calcDisplay.textContent = 'Error';
    calcExpr = '';
  }
}
// keyboard for calc when open
document.addEventListener('keydown', (e)=>{
  if(calcBox.style.display !== 'block') return;
  const k = e.key;
  if((k>='0' && k<='9') || k === '.') { calcExpr += k; updateCalcUI(); }
  else if(k === '+' || k === '-') { calcExpr += (k==='-'? '−' : '+'); updateCalcUI(); }
  else if(k === '*' ) { calcExpr += '×'; updateCalcUI(); }
  else if(k === '/') { calcExpr += '÷'; updateCalcUI(); }
  else if(k === 'Enter'){ e.preventDefault(); evaluateCalc(); }
  else if(k === 'Backspace'){ calcExpr = calcExpr.slice(0,-1); updateCalcUI(); }
});

/* ---------------- Draggable behavior for calculator and deleted popups ---------------- */
// generic draggable helper: make element draggable by its header element
function makeDraggable(dragHandle, dragElement) {
  let isDown = false;
  let startX = 0, startY = 0, origX = 0, origY = 0;

  dragHandle.addEventListener('mousedown', (ev) => {
    ev.preventDefault();
    isDown = true;
    startX = ev.clientX;
    startY = ev.clientY;
    // get current position; if element is centered via transform, compute left/top
    const rect = dragElement.getBoundingClientRect();
    origX = rect.left;
    origY = rect.top;
    // set fixed positioning so we can move
    dragElement.style.left = origX + 'px';
    dragElement.style.top = origY + 'px';
    dragElement.style.transform = 'none';
    dragElement.style.position = 'fixed';
    dragElement.style.zIndex = 9999;
    document.body.style.userSelect = 'none';
  });

  document.addEventListener('mousemove', (ev) => {
    if(!isDown) return;
    const dx = ev.clientX - startX;
    const dy = ev.clientY - startY;
    dragElement.style.left = (origX + dx) + 'px';
    dragElement.style.top = (origY + dy) + 'px';
  });

  document.addEventListener('mouseup', () => {
    if(isDown){
      isDown = false;
      document.body.style.userSelect = '';
    }
  });

  // touch support
  dragHandle.addEventListener('touchstart', (ev)=>{
    const t = ev.touches[0];
    isDown = true;
    startX = t.clientX; startY = t.clientY;
    const rect = dragElement.getBoundingClientRect();
    origX = rect.left; origY = rect.top;
    dragElement.style.left = origX + 'px';
    dragElement.style.top = origY + 'px';
    dragElement.style.transform = 'none';
    dragElement.style.position = 'fixed';
    dragElement.style.zIndex = 9999;
    document.body.style.userSelect = 'none';
  }, {passive:true});

  document.addEventListener('touchmove', (ev)=>{
    if(!isDown) return;
    const t = ev.touches[0];
    const dx = t.clientX - startX;
    const dy = t.clientY - startY;
    dragElement.style.left = (origX + dx) + 'px';
    dragElement.style.top = (origY + dy) + 'px';
  }, {passive:true});

  document.addEventListener('touchend', ()=>{
    if(isDown) { isDown = false; document.body.style.userSelect = ''; }
  });
}

// attach draggable: calcHeader -> calcBox; deletedHeader -> deletedBox
makeDraggable(calcHeader, calcBox);
makeDraggable(deletedHeader, deletedBox);

/* ---------------- Initialize UI state ---------------- */
function hideAll(){
  menuPopup.style.display = 'none';
  // do not hide calc or deleted here
}
document.addEventListener('click', (e)=>{
  if(!e.target.closest('.menu-popup') && !e.target.closest('.menu-icon')){
    menuPopup.style.display = 'none';
  }
});

// menu button actions
openCalcBtn.addEventListener('click', ()=>{
  menuPopup.style.display = 'none';
  // show calc at bottom-right initial if hidden
  calcBox.style.display = 'block';
  deletedBox.style.display = 'none';
});
openDeletedBtn.addEventListener('click', ()=>{
  menuPopup.style.display = 'none';
  openDeletedPopup();
  calcBox.style.display = 'none';
});

// close buttons
closeCalcBtn.addEventListener('click', ()=> calcBox.style.display = 'none');
closeDeletedBtn.addEventListener('click', ()=> deletedBox.style.display = 'none');

// clear deleted
clearDeletedBtn.addEventListener('click', clearAllDeleted);

/* ---------------- initial render ---------------- */
// expose handlers used in inline buttons
window.handleEdit = handleEdit;
window.handleDelete = handleDelete;

renderTransactions();

</script>
</body>
</html>
