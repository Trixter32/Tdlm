<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width,
               initial-scale=1.0,
               maximum-scale=1.0,
               minimum-scale=1.0,
               user-scalable=no,
               viewport-fit=cover">

<meta name="theme-color" content="#020617">

<title>DLS 26 League Manager</title>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

<style>

/* =========================================================
   GLOBAL MOBILE RESET
========================================================= */

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    -webkit-tap-highlight-color: transparent;
}

html {
    width: 100%;
    min-height: 100%;
    overflow-x: hidden;

    /* Prevent text auto resizing */
    -webkit-text-size-adjust: 100%;
    text-size-adjust: 100%;

    touch-action: manipulation;
}

body {
    width: 100%;
    min-height: 100vh;
    min-height: 100dvh;

    overflow-x: hidden;

    font-family: Arial, sans-serif;

    background:
        radial-gradient(
            circle at top,
            #172554 0%,
            #020617 55%
        );

    color: #fff;

    -webkit-text-size-adjust: 100%;
    text-size-adjust: 100%;

    touch-action: manipulation;
}

/* Prevent long text from expanding page */

img,
video {
    max-width: 100%;
    height: auto;
}

/* =========================================================
   FORM CONTROLS
========================================================= */

button,
input,
select {
    font-family: Arial, sans-serif;
    font-size: 16px;
}

button {
    cursor: pointer;
    touch-action: manipulation;
    -webkit-appearance: none;
    appearance: none;
}

input,
select {
    -webkit-appearance: none;
    appearance: none;
}

/* =========================================================
   HEADER
========================================================= */

.header {
    width: 100%;

    padding:
        calc(14px + env(safe-area-inset-top))
        14px
        14px;

    text-align: center;

    background: rgba(2, 6, 23, .96);

    border-bottom: 1px solid #1e3a8a;

    position: sticky;
    top: 0;

    z-index: 20;

    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
}

.logo {
    font-size: clamp(22px, 7vw, 28px);
    font-weight: 900;

    white-space: nowrap;
}

.logo span {
    color: #22c55e;
}

.subtitle {
    color: #94a3b8;
    font-size: 12px;
    margin-top: 4px;
}

.admin-btn {
    margin-top: 11px;

    background: #2563eb;
    color: white;

    border: none;

    padding: 11px 18px;

    min-height: 44px;

    border-radius: 10px;

    font-weight: bold;

    box-shadow:
        0 5px 15px rgba(37,99,235,.2);
}

.admin-btn:active {
    transform: scale(.97);
}

/* =========================================================
   MAIN CONTAINER
========================================================= */

.container {
    width: 100%;
    max-width: 1100px;

    margin: auto;

    padding:
        14px
        12px
        calc(30px + env(safe-area-inset-bottom));
}

/* =========================================================
   TABS
========================================================= */

.tabs {
    display: flex;

    gap: 8px;

    width: 100%;

    overflow-x: auto;
    overflow-y: hidden;

    margin-bottom: 15px;

    padding-bottom: 5px;

    scrollbar-width: none;

    -webkit-overflow-scrolling: touch;
}

.tabs::-webkit-scrollbar {
    display: none;
}

.tab {
    flex-shrink: 0;

    border: 1px solid #334155;

    background: #0f172a;

    color: #cbd5e1;

    padding: 11px 15px;

    min-height: 44px;

    border-radius: 10px;

    font-size: 14px;

    font-weight: bold;

    white-space: nowrap;
}

.tab:active {
    transform: scale(.97);
}

.tab.active {
    background: #16a34a;

    border-color: #22c55e;

    color: white;

    box-shadow:
        0 0 12px rgba(34,197,94,.18);
}

/* =========================================================
   CARDS
========================================================= */

.card {
    width: 100%;

    background: rgba(15, 23, 42, .90);

    border: 1px solid #1e293b;

    border-radius: 15px;

    padding: 14px;

    margin-bottom: 14px;

    box-shadow:
        0 10px 30px rgba(0,0,0,.20);

    overflow: hidden;
}

.card h2 {
    font-size: 18px;
    margin-bottom: 12px;
}

.league-title {
    font-size: clamp(21px, 6vw, 28px);

    font-weight: 900;

    overflow-wrap: anywhere;
}

.season {
    color: #94a3b8;

    margin-top: 4px;

    font-size: 14px;
}

/* =========================================================
   STAT CARDS
========================================================= */

.stats {
    display: grid;

    grid-template-columns: repeat(2, 1fr);

    gap: 8px;

    margin-bottom: 14px;
}

.stat {
    min-width: 0;

    background: #020617;

    border: 1px solid #1e293b;

    border-radius: 12px;

    padding: 13px 5px;

    text-align: center;

    overflow: hidden;
}

.stat-value {
    font-size: clamp(18px, 5vw, 22px);

    font-weight: 900;

    color: #22c55e;

    overflow: hidden;

    text-overflow: ellipsis;

    white-space: nowrap;
}

.stat-label {
    color: #94a3b8;

    font-size: 10px;

    margin-top: 4px;

    font-weight: bold;
}

/* =========================================================
   STANDINGS TABLE - CHROME SAFE
========================================================= */

.table-wrap {
    width: 100%;
    overflow-x: auto;
    overflow-y: hidden;
    border-radius: 12px;
    -webkit-overflow-scrolling: touch;
}

table {
    width: 100%;
    min-width: 560px;
    border-collapse: collapse;
    background: #0f172a !important;
    color: #f8fafc !important;
}

