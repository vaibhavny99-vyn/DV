<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DEVINE VENTURES — Factory Management</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&family=Space+Mono:wght@400;700&display=swap');

:root {
  --bg: #0d0d0f;
  --surface: #16161a;
  --surface2: #1e1e24;
  --border: #2a2a35;
  --accent: #e8c547;
  --accent2: #f0854a;
  --text: #e8e8ef;
  --muted: #7a7a8a;
  --danger: #e85454;
  --success: #54c47a;
  --info: #547ae8;
  --radius: 10px;
}

* { margin:0; padding:0; box-sizing:border-box; }

body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  overflow-x: hidden;
}

/* ===== LOGIN ===== */
#login-screen {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--bg);
  position: relative;
}

#login-screen::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse 60% 50% at 50% 0%, rgba(232,197,71,0.12) 0%, transparent 70%);
  pointer-events: none;
}

.login-box {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 18px;
  padding: 52px 44px;
  width: 420px;
  position: relative;
  z-index: 1;
}

.login-logo {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 42px;
  letter-spacing: 4px;
  color: var(--accent);
  text-align: center;
  line-height: 1;
}

.login-sub {
  text-align: center;
  color: var(--muted);
  font-size: 12px;
  letter-spacing: 3px;
  text-transform: uppercase;
  margin-top: 6px;
  margin-bottom: 36px;
}

.login-tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 28px;
  background: var(--bg);
  border-radius: 8px;
  padding: 4px;
}

.login-tab {
  flex: 1;
  padding: 9px;
  border: none;
  border-radius: 6px;
  background: transparent;
  color: var(--muted);
  font-family: 'DM Sans', sans-serif;
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  transition: all .2s;
}

.login-tab.active {
  background: var(--accent);
  color: #000;
}

.form-group { margin-bottom: 18px; }

.form-group label {
  display: block;
  font-size: 12px;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 8px;
}

.form-group input, .form-group select, .form-group textarea {
  width: 100%;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 12px 16px;
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  font-size: 14px;
  outline: none;
  transition: border-color .2s;
}

.form-group input:focus, .form-group select:focus, .form-group textarea:focus {
  border-color: var(--accent);
}

.form-group select option { background: var(--surface2); }

.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  font-family: 'DM Sans', sans-serif;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all .2s;
  text-decoration: none;
}

.btn-primary { background: var(--accent); color: #000; }
.btn-primary:hover { background: #f0d460; transform: translateY(-1px); }
.btn-danger { background: var(--danger); color: #fff; }
.btn-danger:hover { background: #f06060; }
.btn-success { background: var(--success); color: #000; }
.btn-info { background: var(--info); color: #fff; }
.btn-ghost { background: var(--surface2); color: var(--text); border: 1px solid var(--border); }
.btn-ghost:hover { border-color: var(--accent); color: var(--accent); }
.btn-sm { padding: 7px 14px; font-size: 12px; }
.btn-full { width: 100%; justify-content: center; }

/* ===== APP LAYOUT ===== */
#app { display: none; min-height: 100vh; }

.sidebar {
  position: fixed;
  left: 0; top: 0; bottom: 0;
  width: 240px;
  background: var(--surface);
  border-right: 1px solid var(--border);
  display: flex;
  flex-direction: column;
  z-index: 100;
  overflow-y: auto;
}

.sidebar-logo {
  padding: 28px 20px 20px;
  border-bottom: 1px solid var(--border);
}

.sidebar-logo .brand {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 26px;
  letter-spacing: 3px;
  color: var(--accent);
}

.sidebar-logo .tagline {
  font-size: 10px;
  color: var(--muted);
  letter-spacing: 2px;
  text-transform: uppercase;
}

.sidebar-role {
  margin: 12px 16px;
  padding: 8px 12px;
  background: rgba(232,197,71,0.1);
  border: 1px solid rgba(232,197,71,0.25);
  border-radius: 6px;
  font-size: 11px;
  color: var(--accent);
  letter-spacing: 1px;
  text-transform: uppercase;
}

.nav-section {
  padding: 8px 0;
  border-bottom: 1px solid var(--border);
}

.nav-section-label {
  padding: 8px 20px 4px;
  font-size: 10px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--muted);
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 20px;
  color: var(--muted);
  cursor: pointer;
  font-size: 13px;
  font-weight: 500;
  transition: all .15s;
  border-left: 3px solid transparent;
}

.nav-item:hover { color: var(--text); background: var(--surface2); }
.nav-item.active { color: var(--accent); border-left-color: var(--accent); background: rgba(232,197,71,0.06); }
.nav-item .icon { font-size: 16px; width: 20px; text-align: center; }

.sidebar-footer {
  margin-top: auto;
  padding: 16px;
  border-top: 1px solid var(--border);
}

.user-info {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 10px;
}

.user-avatar {
  width: 36px; height: 36px;
  border-radius: 50%;
  background: var(--accent);
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; font-size: 14px; color: #000;
  flex-shrink: 0;
}

.user-name { font-size: 13px; font-weight: 600; }
.user-role { font-size: 11px; color: var(--muted); }

/* ===== MAIN ===== */
.main {
  margin-left: 240px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.topbar {
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  padding: 16px 32px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky; top: 0; z-index: 50;
}

.page-title {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 28px;
  letter-spacing: 2px;
  color: var(--text);
}

.topbar-actions { display: flex; gap: 10px; align-items: center; }

.content { padding: 32px; flex: 1; }

/* ===== CARDS / STATS ===== */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
  margin-bottom: 28px;
}

.stat-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 20px;
  position: relative;
  overflow: hidden;
}

.stat-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
}

.stat-card.yellow::before { background: var(--accent); }
.stat-card.orange::before { background: var(--accent2); }
.stat-card.green::before { background: var(--success); }
.stat-card.red::before { background: var(--danger); }
.stat-card.blue::before { background: var(--info); }

.stat-label { font-size: 11px; color: var(--muted); letter-spacing: 1.5px; text-transform: uppercase; }
.stat-value { font-family: 'Bebas Neue', sans-serif; font-size: 38px; color: var(--text); letter-spacing: 1px; line-height: 1.1; margin-top: 6px; }
.stat-sub { font-size: 12px; color: var(--muted); margin-top: 2px; }

/* ===== TABLE ===== */
.card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  overflow: hidden;
  margin-bottom: 24px;
}

.card-header {
  padding: 18px 24px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.card-title {
  font-weight: 600;
  font-size: 15px;
}

.card-body { padding: 24px; }

.table-wrap { overflow-x: auto; }

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 13px;
}

thead th {
  text-align: left;
  padding: 10px 14px;
  font-size: 10px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--muted);
  border-bottom: 1px solid var(--border);
  white-space: nowrap;
}

tbody td {
  padding: 12px 14px;
  border-bottom: 1px solid rgba(42,42,53,0.5);
  vertical-align: middle;
}

tbody tr:last-child td { border-bottom: none; }
tbody tr:hover { background: var(--surface2); }

/* ===== BADGES ===== */
.badge {
  display: inline-block;
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.badge-yellow { background: rgba(232,197,71,0.15); color: var(--accent); }
.badge-green { background: rgba(84,196,122,0.15); color: var(--success); }
.badge-red { background: rgba(232,84,84,0.15); color: var(--danger); }
.badge-blue { background: rgba(84,122,232,0.15); color: var(--info); }
.badge-orange { background: rgba(240,133,74,0.15); color: var(--accent2); }
.badge-grey { background: rgba(122,122,138,0.15); color: var(--muted); }

/* ===== MODAL ===== */
.modal-overlay {
  position: fixed; inset: 0;
  background: rgba(0,0,0,0.7);
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.modal {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
  width: 100%;
  max-width: 560px;
  max-height: 90vh;
  overflow-y: auto;
}

.modal-header {
  padding: 22px 28px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.modal-title { font-weight: 700; font-size: 17px; }
.modal-close { background: none; border: none; color: var(--muted); font-size: 22px; cursor: pointer; line-height: 1; }
.modal-close:hover { color: var(--text); }

.modal-body { padding: 28px; }
.modal-footer { padding: 20px 28px; border-top: 1px solid var(--border); display: flex; gap: 10px; justify-content: flex-end; }

.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.form-row-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 12px; }

/* ===== ALERT ===== */
.alert {
  padding: 12px 18px;
  border-radius: 8px;
  font-size: 13px;
  margin-bottom: 16px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.alert-error { background: rgba(232,84,84,0.1); border: 1px solid rgba(232,84,84,0.3); color: var(--danger); }
.alert-success { background: rgba(84,196,122,0.1); border: 1px solid rgba(84,196,122,0.3); color: var(--success); }

/* ===== PROGRESS ===== */
.progress-bar {
  height: 6px;
  background: var(--bg);
  border-radius: 3px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  border-radius: 3px;
  background: var(--accent);
  transition: width .5s;
}

/* ===== TABS ===== */
.tabs {
  display: flex;
  gap: 4px;
  border-bottom: 1px solid var(--border);
  margin-bottom: 24px;
}

.tab-btn {
  padding: 10px 18px;
  border: none;
  background: transparent;
  color: var(--muted);
  font-family: 'DM Sans', sans-serif;
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
  transition: all .15s;
}

.tab-btn.active { color: var(--accent); border-bottom-color: var(--accent); }
.tab-btn:hover:not(.active) { color: var(--text); }

/* ===== PAGES ===== */
.page { display: none; }
.page.active { display: block; }

/* ===== NOTIFICATION ===== */
#toast {
  position: fixed;
  bottom: 24px; right: 24px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 14px 20px;
  font-size: 13px;
  z-index: 9999;
  transform: translateY(100px);
  opacity: 0;
  transition: all .3s;
  display: flex;
  align-items: center;
  gap: 10px;
  box-shadow: 0 8px 32px rgba(0,0,0,0.5);
}

#toast.show { transform: translateY(0); opacity: 1; }
#toast.success { border-color: var(--success); }
#toast.error { border-color: var(--danger); }

/* ===== GRID 2 ===== */
.grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
.grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; }

/* ===== CHART BAR ===== */
.mini-chart { display: flex; align-items: flex-end; gap: 4px; height: 60px; }
.mini-bar {
  flex: 1;
  background: rgba(232,197,71,0.3);
  border-radius: 2px;
  min-height: 4px;
  transition: height .4s;
}
.mini-bar:hover { background: var(--accent); }

/* ===== SEARCH ===== */
.search-box {
  display: flex;
  align-items: center;
  gap: 10px;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 8px 14px;
}

.search-box input {
  background: none;
  border: none;
  outline: none;
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  font-size: 13px;
  width: 200px;
}

/* ===== EMPTY STATE ===== */
.empty-state {
  text-align: center;
  padding: 60px 20px;
  color: var(--muted);
}

.empty-state .icon { font-size: 48px; margin-bottom: 12px; }
.empty-state p { font-size: 14px; }

/* ===== WORKER CARD ===== */
.worker-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 16px; }

.worker-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 20px;
  transition: border-color .2s;
}

.worker-card:hover { border-color: rgba(232,197,71,0.3); }

.worker-card-header { display: flex; align-items: center; gap: 12px; margin-bottom: 16px; }

.worker-avatar {
  width: 44px; height: 44px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--accent), var(--accent2));
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; font-size: 16px; color: #000;
  flex-shrink: 0;
}

.worker-name { font-weight: 600; font-size: 15px; }
.worker-role { font-size: 12px; color: var(--muted); }

.worker-stats { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }

.w-stat {
  background: var(--surface2);
  border-radius: 8px;
  padding: 10px;
}

.w-stat-label { font-size: 10px; color: var(--muted); text-transform: uppercase; letter-spacing: 1px; }
.w-stat-value { font-family: 'Space Mono', monospace; font-size: 16px; font-weight: 700; margin-top: 2px; }

/* ===== SEPARATOR ===== */
hr { border: none; border-top: 1px solid var(--border); margin: 20px 0; }

/* ===== DATE CHIP ===== */
.date-chip {
  font-family: 'Space Mono', monospace;
  font-size: 11px;
  color: var(--muted);
}

/* ===== AMOUNT ===== */
.amount {
  font-family: 'Space Mono', monospace;
  font-size: 13px;
  font-weight: 700;
}

.amount.positive { color: var(--success); }
.amount.negative { color: var(--danger); }

/* ===== CLIENT PORTAL ===== */
.order-tracker {
  border: 1px solid var(--border);
  border-radius: var(--radius);
  overflow: hidden;
}

.order-tracker-row {
  display: flex;
  align-items: center;
  padding: 14px 20px;
  border-bottom: 1px solid var(--border);
  gap: 16px;
}

.order-tracker-row:last-child { border-bottom: none; }

.step-circle {
  width: 32px; height: 32px;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 14px;
  flex-shrink: 0;
}

