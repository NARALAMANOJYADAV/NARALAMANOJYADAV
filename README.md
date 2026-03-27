<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Narala Manoj Yadav — AI Engineer</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=Rajdhani:wght@300;400;500;600;700&family=Share+Tech+Mono&display=swap" rel="stylesheet"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<style>
:root{
  --c:#00FFFF;--p:#BF5FFF;--pk:#FF2D78;--g:#00FF88;--gold:#FFD700;
  --bg:#00000A;--bg2:#06060F;--bg3:#0A0A18;--card:#080814;
  --border:#ffffff08;--border2:#ffffff12;
  --gc: 0 0 20px #00FFFF66,0 0 50px #00FFFF22,0 0 100px #00FFFF11;
  --gp: 0 0 20px #BF5FFF66,0 0 50px #BF5FFF22;
  --gg: 0 0 20px #00FF8866,0 0 50px #00FF8822;
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;font-size:16px;}
body{background:var(--bg);font-family:'Rajdhani',sans-serif;overflow-x:hidden;color:#fff;cursor:none;}

/* ── CURSOR ── */
#cur{position:fixed;width:8px;height:8px;background:var(--c);border-radius:50%;pointer-events:none;z-index:9999;transform:translate(-50%,-50%);box-shadow:0 0 10px var(--c),0 0 20px var(--c)88;transition:width .15s,height .15s,background .15s;}
#cur2{position:fixed;width:36px;height:36px;border:1px solid var(--c)55;border-radius:50%;pointer-events:none;z-index:9998;transform:translate(-50%,-50%);transition:all .1s ease;}
#cur3{position:fixed;width:60px;height:60px;border:1px solid var(--p)22;border-radius:50%;pointer-events:none;z-index:9997;transform:translate(-50%,-50%);transition:all .18s ease;}
body:hover #cur{opacity:1;}

/* ── SCROLLBAR ── */
::-webkit-scrollbar{width:3px;}
::-webkit-scrollbar-track{background:#000;}
::-webkit-scrollbar-thumb{background:linear-gradient(var(--c),var(--p),var(--pk));border-radius:2px;}

/* ── THREE.JS BG ── */
#threeBg{position:fixed;top:0;left:0;width:100%;height:100%;z-index:0;pointer-events:none;}
/* ── NOISE OVERLAY ── */
.noise{position:fixed;inset:0;z-index:1;pointer-events:none;opacity:.025;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='4'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  background-size:150px;}

/* ── SCANLINES ── */
.scanlines{position:fixed;inset:0;z-index:1;pointer-events:none;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,.08) 2px,rgba(0,0,0,.08) 4px);}

