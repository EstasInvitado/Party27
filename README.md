<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 
 <!-- Metadatos Open Graph -->
    <meta property="og:title" content="Invitación Real✨">
    <meta property="og:description" content="Click here">
    <meta property="og:image" content="https://png.pngtree.com/png-clipart/20250513/original/pngtree-png-vintage-blank-envelope-red-wax-seal-png-image_20951033.png">
    <meta property="og:url" content="https://EstasInvitado.github.io/Party27/">

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
.top-decoration {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    pointer-events: none; /* no bloquea clicks */
    z-index: 9999;

    /* opcional: que se vea más elegante */
    opacity: 0.9;
}

/* sobre */
.envelope {
    width: 360px;
    height: 260px;
    background: linear-gradient(145deg, #cfd8e6, #a9b7d1);
    border-radius: 12px;
    border: 5px solid #a9b7d1;
    position: relative;
    box-shadow: 0 30px 60px rgba(0,0,0,0.25);
    cursor: pointer;
    transition: 1s;
}


/* flap */
.flap {
    position: absolute;
    width: 100%;
    height: 55%;
    background: linear-gradient(160deg, #b7c5dc, #dcd6f7);
    clip-path: polygon(0 0, 100% 0, 50% 100%);
    transform-origin: top;
    transition: 1s;
    border-bottom: 1px solid rgba(212,175,55,0.4);
    
}

/* sello */
/* sello con imagen */
.seal {
    position: absolute;
    top: 95px;
    left: 50%;
    transform: translateX(-50%);
    width: 75px;
    height: 75px;
    object-fit: contain;
    cursor: pointer;
    z-index: 10;

    filter: drop-shadow(0 6px 10px rgba(0,0,0,0.4));
    transition: 0.7s ease;
}

/* efecto hover elegante */
.seal:hover {
    transform: translateX(-50%) scale(1.05);
}

/* animación de romper */
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
    background: linear-gradient(#f8f4ef, #efe6d8);
    border: 1px solid #d4af37;
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
    color: #7a8fb5;
    line-height: 1; /* 👈 reduce el espacio entre renglones */
}

p {
    font-size: 14px;
    color: #4a4a5a;
}

/* botón */
button {
    margin-top: 10px;
    padding: 10px 18px;
    border: none;
    background: linear-gradient(145deg, #d4af37, #b8962e);
    color: white;
    border-radius: 25px;
    cursor: pointer;
    font-weight: 500;
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
.bottom-flowers {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 200px;
    pointer-events: none;
    z-index: 1;
}

/* estilos base */
.flower-img {
    position: absolute;
    object-fit: contain;
    opacity: 0.95;
}

/* tamaños variados */
.flower-img.small {
    width: 80px;
}

.flower-img.medium {
    width: 120px;
    transform: rotate(80deg);
}

.flower-img.large {
    width: 160px;
}

/* efecto más natural */
.flower-img:nth-child(odd) {
    transform: rotate(-8deg);
}

.flower-img:nth-child(even) {
    transform: rotate(8deg);
}
/* flor 1 */
.flower-img:nth-child(1) {
    width: 140px;
    left: 5%;
    bottom: -30%;
    transform: rotate(-10deg);
}

/* flor 2 */
.flower-img:nth-child(2) {
    width: 180px;
    left: 20%;
    bottom: -30%;
    transform: rotate(15deg);
}

/* flor 3 (más grande al centro) */
.flower-img:nth-child(3) {
    width: 220px;
    left: 40%;
    bottom: -50%;
    transform: rotate(-5deg);
    z-index: 2;
}

/* flor 4 */
.flower-img:nth-child(4) {
    width: 130px;
    left: 65%;
    bottom: -30%;
    transform: rotate(20deg);
}

/* flor 5 */
.flower-img:nth-child(5) {
    width: 160px;
    left: 80%;
    bottom: -25%;
    transform: rotate(-15deg);
}
</style>
</head>

<body>
    <img src="https://github.com/EstasInvitado/Party27/blob/main/glicina%20corte.png?raw=true"
     class="top-decoration">

<canvas id="fireworks"></canvas>

<div class="envelope" id="env">

    <img src="https://github.com/EstasInvitado/Party27/blob/main/sello.png?raw=true"
     class="seal"
     id="seal"
     onclick="breakSeal(event)">
     
    <div class="flap"></div>

    <div class="card">
        <h1 class="glow">Estás cordialmente invitada</h1>
        <p>
            ✨ Picnic en la playa ✨ <br><br>
           Sabado 16 de mayo <br>
          Hora: 2:00 PM
        </p>

        <button onclick="alert('Asistencia confirmada 💌')">
            Confirmar asistencia
        </button>
    </div>
</div>
<div class="bottom-flowers">
    <img src="https://github.com/EstasInvitado/Party27/blob/main/hortensia.png?raw=true" class="flower-img small">
    <img src="https://github.com/EstasInvitado/Party27/blob/main/hortensia.png?raw=true" class="flower-img medium">
    <img src="https://github.com/EstasInvitado/Party27/blob/main/hortensia.png?raw=true" class="flower-img large">
    <img src="https://github.com/EstasInvitado/Party27/blob/main/hortensia.png?raw=true" class="flower-img small">
    <img src="https://github.com/EstasInvitado/Party27/blob/main/hortensia.png?raw=true" class="flower-img medium">
</div>
<script>

// ===== MUSICA Vals Elegante tipo Bridgerton =====
// ===== MUSICA estilo pop electrónico (tipo 360) =====
// ===== MUSICA estilo Mozart (clásico elegante) =====
// ===== MUSICA estilo Vivaldi (barroco / violines rápidos) =====
let audioCtx;
let i = 0;

// 🎻 melodía inspirada en estilo barroco (tipo Las Cuatro Estaciones)
const melody = [
    {note: 523.25, dur: 0.3}, // C
    {note: 659.25, dur: 0.3}, // E
    {note: 783.99, dur: 0.3}, // G
    {note: 1046.50, dur: 0.5}, // C alto (impacto)

    {note: 783.99, dur: 0.3}, // G
    {note: 880.00, dur: 0.3}, // A
    {note: 783.99, dur: 0.3}, // G
    {note: 659.25, dur: 0.5}, // E

    {note: 523.25, dur: 0.3}, // C
    {note: 659.25, dur: 0.3}, // E
    {note: 783.99, dur: 0.3}, // G
    {note: 1046.50, dur: 0.8}, // C final (gran anuncio)
];

// 🎻 reproducción estilo violín rápido
function playMelody(){
    if(!audioCtx) return;

    const noteData = melody[i % melody.length];

    let osc = audioCtx.createOscillator();
    let gain = audioCtx.createGain();

    osc.frequency.value = noteData.note;
    osc.type = "triangle"; // 🎻 más parecido a cuerdas

    // ✨ ataque tipo arco de violín
    gain.gain.setValueAtTime(0, audioCtx.currentTime);
    gain.gain.linearRampToValueAtTime(0.1, audioCtx.currentTime + 0.02);
    gain.gain.linearRampToValueAtTime(0, audioCtx.currentTime + noteData.dur);
    gain.gain.value = 0.25;
    osc.connect(gain);
    gain.connect(audioCtx.destination);

    osc.start();
    osc.stop(audioCtx.currentTime + noteData.dur);

    i++;

    window.musicTimeout = setTimeout(playMelody, noteData.dur * 1000);
}

// ▶️ iniciar música
function playMusic(){
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();

    if (audioCtx.state === "suspended") {
        audioCtx.resume();
    }

    playMelody();
}

// ⏹️ detener música
function stopMusic(){
    if(window.musicTimeout){
        clearTimeout(window.musicTimeout);
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
    ctx.fillStyle = "rgba(255,255,255,0.15)";
    ctx.fillRect(0,0,canvas.width,canvas.height);

    particlesFW.forEach(p=>{
        p.x += p.vx;
        p.y += p.vy;
        p.alpha -= 0.01;

          ctx.fillStyle = `rgba(255,215,0,${p.alpha})`;

    ctx.beginPath();
    ctx.arc(p.x, p.y, 5, 0, Math.PI * 2);
    ctx.fill();
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
