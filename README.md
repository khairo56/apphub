<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#0d1117">
<title>AppHub</title>
<link rel="manifest" href='data:application/manifest+json,{"name":"AppHub","short_name":"AppHub","start_url":".","display":"standalone","background_color":"%230d1117","theme_color":"%230d1117"}'>
<style>
:root{--bg:#0d1117;--card:#161b22;--line:#30363d;--txt:#e6edf3;--dim:#8b949e;--acc:#2f81f7}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
body{margin:0;font:15px/1.5 system-ui,sans-serif;background:var(--bg);color:var(--txt);padding-bottom:40px}
header{position:sticky;top:0;z-index:5;background:rgba(13,17,23,.92);padding:14px 16px 10px;border-bottom:1px solid var(--line)}
h1{margin:0 0 10px;font-size:17px}
#q{width:100%;font:inherit;padding:11px 13px;border-radius:10px;border:1px solid var(--line);background:#0d1117;color:var(--txt)}
main{padding:16px}
h2{font-size:12px;text-transform:uppercase;color:var(--dim);margin:18px 0 10px}
h2:first-child{margin-top:0}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(80px,1fr));gap:10px}
.tile{display:flex;flex-direction:column;align-items:center;gap:7px;padding:12px 6px;border-radius:14px;background:var(--card);border:1px solid var(--line);text-decoration:none;color:var(--txt)}
.tile:active{transform:scale(.95)}
.ico{width:42px;height:42px;border-radius:12px;display:grid;place-items:center;font-size:22px}
.nm{font-size:11.5px;text-align:center;color:var(--dim)}
.tip{margin-top:26px;font-size:12.5px;color:var(--dim);border-top:1px solid var(--line);padding-top:14px}
.tip b{color:var(--txt)}
</style>
</head>
<body>
<header>
  <h1>AppHub</h1>
  <input id="q" type="search" placeholder="Search apps…" autocomplete="off">
</header>
<main>
  <h2>Apps</h2>
  <div class="grid" id="apps"></div>
  <h2>Phone functions</h2>
  <div class="grid" id="sys"></div>
  <div class="tip">
    <b>How to use with little data:</b> open this page once with data or Wi-Fi, add it to your home screen.
    After that it opens with zero data and only the app you tap uses data.
  </div>
</main>
<script>
const APPS=[
{n:'WhatsApp',e:'💬',c:'#25D366',web:'https://web.whatsapp.com',deep:'whatsapp://send'},
{n:'Telegram',e:'✈️',c:'#2AABEE',web:'https://web.telegram.org/a/',deep:'tg://'},
{n:'Facebook',e:'📘',c:'#1877F2',web:'https://m.facebook.com',deep:'fb://'},
{n:'Messenger',e:'💌',c:'#A334FA',web:'https://m.me',deep:'fb-messenger://'},
{n:'Instagram',e:'📸',c:'#E1306C',web:'https://www.instagram.com',deep:'instagram://'},
{n:'YouTube',e:'▶️',c:'#FF0000',web:'https://m.youtube.com',deep:'vnd.youtube://'},
{n:'TikTok',e:'🎵',c:'#EE1D52',web:'https://www.tiktok.com',deep:'snssdk1233://'},
{n:'X',e:'🐦',c:'#888',web:'https://x.com',deep:'twitter://'},
{n:'Gmail',e:'📧',c:'#EA4335',web:'https://mail.google.com',deep:'googlegmail://'},
{n:'Maps',e:'🗺️',c:'#34A853',web:'https://maps.google.com',deep:'geo:'},
{n:'Spotify',e:'🎧',c:'#1DB954',web:'https://open.spotify.com',deep:'spotify://'},
{n:'Netflix',e:'🎬',c:'#E50914',web:'https://www.netflix.com',deep:'nflx://'},
{n:'Play Store',e:'🛍️',c:'#00D2FF',web:'https://play.google.com/store',deep:'market://'}
];
const SYS=[
{n:'Phone',e:'📞',c:'#3FB950',deep:'tel:'},
{n:'SMS',e:'✉️',c:'#2F81F7',deep:'sms:'}
];
function launch(app){
  const t0=Date.now();
  location.href=app.deep;
  setTimeout(()=>{ if(!document.hidden&&app.web) location.href=app.web; },700);
}
function tile(a){
  const el=document.createElement('a');
  el.className='tile';
  el.href=a.web||a.deep;
  el.dataset.name=a.n.toLowerCase();
  el.innerHTML='<span class="ico" style="background:'+a.c+'22;color:'+a.c+'">'+a.e+'</span><span class="nm">'+a.n+'</span>';
  el.onclick=ev=>{ if(a.deep){ev.preventDefault();launch(a);} };
  return el;
}
const A=document.getElementById('apps'),S=document.getElementById('sys');
APPS.forEach(a=>A.append(tile(a)));
SYS.forEach(a=>S.append(tile(a)));
document.getElementById('q').oninput=e=>{
  const q=e.target.value.trim().toLowerCase();
  document.querySelectorAll('.tile').forEach(t=>{
    t.style.display=(!q||t.dataset.name.includes(q))?'':'none';
  });
};
</script>
</body>
</html># apphub