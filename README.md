<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kasshistore — Digital Coupon 2026</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=DM+Sans:wght@300;400;500;700&display=swap" rel="stylesheet">
<style>
:root {
  --cyan:#00f5ff; --magenta:#ff3de8; --purple:#7b2fff;
  --bg:#04060f; --card:rgba(255,255,255,0.04);
  --border:rgba(255,255,255,0.1); --text:#e8eaf6;
  --muted:rgba(255,255,255,0.5); --green:#00e676; --radius:28px;
}
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
body{min-height:100vh;background:var(--bg);color:var(--text);font-family:'DM Sans',sans-serif;overflow-x:hidden}
#bgCanvas{position:fixed;inset:0;z-index:0;pointer-events:none}
.grid-overlay{position:fixed;inset:0;z-index:0;pointer-events:none;
  background-image:linear-gradient(rgba(0,245,255,0.04) 1px,transparent 1px),linear-gradient(90deg,rgba(0,245,255,0.04) 1px,transparent 1px);
  background-size:60px 60px;mask-image:radial-gradient(ellipse at center,black 20%,transparent 80%)}
.scanline{position:fixed;inset:0;z-index:0;pointer-events:none;
  background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.07) 2px,rgba(0,0,0,0.07) 4px)}

.wrapper{position:relative;z-index:1;max-width:900px;margin:0 auto;padding:32px 20px 80px}
.banner{text-align:center;padding:14px 20px;
  background:linear-gradient(90deg,rgba(0,245,255,0.08),rgba(255,61,232,0.08));
  border:1px solid rgba(0,245,255,0.18);border-radius:14px;
  font-family:'Orbitron',monospace;font-size:12px;letter-spacing:4px;color:var(--cyan);
  margin-bottom:28px;animation:bannerPulse 3s ease-in-out infinite}
@keyframes bannerPulse{0%,100%{border-color:rgba(0,245,255,0.18)}
  50%{border-color:rgba(0,245,255,0.5);box-shadow:0 0 18px rgba(0,245,255,0.12)}}

.card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);
  padding:36px;backdrop-filter:blur(30px);-webkit-backdrop-filter:blur(30px);
  position:relative;overflow:hidden;animation:slideUp 0.7s cubic-bezier(0.22,1,0.36,1) both;margin-bottom:20px}
.card::before{content:'';position:absolute;top:-1px;left:-1px;right:-1px;height:2px;
  background:linear-gradient(90deg,transparent,var(--cyan),var(--magenta),transparent);
  border-radius:var(--radius) var(--radius) 0 0}
@keyframes slideUp{from{opacity:0;transform:translateY(40px)}to{opacity:1;transform:translateY(0)}}

.logo{font-family:'Orbitron',monospace;font-size:42px;font-weight:900;
  background:linear-gradient(120deg,var(--cyan) 0%,var(--magenta) 100%);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
  line-height:1.1;filter:drop-shadow(0 0 28px rgba(0,245,255,0.3))}
.year-badge{display:inline-block;padding:4px 14px;
  background:linear-gradient(90deg,var(--cyan),var(--magenta));border-radius:99px;
  font-size:11px;font-weight:700;color:#04060f;font-family:'Orbitron',monospace;
  margin-bottom:10px;letter-spacing:2px}
.subtitle{color:var(--muted);font-size:14px;line-height:1.8;margin-top:8px}

.profile-wrap{display:flex;align-items:center;gap:20px;margin:24px 0;padding:20px;
  background:rgba(255,255,255,0.03);border:1px solid var(--border);border-radius:20px}
.avatar-ring{position:relative;width:84px;height:84px;flex-shrink:0}
.avatar-ring::before{content:'';position:absolute;inset:-3px;border-radius:50%;
  background:conic-gradient(var(--cyan),var(--magenta),var(--purple),var(--cyan));
  animation:spin 4s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.avatar-ring img{position:relative;z-index:1;width:100%;height:100%;border-radius:50%;
  object-fit:cover;background:#0d1124;border:3px solid var(--bg);
  animation:float 5s ease-in-out infinite;display:block}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-8px)}}
.welcome-name{font-family:'Orbitron',monospace;font-size:16px;font-weight:700;
  background:linear-gradient(90deg,var(--cyan),var(--magenta));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.welcome-sub{color:var(--muted);font-size:12px;margin-top:4px}

.promo-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:24px}
.promo-item{padding:16px;border-radius:16px;background:rgba(255,255,255,0.03);
  border:1px solid var(--border);transition:transform 0.2s,border-color 0.2s}
