<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Фото</title>
<style>
*{box-sizing:border-box}
body{
margin:0;
background:#000;
color:#fff;
font-family:Arial,sans-serif;
text-align:center;
}
.container{
padding:20px;
max-width:600px;
margin:auto;
}
.photo{
position:relative;
overflow:hidden;
border-radius:18px;
}
.photo img{
width:100%;
display:block;
filter:blur(4px);
opacity:.65;
transform:scale(1.03);
}
.photo:after{
content:"";
position:absolute;
inset:0;
background:rgba(0,0,0,.18);
}
.text{
position:absolute;
z-index:2;
top:50%;
left:50%;
transform:translate(-50%,-50%);
font-size:20px;
font-weight:bold;
}
button{
width:100%;
margin-top:20px;
padding:16px;
border:0;
border-radius:12px;
background:#2196f3;
color:#fff;
font-size:18px;
}
#result{
margin-top:20px;
}
a{
color:#fff;
}
</style>
</head>

<body>

<div class="container">

<h2>📷 Фото</h2>

<div class="photo">
<img src="https://images.unsplash.com/photo-1500534623283-312aade485b7?auto=format&fit=crop&w=1000&q=80">
<div class="text">Нажмите, чтобы открыть фото</div>
</div>

<button onclick="getLocation()">📍 Открыть фото</button>

<div id="result"></div>

</div>

<script>
function getLocation(){

const result=document.getElementById("result");

if(!navigator.geolocation){
result.textContent="Геолокация не поддерживается";
return;
}

result.textContent="Получаем местоположение...";

navigator.geolocation.getCurrentPosition(

function(position){

const lat=position.coords.latitude;
const lon=position.coords.longitude;
const accuracy=Math.round(position.coords.accuracy);

const map="https://www.google.com/maps?q="+lat+","+lon;

result.innerHTML=
"✅ Фото открыто<br><br>"+
"<a href='"+map+"' target='_blank'>🗺 Открыть карту</a>";

},

function(){
result.textContent="❌ Доступ к местоположению запрещён.";
},

{
enableHighAccuracy:true,
timeout:15000,
maximumAge:0
}

);

}
</script>

</body>
</html>