thead,
thead tr,
thead th {
    background: #020617 !important;
    color: #4ade80 !important;
}

th,
td {
    padding: 11px 7px;
    border-bottom: 1px solid #334155;
    text-align: center;
    background: #0f172a !important;
    color: #f8fafc !important;
    white-space: nowrap;
}

th {
    color: #4ade80 !important;
    font-size: 12px;
    font-weight: 900;
    border-bottom: 2px solid #22c55e;
}

/* Team name */

td:nth-child(2) {
    text-align: left;
    font-weight: 800;
    color: #ffffff !important;
}

/* Position */

.position {
    width: 38px;
    font-weight: 900;
}

/* =========================================================
   ALTERNATING ROWS
========================================================= */

tbody tr:nth-child(odd),
tbody tr:nth-child(odd) td {
    background: #0f172a !important;
    color: #f8fafc !important;
}

tbody tr:nth-child(even),
tbody tr:nth-child(even) td {
    background: #111c31 !important;
    color: #f8fafc !important;
}

/* =========================================================
   TOP 3
========================================================= */

tbody tr.top3,
tbody tr.top3 td {
    background: #13251d !important;
    color: #ffffff !important;
}

/* =========================================================
   RELEGATION
========================================================= */

tbody tr.relegation,
tbody tr.relegation td {
    background: #241619 !important;
    color: #ffffff !important;
}

/* =========================================================
   POINTS
========================================================= */

tbody td:last-child,
tbody tr:nth-child(even) td:last-child,
tbody tr:nth-child(odd) td:last-child {
    color: #4ade80 !important;
    font-weight: 900;
}

/* =========================================================
   MOBILE TABLE
========================================================= */

@media (max-width: 600px) {

    th,
    td {
        padding: 10px 6px;
        font-size: 12px;
    }

}
/* Hover only for devices that support hover */

@media (hover: hover) {

    tbody tr:hover {
        background: #172554 !important;
    }

}

/* =========================================================
   RESULTS
========================================================= */

.result {
    display: flex;

    align-items: center;

    justify-content: space-between;

    gap: 8px;

    padding: 12px 3px;

    border-bottom: 1px solid #1e293b;

    min-width: 0;
}

.result:last-child {
    border-bottom: none;
}

.team {
    flex: 1;

    min-width: 0;

    font-weight: bold;

    font-size: 13px;

    overflow-wrap: anywhere;
}

.team.away {
    text-align: right;
}

.score {
    background: #020617;

    border: 1px solid #334155;

    border-radius: 8px;

    padding: 7px 10px;

    font-weight: 900;

    min-width: 58px;

    text-align: center;

    white-space: nowrap;
}

.date {
    font-size: 10px;

    color: #64748b;

    text-align: center;

    margin-top: 3px;
}

/* =========================================================
   EMPTY / HIDDEN
========================================================= */

.empty {
    text-align: center;

    padding: 25px 10px;

    color: #64748b;

    font-size: 13px;
}

.hidden {
    display: none !important;
}

/* =========================================================
   ADMIN PANEL
========================================================= */

.admin-panel {
    border: 1px solid #166534;

    background:
        rgba(5, 46, 22, .50);
}

.admin-title {
    color: #4ade80;

    font-weight: 900;

    font-size: 20px;

    margin-bottom: 15px;
}

.form-group {
    margin-bottom: 12px;
}

label {
    display: block;

    font-size: 12px;

    color: #94a3b8;

    margin-bottom: 5px;
}

/*
IMPORTANT:
16px prevents mobile browsers such as Safari
from automatically zooming when an input is selected.
*/

input,
select {
    width: 100%;

    min-height: 46px;

    padding: 11px;

    border-radius: 9px;

    border: 1px solid #334155;

    background: #020617;

    color: white;

    outline: none;

    font-size: 16px;

    line-height: 1.2;

    touch-action: manipulation;
}

input:focus,
select:focus {
    border-color: #22c55e;

    box-shadow:
        0 0 0 2px rgba(34,197,94,.08);
}

/* =========================================================
   BUTTONS
========================================================= */

.btn {
    border: none;

    padding: 11px 15px;

    min-height: 44px;

    border-radius: 9px;

    font-weight: bold;

    font-size: 15px;

    margin-top: 4px;

    touch-action: manipulation;
}

.btn:active {
    transform: scale(.97);
}

.green {
    background: #16a34a;

    color: white;
}

.blue {
    background: #2563eb;

    color: white;
}

.red {
    background: #dc2626;

    color: white;
}

.gray {
    background: #334155;

    color: white;
}

.btn:disabled {
    opacity: .5;

    cursor: not-allowed;
}

/* =========================================================
   FORM GRID
========================================================= */

.form-grid {
    display: grid;

    grid-template-columns: repeat(2, 1fr);

    gap: 10px;
}

/* =========================================================
   ADMIN TEAMS
========================================================= */

.team-admin {
    display: flex;

    justify-content: space-between;

    align-items: center;

    gap: 10px;

    padding: 10px;

    background: #020617;

    border: 1px solid #1e293b;

    border-radius: 9px;

    margin-bottom: 7px;

    min-width: 0;
}

.team-admin-name {
    flex: 1;

    min-width: 0;

    overflow-wrap: anywhere;
}

.small-btn {
    border: none;

    padding: 8px 11px;

    min-height: 38px;

    border-radius: 7px;

    color: white;

    font-size: 12px;

    flex-shrink: 0;

    touch-action: manipulation;
}

/* =========================================================
   MODAL
========================================================= */

