<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Invitación Real</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Playfair+Display:wght@400;600&display=swap" rel="stylesheet">

<style>
body {
    margin: 0;
    height: 100vh;
    overflow: hidden;
    background: radial-gradient(circle at top, #fff0f6, #e7d3e8, #b89ac9);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Playfair Display', serif;
}

/* canvas fireworks */
canvas {
    position: absolute;
    top: 0;
    left: 0;
}

/* flores */
.flower {
    position: absolute;
    width: 14px;
    height: 14px;
    background: pink;
    border-radius: 50%;
    opacity: 0.6;
    animation: float 12s linear infinite;
}

@keyframes float {
    0% {transform: translateY(110vh) scale(0.4);}
    100% {transform: translateY(-10vh) scale(1.2);}
}

/* sobre */
.envelope {
    width: 360px;
    height: 260px;
    background: #f7e9ee;
    border-radius: 12px;
    border: 2px solid #c9a3b0;
    position: relative;
    box-shadow: 0 30px 60px rgba(0,0,0,0.3);
    cursor: pointer;
    transition: 1s;
}

/* flap */
.flap {
    position: absolute;
    width: 100%;
    height: 55%;
    background: #e8cfd8;
    clip-path: polygon(0 0, 100% 0, 50% 100%);
    transform-origin: top;
    transition: 1s;
}

/* sello */
.seal {
    position: absolute;
    top: 95px;
    left: 50%;
    transform: translateX(-50%);
    width: 65px;
    height: 65px;
    background: radial-gradient(circle at 30% 30%, #ff4d4d, #6b0000);
    border-radius: 50%;
    box-shadow: inset 0 3px 8px rgba(0,0,0,0.4),
                0 10px 20px rgba(0,0,0,0.3);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 22px;
    color: gold;
    z-index: 10;
    transition: 0.6s;
}

.seal::before {
    content: "✿";
}

.seal.broken {
    transform: translateX(-50%) scale(0.2) rotate(40deg);
    opacity: 0;
}

/* carta pergamino */
.card {
    position: absolute;
    width: 92%;
    height: 92%;
    top: 4%;
    left: 4%;
    background: linear-gradient(#fffaf0, #f3e3c3);
    border: 1px solid #d8c3a5;
    opacity: 0;
    transform: translateY(40px) scale(0.9);
    transition: 1.2s;
    text-align: center;
    padding: 20px;
    box-sizing: border-box;
}

/* apertura */
.envelope.open .flap {
    transform: rotateX(180deg);
}

.envelope.open .card {
    opacity: 1;
    transform: translateY(-10px) scale(1);
}

/* textos */
h1 {
    font-family: 'Great Vibes', cursive;
    font-size: 38px;
    color: #b76e79;
}

p {
    font-size: 14px;
    color: #5c4a50;
}

/* botón */
button {
    margin-top: 10px;
    padding: 8px 15px;
    border: none;
    background: #c08aa1;
    color: white;
    border-radius: 20px;
    cursor: pointer;
}

/* glow */
.glow {
    animation: glow 2s infinite alternate;
}

@keyframes glow {
    from {text-shadow: 0 0 5px #fff;}
    to {text-shadow: 0 0 25px #ffd6e0;}
}

/* partículas */
.particle {
    position: absolute;
    width: 6px;
    height: 6px;
    background: gold;
    border-radius: 50%;
    animation: rise 4s linear forwards;
}

@keyframes rise {
    from {transform: translateY(0); opacity: 1;}
    to {transform: translateY(-200px); opacity: 0;}
}
</style>
</head>

<body>

<canvas id="fireworks"></canvas>

<div class="envelope" id="env">

    <div class="seal" id="seal" onclick="breakSeal(event)"></div>
    <div class="flap"></div>

    <div class="card">
        <h1 class="glow">Estás cordialmente invitada</h1>
        <p>
            A una velada digna de la alta sociedad.<br><br>
            ✨ Un cumpleaños de ensueño ✨<br><br>
            Vestimenta: elegancia romántica<br>
            Hora: 7:00 PM
        </p>

        <button onclick="alert('Asistencia confirmada 💌')">
            Confirmar asistencia
        </button>
    </div>
</div>

<script>

// ===== MUSICA =====
let audioCtx;
function playMusic(){
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();

    const notes = [261.63, 329.63, 392.00, 523.25];
    let i = 0;

    window.musicInterval = setInterval(() => {
        let osc = audioCtx.createOscillator();
        let gain = audioCtx.createGain();

        osc.frequency.value = notes[i % notes.length];
        osc.type = "sine";

        gain.gain.value = 0.03;

        osc.connect(gain);
        gain.connect(audioCtx.destination);

        osc.start();
        osc.stop(audioCtx.currentTime + 0.6);

        i++;
    }, 700);
}


// detener música
function stopMusic(){
    if(window.musicInterval){
        clearInterval(window.musicInterval);
    }
    if(audioCtx){
        audioCtx.close();
    }
}

// ===== ABRIR =====
function breakSeal(e){
    e.stopPropagation();

    const seal = document.getElementById("seal");
    const env = document.getElementById("env");

    seal.classList.add("broken");

    setTimeout(() => {
        env.classList.add("open");
        startFireworks();
        playMusic();
        spawnParticles();
    }, 600);
}
/* ===== FUEGOS ARTIFICIALES ===== */
const canvas = document.getElementById("fireworks");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particlesFW = [];

function startFireworks(){
    for(let i=0;i<120;i++){
        particlesFW.push({
            x: canvas.width/2,
            y: canvas.height/2,
            vx: Math.random()*6-3,
            vy: Math.random()*6-3,
            alpha: 1
        });
    }
}
function animateFW(){
    ctx.fillStyle = "rgba(0,0,0,0.15)";
    ctx.fillRect(0,0,canvas.width,canvas.height);

    particlesFW.forEach(p=>{
        p.x += p.vx;
        p.y += p.vy;
        p.alpha -= 0.01;

        ctx.fillStyle = `rgba(255,215,0,${p.alpha})`;
        ctx.fillRect(p.x,p.y,3,3);
    });

    particlesFW = particlesFW.filter(p=>p.alpha>0);
    requestAnimationFrame(animateFW);
}
animateFW();

// ===== CERRAR =====
document.body.addEventListener("click", function(e){

    const env = document.getElementById("env");
    const seal = document.getElementById("seal");

    // evitar cerrar si haces click en el sello
    if(e.target.id === "seal") return;

    if(env.classList.contains("open")){
        env.classList.remove("open");

        // restaurar sello
        setTimeout(() => {
            seal.classList.remove("broken");
        }, 500);

        // limpiar efectos
        particlesFW = [];
        stopMusic();

        // eliminar partículas doradas
        document.querySelectorAll(".particle").forEach(p => p.remove());
    }
});

</script>

</body>
</html>
