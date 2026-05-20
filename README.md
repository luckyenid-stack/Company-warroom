<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>METALLUM — 世界金屬行情</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Noto+Sans+TC:wght@300;400;500;700&family=IBM+Plex+Mono:wght@300;400;500&family=Playfair+Display:ital,wght@0,700;1,400&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0D0D0E;
  --bg2:#141416;
  --bg3:#1A1A1C;
  --surface:#222226;
  --border:#2E2E33;
  --muted:#5A5A62;
  --text:#E8E6E0;
  --text2:#9A9890;
  --gold:#C9A84C;
  --gold2:#E8C76A;
  --silver:#B8BCC6;
  --copper:#C97A4C;
  --platinum:#8FA8C4;
  --green:#4CAF7D;
  --red:#E05555;
}
html{scroll-behavior:smooth}
body{
  background:var(--bg);
  color:var(--text);
  font-family:'Noto Sans TC',sans-serif;
  overflow-x:hidden;
  min-height:100vh;
}

/* ── TICKER ── */
.ticker{
  background:var(--bg2);
  border-bottom:1px solid var(--border);
  overflow:hidden;
  white-space:nowrap;
  padding:8px 0;
  position:relative;
}
.ticker::before,.ticker::after{
  content:'';position:absolute;top:0;bottom:0;width:60px;z-index:2;
}
.ticker::before{left:0;background:linear-gradient(to right,var(--bg2),transparent)}
.ticker::after{right:0;background:linear-gradient(to left,var(--bg2),transparent)}
.ticker-track{
  display:inline-flex;gap:0;
  animation:scroll 40s linear infinite;
}
@keyframes scroll{0%{transform:translateX(0)}100%{transform:translateX(-50%)}}
.tick-item{
  display:inline-flex;align-items:center;gap:10px;
  padding:0 32px;
  border-right:1px solid var(--border);
  font-family:'IBM Plex Mono',monospace;font-size:11px;
}
.tick-name{color:var(--text2);letter-spacing:0.08em}
.tick-price{font-weight:500;color:var(--text)}
.tick-chg.up{color:var(--green)}
.tick-chg.dn{color:var(--red)}

/* ── NAV ── */
nav{
  display:flex;align-items:center;justify-content:space-between;
  padding:0 48px;height:60px;
  border-bottom:1px solid var(--border);
  background:var(--bg);
  position:sticky;top:0;z-index:100;
}
.logo{
  font-family:'Bebas Neue',sans-serif;
  font-size:26px;letter-spacing:0.12em;
  color:var(--gold);
  display:flex;align-items:center;gap:12px;
}
.logo-icon{
  width:28px;height:28px;
  border:1.5px solid var(--gold);
  display:flex;align-items:center;justify-content:center;
  font-size:13px;color:var(--gold);
}
.logo-sub{
  font-family:'IBM Plex Mono',monospace;
  font-size:9px;color:var(--muted);
  letter-spacing:0.2em;font-weight:400;
  align-self:flex-end;margin-bottom:3px;
}
.nav-links{display:flex;gap:0;list-style:none}
.nav-links li a{
  font-size:11px;letter-spacing:0.1em;text-transform:uppercase;
  color:var(--muted);text-decoration:none;
  padding:0 18px;height:60px;
  display:flex;align-items:center;
  border-left:1px solid var(--border);
  transition:color 0.2s,background 0.2s;
}
.nav-links li a:hover{color:var(--gold);background:rgba(201,168,76,0.04)}
.nav-links li:last-child a{
  background:var(--gold);color:var(--bg);
  font-weight:500;border-left:none;
}
.nav-links li:last-child a:hover{background:var(--gold2)}

/* ── HERO GRID ── */
.hero{
  display:grid;
  grid-template-columns:1fr 340px;
  min-height:80vh;
  border-bottom:1px solid var(--border);
}
.hero-main{
  padding:64px 48px;
  border-right:1px solid var(--border);
  display:flex;flex-direction:column;justify-content:space-between;
  position:relative;overflow:hidden;
}
.hero-main::after{
  content:'Au';
  position:absolute;right:-20px;bottom:-60px;
  font-family:'Bebas Neue',sans-serif;
  font-size:320px;color:rgba(201,168,76,0.03);
  pointer-events:none;line-height:1;letter-spacing:-0.05em;
}
.hero-label{
  font-family:'IBM Plex Mono',monospace;
  font-size:10px;letter-spacing:0.25em;color:var(--muted);
  text-transform:uppercase;margin-bottom:28px;
  display:flex;align-items:center;gap:14px;
}
.hero-label::before{content:'';width:32px;height:1px;background:var(--gold)}
.hero-title{
  font-family:'Bebas Neue',sans-serif;
  font-size:clamp(56px,7vw,96px);
  line-height:0.95;letter-spacing:0.04em;
  color:var(--text);margin-bottom:6px;
}
.hero-title .accent{color:var(--gold)}
.hero-subtitle{
  font-family:'Playfair Display',serif;
  font-style:italic;font-size:18px;
  color:var(--text2);margin-bottom:36px;margin-top:12px;
  line-height:1.5;
}
.hero-desc{
  font-size:13px;line-height:1.9;
  color:var(--text2);max-width:440px;margin-bottom:40px;
}
.hero-actions{display:flex;gap:14px}
.btn-gold{
  background:var(--gold);color:var(--bg);
  font-family:'IBM Plex Mono',monospace;
  font-size:11px;font-weight:500;letter-spacing:0.14em;
  text-transform:uppercase;padding:13px 26px;
  border:none;cursor:pointer;transition:background 0.2s;
  text-decoration:none;display:inline-block;
}
.btn-gold:hover{background:var(--gold2)}
.btn-outline{
  background:transparent;color:var(--text2);
  border:1px solid var(--border);
  font-family:'IBM Plex Mono',monospace;
  font-size:11px;letter-spacing:0.14em;
  text-transform:uppercase;padding:13px 26px;
  cursor:pointer;transition:border-color 0.2s,color 0.2s;
  text-decoration:none;display:inline-block;
}
.btn-outline:hover{border-color:var(--gold);color:var(--gold)}