.promo-item:hover{transform:translateY(-2px);border-color:rgba(255,255,255,0.2)}
.promo-icon{font-size:24px;margin-bottom:8px}
.promo-label{font-size:11px;color:var(--muted);margin-bottom:3px}
.promo-value{font-family:'Orbitron',monospace;font-size:16px;font-weight:700}
.promo-item:nth-child(1) .promo-value{color:var(--cyan)}
.promo-item:nth-child(2) .promo-value{color:#c084fc}
.promo-item:nth-child(3) .promo-value{color:var(--magenta);font-size:13px}

.section-title{font-family:'Orbitron',monospace;font-size:11px;letter-spacing:3px;
  color:var(--muted);margin-bottom:14px;display:flex;align-items:center;gap:10px}
.section-title::after{content:'';flex:1;height:1px;background:var(--border)}

.input-wrap{position:relative;margin-bottom:10px}
.input-wrap input{width:100%;padding:14px 18px;background:rgba(255,255,255,0.06);
  border:1px solid var(--border);border-radius:14px;color:var(--text);font-size:14px;
  font-family:'DM Sans',sans-serif;outline:none;transition:border-color 0.2s,box-shadow 0.2s}
.input-wrap input:focus{border-color:rgba(0,245,255,0.5);box-shadow:0 0 0 3px rgba(0,245,255,0.08)}
.input-wrap input::placeholder{color:var(--muted)}

.btn{width:100%;padding:14px;border:none;border-radius:14px;font-size:14px;font-weight:700;
  font-family:'Orbitron',monospace;cursor:pointer;letter-spacing:1px;position:relative;
  overflow:hidden;transition:transform 0.15s,box-shadow 0.15s}
.btn-primary{background:linear-gradient(90deg,var(--cyan),var(--magenta));color:#04060f}
.btn-primary:hover{transform:translateY(-2px);box-shadow:0 8px 28px rgba(0,245,255,0.28)}
.btn-primary:active{transform:scale(0.98)}
.btn-primary::after{content:'';position:absolute;inset:0;
  background:linear-gradient(90deg,transparent,rgba(255,255,255,0.2),transparent);
  transform:translateX(-100%);transition:transform 0.5s}
.btn-primary:hover::after{transform:translateX(100%)}
.btn-sm{padding:7px 14px;font-size:11px;width:auto;letter-spacing:0.5px}
.btn-ghost{background:rgba(255,255,255,0.05);border:1px solid var(--border);color:var(--muted);font-size:12px}
.btn-ghost:hover{background:rgba(255,255,255,0.1);color:var(--text);transform:none;box-shadow:none}

.gender-row{display:flex;gap:10px;margin-bottom:10px}
.gender-btn{flex:1;padding:9px;border:1px solid var(--border);border-radius:10px;
  background:rgba(255,255,255,0.04);color:var(--muted);font-size:13px;
  font-family:'DM Sans',sans-serif;cursor:pointer;transition:all 0.2s;
  display:flex;align-items:center;justify-content:center;gap:5px}
.gender-btn.active{background:rgba(0,245,255,0.1);border-color:var(--cyan);color:var(--cyan)}

.result-box{margin-top:18px;padding:22px;background:rgba(255,255,255,0.04);
  border:1px solid var(--border);border-radius:20px;display:none;animation:slideUp 0.4s ease both}
.result-box.show{display:block}
.result-row{display:flex;align-items:center;gap:10px;padding:9px 0;
  border-bottom:1px solid rgba(255,255,255,0.06);font-size:14px}
.result-row:last-child{border-bottom:none}
.result-label{color:var(--muted);min-width:120px;font-size:13px}
.result-value{font-weight:600}

.coupon-visual{display:flex;flex-wrap:wrap;gap:7px;margin:14px 0}
.coupon-dot{width:34px;height:34px;border-radius:9px;display:flex;align-items:center;
  justify-content:center;font-size:16px;border:1px solid var(--border);
  background:rgba(255,255,255,0.03);transition:all 0.3s}
.coupon-dot.filled{background:linear-gradient(135deg,var(--cyan),var(--purple));
  border-color:var(--cyan);box-shadow:0 0 10px rgba(0,245,255,0.3);animation:dotPop 0.4s ease}
@keyframes dotPop{0%{transform:scale(0.5);opacity:0}70%{transform:scale(1.2)}100%{transform:scale(1);opacity:1}}

.reward-ready{padding:16px;border-radius:14px;
  background:linear-gradient(135deg,rgba(0,230,118,0.1),rgba(0,245,255,0.08));
  border:1px solid rgba(0,230,118,0.25);margin-top:12px;text-align:center}
.reward-title{font-family:'Orbitron',monospace;font-size:12px;color:var(--green);
  letter-spacing:2px;margin-bottom:8px}
.wa-btn{display:flex;align-items:center;justify-content:center;gap:10px;padding:14px;
  background:#25D366;color:white;border-radius:12px;text-decoration:none;font-weight:700;
  font-family:'Orbitron',monospace;font-size:11px;letter-spacing:1px;margin-top:12px;
  transition:transform 0.2s,box-shadow 0.2s}
.wa-btn:hover{transform:translateY(-2px);box-shadow:0 8px 22px rgba(37,211,102,0.4)}
.wa-btn svg{width:20px;height:20px;fill:white;flex-shrink:0}

.riwayat-item{padding:10px 14px;background:rgba(255,255,255,0.02);
  border:1px solid rgba(255,255,255,0.06);border-radius:10px;margin-top:7px;
  display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap;font-size:12px}
.ri-left{color:var(--muted);font-size:11px}
.ri-badge{padding:3px 10px;border-radius:99px;font-size:10px;font-weight:700;
  font-family:'Orbitron',monospace;background:rgba(0,230,118,0.1);
  border:1px solid rgba(0,230,118,0.3);color:var(--green)}

.alert{padding:11px 15px;border-radius:11px;font-size:13px;margin-top:10px;display:none;animation:slideUp 0.3s ease}
.alert.success{background:rgba(0,230,118,0.1);border:1px solid rgba(0,230,118,0.3);color:var(--green)}
.alert.error{background:rgba(255,61,232,0.08);border:1px solid rgba(255,61,232,0.3);color:var(--magenta)}
.alert.show{display:block}

/* ══════ ADMIN — subtle floating trigger ══════ */
.admin-trigger{position:fixed;bottom:22px;right:22px;z-index:100;
  width:34px;height:34px;border-radius:50%;background:rgba(255,255,255,0.04);
  border:1px solid rgba(255,255,255,0.07);cursor:pointer;
  display:flex;align-items:center;justify-content:center;font-size:14px;
  transition:all 0.25s;opacity:0.28;user-select:none}
.admin-trigger:hover{opacity:0.65;background:rgba(255,255,255,0.08)}

/* Overlay */
.admin-overlay{position:fixed;inset:0;z-index:200;display:none;align-items:flex-end;
  justify-content:center;background:rgba(0,0,0,0.65);backdrop-filter:blur(10px);padding:16px}
.admin-overlay.open{display:flex}
.admin-drawer{background:#070a18;border:1px solid rgba(123,47,255,0.28);
  border-radius:22px 22px 18px 18px;width:100%;max-width:700px;max-height:90vh;
  overflow-y:auto;padding:26px;animation:drawerUp 0.35s cubic-bezier(0.22,1,0.36,1);position:relative;
  scrollbar-width:thin;scrollbar-color:rgba(123,47,255,0.3) transparent}
.admin-drawer::before{content:'';position:absolute;top:-1px;left:-1px;right:-1px;height:2px;
  background:linear-gradient(90deg,transparent,var(--purple),var(--magenta),transparent);
  border-radius:22px 22px 0 0}
@keyframes drawerUp{from{opacity:0;transform:translateY(50px)}to{opacity:1;transform:translateY(0)}}
.drawer-handle{width:36px;height:3px;background:rgba(255,255,255,0.12);border-radius:2px;margin:0 auto 18px}
.close-btn{position:absolute;top:18px;right:18px;width:30px;height:30px;border-radius:50%;
  background:rgba(255,255,255,0.05);border:1px solid var(--border);cursor:pointer;
  display:flex;align-items:center;justify-content:center;color:var(--muted);font-size:16px;
  transition:all 0.2s;line-height:1}
.close-btn:hover{background:rgba(255,255,255,0.1);color:var(--text)}

.admin-logo{font-family:'Orbitron',monospace;font-size:20px;font-weight:900;
  background:linear-gradient(90deg,var(--purple),var(--magenta));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:4px}

/* Admin tabs */
.admin-tabs{display:flex;gap:7px;margin-bottom:16px;flex-wrap:wrap}
.tab-btn{padding:7px 14px;border:1px solid var(--border);border-radius:99px;font-size:11px;
  font-family:'Orbitron',monospace;letter-spacing:0.5px;cursor:pointer;background:transparent;
  color:var(--muted);transition:all 0.2s}
.tab-btn.active{background:rgba(123,47,255,0.18);border-color:var(--purple);color:#c084fc}
.tab-pane{display:none}
.tab-pane.active{display:block}

.form-section{padding:16px;background:rgba(255,255,255,0.03);
  border:1px solid rgba(255,255,255,0.06);border-radius:14px;margin-bottom:12px}
.form-section h3{font-family:'Orbitron',monospace;font-size:10px;letter-spacing:2px;
  color:var(--cyan);margin-bottom:12px}

/* Admin inputs */
.admin-drawer .input-wrap input{padding:12px 14px;font-size:13px}

/* User list */
.user-list{max-height:320px;overflow-y:auto;scrollbar-width:thin;scrollbar-color:rgba(0,245,255,0.2) transparent}
.user-card{display:flex;align-items:center;gap:11px;padding:11px 13px;
  background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.06);
  border-radius:11px;margin-bottom:7px;transition:border-color 0.2s}
.user-card:hover{border-color:rgba(0,245,255,0.18)}
.user-card img{width:36px;height:36px;border-radius:50%;background:#111;border:2px solid rgba(0,245,255,0.15)}
.user-card-info{flex:1;min-width:0}
.user-card-name{font-weight:600;font-size:13px}
.user-card-meta{font-size:11px;color:var(--muted);margin-top:1px}
.coupon-pill{padding:4px 10px;border-radius:99px;font-family:'Orbitron',monospace;
  font-size:10px;white-space:nowrap;border:1px solid;margin-left:auto}
.cp-normal{background:rgba(0,245,255,0.07);border-color:rgba(0,245,255,0.2);color:var(--cyan)}
.cp-ready{background:rgba(0,230,118,0.1);border-color:rgba(0,230,118,0.3);color:var(--green)}

/* Redeem cards */
.redeem-card{padding:14px;background:rgba(255,255,255,0.03);
  border:1px solid rgba(255,255,255,0.06);border-radius:13px;margin-bottom:10px}
.redeem-top{display:flex;align-items:center;gap:11px;margin-bottom:12px}
.redeem-top img{width:36px;height:36px;border-radius:50%;background:#111;border:2px solid rgba(255,61,232,0.2)}
.rname{font-weight:600;font-size:13px}
.rmeta{font-size:11px;color:var(--muted);margin-top:2px}
.redeem-bottom{display:flex;gap:10px;align-items:center;flex-wrap:wrap}
.redeem-bottom select{flex:1;min-width:160px;padding:9px 12px;background:rgba(255,255,255,0.06);
  border:1px solid var(--border);border-radius:10px;color:var(--text);font-size:12px;
  font-family:'DM Sans',sans-serif;outline:none;cursor:pointer;
  -webkit-appearance:none;appearance:none;
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='10' height='10' fill='%23888' viewBox='0 0 16 16'%3E%3Cpath d='M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z'/%3E%3C/svg%3E");
  background-repeat:no-repeat;background-position:right 10px center}
.redeem-bottom select:focus{border-color:rgba(0,245,255,0.4);box-shadow:0 0 0 2px rgba(0,245,255,0.08)}
.redeem-bottom select option{background:#0d0f1f}
.btn-confirm{padding:8px 16px;border:none;border-radius:99px;font-size:11px;font-weight:700;
  font-family:'Orbitron',monospace;cursor:pointer;
  background:linear-gradient(90deg,var(--green),#00c853);color:#04060f;
  transition:transform 0.15s,box-shadow 0.15s;letter-spacing:0.5px;white-space:nowrap}
.btn-confirm:hover{transform:scale(1.04);box-shadow:0 4px 14px rgba(0,230,118,0.35)}

/* Log */
.log-item{padding:10px 13px;border-radius:9px;margin-bottom:7px;font-size:12px;
  background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.05);
  display:flex;justify-content:space-between;align-items:center;gap:8px;flex-wrap:wrap}
.log-time{color:var(--muted);font-size:10px;white-space:nowrap}
.log-badge{padding:3px 9px;border-radius:99px;font-size:10px;font-weight:700;
  font-family:'Orbitron',monospace;background:rgba(0,230,118,0.1);
  border:1px solid rgba(0,230,118,0.3);color:var(--green);white-space:nowrap}

.footer-bar{text-align:center;color:rgba(255,255,255,0.2);font-size:10px;
  font-family:'Orbitron',monospace;letter-spacing:3px;padding-top:8px}

@media(max-width:640px){
  .promo-grid{grid-template-columns:1fr 1fr}
  .logo{font-size:30px}
  .card{padding:22px}
  .admin-drawer{border-radius:18px 18px 0 0;padding:20px}
  .promo-item:nth-child(3){grid-column:1 / -1}
}
</style>
</head>
<body>
<canvas id="bgCanvas"></canvas>
<div class="grid-overlay"></div>
<div class="scanline"></div>

<div class="wrapper">
  <div class="banner">⚡ KASSHISTORE DIGITAL COUPON SYSTEM 2026 — KUMPULKAN &amp; TUKARKAN HADIAHMU ⚡</div>

  <!-- CUSTOMER CARD -->
  <div class="card">
    <div class="year-badge">SEASON 2026</div>
    <div class="logo">Kasshistore</div>
    <p class="subtitle">Kumpulkan kupon dari setiap pembelian, tukar setiap kelipatan 8 kupon!</p>

    <div class="profile-wrap">
      <div class="avatar-ring">
        <img id="profileImage" src="https://api.dicebear.com/7.x/adventurer/svg?seed=Guest&backgroundColor=0d1124" alt="Avatar">
      </div>
      <div>
        <div class="welcome-name" id="welcomeText">Selamat datang!</div>
        <div class="welcome-sub">Masukkan username untuk cek kuponu</div>
      </div>
    </div>

    <div class="promo-grid">
      <div class="promo-item">
        <div class="promo-icon">🛍️</div>
        <div class="promo-label">Per pembelian</div>
        <div class="promo-value">1 Kupon</div>
      </div>
      <div class="promo-item">
        <div class="promo-icon">🎯</div>
        <div class="promo-label">Tukar mulai dari</div>
        <div class="promo-value">8 Kupon</div>
      </div>
      <div class="promo-item">
        <div class="promo-icon">💸</div>
        <div class="promo-label">Per 8 kupon dapat</div>
        <div class="promo-value">Rp 6.000</div>
      </div>
    </div>

    <div class="section-title">CEK KUPON SAYA</div>
    <div class="input-wrap">
      <input type="text" id="searchName" placeholder="Masukkan username kamu..." autocomplete="off">
    </div>
    <button class="btn btn-primary" onclick="cekKupon()">✦ CEK KUPON ✦</button>
    <div id="alertCustomer" class="alert error"></div>

    <div class="result-box" id="hasilBox">
      <div class="section-title">HASIL PENCARIAN</div>
      <div class="result-row">
        <span class="result-label">👤 Username</span>
        <span class="result-value" id="hasilNama">—</span>
      </div>
      <div class="result-row">
        <span class="result-label">🎟️ Kupon aktif</span>
        <span class="result-value" id="hasilKupon">—</span>
      </div>
      <div class="result-row">
        <span class="result-label">✅ Total ditukar</span>
        <span class="result-value" id="hasilTukar">—</span>
      </div>
      <div id="couponDots" class="coupon-visual"></div>
      <div id="hasilSisa"></div>
      <div id="riwayatWrap" style="display:none;margin-top:14px">
        <div class="section-title" style="margin-bottom:8px">RIWAYAT PENUKARAN</div>
        <div id="riwayatList"></div>
      </div>
    </div>
  </div>

  <div class="footer-bar">© 2026 KASSHISTORE · DIGITAL COUPON SYSTEM · ALL RIGHTS RESERVED</div>
</div>

<!-- Admin trigger: tiny barely-visible lock at bottom-right -->
<div class="admin-trigger" id="adminTrigger" onclick="openAdmin()" title="">🔒</div>

<!-- ADMIN DRAWER OVERLAY -->
<div class="admin-overlay" id="adminOverlay" onclick="overlayBgClick(event)">
  <div class="admin-drawer" id="adminDrawer">
    <div class="drawer-handle"></div>
    <button class="close-btn" onclick="closeAdmin()">✕</button>

    <!-- Login -->
    <div id="adminLoginSection">
      <div class="admin-logo">Admin Panel</div>
      <p style="color:var(--muted);font-size:12px;margin-bottom:16px">Akses terbatas — masukkan password.</p>
      <div class="input-wrap"><input type="password" id="adminPassword" placeholder="Password..." autocomplete="off"></div>
      <button class="btn btn-primary" onclick="loginAdmin()">MASUK</button>
      <div id="alertAdmin" class="alert error"></div>
    </div>

    <!-- Content setelah login -->
    <div id="adminContent" style="display:none">
      <div style="display:fl
