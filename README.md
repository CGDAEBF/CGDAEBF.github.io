<input id="i"><br>
<canvas id="c" width="340" height="340" style="border:1px solid #000">
<script>
let cvs=document.getElementById("c"),x=0,y=0,mx=-8,my=8,itv,tks;
let c=cvs.getContext("2d");
function draw(){
tks++;
document.getElementById("i").value=""
cvs.width=cvs.width
for(let i=-8;i<=8;i++)
for(let j=-8;j<=8;j++)
if(isWall(i+x,j+y))c.fillRect(i*20+160,j*20+160,20,20)
c.fillRect(165,165,10,10)
if(mx<x)mx+=0.0625;
else if(mx>x)mx-=0.0625;
if(my<y)my+=0.0625;
else if(my>y)my-=0.0625;
if(Math.abs(mx-x)<=0.0625&&Math.abs(my-y)<=0.0625){cvs.style="display:none";clearInterval(itv);}
c.fillRect((mx-x)*20+160,(my-y)*20+160,20,20)
}
function f(x,y){
let k=((x+y)%13+13)%13+3
for(let i=0;i<k;i++){
x=(x*x+y+i)%180503
y=(y*y+x+13)%180503
}
return x%4
}
function isWall(x,y){
if(x%2&&y%2)return 1
if(!(x%2||y%2))return 0
if(x%2)return f(x,y-1)==0||f(x,y+1)==2
if(y%2)return f(x-1,y)==1||f(x+1,y)==3
}
document.getElementById("i").onkeydown=function(e){
if(e.key=="w"){y--;if(isWall(x,y))y++}
if(e.key=="a"){x--;if(isWall(x,y))x++}
if(e.key=="s"){y++;if(isWall(x,y))y--}
if(e.key=="d"){x++;if(isWall(x,y))x--}}
itv=setInterval(draw,25)
</script>
