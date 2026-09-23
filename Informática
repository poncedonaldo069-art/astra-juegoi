<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Astra — Simulador</title>
<style>
*{box-sizing:border-box}
:root{--ink:#24283d;--purple:#7668e8;--cyan:#67cdd0;--pink:#ed91bc;--green:#65c98b}
body{margin:0;font-family:system-ui,-apple-system,Segoe UI,sans-serif;background:linear-gradient(135deg,#f5f6ff,#eaf9fa);color:var(--ink)}
header{text-align:center;padding:25px 15px 15px}
h1{margin:0;font-size:clamp(28px,6vw,44px)}
header p{margin:7px auto;color:#6d7590;max-width:620px}
.flow{display:flex;justify-content:center;align-items:center;gap:8px;flex-wrap:wrap;margin:10px auto 18px;font-weight:800}
.flow span{background:white;padding:9px 12px;border-radius:14px;box-shadow:0 5px 15px #38405c15}
.flow i{font-style:normal;color:var(--purple);font-size:20px}
.app{width:min(1000px,94%);margin:auto}
.main{display:grid;grid-template-columns:250px 1fr;gap:18px}
.panel,.scene,.bottom{background:#fff;border:1px solid #e4e6f2;border-radius:24px;box-shadow:0 14px 35px #3d426d18}
.panel{padding:20px;text-align:center}
.remote{background:#252a3d;border-radius:22px;padding:17px;color:white}
.remote-title{font-weight:900;margin-bottom:15px}
button{width:100%;border:0;border-radius:14px;padding:15px;margin:6px 0;font-size:15px;font-weight:900;cursor:pointer;transition:.15s;box-shadow:0 5px 12px #3332}
button:hover{transform:translateY(-2px)}
#advance{background:#6f63df;color:#fff}#deliver{background:#ef92ba;color:#fff}
.status{margin-top:12px;padding:10px;border-radius:12px;background:#f5f6fc;color:#69718a;font-size:12px}
.scene{padding:14px;overflow:hidden}
.sceneTop{height:45px;display:flex;align-items:center;justify-content:space-between;padding:0 10px;font-weight:800;font-size:13px}
#message{opacity:0;transform:translateY(-5px);background:var(--green);color:white;padding:7px 12px;border-radius:99px;transition:.3s}
#message.show{opacity:1;transform:none}
.arena{height:390px;position:relative;overflow:hidden;border-radius:18px;background:linear-gradient(#dff6fa 0 58%,#d7ddcb 58%)}
.floor{position:absolute;left:0;right:0;bottom:0;height:42%;background:repeating-linear-gradient(90deg,#d3d9c9 0 50px,#cbd2c1 51px 52px)}
.lane{position:absolute;left:0;right:0;top:75%;border-top:3px dashed #aeb8a4}
.destination{position:absolute;right:20px;bottom:27%;width:105px;height:105px;border:3px dashed #e1b957;border-radius:18px;background:#fff5d8;display:grid;place-items:center;text-align:center;font-size:12px;font-weight:900;color:#80671e}
.signal{position:absolute;left:10%;top:20%;font-size:20px;opacity:0;z-index:5}
.signal.run{animation:signal 1.7s ease-in-out forwards}
@keyframes signal{0%{left:10%;opacity:0}12%{opacity:1}45%{left:46%;opacity:1}75%{left:70%;opacity:1}100%{left:84%;opacity:0}}
.robot{position:absolute;left:10%;bottom:24px;width:115px;height:190px;z-index:4;transition:left .1s linear}
.body{position:absolute;left:28px;bottom:20px;width:60px;height:105px;border-radius:18px;background:linear-gradient(145deg,#e3e7f1,#adb7c9);border:3px solid #78849b}
.head{position:absolute;left:32px;top:5px;width:52px;height:53px;border-radius:15px;background:#3f475b;border:3px solid #727e95;padding:8px}
.face{width:100%;height:100%;border-radius:9px;background:#9ce4dc;display:flex;align-items:center;justify-content:center;gap:6px}
.eye{width:6px;height:11px;border-radius:50%;background:#264d55}.smile{font-size:14px}
.tray{position:absolute;left:4px;top:63px;width:107px;height:22px;border-radius:7px;background:#f8f9fc;border:3px solid #707b90;z-index:2}
.food{position:absolute;width:40px;height:24px;left:30px;top:-23px;border-radius:50%;background:#e88a72;border:3px solid #ba604e}
.food:after{content:"🍱";font-size:17px;position:absolute;left:8px;top:-2px}
.wheel{position:absolute;bottom:0;width:28px;height:43px;border-radius:13px;background:#252a3a;border:4px solid #59647a}
.w1{left:21px}.w2{right:21px}
.wheel:after{content:"";position:absolute;inset:4px;border:3px dashed #939caf;border-radius:50%}
.moving .wheel:after{animation:spin .25s linear infinite}
.moving{animation:bob .35s infinite alternate}
@keyframes spin{to{transform:rotate(360deg)}}@keyframes bob{to{bottom:28px}}
.chip{position:absolute;left:46%;top:16%;font-size:34px;opacity:.35;transition:.2s}
.chip.active{opacity:1;animation:pulse .5s infinite alternate}
@keyframes pulse{to{transform:scale(1.15)}}
.motors{position:absolute;right:13%;top:18%;font-size:28px;opacity:.35}
.motors.active{opacity:1;animation:spin .4s linear infinite}
.caption{position:absolute;top:7%;left:50%;transform:translateX(-50%);background:#ffffffd9;padding:8px 13px;border-radius:12px;font-size:12px;font-weight:900;white-space:nowrap}
.bottom{margin:18px 0 25px;padding:18px;text-align:center}
.bottom h2{margin:0 0 8px;font-size:18px}.bottom p{margin:0;color:#69718a;font-size:14px}
@media(max-width:720px){.main{grid-template-columns:1fr}.panel{order:1}.scene{order:2}.arena{height:330px}}
</style>
</head>
<body>
<header>
  <h1>🤖 Astra</h1>
  <p>Simulador del recorrido de una orden hasta el movimiento del robot.</p>
  <div class="flow">
    <span>🎮 Persona</span><i>→</i><span>🧠 Microcontrolador</span><i>→</i><span>⚙️ Motores</span><i>→</i><span>🤖 Astra</span>
  </div>
</header>

<main class="app">
  <div class="main">
    <section class="panel">
      <div class="remote">
        <div class="remote-title">🎮 CONTROL</div>
        <button id="advance">▶️ Avanzar</button>
        <button id="deliver">🍱 Entregar pedido</button>
      </div>
      <div class="status" id="status">Presiona un botón para darle una orden a Astra.</div>
    </section>

    <section class="scene">
      <div class="sceneTop"><span id="stage">Esperando una orden...</span><span id="message">🎉 ¡Pedido entregado!</span></div>
      <div class="arena" id="arena">
        <div class="caption">Entrada → Procesamiento → Actuador</div>
        <div class="chip" id="chip">🧠</div>
        <div class="motors" id="motors">⚙️</div>
        <div class="signal" id="signal">✨</div>
        <div class="destination">📍<br>ZONA DE<br>ENTREGA</div>
        <div class="floor"></div><div class="lane"></div>
        <div class="robot" id="robot">
          <div class="head"><div class="face"><span class="eye"></span><span class="smile">⌣</span><span class="eye"></span></div></div>
          <div class="tray"><div class="food"></div></div>
          <div class="body"></div>
          <div class="wheel w1"></div><div class="wheel w2"></div>
        </div>
      </div>
    </section>
  </div>

  <section class="bottom">
    <h2>“La persona decide. Astra ejecuta.”</h2>
    <p>La persona da la orden → el microcontrolador la procesa → los motores hacen que Astra se mueva.</p>
  </section>
</main>

<script>
const robot=document.getElementById('robot'), signal=document.getElementById('signal');
const chip=document.getElementById('chip'), motors=document.getElementById('motors');
const status=document.getElementById('status'), stage=document.getElementById('stage');
const message=document.getElementById('message');
let x=10, moving=false, animation=null, delivery=false;

function stopRobot(){
  moving=false; robot.classList.remove('moving'); motors.classList.remove('active');
  cancelAnimationFrame(animation);
}
function animateForward(target=70,done){
  moving=true; robot.classList.add('moving'); motors.classList.add('active');
  const step=()=>{
    if(!moving)return;
    x+=.45; robot.style.left=x+'%';
    if(x>=target){stopRobot(); if(done)done();return}
    animation=requestAnimationFrame(step);
  };
  step();
}
function signalAnimation(){
  signal.classList.remove('run'); void signal.offsetWidth; signal.classList.add('run');
}
function processOrder(type){
  stopRobot(); message.classList.remove('show'); signalAnimation();
  chip.classList.add('active');
  stage.textContent='🧠 Procesando la orden...';
  status.textContent='La orden está siendo procesada.';
  setTimeout(()=>{
    chip.classList.remove('active'); motors.classList.add('active');
    stage.textContent='⚙️ Señal enviada a los motores...';
    setTimeout(()=>{
      stage.textContent='🤖 Astra está avanzando...';
      if(type==='deliver'){
        delivery=true;
        animateForward(74,()=>{
          stage.textContent='📍 Astra llegó a la zona de entrega.';
          message.classList.add('show');
          status.textContent='¡Pedido entregado!';
        });
      }else{
        animateForward(48,()=>{
          stage.textContent='🤖 Astra se detuvo.';
          status.textContent='Astra ejecutó la orden.';
        });
      }
    },550);
  },900);
}
document.getElementById('advance').onclick=()=>processOrder('advance');
document.getElementById('deliver').onclick=()=>processOrder('deliver');
</script>
</body>
</html>
