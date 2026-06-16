[seif_portfolio (2).html](https://github.com/user-attachments/files/28999101/seif_portfolio.2.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0"/>
<title>Seif Elhdad · Video Editor</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{--black:#070b12;--black2:#0c1220;--white:#e8eef8;--accent:#4a8fff;--accent2:#7b5fff;--muted:#3a4a66;--border:rgba(74,143,255,.18)}
html{scroll-behavior:smooth}
body{background:var(--black);color:var(--white);font-family:'DM Sans',sans-serif;font-weight:300;overflow-x:hidden}

/* ── PARTICLES CANVAS ── */
#particles-canvas{position:fixed;inset:0;pointer-events:none;z-index:0;opacity:.5}

/* ── CURSOR GLOW ── */
.cursor-glow{position:fixed;width:300px;height:300px;border-radius:50%;background:radial-gradient(circle,rgba(74,143,255,.08) 0%,transparent 70%);pointer-events:none;z-index:1;transform:translate(-50%,-50%);transition:opacity .3s}

/* ── SCROLL PROGRESS ── */
.scroll-progress{position:fixed;top:0;left:0;height:2px;background:linear-gradient(90deg,var(--accent),var(--accent2));z-index:300;width:0;box-shadow:0 0 12px rgba(74,143,255,.8),0 0 24px rgba(123,95,255,.4)}

/* ── REVEAL ANIMATIONS ── */
.reveal{opacity:0;transform:translateY(40px);transition:opacity .9s cubic-bezier(.16,1,.3,1),transform .9s cubic-bezier(.16,1,.3,1)}
.reveal.from-left{transform:translateX(-60px) rotate(-1deg)}
.reveal.from-right{transform:translateX(60px) rotate(1deg)}
.reveal.scale-in{transform:scale(.88) translateY(20px)}
.reveal.flip-in{transform:perspective(800px) rotateX(15deg) translateY(30px);opacity:0}
.reveal.visible{opacity:1!important;transform:none!important}
.reveal-delay-1{transition-delay:.12s}.reveal-delay-2{transition-delay:.24s}
.reveal-delay-3{transition-delay:.36s}.reveal-delay-4{transition-delay:.48s}
@media(max-width:768px){.reveal{opacity:1!important;transform:none!important;transition:none!important}}

/* ── NAV ── */
nav{position:fixed;top:0;left:0;right:0;z-index:200;display:flex;align-items:center;justify-content:space-between;padding:1rem 2rem;background:rgba(7,11,18,.85);backdrop-filter:blur(20px);border-bottom:.5px solid var(--border);transition:background .3s}
nav.scrolled{background:rgba(7,11,18,.97)}
.nav-logo{font-family:'Playfair Display',serif;font-size:1.2rem;font-weight:700;letter-spacing:.05em;color:var(--accent);position:relative}
.nav-logo::after{content:'';position:absolute;bottom:-2px;left:0;width:0;height:1px;background:var(--accent);transition:width .4s}
.nav-logo:hover::after{width:100%}
.nav-desktop-links{display:flex;gap:1.5rem;list-style:none;align-items:center}
.nav-desktop-links a{text-decoration:none;color:var(--white);font-size:.75rem;letter-spacing:.12em;text-transform:uppercase;opacity:.6;transition:opacity .2s,color .2s,letter-spacing .3s}
.nav-desktop-links a:hover{opacity:1;color:var(--accent);letter-spacing:.18em}
.admin-btn{background:rgba(74,143,255,.12);border:.5px solid rgba(74,143,255,.35);color:var(--accent);padding:.4rem .9rem;font-family:'DM Sans',sans-serif;font-size:.68rem;letter-spacing:.12em;text-transform:uppercase;cursor:pointer;transition:background .2s,box-shadow .2s;border-radius:2px}
.admin-btn:hover{background:rgba(74,143,255,.25);box-shadow:0 0 16px rgba(74,143,255,.3)}
.hamburger{display:none;flex-direction:column;gap:5px;cursor:pointer;padding:.3rem;background:none;border:none}
.hamburger span{display:block;width:22px;height:1.5px;background:var(--white);transition:all .3s;transform-origin:center}
.hamburger.open span:nth-child(1){transform:rotate(45deg) translate(4.5px,4.5px)}
.hamburger.open span:nth-child(2){opacity:0;transform:scaleX(0)}
.hamburger.open span:nth-child(3){transform:rotate(-45deg) translate(4.5px,-4.5px)}
.mobile-menu{display:none;position:fixed;top:57px;left:0;right:0;background:rgba(7,11,18,.98);backdrop-filter:blur(20px);border-bottom:.5px solid var(--border);z-index:199;padding:1.2rem 1.5rem;flex-direction:column;gap:1rem}
.mobile-menu.open{display:flex;animation:slideDown .3s ease}
@keyframes slideDown{from{opacity:0;transform:translateY(-10px)}to{opacity:1;transform:translateY(0)}}
.mobile-menu a{text-decoration:none;color:var(--white);font-size:.9rem;letter-spacing:.1em;text-transform:uppercase;padding:.4rem 0;border-bottom:.5px solid rgba(74,143,255,.1);opacity:.8}

/* ── PASSWORD ── */
.pw-overlay{display:none;position:fixed;inset:0;z-index:997;background:rgba(7,11,18,.97);backdrop-filter:blur(10px);align-items:center;justify-content:center;padding:1rem}
.pw-overlay.open{display:flex;animation:fadeIn .3s ease}
.pw-box{background:#0c1422;border:.5px solid var(--border);padding:2rem;width:100%;max-width:360px;text-align:center;animation:scaleIn .3s ease}
@keyframes scaleIn{from{transform:scale(.9);opacity:0}to{transform:scale(1);opacity:1}}
.pw-box h3{font-family:'Playfair Display',serif;font-size:1.3rem;font-weight:700;margin-bottom:.4rem}
.pw-box p.desc{font-size:.8rem;color:rgba(232,238,248,.4);margin-bottom:1.5rem}
.pw-error{display:none;color:#ff6a6a;font-size:.75rem;margin-bottom:.8rem;animation:shake .3s ease}
@keyframes shake{0%,100%{transform:translateX(0)}25%{transform:translateX(-6px)}75%{transform:translateX(6px)}}
.pw-input{width:100%;background:rgba(74,143,255,.05);border:.5px solid rgba(74,143,255,.25);color:var(--white);padding:.85rem 1rem;font-family:'DM Sans',sans-serif;font-size:1rem;outline:none;text-align:center;letter-spacing:.15em;margin-bottom:.8rem;transition:border-color .2s,box-shadow .2s;-webkit-appearance:none}
.pw-input:focus{border-color:var(--accent);box-shadow:0 0 0 3px rgba(74,143,255,.1)}
.pw-input::placeholder{letter-spacing:.05em;color:rgba(232,238,248,.2)}
.pw-actions{display:flex;gap:.7rem}
.pw-submit{flex:1;background:var(--accent);color:#070b12;border:none;padding:.75rem;font-family:'DM Sans',sans-serif;font-size:.8rem;font-weight:500;letter-spacing:.1em;text-transform:uppercase;cursor:pointer;transition:background .2s,transform .15s}
.pw-submit:hover{background:#6aabff;transform:translateY(-1px)}
.pw-cancel{background:transparent;color:var(--white);border:.5px solid rgba(74,143,255,.25);padding:.75rem 1rem;font-family:'DM Sans',sans-serif;font-size:.8rem;text-transform:uppercase;cursor:pointer}

/* ── UPLOAD PANEL ── */
.upload-overlay{display:none;position:fixed;inset:0;z-index:998;background:rgba(7,11,18,.97);overflow-y:auto;-webkit-overflow-scrolling:touch}
.upload-overlay.open{display:block;animation:fadeIn .3s ease}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
.upload-panel{background:#0c1422;border:.5px solid var(--border);width:calc(100% - 2rem);max-width:560px;margin:1rem auto 3rem;padding:1.8rem;position:relative}
.upload-panel h2{font-family:'Playfair Display',serif;font-size:1.4rem;font-weight:700;margin-bottom:.3rem}
.upload-panel .sub{font-size:.78rem;color:rgba(232,238,248,.4);margin-bottom:1.6rem;line-height:1.6}
.upload-close{position:absolute;top:1rem;right:1rem;background:none;border:none;color:var(--muted);font-size:1.3rem;cursor:pointer;transition:color .2s,transform .2s}
.upload-close:hover{color:var(--white);transform:rotate(90deg)}
.upload-category{margin-bottom:1.5rem}
.upload-cat-label{font-size:.68rem;letter-spacing:.16em;text-transform:uppercase;color:var(--accent);margin-bottom:.6rem;display:flex;align-items:center;justify-content:space-between}
.upload-cat-count{font-size:.62rem;color:var(--muted);text-transform:none}
.upload-drop{border:.5px dashed rgba(74,143,255,.3);padding:.9rem;background:rgba(74,143,255,.03);display:flex;align-items:center;gap:.8rem;flex-wrap:wrap;transition:border-color .2s,background .2s}
.upload-drop:hover{border-color:rgba(74,143,255,.5);background:rgba(74,143,255,.06)}
.upload-pick-btn{background:rgba(74,143,255,.15);border:.5px solid rgba(74,143,255,.3);color:var(--accent);padding:.45rem 1rem;font-family:'DM Sans',sans-serif;font-size:.72rem;letter-spacing:.1em;text-transform:uppercase;cursor:pointer;transition:background .2s}
.upload-pick-btn:hover{background:rgba(74,143,255,.28)}
.upload-url-input{flex:1;min-width:160px;background:rgba(74,143,255,.05);border:.5px solid rgba(74,143,255,.2);color:var(--white);padding:.42rem .7rem;font-family:'DM Sans',sans-serif;font-size:.72rem;outline:none;transition:border-color .2s}
.upload-url-input:focus{border-color:var(--accent)}
.upload-url-input::placeholder{color:rgba(232,238,248,.2)}
.upload-url-btn{background:rgba(74,143,255,.2);border:.5px solid rgba(74,143,255,.35);color:var(--accent);padding:.42rem .8rem;font-family:'DM Sans',sans-serif;font-size:.7rem;text-transform:uppercase;letter-spacing:.08em;cursor:pointer;white-space:nowrap;transition:background .2s}
.upload-url-btn:hover{background:rgba(74,143,255,.35)}
.upload-hint{font-size:.68rem;color:rgba(232,238,248,.3);width:100%}
input[type="file"]{display:none}
.upload-file-list{margin-top:.6rem;display:flex;flex-direction:column;gap:.3rem}
.upload-file-item{display:flex;align-items:center;background:rgba(74,143,255,.05);border:.5px solid rgba(74,143,255,.1);padding:.45rem .75rem;gap:.7rem;animation:slideIn .2s ease}
@keyframes slideIn{from{opacity:0;transform:translateX(-10px)}to{opacity:1;transform:translateX(0)}}
.upload-file-name{font-size:.73rem;color:var(--accent);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;flex:1}
.upload-file-remove{background:none;border:none;color:var(--muted);cursor:pointer;font-size:.85rem;flex-shrink:0;transition:color .2s}
.upload-file-remove:hover{color:#ff6a6a}
.upload-actions{display:flex;gap:.7rem;margin-top:1.6rem;flex-wrap:wrap}
.btn-save{background:linear-gradient(135deg,var(--accent),var(--accent2));color:#fff;border:none;padding:.75rem 1.5rem;font-family:'DM Sans',sans-serif;font-size:.8rem;font-weight:500;letter-spacing:.1em;text-transform:uppercase;cursor:pointer;flex:1;min-width:140px;transition:transform .15s,box-shadow .2s}
.btn-save:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(74,143,255,.4)}
.btn-cancel-u{background:transparent;color:var(--white);border:.5px solid rgba(74,143,255,.25);padding:.75rem 1rem;font-family:'DM Sans',sans-serif;font-size:.8rem;text-transform:uppercase;cursor:pointer}
.upload-success{display:none;background:rgba(74,143,255,.1);border:.5px solid rgba(74,143,255,.3);color:var(--accent);padding:.6rem 1rem;font-size:.8rem;margin-top:.8rem;text-align:center;animation:pulse 1s ease}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.7}}

/* ── GALLERY MODAL ── */
.gallery-modal{display:none;position:fixed;inset:0;z-index:999;background:rgba(7,11,18,.99);flex-direction:column}
.gallery-modal.open{display:flex;animation:fadeIn .25s ease}
.gallery-header{display:flex;align-items:center;justify-content:space-between;padding:.9rem 1.2rem;border-bottom:.5px solid var(--border);flex-shrink:0;gap:.8rem}
.gallery-title{font-family:'Playfair Display',serif;font-size:1.1rem;font-weight:700;color:var(--accent)}
.gallery-meta{display:flex;align-items:center;gap:.8rem;flex-shrink:0}
.gallery-count{font-size:.7rem;color:var(--muted);letter-spacing:.08em}
.gallery-close-btn{background:none;border:.5px solid rgba(74,143,255,.3);color:var(--white);padding:.35rem .9rem;font-family:'DM Sans',sans-serif;font-size:.7rem;letter-spacing:.1em;text-transform:uppercase;cursor:pointer;transition:border-color .2s,color .2s}
.gallery-close-btn:hover{border-color:var(--accent);color:var(--accent)}
.gallery-body{display:flex;flex:1;overflow:hidden}
.gallery-player{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:1rem;background:#040609;overflow:hidden;min-height:0}
.gallery-player video,.gallery-player iframe{width:100%;max-width:840px;aspect-ratio:16/9;background:#000;outline:none;border:.5px solid var(--border)}
.gallery-player iframe{border:none}
.gallery-empty{color:rgba(232,238,248,.3);font-size:.85rem;text-align:center;line-height:1.8;padding:1rem}
.gallery-empty strong{color:var(--accent);display:block;font-size:.95rem;margin-bottom:.4rem}
.gallery-sidebar{width:190px;flex-shrink:0;border-left:.5px solid var(--border);overflow-y:auto;background:var(--black2);-webkit-overflow-scrolling:touch}
.gallery-thumb{display:flex;flex-direction:column;padding:.75rem .9rem;border-bottom:.5px solid var(--border);cursor:pointer;transition:background .2s,border-left .2s;gap:.2rem}
.gallery-thumb:hover{background:rgba(74,143,255,.08)}
.gallery-thumb.active{background:rgba(74,143,255,.13);border-left:2px solid var(--accent)}
.gallery-thumb-num{font-size:.58rem;color:var(--muted);letter-spacing:.12em;text-transform:uppercase}
.gallery-thumb-name{font-size:.76rem;color:var(--white);line-height:1.3;word-break:break-word}
.gallery-thumb-type{font-size:.58rem;color:rgba(74,143,255,.5);letter-spacing:.08em}
.gallery-thumb.active .gallery-thumb-name{color:var(--accent)}
.gallery-no-videos{padding:1.5rem 1rem;text-align:center;color:var(--muted);font-size:.75rem;line-height:1.6}
.gallery-sidebar::-webkit-scrollbar{width:3px}
.gallery-sidebar::-webkit-scrollbar-thumb{background:rgba(74,143,255,.3);border-radius:2px}

/* ── HERO ── */
.hero{min-height:100vh;display:flex;flex-direction:column;justify-content:flex-end;padding:0 2rem 3.5rem;position:relative;overflow:hidden;z-index:1}
.hero-bg{position:absolute;inset:0;background:radial-gradient(ellipse 80% 60% at 70% 40%,#0d2147 0%,#070b12 65%)}
.hero-grid{position:absolute;inset:0;background-image:linear-gradient(rgba(74,143,255,.05) 1px,transparent 1px),linear-gradient(90deg,rgba(74,143,255,.05) 1px,transparent 1px);background-size:60px 60px;animation:gridPan 25s linear infinite}
@keyframes gridPan{from{background-position:0 0}to{background-position:60px 60px}}

/* Multiple glows */
.hero-glow-1{position:absolute;top:10%;right:5%;width:40vw;height:40vw;max-width:420px;max-height:420px;background:radial-gradient(circle,rgba(74,143,255,.15) 0%,transparent 70%);pointer-events:none;animation:glowFloat1 6s ease-in-out infinite}
.hero-glow-2{position:absolute;bottom:20%;left:10%;width:30vw;height:30vw;max-width:320px;max-height:320px;background:radial-gradient(circle,rgba(123,95,255,.1) 0%,transparent 70%);pointer-events:none;animation:glowFloat2 8s ease-in-out infinite}
.hero-glow-3{position:absolute;top:40%;left:30%;width:20vw;height:20vw;max-width:200px;max-height:200px;background:radial-gradient(circle,rgba(74,143,255,.07) 0%,transparent 70%);pointer-events:none;animation:glowFloat3 5s ease-in-out infinite}
@keyframes glowFloat1{0%,100%{transform:translate(0,0) scale(1)}33%{transform:translate(-20px,15px) scale(1.1)}66%{transform:translate(15px,-10px) scale(.95)}}
@keyframes glowFloat2{0%,100%{transform:translate(0,0) scale(1)}50%{transform:translate(20px,-20px) scale(1.15)}}
@keyframes glowFloat3{0%,100%{transform:translate(0,0)}50%{transform:translate(-15px,20px)}}

/* Animated lines */
.hero-lines{position:absolute;inset:0;overflow:hidden;pointer-events:none}
.hero-line-anim{position:absolute;width:1px;background:linear-gradient(to bottom,transparent,rgba(74,143,255,.3),transparent);animation:lineRise 4s ease-in-out infinite}
.hero-line-anim:nth-child(1){left:15%;height:200px;animation-delay:0s;animation-duration:5s}
.hero-line-anim:nth-child(2){left:40%;height:150px;animation-delay:1.5s;animation-duration:4s}
.hero-line-anim:nth-child(3){left:70%;height:250px;animation-delay:.8s;animation-duration:6s}
.hero-line-anim:nth-child(4){left:85%;height:120px;animation-delay:2s;animation-duration:3.5s}
@keyframes lineRise{0%{top:100%;opacity:0}20%{opacity:1}80%{opacity:1}100%{top:-20%;opacity:0}}

.hero-eyebrow{position:relative;font-size:.68rem;letter-spacing:.22em;text-transform:uppercase;color:var(--accent);margin-bottom:1rem;display:flex;align-items:center;gap:.8rem;animation:fadeUp .8s ease both .3s}
.hero-eyebrow::before{content:'';display:block;width:28px;height:1px;background:var(--accent);opacity:.7}

/* TYPEWRITER effect for title */
.hero-title{position:relative;font-family:'Playfair Display',serif;font-size:clamp(2.6rem,9vw,7rem);font-weight:900;line-height:.95;letter-spacing:-.02em;margin-bottom:1.4rem;animation:fadeUp .8s ease both .5s}
.hero-title em{font-style:italic;background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;animation:gradientShift 4s ease-in-out infinite}
@keyframes gradientShift{0%,100%{filter:hue-rotate(0deg)}50%{filter:hue-rotate(30deg)}}

.hero-sub{position:relative;max-width:480px;font-size:.92rem;line-height:1.7;color:rgba(232,238,248,.5);margin-bottom:2rem;animation:fadeUp .8s ease both .7s}
.hero-cta{position:relative;display:flex;gap:.75rem;align-items:center;flex-wrap:wrap;animation:fadeUp .8s ease both .9s}

/* Floating badges in hero */
.hero-badges{position:absolute;top:30%;right:8%;display:flex;flex-direction:column;gap:.8rem;animation:fadeUp 1s ease both 1.1s}
.hero-badge{background:rgba(7,11,18,.8);border:.5px solid rgba(74,143,255,.25);padding:.5rem 1rem;font-size:.65rem;letter-spacing:.12em;text-transform:uppercase;color:rgba(232,238,248,.6);backdrop-filter:blur(8px);animation:badgeFloat 3s ease-in-out infinite}
.hero-badge:nth-child(2){animation-delay:.8s}
.hero-badge:nth-child(3){animation-delay:1.6s}
.hero-badge span{color:var(--accent);margin-right:.4rem}
@keyframes badgeFloat{0%,100%{transform:translateY(0)}50%{transform:translateY(-6px)}}

.hero-scroll-hint{position:absolute;bottom:1.5rem;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;align-items:center;gap:.5rem;animation:fadeUp 1s ease both 1.3s}
.hero-scroll-hint span{font-size:.58rem;letter-spacing:.2em;text-transform:uppercase;color:rgba(74,143,255,.5)}
.hero-scroll-dot{width:4px;height:4px;border-radius:50%;background:var(--accent);animation:scrollBounce 1.5s ease-in-out infinite}
@keyframes scrollBounce{0%,100%{transform:translateY(0);opacity:1}50%{transform:translateY(10px);opacity:.3}}

@keyframes fadeUp{from{opacity:0;transform:translateY(26px)}to{opacity:1;transform:translateY(0)}}

.btn-primary{background:linear-gradient(135deg,var(--accent),var(--accent2));color:#fff;border:none;padding:.75rem 1.6rem;font-family:'DM Sans',sans-serif;font-size:.76rem;font-weight:500;letter-spacing:.12em;text-transform:uppercase;cursor:pointer;transition:transform .2s,box-shadow .2s;position:relative;overflow:hidden}
.btn-primary::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,var(--accent2),var(--accent));opacity:0;transition:opacity .3s}
.btn-primary:hover::before{opacity:1}
.btn-primary:hover{transform:translateY(-3px);box-shadow:0 12px 32px rgba(74,143,255,.4)}
.btn-primary span{position:relative;z-index:1}
.btn-ghost{background:transparent;color:var(--white);border:.5px solid rgba(74,143,255,.4);padding:.75rem 1.6rem;font-family:'DM Sans',sans-serif;font-size:.76rem;letter-spacing:.12em;text-transform:uppercase;cursor:pointer;transition:border-color .2s,color .2s,box-shadow .2s,background .2s}
.btn-ghost:hover{border-color:var(--accent);color:var(--accent);box-shadow:0 0 20px rgba(74,143,255,.15);background:rgba(74,143,255,.05)}

/* ── MARQUEE ── */
.marquee-wrap{background:linear-gradient(90deg,var(--accent),var(--accent2),var(--accent));background-size:200% 100%;animation:gradientMove 4s linear infinite;overflow:hidden;padding:.55rem 0}
@keyframes gradientMove{0%{background-position:0% 50%}100%{background-position:200% 50%}}
.marquee-track{display:flex;white-space:nowrap;animation:marquee 22s linear infinite}
.marquee-track span{color:#fff;font-size:.66rem;font-weight:500;letter-spacing:.16em;text-transform:uppercase;padding:0 1.5rem;opacity:.9}
.marquee-track span::after{content:'★';margin-left:1.5rem;font-size:.5rem}
@keyframes marquee{from{transform:translateX(0)}to{transform:translateX(-50%)}}

/* ── SECTIONS ── */
section{padding:5rem 2rem;position:relative;z-index:1}
.section-label{font-size:.63rem;letter-spacing:.22em;text-transform:uppercase;color:var(--accent);margin-bottom:2.5rem;display:flex;align-items:center;gap:.8rem}
.section-label::before{content:attr(data-num);font-family:'Playfair Display',serif;font-size:3rem;font-weight:900;opacity:.06;position:absolute;left:2rem;top:-1rem;color:var(--accent);pointer-events:none}
.section-label::after{content:'';flex:1;height:.5px;background:linear-gradient(90deg,var(--border),transparent)}

/* ── WORK GRID ── */
.work-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.2rem;margin-top:1.5rem}
.work-card{position:relative;overflow:hidden;aspect-ratio:16/10;background:#0c1422;border:.5px solid var(--border);cursor:pointer;transition:border-color .4s,transform .4s cubic-bezier(.16,1,.3,1),box-shadow .4s}
.work-card::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(74,143,255,.1),rgba(123,95,255,.1));opacity:0;transition:opacity .4s;z-index:1}
.work-card:hover{border-color:rgba(74,143,255,.6);transform:translateY(-8px) scale(1.01);box-shadow:0 24px 60px rgba(74,143,255,.2),0 0 0 1px rgba(74,143,255,.1)}
.work-card:hover::before{opacity:1}
.work-card.featured{grid-column:span 2;aspect-ratio:21/9}
.work-card-icon{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-size:4rem;opacity:.07;user-select:none;transition:opacity .4s,transform .6s;z-index:0}
.work-card:hover .work-card-icon{opacity:.15;transform:scale(1.2) rotate(5deg)}
.work-card-inner{position:absolute;inset:0;padding:1rem;display:flex;flex-direction:column;justify-content:flex-end;background:linear-gradient(to top,rgba(7,11,18,.97) 0%,rgba(7,11,18,.4) 50%,transparent 100%);z-index:2;transition:padding-bottom .3s}
.work-card:hover .work-card-inner{padding-bottom:1.4rem}
.work-card-play{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);width:52px;height:52px;border:1.5px solid rgba(74,143,255,.5);border-radius:50%;display:flex;align-items:center;justify-content:center;color:var(--accent);font-size:1.1rem;transition:all .3s;z-index:2;background:rgba(7,11,18,.3);backdrop-filter:blur(4px)}
.work-card:hover .work-card-play{border-color:var(--accent);background:rgba(74,143,255,.2);transform:translate(-50%,-50%) scale(1.2);box-shadow:0 0 0 8px rgba(74,143,255,.1),0 0 40px rgba(74,143,255,.4)}
.work-title{font-family:'Playfair Display',serif;font-size:clamp(1rem,3.5vw,1.5rem);font-weight:900;color:var(--white);transition:transform .3s,color .3s}
.work-card:hover .work-title{color:var(--accent);transform:translateX(4px)}
.work-card-sub{font-size:.62rem;color:rgba(74,143,255,.6);margin-top:.25rem;transition:transform .3s}
.work-card:hover .work-card-sub{transform:translateX(4px)}
.work-label{position:absolute;top:.7rem;left:.7rem;font-size:.56rem;letter-spacing:.14em;text-transform:uppercase;color:#fff;background:linear-gradient(135deg,var(--accent),var(--accent2));padding:.22rem .55rem;z-index:3}
.video-count-badge{position:absolute;top:.7rem;right:.7rem;background:rgba(7,11,18,.8);border:.5px solid rgba(74,143,255,.4);color:var(--accent);font-size:.6rem;letter-spacing:.08em;padding:.24rem .6rem;z-index:3;backdrop-filter:blur(4px);transition:background .3s}
.work-card:hover .video-count-badge{background:rgba(74,143,255,.2)}
.tint-ads{background:linear-gradient(135deg,#081428 0%,#070b12 100%)}
.tint-ground{background:linear-gradient(135deg,#071020 0%,#070b12 100%)}
.tint-event{background:linear-gradient(135deg,#0a1530 0%,#070b12 100%)}
.tint-show{background:linear-gradient(135deg,#0d1a38 0%,#070b12 100%)}

/* Shimmer effect on cards */
.work-card::after{content:'';position:absolute;top:-100%;left:-100%;width:60%;height:200%;background:linear-gradient(105deg,transparent 40%,rgba(255,255,255,.03) 50%,transparent 60%);transition:transform .6s;transform:skewX(-15deg);z-index:3}
.work-card:hover::after{transform:skewX(-15deg) translateX(400%)}

/* ── COUNTERS ── */
.counter-section{background:var(--black2);padding:4rem 2rem;position:relative;overflow:hidden;z-index:1}
.counter-section::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(74,143,255,.03),rgba(123,95,255,.03));pointer-events:none}
.counters{display:grid;grid-template-columns:repeat(4,1fr);gap:1.5rem}
.counter-card{text-align:center;padding:2rem 1rem;border:.5px solid var(--border);position:relative;overflow:hidden;transition:border-color .3s,transform .3s;cursor:default}
.counter-card::before{content:'';position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--accent),var(--accent2));transform:scaleX(0);transition:transform .4s;transform-origin:left}
.counter-card:hover::before{transform:scaleX(1)}
.counter-card:hover{border-color:rgba(74,143,255,.4);transform:translateY(-4px)}
.counter-card::after{content:'';position:absolute;inset:0;background:radial-gradient(circle at 50% 100%,rgba(74,143,255,.08),transparent 70%)}
.counter-num{font-family:'Playfair Display',serif;font-size:2.6rem;font-weight:900;background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;line-height:1;display:block}
.counter-label{font-size:.62rem;letter-spacing:.12em;text-transform:uppercase;color:rgba(232,238,248,.4);margin-top:.5rem}

/* ── SERVICES ── */
.services-list{margin-top:1.5rem}
.service-row{display:flex;align-items:center;justify-content:space-between;padding:1.5rem 0;border-bottom:.5px solid var(--border);position:relative;overflow:hidden;transition:padding-left .35s,background .3s}
.service-row::before{content:'';position:absolute;left:0;top:0;bottom:0;width:0;background:linear-gradient(90deg,rgba(74,143,255,.08),transparent);transition:width .5s cubic-bezier(.16,1,.3,1)}
.service-row:hover::before{width:100%}
.service-row:hover{padding-left:.8rem}
.service-row:hover .service-num{color:var(--accent)}
.service-row:hover .service-arrow{color:var(--accent);transform:translateX(8px)}
.service-left{display:flex;align-items:center;gap:1.4rem;position:relative;flex:1}
.service-num{font-family:'Playfair Display',serif;font-size:.85rem;color:var(--muted);transition:color .3s;flex-shrink:0}
.service-name{font-size:1.05rem;font-weight:400;transition:letter-spacing .3s}
.service-row:hover .service-name{letter-spacing:.02em}
.service-arrow{color:var(--muted);font-size:.9rem;transition:color .3s,transform .4s cubic-bezier(.16,1,.3,1);flex-shrink:0}

/* Long/Short Form Cards */
.form-section{padding:2rem 0;border-bottom:.5px solid var(--border)}
.form-section-label{font-size:.6rem;letter-spacing:.2em;text-transform:uppercase;color:var(--muted);margin-bottom:1rem}
.form-cards{display:grid;grid-template-columns:1fr 1fr;gap:.8rem}
.form-card{border:.5px solid rgba(74,143,255,.2);padding:1.4rem;transition:border-color .3s,background .3s,transform .3s;position:relative;overflow:hidden}
.form-card::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(74,143,255,.05),rgba(123,95,255,.05));opacity:0;transition:opacity .3s}
.form-card:hover::before{opacity:1}
.form-card:hover{border-color:rgba(74,143,255,.5);transform:translateY(-3px)}
.form-card-title{font-family:'Playfair Display',serif;font-size:1.1rem;font-weight:700;color:var(--white);margin-bottom:.5rem;transition:color .3s}
.form-card:hover .form-card-title{color:var(--accent)}
.form-card-desc{font-size:.72rem;color:rgba(232,238,248,.45);line-height:1.6}

/* ── CONTACT ── */
.contact-inner{display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:start}
.contact-headline{font-family:'Playfair Display',serif;font-size:clamp(1.8rem,4.5vw,2.8rem);font-weight:900;line-height:1.1;margin-bottom:1.6rem}
.contact-headline em{font-style:italic;background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.contact-info{display:flex;flex-direction:column;gap:1.1rem}
.contact-item{display:flex;align-items:center;gap:.9rem;transition:transform .2s,padding-left .2s}
.contact-item:hover{transform:translateX(6px)}
.contact-item-icon{color:var(--accent);font-size:1rem;width:18px;text-align:center}
.contact-item-link{font-size:.86rem;color:var(--accent);text-decoration:none;transition:color .2s}
.contact-item-link:hover{color:var(--accent2)}
.contact-item-text{font-size:.86rem;color:rgba(232,238,248,.6)}
.contact-form{display:flex;flex-direction:column;gap:.85rem}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:.85rem}
.form-field{display:flex;flex-direction:column;gap:.4rem}
.form-label{font-size:.65rem;letter-spacing:.14em;text-transform:uppercase;color:var(--muted);transition:color .2s}
.form-field:focus-within .form-label{color:var(--accent)}
.form-input{background:rgba(74,143,255,.04);border:.5px solid rgba(74,143,255,.2);color:var(--white);padding:.78rem .9rem;font-family:'DM Sans',sans-serif;font-size:.86rem;outline:none;transition:border-color .2s,box-shadow .2s,background .2s;width:100%;-webkit-appearance:none;border-radius:0}
.form-input:focus{border-color:var(--accent);box-shadow:0 0 0 3px rgba(74,143,255,.08);background:rgba(74,143,255,.06)}
.form-input::placeholder{color:rgba(232,238,248,.2)}
textarea.form-input{resize:vertical;min-height:100px}
.form-status{display:none;padding:.65rem .9rem;font-size:.78rem;margin-top:.4rem;text-align:center;animation:fadeIn .3s ease}
.form-status.success{background:rgba(74,143,255,.1);border:.5px solid rgba(74,143,255,.3);color:var(--accent)}
.form-status.error{background:rgba(255,80,80,.1);border:.5px solid rgba(255,80,80,.3);color:#ff8080}

footer{padding:1.5rem 2rem;border-top:.5px solid var(--border);display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:.8rem;position:relative;z-index:1}
.footer-copy{font-size:.72rem;color:var(--muted)}
.footer-social{display:flex;gap:1.1rem;flex-wrap:wrap}
.footer-social a{color:var(--muted);font-size:.72rem;letter-spacing:.1em;text-transform:uppercase;text-decoration:none;transition:color .2s,transform .2s;display:inline-block}
.footer-social a:hover{color:var(--accent);transform:translateY(-3px)}

/* ── MOBILE ── */
@media(max-width:768px){
  nav{padding:.85rem 1.2rem}
  .nav-desktop-links{display:none}
  .hamburger{display:flex}
  .hero-badges{display:none}
  .hero-scroll-hint{display:none}
  section{padding:3.5rem 1.2rem}
  .counter-section{padding:3rem 1.2rem}
  .hero{padding:0 1.2rem 3rem}
  .work-grid{grid-template-columns:1fr;gap:.9rem}
  .work-card.featured{grid-column:span 1;aspect-ratio:16/9}
  .work-card{aspect-ratio:16/9}
  .counters{grid-template-columns:1fr 1fr;gap:.9rem}
  .counter-num{font-size:2rem}
  .service-name{font-size:.95rem}
  .form-cards{grid-template-columns:1fr}
  .contact-inner{grid-template-columns:1fr;gap:2.2rem}
  .form-row{grid-template-columns:1fr}
  .contact-headline{font-size:1.9rem}
  .gallery-body{flex-direction:column}
  .gallery-player{padding:.8rem;min-height:0}
  .gallery-sidebar{width:100%;border-left:none;border-top:.5px solid var(--border);max-height:160px}
  footer{padding:1.3rem 1.2rem}
}
@media(max-width:420px){
  .hero-title{font-size:2.4rem}
  .counters{gap:.7rem}
  .counter-num{font-size:1.8rem}
}
</style>
</head>
<body>

<canvas id="particles-canvas"></canvas>
<div class="cursor-glow" id="cursorGlow"></div>
<div class="scroll-progress" id="scrollProgress"></div>

<!-- PASSWORD GATE -->
<div class="pw-overlay" id="pwOverlay">
  <div class="pw-box">
    <h3>Admin Access</h3>
    <p class="desc">Enter your password to update videos</p>
    <p class="pw-error" id="pwError">Incorrect password. Try again.</p>
    <input class="pw-input" id="pwInput" type="password" placeholder="Enter password" onkeydown="if(event.key==='Enter')checkPw()"/>
    <div class="pw-actions">
      <button class="pw-submit" onclick="checkPw()">Unlock</button>
      <button class="pw-cancel" onclick="closePw()">Cancel</button>
    </div>
  </div>
</div>

<!-- UPLOAD PANEL -->
<div class="upload-overlay" id="uploadOverlay">
  <div class="upload-panel">
    <button class="upload-close" onclick="closeUpload()">✕</button>
    <h2>Update Videos</h2>
    <p class="sub">Add video files OR paste YouTube/Vimeo links. Both work — mix as you like.</p>
    <div class="upload-category">
      <div class="upload-cat-label">📢 Ads <span class="upload-cat-count" id="uc-ads">0 videos</span></div>
      <div class="upload-drop">
        <button class="upload-pick-btn" onclick="document.getElementById('fi-ads').click()">+ File</button>
        <input class="upload-url-input" id="url-ads" placeholder="or paste YouTube / Vimeo link"/>
        <button class="upload-url-btn" onclick="addURL('ads')">Add Link</button>
        <input type="file" id="fi-ads" accept="video/*" multiple onchange="handleFiles('ads',this)"/>
        <span class="upload-hint">mp4 · mov · webm · YouTube · Vimeo</span>
      </div>
      <div class="upload-file-list" id="ul-ads"></div>
    </div>
    <div class="upload-category">
      <div class="upload-cat-label">📱 Social Media <span class="upload-cat-count" id="uc-ground">0 videos</span></div>
      <div class="upload-drop">
        <button class="upload-pick-btn" onclick="document.getElementById('fi-ground').click()">+ File</button>
        <input class="upload-url-input" id="url-ground" placeholder="or paste YouTube / Vimeo link"/>
        <button class="upload-url-btn" onclick="addURL('ground')">Add Link</button>
        <input type="file" id="fi-ground" accept="video/*" multiple onchange="handleFiles('ground',this)"/>
        <span class="upload-hint">mp4 · mov · webm · YouTube · Vimeo</span>
      </div>
      <div class="upload-file-list" id="ul-ground"></div>
    </div>
    <div class="upload-category">
      <div class="upload-cat-label">🎬 Event Coverage <span class="upload-cat-count" id="uc-event">0 videos</span></div>
      <div class="upload-drop">
        <button class="upload-pick-btn" onclick="document.getElementById('fi-event').click()">+ File</button>
        <input class="upload-url-input" id="url-event" placeholder="or paste YouTube / Vimeo link"/>
        <button class="upload-url-btn" onclick="addURL('event')">Add Link</button>
        <input type="file" id="fi-event" accept="video/*" multiple onchange="handleFiles('event',this)"/>
        <span class="upload-hint">mp4 · mov · webm · YouTube · Vimeo</span>
      </div>
      <div class="upload-file-list" id="ul-event"></div>
    </div>
    <div class="upload-category">
      <div class="upload-cat-label">🎭 Shows <span class="upload-cat-count" id="uc-shows">0 videos</span></div>
      <div class="upload-drop">
        <button class="upload-pick-btn" onclick="document.getElementById('fi-shows').click()">+ File</button>
        <input class="upload-url-input" id="url-shows" placeholder="or paste YouTube / Vimeo link"/>
        <button class="upload-url-btn" onclick="addURL('shows')">Add Link</button>
        <input type="file" id="fi-shows" accept="video/*" multiple onchange="handleFiles('shows',this)"/>
        <span class="upload-hint">mp4 · mov · webm · YouTube · Vimeo</span>
      </div>
      <div class="upload-file-list" id="ul-shows"></div>
    </div>
    <div class="upload-actions">
      <button class="btn-save" onclick="applyVideos()"><span>✓ Apply All Videos</span></button>
      <button class="btn-cancel-u" onclick="closeUpload()">Cancel</button>
    </div>
    <div class="upload-success" id="uploadSuccess">✓ Videos applied successfully!</div>
  </div>
</div>

<!-- GALLERY MODAL -->
<div class="gallery-modal" id="galleryModal">
  <div class="gallery-header">
    <div class="gallery-title" id="galleryTitle">Ads</div>
    <div class="gallery-meta">
      <span class="gallery-count" id="galleryCount">0 videos</span>
      <button class="gallery-close-btn" onclick="closeGallery()">✕ Close</button>
    </div>
  </div>
  <div class="gallery-body">
    <div class="gallery-player">
      <div class="gallery-empty" id="galleryEmpty"><strong>No videos yet</strong>Videos appear here once uploaded.</div>
      <video id="galleryVideo" controls playsinline webkit-playsinline style="display:none"></video>
      <iframe id="galleryFrame" style="display:none;width:100%;max-width:840px;aspect-ratio:16/9;border:none" allowfullscreen allow="autoplay; encrypted-media"></iframe>
    </div>
    <div class="gallery-sidebar" id="gallerySidebar"><div class="gallery-no-videos">No videos uploaded yet.</div></div>
  </div>
</div>

<!-- NAV -->
<nav id="mainNav">
  <div class="nav-logo">Seif</div>
  <ul class="nav-desktop-links">
    <li><a href="#work">Work</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><button class="admin-btn" onclick="openPw()">⚙ Update Videos</button></li>
  </ul>
  <button class="hamburger" id="hamburger" onclick="toggleMenu()" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>

<div class="mobile-menu" id="mobileMenu">
  <a href="#work" onclick="closeMenu()">Work</a>
  <a href="#services" onclick="closeMenu()">Services</a>
  <a href="#contact" onclick="closeMenu()">Contact</a>
  <button class="admin-btn" style="align-self:flex-start;margin-top:.3rem" onclick="closeMenu();openPw()">⚙ Update Videos</button>
</div>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-grid"></div>
  <div class="hero-glow-1"></div>
  <div class="hero-glow-2"></div>
  <div class="hero-glow-3"></div>
  <div class="hero-lines">
    <div class="hero-line-anim"></div>
    <div class="hero-line-anim"></div>
    <div class="hero-line-anim"></div>
    <div class="hero-line-anim"></div>
  </div>
  <div class="hero-badges">
    <div class="hero-badge"><span>✦</span>Video Editor</div>
    <div class="hero-badge"><span>✦</span>AI Creator</div>
    <div class="hero-badge"><span>✦</span>Cairo, Egypt</div>
  </div>
  <p class="hero-eyebrow">Video Editor · AI Video Creator</p>
  <h1 class="hero-title">Crafting<br><em>stories</em><br>frame by frame.</h1>
  <p class="hero-sub">Professional video editing that transforms raw footage into compelling visual narratives — ads, social media, events, shows, and more.</p>
  <div class="hero-cta">
    <button class="btn-primary" onclick="document.getElementById('work').scrollIntoView({behavior:'smooth'})"><span>View My Work</span></button>
    <button class="btn-ghost" onclick="document.getElementById('contact').scrollIntoView({behavior:'smooth'})">Get in Touch</button>
  </div>
  <div class="hero-scroll-hint"><span>Scroll</span><div class="hero-scroll-dot"></div></div>
</section>

<!-- MARQUEE -->
<div class="marquee-wrap"><div class="marquee-track">
  <span>Advertisements</span><span>Social Media Content</span><span>Event Coverage</span><span>Shows & Performances</span><span>AI Video Creation</span><span>Long Form</span><span>Short Form</span>
  <span>Advertisements</span><span>Social Media Content</span><span>Event Coverage</span><span>Shows & Performances</span><span>AI Video Creation</span><span>Long Form</span><span>Short Form</span>
</div></div>

<!-- WORK -->
<section id="work">
  <p class="section-label reveal" data-num="01">Selected Work</p>
  <div class="work-grid">
    <div class="work-card featured tint-ads reveal scale-in" onclick="openGallery('ads')">
      <div class="work-card-icon">📢</div><div class="work-card-play">▶</div>
      <div class="work-label">Featured</div>
      <div class="video-count-badge" id="count-ads">0 Videos</div>
      <div class="work-card-inner"><p class="work-title">Ads</p><p class="work-card-sub">Tap to browse all videos</p></div>
    </div>
    <div class="work-card tint-ground reveal reveal-delay-1" onclick="openGallery('ground')">
      <div class="work-card-icon">📱</div><div class="work-card-play">▶</div>
      <div class="video-count-badge" id="count-ground">0 Videos</div>
      <div class="work-card-inner"><p class="work-title">Social Media</p><p class="work-card-sub">Tap to browse all videos</p></div>
    </div>
    <div class="work-card tint-event reveal reveal-delay-2" onclick="openGallery('event')">
      <div class="work-card-icon">🎬</div><div class="work-card-play">▶</div>
      <div class="video-count-badge" id="count-event">0 Videos</div>
      <div class="work-card-inner"><p class="work-title">Event Coverage</p><p class="work-card-sub">Tap to browse all videos</p></div>
    </div>
    <div class="work-card featured tint-show reveal scale-in reveal-delay-1" onclick="openGallery('shows')">
      <div class="work-card-icon">🎭</div><div class="work-card-play">▶</div>
      <div class="video-count-badge" id="count-shows">0 Videos</div>
      <div class="work-card-inner"><p class="work-title">Shows</p><p class="work-card-sub">Tap to browse all videos</p></div>
    </div>
  </div>
</section>

<!-- COUNTERS -->
<div class="counter-section">
  <div class="counters">
    <div class="counter-card"><span class="counter-num" data-target="1">1</span>+<p class="counter-label">Year Experience</p></div>
    <div class="counter-card"><span class="counter-num" data-target="80">80</span>+<p class="counter-label">Projects Done</p></div>
    <div class="counter-card"><span class="counter-num" data-target="8">8</span>+<p class="counter-label">Happy Clients</p></div>
    <div class="counter-card"><span class="counter-num" data-target="4">4</span>K<p class="counter-label">Max Resolution</p></div>
  </div>
</div>

<!-- SERVICES -->
<section id="services" style="background:var(--black2)">
  <p class="section-label reveal" data-num="02">Services</p>
  <div class="services-list">
    <div class="service-row reveal reveal-delay-1"><div class="service-left"><span class="service-num">01</span><span class="service-name">Advertisements & Commercial Editing</span></div><span class="service-arrow">→</span></div>
    <div class="service-row reveal reveal-delay-2"><div class="service-left"><span class="service-num">02</span><span class="service-name">Generate AI Video</span></div><span class="service-arrow">→</span></div>
    <div class="service-row reveal reveal-delay-3"><div class="service-left"><span class="service-num">03</span><span class="service-name">Social Media Content</span></div><span class="service-arrow">→</span></div>
    <div class="service-row reveal reveal-delay-4"><div class="service-left"><span class="service-num">04</span><span class="service-name">Shows, Concerts & Live Performances</span></div><span class="service-arrow">→</span></div>
    <div class="form-section reveal">
      <div class="form-section-label">Available Formats</div>
      <div class="form-cards">
        <div class="form-card"><div class="form-card-title">Long Form</div><div class="form-card-desc">Full-length edits, documentaries, event recaps, brand films, and show coverage</div></div>
        <div class="form-card"><div class="form-card-title">Short Form</div><div class="form-card-desc">Reels, TikToks, ads, teasers, trailers, and social media highlights</div></div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <p class="section-label reveal" data-num="03">Contact</p>
  <div class="contact-inner">
    <div class="reveal from-left">
      <h2 class="contact-headline">Let's create something <em>great</em> together.</h2>
      <div class="contact-info">
        <div class="contact-item"><span class="contact-item-icon">✉</span><a class="contact-item-link" href="mailto:seifelden625@gmail.com">seifelden625@gmail.com</a></div>
        <div class="contact-item"><span class="contact-item-icon">📞</span><a class="contact-item-link" href="tel:+201020080936">+20 102 008 0936</a></div>
        <div class="contact-item"><span class="contact-item-icon">📍</span><span class="contact-item-text">Nozha, Cairo · Egypt</span></div>
        <div class="contact-item"><span class="contact-item-icon">💼</span><a class="contact-item-link" href="https://www.linkedin.com/in/seif-elhdad-9b8906257" target="_blank">linkedin.com/in/seif-elhdad</a></div>
      </div>
    </div>
    <div class="contact-form reveal from-right">
      <div class="form-row">
        <div class="form-field"><label class="form-label">Name</label><input type="text" class="form-input" id="cf-name" placeholder="Your name"/></div>
        <div class="form-field"><label class="form-label">Email</label><input type="email" class="form-input" id="cf-email" placeholder="your@email.com"/></div>
      </div>
      <div class="form-field"><label class="form-label">Project type</label><input type="text" class="form-input" id="cf-project" placeholder="e.g. Ad, Social media, Show..."/></div>
      <div class="form-field"><label class="form-label">Message</label><textarea class="form-input" id="cf-message" placeholder="Tell me about your project..."></textarea></div>
      <button class="btn-primary" style="align-self:flex-start" onclick="sendMessage()"><span>Send Message</span></button>
      <div class="form-status" id="formStatus"></div>
    </div>
  </div>
</section>

<footer>
  <p class="footer-copy">© 2025 Seif Elhdad · Video Editor</p>
  <div class="footer-social">
    <a href="https://www.linkedin.com/in/seif-elhdad-9b8906257" target="_blank">LinkedIn</a>
    <a href="#">Instagram</a><a href="#">Behance</a><a href="#">YouTube</a>
  </div>
</footer>

<script>
// ── PARTICLES ──
(function(){
  const canvas=document.getElementById('particles-canvas');
  const ctx=canvas.getContext('2d');
  let W,H,particles=[];
  function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight;}
  resize();window.addEventListener('resize',resize);
  class Particle{
    constructor(){this.reset();}
    reset(){
      this.x=Math.random()*W;this.y=Math.random()*H;
      this.size=Math.random()*1.5+.3;
      this.speedX=(Math.random()-.5)*.3;this.speedY=(Math.random()-.5)*.3;
      this.opacity=Math.random()*.5+.1;
      this.color=Math.random()>.5?'74,143,255':'123,95,255';
    }
    update(){
      this.x+=this.speedX;this.y+=this.speedY;
      if(this.x<0||this.x>W||this.y<0||this.y>H)this.reset();
    }
    draw(){
      ctx.beginPath();ctx.arc(this.x,this.y,this.size,0,Math.PI*2);
      ctx.fillStyle=`rgba(${this.color},${this.opacity})`;ctx.fill();
    }
  }
  for(let i=0;i<80;i++)particles.push(new Particle());
  function animate(){
    ctx.clearRect(0,0,W,H);
    particles.forEach(p=>{p.update();p.draw();});
    // Draw connections
    particles.forEach((p1,i)=>{
      particles.slice(i+1).forEach(p2=>{
        const dx=p1.x-p2.x,dy=p1.y-p2.y,dist=Math.sqrt(dx*dx+dy*dy);
        if(dist<120){
          ctx.beginPath();ctx.moveTo(p1.x,p1.y);ctx.lineTo(p2.x,p2.y);
          ctx.strokeStyle=`rgba(74,143,255,${.05*(1-dist/120)})`;ctx.lineWidth=.5;ctx.stroke();
        }
      });
    });
    requestAnimationFrame(animate);
  }
  animate();
})();

// ── CURSOR GLOW (desktop only) ──
if(window.innerWidth>768){
  const glow=document.getElementById('cursorGlow');
  document.addEventListener('mousemove',e=>{
    glow.style.left=e.clientX+'px';glow.style.top=e.clientY+'px';
  });
}

// ── SCROLL ──
window.addEventListener('scroll',()=>{
  const pct=(window.scrollY/(document.documentElement.scrollHeight-window.innerHeight))*100;
  document.getElementById('scrollProgress').style.width=pct+'%';
  document.getElementById('mainNav').classList.toggle('scrolled',window.scrollY>50);
});

// ── REVEAL (desktop only) ──
if(window.innerWidth>768){
  const obs=new IntersectionObserver(entries=>{
    entries.forEach(e=>{if(e.isIntersecting)e.target.classList.add('visible');});
  },{threshold:0.1});
  document.querySelectorAll('.reveal').forEach(el=>obs.observe(el));
}

// ── COUNTER ANIMATION ──
const cobs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      const el=e.target;if(el.dataset.counted)return;el.dataset.counted='1';
      const t=parseInt(el.dataset.target),d=2000,s=performance.now();
      function tick(now){
        const p=Math.min((now-s)/d,1),ease=1-Math.pow(1-p,4);
        el.textContent=Math.floor(ease*t);
        if(p<1)requestAnimationFrame(tick);else el.textContent=t;
      }
      requestAnimationFrame(tick);
    }
  });
},{threshold:0.3});
document.querySelectorAll('.counter-num').forEach(el=>cobs.observe(el));

// ── MOBILE MENU ──
function toggleMenu(){document.getElementById('hamburger').classList.toggle('open');document.getElementById('mobileMenu').classList.toggle('open');}
function closeMenu(){document.getElementById('hamburger').classList.remove('open');document.getElementById('mobileMenu').classList.remove('open');}

// ── PASSWORD ──
const PASS='seif2025';
function openPw(){document.getElementById('pwInput').value='';document.getElementById('pwError').style.display='none';document.getElementById('pwOverlay').classList.add('open');setTimeout(()=>document.getElementById('pwInput').focus(),200);}
function closePw(){document.getElementById('pwOverlay').classList.remove('open');}
function checkPw(){if(document.getElementById('pwInput').value===PASS){closePw();openUpload();}else{document.getElementById('pwError').style.display='block';document.getElementById('pwInput').value='';}}

// ── URL EMBED HELPER ──
function getEmbedURL(url){
  const yt=url.match(/(?:youtu\.be\/|youtube\.com\/(?:watch\?v=|shorts\/|embed\/))([a-zA-Z0-9_-]{11})/);
  if(yt)return{type:'yt',embed:`https://www.youtube.com/embed/${yt[1]}?autoplay=1&rel=0`};
  const vm=url.match(/vimeo\.com\/(\d+)/);
  if(vm)return{type:'vm',embed:`https://player.vimeo.com/video/${vm[1]}?autoplay=1`};
  return null;
}

// ── VIDEO GALLERIES ──
const galleries={ads:[],ground:[],event:[],shows:[]};
const pending={ads:[],ground:[],event:[],shows:[]};
const labels={ads:'Ads',ground:'Social Media',event:'Event Coverage',shows:'Shows'};
let curCat=null,curIdx=0;

function updateBadge(k){const c=galleries[k].length;document.getElementById('count-'+k).textContent=c===0?'0 Videos':c+(c===1?' Video':' Videos');}
function updateUC(k){const c=galleries[k].length+pending[k].length;document.getElementById('uc-'+k).textContent=c+' video'+(c!==1?'s':'');}

function addURL(k){
  const inp=document.getElementById('url-'+k);
  const url=inp.value.trim();if(!url)return;
  const embed=getEmbedURL(url);
  if(!embed){alert('Please paste a valid YouTube or Vimeo link.');return;}
  const name=embed.type==='yt'?'YouTube Video':'Vimeo Video';
  pending[k].push({name,url:null,embed:embed.embed,type:'iframe'});
  inp.value='';renderList(k);
}

function handleFiles(k,inp){
  Array.from(inp.files).forEach(f=>pending[k].push({name:f.name,url:URL.createObjectURL(f),embed:null,type:'video'}));
  renderList(k);inp.value='';
}

function renderList(k){
  updateUC(k);
  const el=document.getElementById('ul-'+k);
  const all=[...galleries[k],...pending[k]];
  el.innerHTML='';
  all.forEach((v,i)=>{
    const isPend=i>=galleries[k].length;
    const d=document.createElement('div');d.className='upload-file-item';
    const icon=v.type==='iframe'?'🔗':'🎬';
    d.innerHTML=`<span class="upload-file-name">${isPend?'🆕 ':''}${icon} ${v.name}</span><button class="upload-file-remove" onclick="removeVid('${k}',${i})">✕</button>`;
    el.appendChild(d);
  });
}

function removeVid(k,i){
  const gc=galleries[k].length;
  if(i<gc){if(galleries[k][i].url)URL.revokeObjectURL(galleries[k][i].url);galleries[k].splice(i,1);updateBadge(k);}
  else{const pi=i-gc;if(pending[k][pi].url)URL.revokeObjectURL(pending[k][pi].url);pending[k].splice(pi,1);}
  renderList(k);
}

function openUpload(){['ads','ground','event','shows'].forEach(k=>renderList(k));document.getElementById('uploadSuccess').style.display='none';document.getElementById('uploadOverlay').classList.add('open');}
function closeUpload(){document.getElementById('uploadOverlay').classList.remove('open');}
function applyVideos(){
  ['ads','ground','event','shows'].forEach(k=>{pending[k].forEach(v=>galleries[k].push(v));pending[k]=[];updateBadge(k);});
  document.getElementById('uploadSuccess').style.display='block';
  setTimeout(()=>{document.getElementById('uploadSuccess').style.display='none';closeUpload();},1500);
}

function openGallery(k){curCat=k;curIdx=0;document.getElementById('galleryTitle').textContent=labels[k];renderGallery(k);document.getElementById('galleryModal').classList.add('open');document.body.style.overflow='hidden';}
function renderGallery(k){
  const list=galleries[k];
  const sidebar=document.getElementById('gallerySidebar');
  document.getElementById('galleryCount').textContent=list.length+(list.length===1?' video':' videos');
  if(list.length===0){sidebar.innerHTML='<div class="gallery-no-videos">No videos yet.</div>';stopAll();document.getElementById('galleryEmpty').style.display='block';return;}
  document.getElementById('galleryEmpty').style.display='none';
  sidebar.innerHTML='';
  list.forEach((v,i)=>{
    const d=document.createElement('div');d.className='gallery-thumb'+(i===curIdx?' active':'');
    d.innerHTML=`<span class="gallery-thumb-num">${String(i+1).padStart(2,'0')}</span><span class="gallery-thumb-name">${v.name}</span><span class="gallery-thumb-type">${v.type==='iframe'?'🔗 Link':'🎬 File'}</span>`;
    d.onclick=()=>playVid(k,i);
    sidebar.appendChild(d);
  });
  playVid(k,curIdx,false);
}

function stopAll(){
  const vid=document.getElementById('galleryVideo');vid.pause();vid.src='';vid.style.display='none';
  const fr=document.getElementById('galleryFrame');fr.src='';fr.style.display='none';
}

function playVid(k,i,play=true){
  curIdx=i;
  const item=galleries[k][i];
  stopAll();
  if(item.type==='iframe'){
    const fr=document.getElementById('galleryFrame');
    fr.src=play?item.embed:item.embed.replace('autoplay=1','autoplay=0');
    fr.style.display='block';
  } else {
    const vid=document.getElementById('galleryVideo');
    vid.src=item.url;vid.style.display='block';
    if(play)vid.play();
    vid.onended=()=>{if(i+1<galleries[k].length)playVid(k,i+1);};
  }
  document.getElementById('galleryEmpty').style.display='none';
  document.querySelectorAll('.gallery-thumb').forEach((t,j)=>t.classList.toggle('active',j===i));
}

function closeGallery(){stopAll();document.getElementById('galleryModal').classList.remove('open');document.body.style.overflow='';}

// ── CONTACT ──
function sendMessage(){
  const n=document.getElementById('cf-name').value.trim(),e=document.getElementById('cf-email').value.trim(),p=document.getElementById('cf-project').value.trim(),m=document.getElementById('cf-message').value.trim(),s=document.getElementById('formStatus');
  if(!n||!e||!m){s.textContent='⚠ Please fill in name, email and message.';s.className='form-status error';s.style.display='block';return;}
  const subj=encodeURIComponent('Portfolio Inquiry from '+n+(p?' — '+p:''));
  const body=encodeURIComponent('Name: '+n+'\nEmail: '+e+'\nProject: '+(p||'Not specified')+'\n\nMessage:\n'+m);
  window.location.href='mailto:seifelden625@gmail.com?subject='+subj+'&body='+body;
  s.textContent='✓ Opening your email app...';s.className='form-status success';s.style.display='block';
  setTimeout(()=>{document.getElementById('cf-name').value='';document.getElementById('cf-email').value='';document.getElementById('cf-project').value='';document.getElementById('cf-message').value='';setTimeout(()=>s.style.display='none',4000);},800);
}

// ── CLOSE HANDLERS ──
document.getElementById('pwOverlay').addEventListener('click',e=>{if(e.target===e.currentTarget)closePw();});
document.getElementById('uploadOverlay').addEventListener('click',e=>{if(e.target===e.currentTarget)closeUpload();});
document.getElementById('galleryModal').addEventListener('click',e=>{if(e.target===e.currentTarget)closeGallery();});
document.addEventListener('keydown',e=>{if(e.key==='Escape'){closeGallery();closeUpload();closePw();}});
</script>
</body>
</html>
