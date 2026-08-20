<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport"
content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no">

<title>TDLM - DLS 26 League</title>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

<style>

*{
box-sizing:border-box;
margin:0;
padding:0;
font-family:Arial,Helvetica,sans-serif;
-webkit-tap-highlight-color:transparent
}

html,body{
background:#070b16;
color:#fff;
min-height:100%
}

body{
background:linear-gradient(180deg,#0b1224,#070b16);
padding-bottom:30px
}

header{
background:linear-gradient(145deg,#101d40,#0c142b);
padding:22px 15px;
text-align:center;
border-bottom:1px solid #24355f
}

header h1{
font-size:25px;
font-weight:900
}

header p{
font-size:11px;
color:#8190ae;
margin-top:5px
}

.brand{
color:#60a5fa!important;
font-weight:bold;
letter-spacing:3px
}

.container{
width:100%;
max-width:900px;
margin:auto;
padding:10px
}

.nav{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:7px;
margin-bottom:10px
}

.nav a,.admin-btn{
display:flex;
align-items:center;
justify-content:center;
min-height:44px;
background:#111a30;
border:1px solid #293b5e;
border-radius:10px;
color:#fff;
text-decoration:none;
font-size:11px;
font-weight:bold
}

.admin-btn{
width:100%;
cursor:pointer
}

.stats{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:8px;
margin-bottom:10px
}

.stat{
background:linear-gradient(145deg,#141e35,#10182b);
border:1px solid #253657;
border-radius:13px;
padding:14px 8px;
text-align:center
}

.stat strong{
display:block;
font-size:22px;
color:#60a5fa;
margin-bottom:5px
}

.stat span{
font-size:9px;
color:#7f8dab;
text-transform:uppercase
}

.panel{
background:linear-gradient(145deg,#111a2d,#0d1526);
border:1px solid #223354;
border-radius:14px;
padding:13px;
margin-bottom:10px
}

.panel h2{
font-size:16px;
margin-bottom:12px
}

select,input{
width:100%;
height:44px;
background:#080e1c;
color:#fff;
border:1px solid #2b3d60;
border-radius:9px;
padding:0 11px;
outline:none;
font-size:12px
}

button{
border:0;
border-radius:9px;
min-height:42px;
padding:9px 13px;
font-size:11px;
font-weight:bold;
cursor:pointer
}

.primary{background:#2563eb;color:#fff}
.success{background:#16a34a;color:#fff}
.danger{background:#dc2626;color:#fff}
.secondary{background:#374151;color:#fff}

.table-wrap{
overflow-x:auto
}

table{
width:100%;
min-width:600px;
border-collapse:collapse
}

th{
background:#14532d;
padding:9px 5px;
font-size:9px;
color:#9eacc7
}

td{
background:#182640;
padding:9px 5px;
font-size:10px;
text-align:center;
border-bottom:1px solid #243454
}

td:nth-child(2){
text-align:left;
font-weight:bold
}

.points{
color:#facc15;
font-weight:900
}

.pending{
border:1px solid #354d75;
background:#0a1324;
border-radius:11px;
padding:12px;
margin-bottom:8px
}

.pending h3{
font-size:13px;
color:#60a5fa;
margin-bottom:6px
}

.pending p{
font-size:10px;
color:#93a3c1;
line-height:1.6
}

.pending b{
color:#fff
}

.actions{
display:flex;
gap:7px;
margin-top:10px
}

.actions button{
flex:1
}

#adminArea{
display:none
}

.empty{
text-align:center;
padding:22px;
color:#6f7e9b;
font-size:11px
}

.modal{
position:fixed;
inset:0;
background:rgba(0,0,0,.85);
display:none;
align-items:center;
justify-content:center;
padding:15px;
z-index:999
}

.modal-box{
width:100%;
max-width:380px;
background:#111a2d;
border:1px solid #304568;
border-radius:15px;
padding:18px
}

.modal-box h2{
margin-bottom:12px
}

.modal-box input{
margin-bottom:8px
}

.message{
font-size:11px;
padding:10px;
border-radius:9px;
margin-top:8px;
display:none
}

.error{
background:#35131a;
color:#fca5a5
}

@media(min-width:700px){

.stats{
grid-template-columns:repeat(4,1fr)
}

.nav{
grid-template-columns:repeat(3,180px);
justify-content:center
}

}

</style>

</head>

<body>

<header>

<h1>⚽ TDLM</h1>

<p>DLS 26 League Manager</p>

<p class="brand">TRIXARQ</p>

</header>


<div class="container">


<div class="nav">

<a href="index.html">
🏆 League
</a>

<a href="register.html">
📝 Register
</a>

<a href="fixtures.html">
⚽ Fixtures
</a>

</div>


<button
class="admin-btn"
onclick="openLogin()">

🔐 Administrator

</button>


<br>


<div class="panel">

<select
id="leagueSelect"
onchange="changeLeague()">

<option>
Loading leagues...
</option>

</select>

</div>


<div class="stats">

<div class="stat">
<strong id="teamCount">0</strong>
<span>Teams</span>
</div>

<div class="stat">
<strong id="matchCount">0</strong>
<span>Matches</span>
</div>

<div class="stat">
<strong id="leader">-</strong>
<span>Leader</span>
</div>

<div class="stat">
<strong id="points">0</strong>
<span>Points</span>
</div>

</div>


<div class="panel">

<h2>🏆 League Standings</h2>

<div class="table-wrap">

<table>

<thead>

<tr>
<th>#</th>
<th>TEAM</th>
<th>P</th>
<th>W</th>
<th>D</th>
<th>L</th>
<th>GF</th>
<th>GA</th>
<th>GD</th>
<th>PTS</th>
</tr>

</thead>

<tbody id="standings">

</tbody>

</table>

</div>

</div>


<section id="adminArea">

<div class="panel">

<h2>🔐 Administrator</h2>

<button
class="danger"
onclick="logout()">

Logout

</button>

</div>


<div class="panel">

<h2>➕ Create League</h2>

<input
id="newLeague"
placeholder="League name">

<br><br>

<input
id="newSeason"
placeholder="Season e.g. Season 1">

<br><br>

<button
class="primary"
onclick="createLeague()">

Create League

</button>

</div>


<div class="panel">

<h2>📋 Registration Requests</h2>

<div id="registrations">

<div class="empty">
Loading...
</div>

</div>

</div>

</section>


</div>


<div
class="modal"
id="loginModal">

<div class="modal-box">

<h2>🔐 Admin Login</h2>

<input
id="email"
type="email"
placeholder="Administrator email">

<input
id="password"
type="password"
placeholder="Password"
onkeydown="if(event.key==='Enter')login()">

<button
class="primary"
style="width:100%"
onclick="login()">

Login

</button>

<br><br>

<button
class="secondary"
style="width:100%"
onclick="closeLogin()">

Cancel

</button>

<div
id="loginError"
class="message error">

</div>

</div>

</div>


<script>

const SUPABASE_URL =
"https://vhcfimwmoajnsxnpjyxa.supabase.co";

const SUPABASE_KEY =
"sb_publishable_WOw1puJqf0gBDrrEL-zXsg_aCcBgbJk";

const supabaseClient =
supabase.createClient(
SUPABASE_URL,
SUPABASE_KEY
);

let leagues=[];
let currentLeague=null;
let admin=false;


/* =========================
   LOAD
========================= */

async function load(){

const {data,error}=await supabaseClient
.from("leagues")
.select("*")
.order("id");

if(error){

console.error(error);
return;

}

leagues=data||[];

const select=
document.getElementById("leagueSelect");

select.innerHTML="";

if(!leagues.length){

select.innerHTML=
"<option>No leagues</option>";

return;

}

leagues.forEach(l=>{

const o=document.createElement("option");

o.value=l.id;

o.textContent=
`${l.name} — ${l.season}`;

select.appendChild(o);

});

if(!currentLeague)
currentLeague=leagues[0].id;

select.value=currentLeague;

await render();

}


/* =========================
   CHANGE LEAGUE
========================= */

function changeLeague(){

currentLeague=
Number(
document.getElementById(
"leagueSelect"
).value
);

render();

}


/* =========================
   RENDER
========================= */

async function render(){

const league=
leagues.find(
l=>Number(l.id)===Number(currentLeague)
);

if(!league)return;

const {data:teams}=await supabaseClient
.from("teams")
.select("*")
.eq("league_id",league.id)
.order("id");

const {data:matches}=await supabaseClient
.from("matches")
.select("*")
.eq("league_id",league.id);

teams=teams||[];
matches=matches||[];

document.getElementById(
"teamCount"
).textContent=teams.length;

document.getElementById(
"matchCount"
).textContent=
matches.filter(
m=>m.home_score!==null &&
m.away_score!==null
).length;

const table={};

teams.forEach(t=>{

table[t.id]={
...t,
p:0,w:0,d:0,l:0,
gf:0,ga:0,pts:0
};

});

matches.forEach(m=>{

if(
m.home_score===null ||
m.away_score===null
)return;

const h=table[m.home_id];
const a=table[m.away_id];

if(!h||!a)return;

h.p++;
a.p++;

h.gf+=m.home_score;
h.ga+=m.away_score;

a.gf+=m.away_score;
a.ga+=m.home_score;

if(m.home_score>m.away_score){

h.w++;
a.l++;
h.pts+=3;

}else if(m.home_score<m.away_score){

a.w++;
h.l++;
a.pts+=3;

}else{

h.d++;
a.d++;
h.pts++;
a.pts++;

}

});

const arr=
Object.values(table)
.sort((a,b)=>
b.pts-a.pts ||
(b.gf-b.ga)-(a.gf-a.ga) ||
b.gf-a.gf
);

const body=
document.getElementById(
"standings"
);

body.innerHTML="";

arr.forEach((t,i)=>{

const gd=t.gf-t.ga;

body.innerHTML+=`

<tr>

<td>${i+1}</td>

<td>${esc(t.name)}</td>

<td>${t.p}</td>

<td>${t.w}</td>

<td>${t.d}</td>

<td>${t.l}</td>

<td>${t.gf}</td>

<td>${t.ga}</td>

<td>${gd>0?"+":""}${gd}</td>

<td class="points">
${t.pts}
</td>

</tr>

`;

});

document.getElementById(
"leader"
).textContent=
arr.length?arr[0].name:"-";

document.getElementById(
"points"
).textContent=
arr.length?arr[0].pts:0;

if(admin)
loadRegistrations();

}


/* =========================
   ADMIN LOGIN
========================= */

function openLogin(){

document.getElementById(
"loginModal"
).style.display="flex";

}

function closeLogin(){

document.getElementById(
"loginModal"
).style.display="none";

}

async function login(){

const email=
document.getElementById(
"email"
).value.trim();

const password=
document.getElementById(
"password"
).value;

const {error}=
await supabaseClient.auth
.signInWithPassword({
email,
password
});

if(error){

const box=
document.getElementById(
"loginError"
);

box.textContent=
"Incorrect email or password.";

box.style.display="block";

return;

}

admin=true;

closeLogin();

document.getElementById(
"adminArea"
).style.display="block";

loadRegistrations();

}


/* =========================
   LOGOUT
========================= */

async function logout(){

await supabaseClient.auth.signOut();

admin=false;

document.getElementById(
"adminArea"
).style.display="none";

}


/* =====
async function createLeague(){

if(!admin)return;

const name=
document.getElementById(
"newLeague"
).value.trim();

const season=
document.getElementById(
"newSeason"
).value.trim()
||"Season 1";

if(!name){

alert("Enter a league name.");

return;

}

const {data,error}=
await supabaseClient
.from("leagues")
.insert({
name,
season
})
.select()
.single();

if(error){

alert(error.message);

return;

}

currentLeague=data.id;

document.getElementById(
"newLeague"
).value="";

document.getElementById(
"newSeason"
).value="";

await load();

}


/* =========================
   REGISTRATIONS
========================= */

async function loadRegistrations(){

const box=
document.getElementById(
"registrations"
);

const {data,error}=
await supabaseClient
.from("registrations")
.select(`
*,
leagues(name,season)
`)
.order(
"created_at",
{ascending:false}
);

if(error){

box.innerHTML=
`<div class="empty">
${esc(error.message)}
</div>`;

return;

}

const pending=
(data||[]).filter(
r=>r.status==="pending"
);

if(!pending.length){

box.innerHTML=
`<div class="empty">
No pending registrations.
</div>`;

return;

}

box.innerHTML="";

pending.forEach(r=>{

const div=
document.createElement("div");

div.className="pending";

div.innerHTML=`

<h3>
⚽ ${esc(r.team_name)}
</h3>

<p>

Player:
<b>${esc(r.player_name)}</b><br>

WhatsApp:
<b>${esc(r.whatsapp)}</b><br>

Beta Code:
<b>${esc(r.beta_code)}</b><br>

League:
<b>
${esc(
r.leagues?.name||"Unknown"
)}
</b>

</p>

<div class="actions">

<button
class="success"
onclick="approve(${r.id})">

✓ Approve

</button>

<button
class="danger"
onclick="reject(${r.id})">

✕ Reject

</button>

</div>

`;

box.appendChild(div);

});

}


/* =========================
   APPROVE
========================= */

async function approve(id){

if(!confirm(
"Approve this player and add the team to the league?"
))
return;

const {data,error}=
await supabaseClient.rpc(
"approve_registration",
{
p_registration_id:id
}
);

if(error){

alert(error.message);

return;

}


/* Automatically generate
   missing fixtures */

await generateFixtures(
data.league_id
);

alert(
"Registration approved. Team added and fixtures updated."
);

await load();

}


/* =========================
   REJECT
========================= */

async function reject(id){

if(!confirm(
"Reject this registration?"
))
return;

const {error}=
await supabaseClient
.from("registrations")
.update({
status:"rejected",
reviewed_at:new Date().toISOString()
})
.eq("id",id);

if(error){

alert(error.message);

return;

}

loadRegistrations();

}


/* =========================
   AUTO FIXTURES
========================= */

async function generateFixtures(
leagueId
){

const {data:teams,error}=
await supabaseClient
.from("teams")
.select("id")
.eq("league_id",leagueId)
.order("id");

if(error||!teams)
return;

if(teams.length<2)
return;


/* Existing fixtures */

const {data:existing}=
await supabaseClient
.from("matches")
.select(
"home_id,away_id"
)
.eq(
"league_id",
leagueId
);

const existingSet=
new Set(
(existing||[])
.map(m=>
`${m.home_id}-${m.away_id}`
)
);


/* Circle method */

let list=
teams.map(t=>t.id);

if(list.length%2!==0)
list.push(null);

const n=list.length;

const rounds=[];


/* First leg */

let rotating=[
...list
];

for(
let round=0;
round<n-1;
round++
){

const games=[];

for(
let i=0;
i<n/2;
i++
){

let a=
rotating[i];

let b=
rotating[n-1-i];

if(a!==null && b!==null){

games.push({
home:a,
away:b,
round
});

}

}

rounds.push(games);


/* Rotate */

rotating=[
rotating[0],
rotating[n-1],
...rotating.slice(1,n-1)
];

}


/* Second leg */

const allGames=[
...rounds
];

rounds.forEach(
(games,round)=>{

allGames.push(
games.map(g=>({

home:g.away,
away:g.home,
round:
round+n-1

}))
);

});


const rows=[];

allGames.forEach(
games=>{

games.forEach(g=>{

const key=
`${g.home}-${g.away}`;

if(existingSet.has(key))
return;

const date=
new Date();

date.setDate(
date.getDate()+
g.round*7
);

rows.push({

league_id:leagueId,

home_id:g.home,

away_id:g.away,

home_score:null,

away_score:null,

match_date:
date.toISOString()
.split("T")[0]

});

});

});


if(!rows.length)
return;

await supabaseClient
.from("matches")
.insert(rows);

}


/* =========================
   ESCAPE
========================= */

function esc(v){

return String(v??"")
.replace(/&/g,"&amp;")
.replace(/</g,"&lt;")
.replace(/>/g,"&gt;")
.replace(/"/g,"&quot;")
.replace(/'/g,"&#039;");

}


/* =========================
   AUTH CHECK
========================= */

async function checkAuth(){

const {data}=
await supabaseClient.auth
.getSession();

if(data.session){

admin=true;

document.getElementById(
"adminArea"
).style.display="block";

}

}


/* =========================
   START
========================= */

async function start(){

await checkAuth();

await load();

}

start();


/* =========================
   REALTIME
========================= */

supabaseClient
.channel("tdlm-main")
.on(
"postgres_changes",
{
event:"*",
schema:"public",
table:"teams"
},
()=>load()
)
.on(
"postgres_changes",
{
event:"*",
schema:"public",
table:"matches"
},
()=>load()
)
.on(
"postgres_changes",
{
event:"*",
schema:"public",
table:"registrations"
},
()=>{

if(admin)
loadRegistrations();

}
)
.subscribe();

</script>

</body>
</html>