.step-done { background: var(--success); color: #000; }
.step-active { background: var(--accent); color: #000; }
.step-pending { background: var(--surface2); color: var(--muted); }

/* ===== PRINT PREVIEW ===== */
.pdf-preview {
  background: #fff;
  color: #111;
  border-radius: var(--radius);
  padding: 40px;
  font-family: 'DM Sans', sans-serif;
  max-width: 680px;
}

/* ===== RESPONSIVE ===== */
@media (max-width: 900px) {
  .sidebar { width: 200px; }
  .main { margin-left: 200px; }
  .stats-grid { grid-template-columns: repeat(2, 1fr); }
  .grid-2, .grid-3 { grid-template-columns: 1fr; }
  .form-row { grid-template-columns: 1fr; }
}

/* ===== scrollbar ===== */
::-webkit-scrollbar { width: 6px; height: 6px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }

/* ===== Select2 fix ===== */
select { appearance: none; background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%237a7a8a' fill='none' stroke-width='1.5'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 12px center; padding-right: 36px; }
</style>
</head>
<body>

<!-- ============ LOGIN SCREEN ============ -->
<div id="login-screen">
  <div class="login-box">
    <div class="login-logo">DEVINE VENTURES</div>
    <div class="login-sub">Garment Factory Management</div>

    <div class="login-tabs">
      <button class="login-tab active" onclick="setLoginType('admin')">Admin</button>
      <button class="login-tab" onclick="setLoginType('client')">Client</button>
    </div>

    <div id="login-error" class="alert alert-error" style="display:none">⚠️ Invalid credentials</div>

    <div class="form-group">
      <label>Username</label>
      <input type="text" id="login-user" placeholder="Enter username">
    </div>
    <div class="form-group">
      <label>Password</label>
      <input type="password" id="login-pass" placeholder="Enter password" onkeydown="if(event.key==='Enter')doLogin()">
    </div>
    <button class="btn btn-primary btn-full" onclick="doLogin()">Sign In →</button>

    <p style="text-align:center;font-size:11px;color:var(--muted);margin-top:20px">
      Admin: admin/admin123 &nbsp;|&nbsp; Client: client/client123
    </p>
  </div>
</div>

<!-- ============ APP ============ -->
<div id="app">
  <!-- SIDEBAR -->
  <div class="sidebar">
    <div class="sidebar-logo">
      <div class="brand">DEVINE</div>
      <div class="tagline">Ventures · Factory OS</div>
    </div>
    <div class="sidebar-role" id="sidebar-role">ADMIN</div>

    <!-- Admin Nav -->
    <div id="admin-nav">
      <div class="nav-section">
        <div class="nav-section-label">Overview</div>
        <div class="nav-item active" onclick="showPage('dashboard')"><span class="icon">🏭</span>Dashboard</div>
      </div>
      <div class="nav-section">
        <div class="nav-section-label">Orders</div>
        <div class="nav-item" onclick="showPage('orders')"><span class="icon">📦</span>Orders</div>
        <div class="nav-item" onclick="showPage('production')"><span class="icon">🧵</span>Production</div>
        <div class="nav-item" onclick="showPage('delivery')"><span class="icon">🚚</span>Delivery Challans</div>
      </div>
      <div class="nav-section">
        <div class="nav-section-label">Finance</div>
        <div class="nav-item" onclick="showPage('expenses')"><span class="icon">💸</span>Expenses</div>
        <div class="nav-item" onclick="showPage('income')"><span class="icon">💰</span>Income / Bills</div>
        <div class="nav-item" onclick="showPage('profit')"><span class="icon">📈</span>Profit & Loss</div>
      </div>
      <div class="nav-section">
        <div class="nav-section-label">People</div>
        <div class="nav-item" onclick="showPage('workers')"><span class="icon">👷</span>Workers</div>
        <div class="nav-item" onclick="showPage('clients')"><span class="icon">🤝</span>Clients</div>
      </div>
      <div class="nav-section">
        <div class="nav-section-label">Reports</div>
        <div class="nav-item" onclick="showPage('reports')"><span class="icon">📊</span>Reports</div>
        <div class="nav-item" onclick="showPage('inventory')"><span class="icon">🧶</span>Inventory</div>
      </div>
    </div>

    <!-- Client Nav -->
    <div id="client-nav" style="display:none">
      <div class="nav-section">
        <div class="nav-item active" onclick="showPage('client-orders')"><span class="icon">📦</span>My Orders</div>
        <div class="nav-item" onclick="showPage('client-bills')"><span class="icon">🧾</span>My Bills</div>
        <div class="nav-item" onclick="showPage('client-challans')"><span class="icon">🚚</span>Delivery Challans</div>
      </div>
    </div>

    <div class="sidebar-footer">
      <div class="user-info">
        <div class="user-avatar" id="user-avatar">A</div>
        <div>
          <div class="user-name" id="user-name">Admin</div>
          <div class="user-role" id="user-role-label">Administrator</div>
        </div>
      </div>
      <button class="btn btn-ghost btn-sm btn-full" onclick="doLogout()">Sign Out</button>
    </div>
  </div>

  <!-- MAIN -->
  <div class="main">
    <div class="topbar">
      <div class="page-title" id="page-title">DASHBOARD</div>
      <div class="topbar-actions" id="topbar-actions"></div>
    </div>
    <div class="content" id="content-area"></div>
  </div>
</div>

<!-- TOAST -->
<div id="toast"></div>

<!-- ============ MODALS ============ -->
<div id="modal-overlay" style="display:none" class="modal-overlay" onclick="if(event.target===this)closeModal()">
  <div class="modal" id="modal-box">
    <div class="modal-header">
      <div class="modal-title" id="modal-title">Modal</div>
      <button class="modal-close" onclick="closeModal()">×</button>
    </div>
    <div class="modal-body" id="modal-body"></div>
    <div class="modal-footer" id="modal-footer"></div>
  </div>
</div>

<script>
// ============================================================
// DATA STORE — localStorage
// ============================================================
const DB = {
  get(k){ try{ return JSON.parse(localStorage.getItem('dv_'+k)||'null') }catch(e){return null} },
  set(k,v){ localStorage.setItem('dv_'+k, JSON.stringify(v)) },
  push(k,v){ const a=this.get(k)||[]; v.id=v.id||Date.now(); a.push(v); this.set(k,a); return v; },
  update(k,id,patch){ const a=this.get(k)||[]; const i=a.findIndex(x=>x.id==id); if(i>-1){a[i]={...a[i],...patch}; this.set(k,a); return a[i];} },
  del(k,id){ const a=(this.get(k)||[]).filter(x=>x.id!=id); this.set(k,a); },
  all(k){ return this.get(k)||[]; }
};

// Seed default data
function seedData(){
  if(DB.get('seeded')) return;
  DB.set('orders',[
    {id:1001,client:'Reliance Retail',item:'Men Shirts',qty:500,ready:320,status:'In Progress',dueDate:'2025-08-10',ratePerUnit:45,advance:5000,createdAt:'2025-07-01'},
    {id:1002,client:'Max Fashion',item:'Ladies Kurti',qty:300,ready:300,status:'Completed',dueDate:'2025-07-20',ratePerUnit:60,advance:8000,createdAt:'2025-07-05'},
    {id:1003,client:'Lifestyle',item:'Kids T-Shirt',qty:1000,ready:0,status:'Pending',dueDate:'2025-08-30',ratePerUnit:30,advance:0,createdAt:'2025-07-15'}
  ]);
  DB.set('workers',[
    {id:101,name:'Ramesh Kumar',role:'Stitching',costPerUnit:8,totalUnits:420,advance:1500,phone:'9876543210',joinDate:'2024-01-01'},
    {id:102,name:'Sunita Devi',role:'Cutting',costPerUnit:6,totalUnits:380,advance:500,phone:'9765432109',joinDate:'2024-02-15'},
    {id:103,name:'Anil Sharma',role:'Stitching',costPerUnit:8,totalUnits:510,advance:2000,phone:'9654321098',joinDate:'2023-11-01'}
  ]);
  DB.set('expenses',[
    {id:1,type:'Rent',amount:15000,date:'2025-07-01',note:'Factory Rent July',category:'Fixed'},
    {id:2,type:'Electricity',amount:4200,date:'2025-07-05',note:'Light Bill July',category:'Utility'},
    {id:3,type:'Material',amount:12000,date:'2025-07-08',note:'Thread & Buttons',category:'Raw Material'},
    {id:4,type:'Salary',amount:28000,date:'2025-07-10',note:'Worker Salaries July',category:'Labour'}
  ]);
  DB.set('income',[
    {id:1,client:'Max Fashion',amount:18000,date:'2025-07-22',orderId:1002,note:'Full Payment',paid:true},
    {id:2,client:'Reliance Retail',amount:5000,date:'2025-07-02',orderId:1001,note:'Advance Payment',paid:true}
  ]);
  DB.set('challans',[
    {id:'DC-001',orderId:1002,client:'Max Fashion',item:'Ladies Kurti',qty:300,date:'2025-07-22',vehicle:'MH04 AB 1234',driver:'Suresh',status:'Delivered'}
  ]);
  DB.set('inventory',[
    {id:1,item:'Cotton Fabric',qty:200,unit:'Meters',minQty:50,cost:120,updatedAt:'2025-07-10'},
    {id:2,item:'Thread (White)',qty:80,unit:'Spools',minQty:20,cost:15,updatedAt:'2025-07-08'},
    {id:3,item:'Buttons',qty:5000,unit:'Pieces',minQty:1000,cost:0.5,updatedAt:'2025-07-05'}
  ]);
  DB.set('clients',[
    {id:201,name:'Reliance Retail',contact:'Rahul Mehta',phone:'9000001111',email:'rahul@reliance.com',city:'Mumbai',username:'client'},
    {id:202,name:'Max Fashion',contact:'Priya Singh',phone:'9000002222',email:'priya@max.com',city:'Delhi',username:''},
    {id:203,name:'Lifestyle',contact:'Karan Patel',phone:'9000003333',email:'karan@lifestyle.com',city:'Bangalore',username:''}
  ]);
  DB.set('workerLog',[
    {id:1,workerId:101,date:'2025-07-15',units:120,note:'Batch 1'},
    {id:2,workerId:101,date:'2025-07-20',units:300,note:'Batch 2'},
    {id:3,workerId:102,date:'2025-07-18',units:380,note:'Cutting done'},
    {id:4,workerId:103,date:'2025-07-22',units:510,note:'All batches'}
  ]);
  DB.set('seeded',true);
}

// ============================================================
// AUTH
// ============================================================
let currentUser = null;
let loginType = 'admin';

function setLoginType(t){
  loginType = t;
  document.querySelectorAll('.login-tab').forEach((el,i)=>{
    el.classList.toggle('active', (t==='admin'&&i===0)||(t==='client'&&i===1));
  });
}

function doLogin(){
  const u = document.getElementById('login-user').value.trim();
  const p = document.getElementById('login-pass').value.trim();
  const err = document.getElementById('login-error');

  if(loginType==='admin' && u==='admin' && p==='admin123'){
    currentUser = {type:'admin', name:'Admin', display:'AD'};
  } else if(loginType==='client' && u==='client' && p==='client123'){
    currentUser = {type:'client', name:'Reliance Retail', display:'RR'};
  } else {
    err.style.display='flex'; return;
  }

  err.style.display='none';
  document.getElementById('login-screen').style.display='none';
  document.getElementById('app').style.display='block';
  document.getElementById('user-avatar').textContent = currentUser.display;
  document.getElementById('user-name').textContent = currentUser.name;
  document.getElementById('user-role-label').textContent = currentUser.type==='admin'?'Administrator':'Client Portal';
  document.getElementById('sidebar-role').textContent = currentUser.type.toUpperCase();

  if(currentUser.type==='admin'){
    document.getElementById('admin-nav').style.display='block';
    document.getElementById('client-nav').style.display='none';
    showPage('dashboard');
  } else {
    document.getElementById('admin-nav').style.display='none';
    document.getElementById('client-nav').style.display='block';
    showPage('client-orders');
  }
}

function doLogout(){
  currentUser = null;
  document.getElementById('login-screen').style.display='flex';
  document.getElementById('app').style.display='none';
  document.getElementById('login-user').value='';
  document.getElementById('login-pass').value='';
}

// ============================================================
// NAVIGATION
// ============================================================
function showPage(page){
  document.querySelectorAll('.nav-item').forEach(el=>el.classList.remove('active'));
  const clicked = [...document.querySelectorAll('.nav-item')].find(el=>el.getAttribute('onclick')&&el.getAttribute('onclick').includes("'"+page+"'"));
  if(clicked) clicked.classList.add('active');

  const titles = {
    dashboard:'DASHBOARD', orders:'ORDERS', production:'PRODUCTION',
    delivery:'DELIVERY CHALLANS', expenses:'EXPENSES', income:'INCOME & BILLS',
    profit:'PROFIT & LOSS', workers:'WORKERS', clients:'CLIENTS',
    reports:'REPORTS', inventory:'INVENTORY',
    'client-orders':'MY ORDERS', 'client-bills':'MY BILLS', 'client-challans':'DELIVERY CHALLANS'
  };
  document.getElementById('page-title').textContent = titles[page]||page.toUpperCase();

  const renderer = {
    dashboard: renderDashboard, orders: renderOrders, production: renderProduction,
    delivery: renderDelivery, expenses: renderExpenses, income: renderIncome,
    profit: renderProfit, workers: renderWorkers, clients: renderClients,
    reports: renderReports, inventory: renderInventory,
    'client-orders': renderClientOrders, 'client-bills': renderClientBills,
    'client-challans': renderClientChallans
  };

  if(renderer[page]) renderer[page]();
}

// ============================================================
// HELPERS
// ============================================================
function fmt(n){ return '₹'+Number(n||0).toLocaleString('en-IN'); }
function fmtN(n){ return Number(n||0).toLocaleString('en-IN'); }
function today(){ return new Date().toISOString().slice(0,10); }
function toast(msg, type='success'){
  const el = document.getElementById('toast');
  el.innerHTML = (type==='success'?'✓ ':'⚠ ') + msg;
  el.className = 'show '+type;
  setTimeout(()=>{ el.className=''; },3000);
}

function openModal(title, body, footer=''){
  document.getElementById('modal-title').textContent = title;
  document.getElementById('modal-body').innerHTML = body;
  document.getElementById('modal-footer').innerHTML = footer;
  document.getElementById('modal-overlay').style.display='flex';
}

function closeModal(){
  document.getElementById('modal-overlay').style.display='none';
}

function statusBadge(s){
  const map = {
    'Pending':'badge-grey','In Progress':'badge-yellow','Completed':'badge-green',
    'Delivered':'badge-green','Cancelled':'badge-red','Partial':'badge-orange'
  };
  return `<span class="badge ${map[s]||'badge-grey'}">${s}</span>`;
}

// ============================================================
// DASHBOARD
// ============================================================
function renderDashboard(){
  const orders = DB.all('orders');
  const expenses = DB.all('expenses');
  const income = DB.all('income');
  const workers = DB.all('workers');

  const totalOrders = orders.length;
  const activeOrders = orders.filter(o=>o.status==='In Progress').length;
  const totalQty = orders.reduce((s,o)=>s+o.qty,0);
  const totalReady = orders.reduce((s,o)=>s+o.ready,0);
  const totalExpense = expenses.reduce((s,e)=>s+e.amount,0);
  const totalIncome = income.reduce((s,i)=>s+i.amount,0);
  const profit = totalIncome - totalExpense;
  const totalWorkers = workers.length;

  // Recent activity
  const recentOrders = [...orders].sort((a,b)=>b.id-a.id).slice(0,5);
  const lowStock = DB.all('inventory').filter(i=>i.qty <= i.minQty);

  document.getElementById('content-area').innerHTML = `
    <div class="stats-grid">
      <div class="stat-card yellow">
        <div class="stat-label">Active Orders</div>
        <div class="stat-value">${activeOrders}</div>
        <div class="stat-sub">${totalOrders} total orders</div>
      </div>
      <div class="stat-card orange">
        <div class="stat-label">Units Progress</div>
        <div class="stat-value">${fmtN(totalReady)}</div>
        <div class="stat-sub">of ${fmtN(totalQty)} total</div>
        <div class="progress-bar" style="margin-top:8px"><div class="progress-fill" style="width:${totalQty?Math.round(totalReady/totalQty*100):0}%"></div></div>
      </div>
      <div class="stat-card green">
        <div class="stat-label">Total Income</div>
        <div class="stat-value">${fmt(totalIncome)}</div>
        <div class="stat-sub">This period</div>
      </div>
      <div class="stat-card red">
        <div class="stat-label">Total Expenses</div>
        <div class="stat-value">${fmt(totalExpense)}</div>
        <div class="stat-sub">This period</div>
      </div>
      <div class="stat-card ${profit>=0?'green':'red'}">
        <div class="stat-label">Net Profit</div>
        <div class="stat-value">${fmt(Math.abs(profit))}</div>
        <div class="stat-sub">${profit>=0?'Profit':'Loss'}</div>
      </div>
      <div class="stat-card blue">
        <div class="stat-label">Workers</div>
        <div class="stat-value">${totalWorkers}</div>
        <div class="stat-sub">Active staff</div>
      </div>
    </div>

    <div class="grid-2">
      <div class="card">
        <div class="card-header">
          <div class="card-title">Recent Orders</div>
          <button class="btn btn-ghost btn-sm" onclick="showPage('orders')">View All</button>
        </div>
        <div class="table-wrap">
          <table>
            <thead><tr><th>Order</th><th>Client</th><th>Item</th><th>Progress</th><th>Status</th></tr></thead>
            <tbody>
              ${recentOrders.map(o=>`
                <tr>
                  <td><span style="font-family:Space Mono;font-size:12px">#${o.id}</span></td>
                  <td>${o.client}</td>
                  <td>${o.item}</td>
                  <td>
                    <div style="display:flex;align-items:center;gap:8px">
                      <div class="progress-bar" style="width:80px"><div class="progress-fill" style="width:${o.qty?Math.round(o.ready/o.qty*100):0}%"></div></div>
                      <span style="font-size:11px;color:var(--muted)">${o.qty?Math.round(o.ready/o.qty*100):0}%</span>
                    </div>
                  </td>
                  <td>${statusBadge(o.status)}</td>
                </tr>
              `).join('')}
            </tbody>
          </table>
        </div>
      </div>

      <div>
        <div class="card" style="margin-bottom:16px">
          <div class="card-header"><div class="card-title">⚠️ Low Stock Alerts</div></div>
          <div class="card-body">
            ${lowStock.length===0
              ? '<p style="color:var(--muted);font-size:13px">All inventory levels OK ✓</p>'
              : lowStock.map(i=>`
                <div style="display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid var(--border)">
                  <div><div style="font-weight:600;font-size:13px">${i.item}</div><div style="font-size:11px;color:var(--muted)">${i.qty} ${i.unit} remaining</div></div>
                  <span class="badge badge-red">LOW</span>
                </div>
              `).join('')
            }
          </div>
        </div>

        <div class="card">
          <div class="card-header"><div class="card-title">Expense Breakdown</div></div>
          <div class="card-body">
            ${Object.entries(expenses.reduce((acc,e)=>{acc[e.type]=(acc[e.type]||0)+e.amount;return acc},{})).map(([k,v])=>`
              <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
                <span style="font-size:13px">${k}</span>
                <span class="amount negative">${fmt(v)}</span>
              </div>
            `).join('')}
          </div>
        </div>
      </div>
    </div>
  `;
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-primary btn-sm" onclick="showPage('orders')">+ New Order</button>`;
}

// ============================================================
// ORDERS
// ============================================================
function renderOrders(){
  const orders = DB.all('orders');
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-primary" onclick="openAddOrder()">+ Add Order</button>`;

  document.getElementById('content-area').innerHTML = `
    <div class="card">
      <div class="card-header">
        <div class="card-title">All Orders (${orders.length})</div>
        <div class="search-box"><span>🔍</span><input type="text" placeholder="Search orders..." oninput="filterOrders(this.value)"></div>
      </div>
      <div class="table-wrap">
        <table id="orders-table">
          <thead>
            <tr>
              <th>Order ID</th><th>Client</th><th>Item</th><th>Qty</th><th>Ready</th>
              <th>Progress</th><th>Rate/Unit</th><th>Total Value</th><th>Advance</th><th>Due Date</th><th>Status</th><th>Actions</th>
            </tr>
          </thead>
          <tbody id="orders-tbody">
            ${renderOrderRows(orders)}
          </tbody>
        </table>
      </div>
    </div>
  `;
}

function renderOrderRows(orders){
  if(!orders.length) return `<tr><td colspan="12"><div class="empty-state"><div class="icon">📦</div><p>No orders yet. Add your first order!</p></div></td></tr>`;
  return orders.map(o=>`
    <tr>
      <td><span style="font-family:Space Mono;font-size:12px;color:var(--accent)">#${o.id}</span></td>
      <td><strong>${o.client}</strong></td>
      <td>${o.item}</td>
      <td>${fmtN(o.qty)}</td>
      <td><span style="color:var(--success);font-weight:600">${fmtN(o.ready)}</span></td>
      <td>
        <div style="display:flex;align-items:center;gap:8px;min-width:120px">
          <div class="progress-bar" style="flex:1"><div class="progress-fill" style="width:${o.qty?Math.round(o.ready/o.qty*100):0}%"></div></div>
          <span style="font-size:11px;color:var(--muted);width:30px">${o.qty?Math.round(o.ready/o.qty*100):0}%</span>
        </div>
      </td>
      <td>${fmt(o.ratePerUnit)}</td>
      <td class="amount">${fmt(o.qty * o.ratePerUnit)}</td>
      <td class="amount positive">${fmt(o.advance)}</td>
      <td class="date-chip">${o.dueDate}</td>
      <td>${statusBadge(o.status)}</td>
      <td>
        <div style="display:flex;gap:6px">
          <button class="btn btn-ghost btn-sm" onclick="editOrder(${o.id})">Edit</button>
          <button class="btn btn-info btn-sm" onclick="generateBillPDF(${o.id})">Bill PDF</button>
          <button class="btn btn-danger btn-sm" onclick="delOrder(${o.id})">Del</button>
        </div>
      </td>
    </tr>
  `).join('');
}

function filterOrders(q){
  const orders = DB.all('orders').filter(o=>
    o.client.toLowerCase().includes(q.toLowerCase())||
    o.item.toLowerCase().includes(q.toLowerCase())||
    String(o.id).includes(q)
  );
  document.getElementById('orders-tbody').innerHTML = renderOrderRows(orders);
}

function openAddOrder(){
  const clients = DB.all('clients');
  openModal('Add New Order',`
    <div class="form-row">
      <div class="form-group"><label>Client Name</label>
        <select id="f-client"><option value="">Select Client</option>${clients.map(c=>`<option>${c.name}</option>`).join('')}<option value="__new__">+ New Client</option></select>
      </div>
      <div class="form-group"><label>Item / Product</label><input type="text" id="f-item" placeholder="e.g. Men Shirts"></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Total Quantity</label><input type="number" id="f-qty" placeholder="500"></div>
      <div class="form-group"><label>Rate per Unit (₹)</label><input type="number" id="f-rate" placeholder="45"></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Advance Paid (₹)</label><input type="number" id="f-adv" placeholder="5000"></div>
      <div class="form-group"><label>Due Date</label><input type="date" id="f-due" value="${today()}"></div>
    </div>
    <div class="form-group"><label>Status</label>
      <select id="f-status">
        <option>Pending</option><option>In Progress</option><option>Completed</option><option>Cancelled</option>
      </select>
    </div>
    <div class="form-group"><label>Notes</label><textarea id="f-notes" rows="2"></textarea></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveOrder()">Save Order</button>`);
}

function saveOrder(){
  const client = document.getElementById('f-client').value;
  const item = document.getElementById('f-item').value;
  if(!client||!item){ toast('Fill required fields','error'); return; }
  const o = {
    id: Date.now(), client, item,
    qty: +document.getElementById('f-qty').value||0,
    ready: 0,
    ratePerUnit: +document.getElementById('f-rate').value||0,
    advance: +document.getElementById('f-adv').value||0,
    dueDate: document.getElementById('f-due').value,
    status: document.getElementById('f-status').value,
    notes: document.getElementById('f-notes').value,
    createdAt: today()
  };
  DB.push('orders',o);
  closeModal(); renderOrders(); toast('Order added!');
}

function editOrder(id){
  const o = DB.all('orders').find(x=>x.id==id);
  const clients = DB.all('clients');
  openModal('Edit Order #'+id,`
    <div class="form-row">
      <div class="form-group"><label>Client</label>
        <select id="f-client"><option value="">Select</option>${clients.map(c=>`<option ${c.name===o.client?'selected':''}>${c.name}</option>`).join('')}</select>
      </div>
      <div class="form-group"><label>Item</label><input type="text" id="f-item" value="${o.item}"></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Total Qty</label><input type="number" id="f-qty" value="${o.qty}"></div>
      <div class="form-group"><label>Units Ready</label><input type="number" id="f-ready" value="${o.ready}"></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Rate/Unit (₹)</label><input type="number" id="f-rate" value="${o.ratePerUnit}"></div>
      <div class="form-group"><label>Advance (₹)</label><input type="number" id="f-adv" value="${o.advance}"></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Due Date</label><input type="date" id="f-due" value="${o.dueDate}"></div>
      <div class="form-group"><label>Status</label>
        <select id="f-status">
          ${['Pending','In Progress','Completed','Cancelled'].map(s=>`<option ${s===o.status?'selected':''}>${s}</option>`).join('')}
        </select>
      </div>
    </div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="updateOrder(${id})">Update</button>`);
}

function updateOrder(id){
  DB.update('orders',id,{
    client: document.getElementById('f-client').value,
    item: document.getElementById('f-item').value,
    qty: +document.getElementById('f-qty').value,
    ready: +document.getElementById('f-ready').value,
    ratePerUnit: +document.getElementById('f-rate').value,
    advance: +document.getElementById('f-adv').value,
    dueDate: document.getElementById('f-due').value,
    status: document.getElementById('f-status').value
  });
  closeModal(); renderOrders(); toast('Order updated!');
}

function delOrder(id){
  if(!confirm('Delete this order?')) return;
  DB.del('orders',id); renderOrders(); toast('Order deleted','error');
}

// ============================================================
// PRODUCTION
// ============================================================
function renderProduction(){
  const orders = DB.all('orders').filter(o=>o.status!=='Cancelled');
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-primary" onclick="openUpdateProduction()">Update Production</button>`;
  document.getElementById('content-area').innerHTML = `
    <div class="card">
      <div class="card-header"><div class="card-title">Production Tracker</div></div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Order</th><th>Client</th><th>Item</th><th>Total</th><th>Ready</th><th>Pending</th><th>Progress</th><th>Status</th><th>Update</th></tr></thead>
          <tbody>
            ${orders.map(o=>{
              const pct = o.qty?Math.round(o.ready/o.qty*100):0;
              const pending = o.qty - o.ready;
              return `<tr>
                <td style="font-family:Space Mono;font-size:12px;color:var(--accent)">#${o.id}</td>
                <td>${o.client}</td>
                <td>${o.item}</td>
                <td>${fmtN(o.qty)}</td>
                <td style="color:var(--success);font-weight:600">${fmtN(o.ready)}</td>
                <td style="color:var(--danger)">${fmtN(pending)}</td>
                <td>
                  <div style="display:flex;align-items:center;gap:8px;min-width:140px">
                    <div class="progress-bar" style="flex:1"><div class="progress-fill" style="width:${pct}%;background:${pct>=100?'var(--success)':pct>=50?'var(--accent)':'var(--accent2)'}"></div></div>
                    <strong style="font-size:12px">${pct}%</strong>
                  </div>
                </td>
                <td>${statusBadge(o.status)}</td>
                <td><button class="btn btn-ghost btn-sm" onclick="quickUpdateProd(${o.id},${o.ready},${o.qty})">+Units</button></td>
              </tr>`;
            }).join('')}
          </tbody>
        </table>
      </div>
    </div>
  `;
}

function quickUpdateProd(id, current, max){
  openModal('Update Production Units',`
    <p style="color:var(--muted);font-size:13px;margin-bottom:16px">Current ready: <strong style="color:var(--accent)">${current}</strong> / ${max}</p>
    <div class="form-group"><label>New Units Ready</label><input type="number" id="f-prod" value="${current}" min="0" max="${max}"></div>
    <div class="form-group"><label>Auto-update status when 100%?</label>
      <select id="f-auto"><option value="1">Yes — mark Completed</option><option value="0">No</option></select>
    </div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveProd(${id},${max})">Update</button>`);
}

function saveProd(id,max){
  const ready = +document.getElementById('f-prod').value;
  const auto = document.getElementById('f-auto').value==='1';
  const patch = {ready};
  if(auto && ready>=max) patch.status='Completed';
  DB.update('orders',id,patch);
  closeModal(); renderProduction(); toast('Production updated!');
}

function openUpdateProduction(){
  const orders = DB.all('orders').filter(o=>o.status==='In Progress'||o.status==='Pending');
  openModal('Bulk Production Update',`
    <p style="font-size:13px;color:var(--muted);margin-bottom:16px">Update units for active orders</p>
    ${orders.map(o=>`
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:14px;padding:12px;background:var(--surface2);border-radius:8px">
        <div style="flex:1"><div style="font-weight:600;font-size:13px">#${o.id} — ${o.item}</div><div style="font-size:11px;color:var(--muted)">${o.client}</div></div>
        <input type="number" value="${o.ready}" min="0" max="${o.qty}" style="width:80px;background:var(--bg);border:1px solid var(--border);border-radius:6px;padding:6px 10px;color:var(--text)" id="bulk-${o.id}">
        <span style="font-size:12px;color:var(--muted)">/${o.qty}</span>
      </div>
    `).join('')}
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveBulkProd([${orders.map(o=>o.id).join(',')}])">Save All</button>`);
}

function saveBulkProd(ids){
  ids.forEach(id=>{
    const el = document.getElementById('bulk-'+id);
    if(el){
      const o = DB.all('orders').find(x=>x.id==id);
      const ready = +el.value;
      const patch = {ready};
      if(ready>=o.qty) patch.status='Completed';
      DB.update('orders',id,patch);
    }
  });
  closeModal(); renderProduction(); toast('Production updated!');
}

// ============================================================
// DELIVERY CHALLANS
// ============================================================
function renderDelivery(){
  const challans = DB.all('challans');
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-primary" onclick="openAddChallan()">+ New Challan</button>`;
  document.getElementById('content-area').innerHTML = `
    <div class="card">
      <div class="card-header"><div class="card-title">Delivery Challans (${challans.length})</div></div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Challan No</th><th>Order</th><th>Client</th><th>Item</th><th>Qty</th><th>Date</th><th>Vehicle</th><th>Driver</th><th>Status</th><th>Actions</th></tr></thead>
          <tbody>
            ${challans.length===0?`<tr><td colspan="10"><div class="empty-state"><div class="icon">🚚</div><p>No challans yet</p></div></td></tr>`:
            challans.map(c=>`
              <tr>
                <td style="font-family:Space Mono;color:var(--accent)">${c.id}</td>
                <td style="font-family:Space Mono;font-size:12px">#${c.orderId}</td>
                <td>${c.client}</td>
                <td>${c.item}</td>
                <td>${fmtN(c.qty)}</td>
                <td class="date-chip">${c.date}</td>
                <td>${c.vehicle}</td>
                <td>${c.driver}</td>
                <td>${statusBadge(c.status)}</td>
                <td><div style="display:flex;gap:6px">
                  <button class="btn btn-info btn-sm" onclick="printChallanPDF('${c.id}')">📄 PDF</button>
                  <button class="btn btn-danger btn-sm" onclick="delChallan('${c.id}')">Del</button>
                </div></td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      </div>
    </div>
  `;
}

function openAddChallan(){
  const orders = DB.all('orders');
  const nextId = 'DC-'+ String((DB.all('challans').length+1)).padStart(3,'0');
  openModal('New Delivery Challan',`
    <div class="form-row">
      <div class="form-group"><label>Challan No</label><input type="text" id="f-cid" value="${nextId}" readonly style="opacity:.6"></div>
      <div class="form-group"><label>Date</label><input type="date" id="f-cdate" value="${today()}"></div>
    </div>
    <div class="form-group"><label>Select Order</label>
      <select id="f-cord" onchange="fillChallanOrder(this)">
        <option value="">Select Order...</option>
        ${orders.map(o=>`<option value="${o.id}">#${o.id} — ${o.client} — ${o.item}</option>`).join('')}
      </select>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Client</label><input type="text" id="f-cclient" placeholder="Auto-filled"></div>
      <div class="form-group"><label>Item</label><input type="text" id="f-citem" placeholder="Auto-filled"></div>
    </div>
    <div class="form-group"><label>Quantity Delivered</label><input type="number" id="f-cqty" placeholder="300"></div>
    <div class="form-row">
      <div class="form-group"><label>Vehicle No</label><input type="text" id="f-cveh" placeholder="MH04 AB 1234"></div>
      <div class="form-group"><label>Driver Name</label><input type="text" id="f-cdrv" placeholder="Driver name"></div>
    </div>
    <div class="form-group"><label>Status</label>
      <select id="f-cstat"><option>In Transit</option><option>Delivered</option></select>
    </div>
    <div class="form-group"><label>Notes</label><textarea id="f-cnote" rows="2"></textarea></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveChallan()">Save & Generate</button>`);
}

function fillChallanOrder(sel){
  const o = DB.all('orders').find(x=>x.id==sel.value);
  if(o){
    document.getElementById('f-cclient').value = o.client;
    document.getElementById('f-citem').value = o.item;
    document.getElementById('f-cqty').value = o.ready;
  }
}

function saveChallan(){
  const orderId = document.getElementById('f-cord').value;
  if(!orderId){ toast('Select an order','error'); return; }
  const c = {
    id: document.getElementById('f-cid').value,
    orderId, date: document.getElementById('f-cdate').value,
    client: document.getElementById('f-cclient').value,
    item: document.getElementById('f-citem').value,
    qty: +document.getElementById('f-cqty').value,
    vehicle: document.getElementById('f-cveh').value,
    driver: document.getElementById('f-cdrv').value,
    status: document.getElementById('f-cstat').value,
    notes: document.getElementById('f-cnote').value
  };
  DB.push('challans',c);
  closeModal(); renderDelivery(); toast('Challan created!');
}

function delChallan(id){ if(!confirm('Delete challan?')) return; DB.del('challans',id); renderDelivery(); toast('Deleted','error'); }

// ============================================================
// EXPENSES
// ============================================================
function renderExpenses(){
  const expenses = DB.all('expenses');
  const total = expenses.reduce((s,e)=>s+e.amount,0);
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-primary" onclick="openAddExpense()">+ Add Expense</button>`;
  document.getElementById('content-area').innerHTML = `
    <div class="stats-grid" style="grid-template-columns:repeat(4,1fr)">
      ${['Rent','Electricity','Salary','Material'].map(cat=>{
        const amt = expenses.filter(e=>e.type===cat).reduce((s,e)=>s+e.amount,0);
        return `<div class="stat-card red"><div class="stat-label">${cat}</div><div class="stat-value" style="font-size:28px">${fmt(amt)}</div></div>`;
      }).join('')}
    </div>
    <div class="card">
      <div class="card-header">
        <div class="card-title">All Expenses — Total: <span style="color:var(--danger)">${fmt(total)}</span></div>
        <select style="background:var(--bg);border:1px solid var(--border);border-radius:6px;padding:6px 12px;color:var(--text);font-size:12px" onchange="filterExpCat(this.value)">
          <option value="">All Categories</option>
          <option>Fixed</option><option>Utility</option><option>Labour</option><option>Raw Material</option><option>Transport</option><option>Other</option>
        </select>
      </div>
      <div class="table-wrap">
        <table id="exp-table">
          <thead><tr><th>#</th><th>Type</th><th>Category</th><th>Amount</th><th>Date</th><th>Note</th><th>Actions</th></tr></thead>
          <tbody id="exp-tbody">${renderExpRows(expenses)}</tbody>
        </table>
      </div>
    </div>
  `;
}

function renderExpRows(expenses){
  if(!expenses.length) return `<tr><td colspan="7"><div class="empty-state"><div class="icon">💸</div><p>No expenses recorded</p></div></td></tr>`;
  return expenses.map(e=>`
    <tr>
      <td style="font-family:Space Mono;font-size:11px;color:var(--muted)">${e.id}</td>
      <td><strong>${e.type}</strong></td>
      <td><span class="badge badge-grey">${e.category}</span></td>
      <td class="amount negative">${fmt(e.amount)}</td>
      <td class="date-chip">${e.date}</td>
      <td style="color:var(--muted);font-size:12px">${e.note||'—'}</td>
      <td><button class="btn btn-danger btn-sm" onclick="delExp(${e.id})">Delete</button></td>
    </tr>
  `).join('');
}

function filterExpCat(cat){
  const all = DB.all('expenses');
  const filtered = cat ? all.filter(e=>e.category===cat) : all;
  document.getElementById('exp-tbody').innerHTML = renderExpRows(filtered);
}

function openAddExpense(){
  openModal('Add Expense',`
    <div class="form-row">
      <div class="form-group"><label>Expense Type</label>
        <select id="f-etype">
          <option>Rent</option><option>Electricity</option><option>Water Bill</option>
          <option>Salary</option><option>Material</option><option>Transport</option>
          <option>Machine Maintenance</option><option>Food/Canteen</option><option>Other</option>
        </select>
      </div>
      <div class="form-group"><label>Category</label>
        <select id="f-ecat">
          <option>Fixed</option><option>Utility</option><option>Labour</option>
          <option>Raw Material</option><option>Transport</option><option>Other</option>
        </select>
      </div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Amount (₹)</label><input type="number" id="f-eamt" placeholder="5000"></div>
      <div class="form-group"><label>Date</label><input type="date" id="f-edate" value="${today()}"></div>
    </div>
    <div class="form-group"><label>Note / Description</label><input type="text" id="f-enote" placeholder="Optional description"></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveExpense()">Save</button>`);
}

function saveExpense(){
  const amt = +document.getElementById('f-eamt').value;
  if(!amt){ toast('Enter amount','error'); return; }
  DB.push('expenses',{
    type: document.getElementById('f-etype').value,
    category: document.getElementById('f-ecat').value,
    amount: amt,
    date: document.getElementById('f-edate').value,
    note: document.getElementById('f-enote').value
  });
  closeModal(); renderExpenses(); toast('Expense added!');
}

function delExp(id){ if(!confirm('Delete?')) return; DB.del('expenses',id); renderExpenses(); toast('Deleted','error'); }

// ============================================================
// INCOME / BILLS
// ============================================================
function renderIncome(){
  const income = DB.all('income');
  const total = income.reduce((s,i)=>s+i.amount,0);
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-primary" onclick="openAddIncome()">+ Record Payment</button>`;
  document.getElementById('content-area').innerHTML = `
    <div class="stats-grid" style="grid-template-columns:repeat(3,1fr)">
      <div class="stat-card green"><div class="stat-label">Total Received</div><div class="stat-value">${fmt(total)}</div></div>
      <div class="stat-card yellow"><div class="stat-label">Payments Count</div><div class="stat-value">${income.length}</div></div>
      <div class="stat-card orange">
        <div class="stat-label">Outstanding Bills</div>
        <div class="stat-value">${fmt(DB.all('orders').reduce((s,o)=>s+(o.qty*o.ratePerUnit-o.advance),0)-income.filter(i=>!i.advance).reduce((s,i)=>s+i.amount,0))}</div>
      </div>
    </div>
    <div class="card">
      <div class="card-header">
        <div class="card-title">Payment Records</div>
        <button class="btn btn-ghost btn-sm" onclick="generateAllBillsPDF()">Export All Bills PDF</button>
      </div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>ID</th><th>Client</th><th>Order</th><th>Amount</th><th>Date</th><th>Note</th><th>Actions</th></tr></thead>
          <tbody>
            ${income.length===0?`<tr><td colspan="7"><div class="empty-state"><div class="icon">💰</div><p>No payments recorded</p></div></td></tr>`:
            income.map(i=>`
              <tr>
                <td style="font-family:Space Mono;font-size:11px;color:var(--muted)">${i.id}</td>
                <td>${i.client}</td>
                <td style="font-family:Space Mono;font-size:12px">#${i.orderId||'—'}</td>
                <td class="amount positive">${fmt(i.amount)}</td>
                <td class="date-chip">${i.date}</td>
                <td style="color:var(--muted);font-size:12px">${i.note||'—'}</td>
                <td>
                  <div style="display:flex;gap:6px">
                    <button class="btn btn-info btn-sm" onclick="generateBillPDF(${i.orderId})">Bill PDF</button>
                    <button class="btn btn-danger btn-sm" onclick="delIncome(${i.id})">Del</button>
                  </div>
                </td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      </div>
    </div>
  `;
}

function openAddIncome(){
  const orders = DB.all('orders');
  const clients = DB.all('clients');
  openModal('Record Payment',`
    <div class="form-row">
      <div class="form-group"><label>Client</label>
        <select id="f-iclient"><option value="">Select</option>${clients.map(c=>`<option>${c.name}</option>`).join('')}</select>
      </div>
      <div class="form-group"><label>Linked Order</label>
        <select id="f-iorder"><option value="">None</option>${orders.map(o=>`<option value="${o.id}">#${o.id} — ${o.item}</option>`).join('')}</select>
      </div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Amount (₹)</label><input type="number" id="f-iamt" placeholder="10000"></div>
      <div class="form-group"><label>Date</label><input type="date" id="f-idate" value="${today()}"></div>
    </div>
    <div class="form-group"><label>Payment Mode</label>
      <select id="f-imode"><option>Cash</option><option>Bank Transfer</option><option>UPI</option><option>Cheque</option></select>
    </div>
    <div class="form-group"><label>Note</label><input type="text" id="f-inote" placeholder="e.g. Full Payment, Advance"></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveIncome()">Save</button>`);
}

function saveIncome(){
  const amt = +document.getElementById('f-iamt').value;
  if(!amt){ toast('Enter amount','error'); return; }
  DB.push('income',{
    client: document.getElementById('f-iclient').value,
    orderId: document.getElementById('f-iorder').value,
    amount: amt,
    date: document.getElementById('f-idate').value,
    mode: document.getElementById('f-imode').value,
    note: document.getElementById('f-inote').value,
    paid: true
  });
  closeModal(); renderIncome(); toast('Payment recorded!');
}

function delIncome(id){ if(!confirm('Delete?')) return; DB.del('income',id); renderIncome(); toast('Deleted','error'); }

// ============================================================
// PROFIT & LOSS
// ============================================================
function renderProfit(){
  const expenses = DB.all('expenses');
  const income = DB.all('income');
  const totalIncome = income.reduce((s,i)=>s+i.amount,0);
  const totalExpense = expenses.reduce((s,e)=>s+e.amount,0);
  const profit = totalIncome - totalExpense;

  const expByCat = expenses.reduce((acc,e)=>{ acc[e.type]=(acc[e.type]||0)+e.amount; return acc; },{});
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-ghost" onclick="exportPLReport()">Export PDF</button>`;

  document.getElementById('content-area').innerHTML = `
    <div class="grid-2" style="margin-bottom:24px">
      <div class="card">
        <div class="card-header"><div class="card-title" style="color:var(--success)">📈 Income</div></div>
        <div class="card-body">
          ${income.map(i=>`
            <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)">
              <div><div style="font-size:13px">${i.client}</div><div class="date-chip">${i.date}</div></div>
              <span class="amount positive">${fmt(i.amount)}</span>
            </div>
          `).join('')}
          <div style="display:flex;justify-content:space-between;margin-top:12px;padding-top:12px;border-top:2px solid var(--success)">
            <strong>Total Income</strong>
            <strong class="amount positive">${fmt(totalIncome)}</strong>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="card-header"><div class="card-title" style="color:var(--danger)">📉 Expenses</div></div>
        <div class="card-body">
          ${Object.entries(expByCat).map(([k,v])=>`
            <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)">
              <span style="font-size:13px">${k}</span>
              <span class="amount negative">${fmt(v)}</span>
            </div>
          `).join('')}
          <div style="display:flex;justify-content:space-between;margin-top:12px;padding-top:12px;border-top:2px solid var(--danger)">
            <strong>Total Expenses</strong>
            <strong class="amount negative">${fmt(totalExpense)}</strong>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-body" style="text-align:center;padding:40px">
        <div style="font-size:13px;color:var(--muted);letter-spacing:2px;text-transform:uppercase;margin-bottom:8px">Net ${profit>=0?'PROFIT':'LOSS'}</div>
        <div style="font-family:'Bebas Neue';font-size:72px;color:${profit>=0?'var(--success)':'var(--danger)'}">
          ${fmt(Math.abs(profit))}
        </div>
        <div style="font-size:13px;color:var(--muted);margin-top:8px">
          Margin: ${totalIncome?Math.round(profit/totalIncome*100):0}%
        </div>
      </div>
    </div>
  `;
}

// ============================================================
// WORKERS
// ============================================================
function renderWorkers(){
  const workers = DB.all('workers');
  const log = DB.all('workerLog');
  document.getElementById('topbar-actions').innerHTML = `
    <button class="btn btn-ghost" onclick="openAddWorkLog()">+ Log Work</button>
    <button class="btn btn-primary" onclick="openAddWorker()">+ Add Worker</button>
  `;

  document.getElementById('content-area').innerHTML = `
    <div class="tabs">
      <button class="tab-btn active" onclick="switchWorkerTab('cards',this)">Worker Cards</button>
      <button class="tab-btn" onclick="switchWorkerTab('salary',this)">Salary Calculator</button>
      <button class="tab-btn" onclick="switchWorkerTab('log',this)">Work Log</button>
    </div>
    <div id="worker-tab-cards">
      <div class="worker-grid">
        ${workers.map(w=>{
          const wLog = log.filter(l=>l.workerId==w.id);
          const totalUnits = wLog.reduce((s,l)=>s+l.units,0);
          const grossSalary = totalUnits * w.costPerUnit;
          const netSalary = grossSalary - w.advance;
          return `
          <div class="worker-card">
            <div class="worker-card-header">
              <div class="worker-avatar">${w.name[0]}</div>
              <div>
                <div class="worker-name">${w.name}</div>
                <div class="worker-role">${w.role} · ${w.phone}</div>
              </div>
            </div>
            <div class="worker-stats">
              <div class="w-stat">
                <div class="w-stat-label">Units Done</div>
                <div class="w-stat-value" style="color:var(--accent)">${fmtN(totalUnits)}</div>
              </div>
              <div class="w-stat">
                <div class="w-stat-label">Rate/Unit</div>
                <div class="w-stat-value">₹${w.costPerUnit}</div>
              </div>
              <div class="w-stat">
                <div class="w-stat-label">Gross Salary</div>
                <div class="w-stat-value" style="color:var(--success)">${fmt(grossSalary)}</div>
              </div>
              <div class="w-stat">
                <div class="w-stat-label">Advance Paid</div>
                <div class="w-stat-value" style="color:var(--danger)">${fmt(w.advance)}</div>
              </div>
            </div>
            <div style="margin-top:12px;display:flex;justify-content:space-between;align-items:center;padding:10px;background:var(--bg);border-radius:8px">
              <span style="font-size:12px;color:var(--muted)">Net Payable</span>
              <strong style="font-family:Space Mono;color:${netSalary>=0?'var(--success)':'var(--danger)'};font-size:16px">${fmt(netSalary)}</strong>
            </div>
            <div style="margin-top:12px;display:flex;gap:8px">
              <button class="btn btn-ghost btn-sm" style="flex:1" onclick="addAdvance(${w.id})">+ Advance</button>
              <button class="btn btn-info btn-sm" style="flex:1" onclick="workerSalaryPDF(${w.id})">PDF Slip</button>
              <button class="btn btn-ghost btn-sm" onclick="editWorker(${w.id})">Edit</button>
            </div>
          </div>
          `;
        }).join('')}
      </div>
      ${workers.length===0?`<div class="empty-state"><div class="icon">👷</div><p>No workers added yet</p></div>`:''}
    </div>

    <div id="worker-tab-salary" style="display:none">
      <div class="card">
        <div class="card-header"><div class="card-title">Salary Summary</div></div>
        <div class="table-wrap">
          <table>
            <thead><tr><th>Worker</th><th>Role</th><th>Units Done</th><th>Rate/Unit</th><th>Gross Salary</th><th>Advance</th><th>Net Payable</th><th>Actions</th></tr></thead>
            <tbody>
              ${workers.map(w=>{
                const wLog = log.filter(l=>l.workerId==w.id);
                const totalUnits = wLog.reduce((s,l)=>s+l.units,0);
                const gross = totalUnits * w.costPerUnit;
                const net = gross - w.advance;
                return `<tr>
                  <td><strong>${w.name}</strong></td>
                  <td>${w.role}</td>
                  <td style="font-family:Space Mono">${fmtN(totalUnits)}</td>
                  <td>₹${w.costPerUnit}</td>
                  <td class="amount positive">${fmt(gross)}</td>
                  <td class="amount negative">${fmt(w.advance)}</td>
                  <td><strong class="amount ${net>=0?'positive':'negative'}">${fmt(net)}</strong></td>
                  <td><button class="btn btn-info btn-sm" onclick="workerSalaryPDF(${w.id})">PDF Slip</button></td>
                </tr>`;
              }).join('')}
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <div id="worker-tab-log" style="display:none">
      <div class="card">
        <div class="card-header">
          <div class="card-title">Work Log</div>
          <button class="btn btn-primary btn-sm" onclick="openAddWorkLog()">+ Log Work</button>
        </div>
        <div class="table-wrap">
          <table>
            <thead><tr><th>Worker</th><th>Date</th><th>Units</th><th>Note</th><th>Value</th><th>Del</th></tr></thead>
            <tbody>
              ${log.length===0?`<tr><td colspan="6"><div class="empty-state"><div class="icon">📋</div><p>No work logged yet</p></div></td></tr>`:
              log.map(l=>{
                const w = workers.find(x=>x.id==l.workerId);
                return `<tr>
                  <td>${w?w.name:'Unknown'}</td>
                  <td class="date-chip">${l.date}</td>
                  <td style="font-family:Space Mono;color:var(--accent)">${fmtN(l.units)}</td>
                  <td style="color:var(--muted);font-size:12px">${l.note||'—'}</td>
                  <td class="amount positive">${w?fmt(l.units*w.costPerUnit):'—'}</td>
                  <td><button class="btn btn-danger btn-sm" onclick="delLog(${l.id})">Del</button></td>
                </tr>`;
              }).join('')}
            </tbody>
          </table>
        </div>
      </div>
    </div>
  `;
}

function switchWorkerTab(tab, btn){
  document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  ['cards','salary','log'].forEach(t=>{
    const el=document.getElementById('worker-tab-'+t);
    if(el) el.style.display = t===tab?'block':'none';
  });
}

function openAddWorker(){
  openModal('Add Worker',`
    <div class="form-row">
      <div class="form-group"><label>Full Name</label><input type="text" id="f-wname" placeholder="Worker name"></div>
      <div class="form-group"><label>Role</label>
        <select id="f-wrole"><option>Stitching</option><option>Cutting</option><option>Finishing</option><option>Embroidery</option><option>Packing</option><option>Other</option></select>
      </div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Cost per Unit (₹)</label><input type="number" id="f-wcpu" placeholder="8"></div>
      <div class="form-group"><label>Phone</label><input type="text" id="f-wphone" placeholder="9876543210"></div>
    </div>
    <div class="form-group"><label>Join Date</label><input type="date" id="f-wjoin" value="${today()}"></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveWorker()">Add Worker</button>`);
}

function saveWorker(){
  const name = document.getElementById('f-wname').value.trim();
  if(!name){ toast('Enter name','error'); return; }
  DB.push('workers',{
    name, role: document.getElementById('f-wrole').value,
    costPerUnit: +document.getElementById('f-wcpu').value||8,
    phone: document.getElementById('f-wphone').value,
    advance: 0, totalUnits: 0,
    joinDate: document.getElementById('f-wjoin').value
  });
  closeModal(); renderWorkers(); toast('Worker added!');
}

function editWorker(id){
  const w = DB.all('workers').find(x=>x.id==id);
  openModal('Edit Worker',`
    <div class="form-row">
      <div class="form-group"><label>Name</label><input type="text" id="f-wname" value="${w.name}"></div>
      <div class="form-group"><label>Role</label>
        <select id="f-wrole">${['Stitching','Cutting','Finishing','Embroidery','Packing','Other'].map(r=>`<option ${r===w.role?'selected':''}>${r}</option>`).join('')}</select>
      </div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Cost per Unit (₹)</label><input type="number" id="f-wcpu" value="${w.costPerUnit}"></div>
      <div class="form-group"><label>Phone</label><input type="text" id="f-wphone" value="${w.phone}"></div>
    </div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="updateWorker(${id})">Update</button>
     <button class="btn btn-danger" onclick="delWorker(${id})">Delete</button>`);
}

function updateWorker(id){
  DB.update('workers',id,{
    name: document.getElementById('f-wname').value,
    role: document.getElementById('f-wrole').value,
    costPerUnit: +document.getElementById('f-wcpu').value,
    phone: document.getElementById('f-wphone').value
  });
  closeModal(); renderWorkers(); toast('Worker updated!');
}

function delWorker(id){ if(!confirm('Delete worker?')) return; DB.del('workers',id); closeModal(); renderWorkers(); toast('Deleted','error'); }

function addAdvance(id){
  const w = DB.all('workers').find(x=>x.id==id);
  openModal('Add Advance — '+w.name,`
    <p style="color:var(--muted);font-size:13px;margin-bottom:16px">Current advance: <strong style="color:var(--danger)">${fmt(w.advance)}</strong></p>
    <div class="form-group"><label>Additional Advance (₹)</label><input type="number" id="f-advadd" placeholder="500"></div>
    <div class="form-group"><label>Note</label><input type="text" id="f-advnote" placeholder="Reason"></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-danger" onclick="saveAdvance(${id},${w.advance})">Add Advance</button>`);
}

function saveAdvance(id, current){
  const add = +document.getElementById('f-advadd').value||0;
  DB.update('workers',id,{advance: current+add});
  // log it as expense
  DB.push('expenses',{type:'Salary Advance',category:'Labour',amount:add,date:today(),note:document.getElementById('f-advnote').value||'Worker Advance'});
  closeModal(); renderWorkers(); toast('Advance recorded!');
}

function openAddWorkLog(){
  const workers = DB.all('workers');
  openModal('Log Worker Output',`
    <div class="form-group"><label>Worker</label>
      <select id="f-lwid"><option value="">Select Worker</option>${workers.map(w=>`<option value="${w.id}">${w.name} (₹${w.costPerUnit}/unit)</option>`).join('')}</select>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Units Completed</label><input type="number" id="f-lunit" placeholder="120"></div>
      <div class="form-group"><label>Date</label><input type="date" id="f-ldate" value="${today()}"></div>
    </div>
    <div class="form-group"><label>Note</label><input type="text" id="f-lnote" placeholder="Batch / Order ref"></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveWorkLog()">Log</button>`);
}

function saveWorkLog(){
  const wid = document.getElementById('f-lwid').value;
  const units = +document.getElementById('f-lunit').value;
  if(!wid||!units){ toast('Fill all fields','error'); return; }
  DB.push('workerLog',{
    workerId: +wid,
    units,
    date: document.getElementById('f-ldate').value,
    note: document.getElementById('f-lnote').value
  });
  // update worker totalUnits
  const w = DB.all('workers').find(x=>x.id==+wid);
  if(w) DB.update('workers',+wid,{totalUnits:(w.totalUnits||0)+units});
  closeModal(); renderWorkers(); toast('Work logged!');
}

function delLog(id){ if(!confirm('Delete log?')) return; DB.del('workerLog',id); renderWorkers(); toast('Deleted','error'); }

// ============================================================
// CLIENTS
// ============================================================
function renderClients(){
  const clients = DB.all('clients');
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-primary" onclick="openAddClient()">+ Add Client</button>`;
  document.getElementById('content-area').innerHTML = `
    <div class="card">
      <div class="card-header"><div class="card-title">Clients (${clients.length})</div></div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Name</th><th>Contact Person</th><th>Phone</th><th>Email</th><th>City</th><th>Orders</th><th>Actions</th></tr></thead>
          <tbody>
            ${clients.map(c=>{
              const orders = DB.all('orders').filter(o=>o.client===c.name);
              return `<tr>
                <td><strong>${c.name}</strong></td>
                <td>${c.contact||'—'}</td>
                <td>${c.phone||'—'}</td>
                <td style="color:var(--muted);font-size:12px">${c.email||'—'}</td>
                <td>${c.city||'—'}</td>
                <td><span class="badge badge-blue">${orders.length} orders</span></td>
                <td><div style="display:flex;gap:6px">
                  <button class="btn btn-ghost btn-sm" onclick="editClient(${c.id})">Edit</button>
                  <button class="btn btn-danger btn-sm" onclick="delClient(${c.id})">Del</button>
                </div></td>
              </tr>`;
            }).join('')}
          </tbody>
        </table>
      </div>
    </div>
  `;
}

function openAddClient(){
  openModal('Add Client',`
    <div class="form-row">
      <div class="form-group"><label>Company Name</label><input type="text" id="f-cname"></div>
      <div class="form-group"><label>Contact Person</label><input type="text" id="f-ccontact"></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Phone</label><input type="text" id="f-cphone"></div>
      <div class="form-group"><label>Email</label><input type="email" id="f-cemail"></div>
    </div>
    <div class="form-group"><label>City</label><input type="text" id="f-ccity"></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveClient()">Save</button>`);
}

function saveClient(){
  const name = document.getElementById('f-cname').value.trim();
  if(!name){ toast('Enter company name','error'); return; }
  DB.push('clients',{
    name, contact: document.getElementById('f-ccontact').value,
    phone: document.getElementById('f-cphone').value,
    email: document.getElementById('f-cemail').value,
    city: document.getElementById('f-ccity').value
  });
  closeModal(); renderClients(); toast('Client added!');
}

function editClient(id){
  const c = DB.all('clients').find(x=>x.id==id);
  openModal('Edit Client',`
    <div class="form-row">
      <div class="form-group"><label>Company Name</label><input type="text" id="f-cname" value="${c.name}"></div>
      <div class="form-group"><label>Contact Person</label><input type="text" id="f-ccontact" value="${c.contact||''}"></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label>Phone</label><input type="text" id="f-cphone" value="${c.phone||''}"></div>
      <div class="form-group"><label>Email</label><input type="email" id="f-cemail" value="${c.email||''}"></div>
    </div>
    <div class="form-group"><label>City</label><input type="text" id="f-ccity" value="${c.city||''}"></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="updateClient(${id})">Update</button>`);
}

function updateClient(id){
  DB.update('clients',id,{
    name:document.getElementById('f-cname').value,
    contact:document.getElementById('f-ccontact').value,
    phone:document.getElementById('f-cphone').value,
    email:document.getElementById('f-cemail').value,
    city:document.getElementById('f-ccity').value
  });
  closeModal(); renderClients(); toast('Updated!');
}

function delClient(id){ if(!confirm('Delete client?')) return; DB.del('clients',id); renderClients(); toast('Deleted','error'); }

// ============================================================
// INVENTORY
// ============================================================
function renderInventory(){
  const inv = DB.all('inventory');
  document.getElementById('topbar-actions').innerHTML = `<button class="btn btn-primary" onclick="openAddInv()">+ Add Item</button>`;
  document.getElementById('content-area').innerHTML = `
    <div class="card">
      <div class="card-header"><div class="card-title">Raw Material Inventory</div></div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Item</th><th>Qty</th><th>Unit</th><th>Min Qty</th><th>Status</th><th>Cost/Unit</th><th>Total Value</th><th>Last Updated</th><th>Actions</th></tr></thead>
          <tbody>
            ${inv.map(i=>`
              <tr>
                <td><strong>${i.item}</strong></td>
                <td style="font-family:Space Mono">${fmtN(i.qty)}</td>
                <td>${i.unit}</td>
                <td style="font-family:Space Mono;color:var(--muted)">${fmtN(i.minQty)}</td>
                <td>${i.qty<=i.minQty?`<span class="badge badge-red">LOW STOCK</span>`:`<span class="badge badge-green">OK</span>`}</td>
                <td>${fmt(i.cost)}</td>
                <td class="amount">${fmt(i.qty*i.cost)}</td>
                <td class="date-chip">${i.updatedAt}</td>
                <td><div style="display:flex;gap:6px">
                  <button class="btn btn-ghost btn-sm" onclick="editInv(${i.id})">Update</button>
                  <button class="btn btn-danger btn-sm" onclick="delInv(${i.id})">Del</button>
                </div></td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      </div>
    </div>
  `;
}

function openAddInv(){
  openModal('Add Inventory Item',`
    <div class="form-row">
      <div class="form-group"><label>Item Name</label><input type="text" id="f-iname" placeholder="Cotton Fabric"></div>
      <div class="form-group"><label>Unit</label>
        <select id="f-iunit"><option>Meters</option><option>Kg</option><option>Spools</option><option>Pieces</option><option>Rolls</option><option>Boxes</option></select>
      </div>
    </div>
    <div class="form-row-3">
      <div class="form-group"><label>Quantity</label><input type="number" id="f-iqty" placeholder="100"></div>
      <div class="form-group"><label>Min Qty</label><input type="number" id="f-imin" placeholder="20"></div>
      <div class="form-group"><label>Cost/Unit (₹)</label><input type="number" id="f-icost" placeholder="120"></div>
    </div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="saveInv()">Add</button>`);
}

function saveInv(){
  const name = document.getElementById('f-iname').value.trim();
  if(!name){ toast('Enter item name','error'); return; }
  DB.push('inventory',{
    item:name, unit:document.getElementById('f-iunit').value,
    qty:+document.getElementById('f-iqty').value||0,
    minQty:+document.getElementById('f-imin').value||10,
    cost:+document.getElementById('f-icost').value||0,
    updatedAt:today()
  });
  closeModal(); renderInventory(); toast('Item added!');
}

function editInv(id){
  const i = DB.all('inventory').find(x=>x.id==id);
  openModal('Update Stock — '+i.item,`
    <div class="form-row">
      <div class="form-group"><label>Current Qty</label><input type="number" id="f-iqty" value="${i.qty}"></div>
      <div class="form-group"><label>Min Qty Alert</label><input type="number" id="f-imin" value="${i.minQty}"></div>
    </div>
    <div class="form-group"><label>Cost per Unit (₹)</label><input type="number" id="f-icost" value="${i.cost}"></div>
  `,`<button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
     <button class="btn btn-primary" onclick="updateInv(${id})">Update</button>`);
}

function updateInv(id){
  DB.update('inventory',id,{
    qty:+document.getElementById('f-iqty').value,
    minQty:+document.getElementById('f-imin').value,
    cost:+document.getElementById('f-icost').value,
    updatedAt:today()
  });
  closeModal(); renderInventory(); toast('Stock updated!');
}

function delInv(id){ if(!confirm('Delete?')) return; DB.del('inventory',id); renderInventory(); toast('Deleted','error'); }

// ============================================================
// REPORTS
// ============================================================
function renderReports(){
  const orders = DB.all('orders');
  const income = DB.all('income');
  const expenses = DB.all('expenses');
  const workers = DB.all('workers');
  const log = DB.all('workerLog');

  document.getElementById('topbar-actions').innerHTML = '';
  document.getElementById('content-area').innerHTML = `
    <div class="grid-3" style="margin-bottom:24px">
      <div class="card" style="cursor:pointer;transition:border-color .2s" onmouseover="this.style.borderColor='var(--accent)'" onmouseout="this.style.borderColor='var(--border)'" onclick="exportPLReport()">
        <div class="card-body" style="text-align:center;padding:30px">
          <div style="font-size:36px;margin-bottom:12px">📊</div>
          <div style="font-weight:700;font-size:15px">P&L Report</div>
          <div style="font-size:12px;color:var(--muted);margin-top:4px">Profit & Loss PDF</div>
        </div>
      </div>
      <div class="card" style="cursor:pointer;transition:border-color .2s" onmouseover="this.style.borderColor='var(--accent)'" onmouseout="this.style.borderColor='var(--border)'" onclick="exportWorkersReport()">
        <div class="card-body" style="text-align:center;padding:30px">
          <div style="font-size:36px;margin-bottom:12px">👷</div>
          <div style="font-weight:700;font-size:15px">Workers Report</div>
          <div style="font-size:12px;color:var(--muted);margin-top:4px">Salary Summary PDF</div>
        </div>
      </div>
      <div class="card" style="cursor:pointer;transition:border-color .2s" onmouseover="this.style.borderColor='var(--accent)'" onmouseout="this.style.borderColor='var(--border)'" onclick="exportOrdersReport()">
        <div class="card-body" style="text-align:center;padding:30px">
          <div style="font-size:36px;margin-bottom:12px">📦</div>
          <div style="font-weight:700;font-size:15px">Orders Report</div>
          <div style="font-size:12px;color:var(--muted);margin-top:4px">Full Orders PDF</div>
        </div>
      </div>
    </div>

    <div class="grid-2">
      <div class="card">
        <div class="card-header"><div class="card-title">Orders by Status</div></div>
        <div class="card-body">
          ${['Pending','In Progress','Completed','Cancelled'].map(s=>{
            const count = orders.filter(o=>o.status===s).length;
            const pct = orders.length ? Math.round(count/orders.length*100) : 0;
            return `<div style="margin-bottom:14px">
              <div style="display:flex;justify-content:space-between;margin-bottom:4px">
                <span style="font-size:13px">${statusBadge(s)}</span>
                <span style="font-size:12px;color:var(--muted)">${count} orders · ${pct}%</span>
              </div>
              <div class="progress-bar"><div class="progress-fill" style="width:${pct}%"></div></div>
            </div>`;
          }).join('')}
        </div>
      </div>

      <div class="card">
        <div class="card-header"><div class="card-title">Top Workers by Output</div></div>
        <div class="card-body">
          ${workers.map(w=>{
            const units = log.filter(l=>l.workerId==w.id).reduce((s,l)=>s+l.units,0);
            return {w,units};
          }).sort((a,b)=>b.units-a.units).slice(0,5).map(({w,units},i)=>`
            <div style="display:flex;align-items:center;gap:12px;margin-bottom:12px">
              <div style="font-family:Space Mono;font-size:11px;color:var(--muted);width:16px">${i+1}</div>
              <div class="worker-avatar" style="width:32px;height:32px;font-size:13px">${w.name[0]}</div>
              <div style="flex:1">
                <div style="font-size:13px;font-weight:600">${w.name}</div>
                <div style="font-size:11px;color:var(--muted)">${w.role}</div>
              </div>
              <span style="font-family:Space Mono;font-size:13px;color:var(--accent)">${fmtN(units)} units</span>
            </div>
          `).join('')}
        </div>
      </div>
    </div>
  `;
}

// ============================================================
// PDF GENERATION
// ============================================================
function generateBillPDF(orderId){
  const o = DB.all('orders').find(x=>x.id==orderId);
  if(!o){ toast('Order not found','error'); return; }
  const payments = DB.all('income').filter(i=>i.orderId==orderId);
  const totalPaid = payments.reduce((s,p)=>s+p.amount,0) + o.advance;
  const totalValue = o.qty * o.ratePerUnit;
  const balance = totalValue - totalPaid;

  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  // Header
  doc.setFillColor(232,197,71);
  doc.rect(0,0,210,35,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(22);
  doc.setTextColor(0,0,0);
  doc.text('DEVINE VENTURES', 14, 18);
  doc.setFontSize(9);
  doc.setFont('helvetica','normal');
  doc.text('Garment Manufacturing | Factory Management', 14, 26);
  doc.text('Mumbai, Maharashtra | Phone: +91 98765 43210', 14, 32);

  // Bill title
  doc.setFontSize(16);
  doc.setFont('helvetica','bold');
  doc.setTextColor(50,50,50);
  doc.text('TAX INVOICE / BILL', 14, 50);

  // Invoice details
  doc.setFontSize(10);
  doc.setFont('helvetica','normal');
  doc.setTextColor(80,80,80);
  doc.text(`Invoice No: INV-${o.id}`, 14, 62);
  doc.text(`Date: ${today()}`, 14, 69);
  doc.text(`Due Date: ${o.dueDate}`, 14, 76);

  doc.text(`Bill To:`, 120, 62);
  doc.setFont('helvetica','bold');
  doc.text(o.client, 120, 69);
  doc.setFont('helvetica','normal');

  // Line
  doc.setDrawColor(220,220,220);
  doc.line(14, 85, 196, 85);

  // Table header
  doc.setFillColor(245,245,245);
  doc.rect(14, 88, 182, 10, 'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(9);
  doc.setTextColor(50,50,50);
  doc.text('Item / Description', 18, 95);
  doc.text('Qty', 100, 95);
  doc.text('Rate (₹)', 130, 95);
  doc.text('Amount (₹)', 162, 95);

  // Item row
  doc.setFont('helvetica','normal');
  doc.setFontSize(10);
  doc.text(o.item, 18, 108);
  doc.text(String(o.qty), 100, 108);
  doc.text(String(o.ratePerUnit), 130, 108);
  doc.text(totalValue.toLocaleString('en-IN'), 162, 108);

  // Totals
  doc.line(14, 118, 196, 118);
  doc.setFont('helvetica','bold');
  doc.text('Sub Total:', 130, 128);
  doc.text('₹'+totalValue.toLocaleString('en-IN'), 162, 128);

  doc.setFont('helvetica','normal');
  doc.setTextColor(150,0,0);
  doc.text('Advance Received:', 130, 136);
  doc.text('₹'+o.advance.toLocaleString('en-IN'), 162, 136);

  payments.forEach((p,idx)=>{
    doc.text(`Payment ${idx+1} (${p.date}):`, 130, 144+idx*8);
    doc.text('₹'+p.amount.toLocaleString('en-IN'), 162, 144+idx*8);
  });

  const afterPayments = 144 + payments.length*8 + 4;
  doc.setFillColor(232,197,71);
  doc.rect(125, afterPayments, 71, 12, 'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(11);
  doc.setTextColor(0,0,0);
  doc.text('BALANCE DUE:', 130, afterPayments+9);
  doc.text('₹'+balance.toLocaleString('en-IN'), 162, afterPayments+9);

  // Status
  doc.setFontSize(10);
  doc.setTextColor(80,80,80);
  doc.setFont('helvetica','normal');
  doc.text(`Order Status: ${o.status}`, 14, afterPayments+20);

  // Footer
  doc.setTextColor(150,150,150);
  doc.setFontSize(8);
  doc.text('Thank you for your business! — DEVINE VENTURES', 14, 280);
  doc.text('This is a computer generated invoice.', 14, 285);

  doc.save(`Bill_${o.client}_${o.id}.pdf`);
  toast('Bill PDF downloaded!');
}

function printChallanPDF(cid){
  const c = DB.all('challans').find(x=>x.id===cid);
  if(!c){ toast('Challan not found','error'); return; }
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  // Header
  doc.setFillColor(30,30,36);
  doc.rect(0,0,210,32,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(20);
  doc.setTextColor(232,197,71);
  doc.text('DEVINE VENTURES', 14, 16);
  doc.setFontSize(9);
  doc.setTextColor(200,200,200);
  doc.text('DELIVERY CHALLAN', 14, 26);

  doc.setTextColor(50,50,50);
  doc.setFontSize(16);
  doc.setFont('helvetica','bold');
  doc.text('DELIVERY CHALLAN', 105, 48, {align:'center'});

  doc.setFontSize(10);
  doc.setFont('helvetica','normal');
  doc.setTextColor(80,80,80);
  // Box
  doc.setDrawColor(220,220,220);
  doc.rect(14,55,90,40);
  doc.rect(110,55,86,40);

  doc.setFont('helvetica','bold');
  doc.text('Challan Details:', 18, 63);
  doc.setFont('helvetica','normal');
  doc.text(`Challan No: ${c.id}`, 18, 71);
  doc.text(`Date: ${c.date}`, 18, 79);
  doc.text(`Order Ref: #${c.orderId}`, 18, 87);

  doc.setFont('helvetica','bold');
  doc.text('Consignee:', 114, 63);
  doc.setFont('helvetica','normal');
  doc.text(c.client, 114, 71);

  // Item table
  doc.setFillColor(245,245,245);
  doc.rect(14,105,182,10,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(9);
  doc.setTextColor(50,50,50);
  doc.text('Description', 18, 112);
  doc.text('Quantity', 140, 112);
  doc.text('Unit', 175, 112);

  doc.setFont('helvetica','normal');
  doc.setFontSize(10);
  doc.text(c.item, 18, 124);
  doc.text(String(c.qty), 140, 124);
  doc.text('Pieces', 175, 124);
  doc.line(14,130,196,130);

  doc.setFont('helvetica','bold');
  doc.text(`Total Quantity: ${c.qty} Pieces`, 14, 140);

  doc.setFont('helvetica','normal');
  doc.setTextColor(80,80,80);
  doc.text(`Vehicle No: ${c.vehicle}`, 14, 155);
  doc.text(`Driver: ${c.driver}`, 14, 163);
  doc.text(`Status: ${c.status}`, 14, 171);
  if(c.notes) doc.text(`Notes: ${c.notes}`, 14, 179);

  // Signatures
  doc.line(14,240,80,240);
  doc.line(130,240,196,240);
  doc.setFontSize(9);
  doc.text('Authorised Signature', 14, 248);
  doc.text('Receiver Signature', 130, 248);
  doc.text('DEVINE VENTURES', 14, 254);
  doc.text('(With Stamp)', 130, 254);

  doc.setTextColor(150,150,150);
  doc.setFontSize(8);
  doc.text('This is a computer generated delivery challan — DEVINE VENTURES', 14, 285);

  doc.save(`Challan_${c.id}.pdf`);
  toast('Challan PDF downloaded!');
}

function workerSalaryPDF(wid){
  const w = DB.all('workers').find(x=>x.id==wid);
  const log = DB.all('workerLog').filter(l=>l.workerId==wid);
  const totalUnits = log.reduce((s,l)=>s+l.units,0);
  const gross = totalUnits * w.costPerUnit;
  const net = gross - w.advance;

  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  doc.setFillColor(232,197,71);
  doc.rect(0,0,210,30,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(18);
  doc.setTextColor(0,0,0);
  doc.text('DEVINE VENTURES', 14, 14);
  doc.setFontSize(9);
  doc.setFont('helvetica','normal');
  doc.text('SALARY SLIP', 14, 24);

  doc.setTextColor(50,50,50);
  doc.setFontSize(13);
  doc.setFont('helvetica','bold');
  doc.text('WORKER SALARY SLIP', 105, 45, {align:'center'});

  doc.setFontSize(10);
  doc.setFont('helvetica','normal');
  doc.setTextColor(80,80,80);
  doc.text(`Name: ${w.name}`, 14, 58);
  doc.text(`Role: ${w.role}`, 14, 66);
  doc.text(`Phone: ${w.phone}`, 14, 74);
  doc.text(`Generated: ${today()}`, 130, 58);

  doc.line(14,82,196,82);

  doc.setFont('helvetica','bold');
  doc.setFillColor(245,245,245);
  doc.rect(14,86,182,10,'F');
  doc.setFontSize(9);
  doc.text('Date', 18, 93);
  doc.text('Units', 90, 93);
  doc.text('Note', 130, 93);

  doc.setFont('helvetica','normal');
  doc.setFontSize(9);
  let y=105;
  log.forEach(l=>{
    doc.text(l.date, 18, y);
    doc.text(String(l.units), 90, y);
    doc.text(l.note||'—', 130, y);
    y+=8;
  });

  doc.line(14,y+2,196,y+2);
  y+=12;
  doc.setFont('helvetica','bold');
  doc.setFontSize(10);
  doc.text(`Total Units: ${totalUnits}`, 14, y);
  doc.text(`Rate per Unit: ₹${w.costPerUnit}`, 14, y+8);
  doc.setTextColor(0,120,0);
  doc.text(`Gross Salary: ₹${gross.toLocaleString('en-IN')}`, 14, y+18);
  doc.setTextColor(180,0,0);
  doc.text(`Advance Deduction: ₹${w.advance.toLocaleString('en-IN')}`, 14, y+26);

  doc.setFillColor(232,197,71);
  doc.rect(14,y+32,182,14,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(12);
  doc.setTextColor(0,0,0);
  doc.text(`NET PAYABLE: ₹${net.toLocaleString('en-IN')}`, 105, y+41, {align:'center'});

  doc.setTextColor(150,150,150);
  doc.setFontSize(8);
  doc.text('DEVINE VENTURES — Confidential Salary Slip', 14, 280);

  doc.save(`Salary_${w.name.replace(' ','_')}.pdf`);
  toast('Salary PDF downloaded!');
}

function exportPLReport(){
  const income = DB.all('income');
  const expenses = DB.all('expenses');
  const totalIncome = income.reduce((s,i)=>s+i.amount,0);
  const totalExpense = expenses.reduce((s,e)=>s+e.amount,0);
  const profit = totalIncome - totalExpense;

  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  doc.setFillColor(30,30,36);
  doc.rect(0,0,210,30,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(18);
  doc.setTextColor(232,197,71);
  doc.text('DEVINE VENTURES', 14, 14);
  doc.setFontSize(9);
  doc.setTextColor(200,200,200);
  doc.text('PROFIT & LOSS REPORT | '+today(), 14, 24);

  doc.setTextColor(50,50,50);
  doc.setFontSize(12);
  doc.setFont('helvetica','bold');
  doc.text('INCOME', 14, 46);
  doc.setFont('helvetica','normal');
  doc.setFontSize(9);
  let y=54;
  income.forEach(i=>{ doc.text(`${i.client} (${i.date})`, 18, y); doc.text('₹'+i.amount.toLocaleString('en-IN'), 160, y); y+=7; });
  doc.setFont('helvetica','bold');
  doc.setTextColor(0,120,0);
  doc.text('Total Income: ₹'+totalIncome.toLocaleString('en-IN'), 18, y+4);
  y+=14;

  doc.setTextColor(50,50,50);
  doc.setFontSize(12);
  doc.setFont('helvetica','bold');
  doc.text('EXPENSES', 14, y);
  doc.setFont('helvetica','normal');
  doc.setFontSize(9);
  y+=8;
  expenses.forEach(e=>{ doc.text(`${e.type} (${e.date})`, 18, y); doc.text('₹'+e.amount.toLocaleString('en-IN'), 160, y); y+=7; });
  doc.setFont('helvetica','bold');
  doc.setTextColor(180,0,0);
  doc.text('Total Expenses: ₹'+totalExpense.toLocaleString('en-IN'), 18, y+4);
  y+=14;

  doc.setFillColor(profit>=0?0:180,profit>=0?120:0,0);
  doc.rect(14,y,182,16,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(13);
  doc.setTextColor(255,255,255);
  doc.text(`NET ${profit>=0?'PROFIT':'LOSS'}: ₹${Math.abs(profit).toLocaleString('en-IN')}`, 105, y+11, {align:'center'});

  doc.save('PL_Report_DEVINE_VENTURES.pdf');
  toast('P&L Report downloaded!');
}

function exportWorkersReport(){
  const workers = DB.all('workers');
  const log = DB.all('workerLog');
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  doc.setFillColor(232,197,71);
  doc.rect(0,0,210,30,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(18);
  doc.setTextColor(0,0,0);
  doc.text('DEVINE VENTURES', 14, 16);
  doc.setFontSize(9);
  doc.text('WORKERS SALARY REPORT | '+today(), 14, 25);

  let y=45;
  doc.setFillColor(240,240,240);
  doc.rect(14,y,182,10,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(9);
  doc.setTextColor(50,50,50);
  doc.text('Worker', 18, y+7);
  doc.text('Role', 65, y+7);
  doc.text('Units', 100, y+7);
  doc.text('Rate', 125, y+7);
  doc.text('Gross', 148, y+7);
  doc.text('Advance', 172, y+7);
  y+=18;

  doc.setFont('helvetica','normal');
  workers.forEach(w=>{
    const units = log.filter(l=>l.workerId==w.id).reduce((s,l)=>s+l.units,0);
    const gross = units*w.costPerUnit;
    doc.text(w.name, 18, y);
    doc.text(w.role, 65, y);
    doc.text(String(units), 100, y);
    doc.text('₹'+w.costPerUnit, 125, y);
    doc.text('₹'+gross.toLocaleString('en-IN'), 148, y);
    doc.text('₹'+w.advance.toLocaleString('en-IN'), 172, y);
    y+=8;
  });

  doc.save('Workers_Report_DEVINE_VENTURES.pdf');
  toast('Workers Report downloaded!');
}

function exportOrdersReport(){
  const orders = DB.all('orders');
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF('l','mm','a4'); // landscape

  doc.setFillColor(30,30,36);
  doc.rect(0,0,297,25,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(16);
  doc.setTextColor(232,197,71);
  doc.text('DEVINE VENTURES — ORDERS REPORT', 14, 16);

  let y=38;
  doc.setFillColor(240,240,240);
  doc.rect(14,y,269,10,'F');
  doc.setFont('helvetica','bold');
  doc.setFontSize(8);
  doc.setTextColor(50,50,50);
  ['Order ID','Client','Item','Qty','Ready','Rate','Total Value','Advance','Balance','Due Date','Status'].forEach((h,i)=>{
    doc.text(h, [18,42,80,115,130,145,162,185,205,225,248][i], y+7);
  });
  y+=16;
  doc.setFont('helvetica','normal');
  orders.forEach(o=>{
    const tv = o.qty*o.ratePerUnit;
    const bal = tv-o.advance;
    const vals = [`#${o.id}`,o.client,o.item,String(o.qty),String(o.ready),'₹'+o.ratePerUnit,'₹'+tv.toLocaleString('en-IN'),'₹'+o.advance.toLocaleString('en-IN'),'₹'+bal.toLocaleString('en-IN'),o.dueDate,o.status];
    vals.forEach((v,i)=>{
      doc.text(String(v).substring(0,14), [18,42,80,115,130,145,162,185,205,225,248][i], y);
    });
    y+=8;
    if(y>185){doc.addPage();y=20;}
  });
  doc.save('Orders_Report_DEVINE_VENTURES.pdf');
  toast('Orders Report downloaded!');
}

// ============================================================
// CLIENT PORTAL
// ============================================================
function renderClientOrders(){
  // Client sees only their orders (Reliance Retail)
  const orders = DB.all('orders').filter(o=>o.client==='Reliance Retail');
  document.getElementById('topbar-actions').innerHTML = '';
  document.getElementById('content-area').innerHTML = `
    <div style="background:rgba(232,197,71,0.08);border:1px solid rgba(232,197,71,0.2);border-radius:var(--radius);padding:16px 20px;margin-bottom:24px;display:flex;align-items:center;gap:12px">
      <span style="font-size:24px">👋</span>
      <div><div style="font-weight:600">Welcome, Reliance Retail</div><div style="font-size:12px;color:var(--muted)">Here are all your active orders with Devine Ventures</div></div>
    </div>

    <div class="stats-grid" style="grid-template-columns:repeat(3,1fr);margin-bottom:24px">
      <div class="stat-card yellow"><div class="stat-label">Total Orders</div><div class="stat-value">${orders.length}</div></div>
      <div class="stat-card green"><div class="stat-label">Units Ready</div><div class="stat-value">${fmtN(orders.reduce((s,o)=>s+o.ready,0))}</div></div>
      <div class="stat-card orange"><div class="stat-label">Total Value</div><div class="stat-value" style="font-size:28px">${fmt(orders.reduce((s,o)=>s+o.qty*o.ratePerUnit,0))}</div></div>
    </div>

    ${orders.map(o=>{
      const pct = o.qty?Math.round(o.ready/o.qty*100):0;
      return `
      <div class="card" style="margin-bottom:16px">
        <div class="card-header">
          <div>
            <div style="font-weight:700;font-size:15px">${o.item} <span style="font-family:Space Mono;font-size:12px;color:var(--muted)">#${o.id}</span></div>
            <div style="font-size:12px;color:var(--muted)">Due: ${o.dueDate}</div>
          </div>
          ${statusBadge(o.status)}
        </div>
        <div class="card-body">
          <div class="grid-2" style="margin-bottom:16px">
            <div>
              <div style="font-size:12px;color:var(--muted);margin-bottom:4px">ORDER QUANTITY</div>
              <div style="font-family:Space Mono;font-size:20px;font-weight:700">${fmtN(o.qty)}</div>
            </div>
            <div>
              <div style="font-size:12px;color:var(--muted);margin-bottom:4px">UNITS READY</div>
              <div style="font-family:Space Mono;font-size:20px;font-weight:700;color:var(--success)">${fmtN(o.ready)}</div>
            </div>
          </div>
          <div style="margin-bottom:8px;display:flex;justify-content:space-between;font-size:12px">
            <span style="color:var(--muted)">Production Progress</span>
            <strong>${pct}%</strong>
          </div>
          <div class="progress-bar" style="height:10px">
            <div class="progress-fill" style="width:${pct}%;height:100%;background:${pct>=100?'var(--success)':pct>=50?'var(--accent)':'var(--accent2)'}"></div>
          </div>
          <div style="margin-top:12px;font-size:12px;color:var(--muted)">
            Total Value: <strong style="color:var(--text)">${fmt(o.qty*o.ratePerUnit)}</strong> &nbsp;·&nbsp;
            Advance Paid: <strong style="color:var(--success)">${fmt(o.advance)}</strong> &nbsp;·&nbsp;
            Balance: <strong style="color:var(--danger)">${fmt(o.qty*o.ratePerUnit-o.advance)}</strong>
          </div>
        </div>
      </div>`;
    }).join('')}
    ${orders.length===0?`<div class="empty-state"><div class="icon">📦</div><p>No orders found</p></div>`:''}
  `;
}

function renderClientBills(){
  const orders = DB.all('orders').filter(o=>o.client==='Reliance Retail');
  const payments = DB.all('income').filter(i=>i.client==='Reliance Retail');
  document.getElementById('topbar-actions').innerHTML = '';
  document.getElementById('content-area').innerHTML = `
    <div class="card">
      <div class="card-header"><div class="card-title">My Bills & Payments</div></div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Order</th><th>Item</th><th>Total Value</th><th>Advance</th><th>Balance</th><th>Actions</th></tr></thead>
          <tbody>
            ${orders.map(o=>`
              <tr>
                <td style="font-family:Space Mono;color:var(--accent)">#${o.id}</td>
                <td>${o.item}</td>
                <td class="amount">${fmt(o.qty*o.ratePerUnit)}</td>
                <td class="amount positive">${fmt(o.advance)}</td>
                <td class="amount negative">${fmt(o.qty*o.ratePerUnit-o.advance)}</td>
                <td><button class="btn btn-info btn-sm" onclick="generateBillPDF(${o.id})">Download Bill PDF</button></td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      </div>
    </div>
  `;
}

function renderClientChallans(){
  const challans = DB.all('challans').filter(c=>c.client==='Reliance Retail');
  document.getElementById('topbar-actions').innerHTML = '';
  document.getElementById('content-area').innerHTML = `
    <div class="card">
      <div class="card-header"><div class="card-title">My Delivery Challans</div></div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Challan No</th><th>Item</th><th>Qty</th><th>Date</th><th>Status</th><th>Download</th></tr></thead>
          <tbody>
            ${challans.length===0?`<tr><td colspan="6"><div class="empty-state"><div class="icon">🚚</div><p>No challans yet</p></div></td></tr>`:
            challans.map(c=>`
              <tr>
                <td style="font-family:Space Mono;color:var(--accent)">${c.id}</td>
                <td>${c.item}</td>
                <td>${fmtN(c.qty)}</td>
                <td class="date-chip">${c.date}</td>
                <td>${statusBadge(c.status)}</td>
                <td><button class="btn btn-info btn-sm" onclick="printChallanPDF('${c.id}')">📄 Download PDF</button></td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      </div>
    </div>
  `;
}

// ============================================================
// INIT
// ============================================================
seedData();
</script>
</body>
</html>
