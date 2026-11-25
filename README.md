<p id="p">电脑端按Esc键也可以起到change的效果</p>
<button id="b" onclick="t++;if(p)ri();else up()">down</button><button onclick="u++;p=!p;document.getElementById('b').innerHTML=lis[+p]">change</button><br>
<canvas id="c" width="600" height="600" style="border:1px solid #000"></canvas><br>
<script>
    let cvs=document.getElementById("c"),c=cvs.getContext("2d"),x=0,y=0,b=0,t=0,p=0,lis=["down","right"],u=0,s=0
    function f(i,j){
    if(i<0||i>=25||j<0||j>=25)return -1
    let a=i,b=j,c=0
    for(let k=0;k<3+(i*i+j*j)%13;k++){a=(a+b+c+k)%23;b=(a+b+c+k)%23;c=(a+b+c+k)%23}
    return a%4
    }
    function g(i,j){
    if(i<0||j<0||i>=25||j>=25)return 1
    if(i%2==1){
    if(j%2==1)return 1
    else return f(i,j-1)==0||f(i,j+1)==2
    }
    else{
    if(j%2==0)return 0
    else return f(i-1,j)==1||f(i+1,j)==3
    }
    }
    function draw(){for(let i=0;i<25;i++)for(let j=0;j<25;j++)if(g(i,j))c.fillRect(i*24,j*24,24,24);if(!b)c.fillRect(x*24+6,y*24+6,12,12);else c.fillRect(x*24+10,y*24+10,4,4);if(x==24&&y==24)clear()}
    function ri(){
    if(b){if(g(x+1,y)==1){x+=2;b=0}else if(g(x+3,y)==1)x+=2;else{x+=4;b=0}}
    else{if(g(x+1,y)==0)x+=2;else if(g(x-1,y)!=1)while(g(x-1,y)==0)x-=2;else{b=1;s++;t--}}
    cvs.width=cvs.width;draw()
    }
    function up(){
    if(b){if(g(x,y+1)==1){y+=2;b=0}else if(g(x,y+3)==1)y+=2;else{y+=4;b=0}}
    else{if(g(x,y+1)==0)y+=2;else if(g(x,y-1)!=1)while(g(x,y-1)==0)y-=2;else b=1}
    cvs.width=cvs.width;draw()
    }
    function clear(){
    document.getElementById("p").innerHTML=`你赢了!你的步数:${t+u},你的切换次数:${u},你的移动次数:${t},你的压缩次数:${s}`
    x=y=b=t=p=u=s=0;cvs.width=cvs.width;draw()
    }
    document.onkeydown=function(){u++;p=!p;document.getElementById('b').innerHTML=lis[+p]}
    draw()
</script>
