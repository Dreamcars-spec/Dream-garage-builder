
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dream Garage</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --bg: #0d0d0d; --surface: #161616; --surface2: #1e1e1e; --surface3: #252525;
  --gold: #c8a84b; --gold-dim: #8a7030; --text: #e8e8e8; --text-dim: #888;
  --text-muted: #555; --border: #2a2a2a; --border-light: #333;
  --danger: #c0392b; --green: #27ae60; --radius: 6px;
}
html, body { height: 100%; }
body { background: var(--bg); color: var(--text); font-family: 'Inter', sans-serif; font-size: 14px; display: flex; flex-direction: column; min-height: 100vh; }

/* ── GARAGE DOOR TRANSITION ── */
#garageDoor {
  position: fixed; inset: 0; z-index: 9999;
  pointer-events: none; display: flex; flex-direction: column;
}
.door-slat {
  flex: 1;
  background: #111;
  border-bottom: 1px solid #222;
  transform: scaleY(0);
  transform-origin: top;
}
#garageDoor.closing .door-slat {
  animation: slatDown 0.04s ease-in forwards;
}
#garageDoor.opening .door-slat {
  animation: slatUp 0.04s ease-out forwards;
}
@keyframes slatDown { from { transform: scaleY(0); } to { transform: scaleY(1); } }
@keyframes slatUp   { from { transform: scaleY(1); } to { transform: scaleY(0); } }

/* ── HEADER ── */
header {
  background: var(--surface); border-bottom: 1px solid var(--border);
  padding: 0 20px; height: 52px; display: flex; align-items: center;
  justify-content: space-between; position: sticky; top: 0; z-index: 100;
  gap: 12px;
}
.logo { font-family: 'Bebas Neue', sans-serif; font-size: 24px; letter-spacing: 3px; color: var(--gold); white-space: nowrap; }
.logo span { color: var(--text); }
.header-controls { display: flex; align-items: center; gap: 10px; flex-wrap: wrap; }
.header-label { font-size: 11px; text-transform: uppercase; letter-spacing: 1px; color: var(--text-muted); }
select {
  background: var(--surface3); color: var(--text); border: 1px solid var(--border-light);
  border-radius: var(--radius); padding: 5px 9px; font-family: 'Inter', sans-serif;
  font-size: 12px; cursor: pointer; outline: none;
}
select:focus { border-color: var(--gold); }

/* ── TABS ── */
.tabs { display: flex; background: var(--surface); border-bottom: 1px solid var(--border); padding: 0 20px; }
.tab {
  padding: 13px 18px; font-size: 12px; font-weight: 500; letter-spacing: 1px;
  text-transform: uppercase; color: var(--text-dim); cursor: pointer;
  border-bottom: 2px solid transparent; transition: color 0.2s, border-color 0.2s; user-select: none;
}
.tab.active { color: var(--gold); border-bottom-color: var(--gold); }
.tab:hover:not(.active) { color: var(--text); }

/* ── LAYOUT ── */
.app-body { display: flex; flex: 1; overflow: hidden; }

/* ── SIDEBAR ── */
.sidebar {
  width: 250px; min-width: 250px; background: var(--surface);
  border-right: 1px solid var(--border); display: flex; flex-direction: column; overflow-y: auto;
}
.sidebar-header {
  padding: 14px 16px; border-bottom: 1px solid var(--border);
  display: flex; align-items: center; justify-content: space-between;
}
.sidebar-title { font-family: 'Bebas Neue', sans-serif; font-size: 14px; letter-spacing: 2px; color: var(--text-dim); }
.btn-icon {
  background: none; border: 1px solid var(--border-light); color: var(--gold);
  border-radius: var(--radius); width: 26px; height: 26px; cursor: pointer; font-size: 17px;
  display: flex; align-items: center; justify-content: center; transition: background 0.15s, border-color 0.15s;
}
.btn-icon:hover { background: var(--surface3); border-color: var(--gold); }
.garage-item {
  padding: 11px 16px; cursor: pointer; border-left: 3px solid transparent;
  transition: background 0.15s, border-color 0.15s; position: relative;
}
.garage-item:hover { background: var(--surface2); }
.garage-item.active { background: var(--surface2); border-left-color: var(--gold); }
.garage-item-name { font-weight: 500; font-size: 13px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; padding-right: 44px; }
.garage-item-meta { font-size: 11px; color: var(--text-dim); margin-top: 3px; }
.garage-item-actions {
  position: absolute; right: 10px; top: 50%; transform: translateY(-50%);
  display: none; gap: 4px;
}
.garage-item:hover .garage-item-actions { display: flex; }
.btn-tiny { background: none; border: none; color: var(--text-muted); cursor: pointer; padding: 2px 4px; border-radius: 3px; font-size: 12px; transition: color 0.15s; }
.btn-tiny:hover { color: var(--text); }
.btn-tiny.danger:hover { color: var(--danger); }

/* ── MAIN ── */
.main { flex: 1; overflow-y: auto; padding: 22px; }

/* ── GARAGE VIEW ── */
.garage-top { display: flex; align-items: flex-start; justify-content: space-between; margin-bottom: 20px; gap: 16px; flex-wrap: wrap; }
.garage-name-display { font-family: 'Bebas Neue', sans-serif; font-size: 34px; letter-spacing: 3px; color: var(--text); line-height: 1; }
.garage-name-display small { display: block; font-family: 'Inter', sans-serif; font-size: 11px; letter-spacing: 1px; text-transform: uppercase; color: var(--text-dim); margin-bottom: 4px; font-weight: 400; }
.budget-bar { background: var(--surface2); border: 1px solid var(--border); border-radius: var(--radius); padding: 11px 14px; min-width: 220px; }
.budget-bar-label { font-size: 10px; text-transform: uppercase; letter-spacing: 1px; color: var(--text-dim); margin-bottom: 5px; }
.budget-bar-values { display: flex; align-items: baseline; gap: 6px; }
.budget-spent { font-family: 'Bebas Neue', sans-serif; font-size: 20px; letter-spacing: 1px; }
.budget-spent.over { color: var(--danger); }
.budget-total { font-size: 12px; color: var(--text-dim); }
.budget-progress { height: 3px; background: var(--border); border-radius: 2px; margin-top: 7px; overflow: hidden; }
.budget-progress-fill { height: 100%; background: var(--gold); border-radius: 2px; transition: width 0.4s; }
.budget-progress-fill.over { background: var(--danger); }
.budget-unlimited { font-size: 11px; color: var(--text-muted); font-style: italic; margin-top: 3px; }