/* Hero right — featured metal */
.hero-side{display:flex;flex-direction:column}
.featured-metal{
  flex:1;padding:36px 28px;
  background:var(--bg2);
  display:flex;flex-direction:column;justify-content:flex-end;
  position:relative;overflow:hidden;
  border-bottom:1px solid var(--border);
}
.fm-bg{
  position:absolute;inset:0;
  background:radial-gradient(ellipse at 60% 20%, rgba(201,168,76,0.07) 0%, transparent 60%);
}
.fm-grid{
  position:absolute;inset:0;
  background-image:
    repeating-linear-gradient(0deg,transparent,transparent 39px,rgba(201,168,76,0.04) 39px,rgba(201,168,76,0.04) 40px),
    repeating-linear-gradient(90deg,transparent,transparent 39px,rgba(201,168,76,0.04) 39px,rgba(201,168,76,0.04) 40px);
}
.fm-label{
  font-family:'IBM Plex Mono',monospace;
  font-size:9px;letter-spacing:0.2em;color:var(--muted);
  text-transform:uppercase;margin-bottom:16px;position:relative;z-index:1;
  display:flex;align-items:center;gap:8px;
}
.live-badge{
  background:var(--red);color:#fff;
  font-size:8px;padding:2px 7px;letter-spacing:0.12em;
}
.fm-symbol{
  font-family:'Bebas Neue',sans-serif;
  font-size:72px;line-height:1;color:var(--gold);
  position:relative;z-index:1;margin-bottom:4px;
}
.fm-name{
  font-size:13px;color:var(--text2);
  position:relative;z-index:1;margin-bottom:20px;
  letter-spacing:0.06em;
}
.fm-price{
  font-family:'IBM Plex Mono',monospace;
  font-size:36px;font-weight:500;color:var(--text);
  position:relative;z-index:1;line-height:1;
}
.fm-unit{font-size:13px;color:var(--muted);margin-left:4px}
.fm-chg{
  font-family:'IBM Plex Mono',monospace;
  font-size:13px;color:var(--green);
  position:relative;z-index:1;margin-top:6px;
  display:flex;align-items:center;gap:8px;
}
.fm-chg.dn{color:var(--red)}
.sparkline{margin-top:20px;position:relative;z-index:1}
.sparkline svg{width:100%;height:48px}

/* Side stats */
.side-stats{display:grid;grid-template-columns:1fr 1fr}
.ss-cell{
  padding:20px;border-right:1px solid var(--border);
  border-bottom:1px solid var(--border);
}
.ss-cell:nth-child(2n){border-right:none}
.ss-cell:nth-child(3),.ss-cell:nth-child(4){border-bottom:none}
.ss-metal{font-family:'IBM Plex Mono',monospace;font-size:10px;letter-spacing:0.12em;color:var(--muted);margin-bottom:6px;text-transform:uppercase}
.ss-price{font-family:'IBM Plex Mono',monospace;font-size:18px;font-weight:500;color:var(--text);line-height:1;margin-bottom:4px}
.ss-chg{font-size:11px}
.ss-chg.up{color:var(--green)}.ss-chg.dn{color:var(--red)}

/* ── METALS TABLE ── */
.metals-section{padding:48px;border-bottom:1px solid var(--border)}
.sec-head{display:flex;align-items:baseline;justify-content:space-between;margin-bottom:28px}
.sec-title{
  font-family:'Bebas Neue',sans-serif;
  font-size:28px;letter-spacing:0.08em;color:var(--text);
}
.sec-title span{color:var(--gold)}
.sec-more{
  font-family:'IBM Plex Mono',monospace;
  font-size:10px;letter-spacing:0.14em;text-transform:uppercase;
  color:var(--muted);text-decoration:none;transition:color 0.2s;
}
.sec-more:hover{color:var(--gold)}

