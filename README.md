<input id="i"><br><input id="j"><br><button onclick="init()">init</button><br>
<canvas id="d" width="70" height="70" style="border:1px solid #000"></canvas><br>
<canvas id="c" width="340" height="340" style="border:1px solid #000"></canvas>
<p id="p"></p>
<script>
    const cvs=document.getElementById('c')
    const c=cvs.getContext("2d")
    const dvs=document.getElementById('d')
    const d=dvs.getContext("2d")
    let a=1,b=Date.now()%1201,t,x,y,s,mx,mn,k=0
    function rand(){
    a=(b*b*b+a+7)%180503;b=(a*a*a+b+7)%180503
    return a
    }
    function init(){
    s=0;mx=0;mn=10000;k=0;cvs.width=cvs.width;dvs.width=dvs.width;document.body.style.background=document.getElementById("j").value;draw()
    }
    function draw(){
    t=Date.now()
    x=rand()%27;y=rand()%27
    cvs.width=cvs.width;dvs.width=dvs.width
    c.fillStyle=d.fillStyle=document.getElementById("i").value
    for(let i=0;i<34;i++)
    for(let j=0;j<34;j++){
    if(rand()%2==0){c.fillRect(i*10,j*10,10,10)
    if(i-x<7&&i-x>=0&&j-y<7&&j-y>=0)d.fillRect((i-x)*10,(j-y)*10,10,10)}
    }}
    cvs.addEventListener('click',(e)=>{
    const rect=cvs.getBoundingClientRect()
    const cx=Math.round((e.clientX-rect.left)/10)
    const cy=Math.round((e.clientY-rect.top)/10)
    if(cx-x<7&&cx-x>=0&&cy-y<7&&cy-y>=0){t-=Date.now();s+=t=-t;mx=Math.max(mx,t);mn=Math.min(mn,t);k++;if(k==3){k=0;document.getElementById("p").innerHTML=s-mx-mn;cvs.width=cvs.width;dvs.width=dvs.width}else draw()}
    })
</script>
