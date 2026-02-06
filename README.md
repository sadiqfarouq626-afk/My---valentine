# My---valentine
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>For نُورَا ❤️</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:'Segoe UI',sans-serif;
}

body{
    height:100vh;
    background:linear-gradient(135deg,#ff4d6d,#ff758c,#ff9a9e);
    display:flex;
    justify-content:center;
    align-items:center;
    overflow:hidden;
}

/* ---------- hearts ---------- */
.heart{
    position:absolute;
    color:#ffffffaa;
    animation:float 6s linear infinite;
}
@keyframes float{
    0%{transform:translateY(100vh);}
    100%{transform:translateY(-10vh);}
}

/* ---------- card ---------- */
.card{
    background:white;
    width:360px;
    padding:35px;
    border-radius:25px;
    text-align:center;
    box-shadow:0 20px 50px rgba(0,0,0,.3);
    z-index:2;
}

#main,#final{display:none;}

button{
    padding:10px 22px;
    margin:6px;
    border:none;
    border-radius:20px;
    cursor:pointer;
}
.yes{background:#ff4d6d;color:white;}
.no{background:#ddd;}

/* ---------- fingerprint ---------- */
.fingerprint{
    width:120px;
    height:120px;
    border-radius:50%;
    border:4px solid #ff4d6d;
    display:flex;
    justify-content:center;
    align-items:center;
    margin:25px auto;
    font-size:55px;
    cursor:pointer;
    position:relative;
    overflow:hidden;
}
.scan{
    position:absolute;
    bottom:0;
    height:0%;
    width:100%;
    background:#ff4d6d55;
}

/* ---------- final ---------- */
.final{
    position:fixed;
    inset:0;
    background:#ff4d6d;
    color:white;
    display:flex;
    justify-content:center;
    align-items:center;
    text-align:center;
    font-size:24px;
    padding:30px;
    z-index:5;
}

/* ---------- confetti ---------- */
.confetti{
    position:fixed;
    width:10px;
    height:10px;
    top:-10px;
    animation:fall linear forwards;
    z-index:10;
}

@keyframes fall{
    to{
        transform:translateY(110vh) rotate(720deg);
    }
}
</style>
</head>

<body>

<!-- LOCK -->
<div class="card" id="lock">
    <h2 style="color:#ff4d6d;">Only for نُورَا ❤️</h2>
    <p>Touch & hold to unlock</p>

    <div class="fingerprint" id="finger">
        🔒
        <div class="scan" id="scan"></div>
    </div>
</div>

<!-- MAIN -->
<div class="card" id="main">
    <h1 style="color:#ff4d6d;">نُورَا ❤️</h1>
    <p id="message"></p>
    <div id="countdown" style="color:#ff4d6d;font-weight:bold;"></div>

    <button class="yes" onclick="yesClick()">Yes 💕</button>
    <button class="no" onmouseover="runAway(this)">No 😅</button>
</div>

<!-- FINAL -->
<div class="final" id="final">
    You just made me the happiest man alive ❤️<br><br>
    I choose you forever, نُورَا 💍<br><br>
    Happy Valentine’s Day<br><br>
    — Farouq
</div>

<script>

/* ---------- fingerprint unlock ---------- */
let hold;
const finger=document.getElementById("finger");
const scan=document.getElementById("scan");

finger.addEventListener("mousedown",start);
finger.addEventListener("touchstart",start);
finger.addEventListener("mouseup",stop);
finger.addEventListener("touchend",stop);

function start(){
    let p=0;
    hold=setInterval(()=>{
        p+=4;
        scan.style.height=p+"%";
        if(p>=100){
            clearInterval(hold);
            unlock();
        }
    },40);
}
function stop(){
    clearInterval(hold);
    scan.style.height="0%";
}

function unlock(){
    document.getElementById("lock").style.display="none";
    document.getElementById("main").style.display="block";
    type();
    startCountdown();
}

/* ---------- typing message ---------- */
const text="From the moment you came into my life, everything became beautiful. You are my happiness, my peace, my forever. Will you be my Valentine?";
let i=0;

function type(){
    if(i<text.length){
        document.getElementById("message").innerHTML+=text[i++];
        setTimeout(type,35);
    }
}

/* ---------- countdown ---------- */
function startCountdown(){
    const target=new Date("Feb 14, 2026 00:00:00").getTime();
    setInterval(()=>{
        const now=new Date().getTime();
        const diff=target-now;

        const d=Math.floor(diff/(1000*60*60*24));
        const h=Math.floor((diff%(1000*60*60*24))/(1000*60*60));
        const m=Math.floor((diff%(1000*60*60))/(1000*60));
        const s=Math.floor((diff%(1000*60))/1000);

        document.getElementById("countdown").innerHTML=
        `⏳ ${d}d ${h}h ${m}m ${s}s until Valentine’s Day`;
    },1000);
}

/* ---------- yes click + confetti ---------- */
function yesClick(){
    document.getElementById("final").style.display="flex";
    launchConfetti();
}

/* confetti */
function launchConfetti(){
    const colors=["#fff","#ffd700","#ff4d6d","#00e5ff","#7cff7c"];

    for(let i=0;i<120;i++){
        const c=document.createElement("div");
        c.className="confetti";
        c.style.left=Math.random()*100+"vw";
        c.style.background=colors[Math.floor(Math.random()*colors.length)];
        c.style.animationDuration=(2+Math.random()*3)+"s";
        document.body.appendChild(c);
        setTimeout(()=>c.remove(),5000);
    }
}

/* ---------- no runs ---------- */
function runAway(btn){
    btn.style.position="absolute";
    btn.style.top=Math.random()*80+"%";
    btn.style.left=Math.random()*80+"%";
}

/* ---------- hearts ---------- */
setInterval(()=>{
    const h=document.createElement("div");
    h.className="heart";
    h.innerHTML="❤";
    h.style.left=Math.random()*100+"vw";
    h.style.fontSize=(12+Math.random()*24)+"px";
    document.body.appendChild(h);
    setTimeout(()=>h.remove(),6000);
},300);

</script>

</body>
</html>