.metals-table{width:100%;border-collapse:collapse}
.metals-table thead tr{border-bottom:1px solid var(--border)}
.metals-table th{
  font-family:'IBM Plex Mono',monospace;
  font-size:9px;letter-spacing:0.18em;text-transform:uppercase;
  color:var(--muted);padding:0 12px 12px;text-align:left;
  font-weight:400;
}
.metals-table th:not(:first-child){text-align:right}
.metals-table tbody tr{
  border-bottom:1px solid rgba(46,46,51,0.6);
  cursor:pointer;transition:background 0.12s;
}
.metals-table tbody tr:hover{background:rgba(201,168,76,0.04)}
.metals-table tbody tr:last-child{border-bottom:none}
.metals-table td{padding:16px 12px;font-size:13px}
.metals-table td:not(:first-child){text-align:right;font-family:'IBM Plex Mono',monospace}
.metal-id{display:flex;align-items:center;gap:14px}
.metal-symbol{
  width:38px;height:38px;
  border:1px solid var(--border);
  display:flex;align-items:center;justify-content:center;
  font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:0.06em;
  flex-shrink:0;transition:border-color 0.2s;
}
.metals-table tbody tr:hover .metal-symbol{border-color:var(--gold)}
.metal-symbol.au{color:var(--gold)}
.metal-symbol.ag{color:var(--silver)}
.metal-symbol.cu{color:var(--copper)}
.metal-symbol.pt{color:var(--platinum)}
.metal-symbol.pd{color:#B89FC8}
.metal-symbol.rh{color:#7EC8C8}
.metal-symbol.al{color:#8FA8C4}
.metal-symbol.ni{color:#A0B89C}
.metal-name-zh{font-size:13px;font-weight:500;color:var(--text)}
.metal-name-en{font-size:11px;color:var(--muted);margin-top:2px;letter-spacing:0.04em}
.chg-up{color:var(--green)}.chg-dn{color:var(--red)}
.vol-bar-wrap{display:flex;align-items:center;gap:10px;justify-content:flex-end}
.vol-bar-bg{width:60px;height:3px;background:var(--border);position:relative}
.vol-bar-fill{position:absolute;left:0;top:0;bottom:0;background:var(--gold);opacity:0.6}

/* ── CATEGORY TABS ── */
.cat-tabs{display:flex;gap:0;margin-bottom:24px;border:1px solid var(--border);width:fit-content}
.cat-tab{
  font-family:'IBM Plex Mono',monospace;font-size:10px;
  letter-spacing:0.12em;text-transform:uppercase;
  padding:9px 18px;cursor:pointer;color:var(--muted);
  border-right:1px solid var(--border);transition:background 0.15s,color 0.15s;
  background:transparent;border-top:none;border-bottom:none;border-left:none;
}
.cat-tab:last-child{border-right:none}
.cat-tab.active{background:var(--gold);color:var(--bg);font-weight:500}
.cat-tab:not(.active):hover{background:rgba(201,168,76,0.07);color:var(--text)}

/* ── NEWS ── */
.news-section{
  display:grid;grid-template-columns:1fr 320px;
  border-bottom:1px solid var(--border);
}
.news-main{padding:48px;border-right:1px solid var(--border)}
.news-grid{display:flex;flex-direction:column;gap:0}
.news-item{
  display:grid;grid-template-columns:auto 1fr;
  gap:20px;padding:20px 0;
  border-bottom:1px solid rgba(46,46,51,0.6);
  cursor:pointer;
  transition:background 0.12s;
}
.news-item:first-child{padding-top:0}
.news-item:last-child{border-bottom:none;padding-bottom:0}
.news-item:hover{background:rgba(201,168,76,0.03)}
.news-num{
  font-family:'Bebas Neue',sans-serif;
  font-size:22px;color:var(--border);letter-spacing:0.04em;
  width:28px;text-align:right;margin-top:2px;flex-shrink:0;
}
.news-cat-tag{
  display:inline-flex;align-items:center;gap:5px;
  font-family:'IBM Plex Mono',monospace;font-size:9px;
  letter-spacing:0.14em;color:var(--muted);text-transform:uppercase;
  margin-bottom:7px;
}
.tag-dot{width:5px;height:5px;border-radius:50%;flex-shrink:0}
.news-headline{font-size:14px;font-weight:500;line-height:1.5;color:var(--text);margin-bottom:6px;transition:color 0.15s}
.news-item:hover .news-headline{color:var(--gold)}
.news-excerpt{font-size:12px;color:var(--muted);line-height:1.8;margin-bottom:8px}
.news-footer{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted);display:flex;gap:16px}

/* Market sentiment side */
.sentiment-panel{padding:36px 28px;background:var(--bg2)}
.sp-title{
  font-family:'IBM Plex Mono',monospace;font-size:9px;
  letter-spacing:0.2em;text-transform:uppercase;color:var(--muted);
  margin-bottom:24px;
}
.sentiment-meter{
  margin-bottom:28px;
  padding:20px;background:var(--bg3);border:1px solid var(--border);
}
.sm-label{font-size:11px;color:var(--text2);margin-bottom:10px}
.sm-bar{height:6px;background:var(--border);position:relative;margin-bottom:8px}
.sm-fill{height:100%;background:var(--green);transition:width 1s ease}
.sm-ends{display:flex;justify-content:space-between;font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);letter-spacing:0.08em}
.sentiment-score{
  font-family:'Bebas Neue',sans-serif;font-size:52px;
  line-height:1;color:var(--green);margin-bottom:4px;
}
.sentiment-verdict{font-size:12px;color:var(--text2)}

.regional-list{display:flex;flex-direction:column;gap:0}
.region-item{
  display:flex;justify-content:space-between;align-items:center;
  padding:12px 0;border-bottom:1px solid rgba(46,46,51,0.6);
}
.region-item:last-child{border-bottom:none}
.region-name{font-size:12px;color:var(--text2)}
.region-time{font-family:'IBM Plex Mono',monospace;font-size:11px;color:var(--muted)}
.region-status{font-family:'IBM Plex Mono',monospace;font-size:10px;padding:3px 8px;letter-spacing:0.08em}
.rs-open{background:rgba(76,175,125,0.12);color:var(--green)}
.rs-closed{background:rgba(90,90,98,0.3);color:var(--muted)}

/* ── FEATURES ── */
.features-section{
  display:grid;grid-template-columns:repeat(4,1fr);
  border-bottom:1px solid var(--border);
}
.feat-card{
  padding:36px 28px;
  border-right:1px solid var(--border);
  transition:background 0.2s;cursor:pointer;
}
.feat-card:last-child{border-right:none}
.feat-card:hover{background:rgba(201,168,76,0.04)}
.feat-icon{
  width:40px;height:40px;border:1px solid var(--border);
  display:flex;align-items:center;justify-content:center;
  font-size:16px;color:var(--gold);margin-bottom:18px;
  transition:border-color 0.2s;
}
.feat-card:hover .feat-icon{border-color:var(--gold)}
.feat-title{font-size:14px;font-weight:500;color:var(--text);margin-bottom:8px}
.feat-desc{font-size:12px;color:var(--muted);line-height:1.8}

/* ── SUBSCRIBE ── */
.subscribe{
  padding:64px 48px;
  display:grid;grid-template-columns:1fr 1fr;
  gap:60px;align-items:center;
  background:var(--bg2);border-bottom:1px solid var(--border);
}
.sub-eyebrow{
  font-family:'IBM Plex Mono',monospace;font-size:9px;
  letter-spacing:0.22em;text-transform:uppercase;
  color:var(--gold);margin-bottom:16px;
}
.sub-title{
  font-family:'Bebas Neue',sans-serif;
  font-size:38px;letter-spacing:0.06em;color:var(--text);
  line-height:1.1;margin-bottom:14px;
}
.sub-desc{font-size:13px;color:var(--text2);line-height:1.8}
.sub-form{display:flex;flex-direction:column;gap:12px}
.sub-row{display:flex;gap:0}
.sub-input{
  flex:1;background:var(--bg3);border:1px solid var(--border);
  border-right:none;color:var(--text);
  font-family:'Noto Sans TC',sans-serif;font-size:13px;
  padding:13px 18px;outline:none;transition:border-color 0.2s;
}
.sub-input:focus{border-color:var(--gold)}
.sub-input::placeholder{color:var(--muted)}
.sub-btn{
  background:var(--gold);color:var(--bg);border:none;
  font-family:'IBM Plex Mono',monospace;font-size:11px;
  font-weight:500;letter-spacing:0.14em;text-transform:uppercase;
  padding:13px 22px;cursor:pointer;transition:background 0.2s;white-space:nowrap;
}
.sub-btn:hover{background:var(--gold2)}
.sub-note{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted);letter-spacing:0.06em}

/* ── FOOTER ── */
footer{
  padding:40px 48px 28px;
  border-top:1px solid var(--border);
}
.footer-top{
  display:grid;grid-template-columns:1.4fr repeat(3,1fr);
  gap:40px;margin-bottom:40px;
}
.footer-logo{
  font-family:'Bebas Neue',sans-serif;
  font-size:22px;letter-spacing:0.1em;color:var(--gold);
  display:block;margin-bottom:12px;
}
.footer-tagline{font-size:12px;color:var(--muted);line-height:1.8}
.footer-col-title{
  font-family:'IBM Plex Mono',monospace;font-size:9px;
  letter-spacing:0.2em;text-transform:uppercase;color:var(--muted);
  display:block;margin-bottom:16px;
}
.footer-links{list-style:none;display:flex;flex-direction:column;gap:10px}
.footer-links a{font-size:12px;color:var(--text2);text-decoration:none;transition:color 0.2s}
.footer-links a:hover{color:var(--gold)}
.footer-bottom{
  padding-top:24px;border-top:1px solid var(--border);
  display:flex;justify-content:space-between;align-items:center;
}
.footer-copy{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted)}
.footer-legal{display:flex;gap:24px}
.footer-legal a{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted);text-decoration:none;transition:color 0.2s}
.footer-legal a:hover{color:var(--gold)}

