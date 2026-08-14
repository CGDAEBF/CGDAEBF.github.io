<button style="visibility:hidden">o</button><button onclick="y--;if(!f(x,y))y++;draw()">o</button><br>
<button onclick="x--;if(!f(x,y))x++;draw()">o</button><button style="visibility:hidden">o</button><button onclick="x++;if(!f(x,y))x--;draw()">o</button><br>
<button style="visibility:hidden">o</button><button onclick="y++;if(!f(x,y))y--;draw()">o</button><br>
<canvas id="c" width="620" height="620" style="border:20px solid #000"></canvas>
<script>
  let cvs=document.getElementById("c"),x=0,y=0,mx=30,my=30,t
  let c=cvs.getContext("2d")
  function f(a,b){
  if(a<0||a>30||b<0||b>30)return 0;
  if(a%2&&b%2)return 0;
  if(!(a%2||b%2))return 1;
  let k=(a+b)%17+7
  for(let i=0;i<k;i++){
  a=(b*b*b+a+4)%180503;
  b=(a*a*a+b+4)%180503;
  }
  return a%4;
  }
  function draw(){
  if(x==mx%16*2&&y==my%16*2){
  mx=(my*my*my+mx+4)%180503;
  my=(mx*mx*mx+my+4)%180503;
  }
  cvs.width=cvs.width
  for(let i=0;i<=30;i++)
  for(let j=0;j<=30;j++){
  if(!f(i,j)){c.fillStyle="#000000";c.fillRect(i*20,j*20,20,20)}
  }
  c.strokeRect(x*20+5,y*20+5,10,10)
  c.fillStyle="#ff0000";c.fillRect(mx%16*40,my%16*40,20,20)
  }
  draw();
</script>