/* ── CAR GRID ── */
.car-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(210px, 1fr)); gap: 14px; }
.car-card {
  background: var(--surface2); border: 1px solid var(--border); border-radius: 8px;
  overflow: hidden; transition: border-color 0.2s, transform 0.15s; cursor: pointer; position: relative;
}
.car-card:hover { border-color: var(--gold-dim); transform: translateY(-2px); }
.car-img-wrap { aspect-ratio: 16/9; background: var(--surface3); display: flex; align-items: center; justify-content: center; overflow: hidden; position: relative; }
.car-img-wrap img { width: 100%; height: 100%; object-fit: cover; display: block; }
.car-img-placeholder { color: var(--text-muted); font-size: 38px; }
.car-info { padding: 10px 12px; }
.car-badges { display: flex; gap: 5px; margin-bottom: 5px; flex-wrap: wrap; }
.badge { display: inline-block; font-size: 9px; font-weight: 600; letter-spacing: 0.8px; text-transform: uppercase; padding: 2px 6px; border-radius: 3px; }
.badge-used { background: rgba(200,168,75,0.15); color: var(--gold); border: 1px solid rgba(200,168,75,0.3); }
.badge-new  { background: rgba(39,174,96,0.15);  color: var(--green); border: 1px solid rgba(39,174,96,0.3); }
.car-name { font-weight: 600; font-size: 13px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.car-brand { font-size: 10px; color: var(--text-dim); margin-top: 2px; text-transform: uppercase; letter-spacing: 0.5px; }
.car-price { font-family: 'Bebas Neue', sans-serif; font-size: 17px; color: var(--gold); margin-top: 7px; letter-spacing: 0.5px; }
.car-remove {
  position: absolute; top: 6px; right: 6px; background: rgba(0,0,0,0.6);
  border: none; color: #fff; width: 22px; height: 22px; border-radius: 50%; font-size: 13px;
  cursor: pointer; display: none; align-items: center; justify-content: center; transition: background 0.15s; line-height: 1;
}
.car-card:hover .car-remove { display: flex; }
.car-remove:hover { background: var(--danger); }
.empty-state { grid-column: 1/-1; text-align: center; padding: 60px 20px; color: var(--text-muted); }
.empty-state-icon { font-size: 52px; margin-bottom: 12px; }
.empty-state p { font-size: 13px; }

/* ── SEARCH TAB ── */
.search-panel { max-width: 860px; }
.search-panel h2 { font-family: 'Bebas Neue', sans-serif; font-size: 26px; letter-spacing: 3px; margin-bottom: 14px; }
.search-row { display: flex; gap: 10px; margin-bottom: 18px; }
input[type="text"], input[type="number"], input[type="url"] {
  background: var(--surface2); border: 1px solid var(--border-light); color: var(--text);
  border-radius: var(--radius); padding: 8px 12px; font-family: 'Inter', sans-serif;
  font-size: 13px; outline: none; transition: border-color 0.15s; width: 100%;
}
input:focus { border-color: var(--gold); }
.btn {
  background: var(--gold); color: #000; border: none; border-radius: var(--radius);
  padding: 8px 16px; font-family: 'Inter', sans-serif; font-size: 13px; font-weight: 600;
  cursor: pointer; white-space: nowrap; transition: opacity 0.15s;
}
.btn:hover { opacity: 0.85; }
.btn.secondary { background: var(--surface3); color: var(--text); border: 1px solid var(--border-light); font-weight: 400; }
.btn.secondary:hover { border-color: var(--gold); color: var(--gold); opacity: 1; }
.btn.danger-btn { background: var(--danger); color: #fff; }

.search-results { display: grid; grid-template-columns: repeat(auto-fill, minmax(190px, 1fr)); gap: 12px; }
.search-car-card { background: var(--surface2); border: 1px solid var(--border); border-radius: 8px; overflow: hidden; transition: border-color 0.2s; }
.search-car-card:hover { border-color: var(--gold-dim); }
.search-car-img { aspect-ratio: 16/9; background: var(--surface3); display: flex; align-items: center; justify-content: center; overflow: hidden; }
.search-car-img img { width: 100%; height: 100%; object-fit: cover; }
.search-car-img-placeholder { font-size: 34px; color: var(--text-muted); }
.search-car-info { padding: 9px 11px; }
.search-car-name { font-weight: 600; font-size: 13px; }
.search-car-brand { font-size: 10px; color: var(--text-dim); text-transform: uppercase; letter-spacing: 0.5px; margin-top: 2px; }
.search-car-price { font-family: 'Bebas Neue', sans-serif; font-size: 15px; color: var(--gold); margin-top: 5px; }
.search-car-actions { padding: 0 11px 10px; }

/* ── MODAL ── */
.modal-overlay {
  position: fixed; inset: 0; background: rgba(0,0,0,0.75); z-index: 200;
  display: flex; align-items: center; justify-content: center; padding: 20px;
  backdrop-filter: blur(4px); opacity: 0; pointer-events: none; transition: opacity 0.2s;
}
.modal-overlay.open { opacity: 1; pointer-events: all; }
.modal {
  background: var(--surface); border: 1px solid var(--border-light); border-radius: 10px;
  padding: 22px; width: 100%; max-width: 430px;
  transform: translateY(12px); transition: transform 0.2s;
}
.modal-overlay.open .modal { transform: translateY(0); }
.modal-title { font-family: 'Bebas Neue', sans-serif; font-size: 20px; letter-spacing: 2px; margin-bottom: 16px; color: var(--gold); }
.modal-field { margin-bottom: 13px; }
.modal-label { font-size: 10px; text-transform: uppercase; letter-spacing: 1px; color: var(--text-dim); margin-bottom: 5px; display: block; }
.modal-actions { display: flex; gap: 8px; margin-top: 18px; justify-content: flex-end; }
.radio-group { display: flex; gap: 8px; }
.radio-opt {
  flex: 1; background: var(--surface3); border: 1px solid var(--border-light);
  border-radius: var(--radius); padding: 7px 8px; cursor: pointer; text-align: center;
  font-size: 12px; transition: border-color 0.15s, background 0.15s;
}
.radio-opt.selected { border-color: var(--gold); color: var(--gold); background: rgba(200,168,75,0.08); }
.car-modal-img { width: 100%; aspect-ratio: 16/9; object-fit: cover; border-radius: 6px; background: var(--surface3); margin-bottom: 13px; display: block; }
.car-modal-img-placeholder { width: 100%; aspect-ratio: 16/9; background: var(--surface3); border-radius: 6px; margin-bottom: 13px; display: flex; align-items: center; justify-content: center; font-size: 48px; }

/* ── CUSTOM CAR FORM ── */
.custom-form { background: var(--surface2); border: 1px solid var(--border); border-radius: 8px; padding: 18px; margin-bottom: 20px; }
.custom-form h3 { font-family: 'Bebas Neue', sans-serif; font-size: 17px; letter-spacing: 2px; margin-bottom: 12px; color: var(--text-dim); }
.form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 9px; margin-bottom: 9px; }
.form-grid-full { grid-column: 1/-1; }
.section-divider { border: none; border-top: 1px solid var(--border); margin: 22px 0; }
.loading { color: var(--text-muted); font-style: italic; text-align: center; padding: 28px; }
::-webkit-scrollbar { width: 5px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--border-light); border-radius: 3px; }
</style>
</head>
<body>