/* ── SCROLL FADE ── */
.fade-in{opacity:0;transform:translateY(20px);transition:opacity 0.55s ease,transform 0.55s ease}
.fade-in.vis{opacity:1;transform:none}
.fd2{transition-delay:0.1s}.fd3{transition-delay:0.2s}.fd4{transition-delay:0.3s}
</style>
</head>
<body>

<!-- TICKER -->
<div class="ticker">
  <div class="ticker-track" id="ticker">
    <span class="tick-item"><span class="tick-name">AU/USD</span><span class="tick-price">$3,342.40</span><span class="tick-chg up">▲ +0.84%</span></span>
    <span class="tick-item"><span class="tick-name">AG/USD</span><span class="tick-price">$33.18</span><span class="tick-chg up">▲ +1.23%</span></span>
    <span class="tick-item"><span class="tick-name">CU/USD</span><span class="tick-price">$9,842</span><span class="tick-chg dn">▼ −0.47%</span></span>
    <span class="tick-item"><span class="tick-name">PT/USD</span><span class="tick-price">$1,024</span><span class="tick-chg up">▲ +0.31%</span></span>
    <span class="tick-item"><span class="tick-name">PD/USD</span><span class="tick-price">$1,148</span><span class="tick-chg dn">▼ −1.02%</span></span>
    <span class="tick-item"><span class="tick-name">RH/USD</span><span class="tick-price">$4,660</span><span class="tick-chg up">▲ +0.55%</span></span>
    <span class="tick-item"><span class="tick-name">AL/USD</span><span class="tick-price">$2,468</span><span class="tick-chg dn">▼ −0.18%</span></span>
    <span class="tick-item"><span class="tick-name">NI/USD</span><span class="tick-price">$16,240</span><span class="tick-chg up">▲ +0.72%</span></span>
    <span class="tick-item"><span class="tick-name">ZN/USD</span><span class="tick-price">$2,886</span><span class="tick-chg dn">▼ −0.33%</span></span>
    <span class="tick-item"><span class="tick-name">PB/USD</span><span class="tick-price">$1,972</span><span class="tick-chg up">▲ +0.12%</span></span>
    <span class="tick-item"><span class="tick-name">AU/USD</span><span class="tick-price">$3,342.40</span><span class="tick-chg up">▲ +0.84%</span></span>
    <span class="tick-item"><span class="tick-name">AG/USD</span><span class="tick-price">$33.18</span><span class="tick-chg up">▲ +1.23%</span></span>
    <span class="tick-item"><span class="tick-name">CU/USD</span><span class="tick-price">$9,842</span><span class="tick-chg dn">▼ −0.47%</span></span>
    <span class="tick-item"><span class="tick-name">PT/USD</span><span class="tick-price">$1,024</span><span class="tick-chg up">▲ +0.31%</span></span>
    <span class="tick-item"><span class="tick-name">PD/USD</span><span class="tick-price">$1,148</span><span class="tick-chg dn">▼ −1.02%</span></span>
    <span class="tick-item"><span class="tick-name">RH/USD</span><span class="tick-price">$4,660</span><span class="tick-chg up">▲ +0.55%</span></span>
    <span class="tick-item"><span class="tick-name">AL/USD</span><span class="tick-price">$2,468</span><span class="tick-chg dn">▼ −0.18%</span></span>
    <span class="tick-item"><span class="tick-name">NI/USD</span><span class="tick-price">$16,240</span><span class="tick-chg up">▲ +0.72%</span></span>
    <span class="tick-item"><span class="tick-name">ZN/USD</span><span class="tick-price">$2,886</span><span class="tick-chg dn">▼ −0.33%</span></span>
    <span class="tick-item"><span class="tick-name">PB/USD</span><span class="tick-price">$1,972</span><span class="tick-chg up">▲ +0.12%</span></span>
  </div>
