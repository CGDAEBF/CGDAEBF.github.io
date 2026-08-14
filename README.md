# CGDAEBF.github.io
<button onclick='f()'>刷新</button>
<p id='p'></p>
<p id='q'></p>
<script>
let a=0,b=0,ans,tmp,tans,tm,p=document.getElementById('p')
function f(){
tm=0;ans=0;tans=0;a+=Date.now()%1201
p.innerHTML=''
for(let i=0;i<256;i++){
a=(a*a*a+b+7)%180503
b=(b*b*b+a+7)%180503
p.innerHTML+=`<button id="${i}"${(a%16==0?(' onclick="g('+i+')">q'):'>p')}</button>`
if(i%16==15)p.innerHTML+='<br>'
if(a%16==0)tans++;
}
q.innerHTML=`共有${tans}个q`;
}
function g(k){
if(tm==0)tm=Date.now()
ans++
tmp=document.getElementById(''+k)
tmp.onclick=''
tmp.innerHTML='p'
q.innerHTML=`剩余${tans-ans}个q`
if(tans==ans)q.innerHTML=`你赢了!用时${(Date.now()-tm)/1000}秒`
}
</script>