<!-- GARAGE DOOR OVERLAY -->
<div id="garageDoor">
  <div class="door-slat"></div><div class="door-slat"></div><div class="door-slat"></div>
  <div class="door-slat"></div><div class="door-slat"></div><div class="door-slat"></div>
  <div class="door-slat"></div><div class="door-slat"></div><div class="door-slat"></div>
  <div class="door-slat"></div><div class="door-slat"></div><div class="door-slat"></div>
  <div class="door-slat"></div><div class="door-slat"></div><div class="door-slat"></div>
</div>

<header>
  <div class="logo">Dream<span>Garage</span></div>
  <div class="header-controls">
    <span class="header-label" data-i18n="currency">Currency</span>
    <select id="currencySelect">
      <option value="DKK">🇩🇰 DKK</option>
      <option value="USD">🇺🇸 USD</option>
      <option value="EUR">🇪🇺 EUR</option>
      <option value="GBP">🇬🇧 GBP</option>
      <option value="NOK">🇳🇴 NOK</option>
      <option value="SEK">🇸🇪 SEK</option>
      <option value="CHF">🇨🇭 CHF</option>
      <option value="JPY">🇯🇵 JPY</option>
      <option value="AUD">🇦🇺 AUD</option>
      <option value="CAD">🇨🇦 CAD</option>
    </select>
    <span class="header-label" data-i18n="language">Language</span>
    <select id="langSelect">
      <option value="en">🇬🇧 English</option>
      <option value="da">🇩🇰 Dansk</option>
    </select>
  </div>
</header>

<div class="tabs">
  <div class="tab active" id="tabGarage" onclick="switchTab('garage')" data-i18n-tab="myGarages">🏎 My Garages</div>
  <div class="tab" id="tabSearch" onclick="switchTab('search')" data-i18n-tab="searchAdd">🔍 Search & Add Cars</div>
</div>

<div class="app-body">
  <div class="sidebar">
    <div class="sidebar-header">
      <span class="sidebar-title" data-i18n="garages">Garages</span>
      <button class="btn-icon" onclick="openNewGarageModal()" title="New garage">+</button>
    </div>
    <div id="garageList"></div>
  </div>
  <div class="main">
    <div id="panelGarage"><div id="garageContent"></div></div>
    <div id="panelSearch" style="display:none">
      <div class="search-panel">
        <h2 data-i18n="searchTitle">Search for your dream car</h2>
        <div class="search-row">
          <input type="text" id="searchInput" data-i18n-placeholder="searchPlaceholder" placeholder="e.g. Ferrari 488, BMW M3, Porsche 911..." onkeydown="if(event.key==='Enter') searchCars()">
          <button class="btn" onclick="searchCars()" data-i18n="search">Search</button>
        </div>
        <div id="searchStatus"></div>
        <div class="search-results" id="searchResults"></div>
        <hr class="section-divider">
        <div class="custom-form">
          <h3 data-i18n="addManually">Add Manually</h3>
          <div class="form-grid">
            <div><label class="modal-label" data-i18n="brand">Brand</label><input type="text" id="customBrand" placeholder="Ferrari"></div>
            <div><label class="modal-label" data-i18n="model">Model</label><input type="text" id="customModel" placeholder="488 GTB"></div>
            <div><label class="modal-label" data-i18n="price">Price</label><input type="number" id="customPrice" placeholder="250000" min="0"></div>
            <div>
              <label class="modal-label" data-i18n="condition">Condition</label>
              <div class="radio-group" id="customConditionRadio">
                <div class="radio-opt selected" onclick="selectCustomCondition('new')" id="customOptNew" data-i18n="condNew">New</div>
                <div class="radio-opt" onclick="selectCustomCondition('used')" id="customOptUsed" data-i18n="condUsed">Used</div>
              </div>
            </div>
            <div class="form-grid-full"><label class="modal-label" data-i18n="imageUrl">Image URL (optional)</label><input type="url" id="customImage" placeholder="https://..."></div>
            <div class="form-grid-full"><label class="modal-label" data-i18n="linkUrl">Link URL (optional)</label><input type="url" id="customLink" placeholder="https://..."></div>
          </div>
          <button class="btn" onclick="addCustomCar()" style="margin-top:4px" data-i18n="addToSelectedGarage">Add to selected garage</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- NEW GARAGE MODAL -->
