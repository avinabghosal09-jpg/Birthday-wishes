<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Happy Birthday Aishani 🎈</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  margin:0;
  font-family:'Segoe UI',sans-serif;
  background:radial-gradient(circle at top,#6a1b9a,#b71c1c);
  color:#fff;
  text-align:center;
  overflow-x:hidden;
}

section{padding:30px}
.hidden{display:none}

/* BUTTONS */
button{
  padding:14px 30px;
  border:none;
  border-radius:30px;
  font-size:16px;
  cursor:pointer;
  color:#fff;
  background:linear-gradient(45deg,#ff1744,#d500f9);
  box-shadow:0 0 18px rgba(255,0,150,.6);
}

/* OPTIONS */
.options button{
  display:block;
  width:85%;
  margin:12px auto;
}

/* POPUP */
.popup{
  background:rgba(0,0,0,.6);
  padding:30px;
  border-radius:22px;
  animation:pop .6s ease;
}
@keyframes pop{
  from{transform:scale(.6);opacity:0}
  to{transform:scale(1);opacity:1}
}

/* SPARKS */
.sparks{
  position:fixed;
  inset:0;
  pointer-events:none;
  background:
    radial-gradient(white 1px,transparent 1px),
    radial-gradient(gold 1px,transparent 1px);
  background-size:22px 22px;
  animation:sparkMove 3s linear infinite;
}
@keyframes sparkMove{
  from{background-position:0 0}
  to{background-position:22px 22px}
}

/* BALLOONS */
.balloon{
  position:fixed;
  bottom:-120px;
  font-size:60px;
  animation:floatUp 7s linear infinite;
}
@keyframes floatUp{
  to{transform:translateY(-120vh)}
}

/* CAKE (3D STYLE ILLUSION) */
.cake{
  font-size:130px;
  filter:drop-shadow(0 25px 35px rgba(0,0,0,.6));
  animation:cakeFloat 2s ease-in-out infinite alternate;
}
@keyframes cakeFloat{
  to{transform:translateY(-15px)}
}

/* GIFT */
.gift{
  font-size:130px;
  animation:shake 1.3s infinite;
  cursor:pointer;
}
@keyframes shake{
  50%{transform:rotate(6deg)}
}

/* COLLAGE */
.collage{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
  background:white;
  padding:14px;
  border-radius:22px;
}
.collage img{
  width:100%;
  border-radius:12px;
}

/* ROSE PARTICLES */
.rose{
  position:fixed;
  top:-40px;
  font-size:28px;
  pointer-events:none;
  animation:fall linear forwards;
  filter:drop-shadow(0 0 6px rgba(255,0,80,.8));
}
@keyframes fall{
  to{transform:translateY(110vh) rotate(360deg)}
}

textarea{
  width:85%;
  height:90px;
  border-radius:14px;
  border:none;
  padding:10px;
}
</style>
</head>

<body>

<div class="sparks"></div>

<!-- MUSIC -->
<iframe id="music" width="0" height="0"
src="https://www.youtube.com/embed/AS3qo8CBJcE?autoplay=1&mute=1&loop=1&playlist=AS3qo8CBJcE">
</iframe>

<!-- SOUND EFFECTS -->
<audio id="whoosh" src="https://assets.mixkit.co/sfx/preview/mixkit-fast-swoosh-transition-168.mp3"></audio>
<audio id="sparkle" src="https://assets.mixkit.co/sfx/preview/mixkit-magical-sparkle-902.mp3"></audio>
<audio id="giftSound" src="https://assets.mixkit.co/sfx/preview/mixkit-unlock-game-notification-253.mp3"></audio>

<!-- INTRO -->
<section id="intro">
<h1>Are you Aishani? 💜</h1>
<p>If yes then answer these questions!!!</p>
<button onclick="startQuiz()">YES</button>
</section>

<!-- QUIZ -->
<section id="quiz" class="hidden">
<div class="popup">
<h2 id="q"></h2>
<div class="options" id="opts"></div>
</div>
</section>

<!-- VERIFIED -->
<section id="verified" class="hidden">
<div class="popup">
<h1>YEAHH U U ARE THE ONE 🍉</h1>
<button onclick="showCake()">Continue</button>
</div>
</section>

<!-- CAKE -->
<section id="cakeSec" class="hidden">
<h1>🎈 HAPPY HAPPY BIRTHDAY 🎈</h1>
<div class="cake">🎂</div>
<button onclick="makeWish()">Make a wish 🥳</button>
</section>

<!-- WISH -->
<section id="wishBox" class="hidden">
<h2>Make a wish ✨</h2>
<textarea id="wishText"></textarea><br>
<button onclick="saveWish()">Save Wish</button>
</section>

<!-- GIFT -->
<section id="giftBox" class="hidden">
<h2>Tap 3 times to open 🎁</h2>
<div class="gift" onclick="tapGift()">🎁</div>
<p id="tapInfo"></p>
</section>

<!-- GIFT CONTENT -->
<section id="giftContent" class="hidden">
<img src="https://i.ibb.co/tpttzYvV/image.jpg" style="width:80%;border-radius:20px">
<button onclick="finalCard()">Next</button>
</section>

<!-- FINAL -->
<section id="final" class="hidden">
<h2>Just for you 💖</h2>
<div class="collage">
<img src="https://i.ibb.co/TBwPVZdP/image.jpg">
<img src="https://i.ibb.co/XfbVQ3X2/image.jpg">
<img src="https://i.ibb.co/FkqLtRWm/image.jpg">
<img src="https://i.ibb.co/TBwPVZdP/image.jpg">
</div>
<h3>With roses, memories & love 🌹</h3>
</section>

<script>
let step=0,answers=[],taps=0;
const quiz=[
{q:"What's your favourite food?",o:["Biryani","Phuchka","Logo ka dimag"],c:1},
{q:"What colour of dress you wore at FETE?",o:["Pink","Yellow","Red"],c:2},
{q:"Your favourite hobby in school?",o:["Singing","Bunking","Dominating the school"],c:1}
];

const q=document.getElementById("q"),opts=document.getElementById("opts");

function startQuiz(){
intro.classList.add("hidden");
quizSec.classList.remove("hidden");
loadQ();
}

function loadQ(){
q.innerText=quiz[step].q;
opts.innerHTML="";
quiz[step].o.forEach((x,i)=>{
let b=document.createElement("button");
b.innerText=x;
b.onclick=()=>pick(i);
opts.appendChild(b);
});
}

function pick(i){
answers.push(i);step++;
step<quiz.length?loadQ():check();
}

function check(){
if(answers[0]==1&&answers[1]==2&&answers[2]==1){
quizSec.classList.add("hidden");
verified.classList.remove("hidden");
}else{alert("Only Aishani 😅");location.reload();}
}

function showCake(){
verified.classList.add("hidden");
cakeSec.classList.remove("hidden");
document.getElementById("music").src=document.getElementById("music").src.replace("mute=1","mute=0");
document.getElementById("sparkle").play();
spawnBalloons();
}

function spawnBalloons(){
for(let i=0;i<10;i++){
let b=document.createElement("div");
b.className="balloon";
b.style.left=Math.random()*100+"%";
b.innerText="🎈";
document.body.appendChild(b);
}
}

function makeWish(){
cakeSec.classList.add("hidden");
wishBox.classList.remove("hidden");
}

function saveWish(){
localStorage.setItem("aishaniWish",wishText.value);
wishBox.classList.add("hidden");
giftBox.classList.remove("hidden");
}

function tapGift(){
taps++;
tapInfo.innerText=`Taps: ${taps}/3`;
if(taps>=3){
document.getElementById("giftSound").play();
giftBox.classList.add("hidden");
giftContent.classList.remove("hidden");
}
}

function finalCard(){
giftContent.classList.add("hidden");
final.classList.remove("hidden");
startRoseRain();
}

function startRoseRain(){
setInterval(()=>{
let r=document.createElement("div");
r.className="rose";
r.innerText="🌹";
r.style.left=Math.random()*100+"vw";
r.style.animationDuration=(5+Math.random()*5)+"s";
document.body.appendChild(r);
setTimeout(()=>r.remove(),10000);
},300);
}

const intro=document.getElementById("intro");
const quizSec=document.getElementById("quiz");
const verified=document.getElementById("verified");
const cakeSec=document.getElementById("cakeSec");
const wishBox=document.getElementById("wishBox");
const giftBox=document.getElementById("giftBox");
const giftContent=document.getElementById("giftContent");
const final=document.getElementById("final");
const tapInfo=document.getElementById("tapInfo");
const wishText=document.getElementById("wishText");
</script>

</body>
</html>