</div>

<!-- NAV -->
<nav>
  <div class="logo">
    <div class="logo-icon">M</div>
    METALLUM
    <span class="logo-sub">全球金屬行情</span>
  </div>
  <ul class="nav-links">
    <li><a href="#">現貨行情</a></li>
    <li><a href="#">期貨市場</a></li>
    <li><a href="#">市場分析</a></li>
    <li><a href="#">產業新聞</a></li>
    <li><a href="#">數據 API</a></li>
    <li><a href="#">免費訂閱</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-main">
    <div>
      <div class="hero-label">World Metals Exchange · Real-time Data</div>
      <h1 class="hero-title">WORLD<br><span class="accent">METALS</span><br>MARKET</h1>
      <p class="hero-subtitle">世界頂尖金屬行情資訊平台</p>
      <p class="hero-desc">蒐羅全球貴金屬、基本金屬與稀有金屬的即時現貨與期貨行情，結合深度產業分析、礦業動態與市場情緒指標，為交易者、投資人與產業研究者提供最精準的決策依據。</p>
      <div class="hero-actions">
        <a href="#" class="btn-gold">查看即時行情</a>
        <a href="#" class="btn-outline">瀏覽市場報告</a>
      </div>
    </div>
    <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:0;margin-top:48px;padding-top:32px;border-top:1px solid var(--border)">
      <div style="padding-right:28px;border-right:1px solid var(--border)">
        <div style="font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:0.16em;color:var(--muted);text-transform:uppercase;margin-bottom:8px">收錄金屬品種</div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:42px;color:var(--gold);line-height:1">84<span style="font-size:22px;color:var(--muted)">+</span></div>
      </div>
      <div style="padding:0 28px;border-right:1px solid var(--border)">
        <div style="font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:0.16em;color:var(--muted);text-transform:uppercase;margin-bottom:8px">交易所覆蓋</div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:42px;color:var(--gold);line-height:1">32</div>
      </div>
      <div style="padding-left:28px">
        <div style="font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:0.16em;color:var(--muted);text-transform:uppercase;margin-bottom:8px">更新頻率</div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:42px;color:var(--gold);line-height:1">15<span style="font-size:18px;color:var(--muted)">sec</span></div>
      </div>
    </div>
  </div>

  <div class="hero-side">
    <div class="featured-metal">
      <div class="fm-bg"></div>
      <div class="fm-grid"></div>
      <div class="fm-label">
        <span class="live-badge">LIVE</span>
        精選金屬 · 黃金
      </div>
      <div class="fm-symbol">AU</div>
      <div class="fm-name">黃金 Gold · 倫敦現貨</div>
      <div class="fm-price" id="gold-price">3,342<span class="fm-unit">USD/oz</span></div>
      <div class="fm-chg up" id="gold-chg">▲ +27.80 &nbsp;(+0.84%)</div>
      <div class="sparkline">
        <svg viewBox="0 0 280 48" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none">
          <polyline points="0,38 28,35 56,40 84,32 112,28 140,30 168,22 196,18 224,14 252,10 280,6" style="fill:none;stroke:#C9A84C;stroke-width:1.5"/>
          <polygon points="0,38 28,35 56,40 84,32 112,28 140,30 168,22 196,18 224,14 252,10 280,6 280,48 0,48" style="fill:rgba(201,168,76,0.1);stroke:none"/>
        </svg>
      </div>
    </div>
    <div class="side-stats">
      <div class="ss-cell">
        <div class="ss-metal">銀 AG</div>
        <div class="ss-price">$33.18</div>
        <div class="ss-chg up">▲ +1.23%</div>
      </div>
      <div class="ss-cell">
        <div class="ss-metal">銅 CU</div>
        <div class="ss-price">$9,842</div>
        <div class="ss-chg dn">▼ −0.47%</div>
      </div>
      <div class="ss-cell">
        <div class="ss-metal">鉑 PT</div>
        <div class="ss-price">$1,024</div>
        <div class="ss-chg up">▲ +0.31%</div>
      </div>
      <div class="ss-cell">
        <div class="ss-metal">鈀 PD</div>
        <div class="ss-price">$1,148</div>
        <div class="ss-chg dn">▼ −1.02%</div>
      </div>
    </div>
  </div>
