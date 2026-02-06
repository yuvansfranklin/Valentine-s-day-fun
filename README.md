
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
footer{
  margin-top:25px;
  font-size:14px;
}
footer a{
  color:#555;
  margin:0 6px;
  cursor:pointer;
  text-decoration:none;
}
</style>
</head>

<body>

<!-- SENDER -->
<div class="card" id="sendBox">
  <h2>💘 Cute Savage Valentine</h2>
  <p>Send a Valentine… even <b>you</b> won’t know what it says 😌</p>

  <input id="from" placeholder="Your Name 😎">
  <input id="to" placeholder="Their Name 👀">

  <select id="cat">
    <option value="">Choose Category</option>
    <option value="friend">Friend 😎</option>
    <option value="crush">Crush 😳</option>
    <option value="lover">Lover 💘</option>
    <option value="family">Family 🤍</option>
    <option value="ex">Ex 😌</option>
  </select>

  <button onclick="send()">Send Valentine 💌</button>
</div>

<!-- SENT -->
<div class="card hidden" id="sentBox">
  <h3>💌 Sent!</h3>
  <p>Only they will know what they received 😏</p>
  <input id="link" readonly>
  <button onclick="copyLink()">Copy Link 🔗</button>
  <button onclick="shareWA()">Share on WhatsApp 📲</button>
</div>

<!-- RECEIVER COVER -->
<div class="card hidden" id="coverBox">
  <h3>💌 Someone sent you a Valentine</h3>
  <p>Tap to open…</p>
  <div class="heart" onclick="openCard()">❤️</div>
</div>

<!-- RECEIVER MESSAGE -->
<div class="card hidden" id="msgBox">
  <h3>Your Valentine 💖</h3>
  <p id="message"></p>
  <p id="names"></p>
  <p><small>📸 Screenshot it. Don’t explain 😌</small></p>
  <button onclick="goHome()">Send One Back 😏</button>
</div>

<footer>
  <a onclick="goHome()">Home</a>
</footer>

<script>
/* 🔐 BASE URL (CHANGE ONLY THIS IF REPO NAME CHANGES) */
const BASE_URL = "https://soolaimanmohamed-ship-it.github.io/Valentine-s-day/";

/* 💬 EMOJI MESSAGES (SAFE PLACE) */
const messages = {
  friend: [
    "Bestie energy only 😎🔥",
    "Chaos but loyal 😂💯",
    "Friendship > everything 🤝💖"
  ],
  crush: [
    "Low-key obsessed 😏💘",
    "This took courage 😳🔥",
    "Not flirting… maybe 👀😌"
  ],
  lover: [
    "Always you 💞🥹",
    "You’re my peace 😌💖",
    "Home is you 🏠💘"
  ],
  family: [
    "Forever grateful 🤍🙏",
    "Family = strength 💪🫶",
    "Love without conditions 🏡💖"
  ],
  ex: [
    "No hate, just growth 😌✨",
    "Lesson learned 📖💭",
    "Chapter closed 🚪🔥"
  ]
};

/* 🧹 HELPER */
function hideAll(){
  document.querySelectorAll(".card").forEach(c=>c.classList.add("hidden"));
}

/* ✉️ SENDER */
function send(){
  const f = from.value.trim();
  const t = to.value.trim();
  const c = cat.value;

  if(!f || !t || !c){
    alert("Fill all fields 🙂");
    return;
  }

  const url =
    BASE_URL +
    "?cat=" + encodeURIComponent(c) +
    "&from=" + encodeURIComponent(f) +
    "&to=" + encodeURIComponent(t);

  hideAll();
  sentBox.classList.remove("hidden");
  link.value = url;
}

/* 📋 COPY */
function copyLink(){
  link.select();
  document.execCommand("copy");
  alert("Link copied 😌");
}

/* 📲 WHATSAPP */
function shareWA(){
  const text =
    "💘 Someone sent you a Valentine…\nOnly you can see it 😌\n\n" +
    link.value;
  window.open("https://wa.me/?text=" + encodeURIComponent(text));
}

/* 📥 RECEIVER */
const params = new URLSearchParams(window.location.search);
if(params.has("cat") && params.has("from") && params.has("to")){
  hideAll();
  coverBox.classList.remove("hidden");

  window.rcv = {
    cat: params.get("cat"),
    from: params.get("from"),
    to: params.get("to")
  };
}

/* ❤️ OPEN CARD */
function openCard(){
  const list = messages[rcv.cat];
  const msg = list[Math.floor(Math.random()*list.length)];

  hideAll();
  msgBox.classList.remove("hidden");
  message.innerText = msg;
  names.innerText = "From: " + rcv.from + " → To: " + rcv.to;
}

/* 🔁 RESET */
function goHome(){
  window.location.href = BASE_URL;
}
</script>

</body>
</html>
