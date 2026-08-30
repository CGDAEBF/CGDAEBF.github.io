<button onclick="restart()">开始游戏</button><button onclick='document.getElementById("coin").innerHTML=localStorage.getItem("cgd-aeb-f-coins")'>找回数据</button><br>
<p id="coin">0</p>
<p id="p"><canvas id="c" width="343" height="343" style="position:fixed;border:1px solid #000"></canvas></p>
<script>
    let a,b,a1,b1,px,py,vx,vy,mx,my,gx,gy,score,ticks,itv
    const cvs=document.getElementById("c"),c=cvs.getContext("2d")
    function restart(){
    a=0,b=0,a1=Date.now()%180503,b1=0,px=0,py=0,vx=0,vy=0,mx=4,my=4,gx=0,gy=0,score=0,ticks=0,itv=setInterval(draw,25)
    }
    function f(x,y){
    if(x>16||x<-16||y>16||y<-16)return 4
    if(x%2==0&&y%2==0)return -1
    if(x%2==0||y%2==0)return (f(x+1,y)==1||f(x,y+1)==2||f(x-1,y)==3||f(x,y-1)==0)-1
    a=x%180503+180503;b=y%180503+180503
    for(let i=0;i<(x%7+y%7+14)%7+11;i++){
    a=(a*a*a+b+7)%180503
    b=(b*b*b+a+7)%180503
    }
    return a%4;
    }
    function draw(){
    a1=(a1*a1*a1+b1+7)%180503
    b1=(b1*b1*b1+a1+7)%180503
    if(ticks==0){gx=(a1%17-8)*2;gy=(b1%17-8)*2}
    score++;ticks++;ticks%=600
    px+=vx
    py+=vy
    if(f(Math.round(px),Math.round(py))!=-1){px-=vx;py-=vy;while(f(Math.round(px+0.0625*vx),Math.round(py+0.0625*vy))==-1){px+=0.0625*vx;py+=0.0625*vy}}
    if((gx-px)*(gx-px)+(gy-py)*(gy-py)<=1/16){score+=800;ticks=0}
    if((mx-px)*(mx-px)+(my-py)*(my-py)<=1/196){clearInterval(itv);localStorage.setItem("cgd-aeb-f-coins",(document.getElementById("coin").innerHTML=+document.getElementById("coin").innerHTML+Math.floor(score/100)).toString())}
    mx-=(mx-px)/Math.sqrt(196*((mx-px)*(mx-px)+(my-py)*(my-py)))
    my-=(my-py)/Math.sqrt(196*((mx-px)*(mx-px)+(my-py)*(my-py)))
    cvs.width=cvs.width
    for(let i=-3;i<=4;i++)for(let j=-3;j<=4;j++)if(f(i+Math.floor(px),j+Math.floor(py))!=-1)c.fillRect(i*49+147-px*49+Math.floor(px)*49,j*49+147-py*49+Math.floor(py)*49,49,49)
    c.fillRect(170,170,3,3)
    c.fillStyle="#00f"
    c.fillRect(168.5-(px-mx)*49,168.5-(py-my)*49,6,6)
    c.fillRect(168.5-(px-gx)*49,168.5-(py-gy)*49,6,6)
    c.moveTo(171.5,171.5)
    c.lineTo(171.5-49*(px-gx)/Math.sqrt((gx-px)*(gx-px)+(gy-py)*(gy-py)),171.5-49*(py-gy)/Math.sqrt((gx-px)*(gx-px)+(gy-py)*(gy-py)))
    c.stroke()
    }
    cvs.addEventListener('mousemove',function(e){
    var x=e.pageX-this.offsetLeft
    var y=e.pageY-this.offsetTop
    if(this!=cvs)return 0
    vx=(x-171.5)/1024
    vy=(y-171.5)/1024
    })
    cvs.addEventListener('touchmove',function(e){
    e=e.touches[0]
    var x=e.pageX-this.offsetLeft
    var y=e.pageY-this.offsetTop
    if(this!=cvs)return 0
    vx=(x-171.5)/1024
    vy=(y-171.5)/1024
    })
</script>