</section>

<!-- METALS TABLE -->
<section class="metals-section fade-in">
  <div class="sec-head">
    <h2 class="sec-title">即時 <span>金屬行情</span></h2>
    <a href="#" class="sec-more">完整行情表 →</a>
  </div>
  <div class="cat-tabs">
    <button class="cat-tab active">全部</button>
    <button class="cat-tab">貴金屬</button>
    <button class="cat-tab">基本金屬</button>
    <button class="cat-tab">稀有金屬</button>
    <button class="cat-tab">期貨</button>
  </div>
  <table class="metals-table">
    <thead>
      <tr>
        <th>金屬</th>
        <th>現貨價格</th>
        <th>漲跌</th>
        <th>漲跌幅</th>
        <th>今日最高</th>
        <th>今日最低</th>
        <th>成交量</th>
      </tr>
    </thead>
    <tbody id="metals-body">
      <tr>
        <td><div class="metal-id"><div class="metal-symbol au">AU</div><div><div class="metal-name-zh">黃金</div><div class="metal-name-en">Gold · LBMA</div></div></div></td>
        <td>$3,342.40</td>
        <td class="chg-up">+27.80</td>
        <td class="chg-up">+0.84%</td>
        <td>$3,358.10</td>
        <td>$3,310.20</td>
        <td><div class="vol-bar-wrap"><span>284K oz</span><div class="vol-bar-bg"><div class="vol-bar-fill" style="width:90%"></div></div></div></td>
      </tr>
      <tr>
        <td><div class="metal-id"><div class="metal-symbol ag">AG</div><div><div class="metal-name-zh">白銀</div><div class="metal-name-en">Silver · LBMA</div></div></div></td>
        <td>$33.18</td>
        <td class="chg-up">+0.40</td>
        <td class="chg-up">+1.23%</td>
        <td>$33.52</td>
        <td>$32.75</td>
        <td><div class="vol-bar-wrap"><span>8.4M oz</span><div class="vol-bar-bg"><div class="vol-bar-fill" style="width:75%"></div></div></div></td>
      </tr>
      <tr>
        <td><div class="metal-id"><div class="metal-symbol cu">CU</div><div><div class="metal-name-zh">銅</div><div class="metal-name-en">Copper · LME</div></div></div></td>
        <td>$9,842/t</td>
        <td class="chg-dn">−46.20</td>
        <td class="chg-dn">−0.47%</td>
        <td>$9,920</td>
        <td>$9,805</td>
        <td><div class="vol-bar-wrap"><span>142K t</span><div class="vol-bar-bg"><div class="vol-bar-fill" style="width:82%"></div></div></div></td>
      </tr>
      <tr>
        <td><div class="metal-id"><div class="metal-symbol pt">PT</div><div><div class="metal-name-zh">鉑金</div><div class="metal-name-en">Platinum · LBMA</div></div></div></td>
        <td>$1,024.50</td>
        <td class="chg-up">+3.20</td>
        <td class="chg-up">+0.31%</td>
        <td>$1,032</td>
        <td>$1,016</td>
        <td><div class="vol-bar-wrap"><span>48K oz</span><div class="vol-bar-bg"><div class="vol-bar-fill" style="width:38%"></div></div></div></td>
      </tr>
      <tr>
        <td><div class="metal-id"><div class="metal-symbol pd">PD</div><div><div class="metal-name-zh">鈀金</div><div class="metal-name-en">Palladium · LBMA</div></div></div></td>
        <td>$1,148.00</td>
        <td class="chg-dn">−11.80</td>
        <td class="chg-dn">−1.02%</td>
        <td>$1,168</td>
        <td>$1,140</td>
        <td><div class="vol-bar-wrap"><span>22K oz</span><div class="vol-bar-bg"><div class="vol-bar-fill" style="width:28%"></div></div></div></td>
      </tr>
      <tr>
        <td><div class="metal-id"><div class="metal-symbol rh">RH</div><div><div class="metal-name-zh">銠</div><div class="metal-name-en">Rhodium · LPPM</div></div></div></td>
        <td>$4,660</td>
        <td class="chg-up">+25.50</td>
        <td class="chg-up">+0.55%</td>
        <td>$4,690</td>
        <td>$4,620</td>
        <td><div class="vol-bar-wrap"><span>6.2K oz</span><div class="vol-bar-bg"><div class="vol-bar-fill" style="width:18%"></div></div></div></td>
      </tr>
      <tr>
        <td><div class="metal-id"><div class="metal-symbol al">AL</div><div><div class="metal-name-zh">鋁</div><div class="metal-name-en">Aluminium · LME</div></div></div></td>
        <td>$2,468/t</td>
        <td class="chg-dn">−4.40</td>
        <td class="chg-dn">−0.18%</td>
        <td>$2,492</td>
        <td>$2,455</td>
        <td><div class="vol-bar-wrap"><span>380K t</span><div class="vol-bar-bg"><div class="vol-bar-fill" style="width:95%"></div></div></div></td>
      </tr>
      <tr>
        <td><div class="metal-id"><div class="metal-symbol ni">NI</div><div><div class="metal-name-zh">鎳</div><div class="metal-name-en">Nickel · LME</div></div></div></td>
        <td>$16,240/t</td>
        <td class="chg-up">+116.50</td>
        <td class="chg-up">+0.72%</td>
        <td>$16,380</td>
        <td>$16,080</td>
        <td><div class="vol-bar-wrap"><span>98K t</span><div class="vol-bar-bg"><div class="vol-bar-fill" style="width:62%"></div></div></div></td>
      </tr>
    </tbody>
  </table>
