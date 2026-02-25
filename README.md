<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Dami 🎂</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">

<style>
*{
  box-sizing:border-box;
  font-family:'Poppins',sans-serif;
  margin:0;
  padding:0;
  -webkit-tap-highlight-color: transparent;
}

body{
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  background:linear-gradient(135deg,#ff9a9e,#fad0c4);
  padding:20px;
  overflow:hidden;
  position:relative;
}

.card{
  background:#fff;
  width:100%;
  max-width:400px;
  padding:30px 25px;
  border-radius:25px;
  text-align:center;
  box-shadow:0 20px 40px rgba(0,0,0,0.15);
  position:absolute;
  transition:0.6s ease;
}

h1{
  font-size:1.8rem;
  color:#ff4d6d;
  margin-bottom:15px;
}

p{
  font-size:0.95rem;
  color:#444;
  line-height:1.6;
  margin-bottom:20px;
}

button{
  border:none;
  background:#ff4d6d;
  color:#fff;
  padding:12px 22px;
  border-radius:30px;
  font-size:0.95rem;
  cursor:pointer;
  box-shadow:0 10px 20px rgba(255,77,109,0.4);
  transition:0.2s;
  margin-top:10px;
}

button:active{
  transform:scale(0.95);
}

.hidden{
  opacity:0;
  pointer-events:none;
  transform:translateY(30px);
}

.footer{
  margin-top:15px;
  font-size:0.75rem;
  color:#999;
}

canvas{
  position:fixed;
  top:0;
  left:0;
  pointer-events:none;
}

/* Floating balloons */
.balloon{
  position:absolute;
  bottom:-150px;
  width:40px;
  height:55px;
  background:radial-gradient(circle at 30% 30%, #fff, #ff4d6d);
  border-radius:50% 50% 45% 45%;
  animation:floatUp linear infinite;
  opacity:0.7;
}

@keyframes floatUp{
  to{
    transform:translateY(-120vh);
  }
}

/* Wish sparkle */
.sparkle{
  position:absolute;
  font-size:20px;
  animation:pop 1s ease forwards;
}

@keyframes pop{
  0%{transform:scale(0);opacity:1;}
  100%{transform:scale(2);opacity:0;}
}
</style>
</head>

<body>

<!-- SCREEN 1 -->
<div class="card" id="screen1">
  <h1>Hey Dami 🎂✨</h1>
  <p>
    Today isn’t just another day…<br><br>
    The world became brighter the day you were born.
  </p>
  <button onclick="nextScreen(1)">See Why 💌</button>
  <div class="footer">— Ridwan</div>
</div>

<!-- SCREEN 2 -->
<div class="card hidden" id="screen2">
  <h1>Because You Are 🌸</h1>
  <p>
    Not just a year older,<br>
    but a year more powerful.<br><br>
    More beautiful.<br>
    More unforgettable.
  </p>
  <button onclick="nextScreen(2)">There’s More 🎉</button>
</div>

<!-- SCREEN 3 -->
<div class="card hidden" id="screen3">
  <h1>Happy Birthday Dami 🎉💖</h1>
  <p>
    This new age is your season to achieve great things.<br>
    I truly believe in you,<br>
    and I will always be rooting for you.<br><br>
    Keep shining. Keep winning.
  </p>

  <button onclick="makeWish()">Make a Wish ✨</button>
  <p id="wishMessage" style="display:none; margin-top:15px; color:#ff4d6d; font-weight:600;">
    I hope one of those wishes secretly includes me 😉💖
  </p>

  <div class="footer">With love — Ridwan ❤️</div>
</div>

<canvas id="confetti"></canvas>

<script>
function nextScreen(current){
  document.getElementById("screen"+current).classList.add("hidden");
  document.getElementById("screen"+(current+1)).classList.remove("hidden");
  if(current === 2){
    launchConfetti();
    createBalloons();
  }
}

/* Confetti */
const canvas = document.getElementById("confetti");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
let pieces = [];

function launchConfetti(){
  for(let i=0;i<120;i++){
    pieces.push({
      x: Math.random()*canvas.width,
      y: Math.random()*canvas.height- canvas.height,
      size: Math.random()*8+4,
      speed: Math.random()*3+2,
      color: `hsl(${Math.random()*360},100%,70%)`
    });
  }
  animate();
}

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  pieces.forEach(p=>{
    p.y += p.speed;
    ctx.fillStyle = p.color;
    ctx.fillRect(p.x,p.y,p.size,p.size);
  });
  requestAnimationFrame(animate);
}

/* Balloons */
function createBalloons(){
  for(let i=0;i<10;i++){
    const balloon=document.createElement("div");
    balloon.classList.add("balloon");
    balloon.style.left=Math.random()*100+"vw";
    balloon.style.animationDuration=(6+Math.random()*4)+"s";
    document.body.appendChild(balloon);
  }
}

/* Wish Feature */
function makeWish(){
  document.getElementById("wishMessage").style.display="block";
  for(let i=0;i<15;i++){
    const sparkle=document.createElement("div");
    sparkle.classList.add("sparkle");
    sparkle.innerHTML="✨";
    sparkle.style.left=Math.random()*100+"vw";
    sparkle.style.top=Math.random()*100+"vh";
    document.body.appendChild(sparkle);
    setTimeout(()=>sparkle.remove(),1000);
  }
}
</script>

</body>
</html>