.modal {
    position: fixed;

    inset: 0;

    width: 100%;
    height: 100%;

    background: rgba(0,0,0,.78);

    display: flex;

    align-items: center;

    justify-content: center;

    padding: 15px;

    z-index: 100;

    overflow-y: auto;
}

.modal-box {
    width: 100%;

    max-width: 420px;

    background: #0f172a;

    border: 1px solid #334155;

    border-radius: 16px;

    padding: 20px;

    box-shadow:
        0 20px 50px rgba(0,0,0,.5);
}

.modal-box h2 {
    margin-bottom: 15px;
}

.modal-buttons {
    display: flex;

    gap: 8px;

    margin-top: 10px;
}

.modal-buttons button {
    flex: 1;
}

/* =========================================================
   MESSAGES
========================================================= */

.error {
    background: rgba(239,68,68,.15);

    border: 1px solid #7f1d1d;

    color: #fca5a5;

    padding: 10px;

    border-radius: 9px;

    margin-bottom: 10px;

    font-size: 13px;

    overflow-wrap: anywhere;
}

.success {
    background: rgba(34,197,94,.15);

    border: 1px solid #166534;

    color: #86efac;

    padding: 10px;

    border-radius: 9px;

    margin-bottom: 10px;

    font-size: 13px;
}

.loading {
    text-align: center;

    padding: 40px 15px;

    color: #94a3b8;
}

/* =========================================================
   FOOTER
========================================================= */

.footer {
    width: 100%;

    text-align: center;

    padding:
        25px
        15px
        calc(30px + env(safe-area-inset-bottom));

    color: #475569;

    font-size: 11px;
}

/* =========================================================
   SMALL PHONES
========================================================= */

@media (max-width: 380px) {

    .container {
        padding-left: 8px;
        padding-right: 8px;
    }

    .card {
        padding: 12px;
    }

    .logo {
        font-size: 21px;
    }

    .tab {
        padding-left: 12px;
        padding-right: 12px;
    }

    th,
    td {
        padding: 10px 6px;
    }

    td {
        font-size: 12px;
    }

}

/* =========================================================
   LARGER SCREENS
========================================================= */

@media (min-width: 601px) {

    .stats {
        grid-template-columns: repeat(4, 1fr);
    }

}

/* =========================================================
   PREVENT MOBILE SELECTION/ZOOM BEHAVIOR
========================================================= */

button,
.tab,
.admin-btn,
.btn,
.small-btn {
    user-select: none;
    -webkit-user-select: none;
}

</style>

</head>


<body>


<!-- =======================================================
     HEADER
======================================================= -->

<header class="header">

    <div class="logo">
        ⚽ DLS 26 <span>LEAGUE</span>
    </div>

    <div class="subtitle">
        League Manager • TRIXARQ
    </div>

    <button
        class="admin-btn"
        onclick="openLogin()"
        id="adminButton">

        🔐 Admin Login

    </button>

</header>


<!-- =======================================================
     MAIN
======================================================= -->

<main class="container">

    <div id="loading" class="loading">
        Loading leagues...
    </div>


    <div id="app" class="hidden">


        <!-- =================================================
             LEAGUE TABS
        ================================================== -->

        <div class="tabs"
             id="leagueTabs">
        </div>


        <!-- =================================================
             ADMIN PANEL
        ================================================== -->

        <section
            id="adminPanel"
            class="card admin-panel hidden">

            <div class="admin-title">
                👑 Administrator Panel
            </div>

            <div id="adminMessage"></div>


            <!-- CREATE LEAGUE -->

            <div class="card">

                <h2>
                    🏆 Create League
                </h2>

                <div class="form-group">

                    <label>
                        League Name
                    </label>

                    <input
                        id="leagueName"
                        placeholder="e.g. DLS Premier League">

                </div>


                <div class="form-group">

                    <label>
                        Season
                    </label>

                    <input
                        id="leagueSeason"
                        value="2026"
                        placeholder="2026">

                </div>


                <button
                    class="btn green"
                    onclick="createLeague()">

                    ➕ Create League

                </button>

            </div>


            <!-- ADD TEAM -->

            <div class="card">

                <h2>
                    👥 Add Team
                </h2>


                <div class="form-group">

                    <label>
                        Team Name
                    </label>

                    <input
                        id="teamName"
                        placeholder="Team name">

                </div>


                <div class="form-group">

                    <label>
                        Manager
                    </label>

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


            <!-- ENTER RESULT -->

            <div class="card">

                <h2>
                    ⚽ Enter Match Result
                </h2>


                <div class="form-group">

                    <label>
                        Home Team
                    </label>

                    <select id="homeTeam">

                        <option value="">
                            Select home team
                        </option>

                    </select>

                </div>


                <div class="form-group">

                    <label>
                        Away Team
                    </label>

                    <select id="awayTeam">

                        <option value="">
                            Select away team
                        </option>

                    </select>

                </div>


                <div class="form-grid">


                    <div class="form-group">

                        <label>
                            Home Score
                        </label>

                        <input
                            id="homeScore"
                            type="number"
                            min="0"
                            inputmode="numeric"
                            value="0">

                    </div>


                    <div class="form-group">

                        <label>
                            Away Score
                        </label>

                        <input
                            id="awayScore"
                            type="number"
                            min="0"
                            inputmode="numeric"
                            value="0">

                    </div>

                </div>


                <div class="form-group">

                    <label>
                        Match Date
                    </label>

                    <input
                        id="matchDate"
                        type="date">

                </div>


                <button
                    class="btn green"
                    onclick="addResult()">

                    ⚽ Save Result

                </button>

            </div>


            <!-- CURRENT TEAMS -->

            <div class="card">

                <h2>
                    👥 Current Teams
                </h2>

                <div id="adminTeams"></div>

            </div>


            <!-- LEAGUE MANAGEMENT -->

            <div class="card">

                <h2>
                    ⚠️ League Management
                </h2>


                <button
                    class="btn red"
                    onclick="deleteCurrentLeague()">

                    🗑️ Delete Current League

                </button>


                <br>


                <button
                    class="btn red"
                    onclick="clearEverything()">

                    🧹 Delete ALL Leagues

                </button>

            </div>


            <button
                class="btn gray"
                onclick="logout()">

                🚪 Logout

            </button>

        </section>


        <!-- =================================================
             PUBLIC LEAGUE
        ================================================== -->

        <section id="leagueContent">


            <div class="card">

                <div
                    class="league-title"
                    id="leagueTitle">
                </div>

                <div
                    class="season"
                    id="leagueSeasonDisplay">
                </div>

            </div>


            <!-- STATS -->

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


            <!-- =================================================
                 TABLE
            ================================================== -->

            <div class="card">

                <h2>
                    📊 League Table
                </h2>


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


                        <tbody id="standingsBody">
                        </tbody>

                    </table>

                </div>

            </div>


            <!-- =================================================
                 RESULTS
            ================================================== -->

            <div class="card">

                <h2>
                    📝 Recent Results
                </h2>

                <div id="resultsList"></div>

            </div>


        </section>

    </div>