</section>

<!-- NEWS + SENTIMENT -->
<div class="news-section fade-in">
  <div class="news-main">
    <div class="sec-head">
      <h2 class="sec-title">產業 <span>新聞</span></h2>
      <a href="#" class="sec-more">全部新聞 →</a>
    </div>
    <div class="news-grid">
      <div class="news-item">
        <div class="news-num">01</div>
        <div>
          <div class="news-cat-tag"><span class="tag-dot" style="background:var(--gold)"></span>黃金 · 貴金屬</div>
          <div class="news-headline">美聯準會鴿派訊號推升金價至三個月高點，分析師上修年末目標至 $3,500</div>
          <div class="news-excerpt">Fed 最新會議紀錄暗示降息時間表提前，帶動避險買盤湧入，黃金現貨單日漲幅逾 0.8%，多家大行同步調升目標價。</div>
          <div class="news-footer"><span>2025.05.20</span><span>Reuters</span><span>閱讀 5 分鐘</span></div>
        </div>
      </div>
      <div class="news-item">
        <div class="news-num">02</div>
        <div>
          <div class="news-cat-tag"><span class="tag-dot" style="background:var(--copper)"></span>銅 · 基本金屬</div>
          <div class="news-headline">智利最大銅礦罷工進入第 12 天，全球銅供應鏈拉響警報</div>
          <div class="news-excerpt">Escondida 礦場工人持續與 BHP 談判破裂，每日影響產量估達 1.8 萬噸，倫敦期銅庫存降至近年低位。</div>
          <div class="news-footer"><span>2025.05.20</span><span>Bloomberg</span><span>閱讀 4 分鐘</span></div>
        </div>
      </div>
      <div class="news-item">
        <div class="news-num">03</div>
        <div>
          <div class="news-cat-tag"><span class="tag-dot" style="background:var(--platinum)"></span>鉑族金屬</div>
          <div class="news-headline">電動車滲透率衝擊鈀金需求，氫能經濟卻帶來鉑金長線利多</div>
          <div class="news-excerpt">全球 EV 銷量增速壓縮汽車觸媒轉化器需求，鈀金走弱；反觀燃料電池技術加速商業化，鉑金中長期前景受機構看好。</div>
          <div class="news-footer"><span>2025.05.19</span><span>FT</span><span>閱讀 6 分鐘</span></div>
        </div>
      </div>
    </div>
  </div>

  <div class="sentiment-panel">
    <div class="sp-title">市場情緒 &amp; 交易所狀態</div>
    <div class="sentiment-meter">
      <div class="sm-label">貴金屬市場情緒指數</div>
      <div class="sentiment-score">74</div>
      <div class="sentiment-verdict" style="color:var(--green)">偏多 · 樂觀</div>
      <div class="sm-bar" style="margin-top:16px"><div class="sm-fill" style="width:74%"></div></div>
      <div class="sm-ends"><span>極度悲觀</span><span>極度樂觀</span></div>
    </div>
    <div class="sp-title" style="margin-top:24px;margin-bottom:14px">主要交易所狀態</div>
    <div class="regional-list">
      <div class="region-item">
        <div><div class="region-name">倫敦 LBMA</div><div class="region-time" id="london-time">--:--</div></div>
        <span class="region-status rs-open">開市中</span>
      </div>
      <div class="region-item">
        <div><div class="region-name">紐約 COMEX</div><div class="region-time" id="ny-time">--:--</div></div>
        <span class="region-status rs-open">開市中</span>
      </div>
      <div class="region-item">
        <div><div class="region-name">上海 SHFE</div><div class="region-time" id="sh-time">--:--</div></div>
        <span class="region-status rs-closed">已收盤</span>
      </div>
      <div class="region-item">
        <div><div class="region-name">東京 TOCOM</div><div class="region-time" id="tk-time">--:--</div></div>
        <span class="region-status rs-closed">已收盤</span>
      </div>
    </div>
  </div>
</div>

<!-- FEATURES -->
<section class="features-section fade-in">
  <div class="feat-card">
    <div class="feat-icon">
      <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M3 3v18h18"/><path d="m7 16 4-4 4 4 4-6"/></svg>
    </div>
    <div class="feat-title">即時行情串流</div>
    <div class="feat-desc">每 15 秒同步 32 個全球交易所，覆蓋現貨、期貨與選擇權，價差精度達 0.01%。</div>
  </div>
  <div class="feat-card">
    <div class="feat-icon">
      <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="12" cy="12" r="3"/><path d="M12 1v4M12 19v4M4.22 4.22l2.83 2.83M16.95 16.95l2.83 2.83M1 12h4M19 12h4M4.22 19.78l2.83-2.83M16.95 7.05l2.83-2.83"/></svg>
    </div>
    <div class="feat-title">深度歷史數據</div>
    <div class="feat-desc">完整保留逾 50 年的金屬歷史行情，支援自訂時間區間下載與 API 存取。</div>
  </div>
  <div class="feat-card">
    <div class="feat-icon">
      <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M18 20V10M12 20V4M6 20v-6"/></svg>
    </div>
    <div class="feat-title">市場情緒分析</div>
    <div class="feat-desc">整合 COT 持倉報告、ETF 資金流向與新聞情緒，量化多空力道變化。</div>
  </div>
  <div class="feat-card">
    <div class="feat-icon">
      <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M15 17h5l-1.405-1.405A2.032 2.032 0 0 1 18 14.158V11a6.002 6.002 0 0 0-4-5.659V5a2 2 0 1 0-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 1 1-6 0v-1m6 0H9"/></svg>
    </div>
    <div class="feat-title">價格警報通知</div>
    <div class="feat-desc">設定目標價位或漲跌幅，即時 Email、LINE 或 Webhook 推送，不錯過任何機會。</div>
  </div>
