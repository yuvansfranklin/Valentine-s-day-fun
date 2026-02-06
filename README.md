<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cute Savage Valentine 💘</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg,#ffd6e7,#e0f2ff);
  text-align:center;
  padding:20px;
}
.card{
  background:#fff;
  border-radius:18px;
  padding:25px;
  max-width:420px;
  margin:20px auto;
  box-shadow:0 10px 30px rgba(0,0,0,.1);
}
input,select,button{
  width:100%;
  padding:12px;
  margin-top:10px;
  border-radius:10px;
  border:1px solid #ddd;
  font-size:16px;
}
button{
  background:#ff4f93;
  color:#fff;
  font-weight:bold;
  border:none;
  cursor:pointer;
}
.hidden{display:none;}
.heart{
  font-size:70px;
  cursor:pointer;
  animation:pulse 1.2s infinite;
}
@keyframes pulse{
  0%{transform:scale(1)}
  50%{transform:scale(1.2)}
  100%{transform:scale(1)}
}
footer a{
  color:#555;
  margin:0 8px;
  cursor:pointer;
  text-decoration:none;
}
</style>
</head>

<body>

<!-- MAIN -->
<div class="card" id="main">
<h2>💘 Cute Savage Valentine</h2>
<p>Send a Valentine… even <b>you</b> won’t know what it says 😌</p>

<input id="from" placeholder="Your Name 😎">
<input id="to" placeholder="Their Name 👀">

<select id="type">
<option value="">Choose Category</option>
<option value="friend">Friend 😎</option>
<option value="crush">Crush 😳</option>
<option value="lover">Lover 💘</option>
<option value="family">Family 🤍</option>
<option value="ex">Ex 😌</option>
</select>

<button onclick="sendValentine()">Send Valentine 💌</button>
</div>

<!-- SENT -->
<div class="card hidden" id="sent">
<h3>💌 Sent!</h3>
<p>Only they will know what they received 😏</p>
<input id="link" readonly>
<button onclick="copyLink()">Copy Link 🔗</button>
<button onclick="shareWA()">Share on WhatsApp 📲</button>
</div>

<!-- COVER -->
<div class="card hidden" id="cover">
<h3>💌 Someone sent you a Valentine</h3>
<p>Tap to open…</p>
<div class="heart" onclick="openCard()">❤️</div>
</div>

<!-- MESSAGE -->
<div class="card hidden" id="message">
<h3>Your Valentine 💖</h3>
<p id="msg"></p>
<p id="names"></p>
<button onclick="goHome()">Send One Back 😏</button>
</div>

<footer>
<a onclick="goHome()">Home</a>
</footer>

<script>
/* 🔒 BASE URL – MUST MATCH YOUR REPO */
const BASE_URL = "https://soolaimanmohamed-ship-it.github.io/Valentine-s-day/";

/* Messages */
const messages = {
  friend:["Unlimited teasing rights 😌","Bestie vibes 😎","Chaos but loyal 😂","Friendship > everything"],
  crush:["Low-key obsessed 😏","This took courage 😳","Not flirting… maybe 👀","Rent-free in my head"],
  lover:["You’re my Valentine 😌","You’re home 🏠","Always you 💘","Soft love 💞"],
  family:["Family is everything 🤍","Forever grateful 🙏","Home is you 🏡","Love without conditions"],
  ex:["No hate, just growth 😌","Chapter closed 📕","Boundaries matter 🚧","Moved on 💨"]
};

function hideAll(){
  document.querySelectorAll('.card').forEach(c=>c.classList.add('hidden'));
}

/* SENDER */
function sendValentine(){
  const f = document.getElementById("from").value.trim();
  const t = document.getElementById("to").value.trim();
  const tp = document.getElementById("type").value;

  if(!f || !t || !tp){
    alert("Please fill all fields 🙂");
    return;
  }

  const msg = messages[tp][Math.floor(Math.random()*messages[tp].length)];

  const payload = btoa(unescape(encodeURIComponent(
    JSON.stringify({f,t,m:msg})
  )));

  const finalLink = BASE_URL + "?v=" + payload;

  hideAll();
  document.getElementById("sent").classList.remove("hidden");
  document.getElementById("link").value = finalLink;
}

/* COPY */
function copyLink(){
  const l = document.getElementById("link");
  l.select();
  document.execCommand("copy");
  alert("Link copied 😌");
}

/* WHATSAPP */
function shareWA(){
  const text = "💘 Someone sent you a Valentine… only you can see it 😌\n\n" +
               document.getElementById("link").value;
  window.open("https://wa.me/?text="+encodeURIComponent(text));
}

/* RECEIVER */
const params = new URLSearchParams(window.location.search);
if(params.has("v")){
  try{
    const decoded = JSON.parse(
      decodeURIComponent(escape(atob(params.get("v"))))
    );
    hideAll();
    document.getElementById("cover").classList.remove("hidden");
    window.card = decoded;
  }catch(e){
    alert("Invalid Valentine link 💔");
    window.location.href = BASE_URL;
  }
}

function openCard(){
  hideAll();
  document.getElementById("message").classList.remove("hidden");
  document.getElementById("msg").innerText = window.card.m;
  document.getElementById("names").innerText =
    "From: " + window.card.f + " → To: " + window.card.t;
}

/* RESET */
function goHome(){
  window.location.href = BASE_URL;
}
</script>

</body>
</html>
