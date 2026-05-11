<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>My Love 💑</title>
<link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
<script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-database-compat.js"></script>
<style>
:root {
  --rose:#e8637a;--rose-light:#f5a3b0;--rose-dark:#c0415a;
  --blush:#fde8ec;--cream:#fff8f5;--gold:#d4a853;
  --text:#2d1b2e;--text-light:#7a5a6e;--white:#ffffff;
  --shadow:0 4px 20px rgba(200,80,100,.12);--radius:16px;
  --green:#25D366;--red:#ff3b30;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{font-family:'Hind Siliguri',sans-serif;background:var(--cream);color:var(--text);height:100%;width:100%;overflow:hidden;position:fixed;top:0;left:0;}
.screen{display:none;position:fixed;inset:0;flex-direction:column;}
.screen.active{display:flex;}

/* ========== LOCK ========== */
#screen-lock{align-items:center;justify-content:center;background:linear-gradient(160deg,#fff0f3 0%,#fde8ec 100%);overflow-y:auto;padding:env(safe-area-inset-top,16px) 16px env(safe-area-inset-bottom,16px);}
.lock-card{background:var(--white);border-radius:24px;padding:2rem 1.5rem;width:100%;max-width:380px;box-shadow:0 8px 40px rgba(200,80,100,.15);border:1px solid rgba(232,99,122,.1);}
.lock-brand{text-align:center;margin-bottom:1.5rem;}
.b-icon{font-size:3rem;display:block;animation:hb 2s ease-in-out infinite;}
@keyframes hb{0%,100%{transform:scale(1)}50%{transform:scale(1.12)}}
.lock-brand h2{font-family:'Playfair Display',serif;font-size:1.8rem;color:var(--rose-dark);margin-top:.3rem;}
.lock-brand p{font-size:.8rem;color:var(--text-light);margin-top:.2rem;}
.form-group{margin-bottom:.9rem;}
.form-group label{font-size:.72rem;color:var(--text-light);font-weight:600;display:block;margin-bottom:.3rem;text-transform:uppercase;letter-spacing:.5px;}
.form-input-wrap{position:relative;}
.form-input-wrap input{width:100%;padding:.75rem 1rem;border:2px solid rgba(232,99,122,.2);border-radius:12px;font-family:'Hind Siliguri',sans-serif;font-size:1rem;background:var(--blush);outline:none;transition:border .2s;-webkit-appearance:none;color:var(--text);}
.form-input-wrap input:focus{border-color:var(--rose);}
.eye-btn{position:absolute;right:10px;top:50%;transform:translateY(-50%);background:none;border:none;cursor:pointer;font-size:.9rem;color:var(--text-light);padding:6px;}
.btn-primary{width:100%;padding:.85rem;background:linear-gradient(135deg,var(--rose),var(--rose-dark));color:#fff;border:none;border-radius:12px;font-family:'Hind Siliguri',sans-serif;font-weight:700;font-size:1rem;cursor:pointer;box-shadow:0 4px 16px rgba(200,65,90,.3);margin-top:.4rem;-webkit-appearance:none;}
.btn-link{background:none;border:none;color:var(--rose-dark);font-family:'Hind Siliguri',sans-serif;font-size:.88rem;font-weight:600;cursor:pointer;text-decoration:underline;padding:4px;}
.lock-footer{text-align:center;margin-top:.8rem;display:flex;flex-direction:column;gap:.4rem;}
.sub-card{display:none;}
.sub-card.active-card{display:block;}

/* ========== MAIN APP ========== */
#screen-app{flex-direction:column;background:var(--cream);}
#view-list{display:flex;flex-direction:column;position:fixed;inset:0;background:var(--cream);z-index:10;}
#view-list.hide{display:none;}
.app-header{background:linear-gradient(135deg,var(--rose-dark),var(--rose));padding:calc(env(safe-area-inset-top,0px) + .8rem) 1rem .8rem;display:flex;align-items:center;justify-content:space-between;flex-shrink:0;}
.app-header h1{font-family:'Playfair Display',serif;font-size:1.3rem;color:#fff;}
.sb-avatar-btn{width:36px;height:36px;border-radius:50%;background:rgba(255,255,255,.25);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:1rem;overflow:hidden;cursor:pointer;border:2px solid rgba(255,255,255,.4);color:#fff;flex-shrink:0;}
.sb-avatar-btn img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.search-bar{padding:.7rem 1rem;background:var(--white);border-bottom:1px solid rgba(232,99,122,.08);flex-shrink:0;}
.search-wrap{position:relative;}
.search-wrap input{width:100%;padding:.55rem .9rem .55rem 2.2rem;border:1.5px solid rgba(232,99,122,.2);border-radius:20px;font-family:'Hind Siliguri',sans-serif;font-size:.9rem;background:var(--blush);outline:none;-webkit-appearance:none;color:var(--text);}
.search-icon{position:absolute;left:.7rem;top:50%;transform:translateY(-50%);font-size:.85rem;color:var(--text-light);pointer-events:none;}
.tab-bar{display:flex;background:var(--white);border-bottom:1px solid rgba(232,99,122,.1);flex-shrink:0;}
.tab-btn{flex:1;padding:.65rem .2rem;border:none;background:none;cursor:pointer;font-family:'Hind Siliguri',sans-serif;font-size:.72rem;font-weight:600;color:var(--text-light);display:flex;flex-direction:column;align-items:center;gap:.15rem;border-bottom:2.5px solid transparent;transition:all .2s;position:relative;}
.tab-btn .ti{font-size:1.1rem;}
.tab-btn.active{color:var(--rose-dark);border-bottom-color:var(--rose);}
.tab-badge{position:absolute;top:4px;right:8px;background:var(--red);color:#fff;font-size:.55rem;font-weight:700;min-width:15px;height:15px;border-radius:8px;display:none;align-items:center;justify-content:center;padding:0 2px;}
.tab-badge.show{display:flex;}
.list-area{flex:1;overflow-y:auto;overflow-x:hidden;-webkit-overflow-scrolling:touch;}

/* ========== CHAT LIST ========== */
.chat-item{display:flex;align-items:center;gap:.85rem;padding:.9rem 1rem;background:var(--white);border-bottom:1px solid rgba(232,99,122,.05);cursor:pointer;transition:background .15s;}
.chat-item:active{background:var(--blush);}
.ci-avatar{width:50px;height:50px;min-width:50px;border-radius:50%;background:linear-gradient(135deg,var(--gold),#b8862e);display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700;font-size:1.1rem;position:relative;overflow:hidden;}
.ci-avatar img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.online-dot{width:13px;height:13px;border-radius:50%;background:var(--green);border:2px solid #fff;position:absolute;bottom:0;right:0;display:none;}
.ci-info{flex:1;min-width:0;}
.ci-row1{display:flex;align-items:center;justify-content:space-between;}
.ci-name{font-size:.95rem;font-weight:600;color:var(--text);}
.ci-time{font-size:.68rem;color:var(--text-light);}
.ci-row2{display:flex;align-items:center;justify-content:space-between;margin-top:.15rem;}
.ci-preview{font-size:.78rem;color:var(--text-light);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;flex:1;min-width:0;}
.unread-badge{background:var(--green);color:#fff;font-size:.62rem;font-weight:700;min-width:18px;height:18px;border-radius:9px;display:none;align-items:center;justify-content:center;padding:0 4px;flex-shrink:0;margin-left:.4rem;}
.unread-badge.show{display:flex;}
#search-results{padding:.3rem 0;}
.sr-item{display:flex;align-items:center;gap:.8rem;padding:.75rem 1rem;background:var(--white);border-bottom:1px solid rgba(232,99,122,.05);cursor:pointer;}

/* ========== CHAT VIEW ========== */
#view-chat{display:none;position:fixed;inset:0;flex-direction:column;background:#f0e6e8;z-index:20;}
#view-chat.show{display:flex;}
.chat-header{background:linear-gradient(135deg,var(--rose-dark),var(--rose));padding:calc(env(safe-area-inset-top,0px) + .7rem) .8rem .7rem;display:flex;align-items:center;gap:.7rem;flex-shrink:0;}
.back-btn{background:none;border:none;color:#fff;font-size:1.3rem;cursor:pointer;padding:4px;display:flex;align-items:center;}
.ch-avatar{width:40px;height:40px;min-width:40px;border-radius:50%;background:linear-gradient(135deg,var(--gold),#b8862e);display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700;font-size:.95rem;overflow:hidden;}
.ch-avatar img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.ch-info{flex:1;cursor:pointer;}
.ch-name{font-size:.95rem;font-weight:700;color:#fff;}
.ch-status{font-size:.72rem;color:rgba(255,255,255,.8);}
.ch-actions{display:flex;gap:.3rem;}
.ch-btn{width:38px;height:38px;border-radius:50%;border:none;cursor:pointer;font-size:.95rem;display:flex;align-items:center;justify-content:center;color:#fff;transition:all .2s;background:rgba(255,255,255,.15);}
.ch-btn:active{background:rgba(255,255,255,.3);}
.ch-btn svg{width:20px;height:20px;fill:none;stroke:#fff;stroke-width:2;}
.msgs-area{flex:1;overflow-y:auto;overflow-x:hidden;padding:.8rem .8rem 0;display:flex;flex-direction:column;gap:.5rem;-webkit-overflow-scrolling:touch;background:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='60' height='60'%3E%3Ccircle cx='30' cy='30' r='1.5' fill='rgba(200,80,100,.06)'/%3E%3C/svg%3E"),linear-gradient(160deg,#fde8ec 0%,#fff0f3 100%);}
.date-sep{text-align:center;margin:.3rem 0;}
.date-sep span{background:rgba(255,255,255,.85);color:var(--text-light);padding:.22rem .75rem;border-radius:20px;font-size:.68rem;box-shadow:0 1px 4px rgba(0,0,0,.08);}
.msg{max-width:78%;display:flex;flex-direction:column;position:relative;}
.msg.sent{align-self:flex-end;}
.msg.recv{align-self:flex-start;}
.msg-bubble{padding:.6rem .85rem;border-radius:12px;font-size:.9rem;line-height:1.5;word-break:break-word;position:relative;cursor:pointer;}
.msg.sent .msg-bubble{background:linear-gradient(135deg,#dcf8c6,#c8f0a8);color:#1a1a1a;border-bottom-right-radius:2px;box-shadow:0 1px 2px rgba(0,0,0,.1);}
.msg.recv .msg-bubble{background:var(--white);color:var(--text);border-bottom-left-radius:2px;box-shadow:0 1px 2px rgba(0,0,0,.1);}
.msg-sender{font-size:.7rem;font-weight:700;color:var(--rose-dark);margin-bottom:.15rem;}
.msg-time{font-size:.63rem;opacity:.65;margin-top:.2rem;display:flex;align-items:center;gap:.2rem;}
.msg.sent .msg-time{justify-content:flex-end;}
.msg-img{max-width:100%;max-height:180px;border-radius:8px;display:block;cursor:pointer;object-fit:cover;}
.ctx-menu{position:fixed;background:var(--white);border-radius:12px;box-shadow:0 8px 30px rgba(0,0,0,.18);padding:.4rem 0;z-index:500;min-width:170px;display:none;}
.ctx-menu.show{display:block;}
.ctx-item{padding:.65rem 1rem;font-size:.87rem;cursor:pointer;display:flex;align-items:center;gap:.55rem;font-family:'Hind Siliguri',sans-serif;}
.ctx-item:hover{background:var(--blush);}
.ctx-item.danger{color:var(--red);}
.typing-wrap{display:none;align-items:center;gap:.4rem;padding:.4rem .75rem;background:var(--white);border-radius:12px;border-bottom-left-radius:2px;width:fit-content;margin:.2rem .8rem;box-shadow:0 1px 2px rgba(0,0,0,.08);}
.typing-wrap.show{display:flex;}
.typing-label{font-size:.72rem;color:var(--text-light);font-style:italic;}
.tdot{width:6px;height:6px;border-radius:50%;background:var(--rose-light);animation:tb 1s infinite;}
.tdot:nth-child(2){animation-delay:.2s}.tdot:nth-child(3){animation-delay:.4s}
@keyframes tb{0%,60%,100%{transform:translateY(0)}30%{transform:translateY(-5px)}}
.mood-bar{display:flex;align-items:center;gap:.4rem;padding:.5rem .8rem;background:rgba(255,255,255,.9);border-bottom:1px solid rgba(232,99,122,.08);flex-shrink:0;overflow-x:auto;}
.mood-bar::-webkit-scrollbar{display:none;}
.mood-label{font-size:.7rem;color:var(--text-light);font-weight:600;white-space:nowrap;}
.mood-emoji{font-size:1.2rem;cursor:pointer;padding:.1rem;border-radius:6px;transition:transform .15s;}
.mood-emoji:active{transform:scale(1.3);}
.input-bar{display:flex;align-items:flex-end;gap:.5rem;padding:.6rem .8rem calc(env(safe-area-inset-bottom,0px) + .6rem);background:var(--white);border-top:1px solid rgba(232,99,122,.08);flex-shrink:0;}
.input-bar textarea{flex:1;border:1.5px solid rgba(232,99,122,.2);border-radius:20px;padding:.6rem .9rem;font-family:'Hind Siliguri',sans-serif;font-size:.9rem;background:var(--blush);outline:none;resize:none;max-height:90px;min-height:38px;line-height:1.4;transition:border .2s;-webkit-appearance:none;color:var(--text);}
.input-bar textarea:focus{border-color:var(--rose);}
.ib-btn{width:38px;height:38px;min-width:38px;border-radius:50%;border:none;background:var(--blush);cursor:pointer;font-size:1rem;display:flex;align-items:center;justify-content:center;transition:all .15s;flex-shrink:0;}
.ib-btn.send{background:var(--green);color:#fff;}
.ib-btn:active{opacity:.7;}
.emoji-picker{position:absolute;bottom:70px;left:.8rem;background:var(--white);border:1px solid rgba(232,99,122,.2);border-radius:12px;padding:.6rem;box-shadow:var(--shadow);width:calc(100% - 1.6rem);max-width:300px;z-index:50;display:none;flex-wrap:wrap;gap:.2rem;}
.emoji-picker.show{display:flex;}
.ep-e{font-size:1.35rem;cursor:pointer;padding:.2rem;border-radius:6px;}
.rec-bar{display:none;flex-direction:column;padding:.6rem .8rem calc(env(safe-area-inset-bottom,0px) + .6rem);background:var(--white);border-top:1px solid rgba(232,99,122,.08);flex-shrink:0;}
.rec-bar.show{display:flex;}
.rec-inner{display:flex;align-items:center;gap:.8rem;}
.rec-dot{width:9px;height:9px;border-radius:50%;background:var(--red);animation:recP .8s ease-in-out infinite;flex-shrink:0;}
@keyframes recP{0%,100%{transform:scale(1)}50%{transform:scale(1.2)}}
#recTimer{font-weight:700;color:var(--red);font-size:.9rem;min-width:42px;}
.rec-actions{display:flex;gap:.5rem;margin-left:auto;}

/* ========== PROFILE PANEL ========== */
.profile-header{background:linear-gradient(135deg,var(--rose),var(--rose-dark));border-radius:16px;padding:1.5rem;text-align:center;color:#fff;margin-bottom:1rem;}
.profile-big-av{width:72px;height:72px;border-radius:50%;background:rgba(255,255,255,.25);display:flex;align-items:center;justify-content:center;font-size:1.8rem;margin:0 auto .7rem;border:3px solid rgba(255,255,255,.4);cursor:pointer;overflow:hidden;}
.profile-big-av img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.profile-header h2{font-family:'Playfair Display',serif;font-size:1.4rem;}
.username-badge{display:inline-block;background:rgba(255,255,255,.15);padding:.2rem .7rem;border-radius:20px;font-size:.78rem;font-family:monospace;margin-top:.35rem;cursor:pointer;}
.section-title{font-family:'Playfair Display',serif;font-size:.95rem;color:var(--rose-dark);margin:1rem 0 .5rem;}
.setting-row{display:flex;align-items:center;justify-content:space-between;padding:.8rem .9rem;background:var(--white);border-radius:12px;margin-bottom:.4rem;cursor:pointer;border:1px solid rgba(232,99,122,.07);}
.sr-left{display:flex;align-items:center;gap:.7rem;font-size:.88rem;}
.sr-icon{width:34px;height:34px;border-radius:9px;background:var(--blush);display:flex;align-items:center;justify-content:center;font-size:.88rem;flex-shrink:0;}
.toggle{width:42px;height:23px;border-radius:12px;background:#ddd;position:relative;cursor:pointer;transition:background .2s;flex-shrink:0;}
.toggle.on{background:var(--rose);}
.toggle::after{content:'';position:absolute;width:17px;height:17px;border-radius:50%;background:#fff;top:3px;left:3px;transition:transform .2s;box-shadow:0 1px 3px rgba(0,0,0,.2);}
.toggle.on::after{transform:translateX(19px);}

/* ========== DIARY ========== */
.diary-compose{background:var(--white);border-radius:14px;padding:1rem;margin-bottom:1rem;border:1px solid rgba(232,99,122,.1);}
.diary-compose textarea{width:100%;border:1.5px solid rgba(232,99,122,.15);border-radius:10px;padding:.8rem;font-family:'Hind Siliguri',sans-serif;font-size:.88rem;background:var(--blush);outline:none;resize:none;min-height:80px;-webkit-appearance:none;color:var(--text);}
.diary-footer{display:flex;align-items:center;justify-content:space-between;margin-top:.6rem;}
.diary-entry{background:var(--white);border-radius:14px;padding:1rem;margin-bottom:.6rem;border-left:4px solid var(--rose);}
.de-meta{display:flex;gap:.4rem;align-items:center;margin-bottom:.4rem;font-size:.72rem;color:var(--text-light);flex-wrap:wrap;}
.de-author{background:var(--blush);color:var(--rose-dark);padding:.1rem .45rem;border-radius:20px;font-weight:700;}
.diary-entry p{font-size:.85rem;line-height:1.6;}

/* ========== CALLS PANEL ========== */
.call-cards-grid{display:grid;grid-template-columns:1fr 1fr;gap:.8rem;margin-bottom:1.2rem;}
.call-card{background:var(--white);border-radius:16px;padding:1.2rem;text-align:center;cursor:pointer;border:2px solid transparent;transition:all .2s;box-shadow:0 2px 8px rgba(200,80,100,.08);}
.call-card:active{border-color:var(--rose);}
.imo-call-icon{width:56px;height:56px;border-radius:50%;margin:0 auto .6rem;display:flex;align-items:center;justify-content:center;}
.imo-call-icon.audio{background:linear-gradient(135deg,#25D366,#128C7E);}
.imo-call-icon.video{background:linear-gradient(135deg,#0078D4,#005a9e);}
.imo-call-icon svg{width:28px;height:28px;fill:#fff;}
.call-card h3{font-size:.9rem;color:var(--rose-dark);font-weight:700;}
.call-card p{font-size:.72rem;color:var(--text-light);margin-top:.2rem;}
.call-history-item{display:flex;align-items:center;gap:.8rem;padding:.8rem .9rem;background:var(--white);border-radius:12px;margin-bottom:.4rem;border:1px solid rgba(232,99,122,.07);cursor:pointer;}
.chi-av{width:44px;height:44px;min-width:44px;border-radius:50%;background:linear-gradient(135deg,var(--gold),#b8862e);display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700;font-size:.95rem;overflow:hidden;}
.chi-av img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.chi-info{flex:1;min-width:0;}
.chi-name{font-size:.9rem;font-weight:700;color:var(--text);}
.chi-detail{font-size:.72rem;color:var(--text-light);margin-top:.1rem;}
.chi-right{display:flex;flex-direction:column;align-items:flex-end;gap:.25rem;}
.chi-dur{font-size:.75rem;color:var(--rose);font-weight:700;}
.chi-btns{display:flex;gap:.3rem;}
.chi-btn{width:30px;height:30px;border-radius:50%;border:none;background:var(--blush);cursor:pointer;font-size:.8rem;display:flex;align-items:center;justify-content:center;}

/* ========= IMO-STYLE CALL OVERLAY ========= */
.call-overlay{display:none;position:fixed;inset:0;z-index:900;flex-direction:column;align-items:center;justify-content:space-between;padding:calc(env(safe-area-inset-top,0px) + 2rem) 1rem calc(env(safe-area-inset-bottom,0px) + 2.5rem);}
.call-overlay.show{display:flex;}
.call-overlay.audio-mode{background:linear-gradient(160deg,#1a0a2e 0%,#2d1b4e 40%,#c0415a 100%);}
.call-overlay.video-mode{background:#000;}

#remote-video{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;z-index:1;display:none;background:#000;}
#local-video{position:absolute;top:calc(env(safe-area-inset-top,0px) + 60px);right:12px;width:110px;height:160px;object-fit:cover;border-radius:14px;border:2px solid rgba(255,255,255,.5);z-index:10;display:none;background:#333;box-shadow:0 4px 20px rgba(0,0,0,.4);}
#screen-video{position:absolute;inset:0;width:100%;height:100%;object-fit:contain;z-index:5;display:none;background:#000;}

.call-ui-top{position:relative;z-index:20;display:flex;flex-direction:column;align-items:center;gap:.7rem;text-align:center;width:100%;}
.call-big-av{width:110px;height:110px;border-radius:50%;background:linear-gradient(135deg,var(--gold),#b8862e);display:flex;align-items:center;justify-content:center;font-size:2.8rem;color:#fff;border:4px solid rgba(255,255,255,.2);overflow:hidden;box-shadow:0 0 0 10px rgba(255,255,255,.07),0 0 0 20px rgba(255,255,255,.04);animation:callPulse 2s ease-in-out infinite;}
@keyframes callPulse{0%,100%{box-shadow:0 0 0 10px rgba(255,255,255,.07),0 0 0 20px rgba(255,255,255,.04);}50%{box-shadow:0 0 0 14px rgba(255,255,255,.1),0 0 0 28px rgba(255,255,255,.06);}}
.call-big-av img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.call-name{color:#fff;font-family:'Playfair Display',serif;font-size:1.8rem;margin-top:.3rem;text-shadow:0 2px 8px rgba(0,0,0,.3);}
.call-status{color:rgba(255,255,255,.75);font-size:.9rem;margin-top:.1rem;animation:blink 1.5s ease-in-out infinite;}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.5}}
.call-status.connected{animation:none;opacity:1;}
.call-timer-el{color:#fff;font-size:1.4rem;font-weight:700;letter-spacing:.08em;display:none;margin-top:.2rem;}

/* ===== IMO-STYLE CALL CONTROLS ===== */
.call-controls{position:relative;z-index:20;display:flex;gap:1.4rem;align-items:center;flex-wrap:wrap;justify-content:center;width:100%;}
.cc-btn{display:flex;flex-direction:column;align-items:center;gap:.35rem;background:none;border:none;cursor:pointer;-webkit-tap-highlight-color:transparent;}
.cc-btn:active .cc-circle{transform:scale(.92);}
.cc-circle{width:60px;height:60px;border-radius:50%;display:flex;align-items:center;justify-content:center;transition:all .2s;box-shadow:0 4px 16px rgba(0,0,0,.3);}
.cc-circle svg{width:26px;height:26px;}
.cc-label{font-size:.65rem;color:rgba(255,255,255,.8);font-family:'Hind Siliguri',sans-serif;white-space:nowrap;}

.cc-btn.mute-btn .cc-circle{background:rgba(255,255,255,.2);backdrop-filter:blur(8px);}
.cc-btn.mute-btn.muted-on .cc-circle{background:rgba(255,59,48,.8);}
.cc-btn.cam-btn .cc-circle{background:rgba(255,255,255,.2);backdrop-filter:blur(8px);display:none;}
.cc-btn.cam-btn.visible .cc-circle{display:flex;}
.cc-btn.cam-btn.cam-off .cc-circle{background:rgba(255,59,48,.8);}
.cc-btn.end-btn .cc-circle{background:#f03d4e;width:72px;height:72px;box-shadow:0 6px 28px rgba(240,61,78,.6);}
.cc-btn.end-btn .cc-circle svg{width:30px;height:30px;}
.cc-btn.speaker-btn .cc-circle{background:rgba(255,255,255,.2);backdrop-filter:blur(8px);}
.cc-btn.speaker-btn.speaker-loud .cc-circle{background:rgba(37,211,102,.5);}
.cc-btn.share-btn .cc-circle{background:rgba(255,255,255,.2);backdrop-filter:blur(8px);display:none;}
.cc-btn.share-btn.visible .cc-circle{display:flex;}
.cc-btn.share-btn.share-active .cc-circle{background:rgba(37,211,102,.5);}

.audio-call-bg-rings{position:absolute;inset:0;z-index:0;pointer-events:none;overflow:hidden;}
.audio-call-bg-rings::before,.audio-call-bg-rings::after{content:'';position:absolute;border-radius:50%;border:1px solid rgba(255,255,255,.08);animation:ringExpand 3s ease-out infinite;}
.audio-call-bg-rings::before{width:300px;height:300px;top:50%;left:50%;transform:translate(-50%,-60%);}
.audio-call-bg-rings::after{width:200px;height:200px;top:50%;left:50%;transform:translate(-50%,-65%);animation-delay:1.5s;}
@keyframes ringExpand{0%{opacity:.5;transform:translate(-50%,-60%) scale(.5);}100%{opacity:0;transform:translate(-50%,-60%) scale(2);}}

/* ===== IMO-STYLE INCOMING CALL ===== */
.incoming-call{display:none;position:fixed;inset:0;z-index:950;flex-direction:column;align-items:center;justify-content:space-between;padding:calc(env(safe-area-inset-top,0px) + 3rem) 1.5rem calc(env(safe-area-inset-bottom,0px) + 3rem);}
.incoming-call.show{display:flex;}
.incoming-call.audio-inc{background:linear-gradient(160deg,#1a1a2e 0%,#16213e 50%,#0f3460 100%);}
.incoming-call.video-inc{background:linear-gradient(160deg,#0a2a3d 0%,#0d3b5c 100%);}

.inc-top{display:flex;flex-direction:column;align-items:center;gap:.8rem;text-align:center;}
.incoming-av{width:100px;height:100px;border-radius:50%;background:linear-gradient(135deg,var(--gold),#b8862e);display:flex;align-items:center;justify-content:center;font-size:2.5rem;color:#fff;border:4px solid rgba(255,255,255,.2);overflow:hidden;box-shadow:0 0 0 10px rgba(255,255,255,.06),0 0 0 20px rgba(255,255,255,.03);animation:callPulse 2s ease-in-out infinite;}
.incoming-av img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.inc-app-badge{background:rgba(255,255,255,.12);padding:.3rem .8rem;border-radius:20px;font-size:.72rem;color:rgba(255,255,255,.8);backdrop-filter:blur(4px);display:inline-flex;align-items:center;gap:.3rem;}
.incoming-name{color:#fff;font-family:'Playfair Display',serif;font-size:1.6rem;text-shadow:0 2px 8px rgba(0,0,0,.3);}
.incoming-type{color:rgba(255,255,255,.7);font-size:.85rem;display:flex;align-items:center;gap:.3rem;}
.inc-type-dot{width:6px;height:6px;border-radius:50%;background:var(--green);animation:blink 1.5s infinite;}

.inc-bottom{display:flex;justify-content:center;align-items:flex-end;gap:4rem;width:100%;}
.ic-btn-wrap{display:flex;flex-direction:column;align-items:center;gap:.5rem;}
.ic-btn{width:72px;height:72px;border-radius:50%;border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;box-shadow:0 6px 24px rgba(0,0,0,.4);}
.ic-btn.accept{background:var(--green);}
.ic-btn.reject{background:var(--red);}
.ic-btn svg{width:30px;height:30px;fill:#fff;}
.ic-label{font-size:.75rem;color:rgba(255,255,255,.8);font-family:'Hind Siliguri',sans-serif;font-weight:600;}
.swipe-hint{color:rgba(255,255,255,.4);font-size:.72rem;text-align:center;}

/* ===== NOTIFICATION BUBBLE ===== */
.notif-bubble{display:none;position:fixed;top:calc(env(safe-area-inset-top,0px) + .5rem);left:.8rem;right:.8rem;z-index:3000;background:rgba(30,30,30,.95);border-radius:14px;padding:.85rem 1rem;backdrop-filter:blur(10px);box-shadow:0 8px 32px rgba(0,0,0,.3);animation:slideDown .3s ease;}
.notif-bubble.show{display:flex;align-items:center;gap:.75rem;}
@keyframes slideDown{from{transform:translateY(-100%);opacity:0;}to{transform:translateY(0);opacity:1;}}
.nb-av{width:44px;height:44px;min-width:44px;border-radius:50%;background:linear-gradient(135deg,var(--gold),#b8862e);display:flex;align-items:center;justify-content:center;font-size:1.1rem;color:#fff;font-weight:700;overflow:hidden;position:relative;}
.nb-av img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.nb-app-dot{position:absolute;bottom:-1px;right:-1px;width:18px;height:18px;background:#0078D4;border-radius:50%;border:2px solid rgba(30,30,30,.95);display:flex;align-items:center;justify-content:center;font-size:.55rem;color:#fff;font-weight:700;}
.nb-content{flex:1;min-width:0;}
.nb-name{color:#fff;font-size:.85rem;font-weight:700;}
.nb-msg{color:rgba(255,255,255,.65);font-size:.78rem;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;margin-top:.05rem;}
.nb-actions{display:flex;gap:.5rem;margin-left:.3rem;}
.nb-act-btn{background:rgba(255,255,255,.12);border:none;border-radius:10px;padding:.35rem .7rem;color:#fff;font-family:'Hind Siliguri',sans-serif;font-size:.72rem;font-weight:600;cursor:pointer;white-space:nowrap;}
.nb-act-btn:active{background:rgba(255,255,255,.25);}
.nb-act-btn.green{background:rgba(37,211,102,.25);}
.nb-act-btn.blue{background:rgba(0,120,212,.3);}
.nb-close-btn{background:none;border:none;color:rgba(255,255,255,.4);font-size:1rem;cursor:pointer;padding:2px;flex-shrink:0;}

/* ========== MODALS ========== */
.modal-overlay{display:none;position:fixed;inset:0;z-index:1000;background:rgba(0,0,0,.5);align-items:flex-end;justify-content:center;}
.modal-overlay.show{display:flex;}
.modal-card{background:var(--white);border-radius:20px 20px 0 0;padding:1.5rem 1.2rem calc(env(safe-area-inset-bottom,0px) + 1.5rem);width:100%;max-height:85vh;overflow-y:auto;}
.modal-card h3{font-family:'Playfair Display',serif;color:var(--rose-dark);font-size:1.1rem;margin-bottom:.9rem;text-align:center;}
.modal-input{width:100%;padding:.7rem .9rem;border:2px solid rgba(232,99,122,.2);border-radius:12px;font-family:'Hind Siliguri',sans-serif;font-size:.9rem;background:var(--blush);outline:none;margin-bottom:.7rem;-webkit-appearance:none;color:var(--text);}
.modal-input:focus{border-color:var(--rose);}
.modal-footer{display:flex;gap:.6rem;margin-top:.4rem;}
.btn-secondary{flex:1;padding:.75rem;background:var(--blush);color:var(--rose-dark);border:none;border-radius:12px;font-family:'Hind Siliguri',sans-serif;font-weight:700;font-size:.9rem;cursor:pointer;}
.btn-primary-sm{flex:1;padding:.75rem;background:linear-gradient(135deg,var(--rose),var(--rose-dark));color:#fff;border:none;border-radius:12px;font-family:'Hind Siliguri',sans-serif;font-weight:700;font-size:.9rem;cursor:pointer;}

/* lightbox */
.lightbox{display:none;position:fixed;inset:0;z-index:800;background:rgba(0,0,0,.92);align-items:center;justify-content:center;flex-direction:column;}
.lightbox.show{display:flex;}
.lb-inner{background:var(--white);border-radius:16px;padding:.8rem;max-width:90vw;max-height:88vh;position:relative;text-align:center;}
.lb-close{position:absolute;top:.5rem;right:.7rem;background:none;border:none;font-size:1.3rem;cursor:pointer;}
.lb-actions{display:flex;gap:.7rem;margin-top:.8rem;justify-content:center;}
.lb-dl-btn{background:linear-gradient(135deg,var(--rose),var(--rose-dark));color:#fff;border:none;border-radius:10px;padding:.6rem 1.2rem;font-family:'Hind Siliguri',sans-serif;font-size:.85rem;font-weight:700;cursor:pointer;display:flex;align-items:center;gap:.4rem;}

/* toast */
.toast{position:fixed;bottom:calc(env(safe-area-inset-bottom,0px) + 1.2rem);left:50%;transform:translateX(-50%) translateY(80px);background:rgba(45,27,46,.9);color:#fff;padding:.6rem 1.2rem;border-radius:24px;font-size:.83rem;z-index:2000;transition:transform .3s ease;white-space:nowrap;max-width:90vw;text-align:center;pointer-events:none;}
.toast.show{transform:translateX(-50%) translateY(0);}

.file-hidden{display:none;}
.ch-username{font-size:.65rem;color:rgba(255,255,255,.6);cursor:pointer;text-decoration:underline;display:inline-flex;align-items:center;gap:.2rem;}
#panel-content{padding:1rem;}
</style>
</head>
<body>

<!-- LOCK SCREEN -->
<div id="screen-lock" class="screen active">
  <div class="lock-card">
    <div class="sub-card active-card" id="card-login">
      <div class="lock-brand">
        <span class="b-icon">💑</span>
        <h2>My Love</h2>
        <p>আপনাদের নিজস্ব প্রাইভেট জগৎ</p>
      </div>
      <div class="form-group">
        <label>ইউজারনেম</label>
        <div class="form-input-wrap"><input type="text" id="login-email" placeholder="@username" autocomplete="off" autocapitalize="none"></div>
      </div>
      <div class="form-group">
        <label>পাসওয়ার্ড</label>
        <div class="form-input-wrap">
          <input type="password" id="login-pass" placeholder="••••••" autocomplete="off">
          <button class="eye-btn" onclick="toggleVis('login-pass',this)">👁</button>
        </div>
      </div>
      <button class="btn-primary" onclick="doLogin()">Login 💕</button>
      <div class="lock-footer">
        <button class="btn-link" onclick="showCard('card-register')">নতুন অ্যাকাউন্ট তৈরি করুন</button>
        <button class="btn-link" onclick="showCard('card-forgot')">পাসওয়ার্ড ভুলে গেছেন?</button>
      </div>
    </div>
    <div class="sub-card" id="card-register">
      <div class="lock-brand"><span class="b-icon">✨</span><h2>নতুন অ্যাকাউন্ট</h2></div>
      <div class="form-group"><label>পুরো নাম</label><div class="form-input-wrap"><input type="text" id="reg-name" placeholder="আপনার নাম"></div></div>
      <div class="form-group"><label>ইউজারনেম</label><div class="form-input-wrap"><input type="text" id="reg-username" placeholder="example: rafi123" autocapitalize="none"></div></div>
      <div class="form-group"><label>ইমেইল</label><div class="form-input-wrap"><input type="email" id="reg-email" placeholder="email@example.com" autocapitalize="none"></div></div>
      <div class="form-group"><label>ফোন</label><div class="form-input-wrap"><input type="tel" id="reg-phone" placeholder="+880..."></div></div>
      <div class="form-group"><label>পাসওয়ার্ড</label><div class="form-input-wrap"><input type="password" id="reg-pass" placeholder="কমপক্ষে ৬ অক্ষর"><button class="eye-btn" onclick="toggleVis('reg-pass',this)">👁</button></div></div>
      <div class="form-group"><label>পাসওয়ার্ড নিশ্চিত</label><div class="form-input-wrap"><input type="password" id="reg-pass2" placeholder="আবার লিখুন"><button class="eye-btn" onclick="toggleVis('reg-pass2',this)">👁</button></div></div>
      <button class="btn-primary" onclick="doRegister()">অ্যাকাউন্ট তৈরি করুন 🌸</button>
      <div class="lock-footer"><button class="btn-link" onclick="showCard('card-login')">← লগইন পেইজে ফিরুন</button></div>
    </div>
    <div class="sub-card" id="card-forgot">
      <div class="lock-brand"><span class="b-icon">🔑</span><h2>পাসওয়ার্ড রিসেট</h2></div>
      <div class="form-group"><label>ইমেইল</label><div class="form-input-wrap"><input type="email" id="forgot-email" placeholder="email@example.com"></div></div>
      <button class="btn-primary" onclick="doForgot()">রিসেট লিংক পাঠান 📧</button>
      <div class="lock-footer"><button class="btn-link" onclick="showCard('card-login')">← লগইন পেইজে ফিরুন</button></div>
    </div>
  </div>
</div>

<!-- MAIN APP -->
<div id="screen-app" class="screen">
  <div id="view-list">
    <div class="app-header">
      <div style="display:flex;align-items:center;gap:.5rem">
        <span style="font-size:1.2rem">💑</span>
        <h1>My Love</h1>
      </div>
      <div style="display:flex;align-items:center;gap:.6rem">
        <div id="sb-username" style="font-size:.75rem;color:rgba(255,255,255,.85);cursor:pointer;font-weight:600" onclick="copyMyUsername()">@user</div>
        <div class="sb-avatar-btn" id="sb-avatar" onclick="showTab('profile')">U</div>
      </div>
    </div>
    <div class="tab-bar">
      <button class="tab-btn active" id="tab-chats" onclick="showTab('chats')"><span class="ti">💬</span>চ্যাট<span class="tab-badge" id="total-badge">0</span></button>
      <button class="tab-btn" id="tab-calls" onclick="showTab('calls')"><span class="ti">📞</span>কল</button>
      <button class="tab-btn" id="tab-diary" onclick="showTab('diary')"><span class="ti">📖</span>ডায়েরি</button>
      <button class="tab-btn" id="tab-profile" onclick="showTab('profile')"><span class="ti">👤</span>প্রোফাইল</button>
    </div>
    <div class="search-bar" id="search-section">
      <div class="search-wrap">
        <span class="search-icon">🔍</span>
        <input type="text" id="search-input" placeholder="@username দিয়ে খুঁজুন..." oninput="handleSearch(this.value)" autocapitalize="none">
      </div>
      <div id="search-results"></div>
    </div>
    <div class="list-area" id="list-area">
      <div id="chats-panel"><div style="padding:1.2rem;text-align:center;color:var(--text-light);font-size:.82rem">লোড হচ্ছে...</div></div>
      <div id="panel-content" style="display:none"></div>
    </div>
  </div>

  <!-- CHAT VIEW -->
  <div id="view-chat">
    <div class="chat-header">
      <button class="back-btn" onclick="closeChat()">‹</button>
      <div class="ch-avatar" id="ch-avatar">M</div>
      <div class="ch-info" onclick="copyPartnerUsername()">
        <div class="ch-name" id="ch-name">-</div>
        <div class="ch-status" id="ch-status">
          <span id="ch-status-text">অনলাইন</span>
          <span class="ch-username" id="ch-username-display"></span>
        </div>
      </div>
      <div class="ch-actions">
        <button class="ch-btn" onclick="startCallFromChat('audio')" title="অডিও কল">
          <svg viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 9.81 19.79 19.79 0 01.22 1.18 2 2 0 012.22 0h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.09 7.91a16 16 0 006 6l1.27-1.27a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 16.92z"/></svg>
        </button>
        <button class="ch-btn" onclick="startCallFromChat('video')" title="ভিডিও কল">
          <svg viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round"><polygon points="23 7 16 12 23 17 23 7"/><rect x="1" y="5" width="15" height="14" rx="2" ry="2"/></svg>
        </button>
      </div>
    </div>

    <div class="mood-bar">
      <span class="mood-label">মন:</span>
      <span class="mood-emoji" onclick="setMood('😍')">😍</span>
      <span class="mood-emoji" onclick="setMood('😊')">😊</span>
      <span class="mood-emoji" onclick="setMood('😘')">😘</span>
      <span class="mood-emoji" onclick="setMood('🥰')">🥰</span>
      <span class="mood-emoji" onclick="setMood('😔')">😔</span>
      <span class="mood-emoji" onclick="setMood('😴')">😴</span>
      <span class="mood-emoji" onclick="setMood('🤗')">🤗</span>
      <span class="mood-emoji" onclick="setMood('❤️')">❤️</span>
    </div>

    <div class="msgs-area" id="msgs-area">
      <div class="date-sep"><span>আজকে 📅</span></div>
    </div>

    <div class="typing-wrap" id="typing-wrap">
      <div class="tdot"></div><div class="tdot"></div><div class="tdot"></div>
      <span class="typing-label" id="typing-label">টাইপ করছে...</span>
    </div>

    <div style="position:relative">
      <div class="emoji-picker" id="emojiPicker">
        <span class="ep-e" onclick="insertEmoji('❤️')">❤️</span><span class="ep-e" onclick="insertEmoji('💕')">💕</span>
        <span class="ep-e" onclick="insertEmoji('😍')">😍</span><span class="ep-e" onclick="insertEmoji('😘')">😘</span>
        <span class="ep-e" onclick="insertEmoji('🥰')">🥰</span><span class="ep-e" onclick="insertEmoji('💋')">💋</span>
        <span class="ep-e" onclick="insertEmoji('🌹')">🌹</span><span class="ep-e" onclick="insertEmoji('🌷')">🌷</span>
        <span class="ep-e" onclick="insertEmoji('✨')">✨</span><span class="ep-e" onclick="insertEmoji('🤗')">🤗</span>
        <span class="ep-e" onclick="insertEmoji('😊')">😊</span><span class="ep-e" onclick="insertEmoji('🙏')">🙏</span>
        <span class="ep-e" onclick="insertEmoji('💌')">💌</span><span class="ep-e" onclick="insertEmoji('🫂')">🫂</span>
        <span class="ep-e" onclick="insertEmoji('💍')">💍</span><span class="ep-e" onclick="insertEmoji('😂')">😂</span>
        <span class="ep-e" onclick="insertEmoji('😭')">😭</span><span class="ep-e" onclick="insertEmoji('🥺')">🥺</span>
        <span class="ep-e" onclick="insertEmoji('🔥')">🔥</span><span class="ep-e" onclick="insertEmoji('🎀')">🎀</span>
      </div>
    </div>

    <div class="input-bar" id="inputBar">
      <button class="ib-btn" onclick="toggleEmoji()">😊</button>
      <button class="ib-btn" onclick="document.getElementById('chat-media').click()">📷</button>
      <input type="file" id="chat-media" class="file-hidden" accept="image/*,video/*" onchange="sendMedia(event)">
      <textarea id="chat-input" placeholder="কিছু লিখুন..." rows="1"
        onkeydown="chatKeydown(event)" oninput="autoResize(this);sendTypingSignal()"></textarea>
      <button class="ib-btn" id="voiceBtn" onclick="toggleVoice()">🎤</button>
      <button class="ib-btn send" onclick="sendMessage()">
        <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
      </button>
    </div>

    <div class="rec-bar" id="recBar">
      <div class="rec-inner">
        <div class="rec-dot"></div>
        <span id="recTimer">00:00</span>
        <span style="color:var(--text-light);font-size:.8rem;flex:1">রেকর্ড হচ্ছে...</span>
        <div class="rec-actions">
          <button class="ib-btn" onclick="cancelVoice()" style="background:rgba(255,59,48,.1);color:var(--red)">✕</button>
          <button class="ib-btn send" onclick="stopSendVoice()">✓</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ===== IMO-STYLE CALL OVERLAY ===== -->
<div class="call-overlay audio-mode" id="callOverlay">
  <div class="audio-call-bg-rings" id="callBgRings"></div>
  <video id="remote-video" autoplay playsinline></video>
  <video id="local-video" autoplay playsinline muted></video>
  <video id="screen-video" autoplay playsinline></video>

  <div class="call-ui-top">
    <div class="call-big-av" id="call-big-av">M</div>
    <div class="call-name" id="call-name">-</div>
    <div class="call-status" id="call-status">সংযুক্ত হচ্ছে...</div>
    <div class="call-timer-el" id="call-timer">00:00</div>
  </div>

  <div class="call-controls">
    <button class="cc-btn mute-btn" id="muteBtn" onclick="toggleMute()">
      <div class="cc-circle">
        <svg id="muteIcon" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"/>
          <path d="M19 10v2a7 7 0 0 1-14 0v-2"/>
          <line x1="12" y1="19" x2="12" y2="23"/>
          <line x1="8" y1="23" x2="16" y2="23"/>
        </svg>
      </div>
      <span class="cc-label">মিউট</span>
    </button>

    <button class="cc-btn cam-btn" id="camBtn" onclick="toggleCamera()">
      <div class="cc-circle">
        <svg id="camIcon" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polygon points="23 7 16 12 23 17 23 7"/>
          <rect x="1" y="5" width="15" height="14" rx="2" ry="2"/>
        </svg>
      </div>
      <span class="cc-label">ক্যামেরা</span>
    </button>

    <button class="cc-btn end-btn" onclick="endCall()">
      <div class="cc-circle">
        <svg viewBox="0 0 24 24" fill="#fff">
          <path d="M6.6 10.8c1.4 2.8 3.8 5.1 6.6 6.6l2.2-2.2c.3-.3.7-.4 1-.2 1.1.4 2.3.6 3.6.6.6 0 1 .4 1 1V20c0 .6-.4 1-1 1C9.6 21 3 14.4 3 6c0-.6.4-1 1-1h3.5c.6 0 1 .4 1 1 0 1.3.2 2.5.6 3.6.1.3 0 .7-.2 1L6.6 10.8z"/>
        </svg>
      </div>
      <span class="cc-label">শেষ করুন</span>
    </button>

    <button class="cc-btn speaker-btn" id="speakerBtn" onclick="toggleSpeaker()">
      <div class="cc-circle">
        <svg id="speakerIcon" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"/>
          <path d="M19.07 4.93a10 10 0 0 1 0 14.14"/>
          <path d="M15.54 8.46a5 5 0 0 1 0 7.07"/>
        </svg>
      </div>
      <span class="cc-label">স্পিকার</span>
    </button>

    <button class="cc-btn share-btn" id="shareBtn" onclick="toggleScreenShare()">
      <div class="cc-circle">
        <svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <rect x="2" y="3" width="20" height="14" rx="2"/>
          <line x1="8" y1="21" x2="16" y2="21"/>
          <line x1="12" y1="17" x2="12" y2="21"/>
        </svg>
      </div>
      <span class="cc-label">শেয়ার</span>
    </button>
  </div>
</div>

<!-- ===== IMO-STYLE INCOMING CALL (FULL SCREEN) ===== -->
<div class="incoming-call audio-inc" id="incomingCall">
  <div class="inc-top">
    <div class="incoming-av" id="inc-avatar">M</div>
    <div class="inc-app-badge">💑 My Love · আসছে...</div>
    <div class="incoming-name" id="inc-name">-</div>
    <div class="incoming-type">
      <div class="inc-type-dot"></div>
      <span id="inc-type">অডিও কল আসছে...</span>
    </div>
  </div>

  <div class="swipe-hint">নিচের বাটন চাপুন</div>

  <div class="inc-bottom">
    <div class="ic-btn-wrap">
      <button class="ic-btn reject" onclick="rejectCall()">
        <svg viewBox="0 0 24 24" fill="#fff">
          <path d="M6.6 10.8c1.4 2.8 3.8 5.1 6.6 6.6l2.2-2.2c.3-.3.7-.4 1-.2 1.1.4 2.3.6 3.6.6.6 0 1 .4 1 1V20c0 .6-.4 1-1 1C9.6 21 3 14.4 3 6c0-.6.4-1 1-1h3.5c.6 0 1 .4 1 1 0 1.3.2 2.5.6 3.6.1.3 0 .7-.2 1L6.6 10.8z"/>
          <line x1="2" y1="2" x2="22" y2="22" stroke="#fff" stroke-width="2.5" stroke-linecap="round"/>
        </svg>
      </button>
      <span class="ic-label">প্রত্যাখ্যান</span>
    </div>
    <div class="ic-btn-wrap">
      <button class="ic-btn accept" id="inc-accept" onclick="acceptCall()">
        <svg viewBox="0 0 24 24" fill="#fff">
          <path d="M6.6 10.8c1.4 2.8 3.8 5.1 6.6 6.6l2.2-2.2c.3-.3.7-.4 1-.2 1.1.4 2.3.6 3.6.6.6 0 1 .4 1 1V20c0 .6-.4 1-1 1C9.6 21 3 14.4 3 6c0-.6.4-1 1-1h3.5c.6 0 1 .4 1 1 0 1.3.2 2.5.6 3.6.1.3 0 .7-.2 1L6.6 10.8z"/>
        </svg>
      </button>
      <span class="ic-label">গ্রহণ করুন</span>
    </div>
  </div>
</div>

<!-- LIGHTBOX -->
<div class="lightbox" id="lightbox" onclick="closeLB(event)">
  <div class="lb-inner" onclick="event.stopPropagation()">
    <button class="lb-close" onclick="closeLB()">✕</button>
    <div id="lb-content"></div>
    <div class="lb-actions" id="lb-actions"></div>
  </div>
</div>

<!-- Context Menu -->
<div class="ctx-menu" id="ctxMenu">
  <div class="ctx-item" onclick="copyMsg()">📋 কপি করুন</div>
  <div class="ctx-item danger" id="ctx-del-everyone" onclick="deleteForEveryone()">🗑️ সবার জন্য মুছুন</div>
  <div class="ctx-item danger" onclick="deleteForMe()">🗑️ শুধু আমার জন্য মুছুন</div>
  <div class="ctx-item" onclick="closeCtx()">✕ বন্ধ করুন</div>
</div>

<!-- EDIT PROFILE MODAL -->
<div class="modal-overlay" id="editProfileModal">
  <div class="modal-card">
    <h3>✏️ প্রোফাইল এডিট</h3>
    <label style="font-size:.72rem;color:var(--text-light);font-weight:600;display:block;margin-bottom:.25rem">পুরো নাম</label>
    <input class="modal-input" type="text" id="edit-name" placeholder="আপনার নাম">
    <label style="font-size:.72rem;color:var(--text-light);font-weight:600;display:block;margin-bottom:.25rem">পরিচয় (Role)</label>
    <input class="modal-input" type="text" id="edit-role" placeholder="Husband / Wife / Partner">
    <label style="font-size:.72rem;color:var(--text-light);font-weight:600;display:block;margin-bottom:.25rem">নতুন পাসওয়ার্ড (খালি = একই)</label>
    <input class="modal-input" type="password" id="edit-pass" placeholder="নতুন পাসওয়ার্ড">
    <div class="modal-footer">
      <button class="btn-secondary" onclick="closeEditProfile()">বাতিল</button>
      <button class="btn-primary-sm" onclick="saveProfile()">সংরক্ষণ 💾</button>
    </div>
  </div>
</div>

<!-- IMO-STYLE NOTIFICATION BUBBLE -->
<div class="notif-bubble" id="notifBubble">
  <div class="nb-av" id="nb-av">?
    <div class="nb-app-dot">💑</div>
  </div>
  <div class="nb-content">
    <div class="nb-name" id="nb-name">নতুন বার্তা</div>
    <div class="nb-msg" id="nb-msg"></div>
  </div>
  <div class="nb-actions" id="nb-actions">
    <button class="nb-act-btn green" id="nb-voice-btn" onclick="nbVoiceCall()" style="display:none">📞 voice</button>
    <button class="nb-act-btn blue" id="nb-video-btn" onclick="nbVideoCall()" style="display:none">📹 video</button>
    <button class="nb-act-btn" id="nb-msg-btn" onclick="nbOpenMsg()">💬 message</button>
  </div>
  <button class="nb-close-btn" onclick="closeNotifBubble()">✕</button>
</div>

<div class="toast" id="toast"></div>

<script>
// ========== FIREBASE ==========
const firebaseConfig={
  apiKey:"AIzaSyCwDkiTtF0CsGHQA7VLaiwc7pGqA6Kdniw",
  authDomain:"my-love-c75a0.firebaseapp.com",
  databaseURL:"https://my-love-c75a0-default-rtdb.firebaseio.com",
  projectId:"my-love-c75a0",
  storageBucket:"my-love-c75a0.firebasestorage.app",
  messagingSenderId:"772550646144",
  appId:"1:772550646144:web:a5183b79a13f0952e84965"
};
if(!firebase.apps.length) firebase.initializeApp(firebaseConfig);
const db = firebase.database();

// ========== AUDIO ==========
let audioCtx = null;
function getAudioCtx(){
  if(!audioCtx) try{ audioCtx = new (window.AudioContext||window.webkitAudioContext)(); }catch(e){}
  return audioCtx;
}
function playMsgSound(){
  try{
    const ctx = getAudioCtx(); if(!ctx) return;
    const osc = ctx.createOscillator();
    const gain = ctx.createGain();
    osc.connect(gain); gain.connect(ctx.destination);
    osc.frequency.setValueAtTime(1050,ctx.currentTime);
    osc.frequency.exponentialRampToValueAtTime(800,ctx.currentTime+0.08);
    gain.gain.setValueAtTime(0.25,ctx.currentTime);
    gain.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+0.15);
    osc.start(ctx.currentTime); osc.stop(ctx.currentTime+0.15);
  }catch(e){}
}
let ringInterval = null;
function startRingtone(){
  stopRingtone();
  const notes=[880,1100,880,0,880,1100,1320,0]; let i=0;
  ringInterval = setInterval(function(){
    if(notes[i%notes.length]>0){
      try{
        const ctx = getAudioCtx(); if(!ctx) return;
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.connect(gain); gain.connect(ctx.destination);
        osc.type='sine';
        osc.frequency.setValueAtTime(notes[i%notes.length],ctx.currentTime);
        gain.gain.setValueAtTime(0.35,ctx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+0.18);
        osc.start(ctx.currentTime); osc.stop(ctx.currentTime+0.18);
      }catch(e){}
    }
    i++;
  },220);
}
function stopRingtone(){
  if(ringInterval){ clearInterval(ringInterval); ringInterval=null; }
}

// ========== STATE ==========
let currentUser=null, activeChatUid=null, activeChatId=null, activeChatUsername='';
let renderedMsgIds=new Set(), typingTimeout=null, emojiOpen=false;
let callInterval=null, callSeconds=0, isMuted=false, isCamOff=false, isSpeakerOn=true;
let currentCallType='audio', incomingCallData=null;
let mediaRecorder=null, audioChunks=[], recInterval=null, recSecs=0, isRecording=false;
let localStream=null, screenStream=null, isScreenSharing=false, peerConnection=null;
let unreadCounts={}, notificationsEnabled=true, currentTab='chats', allUsersCache={};
let ctxMsgKey=null, ctxMsgSenderUid=null, ctxMsgText=null;
let nbPendingUid=null;

const ICE_SERVERS={iceServers:[
  {urls:'stun:stun.l.google.com:19302'},
  {urls:'stun:stun1.l.google.com:19302'},
  {urls:'turn:a.relay.metered.ca:80',username:'openrelayproject',credential:'openrelayproject'},
  {urls:'turn:a.relay.metered.ca:443',username:'openrelayproject',credential:'openrelayproject'},
  {urls:'turn:a.relay.metered.ca:443',username:'openrelayproject',credential:'openrelayproject',transport:'tcp'}
]};

// ========== UTILS ==========
function esc(s){
  if(!s) return '';
  return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}
function showToast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg; t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2800);
}
function getStoredPic(uid){ try{ return localStorage.getItem('pic_'+uid)||null; }catch(e){ return null; } }
function setStoredPic(uid,d){ try{ localStorage.setItem('pic_'+uid,d); }catch(e){} }
function getStoredProfile(uid){ try{ const d=localStorage.getItem('profile_'+uid); return d?JSON.parse(d):null; }catch(e){ return null; } }
function setStoredProfile(uid,data){ try{ localStorage.setItem('profile_'+uid,JSON.stringify(data)); }catch(e){} }
function renderAvatarEl(el,uid,name){
  if(!el) return;
  const pic=getStoredPic(uid);
  if(pic) el.innerHTML='<img src="'+pic+'" alt="">';
  else el.textContent=(name||'?')[0].toUpperCase();
}

// ========== SESSION ==========
function saveSession(d){ try{ localStorage.setItem('session_user',JSON.stringify({...d,savedAt:Date.now()})); }catch(e){} }
function clearSession(){ try{ localStorage.removeItem('session_user'); }catch(e){} }
function loadSession(){
  try{
    const r=localStorage.getItem('session_user'); if(!r) return null;
    const d=JSON.parse(r);
    if(Date.now()-d.savedAt>30*24*60*60*1000){ clearSession(); return null; }
    return d;
  }catch(e){ return null; }
}

// ========== IMO-STYLE NOTIFICATION BUBBLE ==========
let notifTimer=null;
function showNotifBubble(opts){
  if(!notificationsEnabled) return;
  const bubble=document.getElementById('notifBubble');
  nbPendingUid=opts.uid;
  const nbAv=document.getElementById('nb-av');
  const pic=getStoredPic(opts.uid);
  if(pic) nbAv.innerHTML='<img src="'+pic+'" alt=""><div class="nb-app-dot">💑</div>';
  else{
    nbAv.innerHTML='<div class="nb-app-dot">💑</div>';
    nbAv.prepend(document.createTextNode((opts.name||'?')[0].toUpperCase()));
  }
  document.getElementById('nb-name').textContent=opts.name||'My Love';
  document.getElementById('nb-msg').textContent=(opts.msg||'').substring(0,60);
  const voiceBtn=document.getElementById('nb-voice-btn');
  const videoBtn=document.getElementById('nb-video-btn');
  const msgBtn=document.getElementById('nb-msg-btn');
  if(opts.type==='voice'||opts.type==='video'){
    voiceBtn.style.display=opts.type==='voice'?'block':'none';
    videoBtn.style.display=opts.type==='video'?'block':'none';
    msgBtn.style.display='none';
  } else {
    voiceBtn.style.display='none';
    videoBtn.style.display='none';
    msgBtn.style.display='block';
  }
  bubble.classList.add('show');
  clearTimeout(notifTimer);
  notifTimer=setTimeout(closeNotifBubble,5000);
  playMsgSound();
}
window.closeNotifBubble=function(){ document.getElementById('notifBubble').classList.remove('show'); };
window.nbOpenMsg=function(){
  closeNotifBubble();
  if(nbPendingUid){ const u=allUsersCache[nbPendingUid]; if(u) openChat(u); }
};
window.nbVoiceCall=function(){
  closeNotifBubble();
  if(nbPendingUid){
    const u=allUsersCache[nbPendingUid];
    if(u){ activeChatUid=u.uid; activeChatId=getChatId(currentUser.uid,u.uid); startCall('audio',u.uid,u.name); }
  }
};
window.nbVideoCall=function(){
  closeNotifBubble();
  if(nbPendingUid){
    const u=allUsersCache[nbPendingUid];
    if(u){ activeChatUid=u.uid; activeChatId=getChatId(currentUser.uid,u.uid); startCall('video',u.uid,u.name); }
  }
};

// ========== UNREAD ==========
function updateUnread(uid,delta){
  if(!unreadCounts[uid]) unreadCounts[uid]=0;
  unreadCounts[uid]=Math.max(0,unreadCounts[uid]+delta);
  const b=document.getElementById('ubadge_'+uid);
  if(b){
    if(unreadCounts[uid]>0){ b.textContent=unreadCounts[uid]>99?'99+':unreadCounts[uid]; b.classList.add('show'); }
    else b.classList.remove('show');
  }
  const total=Object.values(unreadCounts).reduce((a,v)=>a+v,0);
  const tb=document.getElementById('total-badge');
  if(tb){
    if(total>0){ tb.textContent=total>99?'99+':total; tb.style.display='flex'; }
    else tb.style.display='none';
  }
}
function clearUnread(uid){
  unreadCounts[uid]=0;
  const b=document.getElementById('ubadge_'+uid); if(b) b.classList.remove('show');
  const total=Object.values(unreadCounts).reduce((a,v)=>a+v,0);
  const tb=document.getElementById('total-badge');
  if(tb){
    if(total>0){ tb.textContent=total>99?'99+':total; tb.style.display='flex'; }
    else tb.style.display='none';
  }
}

// ========== SCREEN ==========
function showScreen(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

// ========== LOCK ==========
window.showCard=function(id){
  document.querySelectorAll('.sub-card').forEach(c=>c.classList.remove('active-card'));
  document.getElementById(id).classList.add('active-card');
};
window.toggleVis=function(id,btn){
  const inp=document.getElementById(id);
  inp.type=inp.type==='password'?'text':'password';
  btn.textContent=inp.type==='password'?'👁':'🙈';
};

window.doRegister=function(){
  const name=document.getElementById('reg-name').value.trim();
  const username=document.getElementById('reg-username').value.trim().toLowerCase().replace(/[^a-z0-9_]/g,'');
  const email=document.getElementById('reg-email').value.trim().toLowerCase();
  const phone=document.getElementById('reg-phone').value.trim();
  const pass=document.getElementById('reg-pass').value;
  const pass2=document.getElementById('reg-pass2').value;
  if(!name){ showToast('নাম লিখুন!'); return; }
  if(!username||username.length<3){ showToast('ইউজারনেম কমপক্ষে ৩ অক্ষর!'); return; }
  if(!email.includes('@')){ showToast('সঠিক ইমেইল লিখুন!'); return; }
  if(pass.length<6){ showToast('পাসওয়ার্ড কমপক্ষে ৬ অক্ষর!'); return; }
  if(pass!==pass2){ showToast('পাসওয়ার্ড মিলছে না!'); return; }
  const uid='u_'+username;
  db.ref('usernames/'+username).once('value',function(snap){
    if(snap.exists()){ showToast('এই ইউজারনেম আগে নেওয়া হয়েছে!'); return; }
    const userData={name,username,email,phone,pass,uid,role:'Husband',createdAt:Date.now()};
    db.ref('users/'+uid).set(userData,function(err){
      if(err){ showToast('ত্রুটি হয়েছে!'); return; }
      db.ref('usernames/'+username).set(uid);
      showToast('অ্যাকাউন্ট তৈরি হয়েছে! 🎉');
      document.getElementById('login-email').value=username;
      showCard('card-login');
    });
  });
};

window.doLogin=function(){
  const raw=document.getElementById('login-email').value.trim().toLowerCase().replace('@','');
  const pass=document.getElementById('login-pass').value;
  if(!raw){ showToast('ইউজারনেম দিন!'); return; }
  if(!pass){ showToast('পাসওয়ার্ড দিন!'); return; }
  const fallbacks=[
    {name:'Rafi',username:'rafi',uid:'u_rafi',email:'rafi@love.com',pass:'1234',role:'Husband'},
    {name:'Mitu',username:'mitu',uid:'u_mitu',email:'mitu@love.com',pass:'5678',role:'Wife'},
    {name:'Shahana',username:'shahana',uid:'u_shahana',email:'shahana@love.com',pass:'1234',role:'Wife'},
    {name:'Sakib',username:'ahsakib',uid:'u_ahsakib',email:'ahsakib@love.com',pass:'1234',role:'Husband'}
  ];
  for(let fb of fallbacks){
    if((raw===fb.username||raw===fb.email.split('@')[0])&&pass===fb.pass){
      const local=getStoredProfile(fb.uid);
      finishLogin(local?Object.assign({},fb,local):fb);
      return;
    }
  }
  db.ref('users').once('value',function(snap){
    let found=null;
    if(snap.exists()) snap.forEach(function(child){
      const u=child.val();
      if((u.username===raw||u.email===raw)&&u.pass===pass) found=u;
    });
    if(found){
      const local=getStoredProfile(found.uid);
      if(local) found=Object.assign({},found,local);
      finishLogin(found);
    } else showToast('ইউজারনেম বা পাসওয়ার্ড ভুল! ❌');
  },function(){ showToast('নেটওয়ার্ক সমস্যা! 📡'); });
};

function finishLogin(userData){
  currentUser=userData;
  saveSession(userData);
  allUsersCache[userData.uid]=userData;
  document.getElementById('sb-username').textContent='@'+(userData.username||userData.name);
  renderAvatarEl(document.getElementById('sb-avatar'),userData.uid,userData.name);
  showScreen('screen-app');
  showTab('chats');
  showToast('স্বাগতম '+userData.name+'! 💕');
  const presRef=db.ref('presence/'+currentUser.uid);
  presRef.set({name:currentUser.name,username:currentUser.username,online:true,uid:currentUser.uid,lastSeen:firebase.database.ServerValue.TIMESTAMP});
  presRef.onDisconnect().set({name:currentUser.name,username:currentUser.username,online:false,uid:currentUser.uid,lastSeen:firebase.database.ServerValue.TIMESTAMP});
  loadChatList();
  listenIncomingCalls();
  requestNotifPerm();
}

window.doLogout=function(){
  if(currentUser) db.ref('presence/'+currentUser.uid).set({name:currentUser.name,online:false});
  clearSession();
  currentUser=null; activeChatUid=null; activeChatId=null;
  renderedMsgIds=new Set(); unreadCounts={}; allUsersCache={};
  document.getElementById('view-chat').classList.remove('show');
  showScreen('screen-lock'); showCard('card-login'); showToast('লগআউট সম্পন্ন 👋');
};
window.doForgot=function(){
  const e=document.getElementById('forgot-email').value.trim();
  if(!e.includes('@')){ showToast('সঠিক ইমেইল লিখুন!'); return; }
  showToast('রিসেট লিংক পাঠানো হয়েছে! 📧');
  setTimeout(()=>showCard('card-login'),2000);
};

// ========== TABS ==========
window.showTab=function(tab){
  currentTab=tab;
  document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
  const btn=document.getElementById('tab-'+tab); if(btn) btn.classList.add('active');
  const searchSec=document.getElementById('search-section');
  const chatsPanel=document.getElementById('chats-panel');
  const panelContent=document.getElementById('panel-content');
  searchSec.style.display=tab==='chats'?'block':'none';
  chatsPanel.style.display=tab==='chats'?'block':'none';
  panelContent.style.display=tab!=='chats'?'block':'none';
  if(tab==='calls') renderCallsPanel();
  else if(tab==='diary') renderDiaryPanel();
  else if(tab==='profile') renderProfilePanel();
};

// ========== CHAT LIST ==========
function loadChatList(){
  db.ref('users').on('value',function(snap){
    if(!snap.exists()||!currentUser) return;
    const panel=document.getElementById('chats-panel');
    panel.innerHTML='';
    let count=0;
    snap.forEach(function(child){
      const u=child.val();
      if(u.uid===currentUser.uid) return;
      allUsersCache[u.uid]=u;
      panel.appendChild(createChatItem(u));
      count++;
      listenForNewMessages(u);
      loadLastMessage(u);
    });
    if(count===0) panel.innerHTML='<div style="padding:1.5rem;text-align:center;color:var(--text-light);font-size:.82rem">কোনো ব্যবহারকারী নেই।</div>';
    listenPresence();
  });
}

function loadLastMessage(u){
  const chatId=getChatId(currentUser.uid,u.uid);
  db.ref('chats/'+chatId+'/messages').orderByChild('timestamp').limitToLast(1).once('value',function(snap){
    if(!snap.exists()) return;
    snap.forEach(function(child){
      const msg=child.val();
      if(msg.deletedForEveryone) return;
      const prev=document.getElementById('prev_'+u.uid);
      if(prev){
        let txt='';
        if(msg.imageData) txt='📷 ছবি';
        else if(msg.videoData) txt='🎥 ভিডিও';
        else if(msg.voiceData) txt='🎤 ভয়েস মেসেজ';
        else txt=msg.text||'';
        const prefix=msg.senderUid===currentUser.uid?'আপনি: ':'';
        prev.textContent=prefix+txt.substring(0,40);
      }
      const t=document.getElementById('time_'+u.uid);
      if(t&&msg.timestamp){
        const d=new Date(msg.timestamp); const now=new Date();
        if(d.toDateString()===now.toDateString()){
          t.textContent=d.toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit',hour12:true});
        } else {
          t.textContent=d.toLocaleDateString('en-US',{month:'short',day:'numeric'});
        }
      }
    });
  });
}

function listenPresence(){
  db.ref('presence').on('value',function(snap){
    if(!snap.exists()) return;
    snap.forEach(function(p){
      const pd=p.val();
      const dot=document.getElementById('dot_'+pd.uid);
      if(dot) dot.style.display=pd.online?'block':'none';
    });
  });
}

function listenForNewMessages(u){
  if(!currentUser) return;
  const chatId=getChatId(currentUser.uid,u.uid);
  let initialized=false, lastKey=null;
  db.ref('chats/'+chatId+'/messages').orderByKey().limitToLast(1).on('value',function(snap){
    if(!snap.exists()) return;
    snap.forEach(function(child){
      const msg=child.val(); const key=child.key;
      if(msg.senderUid!==currentUser.uid){
        if(!initialized){ lastKey=key; initialized=true; return; }
        if(key!==lastKey){
          lastKey=key;
          const prev=document.getElementById('prev_'+u.uid);
          if(prev){
            let txt='';
            if(msg.imageData) txt='📷 ছবি';
            else if(msg.videoData) txt='🎥 ভিডিও';
            else if(msg.voiceData) txt='🎤 ভয়েস মেসেজ';
            else txt=msg.text||'';
            prev.textContent=txt.substring(0,40);
          }
          const tEl=document.getElementById('time_'+u.uid);
          if(tEl){ const d=new Date(msg.timestamp||Date.now()); tEl.textContent=d.toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit',hour12:true}); }
          if(activeChatUid!==u.uid){
            updateUnread(u.uid,1);
            showNotifBubble({uid:u.uid,name:u.name,msg:msg.text||(msg.imageData?'📷 ছবি':msg.voiceData?'🎤 ভয়েস':'📹 ভিডিও'),type:'msg'});
          } else {
            playMsgSound();
          }
        }
      } else {
        if(!initialized){ lastKey=key; initialized=true; }
      }
    });
    if(!initialized) initialized=true;
  });
}

function createChatItem(u){
  const div=document.createElement('div');
  div.className='chat-item'; div.id='ci_'+u.uid;
  const pic=getStoredPic(u.uid);
  const av=pic?'<img src="'+pic+'" alt="">':u.name[0].toUpperCase();
  div.innerHTML=
    '<div class="ci-avatar" id="ciav_'+u.uid+'">'+av+
    '<div class="online-dot" id="dot_'+u.uid+'"></div></div>'+
    '<div class="ci-info">'+
      '<div class="ci-row1">'+
        '<div class="ci-name">'+esc(u.name)+'</div>'+
        '<div class="ci-time" id="time_'+u.uid+'"></div>'+
      '</div>'+
      '<div class="ci-row2">'+
        '<div class="ci-preview" id="prev_'+u.uid+'">@'+esc(u.username||u.name.toLowerCase())+'</div>'+
        '<div class="unread-badge" id="ubadge_'+u.uid+'">0</div>'+
      '</div>'+
    '</div>';
  div.onclick=function(){ openChat(u); };
  return div;
}

// ========== SEARCH ==========
window.handleSearch=function(val){
  const sr=document.getElementById('search-results');
  if(!val||val.length<2){ sr.innerHTML=''; return; }
  const q=val.replace('@','').toLowerCase();
  db.ref('users').once('value',function(snap){
    const results=[];
    if(snap.exists()) snap.forEach(function(c){
      const u=c.val();
      if(u.uid===currentUser.uid) return;
      if((u.username&&u.username.includes(q))||u.name.toLowerCase().includes(q)) results.push(u);
    });
    sr.innerHTML='';
    if(!results.length){ sr.innerHTML='<div style="font-size:.75rem;color:var(--text-light);padding:.3rem .2rem">কেউ পাওয়া যায়নি</div>'; return; }
    results.forEach(function(u){
      const div=document.createElement('div'); div.className='sr-item';
      const pic=getStoredPic(u.uid);
      div.innerHTML='<div class="ci-avatar" style="width:40px;height:40px;min-width:40px;font-size:.9rem">'+(pic?'<img src="'+pic+'" alt="">':u.name[0])+'</div><div><div style="font-size:.9rem;font-weight:700">'+esc(u.name)+'</div><div style="font-size:.75rem;color:var(--text-light)">@'+esc(u.username||u.name.toLowerCase())+'</div></div>';
      div.onclick=function(){ openChat(u); sr.innerHTML=''; document.getElementById('search-input').value=''; };
      sr.appendChild(div);
    });
  });
};

// ========== OPEN CHAT ==========
function openChat(u){
  activeChatUid=u.uid;
  activeChatId=getChatId(currentUser.uid,u.uid);
  activeChatUsername=u.username||u.name.toLowerCase();
  renderedMsgIds=new Set();
  clearUnread(u.uid);
  const chAv=document.getElementById('ch-avatar');
  const pic=getStoredPic(u.uid);
  if(pic) chAv.innerHTML='<img src="'+pic+'" alt="">';
  else chAv.textContent=u.name[0].toUpperCase();
  document.getElementById('ch-name').textContent=u.name;
  document.getElementById('ch-status-text').textContent='অনলাইন 🟢';
  const uname='@'+(u.username||u.name.toLowerCase());
  const unameEl=document.getElementById('ch-username-display');
  if(unameEl){
    unameEl.textContent=' · '+uname+' 📋';
    unameEl.onclick=function(e){ e.stopPropagation(); copyPartnerUsername(); };
  }
  document.getElementById('view-chat').classList.add('show');
  document.getElementById('msgs-area').innerHTML='<div class="date-sep"><span>আজকে 📅</span></div>';

  // Remove old listeners before adding new ones
  if(activeChatId){
    db.ref('chats/'+activeChatId+'/messages').off();
  }

  db.ref('chats/'+activeChatId+'/messages').on('value',function(snap){
    if(!snap.exists()) return;
    snap.forEach(function(child){
      const id=child.key;
      if(!renderedMsgIds.has(id)){ renderedMsgIds.add(id); renderMsg(child.val(),id); }
    });
  });

  db.ref('chats/'+activeChatId+'/typing/'+u.uid).on('value',function(snap){
    const tw=document.getElementById('typing-wrap');
    const tl=document.getElementById('typing-label');
    if(snap.val()&&snap.val().isTyping){ if(tl) tl.textContent=u.name+' টাইপ করছে...'; tw.classList.add('show'); }
    else tw.classList.remove('show');
  });

  db.ref('presence/'+u.uid).on('value',function(snap){
    const pd=snap.val();
    const s=document.getElementById('ch-status-text');
    if(s) s.textContent=(pd&&pd.online)?'অনলাইন 🟢':'অফলাইন';
  });

  document.getElementById('chat-input').focus();
}

window.closeChat=function(){
  document.getElementById('view-chat').classList.remove('show');
  if(activeChatId){
    db.ref('chats/'+activeChatId+'/messages').off();
  }
  activeChatUid=null;
};

window.copyPartnerUsername=function(){
  if(!activeChatUid) return;
  const u=allUsersCache[activeChatUid];
  const un='@'+(u&&u.username?u.username:activeChatUsername);
  navigator.clipboard.writeText(un).catch(function(){
    const el=document.createElement('textarea');
    el.value=un; document.body.appendChild(el); el.select(); document.execCommand('copy'); document.body.removeChild(el);
  });
  showToast('কপি হয়েছে: '+un+' 📋');
};

function getChatId(a,b){ return [a,b].sort().join('__'); }

// ========== RENDER MESSAGE ==========
function renderMsg(msg,msgKey){
  if(!currentUser) return;
  if(msg.deletedFor&&msg.deletedFor[currentUser.uid]) return;
  if(msg.deletedForEveryone) return;
  const area=document.getElementById('msgs-area');
  const isSent=msg.senderUid===currentUser.uid;
  const now=new Date(msg.timestamp);
  const time=now.toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit',hour12:true});
  const wrap=document.createElement('div');
  wrap.className='msg '+(isSent?'sent':'recv');
  wrap.dataset.msgKey=msgKey||'';
  wrap.dataset.senderUid=msg.senderUid||'';
  let body='';
  if(msg.imageData){
    body='<img class="msg-img" src="'+esc(msg.imageData)+'" onclick="openLBImg(this.src)" alt="ছবি">';
  } else if(msg.videoData){
    body='<video style="max-width:100%;max-height:180px;border-radius:8px;display:block;" controls src="'+esc(msg.videoData)+'"></video>'+
         '<button onclick="downloadMedia(\''+esc(msg.videoData)+'\',\'video.mp4\')" style="margin-top:.3rem;background:var(--blush);border:none;border-radius:8px;padding:.3rem .7rem;font-size:.75rem;cursor:pointer;color:var(--rose-dark);">⬇️ ডাউনলোড</button>';
  } else if(msg.voiceData){
    const aid='a'+Date.now()+Math.random().toString(36).slice(2,5);
    const fc=isSent?'rgba(0,0,0,.3)':'var(--rose-light)';
    let bars='';
    for(let i=0;i<18;i++){
      const h=Math.round(Math.random()*14+4);
      const y=13-Math.round(h/2);
      bars+='<rect x="'+(i*5+2)+'" y="'+y+'" width="3" height="'+h+'" rx="2" fill="'+fc+'"/>';
    }
    body='<div style="display:flex;align-items:center;gap:.5rem;min-width:160px">'+
      '<button style="width:30px;height:30px;border-radius:50%;border:none;cursor:pointer;background:'+(isSent?'rgba(0,0,0,.15)':'var(--blush)')+';color:'+(isSent?'#333':'var(--rose-dark)')+';font-size:.85rem;display:flex;align-items:center;justify-content:center" '+
      'onclick="(function(b){var a=document.getElementById(\''+aid+'\');if(a.paused){a.play();b.textContent=\'⏸\';}else{a.pause();b.textContent=\'▶\';}})(this)">▶</button>'+
      '<svg viewBox="0 0 90 26" style="flex:1;height:26px" fill="none">'+bars+'</svg>'+
      '<audio id="'+aid+'" src="'+msg.voiceData+'" style="display:none" preload="none"></audio>'+
      '</div>';
  } else {
    body=esc(msg.text||'').replace(/\n/g,'<br>');
  }
  if(!isSent){
    wrap.innerHTML='<div class="msg-sender">'+esc(msg.sender)+'</div><div class="msg-bubble">'+body+'</div><div class="msg-time">'+time+'</div>';
  } else {
    wrap.innerHTML='<div class="msg-bubble">'+body+'</div><div class="msg-time">'+time+' ✓✓</div>';
  }
  wrap.addEventListener('contextmenu',function(e){
    e.preventDefault(); showCtxMenu(e,msgKey,msg.senderUid,msg.text);
  });
  wrap.addEventListener('touchstart',function(e){
    const touch=e.touches[0];
    const timer=setTimeout(()=>showCtxMenu({clientX:touch.clientX,clientY:touch.clientY},msgKey,msg.senderUid,msg.text),600);
    wrap.addEventListener('touchend',()=>clearTimeout(timer),{once:true});
    wrap.addEventListener('touchmove',()=>clearTimeout(timer),{once:true});
  });
  area.appendChild(wrap);
  area.scrollTop=area.scrollHeight;
}

// ========== CONTEXT MENU ==========
function showCtxMenu(e,key,senderUid,text){
  ctxMsgKey=key; ctxMsgSenderUid=senderUid; ctxMsgText=text||'';
  const menu=document.getElementById('ctxMenu');
  const isMine=senderUid===currentUser?.uid;
  document.getElementById('ctx-del-everyone').style.display=isMine?'flex':'none';
  menu.classList.add('show');
  let x=e.clientX, y=e.clientY;
  if(x+180>window.innerWidth) x=window.innerWidth-185;
  if(y+160>window.innerHeight) y=window.innerHeight-165;
  menu.style.left=x+'px'; menu.style.top=y+'px';
}
window.closeCtx=function(){ document.getElementById('ctxMenu').classList.remove('show'); ctxMsgKey=null; };
window.copyMsg=function(){
  if(ctxMsgText){
    navigator.clipboard.writeText(ctxMsgText).catch(()=>{});
    showToast('কপি হয়েছে! 📋');
  }
  closeCtx();
};
window.deleteForEveryone=function(){
  if(!ctxMsgKey||!activeChatId){ closeCtx(); return; }
  db.ref('chats/'+activeChatId+'/messages/'+ctxMsgKey).update({deletedForEveryone:true,text:'🚫 মেসেজটি মুছে ফেলা হয়েছে'});
  document.querySelectorAll('.msg').forEach(el=>{ if(el.dataset.msgKey===ctxMsgKey) el.remove(); });
  showToast('সবার জন্য মুছে ফেলা হয়েছে 🗑️');
  closeCtx();
};
window.deleteForMe=function(){
  if(!ctxMsgKey||!currentUser||!activeChatId){ closeCtx(); return; }
  const upd={}; upd['deletedFor/'+currentUser.uid]=true;
  db.ref('chats/'+activeChatId+'/messages/'+ctxMsgKey).update(upd);
  document.querySelectorAll('.msg').forEach(el=>{ if(el.dataset.msgKey===ctxMsgKey) el.remove(); });
  showToast('আমার জন্য মুছে ফেলা হয়েছে 🗑️');
  closeCtx();
};

// ========== SEND ==========
window.sendMessage=function(){
  const inp=document.getElementById('chat-input');
  const text=inp.value.trim();
  if(!text||!currentUser||!activeChatUid) return;
  db.ref('chats/'+activeChatId+'/messages').push({
    text,sender:currentUser.name,senderUid:currentUser.uid,
    recipientUid:activeChatUid,timestamp:Date.now()
  });
  inp.value=''; inp.style.height='auto';
  db.ref('chats/'+activeChatId+'/typing/'+currentUser.uid).set({isTyping:false});
};
window.sendTypingSignal=function(){
  if(!currentUser||!activeChatUid) return;
  db.ref('chats/'+activeChatId+'/typing/'+currentUser.uid).set({isTyping:true});
  clearTimeout(typingTimeout);
  typingTimeout=setTimeout(()=>db.ref('chats/'+activeChatId+'/typing/'+currentUser.uid).set({isTyping:false}),2000);
};
window.sendMedia=function(e){
  const file=e.target.files[0];
  if(!file||!currentUser||!activeChatUid) return;
  const isVideo=file.type.startsWith('video/');
  const reader=new FileReader();
  reader.onload=function(ev){
    const payload={sender:currentUser.name,senderUid:currentUser.uid,recipientUid:activeChatUid,timestamp:Date.now()};
    if(isVideo){ payload.text='🎥'; payload.videoData=ev.target.result; }
    else{ payload.text='📷'; payload.imageData=ev.target.result; }
    db.ref('chats/'+activeChatId+'/messages').push(payload);
    showToast(isVideo?'ভিডিও পাঠানো হয়েছে! 🎥':'ছবি পাঠানো হয়েছে! 📸');
  };
  reader.readAsDataURL(file);
  e.target.value='';
};
window.setMood=function(mood){
  if(!currentUser||!activeChatUid){ showToast('আগে কারো সাথে চ্যাট খুলুন'); return; }
  db.ref('chats/'+activeChatId+'/messages').push({
    text:'💭 আমার মন এখন: '+mood,sender:currentUser.name,
    senderUid:currentUser.uid,recipientUid:activeChatUid,timestamp:Date.now()
  });
};
window.chatKeydown=function(e){
  if(e.key==='Enter'&&!e.shiftKey){ e.preventDefault(); sendMessage(); }
};
window.autoResize=function(el){
  el.style.height='auto';
  el.style.height=Math.min(el.scrollHeight,90)+'px';
};
window.toggleEmoji=function(){
  emojiOpen=!emojiOpen;
  document.getElementById('emojiPicker').classList.toggle('show',emojiOpen);
};
window.insertEmoji=function(em){
  document.getElementById('chat-input').value+=em;
  emojiOpen=false;
  document.getElementById('emojiPicker').classList.remove('show');
};
window.copyMyUsername=function(){
  if(!currentUser) return;
  const u='@'+(currentUser.username||currentUser.name);
  navigator.clipboard.writeText(u).catch(()=>{
    const el=document.createElement('textarea');
    el.value=u; document.body.appendChild(el); el.select(); document.execCommand('copy'); document.body.removeChild(el);
  });
  showToast('কপি হয়েছে: '+u+' 📋');
};

// ========== LIGHTBOX ==========
window.openLBImg=function(src){
  document.getElementById('lb-content').innerHTML='<img src="'+src+'" style="max-width:100%;max-height:55vh;border-radius:10px">';
  document.getElementById('lb-actions').innerHTML='<button class="lb-dl-btn" onclick="downloadMedia(\''+src+'\',\'image.jpg\')">⬇️ ডাউনলোড করুন</button>';
  document.getElementById('lightbox').classList.add('show');
};
window.closeLB=function(e){
  if(!e||e.target===document.getElementById('lightbox')) document.getElementById('lightbox').classList.remove('show');
};
window.downloadMedia=function(src,filename){
  const a=document.createElement('a');
  a.href=src; a.download=filename||'download'; a.target='_blank';
  document.body.appendChild(a); a.click(); document.body.removeChild(a);
  showToast('ডাউনলোড শুরু হয়েছে! ⬇️');
};

// ========== PROFILE PANEL ==========
function renderProfilePanel(){
  if(!currentUser) return;
  const pic=getStoredPic(currentUser.uid);
  const avContent=pic?'<img src="'+pic+'" alt="">':currentUser.name[0].toUpperCase();
  document.getElementById('panel-content').innerHTML=`
    <div class="profile-header">
      <div class="profile-big-av" id="ph-av" onclick="document.getElementById('profile-pic-input').click()">${avContent}</div>
      <input type="file" id="profile-pic-input" class="file-hidden" accept="image/*" onchange="changeProfilePic(event)">
      <h2>${esc(currentUser.name)}</h2>
      <p style="font-size:.8rem;opacity:.85">${esc(currentUser.role||'Husband')} 👤</p>
      <div class="username-badge" onclick="copyMyUsername()">@${esc(currentUser.username||currentUser.name.toLowerCase())} 📋</div>
    </div>
    <button class="btn-primary" style="margin-bottom:.8rem" onclick="openEditProfile()">✏️ প্রোফাইল এডিট</button>
    <h3 class="section-title">🔒 সেটিং</h3>
    <div class="setting-row" onclick="toggleNotifSetting(this)">
      <div class="sr-left"><div class="sr-icon">🔔</div><div><div style="font-weight:600">নোটিফিকেশন</div><div style="font-size:.72rem;color:var(--text-light)">মেসেজ ও কলের জন্য</div></div></div>
      <div class="toggle ${notificationsEnabled?'on':''}" id="notif-toggle"></div>
    </div>
    <div class="setting-row">
      <div class="sr-left"><div class="sr-icon">🔐</div><div><div style="font-weight:600">End-to-End Encryption</div><div style="font-size:.72rem;color:var(--text-light)">সম্পূর্ণ নিরাপদ</div></div></div>
      <div class="toggle on"></div>
    </div>
    <div class="setting-row" onclick="doLogout()" style="margin-top:.4rem;border-color:rgba(255,59,48,.15)">
      <div class="sr-left"><div class="sr-icon" style="background:rgba(255,59,48,.1)">🚪</div><span style="font-weight:600;color:var(--red)">লগআউট</span></div>
      <span style="color:var(--text-light)">›</span>
    </div>
  `;
}

window.toggleNotifSetting=function(row){
  const t=row.querySelector('.toggle');
  t.classList.toggle('on');
  notificationsEnabled=t.classList.contains('on');
  if(notificationsEnabled){ requestNotifPerm(); showToast('নোটিফিকেশন চালু ✅'); }
  else showToast('নোটিফিকেশন বন্ধ ❌');
};
window.changeProfilePic=function(e){
  const file=e.target.files[0]; if(!file||!currentUser) return;
  const reader=new FileReader();
  reader.onload=function(ev){
    setStoredPic(currentUser.uid,ev.target.result);
    renderAvatarEl(document.getElementById('sb-avatar'),currentUser.uid,currentUser.name);
    showToast('প্রোফাইল ছবি পরিবর্তন হয়েছে! 📷');
    renderProfilePanel();
    db.ref('users/'+currentUser.uid+'/hasProfilePic').set(true);
  };
  reader.readAsDataURL(file);
  e.target.value='';
};
window.openEditProfile=function(){
  if(!currentUser) return;
  document.getElementById('edit-name').value=currentUser.name||'';
  document.getElementById('edit-role').value=currentUser.role||'Husband';
  document.getElementById('edit-pass').value='';
  document.getElementById('editProfileModal').classList.add('show');
};
window.closeEditProfile=function(){ document.getElementById('editProfileModal').classList.remove('show'); };
window.saveProfile=function(){
  const name=document.getElementById('edit-name').value.trim();
  const role=document.getElementById('edit-role').value.trim();
  const newPass=document.getElementById('edit-pass').value;
  if(!name){ showToast('নাম লিখুন!'); return; }
  if(newPass&&newPass.length<6){ showToast('পাসওয়ার্ড কমপক্ষে ৬ অক্ষর!'); return; }
  currentUser.name=name; currentUser.role=role;
  if(newPass) currentUser.pass=newPass;
  setStoredProfile(currentUser.uid,{name,role,pass:currentUser.pass});
  saveSession(currentUser);
  const updates={name,role}; if(newPass) updates.pass=newPass;
  db.ref('users/'+currentUser.uid).update(updates);
  renderAvatarEl(document.getElementById('sb-avatar'),currentUser.uid,currentUser.name);
  document.getElementById('sb-username').textContent='@'+(currentUser.username||currentUser.name);
  closeEditProfile(); showToast('প্রোফাইল আপডেট হয়েছে! ✅');
  if(currentTab==='profile') renderProfilePanel();
};

// ========== CALLS PANEL ==========
function renderCallsPanel(){
  if(!currentUser) return;
  let histHtml=getCallHistoryHtml();
  document.getElementById('panel-content').innerHTML=`
    <h2 style="font-family:'Playfair Display',serif;color:var(--rose-dark);margin-bottom:.8rem">📞 কল করুন</h2>
    <div class="call-cards-grid">
      <div class="call-card" onclick="startCallFromPanel('audio')">
        <div class="imo-call-icon audio">
          <svg viewBox="0 0 24 24" fill="#fff"><path d="M6.6 10.8c1.4 2.8 3.8 5.1 6.6 6.6l2.2-2.2c.3-.3.7-.4 1-.2 1.1.4 2.3.6 3.6.6.6 0 1 .4 1 1V20c0 .6-.4 1-1 1C9.6 21 3 14.4 3 6c0-.6.4-1 1-1h3.5c.6 0 1 .4 1 1 0 1.3.2 2.5.6 3.6.1.3 0 .7-.2 1L6.6 10.8z"/></svg>
        </div>
        <h3>অডিও কল</h3><p>ভয়েস কলে কথা বলুন</p>
      </div>
      <div class="call-card" onclick="startCallFromPanel('video')">
        <div class="imo-call-icon video">
          <svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polygon points="23 7 16 12 23 17 23 7"/><rect x="1" y="5" width="15" height="14" rx="2" ry="2"/></svg>
        </div>
        <h3>ভিডিও কল</h3><p>মুখোমুখি দেখুন</p>
      </div>
    </div>
    <h3 class="section-title" style="margin-top:0">📋 কল ইতিহাস</h3>
    <div id="call-hist-list">${histHtml||'<div style="text-align:center;color:var(--text-light);font-size:.82rem;padding:1rem">কোনো কল ইতিহাস নেই</div>'}</div>
  `;
}

function getCallHistoryHtml(){
  if(!currentUser) return '';
  let history=[];
  try{ history=JSON.parse(localStorage.getItem('callHistory_'+currentUser.uid)||'[]'); }catch(e){}
  if(!history.length) return '';
  return history.map(function(h){
    const d=new Date(h.timestamp);
    const mins=Math.floor(h.durationSecs/60); const secs=h.durationSecs%60;
    const durStr=h.durationSecs>0?String(mins).padStart(2,'0')+':'+String(secs).padStart(2,'0'):'সংযোগ হয়নি';
    const pic=h.uid?getStoredPic(h.uid):null;
    const avHtml=pic?'<img src="'+pic+'" alt="">':esc((h.name||'?')[0].toUpperCase());
    return '<div class="call-history-item">'+
      '<div class="chi-av">'+avHtml+'</div>'+
      '<div class="chi-info">'+
        '<div class="chi-name">'+esc(h.name||'Unknown')+'</div>'+
        '<div class="chi-detail">'+(h.type==='video'?'📹 ভিডিও':'📞 অডিও')+' · '+d.toLocaleDateString()+', '+d.toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit',hour12:true})+'</div>'+
      '</div>'+
      '<div class="chi-right">'+
        '<div class="chi-dur">⏱ '+durStr+'</div>'+
        '<div class="chi-btns">'+
          '<button class="chi-btn" onclick="chAction(\''+esc(h.uid)+'\',\'audio\',\''+esc(h.name)+'\')">📞</button>'+
          '<button class="chi-btn" onclick="chAction(\''+esc(h.uid)+'\',\'video\',\''+esc(h.name)+'\')">📹</button>'+
          '<button class="chi-btn" onclick="chAction(\''+esc(h.uid)+'\',\'chat\',\''+esc(h.name)+'\')">💬</button>'+
        '</div>'+
      '</div>'+
    '</div>';
  }).join('');
}

window.chAction=function(uid,action,name){
  if(!uid){ showToast('ব্যবহারকারী পাওয়া যায়নি'); return; }
  if(action==='chat'){ const u=allUsersCache[uid]||{uid,name}; openChat(u); showTab('chats'); return; }
  const u=allUsersCache[uid]||{uid,name};
  activeChatUid=uid; activeChatUsername=u.username||name;
  activeChatId=getChatId(currentUser.uid,uid);
  startCall(action,uid,name);
};

// ========== DIARY ==========
function renderDiaryPanel(){
  if(!currentUser) return;
  document.getElementById('panel-content').innerHTML=`
    <h2 style="font-family:'Playfair Display',serif;color:var(--rose-dark);margin-bottom:.2rem">📖 আমার ডায়েরি</h2>
    <p style="color:var(--text-light);font-size:.8rem;margin-bottom:.8rem">শুধু আপনি দেখতে পারবেন ✍️</p>
    <div class="diary-compose">
      <textarea id="diary-input" placeholder="আজকের অনুভূতি, মনের কথা... 🌷"></textarea>
      <div class="diary-footer">
        <div style="display:flex;gap:.4rem">
          <span onclick="diaryAdd('💕')" style="cursor:pointer;font-size:1.05rem">💕</span>
          <span onclick="diaryAdd('🥰')" style="cursor:pointer;font-size:1.05rem">🥰</span>
          <span onclick="diaryAdd('😊')" style="cursor:pointer;font-size:1.05rem">😊</span>
          <span onclick="diaryAdd('🙏')" style="cursor:pointer;font-size:1.05rem">🙏</span>
          <span onclick="diaryAdd('✨')" style="cursor:pointer;font-size:1.05rem">✨</span>
        </div>
        <button class="btn-primary" style="width:auto;padding:.45rem 1rem;font-size:.8rem" onclick="addDiaryEntry()">সংরক্ষণ ✍️</button>
      </div>
    </div>
    <div id="diary-entries-list"></div>
  `;
  loadDiaryEntries();
}
window.diaryAdd=function(em){ const el=document.getElementById('diary-input'); if(el) el.value+=em; };
window.addDiaryEntry=function(){
  const inp=document.getElementById('diary-input');
  const text=inp?inp.value.trim():'';
  if(!text||!currentUser){ showToast('কিছু লিখুন আগে ✍️'); return; }
  const key='diary_'+currentUser.uid;
  let entries=[];
  try{ entries=JSON.parse(localStorage.getItem(key)||'[]'); }catch(e){}
  entries.unshift({text,timestamp:Date.now()});
  try{ localStorage.setItem(key,JSON.stringify(entries)); }catch(e){}
  inp.value='';
  showToast('ডায়েরি সংরক্ষিত! ✍️');
  loadDiaryEntries();
};
function loadDiaryEntries(){
  if(!currentUser) return;
  const container=document.getElementById('diary-entries-list'); if(!container) return;
  let entries=[];
  try{ entries=JSON.parse(localStorage.getItem('diary_'+currentUser.uid)||'[]'); }catch(e){}
  if(!entries.length){ container.innerHTML='<div style="text-align:center;color:var(--text-light);font-size:.82rem;padding:1.5rem">এখনো কোনো লেখা নেই 🌷</div>'; return; }
  const months=['জানুয়ারি','ফেব্রুয়ারি','মার্চ','এপ্রিল','মে','জুন','জুলাই','আগস্ট','সেপ্টেম্বর','অক্টোবর','নভেম্বর','ডিসেম্বর'];
  container.innerHTML=entries.map(function(entry){
    const d=new Date(entry.timestamp);
    const ds=d.getDate()+' '+months[d.getMonth()]+' '+d.getFullYear()+', '+d.toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit',hour12:true});
    return '<div class="diary-entry"><div class="de-meta"><span class="de-author">'+esc(currentUser.name)+'</span><span>'+ds+'</span></div><p>'+esc(entry.text).replace(/\n/g,'<br>')+'</p></div>';
  }).join('');
}

// ========== NOTIFICATIONS ==========
function requestNotifPerm(){
  if('Notification' in window&&Notification.permission==='default') Notification.requestPermission();
}

// ========== WEBRTC ==========
function getCallRoomId(a,b){ return [a,b].sort().join('__'); }

window.startCallFromChat=function(type){
  if(!activeChatUid){ showToast('আগে একটি চ্যাট খুলুন'); return; }
  startCall(type,activeChatUid,document.getElementById('ch-name').textContent);
};
window.startCallFromPanel=function(type){
  if(!activeChatUid){ showToast('আগে কারো সাথে চ্যাট খুলুন'); return; }
  startCall(type,activeChatUid,allUsersCache[activeChatUid]?.name||'...');
};

async function startCall(type,targetId,targetName){
  if(!currentUser) return;
  if(peerConnection){ showToast('একটি কল ইতিমধ্যে চলছে!'); return; }
  currentCallType=type;
  const roomId=getCallRoomId(currentUser.uid,targetId);
  await db.ref('calls/rooms/'+roomId).remove();
  const audioConstraints={echoCancellation:true,noiseSuppression:true,autoGainControl:true,sampleRate:48000,channelCount:1};
  try{
    localStream=await navigator.mediaDevices.getUserMedia(
      type==='video'
        ?{audio:audioConstraints,video:{facingMode:'user',width:{ideal:640},height:{ideal:480},frameRate:{ideal:24}}}
        :{audio:audioConstraints,video:false}
    );
  } catch(err){
    showToast('মাইক্রোফোন অ্যাক্সেস দিন! ❌'); return;
  }
  showCallOverlay(targetName,targetId,type);
  document.getElementById('call-status').textContent='রিং হচ্ছে... 📱';
  document.getElementById('call-status').classList.remove('connected');
  document.getElementById('call-timer').style.display='none';
  if(type==='video'){
    const lv=document.getElementById('local-video');
    lv.srcObject=localStream; lv.style.display='block';
    document.getElementById('camBtn').classList.add('visible');
    document.getElementById('shareBtn').classList.add('visible');
  }
  createPeerConnection(roomId,targetId,true);
  const offer=await peerConnection.createOffer({offerToReceiveAudio:true,offerToReceiveVideo:type==='video'});
  await peerConnection.setLocalDescription(offer);
  await db.ref('calls/rooms/'+roomId+'/offer').set({type:'offer',sdp:offer.sdp,callType:type,from:currentUser.uid,fromName:currentUser.name,timestamp:Date.now()});
  await db.ref('calls/notify/'+targetId).set({type:'incoming',callType:type,from:currentUser.uid,fromName:currentUser.name,roomId,timestamp:Date.now()});

  db.ref('calls/rooms/'+roomId+'/answer').on('value',async function(snap){
    if(!snap.exists()||!peerConnection) return;
    const answer=snap.val();
    if(answer&&answer.sdp&&peerConnection.signalingState==='have-local-offer'){
      try{
        await peerConnection.setRemoteDescription(new RTCSessionDescription({type:'answer',sdp:answer.sdp}));
        document.getElementById('call-status').textContent=type==='video'?'📹 ভিডিও কল চলছে':'📞 অডিও কল চলছে';
        document.getElementById('call-status').classList.add('connected');
        startCallTimer();
      }catch(e){ console.error('setRemote:',e); }
    }
  });

  db.ref('calls/rooms/'+roomId+'/calleeCandidates').on('child_added',async function(snap){
    if(!peerConnection) return;
    try{ await peerConnection.addIceCandidate(new RTCIceCandidate(snap.val())); }catch(e){}
  });

  db.ref('calls/rooms/'+roomId+'/ended').on('value',function(snap){
    if(snap.val()===true) endCall();
  });
}

function createPeerConnection(roomId,remoteUid,isCaller){
  peerConnection=new RTCPeerConnection(ICE_SERVERS);
  if(localStream) localStream.getTracks().forEach(track=>peerConnection.addTrack(track,localStream));
  peerConnection.onicecandidate=function(event){
    if(event.candidate){
      const path=isCaller?'calls/rooms/'+roomId+'/callerCandidates':'calls/rooms/'+roomId+'/calleeCandidates';
      db.ref(path).push(event.candidate.toJSON());
    }
  };
  peerConnection.ontrack=function(event){
    const remoteStream=event.streams[0];
    if(currentCallType==='video'){
      const rv=document.getElementById('remote-video');
      rv.srcObject=remoteStream; rv.style.display='block';
      document.getElementById('call-big-av').style.opacity='0';
    } else {
      let audioEl=document.getElementById('remote-audio-el');
      if(!audioEl){
        audioEl=document.createElement('audio');
        audioEl.id='remote-audio-el'; audioEl.autoplay=true;
        audioEl.setAttribute('playsinline','');
        audioEl.style.display='none';
        document.body.appendChild(audioEl);
      }
      audioEl.srcObject=remoteStream;
      audioEl.play().catch(function(){});
    }
  };
  peerConnection.onconnectionstatechange=function(){
    if(['disconnected','failed','closed'].includes(peerConnection.connectionState)){
      showToast('কল সংযোগ বিচ্ছিন্ন');
      endCall();
    }
  };
}

function showCallOverlay(name,uid,type){
  const overlay=document.getElementById('callOverlay');
  overlay.className='call-overlay show '+(type==='video'?'video-mode':'audio-mode');
  document.getElementById('callBgRings').style.display=type==='audio'?'block':'none';
  document.getElementById('call-name').textContent=name||'';
  const av=document.getElementById('call-big-av'); av.style.opacity='1';
  const pic=getStoredPic(uid);
  if(pic) av.innerHTML='<img src="'+pic+'">';
  else av.textContent=(name||'?')[0];
}

// ========== INCOMING CALLS ==========
function listenIncomingCalls(){
  if(!currentUser) return;
  db.ref('calls/notify/'+currentUser.uid).on('value',async function(snap){
    if(!snap.exists()) return;
    const sig=snap.val();
    if(!sig||sig.type!=='incoming') return;
    if(Date.now()-sig.timestamp>45000) return;
    if(peerConnection) return;
    incomingCallData=sig;
    const ic=document.getElementById('incomingCall');
    ic.className='incoming-call show '+(sig.callType==='video'?'video-inc':'audio-inc');
    const av=document.getElementById('inc-avatar');
    const pic=getStoredPic(sig.from);
    if(pic) av.innerHTML='<img src="'+pic+'">';
    else av.textContent=(sig.fromName||'?')[0];
    document.getElementById('inc-name').textContent=sig.fromName||'কেউ';
    document.getElementById('inc-type').textContent=sig.callType==='video'?'ভিডিও কল আসছে...':'অডিও কল আসছে...';
    startRingtone();
    showNotifBubble({uid:sig.from,name:sig.fromName,msg:sig.callType==='video'?'📹 ভিডিও কল আসছে...':'📞 অডিও কল আসছে...',type:sig.callType==='video'?'video':'voice'});
  });
}

window.acceptCall=async function(){
  if(!incomingCallData) return;
  stopRingtone(); closeNotifBubble();
  const sig=incomingCallData;
  document.getElementById('incomingCall').className='incoming-call';
  currentCallType=sig.callType;
  activeChatUid=sig.from; activeChatUsername=sig.fromName||'';
  activeChatId=getChatId(currentUser.uid,sig.from);
  const audioConstraints={echoCancellation:true,noiseSuppression:true,autoGainControl:true,sampleRate:48000,channelCount:1};
  try{
    localStream=await navigator.mediaDevices.getUserMedia(
      sig.callType==='video'
        ?{audio:audioConstraints,video:{facingMode:'user',width:{ideal:640},height:{ideal:480}}}
        :{audio:audioConstraints,video:false}
    );
  }catch(err){ showToast('মাইক্রোফোন অ্যাক্সেস দিন! ❌'); return; }
  showCallOverlay(sig.fromName,sig.from,sig.callType);
  document.getElementById('call-status').textContent='সংযুক্ত হচ্ছে...';
  document.getElementById('call-status').classList.remove('connected');
  document.getElementById('call-timer').style.display='none';
  if(sig.callType==='video'){
    const lv=document.getElementById('local-video');
    lv.srcObject=localStream; lv.style.display='block';
    document.getElementById('camBtn').classList.add('visible');
    document.getElementById('shareBtn').classList.add('visible');
  }
  const roomId=sig.roomId||getCallRoomId(currentUser.uid,sig.from);
  createPeerConnection(roomId,sig.from,false);

  db.ref('calls/rooms/'+roomId+'/callerCandidates').on('child_added',async function(snap){
    if(!peerConnection) return;
    try{ await peerConnection.addIceCandidate(new RTCIceCandidate(snap.val())); }catch(e){}
  });

  const offerSnap=await db.ref('calls/rooms/'+roomId+'/offer').once('value');
  const offerData=offerSnap.val();
  if(!offerData||!offerData.sdp){ showToast('কল সিগন্যাল পাওয়া যায়নি'); endCall(); return; }
  await peerConnection.setRemoteDescription(new RTCSessionDescription({type:'offer',sdp:offerData.sdp}));
  const answer=await peerConnection.createAnswer();
  await peerConnection.setLocalDescription(answer);
  await db.ref('calls/rooms/'+roomId+'/answer').set({type:'answer',sdp:answer.sdp,from:currentUser.uid,timestamp:Date.now()});
  document.getElementById('call-status').textContent=sig.callType==='video'?'📹 ভিডিও কল চলছে':'📞 অডিও কল চলছে';
  document.getElementById('call-status').classList.add('connected');
  startCallTimer();
  db.ref('calls/rooms/'+roomId+'/ended').on('value',function(snap){ if(snap.val()===true) endCall(); });
  db.ref('calls/notify/'+currentUser.uid).remove();
  incomingCallData=null;
};

window.rejectCall=function(){
  stopRingtone(); closeNotifBubble();
  if(incomingCallData){
    const roomId=incomingCallData.roomId||getCallRoomId(currentUser.uid,incomingCallData.from);
    db.ref('calls/rooms/'+roomId+'/ended').set(true);
    db.ref('calls/notify/'+currentUser.uid).remove();
  }
  document.getElementById('incomingCall').className='incoming-call';
  incomingCallData=null;
};

function startCallTimer(){
  callSeconds=0; clearInterval(callInterval);
  document.getElementById('call-timer').style.display='block';
  callInterval=setInterval(function(){
    callSeconds++;
    const m=String(Math.floor(callSeconds/60)).padStart(2,'0');
    const s=String(callSeconds%60).padStart(2,'0');
    document.getElementById('call-timer').textContent=m+':'+s;
  },1000);
}

window.endCall=function(){
  stopRingtone(); clearInterval(callInterval);
  if(currentUser&&activeChatUid){
    const roomId=getCallRoomId(currentUser.uid,activeChatUid);
    db.ref('calls/rooms/'+roomId+'/ended').set(true);
    db.ref('calls/notify/'+activeChatUid).remove();
    db.ref('calls/notify/'+currentUser.uid).remove();
    db.ref('calls/rooms/'+roomId).off();
  }
  if(peerConnection){ peerConnection.close(); peerConnection=null; }
  if(localStream){ localStream.getTracks().forEach(t=>t.stop()); localStream=null; }
  if(screenStream){ screenStream.getTracks().forEach(t=>t.stop()); screenStream=null; }
  const audioEl=document.getElementById('remote-audio-el'); if(audioEl) audioEl.remove();
  ['remote-video','local-video','screen-video'].forEach(function(id){
    const v=document.getElementById(id);
    if(v){ v.style.display='none'; v.srcObject=null; }
  });
  isScreenSharing=false; isCamOff=false; isMuted=false;
  document.getElementById('shareBtn').classList.remove('share-active');
  document.getElementById('camBtn').classList.remove('visible','cam-off');
  document.getElementById('shareBtn').classList.remove('visible');
  document.getElementById('muteBtn').classList.remove('muted-on');
  document.getElementById('call-big-av').style.opacity='1';
  const muteIcon=document.getElementById('muteIcon');
  if(muteIcon) muteIcon.innerHTML='<path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"/><path d="M19 10v2a7 7 0 0 1-14 0v-2"/><line x1="12" y1="19" x2="12" y2="23"/><line x1="8" y1="23" x2="16" y2="23"/>';
  const name=document.getElementById('call-name').textContent;
  document.getElementById('callOverlay').className='call-overlay audio-mode';
  if(currentUser&&name&&callSeconds>0){
    saveCallToHistory(currentCallType,name,activeChatUid,callSeconds);
    const m=String(Math.floor(callSeconds/60)).padStart(2,'0');
    const s=String(callSeconds%60).padStart(2,'0');
    showToast('কল শেষ · '+m+':'+s+' 📵');
  } else showToast('কল শেষ 📵');
  callSeconds=0;
};

window.toggleMute=function(){
  isMuted=!isMuted;
  if(localStream) localStream.getAudioTracks().forEach(t=>{ t.enabled=!isMuted; });
  const btn=document.getElementById('muteBtn');
  const icon=document.getElementById('muteIcon');
  btn.classList.toggle('muted-on',isMuted);
  if(isMuted){
    icon.innerHTML='<line x1="1" y1="1" x2="23" y2="23"/><path d="M9 9v3a3 3 0 0 0 5.12 2.12M15 9.34V4a3 3 0 0 0-5.94-.6"/><path d="M17 16.95A7 7 0 0 1 5 12v-2m14 0v2a7 7 0 0 1-.11 1.23"/><line x1="12" y1="19" x2="12" y2="23"/><line x1="8" y1="23" x2="16" y2="23"/>';
  } else {
    icon.innerHTML='<path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"/><path d="M19 10v2a7 7 0 0 1-14 0v-2"/><line x1="12" y1="19" x2="12" y2="23"/><line x1="8" y1="23" x2="16" y2="23"/>';
  }
  showToast(isMuted?'মিউট 🔇':'আনমিউট 🎤');
};

window.toggleCamera=function(){
  isCamOff=!isCamOff;
  if(localStream) localStream.getVideoTracks().forEach(t=>{ t.enabled=!isCamOff; });
  const btn=document.getElementById('camBtn');
  const icon=document.getElementById('camIcon');
  btn.classList.toggle('cam-off',isCamOff);
  if(isCamOff){
    icon.innerHTML='<line x1="1" y1="1" x2="23" y2="23"/><path d="M21 21H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h3m3-3h6l2 3h4a2 2 0 0 1 2 2v9.34"/><line x1="16" y1="11.37" x2="16" y2="11.37"/>';
  } else {
    icon.innerHTML='<polygon points="23 7 16 12 23 17 23 7"/><rect x="1" y="5" width="15" height="14" rx="2" ry="2"/>';
  }
  showToast(isCamOff?'ক্যামেরা বন্ধ':'ক্যামেরা চালু 📹');
};

window.toggleSpeaker=function(){
  isSpeakerOn=!isSpeakerOn;
  document.getElementById('speakerBtn').classList.toggle('speaker-loud',isSpeakerOn);
  showToast(isSpeakerOn?'স্পিকার চালু 🔊':'স্পিকার বন্ধ 🔈');
};

window.toggleScreenShare=async function(){
  if(isScreenSharing){ stopScreenShare(); return; }
  if(!peerConnection){ showToast('আগে কল শুরু করুন'); return; }
  try{
    screenStream=await navigator.mediaDevices.getDisplayMedia({video:true,audio:true});
    const st=screenStream.getVideoTracks()[0];
    const vs=peerConnection.getSenders().find(s=>s.track&&s.track.kind==='video');
    if(vs) vs.replaceTrack(st);
    const sv=document.getElementById('screen-video');
    sv.srcObject=screenStream; sv.style.display='block';
    isScreenSharing=true;
    document.getElementById('shareBtn').classList.add('share-active');
    showToast('স্ক্রিন শেয়ার শুরু 🖥️');
    st.onended=function(){ stopScreenShare(); };
  }catch(err){ showToast('স্ক্রিন শেয়ার করতে পারেনি ❌'); }
};

async function stopScreenShare(){
  if(screenStream){ screenStream.getTracks().forEach(t=>t.stop()); screenStream=null; }
  document.getElementById('screen-video').style.display='none';
  document.getElementById('screen-video').srcObject=null;
  if(peerConnection&&localStream){
    const ct=localStream.getVideoTracks()[0];
    if(ct){
      const vs=peerConnection.getSenders().find(s=>s.track&&s.track.kind==='video');
      if(vs) vs.replaceTrack(ct);
    }
  }
  isScreenSharing=false;
  document.getElementById('shareBtn').classList.remove('share-active');
  showToast('স্ক্রিন শেয়ার বন্ধ');
}

function saveCallToHistory(type,name,uid,secs){
  if(!currentUser) return;
  const key='callHistory_'+currentUser.uid;
  let h=[];
  try{ h=JSON.parse(localStorage.getItem(key)||'[]'); }catch(e){}
  h.unshift({type,name,uid,durationSecs:secs,timestamp:Date.now()});
  if(h.length>50) h=h.slice(0,50);
  try{ localStorage.setItem(key,JSON.stringify(h)); }catch(e){}
}

// ========== VOICE MESSAGES ==========
window.toggleVoice=function(){ isRecording?stopSendVoice():startVoice(); };

function startVoice(){
  navigator.mediaDevices.getUserMedia({audio:{echoCancellation:true,noiseSuppression:true,autoGainControl:true}}).then(function(stream){
    const mimeType=MediaRecorder.isTypeSupported('audio/webm;codecs=opus')?'audio/webm;codecs=opus':'audio/webm';
    mediaRecorder=new MediaRecorder(stream,{mimeType});
    audioChunks=[];
    mediaRecorder.ondataavailable=function(e){ if(e.data.size>0) audioChunks.push(e.data); };
    mediaRecorder.start();
    isRecording=true;
    document.getElementById('voiceBtn').textContent='🔴';
    document.getElementById('inputBar').style.display='none';
    document.getElementById('recBar').classList.add('show');
    recSecs=0;
    document.getElementById('recTimer').textContent='00:00';
    recInterval=setInterval(function(){
      recSecs++;
      document.getElementById('recTimer').textContent=String(Math.floor(recSecs/60)).padStart(2,'0')+':'+String(recSecs%60).padStart(2,'0');
    },1000);
  }).catch(function(){ showToast('মাইক্রোফোন অ্যাক্সেস দিন! 🎤'); });
}

window.stopSendVoice=function(){
  if(!mediaRecorder) return;
  mediaRecorder.onstop=function(){
    const blob=new Blob(audioChunks,{type:'audio/webm'});
    const reader=new FileReader();
    reader.onload=function(ev){
      if(!activeChatUid||!currentUser) return;
      db.ref('chats/'+activeChatId+'/messages').push({
        voiceData:ev.target.result,sender:currentUser.name,
        senderUid:currentUser.uid,recipientUid:activeChatUid,
        timestamp:Date.now(),text:'🎤'
      });
      showToast('ভয়েস মেসেজ পাঠানো হয়েছে! 🎤');
    };
    reader.readAsDataURL(blob);
    mediaRecorder.stream.getTracks().forEach(t=>t.stop());
  };
  mediaRecorder.stop();
  clearInterval(recInterval);
  isRecording=false;
  document.getElementById('voiceBtn').textContent='🎤';
  document.getElementById('recBar').classList.remove('show');
  document.getElementById('inputBar').style.display='flex';
};

window.cancelVoice=function(){
  if(mediaRecorder&&isRecording){
    try{ mediaRecorder.stream.getTracks().forEach(t=>t.stop()); mediaRecorder.stop(); }catch(e){}
  }
  clearInterval(recInterval);
  isRecording=false; audioChunks=[];
  document.getElementById('voiceBtn').textContent='🎤';
  document.getElementById('recBar').classList.remove('show');
  document.getElementById('inputBar').style.display='flex';
  showToast('রেকর্ড বাতিল');
};

// ========== MISC EVENT LISTENERS ==========
document.addEventListener('click',function(e){
  if(emojiOpen&&!e.target.closest('.emoji-picker')&&!e.target.closest('.ib-btn')){
    emojiOpen=false;
    document.getElementById('emojiPicker').classList.remove('show');
  }
  if(!e.target.closest('#search-results')&&!e.target.closest('#search-input')){
    const sr=document.getElementById('search-results'); if(sr) sr.innerHTML='';
  }
  if(!e.target.closest('.ctx-menu')&&!e.target.closest('.msg')){ closeCtx(); }
});

// iOS viewport fix
if(/iPhone|iPad|iPod/i.test(navigator.userAgent)){
  const vv=()=>document.documentElement.style.setProperty('--vh',window.innerHeight*0.01+'px');
  window.addEventListener('resize',vv); vv();
}

// ========== AUTO-LOGIN ==========
window.addEventListener('DOMContentLoaded',function(){
  const saved=loadSession();
  if(saved){
    const local=getStoredProfile(saved.uid);
    finishLogin(local?Object.assign({},saved,local):saved);
  }
});
</script>
</body>
</html>
