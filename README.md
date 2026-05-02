# Experiential-Learning-API-Bootstrap-framework
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ServerPanel — Live Admin Dashboard</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.3/css/bootstrap.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-icons/1.11.3/font/bootstrap-icons.min.css">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
@keyframes bgShift {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
@keyframes fadeUp {
  from { opacity:0; transform:translateY(14px); }
  to   { opacity:1; transform:translateY(0); }
}
@keyframes slideLeft {
  from { opacity:0; transform:translateX(-20px); }
  to   { opacity:1; transform:translateX(0); }
}
@keyframes blink {
  0%,100% { opacity:1; }
  50%      { opacity:0.2; }
}
@keyframes pulse-ring {
  0%   { transform:scale(1);   opacity:.6; }
  100% { transform:scale(1.8); opacity:0; }
}
@keyframes countUp {
  from { opacity:0; transform:translateY(6px); }
  to   { opacity:1; transform:translateY(0); }
}
*  { box-sizing:border-box; }
body {
  font-family:'Inter',sans-serif;
  background: linear-gradient(135deg,#0f172a,#0d1f3c,#0f2744,#0a1f38,#111827,#1a1035,#0f172a);
  background-size:400% 400%;
  animation: bgShift 18s ease infinite;
  color:#cbd5e1;
  min-height:100vh;
}
/* ── NAVBAR ── */
.topnav {
  background:rgba(10,16,32,0.92)!important;
  backdrop-filter:blur(16px);
  border-bottom:1px solid rgba(255,255,255,0.07);
  height:56px;
}
.navbar-brand { font-size:18px; font-weight:700; color:#f1f5f9!important; letter-spacing:-.3px; }
.navbar-brand span { color:#38bdf8; }
.nav-link { color:#64748b!important; font-size:13px; font-weight:500; border-radius:7px; padding:5px 12px!important; transition:.2s; }
.nav-link:hover { background:rgba(255,255,255,0.07); color:#e2e8f0!important; }
.nav-link.active { background:rgba(56,189,248,0.13); color:#38bdf8!important; }
.navbar-toggler { border-color:rgba(255,255,255,0.15); }
/* ── SIDEBAR ── */
.sidebar {
  width:215px; flex-shrink:0;
  background:rgba(10,16,32,0.88);
  backdrop-filter:blur(14px);
  border-right:1px solid rgba(255,255,255,0.06);
  position:sticky; top:56px;
  height:calc(100vh - 56px);
  overflow-y:auto;
  animation:slideLeft .4s ease .1s both;
}
.sidebar::-webkit-scrollbar { width:3px; }
.sidebar::-webkit-scrollbar-thumb { background:rgba(255,255,255,0.08); border-radius:2px; }
.sb-label { font-size:9px; font-weight:700; text-transform:uppercase; letter-spacing:.1em; color:#334155; padding:14px 16px 4px; }
.sb-link {
  display:flex; align-items:center; gap:10px;
  padding:8px 12px; margin:1px 8px; border-radius:8px;
  color:#64748b; font-size:13px; font-weight:500;
  text-decoration:none; cursor:pointer;
  transition:background .15s, color .15s;
  position:relative; border:none; background:none; width:calc(100% - 16px);
}
.sb-link:hover { background:rgba(255,255,255,0.06); color:#cbd5e1; }
.sb-link.active { background:rgba(56,189,248,0.12); color:#38bdf8; }
.sb-link.active::before {
  content:''; position:absolute; left:0; top:22%; bottom:22%;
  width:3px; border-radius:0 3px 3px 0; background:#38bdf8;
}
.sb-divider { height:1px; background:rgba(255,255,255,0.05); margin:8px 12px; }
/* ── ALERT BAR ── */
.alert-bar {
  background:rgba(239,68,68,0.09);
  border-left:4px solid #ef4444;
  padding:10px 24px;
  font-size:13px; color:#fca5a5;
  display:flex; align-items:center; gap:10px;
  animation:fadeUp .4s ease .2s both;
}
.alert-dot { width:8px; height:8px; border-radius:50%; background:#ef4444; flex-shrink:0; animation:blink 1.5s infinite; }
/* ── PANELS ── */
.panel {
  background:rgba(22,34,57,0.75);
  backdrop-filter:blur(10px);
  border:1px solid rgba(255,255,255,0.07);
  border-radius:12px;
  animation:fadeUp .5s ease both;
}
.panel-title { font-size:11px; font-weight:600; text-transform:uppercase; letter-spacing:.07em; color:#475569; }
/* ── STAT CARDS ── */
.stat-card {
  background:rgba(22,34,57,0.8);
  backdrop-filter:blur(10px);
  border:1px solid rgba(255,255,255,0.07)!important;
  border-radius:12px;
  transition:transform .2s, box-shadow .2s;
  animation:fadeUp .5s ease both;
  cursor:default;
}
.stat-card:hover { transform:translateY(-3px); box-shadow:0 10px 32px rgba(0,0,0,.5)!important; }
.card-lbl { font-size:11px; font-weight:500; color:#64748b; }
.card-val { font-size:24px; font-weight:700; line-height:1.1; transition:all .3s; animation:countUp .4s ease both; }
.card-sub { font-size:11px; color:#475569; }
/* ── PROGRESS ── */
.prog-track { height:6px; background:rgba(0,0,0,.35); border-radius:20px; overflow:hidden; }
.prog-fill  { height:100%; border-radius:20px; transition:width 1.2s cubic-bezier(.4,0,.2,1); }
.prog-lbl   { font-size:13px; font-weight:500; color:#94a3b8; }
.prog-info  { font-size:11px; color:#475569; }
.prog-pct   { font-size:12px; font-weight:700; font-family:'JetBrains Mono',monospace; }
/* ── SERVICES ── */
.svc-row { font-size:13px; border-bottom:1px solid rgba(255,255,255,.05); transition:background .15s; cursor:default; }
.svc-row:last-child { border-bottom:none; }
.svc-row:hover { background:rgba(255,255,255,.02); border-radius:6px; }
.status-dot { width:8px; height:8px; border-radius:50%; display:inline-block; position:relative; flex-shrink:0; }
.status-dot.dot-green { background:#10b981; box-shadow:0 0 0 0 rgba(16,185,129,.4); animation:pulse-status 2s infinite; }
.status-dot.dot-red   { background:#ef4444; }
.status-dot.dot-amber { background:#f59e0b; animation:blink 2s infinite; }
@keyframes pulse-status {
  0%   { box-shadow:0 0 0 0 rgba(16,185,129,.5); }
  70%  { box-shadow:0 0 0 6px rgba(16,185,129,0); }
  100% { box-shadow:0 0 0 0 rgba(16,185,129,0); }
}
.pill { font-size:10px; font-weight:600; padding:2px 9px; border-radius:20px; }
.pill-g { background:rgba(16,185,129,.12); color:#34d399; }
.pill-r { background:rgba(239,68,68,.12);  color:#f87171; }
.pill-a { background:rgba(245,158,11,.12); color:#fbbf24; }
.pill-b { background:rgba(56,189,248,.12); color:#38bdf8; }
/* ── TABLE ── */
.dark-table { width:100%; border-collapse:collapse; font-size:12px; }
.dark-table th { font-size:10px; font-weight:600; text-transform:uppercase; letter-spacing:.05em; color:#475569; padding:0 10px 10px; text-align:left; border-bottom:1px solid rgba(255,255,255,.07); }
.dark-table td { padding:8px 10px; border-bottom:1px solid rgba(255,255,255,.03); font-family:'JetBrains Mono',monospace; font-size:11px; color:#64748b; transition:background .15s; }
.dark-table tr:last-child td { border-bottom:none; }
.dark-table tbody tr:hover td { background:rgba(255,255,255,.025); }
.td-w { color:#e2e8f0!important; font-weight:600; }
/* ── LOG ── */
.log-area {
  width:100%; height:195px; resize:none;
  font-family:'JetBrains Mono',monospace; font-size:11px; line-height:1.8;
  background:rgba(4,9,20,.9); color:#7dd3fc;
  border:1px solid rgba(255,255,255,.07); border-radius:8px;
  padding:10px 12px; outline:none;
}
.log-chip { font-size:10px; font-weight:600; padding:2px 9px; border-radius:20px; cursor:pointer; transition:.15s; }
.log-chip.active-chip { ring:2px; }
.chip-r { background:rgba(239,68,68,.12); color:#f87171; }
.chip-r.active-chip { background:rgba(239,68,68,.3); }
.chip-a { background:rgba(245,158,11,.12); color:#fbbf24; }
.chip-a.active-chip { background:rgba(245,158,11,.3); }
.chip-b { background:rgba(59,130,246,.12); color:#60a5fa; }
.chip-b.active-chip { background:rgba(59,130,246,.3); }
/* ── STORAGE ── */
.stor-bar  { height:3px; background:rgba(0,0,0,.35); border-radius:20px; margin-top:4px; overflow:hidden; }
.stor-fill { height:100%; border-radius:20px; transition:width 1.2s cubic-bezier(.4,0,.2,1); }
/* ── SYSINFO ── */
.si-box { background:rgba(0,0,0,.25); border:1px solid rgba(255,255,255,.06); border-radius:8px; }
.si-label { font-size:10px; color:#475569; }
.si-val   { font-size:13px; font-weight:600; color:#e2e8f0; }
.si-sub   { font-size:10px; color:#475569; }
/* ── FORM ── */
.form-control-dark, .form-select-dark {
  background:rgba(10,16,32,.85)!important;
  border:1px solid rgba(255,255,255,.1)!important;
  color:#cbd5e1!important; border-radius:8px;
}
.form-control-dark:focus, .form-select-dark:focus {
  border-color:#38bdf8!important;
  box-shadow:0 0 0 3px rgba(56,189,248,.15)!important;
  color:#f1f5f9!important;
}
.form-control-dark::placeholder { color:#475569!important; }
.form-label-dark { font-size:12px; font-weight:500; color:#64748b; margin-bottom:5px; display:block; }
.form-check-input { background-color:rgba(10,16,32,.8)!important; border-color:rgba(255,255,255,.2)!important; }
.form-check-input:checked { background-color:#38bdf8!important; border-color:#38bdf8!important; }
.form-check-label { font-size:13px; color:#94a3b8; }
select.form-select-dark option { background:#0f172a; color:#cbd5e1; }
/* ── LIVE INDICATOR ── */
.live-dot { width:8px; height:8px; border-radius:50%; background:#10b981; display:inline-block; animation:blink 2s infinite; }
.live-badge { font-size:12px; color:#10b981; font-weight:500; }
.user-avatar {
  width:34px; height:34px; border-radius:50%;
  background:linear-gradient(135deg,#38bdf8,#818cf8);
  display:flex; align-items:center; justify-content:center;
  font-size:13px; font-weight:700; color:#fff;
}
/* ── PAGE VIEWS ── */
.page-view { display:none; }
.page-view.active { display:block; animation:fadeUp .4s ease; }
/* ── TOAST ── */
.toast-container { position:fixed; top:66px; right:16px; z-index:9999; }
.toast-msg {
  background:rgba(22,34,57,.97); backdrop-filter:blur(16px);
  border:1px solid rgba(255,255,255,.1); border-radius:10px;
  padding:12px 16px; margin-bottom:8px; font-size:13px;
  color:#e2e8f0; box-shadow:0 8px 24px rgba(0,0,0,.5);
  animation:fadeUp .3s ease;
  display:flex; align-items:center; gap:10px; min-width:260px;
}
.toast-msg.hide { opacity:0; transform:translateY(-8px); transition:.3s; }
/* ── CLOCK ── */
.clock-display { font-family:'JetBrains Mono',monospace; font-size:12px; color:#475569; }
/* ── SETTINGS PAGE ── */
.settings-section { border-bottom:1px solid rgba(255,255,255,.06); padding-bottom:20px; margin-bottom:20px; }
.settings-section:last-child { border-bottom:none; margin-bottom:0; padding-bottom:0; }
/* ── FOOTER ── */
.site-footer {
  background:rgba(10,16,32,.92);
  backdrop-filter:blur(14px);
  border-top:1px solid rgba(255,255,255,.07);
}
.ft-brand { font-size:18px; font-weight:700; color:#f1f5f9; }
.ft-brand span { color:#38bdf8; }
.ft-head { font-size:10px; font-weight:600; text-transform:uppercase; letter-spacing:.07em; color:#475569; }
.ft-link { font-size:13px; color:#475569; text-decoration:none; display:block; transition:color .15s; }
.ft-link:hover { color:#cbd5e1; }
.ft-tag { font-size:10px; padding:2px 8px; border-radius:20px; border:1px solid rgba(255,255,255,.08); color:#475569; 
.tag-sm { font-size:10px; font-weight:600; padding:2px 6px; border-radius:20px; vertical-align:middle; }
.tag-g { background:rgba(16,185,129,.15); color:#34d399; }
.tag-r { background:rgba(239,68,68,.15); color:#f87171; }
.mono { font-family:'JetBrains Mono',monospace; }
/* scrollbar */
::-webkit-scrollbar { width:4px; height:4px; }
::-webkit-scrollbar-track { background:transparent; }
::-webkit-scrollbar-thumb { background:rgba(255,255,255,.1); border-radius:4px; 
/* animation delays */
.ad1{animation-delay:.05s} .ad2{animation-delay:.1s} .ad3{animation-delay:.15s}
.ad4{animation-delay:.2s}  .ad5{animation-delay:.25s} .ad6{animation-delay:.3s}
/* progress bar hover tooltip */
.prog-wrap { position:relative; }
/* alert counters */
#alertCount { animation:blink 2s infinite; }
</style>
</head>
<body>
<!-- ══ TOAST CONTAINER ══ -->
<div class="toast-container" id="toastContainer"></div>
<!-- ══ NAVBAR ══ -->
<nav class="navbar navbar-expand-lg topnav sticky-top py-0" style="height:56px">
  <div class="container-fluid px-3">
    <a class="navbar-brand fw-bold" href="#" onclick="navigate('dashboard');return false;">
      <i class="bi bi-server me-2" style="color:#38bdf8"></i>Server<span>Panel</span>
    </a>
    <button class="navbar-toggler border-0 py-1" type="button" data-bs-toggle="collapse" data-bs-target="#navContent">
      <i class="bi bi-list text-secondary fs-5"></i>
    </button>
    <div class="collapse navbar-collapse" id="navContent">
      <ul class="navbar-nav ms-3 gap-1">
        <li class="nav-item"><a class="nav-link active" id="nav-dashboard" href="#" onclick="navigate('dashboard');return false;"><i class="bi bi-grid me-1"></i>Dashboard</a></li>
        <li class="nav-item"><a class="nav-link" id="nav-servers" href="#" onclick="navigate('servers');return false;"><i class="bi bi-hdd-stack me-1"></i>Servers</a></li>
        <li class="nav-item"><a class="nav-link" id="nav-logs" href="#" onclick="navigate('logs');return false;"><i class="bi bi-journal-text me-1"></i>Logs</a></li>
        <li class="nav-item"><a class="nav-link" id="nav-alerts" href="#" onclick="navigate('alerts');return false;"><i class="bi bi-bell me-1"></i>Alerts <span class="badge bg-danger ms-1" style="font-size:9px" id="alertCount">2</span></a></li>
        <li class="nav-item"><a class="nav-link" id="nav-settings" href="#" onclick="navigate('settings');return false;"><i class="bi bi-gear me-1"></i>Settings</a></li>
      </ul>
      <div class="ms-auto d-flex align-items-center gap-3 mt-2 mt-lg-0 mb-2 mb-lg-0">
        <span class="clock-display" id="clockDisplay">--:--:--</span>
        <span class="live-dot"></span>
        <span class="live-badge">All systems up</span>
        <div class="user-avatar">AK</div>
      </div>
    </div>
  </div>
</nav>
<!-- ══ LAYOUT ══ -->
<div class="d-flex">
  <!-- SIDEBAR -->
  <div class="sidebar d-none d-lg-flex flex-column pt-2">
    <div class="sb-label mt-1">Main</div>
    <button class="sb-link active" id="sb-dashboard" onclick="navigate('dashboard')"><i class="bi bi-grid-fill"></i>Dashboard</button>
    <button class="sb-link" id="sb-servers" onclick="navigate('servers')"><i class="bi bi-hdd-stack"></i>Servers<span class="ms-auto badge rounded-pill" style="background:rgba(56,189,248,.12);color:#38bdf8;font-size:10px">4</span></button>
    <button class="sb-link" id="sb-alerts" onclick="navigate('alerts')"><i class="bi bi-bell"></i>Alerts<span class="ms-auto badge rounded-pill bg-danger" style="font-size:10px" id="sbAlertCount">2</span></button>
    <div class="sb-divider"></div>
    <div class="sb-label">Infrastructure</div>
    <button class="sb-link" id="sb-logs" onclick="navigate('logs')"><i class="bi bi-terminal"></i>Log Viewer</button>
    <button class="sb-link" onclick="navigate('dashboard')"><i class="bi bi-database"></i>Storage</button>
    <button class="sb-link" onclick="navigate('servers')"><i class="bi bi-box"></i>Containers<span class="ms-auto badge rounded-pill" style="background:rgba(56,189,248,.12);color:#38bdf8;font-size:10px">5</span></button>
    <button class="sb-link" onclick="navigate('dashboard')"><i class="bi bi-diagram-3"></i>Network</button>
    <div class="sb-divider"></div>
    <div class="sb-label">Tools</div>
    <button class="sb-link" id="sb-settings" onclick="navigate('settings')"><i class="bi bi-gear"></i>Settings</button>
    <button class="sb-link" onclick="showToast('Opening help center…','info')"><i class="bi bi-question-circle"></i>Help</button>
  </div>
  <!-- CONTENT -->
  <div class="flex-grow-1" style="min-width:0">
    <!-- ══ PAGE: DASHBOARD ══ -->
    <div class="page-view active" id="page-dashboard">
      <!-- Page header -->
      <div class="d-flex align-items-center justify-content-between flex-wrap gap-2 px-4 py-3"
           style="background:rgba(10,16,32,.75);backdrop-filter:blur(10px);border-bottom:1px solid rgba(255,255,255,.07)">
        <div>
          <h1 class="fs-5 fw-bold text-white mb-0">Server Dashboard</h1>
          <p class="mb-0 mt-1 mono" style="font-size:12px;color:#64748b">
            <i class="bi bi-circle-fill me-1" style="color:#10b981;font-size:8px"></i>
            prod-server-01 &nbsp;·&nbsp; Ubuntu 22.04 LTS &nbsp;·&nbsp; <span id="headerTime">--:-- UTC</span>
          </p>
        </div>
        <div class="d-flex gap-2 flex-wrap">
          <button class="btn btn-sm btn-outline-secondary px-3" onclick="exportReport()"><i class="bi bi-download me-1"></i>Export</button>
          <button class="btn btn-sm btn-outline-secondary px-3" onclick="refreshAll()"><i class="bi bi-arrow-clockwise me-1"></i>Refresh</button>
          <button class="btn btn-sm btn-primary px-3" onclick="runDiagnostics()"><i class="bi bi-play-fill me-1"></i>Run Diagnostics</button>
        </div>
      </div>
      <!-- Alert bar -->
      <div class="alert-bar" id="alertBar">
        <span class="alert-dot"></span>
        <span id="alertMsg"><b style="color:#f87171">Warning:</b> Redis stopped unexpectedly (OOM) &nbsp;·&nbsp; /data disk at <span id="diskDataPctAlert">86</span>% — near critical</span>
        <span class="ms-auto pill pill-r" style="cursor:pointer" onclick="navigate('alerts')">2 alerts</span>
      </div>
      <div class="container-fluid p-3 p-lg-4">
        <!-- METRIC CARDS -->
        <div class="row g-3 mb-3">
          <div class="col-6 col-md-4 col-xl-2">
            <div class="stat-card card border-0 p-3 h-100 ad1">
              <div class="card-lbl mb-1"><i class="bi bi-cpu me-1"></i>CPU Usage</div>
              <div class="card-val" style="color:#60a5fa" id="cpuVal">63%</div>
              <div class="card-sub">8 cores · load <span id="loadVal">1.84</span></div>
            </div>
          </div>
          <div class="col-6 col-md-4 col-xl-2">
            <div class="stat-card card border-0 p-3 h-100 ad2">
              <div class="card-lbl mb-1"><i class="bi bi-memory me-1"></i>RAM Used</div>
              <div class="card-val" style="color:#34d399" id="ramVal">11.2 GB</div>
              <div class="card-sub">of 16 GB <span class="tag-sm tag-g" id="ramPct">70%</span></div>
            </div>
          </div>
          <div class="col-6 col-md-4 col-xl-2">
            <div class="stat-card card border-0 p-3 h-100 ad3">
              <div class="card-lbl mb-1"><i class="bi bi-hdd me-1"></i>Disk /root</div>
              <div class="card-val" style="color:#fbbf24" id="diskRootVal">68 GB</div>
              <div class="card-sub">of 100 GB · 68%</div>
            </div>
          </div>
          <div class="col-6 col-md-4 col-xl-2">
            <div class="stat-card card border-0 p-3 h-100 ad4">
              <div class="card-lbl mb-1"><i class="bi bi-hdd-fill me-1"></i>Disk /data</div>
              <div class="card-val" style="color:#f87171" id="diskDataVal">430 GB</div>
              <div class="card-sub">of 500 GB <span class="tag-sm tag-r" id="diskDataPct">86%</span></div>
            </div>
          </div>
          <div class="col-6 col-md-4 col-xl-2">
            <div class="stat-card card border-0 p-3 h-100 ad5">
              <div class="card-lbl mb-1"><i class="bi bi-arrow-down-up me-1"></i>Network In</div>
              <div class="card-val" style="color:#a78bfa" id="netInVal">9.2 MB/s</div>
              <div class="card-sub">Out · <span id="netOutVal">3.7</span> MB/s</div>
            </div>
          </div>
          <div class="col-6 col-md-4 col-xl-2">
            <div class="stat-card card border-0 p-3 h-100 ad6">
              <div class="card-lbl mb-1"><i class="bi bi-clock me-1"></i>Uptime</div>
              <div class="card-val" style="color:#38bdf8" id="uptimeVal">312d</div>
              <div class="card-sub" id="uptimeSub">7h 14m · stable</div>
            </div>
          </div>
        </div>
        <!-- RESOURCES + SERVICES -->
        <div class="row g-3 mb-3">
          <div class="col-lg-6">
            <div class="panel p-3 h-100">
              <div class="panel-title mb-3"><i class="bi bi-bar-chart-line me-2"></i>Resource Usage</div>
              <div class="mb-3 prog-wrap">
                <div class="d-flex justify-content-between mb-1"><span class="prog-lbl">CPU</span><span class="prog-info" id="cpuInfo">8 cores</span><b class="prog-pct" style="color:#60a5fa" id="cpuPct">63%</b></div>
                <div class="prog-track"><div class="prog-fill" id="cpuBar" style="width:63%;background:#3b82f6"></div></div>
              </div>
              <div class="mb-3 prog-wrap">
                <div class="d-flex justify-content-between mb-1"><span class="prog-lbl">RAM</span><span class="prog-info">11.2 / 16 GB</span><b class="prog-pct" style="color:#34d399" id="ramBarPct">70%</b></div>
                <div class="prog-track"><div class="prog-fill" id="ramBar" style="width:70%;background:#10b981"></div></div>
              </div>
              <div class="mb-3 prog-wrap">
                <div class="d-flex justify-content-between mb-1"><span class="prog-lbl">Disk /</span><span class="prog-info">68 / 100 GB</span><b class="prog-pct" style="color:#fbbf24">68%</b></div>
                <div class="prog-track"><div class="prog-fill" style="width:68%;background:#f59e0b"></div></div>
              </div>
              <div class="mb-3 prog-wrap">
                <div class="d-flex justify-content-between mb-1"><span class="prog-lbl">Disk /data</span><span class="prog-info" id="diskDataInfo">430 / 500 GB</span><b class="prog-pct" style="color:#f87171" id="diskDataBarPct">86%</b></div>
                <div class="prog-track"><div class="prog-fill" id="diskDataBar" style="width:86%;background:#ef4444"></div></div>
              </div>
              <div class="mb-3 prog-wrap">
                <div class="d-flex justify-content-between mb-1"><span class="prog-lbl">Swap</span><span class="prog-info">1.1 / 8 GB</span><b class="prog-pct" style="color:#a78bfa" id="swapPct">14%</b></div>
                <div class="prog-track"><div class="prog-fill" id="swapBar" style="width:14%;background:#8b5cf6"></div></div>
              </div>
              <div class="prog-wrap">
                <div class="d-flex justify-content-between mb-1"><span class="prog-lbl">Network BW</span><span class="prog-info" id="netBwInfo">9.2 MB/s</span><b class="prog-pct" style="color:#22d3ee" id="netBwPct">46%</b></div>
                <div class="prog-track"><div class="prog-fill" id="netBwBar" style="width:46%;background:#06b6d4"></div></div>
              </div>
            </div>
          </div>
          <div class="col-lg-6">
            <div class="panel p-3 h-100">
              <div class="d-flex align-items-center justify-content-between mb-3">
                <div class="panel-title"><i class="bi bi-activity me-2"></i>Services Status</div>
                <button class="btn btn-sm btn-outline-secondary py-0 px-2" style="font-size:11px" onclick="refreshServices()"><i class="bi bi-arrow-clockwise me-1"></i>Refresh</button>
              </div>
              <div id="servicesContainer">
                <!-- populated by JS -->
              </div>
            </div>
          </div>
        </div>
        <!-- NETWORK + STORAGE -->
        <div class="row g-3 mb-3">
          <div class="col-lg-8">
            <div class="panel p-3 h-100">
              <div class="panel-title mb-3"><i class="bi bi-diagram-3 me-2"></i>Network Interfaces</div>
              <div class="table-responsive">
                <table class="dark-table">
                  <thead><tr><th>Interface</th><th>IP</th><th class="d-none d-md-table-cell">In</th><th class="d-none d-md-table-cell">Out</th><th>Conn</th><th>Status</th></tr></thead>
                  <tbody id="networkTable"></tbody>
                </table>
              </div>
            </div>
          </div>
          <div class="col-lg-4">
            <div class="panel p-3 h-100">
              <div class="panel-title mb-3"><i class="bi bi-hdd-stack me-2"></i>Storage Volumes</div>
              <div id="storageContainer"></div>
            </div>
          </div>
        </div>
        <!-- EVENTS + LOG -->
        <div class="row g-3 mb-3">
          <div class="col-lg-4">
            <div class="panel p-3 h-100">
              <div class="panel-title mb-3"><i class="bi bi-lightning me-2"></i>Recent Events</div>
              <div id="eventsContainer"></div>
            </div>
          </div>
          <div class="col-lg-8">
            <div class="panel p-3 h-100">
              <div class="d-flex align-items-center justify-content-between mb-2 flex-wrap gap-2">
                <div class="panel-title"><i class="bi bi-terminal me-2"></i>Live System Log</div>
                <div class="d-flex gap-2 align-items-center flex-wrap">
                  <span class="log-chip chip-r active-chip" id="chip-err" onclick="filterLog('err')">0 ERR</span>
                  <span class="log-chip chip-a" id="chip-warn" onclick="filterLog('warn')">0 WARN</span>
                  <span class="log-chip chip-b active-chip" id="chip-info" onclick="filterLog('info')">0 INFO</span>
                  <button class="btn btn-sm btn-outline-secondary py-0 px-2" style="font-size:11px" onclick="clearLog()"><i class="bi bi-trash3"></i></button>
                  <button class="btn btn-sm btn-outline-secondary py-0 px-2" style="font-size:11px" onclick="pauseLog()" id="pauseBtn"><i class="bi bi-pause-fill"></i></button>
                </div>
              </div>
              <textarea class="log-area" readonly id="logArea"></textarea>
              <div class="row g-2 mt-1">
                <div class="col-6 col-md-3"><div class="si-box p-2"><div class="si-label"><i class="bi bi-ubuntu me-1"></i>OS</div><div class="si-val">Ubuntu 22.04</div><div class="si-sub">LTS Jammy</div></div></div>
                <div class="col-6 col-md-3"><div class="si-box p-2"><div class="si-label"><i class="bi bi-layers me-1"></i>Kernel</div><div class="si-val">6.5.0-21</div><div class="si-sub">x86_64</div></div></div>
                <div class="col-6 col-md-3"><div class="si-box p-2"><div class="si-label"><i class="bi bi-speedometer2 me-1"></i>Load avg</div><div class="si-val" id="sysLoad">1.84</div><div class="si-sub">1m average</div></div></div>
                <div class="col-6 col-md-3"><div class="si-box p-2"><div class="si-label"><i class="bi bi-thermometer-half me-1"></i>CPU Temp</div><div class="si-val" style="color:#fbbf24" id="cpuTemp">58°C</div><div class="si-sub">safe range</div></div></div>
              </div>
            </div>
          </div>
        </div>
        <!-- DOCKER -->
        <div class="row g-3 mb-3">
          <div class="col-12">
            <div class="panel p-3">
              <div class="d-flex align-items-center justify-content-between mb-3 flex-wrap gap-2">
                <div class="panel-title"><i class="bi bi-box me-2"></i>Docker Containers</div>
                <button class="btn btn-sm btn-outline-secondary py-0 px-2" style="font-size:11px" onclick="refreshContainers()"><i class="bi bi-arrow-clockwise me-1"></i>Refresh</button>
              </div>
              <div class="table-responsive">
                <table class="dark-table">
                  <thead><tr><th>Container</th><th>Image</th><th class="d-none d-md-table-cell">Ports</th><th>CPU</th><th>Memory</th><th>Uptime</th><th>Status</th><th>Action</th></tr></thead>
                  <tbody id="dockerTable"></tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
        <!-- QUICK ACTIONS + LOG SEARCH -->
        <div class="row g-3 mb-3">
          <div class="col-lg-6">
            <div class="panel p-3 h-100">
              <div class="panel-title mb-3"><i class="bi bi-sliders me-2"></i>Quick Actions</div>
              <div class="mb-3">
                <label class="form-label-dark">Select Server</label>
                <select class="form-select form-select-sm form-select-dark" id="actionServer">
                  <option>prod-server-01 (current)</option>
                  <option>prod-server-02</option>
                  <option>staging-server-01</option>
                  <option>dev-server-01</option>
                </select>
              </div>
              <div class="mb-3">
                <label class="form-label-dark">Action</label>
                <select class="form-select form-select-sm form-select-dark" id="actionType">
                  <option value="restart">Restart service</option>
                  <option value="diag">Run diagnostics</option>
                  <option value="cache">Clear cache</option>
                  <option value="backup">Force backup</option>
                  <option value="rotate">Rotate logs</option>
                </select>
              </div>
              <div class="mb-3">
                <label class="form-label-dark">Target Service</label>
                <input type="text" class="form-control form-control-sm form-control-dark" id="actionTarget" placeholder="e.g. redis, nginx, postgres">
              </div>
              <div class="mb-3">
                <label class="form-label-dark">Notes</label>
                <textarea class="form-control form-control-sm form-control-dark" rows="2" id="actionNotes" placeholder="Reason for action..."></textarea>
              </div>
              <div class="mb-3 d-flex gap-3">
                <div class="form-check"><input class="form-check-input" type="checkbox" id="chkNotify" checked><label class="form-check-label" for="chkNotify">Notify team</label></div>
                <div class="form-check"><input class="form-check-input" type="checkbox" id="chkLog" checked><label class="form-check-label" for="chkLog">Log action</label></div>
              </div>
              <div class="d-flex gap-2">
                <button class="btn btn-sm btn-primary px-3" onclick="executeAction()"><i class="bi bi-play-fill me-1"></i>Execute</button>
                <button class="btn btn-sm btn-outline-secondary px-3" onclick="clearForm()"><i class="bi bi-x me-1"></i>Clear</button>
              </div>
              <div id="actionResult" class="mt-3" style="display:none"></div>
            </div>
         </div>
          <div class="col-lg-6">
            <div class="panel p-3 h-100">
              <div class="panel-title mb-3"><i class="bi bi-search me-2"></i>Search & Filter Logs</div>
              <div class="mb-3">
                <label class="form-label-dark">Search keyword</label>
                <div class="input-group input-group-sm">
                  <span class="input-group-text" style="background:rgba(10,16,32,.8);border-color:rgba(255,255,255,.1);color:#64748b"><i class="bi bi-search"></i></span>
                  <input type="text" class="form-control form-control-dark" placeholder="Search logs..." id="logSearch" oninput="searchLogs()">
                </div>
              </div>
              <div class="row g-2 mb-3">
                <div class="col-6">
                  <label class="form-label-dark">Log level</label>
                  <select class="form-select form-select-sm form-select-dark" id="logLevelFilter" onchange="searchLogs()">
                    <option value="all">All levels</option>
                    <option value="error">ERROR only</option>
                    <option value="warn">WARN + ERROR</option>
                    <option value="info">INFO only</option>
                  </select>
                </div>
                <div class="col-6">
                  <label class="form-label-dark">Service</label>
                  <select class="form-select form-select-sm form-select-dark" id="logServiceFilter" onchange="searchLogs()">
                    <option value="all">All services</option>
                    <option value="nginx">nginx</option>
                    <option value="postgres">postgres</option>
                    <option value="redis">redis</option>
                    <option value="node">node</option>
                    <option value="cron">cron</option>
                    <option value="disk">disk</option>
                  </select>
                </div>
              </div>
              <div class="mb-3">
                <label class="form-label-dark">Results: <span id="searchResultCount" style="color:#38bdf8">—</span></label>
                <textarea class="log-area" readonly id="searchLogArea" style="height:140px"></textarea>
              </div>
              <div class="d-flex gap-2">
                <button class="btn btn-sm btn-primary px-3" onclick="searchLogs()"><i class="bi bi-search me-1"></i>Search</button>
                <button class="btn btn-sm btn-outline-secondary px-3" onclick="downloadSearchResults()"><i class="bi bi-download me-1"></i>Export</button>
                <button class="btn btn-sm btn-outline-secondary px-3" onclick="resetSearch()"><i class="bi bi-x me-1"></i>Reset</button>
              </div>
            </div>
          </div>
        </div>
      </div><!-- end container-fluid -->
    </div><!-- end page-dashboard -->
    <!-- ══ PAGE: SERVERS ══ -->
    <div class="page-view" id="page-servers">
      <div class="d-flex align-items-center justify-content-between px-4 py-3" style="background:rgba(10,16,32,.75);backdrop-filter:blur(10px);border-bottom:1px solid rgba(255,255,255,.07)">
        <div><h1 class="fs-5 fw-bold text-white mb-0">Server Fleet</h1><p class="mb-0 mono" style="font-size:12px;color:#64748b">4 servers registered</p></div>
        <button class="btn btn-sm btn-primary px-3" onclick="showToast('Add server dialog coming soon…','info')"><i class="bi bi-plus-lg me-1"></i>Add Server</button>
      </div>
      <div class="container-fluid p-4">
        <div class="row g-3" id="serverCards"></div>
      </div>
    </div>
    <!-- ══ PAGE: LOGS ══ -->
    <div class="page-view" id="page-logs">
      <div class="d-flex align-items-center justify-content-between px-4 py-3" style="background:rgba(10,16,32,.75);backdrop-filter:blur(10px);border-bottom:1px solid rgba(255,255,255,.07)">
        <div><h1 class="fs-5 fw-bold text-white mb-0">Log Viewer</h1><p class="mb-0 mono" style="font-size:12px;color:#64748b">Real-time system logs</p></div>
        <div class="d-flex gap-2">
          <button class="btn btn-sm btn-outline-secondary px-3" onclick="clearLog()"><i class="bi bi-trash3 me-1"></i>Clear</button>
          <button class="btn btn-sm btn-primary px-3" onclick="downloadLog()"><i class="bi bi-download me-1"></i>Download</button>
        </div>
      </div>
      <div class="container-fluid p-4">
        <div class="panel p-3">
          <div class="d-flex gap-2 mb-3 flex-wrap">
            <input type="text" class="form-control form-control-sm form-control-dark" style="max-width:250px" placeholder="Filter logs…" id="logPageFilter" oninput="filterLogPage()">
            <select class="form-select form-select-sm form-select-dark" style="max-width:160px" id="logPageLevel" onchange="filterLogPage()">
              <option value="all">All levels</option>
              <option value="ERROR">ERROR</option>
              <option value="WARN">WARN</option>
              <option value="INFO">INFO</option>
            </select>
            <button class="btn btn-sm btn-outline-secondary px-3" onclick="filterLogPage()"><i class="bi bi-funnel me-1"></i>Filter</button>
          </div>
          <textarea class="log-area" readonly id="logPageArea" style="height:420px"></textarea>
        </div>
      </div>
    </div>
    <!-- ══ PAGE: ALERTS ══ -->
    <div class="page-view" id="page-alerts">
      <div class="d-flex align-items-center justify-content-between px-4 py-3" style="background:rgba(10,16,32,.75);backdrop-filter:blur(10px);border-bottom:1px solid rgba(255,255,255,.07)">
        <div><h1 class="fs-5 fw-bold text-white mb-0">Alerts</h1><p class="mb-0 mono" style="font-size:12px;color:#64748b">Active alerts &amp; notifications</p></div>
        <button class="btn btn-sm btn-outline-secondary px-3" onclick="acknowledgeAll()"><i class="bi bi-check-all me-1"></i>Acknowledge All</button>
      </div>
      <div class="container-fluid p-4">
        <div id="alertsList"></div>
      </div>
    </div>
    <!-- ══ PAGE: SETTINGS ══ -->
    <div class="page-view" id="page-settings">
      <div class="px-4 py-3" style="background:rgba(10,16,32,.75);backdrop-filter:blur(10px);border-bottom:1px solid rgba(255,255,255,.07)">
        <h1 class="fs-5 fw-bold text-white mb-0">Settings</h1>
        <p class="mb-0 mono" style="font-size:12px;color:#64748b">Dashboard configuration</p>
      </div>
      <div class="container-fluid p-4">
        <div class="row g-3">
          <div class="col-lg-6">
            <div class="panel p-4">
              <div class="settings-section">
                <h6 class="text-white fw-semibold mb-3"><i class="bi bi-bell me-2" style="color:#38bdf8"></i>Alert Thresholds</h6>
                <div class="mb-3">
                  <label class="form-label-dark">CPU Alert Threshold (%)</label>
                  <input type="range" class="form-range" min="50" max="99" value="85" id="cpuThreshold" oninput="document.getElementById('cpuThresholdVal').textContent=this.value+'%'" style="accent-color:#38bdf8">
                  <div class="d-flex justify-content-between"><span style="font-size:11px;color:#475569">50%</span><span style="font-size:11px;color:#38bdf8" id="cpuThresholdVal">85%</span><span style="font-size:11px;color:#475569">99%</span></div>
                </div>
                <div class="mb-3">
                  <label class="form-label-dark">Disk Alert Threshold (%)</label>
                  <input type="range" class="form-range" min="50" max="99" value="80" id="diskThreshold" oninput="document.getElementById('diskThresholdVal').textContent=this.value+'%'" style="accent-color:#38bdf8">
                  <div class="d-flex justify-content-between"><span style="font-size:11px;color:#475569">50%</span><span style="font-size:11px;color:#38bdf8" id="diskThresholdVal">80%</span><span style="font-size:11px;color:#475569">99%</span></div>
                </div>
                <div class="mb-3">
                  <label class="form-label-dark">RAM Alert Threshold (%)</label>
                  <input type="range" class="form-range" min="50" max="99" value="90" id="ramThreshold" oninput="document.getElementById('ramThresholdVal').textContent=this.value+'%'" style="accent-color:#38bdf8">
                  <div class="d-flex justify-content-between"><span style="font-size:11px;color:#475569">50%</span><span style="font-size:11px;color:#38bdf8" id="ramThresholdVal">90%</span><span style="font-size:11px;color:#475569">99%</span></div>
                </div>
              </div>
              <div class="settings-section">
                <h6 class="text-white fw-semibold mb-3"><i class="bi bi-envelope me-2" style="color:#38bdf8"></i>Notifications</h6>
                <div class="mb-2"><div class="form-check form-switch"><input class="form-check-input" type="checkbox" id="emailAlerts" checked><label class="form-check-label" for="emailAlerts">Email alerts</label></div></div>
                <div class="mb-2"><div class="form-check form-switch"><input class="form-check-input" type="checkbox" id="slackAlerts" checked><label class="form-check-label" for="slackAlerts">Slack notifications</label></div></div>
                <div class="mb-3"><div class="form-check form-switch"><input class="form-check-input" type="checkbox" id="smsAlerts"><label class="form-check-label" for="smsAlerts">SMS alerts</label></div></div>
                <div class="mb-3">
                  <label class="form-label-dark">Alert Email</label>
                  <input type="email" class="form-control form-control-sm form-control-dark" value="admin@company.com" id="alertEmail">
                </div>
              </div>
              <button class="btn btn-sm btn-primary px-4" onclick="saveSettings()"><i class="bi bi-check-lg me-1"></i>Save Settings</button>
            </div>
          </div>
          <div class="col-lg-6">
            <div class="panel p-4">
              <div class="settings-section">
                <h6 class="text-white fw-semibold mb-3"><i class="bi bi-display me-2" style="color:#38bdf8"></i>Dashboard Preferences</h6>
                <div class="mb-3">
                  <label class="form-label-dark">Refresh Interval</label>
                  <select class="form-select form-select-sm form-select-dark" id="refreshInterval" onchange="updateRefreshInterval()">
                    <option value="3000">Every 3 seconds</option>
                    <option value="5000" selected>Every 5 seconds</option>
                    <option value="10000">Every 10 seconds</option>
                    <option value="30000">Every 30 seconds</option>
                  </select>
                </div>
                <div class="mb-3">
                  <label class="form-label-dark">Log Lines to Display</label>
                  <select class="form-select form-select-sm form-select-dark" id="logLines">
                    <option value="50">50 lines</option>
                    <option value="100" selected>100 lines</option>
                    <option value="200">200 lines</option>
                    <option value="500">500 lines</option>
                  </select>
                </div>
                <div class="mb-2"><div class="form-check form-switch"><input class="form-check-input" type="checkbox" id="autoScroll" checked><label class="form-check-label" for="autoScroll">Auto-scroll log</label></div></div>
                <div class="mb-2"><div class="form-check form-switch"><input class="form-check-input" type="checkbox" id="soundAlerts"><label class="form-check-label" for="soundAlerts">Sound on error</label></div></div>
                <div class="mb-2"><div class="form-check form-switch"><input class="form-check-input" type="checkbox" id="compactMode"><label class="form-check-label" for="compactMode">Compact mode</label></div></div>
              </div>
              <div class="settings-section">
                <h6 class="text-white fw-semibold mb-3"><i class="bi bi-server me-2" style="color:#38bdf8"></i>Server Info</h6>
                <div class="mb-2 d-flex justify-content-between"><span style="font-size:13px;color:#64748b">Hostname</span><span class="mono" style="font-size:12px;color:#e2e8f0">prod-server-01</span></div>
                <div class="mb-2 d-flex justify-content-between"><span style="font-size:13px;color:#64748b">IP Address</span><span class="mono" style="font-size:12px;color:#e2e8f0">10.0.1.12</span></div>
                <div class="mb-2 d-flex justify-content-between"><span style="font-size:13px;color:#64748b">OS</span><span class="mono" style="font-size:12px;color:#e2e8f0">Ubuntu 22.04 LTS</span></div>
                <div class="mb-2 d-flex justify-content-between"><span style="font-size:13px;color:#64748b">Kernel</span><span class="mono" style="font-size:12px;color:#e2e8f0">6.5.0-21-generic</span></div>
                <div class="mb-2 d-flex justify-content-between"><span style="font-size:13px;color:#64748b">Panel Version</span><span class="mono" style="font-size:12px;color:#38bdf8">v4.2.1</span></div>
              </div>
              <button class="btn btn-sm btn-outline-danger px-3" onclick="if(confirm('Reset all settings to defaults?'))showToast('Settings reset to defaults','success')"><i class="bi bi-arrow-counterclockwise me-1"></i>Reset Defaults</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- ══ FOOTER ══ -->
    <footer class="site-footer px-4 pt-4 pb-3">
      <div class="row g-4 mb-3">
        <div class="col-lg-4 col-md-6">
          <div class="ft-brand mb-2"><i class="bi bi-server me-2" style="color:#38bdf8"></i>Server<span>Panel</span></div>
          <p class="mb-3" style="font-size:13px;color:#475569;line-height:1.7;max-width:260px">A fully working server administration dashboard. Real-time metrics, live logs, interactive controls, and Bootstrap 5.</p>
          <div class="d-flex align-items-center gap-2">
            <span class="live-dot"></span>
            <span style="font-size:12px;color:#10b981">All systems operational · 99.98% uptime</span>
          </div>
          <div class="d-flex gap-2 mt-3">
            <a href="#" class="btn btn-sm btn-outline-secondary px-2 py-1" style="font-size:11px"><i class="bi bi-github me-1"></i>GitHub</a>
            <a href="#" class="btn btn-sm btn-outline-secondary px-2 py-1" style="font-size:11px"><i class="bi bi-book me-1"></i>Docs</a>
            <a href="#" class="btn btn-sm btn-outline-secondary px-2 py-1" style="font-size:11px"><i class="bi bi-discord me-1"></i>Discord</a>
          </div>
        </div>
        <div class="col-6 col-md-3 col-lg-2">
          <div class="ft-head mb-2">Platform</div>
          <div class="d-flex flex-column gap-2">
            <a class="ft-link" href="#" onclick="navigate('dashboard');return false;"><i class="bi bi-grid me-1"></i>Dashboard</a>
            <a class="ft-link" href="#" onclick="navigate('servers');return false;"><i class="bi bi-hdd-stack me-1"></i>Servers</a>
            <a class="ft-link" href="#" onclick="navigate('logs');return false;"><i class="bi bi-journal-text me-1"></i>Logs</a>
            <a class="ft-link" href="#" onclick="navigate('alerts');return false;"><i class="bi bi-bell me-1"></i>Alerts</a>
          </div>
        </div>
        <div class="col-6 col-md-3 col-lg-2">
          <div class="ft-head mb-2">Resources</div>
          <div class="d-flex flex-column gap-2">
            <a class="ft-link" href="#"><i class="bi bi-book me-1"></i>Documentation</a>
            <a class="ft-link" href="#"><i class="bi bi-code-slash me-1"></i>API Reference</a>
            <a class="ft-link" href="#"><i class="bi bi-terminal me-1"></i>CLI Tools</a>
            <a class="ft-link" href="#"><i class="bi bi-check-circle me-1"></i>Status Page</a>
          </div>
        </div>
        <div class="col-6 col-md-3 col-lg-2">
          <div class="ft-head mb-2">Company</div>
          <div class="d-flex flex-column gap-2">
            <a class="ft-link" href="#"><i class="bi bi-info-circle me-1"></i>About</a>
            <a class="ft-link" href="#"><i class="bi bi-shield me-1"></i>Security</a>
            <a class="ft-link" href="#"><i class="bi bi-lock me-1"></i>Privacy</a>
            <a class="ft-link" href="#"><i class="bi bi-envelope me-1"></i>Contact</a>
          </div>
        </div>
        <div class="col-md-6 col-lg-2">
          <div class="ft-head mb-2">Newsletter</div>
          <p style="font-size:12px;color:#475569;margin-bottom:10px">Get updates on new features.</p>
          <div class="input-group input-group-sm mb-2">
            <input type="email" class="form-control form-control-dark" placeholder="you@email.com" id="newsletterEmail">
            <button class="btn btn-primary btn-sm px-2" onclick="subscribeNewsletter()"><i class="bi bi-send"></i></button>
          </div>
          <p style="font-size:10px;color:#334155">No spam. Unsubscribe anytime.</p>
        </div>
      </div>
      <div class="d-flex align-items-center justify-content-between flex-wrap gap-2 pt-3" style="border-top:1px solid rgba(255,255,255,.06);font-size:12px;color:#334155">
        <span>© 2026 ServerPanel Inc. · Built for production infrastructure teams.</span>
        <div class="d-flex gap-2">
          <span class="ft-tag">v4.2.1</span>
          <span class="ft-tag"><i class="bi bi-bootstrap me-1"></i>Bootstrap 5</span>
          <span class="ft-tag"><i class="bi bi-icons me-1"></i>BI Icons</span>
          <span class="ft-tag">Fully Working</span>
        </div>
      </div>
    </footer>
  </div><!-- end content -->
</div><!-- end d-flex -->

<script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.3/js/bootstrap.bundle.min.js"></script>
<script>
// ═══════════════════════════════════════
//  STATE
// ═══════════════════════════════════════
const state = {
  cpu: 63, ram: 70, swap: 14, netBw: 46,
  netIn: 9.2, netOut: 3.7, temp: 58, load: 1.84,
  diskData: 86,
  logLines: [], logFilter: 'all', logPaused: false,
  refreshInterval: 5000, refreshTimer: null,
  uptimeSeconds: 312*86400 + 7*3600 + 14*60,
  alerts: [
    { id:1, level:'error', title:'Redis service stopped', msg:'Redis exited with OOM error (exit code 1). Memory usage exceeded limits.', time:'14:31:58', acked:false },
    { id:2, level:'warn',  title:'Disk /data near capacity', msg:'/data volume at 86% usage. Consider cleaning or expanding storage.', time:'14:31:10', acked:false },
    { id:3, level:'warn',  title:'Elasticsearch degraded', msg:'JVM heap usage at 78%. GC pressure detected.', time:'14:28:00', acked:false }
  ],
  services: [
    { name:'nginx',         port:':80/:443',  mem:'34 MB',   status:'running' },
    { name:'postgres',      port:':5432',     mem:'512 MB',  status:'running' },
    { name:'redis',         port:':6379',     mem:'—',       status:'stopped' },
    { name:'node',          port:':3000',     mem:'210 MB',  status:'running' },
    { name:'elasticsearch', port:':9200',     mem:'1.2 GB',  status:'degraded'},
    { name:'docker',        port:'daemon',    mem:'88 MB',   status:'running' },
    { name:'prometheus',    port:':9090',     mem:'156 MB',  status:'running' },
    { name:'cron',          port:'system',    mem:'4 MB',    status:'running' },
  ],
  containers: [
    { name:'app_web_1',    image:'node:20-alpine',  ports:'3000→3000', cpu:4.2,  mem:'210 MB', uptime:'6d 12h',  status:'running' },
    { name:'app_worker_3', image:'node:20-alpine',  ports:'—',         cpu:18.7, mem:'340 MB', uptime:'6d 12h',  status:'running' },
    { name:'pg_primary',   image:'postgres:16',     ports:'5432→5432', cpu:9.1,  mem:'512 MB', uptime:'12d 3h',  status:'running' },
    { name:'redis_cache',  image:'redis:7-alpine',  ports:'6379→6379', cpu:0,    mem:'—',      uptime:'Exited',  status:'exited'  },
    { name:'prometheus',   image:'prom/prometheus', ports:'9090→9090', cpu:1.4,  mem:'156 MB', uptime:'30d 0h',  status:'running' },
  ],
  logPool: [
    'INFO   [nginx]      200 GET /api/health — 3ms',
    'INFO   [nginx]      200 GET /dashboard — 12ms',
    'INFO   [nginx]      304 GET /static/main.js — 1ms',
    'INFO   [nginx]      200 POST /api/data — 28ms',
    'INFO   [postgres]   checkpoint complete: wrote 842 buffers',
    'INFO   [postgres]   autovacuum: table public.events',
    'INFO   [postgres]   connection established from 10.0.1.5',
    'INFO   [node]       active connections: 214',
    'INFO   [node]       cache hit ratio: 94.3%',
    'INFO   [node]       worker recycled after 24h uptime',
    'INFO   [cron]       job backup-db completed in 4.2s',
    'INFO   [cron]       scheduled job sync-metrics started',
    'INFO   [docker]     container app_worker_3 healthy',
    'INFO   [prometheus] scrape completed in 38ms',
    'WARN   [disk]       /data usage crossed 85% threshold',
    'WARN   [cron]       maintenance window in 6h',
    'WARN   [elasticsearch] JVM heap at 78% — tune GC',
    'ERROR  [redis]      service exited unexpectedly (OOM, exit 1)',
    'ERROR  [postgres]   slow query (1842ms): SELECT * FROM sessions',
  ],
  servers: [
    { name:'prod-server-01', ip:'10.0.1.12', os:'Ubuntu 22.04', cpu:63, status:'online',  uptime:'312d 7h' },
    { name:'prod-server-02', ip:'10.0.1.13', os:'Ubuntu 22.04', cpu:41, status:'online',  uptime:'45d 3h'  },
    { name:'staging-server', ip:'10.0.2.5',  os:'Debian 12',    cpu:18, status:'online',  uptime:'7d 12h'  },
    { name:'dev-server-01',  ip:'10.0.3.1',  os:'Ubuntu 22.04', cpu:0,  status:'offline', uptime:'0'       },
  ]
};

// ═══════════════════════════════════════
//  NAVIGATION
// ═══════════════════════════════════════
function navigate(page) {
  document.querySelectorAll('.page-view').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-link').forEach(a => a.classList.remove('active'));
  document.querySelectorAll('.sb-link').forEach(b => b.classList.remove('active'));

  const el = document.getElementById('page-' + page);
  if (el) el.classList.add('active');

  const nav = document.getElementById('nav-' + page);
  if (nav) nav.classList.add('active');
  const sb = document.getElementById('sb-' + page);
  if (sb) sb.classList.add('active');

  if (page === 'alerts') renderAlerts();
  if (page === 'servers') renderServerCards();
  if (page === 'logs') { renderLogPage(); }

  // collapse mobile navbar
  const nc = document.getElementById('navContent');
  if (nc.classList.contains('show')) {
    bootstrap.Collapse.getInstance(nc)?.hide();
  }
}

// ═══════════════════════════════════════
//  CLOCK
// ═══════════════════════════════════════
function updateClock() {
  const now = new Date();
  const t = now.toUTCString().slice(17,25);
  document.getElementById('clockDisplay').textContent = t + ' UTC';
  document.getElementById('headerTime').textContent   = t + ' UTC';
}
setInterval(updateClock, 1000);
updateClock();

// ═══════════════════════════════════════
//  UPTIME
// ═══════════════════════════════════════
function updateUptime() {
  state.uptimeSeconds++;
  const d = Math.floor(state.uptimeSeconds / 86400);
  const h = Math.floor((state.uptimeSeconds % 86400) / 3600);
  const m = Math.floor((state.uptimeSeconds % 3600) / 60);
  document.getElementById('uptimeVal').textContent = d + 'd';
  document.getElementById('uptimeSub').textContent = h + 'h ' + m + 'm · stable';
}
setInterval(updateUptime, 1000);

// ═══════════════════════════════════════
//  LIVE METRICS
// ═══════════════════════════════════════
function rand(min,max,dec=0) {
  const v = Math.random()*(max-min)+min;
  return dec ? +v.toFixed(dec) : Math.round(v);
}

function updateMetrics() {
  // CPU fluctuates
  state.cpu = Math.max(10, Math.min(95, state.cpu + rand(-6,6)));
  state.ram = Math.max(40, Math.min(90, state.ram + rand(-2,2)));
  state.swap = Math.max(5, Math.min(35, state.swap + rand(-2,2)));
  state.netIn  = rand(1,20,1);
  state.netOut = rand(0.5,10,1);
  state.netBw  = Math.round(state.netIn/20*100);
  state.load   = rand(0.4,4.0,2);
  state.temp   = rand(42,75);

  // update CPU card
  document.getElementById('cpuVal').textContent = state.cpu + '%';
  document.getElementById('loadVal').textContent = state.load;
  document.getElementById('cpuPct').textContent  = state.cpu + '%';
  document.getElementById('cpuBar').style.width  = state.cpu + '%';
  document.getElementById('cpuInfo').textContent = '8 cores';

  // RAM
  const ramGB = (state.ram/100*16).toFixed(1);
  document.getElementById('ramVal').textContent    = ramGB + ' GB';
  document.getElementById('ramPct').textContent    = state.ram + '%';
  document.getElementById('ramBarPct').textContent = state.ram + '%';
  document.getElementById('ramBar').style.width    = state.ram + '%';

  // Swap
  document.getElementById('swapPct').textContent = state.swap + '%';
  document.getElementById('swapBar').style.width = state.swap + '%';

  // Net
  document.getElementById('netInVal').textContent  = state.netIn + ' MB/s';
  document.getElementById('netOutVal').textContent = state.netOut;
  document.getElementById('netBwInfo').textContent = state.netIn + ' MB/s';
  document.getElementById('netBwPct').textContent  = state.netBw + '%';
  document.getElementById('netBwBar').style.width  = state.netBw + '%';

  // Sysinfo
  document.getElementById('sysLoad').textContent = state.load;
  document.getElementById('cpuTemp').textContent = state.temp + '°C';

  // Network table
  renderNetworkTable();

  // Disk /data fluctuates slowly
  if(Math.random() > 0.7) {
    state.diskData = Math.max(82, Math.min(92, state.diskData + (Math.random()>0.4?1:-1)));
    document.getElementById('diskDataVal').textContent     = Math.round(state.diskData/100*500) + ' GB';
    document.getElementById('diskDataPct').textContent     = state.diskData + '%';
    document.getElementById('diskDataBarPct').textContent  = state.diskData + '%';
    document.getElementById('diskDataBar').style.width     = state.diskData + '%';
    document.getElementById('diskDataPctAlert').textContent= state.diskData;
    document.getElementById('diskDataInfo').textContent    = Math.round(state.diskData/100*500) + ' / 500 GB';
  }

  // Container CPU fluctuate
  state.containers.forEach(c => {
    if(c.status==='running') c.cpu = rand(0.5,25,1);
  });
}

// ═══════════════════════════════════════
//  NETWORK TABLE
// ═══════════════════════════════════════
function renderNetworkTable() {
  const tbody = document.getElementById('networkTable');
  if(!tbody) return;
  const ifaces = [
    { name:'eth0',    ip:'10.0.1.12',   in:state.netIn,  out:state.netOut, conn:rand(180,250), status:'up' },
    { name:'eth1',    ip:'192.168.1.5', in:rand(0.1,1,1),out:rand(0.1,0.5,1), conn:rand(10,30), status:'up' },
    { name:'lo',      ip:'127.0.0.1',   in:rand(10,14,1),out:rand(10,14,1), conn:rand(800,900), status:'up' },
    { name:'docker0', ip:'172.17.0.1',  in:rand(1,3,1),  out:rand(0.5,1.5,1), conn:rand(40,70), status:'warn'},
  ];
  tbody.innerHTML = ifaces.map(i=>`
    <tr>
      <td class="td-w">${i.name}</td>
      <td>${i.ip}</td>
      <td class="d-none d-md-table-cell" style="color:#34d399">${i.in} MB/s</td>
      <td class="d-none d-md-table-cell" style="color:#60a5fa">${i.out} MB/s</td>
      <td>${i.conn}</td>
      <td><span class="pill ${i.status==='up'?'pill-g':'pill-a'}">${i.status==='up'?'Up':'Warn'}</span></td>
    </tr>`).join('');
}

// ═══════════════════════════════════════
//  SERVICES
// ═══════════════════════════════════════
function renderServices() {
  const c = document.getElementById('servicesContainer');
  if(!c) return;
  c.innerHTML = state.services.map(s=>{
    const cls = s.status==='running'?'dot-green':s.status==='stopped'?'dot-red':'dot-amber';
    const pill = s.status==='running'?'pill-g':s.status==='stopped'?'pill-r':'pill-a';
    const label = s.status.charAt(0).toUpperCase()+s.status.slice(1);
    return `<div class="svc-row py-2 d-flex align-items-center gap-2 px-1">
      <span class="status-dot ${cls}"></span>
      <span class="fw-semibold text-white" style="width:105px;font-size:13px">${s.name}</span>
      <span class="mono flex-grow-1" style="font-size:11px;color:#475569">${s.port}</span>
      <span class="mono" style="font-size:11px;color:#64748b;min-width:52px;text-align:right">${s.mem}</span>
      <span class="pill ${pill}">${label}</span>
      <button class="btn btn-sm py-0 px-1" style="font-size:10px;border:1px solid rgba(255,255,255,.1);color:#64748b;background:none;border-radius:4px" onclick="toggleService('${s.name}')" title="${s.status==='running'?'Stop':'Start'}">
        <i class="bi bi-${s.status==='running'?'stop-fill':'play-fill'}"></i>
      </button>
    </div>`;
  }).join('');
}

function toggleService(name) {
  const svc = state.services.find(s=>s.name===name);
  if(!svc) return;
  if(svc.status==='running'){
    svc.status='stopped'; svc.mem='—';
    showToast(`<i class="bi bi-stop-fill text-danger me-2"></i>Stopped <b>${name}</b>`,'error');
    addLogLine('WARN','system',`service ${name} manually stopped by admin`);
  } else {
    svc.status='running'; svc.mem=name==='redis'?'38 MB':svc.mem==='—'?'64 MB':svc.mem;
    showToast(`<i class="bi bi-play-fill text-success me-2"></i>Started <b>${name}</b>`,'success');
    addLogLine('INFO','system',`service ${name} started successfully`);
  }
  renderServices();
}

function refreshServices() {
  renderServices();
  showToast('<i class="bi bi-check-circle me-2 text-success"></i>Services refreshed','success');
}

// ═══════════════════════════════════════
//  STORAGE
// ═══════════════════════════════════════
function renderStorage() {
  const c = document.getElementById('storageContainer');
  if(!c) return;
  const vols = [
    { icon:'💾', name:'System /',   path:'ext4 · SSD',    used:68,  total:100,  unit:'GB',  color:'#f59e0b' },
    { icon:'🗄️', name:'Data /data', path:'xfs · RAID',    used:state.diskData,total:100, unit:'%', color:'#ef4444', isPercent:true, usedGB:Math.round(state.diskData/100*500),totalGB:500 },
    { icon:'📦', name:'Backups',    path:'ext4 · NAS',    used:41,  total:100,  unit:'%',  color:'#10b981', usedGB:820,totalGB:2000,tbunit:true },
    { icon:'🐳', name:'Docker',     path:'/var/lib/docker',used:29, total:100,  unit:'%',  color:'#8b5cf6', usedGB:29,totalGB:100 },
  ];
  c.innerHTML = vols.map((v,i)=>{
    const pct = v.isPercent ? state.diskData : v.used;
    const label = v.tbunit ? `${v.usedGB}GB / 2TB` : v.usedGB ? `${v.usedGB}/${v.totalGB} GB` : `${v.used}/${v.total} GB`;
    return `<div class="py-2 ${i<vols.length-1?'border-bottom':''}" style="border-color:rgba(255,255,255,.05)!important">
      <div class="d-flex align-items-center gap-2 mb-1">
        <span style="font-size:18px">${v.icon}</span>
        <div class="flex-grow-1">
          <div class="fw-semibold text-white" style="font-size:12px">${v.name}</div>
          <div class="mono" style="font-size:10px;color:#475569">${v.path}</div>
        </div>
        <span class="mono" style="font-size:10px;color:${pct>85?'#f87171':'#64748b'}">${label}</span>
      </div>
      <div class="stor-bar"><div class="stor-fill" style="width:${pct}%;background:${v.color}"></div></div>
    </div>`;
  }).join('');
}

// ═══════════════════════════════════════
//  LOG SYSTEM
// ═══════════════════════════════════════
let errCount=0, warnCount=0, infoCount=0;

function timeStr() {
  const n=new Date();
  return `[${n.getHours().toString().padStart(2,'0')}:${n.getMinutes().toString().padStart(2,'0')}:${n.getSeconds().toString().padStart(2,'0')}]`;
}

function addLogLine(level, service, msg) {
  const line = `${timeStr()}  ${level.padEnd(6)} [${service}]${' '.repeat(Math.max(1,12-service.length))}${msg}`;
  state.logLines.unshift(line);
  if(state.logLines.length > 200) state.logLines.pop();

  if(level==='ERROR') errCount++;
  else if(level==='WARN') warnCount++;
  else infoCount++;

  updateLogChips();
  renderLog();
}

function updateLogChips() {
  document.getElementById('chip-err').textContent  = errCount  + ' ERR';
  document.getElementById('chip-warn').textContent = warnCount + ' WARN';
  document.getElementById('chip-info').textContent = infoCount + ' INFO';
}

function filterLog(type) {
  ['err','warn','info'].forEach(t=>{
    const el = document.getElementById('chip-'+t);
    if(t===type) el.classList.toggle('active-chip');
    else el.classList.remove('active-chip');
  });
  if(state.logFilter===type) state.logFilter='all';
  else state.logFilter=type;
  renderLog();
}

function renderLog() {
  if(state.logPaused) return;
  const area = document.getElementById('logArea');
  if(!area) return;
  let lines = state.logLines;
  if(state.logFilter==='err')  lines = lines.filter(l=>l.includes('ERROR'));
  if(state.logFilter==='warn') lines = lines.filter(l=>l.includes('WARN'));
  if(state.logFilter==='info') lines = lines.filter(l=>l.includes('INFO'));
  area.value = lines.join('\n');
  area.scrollTop = 0;
  // also update log page
  const lpa = document.getElementById('logPageArea');
  if(lpa) lpa.value = area.value;
}

function clearLog() {
  state.logLines = []; errCount=0; warnCount=0; infoCount=0;
  updateLogChips(); renderLog();
  showToast('<i class="bi bi-trash3 me-2"></i>Log cleared','success');
}

function pauseLog() {
  state.logPaused = !state.logPaused;
  const btn = document.getElementById('pauseBtn');
  btn.innerHTML = state.logPaused
    ? '<i class="bi bi-play-fill"></i>'
    : '<i class="bi bi-pause-fill"></i>';
  btn.title = state.logPaused ? 'Resume' : 'Pause';
  showToast(state.logPaused ? 'Log paused' : 'Log resumed', 'info');
}

function downloadLog() {
  const blob = new Blob([state.logLines.join('\n')], {type:'text/plain'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'serverpanel-log-' + Date.now() + '.txt';
  a.click();
  showToast('<i class="bi bi-download me-2"></i>Log downloaded','success');
}

function filterLogPage() {
  const q = (document.getElementById('logPageFilter')?.value||'').toLowerCase();
  const lv = document.getElementById('logPageLevel')?.value||'all';
  let lines = state.logLines;
  if(lv!=='all') lines = lines.filter(l=>l.includes(lv));
  if(q) lines = lines.filter(l=>l.toLowerCase().includes(q));
  const area = document.getElementById('logPageArea');
  if(area) { area.value = lines.join('\n'); area.scrollTop=0; }
}

function renderLogPage() {
  const area = document.getElementById('logPageArea');
  if(area) { area.value = state.logLines.join('\n'); area.scrollTop=0; }
}

// Auto-add logs
function generateLogLine() {
  if(state.logPaused) return;
  const entry = state.logPool[Math.floor(Math.random()*state.logPool.length)];
  const parts = entry.match(/^(INFO|WARN|ERROR)\s+\[(\w+)\]\s+(.+)$/);
  if(parts) addLogLine(parts[1], parts[2], parts[3]);
}

// ═══════════════════════════════════════
//  EVENTS
// ═══════════════════════════════════════
const eventPool = [
  { dot:'#60a5fa', title:'Health check passed',    sub:'nginx · /api/health' },
  { dot:'#34d399', title:'Backup completed',        sub:'cron · success' },
  { dot:'#34d399', title:'Autovacuum completed',    sub:'postgres · public.events' },
  { dot:'#fbbf24', title:'High CPU warning',        sub:'cpu > 80% for 30s' },
  { dot:'#fbbf24', title:'Slow query detected',     sub:'postgres · >1s' },
  { dot:'#f87171', title:'Service error',           sub:'redis · OOM killed' },
  { dot:'#60a5fa', title:'Worker recycled',         sub:'node · healthy restart' },
  { dot:'#34d399', title:'Cache warmed up',         sub:'node · 94% hit rate' },
];
let recentEvents = [
  { dot:'#60a5fa', title:'Health check passed', sub:'nginx · /api/health · 3ms', time:'14:32' },
  { dot:'#f87171', title:'Redis service stopped', sub:'OOM killed · exit code 1', time:'14:31' },
  { dot:'#fbbf24', title:'Slow query detected', sub:'postgres · 1842ms', time:'14:31' },
  { dot:'#fbbf24', title:'/data usage > 85%', sub:'disk threshold alert', time:'14:30' },
  { dot:'#34d399', title:'Backup completed', sub:'cron · 4.2s · success', time:'14:30' },
  { dot:'#34d399', title:'Worker recycled', sub:'node · PID 29441', time:'14:29' },
];

function renderEvents() {
  const c = document.getElementById('eventsContainer');
  if(!c) return;
  c.innerHTML = recentEvents.slice(0,7).map(e=>`
    <div class="d-flex gap-2 py-2 border-bottom" style="border-color:rgba(255,255,255,.05)!important">
      <span style="font-family:'JetBrains Mono';font-size:10px;color:#475569;min-width:40px;padding-top:2px">${e.time}</span>
      <span style="width:7px;height:7px;border-radius:50%;background:${e.dot};flex-shrink:0;margin-top:5px"></span>
      <div>
        <div style="font-size:12px;font-weight:500;color:#cbd5e1">${e.title}</div>
        <div style="font-size:11px;color:#475569;margin-top:1px">${e.sub}</div>
      </div>
    </div>`).join('');
}

function addRandomEvent() {
  const e = eventPool[Math.floor(Math.random()*eventPool.length)];
  const now = new Date();
  const t = now.getHours().toString().padStart(2,'0')+':'+now.getMinutes().toString().padStart(2,'0');
  recentEvents.unshift({ ...e, time:t });
  if(recentEvents.length > 20) recentEvents.pop();
  renderEvents();
}

// ═══════════════════════════════════════
//  DOCKER TABLE
// ═══════════════════════════════════════
function renderDockerTable() {
  const tbody = document.getElementById('dockerTable');
  if(!tbody) return;
  tbody.innerHTML = state.containers.map(c=>{
    const pill = c.status==='running'?'pill-g':c.status==='exited'?'pill-r':'pill-a';
    const label = c.status.charAt(0).toUpperCase()+c.status.slice(1);
    const cpuColor = c.cpu>15?'#fbbf24':'#34d399';
    return `<tr>
      <td class="td-w">${c.name}</td>
      <td>${c.image}</td>
      <td class="d-none d-md-table-cell">${c.ports}</td>
      <td style="color:${cpuColor}">${c.status==='exited'?'—':c.cpu+'%'}</td>
      <td>${c.mem}</td>
      <td>${c.uptime}</td>
      <td><span class="pill ${pill}">${label}</span></td>
      <td>
        <button class="btn btn-sm py-0 px-1" style="font-size:10px;border:1px solid rgba(255,255,255,.1);color:#64748b;background:none;border-radius:4px" onclick="restartContainer('${c.name}')">
          <i class="bi bi-arrow-clockwise"></i>
        </button>
      </td>
    </tr>`;
  }).join('');
}

function restartContainer(name) {
  showToast(`<i class="bi bi-arrow-clockwise me-2"></i>Restarting <b>${name}</b>…`,'info');
  addLogLine('INFO','docker',`container ${name} restart initiated`);
  setTimeout(()=>{
    addLogLine('INFO','docker',`container ${name} restarted successfully`);
    showToast(`<i class="bi bi-check-circle me-2 text-success"></i><b>${name}</b> restarted`,'success');
  }, 2000);
}

function refreshContainers() {
  state.containers.forEach(c=>{ if(c.status==='running') c.cpu=rand(0.5,25,1); });
  renderDockerTable();
  showToast('<i class="bi bi-check-circle me-2 text-success"></i>Containers refreshed','success');
}

// ═══════════════════════════════════════
//  ALERTS PAGE
// ═══════════════════════════════════════
function renderAlerts() {
  const c = document.getElementById('alertsList');
  if(!c) return;
  const active = state.alerts.filter(a=>!a.acked);
  const acked  = state.alerts.filter(a=>a.acked);
  c.innerHTML = `
    <div class="panel p-3 mb-3">
      <div class="panel-title mb-3"><i class="bi bi-exclamation-triangle me-2" style="color:#f87171"></i>Active Alerts (${active.length})</div>
      ${active.length===0?'<p style="font-size:13px;color:#475569">No active alerts. All clear!</p>':''}
      ${active.map(a=>`
        <div class="d-flex gap-3 p-3 mb-2 rounded-3" style="background:rgba(${a.level==='error'?'239,68,68':'245,158,11'},.08);border:1px solid rgba(${a.level==='error'?'239,68,68':'245,158,11'},.2)">
          <i class="bi bi-${a.level==='error'?'x-circle-fill text-danger':'exclamation-triangle-fill text-warning'} mt-1"></i>
          <div class="flex-grow-1">
            <div class="fw-semibold text-white" style="font-size:13px">${a.title}</div>
            <div style="font-size:12px;color:#94a3b8;margin-top:3px">${a.msg}</div>
            <div class="mono" style="font-size:10px;color:#475569;margin-top:4px">${a.time}</div>
          </div>
          <button class="btn btn-sm btn-outline-secondary py-0 px-2" style="font-size:11px;height:fit-content" onclick="ackAlert(${a.id})">
            <i class="bi bi-check me-1"></i>Ack
          </button>
        </div>`).join('')}
    </div>
    ${acked.length>0?`
    <div class="panel p-3">
      <div class="panel-title mb-3" style="color:#334155"><i class="bi bi-check-all me-2"></i>Acknowledged (${acked.length})</div>
      ${acked.map(a=>`
        <div class="d-flex gap-3 p-2 mb-1 rounded-2" style="background:rgba(255,255,255,.02);opacity:.6">
          <i class="bi bi-check-circle-fill" style="color:#334155;margin-top:2px"></i>
          <div>
            <div style="font-size:13px;color:#475569">${a.title}</div>
            <div class="mono" style="font-size:10px;color:#334155">${a.time}</div>
          </div>
        </div>`).join('')}
    </div>`:''}`;

  updateAlertBadges();
}

function ackAlert(id) {
  const a = state.alerts.find(x=>x.id===id);
  if(a) { a.acked=true; renderAlerts(); updateAlertBadges(); showToast('<i class="bi bi-check-circle me-2 text-success"></i>Alert acknowledged','success'); }
}

function acknowledgeAll() {
  state.alerts.forEach(a=>a.acked=true);
  renderAlerts(); updateAlertBadges();
  showToast('<i class="bi bi-check-all me-2 text-success"></i>All alerts acknowledged','success');
}

function updateAlertBadges() {
  const count = state.alerts.filter(a=>!a.acked).length;
  ['alertCount','sbAlertCount'].forEach(id=>{
    const el = document.getElementById(id);
    if(el) { el.textContent=count; el.style.display=count>0?'':'none'; }
  });
}

// ═══════════════════════════════════════
//  SERVERS PAGE
// ═══════════════════════════════════════
function renderServerCards() {
  const c = document.getElementById('serverCards');
  if(!c) return;
  c.innerHTML = state.servers.map(s=>`
    <div class="col-md-6 col-xl-3">
      <div class="panel p-3 h-100">
        <div class="d-flex align-items-center justify-content-between mb-3">
          <div class="fw-bold text-white" style="font-size:14px"><i class="bi bi-server me-2" style="color:#38bdf8"></i>${s.name}</div>
          <span class="pill ${s.status==='online'?'pill-g':'pill-r'}">${s.status}</span>
        </div>
        <div class="mb-2 d-flex justify-content-between"><span style="font-size:12px;color:#64748b">IP</span><span class="mono" style="font-size:12px;color:#e2e8f0">${s.ip}</span></div>
        <div class="mb-2 d-flex justify-content-between"><span style="font-size:12px;color:#64748b">OS</span><span class="mono" style="font-size:12px;color:#e2e8f0">${s.os}</span></div>
        <div class="mb-2 d-flex justify-content-between"><span style="font-size:12px;color:#64748b">Uptime</span><span class="mono" style="font-size:12px;color:#34d399">${s.uptime}</span></div>
        <div class="mb-1" style="font-size:12px;color:#64748b">CPU</div>
        <div class="prog-track"><div class="prog-fill" style="width:${s.cpu}%;background:${s.cpu>80?'#ef4444':s.cpu>60?'#f59e0b':'#3b82f6'}"></div></div>
        <div class="mono mt-1 mb-3" style="font-size:10px;color:#475569">${s.cpu}% utilization</div>
        <div class="d-flex gap-2">
          <button class="btn btn-sm btn-outline-secondary px-2 py-0" style="font-size:11px" onclick="showToast('Connecting to ${s.name}…','info')"><i class="bi bi-terminal me-1"></i>SSH</button>
          <button class="btn btn-sm btn-outline-secondary px-2 py-0" style="font-size:11px" onclick="navigate('dashboard')"><i class="bi bi-speedometer2 me-1"></i>Monitor</button>
          ${s.status==='online'?`<button class="btn btn-sm btn-outline-danger px-2 py-0" style="font-size:11px" onclick="showToast('Restart scheduled for ${s.name}','warn')"><i class="bi bi-arrow-clockwise"></i></button>`:'<button class="btn btn-sm btn-success px-2 py-0" style="font-size:11px" onclick="showToast(\'Powering on ${s.name}…\',\'success\')"><i class="bi bi-power"></i></button>'}
        </div>
      </div>
    </div>`).join('');
}

// ═══════════════════════════════════════
//  QUICK ACTIONS FORM
// ═══════════════════════════════════════
function executeAction() {
  const server  = document.getElementById('actionServer').value;
  const action  = document.getElementById('actionType').value;
  const target  = document.getElementById('actionTarget').value.trim();
  const notes   = document.getElementById('actionNotes').value.trim();
  const notify  = document.getElementById('chkNotify').checked;
  const logIt   = document.getElementById('chkLog').checked;

  if(!target) { showToast('<i class="bi bi-exclamation me-2 text-warning"></i>Please specify a target service','warn'); return; }

  const actions = { restart:'Restarting', diag:'Running diagnostics on', cache:'Clearing cache for', backup:'Starting backup of', rotate:'Rotating logs for' };
  const verb = actions[action] || 'Executing action on';

  const resultEl = document.getElementById('actionResult');
  resultEl.style.display='block';
  resultEl.innerHTML=`<div class="d-flex align-items-center gap-2 p-2 rounded-2" style="background:rgba(56,189,248,.08);border:1px solid rgba(56,189,248,.2);font-size:12px;color:#7dd3fc"><i class="bi bi-gear-fill spin"></i><span>${verb} <b>${target}</b> on <b>${server}</b>…</span></div>`;

  if(logIt) addLogLine('INFO','admin',`action=${action} target=${target} server=${server}`);
  if(notify) showToast(`<i class="bi bi-bell me-2"></i>Team notified about ${action} on ${target}`,'info');

  setTimeout(()=>{
    resultEl.innerHTML=`<div class="d-flex align-items-center gap-2 p-2 rounded-2" style="background:rgba(16,185,129,.08);border:1px solid rgba(16,185,129,.2);font-size:12px;color:#34d399"><i class="bi bi-check-circle-fill"></i><span>${verb.replace('ing','ed')} <b>${target}</b> successfully.</span></div>`;
    addLogLine('INFO','admin',`action completed: ${action} on ${target}`);
    showToast(`<i class="bi bi-check-circle me-2 text-success"></i><b>${target}</b> — action completed`,'success');
  }, 2000);
}

function clearForm() {
  document.getElementById('actionTarget').value='';
  document.getElementById('actionNotes').value='';
  document.getElementById('actionResult').style.display='none';
}

// ═══════════════════════════════════════
//  LOG SEARCH
// ═══════════════════════════════════════
function searchLogs() {
  const q   = document.getElementById('logSearch').value.toLowerCase();
  const lv  = document.getElementById('logLevelFilter').value;
  const svc = document.getElementById('logServiceFilter').value;

  let lines = state.logLines;
  if(lv!=='all') lines = lines.filter(l=>l.toUpperCase().includes(lv.toUpperCase()));
  if(svc!=='all') lines = lines.filter(l=>l.includes('['+svc+']'));
  if(q) lines = lines.filter(l=>l.toLowerCase().includes(q));

  document.getElementById('searchResultCount').textContent = lines.length + ' results';
  document.getElementById('searchLogArea').value = lines.join('\n');
}

function downloadSearchResults() {
  const content = document.getElementById('searchLogArea').value;
  if(!content) { showToast('No results to download','warn'); return; }
  const blob = new Blob([content], {type:'text/plain'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'log-search-' + Date.now() + '.txt';
  a.click();
  showToast('<i class="bi bi-download me-2"></i>Results downloaded','success');
}

function resetSearch() {
  document.getElementById('logSearch').value='';
  document.getElementById('logLevelFilter').value='all';
  document.getElementById('logServiceFilter').value='all';
  document.getElementById('searchResultCount').textContent='—';
  document.getElementById('searchLogArea').value='';
}

// ═══════════════════════════════════════
//  SETTINGS
// ═══════════════════════════════════════
function saveSettings() {
  showToast('<i class="bi bi-check-circle me-2 text-success"></i>Settings saved successfully','success');
}

function updateRefreshInterval() {
  const val = parseInt(document.getElementById('refreshInterval').value);
  state.refreshInterval = val;
  clearInterval(state.refreshTimer);
  state.refreshTimer = setInterval(tickLive, state.refreshInterval);
  showToast(`<i class="bi bi-clock me-2"></i>Refresh interval set to ${val/1000}s`,'info');
}

// ═══════════════════════════════════════
//  GLOBAL ACTIONS
// ═══════════════════════════════════════
function refreshAll() {
  updateMetrics(); renderServices(); renderDockerTable(); renderStorage(); renderEvents();
  showToast('<i class="bi bi-arrow-clockwise me-2 text-success"></i>Dashboard refreshed','success');
}

function runDiagnostics() {
  showToast('<i class="bi bi-gear-fill me-2"></i>Running diagnostics…','info');
  ['Checking CPU health…','Checking memory usage…','Testing disk I/O…','Pinging services…','Checking network interfaces…','Diagnostics complete ✓'].forEach((msg,i)=>{
    setTimeout(()=>{
      addLogLine(i===5?'INFO':'INFO','diag',msg);
      if(i===5) showToast('<i class="bi bi-check-circle me-2 text-success"></i>All diagnostics passed','success');
    }, i*800);
  });
}

function exportReport() {
  const report = [
    'ServerPanel Report — ' + new Date().toUTCString(),
    '='.repeat(50),
    `CPU: ${state.cpu}%  RAM: ${state.ram}%  Load: ${state.load}`,
    `Disk /data: ${state.diskData}%  Temp: ${state.temp}°C`,
    `Net In: ${state.netIn} MB/s  Net Out: ${state.netOut} MB/s`,
    '',
    'SERVICES:',
    ...state.services.map(s=>`  ${s.name.padEnd(16)} ${s.status.padEnd(10)} ${s.port}`),
    '',
    'RECENT LOG (last 20 lines):',
    ...state.logLines.slice(0,20)
  ].join('\n');
  const blob = new Blob([report], {type:'text/plain'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'serverpanel-report-' + Date.now() + '.txt';
  a.click();
  showToast('<i class="bi bi-download me-2"></i>Report exported','success');
}

// ═══════════════════════════════════════
//  TOAST
// ═══════════════════════════════════════
function showToast(msg, type='info') {
  const colors = { success:'#34d399', error:'#f87171', warn:'#fbbf24', info:'#38bdf8' };
  const c = document.getElementById('toastContainer');
  const t = document.createElement('div');
  t.className = 'toast-msg';
  t.style.borderLeft = `3px solid ${colors[type]||colors.info}`;
  t.innerHTML = msg;
  c.appendChild(t);
  setTimeout(()=>{ t.classList.add('hide'); setTimeout(()=>t.remove(), 350); }, 3500);
}

// ═══════════════════════════════════════
//  NEWSLETTER
// ═══════════════════════════════════════
function subscribeNewsletter() {
  const email = document.getElementById('newsletterEmail').value;
  if(!email || !email.includes('@')) { showToast('<i class="bi bi-exclamation me-2 text-warning"></i>Please enter a valid email','warn'); return; }
  showToast(`<i class="bi bi-check-circle me-2 text-success"></i>Subscribed! Welcome <b>${email}</b>`,'success');
  document.getElementById('newsletterEmail').value='';
}

// ═══════════════════════════════════════
//  TICK — MAIN LOOP
// ═══════════════════════════════════════
function tickLive() {
  updateMetrics();
  renderDockerTable();
  renderStorage();
  if(Math.random() > 0.3) generateLogLine();
  if(Math.random() > 0.7) addRandomEvent();
  // Occasionally fluctuate a service
  if(Math.random() > 0.97) {
    const running = state.services.filter(s=>s.status==='running'&&s.name!=='cron');
    if(running.length) {
      const svc = running[Math.floor(Math.random()*running.length)];
      svc.status='degraded';
      addLogLine('WARN', svc.name, 'response time elevated, checking…');
      setTimeout(()=>{ svc.status='running'; addLogLine('INFO', svc.name, 'recovered, back to normal'); renderServices(); }, 5000);
    }
  }
  renderServices();
}

// ═══════════════════════════════════════
//  INIT
// ═══════════════════════════════════════
(function init(){
  // seed initial log
  const seedLines = [
    ['INFO','nginx','200 GET /api/health — 3ms'],
    ['INFO','postgres','checkpoint complete: wrote 842 buffers'],
    ['ERROR','redis','service exited unexpectedly (OOM, exit code 1)'],
    ['INFO','nginx','200 GET /dashboard — 12ms'],
    ['INFO','cron','job backup-db completed in 4.2s'],
    ['ERROR','postgres','slow query (1842ms): SELECT * FROM sessions WHERE...'],
    ['WARN','disk','/data usage crossed 85% threshold (now: 86%)'],
    ['INFO','node','worker PID 29441 recycled after 24h uptime'],
    ['INFO','nginx','304 GET /static/main.js — 1ms'],
    ['INFO','node','active connections: 214'],
    ['WARN','cron','maintenance window in 6h'],
    ['INFO','postgres','autovacuum: table public.events'],
    ['INFO','nginx','200 POST /api/data — 28ms'],
    ['INFO','node','cache hit ratio: 94.3%'],
  ];
  seedLines.forEach(([l,s,m])=>addLogLine(l,s,m));

  renderServices();
  renderDockerTable();
  renderStorage();
  renderNetworkTable();
  renderEvents();
  updateAlertBadges();

  // Start live tick
  state.refreshTimer = setInterval(tickLive, state.refreshInterval);

  showToast('<i class="bi bi-check-circle me-2 text-success"></i>Dashboard connected — live data streaming','success');
})();
</script>
</body>
</html>
