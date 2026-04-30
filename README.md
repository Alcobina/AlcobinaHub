<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AlcoBina | Pings Promotion System</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&family=DM+Mono:wght@400;500&family=Syne:wght@600;700;800&display=swap" rel="stylesheet">
<style>
/* ── TOKENS ─────────────────────────────────────────── */
:root{
  --navy:#0B1E45;--navy2:#122259;--blue:#1A4FA0;--blue2:#2563C7;
  --orange:#E8760A;--orange2:#FF8C1A;--amber:#FFC107;
  --green:#0A7A45;--green-lt:#D4F5E4;
  --red:#C0241E;--red-lt:#FCE8E7;
  --sky:#EBF2FF;--sky2:#C8DCFF;
  --gray0:#F8F9FC;--gray1:#EEF1F8;--gray2:#D8DDEF;
  --gray3:#9AA3BB;--gray4:#5A6380;--gray5:#2C3350;
  --white:#FFFFFF;
  --font-head:'Syne',sans-serif;
  --font-body:'DM Sans',sans-serif;
  --font-mono:'DM Mono',monospace;
  --shadow-sm:0 1px 4px rgba(11,30,69,.08);
  --shadow-md:0 4px 18px rgba(11,30,69,.12);
  --shadow-lg:0 12px 40px rgba(11,30,69,.18);
  --radius:12px;--radius-sm:8px;
  --transition:.18s cubic-bezier(.4,0,.2,1);
}
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
body{font-family:var(--font-body);background:var(--gray0);color:var(--gray5);font-size:15px;line-height:1.55}

/* ── SCROLLBAR ── */
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:var(--gray1)}
::-webkit-scrollbar-thumb{background:var(--gray2);border-radius:3px}

/* ── APP SHELL ── */
.app{display:flex;min-height:100vh}

/* ── SIDEBAR ── */
.sidebar{width:240px;background:var(--navy);display:flex;flex-direction:column;
  position:fixed;top:0;left:0;bottom:0;z-index:100;transition:transform var(--transition)}