<div class="modal-overlay" id="modalNewGarage">
  <div class="modal">
    <div class="modal-title" data-i18n="newGarage">New Garage</div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="name">Name</label>
      <input type="text" id="newGarageName" placeholder="My Supercar Dream" onkeydown="if(event.key==='Enter') createGarage()">
    </div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="budget">Budget</label>
      <div class="radio-group" id="budgetTypeRadio">
        <div class="radio-opt selected" onclick="selectBudgetType('unlimited')" id="optUnlimited" data-i18n="unlimited">∞ Unlimited</div>
        <div class="radio-opt" onclick="selectBudgetType('fixed')" id="optFixed" data-i18n="fixedAmount">💰 Fixed amount</div>
      </div>
    </div>
    <div class="modal-field" id="budgetAmountField" style="display:none">
      <label class="modal-label" data-i18n="amount">Amount</label>
      <input type="number" id="newGarageBudget" placeholder="5000000" min="0">
    </div>
    <div class="modal-actions">
      <button class="btn secondary" onclick="closeModal('modalNewGarage')" data-i18n="cancel">Cancel</button>
      <button class="btn" onclick="createGarage()" data-i18n="create">Create</button>
    </div>
  </div>
</div>

<!-- EDIT GARAGE MODAL -->
<div class="modal-overlay" id="modalEditGarage">
  <div class="modal">
    <div class="modal-title" data-i18n="editGarage">Edit Garage</div>
    <input type="hidden" id="editGarageId">
    <div class="modal-field">
      <label class="modal-label" data-i18n="name">Name</label>
      <input type="text" id="editGarageName">
    </div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="budget">Budget</label>
      <div class="radio-group">
        <div class="radio-opt" onclick="selectEditBudgetType('unlimited')" id="editOptUnlimited" data-i18n="unlimited">∞ Unlimited</div>
        <div class="radio-opt" onclick="selectEditBudgetType('fixed')" id="editOptFixed" data-i18n="fixedAmount">💰 Fixed amount</div>
      </div>
    </div>
    <div class="modal-field" id="editBudgetAmountField" style="display:none">
      <label class="modal-label" data-i18n="amount">Amount</label>
      <input type="number" id="editGarageBudget" min="0">
    </div>
    <div class="modal-actions">
      <button class="btn secondary" onclick="closeModal('modalEditGarage')" data-i18n="cancel">Cancel</button>
      <button class="btn" onclick="saveEditGarage()" data-i18n="save">Save</button>
    </div>
  </div>
</div>

<!-- CAR DETAIL MODAL -->
<div class="modal-overlay" id="modalCarDetail">
  <div class="modal" style="max-width:470px">
    <div id="carDetailImg"></div>
    <div class="modal-title" id="carDetailTitle"></div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="condition">Condition</label>
      <div class="radio-group">
        <div class="radio-opt" onclick="selectDetailCondition('new')" id="detailOptNew" data-i18n="condNew">New</div>
        <div class="radio-opt" onclick="selectDetailCondition('used')" id="detailOptUsed" data-i18n="condUsed">Used</div>
      </div>
    </div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="price">Price (in selected currency)</label>
      <input type="number" id="carDetailPrice" min="0">
    </div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="imageUrl">Image URL</label>
      <input type="url" id="carDetailImage" placeholder="https://...">
    </div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="linkUrl">Link (opens on click)</label>
      <input type="url" id="carDetailLink" placeholder="https://...">
    </div>
    <input type="hidden" id="carDetailGarageId">
    <input type="hidden" id="carDetailCarId">
    <div class="modal-actions">
      <button class="btn danger-btn" onclick="removeCarFromDetail()" data-i18n="removeCar">Remove car</button>
      <button class="btn secondary" onclick="closeModal('modalCarDetail')" data-i18n="cancel">Cancel</button>
      <button class="btn" onclick="saveCarDetail()" data-i18n="save">Save</button>
    </div>
  </div>
</div>

<!-- ADD TO GARAGE MODAL -->
<div class="modal-overlay" id="modalAddToGarage">
  <div class="modal">
    <div class="modal-title" data-i18n="addToGarage">Add to Garage</div>
    <div id="addToGarageCarInfo" style="margin-bottom:12px;color:var(--text-dim);font-size:13px;"></div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="condition">Condition</label>
      <div class="radio-group">
        <div class="radio-opt selected" onclick="selectAddCondition('new')" id="addOptNew" data-i18n="condNew">New</div>
        <div class="radio-opt" onclick="selectAddCondition('used')" id="addOptUsed" data-i18n="condUsed">Used</div>
      </div>
    </div>
    <div class="modal-field">
      <label class="modal-label" data-i18n="selectGarage">Select garage</label>
      <select id="addToGarageSelect" style="width:100%"></select>
    </div>
    <div class="modal-actions">
      <button class="btn secondary" onclick="closeModal('modalAddToGarage')" data-i18n="cancel">Cancel</button>
      <button class="btn" onclick="confirmAddToGarage()" data-i18n="add">Add</button>
    </div>
  </div>
