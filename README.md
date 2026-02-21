# Darkzone-gamer
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DarkZone Gamer</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial, Helvetica, sans-serif;
}

body{
background:linear-gradient(135deg,#0f0f0f,#1c1c1c);
color:white;
}

header{
background:#111;
padding:15px;
display:flex;
flex-wrap:wrap;
justify-content:space-between;
align-items:center;
box-shadow:0 0 15px #00ffcc;
}

.logo{
font-size:22px;
color:#00ffcc;
font-weight:bold;
}

input, select{
padding:8px;
border:none;
border-radius:5px;
margin:5px;
}

button{
background:#00ffcc;
border:none;
padding:8px 12px;
border-radius:5px;
cursor:pointer;
font-weight:bold;
transition:0.3s;
}

button:hover{
background:#00bfa6;
transform:scale(1.05);
}

.container{
padding:20px;
}

.games{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:20px;
}

.card{
background:#1a1a1a;
padding:15px;
border-radius:12px;
transition:0.4s;
box-shadow:0 0 10px rgba(0,255,204,0.3);
}

.card:hover{
transform:translateY(-5px);
box-shadow:0 0 20px #00ffcc;
}

.hidden{
display:none;
}

.ad{
margin:20px 0;
padding:20px;
text-align:center;
background:#111;
border:1px solid #00ffcc;
border-radius:10px;
}

.user-box{
margin-top:10px;
}

@media(max-width:600px){
header{
flex-direction:column;
align-items:flex-start;
}
}
</style>
</head>
<body>

<header>
<div class="logo">🎮 DarkZone Gamer</div>

<div>
<input type="text" id="search" placeholder="Buscar juego...">
<select id="filter">
<option value="all">Todas las consolas</option>
<option value="PC">PC</option>
<option value="PS2">PlayStation 2</option>
<option value="Xbox">Xbox</option>
</select>
</div>

<div class="user-box" id="userArea">
<input type="text" id="username" placeholder="Usuario">
<input type="password" id="password" placeholder="Contraseña">
<button onclick="register()">Registrarse</button>
<button onclick="login()">Login</button>
</div>

<div id="welcome" class="hidden">
<span id="userText"></span>
<button onclick="logout()">Salir</button>
</div>

</header>

<div class="container">

<div class="ad">
<!-- PEGAR AQUÍ CÓDIGO DE GOOGLE ADSENSE -->
ESPACIO PARA ANUNCIO
</div>

<div class="games" id="gameList">

<div class="card" data-console="PC">
<h3>Juego Free PC</h3>
<p>Disponible oficialmente</p>
<button>Ver más</button>
</div>

<div class="card" data-console="PS2">
<h3>Juego Retro PS2</h3>
<p>Homebrew legal</p>
<button>Ver más</button>
</div>

<div class="card" data-console="Xbox">
<h3>Juego Free Xbox</h3>
<p>Microsoft Store</p>
<button>Ver más</button>
</div>

</div>
</div>

<script>
// FILTRO Y BUSCADOR
const searchInput = document.getElementById("search");
const filterSelect = document.getElementById("filter");
const cards = document.querySelectorAll(".card");

function filterGames(){
const searchText = searchInput.value.toLowerCase();
const filterValue = filterSelect.value;

cards.forEach(card=>{
const title = card.querySelector("h3").textContent.toLowerCase();
const consoleType = card.getAttribute("data-console");

let matchesSearch = title.includes(searchText);
let matchesFilter = filterValue === "all" || consoleType === filterValue;

if(matchesSearch && matchesFilter){
card.style.display="block";
}else{
card.style.display="none";
}
});
}

searchInput.addEventListener("input",filterGames);
filterSelect.addEventListener("change",filterGames);

// SISTEMA DE USUARIOS (LocalStorage)
function register(){
let user = document.getElementById("username").value;
let pass = document.getElementById("password").value;

if(user && pass){
localStorage.setItem(user,pass);
alert("Usuario registrado!");
}else{
alert("Completa los campos");
}
}

function login(){
let user = document.getElementById("username").value;
let pass = document.getElementById("password").value;

if(localStorage.getItem(user) === pass){
localStorage.setItem("loggedUser",user);
showUser(user);
}else{
alert("Datos incorrectos");
}
}

function showUser(user){
document.getElementById("userArea").classList.add("hidden");
document.getElementById("welcome").classList.remove("hidden");
document.getElementById("userText").innerText="Bienvenido "+user;
}

function logout(){
localStorage.removeItem("loggedUser");
location.reload();
}

window.onload = function(){
let logged = localStorage.getItem("loggedUser");
if(logged){
showUser(logged);
}
}
</script>

</body>
</html>
