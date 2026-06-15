<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pro Trader OS — Abdi Qani</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0d0f14;--bg2:#13161e;--bg3:#1a1e28;
  --gold:#c9a84c;--gold2:#e8c96a;
  --text:#e8e8e8;--muted:#8a8f9e;--dim:#555b6e;
  --border:#252a38;--border2:#2e3447;
  --green:#2ecc71;--red:#e74c3c;--blue:#4a9eff;--amber:#f0a500;
  --radius:8px;--font:system-ui,sans-serif;--mono:'Courier New',monospace;
}
body{font-family:var(--font);background:var(--bg);color:var(--text);min-height:100vh;display:flex;flex-direction:column}
#app{display:flex;min-height:100vh}
nav{width:56px;background:var(--bg2);border-right:1px solid var(--border);display:flex;flex-direction:column;align-items:center;padding:12px 0;gap:4px;flex-shrink:0;position:fixed;top:0;left:0;bottom:0;z-index:50}
.nav-logo{width:32px;height:32px;background:var(--gold);border-radius:6px;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:13px;color:#000;margin-bottom:12px;font-family:var(--mono)}
.nav-btn{width:40px;height:40px;border-radius:var(--radius);border:none;background:transparent;color:var(--muted);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:18px;transition:all .15s;position:relative}
.nav-btn:hover{background:var(--bg3);color:var(--gold)}
.nav-btn.active{background:rgba(201,168,76,.12);color:var(--gold)}
.nav-tip{position:absolute;left:48px;background:var(--bg3);border:1px solid var(--border2);color:var(--text);font-size:11px;padding:4px 8px;border-radius:4px;white-space:nowrap;pointer-events:none;opacity:0;transition:opacity .15s;z-index:100}
.nav-btn:hover .nav-tip{opacity:1}
main{flex:1;margin-left:56px;display:flex;flex-direction:column;min-height:100vh}
.page{display:none;flex-direction:column;min-height:100vh}
.page.active{display:flex}
.topbar{display:flex;align-items:center;justify-content:space-between;padding:10px 16px;border-bottom:1px solid var(--border);background:var(--bg2);flex-shrink:0;position:sticky;top:0;z-index:40}
.topbar h1{font-size:14px;font-weight:600;color:var(--text);letter-spacing:.3px}
.clock{font-family:var(--mono);font-size:12px;color:var(--gold);background:rgba(201,168,76,.08);padding:4px 10px;border-radius:4px;border:1px solid rgba(201,168,76,.2)}
.badge{font-size:10px;padding:2px 7px;border-radius:3px;font-weight:600;letter-spacing:.5px}
.badge.bull{background:rgba(46,204,113,.12);color:var(--green);border:1px solid rgba(46,204,113,.2)}
.badge.bear{background:rgba(231,76,60,.12);color:var(--red);border:1px solid rgba(231,76,60,.2)}
.badge.neutral{background:rgba(255,255,255,.06);color:var(--muted);border:1px solid var(--border2)}
.content{padding:14px;flex:1}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.grid3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px}
.grid4{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:10px}
.card{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius);padding:12px 14px}
.card-title{font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--muted);margin-bottom:8px}
.metric-val{font-size:22px;font-weight:600;font-family:var(--mono)}
.metric-sub{font-size:11px;color:var(--muted);margin-top:2px}
.green{color:var(--green)}.red{color:var(--red)}.gold{color:var(--gold)}.blue{color:var(--blue)}.amber{color:var(--amber)}
.section-title{font-size:11px;text-transform:uppercase;letter-spacing:1px;color:var(--dim);margin:14px 0 8px;border-bottom:1px solid var(--border);padding-bottom:6px}
table{width:100%;border-collapse:collapse;font-size:12px}
th{text-align:left;padding:6px 8px;color:var(--muted);font-size:10px;letter-spacing:.8px;border-bottom:1px solid var(--border);font-weight:500}
td{padding:6px 8px;border-bottom:1px solid rgba(255,255,255,.03)}
tr:hover td{background:rgba(255,255,255,.02)}
.btn{padding:6px 14px;border-radius:var(--radius);border:1px solid var(--border2);background:var(--bg3);color:var(--text);font-size:12px;cursor:pointer;transition:all .15s}
.btn:hover{border-color:var(--gold);color:var(--gold)}
.btn-gold{background:var(--gold);color:#000;border-color:var(--gold);font-weight:600}
.btn-gold:hover{background:var(--gold2);color:#000}
.btn-sm{padding:4px 10px;font-size:11px}
input,select,textarea{background:var(--bg3);border:1px solid var(--border2);border-radius:var(--radius);color:var(--text);font-size:12px;padding:7px 10px;width:100%;font-family:var(--font);outline:none}
input:focus,select:focus,textarea:focus{border-color:var(--gold);box-shadow:0 0 0 2px rgba(201,168,76,.12)}
textarea{resize:vertical;min-height:70px}
label{font-size:11px;color:var(--muted);margin-bottom:4px;display:block;letter-spacing:.3px}
.field{margin-bottom:10px}
.row{display:flex;gap:10px;align-items:center}
.row.sb{justify-content:space-between}
.dxy-bar{height:4px;background:var(--border);border-radius:2px;margin-top:6px;overflow:hidden}
.dxy-fill{height:100%;background:linear-gradient(90deg,var(--red),var(--amber),var(--green));border-radius:2px;transition:width .4s}
.pnl-bar{display:flex;height:28px;border-radius:4px;overflow:hidden;margin-top:8px}
.pnl-w{background:rgba(46,204,113,.18);flex:0 0 auto;display:flex;align-items:center;justify-content:center;font-size:10px;color:var(--green);font-weight:600}
.pnl-l{background:rgba(231,76,60,.18);flex:1;display:flex;align-items:center;justify-content:center;font-size:10px;color:var(--red);font-weight:600}
.tag{display:inline-block;font-size:10px;padding:2px 6px;border-radius:3px;margin:1px;border:1px solid}
.tag-long{background:rgba(46,204,113,.08);color:var(--green);border-color:rgba(46,204,113,.2)}
.tag-short{background:rgba(231,76,60,.08);color:var(--red);border-color:rgba(231,76,60,.2)}
.tag-pair{background:rgba(74,158,255,.08);color:var(--blue);border-color:rgba(74,158,255,.2)}
.tag-strat{background:rgba(240,165,0,.08);color:var(--amber);border-color:rgba(240,165,0,.2)}
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.7);z-index:200;align-items:center;justify-content:center}
.modal-bg.open{display:flex}
.modal{background:var(--bg2);border:1px solid var(--border2);border-radius:12px;padding:20px;width:420px;max-width:95vw;max-height:90vh;overflow-y:auto}
.modal h2{font-size:14px;font-weight:600;margin-bottom:14px;color:var(--gold)}
.note-card{background:var(--bg3);border:1px solid var(--border);border-radius:var(--radius);padding:12px;margin-bottom:8px;cursor:pointer;transition:border-color .15s}
.note-card:hover{border-color:var(--gold)}
.note-card h3{font-size:13px;font-weight:500;margin-bottom:4px}
.note-card p{font-size:11px;color:var(--muted);line-height:1.5}
.tab-row{display:flex;gap:2px;margin-bottom:14px;background:var(--bg2);padding:3px;border-radius:var(--radius);border:1px solid var(--border)}
.tab{flex:1;text-align:center;padding:5px 8px;font-size:11px;border-radius:5px;cursor:pointer;color:var(--muted);transition:all .15s}
.tab.active{background:var(--gold);color:#000;font-weight:600}
svg.spark{width:100%;height:60px;overflow:visible}
.progress-bar{height:6px;background:var(--border);border-radius:3px;overflow:hidden;margin-top:4px}
.progress-fill{height:100%;border-radius:3px;transition:width .4s}
.pf-gold{background:var(--gold)}.pf-green{background:var(--green)}.pf-red{background:var(--red)}
.chip{display:inline-flex;align-items:center;gap:4px;font-size:10px;padding:3px 7px;border-radius:3px;border:1px solid var(--border2);color:var(--muted)}
.save-toast{position:fixed;bottom:20px;right:20px;background:rgba(46,204,113,.15);border:1px solid rgba(46,204,113,.3);color:var(--green);padding:8px 14px;border-radius:6px;font-size:12px;z-index:300;opacity:0;transition:opacity .3s;pointer-events:none}
.save-toast.show{opacity:1}
@media(max-width:768px){
  .grid4{grid-template-columns:1fr 1fr}
  .grid3{grid-template-columns:1fr 1fr}
  .grid2{grid-template-columns:1fr}
}
</style>
</head>
<body>
<div id="app">
<nav>
  <div class="nav-logo">AQ</div>
  <button class="nav-btn active" onclick="showPage('dash')">
    <i class="ti ti-layout-dashboard"></i>
    <span class="nav-tip">Dashboard</span>
  </button>
  <button class="nav-btn" onclick="showPage('journal')">
    <i class="ti ti-chart-candle"></i>
    <span class="nav-tip">Trading Journal</span>
  </button>
  <button class="nav-btn" onclick="showPage('daily')">
    <i class="ti ti-calendar-event"></i>
    <span class="nav-tip">Daily Journal</span>
  </button>
  <button class="nav-btn" onclick="showPage('notes')">
    <i class="ti ti-notebook"></i>
    <span class="nav-tip">Notebook</span>
  </button>
  <button class="nav-btn" onclick="showPage('payout')">
    <i class="ti ti-cash"></i>
    <span class="nav-tip">Payout Tracker</span>
  </button>
  <div style="flex:1"></div>
  <button class="nav-btn" onclick="showPage('settings')">
    <i class="ti ti-settings"></i>
    <span class="nav-tip">Settings</span>
  </button>
</nav>

<main>

<!-- DASHBOARD -->
<div class="page active" id="page-dash">
  <div class="topbar">
    <div class="row" style="gap:10px">
      <h1>Dashboard</h1>
      <span class="badge bull" id="dxy-badge">DXY BULLISH</span>
    </div>
    <div class="row" style="gap:10px">
      <span style="font-size:11px;color:var(--muted)">EVC / Hormuud</span>
      <span class="clock" id="clock">--:--:--</span>
    </div>
  </div>
  <div class="content">
    <div class="grid4" style="margin-bottom:10px">
      <div class="card">
        <div class="card-title">Account Equity</div>
        <div class="metric-val gold" id="d-equity">$10,000</div>
        <div class="metric-sub">Base: $10,000</div>
      </div>
      <div class="card">
        <div class="card-title">Net P&L</div>
        <div class="metric-val" id="d-pnl">$0.00</div>
        <div class="metric-sub" id="d-pnlpct">0.00% of equity</div>
      </div>
      <div class="card">
        <div class="card-title">Win Rate</div>
        <div class="metric-val" id="d-wr">0%</div>
        <div class="metric-sub" id="d-trades">0 trades closed</div>
      </div>
      <div class="card">
        <div class="card-title">Profit Factor</div>
        <div class="metric-val" id="d-pf">—</div>
        <div class="metric-sub">Gross W / Gross L</div>
      </div>
    </div>

    <div class="grid2" style="margin-bottom:10px">
      <div class="card">
        <div class="card-title">DXY Bias — Anchor Rule</div>
        <div class="row sb" style="margin-bottom:6px">
          <span style="font-size:12px;font-weight:500" id="dxy-level">~103.40</span>
          <div class="row" style="gap:6px">
            <span class="badge bear" style="cursor:pointer" onclick="setDXY('bearish')">Bearish</span>
            <span class="badge neutral" style="cursor:pointer" onclick="setDXY('neutral')">Neutral</span>
            <span class="badge bull" style="cursor:pointer" onclick="setDXY('bullish')">Bullish</span>
          </div>
        </div>
        <div class="dxy-bar"><div class="dxy-fill" id="dxy-fill" style="width:60%"></div></div>
        <div class="row sb" style="margin-top:4px">
          <span style="font-size:9px;color:var(--dim)">95.65 Target</span>
          <span style="font-size:9px;color:var(--dim)">99.18 Apr High</span>
        </div>
      </div>
      <div class="card">
        <div class="card-title">Equity Curve</div>
        <svg class="spark" id="spark-svg" viewBox="0 0 240 60" preserveAspectRatio="none"></svg>
      </div>
    </div>

    <div class="grid2">
      <div class="card">
        <div class="card-title">Win / Loss Distribution</div>
        <div class="pnl-bar" id="pnl-bar">
          <div class="pnl-w" style="flex:1" id="bar-w">—</div>
          <div class="pnl-l" style="flex:0 0 0px" id="bar-l"></div>
        </div>
        <div class="row sb" style="margin-top:8px">
          <div><div style="font-size:10px;color:var(--muted)">Best Trade</div><div class="green" style="font-size:13px;font-weight:500" id="d-best">—</div></div>
          <div style="text-align:right"><div style="font-size:10px;color:var(--muted)">Worst Trade</div><div class="red" style="font-size:13px;font-weight:500" id="d-worst">—</div></div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">Recent Trades</div>
        <table>
          <thead><tr><th>PAIR</th><th>DIR</th><th>P&L</th><th>DATE</th></tr></thead>
          <tbody id="dash-recent"></tbody>
        </table>
      </div>
    </div>

    <div class="section-title">Pair Breakdown</div>
    <div id="pair-breakdown" class="grid4"></div>
  </div>
</div>

<!-- TRADING JOURNAL -->
<div class="page" id="page-journal">
  <div class="topbar">
    <h1>Trading Journal</h1>
    <button class="btn btn-gold btn-sm" onclick="openModal('modal-trade')"><i class="ti ti-plus"></i> New Trade</button>
  </div>
  <div class="content">
    <div class="tab-row">
      <div class="tab active" onclick="jTab(this,'jtab-open')">Open Positions</div>
      <div class="tab" onclick="jTab(this,'jtab-closed')">Closed Trades</div>
      <div class="tab" onclick="jTab(this,'jtab-stats')">Statistics</div>
    </div>
    <div id="jtab-open">
      <table>
        <thead><tr><th>PAIR</th><th>DIR</th><th>ENTRY</th><th>SL</th><th>TP</th><th>SIZE</th><th>RISK $</th><th>STRATEGY</th><th>DATE</th><th>ACTION</th></tr></thead>
        <tbody id="tbl-open"></tbody>
      </table>
      <div id="open-empty" style="text-align:center;padding:30px;color:var(--muted);font-size:12px">No open positions</div>
    </div>
    <div id="jtab-closed" style="display:none">
      <table>
        <thead><tr><th>PAIR</th><th>DIR</th><th>ENTRY</th><th>EXIT</th><th>P&L $</th><th>R:R</th><th>RESULT</th><th>DATE</th></tr></thead>
        <tbody id="tbl-closed"></tbody>
      </table>
      <div id="closed-empty" style="text-align:center;padding:30px;color:var(--muted);font-size:12px">No closed trades</div>
    </div>
    <div id="jtab-stats" style="display:none">
      <div class="grid4">
        <div class="card"><div class="card-title">Total Trades</div><div class="metric-val" id="st-total">0</div></div>
        <div class="card"><div class="card-title">Win Rate</div><div class="metric-val green" id="st-wr">0%</div></div>
        <div class="card"><div class="card-title">Profit Factor</div><div class="metric-val gold" id="st-pf">—</div></div>
        <div class="card"><div class="card-title">Avg RR</div><div class="metric-val blue" id="st-rr">—</div></div>
        <div class="card"><div class="card-title">Total Wins</div><div class="metric-val" id="st-tw">0</div></div>
        <div class="card"><div class="card-title">Total Losses</div><div class="metric-val" id="st-tl">0</div></div>
        <div class="card"><div class="card-title">Gross Profit</div><div class="metric-val green" id="st-gp">$0</div></div>
        <div class="card"><div class="card-title">Gross Loss</div><div class="metric-val red" id="st-gl">$0</div></div>
        <div class="card"><div class="card-title">Best Trade</div><div class="metric-val green" id="st-best">—</div></div>
        <div class="card"><div class="card-title">Worst Trade</div><div class="metric-val red" id="st-worst">—</div></div>
        <div class="card"><div class="card-title">Avg Win</div><div class="metric-val" id="st-aw">—</div></div>
        <div class="card"><div class="card-title">Avg Loss</div><div class="metric-val" id="st-al">—</div></div>
      </div>
    </div>
  </div>
</div>

<!-- DAILY JOURNAL -->
<div class="page" id="page-daily">
  <div class="topbar">
    <h1>Daily Journal</h1>
    <button class="btn btn-gold btn-sm" onclick="openModal('modal-daily')"><i class="ti ti-plus"></i> New Entry</button>
  </div>
  <div class="content">
    <div id="daily-list"></div>
    <div id="daily-empty" style="text-align:center;padding:40px;color:var(--muted);font-size:12px">No journal entries yet. Start your first pre/post-session log.</div>
  </div>
</div>

<!-- NOTEBOOK -->
<div class="page" id="page-notes">
  <div class="topbar">
    <h1>Notebook</h1>
    <button class="btn btn-gold btn-sm" onclick="openModal('modal-note')"><i class="ti ti-plus"></i> New Note</button>
  </div>
  <div class="content">
    <div class="grid3" id="notes-grid"></div>
    <div id="notes-empty" style="text-align:center;padding:40px;color:var(--muted);font-size:12px">No notes yet. Capture your SMC observations, setups, and rules.</div>
  </div>
</div>

<!-- PAYOUT TRACKER -->
<div class="page" id="page-payout">
  <div class="topbar">
    <h1>Payout Tracker</h1>
    <button class="btn btn-gold btn-sm" onclick="openModal('modal-payout')"><i class="ti ti-plus"></i> Log Payout</button>
  </div>
  <div class="content">
    <div class="grid4" style="margin-bottom:14px">
      <div class="card"><div class="card-title">Total Withdrawn</div><div class="metric-val gold" id="pay-total">$0.00</div></div>
      <div class="card"><div class="card-title">This Month</div><div class="metric-val" id="pay-month">$0.00</div></div>
      <div class="card"><div class="card-title">Payouts Count</div><div class="metric-val" id="pay-count">0</div></div>
      <div class="card"><div class="card-title">Net After Payouts</div><div class="metric-val blue" id="pay-net">$10,000</div></div>
    </div>
    <div class="section-title">Payout Goal</div>
    <div class="card" style="margin-bottom:14px">
      <div class="row sb" style="margin-bottom:6px">
        <span style="font-size:12px" id="pay-goal-label">Monthly goal: $500</span>
        <input type="number" id="goal-input" style="width:100px" value="500" onchange="updatePayoutGoal()">
      </div>
      <div class="progress-bar"><div class="progress-fill pf-gold" id="goal-bar" style="width:0%"></div></div>
      <div style="font-size:10px;color:var(--muted);margin-top:4px" id="goal-pct">0% of goal</div>
    </div>
    <div class="section-title">Payout History</div>
    <table>
      <thead><tr><th>DATE</th><th>AMOUNT</th><th>METHOD</th><th>NOTE</th><th>SOURCE</th></tr></thead>
      <tbody id="tbl-payouts"></tbody>
    </table>
    <div id="pay-empty" style="text-align:center;padding:30px;color:var(--muted);font-size:12px">No payouts logged yet.</div>
  </div>
</div>

<!-- SETTINGS -->
<div class="page" id="page-settings">
  <div class="topbar"><h1>Settings</h1></div>
  <div class="content">
    <div class="card" style="max-width:400px;margin-bottom:14px">
      <div class="card-title">Account Settings</div>
      <div class="field"><label>Trader Name</label><input type="text" id="s-name" value="Abdi Qani" onchange="saveSetting('name',this.value)"></div>
      <div class="field"><label>Base Equity ($)</label><input type="number" id="s-equity" value="10000" onchange="saveSetting('base',parseFloat(this.value))"></div>
      <div class="field"><label>Max Daily Risk (%)</label><input type="number" id="s-risk" value="2" step="0.1" onchange="saveSetting('risk',this.value)"></div>
      <div class="field"><label>Currency</label>
        <select id="s-curr" onchange="saveSetting('curr',this.value)">
          <option value="USD">USD</option><option value="EUR">EUR</option><option value="GBP">GBP</option>
        </select>
      </div>
    </div>
    <div class="card" style="max-width:400px">
      <div class="card-title">Data Management</div>
      <div style="font-size:12px;color:var(--muted);margin-bottom:10px">Data-kaagu browser-kaaga ayuu ku kaydsan yahay (localStorage). Export-garee si aad backup u samaysato.</div>
      <div class="row" style="gap:8px">
        <button class="btn btn-sm" onclick="exportData()"><i class="ti ti-download"></i> Export JSON</button>
        <button class="btn btn-sm" onclick="document.getElementById('import-file').click()"><i class="ti ti-upload"></i> Import JSON</button>
        <input type="file" id="import-file" accept=".json" style="display:none" onchange="importData(event)">
        <button class="btn btn-sm" style="color:var(--red);border-color:rgba(231,76,60,.3)" onclick="clearAllData()"><i class="ti ti-trash"></i> Clear All</button>
      </div>
    </div>
  </div>
</div>

</main>
</div>

<!-- MODALS -->
<div class="modal-bg" id="modal-trade">
<div class="modal">
  <div class="row sb" style="margin-bottom:14px">
    <h2><i class="ti ti-chart-candle" style="margin-right:6px"></i>New Trade</h2>
    <button class="btn btn-sm" onclick="closeModal('modal-trade')"><i class="ti ti-x"></i></button>
  </div>
  <div class="grid2">
    <div class="field"><label>Pair</label>
      <select id="t-pair"><option>EURUSD</option><option>USDCAD</option><option>USDCHF</option><option>USDJPY</option><option>GBPUSD</option><option>AUDUSD</option><option>XAUUSD</option></select>
    </div>
    <div class="field"><label>Direction</label>
      <select id="t-dir"><option value="LONG">LONG</option><option value="SHORT">SHORT</option></select>
    </div>
  </div>
  <div class="grid3">
    <div class="field"><label>Entry Price</label><input type="number" id="t-entry" step="0.00001" placeholder="1.08500"></div>
    <div class="field"><label>Stop Loss</label><input type="number" id="t-sl" step="0.00001" placeholder="1.08200"></div>
    <div class="field"><label>Take Profit</label><input type="number" id="t-tp" step="0.00001" placeholder="1.09100"></div>
  </div>
  <div class="grid2">
    <div class="field"><label>Position Size (lots)</label><input type="number" id="t-size" step="0.01" placeholder="0.10"></div>
    <div class="field"><label>Risk ($)</label><input type="number" id="t-risk" placeholder="100"></div>
  </div>
  <div class="field"><label>Strategy / Setup</label>
    <select id="t-strat">
      <option>Scenario 1</option><option>Scenario 2</option><option>Scenario 3</option><option>Scenario 4</option>
    </select>
  </div>
  <div class="field"><label>DXY Bias at Entry</label>
    <select id="t-dxy"><option>Bullish</option><option>Bearish</option><option>Neutral</option></select>
  </div>
  <div class="field"><label>Notes</label><textarea id="t-notes" placeholder="SMC reasoning, confluences..."></textarea></div>
  <div class="row" style="justify-content:flex-end;gap:8px;margin-top:4px">
    <button class="btn btn-sm" onclick="closeModal('modal-trade')">Cancel</button>
    <button class="btn btn-gold btn-sm" onclick="addTrade()">Open Trade</button>
  </div>
</div>
</div>

<div class="modal-bg" id="modal-close">
<div class="modal">
  <div class="row sb" style="margin-bottom:14px">
    <h2><i class="ti ti-lock" style="margin-right:6px"></i>Close Trade</h2>
    <button class="btn btn-sm" onclick="closeModal('modal-close')"><i class="ti ti-x"></i></button>
  </div>
  <div class="field"><label>Exit Price</label><input type="number" id="c-exit" step="0.00001"></div>
  <div class="field"><label>Exit Notes</label><textarea id="c-notes" placeholder="What happened? Execution quality..."></textarea></div>
  <div class="row" style="justify-content:flex-end;gap:8px;margin-top:4px">
    <button class="btn btn-sm" onclick="closeModal('modal-close')">Cancel</button>
    <button class="btn btn-gold btn-sm" onclick="confirmClose()">Close Trade</button>
  </div>
</div>
</div>

<div class="modal-bg" id="modal-daily">
<div class="modal">
  <div class="row sb" style="margin-bottom:14px">
    <h2><i class="ti ti-calendar-event" style="margin-right:6px"></i>Daily Journal Entry</h2>
    <button class="btn btn-sm" onclick="closeModal('modal-daily')"><i class="ti ti-x"></i></button>
  </div>
  <div class="grid2">
    <div class="field"><label>Session</label>
      <select id="dj-session"><option>London</option><option>New York</option><option>Asian</option><option>Pre-Session</option><option>Post-Session</option></select>
    </div>
    <div class="field"><label>DXY Bias Today</label>
      <select id="dj-dxy"><option>Bullish</option><option>Bearish</option><option>Neutral</option></select>
    </div>
  </div>
  <div class="field"><label>Market Narrative</label><textarea id="dj-narrative" placeholder="What is DXY doing? HTF structure? Key levels..."></textarea></div>
  <div class="field"><label>Pairs in Focus</label><input type="text" id="dj-pairs" placeholder="EURUSD, XAUUSD..."></div>
  <div class="field"><label>Trades Taken</label><input type="number" id="dj-trades" placeholder="0"></div>
  <div class="field"><label>Emotional State</label>
    <select id="dj-mood"><option>Disciplined 🟢</option><option>Neutral 🟡</option><option>Emotional 🔴</option><option>Overtraded 🔴</option></select>
  </div>
  <div class="field"><label>Key Lesson / Reflection</label><textarea id="dj-lesson" placeholder="What did you learn today?"></textarea></div>
  <div class="row" style="justify-content:flex-end;gap:8px;margin-top:4px">
    <button class="btn btn-sm" onclick="closeModal('modal-daily')">Cancel</button>
    <button class="btn btn-gold btn-sm" onclick="addDailyEntry()">Save Entry</button>
  </div>
</div>
</div>

<div class="modal-bg" id="modal-note">
<div class="modal">
  <div class="row sb" style="margin-bottom:14px">
    <h2><i class="ti ti-notebook" style="margin-right:6px"></i>New Note</h2>
    <button class="btn btn-sm" onclick="closeModal('modal-note')"><i class="ti ti-x"></i></button>
  </div>
  <div class="field"><label>Title</label><input type="text" id="n-title" placeholder="SMC Observation, Rule, Setup..."></div>
  <div class="field"><label>Category</label>
    <select id="n-cat"><option>SMC Concept</option><option>Trade Rule</option><option>Market Observation</option><option>DXY Analysis</option><option>Psychology</option><option>Setup Playbook</option></select>
  </div>
  <div class="field"><label>Content</label><textarea id="n-body" style="min-height:120px" placeholder="Your notes..."></textarea></div>
  <div class="row" style="justify-content:flex-end;gap:8px;margin-top:4px">
    <button class="btn btn-sm" onclick="closeModal('modal-note')">Cancel</button>
    <button class="btn btn-gold btn-sm" onclick="addNote()">Save Note</button>
  </div>
</div>
</div>

<div class="modal-bg" id="modal-payout">
<div class="modal">
  <div class="row sb" style="margin-bottom:14px">
    <h2><i class="ti ti-cash" style="margin-right:6px"></i>Log Payout</h2>
    <button class="btn btn-sm" onclick="closeModal('modal-payout')"><i class="ti ti-x"></i></button>
  </div>
  <div class="field"><label>Amount ($)</label><input type="number" id="p-amount" placeholder="500"></div>
  <div class="field"><label>Payment Method</label>
    <select id="p-method"><option>EVC Plus / Hormuud</option><option>Zaad / Telesom</option><option>E-Dahab / Golis</option><option>Bank Transfer</option><option>Crypto</option><option>Other</option></select>
  </div>
  <div class="field"><label>Source</label>
    <select id="p-source"><option>Trading Profit</option><option>Salary / Prop Firm</option><option>Other</option></select>
  </div>
  <div class="field"><label>Note</label><input type="text" id="p-note" placeholder="Optional note..."></div>
  <div class="row" style="justify-content:flex-end;gap:8px;margin-top:4px">
    <button class="btn btn-sm" onclick="closeModal('modal-payout')">Cancel</button>
    <button class="btn btn-gold btn-sm" onclick="addPayout()">Log Payout</button>
  </div>
</div>
</div>

<div class="save-toast" id="save-toast">✓ Saved</div>

<script>
const STORAGE_KEY = 'pro_trader_os_v2';

const defaultState = {
  trades: [],
  dailyEntries: [],
  notes: [],
  payouts: [],
  settings: { name:'Abdi Qani', base:10000, risk:2, curr:'USD' },
  dxy: 'bullish',
  closingTradeId: null
};

function loadState() {
  try {
    const saved = localStorage.getItem(STORAGE_KEY);
    if (saved) {
      const parsed = JSON.parse(saved);
      return {...defaultState, ...parsed, settings: {...defaultState.settings, ...parsed.settings}};
    }
  } catch(e) { console.warn('Load failed', e); }
  return {...defaultState};
}

function saveState() {
  try {
    const toSave = {
      trades: state.trades,
      dailyEntries: state.dailyEntries,
      notes: state.notes,
      payouts: state.payouts,
      settings: state.settings,
      dxy: state.dxy
    };
    localStorage.setItem(STORAGE_KEY, JSON.stringify(toSave));
    showToast();
  } catch(e) { console.warn('Save failed', e); }
}

function showToast() {
  const t = document.getElementById('save-toast');
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 1500);
}