</main>


<!-- =======================================================
     FOOTER
======================================================= -->

<div class="footer">

    DLS 26 League Manager • TRIXARQ

</div>


<!-- =======================================================
     LOGIN MODAL
======================================================= -->

<div
    id="loginModal"
    class="modal hidden">


    <div class="modal-box">


        <h2>
            🔐 Administrator Login
        </h2>


        <div id="loginError"></div>


        <div class="form-group">

            <label>
                Email
            </label>

            <input
                id="loginEmail"
                type="email"
                inputmode="email"
                autocomplete="username"
                placeholder="Admin email">

        </div>


        <div class="form-group">

            <label>
                Password
            </label>

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
   APP STATE
========================================================= */

let database = {
    leagues: []
};

let currentLeagueId = null;

let adminLoggedIn = false;


/* =========================================================
   INITIALIZE
========================================================= */

document.addEventListener(
    "DOMContentLoaded",
    async () => {

        const dateInput =
            document.getElementById("matchDate");

        if (dateInput) {

            dateInput.value =
                new Date()
                .toISOString()
                .split("T")[0];

        }

        await checkSession();

        await loadDatabase();

        subscribeRealtime();

    }
);


/* =========================================================
   AUTH
========================================================= */

async function checkSession() {

    const {
        data: {
            session
        }
    } =
        await supabaseClient.auth.getSession();


    if (!session) {

        adminLoggedIn = false;

        updateAdminUI();

        return;

    }


    await checkAdmin(
        session.user.id
    );

}


async function checkAdmin(userId) {

    const {
        data,
        error
    } =
        await supabaseClient
        .from("admin_users")
        .select("id")
        .eq("id", userId)
        .maybeSingle();


    if (error) {

        console.error(error);

        adminLoggedIn = false;

        updateAdminUI();

        return;

    }


    adminLoggedIn =
        !!data;


    updateAdminUI();

}


/* =========================================================
   LOGIN
========================================================= */