/* ── NAV ── */
nav{position:fixed;top:0;left:0;right:0;z-index:500;padding:.9rem 2.5rem;display:flex;justify-content:space-between;align-items:center;backdrop-filter:blur(30px) saturate(180%);background:rgba(0,0,10,.65);border-bottom:1px solid var(--border);}
.nav-logo{font-family:'Orbitron',monospace;font-size:.95rem;font-weight:900;letter-spacing:5px;background:linear-gradient(90deg,var(--c),var(--p));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.nav-links{display:flex;gap:1.5rem;}
.nav-a{font-family:'Orbitron',monospace;font-size:.5rem;letter-spacing:2px;color:#444;text-decoration:none;padding:5px 12px;border:1px solid transparent;border-radius:2px;transition:all .3s;position:relative;overflow:hidden;}
.nav-a::after{content:'';position:absolute;bottom:0;left:0;width:0;height:1px;background:var(--c);transition:width .3s;}
.nav-a:hover{color:var(--c);border-color:var(--c)22;}
.nav-a:hover::after{width:100%;}
.nav-pill{display:flex;align-items:center;gap:6px;font-family:'Orbitron',monospace;font-size:.5rem;letter-spacing:2px;color:var(--g);padding:5px 14px;border:1px solid var(--g)33;border-radius:20px;background:var(--g)08;}
.ndot{width:5px;height:5px;background:var(--g);border-radius:50%;animation:npulse 1.4s infinite;}

/* ── PAGE WRAPPER ── */
.page{position:relative;z-index:10;}

/* ── HERO ── */
.hero{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:7rem 2rem 4rem;position:relative;}
.hero-eyebrow{font-family:'Share Tech Mono',monospace;font-size:.65rem;color:var(--p);letter-spacing:7px;margin-bottom:1.2rem;opacity:0;animation:riseIn .8s ease .2s forwards;}
.glitch-wrap{position:relative;opacity:0;animation:riseIn .9s ease .4s forwards;}
.hero-name{font-family:'Orbitron',monospace;font-size:clamp(2.2rem,7vw,5.5rem);font-weight:900;line-height:1.05;letter-spacing:3px;position:relative;}
.hero-name .l1{display:block;color:#fff;text-shadow:0 0 40px rgba(255,255,255,.2);}
.hero-name .l2{display:block;background:linear-gradient(135deg,var(--c) 0%,var(--p) 50%,var(--pk) 100%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;filter:drop-shadow(0 0 25px var(--c)66);}
/* glitch */
.hero-name::before,.hero-name::after{content:attr(data-text);position:absolute;top:0;left:0;width:100%;font-family:'Orbitron',monospace;font-size:clamp(2.2rem,7vw,5.5rem);font-weight:900;letter-spacing:3px;opacity:.06;}
.hero-name::before{color:var(--c);animation:glitchA 4s infinite;clip-path:polygon(0 30%,100% 30%,100% 50%,0 50%);}
.hero-name::after{color:var(--pk);animation:glitchB 4s infinite;clip-path:polygon(0 60%,100% 60%,100% 75%,0 75%);}
.hero-sub{margin-top:1.2rem;font-size:clamp(.85rem,1.8vw,1.1rem);color:#666;letter-spacing:3px;font-weight:300;opacity:0;animation:riseIn 1s ease .7s forwards;}
.hero-sub span{color:var(--c);}
.hero-chips{display:flex;gap:7px;flex-wrap:wrap;justify-content:center;margin-top:1.8rem;opacity:0;animation:riseIn 1s ease .9s forwards;}
.chip{padding:4px 14px;border-radius:20px;font-family:'Share Tech Mono',monospace;font-size:.58rem;letter-spacing:1px;border:1px solid;cursor:default;transition:all .3s;}
.chip:hover{transform:translateY(-3px) scale(1.05);}
.cc{color:var(--c);border-color:var(--c)44;background:var(--c)08;}
.cp{color:var(--p);border-color:var(--p)44;background:var(--p)08;}
.cg{color:var(--g);border-color:var(--g)44;background:var(--g)08;}
.cpk{color:var(--pk);border-color:var(--pk)44;background:var(--pk)08;}
.hero-btns{display:flex;gap:12px;margin-top:2rem;justify-content:center;flex-wrap:wrap;opacity:0;animation:riseIn 1s ease 1.1s forwards;}
.mbtn{position:relative;padding:11px 32px;font-family:'Orbitron',monospace;font-size:.6rem;letter-spacing:2px;border-radius:3px;cursor:pointer;overflow:hidden;transition:all .3s;font-weight:700;}
.mbtn-p{color:#000;background:var(--c);border:none;}
.mbtn-p:hover{box-shadow:0 0 30px var(--c),0 0 60px var(--c)44;transform:translateY(-3px);}
.mbtn-o{color:var(--p);background:transparent;border:1px solid var(--p);}
.mbtn-o:hover{background:var(--p)11;box-shadow:var(--gp);transform:translateY(-3px);}
.mbtn .shine{position:absolute;top:0;left:-100%;width:100%;height:100%;background:linear-gradient(90deg,transparent,rgba(255,255,255,.25),transparent);transition:.5s;}
.mbtn:hover .shine{left:100%;}
.scroll-cue{position:absolute;bottom:2rem;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;align-items:center;gap:5px;opacity:0;animation:riseIn 1s ease 1.5s forwards;}
.sc-line{width:1px;height:44px;background:linear-gradient(transparent,var(--c));animation:scPulse 2s ease-in-out infinite;}
.sc-txt{font-family:'Orbitron',monospace;font-size:.45rem;color:#333;letter-spacing:3px;}

/* ── SECTION FRAME ── */
.sec{padding:5rem 2.5rem;max-width:1040px;margin:0 auto;}
.sec-eye{font-family:'Share Tech Mono',monospace;font-size:.6rem;color:var(--p);letter-spacing:5px;display:flex;align-items:center;gap:8px;margin-bottom:.4rem;}
.sec-eye::before{content:'//';color:var(--c);}
.sec-h{font-family:'Orbitron',monospace;font-size:clamp(1.3rem,3vw,2rem);font-weight:700;margin-bottom:2rem;}
.sec-h .ac{color:var(--c);}
.sep{height:1px;background:linear-gradient(90deg,var(--c)44,var(--p)33,transparent);margin-bottom:3rem;}

/* ── ABOUT ── */
.about-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem;align-items:start;}
.glass-card{background:linear-gradient(135deg,rgba(0,255,255,.03),rgba(191,95,255,.02));border:1px solid var(--border2);border-radius:14px;padding:2rem;position:relative;overflow:hidden;transition:transform .4s ease,box-shadow .4s ease;transform-style:preserve-3d;}
.glass-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--c),var(--p),var(--pk));}
.glass-card::after{content:'';position:absolute;inset:0;background:radial-gradient(circle at 50% 0%,var(--c)05,transparent 70%);opacity:0;transition:opacity .4s;}
.glass-card:hover{box-shadow:0 25px 80px var(--c)12,0 0 0 1px var(--c)22;transform:translateY(-6px) rotateX(2deg) rotateY(1deg);}
.glass-card:hover::after{opacity:1;}
.json-block{font-family:'Share Tech Mono',monospace;font-size:.67rem;line-height:2.1;}
.jbr{color:var(--gold);} .jk{color:#79c0ff;} .jstr{color:#a8d8a8;} .jval{color:var(--c);} .jarr{color:var(--p);}
.skills-wrap{display:flex;flex-direction:column;gap:14px;}
.sk-item{display:flex;flex-direction:column;gap:6px;}
.sk-top{display:flex;justify-content:space-between;}
.sk-nm{font-family:'Orbitron',monospace;font-size:.55rem;color:#aaa;letter-spacing:1px;}
.sk-pc{font-family:'Share Tech Mono',monospace;font-size:.6rem;color:var(--c);}
.sk-track{height:5px;background:#0a0a18;border-radius:3px;overflow:visible;position:relative;border:1px solid #0f0f22;}
.sk-bar{height:100%;border-radius:3px;width:0;transition:width 1.8s cubic-bezier(.22,1,.36,1);position:relative;}
.sk-bar::after{content:'';position:absolute;right:-1px;top:50%;transform:translateY(-50%);width:9px;height:9px;border-radius:50%;background:inherit;box-shadow:0 0 10px currentColor,0 0 20px currentColor;}
.sk-c{background:linear-gradient(90deg,#004455,var(--c));color:var(--c);}
.sk-p{background:linear-gradient(90deg,#220044,var(--p));color:var(--p);}
.sk-g{background:linear-gradient(90deg,#002211,var(--g));color:var(--g);}
.sk-o{background:linear-gradient(90deg,#221100,#FF8800);color:#FF8800;}
.sk-pk{background:linear-gradient(90deg,#220011,var(--pk));color:var(--pk);}

/* ── TECH ORBS ── */
.tech-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(105px,1fr));gap:10px;}
.tech-cat{font-family:'Orbitron',monospace;font-size:.52rem;color:var(--p);letter-spacing:3px;margin:1.5rem 0 .8rem;grid-column:1/-1;display:flex;align-items:center;gap:8px;}
.tech-cat::before{content:'';width:20px;height:1px;background:var(--p);}
.torb{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:1rem .5rem;text-align:center;cursor:pointer;transition:all .3s;position:relative;overflow:hidden;transform-style:preserve-3d;}
.torb-glow{position:absolute;inset:0;opacity:0;transition:opacity .3s;border-radius:12px;}
.torb:hover{transform:translateY(-8px) rotateX(8deg) scale(1.04);border-color:var(--c)55;}
.torb:hover .torb-glow{opacity:1;}
.torb:hover .t-icon{filter:drop-shadow(0 0 10px var(--c)) drop-shadow(0 0 20px var(--c)66);}
.torb:hover .t-name{color:var(--c);}
.t-icon{font-size:1.9rem;margin-bottom:.5rem;transition:filter .3s;display:block;}
.t-name{font-family:'Orbitron',monospace;font-size:.48rem;color:#666;letter-spacing:1px;transition:color .3s;}

/* ── REPOS ── */
.repo-header{display:flex;flex-wrap:wrap;gap:10px;align-items:center;margin-bottom:1.2rem;}
.fetch-wrap{display:flex;gap:8px;flex:1;min-width:200px;}
.fi{flex:1;padding:8px 14px;background:#040410;border:1px solid #1a1a2e;color:var(--c);font-family:'Share Tech Mono',monospace;font-size:.68rem;border-radius:4px;outline:none;}
.fi:focus{border-color:var(--c);box-shadow:0 0 0 2px var(--c)18;}
.fi::placeholder{color:#333;}
.fbtn{padding:8px 20px;background:var(--c)11;border:1px solid var(--c)44;color:var(--c);font-family:'Orbitron',monospace;font-size:.58rem;letter-spacing:1px;border-radius:4px;cursor:pointer;transition:all .25s;font-weight:700;}
.fbtn:hover{background:var(--c)22;box-shadow:var(--gc);}
.rstatbar{display:flex;gap:24px;flex-wrap:wrap;padding:1rem 1.5rem;background:var(--card);border:1px solid var(--border2);border-radius:10px;margin-bottom:1.2rem;}
.rst{display:flex;flex-direction:column;gap:2px;}
.rst-n{font-family:'Orbitron',monospace;font-size:1.15rem;font-weight:700;color:var(--c);text-shadow:var(--gc);}
.rst-l{font-family:'Share Tech Mono',monospace;font-size:.52rem;color:#333;letter-spacing:1px;}
.rctrl{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:1.2rem;}
.rfb{padding:5px 14px;font-family:'Orbitron',monospace;font-size:.48rem;letter-spacing:1px;border:1px solid #1a1a2e;background:transparent;color:#444;border-radius:3px;cursor:pointer;transition:all .2s;}
.rfb.on,.rfb:hover{border-color:var(--c);color:var(--c);background:var(--c)0a;}
.rsrt{padding:6px 10px;background:#040410;border:1px solid #1a1a2e;color:#555;font-family:'Share Tech Mono',monospace;font-size:.58rem;border-radius:3px;outline:none;cursor:pointer;}
.rsrch{flex:1;min-width:140px;padding:6px 12px;background:#040410;border:1px solid #1a1a2e;color:#ccc;font-family:'Share Tech Mono',monospace;font-size:.62rem;border-radius:3px;outline:none;}
.rsrch:focus{border-color:var(--c);box-shadow:0 0 0 2px var(--c)18;}
.rsrch::placeholder{color:#222;}
.rgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(285px,1fr));gap:12px;}
.rcard{background:linear-gradient(135deg,var(--bg2),var(--bg3));border:1px solid #0d0d22;border-radius:12px;padding:1.2rem;cursor:pointer;transition:all .3s;position:relative;overflow:hidden;transform-style:preserve-3d;}
.rcard::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--p),var(--c));transform:scaleX(0);transition:transform .35s;transform-origin:left;}
.rcard::after{content:'';position:absolute;inset:0;background:radial-gradient(circle at 50% 0%,var(--c)06,transparent 65%);opacity:0;transition:opacity .3s;border-radius:12px;}
.rcard:hover{transform:translateY(-5px) rotateX(3deg);border-color:var(--c)33;box-shadow:0 20px 60px var(--c)12,0 0 0 1px var(--c)18;}
.rcard:hover::before{transform:scaleX(1);}
.rcard:hover::after{opacity:1;}
.rc-nm{font-family:'Orbitron',monospace;font-size:.65rem;color:var(--c);font-weight:700;letter-spacing:1px;word-break:break-all;margin-bottom:.4rem;}
.rc-fork{font-size:.48rem;color:#FF8800;border:1px solid #FF880033;padding:1px 6px;border-radius:2px;background:#FF880008;float:right;}
.rc-desc{font-size:.7rem;color:#555;line-height:1.55;margin-bottom:.7rem;min-height:26px;font-family:'Rajdhani',sans-serif;font-weight:400;}
.rc-topics{display:flex;flex-wrap:wrap;gap:4px;margin-bottom:.6rem;}
.tp{font-size:.48rem;padding:2px 7px;border-radius:10px;background:var(--p)0a;color:var(--p)77;border:1px solid var(--p)22;}
.rc-foot{display:flex;align-items:center;gap:10px;flex-wrap:wrap;}
.rc-lang{display:flex;align-items:center;gap:5px;}
.lcdot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.lcnm{font-size:.58rem;color:#777;font-family:'Share Tech Mono',monospace;}
.rc-st{font-size:.58rem;color:#333;font-family:'Share Tech Mono',monospace;display:flex;align-items:center;gap:3px;}
.rc-dt{font-size:.5rem;color:#1e1e30;font-family:'Share Tech Mono',monospace;margin-left:auto;}
.load-box{text-align:center;padding:4rem 1rem;}
.lspin{width:38px;height:38px;border:2px solid #0a0a18;border-top:2px solid var(--c);border-radius:50%;animation:spin .75s linear infinite;margin:0 auto 1rem;}
.ltxt{font-family:'Orbitron',monospace;font-size:.62rem;color:var(--c)77;letter-spacing:3px;animation:pulse 1.3s infinite;}
.err-box{text-align:center;padding:3rem;color:var(--pk);font-family:'Share Tech Mono',monospace;font-size:.7rem;line-height:2;}
.pager{display:flex;gap:6px;justify-content:center;margin-top:1.5rem;flex-wrap:wrap;}
.pgb{padding:5px 13px;font-family:'Orbitron',monospace;font-size:.48rem;border:1px solid #1a1a2e;background:transparent;color:#333;border-radius:3px;cursor:pointer;transition:all .2s;}
.pgb:hover:not(:disabled){border-color:var(--p);color:var(--p);}
.pgb.cur{border-color:var(--c);color:var(--c);background:var(--c)0a;}
.pgb:disabled{opacity:.15;cursor:default;}

/* ── STATS IMAGES ── */
.stats-grid{display:grid;gap:12px;}
.stat-row2{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.stat-img{width:100%;border-radius:10px;border:1px solid var(--border2);transition:transform .3s,box-shadow .3s;display:block;}
.stat-img:hover{transform:translateY(-5px) scale(1.01);box-shadow:0 16px 50px var(--c)15;}

/* ── CONNECT ── */
.conn-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(210px,1fr));gap:14px;}
.cc-card{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:1.8rem;text-align:center;cursor:pointer;transition:all .3s;text-decoration:none;display:block;position:relative;overflow:hidden;transform-style:preserve-3d;}
.cc-card::before{content:'';position:absolute;inset:0;opacity:0;transition:opacity .35s;border-radius:14px;}
.cc-card:hover{transform:translateY(-7px) rotateX(5deg);}
.cc-card:hover::before{opacity:1;}
.cc-gh::before{background:radial-gradient(circle at 50% 0%,#ffffff0a,transparent 70%);}
.cc-gh:hover{border-color:#fff3;box-shadow:0 16px 50px #ffffff12;}
.cc-li::before{background:radial-gradient(circle at 50% 0%,#0077b50a,transparent 70%);}
.cc-li:hover{border-color:#0077b544;box-shadow:0 16px 50px #0077b515;}
.cc-gm::before{background:radial-gradient(circle at 50% 0%,#ea43350a,transparent 70%);}
.cc-gm:hover{border-color:#ea433544;box-shadow:0 16px 50px #ea433515;}
.cc-po::before{background:radial-gradient(circle at 50% 0%,#FF57220a,transparent 70%);}
.cc-po:hover{border-color:#FF572244;box-shadow:0 16px 50px #FF572215;}
.cc-ic{font-size:2.2rem;margin-bottom:.6rem;}
.cc-tl{font-family:'Orbitron',monospace;font-size:.58rem;letter-spacing:2px;color:#ddd;margin-bottom:.25rem;}
.cc-sb{font-size:.68rem;color:#444;font-family:'Rajdhani',sans-serif;}

/* ── FOOTER ── */
footer{border-top:1px solid var(--border);padding:2.5rem 2rem;text-align:center;position:relative;z-index:10;}
.ft-nm{font-family:'Orbitron',monospace;font-size:.85rem;font-weight:900;letter-spacing:5px;background:linear-gradient(90deg,var(--c),var(--p));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;margin-bottom:.5rem;}
.ft-q{font-family:'Rajdhani',sans-serif;font-size:.9rem;color:#333;font-style:italic;letter-spacing:2px;}

/* ── ANIMATIONS ── */
@keyframes riseIn{from{opacity:0;transform:translateY(24px)}to{opacity:1;transform:translateY(0)}}
@keyframes glitchA{0%,90%,100%{transform:none}92%{transform:translateX(-3px) skewX(2deg)}94%{transform:translateX(3px) skewX(-2deg)}96%{transform:translateX(-2px)}}
@keyframes glitchB{0%,88%,100%{transform:none}90%{transform:translateX(3px) skewX(-3deg)}93%{transform:translateX(-3px) skewX(2deg)}96%{transform:translateX(2px)}}
@keyframes scPulse{0%,100%{opacity:0;transform:scaleY(0);transform-origin:top}50%{opacity:1}100%{opacity:0;transform:scaleY(1);transform-origin:bottom}}
@keyframes npulse{0%,100%{box-shadow:0 0 4px var(--g)}50%{box-shadow:0 0 14px var(--g),0 0 28px var(--g)44}}
@keyframes spin{to{transform:rotate(360deg)}}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}
@keyframes cardReveal{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
@keyframes floatChip{0%,100%{transform:translateY(0)}50%{transform:translateY(-5px)}}

/* chip float stagger */
.chip:nth-child(1){animation:floatChip 2.8s ease-in-out infinite;}
.chip:nth-child(2){animation:floatChip 3.1s ease-in-out .3s infinite;}
.chip:nth-child(3){animation:floatChip 2.6s ease-in-out .6s infinite;}
.chip:nth-child(4){animation:floatChip 3.4s ease-in-out .9s infinite;}
.chip:nth-child(5){animation:floatChip 2.9s ease-in-out .15s infinite;}
.chip:nth-child(6){animation:floatChip 3.2s ease-in-out .5s infinite;}
.chip:nth-child(7){animation:floatChip 2.7s ease-in-out .8s infinite;}

/* scroll-reveal */
.reveal{opacity:0;transform:translateY(30px);transition:opacity .7s ease,transform .7s ease;}
.reveal.in{opacity:1;transform:translateY(0);}
</style>
</head>
<body>

<!-- CURSOR RINGS -->
<div id="cur"></div>
<div id="cur2"></div>
<div id="cur3"></div>

<!-- THREE.JS CANVAS -->
<canvas id="threeBg"></canvas>
<div class="noise"></div>
<div class="scanlines"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">MNY</div>
  <div class="nav-links">
    <a class="nav-a" href="#about">ABOUT</a>
    <a class="nav-a" href="#tech">TECH</a>
    <a class="nav-a" href="#repos">REPOS</a>
    <a class="nav-a" href="#stats">STATS</a>
    <a class="nav-a" href="#connect">CONNECT</a>
  </div>
  <div class="nav-pill"><div class="ndot"></div>OPEN TO WORK</div>
</nav>

<!-- PAGE -->
<div class="page">

<!-- ── HERO ── -->
<section class="hero">
  <div class="hero-eyebrow">// AI ENGINEER · FULL STACK DEVELOPER · ML EXPLORER</div>
  <div class="glitch-wrap">
    <div class="hero-name" data-text="NARALA MANOJ YADAV">
      <span class="l1">NARALA</span>
      <span class="l2">MANOJ YADAV</span>
    </div>
  </div>
  <div class="hero-sub">Building <span>AI-Powered</span> Experiences · Hyderabad, India 🇮🇳</div>
  <div class="hero-chips">
    <span class="chip cc">Python</span>
    <span class="chip cp">LangChain</span>
    <span class="chip cc">React</span>
    <span class="chip cg">Next.js</span>
    <span class="chip cp">OpenAI</span>
    <span class="chip cc">Node.js</span>
    <span class="chip cpk">TensorFlow</span>
  </div>
  <div class="hero-btns">
    <button class="mbtn mbtn-p" onclick="document.getElementById('repos').scrollIntoView({behavior:'smooth'})"><span class="shine"></span>⚡ VIEW MY REPOS</button>
    <button class="mbtn mbtn-o" onclick="document.getElementById('connect').scrollIntoView({behavior:'smooth'})"><span class="shine"></span>💬 CONNECT</button>
  </div>
  <div class="scroll-cue"><div class="sc-line"></div><div class="sc-txt">SCROLL</div></div>
</section>

<!-- ── ABOUT ── -->
<section class="sec reveal" id="about">
  <div class="sec-eye">01 · ABOUT ME</div>
  <div class="sec-h">Who <span class="ac">Am I?</span></div>
  <div class="sep"></div>
  <div class="about-grid">
    <div class="glass-card" id="tiltCard1">
      <div class="json-block">
        <span class="jbr">{</span><br>
        &nbsp;&nbsp;<span class="jk">"name"</span>: <span class="jstr">"Narala Manoj Yadav"</span>,<br>
        &nbsp;&nbsp;<span class="jk">"role"</span>: <span class="jarr">["AI Engineer","FS Dev"]</span>,<br>
        &nbsp;&nbsp;<span class="jk">"edu"</span>: <span class="jstr">"B.Tech AI &amp; Data Science"</span>,<br>
        &nbsp;&nbsp;<span class="jk">"city"</span>: <span class="jstr">"Hyderabad, India 🇮🇳"</span>,<br>
        &nbsp;&nbsp;<span class="jk">"ai_focus"</span>: <span class="jarr">["LLMs","RAG","NLP","CV"]</span>,<br>
        &nbsp;&nbsp;<span class="jk">"currently"</span>: <span class="jstr">"B.Tech AI &amp; DS"</span>,<br>
        &nbsp;&nbsp;<span class="jk">"status"</span>: <span class="jval">OPEN_TO_HIRE</span>,<br>
        &nbsp;&nbsp;<span class="jk">"mission"</span>: <span class="jstr">"Build AI that matters"</span>,<br>
        &nbsp;&nbsp;<span class="jk">"fun"</span>: <span class="jstr">"console.log addict 😅"</span><br>
        <span class="jbr">}</span>
      </div>
    </div>
    <div class="glass-card" id="tiltCard2">
      <div class="skills-wrap">
        <div class="sk-item"><div class="sk-top"><span class="sk-nm">PYTHON</span><span class="sk-pc">92%</span></div><div class="sk-track"><div class="sk-bar sk-c" data-w="92"></div></div></div>
        <div class="sk-item"><div class="sk-top"><span class="sk-nm">REACT / NEXT.JS</span><span class="sk-pc">88%</span></div><div class="sk-track"><div class="sk-bar sk-p" data-w="88"></div></div></div>
        <div class="sk-item"><div class="sk-top"><span class="sk-nm">ML / DEEP LEARNING</span><span class="sk-pc">84%</span></div><div class="sk-track"><div class="sk-bar sk-g" data-w="84"></div></div></div>
        <div class="sk-item"><div class="sk-top"><span class="sk-nm">NODE.JS / EXPRESS</span><span class="sk-pc">80%</span></div><div class="sk-track"><div class="sk-bar sk-o" data-w="80"></div></div></div>
        <div class="sk-item"><div class="sk-top"><span class="sk-nm">LANGCHAIN / LLMs</span><span class="sk-pc">76%</span></div><div class="sk-track"><div class="sk-bar sk-pk" data-w="76"></div></div></div>
        <div class="sk-item"><div class="sk-top"><span class="sk-nm">TYPESCRIPT</span><span class="sk-pc">79%</span></div><div class="sk-track"><div class="sk-bar sk-c" data-w="79"></div></div></div>
        <div class="sk-item"><div class="sk-top"><span class="sk-nm">GCP / CLOUD</span><span class="sk-pc">70%</span></div><div class="sk-track"><div class="sk-bar sk-p" data-w="70"></div></div></div>
      </div>
    </div>
  </div>
</section>

<!-- ── TECH ── -->
<section class="sec reveal" id="tech">
  <div class="sec-eye">02 · TECH STACK</div>
  <div class="sec-h">My <span class="ac">Arsenal</span></div>
  <div class="sep"></div>
  <div class="tech-grid">
    <div class="tech-cat">AI &amp; MACHINE LEARNING</div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#3572A522,transparent 70%)"></div><span class="t-icon">🐍</span><div class="t-name">Python</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#FF6F0022,transparent 70%)"></div><span class="t-icon">🔶</span><div class="t-name">TensorFlow</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#EE4C2C22,transparent 70%)"></div><span class="t-icon">🔥</span><div class="t-name">PyTorch</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#FFD21F22,transparent 70%)"></div><span class="t-icon">🤗</span><div class="t-name">HuggingFace</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#1C3C3C22,transparent 70%)"></div><span class="t-icon">🧠</span><div class="t-name">LangChain</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#41209122,transparent 70%)"></div><span class="t-icon">⚡</span><div class="t-name">OpenAI</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#F7931E22,transparent 70%)"></div><span class="t-icon">🔬</span><div class="t-name">scikit-learn</div></div>
    <div class="tech-cat">FULL STACK</div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#61DAFB22,transparent 70%)"></div><span class="t-icon">⚛️</span><div class="t-name">React</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#ffffff22,transparent 70%)"></div><span class="t-icon">▲</span><div class="t-name">Next.js</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#33993322,transparent 70%)"></div><span class="t-icon">💚</span><div class="t-name">Node.js</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#007ACC22,transparent 70%)"></div><span class="t-icon">🔷</span><div class="t-name">TypeScript</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#06B6D422,transparent 70%)"></div><span class="t-icon">🎨</span><div class="t-name">Tailwind</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#00000022,transparent 70%)"></div><span class="t-icon">🚀</span><div class="t-name">Express</div></div>
    <div class="tech-cat">CLOUD &amp; DATA</div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#4285F422,transparent 70%)"></div><span class="t-icon">☁️</span><div class="t-name">GCP</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#4EA94B22,transparent 70%)"></div><span class="t-icon">🍃</span><div class="t-name">MongoDB</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#31619222,transparent 70%)"></div><span class="t-icon">🐘</span><div class="t-name">PostgreSQL</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#2CA5E022,transparent 70%)"></div><span class="t-icon">🐳</span><div class="t-name">Docker</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#FFCA2822,transparent 70%)"></div><span class="t-icon">🔥</span><div class="t-name">Firebase</div></div>
    <div class="torb"><div class="torb-glow" style="background:radial-gradient(circle at 50% 0%,#00ADD822,transparent 70%)"></div><span class="t-icon">🐹</span><div class="t-name">Go</div></div>
  </div>
</section>

<!-- ── REPOS ── -->
<section class="sec reveal" id="repos">
  <div class="sec-eye">03 · REPOSITORIES</div>
  <div class="sec-h">Live <span class="ac">GitHub Repos</span></div>
  <div class="sep"></div>

  <div class="repo-header">
    <div class="fetch-wrap">
      <input class="fi" id="unIn" value="NARALAMANOJYADAV" placeholder="GitHub username..."/>
      <button class="fbtn" onclick="fetchRepos()">⚡ FETCH</button>
    </div>
  </div>

  <div id="rstatbar" class="rstatbar" style="display:none">
    <div class="rst"><div class="rst-n" id="rN">0</div><div class="rst-l">REPOS</div></div>
    <div class="rst"><div class="rst-n" id="rS" style="color:var(--gold)">0</div><div class="rst-l">STARS</div></div>
    <div class="rst"><div class="rst-n" id="rF" style="color:var(--p)">0</div><div class="rst-l">FORKS</div></div>
    <div class="rst"><div class="rst-n" id="rW" style="color:var(--g)">0</div><div class="rst-l">WATCHERS</div></div>
    <div class="rst"><div class="rst-n" id="rL" style="color:var(--pk)">—</div><div class="rst-l">TOP LANG</div></div>
  </div>

  <div class="rctrl" id="rctrl" style="display:none">
    <button class="rfb on" data-f="all" onclick="setF('all',this)">ALL</button>
    <button class="rfb" data-f="source" onclick="setF('source',this)">ORIGINALS</button>
    <button class="rfb" data-f="fork" onclick="setF('fork',this)">FORKS</button>
    <select class="rsrt" id="rsrt" onchange="renderRepos()">
      <option value="updated">RECENTLY UPDATED</option>
      <option value="stars">MOST STARS</option>
      <option value="name">NAME A–Z</option>
      <option value="size">LARGEST</option>
      <option value="forks">MOST FORKS</option>
    </select>
    <input class="rsrch" id="rsrch" placeholder="Search repos..." oninput="renderRepos()"/>
  </div>

  <div id="repoArea"><div class="load-box"><div class="lspin"></div><div class="ltxt">INITIALIZING...</div></div></div>
  <div class="pager" id="pager"></div>
</section>

<!-- ── STATS ── -->
<section class="sec reveal" id="stats">
  <div class="sec-eye">04 · GITHUB STATS</div>
  <div class="sec-h">My <span class="ac">Numbers</span></div>
  <div class="sep"></div>
  <div class="stats-grid">
    <div class="stat-row2">
      <img class="stat-img" src="https://github-readme-stats.vercel.app/api?username=NARALAMANOJYADAV&show_icons=true&theme=radical&hide_border=true&count_private=true&bg_color=06060F&title_color=00FFFF&icon_color=BF5FFF&text_color=ffffff" alt="GitHub Stats"/>
      <img class="stat-img" src="https://github-readme-streak-stats.herokuapp.com/?user=NARALAMANOJYADAV&theme=radical&hide_border=true&background=06060F&ring=00FFFF&fire=BF5FFF&currStreakLabel=00FFFF" alt="Streak"/>
    </div>
    <img class="stat-img" src="https://github-readme-activity-graph.vercel.app/graph?username=NARALAMANOJYADAV&bg_color=06060F&color=00FFFF&line=BF5FFF&point=FFFFFF&area=true&area_color=BF5FFF&hide_border=true&radius=4" alt="Activity Graph"/>
    <div class="stat-row2">
      <img class="stat-img" src="https://github-readme-stats.vercel.app/api/top-langs/?username=NARALAMANOJYADAV&layout=compact&theme=radical&hide_border=true&bg_color=06060F&title_color=00FFFF&text_color=ffffff&langs_count=8" alt="Top Languages"/>
      <img class="stat-img" src="https://github-profile-trophy.vercel.app/?username=NARALAMANOJYADAV&theme=matrix&no-frame=true&no-bg=true&margin-w=4&column=4" alt="Trophies"/>
    </div>
    <img class="stat-img" src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=NARALAMANOJYADAV&theme=2077" alt="Profile Summary"/>
  </div>
</section>

<!-- ── CONNECT ── -->
<section class="sec reveal" id="connect">
  <div class="sec-eye">05 · CONNECT</div>
  <div class="sec-h">Let's <span class="ac">Build Together</span></div>
  <div class="sep"></div>
  <div class="conn-grid">
    <a class="cc-card cc-gh" href="https://github.com/NARALAMANOJYADAV" target="_blank"><div class="cc-ic">🐙</div><div class="cc-tl">GITHUB</div><div class="cc-sb">@NARALAMANOJYADAV</div></a>
    <a class="cc-card cc-li" href="https://linkedin.com/in/YOUR_LINKEDIN" target="_blank"><div class="cc-ic">💼</div><div class="cc-tl">LINKEDIN</div><div class="cc-sb">Connect professionally</div></a>
    <a class="cc-card cc-gm" href="mailto:yourmail@gmail.com"><div class="cc-ic">✉️</div><div class="cc-tl">EMAIL</div><div class="cc-sb">yourmail@gmail.com</div></a>
    <a class="cc-card cc-po" href="https://your-portfolio.com" target="_blank"><div class="cc-ic">🌐</div><div class="cc-tl">PORTFOLIO</div><div class="cc-sb">your-portfolio.com</div></a>
  </div>
  <div style="text-align:center;margin-top:3rem;font-family:'Rajdhani',sans-serif;font-size:1rem;color:#2a2a3a;font-style:italic;letter-spacing:2px;">"I don't just write code — I build experiences powered by intelligence."</div>
</section>

<footer>
  <div class="ft-nm">NARALA MANOJ YADAV</div>
  <div class="ft-q">AI Engineer · Full Stack Developer · Hyderabad, India</div>
</footer>

</div><!-- end .page -->

<script>
/* ══════════════════════════════
   THREE.JS – TORUS KNOT + STARS
══════════════════════════════ */
(function(){
  const canvas=document.getElementById('threeBg');
  const renderer=new THREE.WebGLRenderer({canvas,antialias:true,alpha:true});
  renderer.setPixelRatio(Math.min(window.devicePixelRatio,2));
  renderer.setSize(window.innerWidth,window.innerHeight);
  renderer.setClearColor(0x000000,0);

  const scene=new THREE.Scene();
  const camera=new THREE.PerspectiveCamera(60,window.innerWidth/window.innerHeight,0.1,1000);
  camera.position.set(0,0,28);

  /* TORUS KNOT – main hero object */
  const tkGeo=new THREE.TorusKnotGeometry(5,1.2,200,20,3,5);
  const tkMat=new THREE.MeshPhongMaterial({
    color:0x002222,emissive:0x002222,wireframe:true,
    wireframeLinewidth:1
  });
  const tk=new THREE.Mesh(tkGeo,tkMat);
  tk.position.set(14,-2,0);
  scene.add(tk);

  /* WIREFRAME SPHERE */
  const sGeo=new THREE.SphereGeometry(3.5,20,20);
  const sMat=new THREE.MeshPhongMaterial({color:0x110022,emissive:0x110022,wireframe:true});
  const sphere=new THREE.Mesh(sGeo,sMat);
  sphere.position.set(-14,4,-5);
  scene.add(sphere);

  /* ICOSAHEDRON */
  const iGeo=new THREE.IcosahedronGeometry(2.5,1);
  const iMat=new THREE.MeshPhongMaterial({color:0x002211,emissive:0x002211,wireframe:true});
  const ico=new THREE.Mesh(iGeo,iMat);
  ico.position.set(-8,-8,-8);
  scene.add(ico);

  /* STAR FIELD */
  const starGeo=new THREE.BufferGeometry();
  const starCount=3000;
  const starPos=new Float32Array(starCount*3);
  const starCol=new Float32Array(starCount*3);
  for(let i=0;i<starCount;i++){
    starPos[i*3]=(Math.random()-0.5)*400;
    starPos[i*3+1]=(Math.random()-0.5)*400;
    starPos[i*3+2]=(Math.random()-0.5)*200-50;
    const t=Math.random();
    if(t<0.6){starCol[i*3]=0;starCol[i*3+1]=0.7+Math.random()*0.3;starCol[i*3+2]=0.7+Math.random()*0.3;}
    else if(t<0.8){starCol[i*3]=0.5+Math.random()*0.3;starCol[i*3+1]=0;starCol[i*3+2]=0.7+Math.random()*0.3;}
    else{starCol[i*3]=1;starCol[i*3+1]=1;starCol[i*3+2]=1;}
  }
  starGeo.setAttribute('position',new THREE.BufferAttribute(starPos,3));
  starGeo.setAttribute('color',new THREE.BufferAttribute(starCol,3));
  const starMat=new THREE.PointsMaterial({size:.5,vertexColors:true,transparent:true,opacity:.85});
  scene.add(new THREE.Points(starGeo,starMat));

  /* LIGHTS */
  const aLight=new THREE.AmbientLight(0x000011,0.5);
  scene.add(aLight);
  const pLight=new THREE.PointLight(0x00FFFF,2,80);
  pLight.position.set(10,10,10);
  scene.add(pLight);
  const pLight2=new THREE.PointLight(0xBF5FFF,1.5,80);
  pLight2.position.set(-10,-5,5);
  scene.add(pLight2);
  const pLight3=new THREE.PointLight(0xFF2D78,1,60);
  pLight3.position.set(0,-10,-10);
  scene.add(pLight3);

  /* FLOATING GRID PLANE */
  const gridHelper=new THREE.GridHelper(80,30,0x001111,0x000a0a);
  gridHelper.position.y=-15;
  gridHelper.material.opacity=0.4;
  gridHelper.material.transparent=true;
  scene.add(gridHelper);

  /* MOUSE PARALLAX */
  let mx=0,my=0;
  document.addEventListener('mousemove',e=>{
    mx=(e.clientX/window.innerWidth-0.5)*2;
    my=(e.clientY/window.innerHeight-0.5)*2;
  });

  let t=0;
  function animate(){
    requestAnimationFrame(animate);
    t+=0.005;
    tk.rotation.x+=0.004;
    tk.rotation.y+=0.003;
    tk.rotation.z+=0.002;
    tk.position.y=Math.sin(t)*1.5-2;
    sphere.rotation.x-=0.003;
    sphere.rotation.y+=0.004;
    sphere.position.x=-14+Math.sin(t*0.7)*1.5;
    ico.rotation.x+=0.006;
    ico.rotation.z+=0.004;
    ico.position.y=-8+Math.sin(t*1.2)*1;
    camera.position.x+=(-mx*3-camera.position.x)*0.04;
    camera.position.y+=(my*2-camera.position.y)*0.04;
    camera.lookAt(0,0,0);
    pLight.position.x=10+Math.sin(t)*5;
    pLight.position.y=10+Math.cos(t)*4;
    pLight2.position.x=-10+Math.cos(t*1.3)*4;
    renderer.render(scene,camera);
  }
  animate();

  window.addEventListener('resize',()=>{
    camera.aspect=window.innerWidth/window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth,window.innerHeight);
  });
})();

/* ══════════════════════
   CURSOR
══════════════════════ */
const c1=document.getElementById('cur');
const c2=document.getElementById('cur2');
const c3=document.getElementById('cur3');
let mx=window.innerWidth/2,my=window.innerHeight/2;
let t2x=mx,t2y=my,t3x=mx,t3y=my;
document.addEventListener('mousemove',e=>{
  mx=e.clientX;my=e.clientY;
  c1.style.left=mx+'px';c1.style.top=my+'px';
});
setInterval(()=>{
  t2x+=(mx-t2x)*.2;t2y+=(my-t2y)*.2;
  t3x+=(mx-t3x)*.08;t3y+=(my-t3y)*.08;
  c2.style.left=t2x+'px';c2.style.top=t2y+'px';
  c3.style.left=t3x+'px';c3.style.top=t3y+'px';
},13);
document.querySelectorAll('a,button,.torb,.rcard,.cc-card,.mbtn').forEach(el=>{
  el.addEventListener('mouseenter',()=>{c1.style.width='18px';c1.style.height='18px';c1.style.background='var(--p)';c2.style.borderColor='var(--p)55';});
  el.addEventListener('mouseleave',()=>{c1.style.width='8px';c1.style.height='8px';c1.style.background='var(--c)';c2.style.borderColor='var(--c)55';});
});

/* ══════════════════════
   SCROLL REVEAL
══════════════════════ */
const observer=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');}});
},{threshold:0.12});
document.querySelectorAll('.reveal').forEach(el=>observer.observe(el));

/* ══════════════════════
   SKILL BARS
══════════════════════ */
const skillObs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('.sk-bar').forEach(b=>{
        b.style.width=b.dataset.w+'%';
      });
      skillObs.unobserve(e.target);
    }
  });
},{threshold:0.3});
const skillSec=document.getElementById('about');
if(skillSec)skillObs.observe(skillSec);

/* ══════════════════════
   3D CARD TILT
══════════════════════ */
function makeTilt(el){
  el.addEventListener('mousemove',e=>{
    const r=el.getBoundingClientRect();
    const cx=r.left+r.width/2,cy=r.top+r.height/2;
    const dx=(e.clientX-cx)/(r.width/2);
    const dy=(e.clientY-cy)/(r.height/2);
    el.style.transform=`perspective(800px) rotateY(${dx*10}deg) rotateX(${-dy*10}deg) translateZ(8px)`;
    el.style.boxShadow=`${-dx*20}px ${-dy*20}px 60px var(--c)18,0 0 0 1px var(--c)22`;
  });
  el.addEventListener('mouseleave',()=>{
    el.style.transform='perspective(800px) rotateY(0) rotateX(0) translateZ(0)';
    el.style.boxShadow='';
  });
}
['tiltCard1','tiltCard2'].forEach(id=>{const el=document.getElementById(id);if(el)makeTilt(el);});

/* ══════════════════════
   MAGNETIC BUTTONS
══════════════════════ */
document.querySelectorAll('.mbtn').forEach(btn=>{
  btn.addEventListener('mousemove',e=>{
    const r=btn.getBoundingClientRect();
    const dx=(e.clientX-(r.left+r.width/2))*.3;
    const dy=(e.clientY-(r.top+r.height/2))*.3;
    btn.style.transform=`translate(${dx}px,${dy}px)`;
  });
  btn.addEventListener('mouseleave',()=>btn.style.transform='');
});

/* ══════════════════════
   REPO SYSTEM
══════════════════════ */
const LANG_C={JavaScript:'#f7df1e',TypeScript:'#3178c6',Python:'#3572A5',HTML:'#e34c26',CSS:'#563d7c',Java:'#b07219','C++':'#f34b7d',C:'#555555',Shell:'#89e051','Jupyter Notebook':'#DA5B0B',Vue:'#41b883',Go:'#00ADD8',Rust:'#dea584',Ruby:'#701516',PHP:'#4F5D95',Swift:'#ffac45',Kotlin:'#A97BFF',default:'#8b949e'};
let allRepos=[],curFilter='all',curPage=1;
const PPG=9;

async function fetchRepos(){
  const u=document.getElementById('unIn').value.trim();
  if(!u)return;
  document.getElementById('repoArea').innerHTML='<div class="load-box"><div class="lspin"></div><div class="ltxt">FETCHING FROM GITHUB...</div></div>';
  document.getElementById('rstatbar').style.display='none';
  document.getElementById('rctrl').style.display='none';
  document.getElementById('pager').innerHTML='';
  try{
    let all=[],page=1;
    while(true){
      const res=await fetch(`https://api.github.com/users/${u}/repos?per_page=100&page=${page}`);
      if(!res.ok)throw new Error(`GitHub ${res.status}: ${res.statusText}`);
      const data=await res.json();
      all=[...all,...data];
      if(data.length<100)break;
      page++;
    }
    allRepos=all;
    /* stats */
    const stars=allRepos.reduce((s,r)=>s+r.stargazers_count,0);
    const forks=allRepos.reduce((s,r)=>s+r.forks_count,0);
    const watchers=allRepos.reduce((s,r)=>s+(r.watchers_count||0),0);
    const lm={};allRepos.forEach(r=>{if(r.language)lm[r.language]=(lm[r.language]||0)+1;});
    const tl=Object.entries(lm).sort((a,b)=>b[1]-a[1])[0];
    document.getElementById('rN').textContent=allRepos.length;
    document.getElementById('rS').textContent=stars;
    document.getElementById('rF').textContent=forks;
    document.getElementById('rW').textContent=watchers;
    document.getElementById('rL').textContent=tl?tl[0]:'—';
    document.getElementById('rstatbar').style.display='flex';
    document.getElementById('rctrl').style.display='flex';
    curFilter='all';curPage=1;
    document.querySelectorAll('.rfb').forEach(b=>b.classList.remove('on'));
    document.querySelector('.rfb[data-f="all"]').classList.add('on');
    document.getElementById('rsrch').value='';
    renderRepos();
  }catch(e){
    document.getElementById('repoArea').innerHTML=`<div class="err-box">⚠ FETCH FAILED<br/><span style="font-size:.6rem;opacity:.5">${e.message}</span><br/><span style="font-size:.55rem;color:#333">Check username spelling or try again</span></div>`;
  }
}

function setF(f,btn){
  curFilter=f;curPage=1;
  document.querySelectorAll('.rfb').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on');
  renderRepos();
}

function renderRepos(){
  const q=(document.getElementById('rsrch')||{value:''}).value.toLowerCase();
  const sort=(document.getElementById('rsrt')||{value:'updated'}).value;
  let rs=allRepos.filter(r=>{
    if(curFilter==='source'&&r.fork)return false;
    if(curFilter==='fork'&&!r.fork)return false;
    if(q&&!r.name.toLowerCase().includes(q)&&!(r.description||'').toLowerCase().includes(q))return false;
    return true;
  });
  const sortFns={stars:(a,b)=>b.stargazers_count-a.stargazers_count,name:(a,b)=>a.name.localeCompare(b.name),size:(a,b)=>b.size-a.size,forks:(a,b)=>b.forks_count-a.forks_count,updated:(a,b)=>new Date(b.updated_at)-new Date(a.updated_at)};
  rs.sort(sortFns[sort]||sortFns.updated);
  window._rs=rs;
  const pages=Math.ceil(rs.length/PPG);
  const slice=rs.slice((curPage-1)*PPG,curPage*PPG);
  const area=document.getElementById('repoArea');
  if(!slice.length){
    area.innerHTML='<div class="load-box"><div class="ltxt" style="color:#222">// NO REPOS FOUND</div></div>';
    document.getElementById('pager').innerHTML='';
    return;
  }
  area.innerHTML=`<div class="rgrid">${slice.map((r,i)=>repoCard(r,i)).join('')}</div>`;
  /* paginator */
  const pg=document.getElementById('pager');
  if(pages<=1){pg.innerHTML='';return;}
  let btns=`<button class="pgb" onclick="goPage(${curPage-1})" ${curPage===1?'disabled':''}>◀ PREV</button>`;
  for(let i=1;i<=pages;i++){
    if(i===1||i===pages||Math.abs(i-curPage)<=1){
      btns+=`<button class="pgb ${i===curPage?'cur':''}" onclick="goPage(${i})">${i}</button>`;
    } else if(Math.abs(i-curPage)===2){
      btns+=`<span style="color:#1a1a2e;padding:0 4px;font-size:11px">…</span>`;
    }
  }
  btns+=`<button class="pgb" onclick="goPage(${curPage+1})" ${curPage===pages?'disabled':''}>NEXT ▶</button>`;
  pg.innerHTML=btns;
}

function goPage(p){curPage=p;renderRepos();document.getElementById('repos').scrollIntoView({behavior:'smooth',block:'start'});}

function repoCard(r,idx){
  const col=LANG_C[r.language]||LANG_C.default;
  const upd=new Date(r.updated_at).toLocaleDateString('en-US',{month:'short',day:'numeric',year:'2-digit'});
  const topics=(r.topics||[]).slice(0,4).map(t=>`<span class="tp">${t}</span>`).join('');
  const delay=(idx%9)*0.05;
  return `<div class="rcard" style="animation:cardReveal .4s ease ${delay}s both" onclick="window.open('${r.html_url}','_blank')">
    <div>${r.fork?`<span class="rc-fork">FORK</span>`:''}<div class="rc-nm">📁 ${r.name}</div></div>
    <div class="rc-desc">${r.description||'<span style="color:#1a1a2e;font-style:italic">// no description</span>'}</div>
    ${topics?`<div class="rc-topics">${topics}</div>`:''}
    <div class="rc-foot">
      ${r.language?`<div class="rc-lang"><span class="lcdot" style="background:${col};box-shadow:0 0 6px ${col}88"></span><span class="lcnm">${r.language}</span></div>`:''}
      <span class="rc-st">★ ${r.stargazers_count}</span>
      <span class="rc-st">⑂ ${r.forks_count}</span>
      <span class="rc-dt">${upd}</span>
    </div>
  </div>`;
}

/* auto-fetch on load */
fetchRepos();
</script>
</body>
</html>