function exportData() {
  const data = JSON.stringify({
    trades: state.trades,
    dailyEntries: state.dailyEntries,
    notes: state.notes,
    payouts: state.payouts,
    settings: state.settings,
    dxy: state.dxy,
    exportDate: new Date().toISOString()
  }, null, 2);
  const blob = new Blob([data], {type:'application/json'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'trader_os_backup_' + new Date().toISOString().slice(0,10) + '.json';
  a.click();
  URL.revokeObjectURL(url);
}

function importData(event) {
  const file = event.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = (e) => {
    try {
      const parsed = JSON.parse(e.target.result);
      if (confirm('Import-gareeya? Data-da hadda jirta waa la bedeli doonaa.')) {
        state.trades = parsed.trades || [];
        state.dailyEntries = parsed.dailyEntries || [];
        state.notes = parsed.notes || [];
        state.payouts = parsed.payouts || [];
        state.settings = {...defaultState.settings, ...parsed.settings};
        state.dxy = parsed.dxy || 'bullish';
        saveState();
        location.reload();
      }
    } catch(err) { alert('File-ka kuma jiro data sax ah.'); }
  };
  reader.readAsText(file);
  event.target.value = '';
}

function clearAllData() {
  if (confirm('Data oo dhan sheegid? Tani ma dib loo celin karo.')) {
    localStorage.removeItem(STORAGE_KEY);
    location.reload();
  }
}

let state = loadState();

// Apply loaded settings to UI
function applySettings() {
  const sn = document.getElementById('s-name');
  const se = document.getElementById('s-equity');
  const sr = document.getElementById('s-risk');
  if (sn) sn.value = state.settings.name;
  if (se) se.value = state.settings.base;
  if (sr) sr.value = state.settings.risk;
  setDXY(state.dxy, false);
}

function saveSetting(k,v) { state.settings[k]=v; saveState(); updateDash(); }

function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  const idx=['dash','journal','daily','notes','payout','settings'].indexOf(id);
  document.querySelectorAll('.nav-btn')[idx+1]?.classList.add('active');
  if(id==='dash')updateDash();
  if(id==='journal')renderJournal();
  if(id==='daily')renderDaily();
  if(id==='notes')renderNotes();
  if(id==='payout')renderPayout();
}

function openModal(id){document.getElementById(id).classList.add('open')}
function closeModal(id){document.getElementById(id).classList.remove('open')}

function setDXY(bias, save=true){
  state.dxy=bias;
  const fill={bullish:'65%',neutral:'45%',bearish:'25%'};
  document.getElementById('dxy-fill').style.width=fill[bias];
  document.getElementById('dxy-badge').textContent='DXY '+bias.toUpperCase();
  document.getElementById('dxy-badge').className='badge '+(bias==='bullish'?'bull':bias==='bearish'?'bear':'neutral');
  if(save) saveState();
}

function fmt(n){return (n>=0?'+':'')+n.toFixed(2)}
function fmtD(d){return new Date(d).toLocaleDateString('en-GB',{day:'2-digit',month:'short',year:'2-digit'})}

function addTrade(){
  const t={
    id:Date.now(),
    pair:document.getElementById('t-pair').value,
    dir:document.getElementById('t-dir').value,
    entry:parseFloat(document.getElementById('t-entry').value)||0,
    sl:parseFloat(document.getElementById('t-sl').value)||0,
    tp:parseFloat(document.getElementById('t-tp').value)||0,
    size:parseFloat(document.getElementById('t-size').value)||0,
    risk:parseFloat(document.getElementById('t-risk').value)||0,
    strategy:document.getElementById('t-strat').value,
    dxy:document.getElementById('t-dxy').value,
    notes:document.getElementById('t-notes').value,
    status:'open',date:Date.now()
  };
  state.trades.push(t);
  saveState();
  closeModal('modal-trade');
  renderJournal();updateDash();
}

function closeTrade(id){state.closingTradeId=id;openModal('modal-close')}

function confirmClose(){
  const exit=parseFloat(document.getElementById('c-exit').value)||0;
  const notes=document.getElementById('c-notes').value;
  const t=state.trades.find(x=>x.id===state.closingTradeId);
  if(!t)return;
  const pips=(t.dir==='LONG')?(exit-t.entry):(t.entry-exit);
  const pipValues={'EURUSD':10,'GBPUSD':10,'AUDUSD':10,'NZDUSD':10,'XAUUSD':1,'USDCAD':7.5,'USDCHF':10,'USDJPY':9};
  const pipVal=pipValues[t.pair]||10;
  const pipSize=(t.pair&&t.pair.includes('JPY'))?0.01:0.0001;
  const pnl=(pips/pipSize)*pipVal*t.size;
  t.exit=exit;t.exitNotes=notes;t.pnl=pnl;t.status='closed';t.closeDate=Date.now();
  const slRange=Math.abs(t.entry-t.sl);
  t.rr=slRange>0?(Math.abs(pips)/slRange).toFixed(2):'—';
  saveState();
  closeModal('modal-close');renderJournal();updateDash();
}

function renderJournal(){
  const open=state.trades.filter(t=>t.status==='open');
  const closed=state.trades.filter(t=>t.status==='closed');
  const ob=document.getElementById('tbl-open');
  const oe=document.getElementById('open-empty');
  ob.innerHTML='';oe.style.display=open.length?'none':'block';
  open.forEach(t=>{ob.innerHTML+=`<tr>
    <td><span class="tag tag-pair">${t.pair}</span></td>
    <td><span class="tag ${t.dir==='LONG'?'tag-long':'tag-short'}">${t.dir}</span></td>
    <td style="font-family:var(--mono);font-size:11px">${t.entry}</td>
    <td style="font-family:var(--mono);font-size:11px;color:var(--red)">${t.sl}</td>
    <td style="font-family:var(--mono);font-size:11px;color:var(--green)">${t.tp}</td>
    <td>${t.size}</td>
    <td class="red">$${t.risk}</td>
    <td><span class="tag tag-strat" style="font-size:9px">${t.strategy.split(' ')[0]}</span></td>
    <td style="color:var(--muted)">${fmtD(t.date)}</td>
    <td><button class="btn btn-sm" style="color:var(--amber);border-color:rgba(240,165,0,.3)" onclick="closeTrade(${t.id})">Close</button></td>
  </tr>`;});
  const cb=document.getElementById('tbl-closed');
  const ce=document.getElementById('closed-empty');
  cb.innerHTML='';ce.style.display=closed.length?'none':'block';
  closed.forEach(t=>{const pos=t.pnl>=0;cb.innerHTML+=`<tr>
    <td><span class="tag tag-pair">${t.pair}</span></td>
    <td><span class="tag ${t.dir==='LONG'?'tag-long':'tag-short'}">${t.dir}</span></td>
    <td style="font-family:var(--mono);font-size:11px">${t.entry}</td>
    <td style="font-family:var(--mono);font-size:11px">${t.exit}</td>
    <td class="${pos?'green':'red'}" style="font-weight:600;font-family:var(--mono)">${fmt(t.pnl)}</td>
    <td class="gold">${t.rr}R</td>
    <td><span class="badge ${pos?'bull':'bear'}">${pos?'WIN':'LOSS'}</span></td>
    <td style="color:var(--muted)">${fmtD(t.closeDate)}</td>
  </tr>`;});
  updateStats();
}

function jTab(el,id){
  document.querySelectorAll('.tab-row .tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  ['jtab-open','jtab-closed','jtab-stats'].forEach(i=>document.getElementById(i).style.display='none');
  document.getElementById(id).style.display='block';
  if(id==='jtab-stats')updateStats();
}

function updateStats(){
  const closed=state.trades.filter(t=>t.status==='closed');
  const wins=closed.filter(t=>t.pnl>=0);
  const losses=closed.filter(t=>t.pnl<0);
  const gp=wins.reduce((a,t)=>a+t.pnl,0);
  const gl=Math.abs(losses.reduce((a,t)=>a+t.pnl,0));
  const pf=gl>0?(gp/gl).toFixed(2):'—';
  const wr=closed.length>0?((wins.length/closed.length)*100).toFixed(0)+'%':'0%';
  const rrs=closed.filter(t=>!isNaN(t.rr)).map(t=>parseFloat(t.rr));
  const avgRR=rrs.length>0?(rrs.reduce((a,b)=>a+b,0)/rrs.length).toFixed(2)+'R':'—';
  const pnls=closed.map(t=>t.pnl);
  [['st-total',closed.length],['st-wr',wr],['st-pf',pf],['st-rr',avgRR],
   ['st-tw',wins.length],['st-tl',losses.length],
   ['st-gp','$'+gp.toFixed(2)],['st-gl','$'+gl.toFixed(2)],
   ['st-best',pnls.length?'$'+Math.max(...pnls).toFixed(2):'—'],
   ['st-worst',pnls.length?'$'+Math.min(...pnls).toFixed(2):'—'],
   ['st-aw',wins.length?'$'+(gp/wins.length).toFixed(2):'—'],
   ['st-al',losses.length?'$'+(gl/losses.length).toFixed(2):'—']
  ].forEach(([id,v])=>{const el=document.getElementById(id);if(el)el.textContent=v;});
}

function updateDash(){
  const closed=state.trades.filter(t=>t.status==='closed');
  const wins=closed.filter(t=>t.pnl>=0);
  const losses=closed.filter(t=>t.pnl<0);
  const netPnl=closed.reduce((a,t)=>a+t.pnl,0);
  const equity=state.settings.base+netPnl;
  const gp=wins.reduce((a,t)=>a+t.pnl,0);
  const gl=Math.abs(losses.reduce((a,t)=>a+t.pnl,0));
  const pf=gl>0?(gp/gl).toFixed(2):'—';
  const wr=closed.length>0?((wins.length/closed.length)*100).toFixed(0)+'%':'0%';
  const pnls=closed.map(t=>t.pnl);
  document.getElementById('d-equity').textContent='$'+equity.toFixed(0);
  document.getElementById('d-equity').className='metric-val '+(netPnl>=0?'gold':'red');
  document.getElementById('d-pnl').textContent=(netPnl>=0?'+':'')+' $'+Math.abs(netPnl).toFixed(2);
  document.getElementById('d-pnl').className='metric-val '+(netPnl>=0?'green':'red');
  document.getElementById('d-pnlpct').textContent=((netPnl/state.settings.base)*100).toFixed(2)+'% of equity';
  document.getElementById('d-wr').textContent=wr;
  document.getElementById('d-wr').className='metric-val '+(wins.length>losses.length?'green':'red');
  document.getElementById('d-trades').textContent=closed.length+' trades closed';
  document.getElementById('d-pf').textContent=pf;
  document.getElementById('d-pf').className='metric-val '+(parseFloat(pf)>1?'gold':'red');
  document.getElementById('d-best').textContent=pnls.length?'$'+Math.max(...pnls).toFixed(2):'—';
  document.getElementById('d-worst').textContent=pnls.length?'$'+Math.min(...pnls).toFixed(2):'—';
  const wr_num=closed.length>0?wins.length/closed.length:0.5;
  const bw=document.getElementById('bar-w');const bl=document.getElementById('bar-l');
  bw.style.flex=wr_num;bw.textContent=wins.length+'W';
  bl.style.flex=1-wr_num;bl.textContent=losses.length>0?losses.length+'L':'';
  const recent=closed.slice(-5).reverse();
  const dr=document.getElementById('dash-recent');
  dr.innerHTML=recent.map(t=>`<tr>
    <td><span class="tag tag-pair">${t.pair}</span></td>
    <td><span class="tag ${t.dir==='LONG'?'tag-long':'tag-short'}">${t.dir}</span></td>
    <td class="${t.pnl>=0?'green':'red'}" style="font-weight:600">${fmt(t.pnl)}</td>
    <td style="color:var(--muted);font-size:10px">${fmtD(t.closeDate)}</td>
  </tr>`).join('')||'<tr><td colspan="4" style="text-align:center;color:var(--muted);padding:12px">No trades yet</td></tr>';
  const pairs=['EURUSD','USDCAD','USDCHF','USDJPY','GBPUSD','AUDUSD','XAUUSD'];
  document.getElementById('pair-breakdown').innerHTML=pairs.map(p=>{
    const pt=closed.filter(t=>t.pair===p);
    const ppnl=pt.reduce((a,t)=>a+t.pnl,0);
    const pw=pt.filter(t=>t.pnl>=0).length;
    return `<div class="card"><div class="card-title">${p}</div>
      <div class="${ppnl>=0?'green':'red'}" style="font-size:14px;font-weight:600">${pt.length?fmt(ppnl):'—'}</div>
      <div style="font-size:10px;color:var(--muted)">${pt.length} trades${pt.length?' · '+pw+'W':''}</div></div>`;
  }).join('');
  drawSparkline(equity);
  updatePayoutDash();
}

function updatePayoutDash(){
  const total=state.payouts.reduce((a,p)=>a+p.amount,0);
  const el=document.getElementById('pay-total');
  if(el)el.textContent='$'+total.toFixed(2);
}

function drawSparkline(currentEquity){
  const svg=document.getElementById('spark-svg');
  const closed=state.trades.filter(t=>t.status==='closed');
  const base=state.settings.base;
  let points=[base],running=base;
  closed.forEach(t=>{running+=t.pnl;points.push(running)});
  if(points.length<2)points=[base,base];
  const min=Math.min(...points),max=Math.max(...points),range=max-min||100;
  const W=240,H=60;
  const coords=points.map((v,i)=>`${(i/(points.length-1))*W},${H-((v-min)/range)*(H-4)-2}`);
  const color=currentEquity>=base?'#2ecc71':'#e74c3c';
  svg.innerHTML=`<polyline points="${coords.join(' ')}" fill="none" stroke="${color}" stroke-width="1.5" stroke-linejoin="round"/>
    <circle cx="${W}" cy="${H-((points[points.length-1]-min)/range)*(H-4)-2}" r="3" fill="${color}"/>`;
}

function addDailyEntry(){
  const e={
    id:Date.now(),
    session:document.getElementById('dj-session').value,
    dxy:document.getElementById('dj-dxy').value,
    narrative:document.getElementById('dj-narrative').value,
    pairs:document.getElementById('dj-pairs').value,
    trades:document.getElementById('dj-trades').value,
    mood:document.getElementById('dj-mood').value,
    lesson:document.getElementById('dj-lesson').value,
    date:Date.now()
  };
  state.dailyEntries.unshift(e);
  saveState();
  closeModal('modal-daily');renderDaily();
}

function renderDaily(){
  const list=document.getElementById('daily-list');
  const empty=document.getElementById('daily-empty');
  empty.style.display=state.dailyEntries.length?'none':'block';
  list.innerHTML=state.dailyEntries.map(e=>`
    <div class="card" style="margin-bottom:10px">
      <div class="row sb" style="margin-bottom:8px">
        <div class="row" style="gap:8px">
          <span style="font-size:13px;font-weight:500">${fmtD(e.date)}</span>
          <span class="chip"><i class="ti ti-chart-line" style="font-size:12px"></i>${e.session}</span>
          <span class="badge ${e.dxy==='Bullish'?'bull':e.dxy==='Bearish'?'bear':'neutral'}">DXY ${e.dxy.toUpperCase()}</span>
        </div>
        <span style="font-size:11px;color:var(--muted)">${e.mood}</span>
      </div>
      ${e.narrative?`<p style="font-size:12px;color:var(--text);margin-bottom:6px;line-height:1.6">${e.narrative}</p>`:''}
      ${e.pairs?`<div style="margin-bottom:4px">${e.pairs.split(',').map(p=>`<span class="tag tag-pair">${p.trim()}</span>`).join('')}</div>`:''}
      ${e.lesson?`<div style="border-top:1px solid var(--border);margin-top:8px;padding-top:8px;font-size:11px;color:var(--muted)"><i class="ti ti-bulb" style="color:var(--gold);margin-right:4px"></i>${e.lesson}</div>`:''}
    </div>`).join('');
}

function addNote(){
  const n={id:Date.now(),title:document.getElementById('n-title').value,cat:document.getElementById('n-cat').value,body:document.getElementById('n-body').value,date:Date.now()};
  state.notes.unshift(n);saveState();closeModal('modal-note');renderNotes();
}

function deleteNote(id){state.notes=state.notes.filter(n=>n.id!==id);saveState();renderNotes();}

function renderNotes(){
  const grid=document.getElementById('notes-grid');
  const empty=document.getElementById('notes-empty');
  empty.style.display=state.notes.length?'none':'block';
  const catColors={'SMC Concept':'tag-pair','Trade Rule':'tag-strat','Market Observation':'tag-long','DXY Analysis':'tag-long','Psychology':'tag-short','Setup Playbook':'tag-strat'};
  grid.innerHTML=state.notes.map(n=>`
    <div class="note-card">
      <div class="row sb" style="margin-bottom:6px">
        <span class="tag ${catColors[n.cat]||'tag-pair'}">${n.cat}</span>
        <button class="btn btn-sm" style="padding:2px 6px;font-size:10px;color:var(--red)" onclick="deleteNote(${n.id})"><i class="ti ti-trash"></i></button>
      </div>
      <h3>${n.title}</h3>
      <p style="margin-top:4px">${n.body}</p>
      <div style="font-size:10px;color:var(--dim);margin-top:8px">${fmtD(n.date)}</div>
    </div>`).join('');
}

function addPayout(){
  const p={id:Date.now(),amount:parseFloat(document.getElementById('p-amount').value)||0,method:document.getElementById('p-method').value,source:document.getElementById('p-source').value,note:document.getElementById('p-note').value,date:Date.now(),month:new Date().getMonth()};
  state.payouts.unshift(p);saveState();closeModal('modal-payout');renderPayout();updateDash();
}

function updatePayoutGoal(){renderPayout();}

function renderPayout(){
  const total=state.payouts.reduce((a,p)=>a+p.amount,0);
  const thisMonth=state.payouts.filter(p=>new Date(p.date).getMonth()===new Date().getMonth()).reduce((a,p)=>a+p.amount,0);
  const closed=state.trades.filter(t=>t.status==='closed');
  const netPnl=closed.reduce((a,t)=>a+t.pnl,0);
  const netAfter=(state.settings.base+netPnl)-total;
  const goal=parseFloat(document.getElementById('goal-input')?.value)||500;
  document.getElementById('pay-total').textContent='$'+total.toFixed(2);
  document.getElementById('pay-month').textContent='$'+thisMonth.toFixed(2);
  document.getElementById('pay-count').textContent=state.payouts.length;
  document.getElementById('pay-net').textContent='$'+netAfter.toFixed(2);
  document.getElementById('pay-net').className='metric-val '+(netAfter>=state.settings.base?'blue':'red');
  const pct=Math.min((thisMonth/goal)*100,100);
  const gb=document.getElementById('goal-bar');const gp=document.getElementById('goal-pct');
  if(gb)gb.style.width=pct.toFixed(0)+'%';
  if(gp)gp.textContent=pct.toFixed(0)+'% of $'+goal+' monthly goal';
  document.getElementById('pay-goal-label').textContent='Monthly goal: $'+goal;
  const tbl=document.getElementById('tbl-payouts');
  const pe=document.getElementById('pay-empty');
  pe.style.display=state.payouts.length?'none':'block';
  tbl.innerHTML=state.payouts.map(p=>`<tr>
    <td style="color:var(--muted)">${fmtD(p.date)}</td>
    <td class="gold" style="font-weight:600;font-family:var(--mono)">$${p.amount.toFixed(2)}</td>
    <td style="font-size:11px">${p.method}</td>
    <td style="font-size:11px;color:var(--muted)">${p.note||'—'}</td>
    <td><span class="badge neutral">${p.source}</span></td>
  </tr>`).join('');
}

function updateClock(){
  const now=new Date();
  const mog=new Date(now.toLocaleString('en-US',{timeZone:'Africa/Mogadishu'}));
  const h=String(mog.getHours()).padStart(2,'0');
  const m=String(mog.getMinutes()).padStart(2,'0');
  const s=String(mog.getSeconds()).padStart(2,'0');
  const el=document.getElementById('clock');
  if(el)el.textContent=`MGA ${h}:${m}:${s}`;
}

setInterval(updateClock,1000);
updateClock();
applySettings();
updateDash();
drawSparkline(state.settings.base);
</script>
</body>
</html>
