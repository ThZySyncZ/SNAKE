<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Snake Versão ThZy</title>
<style>
  *{box-sizing:border-box;}
  body{
    margin:0;
    font-family:'Helvetica',sans-serif;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    height:100vh;
    background:#0a0a0a;
    color:#fff;
    user-select:none;
    overflow:hidden;
  }
  canvas{
    border:2px solid #0ff;
    background:#111;
    display:block;
    margin-bottom:15px;
  }
  #overlay{
    position:absolute;
    color:#0ff;
    font-size:36px;
    font-weight:bold;
    text-align:center;
    width:100%;
    top:50%;
    transform:translateY(-50%);
    display:none;
    text-shadow:0 0 10px #0ff,0 0 20px #0ff;
  }
  #controls{
    display:grid;
    grid-template-columns:repeat(3,70px);
    grid-gap:8px;
    justify-content:center;
    margin-bottom:15px;
  }
  .btn{
    width:70px;
    height:70px;
    background:linear-gradient(145deg,#00ffff,#005555);
    border:2px solid #0ff;
    border-radius:12px;
    font-size:24px;
    font-weight:bold;
    color:#0ff;
    cursor:pointer;
    box-shadow:0 0 10px #0ff;
    transition:all 0.1s ease-in-out;
  }
  .btn:active{
    transform:scale(0.9);
    box-shadow:0 0 5px #0ff inset;
  }
  #settings{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:10px;
    margin-bottom:15px;
    align-items:center;
  }
  #settings label{margin-right:5px;}
  select,input[type=number],input[type=checkbox]{margin-right:10px;}
  button#applyBtn{
    background:#0ff;
    border:none;
    border-radius:8px;
    padding:6px 12px;
    color:#000;
    font-weight:bold;
    cursor:pointer;
    transition:0.1s;
  }
  button#applyBtn:hover{background:#0cc;}
</style>
</head>
<body>

<div id="settings">
  <label>Modo gráfico:</label>
  <select id="graphicMode">
    <option value="2d">2D Futurista</option>
    <option value="3d">3D Neon</option>
  </select>
  <label>Velocidade inicial:</label>
  <input id="speedInput" type="number" min="1" max="20" value="8">
  <label>Paredes:</label>
  <input type="checkbox" id="wallInput">
  <label>Mostrar Grid:</label>
  <input type="checkbox" id="gridInput" checked>
  <button id="applyBtn" onclick="applySettings()">Aplicar</button>
</div>

<canvas id="gc" width="500" height="500"></canvas>
<div id="overlay">PAUSADO</div>

<div id="controls">
  <button class="btn" onclick="Snake.action('up')">↑</button>
  <button class="btn" onclick="Snake.pause()">⏸</button>
  <button class="btn" onclick="Snake.reset()">⟳</button>
  <button class="btn" onclick="Snake.action('left')">←</button>
  <div></div>
  <button class="btn" onclick="Snake.action('right')">→</button>
  <div></div>
  <button class="btn" onclick="Snake.action('down')">↓</button>
</div>

<audio id="eatSound" src="https://freesound.org/data/previews/66/66717_931655-lq.mp3"></audio>

