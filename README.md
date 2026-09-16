<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport"
content="width=device-width,
initial-scale=1.0,
maximum-scale=1.0,
user-scalable=no">

<meta name="theme-color" content="#020617">

<title>DLS 26 League Manager</title>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

<style>

*{
box-sizing:border-box;
margin:0;
padding:0;
-webkit-tap-highlight-color:transparent;
}

html,body{
width:100%;
min-height:100%;
font-family:Arial,sans-serif;
background:
radial-gradient(circle at top,#172554,#020617 60%);
color:white;
}

body{
min-height:100vh;
}

button,input,select{
font-family:Arial,sans-serif;
font-size:16px;
}

button{
cursor:pointer;
border:0;
}

input,select{
width:100%;
min-height:46px;
padding:11px;
border-radius:9px;
border:1px solid #334155;
background:#020617;
color:white;
outline:none;
}

input:focus,
select:focus{
border-color:#22c55e;
box-shadow:0 0 0 2px rgba(34,197,94,.1);
}

.hidden{
display:none!important;
}

.header{
position:sticky;
top:0;
z-index:20;
text-align:center;
padding:18px 12px 14px;
background:rgba(2,6,23,.96);
border-bottom:1px solid #1e3a8a;
backdrop-filter:blur(10px);
}

.logo{
font-size:27px;
font-weight:900;
user-select:none;
}

.logo span{
color:#22c55e;
}

.subtitle{
font-size:12px;
color:#94a3b8;
margin-top:4px;
}

.container{
width:100%;
max-width:1100px;
margin:auto;
padding:14px 12px 40px;
}

.tabs{
display:flex;
gap:8px;
overflow-x:auto;
margin-bottom:15px;
padding-bottom:5px;
scrollbar-width:none;
}

.tabs::-webkit-scrollbar{
display:none;
}

.tab{
flex-shrink:0;
padding:11px 15px;
min-height:44px;
border-radius:10px;
border:1px solid #334155;
background:#0f172a;
color:#cbd5e1;
font-weight:bold;
}

.tab.active{
background:#16a34a;
border-color:#22c55e;
color:white;
}

.card{
background:rgba(15,23,42,.92);
border:1px solid #1e293b;
border-radius:15px;
padding:14px;
margin-bottom:14px;
box-shadow:0 10px 30px rgba(0,0,0,.2);
overflow:hidden;
}

.card h2{
font-size:18px;
margin-bottom:12px;
}

.league-title{
font-size:clamp(21px,6vw,28px);
font-weight:900;
overflow-wrap:anywhere;
}

.season{
color:#94a3b8;
margin-top:5px;
}

.stats{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:8px;
margin-bottom:14px;
}

.stat{
background:#020617;
border:1px solid #1e293b;
border-radius:12px;
padding:13px 5px;
text-align:center;
overflow:hidden;
}

.stat-value{
font-size:20px;
font-weight:900;
color:#22c55e;
overflow:hidden;
text-overflow:ellipsis;
white-space:nowrap;
}

.stat-label{
font-size:10px;
color:#94a3b8;
margin-top:4px;
font-weight:bold;
}

.table-wrap{
width:100%;
overflow-x:auto;
border-radius:12px;
}

table{
width:100%;
min-width:560px;
border-collapse:collapse;
}

thead{
background:#020617;
}

th{
color:#4ade80;
font-size:12px;
font-weight:900;
padding:11px 7px;
border-bottom:2px solid #22c55e;
}

td{
padding:11px 7px;
border-bottom:1px solid #334155;
text-align:center;
white-space:nowrap;
}

td:nth-child(2){
text-align:left;
font-weight:800;
}

tbody tr:nth-child(even){
background:#111c31;
}

tbody tr:nth-child(odd){
background:#0f172a;
}

.top3{
background:#13251d!important;
}

.relegation{
background:#241619!important;
}

.result{
display:grid;
grid-template-columns:1fr auto 1fr;
align-items:center;
gap:8px;
padding:12px 3px;
border-bottom:1px solid #1e293b;
}

.team{
font-weight:bold;
font-size:13px;
overflow-wrap:anywhere;
}

.team.away{
text-align:right;
}

.score{
background:#020617;
border:1px solid #334155;
border-radius:8px;
padding:7px 10px;
font-weight:900;
min-width:60px;
text-align:center;
}

.date{
font-size:10px;
color:#64748b;
text-align:center;
margin-top:4px;
}

.status{
font-size:10px;
text-align:center;
margin-top:4px;
}

.played{
color:#4ade80;
}

.scheduled{
color:#facc15;
}

.btn{
padding:11px 15px;
min-height:44px;
border-radius:9px;
font-weight:bold;
margin-top:4px;
}

.green{
background:#16a34a;
color:white;
}

.blue{
background:#2563eb;
color:white;
}

.red{
background:#dc2626;
color:white;
}

.gray{
background:#334155;
color:white;
}

.form-group{
margin-bottom:12px;
}

label{
display:block;
font-size:12px;
color:#94a3b8;
margin-bottom:5px;
}

.form-grid{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:10px;
}

.admin-panel{
border-color:#166534;
background:rgba(5,46,22,.5);
}

.admin-title{
font-size:20px;
font-weight:900;
color:#4ade80;
margin-bottom:15px;
}

.team-admin{
display:flex;
justify-content:space-between;
align-items:center;
gap:10px;
padding:10px;
margin-bottom:7px;
background:#020617;
border:1px solid #1e293b;
border-radius:9px;
}

.team-admin-name{
flex:1;
min-width:0;
overflow-wrap:anywhere;
}

.small-btn{
padding:8px 11px;
min-height:38px;
border-radius:7px;
color:white;
font-size:12px;
}

.message{
padding:10px;
border-radius:9px;
margin-bottom:10px;
font-size:13px;
}

.error{
background:rgba(239,68,68,.15);
border:1px solid #7f1d1d;
color:#fca5a5;
}

.success{
background:rgba(34,197,94,.15);
border:1px solid #166534;
color:#86efac;
}

.empty{
text-align:center;
padding:25px 10px;
color:#64748b;
font-size:13px;
}

.loading{
text-align:center;
padding:40px;
color:#94a3b8;
}

.footer{
text-align:center;
padding:25px;
color:#475569;
font-size:11px;
}

.modal{
position:fixed;
inset:0;
z-index:100;
display:flex;
align-items:center;
justify-content:center;
padding:15px;
background:rgba(0,0,0,.8);
}

.modal-box{
width:100%;
max-width:420px;
background:#0f172a;
border:1px solid #334155;
border-radius:16px;
padding:20px;
}

.modal-box h2{
margin-bottom:15px;
}

.modal-buttons{
display:flex;
gap:8px;
margin-top:10px;
}

.modal-buttons button{
flex:1;
}

.fixture{
padding:12px 3px;
border-bottom:1px solid #1e293b;
}

.fixture:last-child{
border-bottom:0;
}

.fixture-teams{
display:grid;
grid-template-columns:1fr auto 1fr;
align-items:center;
gap:8px;
}

.fixture-team{
font-weight:bold;
font-size:13px;
}

.fixture-away{
text-align:right;
}

.vs{
color:#64748b;
font-weight:bold;
}

.fixture-date{
text-align:center;
font-size:10px;
color:#94a3b8;
margin-top:5px;
}

@media(min-width:601px){

.stats{
grid-template-columns:repeat(4,1fr);
}

}

</style>

</head>

<body>

<header class="header">

<div
class="logo"
id="secretAdminTrigger">
⚽ DLS 26 <span>LEAGUE</span>
</div>

<div class="subtitle">
League Manager • TRIXARQ
</div>

</header>


<main class="container">

<div id="loading" class="loading">
Loading leagues...
</div>


<div id="app" class="hidden">


<!-- LEAGUE SELECTOR -->

<div
class="tabs"
id="leagueTabs">
</div>


<!-- PAGE NAVIGATION -->

<div class="tabs">

<button
class="tab active"
id="overviewTab"
onclick="showPage('overview')">

📊 Overview

</button>

<button
class="tab"
id="fixturesTab"
onclick="showPage('fixtures')">

📅 Fixtures

</button>

<button
class="tab"
id="resultsTab"
onclick="showPage('results')">

⚽ Results

</button>

</div>


<!-- ADMIN -->

<section
id="adminPanel"
class="card admin-panel hidden">

<div class="admin-title">
👑 Administrator Panel
</div>

<div id="adminMessage"></div>


<div class="card">

<h2>🏆 Create League</h2>

<div class="form-group">

<label>League Name</label>

<input
id="leagueName"
placeholder="DLS Premier League">

</div>

<div class="form-group">

<label>Season</label>

<input
id="leagueSeason"
value="2026">

</div>

<button
class="btn green"
onclick="createLeague()">

➕ Create League

</button>

</div>


<div class="card">

<h2>👥 Add Team</h2>

<div class="form-group">

<label>Team Name</label>

<input
id="teamName"
placeholder="Team name">

</div>

<div class="form-group">

<label>Manager</label>

<input
id="managerName"
placeholder="Manager name">

</div>

<button
class="btn blue"
onclick="addTeam()">

➕ Add Team

</button>

</div>


<div class="card">

<h2>📅 Add Fixture</h2>

<div class="form-group">

<label>Home Team</label>

<select id="fixtureHome"></select>

</div>

<div class="form-group">

<label>Away Team</label>

<select id="fixtureAway"></select>

</div>

<div class="form-group">

<label>Match Date</label>

<input
id="fixtureDate"
type="date">

</div>

<button
class="btn blue"
onclick="addFixture()">

📅 Save Fixture

</button>

</div>


<div class="card">

<h2>⚽ Enter Result</h2>

<div class="form-group">

<label>Fixture</label>

<select id="resultMatch"></select>

</div>

<div class="form-grid">

<div class="form-group">

<label>Home Score</label>

<input
id="homeScore"
type="number"
min="0"
value="0">

</div>

<div class="form-group">

<label>Away Score</label>

<input
id="awayScore"
type="number"
min="0"
value="0">

</div>

</div>

<button
class="btn green"
onclick="saveResult()">

⚽ Save Result

</button>

</div>


<div class="card">

<h2>👥 Current Teams</h2>

<div id="adminTeams"></div>

</div>


<div class="card">

<h2>🗑️ League Management</h2>

<button
class="btn red"
onclick="deleteCurrentLeague()">

Delete Current League

</button>

<br>

<button
class="btn red"
onclick="clearEverything()">

Delete ALL Leagues

</button>

<br>

<button
class="btn gray"
onclick="logout()">

🚪 Logout

</button>

</div>

</section>


<!-- OVERVIEW -->

<section id="overviewPage">

<div class="card">

<div
class="league-title"
id="leagueTitle">
No League
</div>

<div
class="season"
id="leagueSeasonDisplay">
</div>

</div>


<div class="stats">

<div class="stat">

<div
class="stat-value"
id="teamCount">
0
</div>

<div class="stat-label">
TEAMS
</div>

</div>

<div class="stat">

<div
class="stat-value"
id="matchCount">
0
</div>

<div class="stat-label">
MATCHES
</div>

</div>

<div class="stat">

<div
class="stat-value"
id="leaderName">
-
</div>

<div class="stat-label">
LEADER
</div>

</div>

<div class="stat">

<div
class="stat-value"
id="leaderPoints">
0
</div>

<div class="stat-label">
POINTS
</div>

</div>

</div>


<div class="card">

<h2>📊 League Table</h2>

<div class="table-wrap">

<table>

<thead>

<tr>

<th>#</th>
<th>Team</th>
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

<tbody id="standingsBody"></tbody>

</table>

</div>

</div>

</section>


<!-- FIXTURES -->

<section
id="fixturesPage"
class="hidden">

<div class="card">

<h2>📅 Fixtures</h2>

<div id="fixturesList"></div>

</div>

</section>


<!-- RESULTS -->

<section
id="resultsPage"
class="hidden">

<div class="card">

<h2>⚽ Results</h2>

<div id="resultsList"></div>

</div>

</section>


</div>

</main>


<footer class="footer">

DLS 26 League Manager • TRIXARQ

</footer>


<!-- LOGIN MODAL -->

<div
id="loginModal"
class="modal hidden">

<div class="modal-box">

<h2>🔐 Administrator Login</h2>

<div id="loginError"></div>

<div class="form-group">

<label>Email</label>

<input
id="loginEmail"
type="email"
autocomplete="username"
placeholder="Admin email">

</div>

<div class="form-group">

<label>Password</label>

<input
id="loginPassword"
type="password"
autocomplete="current-password"
placeholder="Password">

</div>

<div class="modal-buttons">

<button
class="btn green"
onclick="login()">

Login

</button>

<button
class="btn gray"
onclick="closeLogin()">

Cancel

</button>

</div>

</div>

</div>


<script>

/* =========================================================
SUPABASE
========================================================= */

const SUPABASE_URL =
"https://vhcfimwmoajnsxnpjyxa.supabase.co";

const SUPABASE_KEY =
"sb_publishable_WOw1puJqf0gBDrrEL-zXsg_aCcBgbJk";

const supabaseClient =
window.supabase.createClient(
SUPABASE_URL,
SUPABASE_KEY
);


/* =========================================================
STATE
========================================================= */

let database={
leagues:[]
};

let currentLeagueId=null;

let adminLoggedIn=false;


/* =========================================================
INITIALIZE
========================================================= */

document.addEventListener(
"DOMContentLoaded",
async()=>{

const today=
new Date()
.toISOString()
.split("T")[0];

document.getElementById(
"fixtureDate"
).value=today;

await checkSession();

await loadDatabase();

subscribeRealtime();

}
);


/* =========================================================
HIDDEN ADMIN ACCESS
========================================================= */

let logoTaps=0;
let tapTimer=null;

document.getElementById(
"secretAdminTrigger"
).addEventListener(
"click",
()=>{

logoTaps++;

clearTimeout(tapTimer);

tapTimer=setTimeout(
()=>{
logoTaps=0;
},
1200
);

if(logoTaps>=5){

logoTaps=0;

openLogin();

}

}
);


/* DESKTOP SHORTCUT */

document.addEventListener(
"keydown",
e=>{

if(
e.ctrlKey &&
e.shiftKey &&
e.key.toLowerCase()==="a"
){

e.preventDefault();

openLogin();

}

}
);


/* =========================================================
AUTH
========================================================= */

async function checkSession(){

const {
data:{
session
}
}=await supabaseClient.auth.getSession();

if(!session){

adminLoggedIn=false;

updateAdminUI();

return;

}

await checkAdmin(
session.user.id
);

}


async function checkAdmin(userId){

const {
data,
error
}=
await supabaseClient
.from("admin_users")
.select("id")
.eq("id",userId)
.maybeSingle();

if(error){

console.error(error);

adminLoggedIn=false;

updateAdminUI();

return;

}

adminLoggedIn=!!data;

updateAdminUI();

}


/* =========================================================
LOGIN
========================================================= */

async function login(){

const email=
document.getElementById(
"loginEmail"
).value.trim();

const password=
document.getElementById(
"loginPassword"
).value;

const errorBox=
document.getElementById(
"loginError"
);

errorBox.innerHTML="";

if(!email||!password){

errorBox.innerHTML=
`<div class="message error">
Enter email and password.
</div>`;

return;

}

const {
data,
error
}=
await supabaseClient.auth
.signInWithPassword({
email,
password
});

if(error){

errorBox.innerHTML=
`<div class="message error">
${escapeHTML(error.message)}
</div>`;

return;

}

const {
data:admin,
error:adminError
}=
await supabaseClient
.from("admin_users")
.select("id")
.eq("id",data.user.id)
.maybeSingle();

if(adminError||!admin){

await supabaseClient.auth.signOut();

errorBox.innerHTML=
`<div class="message error">
This account is not an administrator.
</div>`;

return;

}

adminLoggedIn=true;

closeLogin();

updateAdminUI();

showAdminMessage(
"Login successful.",
true
);

}


/* =========================================================
LOGOUT
========================================================= */

async function logout(){

await supabaseClient.auth.signOut();

adminLoggedIn=false;

updateAdminUI();

}


/* =========================================================
AUTH STATE
========================================================= */

supabaseClient.auth.onAuthStateChange(
async(event,session)=>{

if(!session){

adminLoggedIn=false;

updateAdminUI();

return;

}

await checkAdmin(
session.user.id
);

}
);


/* =========================================================
LOGIN MODAL
========================================================= */

function openLogin(){

if(adminLoggedIn){

document.getElementById(
"adminPanel"
).classList.remove(
"hidden"
);

document.getElementById(
"adminPanel"
).scrollIntoView({
behavior:"smooth"
});

return;

}

document.getElementById(
"loginModal"
).classList.remove(
"hidden"
);

document.getElementById(
"loginEmail"
).focus();

}


function closeLogin(){

document.getElementById(
"loginModal"
).classList.add(
"hidden"
);

document.getElementById(
"loginError"
).innerHTML="";

}


/* =========================================================
ADMIN UI
========================================================= */

function updateAdminUI(){

const panel=
document.getElementById(
"adminPanel"
);

if(adminLoggedIn){

panel.classList.remove(
"hidden"
);

}else{

panel.classList.add(
"hidden"
);

}

}


/* =========================================================
LOAD DATABASE
========================================================= */

async function loadDatabase(){

document.getElementById(
"loading"
).classList.remove(
"hidden"
);

document.getElementById(
"app"
).classList.add(
"hidden"
);

const [
leaguesResponse,
teamsResponse,
matchesResponse
]=await Promise.all([

supabaseClient
.from("leagues")
.select("*")
.order("created_at",{ascending:true}),

supabaseClient
.from("teams")
.select("*")
.order("created_at",{ascending:true}),

supabaseClient
.from("matches")
.select("*")
.order("match_date",{ascending:true})

]);

if(
leaguesResponse.error||
teamsResponse.error||
matchesResponse.error
){

showFatalError(
leaguesResponse.error||
teamsResponse.error||
matchesResponse.error
);

return;

}

const leagues=
leaguesResponse.data||[];

const teams=
teamsResponse.data||[];

const matches=
matchesResponse.data||[];

database.leagues=
leagues.map(
league=>({

id:Number(league.id),

name:league.name,

season:league.season,

teams:teams
.filter(
team=>
Number(team.league_id)===
Number(league.id)
)
.map(
team=>({

id:Number(team.id),

name:team.name,

manager:team.manager||""

})
),

matches:matches
.filter(
match=>
Number(match.league_id)===
Number(league.id)
)
.map(
match=>({

id:Number(match.id),

homeId:Number(match.home_id),

awayId:Number(match.away_id),

homeScore:
match.home_score===null
?null
:Number(match.home_score),

awayScore:
match.away_score===null
?null
:Number(match.away_score),

date:match.match_date,

status:match.status

})
)

})
);

if(
currentLeagueId===null||
!database.leagues.some(
l=>l.id===currentLeagueId
)
){

currentLeagueId=
database.leagues.length
?database.leagues[0].id
:null;

}

document.getElementById(
"loading"
).classList.add(
"hidden"
);

document.getElementById(
"app"
).classList.remove(
"hidden"
);

render();

}


/* =========================================================
REALTIME
========================================================= */

function subscribeRealtime(){

supabaseClient
.channel("dls-live")

.on(
"postgres_changes",
{
event:"*",
schema:"public",
table:"leagues"
},
()=>loadDatabase()
)

.on(
"postgres_changes",
{
event:"*",
schema:"public",
table:"teams"
},
()=>loadDatabase()
)

.on(
"postgres_changes",
{
event:"*",
schema:"public",
table:"matches"
},
()=>loadDatabase()
)

.subscribe();

}


/* =========================================================
RENDER
========================================================= */

function render(){

renderLeagueTabs();

renderCurrentLeague();

renderAdmin();

}


/* =========================================================
LEAGUE TABS
========================================================= */

function renderLeagueTabs(){

const tabs=
document.getElementById(
"leagueTabs"
);

tabs.innerHTML="";

if(!database.leagues.length){

tabs.innerHTML=
`<div class="empty">
No leagues created yet.
</div>`;

return;

}

database.leagues.forEach(
league=>{

const button=
document.createElement(
"button"
);

button.className=
"tab"+
(
league.id===currentLeagueId
?" active"
:""
);

button.textContent=
league.name;

button.onclick=()=>{

currentLeagueId=
league.id;

render();

};

tabs.appendChild(button);

}
);

}


/* =========================================================
CURRENT LEAGUE
========================================================= */

function getCurrentLeague(){

return database.leagues.find(
league=>
Number(league.id)===
Number(currentLeagueId)
);

}


/* =========================================================
CURRENT LEAGUE RENDER
========================================================= */

function renderCurrentLeague(){

const league=
getCurrentLeague();

if(!league){

document.getElementById(
"leagueTitle"
).textContent=
"No League";

document.getElementById(
"leagueSeasonDisplay"
).textContent="";

document.getElementById(
"teamCount"
).textContent="0";

document.getElementById(
"matchCount"
).textContent="0";

document.getElementById(
"leaderName"
).textContent="-";

document.getElementById(
"leaderPoints"
).textContent="0";

document.getElementById(
"standingsBody"
).innerHTML=
`<tr>
<td colspan="10">
<div class="empty">
No teams registered.
</div>
</td>
</tr>`;

document.getElementById(
"fixturesList"
).innerHTML=
`<div class="empty">
No fixtures.
</div>`;

document.getElementById(
"resultsList"
).innerHTML=
`<div class="empty">
No results.
</div>`;

updateSelectors();

return;

}

document.getElementById(
"leagueTitle"
).textContent=
league.name;

document.getElementById(
"leagueSeasonDisplay"
).textContent=
"Season "+league.season;

document.getElementById(
"teamCount"
).textContent=
league.teams.length;

document.getElementById(
"matchCount"
).textContent=
league.matches.length;

const standings=
calculateStandings(league);

if(standings.length){

document.getElementById(
"leaderName"
).textContent=
standings[0].name;

document.getElementById(
"leaderPoints"
).textContent=
standings[0].pts;

}

renderStandings(standings);

renderFixtures(league);

renderResults(league);

updateSelectors();

}


/* =========================================================
STANDINGS
========================================================= */

function calculateStandings(league){

const table={};

league.teams.forEach(
team=>{

table[team.id]={
id:team.id,
name:team.name,
p:0,
w:0,
d:0,
l:0,
gf:0,
ga:0,
gd:0,
pts:0
};

}
);

league.matches
.filter(
match=>
match.status==="played"
)
.forEach(
match=>{

const home=
table[match.homeId];

const away=
table[match.awayId];

if(!home||!away)
return;

const hs=
Number(match.homeScore);

const as=
Number(match.awayScore);

home.p++;
away.p++;

home.gf+=hs;
home.ga+=as;

away.gf+=as;
away.ga+=hs;

if(hs>as){

home.w++;
away.l++;
home.pts+=3;

}else if(hs<as){

away.w++;
home.l++;
away.pts+=3;

}else{

home.d++;
away.d++;
home.pts++;
away.pts++;

}

}
);

Object.values(table)
.forEach(
team=>{
team.gd=
team.gf-team.ga;
}
);

return Object.values(table)
.sort(
(a,b)=>{

if(b.pts!==a.pts)
return b.pts-a.pts;

if(b.gd!==a.gd)
return b.gd-a.gd;

if(b.gf!==a.gf)
return b.gf-a.gf;

return a.name.localeCompare(b.name);

}
);

}


/* =========================================================
RENDER STANDINGS
========================================================= */

function renderStandings(
standings
){

const body=
document.getElementById(
"standingsBody"
);

body.innerHTML="";

if(!standings.length){

body.innerHTML=
`<tr>
<td colspan="10">
<div class="empty">
No teams registered.
</div>
</td>
</tr>`;

return;

}

standings.forEach(
(team,index)=>{

const row=
document.createElement("tr");

if(index<3)
row.classList.add("top3");

if(
standings.length>=4&&
index>=standings.length-3
)
row.classList.add(
"relegation"
);

let pos=index+1;

if(index===0)pos="🥇";
if(index===1)pos="🥈";
if(index===2)pos="🥉";

row.innerHTML=`

<td>${pos}</td>

<td>
${escapeHTML(team.name)}
</td>

<td>${team.p}</td>
<td>${team.w}</td>
<td>${team.d}</td>
<td>${team.l}</td>
<td>${team.gf}</td>
<td>${team.ga}</td>
<td>${team.gd}</td>

<td>
<strong>${team.pts}</strong>
</td>

`;

body.appendChild(row);

}
);

}


/* =========================================================
FIXTURES
========================================================= */

function renderFixtures(league){

const list=
document.getElementById(
"fixturesList"
);

list.innerHTML="";

const fixtures=
league.matches
.filter(
match=>
match.status==="scheduled"
)
.sort(
(a,b)=>
new Date(a.date)-
new Date(b.date)
);

if(!fixtures.length){

list.innerHTML=
`<div class="empty">
No upcoming fixtures.
</div>`;

return;

}

fixtures.forEach(
match=>{

const home=
league.teams.find(
t=>t.id===match.homeId
);

const away=
league.teams.find(
t=>t.id===match.awayId
);

if(!home||!away)
return;

const item=
document.createElement("div");

item.className="fixture";

item.innerHTML=`

<div class="fixture-teams">

<div class="fixture-team">

${escapeHTML(home.name)}

</div>

<div class="vs">
VS
</div>

<div class="fixture-team fixture-away">

${escapeHTML(away.name)}

</div>

</div>

<div class="fixture-date">

📅 ${escapeHTML(match.date)}

</div>

`;

list.appendChild(item);

}
);

}


/* =========================================================
RESULTS
========================================================= */

function renderResults(league){

const list=
document.getElementById(
"resultsList"
);

list.innerHTML="";

const results=
league.matches
.filter(
match=>
match.status==="played"
)
.sort(
(a,b)=>
new Date(b.date)-
new Date(a.date)
);

if(!results.length){

list.innerHTML=
`<div class="empty">
No results yet.
</div>`;

return;

}

results.forEach(
match=>{

const home=
league.teams.find(
t=>t.id===match.homeId
);

const away=
league.teams.find(
t=>t.id===match.awayId
);

if(!home||!away)
return;

const item=
document.createElement("div");

item.className="result";

item.innerHTML=`

<div class="team">

${escapeHTML(home.name)}

</div>

<div>

<div class="score">

${match.homeScore}
-
${match.awayScore}

</div>

<div class="date">

${escapeHTML(match.date)}

</div>

</div>

<div class="team away">

${escapeHTML(away.name)}

</div>

`;

list.appendChild(item);

}
);

}


/* =========================================================
PAGE SWITCHING
========================================================= */

function showPage(page){

const pages={
overview:
document.getElementById(
"overviewPage"
),

fixtures:
document.getElementById(
"fixturesPage"
),

results:
document.getElementById(
"resultsPage"
)
};

Object.values(pages)
.forEach(
p=>p.classList.add("hidden")
);

pages[page].classList.remove(
"hidden"
);

document.getElementById(
"overviewTab"
).classList.toggle(
"active",
page==="overview"
);

document.getElementById(
"fixturesTab"
).classList.toggle(
"active",
page==="fixtures"
);

document.getElementById(
"resultsTab"
).classList.toggle(
"active",
page==="results"
);

}


/* =========================================================
ADMIN RENDER
========================================================= */

function renderAdmin(){

if(!adminLoggedIn)
return;

const league=
getCurrentLeague();

const list=
document.getElementById(
"adminTeams"
);

list.innerHTML="";

if(!league){

list.innerHTML=
`<div class="empty">
Select a league.
</div>`;

return;

}

if(!league.teams.length){

list.innerHTML=
`<div class="empty">
No teams registered.
</div>`;

return;

}

league.teams.forEach(
team=>{

const item=
document.createElement("div");

item.className=
"team-admin";

item.innerHTML=`

<div class="team-admin-name">

<strong>
${escapeHTML(team.name)}
</strong>

<br>

<small style="color:#64748b">

${escapeHTML(
team.manager||
"No manager"
)}

</small>

</div>

<button
class="small-btn red"
onclick="removeTeam(${team.id})">

Remove

</button>

`;

list.appendChild(item);

}
);

}


/* =========================================================
SELECTORS
========================================================= */

function updateSelectors(){

const fixtureHome=
document.getElementById(
"fixtureHome"
);

const fixtureAway=
document.getElementById(
"fixtureAway"
);

const resultMatch=
document.getElementById(
"resultMatch"
);

fixtureHome.innerHTML=
`<option value="">
Select home team
</option>`;

fixtureAway.innerHTML=
`<option value="">
Select away team
</option>`;

resultMatch.innerHTML=
`<option value="">
Select fixture
</option>`;

const league=
getCurrentLeague();

if(!league)
return;

league.teams.forEach(
team=>{

fixtureHome.innerHTML+=
`<option value="${team.id}">
${escapeHTML(team.name)}
</option>`;

fixtureAway.innerHTML+=
`<option value="${team.id}">
${escapeHTML(team.name)}
</option>`;

}
);

league.matches
.filter(
m=>m.status==="scheduled"
)
.forEach(
match=>{

const home=
league.teams.find(
t=>t.id===match.homeId
);

const away=
league.teams.find(
t=>t.id===match.awayId
);

if(!home||!away)
return;

resultMatch.innerHTML+=
`<option value="${match.id}">
${escapeHTML(home.name)}
 vs
 ${escapeHTML(away.name)}
 — ${escapeHTML(match.date)}
</option>`;

}
);

}


/* =========================================================
CREATE LEAGUE
========================================================= */

async function createLeague(){

if(!requireAdmin())
return;

const name=
document.getElementById(
"leagueName"
).value.trim();

const season=
document.getElementById(
"leagueSeason"
).value.trim()||
"2026";

if(!name){

showAdminMessage(
"Enter a league name.",
false
);

return;

}

const {
data,
error
}=
await supabaseClient
.from("leagues")
.insert({
name,
season
})
.select()
.single();

if(error){

showAdminMessage(
error.message,
false
);

return;

}

currentLeagueId=
Number(data.id);

document.getElementById(
"leagueName"
).value="";

showAdminMessage(
"League created successfully.",
true
);

await loadDatabase();

}


/* =========================================================
ADD TEAM
========================================================= */

async function addTeam(){

if(!requireAdmin())
return;

const league=
getCurrentLeague();

if(!league){

showAdminMessage(
"Select a league first.",
false
);

return;

}

const name=
document.getElementById(
"teamName"
).value.trim();

const manager=
document.getElementById(
"managerName"
).value.trim();

if(!name){

showAdminMessage(
"Enter a team name.",
false
);

return;

}

const {
error
}=
await supabaseClient
.from("teams")
.insert({
league_id:league.id,
name,
manager:manager||null
});

if(error){

showAdminMessage(
error.message,
false
);

return;

}

document.getElementById(
"teamName"
).value="";

document.getElementById(
"managerName"
).value="";

showAdminMessage(
"Team added.",
true
);

await loadDatabase();

}


/* =========================================================
ADD FIXTURE
========================================================= */

async function addFixture(){

if(!requireAdmin())
return;

const league=
getCurrentLeague();

if(!league){

showAdminMessage(
"Select a league.",
false
);

return;

}

const homeId=
Number(
document.getElementById(
"fixtureHome"
).value
);

const awayId=
Number(
document.getElementById(
"fixtureAway"
).value
);

const date=
document.getElementById(
"fixtureDate"
).value;

if(!homeId||!awayId){

showAdminMessage(
"Select both teams.",
false
);

return;

}

if(homeId===awayId){

showAdminMessage(
"A team cannot play itself.",
false
);

return;

}

if(!date){

showAdminMessage(
"Select a match date.",
false
);

return;

}

const {
error
}=
await supabaseClient
.from("matches")
.insert({

league_id:league.id,

home_id:homeId,

away_id:awayId,

home_score:null,

away_score:null,

match_date:date,

status:"scheduled"

});

if(error){

showAdminMessage(
error.message,
false
);

return;

}

showAdminMessage(
"Fixture added successfully.",
true
);

await loadDatabase();

}


/* =========================================================
SAVE RESULT
========================================================= */

async function saveResult(){

if(!requireAdmin())
return;

const matchId=
Number(
document.getElementById(
"resultMatch"
).value
);

const homeScore=
Number(
document.getElementById(
"homeScore"
).value
);

const awayScore=
Number(
document.getElementById(
"awayScore"
).value
);

if(!matchId){

showAdminMessage(
"Select a fixture.",
false
);

return;

}

if(
!Number.isInteger(homeScore)||
homeScore<0||
!Number.isInteger(awayScore)||
awayScore<0
){

showAdminMessage(
"Enter valid scores.",
false
);

return;

}

const {
error
}=
await supabaseClient
.from("matches")
.update({

home_score:homeScore,

away_score:awayScore,

status:"played"

})
.eq("id",matchId);

if(error){

showAdminMessage(
error.message,
false
);

return;

}

document.getElementById(
"homeScore"
).value="0";

document.getElementById(
"awayScore"
).value="0";

showAdminMessage(
"Result saved successfully.",
true
);

await loadDatabase();

}


/* =========================================================
REMOVE TEAM
========================================================= */

async function removeTeam(teamId){

if(!requireAdmin())
return;

const league=
getCurrentLeague();

if(!league)
return;

const team=
league.teams.find(
t=>t.id===Number(teamId)
);

if(!team)
return;

if(
!confirm(
"Remove "+team.name+
"?\n\nAll matches involving this team will also be deleted."
)
)
return;

const {
error
}=
await supabaseClient
.from("teams")
.delete()
.eq("id",teamId);

if(error){

showAdminMessage(
error.message,
false
);

return;

}

showAdminMessage(
"Team removed.",
true
);

await loadDatabase();

}


/* =========================================================
DELETE CURRENT LEAGUE
========================================================= */

async function deleteCurrentLeague(){

if(!requireAdmin())
return;

const league=
getCurrentLeague();

if(!league)
return;

if(
!confirm(
"DELETE "+league.name+
"?\n\nAll teams, fixtures and results will be deleted."
)
)
return;

const {
error
}=
await supabaseClient
.from("leagues")
.delete()
.eq("id",league.id);

if(error){

showAdminMessage(
error.message,
false
);

return;

}

currentLeagueId=null;

showAdminMessage(
"League deleted.",
true
);

await loadDatabase();

}


/* =========================================================
DELETE EVERYTHING
========================================================= */

async function clearEverything(){

if(!requireAdmin())
return;

if(
!confirm(
"WARNING!\n\n"+
"This will permanently delete ALL leagues, teams, fixtures and results.\n\n"+
"Continue?"
)
)
return;

const {
error
}=
await supabaseClient
.from("leagues")
.delete()
.gte("id",0);

if(error){

showAdminMessage(
error.message,
false
);

return;

}

currentLeagueId=null;

showAdminMessage(
"All league data deleted.",
true
);

await loadDatabase();

}


/* =========================================================
REQUIRE ADMIN
========================================================= */

function requireAdmin(){

if(!adminLoggedIn){

openLogin();

return false;

}

return true;

}


/* =========================================================
ADMIN MESSAGE
========================================================= */

function showAdminMessage(
message,
success
){

const box=
document.getElementById(
"adminMessage"
);

box.innerHTML=
`<div class="message ${
success?"success":"error"
}">
${escapeHTML(message)}
</div>`;

setTimeout(
()=>{
box.innerHTML="";
},
5000
);

}


/* =========================================================
ERROR
========================================================= */

function showFatalError(error){

document.getElementById(
"loading"
).innerHTML=
`<div class="message error">

<strong>
Database Error
</strong>

<br><br>

${escapeHTML(
error?.message||
"Unknown error"
)}

</div>`;

}


/* =========================================================
ESCAPE HTML
========================================================= */

function escapeHTML(value){

return String(value??"")
.replace(/&/g,"&amp;")
.replace(/</g,"&lt;")
.replace(/>/g,"&gt;")
.replace(/"/g,"&quot;")
.replace(/'/g,"&#039;");

}

</script>

</body>
</html>