</div>

<script>
// ── i18n ──
const LANGS = {
  en: {
    currency:'Currency', language:'Language', garages:'Garages',
    myGarages:'🏎 My Garages', searchAdd:'🔍 Search & Add Cars',
    searchTitle:'Search for your dream car',
    searchPlaceholder:'e.g. Ferrari 488, BMW M3, Porsche 911...',
    search:'Search', addManually:'Add Manually', brand:'Brand', model:'Model',
    price:'Price', condition:'Condition', condNew:'New', condUsed:'Used',
    imageUrl:'Image URL (optional)', linkUrl:'Link URL (optional)',
    addToSelectedGarage:'Add to selected garage', newGarage:'New Garage',
    name:'Name', budget:'Budget', unlimited:'∞ Unlimited', fixedAmount:'💰 Fixed amount',
    amount:'Amount', cancel:'Cancel', create:'Create', editGarage:'Edit Garage',
    save:'Save', removeCar:'Remove car', addToGarage:'Add to Garage',
    selectGarage:'Select garage', add:'Add',
    yourGarage:'Your Garage', noCars:'No cars yet — search for cars in the "Search & Add" tab',
    searching:'Searching...', searchFailed:'Search failed. Please try again.',
    results:'results for', addedFeedback:'✓ Added!',
    noGarages:'No garages yet', deleteConfirm:'Delete this garage?',
    selectGarageFirst:'Select a garage in the sidebar first',
    budgetLabel:'Budget', unlimitedBudget:'Unlimited budget',
    carCount:'car', cars:'cars',
  },
  da: {
    currency:'Valuta', language:'Sprog', garages:'Garager',
    myGarages:'🏎 Mine Garager', searchAdd:'🔍 Søg & Tilføj Biler',
    searchTitle:'Søg efter din drømmebil',
    searchPlaceholder:'F.eks. Ferrari 488, BMW M3, Porsche 911...',
    search:'Søg', addManually:'Tilføj Manuelt', brand:'Mærke', model:'Model',
    price:'Pris', condition:'Stand', condNew:'Ny', condUsed:'Brugt',
    imageUrl:'Billede-URL (valgfri)', linkUrl:'Link-URL (valgfri)',
    addToSelectedGarage:'Tilføj til valgt garage', newGarage:'Ny Garage',
    name:'Navn', budget:'Budget', unlimited:'∞ Ubegrænset', fixedAmount:'💰 Fast beløb',
    amount:'Beløb', cancel:'Annuller', create:'Opret', editGarage:'Rediger Garage',
    save:'Gem', removeCar:'Fjern bil', addToGarage:'Tilføj til Garage',
    selectGarage:'Vælg garage', add:'Tilføj',
    yourGarage:'Din Garage', noCars:'Ingen biler endnu — søg efter biler i fanen "Søg & Tilføj"',
    searching:'Søger...', searchFailed:'Søgning fejlede. Prøv igen.',
    results:'resultater for', addedFeedback:'✓ Tilføjet!',
    noGarages:'Ingen garager endnu', deleteConfirm:'Slet denne garage?',
    selectGarageFirst:'Vælg en garage i sidebaren først',
    budgetLabel:'Budget', unlimitedBudget:'Ubegrænset budget',
    carCount:'bil', cars:'biler',
  }
};

// ── STATE ──
let garages = JSON.parse(localStorage.getItem('dg_garages') || '[]');
let currency = localStorage.getItem('dg_currency') || 'DKK';
let lang = localStorage.getItem('dg_lang') || 'en';
let activeGarageId = null;
let currentTab = 'garage';
let pendingAddCar = null;
let newBudgetType = 'unlimited';
let editBudgetType = 'unlimited';
let customCondition = 'new';
let addCondition = 'new';
let detailCondition = 'new';

const rates = { DKK:1, USD:0.145, EUR:0.134, GBP:0.115, NOK:1.55, SEK:1.52, CHF:0.128, JPY:21.8, AUD:0.222, CAD:0.198 };
const symbols = { DKK:'kr', USD:'$', EUR:'€', GBP:'£', NOK:'kr', SEK:'kr', CHF:'Fr', JPY:'¥', AUD:'A$', CAD:'C$' };

function t(key) { return (LANGS[lang]||LANGS.en)[key] || key; }
function fmt(amount) {
  if (!amount && amount !== 0) return '—';
  const v = Math.round(amount * rates[currency]);
  return symbols[currency] + v.toLocaleString('de-DE');
}
function toDKK(amount) { return amount / rates[currency]; }
function save() { localStorage.setItem('dg_garages', JSON.stringify(garages)); localStorage.setItem('dg_currency', currency); localStorage.setItem('dg_lang', lang); }
function uid() { return Math.random().toString(36).slice(2,10); }
function esc(s) { if (!s) return ''; return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }

// ── INIT ──
document.getElementById('currencySelect').value = currency;
document.getElementById('langSelect').value = lang;
document.getElementById('currencySelect').addEventListener('change', e => { currency = e.target.value; save(); renderAll(); });
document.getElementById('langSelect').addEventListener('change', e => { lang = e.target.value; save(); applyLang(); renderAll(); });

if (garages.length === 0) { garages.push({ id: uid(), name: 'My First Garage', budget: null, cars: [] }); save(); }
activeGarageId = garages[0].id;
applyLang();
renderAll();

// ── i18n apply ──
function applyLang() {
  document.querySelectorAll('[data-i18n]').forEach(el => {
    const k = el.getAttribute('data-i18n');
    if (t(k) !== k) el.textContent = t(k);
  });
  document.querySelectorAll('[data-i18n-tab]').forEach(el => {
    const k = el.getAttribute('data-i18n-tab');
    if (t(k) !== k) el.textContent = t(k);
  });
  document.querySelectorAll('[data-i18n-placeholder]').forEach(el => {
    const k = el.getAttribute('data-i18n-placeholder');
    if (t(k) !== k) el.placeholder = t(k);
  });
}