<script>
const Snake=(function(){
  const INITIAL_TAIL=4;
  let fixedTail=false, intervalID, fps=8, paused=false, tileCount=20;
  let gridSize=500/tileCount, player={x:Math.floor(tileCount/2),y:Math.floor(tileCount/2)}, velocity={x:0,y:0};
  let walls=false, showGrid=true, mode2D=true;
  let fruits=[], trail=[], tail=INITIAL_TAIL, points=0, pointsMax=0;
  const ActionEnum={none:0, up:1, down:2, left:3, right:4}; Object.freeze(ActionEnum);
  let lastAction=ActionEnum.none;
  const canv=document.getElementById('gc'), ctx=canv.getContext('2d');
  const overlay=document.getElementById('overlay'), eatSound=document.getElementById('eatSound');
  let particles=[];
  const fruitTypes=[
    {type:'maçã',color:'255,0,0',points:1,img:'https://i.imgur.com/1Jv2F9b.png'},
    {type:'banana',color:'255,255,0',points:2,img:'https://i.imgur.com/LFqYI6r.png'},
    {type:'melancia',color:'0,255,0',points:3,img:'https://i.imgur.com/lkQx0sN.png'}
  ];
  const fruitImgs={};
  fruitTypes.forEach(f=>{const img=new Image(); img.src=f.img; fruitImgs[f.type]=img;});

  function reset(){
    player={x:Math.floor(tileCount/2),y:Math.floor(tileCount/2)};
    velocity={x:0,y:0};
    tail=INITIAL_TAIL;
    points=0;
    lastAction=ActionEnum.none;
    trail=[{...player}];
    spawnFruits();
    draw();
  }

  function spawnFruits(){
    fruits=[];
    fruitTypes.forEach(ft=>{
      let pos; do{ pos={x:Math.floor(Math.random()*tileCount),y:Math.floor(Math.random()*tileCount)};}
      while(trail.some(s=>s.x===pos.x && s.y===pos.y));
      fruits.push({...ft,x:pos.x,y:pos.y});
    });
  }

  function createParticles(x,y,color){
    for(let i=0;i<15;i++){
      particles.push({x:x*gridSize+gridSize/2,y:y*gridSize+gridSize/2,vx:(Math.random()-0.5)*5,vy:(Math.random()-0.5)*5,alpha:1,color:color});
    }
  }

  function drawParticles(){
    particles.forEach(p=>{
      ctx.fillStyle=`rgba(${p.color},${p.alpha})`;
      ctx.beginPath(); ctx.arc(p.x,p.y,4,0,Math.PI*2); ctx.fill();
      p.x+=p.vx; p.y+=p.vy; p.alpha-=0.05;
    });
    particles=particles.filter(p=>p.alpha>0);
  }

  function draw(){
    ctx.clearRect(0,0,canv.width,canv.height);
    ctx.fillStyle='#0a0a0a'; ctx.fillRect(0,0,canv.width,canv.height);
    if(showGrid){
      ctx.strokeStyle='rgba(0,255,255,0.2)'; ctx.lineWidth=1;
      for(let i=0;i<=tileCount;i++){ ctx.beginPath(); ctx.moveTo(i*gridSize,0); ctx.lineTo(i*gridSize,canv.height); ctx.moveTo(0,i*gridSize); ctx.lineTo(canv.width,i*gridSize); ctx.stroke();}
    }

    trail.forEach((seg,index)=>{
      const shade=Math.floor(50+(index/trail.length)*205);
      ctx.shadowColor='cyan';
      ctx.shadowBlur=15;
      ctx.fillStyle=`rgb(0,${shade},${shade})`;
      ctx.fillRect(seg.x*gridSize+1,seg.y*gridSize+1,gridSize-2,gridSize-2);
      ctx.shadowBlur=0;
    });

    const pulse=Math.sin(Date.now()/150)*5;
    fruits.forEach(f=>{
      const img=fruitImgs[f.type];
      ctx.shadowColor=f.color; ctx.shadowBlur=15;
      ctx.drawImage(img,f.x*gridSize+1+pulse/2,f.y*gridSize+1+pulse/2,gridSize-2-pulse,gridSize-2-pulse);
      ctx.shadowBlur=0;
    });

    drawParticles();
    ctx.fillStyle='#0ff'; ctx.font='bold 18px Helvetica';
    ctx.fillText(`Points: ${points}`,10,25);
    ctx.fillText(`Top: ${pointsMax}`,10,45);
  }

  function gameLoop(){
    if(paused) return;
    player.x+=velocity.x; player.y+=velocity.y;
    if(!walls){ player.x=(player.x+tileCount)%tileCount; player.y=(player.y+tileCount)%tileCount;}
    else{ if(player.x<0||player.x>=tileCount||player.y<0||player.y>=tileCount){reset(); return;}}

    lastAction=velocity.x===1?ActionEnum.right:velocity.x===-1?ActionEnum.left:velocity.y===1?ActionEnum.down:velocity.y===-1?ActionEnum.up:lastAction;
    trail.push({...player}); while(trail.length>tail) trail.shift();

    for(let i=0;i<trail.length-1;i++){ if(trail[i].x===player.x&&trail[i].y===player.y){reset(); return;} }

    fruits.forEach((f,index)=>{
      if(player.x===f.x&&player.y===f.y){
        tail+=f.points; points+=f.points; if(points>pointsMax) pointsMax=points;
        createParticles(f.x,f.y,f.color);
        eatSound.currentTime=0; eatSound.play();
        let pos; do{ pos={x:Math.floor(Math.random()*tileCount),y:Math.floor(Math.random()*tileCount)};} while(trail.some(s=>s.x===pos.x&&s.y===pos.y));
        fruits[index].x=pos.x; fruits[index].y=pos.y;
      }
    });
    draw();
  }

  function keyHandler(evt){
    switch(evt.keyCode){
      case 37: if(lastAction!==ActionEnum.right){velocity={x:-1,y:0}} break;
      case 38: if(lastAction!==ActionEnum.down){velocity={x:0,y:-1}} break;
      case 39: if(lastAction!==ActionEnum.left){velocity={x:1,y:0}} break;
      case 40: if(lastAction!==ActionEnum.up){velocity={x:0,y:1}} break;
      case 32: togglePause(); break;
      case 27: reset(); break;
    }
  }

  function togglePause(){ paused=!paused; overlay.style.display=paused?'block':'none'; }

  return {
    start:function(fpsStart=8){ fps=fpsStart; reset(); intervalID=setInterval(gameLoop,1000/fps); document.addEventListener('keydown',keyHandler);},
    reset:reset,
    pause:togglePause,
    action:function(dir){switch(dir){case 'up':if(lastAction!==ActionEnum.down){velocity={x:0,y:-1}} break; case 'down':if(lastAction!==ActionEnum.up){velocity={x:0,y:1}} break; case 'left':if(lastAction!==ActionEnum.right){velocity={x:-1,y:0}} break; case 'right':if(lastAction!==ActionEnum.left){velocity={x:1,y:0}} break;}},
    setup:{ fixedTail:function(state){fixedTail=state;}, wall:function(state){walls=state;}, grid:function(state){showGrid=state;}, graphic:function(state){mode2D=state==='2d';} }
  };
})();

function applySettings(){
  const mode=document.getElementById('graphicMode').value;
  const speed=parseInt(document.getElementById('speedInput').value)||8;
  const walls=document.getElementById('wallInput').checked;
  const grid=document.getElementById('gridInput').checked;
  Snake.setup.graphic(mode);
  Snake.setup.wall(walls);
  Snake.setup.grid(grid);
  Snake.reset();
  clearInterval(Snake.intervalID);
  Snake.start(speed);
}

Snake.start(8);
</script>
</body>
</html>