</section>

<!-- SUBSCRIBE -->
<section class="subscribe fade-in">
  <div>
    <div class="sub-eyebrow">Weekly Intelligence Report</div>
    <h2 class="sub-title">每週金屬行情<br>深度簡報</h2>
    <p class="sub-desc">精選本週貴金屬與基本金屬走勢分析、礦業動態、<br>LME 庫存變化與下週關鍵觀察，每週一早晨直送信箱。<br>已有超過 42,000 位讀者訂閱，完全免費。</p>
  </div>
  <div class="sub-form">
    <div class="sub-row">
      <input type="email" class="sub-input" placeholder="your@email.com">
      <button class="sub-btn">免費訂閱</button>
    </div>
    <p class="sub-note">免費訂閱 · 隨時取消 · 不推廣告 · 不轉售資料</p>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-top">
    <div>
      <span class="footer-logo">METALLUM</span>
      <p class="footer-tagline">全球金屬行情資訊平台。<br>蒐羅貴金屬、基本金屬與稀有金屬即時數據，<br>為專業交易者與產業研究者而生。</p>
    </div>
    <div>
      <span class="footer-col-title">行情類別</span>
      <ul class="footer-links">
        <li><a href="#">貴金屬現貨</a></li>
        <li><a href="#">基本金屬 LME</a></li>
        <li><a href="#">稀有地球金屬</a></li>
        <li><a href="#">金屬期貨</a></li>
        <li><a href="#">礦業股票</a></li>
      </ul>
    </div>
    <div>
      <span class="footer-col-title">市場工具</span>
      <ul class="footer-links">
        <li><a href="#">行情圖表</a></li>
        <li><a href="#">歷史數據下載</a></li>
        <li><a href="#">換算工具</a></li>
        <li><a href="#">API 文件</a></li>
        <li><a href="#">價格警報</a></li>
      </ul>
    </div>
    <div>
      <span class="footer-col-title">關於我們</span>
      <ul class="footer-links">
        <li><a href="#">資料來源</a></li>
        <li><a href="#">研究方法</a></li>
        <li><a href="#">媒體合作</a></li>
        <li><a href="#">企業方案</a></li>
        <li><a href="#">聯絡我們</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <span class="footer-copy">© 2025 METALLUM Global Metals Data. All rights reserved.</span>
    <div class="footer-legal">
      <a href="#">隱私政策</a>
      <a href="#">服務條款</a>
      <a href="#">免責聲明</a>
    </div>
  </div>
</footer>

<script>
// Scroll reveal
const io = new IntersectionObserver(entries => {
  entries.forEach(e => { if(e.isIntersecting) e.target.classList.add('vis'); });
},{threshold:0.08});
document.querySelectorAll('.fade-in').forEach(el => io.observe(el));

// Category tabs
document.querySelectorAll('.cat-tab').forEach(btn => {
  btn.addEventListener('click', function(){
    document.querySelectorAll('.cat-tab').forEach(b => b.classList.remove('active'));
    this.classList.add('active');
  });
});

// Clock
function pad(n){return String(n).padStart(2,'0')}
function updateClocks(){
  const now = new Date();
  // London UTC+1
  const ldn = new Date(now.getTime() + (1)*3600000);
  document.getElementById('london-time').textContent = pad(ldn.getUTCHours())+':'+pad(ldn.getUTCMinutes());
  // NY UTC-4
  const ny = new Date(now.getTime() + (-4)*3600000);
  document.getElementById('ny-time').textContent = pad(ny.getUTCHours())+':'+pad(ny.getUTCMinutes());
  // Shanghai UTC+8
  const sh = new Date(now.getTime() + (8)*3600000);
  document.getElementById('sh-time').textContent = pad(sh.getUTCHours())+':'+pad(sh.getUTCMinutes());
  // Tokyo UTC+9
  const tk = new Date(now.getTime() + (9)*3600000);
  document.getElementById('tk-time').textContent = pad(tk.getUTCHours())+':'+pad(tk.getUTCMinutes());
}
updateClocks();
setInterval(updateClocks, 10000);

// Gold price fluctuation
let goldBase = 3342.40;
setInterval(()=>{
  const delta = (Math.random()-0.48)*3;
  goldBase = Math.max(3310, Math.min(3380, goldBase + delta));
  const chg = goldBase - 3314.60;
  const pct = (chg/3314.60*100).toFixed(2);
  document.getElementById('gold-price').innerHTML =
    goldBase.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g,',')+
    '<span class="fm-unit">USD/oz</span>';
  const chgEl = document.getElementById('gold-chg');
  const up = chg >= 0;
  chgEl.className = 'fm-chg ' + (up?'up':'dn');
  chgEl.textContent = (up?'▲ +':'▼ ') + Math.abs(chg).toFixed(2) + '  (' + (up?'+':'') + pct + '%)';
}, 4000);
</script>
</body>
</html>