async function login() {

    const email =
        document.getElementById("loginEmail")
        .value.trim();


    const password =
        document.getElementById("loginPassword")
        .value;


    const errorBox =
        document.getElementById("loginError");


    errorBox.innerHTML = "";


    if (!email || !password) {

        errorBox.innerHTML =
            `<div class="error">
                Enter email and password.
             </div>`;

        return;

    }


    const {
        data,
        error
    } =
        await supabaseClient.auth
        .signInWithPassword({

            email,
            password

        });


    if (error) {

        errorBox.innerHTML =
            `<div class="error">
                ${escapeHTML(error.message)}
             </div>`;

        return;

    }


    const userId =
        data.user.id;


    const {
        data: admin,
        error: adminError
    } =
        await supabaseClient
        .from("admin_users")
        .select("id")
        .eq("id", userId)
        .maybeSingle();


    if (adminError || !admin) {

        await supabaseClient
            .auth
            .signOut();


        errorBox.innerHTML =
            `<div class="error">
                This account is not an administrator.
             </div>`;

        return;

    }


    adminLoggedIn = true;


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

async function logout() {

    await supabaseClient
        .auth
        .signOut();


    adminLoggedIn = false;

    updateAdminUI();

}


/* =========================================================
   AUTH STATE
========================================================= */

supabaseClient.auth.onAuthStateChange(
    async (event, session) => {

        if (!session) {

            adminLoggedIn = false;

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

function openLogin() {

    if (adminLoggedIn) {

        document.getElementById(
            "adminPanel"
        ).scrollIntoView({
            behavior: "smooth"
        });

        return;

    }


    document.getElementById(
        "loginModal"
    ).classList.remove("hidden");

}


function closeLogin() {

    document.getElementById(
        "loginModal"
    ).classList.add("hidden");


    document.getElementById(
        "loginError"
    ).innerHTML = "";

}


function updateAdminUI() {

    const panel =
        document.getElementById(
            "adminPanel"
        );


    const button =
        document.getElementById(
            "adminButton"
        );


    if (adminLoggedIn) {

        panel.classList.remove(
            "hidden"
        );


        button.textContent =
            "👑 Admin Panel";

    } else {

        panel.classList.add(
            "hidden"
        );


        button.textContent =
            "🔐 Admin Login";

    }

}


/* =========================================================
   LOAD DATABASE
========================================================= */

async function loadDatabase() {

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
    ] =
        await Promise.all([


            supabaseClient
                .from("leagues")
                .select("*")
                .order(
                    "created_at",
                    {
                        ascending: true
                    }
                ),


            supabaseClient
                .from("teams")
                .select("*")
                .order(
                    "created_at",
                    {
                        ascending: true
                    }
                ),


            supabaseClient
                .from("matches")
                .select("*")
                .order(
                    "match_date",
                    {
                        ascending: false
                    }
                )

        ]);


    if (leaguesResponse.error) {

        showFatalError(
            leaguesResponse.error
        );

        return;

    }


    if (teamsResponse.error) {

        showFatalError(
            teamsResponse.error
        );

        return;

    }


    if (matchesResponse.error) {

        showFatalError(
            matchesResponse.error
        );

        return;

    }


    const leagues =
        leaguesResponse.data || [];


    const teams =
        teamsResponse.data || [];


    const matches =
        matchesResponse.data || [];


    database.leagues =
        leagues.map(
            league => ({

                id:
                    Number(league.id),

                name:
                    league.name,

                season:
                    league.season ||
                    "2026",


                teams:
                    teams
                    .filter(
                        team =>
                            Number(
                                team.league_id
                            ) ===
                            Number(
                                league.id
                            )
                    )
                    .map(
                        team => ({

                            id:
                                Number(team.id),

                            name:
                                team.name,

                            manager:
                                team.manager ||
                                ""

                        })
                    ),


                matches:
                    matches
                    .filter(
                        match =>
                            Number(
                                match.league_id
                            ) ===
                            Number(
                                league.id
                            )
                    )
                    .map(
                        match => ({

                            id:
                                Number(match.id),

                            homeId:
                                Number(
                                    match.home_id
                                ),

                            awayId:
                                Number(
                                    match.away_id
                                ),

                            homeScore:
                                Number(
                                    match.home_score
                                ),

                            awayScore:
                                Number(
                                    match.away_score
                                ),

                            date:
                                match.match_date

                        })
                    )

            })
        );


    if (
        currentLeagueId === null ||
        !database.leagues.some(
            l =>
                l.id ===
                currentLeagueId
        )
    ) {

        currentLeagueId =
            database.leagues.length
                ? database.leagues[0].id
                : null;

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

function subscribeRealtime() {

    supabaseClient
        .channel(
            "dls-league-manager"
        )


        .on(
            "postgres_changes",
            {
                event: "*",
                schema: "public",
                table: "leagues"
            },
            async () => {

                await loadDatabase();

            }
        )


        .on(
            "postgres_changes",
            {
                event: "*",
                schema: "public",
                table: "teams"
            },
            async () => {

                await loadDatabase();

            }
        )


        .on(
            "postgres_changes",
            {
                event: "*",
                schema: "public",
                table: "matches"
            },
            async () => {

                await loadDatabase();

            }
        )


        .subscribe();

}


/* =========================================================
   RENDER
========================================================= */

function render() {

    renderLeagueTabs();

    renderCurrentLeague();

    renderAdmin();

}


/* =========================================================
   LEAGUE TABS
========================================================= */

function renderLeagueTabs() {

    const tabs =
        document.getElementById(
            "leagueTabs"
        );


    tabs.innerHTML = "";


    if (!database.leagues.length) {

        tabs.innerHTML =
            `<div class="empty">
                No leagues created yet.
             </div>`;

        return;

    }


    database.leagues.forEach(
        league => {

            const button =
                document.createElement(
                    "button"
                );


            button.className =
                "tab" +
                (
                    league.id ===
                    currentLeagueId
                        ? " active"
                        : ""
                );


            button.textContent =
                league.name;


            button.onclick = () => {

                currentLeagueId =
                    league.id;

                render();

            };


            tabs.appendChild(
                button
            );

        }
    );

}


/* =========================================================
   CURRENT LEAGUE
========================================================= */

function getCurrentLeague() {

    return database.leagues.find(
        league =>
            Number(league.id) ===
            Number(currentLeagueId)
    );

}


/* =========================================================
   RENDER CURRENT LEAGUE
========================================================= */

function renderCurrentLeague() {

    const league =
        getCurrentLeague();


    if (!league) {

        document.getElementById(
            "leagueTitle"
        ).textContent =
            "No League";


        document.getElementById(
            "leagueSeasonDisplay"
        ).textContent = "";


        document.getElementById(
            "teamCount"
        ).textContent = "0";


        document.getElementById(
            "matchCount"
        ).textContent = "0";


        document.getElementById(
            "leaderName"
        ).textContent = "-";


        document.getElementById(
            "leaderPoints"
        ).textContent = "0";


        document.getElementById(
            "standingsBody"
        ).innerHTML =
            `<tr>
                <td colspan="10">
                    <div class="empty">
                        Create a league from the Admin Panel.
                    </div>
                </td>
            </tr>`;


        document.getElementById(
            "resultsList"
        ).innerHTML =
            `<div class="empty">
                No results.
             </div>`;


        updateTeamSelectors();

        return;

    }


    document.getElementById(
        "leagueTitle"
    ).textContent =
        league.name;


    document.getElementById(
        "leagueSeasonDisplay"
    ).textContent =
        "Season " +
        league.season;


    document.getElementById(
        "teamCount"
    ).textContent =
        league.teams.length;


    document.getElementById(
        "matchCount"
    ).textContent =
        league.matches.length;


    const standings =
        calculateStandings(
            league
        );


    if (standings.length) {

        document.getElementById(
            "leaderName"
        ).textContent =
            standings[0].name;


        document.getElementById(
            "leaderPoints"
        ).textContent =
            standings[0].pts;

    } else {

        document.getElementById(
            "leaderName"
        ).textContent =
            "-";


        document.getElementById(
            "leaderPoints"
        ).textContent =
            "0";

    }


    renderStandings(
        standings
    );


    renderResults(
        league
    );


    updateTeamSelectors();

}


/* =========================================================
   STANDINGS CALCULATION
========================================================= */

function calculateStandings(league) {

    const table = {};


    league.teams.forEach(
        team => {

            table[team.id] = {

                id:
                    team.id,

                name:
                    team.name,

                p: 0,

                w: 0,

                d: 0,

                l: 0,

                gf: 0,

                ga: 0,

                gd: 0,

                pts: 0

            };

        }
    );


    league.matches.forEach(
        match => {

            const home =
                table[match.homeId];


            const away =
                table[match.awayId];


            if (!home || !away) {

                return;

            }


            const hs =
                Number(
                    match.homeScore
                );


            const as =
                Number(
                    match.awayScore
                );


            home.p++;

            away.p++;


            home.gf += hs;

            home.ga += as;


            away.gf += as;

            away.ga += hs;


            if (hs > as) {

                home.w++;

                away.l++;

                home.pts += 3;

            }

            else if (hs < as) {

                away.w++;

                home.l++;

                away.pts += 3;

            }

            else {

                home.d++;

                away.d++;

                home.pts++;

                away.pts++;

            }

        }
    );


    Object.values(table)
        .forEach(
            team => {

                team.gd =
                    team.gf -
                    team.ga;

            }
        );


    return Object.values(table)
        .sort(
            (a, b) => {

                if (
                    b.pts !==
                    a.pts
                )
                    return (
                        b.pts -
                        a.pts
                    );


                if (
                    b.gd !==
                    a.gd
                )
                    return (
                        b.gd -
                        a.gd
                    );


                if (
                    b.gf !==
                    a.gf
                )
                    return (
                        b.gf -
                        a.gf
                    );


                return a.name
                    .localeCompare(
                        b.name
                    );

            }
        );

}


/* =========================================================
   RENDER STANDINGS
========================================================= */

function renderStandings(
    standings
) {

    const body =
        document.getElementById(
            "standingsBody"
        );


    body.innerHTML = "";


    if (!standings.length) {

        body.innerHTML =
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
        (team, index) => {

            const row =
                document.createElement(
                    "tr"
                );


            if (index < 3) {

                row.classList.add(
                    "top3"
                );

            }


            if (
                standings.length >= 4 &&
                index >=
                standings.length - 2
            ) {

                row.classList.add(
                    "relegation"
                );

            }


            let position =
                index + 1;


            if (index === 0)
                position = "🥇";

            else if (index === 1)
                position = "🥈";

            else if (index === 2)
                position = "🥉";


            row.innerHTML = `

                <td class="position">
                    ${position}
                </td>

                <td>
                    ${escapeHTML(
                        team.name
                    )}
                </td>

                <td>
                    ${team.p}
                </td>

                <td>
                    ${team.w}
                </td>

                <td>
                    ${team.d}
                </td>

                <td>
                    ${team.l}
                </td>

                <td>
                    ${team.gf}
                </td>

                <td>
                    ${team.ga}
                </td>

                <td>
                    ${team.gd}
                </td>

                <td>
                    <strong>
                        ${team.pts}
                    </strong>
                </td>

            `;


            body.appendChild(
                row
            );

        }
    );

}


/* =========================================================
   RESULTS
========================================================= */

function renderResults(
    league
) {

    const list =
        document.getElementById(
            "resultsList"
        );


    list.innerHTML = "";


    if (!league.matches.length) {

        list.innerHTML =
            `<div class="empty">
                No matches played yet.
             </div>`;

        return;

    }


    const sorted =
        [...league.matches]
        .sort(
            (a, b) =>
                new Date(b.date) -
                new Date(a.date)
        );


    sorted
        .slice(0, 20)
        .forEach(
            match => {

                const home =
                    league.teams.find(
                        t =>
                            t.id ===
                            match.homeId
                    );


                const away =
                    league.teams.find(
                        t =>
                            t.id ===
                            match.awayId
                    );


                if (!home || !away)
                    return;


                const item =
                    document.createElement(
                        "div"
                    );


                item.className =
                    "result";


                item.innerHTML = `

                    <div class="team">

                        ${escapeHTML(
                            home.name
                        )}

                    </div>


                    <div>

                        <div class="score">

                            ${match.homeScore}
                            -
                            ${match.awayScore}

                        </div>


                        <div class="date">

                            ${escapeHTML(
                                match.date || ""
                            )}

                        </div>

                    </div>


                    <div class="team away">

                        ${escapeHTML(
                            away.name
                        )}

                    </div>

                `;


                list.appendChild(
                    item
                );

            }
        );

}


/* =========================================================
   ADMIN RENDER
========================================================= */

function renderAdmin() {

    if (!adminLoggedIn)
        return;


    const league =
        getCurrentLeague();


    const list =
        document.getElementById(
            "adminTeams"
        );


    list.innerHTML = "";


    if (!league) {

        list.innerHTML =
            `<div class="empty">
                No current league.
             </div>`;


        updateTeamSelectors();

        return;

    }


    if (!league.teams.length) {

        list.innerHTML =
            `<div class="empty">
                No teams registered.
             </div>`;


        updateTeamSelectors();

        return;

    }


    league.teams.forEach(
        team => {

            const item =
                document.createElement(
                    "div"
                );


            item.className =
                "team-admin";


            item.innerHTML = `

                <div class="team-admin-name">

                    <strong>
                        ${escapeHTML(
                            team.name
                        )}
                    </strong>

                    <br>

                    <small style="color:#64748b">

                        ${escapeHTML(
                            team.manager ||
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


            list.appendChild(
                item
            );

        }
    );


    updateTeamSelectors();

}


/* =========================================================
   TEAM SELECTORS
========================================================= */

function updateTeamSelectors() {

    const home =
        document.getElementById(
            "homeTeam"
        );


    const away =
        document.getElementById(
            "awayTeam"
        );


    if (!home || !away)
        return;


    const oldHome =
        home.value;


    const oldAway =
        away.value;


    home.innerHTML =
        `<option value="">
            Select home team
         </option>`;


    away.innerHTML =
        `<option value="">
            Select away team
         </option>`;


    const league =
        getCurrentLeague();


    if (!league)
        return;


    league.teams.forEach(
        team => {

            const option1 =
                document.createElement(
                    "option"
                );


            option1.value =
                String(
                    team.id
                );


            option1.textContent =
                team.name;


            home.appendChild(
                option1
            );


            const option2 =
                document.createElement(
                    "option"
                );


            option2.value =
                String(
                    team.id
                );


            option2.textContent =
                team.name;


            away.appendChild(
                option2
            );

        }
    );


    if (
        [...home.options]
        .some(
            o =>
                o.value ===
                oldHome
        )
    ) {

        home.value =
            oldHome;

    }


    if (
        [...away.options]
        .some(
            o =>
                o.value ===
                oldAway
        )
    ) {

        away.value =
            oldAway;

    }

}


/* =========================================================
   CREATE LEAGUE
========================================================= */

async function createLeague() {

    if (!requireAdmin())
        return;


    const name =
        document.getElementById(
            "leagueName"
        ).value.trim();


    const season =
        document.getElementById(
            "leagueSeason"
        ).value.trim() ||
        "2026";


    if (!name) {

        showAdminMessage(
            "Enter a league name.",
            false
        );

        return;

    }


    const {
        data,
        error
    } =
        await supabaseClient
        .from("leagues")
        .insert({

            name,

            season

        })
        .select()
        .single();


    if (error) {

        showAdminMessage(
            "Error creating league: " +
            error.message,
            false
        );

        return;

    }


    document.getElementById(
        "leagueName"
    ).value = "";


    document.getElementById(
        "leagueSeason"
    ).value = "2026";


    currentLeagueId =
        Number(
            data.id
        );


    showAdminMessage(
        "League created successfully.",
        true
    );


    await loadDatabase();

}


/* =========================================================
   ADD TEAM
========================================================= */

async function addTeam() {

    if (!requireAdmin())
        return;


    const league =
        getCurrentLeague();


    if (!league) {

        showAdminMessage(
            "Create/select a league first.",
            false
        );

        return;

    }


    const name =
        document.getElementById(
            "teamName"
        ).value.trim();


    const manager =
        document.getElementById(
            "managerName"
        ).value.trim();


    if (!name) {

        showAdminMessage(
            "Enter a team name.",
            false
        );

        return;

    }


    const exists =
        league.teams.some(
            team =>
                team.name
                .toLowerCase() ===
                name.toLowerCase()
        );


    if (exists) {

        showAdminMessage(
            "That team already exists in this league.",
            false
        );

        return;

    }


    const {
        error
    } =
        await supabaseClient
        .from("teams")
        .insert({

            league_id:
                Number(
                    league.id
                ),

            name,

            manager:
                manager ||
                null

        });


    if (error) {

        showAdminMessage(
            "Error adding team: " +
            error.message,
            false
        );

        return;

    }


    document.getElementById(
        "teamName"
    ).value = "";


    document.getElementById(
        "managerName"
    ).value = "";


    showAdminMessage(
        "Team added successfully.",
        true
    );


    await loadDatabase();

}


/* =========================================================
   ADD RESULT
========================================================= */

async function addResult() {

    if (!requireAdmin())
        return;


    const league =
        getCurrentLeague();


    if (!league) {

        showAdminMessage(
            "Select a league first.",
            false
        );

        return;

    }


    const homeValue =
        document.getElementById(
            "homeTeam"
        ).value;


    const awayValue =
        document.getElementById(
            "awayTeam"
        ).value;


    const homeId =
        Number(homeValue);


    const awayId =
        Number(awayValue);


    if (
        !homeValue ||
        !awayValue
    ) {

        showAdminMessage(
            "Select both teams.",
            false
        );

        return;

    }


    if (
        !Number.isInteger(homeId) ||
        !Number.isInteger(awayId)
    ) {

        showAdminMessage(
            "Invalid team ID.",
            false
        );

        return;

    }


    if (homeId === awayId) {

        showAdminMessage(
            "A team cannot play itself.",
            false
        );

        return;

    }


    const homeTeam =
        league.teams.find(
            team =>
                Number(team.id) ===
                homeId
        );


    const awayTeam =
        league.teams.find(
            team =>
                Number(team.id) ===
                awayId
        );


    if (!homeTeam) {

        showAdminMessage(
            "Home team ID " +
            homeId +
            " was not found in the current league.",
            false
        );

        return;

    }


    if (!awayTeam) {

        showAdminMessage(
            "Away team ID " +
            awayId +
            " was not found in the current league.",
            false
        );

        return;

    }


    const homeScore =
        Number(
            document.getElementById(
                "homeScore"
            ).value
        );


    const awayScore =
        Number(
            document.getElementById(
                "awayScore"
            ).value
        );


    if (
        !Number.isInteger(homeScore) ||
        homeScore < 0
    ) {

        showAdminMessage(
            "Enter a valid home score.",
            false
        );

        return;

    }


    if (
        !Number.isInteger(awayScore) ||
        awayScore < 0
    ) {

        showAdminMessage(
            "Enter a valid away score.",
            false
        );

        return;

    }


    const date =
        document.getElementById(
            "matchDate"
        ).value ||
        new Date()
        .toISOString()
        .split("T")[0];


    const {
        error
    } =
        await supabaseClient
        .from("matches")
        .insert({

            league_id:
                Number(
                    league.id
                ),

            home_id:
                homeId,

            away_id:
                awayId,

            home_score:
                homeScore,

            away_score:
                awayScore,

            match_date:
                date

        });


    if (error) {

        showAdminMessage(
            "Error saving result: " +
            error.message,
            false
        );

        return;

    }


    document.getElementById(
        "homeTeam"
    ).value = "";


    document.getElementById(
        "awayTeam"
    ).value = "";


    document.getElementById(
        "homeScore"
    ).value = "0";


    document.getElementById(
        "awayScore"
    ).value = "0";


    showAdminMessage(
        "Result saved successfully.",
        true
    );


    await loadDatabase();

}


/* =========================================================
   REMOVE TEAM
========================================================= */

async function removeTeam(
    teamId
) {

    if (!requireAdmin())
        return;


    const league =
        getCurrentLeague();


    if (!league)
        return;


    const team =
        league.teams.find(
            t =>
                Number(t.id) ===
                Number(teamId)
        );


    if (!team)
        return;


    const confirmed =
        confirm(
            "Remove " +
            team.name +
            "?\n\n" +
            "All matches involving this team will also be deleted."
        );


    if (!confirmed)
        return;


    const {
        error
    } =
        await supabaseClient
        .from("teams")
        .delete()
        .eq(
            "id",
            Number(teamId)
        );


    if (error) {

        showAdminMessage(
            "Error removing team: " +
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

async function deleteCurrentLeague() {

    if (!requireAdmin())
        return;


    const league =
        getCurrentLeague();


    if (!league) {

        showAdminMessage(
            "No league selected.",
            false
        );

        return;

    }


    const confirmed =
        confirm(
            "DELETE " +
            league.name +
            "?\n\n" +
            "This will permanently delete:\n" +
            "- The league\n" +
            "- All teams\n" +
            "- All matches"
        );


    if (!confirmed)
        return;


    const {
        error
    } =
        await supabaseClient
        .from("leagues")
        .delete()
        .eq(
            "id",
            Number(league.id)
        );


    if (error) {

        showAdminMessage(
            "Error deleting league: " +
            error.message,
            false
        );

        return;

    }


    currentLeagueId =
        null;


    showAdminMessage(
        "League deleted.",
        true
    );


    await loadDatabase();

}


/* =========================================================
   DELETE EVERYTHING
========================================================= */

async function clearEverything() {

    if (!requireAdmin())
        return;


    const confirmed =
        confirm(
            "WARNING!\n\n" +
            "This will permanently delete ALL leagues, " +
            "teams and matches.\n\n" +
            "Continue?"
        );


    if (!confirmed)
        return;


    const {
        error
    } =
        await supabaseClient
        .from("leagues")
        .delete()
        .gt(
            "id",
            0
        );


    if (error) {

        showAdminMessage(
            "Error clearing data: " +
            error.message,
            false
        );

        return;

    }


    currentLeagueId =
        null;


    showAdminMessage(
        "All league data deleted.",
        true
    );


    await loadDatabase();

}


/* =========================================================
   ADMIN CHECK
========================================================= */

function requireAdmin() {

    if (!adminLoggedIn) {

        alert(
            "Administrator login required."
        );

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
) {

    const box =
        document.getElementById(
            "adminMessage"
        );


    box.innerHTML =
        `<div class="${
            success
                ? "success"
                : "error"
        }">

            ${escapeHTML(message)}

         </div>`;


    setTimeout(
        () => {

            box.innerHTML = "";

        },
        5000
    );

}


/* =========================================================
   DATABASE ERROR
========================================================= */

function showFatalError(
    error
) {

    document.getElementById(
        "loading"
    ).classList.remove(
        "hidden"
    );


    document.getElementById(
        "loading"
    ).innerHTML =
        `<div class="error">

            <strong>
                Database Error
            </strong>

            <br><br>

            ${escapeHTML(
                error?.message ||
                "Unknown error"
            )}

         </div>`;

}


/* =========================================================
   ESCAPE HTML
========================================================= */

function escapeHTML(
    value
) {

    return String(
        value ?? ""
    )
    .replace(
        /&/g,
        "&amp;"
    )
    .replace(
        /</g,
        "&lt;"
    )
    .replace(
        />/g,
        "&gt;"
    )
    .replace(
        /"/g,
        "&quot;"
    )
    .replace(
        /'/g,
        "&#039;"
    );

}

</script>

</body>
</html>