// ── GARAGE DOOR ANIMATION ──
function garageTransition(callback) {
  const door = document.getElementById('garageDoor');
  const slats = door.querySelectorAll('.door-slat');
  door.classList.remove('opening','closing');

  // Close: slats drop down one by one
  door.classList.add('closing');
  slats.forEach((s,i) => {
    s.style.animationDelay = (i * 30) + 'ms';
  });

  const closeDuration = slats.length * 30 + 80;
  setTimeout(() => {
    callback();
    // Open: slats roll up
    door.classList.remove('closing');
    door.classList.add('opening');
    slats.forEach((s,i) => {
      s.style.animationDelay = (i * 25) + 'ms';
    });
    const openDuration = slats.length * 25 + 80;
    setTimeout(() => {
      door.classList.remove('opening');
      slats.forEach(s => s.style.animationDelay = '');
    }, openDuration);
  }, closeDuration);
}

// ── RENDER ALL ──
function renderAll() { renderSidebar(); if (currentTab === 'garage') renderGaragePanel(); }

// ── SIDEBAR ──
function renderSidebar() {
  const list = document.getElementById('garageList');
  if (!garages.length) {
    list.innerHTML = `<div style="text-align:center;padding:40px 16px;color:var(--text-muted)"><div style="font-size:40px;margin-bottom:8px">🏗️</div><p style="font-size:12px">${t('noGarages')}</p></div>`;
    return;
  }
  list.innerHTML = garages.map(g => {
    const total = g.cars.reduce((s,c) => s + (c.price||0), 0);
    const budgetInfo = g.budget ? fmt(g.budget) : '∞';
    const cc = g.cars.length;
    const carLabel = cc === 1 ? t('carCount') : t('cars');
    return `<div class="garage-item ${g.id===activeGarageId?'active':''}" onclick="selectGarage('${g.id}')">
      <div class="garage-item-name">${esc(g.name)}</div>
      <div class="garage-item-meta">${cc} ${carLabel} · ${budgetInfo}</div>
      <div class="garage-item-actions">
        <button class="btn-tiny" onclick="event.stopPropagation();openEditGarage('${g.id}')" title="Edit">✏️</button>
        <button class="btn-tiny danger" onclick="event.stopPropagation();deleteGarage('${g.id}')" title="Delete">🗑</button>
      </div>
    </div>`;
  }).join('');
}

function selectGarage(id) {
  if (id === activeGarageId && currentTab === 'garage') return;
  garageTransition(() => {
    activeGarageId = id;
    if (currentTab !== 'garage') {
      currentTab = 'garage';
      document.getElementById('tabGarage').classList.add('active');
      document.getElementById('tabSearch').classList.remove('active');
      document.getElementById('panelGarage').style.display = '';
      document.getElementById('panelSearch').style.display = 'none';
    }
    renderAll();
  });
}

// ── GARAGE PANEL ──
function renderGaragePanel() {
  const el = document.getElementById('garageContent');
  const g = garages.find(x => x.id === activeGarageId);
  if (!g) { el.innerHTML = `<div style="text-align:center;padding:60px;color:var(--text-muted)">🚗</div>`; return; }
  const total = g.cars.reduce((s,c) => s + (c.price||0), 0);
  const pct = g.budget ? Math.min(100, (total/g.budget)*100) : 0;
  const over = g.budget && total > g.budget;

  let budgetHTML = '';
  if (g.budget) {
    budgetHTML = `<div class="budget-bar">
      <div class="budget-bar-label">${t('budgetLabel')}</div>
      <div class="budget-bar-values">
        <span class="budget-spent ${over?'over':''}">${fmt(total)}</span>
        <span class="budget-total">/ ${fmt(g.budget)}</span>
      </div>
      <div class="budget-progress"><div class="budget-progress-fill ${over?'over':''}" style="width:${pct}%"></div></div>
    </div>`;
  } else {
    budgetHTML = `<div class="budget-bar">
      <div class="budget-bar-label">${t('budgetLabel')}</div>
      <div class="budget-bar-values"><span class="budget-spent">${fmt(total)}</span></div>
      <div class="budget-unlimited">${t('unlimitedBudget')}</div>
    </div>`;
  }

  let carsHTML = '';
  if (!g.cars.length) {
    carsHTML = `<div class="empty-state"><div class="empty-state-icon">🏎️</div><p>${t('noCars')}</p></div>`;
  } else {
    carsHTML = g.cars.map(c => {
      const cond = c.condition === 'used' ? `<span class="badge badge-used">${t('condUsed')}</span>` : `<span class="badge badge-new">${t('condNew')}</span>`;
      const imgHTML = c.image ? `<img src="${esc(c.image)}" alt="${esc(c.name)}" onerror="this.style.display='none';this.nextElementSibling.style.display='flex'">` : '';
      const ph = `<div class="car-img-placeholder" ${c.image?'style="display:none"':''}>🚗</div>`;
      return `<div class="car-card" onclick="openCarDetail('${g.id}','${c.id}')">
        <button class="car-remove" onclick="event.stopPropagation();removeCar('${g.id}','${c.id}')">×</button>
        <div class="car-img-wrap">${imgHTML}${ph}</div>
        <div class="car-info">
          <div class="car-badges">${cond}</div>
          <div class="car-brand">${esc(c.brand||'')}</div>
          <div class="car-name">${esc(c.name)}</div>
          <div class="car-price">${fmt(c.price)}</div>
        </div>
      </div>`;
    }).join('');
  }

  el.innerHTML = `
    <div class="garage-top">
      <div class="garage-name-display"><small>${t('yourGarage')}</small>${esc(g.name)}</div>
      ${budgetHTML}
    </div>
    <div class="car-grid">${carsHTML}</div>`;
}

