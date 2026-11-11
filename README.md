[index.html](https://github.com/user-attachments/files/34706726/index.html)
<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>El desafío del plato saludable</title>
<style>
:root{--ink:#263447;--green:#287a54;--mint:#e9f7ef;--yellow:#fff3c4;--pink:#ffe8e8;--blue:#e8f3ff;--purple:#f0eaff}
*{box-sizing:border-box}
body{margin:0;font-family:system-ui,-apple-system,"Segoe UI",sans-serif;color:var(--ink);background:linear-gradient(135deg,#f3fbf5,#fff8e7);min-height:100vh}
header{text-align:center;padding:25px 16px 12px}
h1{margin:0;font-size:clamp(1.7rem,4vw,2.6rem);color:#216747}
header p{margin:8px auto 0;max-width:700px;font-size:1.05rem}
main{max-width:1050px;margin:auto;padding:14px}
.panel{background:white;border-radius:22px;padding:18px;box-shadow:0 5px 20px #294a3012;margin-bottom:16px}
h2{font-size:1.25rem;margin:0 0 12px}
.instruction{background:var(--yellow);border-radius:14px;padding:12px 15px;line-height:1.45}
.layout{display:grid;grid-template-columns:1fr 1fr;gap:16px;align-items:start}
.foods{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:9px}
.food{border:2px solid #e6ebee;background:#fff;border-radius:15px;padding:10px 5px;cursor:pointer;text-align:center;min-height:95px;color:var(--ink);font:inherit;transition:.15s}
.food:hover{transform:translateY(-2px);border-color:#7ebc98}
.food:focus-visible,.action:focus-visible{outline:3px solid #f2b632;outline-offset:2px}
.food.selected{border-color:var(--green);background:var(--mint);box-shadow:inset 0 0 0 1px var(--green)}
.food .emoji{display:block;font-size:2rem;margin-bottom:3px}
.food small{display:block;font-size:.82rem}
.plate-wrap{text-align:center}
.plate{width:min(100%,340px);aspect-ratio:1;border-radius:50%;margin:10px auto 12px;border:12px solid #e6e9ed;background:conic-gradient(#dff1d9 0 25%,#fff0c9 25% 50%,#fbe0dc 50% 75%,#e3efff 75% 100%);box-shadow:inset 0 0 0 7px white,0 4px 10px #00000012;display:flex;flex-wrap:wrap;align-content:center;justify-content:center;gap:8px;padding:24px}
.plate .empty{font-weight:700;color:#54715e;max-width:190px;line-height:1.35}
.piece{font-size:2.25rem;background:#ffffffd9;border-radius:13px;padding:4px;min-width:48px}
.counter{font-weight:700;color:#46604f}
.actions{display:flex;gap:10px;flex-wrap:wrap;justify-content:center;margin-top:12px}
.action{border:0;border-radius:13px;padding:12px 18px;font-weight:750;font-size:1rem;cursor:pointer}
.primary{background:#287a54;color:white}.secondary{background:#edf1f4;color:#334155}
.feedback{min-height:28px;text-align:center;font-weight:700;margin-top:12px}
.namebox{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
input{flex:1;min-width:190px;border:2px solid #dce4e8;border-radius:12px;padding:12px;font:inherit}
.result{display:none;background:var(--mint);border-radius:16px;padding:15px;margin-top:12px}
.result.show{display:block}
.tags{display:flex;gap:7px;flex-wrap:wrap;justify-content:center;margin:8px 0}
.tag{background:white;border-radius:30px;padding:5px 10px;font-size:.9rem}
footer{text-align:center;color:#64748b;font-size:.85rem;padding:0 12px 25px}
@media(max-width:760px){.layout{grid-template-columns:1fr}.foods{grid-template-columns:repeat(3,minmax(0,1fr))}.plate{width:min(82vw,320px)}}
</style>
</head>
<body>
<header>
  <h1>🥗 ¡El desafío del plato saludable!</h1>
  <p>¡Conviértete en chef! Elige alimentos y crea una comida variada para tu plato.</p>
</header>
<main>
  <section class="panel">
    <div class="instruction"><strong>Tu misión:</strong> toca los alimentos que quieras añadir al plato. Puedes elegir varios y cambiar tu combinación hasta que estés satisfecho/a. Después, ponle un nombre a tu creación.</div>
  </section>
  <div class="layout">
    <section class="panel">
      <h2>🧺 Elige tus alimentos</h2>
      <p style="margin-top:-5px;color:#64748b">Pulsa una tarjeta para añadirla o quitarla.</p>
      <div class="foods" id="foods"></div>
    </section>
    <section class="panel plate-wrap">
      <h2>🍽️ Tu plato creativo</h2>
      <div class="plate" id="plate" aria-live="polite"><div class="empty">¡Tu plato está vacío!<br>Elige alimentos para empezar.</div></div>
      <div class="counter" id="counter">0 alimentos elegidos</div>
      <div class="namebox">
        <input id="dishName" maxlength="45" placeholder="Pon un nombre a tu plato…" aria-label="Nombre de tu plato">
      </div>
      <div class="actions">
        <button class="action primary" id="check">¡Comprobar mi creación!</button>
        <button class="action secondary" id="reset">Empezar de nuevo</button>
      </div>
      <div class="feedback" id="feedback" role="status"></div>
      <div class="result" id="result"></div>
    </section>
  </div>
  <section class="panel">
    <h2>💡 Piensa como un chef</h2>
    <p>Cuando termines, cuéntale a alguien:</p>
    <ul>
      <li>¿Qué nombre has puesto a tu plato?</li>
      <li>¿Qué alimentos has combinado?</li>
      <li>¿Por qué has elegido esa combinación?</li>
      <li>¿Qué otro alimento podrías añadir o cambiar?</li>
    </ul>
  </section>
</main>
<footer>Actividad educativa · Alimentación saludable · 2.º de Primaria</footer>
<script>
const items=[
 {n:"Tomate",e:"🍅",g:"verduras y frutas"},{n:"Zanahoria",e:"🥕",g:"verduras y frutas"},{n:"Manzana",e:"🍎",g:"verduras y frutas"},
 {n:"Plátano",e:"🍌",g:"verduras y frutas"},{n:"Brócoli",e:"🥦",g:"verduras y frutas"},{n:"Fresas",e:"🍓",g:"verduras y frutas"},
 {n:"Pan integral",e:"🍞",g:"cereales"},{n:"Arroz",e:"🍚",g:"cereales"},{n:"Pasta",e:"🍝",g:"cereales"},
 {n:"Huevo",e:"🥚",g:"proteínas"},{n:"Pescado",e:"🐟",g:"proteínas"},{n:"Lentejas",e:"🥣",g:"proteínas"},
 {n:"Pollo",e:"🍗",g:"proteínas"},{n:"Yogur natural",e:"🥛",g:"lácteos"},{n:"Agua",e:"💧",g:"bebida"}
];
let chosen=[];
const foods=document.getElementById('foods'),plate=document.getElementById('plate');
function render(){
 foods.innerHTML='';
 items.forEach((it,i)=>{
  const b=document.createElement('button');b.className='food'+(chosen.includes(i)?' selected':'');
  b.setAttribute('aria-pressed',chosen.includes(i));
  b.innerHTML=`<span class="emoji">${it.e}</span><small>${it.n}</small>`;
  b.onclick=()=>{chosen=chosen.includes(i)?chosen.filter(x=>x!==i):[...chosen,i];render();document.getElementById('feedback').textContent='';document.getElementById('result').classList.remove('show')};
  foods.appendChild(b);
 });
 plate.innerHTML=chosen.length?chosen.map(i=>`<span class="piece" title="${items[i].n}">${items[i].e}</span>`).join(''):'<div class="empty">¡Tu plato está vacío!<br>Elige alimentos para empezar.</div>';
 document.getElementById('counter').textContent=`${chosen.length} ${chosen.length===1?'alimento elegido':'alimentos elegidos'}`;
}
document.getElementById('check').onclick=()=>{
 const feedback=document.getElementById('feedback'),result=document.getElementById('result');
 const name=document.getElementById('dishName').value.trim();
 if(chosen.length<3){feedback.textContent='¡Añade al menos 3 alimentos para crear tu plato!';result.classList.remove('show');return}
 if(!name){feedback.textContent='¡Tu creación necesita un nombre! Escríbelo arriba.';result.classList.remove('show');return}
 const groups=[...new Set(chosen.map(i=>items[i].g))];
 feedback.textContent='🎉 ¡Buen trabajo, chef! Has creado tu propia combinación.';
 result.innerHTML=`<strong>🌟 ${name}</strong><p>Has combinado ${chosen.length} alimentos de ${groups.length} grupos diferentes:</p><div class="tags">${groups.map(g=>`<span class="tag">${g}</span>`).join('')}</div><p>Ahora explica por qué has elegido estos alimentos y qué cambiarías para crear otra versión.</p>`;
 result.classList.add('show');
};
document.getElementById('reset').onclick=()=>{chosen=[];document.getElementById('dishName').value='';document.getElementById('feedback').textContent='';document.getElementById('result').classList.remove('show');render()};
render();
</script>
</body>
</html>
