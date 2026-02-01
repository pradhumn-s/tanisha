# tanisha
<!doctype html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>One Question ❤️</title>

<style>
html,body{
  margin:0;
  height:100%;
  font-family: 'Segoe UI', system-ui, sans-serif;
  overflow:hidden;
}

body{
  display:flex;
  align-items:center;
  justify-content:center;
  background: linear-gradient(135deg,#ff4ecd,#6a5cff,#00e0ff);
  background-size:300% 300%;
  animation:bg 8s infinite ease-in-out;
}

@keyframes bg{
  0%{background-position:0% 50%}
  50%{background-position:100% 50%}
  100%{background-position:0% 50%}
}

.card{
  background:rgba(255,255,255,0.18);
  backdrop-filter: blur(16px);
  padding:32px 26px;
  border-radius:26px;
  text-align:center;
  box-shadow:0 30px 70px rgba(0,0,0,0.35);
  width:min(520px,92vw);
}

h1{
  color:white;
  font-size:clamp(28px,4vw,40px);
  margin-bottom:10px;
}

p{
  color:rgba(255,255,255,0.85);
  font-size:16px;
}

.buttons{
  margin-top:26px;
  display:flex;
  gap:20px;
  justify-content:center;
}

button{
  border:none;
  padding:14px 24px;
  border-radius:18px;
  font-size:16px;
  font-weight:700;
  cursor:pointer;
  transition:all .15s ease;
  box-shadow:0 15px 30px rgba(0,0,0,0.3);
}

#yes{
  background:linear-gradient(135deg,#00ffb3,#00d4ff,#6a5cff);
  color:#05152e;
}

#no{
  background:linear-gradient(135deg,#ff6a88,#ff99ac);
  color:#3a0916;
  position:relative;
}

.celebrate{
  position:fixed;
  inset:0;
  display:none;
  align-items:center;
  justify-content:center;
  background:linear-gradient(135deg,#ff2fb1,#7a5cff,#00e0ff,#00ffb3);
  background-size:400% 400%;
  animation:bg 6s infinite ease-in-out;
  z-index:999;
}

.message{
  background:rgba(255,255,255,0.18);
  padding:32px 28px;
  border-radius:30px;
  backdrop-filter: blur(16px);
  text-align:center;
  color:white;
  box-shadow:0 30px 80px rgba(0,0,0,0.4);
}

.message h2{
  font-size:clamp(28px,4vw,44px);
  margin-bottom:10px;
}

.snow{
  position:absolute;
  inset:0;
  pointer-events:none;
}

.flake{
  position:absolute;
  top:-10vh;
  animation:fall linear forwards;
}

@keyframes fall{
  to{
    transform:translate(var(--x),110vh) rotate(var(--r));
  }
}
</style>
</head>

<body>

<div class="card">
  <h1>Tanisha, do you love me? ❤️</h1>
  <p>Your husband is asking… choose carefully 😌</p>

  <div class="buttons">
    <button id="yes">Yes 💖</button>
    <button id="no">No 🙃</button>
  </div>
</div>

<div class="celebrate" id="celebrate">
  <div class="snow" id="snow"></div>
  <div class="message">
    <h2>Of course you do 😘💍</h2>
    <p>Tanisha, my wife forever ❤️  
    No refunds, no returns, only love 😌✨</p>
  </div>
</div>

<script>
const noBtn = document.getElementById('no');
const yesBtn = document.getElementById('yes');
const celebrate = document.getElementById('celebrate');
const snow = document.getElementById('snow');

let noScale = 1;
let yesScale = 1;
let speed = 120;

const texts = [
  "Nice try 😏",
  "Nope 😜",
  "Almost 😂",
  "Still trying? 😌",
  "Wife.exe failed 🤭"
];

function moveNo(){
  const w = innerWidth - noBtn.offsetWidth;
  const h = innerHeight - noBtn.offsetHeight;

  noBtn.style.position = "fixed";
  noBtn.style.left = Math.random()*w + "px";
  noBtn.style.top = Math.random()*h + "px";

  noScale -= 0.05;
  noScale = Math.max(0.55,noScale);
  noBtn.style.transform = `scale(${noScale})`;

  yesScale += 0.05;
  yesBtn.style.transform = `scale(${yesScale})`;

  noBtn.textContent = texts[Math.floor(Math.random()*texts.length)];
}

window.addEventListener("mousemove",e=>{
  const r = noBtn.getBoundingClientRect();
  const d = Math.hypot(
    e.clientX-(r.left+r.width/2),
    e.clientY-(r.top+r.height/2)
  );
  if(d < speed){
    moveNo();
    speed += 8;
  }
});

noBtn.addEventListener("click",e=>{
  e.preventDefault();
  moveNo();
});

yesBtn.addEventListener("click",()=>{
  celebrate.style.display="flex";
  startSnow();
});

const emojis = ["💖","💘","💕","❤️","😘","😍","💋","🌹","✨","🥰"];

function startSnow(){
  setInterval(()=>{
    for(let i=0;i<6;i++) spawn();
  },200);
}

function spawn(){
  const f = document.createElement("div");
  f.className="flake";
  f.textContent = emojis[Math.floor(Math.random()*emojis.length)];
  f.style.left = Math.random()*innerWidth+"px";
  f.style.fontSize = 20+Math.random()*30+"px";
  f.style.setProperty("--x",(-80+Math.random()*160)+"px");
  f.style.setProperty("--r",(-180+Math.random()*360)+"deg");
  f.style.animationDuration = 3+Math.random()*3+"s";
  snow.appendChild(f);
  setTimeout(()=>f.remove(),6000);
}
</script>

</body>
</html>