// ── TABS ──
function switchTab(tab) {
  currentTab = tab;
  document.getElementById('tabGarage').classList.toggle('active', tab==='garage');
  document.getElementById('tabSearch').classList.toggle('active', tab==='search');
  document.getElementById('panelGarage').style.display = tab==='garage' ? '' : 'none';
  document.getElementById('panelSearch').style.display = tab==='search' ? '' : 'none';
  if (tab === 'garage') renderGaragePanel();
  renderSidebar();
}

// ── NEW GARAGE ──
function openNewGarageModal() {
  newBudgetType = 'unlimited';
  document.getElementById('newGarageName').value = '';
  document.getElementById('newGarageBudget').value = '';
  document.getElementById('budgetAmountField').style.display = 'none';
  document.getElementById('optUnlimited').classList.add('selected');
  document.getElementById('optFixed').classList.remove('selected');
  openModal('modalNewGarage');
  setTimeout(() => document.getElementById('newGarageName').focus(), 100);
}
function selectBudgetType(t2) {
  newBudgetType = t2;
  document.getElementById('optUnlimited').classList.toggle('selected', t2==='unlimited');
  document.getElementById('optFixed').classList.toggle('selected', t2==='fixed');
  document.getElementById('budgetAmountField').style.display = t2==='fixed' ? '' : 'none';
}
function createGarage() {
  const name = document.getElementById('newGarageName').value.trim();
  if (!name) { document.getElementById('newGarageName').focus(); return; }
  const budget = newBudgetType==='fixed' ? parseFloat(document.getElementById('newGarageBudget').value)||null : null;
  const g = { id: uid(), name, budget, cars: [] };
  garages.push(g);
  save();
  closeModal('modalNewGarage');
  garageTransition(() => { activeGarageId = g.id; switchTab('garage'); });
}

// ── EDIT GARAGE ──
function openEditGarage(id) {
  const g = garages.find(x => x.id===id);
  if (!g) return;
  document.getElementById('editGarageId').value = id;
  document.getElementById('editGarageName').value = g.name;
  editBudgetType = g.budget ? 'fixed' : 'unlimited';
  document.getElementById('editOptUnlimited').classList.toggle('selected', editBudgetType==='unlimited');
  document.getElementById('editOptFixed').classList.toggle('selected', editBudgetType==='fixed');
  document.getElementById('editBudgetAmountField').style.display = editBudgetType==='fixed' ? '' : 'none';
  document.getElementById('editGarageBudget').value = g.budget||'';
  openModal('modalEditGarage');
}
function selectEditBudgetType(t2) {
  editBudgetType = t2;
  document.getElementById('editOptUnlimited').classList.toggle('selected', t2==='unlimited');
  document.getElementById('editOptFixed').classList.toggle('selected', t2==='fixed');
  document.getElementById('editBudgetAmountField').style.display = t2==='fixed' ? '' : 'none';
}
function saveEditGarage() {
  const id = document.getElementById('editGarageId').value;
  const g = garages.find(x => x.id===id);
  if (!g) return;
  const name = document.getElementById('editGarageName').value.trim();
  if (!name) return;
  g.name = name;
  g.budget = editBudgetType==='fixed' ? parseFloat(document.getElementById('editGarageBudget').value)||null : null;
  save(); closeModal('modalEditGarage'); renderAll();
}
function deleteGarage(id) {
  if (!confirm(t('deleteConfirm'))) return;
  garages = garages.filter(x => x.id!==id);
  if (activeGarageId===id) activeGarageId = garages[0]?.id||null;
  save(); renderAll();
}

// ── CAR DETAIL ──
function openCarDetail(garageId, carId) {
  const g = garages.find(x => x.id===garageId);
  const c = g?.cars.find(x => x.id===carId);
  if (!c) return;
  detailCondition = c.condition || 'new';
  document.getElementById('carDetailGarageId').value = garageId;
  document.getElementById('carDetailCarId').value = carId;
  document.getElementById('carDetailTitle').textContent = (c.brand ? c.brand+' ' : '') + c.name;
  document.getElementById('carDetailPrice').value = c.price ? Math.round(c.price * rates[currency]) : '';
  document.getElementById('carDetailImage').value = c.image||'';
  document.getElementById('carDetailLink').value = c.link||'';
  document.getElementById('detailOptNew').classList.toggle('selected', detailCondition==='new');
  document.getElementById('detailOptUsed').classList.toggle('selected', detailCondition==='used');
  const imgEl = document.getElementById('carDetailImg');
  imgEl.innerHTML = c.image
    ? `<img class="car-modal-img" src="${esc(c.image)}" alt="${esc(c.name)}" onerror="this.outerHTML='<div class=car-modal-img-placeholder>🚗</div>'">`
    : '<div class="car-modal-img-placeholder">🚗</div>';
  // open link on image click if link exists
  if (c.link) { imgEl.style.cursor='pointer'; imgEl.onclick = () => window.open(c.link,'_blank'); }
  else { imgEl.style.cursor=''; imgEl.onclick = null; }
  openModal('modalCarDetail');
}
function selectDetailCondition(v) {
  detailCondition = v;
  document.getElementById('detailOptNew').classList.toggle('selected', v==='new');
  document.getElementById('detailOptUsed').classList.toggle('selected', v==='used');
}
function saveCarDetail() {
  const gId = document.getElementById('carDetailGarageId').value;
  const cId = document.getElementById('carDetailCarId').value;
  const g = garages.find(x => x.id===gId);
  const c = g?.cars.find(x => x.id===cId);
  if (!c) return;
  const priceInCurrency = parseFloat(document.getElementById('carDetailPrice').value)||0;
  c.price = priceInCurrency / rates[currency];
  c.image = document.getElementById('carDetailImage').value.trim();
  c.link = document.getElementById('carDetailLink').value.trim();
  c.condition = detailCondition;
  save(); closeModal('modalCarDetail'); renderAll();
}
function removeCarFromDetail() {
  const gId = document.getElementById('carDetailGarageId').value;
  const cId = document.getElementById('carDetailCarId').value;
  removeCar(gId, cId); closeModal('modalCarDetail');
}
function removeCar(garageId, carId) {
  const g = garages.find(x => x.id===garageId);
  if (!g) return;
  g.cars = g.cars.filter(x => x.id!==carId);
  save(); renderAll();
}

