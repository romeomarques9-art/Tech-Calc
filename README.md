# Tech-Calc
My first project coding a calculator that calculates arithmetic and trigonometric functions. 
 http://127.0.0.1:5500/index.html  
 <img width="1863" height="842" alt="image" src="https://github.com/user-attachments/assets/148dad82-424e-41b8-a6d5-090372839e65" />
@romeomarques9-art 
Code 
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>TechCalc — Calculator & Technical Solver</title>
  <style>
    :root { --bg:#07111f; --surface:#101d30; --surface-2:#16263d; --line:#29415f; --text:#eef5ff; --muted:#9fb2cc; --blue:#3c9cff; --cyan:#54e0d0; --warn:#ffb545; }
    * { box-sizing:border-box; }
    body { margin:0; min-height:100vh; font-family:Inter,ui-sans-serif,system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif; color:var(--text); background:radial-gradient(circle at 12% 8%,#17335b 0,transparent 30rem),radial-gradient(circle at 90% 100%,#0a5a5c 0,transparent 28rem),var(--bg); }
    .app { width:min(1100px,calc(100% - 32px)); margin:0 auto; padding:34px 0 46px; }
    header { display:flex; justify-content:space-between; align-items:end; gap:20px; margin-bottom:25px; }
    h1 { font-size:clamp(1.7rem,4vw,2.55rem); margin:0; letter-spacing:-.055em; }
    .tagline { color:var(--muted); margin:8px 0 0; }
    .badge { color:#07111f; background:var(--cyan); padding:7px 11px; border-radius:999px; font-size:.76rem; font-weight:800; letter-spacing:.04em; white-space:nowrap; }
    .layout { display:grid; grid-template-columns:minmax(290px,.9fr) minmax(390px,1.45fr); gap:20px; align-items:start; }
    .card { background:linear-gradient(145deg,rgba(22,38,61,.98),rgba(12,25,43,.98)); border:1px solid var(--line); box-shadow:0 20px 60px #0004; border-radius:20px; overflow:hidden; }
    .calculator { padding:18px; }
    .display { background:#081321; border:1px solid #2e496a; border-radius:13px; padding:14px 16px; margin-bottom:14px; text-align:right; overflow:hidden; }
    #expression { min-height:22px; color:var(--muted); font-size:.84rem; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
    #result { font-size:2.35rem; font-weight:650; letter-spacing:-.05em; line-height:1.25; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
    .keys { display:grid; grid-template-columns:repeat(4,1fr); gap:9px; }
    button { border:0; cursor:pointer; color:var(--text); font:inherit; font-weight:650; border-radius:11px; min-height:53px; background:#20334d; transition:transform .12s,background .12s,filter .12s; }
    button:hover { transform:translateY(-1px); background:#2a4160; } button:active { transform:translateY(1px); }
    .op { color:#7ec4ff; background:#183653; }.utility { color:var(--warn); background:#283546; }.equals { background:var(--blue); color:white; }.equals:hover { background:#5aaaff; }
    .solver-head { padding:19px 20px 15px; border-bottom:1px solid var(--line); }
    h2 { margin:0; font-size:1.12rem; }.solver-head p { margin:5px 0 0; font-size:.88rem; color:var(--muted); }
    .tabs { display:flex; gap:7px; padding:14px 15px 0; overflow-x:auto; }
    .tabs button { min-height:auto; padding:8px 11px; font-size:.79rem; white-space:nowrap; color:var(--muted); background:transparent; border:1px solid transparent; }
    .tabs button.active { color:var(--text); background:#203a59; border-color:#38618d; }
    .solver { padding:17px 20px 20px; }.tool { display:none; }.tool.active { display:block; }
    .tool h3 { font-size:1rem; margin:0 0 5px; }.formula { color:var(--cyan); font-size:.82rem; margin:0 0 16px; }
    .fields { display:grid; grid-template-columns:repeat(2,minmax(0,1fr)); gap:12px; }
    label { display:block; color:var(--muted); font-size:.8rem; font-weight:650; } input,select { width:100%; margin-top:6px; border-radius:9px; border:1px solid #345271; color:var(--text); background:#091625; padding:10px; font:inherit; outline:none; } input:focus,select:focus { border-color:var(--blue); box-shadow:0 0 0 3px #3c9cff25; }
    select { cursor:pointer; } .solve { width:100%; margin-top:15px; min-height:45px; background:#1c806f; }.solve:hover { background:#259887; }
    .answer { margin-top:14px; min-height:59px; padding:11px 13px; border:1px solid #2a5770; background:#0c2030; border-radius:10px; }.answer small { display:block; color:var(--muted); margin-bottom:3px; }.answer strong { font-size:1.1rem; color:var(--cyan); }
    .note { margin:15px 20px 0; color:var(--muted); font-size:.76rem; line-height:1.45; }
    @media(max-width:760px){ .app{width:min(100% - 22px,560px);padding-top:20px}.layout{grid-template-columns:1fr}header{align-items:start;flex-direction:column}.badge{display:none}.calculator{padding:13px}.keys button{min-height:48px}.fields{grid-template-columns:1fr} }
  </style>
</head>
<body>
  <main class="app">
    <header><div><h1>TechCalc</h1><p class="tagline">Everyday arithmetic and practical technical calculations.</p></div><span class="badge">ENGINEERING TOOLKIT</span></header>
    <div class="layout">
      <section class="card calculator" aria-label="Arithmetic calculator">
        <div class="display"><div id="expression">0</div><div id="result" aria-live="polite">0</div></div>
        <div class="keys" id="keys">
          <button class="utility" data-action="clear">AC</button><button class="utility" data-action="back">⌫</button><button class="utility" data-value="(">(</button><button class="op" data-value="/">÷</button>
          <button data-value="7">7</button><button data-value="8">8</button><button data-value="9">9</button><button class="op" data-value="*">×</button>
          <button data-value="4">4</button><button data-value="5">5</button><button data-value="6">6</button><button class="op" data-value="-">−</button>
          <button data-value="1">1</button><button data-value="2">2</button><button data-value="3">3</button><button class="op" data-value="+">+</button>
          <button data-value="0">0</button><button data-value=".">.</button><button data-value="%">%</button><button class="equals" data-action="equals">=</button>
        </div>
      </section>
      <section class="card">
        <div class="solver-head"><h2>Technical task solver</h2><p>Select a formula, provide known values, and calculate the missing result.</p></div>
        <nav class="tabs" aria-label="Technical calculation types">
          <button class="active" data-tool="ohm">Ohm’s law</button><button data-tool="power">Electrical power</button><button data-tool="motion">Motion</button><button data-tool="geometry">Geometry</button><button data-tool="units">Units</button>
        </nav>
        <div class="solver">
          <div class="tool active" id="ohm"><h3>Ohm’s law</h3><p class="formula">V = I × R</p><div class="fields"><label>Current (I), amperes<input id="ohmI" type="number" step="any" placeholder="e.g. 2"></label><label>Resistance (R), ohms<input id="ohmR" type="number" step="any" placeholder="e.g. 12"></label></div><button class="solve" data-solve="ohm">Calculate voltage</button><div class="answer" id="ohmAnswer"><small>Voltage (V)</small><strong>Enter values above</strong></div></div>
          <div class="tool" id="power"><h3>Electrical power</h3><p class="formula">P = V × I</p><div class="fields"><label>Voltage (V), volts<input id="powerV" type="number" step="any" placeholder="e.g. 120"></label><label>Current (I), amperes<input id="powerI" type="number" step="any" placeholder="e.g. 1.5"></label></div><button class="solve" data-solve="power">Calculate power</button><div class="answer" id="powerAnswer"><small>Power (P)</small><strong>Enter values above</strong></div></div>
          <div class="tool" id="motion"><h3>Speed, distance & time</h3><p class="formula">Distance = speed × time</p><div class="fields"><label>Speed (km/h)<input id="motionSpeed" type="number" step="any" placeholder="e.g. 65"></label><label>Time (hours)<input id="motionTime" type="number" step="any" placeholder="e.g. 2.5"></label></div><button class="solve" data-solve="motion">Calculate distance</button><div class="answer" id="motionAnswer"><small>Distance</small><strong>Enter values above</strong></div></div>
          <div class="tool" id="geometry"><h3>Circle area</h3><p class="formula">A = πr²</p><div class="fields"><label>Radius (r), units<input id="radius" type="number" step="any" placeholder="e.g. 7"></label></div><button class="solve" data-solve="geometry">Calculate area</button><div class="answer" id="geometryAnswer"><small>Area</small><strong>Enter a radius above</strong></div></div>
          <div class="tool" id="units"><h3>Unit converter</h3><p class="formula">Quick metric ↔ imperial conversion</p><div class="fields"><label>Value<input id="unitValue" type="number" step="any" placeholder="e.g. 10"></label><label>Conversion<select id="conversion"><option value="km-mi">Kilometers → miles</option><option value="mi-km">Miles → kilometers</option><option value="c-f">Celsius → Fahrenheit</option><option value="f-c">Fahrenheit → Celsius</option><option value="kg-lb">Kilograms → pounds</option><option value="lb-kg">Pounds → kilograms</option></select></label></div><button class="solve" data-solve="units">Convert</button><div class="answer" id="unitsAnswer"><small>Converted value</small><strong>Enter a value above</strong></div></div>
        </div>
        <p class="note">Tip: use the arithmetic calculator for expressions with parentheses and percentages. Keyboard input is supported.</p>
      </section>
    </div>
  </main>
  <script>
    let expression = '';
    const expEl = document.getElementById('expression'), resEl = document.getElementById('result');
    const pretty = s => s.replaceAll('*','×').replaceAll('/','÷');
    function render() { expEl.textContent = pretty(expression || '0'); }
    function calculate() { try { let sanitized = expression.replace(/(\d+(?:\.\d+)?)%/g,'($1/100)'); if (!sanitized || !/^[0-9+\-*/().\s]+$/.test(sanitized)) throw Error(); const value = Function('"use strict"; return (' + sanitized + ')')(); if (!Number.isFinite(value)) throw Error(); resEl.textContent = Number(value.toPrecision(12)).toString(); } catch { resEl.textContent = 'Error'; } }
    document.getElementById('keys').addEventListener('click', e => { const b=e.target.closest('button'); if(!b)return; if(b.dataset.value){ expression += b.dataset.value; render(); } if(b.dataset.action==='clear'){expression='';resEl.textContent='0';render()} if(b.dataset.action==='back'){expression=expression.slice(0,-1);render()} if(b.dataset.action==='equals')calculate(); });
    window.addEventListener('keydown',e=>{ if(/[0-9.+\-*/()%]/.test(e.key)){expression+=e.key;render()} else if(e.key==='Enter'){e.preventDefault();calculate()} else if(e.key==='Backspace'){expression=expression.slice(0,-1);render()} else if(e.key==='Escape'){expression='';resEl.textContent='0';render()} });
    document.querySelector('.tabs').addEventListener('click', e=>{const b=e.target.closest('button');if(!b)return;document.querySelectorAll('.tabs button,.tool').forEach(x=>x.classList.remove('active'));b.classList.add('active');document.getElementById(b.dataset.tool).classList.add('active');});
    const num=id=>parseFloat(document.getElementById(id).value); const out=(id,label,value,unit)=>document.getElementById(id).innerHTML=`<small>${label}</small><strong>${Number(value.toPrecision(10)).toLocaleString()} ${unit}</strong>`; const valid=(...x)=>x.every(Number.isFinite);
    document.querySelectorAll('[data-solve]').forEach(b=>b.addEventListener('click',()=>{const t=b.dataset.solve;
      if(t==='ohm'){let i=num('ohmI'),r=num('ohmR'); valid(i,r)?out('ohmAnswer','Voltage (V)',i*r,'V'):out('ohmAnswer','Voltage (V)',0,'—');}
      if(t==='power'){let v=num('powerV'),i=num('powerI'); valid(v,i)?out('powerAnswer','Power (P)',v*i,'W'):out('powerAnswer','Power (P)',0,'—');}
      if(t==='motion'){let s=num('motionSpeed'),time=num('motionTime'); valid(s,time)?out('motionAnswer','Distance',s*time,'km'):out('motionAnswer','Distance',0,'—');}
      if(t==='geometry'){let r=num('radius'); valid(r)&&r>=0?out('geometryAnswer','Area',Math.PI*r*r,'square units'):out('geometryAnswer','Area',0,'—');}
      if(t==='units'){let v=num('unitValue'),c=document.getElementById('conversion').value, maps={'km-mi':[x=>x*.621371,'mi'],'mi-km':[x=>x*1.60934,'km'],'c-f':[x=>x*9/5+32,'°F'],'f-c':[x=>(x-32)*5/9,'°C'],'kg-lb':[x=>x*2.20462,'lb'],'lb-kg':[x=>x*.453592,'kg']}; valid(v)?out('unitsAnswer','Converted value',maps[c][0](v),maps[c][1]):out('unitsAnswer','Converted value',0,'—');}
    }));
  </script>
</body>
</html>