.sidebar-logo{padding:24px 20px 18px;border-bottom:1px solid rgba(255,255,255,.08)}
.logo-mark{display:flex;align-items:center;gap:10px}
.logo-icon{width:36px;height:36px;background:var(--orange);border-radius:9px;
  display:grid;place-items:center;font-family:var(--font-head);font-size:14px;font-weight:800;color:#fff}
.logo-txt{font-family:var(--font-head);font-size:15px;font-weight:700;color:#fff;line-height:1.2}
.logo-txt small{display:block;font-size:10px;font-weight:400;color:rgba(255,255,255,.45);
  letter-spacing:.8px;text-transform:uppercase;font-family:var(--font-body);margin-top:1px}
.sidebar-nav{padding:16px 12px;flex:1;overflow-y:auto}
.nav-group{margin-bottom:20px}
.nav-group-label{font-size:9.5px;font-weight:600;letter-spacing:1.5px;text-transform:uppercase;
  color:rgba(255,255,255,.35);padding:0 8px;margin-bottom:6px}
.nav-item{display:flex;align-items:center;gap:10px;padding:9px 10px;
  border-radius:var(--radius-sm);cursor:pointer;color:rgba(255,255,255,.6);
  font-size:13.5px;font-weight:500;transition:all var(--transition);margin-bottom:2px}
.nav-item:hover{background:rgba(255,255,255,.07);color:#fff}
.nav-item.active{background:rgba(232,118,10,.18);color:var(--orange2);border:1px solid rgba(232,118,10,.25)}
.nav-item .ni{font-size:16px;width:20px;text-align:center;flex-shrink:0}
.nav-badge{margin-left:auto;background:var(--orange);color:#fff;
  font-size:10px;font-weight:700;border-radius:100px;padding:1px 7px;font-family:var(--font-mono)}

.sidebar-footer{padding:14px 16px;border-top:1px solid rgba(255,255,255,.08)}
.sf-time{font-family:var(--font-mono);font-size:11px;color:rgba(255,255,255,.35);text-align:center}
.sf-time #live-clock{color:var(--orange2)}

/* ── MAIN CONTENT ── */
.main{margin-left:240px;flex:1;display:flex;flex-direction:column;min-height:100vh}

/* ── TOP BAR ── */
.topbar{background:#fff;border-bottom:1px solid var(--gray2);padding:14px 28px;
  display:flex;justify-content:space-between;align-items:center;
  position:sticky;top:0;z-index:50;box-shadow:var(--shadow-sm)}
.topbar-title{font-family:var(--font-head);font-size:17px;font-weight:700;color:var(--navy)}
.topbar-title span{color:var(--orange)}
.topbar-meta{display:flex;align-items:center;gap:14px}
.tb-tag{background:var(--sky);color:var(--blue2);font-size:11.5px;font-weight:600;
  border-radius:100px;padding:4px 12px;letter-spacing:.3px}
.tb-tag.orange{background:#FFF3E0;color:var(--orange)}
.topbar-actions{display:flex;gap:8px}

/* ── PAGE VIEWS ── */
.page{display:none;padding:28px;animation:fadeIn .3s ease}
.page.active{display:block}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}

/* ── FORM PAGE ── */
.form-header{background:linear-gradient(135deg,var(--navy) 0%,var(--navy2) 60%,#1A3A7A 100%);
  border-radius:var(--radius);padding:28px 32px;margin-bottom:24px;position:relative;overflow:hidden}
.form-header::before{content:'';position:absolute;right:-40px;top:-40px;
  width:200px;height:200px;border-radius:50%;background:rgba(232,118,10,.12)}
.form-header::after{content:'';position:absolute;right:60px;bottom:-60px;
  width:140px;height:140px;border-radius:50%;background:rgba(37,99,199,.2)}
.fh-top{display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:12px;position:relative;z-index:1}
.fh-brand{display:flex;align-items:center;gap:12px}
.fh-icon{width:48px;height:48px;background:var(--orange);border-radius:12px;
  display:grid;place-items:center;font-family:var(--font-head);font-size:18px;font-weight:800;color:#fff;
  box-shadow:0 4px 16px rgba(232,118,10,.4)}
.fh-txt h2{font-family:var(--font-head);font-size:20px;font-weight:700;color:#fff}
.fh-txt p{font-size:12px;color:rgba(255,255,255,.55);margin-top:2px}
.fh-ts{text-align:right;position:relative;z-index:1}
.fh-ts .ts-label{font-size:10px;letter-spacing:1.5px;text-transform:uppercase;
  color:rgba(255,255,255,.4);margin-bottom:4px}
.fh-ts .ts-val{font-family:var(--font-mono);font-size:12px;color:var(--orange2);font-weight:500}
.fh-ts .ts-uid{font-family:var(--font-mono);font-size:10px;color:rgba(255,255,255,.35);margin-top:2px}

/* ── SECTION CARDS ── */
.form-section{background:#fff;border-radius:var(--radius);margin-bottom:18px;
  box-shadow:var(--shadow-sm);overflow:hidden;border:1px solid var(--gray2)}
.fs-head{display:flex;align-items:center;gap:12px;padding:16px 22px;
  border-bottom:1px solid var(--gray1);background:var(--gray0)}
.fs-num{width:28px;height:28px;background:var(--navy);color:#fff;border-radius:50%;
  display:grid;place-items:center;font-size:12px;font-weight:700;flex-shrink:0;font-family:var(--font-mono)}
.fs-title{font-family:var(--font-head);font-size:15px;font-weight:700;color:var(--navy)}
.fs-desc{font-size:12px;color:var(--gray3);margin-top:1px}
.fs-icon{margin-left:auto;font-size:20px}
.fs-body{padding:20px 22px}

/* ── FORM GRID ── */
.fg{display:grid;gap:14px}
.fg-2{grid-template-columns:repeat(2,1fr)}
.fg-3{grid-template-columns:repeat(3,1fr)}
.fg-4{grid-template-columns:repeat(4,1fr)}
@media(max-width:900px){.fg-4,.fg-3{grid-template-columns:repeat(2,1fr)}.fg-2{grid-template-columns:1fr}}

.field{display:flex;flex-direction:column;gap:5px}
.field label{font-size:12px;font-weight:600;color:var(--gray4);letter-spacing:.3px;text-transform:uppercase}
.field input,.field select,.field textarea{
  border:1.5px solid var(--gray2);border-radius:var(--radius-sm);
  padding:9px 13px;font-family:var(--font-body);font-size:14px;color:var(--gray5);
  background:#fff;transition:border-color var(--transition),box-shadow var(--transition);outline:none}
.field input:focus,.field select:focus,.field textarea:focus{
  border-color:var(--blue2);box-shadow:0 0 0 3px rgba(37,99,199,.1)}
.field textarea{resize:vertical;min-height:80px}
.field-hint{font-size:11px;color:var(--gray3);margin-top:2px}
.field-required::after{content:' *';color:var(--red)}
.field input[readonly]{background:var(--gray0);color:var(--gray3);cursor:default}

/* ── SKU TABLE ── */
.sku-table-wrap{overflow-x:auto;border-radius:var(--radius-sm);border:1px solid var(--gray2)}
table.sku-table{width:100%;border-collapse:collapse;min-width:900px;font-size:13px}
table.sku-table th{background:var(--navy);color:#fff;padding:10px 12px;
  font-weight:600;font-size:11px;letter-spacing:.6px;text-transform:uppercase;
  text-align:center;font-family:var(--font-mono)}
table.sku-table th:first-child{text-align:left;border-radius:0}
table.sku-table td{padding:8px 10px;border-bottom:1px solid var(--gray1);vertical-align:middle;text-align:center}
table.sku-table td:first-child{text-align:left;font-weight:600;color:var(--gray5)}
table.sku-table tbody tr:hover{background:var(--sky)}
table.sku-table tbody tr:last-child td{border-bottom:none}
table.sku-table input[type="number"]{
  width:80px;border:1.5px solid var(--gray2);border-radius:6px;
  padding:5px 8px;text-align:center;font-family:var(--font-mono);font-size:13px;
  color:var(--gray5);background:#fff;outline:none}
table.sku-table input[type="number"]:focus{border-color:var(--blue2);background:var(--sky)}
.sku-total{font-family:var(--font-mono);font-weight:700;color:var(--green);font-size:14px}
.sku-total-row td{background:var(--sky);font-weight:700;color:var(--navy);font-size:13px;border-top:2px solid var(--navy)}
.sku-uom{font-size:11px;color:var(--gray3);font-family:var(--font-mono)}

/* ── DAY TABS ── */
.day-tabs{display:flex;gap:6px;margin-bottom:16px;flex-wrap:wrap}
.day-tab{padding:8px 18px;border-radius:100px;font-size:13px;font-weight:600;
  cursor:pointer;border:1.5px solid var(--gray2);color:var(--gray4);
  background:#fff;transition:all var(--transition)}
.day-tab:hover{border-color:var(--blue2);color:var(--blue2)}
.day-tab.active{background:var(--navy);border-color:var(--navy);color:#fff}
.day-content{display:none}.day-content.active{display:block}

/* ── COMP TABLE ── */
table.comp-table{width:100%;border-collapse:collapse;font-size:13px}
table.comp-table th{background:var(--orange);color:#fff;padding:9px 12px;font-size:11px;font-weight:700;text-align:left;letter-spacing:.5px;text-transform:uppercase}
table.comp-table td{padding:8px 10px;border-bottom:1px solid var(--gray1)}
table.comp-table tbody tr:hover{background:#FFF8F0}
table.comp-table input,table.comp-table select{
  border:1px solid var(--gray2);border-radius:6px;padding:5px 8px;
  font-family:var(--font-body);font-size:12.5px;color:var(--gray5);width:100%;outline:none}
table.comp-table input:focus,table.comp-table select:focus{border-color:var(--orange)}
.add-row-btn{display:flex;align-items:center;gap:6px;padding:7px 14px;
  border:1.5px dashed var(--gray2);border-radius:var(--radius-sm);
  background:none;cursor:pointer;color:var(--gray3);font-size:13px;
  font-family:var(--font-body);margin-top:8px;transition:all var(--transition)}
.add-row-btn:hover{border-color:var(--orange);color:var(--orange);background:#FFF8F0}

/* ── BUTTONS ── */
.btn{display:inline-flex;align-items:center;gap:7px;padding:11px 22px;
  border-radius:var(--radius-sm);font-family:var(--font-body);font-size:14px;
  font-weight:600;cursor:pointer;border:none;transition:all var(--transition)}
.btn-primary{background:var(--navy);color:#fff}
.btn-primary:hover{background:var(--blue);box-shadow:var(--shadow-md)}
.btn-orange{background:var(--orange);color:#fff}
.btn-orange:hover{background:var(--orange2);box-shadow:0 4px 16px rgba(232,118,10,.35)}
.btn-outline{background:none;border:1.5px solid var(--gray2);color:var(--gray4)}
.btn-outline:hover{border-color:var(--navy);color:var(--navy)}
.btn-green{background:var(--green);color:#fff}
.btn-green:hover{background:#0B9655;box-shadow:0 4px 16px rgba(10,122,69,.3)}
.btn-sm{padding:7px 14px;font-size:12.5px}

/* ── TOAST ── */
.toast{position:fixed;bottom:28px;right:28px;padding:14px 20px;
  border-radius:var(--radius);background:var(--green);color:#fff;font-weight:600;
  font-size:14px;box-shadow:var(--shadow-lg);z-index:9999;display:none;
  animation:slideUp .3s ease}
@keyframes slideUp{from{transform:translateY(20px);opacity:0}to{transform:translateY(0);opacity:1}}

/* ── DASHBOARD ── */
.dash-stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:16px;margin-bottom:24px}
.stat-card{background:#fff;border-radius:var(--radius);padding:20px;
  box-shadow:var(--shadow-sm);border:1px solid var(--gray2);position:relative;overflow:hidden}
.stat-card::before{content:'';position:absolute;top:0;left:0;right:0;height:3px}
.stat-card.blue::before{background:var(--blue2)}
.stat-card.orange::before{background:var(--orange)}
.stat-card.green::before{background:var(--green)}
.stat-card.red::before{background:var(--red)}
.stat-card.navy::before{background:var(--navy)}
.sc-icon{font-size:24px;margin-bottom:8px}
.sc-val{font-family:var(--font-head);font-size:28px;font-weight:800;color:var(--navy);line-height:1}
.sc-label{font-size:12px;color:var(--gray3);margin-top:4px;font-weight:500}
.sc-delta{font-size:11.5px;font-weight:700;margin-top:6px}
.sc-delta.up{color:var(--green)}.sc-delta.dn{color:var(--red)}

/* ── CHART PLACEHOLDER ── */
.chart-grid{display:grid;grid-template-columns:2fr 1fr;gap:16px;margin-bottom:24px}
@media(max-width:900px){.chart-grid{grid-template-columns:1fr}}
.chart-card{background:#fff;border-radius:var(--radius);padding:20px;
  box-shadow:var(--shadow-sm);border:1px solid var(--gray2)}
.chart-title{font-family:var(--font-head);font-size:14px;font-weight:700;color:var(--navy);margin-bottom:16px;
  display:flex;justify-content:space-between;align-items:center}
.chart-title span{font-size:11px;color:var(--gray3);font-weight:400;font-family:var(--font-body)}
.bar-chart{display:flex;align-items:flex-end;gap:8px;height:160px;padding-top:10px}
.bar-group{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px}
.bar{width:100%;background:var(--blue2);border-radius:4px 4px 0 0;transition:height .5s ease;
  position:relative;min-height:4px;cursor:pointer}
.bar:hover::after{content:attr(data-val);position:absolute;top:-28px;left:50%;transform:translateX(-50%);
  background:var(--navy);color:#fff;padding:3px 8px;border-radius:4px;font-size:11px;font-family:var(--font-mono);white-space:nowrap}
.bar.orange{background:var(--orange)}
.bar-lbl{font-size:10px;color:var(--gray3);text-align:center;font-weight:500}
.bar-val{font-size:11px;font-weight:700;color:var(--navy);font-family:var(--font-mono)}

/* Donut chart */
.donut-wrap{display:flex;flex-direction:column;align-items:center;gap:12px}
.donut-svg{width:140px;height:140px}
.donut-legend{width:100%}
.dl-item{display:flex;align-items:center;gap:8px;padding:4px 0;font-size:12px}
.dl-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}
.dl-name{flex:1;color:var(--gray4)}
.dl-val{font-family:var(--font-mono);font-weight:700;color:var(--navy)}

/* ── REPORTS TABLE ── */
.reports-table-wrap{background:#fff;border-radius:var(--radius);border:1px solid var(--gray2);
  overflow:hidden;box-shadow:var(--shadow-sm)}
.rt-head{display:flex;justify-content:space-between;align-items:center;
  padding:16px 22px;border-bottom:1px solid var(--gray1);background:var(--gray0)}
.rt-head h3{font-family:var(--font-head);font-size:15px;font-weight:700;color:var(--navy)}
table.rt{width:100%;border-collapse:collapse;font-size:13px}
table.rt th{background:var(--navy);color:#fff;padding:10px 14px;font-size:10.5px;
  font-weight:600;letter-spacing:.6px;text-transform:uppercase;text-align:left}
table.rt td{padding:11px 14px;border-bottom:1px solid var(--gray1);vertical-align:middle}
table.rt tbody tr:hover{background:var(--sky)}
table.rt tbody tr:last-child td{border-bottom:none}
.status-badge{display:inline-flex;align-items:center;gap:4px;padding:3px 10px;
  border-radius:100px;font-size:11px;font-weight:700}
.sb-green{background:var(--green-lt);color:var(--green)}
.sb-orange{background:#FFF3E0;color:var(--orange)}
.sb-red{background:var(--red-lt);color:var(--red)}
.sb-gray{background:var(--gray1);color:var(--gray4)}
.progress-bar{height:6px;background:var(--gray1);border-radius:3px;overflow:hidden}
.pb-fill{height:100%;border-radius:3px;transition:width .5s ease}

/* ── LEADERBOARD ── */
.lb-wrap{background:#fff;border-radius:var(--radius);border:1px solid var(--gray2);
  overflow:hidden;box-shadow:var(--shadow-sm)}
.lb-item{display:flex;align-items:center;gap:14px;padding:14px 20px;
  border-bottom:1px solid var(--gray1);transition:background var(--transition)}
.lb-item:hover{background:var(--sky)}
.lb-item:last-child{border-bottom:none}
.lb-rank{font-family:var(--font-head);font-size:18px;font-weight:800;color:var(--gray2);width:28px;flex-shrink:0}
.lb-rank.r1{color:var(--amber)}.lb-rank.r2{color:var(--gray3)}.lb-rank.r3{color:var(--orange)}
.lb-avatar{width:36px;height:36px;border-radius:50%;background:var(--navy);
  display:grid;place-items:center;color:#fff;font-weight:700;font-size:13px;flex-shrink:0}
.lb-info{flex:1}
.lb-name{font-weight:700;font-size:14px;color:var(--gray5)}
.lb-sub{font-size:11.5px;color:var(--gray3);margin-top:1px}
.lb-score{font-family:var(--font-head);font-size:18px;font-weight:800;color:var(--navy)}
.lb-delta{font-size:11px;color:var(--green);font-weight:700}

/* ── FILTER BAR ── */
.filter-bar{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;padding:14px 20px;
  background:#fff;border-radius:var(--radius);border:1px solid var(--gray2);box-shadow:var(--shadow-sm)}
.filter-bar input,.filter-bar select{
  border:1.5px solid var(--gray2);border-radius:var(--radius-sm);padding:8px 12px;
  font-family:var(--font-body);font-size:13px;color:var(--gray5);background:#fff;outline:none;
  transition:border-color var(--transition)}
.filter-bar input:focus,.filter-bar select:focus{border-color:var(--blue2)}
.filter-bar label{font-size:11.5px;font-weight:600;color:var(--gray4);
  display:flex;flex-direction:column;gap:4px}

/* ── MODAL PREVIEW ── */
.modal-overlay{display:none;position:fixed;inset:0;background:rgba(11,30,69,.5);
  z-index:200;justify-content:center;align-items:flex-start;padding:40px 20px;overflow-y:auto}
.modal-overlay.open{display:flex}
.modal{background:#fff;border-radius:var(--radius);max-width:720px;width:100%;
  box-shadow:var(--shadow-lg);animation:fadeIn .25s ease}
.modal-head{display:flex;justify-content:space-between;align-items:center;
  padding:18px 24px;border-bottom:1px solid var(--gray1);background:var(--gray0)}
.modal-head h3{font-family:var(--font-head);font-size:16px;font-weight:700;color:var(--navy)}
.modal-close{background:none;border:none;cursor:pointer;font-size:20px;color:var(--gray3);
  line-height:1;transition:color var(--transition)}
.modal-close:hover{color:var(--red)}
.modal-body{padding:24px}

/* ── ANALYTICS DETAIL ── */
.analytics-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:16px;margin-bottom:24px}
.perf-card{background:#fff;border-radius:var(--radius);padding:20px;
  box-shadow:var(--shadow-sm);border:1px solid var(--gray2)}
.perf-title{font-family:var(--font-head);font-size:13px;font-weight:700;color:var(--navy);margin-bottom:14px;
  text-transform:uppercase;letter-spacing:.5px}
.metric-row{display:flex;justify-content:space-between;align-items:center;
  padding:8px 0;border-bottom:1px solid var(--gray1)}
.metric-row:last-child{border-bottom:none}
.mr-label{font-size:13px;color:var(--gray4)}
.mr-val{font-family:var(--font-mono);font-size:14px;font-weight:700;color:var(--navy)}
.mr-bar{height:4px;background:var(--gray1);border-radius:2px;margin-top:4px;overflow:hidden}
.mrb-fill{height:100%;border-radius:2px;background:var(--blue2)}

/* ── RESPONSIVE ── */
@media(max-width:768px){
  .sidebar{transform:translateX(-100%)}
  .sidebar.open{transform:translateX(0)}
  .main{margin-left:0}
  .page{padding:16px}
  .fh-top{flex-direction:column}
  .chart-grid{grid-template-columns:1fr}
  .dash-stats{grid-template-columns:1fr 1fr}
}

.section-divider{height:1px;background:linear-gradient(90deg,var(--orange),transparent);
  margin:8px 0 20px;border:none}

.info-box{background:var(--sky);border:1px solid var(--sky2);border-radius:var(--radius-sm);
  padding:12px 16px;font-size:13px;color:var(--blue);margin-top:8px;
  display:flex;gap:10px;align-items:flex-start}
.warn-box{background:#FFF8F0;border:1px solid #FFDCB0;border-radius:var(--radius-sm);
  padding:12px 16px;font-size:13px;color:var(--orange);margin-top:8px;
  display:flex;gap:10px;align-items:flex-start}

.print-btn{display:none}
@media print{
  .sidebar,.topbar,.print-btn,.btn-orange,.btn-primary,.btn-outline,
  .day-tabs,.add-row-btn,.form-actions-bar{display:none!important}
  .main{margin-left:0}
  .page{padding:10px}
  .print-btn{display:inline-flex}
  .form-section{break-inside:avoid}
}
</style>
</head>
<body>

<!-- ════════════════════════════════════════════════ -->
<!-- SIDEBAR -->
<!-- ════════════════════════════════════════════════ -->
<nav class="sidebar" id="sidebar">
  <div class="sidebar-logo">
    <div class="logo-mark">
      <div class="logo-icon">AB</div>
      <div class="logo-txt">AlcoBina<small>Promotion System</small></div>
    </div>
  </div>
  <div class="sidebar-nav">
    <div class="nav-group">
      <div class="nav-group-label">Promoter</div>
      <div class="nav-item active" onclick="showPage('form')">
        <span class="ni">📋</span>Promotion Form
        <span class="nav-badge" id="nb-form">1</span>
      </div>
      <div class="nav-item" onclick="showPage('preview')">
        <span class="ni">👁</span>My Submissions
      </div>
    </div>
    <div class="nav-group">
      <div class="nav-group-label">Management</div>
      <div class="nav-item" onclick="showPage('dashboard')">
        <span class="ni">📊</span>Dashboard
      </div>
      <div class="nav-item" onclick="showPage('analytics')">
        <span class="ni">📈</span>Analytics
      </div>
      <div class="nav-item" onclick="showPage('leaderboard')">
        <span class="ni">🏆</span>Performance
      </div>
      <div class="nav-item" onclick="showPage('reports')">
        <span class="ni">📁</span>All Reports
      </div>
    </div>
    <div class="nav-group">
      <div class="nav-group-label">System</div>
      <div class="nav-item" onclick="showPage('settings')">
        <span class="ni">⚙️</span>Settings
      </div>
    </div>
  </div>
  <div class="sidebar-footer">
    <div class="sf-time">Live: <span id="live-clock">--:--:--</span></div>
  </div>
</nav>

<!-- ════════════════════════════════════════════════ -->
<!-- MAIN -->
<!-- ════════════════════════════════════════════════ -->
<div class="main">

  <!-- TOPBAR -->
  <div class="topbar">
    <div class="topbar-title">AlcoBina <span>× Pings</span> Promotion System</div>
    <div class="topbar-meta">
      <span class="tb-tag" id="top-date">Loading…</span>
      <span class="tb-tag orange" id="top-submissions">0 Submissions Today</span>
    </div>
    <div class="topbar-actions">
      <button class="btn btn-outline btn-sm" onclick="clearForm()">🔄 New Form</button>
      <button class="btn btn-orange btn-sm" onclick="showPage('dashboard')">📊 Dashboard</button>
    </div>
  </div>

  <!-- ══════════════════════════════════════════════ -->
  <!-- PAGE: PROMOTION FORM -->
  <!-- ══════════════════════════════════════════════ -->
  <div class="page active" id="page-form">

    <!-- Header -->
    <div class="form-header">
      <div class="fh-top">
        <div class="fh-brand">
          <div class="fh-icon">📋</div>
          <div class="fh-txt">
            <h2>In-Store Promotion Report</h2>
            <p>Pings Manufacturing Limited — FMCG Activation Form</p>
          </div>
        </div>
        <div class="fh-ts">
          <div class="ts-label">Timestamp</div>
          <div class="ts-val" id="form-timestamp">Loading…</div>
          <div class="ts-uid" id="form-uid">Form ID: —</div>
        </div>
      </div>
    </div>

    <!-- §1 — PROMOTION DETAILS -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">1</div>
        <div>
          <div class="fs-title">Promotion Details</div>
          <div class="fs-desc">General information about this activation</div>
        </div>
        <div class="fs-icon">📌</div>
      </div>
      <div class="fs-body">
        <div class="fg fg-3">
          <div class="field">
            <label class="field-required">Promoter Name</label>
            <input type="text" id="promoter-name" placeholder="Full name" required>
          </div>
          <div class="field">
            <label class="field-required">Promoter ID / Code</label>
            <input type="text" id="promoter-id" placeholder="e.g. PMS-001">
          </div>
          <div class="field">
            <label>Supervisor Name</label>
            <input type="text" id="supervisor-name" placeholder="Direct supervisor">
          </div>
        </div>
        <div class="fg fg-3" style="margin-top:14px">
          <div class="field">
            <label class="field-required">Promotion Start Date</label>
            <input type="date" id="promo-start" onchange="updateDayTabs()">
          </div>
          <div class="field">
            <label class="field-required">Promotion End Date</label>
            <input type="date" id="promo-end" onchange="updateDayTabs()">
          </div>
          <div class="field">
            <label>No. of Promotion Days</label>
            <input type="number" id="promo-days" readonly placeholder="Auto-calculated">
          </div>
        </div>
        <div class="fg fg-2" style="margin-top:14px">
          <div class="field">
            <label class="field-required">Check-In Timestamp</label>
            <input type="text" id="checkin-time" readonly>
          </div>
          <div class="field">
            <label>GPS / Location Tag</label>
            <input type="text" id="gps-location" placeholder="Fetching location…" readonly>
          </div>
        </div>
      </div>
    </div>

    <!-- §2 — CUSTOMER / STORE DETAILS -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">2</div>
        <div>
          <div class="fs-title">Customer / Store Information</div>
          <div class="fs-desc">Where the promotion is being conducted</div>
        </div>
        <div class="fs-icon">🏪</div>
      </div>
      <div class="fs-body">
        <div class="fg fg-2">
          <div class="field">
            <label class="field-required">Customer / Store Name</label>
            <input type="text" id="customer-name" placeholder="Store or wholesale name">
          </div>
          <div class="field">
            <label>Contact Person at Store</label>
            <input type="text" id="store-contact" placeholder="Store manager/owner name">
          </div>
        </div>
        <div class="fg fg-3" style="margin-top:14px">
          <div class="field">
            <label class="field-required">Store Address</label>
            <input type="text" id="store-address" placeholder="Full address">
          </div>
          <div class="field">
            <label class="field-required">Parish</label>
            <select id="store-parish">
              <option value="">Select parish…</option>
              <option>Kingston & St. Andrew</option>
              <option>St. Catherine</option>
              <option>Clarendon</option>
              <option>Manchester</option>
              <option>St. Elizabeth</option>
              <option>St. James</option>
              <option>Hanover</option>
              <option>Westmoreland</option>
              <option>St. Mary</option>
              <option>St. Ann</option>
              <option>Trelawny</option>
              <option>Portland</option>
              <option>St. Thomas</option>
            </select>
          </div>
          <div class="field">
            <label>Store Type</label>
            <select id="store-type">
              <option value="">Select type…</option>
              <option>Supermarket</option>
              <option>Wholesale</option>
              <option>Variety / Convenience</option>
              <option>Pharmacy / Health Store</option>
              <option>Hardware / General Store</option>
              <option>Mini Mart</option>
              <option>Other</option>
            </select>
          </div>
        </div>
        <div class="fg fg-3" style="margin-top:14px">
          <div class="field">
            <label>Store Phone</label>
            <input type="tel" id="store-phone" placeholder="Store contact number">
          </div>
          <div class="field">
            <label>Store Email</label>
            <input type="email" id="store-email" placeholder="Store email (if available)">
          </div>
          <div class="field">
            <label>Activation Type</label>
            <select id="activation-type">
              <option value="">Select…</option>
              <option>Dry Push</option>
              <option>Consumer Deal Promotion</option>
              <option>Dry Push + Consumer Deal</option>
              <option>Sampling Activation</option>
              <option>Shelf Merchandising</option>
              <option>POSM Placement</option>
              <option>Full Brand Activation</option>
            </select>
          </div>
        </div>
      </div>
    </div>

    <!-- §3 — OPENING INVENTORY -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">3</div>
        <div>
          <div class="fs-title">Opening Inventory by SKU</div>
          <div class="fs-desc">Record stock available at the start of the promotion</div>
        </div>
        <div class="fs-icon">📦</div>
      </div>
      <div class="fs-body">
        <div class="info-box">ℹ️ Count and record all Pings product inventory present in-store at the start of Day 1. This establishes your baseline for sell-through calculations.</div>
        <div style="margin-top:16px" class="sku-table-wrap">
          <table class="sku-table" id="inventory-table">
            <thead>
              <tr>
                <th style="width:220px">Product / SKU</th>
                <th>Unit of Measure</th>
                <th>Units per Case</th>
                <th>Opening Cases</th>
                <th>Opening Units</th>
                <th>Unit Price (J$)</th>
                <th>Opening Value (J$)</th>
                <th>Shelf Location</th>
              </tr>
            </thead>
            <tbody id="inv-tbody">
              <!-- populated by JS -->
            </tbody>
            <tfoot>
              <tr class="sku-total-row">
                <td colspan="4"><strong>TOTAL OPENING</strong></td>
                <td><span class="sku-total" id="total-opening-units">0</span></td>
                <td>—</td>
                <td><span class="sku-total" id="total-opening-value">J$0</span></td>
                <td>—</td>
              </tr>
            </tfoot>
          </table>
        </div>
      </div>
    </div>

    <!-- §4 — DAILY SALES -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">4</div>
        <div>
          <div class="fs-title">Daily Sales by SKU</div>
          <div class="fs-desc">Record units sold by the promoter each day</div>
        </div>
        <div class="fs-icon">📊</div>
      </div>
      <div class="fs-body">
        <div class="day-tabs" id="day-tabs">
          <button class="day-tab active" onclick="switchDay(0)" id="dtab-0">Day 1</button>
          <button class="day-tab" onclick="switchDay(1)" id="dtab-1">Day 2</button>
        </div>
        <div id="day-panels">
          <!-- populated by JS -->
        </div>
        <!-- Totals Summary -->
        <div style="margin-top:20px">
          <div style="font-family:var(--font-head);font-size:14px;font-weight:700;color:var(--navy);margin-bottom:10px">📊 Cumulative Sales Summary</div>
          <div class="sku-table-wrap">
            <table class="sku-table" id="summary-table">
              <thead>
                <tr>
                  <th style="width:200px">Product / SKU</th>
                  <th id="sum-d1h">Day 1</th>
                  <th id="sum-d2h">Day 2</th>
                  <th>Total Units Sold</th>
                  <th>Opening Units</th>
                  <th>Sell-Through %</th>
                  <th>Closing Stock</th>
                </tr>
              </thead>
              <tbody id="summary-tbody"></tbody>
              <tfoot>
                <tr class="sku-total-row">
                  <td><strong>GRAND TOTAL</strong></td>
                  <td><span class="sku-total" id="gt-d1">0</span></td>
                  <td><span class="sku-total" id="gt-d2">0</span></td>
                  <td><span class="sku-total" id="gt-total">0</span></td>
                  <td><span class="sku-total" id="gt-opening">0</span></td>
                  <td><span class="sku-total" id="gt-pct">0%</span></td>
                  <td><span class="sku-total" id="gt-closing">0</span></td>
                </tr>
              </tfoot>
            </table>
          </div>
        </div>
      </div>
    </div>

    <!-- §5 — COMPETITION DAILY LOG -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">5</div>
        <div>
          <div class="fs-title">Competition Activity Log</div>
          <div class="fs-desc">Record competitor promotions and activities observed each day</div>
        </div>
        <div class="fs-icon">🔍</div>
      </div>
      <div class="fs-body">
        <div class="warn-box">⚠️ Record ALL competitor activity observed — promotions, pricing, shelf placements, staff presence, BOGO deals, and POP materials. This intelligence is critical for management.</div>
        <div style="margin-top:16px;overflow-x:auto">
          <table class="comp-table" id="comp-table">
            <thead>
              <tr>
                <th style="width:70px">Day</th>
                <th style="width:140px">Competitor Brand</th>
                <th style="width:130px">Activity Type</th>
                <th style="width:160px">Product / SKU Affected</th>
                <th style="width:100px">Price Observed</th>
                <th>Details / Notes</th>
                <th style="width:80px">Threat Level</th>
                <th style="width:40px"></th>
              </tr>
            </thead>
            <tbody id="comp-tbody">
              <tr>
                <td><select name="comp-day" style="width:55px"><option>Day 1</option><option>Day 2</option></select></td>
                <td><input type="text" placeholder="Brand name"></td>
                <td><select><option value="">Type…</option><option>BOGO</option><option>Price Reduction</option><option>Sampling</option><option>Paid Shelf</option><option>Poster Campaign</option><option>Promoter Present</option><option>Price Tag Removal</option><option>Other</option></select></td>
                <td><input type="text" placeholder="Product/SKU"></td>
                <td><input type="text" placeholder="e.g. J$250/unit"></td>
                <td><input type="text" placeholder="Describe the activity in detail…"></td>
                <td><select><option value="">—</option><option>🟢 Low</option><option>🟡 Medium</option><option>🔴 High</option><option>🚨 Critical</option></select></td>
                <td><button type="button" onclick="removeRow(this)" style="border:none;background:none;color:var(--red);cursor:pointer;font-size:16px">✕</button></td>
              </tr>
            </tbody>
          </table>
          <button type="button" class="add-row-btn" onclick="addCompRow()">+ Add Competitor Entry</button>
        </div>
      </div>
    </div>

    <!-- §6 — REORDER RECOMMENDATION -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">6</div>
        <div>
          <div class="fs-title">Reorder Recommendations</div>
          <div class="fs-desc">Recommended stock replenishment for the store after the promotion</div>
        </div>
        <div class="fs-icon">🔄</div>
      </div>
      <div class="fs-body">
        <div class="sku-table-wrap">
          <table class="sku-table">
            <thead>
              <tr>
                <th style="width:200px">Product / SKU</th>
                <th>Closing Stock (Units)</th>
                <th>Recommended Reorder (Cases)</th>
                <th>Reorder Urgency</th>
                <th>Reason / Notes</th>
              </tr>
            </thead>
            <tbody id="reorder-tbody">
              <!-- populated by JS -->
            </tbody>
          </table>
        </div>
        <div class="fg fg-2" style="margin-top:16px">
          <div class="field">
            <label>Suggested Reorder Date</label>
            <input type="date" id="reorder-date">
          </div>
          <div class="field">
            <label>Preferred Delivery Window</label>
            <select id="delivery-window">
              <option>Within 24 hours</option>
              <option>Within 48 hours</option>
              <option>Within 3 days</option>
              <option>Within 1 week</option>
              <option>No urgency</option>
            </select>
          </div>
        </div>
      </div>
    </div>

    <!-- §7 — SHELF & MERCHANDISING -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">7</div>
        <div>
          <div class="fs-title">Shelf & Merchandising Assessment</div>
          <div class="fs-desc">Evaluate in-store presence and brand visibility</div>
        </div>
        <div class="fs-icon">🏷</div>
      </div>
      <div class="fs-body">
        <div class="fg fg-3">
          <div class="field">
            <label>Shelf Position Quality</label>
            <select id="shelf-position">
              <option>Excellent — Eye level, primary aisle</option>
              <option>Good — Visible, secondary position</option>
              <option>Fair — Low shelf, limited visibility</option>
              <option>Poor — Hidden / no display</option>
            </select>
          </div>
          <div class="field">
            <label>POP Materials Present?</label>
            <select id="pop-materials">
              <option>Yes — Full POP suite in place</option>
              <option>Yes — Partial (some materials)</option>
              <option>No — None present</option>
              <option>Damaged / needs replacement</option>
            </select>
          </div>
          <div class="field">
            <label>Price Tags Visible?</label>
            <select id="price-tags">
              <option>Yes — All products priced</option>
              <option>Partial — Some missing</option>
              <option>No — None visible</option>
              <option>Competitor tags present on Pings stock</option>
            </select>
          </div>
        </div>
        <div class="fg fg-3" style="margin-top:14px">
          <div class="field">
            <label>Planogram Compliance</label>
            <select id="planogram">
              <option>Fully compliant</option>
              <option>Mostly compliant</option>
              <option>Non-compliant</option>
              <option>No planogram in place</option>
            </select>
          </div>
          <div class="field">
            <label>Number of Facings (Pings)</label>
            <input type="number" id="facings-count" min="0" placeholder="Count">
          </div>
          <div class="field">
            <label>Competitor Facings Observed</label>
            <input type="number" id="comp-facings" min="0" placeholder="Count">
          </div>
        </div>
        <div class="field" style="margin-top:14px">
          <label>Shelf / Display Action Taken</label>
          <textarea id="shelf-action" placeholder="Describe any shelf improvements made during the promotion (re-stocking, signage placed, facing adjustments, etc.)"></textarea>
        </div>
      </div>
    </div>

    <!-- §8 — CONSUMER FEEDBACK -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">8</div>
        <div>
          <div class="fs-title">Consumer Feedback & Market Intelligence</div>
          <div class="fs-desc">Record real-time consumer and trade insights</div>
        </div>
        <div class="fs-icon">💬</div>
      </div>
      <div class="fs-body">
        <div class="fg fg-2">
          <div class="field">
            <label>Consumer Sentiment</label>
            <select id="consumer-sentiment">
              <option>⭐⭐⭐⭐⭐ Very Positive</option>
              <option>⭐⭐⭐⭐ Positive</option>
              <option>⭐⭐⭐ Neutral</option>
              <option>⭐⭐ Negative</option>
              <option>⭐ Very Negative</option>
            </select>
          </div>
          <div class="field">
            <label>Most Requested Product</label>
            <input type="text" id="most-requested" placeholder="Which Pings SKU did consumers ask for most?">
          </div>
        </div>
        <div class="fg fg-2" style="margin-top:14px">
          <div class="field">
            <label>Most Common Objection / Feedback</label>
            <textarea id="consumer-objection" placeholder="What were the main concerns or objections raised by consumers?"></textarea>
          </div>
          <div class="field">
            <label>Product / Price Feedback</label>
            <textarea id="price-feedback" placeholder="What did consumers say about product quality, size, or pricing?"></textarea>
          </div>
        </div>
        <div class="field" style="margin-top:14px">
          <label>Notable Consumer Quote / Observation</label>
          <textarea id="consumer-quote" placeholder="Record any standout consumer comment, question, or insight verbatim…"></textarea>
        </div>
      </div>
    </div>

    <!-- §9 — PROMOTER FINDINGS -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">9</div>
        <div>
          <div class="fs-title">Promoter Findings & Field Intelligence</div>
          <div class="fs-desc">Overall observations and operational notes from the promoter</div>
        </div>
        <div class="fs-icon">🔎</div>
      </div>
      <div class="fs-body">
        <div class="fg fg-2">
          <div class="field">
            <label>Overall Promotion Rating</label>
            <select id="promo-rating">
              <option>⭐⭐⭐⭐⭐ Excellent</option>
              <option>⭐⭐⭐⭐ Good</option>
              <option>⭐⭐⭐ Fair</option>
              <option>⭐⭐ Poor</option>
              <option>⭐ Very Poor</option>
            </select>
          </div>
          <div class="field">
            <label>Key Win / Achievement</label>
            <input type="text" id="key-win" placeholder="Single best outcome from this promotion">
          </div>
        </div>
        <div class="field" style="margin-top:14px">
          <label>Key Challenges Encountered</label>
          <textarea id="key-challenges" placeholder="What challenges were faced? (delivery issues, shelf space, staff cooperation, expired stock, etc.)"></textarea>
        </div>
        <div class="field" style="margin-top:14px">
          <label>Detailed Findings & Observations</label>
          <textarea id="detailed-findings" style="min-height:120px" placeholder="Full narrative of what happened during the promotion — include anything relevant to management: trade behaviour, store dynamics, pricing, distribution gaps, staff attitude, repeat customers, volume trends, etc."></textarea>
        </div>
        <div class="fg fg-2" style="margin-top:14px">
          <div class="field">
            <label>Issues Requiring Immediate Action</label>
            <textarea id="immediate-issues" placeholder="Any issues that need to be escalated to management immediately (expired product, hostile trade, supply chain problems, etc.)"></textarea>
          </div>
          <div class="field">
            <label>Promoter Recommendation to Management</label>
            <textarea id="promoter-recommendation" placeholder="Based on your time in trade, what do you recommend Pings or AlcoBina do next at this account?"></textarea>
          </div>
        </div>
      </div>
    </div>

    <!-- §10 — SIGN-OFF -->
    <div class="form-section">
      <div class="fs-head">
        <div class="fs-num">10</div>
        <div>
          <div class="fs-title">Sign-Off & Declaration</div>
          <div class="fs-desc">Promoter check-out and submission</div>
        </div>
        <div class="fs-icon">✅</div>
      </div>
      <div class="fs-body">
        <div class="fg fg-3">
          <div class="field">
            <label>Check-Out Timestamp</label>
            <input type="text" id="checkout-time" readonly>
          </div>
          <div class="field">
            <label>Total Hours on Site</label>
            <input type="text" id="hours-on-site" readonly placeholder="Auto-calculated">
          </div>
          <div class="field">
            <label>Promotion Status</label>
            <select id="promo-status">
              <option>Completed</option>
              <option>Partially Completed</option>
              <option>Interrupted — Will Continue</option>
              <option>Cancelled</option>
            </select>
          </div>
        </div>
        <div class="fg fg-2" style="margin-top:14px">
          <div class="field">
            <label>Store Manager / Owner Sign-Off Name</label>
            <input type="text" id="store-signoff-name" placeholder="Name of person authorising">
          </div>
          <div class="field">
            <label>Any Promised Follow-Up by Pings / AlcoBina?</label>
            <input type="text" id="followup-promise" placeholder="e.g. Delivery by Thursday, Reorder call Tuesday">
          </div>
        </div>
        <div class="field" style="margin-top:14px">
          <label>Final Promoter Notes</label>
          <textarea id="final-notes" placeholder="Anything else you want management to know about this visit?"></textarea>
        </div>
        <div class="info-box" style="margin-top:14px">
          ✅ By submitting this form, I confirm that all information recorded is accurate to the best of my knowledge at the time of submission. Timestamp and GPS data will be auto-appended.
        </div>
      </div>
    </div>

    <!-- ACTION BAR -->
    <div class="form-actions-bar" style="display:flex;gap:10px;flex-wrap:wrap;padding:8px 0 20px">
      <button class="btn btn-primary" onclick="checkOutAndSubmit()">✅ Check Out & Submit Report</button>
      <button class="btn btn-outline" onclick="saveDraft()">💾 Save Draft</button>
      <button class="btn btn-outline" onclick="window.print()">🖨 Print Form</button>
      <button class="btn btn-outline" onclick="exportJSON()">⬇ Export JSON</button>
    </div>

  </div><!-- /page-form -->

  <!-- ══════════════════════════════════════════════ -->
  <!-- PAGE: DASHBOARD -->
  <!-- ══════════════════════════════════════════════ -->
  <div class="page" id="page-dashboard">
    <div style="font-family:var(--font-head);font-size:22px;font-weight:800;color:var(--navy);margin-bottom:4px">Management Dashboard</div>
    <div style="font-size:13px;color:var(--gray3);margin-bottom:22px">Live overview of all AlcoBina × Pings promotion activity</div>

    <!-- KPI Stats -->
    <div class="dash-stats">
      <div class="stat-card blue">
        <div class="sc-icon">📋</div>
        <div class="sc-val" id="kpi-submissions">1</div>
        <div class="sc-label">Total Submissions</div>
        <div class="sc-delta up" id="kpi-sub-delta">+1 today</div>
      </div>
      <div class="stat-card orange">
        <div class="sc-icon">👥</div>
        <div class="sc-val" id="kpi-promoters">1</div>
        <div class="sc-label">Active Promoters</div>
        <div class="sc-delta up">In field today</div>
      </div>
      <div class="stat-card green">
        <div class="sc-icon">📦</div>
        <div class="sc-val" id="kpi-units">0</div>
        <div class="sc-label">Total Units Sold</div>
        <div class="sc-delta up" id="kpi-units-delta">Across all reports</div>
      </div>
      <div class="stat-card navy">
        <div class="sc-icon">🏪</div>
        <div class="sc-val" id="kpi-stores">0</div>
        <div class="sc-label">Stores Activated</div>
        <div class="sc-delta up">This period</div>
      </div>
      <div class="stat-card red">
        <div class="sc-icon">🚨</div>
        <div class="sc-val" id="kpi-issues">0</div>
        <div class="sc-label">Issues Flagged</div>
        <div class="sc-delta dn" id="kpi-issues-txt">Requires attention</div>
      </div>
    </div>

    <!-- Charts -->
    <div class="chart-grid">
      <div class="chart-card">
        <div class="chart-title">Units Sold by SKU <span>Across all reports</span></div>
        <div class="bar-chart" id="sku-bar-chart">
          <!-- populated by JS -->
        </div>
        <div id="sku-bar-labels" style="display:flex;gap:8px;margin-top:8px;flex-wrap:wrap"></div>
      </div>
      <div class="chart-card">
        <div class="chart-title">Sell-Through by Product <span>% of opening sold</span></div>
        <div class="donut-wrap" id="donut-wrap">
          <svg class="donut-svg" viewBox="0 0 120 120" id="donut-svg">
            <circle cx="60" cy="60" r="45" fill="none" stroke="#EEF1F8" stroke-width="18"/>
            <text x="60" y="65" text-anchor="middle" font-size="14" font-weight="700" fill="#0B1E45">—</text>
          </svg>
          <div class="donut-legend" id="donut-legend"></div>
        </div>
      </div>
    </div>

    <!-- Recent Reports -->
    <div class="reports-table-wrap">
      <div class="rt-head">
        <h3>Recent Promotion Reports</h3>
        <div style="display:flex;gap:8px">
          <button class="btn btn-outline btn-sm" onclick="showPage('reports')">View All</button>
        </div>
      </div>
      <div style="overflow-x:auto">
        <table class="rt" id="dash-recent-table">
          <thead>
            <tr>
              <th>Form ID</th><th>Promoter</th><th>Store</th>
              <th>Parish</th><th>Date</th><th>Units Sold</th>
              <th>Sell-Through</th><th>Status</th><th>Action</th>
            </tr>
          </thead>
          <tbody id="dash-tbody">
            <tr><td colspan="9" style="text-align:center;padding:24px;color:var(--gray3)">No submissions yet. Complete a promotion form to see data here.</td></tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- ══════════════════════════════════════════════ -->
  <!-- PAGE: ANALYTICS -->
  <!-- ══════════════════════════════════════════════ -->
  <div class="page" id="page-analytics">
    <div style="font-family:var(--font-head);font-size:22px;font-weight:800;color:var(--navy);margin-bottom:4px">Analytics</div>
    <div style="font-size:13px;color:var(--gray3);margin-bottom:22px">Deep performance metrics across all promotion activities</div>

    <div class="analytics-grid" id="analytics-grid">
      <!-- SKU Performance Card -->
      <div class="perf-card">
        <div class="perf-title">📦 SKU Performance</div>
        <div id="sku-perf-rows">
          <div style="color:var(--gray3);font-size:13px">Submit a form to see SKU analytics</div>
        </div>
      </div>
      <!-- Sell-Through Card -->
      <div class="perf-card">
        <div class="perf-title">📊 Sell-Through Rates</div>
        <div id="sellthru-rows">
          <div style="color:var(--gray3);font-size:13px">Submit a form to see sell-through data</div>
        </div>
      </div>
      <!-- Competition Intel -->
      <div class="perf-card">
        <div class="perf-title">🔍 Competition Intel Summary</div>
        <div id="comp-intel-rows">
          <div style="color:var(--gray3);font-size:13px">Log competitor activity to see summary</div>
        </div>
      </div>
      <!-- Parish Coverage -->
      <div class="perf-card">
        <div class="perf-title">📍 Parish Coverage</div>
        <div id="parish-rows">
          <div style="color:var(--gray3);font-size:13px">Submissions needed to see parish data</div>
        </div>
      </div>
    </div>

    <!-- Trend -->
    <div class="chart-card" style="margin-bottom:20px">
      <div class="chart-title">Promoter Activity Timeline <span>Last 7 submissions</span></div>
      <div class="bar-chart" id="timeline-chart" style="height:120px">
        <div style="display:flex;align-items:center;color:var(--gray3);font-size:13px;width:100%">No timeline data yet</div>
      </div>
    </div>
  </div>

  <!-- ══════════════════════════════════════════════ -->
  <!-- PAGE: LEADERBOARD -->
  <!-- ══════════════════════════════════════════════ -->
  <div class="page" id="page-leaderboard">
    <div style="font-family:var(--font-head);font-size:22px;font-weight:800;color:var(--navy);margin-bottom:4px">Promoter Performance</div>
    <div style="font-size:13px;color:var(--gray3);margin-bottom:22px">Ranked by total units sold across all promotions</div>
    <div class="lb-wrap" id="leaderboard-wrap">
      <div style="padding:24px;text-align:center;color:var(--gray3);font-size:13px">No promoter data yet. Leaderboard populates automatically from form submissions.</div>
    </div>
  </div>

  <!-- ══════════════════════════════════════════════ -->
  <!-- PAGE: ALL REPORTS -->
  <!-- ══════════════════════════════════════════════ -->
  <div class="page" id="page-reports">
    <div style="font-family:var(--font-head);font-size:22px;font-weight:800;color:var(--navy);margin-bottom:4px">All Promotion Reports</div>
    <div style="font-size:13px;color:var(--gray3);margin-bottom:18px">Complete historical record of all AlcoBina × Pings promotion submissions</div>

    <div class="filter-bar">
      <label>Search<input type="text" placeholder="Name, store, ID…" id="filter-search" oninput="filterReports()"></label>
      <label>Parish<select id="filter-parish" onchange="filterReports()">
        <option value="">All parishes</option>
        <option>Kingston & St. Andrew</option><option>St. Catherine</option>
        <option>Clarendon</option><option>Manchester</option>
        <option>St. Elizabeth</option><option>St. James</option>
      </select></label>
      <label>Status<select id="filter-status" onchange="filterReports()">
        <option value="">All statuses</option>
        <option>Completed</option><option>Partially Completed</option><option>Cancelled</option>
      </select></label>
      <label>Date From<input type="date" id="filter-date-from" onchange="filterReports()"></label>
      <label>Date To<input type="date" id="filter-date-to" onchange="filterReports()"></label>
      <button class="btn btn-outline btn-sm" onclick="clearFilters()">Clear</button>
    </div>

    <div class="reports-table-wrap">
      <div class="rt-head">
        <h3>All Reports (<span id="report-count">0</span>)</h3>
        <button class="btn btn-green btn-sm" onclick="exportAllCSV()">⬇ Export CSV</button>
      </div>
      <div style="overflow-x:auto">
        <table class="rt">
          <thead>
            <tr>
              <th>Form ID</th><th>Promoter</th><th>Store</th>
              <th>Parish</th><th>Start Date</th><th>Days</th>
              <th>Units Sold</th><th>Sell-Through</th>
              <th>Submitted</th><th>Status</th><th>Actions</th>
            </tr>
          </thead>
          <tbody id="all-reports-tbody">
            <tr><td colspan="11" style="text-align:center;padding:24px;color:var(--gray3)">No reports submitted yet.</td></tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- ══════════════════════════════════════════════ -->
  <!-- PAGE: PREVIEW (my submissions) -->
  <!-- ══════════════════════════════════════════════ -->
  <div class="page" id="page-preview">
    <div style="font-family:var(--font-head);font-size:22px;font-weight:800;color:var(--navy);margin-bottom:18px">My Submissions</div>
    <div id="my-submissions-list">
      <div style="text-align:center;padding:48px;color:var(--gray3);font-size:14px">You have not submitted any reports yet.</div>
    </div>
  </div>

  <!-- ══════════════════════════════════════════════ -->
  <!-- PAGE: SETTINGS -->
  <!-- ══════════════════════════════════════════════ -->
  <div class="page" id="page-settings">
    <div style="font-family:var(--font-head);font-size:22px;font-weight:800;color:var(--navy);margin-bottom:18px">⚙️ System Settings</div>
    <div class="form-section">
      <div class="fs-head"><div class="fs-num">1</div><div><div class="fs-title">Product SKU Configuration</div><div class="fs-desc">Manage the Pings product list used in forms</div></div></div>
      <div class="fs-body">
        <div style="font-size:13px;color:var(--gray4);margin-bottom:12px">Current active SKUs (edit <code>SKUS</code> array in JS to customise):</div>
        <div id="settings-sku-list" style="display:flex;flex-direction:column;gap:6px"></div>
      </div>
    </div>
    <div class="form-section">
      <div class="fs-head"><div class="fs-num">2</div><div><div class="fs-title">Data Management</div><div class="fs-desc">Export, import, or clear stored data</div></div></div>
      <div class="fs-body" style="display:flex;gap:10px;flex-wrap:wrap">
        <button class="btn btn-green" onclick="exportAllCSV()">⬇ Export All to CSV</button>
        <button class="btn btn-outline" onclick="exportJSON()">⬇ Export Current Form JSON</button>
        <button class="btn btn-outline" onclick="if(confirm('Clear all data? This cannot be undone.'))clearAllData()">🗑 Clear All Data</button>
      </div>
    </div>
  </div>

</div><!-- /main -->

<!-- MODAL -->
<div class="modal-overlay" id="modal-overlay">
  <div class="modal">
    <div class="modal-head">
      <h3 id="modal-title">Report Detail</h3>
      <button class="modal-close" onclick="closeModal()">✕</button>
    </div>
    <div class="modal-body" id="modal-body"></div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<!-- ════════════════════════════════════════════════ -->
<!-- JAVASCRIPT -->
<!-- ════════════════════════════════════════════════ -->
<script>
// ── DATA ─────────────────────────────────────────────────
const SKUS = [
  {name:"Sud Sud (Yellow) 350g",  uom:"Grams",    upc:20, price:137.50},
  {name:"Sud Sud (Green) 250g",   uom:"Grams",    upc:20, price:104.67},
  {name:"High Grade 350g",        uom:"Grams",    upc:20, price:180.00},
  {name:"Sud Sud Yellow 900g",    uom:"Grams",    upc:12, price:287.50},
  {name:"Sud Sud Sea Breeze 700g",uom:"Grams",    upc:10, price:325.00},
  {name:"Sud Sud Sea Breeze 200g",uom:"Grams",    upc:40, price:94.50},
  {name:"Go Fresh (500g)",        uom:"Grams",    upc:24, price:80.00},
  {name:"Go Fresh (1kg)",         uom:"Grams",    upc:12, price:145.00},
];

let submissions = JSON.parse(localStorage.getItem("ab_submissions") || "[]");
let currentDays = 2;
let checkInTime = null;
let formUID = generateUID();

// ── INIT ─────────────────────────────────────────────────
function init(){
  buildInventoryTable();
  buildReorderTable();
  buildDayPanels(2);
  buildSummaryTable();
  setTimestamps();
  updateClock();
  setInterval(updateClock, 1000);
  getGPS();
  setTopDate();
  updateDashboard();
  buildSettingsSKUs();
  updateNavBadge();
  setInterval(updateHoursOnSite, 60000);
}

function generateUID(){
  return "ABF-" + Date.now().toString(36).toUpperCase() + "-" + Math.random().toString(36).substr(2,4).toUpperCase();
}

function setTimestamps(){
  checkInTime = new Date();
  const f = formatDateTime(checkInTime);
  document.getElementById("form-timestamp").textContent = f;
  document.getElementById("checkin-time").value = f;
  document.getElementById("form-uid").textContent = "Form ID: " + formUID;
}

function updateClock(){
  const now = new Date();
  document.getElementById("live-clock").textContent = now.toLocaleTimeString("en-JM");
}

function setTopDate(){
  const now = new Date();
  document.getElementById("top-date").textContent = now.toLocaleDateString("en-JM",{weekday:"long",year:"numeric",month:"long",day:"numeric"});
}

function formatDateTime(d){ return d.toLocaleDateString("en-JM",{day:"2-digit",month:"short",year:"numeric"}) + " " + d.toLocaleTimeString("en-JM"); }
function formatDate(d){ return d.toLocaleDateString("en-JM",{day:"2-digit",month:"short",year:"numeric"}); }

function getGPS(){
  if(navigator.geolocation){
    navigator.geolocation.getCurrentPosition(
      p => { document.getElementById("gps-location").value = `${p.coords.latitude.toFixed(5)}, ${p.coords.longitude.toFixed(5)}`; },
      ()  => { document.getElementById("gps-location").value = "Location unavailable"; }
    );
  } else {
    document.getElementById("gps-location").value = "Not supported";
  }
}

// ── INVENTORY TABLE ──────────────────────────────────────
function buildInventoryTable(){
  const tbody = document.getElementById("inv-tbody");
  tbody.innerHTML = SKUS.map((s,i) => `
    <tr>
      <td>${s.name}</td>
      <td class="sku-uom">${s.uom}</td>
      <td class="sku-uom">${s.upc}</td>
      <td><input type="number" min="0" value="0" id="inv-cases-${i}" oninput="calcInvRow(${i})" style="width:80px"></td>
      <td><input type="number" min="0" value="0" id="inv-units-${i}" oninput="calcInvTotals()" style="width:80px"></td>
      <td class="sku-uom">J$${s.price.toFixed(2)}</td>
      <td><span class="sku-total" id="inv-val-${i}">J$0.00</span></td>
      <td><input type="text" placeholder="e.g. Aisle 3, Shelf B" id="inv-shelf-${i}" style="border:1.5px solid var(--gray2);border-radius:6px;padding:5px 8px;font-size:12px;width:140px"></td>
    </tr>
  `).join("");
}

function calcInvRow(i){
  const cases = parseInt(document.getElementById(`inv-cases-${i}`).value)||0;
  const units = cases * SKUS[i].upc;
  document.getElementById(`inv-units-${i}`).value = units;
  document.getElementById(`inv-val-${i}`).textContent = "J$" + (units * SKUS[i].price).toLocaleString("en-JM",{minimumFractionDigits:2});
  calcInvTotals();
  updateSummaryTable();
}

function calcInvTotals(){
  let tu=0, tv=0;
  SKUS.forEach((_,i)=>{
    const u = parseInt(document.getElementById(`inv-units-${i}`).value)||0;
    tu += u; tv += u * SKUS[i].price;
  });
  document.getElementById("total-opening-units").textContent = tu.toLocaleString();
  document.getElementById("total-opening-value").textContent = "J$" + tv.toLocaleString("en-JM",{minimumFractionDigits:2});
  document.getElementById("gt-opening").textContent = tu.toLocaleString();
  updateSummaryTable();
}

// ── DAY PANELS ────────────────────────────────────────────
function buildDayPanels(days){
  currentDays = days;
  const cont = document.getElementById("day-panels");
  cont.innerHTML = "";
  for(let d=0;d<days;d++){
    const div = document.createElement("div");
    div.className = "day-content" + (d===0?" active":"");
    div.id = `day-panel-${d}`;
    div.innerHTML = `
      <div class="fg fg-3" style="margin-bottom:14px">
        <div class="field"><label>Date (Day ${d+1})</label><input type="date" id="day-date-${d}"></div>
        <div class="field"><label>Start Time</label><input type="time" id="day-start-${d}"></div>
        <div class="field"><label>End Time</label><input type="time" id="day-end-${d}"></div>
      </div>
      <div class="sku-table-wrap">
        <table class="sku-table">
          <thead><tr>
            <th style="width:200px">Product / SKU</th>
            <th>Units Sold</th>
            <th>Cases Equivalent</th>
            <th>Revenue (J$)</th>
            <th>Notes</th>
          </tr></thead>
          <tbody>
            ${SKUS.map((s,i)=>`
              <tr>
                <td>${s.name}</td>
                <td><input type="number" min="0" value="0" id="sold-${d}-${i}" oninput="calcDaySales(${d})" style="width:80px"></td>
                <td><span id="sold-cases-${d}-${i}" class="sku-uom">0</span></td>
                <td><span id="sold-rev-${d}-${i}" class="sku-uom">J$0</span></td>
                <td><input type="text" placeholder="Note…" id="sold-note-${d}-${i}" style="border:1.5px solid var(--gray2);border-radius:6px;padding:4px 8px;font-size:12px;width:140px"></td>
              </tr>
            `).join("")}
          </tbody>
          <tfoot>
            <tr class="sku-total-row">
              <td><strong>Day ${d+1} Total</strong></td>
              <td><span class="sku-total" id="day-total-units-${d}">0</span></td>
              <td>—</td>
              <td><span class="sku-total" id="day-total-rev-${d}">J$0</span></td>
              <td>—</td>
            </tr>
          </tfoot>
        </table>
      </div>
      <div class="field" style="margin-top:12px">
        <label>Day ${d+1} — Promoter Observations</label>
        <textarea placeholder="What happened today? Consumer reactions, store activity, challenges…" id="day-obs-${d}" style="min-height:70px"></textarea>
      </div>
    `;
    cont.appendChild(div);
  }
  // update tabs
  const tabs = document.getElementById("day-tabs");
  tabs.innerHTML = "";
  for(let d=0;d<days;d++){
    const btn = document.createElement("button");
    btn.className = "day-tab" + (d===0?" active":"");
    btn.id = "dtab-"+d;
    btn.textContent = "Day " + (d+1);
    btn.onclick = (()=>{ const dd=d; return ()=>switchDay(dd); })();
    tabs.appendChild(btn);
  }
  buildSummaryTable();
}

function switchDay(d){
  document.querySelectorAll(".day-content").forEach(el=>el.classList.remove("active"));
  document.querySelectorAll(".day-tab").forEach(el=>el.classList.remove("active"));
  const panel = document.getElementById(`day-panel-${d}`);
  const tab   = document.getElementById(`dtab-${d}`);
  if(panel) panel.classList.add("active");
  if(tab)   tab.classList.add("active");
}

function calcDaySales(d){
  let tu=0, tr=0;
  SKUS.forEach((s,i)=>{
    const u = parseInt(document.getElementById(`sold-${d}-${i}`).value)||0;
    const cases = (u/s.upc).toFixed(2);
    const rev = u * s.price;
    document.getElementById(`sold-cases-${d}-${i}`).textContent = cases;
    document.getElementById(`sold-rev-${d}-${i}`).textContent = "J$" + rev.toLocaleString("en-JM",{minimumFractionDigits:2});
    tu += u; tr += rev;
  });
  document.getElementById(`day-total-units-${d}`).textContent = tu.toLocaleString();
  document.getElementById(`day-total-rev-${d}`).textContent = "J$" + tr.toLocaleString("en-JM",{minimumFractionDigits:2});
  updateSummaryTable();
}

function buildSummaryTable(){
  const tbody = document.getElementById("summary-tbody");
  // Update column headers
  for(let d=0;d<currentDays;d++){
    const hd = document.getElementById(`sum-d${d+1}h`);
    if(hd) hd.textContent = `Day ${d+1}`;
  }
  tbody.innerHTML = SKUS.map((s,i)=>`
    <tr>
      <td>${s.name}</td>
      ${Array.from({length:currentDays},(_,d)=>`<td id="sum-${d}-${i}">0</td>`).join("")}
      <td><strong id="sum-total-${i}">0</strong></td>
      <td id="sum-open-${i}">0</td>
      <td id="sum-pct-${i}">—</td>
      <td id="sum-close-${i}">0</td>
    </tr>
  `).join("");
  updateSummaryTable();
}

function updateSummaryTable(){
  let gtD=[],gtTotal=0,gtOpen=0;
  for(let d=0;d<currentDays;d++) gtD.push(0);
  SKUS.forEach((s,i)=>{
    let total=0;
    for(let d=0;d<currentDays;d++){
      const el = document.getElementById(`sold-${d}-${i}`);
      const u = el ? (parseInt(el.value)||0) : 0;
      const cell = document.getElementById(`sum-${d}-${i}`);
      if(cell) cell.textContent = u;
      total += u; gtD[d] += u;
    }
    const open = parseInt(document.getElementById(`inv-units-${i}`)?.value)||0;
    const close = Math.max(0, open - total);
    const pct = open > 0 ? ((total/open)*100).toFixed(1)+"%" : "—";
    const te = document.getElementById(`sum-total-${i}`);
    const oe = document.getElementById(`sum-open-${i}`);
    const pe = document.getElementById(`sum-pct-${i}`);
    const ce = document.getElementById(`sum-close-${i}`);
    if(te) te.textContent = total;
    if(oe) oe.textContent = open;
    if(pe){ pe.textContent = pct; pe.style.color = open>0&&total>0 ? "var(--green)" : "var(--gray3)"; }
    if(ce) ce.textContent = close;
    gtTotal += total; gtOpen += open;
  });
  for(let d=0;d<currentDays;d++){
    const gt = document.getElementById(`gt-d${d+1}`);
    if(gt) gt.textContent = gtD[d];
  }
  document.getElementById("gt-total").textContent = gtTotal;
  document.getElementById("gt-opening").textContent = gtOpen;
  document.getElementById("gt-pct").textContent = gtOpen>0 ? ((gtTotal/gtOpen)*100).toFixed(1)+"%" : "—";
  document.getElementById("gt-closing").textContent = Math.max(0,gtOpen-gtTotal);
  updateReorderTable();
}

function updateDayTabs(){
  const s = document.getElementById("promo-start").value;
  const e = document.getElementById("promo-end").value;
  if(s&&e){
    const start = new Date(s); const end = new Date(e);
    const diff = Math.max(1, Math.round((end-start)/(1000*60*60*24))+1);
    document.getElementById("promo-days").value = diff;
    if(diff !== currentDays) buildDayPanels(diff);
  }
}

// ── REORDER TABLE ──────────────────────────────────────────
function buildReorderTable(){
  const tbody = document.getElementById("reorder-tbody");
  tbody.innerHTML = SKUS.map((s,i) => `
    <tr>
      <td>${s.name}</td>
      <td><span id="ro-close-${i}">0</span></td>
      <td><input type="number" min="0" value="" id="ro-qty-${i}" placeholder="Cases" style="width:80px;border:1.5px solid var(--gray2);border-radius:6px;padding:5px 8px;font-size:13px;text-align:center"></td>
      <td><select id="ro-urg-${i}" style="border:1.5px solid var(--gray2);border-radius:6px;padding:5px 8px;font-size:12px">
        <option>🔴 Urgent — reorder now</option>
        <option>🟡 Soon — within 48 hrs</option>
        <option>🟢 Standard — next delivery</option>
        <option>⬜ Not needed</option>
      </select></td>
      <td><input type="text" placeholder="Reason for recommendation…" id="ro-note-${i}" style="border:1.5px solid var(--gray2);border-radius:6px;padding:5px 8px;font-size:12px;width:200px"></td>
    </tr>
  `).join("");
}

function updateReorderTable(){
  SKUS.forEach((_,i)=>{
    const open = parseInt(document.getElementById(`inv-units-${i}`)?.value)||0;
    let total=0;
    for(let d=0;d<currentDays;d++){
      const el = document.getElementById(`sold-${d}-${i}`);
      total += el ? (parseInt(el.value)||0) : 0;
    }
    const close = Math.max(0,open-total);
    const el = document.getElementById(`ro-close-${i}`);
    if(el) el.textContent = close;
  });
}

// ── COMPETITOR TABLE ──────────────────────────────────────
function addCompRow(){
  const tbody = document.getElementById("comp-tbody");
  const row = document.createElement("tr");
  const dayOpts = Array.from({length:currentDays},(_,i)=>`<option>Day ${i+1}</option>`).join("");
  row.innerHTML = `
    <td><select name="comp-day" style="width:55px">${dayOpts}</select></td>
    <td><input type="text" placeholder="Brand name"></td>
    <td><select><option value="">Type…</option><option>BOGO</option><option>Price Reduction</option><option>Sampling</option><option>Paid Shelf</option><option>Poster Campaign</option><option>Promoter Present</option><option>Price Tag Removal</option><option>Other</option></select></td>
    <td><input type="text" placeholder="Product/SKU"></td>
    <td><input type="text" placeholder="e.g. J$250/unit"></td>
    <td><input type="text" placeholder="Details…"></td>
    <td><select><option value="">—</option><option>🟢 Low</option><option>🟡 Medium</option><option>🔴 High</option><option>🚨 Critical</option></select></td>
    <td><button type="button" onclick="removeRow(this)" style="border:none;background:none;color:var(--red);cursor:pointer;font-size:16px">✕</button></td>
  `;
  tbody.appendChild(row);
}

function removeRow(btn){ btn.closest("tr").remove(); }

// ── HOURS ON SITE ─────────────────────────────────────────
function updateHoursOnSite(){
  if(!checkInTime) return;
  const now = new Date();
  const diff = now - checkInTime;
  const h = Math.floor(diff/3600000);
  const m = Math.floor((diff%3600000)/60000);
  document.getElementById("hours-on-site").value = `${h}h ${m}m`;
}

// ── FORM SUBMISSION ────────────────────────────────────────
function checkOutAndSubmit(){
  const name = document.getElementById("promoter-name").value.trim();
  const store = document.getElementById("customer-name").value.trim();
  if(!name){ showToast("⚠️ Please enter promoter name","var(--orange)"); return; }
  if(!store){ showToast("⚠️ Please enter customer/store name","var(--orange)"); return; }

  const checkOut = new Date();
  document.getElementById("checkout-time").value = formatDateTime(checkOut);
  updateHoursOnSite();

  const data = collectFormData(checkOut);
  submissions.push(data);
  localStorage.setItem("ab_submissions", JSON.stringify(submissions));
  updateDashboard();
  updateNavBadge();
  showToast("✅ Report submitted successfully! Form ID: " + formUID);
  document.getElementById("top-submissions").textContent = submissions.length + " Submissions";
  setTimeout(()=>{ if(confirm("Form submitted! Start a new form?")) clearForm(); }, 1200);
}

function collectFormData(checkOut){
  const daysSales = [];
  for(let d=0;d<currentDays;d++){
    const sold = SKUS.map((_,i)=> parseInt(document.getElementById(`sold-${d}-${i}`)?.value)||0 );
    daysSales.push(sold);
  }
  const opening = SKUS.map((_,i)=> parseInt(document.getElementById(`inv-units-${i}`)?.value)||0 );
  const totalSold = SKUS.map((_,i)=> daysSales.reduce((s,d)=>s+d[i],0));

  const compRows = [];
  document.querySelectorAll("#comp-tbody tr").forEach(tr=>{
    const cells = tr.querySelectorAll("input,select");
    if(cells.length>=6){
      compRows.push({
        day: cells[0].value, brand: cells[1].value, type: cells[2].value,
        product: cells[3].value, price: cells[4].value, notes: cells[5].value,
        threat: cells[6]?.value || ""
      });
    }
  });

  return {
    uid: formUID, submittedAt: checkOut.toISOString(), checkIn: checkInTime.toISOString(),
    checkOut: checkOut.toISOString(),
    promoterName: document.getElementById("promoter-name").value,
    promoterID: document.getElementById("promoter-id").value,
    supervisor: document.getElementById("supervisor-name").value,
    customerName: document.getElementById("customer-name").value,
    customerAddress: document.getElementById("store-address").value,
    parish: document.getElementById("store-parish").value,
    storeType: document.getElementById("store-type").value,
    promoStart: document.getElementById("promo-start").value,
    promoEnd: document.getElementById("promo-end").value,
    promoDays: parseInt(document.getElementById("promo-days").value)||currentDays,
    activationType: document.getElementById("activation-type").value,
    gps: document.getElementById("gps-location").value,
    status: document.getElementById("promo-status").value,
    opening, daysSales, totalSold,
    totalUnits: totalSold.reduce((a,b)=>a+b,0),
    openingTotal: opening.reduce((a,b)=>a+b,0),
    sellThruPct: opening.reduce((a,b)=>a+b,0) > 0 ? (totalSold.reduce((a,b)=>a+b,0)/opening.reduce((a,b)=>a+b,0)*100).toFixed(1) : "0",
    competitionLog: compRows,
    shelfPosition: document.getElementById("shelf-position").value,
    popMaterials: document.getElementById("pop-materials").value,
    priceTags: document.getElementById("price-tags").value,
    consumerSentiment: document.getElementById("consumer-sentiment").value,
    mostRequested: document.getElementById("most-requested").value,
    findings: document.getElementById("detailed-findings").value,
    challenges: document.getElementById("key-challenges").value,
    keyWin: document.getElementById("key-win").value,
    immediateIssues: document.getElementById("immediate-issues").value,
    recommendation: document.getElementById("promoter-recommendation").value,
    promoRating: document.getElementById("promo-rating").value,
    finalNotes: document.getElementById("final-notes").value,
  };
}

function saveDraft(){
  const data = collectFormData(new Date());
  localStorage.setItem("ab_draft", JSON.stringify(data));
  showToast("💾 Draft saved");
}

function clearForm(){
  formUID = generateUID();
  checkInTime = new Date();
  currentDays = 2;
  document.querySelectorAll("input:not([readonly]),select,textarea").forEach(el=>{
    if(el.type==="number") el.value="0";
    else if(el.type!=="submit"&&el.tagName==="INPUT") el.value="";
    else if(el.tagName==="SELECT") el.selectedIndex=0;
    else if(el.tagName==="TEXTAREA") el.value="";
  });
  setTimestamps();
  buildInventoryTable();
  buildDayPanels(2);
  buildSummaryTable();
  buildReorderTable();
  showToast("🔄 New form started");
}

// ── DASHBOARD ──────────────────────────────────────────────
function updateDashboard(){
  if(!submissions.length){ return; }
  const totalUnits = submissions.reduce((s,r)=>s+r.totalUnits,0);
  const stores = new Set(submissions.map(r=>r.customerName)).size;
  const issues = submissions.filter(r=>r.immediateIssues&&r.immediateIssues.trim()).length;
  const promos = new Set(submissions.map(r=>r.promoterName)).size;

  document.getElementById("kpi-submissions").textContent = submissions.length;
  document.getElementById("kpi-promoters").textContent = promos;
  document.getElementById("kpi-units").textContent = totalUnits.toLocaleString();
  document.getElementById("kpi-stores").textContent = stores;
  document.getElementById("kpi-issues").textContent = issues;
  document.getElementById("kpi-sub-delta").textContent = `+${submissions.length} total`;
  document.getElementById("kpi-units-delta").textContent = `${totalUnits.toLocaleString()} units across ${submissions.length} reports`;
  document.getElementById("top-submissions").textContent = submissions.length + " Submission" + (submissions.length!==1?"s":"");

  buildSKUBarChart();
  buildDonut();
  buildDashTable();
  buildAllReportsTable();
  buildLeaderboard();
  buildAnalyticsCards();
}

function buildSKUBarChart(){
  const totals = SKUS.map((_,i)=> submissions.reduce((s,r)=>s+(r.totalSold[i]||0),0));
  const maxVal = Math.max(...totals,1);
  const colors = ["#2563C7","#E8760A","#6D28D9","#0A7A45","#009EB4","#C0241E","#92400E","#0F766E"];
  const cont = document.getElementById("sku-bar-chart");
  cont.innerHTML = SKUS.map((s,i)=>`
    <div class="bar-group">
      <div class="bar-val">${totals[i]}</div>
      <div class="bar" style="height:${Math.round((totals[i]/maxVal)*140)}px;background:${colors[i%colors.length]}" data-val="${totals[i]} units"></div>
      <div class="bar-lbl">${s.name.split(" ").slice(0,2).join(" ")}</div>
    </div>
  `).join("");
}

function buildDonut(){
  const totals = SKUS.map((_,i)=> submissions.reduce((s,r)=>s+(r.totalSold[i]||0),0));
  const opening = SKUS.map((_,i)=> submissions.reduce((s,r)=>s+(r.opening[i]||0),0));
  const pcts = SKUS.map((_,i)=> opening[i]>0 ? Math.round(totals[i]/opening[i]*100) : 0);
  const avgPct = pcts.reduce((a,b)=>a+b,0)/pcts.length;
  const colors=["#2563C7","#E8760A","#6D28D9","#0A7A45","#009EB4","#C0241E","#92400E","#0F766E"];
  const R=45, C=2*Math.PI*R;
  let offset=0;
  const total=totals.reduce((a,b)=>a+b,0)||1;
  let segs="";
  totals.forEach((v,i)=>{
    const l=(v/total)*C;
    segs+=`<circle cx="60" cy="60" r="${R}" fill="none" stroke="${colors[i]}" stroke-width="18" stroke-dasharray="${l} ${C-l}" stroke-dashoffset="${-offset+C*0.25}" style="transition:stroke-dasharray .5s"/>`;
    offset+=l;
  });
  document.getElementById("donut-svg").innerHTML = segs +
    `<text x="60" y="56" text-anchor="middle" font-size="12" font-weight="700" fill="#0B1E45">${Math.round(avgPct)}%</text>
     <text x="60" y="69" text-anchor="middle" font-size="8" fill="#9AA3BB">avg sell-thru</text>`;
  document.getElementById("donut-legend").innerHTML = SKUS.map((s,i)=>`
    <div class="dl-item">
      <div class="dl-dot" style="background:${colors[i]}"></div>
      <div class="dl-name">${s.name.split("(")[0].trim()}</div>
      <div class="dl-val">${pcts[i]}%</div>
    </div>
  `).join("");
}

function buildDashTable(){
  const tbody = document.getElementById("dash-tbody");
  const recent = submissions.slice(-10).reverse();
  if(!recent.length){ tbody.innerHTML='<tr><td colspan="9" style="text-align:center;padding:24px;color:var(--gray3)">No submissions yet.</td></tr>'; return; }
  tbody.innerHTML = recent.map(r=>`
    <tr>
      <td><code style="font-size:11px;color:var(--gray3)">${r.uid}</code></td>
      <td><strong>${r.promoterName||"—"}</strong></td>
      <td>${r.customerName||"—"}</td>
      <td>${r.parish||"—"}</td>
      <td>${r.promoStart||"—"}</td>
      <td><strong>${r.totalUnits}</strong></td>
      <td>
        <div class="progress-bar" style="width:80px;display:inline-block;vertical-align:middle;margin-right:6px">
          <div class="pb-fill" style="width:${Math.min(100,r.sellThruPct)}%;background:var(--green)"></div>
        </div>${r.sellThruPct}%
      </td>
      <td><span class="status-badge ${r.status==="Completed"?"sb-green":r.status==="Cancelled"?"sb-red":"sb-orange"}">${r.status}</span></td>
      <td><button class="btn btn-outline btn-sm" onclick="viewReport('${r.uid}')">View</button></td>
    </tr>
  `).join("");
}

function buildAllReportsTable(filter={}){
  let filtered = submissions.filter(r=>{
    if(filter.search && !JSON.stringify(r).toLowerCase().includes(filter.search.toLowerCase())) return false;
    if(filter.parish && r.parish !== filter.parish) return false;
    if(filter.status && r.status !== filter.status) return false;
    return true;
  });
  document.getElementById("report-count").textContent = filtered.length;
  const tbody = document.getElementById("all-reports-tbody");
  if(!filtered.length){ tbody.innerHTML='<tr><td colspan="11" style="text-align:center;padding:24px;color:var(--gray3)">No reports found.</td></tr>'; return; }
  tbody.innerHTML = filtered.map(r=>`
    <tr>
      <td><code style="font-size:11px;color:var(--gray3)">${r.uid}</code></td>
      <td>${r.promoterName||"—"}</td>
      <td>${r.customerName||"—"}</td>
      <td>${r.parish||"—"}</td>
      <td>${r.promoStart||"—"}</td>
      <td>${r.promoDays||"—"}</td>
      <td><strong>${r.totalUnits}</strong></td>
      <td>${r.sellThruPct}%</td>
      <td style="font-size:11px">${new Date(r.submittedAt).toLocaleString("en-JM")}</td>
      <td><span class="status-badge ${r.status==="Completed"?"sb-green":r.status==="Cancelled"?"sb-red":"sb-orange"}">${r.status}</span></td>
      <td style="display:flex;gap:4px">
        <button class="btn btn-outline btn-sm" onclick="viewReport('${r.uid}')">View</button>
        <button class="btn btn-outline btn-sm" onclick="deleteReport('${r.uid}')">🗑</button>
      </td>
    </tr>
  `).join("");
}

function buildLeaderboard(){
  const leaderMap = {};
  submissions.forEach(r=>{
    if(!r.promoterName) return;
    if(!leaderMap[r.promoterName]) leaderMap[r.promoterName]={name:r.promoterName,units:0,reports:0,stores:new Set()};
    leaderMap[r.promoterName].units += r.totalUnits;
    leaderMap[r.promoterName].reports++;
    leaderMap[r.promoterName].stores.add(r.customerName);
  });
  const ranked = Object.values(leaderMap).sort((a,b)=>b.units-a.units);
  const cont = document.getElementById("leaderboard-wrap");
  if(!ranked.length){ cont.innerHTML='<div style="padding:24px;text-align:center;color:var(--gray3);font-size:13px">No data yet.</div>'; return; }
  cont.innerHTML = ranked.map((p,i)=>`
    <div class="lb-item">
      <div class="lb-rank ${i===0?"r1":i===1?"r2":i===2?"r3":""}">${i===0?"🥇":i===1?"🥈":i===2?"🥉":"#"+(i+1)}</div>
      <div class="lb-avatar">${p.name.split(" ").map(n=>n[0]).join("").substring(0,2)}</div>
      <div class="lb-info">
        <div class="lb-name">${p.name}</div>
        <div class="lb-sub">${p.reports} report${p.reports!==1?"s":""} · ${p.stores.size} store${p.stores.size!==1?"s":""}</div>
      </div>
      <div>
        <div class="lb-score">${p.units.toLocaleString()}</div>
        <div style="font-size:10px;color:var(--gray3)">units sold</div>
      </div>
    </div>
  `).join("");
}

function buildAnalyticsCards(){
  // SKU performance
  const skuTotals = SKUS.map((_,i)=>submissions.reduce((s,r)=>s+(r.totalSold[i]||0),0));
  const maxSku = Math.max(...skuTotals,1);
  document.getElementById("sku-perf-rows").innerHTML = SKUS.map((s,i)=>`
    <div class="metric-row">
      <div>
        <div class="mr-label">${s.name}</div>
        <div class="mr-bar"><div class="mrb-fill" style="width:${Math.round(skuTotals[i]/maxSku*100)}%"></div></div>
      </div>
      <div class="mr-val">${skuTotals[i].toLocaleString()} u</div>
    </div>
  `).join("");

  // Sell-through
  const skuOpen = SKUS.map((_,i)=>submissions.reduce((s,r)=>s+(r.opening[i]||0),0));
  document.getElementById("sellthru-rows").innerHTML = SKUS.map((s,i)=>{
    const pct = skuOpen[i]>0 ? Math.round(skuTotals[i]/skuOpen[i]*100) : 0;
    return `
    <div class="metric-row">
      <div>
        <div class="mr-label">${s.name}</div>
        <div class="mr-bar"><div class="mrb-fill" style="width:${pct}%;background:${pct>=80?"var(--green)":pct>=50?"var(--orange)":"var(--red)"}"></div></div>
      </div>
      <div class="mr-val" style="color:${pct>=80?"var(--green)":pct>=50?"var(--orange)":"var(--red)"}">${pct}%</div>
    </div>`;
  }).join("");

  // Competition intel
  const allComp = submissions.flatMap(r=>r.competitionLog||[]);
  const byBrand = {};
  allComp.forEach(c=>{ if(c.brand){ byBrand[c.brand]=(byBrand[c.brand]||0)+1; }});
  const compSorted = Object.entries(byBrand).sort((a,b)=>b[1]-a[1]).slice(0,8);
  document.getElementById("comp-intel-rows").innerHTML = compSorted.length
    ? compSorted.map(([b,n])=>`<div class="metric-row"><div class="mr-label">${b}</div><div class="mr-val">${n} entries</div></div>`).join("")
    : '<div style="color:var(--gray3);font-size:13px">No competitor data logged yet</div>';

  // Parish coverage
  const parishMap = {};
  submissions.forEach(r=>{ if(r.parish){ parishMap[r.parish]=(parishMap[r.parish]||{count:0,units:0}); parishMap[r.parish].count++; parishMap[r.parish].units+=r.totalUnits; }});
  const parishSorted = Object.entries(parishMap).sort((a,b)=>b[1].units-a[1].units);
  document.getElementById("parish-rows").innerHTML = parishSorted.length
    ? parishSorted.map(([p,v])=>`<div class="metric-row"><div class="mr-label">${p}</div><div class="mr-val">${v.units.toLocaleString()} u</div></div>`).join("")
    : '<div style="color:var(--gray3);font-size:13px">No parish data yet</div>';
}

function buildSettingsSKUs(){
  document.getElementById("settings-sku-list").innerHTML = SKUS.map(s=>`
    <div style="display:flex;align-items:center;gap:10px;padding:8px 12px;background:var(--gray0);border-radius:6px;font-size:13px">
      <span style="flex:1;font-weight:600">${s.name}</span>
      <span style="color:var(--gray3)">${s.uom}</span>
      <span style="font-family:var(--font-mono);color:var(--gray4)">${s.upc} units/case</span>
      <span style="font-family:var(--font-mono);color:var(--navy)">J$${s.price.toFixed(2)}/unit</span>
    </div>
  `).join("");
}

// ── REPORT VIEWER ──────────────────────────────────────────
function viewReport(uid){
  const r = submissions.find(x=>x.uid===uid);
  if(!r) return;
  document.getElementById("modal-title").textContent = "Report: " + r.uid;
  document.getElementById("modal-body").innerHTML = `
    <div style="display:grid;gap:12px;font-size:13px">
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
        <div><strong>Promoter:</strong> ${r.promoterName||"—"}</div>
        <div><strong>Store:</strong> ${r.customerName||"—"}</div>
        <div><strong>Parish:</strong> ${r.parish||"—"}</div>
        <div><strong>Dates:</strong> ${r.promoStart||"—"} to ${r.promoEnd||"—"}</div>
        <div><strong>Status:</strong> ${r.status||"—"}</div>
        <div><strong>Submitted:</strong> ${new Date(r.submittedAt).toLocaleString("en-JM")}</div>
        <div><strong>Total Units Sold:</strong> <span style="color:var(--green);font-weight:700">${r.totalUnits}</span></div>
        <div><strong>Sell-Through:</strong> <span style="color:var(--green);font-weight:700">${r.sellThruPct}%</span></div>
      </div>
      <hr>
      <div><strong>SKU Breakdown:</strong><br>
        ${SKUS.map((s,i)=>`${s.name}: <strong>${r.totalSold[i]||0}</strong> units sold`).join(" | ")}
      </div>
      ${r.findings ? `<div><strong>Findings:</strong><br>${r.findings}</div>`:""}
      ${r.recommendation ? `<div><strong>Recommendation:</strong><br>${r.recommendation}</div>`:""}
      ${r.immediateIssues ? `<div style="background:var(--red-lt);padding:10px;border-radius:6px;border-left:3px solid var(--red)"><strong style="color:var(--red)">⚠️ Issues Flagged:</strong><br>${r.immediateIssues}</div>`:""}
      ${r.competitionLog&&r.competitionLog.length ? `
        <div><strong>Competition Log (${r.competitionLog.length} entries):</strong><br>
          ${r.competitionLog.map(c=>`<div style="padding:4px 0;border-bottom:1px solid var(--gray1)">${c.day||""} · <strong>${c.brand||"—"}</strong> · ${c.type||""} · ${c.notes||""}</div>`).join("")}
        </div>`:""
      }
    </div>
  `;
  document.getElementById("modal-overlay").classList.add("open");
}

function closeModal(){ document.getElementById("modal-overlay").classList.remove("open"); }
document.getElementById("modal-overlay").addEventListener("click",e=>{ if(e.target===e.currentTarget) closeModal(); });

function deleteReport(uid){
  if(!confirm("Delete this report? This cannot be undone.")) return;
  submissions = submissions.filter(r=>r.uid!==uid);
  localStorage.setItem("ab_submissions",JSON.stringify(submissions));
  updateDashboard();
  showToast("🗑 Report deleted","var(--red)");
}

// ── FILTERS ────────────────────────────────────────────────
function filterReports(){
  buildAllReportsTable({
    search: document.getElementById("filter-search").value,
    parish: document.getElementById("filter-parish").value,
    status: document.getElementById("filter-status").value,
  });
}
function clearFilters(){
  ["filter-search","filter-parish","filter-status","filter-date-from","filter-date-to"].forEach(id=>{
    const el=document.getElementById(id); if(el) el.value="";
  });
  filterReports();
}

// ── EXPORTS ────────────────────────────────────────────────
function exportJSON(){
  const data = collectFormData(new Date());
  const blob = new Blob([JSON.stringify(data,null,2)],{type:"application/json"});
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = `promo-${formUID}.json`;
  a.click();
}

function exportAllCSV(){
  if(!submissions.length){ showToast("No data to export","var(--orange)"); return; }
  const headers = ["FormID","Promoter","Store","Parish","Start","End","Days","TotalUnits","SellThru","Status","Submitted","Findings","Issues"];
  const rows = submissions.map(r=>[
    r.uid, r.promoterName, r.customerName, r.parish,
    r.promoStart, r.promoEnd, r.promoDays, r.totalUnits, r.sellThruPct+"%",
    r.status, new Date(r.submittedAt).toLocaleString("en-JM"),
    (r.findings||"").replace(/,/g," "), (r.immediateIssues||"").replace(/,/g," ")
  ]);
  const csv = [headers, ...rows].map(r=>r.map(v=>`"${v}"`).join(",")).join("\n");
  const blob = new Blob([csv],{type:"text/csv"});
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = `alcobina-pings-reports-${Date.now()}.csv`;
  a.click();
}

function clearAllData(){
  submissions = [];
  localStorage.removeItem("ab_submissions");
  updateDashboard();
  showToast("🗑 All data cleared","var(--red)");
}

// ── NAV ────────────────────────────────────────────────────
function showPage(id){
  document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
  document.querySelectorAll(".nav-item").forEach(n=>n.classList.remove("active"));
  document.getElementById("page-"+id).classList.add("active");
  const navMap = {form:0,preview:1,dashboard:2,analytics:3,leaderboard:4,reports:5,settings:6};
  const items = document.querySelectorAll(".nav-item");
  if(navMap[id]!==undefined) items[navMap[id]]?.classList.add("active");
  if(id==="reports") buildAllReportsTable();
}

function updateNavBadge(){ document.getElementById("nb-form").textContent = submissions.length; }

// ── TOAST ──────────────────────────────────────────────────
function showToast(msg, color="var(--green)"){
  const t = document.getElementById("toast");
  t.textContent = msg; t.style.background = color; t.style.display = "block";
  setTimeout(()=>{ t.style.display="none"; }, 3500);
}

// ── BOOT ──────────────────────────────────────────────────
document.addEventListener("DOMContentLoaded", init);
</script>
</body>
</html>