// ── SEARCH ──
async function searchCars() {
  const q = document.getElementById('searchInput').value.trim();
  if (!q) return;
  const status = document.getElementById('searchStatus');
  const results = document.getElementById('searchResults');
  status.innerHTML = `<div class="loading">${t('searching')}</div>`;
  results.innerHTML = '';
  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'anthropic-dangerous-direct-browser-access': 'true' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{
          role: 'user',
          content: `You are a car database. The user searched for: "${q}". Return a JSON array of 6 relevant cars matching this search. Each object: { "brand": string, "name": string (model only), "year": number, "priceDKK": number (realistic current market price in Danish Krone), "emoji": string (one emoji for the car's vibe) }. Return ONLY the JSON array with no markdown fences, no explanation.`
        }]
      })
    });
    const data = await res.json();
    const raw = data.content?.map(b => b.text||'').join('') || '';
    const clean = raw.replace(/```json|```/g,'').trim();
    const cars = JSON.parse(clean);
    status.innerHTML = `<p style="color:var(--text-dim);font-size:12px;margin-bottom:12px">${cars.length} ${t('results')} "${q}"</p>`;
    results.innerHTML = cars.map(c => {
      const safeC = JSON.stringify({brand:c.brand,name:c.name,price:c.priceDKK,emoji:c.emoji}).replace(/'/g,'&#39;');
      return `<div class="search-car-card">
        <div class="search-car-img"><div class="search-car-img-placeholder">${c.emoji||'🚗'}</div></div>
        <div class="search-car-info">
          <div class="search-car-brand">${esc(c.brand)}</div>
          <div class="search-car-name">${esc(c.name)} ${c.year||''}</div>
          <div class="search-car-price">${fmt(c.priceDKK)}</div>
        </div>
        <div class="search-car-actions">
          <button class="btn" style="width:100%;font-size:12px" onclick='openAddToGarage(${safeC})'>+ ${t('addToGarage')}</button>
        </div>
      </div>`;
    }).join('');
  } catch(e) {
    console.error(e);
    status.innerHTML = `<div class="loading" style="color:var(--danger)">${t('searchFailed')}</div>`;
  }
}

// ── ADD TO GARAGE ──
function selectAddCondition(v) {
  addCondition = v;
  document.getElementById('addOptNew').classList.toggle('selected', v==='new');
  document.getElementById('addOptUsed').classList.toggle('selected', v==='used');
}
function openAddToGarage(car) {
  pendingAddCar = car;
  addCondition = 'new';
  document.getElementById('addOptNew').classList.add('selected');
  document.getElementById('addOptUsed').classList.remove('selected');
  const sel = document.getElementById('addToGarageSelect');
  sel.innerHTML = garages.map(g => `<option value="${g.id}">${esc(g.name)}</option>`).join('');
  if (activeGarageId) sel.value = activeGarageId;
  document.getElementById('addToGarageCarInfo').textContent = `${car.brand} ${car.name} — ${fmt(car.price)}`;
  openModal('modalAddToGarage');
}
function confirmAddToGarage() {
  const gId = document.getElementById('addToGarageSelect').value;
  const g = garages.find(x => x.id===gId);
  if (!g || !pendingAddCar) return;
  g.cars.push({ id: uid(), brand: pendingAddCar.brand, name: pendingAddCar.name, price: pendingAddCar.price, image:'', link:'', condition: addCondition });
  save(); closeModal('modalAddToGarage'); activeGarageId = gId; renderSidebar();
}

// ── CUSTOM CAR ──
function selectCustomCondition(v) {
  customCondition = v;
  document.getElementById('customOptNew').classList.toggle('selected', v==='new');
  document.getElementById('customOptUsed').classList.toggle('selected', v==='used');
}
function addCustomCar() {
  const brand = document.getElementById('customBrand').value.trim();
  const model = document.getElementById('customModel').value.trim();
  const price = parseFloat(document.getElementById('customPrice').value)||0;
  const image = document.getElementById('customImage').value.trim();
  const link = document.getElementById('customLink').value.trim();
  if (!model) { document.getElementById('customModel').focus(); return; }
  const g = garages.find(x => x.id===activeGarageId);
  if (!g) { alert(t('selectGarageFirst')); return; }
  g.cars.push({ id: uid(), brand, name: model, price: toDKK(price), image, link, condition: customCondition });
  save();
  ['customBrand','customModel','customPrice','customImage','customLink'].forEach(id => document.getElementById(id).value='');
  renderSidebar();
  const btn = event.target;
  const orig = btn.textContent;
  btn.textContent = t('addedFeedback');
  setTimeout(() => btn.textContent = orig, 1500);
}

// ── MODALS ──
function openModal(id) { document.getElementById(id).classList.add('open'); }
function closeModal(id) { document.getElementById(id).classList.remove('open'); }
document.querySelectorAll('.modal-overlay').forEach(m => {
  m.addEventListener('click', e => { if (e.target===m) closeModal(m.id); });
});
</script>
</body>
</html>
HTMLEOF
echo "done"
Output

done
