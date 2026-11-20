<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>🏐 排球卡牌大亂鬥</title>

<style>

*{
    box-sizing:border-box;
}

body{
    margin:0;
    font-family:
        Arial,
        "Noto Sans TC",
        sans-serif;

    background:
        linear-gradient(
            135deg,
            #0f172a,
            #172554,
            #0f172a
        );

    color:white;
    min-height:100vh;
}

.container{
    width:min(1200px,95%);
    margin:auto;
    padding:20px 0 50px;
}

/* ===== 標題 ===== */

header{
    text-align:center;
    margin-bottom:20px;
}

header h1{
    font-size:36px;
    margin:5px 0;
}

header p{
    color:#cbd5e1;
    margin:5px;
}

/* ===== 比分 ===== */

.scoreboard{
    display:grid;
    grid-template-columns:1fr 150px 1fr;
    gap:15px;
    align-items:stretch;
}

.team{
    background:#111827;
    border:2px solid #334155;
    border-radius:20px;
    padding:20px;
    text-align:center;
    box-shadow:0 10px 30px #0005;
}

.team-a{
    border-color:#2563eb;
}

.team-b{
    border-color:#ef4444;
}

.team h2{
    margin:0;
}

.team-a h2{
    color:#60a5fa;
}

.team-b h2{
    color:#fb7185;
}

.score{
    font-size:72px;
    font-weight:bold;
    margin:10px 0;
}

.score-buttons{
    display:flex;
    justify-content:center;
    gap:10px;
}

.score-buttons button{
    width:60px;
    height:45px;
    font-size:25px;
}

.center-score{
    display:flex;
    justify-content:center;
    align-items:center;
    flex-direction:column;

    background:#111827;
    border-radius:20px;
    border:2px solid #334155;
}

.vs{
    font-size:30px;
    font-weight:bold;
}

button{
    border:none;
    border-radius:10px;
    padding:10px 15px;
    font-weight:bold;
    cursor:pointer;
    color:white;
    background:#334155;
    transition:.15s;
}

button:hover{
    transform:translateY(-2px);
    filter:brightness(1.15);
}

.reset-score{
    margin-top:10px;
    font-size:12px;
}

/* ===== 主要區塊 ===== */

.section{
    margin-top:20px;
    background:#111827;
    border:1px solid #334155;
    border-radius:20px;
    padding:20px;
}

.section h2{
    margin-top:0;
}

/* ===== 抽卡 ===== */

.draw-area{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:20px;
}

.draw-box{
    background:#0f172a;
    border:1px solid #334155;
    border-radius:15px;
    padding:20px;
    text-align:center;
}

.draw-box h3{
    margin-top:0;
}

.draw-button{
    width:100%;
    font-size:18px;
    padding:15px;
    background:#2563eb;
}

.hand{
    min-height:60px;
    margin-top:15px;

    display:flex;
    flex-wrap:wrap;
    gap:8px;

    justify-content:center;
}

.card-small{
    border-radius:10px;
    padding:10px;
    font-size:13px;
    font-weight:bold;
}

.card-small.good{
    background:#166534;
    border:1px solid #22c55e;
}

.card-small.bad{
    background:#991b1b;
    border:1px solid #ef4444;
}

.use-button{
    margin-left:5px;
    background:#475569;
    padding:5px 8px;
    font-size:11px;
}

.empty{
    color:#94a3b8;
    font-size:14px;
}

/* ===== 卡片圖鑑 ===== */

.tabs{
    display:flex;
    gap:8px;
    flex-wrap:wrap;
    margin-bottom:15px;
}

.tabs button.active{
    background:white;
    color:#0f172a;
}

.card-list{
    display:grid;
    grid-template-columns:
        repeat(4,1fr);

    gap:12px;
}

.card{
    min-height:145px;
    padding:15px;

    background:#0f172a;

    border-radius:15px;

    border:2px solid #334155;
}

.card.good{
    border-color:#22c55e;
}

.card.bad{
    border-color:#ef4444;
}

.card.both{
    border-color:#f59e0b;
}

.card-type{
    display:inline-block;
    padding:4px 8px;

    border-radius:20px;

    font-size:11px;
    font-weight:bold;

    margin-bottom:8px;
}

.card.good .card-type{
    background:#166534;
}

.card.bad .card-type{
    background:#991b1b;
}

.card.both .card-type{
    background:#92400e;
}

.card-name{
    font-size:18px;
    font-weight:bold;
    margin-bottom:8px;
}

.card-description{
    color:#cbd5e1;
    font-size:13px;
    line-height:1.6;
}

/* ===== 紀錄 ===== */

.history{
    max-height:250px;
    overflow:auto;
}

.history-item{
    padding:8px 0;
    border-bottom:1px solid #334155;
    color:#cbd5e1;
}

/* ===== Modal ===== */

.modal{
    position:fixed;
    inset:0;

    background:#000b;

    display:none;

    justify-content:center;
    align-items:center;

    padding:20px;

    z-index:1000;
}

.modal.show{
    display:flex;
}

.modal-content{
    width:min(450px,100%);

    background:#111827;

    border-radius:20px;

    border:2px solid #f59e0b;

    padding:25px;

    text-align:center;
}

.modal-content h2{
    font-size:30px;
}

.modal-content p{
    color:#cbd5e1;
    line-height:1.7;
}

.modal-close{
    background:#f59e0b;
}

/* ===== 自動保存提示 ===== */

.save-status{
    text-align:center;
    color:#86efac;
    font-size:12px;
    margin-top:10px;
}

/* ===== 手機 ===== */

@media(max-width:800px){

    header h1{
        font-size:27px;
    }

    .scoreboard{
        grid-template-columns:
            1fr 70px 1fr;
    }

    .score{
        font-size:50px;
    }

    .draw-area{
        grid-template-columns:1fr;
    }

    .card-list{
        grid-template-columns:
            repeat(2,1fr);
    }

}

@media(max-width:500px){

    .container{
        width:96%;
    }

    .scoreboard{
        grid-template-columns:
            1fr 55px 1fr;
        gap:6px;
    }

    .team{
        padding:12px 5px;
    }

    .score{
        font-size:40px;
    }

    .score-buttons button{
        width:45px;
        height:40px;
    }

    .card-list{
        grid-template-columns:1fr;
    }

    .center-score{
        padding:5px;
    }

    .vs{
        font-size:20px;
    }

}

</style>
</head>

<body>

<div class="container">

<header>

<h1>🏐 排球卡牌大亂鬥</h1>

<p>
排球 × 抽卡 × 策略 × 社團遊戲
</p>

<div class="save-status" id="saveStatus">
💾 遊戲會自動保存
</div>

</header>


<!-- =========================
     比分
========================= -->

<div class="scoreboard">

<div class="team team-a">

<h2>🔵 A隊</h2>

<div
    class="score"
    id="scoreA">
0
</div>

<div class="score-buttons">

<button onclick="changeScore('A',1)">
＋
</button>

<button onclick="changeScore('A',-1)">
－
</button>

</div>

</div>


<div class="center-score">

<div class="vs">
VS
</div>

<button
    class="reset-score"
    onclick="resetScore()">

比分歸零

</button>

</div>


<div class="team team-b">

<h2>🔴 B隊</h2>

<div
    class="score"
    id="scoreB">
0
</div>

<div class="score-buttons">

<button onclick="changeScore('B',1)">
＋
</button>

<button onclick="changeScore('B',-1)">
－
</button>

</div>

</div>

</div>


<!-- =========================
     抽卡
========================= -->

<div class="section">

<h2>🎴 雙方抽卡</h2>

<div class="draw-area">


<div class="draw-box">

<h3>🔵 A隊</h3>

<button
    class="draw-button"
    onclick="drawCard('A')">

🎴 A隊抽卡

</button>

<div
    class="hand"
    id="handA">

</div>

</div>


<div class="draw-box">

<h3>🔴 B隊</h3>

<button
    class="draw-button"
    onclick="drawCard('B')">

🎴 B隊抽卡

</button>

<div
    class="hand"
    id="handB">

</div>

</div>

</div>

<p style="color:#fbbf24;text-align:center">

🟡 抽到「雙方卡」後會立即使用，不會進入手牌。

</p>

</div>


<!-- =========================
     卡片圖鑑
========================= -->

<div class="section">

<h2>📚 卡片圖鑑</h2>

<div class="tabs">

<button
    class="active"
    onclick="showCards('all',this)">
全部
</button>

<button
    onclick="showCards('good',this)">
🟢 好卡
</button>

<button
    onclick="showCards('bad',this)">
🔴 壞卡
</button>

<button
    onclick="showCards('both',this)">
🟡 雙方卡
</button>

</div>

<div
    class="card-list"
    id="cardList">
</div>

</div>


<!-- =========================
     持有卡
========================= -->

<div class="section">

<h2>🎒 雙方持有卡片</h2>

<h3>🔵 A隊</h3>

<div
    class="hand"
    id="ownedA">
</div>


<hr style="border-color:#334155;margin:20px 0">


<h3>🔴 B隊</h3>

<div
    class="hand"
    id="ownedB">
</div>

</div>


<!-- =========================
     紀錄
========================= -->

<div class="section">

<h2>📜 比賽紀錄</h2>

<div
    class="history"
    id="history">
</div>

</div>


<!-- =========================
     清除資料
========================= -->

<div class="section" style="text-align:center">

<button
    onclick="clearSave()"
    style="background:#991b1b">

🗑️ 清除所有保存資料並重新開始

</button>

</div>


</div>


<!-- =========================
     卡片 Modal
========================= -->

<div
    class="modal"
    id="modal">

<div class="modal-content">

<div id="modalType"></div>

<h2 id="modalName"></h2>

<p id="modalText"></p>

<button
    class="modal-close"
    onclick="closeModal()">

知道了

</button>

</div>

</div>


<script>


/* =========================================
   卡片資料
========================================= */

const cards = [

/* ===== 好卡 ===== */

{
id:1,
type:"good",
name:"金手指",
text:"下一球完成接球 → 舉球 → 攻擊並得分，額外＋1分。"
},

{
id:2,
type:"good",
name:"再來一次",
text:"下一次己方發球失誤，可取消失誤並重新發球一次。第二次失誤正常計分。"
},

{
id:3,
type:"good",
name:"超級發球",
text:"下一次發球可在三米線後的任何位置發球。"
},

{
id:4,
type:"good",
name:"完美接發",
text:"下一球第一球成功接到且未出界，可多一次觸球機會。"
},

{
id:5,
type:"good",
name:"神速換位",
text:"下一球開始前，可重新安排己方所有人的合法場上位置。"
},

{
id:6,
type:"good",
name:"火力全開",
text:"下一次進攻前全隊喊「火力全開」，若成功得分額外＋1分。"
},

{
id:7,
type:"good",
name:"王牌登場",
text:"指定一名己方球員，下一球可自由選擇合法站位。"
},

{
id:8,
type:"good",
name:"教練時間",
text:"獲得30秒戰術討論時間，可重新安排站位與戰術。"
},


/* ===== 壞卡 ===== */

{
id:9,
type:"bad",
name:"旋轉地獄",
text:"對方下一球所有人必須順時針換位一次，不能討論。"
},

{
id:10,
type:"bad",
name:"禁止扣球",
text:"對方下一球禁止扣球，只能吊球、推球、放球或高球。"
},

{
id:11,
type:"bad",
name:"一人消失",
text:"指定對方一名球員，下一球必須站到場外。"
},

{
id:12,
type:"bad",
name:"小心地雷",
text:"指定對方一個位置，該位置球員下一球不能碰第一球。"
},

{
id:13,
type:"bad",
name:"反手發球",
text:"對方下一次發球必須使用非慣用手。"
},

{
id:14,
type:"bad",
name:"靜音模式",
text:"對方下一球禁止說話，只能靠手勢溝通。"
},

{
id:15,
type:"bad",
name:"不能跑",
text:"指定一名對方球員，下一球雙腳不能離開原本站位。"
},

{
id:16,
type:"bad",
name:"限制觸球",
text:"對方下一球全隊最多只能使用2次觸球。"
},


/* ===== 雙方卡 ===== */

{
id:17,
type:"both",
name:"死亡模式",
text:"下一球雙方只能使用下手接球，不能托球、扣球。"
},

{
id:18,
type:"both",
name:"一球定江山",
text:"下一球勝方直接＋2分。"
},

{
id:19,
type:"both",
name:"禁止扣球",
text:"下一球雙方都不能扣球，只能吊球、推球或放球。"
},

{
id:20,
type:"both",
name:"安靜排球",
text:"下一球雙方都不能說話，講話者直接犯規。"
},

{
id:21,
type:"both",
name:"全員換位",
text:"下一球開始前，兩隊所有人都必須順時針換位。"
},

{
id:22,
type:"both",
name:"三秒快攻",
text:"發球後球隊必須在3秒內完成攻擊，超過3秒對方得分。"
},

{
id:23,
type:"both",
name:"地獄模式",
text:"下一球每隊第一次碰球就必須成功控制住，第一球直接失控出界即失分。"
},

{
id:24,
type:"both",
name:"黃金球",
text:"下一球得分方直接＋2分；若發球直接失誤，對方直接＋2分。"
}

];


/* =========================================
   遊戲資料
========================================= */

const SAVE_KEY =
"volleyball_card_game_save_v2";


let state = {

scoreA:0,

scoreB:0,

ownedA:[],

ownedB:[],

history:[]

};


let remainingCards = [];


/* =========================================
   初始化牌庫
========================================= */

function resetDeck(){

remainingCards =
cards.map(card => card.id);

}


/* =========================================
   找卡片
========================================= */

function getCard(id){

return cards.find(
card => card.id === id
);

}


/* =========================================
   自動保存
========================================= */

function saveGame(){

const data = {

state:state,

remainingCards:
remainingCards

};

localStorage.setItem(
SAVE_KEY,
JSON.stringify(data)
);

document.getElementById(
"saveStatus"
).textContent =
"💾 已自動保存";

}


/* =========================================
   載入保存資料
========================================= */

function loadGame(){

const saved =
localStorage.getItem(
SAVE_KEY
);

if(!saved){

resetDeck();

return;

}


try{

const data =
JSON.parse(saved);


if(data.state){

state = {

scoreA:
Number(data.state.scoreA) || 0,

scoreB:
Number(data.state.scoreB) || 0,

ownedA:
Array.isArray(
data.state.ownedA
)
? data.state.ownedA
:[],

ownedB:
Array.isArray(
data.state.ownedB
)
? data.state.ownedB
:[],

history:
Array.isArray(
data.state.history
)
? data.state.history
:[]

};

}


if(
Array.isArray(
data.remainingCards
)
){

remainingCards =
data.remainingCards;

}

else{

resetDeck();

}

}

catch(error){

console.log(
"讀取存檔失敗",
error
);

resetDeck();

}

}


/* =========================================
   分數
========================================= */

function changeScore(team,amount){

if(team === "A"){

state.scoreA =
Math.max(
0,
state.scoreA + amount
);

}

else{

state.scoreB =
Math.max(
0,
state.scoreB + amount
);

}


renderScore();


addHistory(

team === "A"
? `🔵 A隊 ${amount > 0 ? "得" : "扣"} ${Math.abs(amount)} 分`
: `🔴 B隊 ${amount > 0 ? "得" : "扣"} ${Math.abs(amount)} 分`

);


saveGame();

}


/* =========================================
   比分歸零
========================================= */

function resetScore(){

state.scoreA = 0;

state.scoreB = 0;

renderScore();

addHistory(
"🏐 比分歸零"
);

saveGame();

}


/* =========================================
   抽卡
========================================= */

function drawCard(team){

if(
remainingCards.length === 0
){

alert(
"🎴 牌庫已經抽完！"
);

return;

}


const randomIndex =
Math.floor(
Math.random() *
remainingCards.length
);


const id =
remainingCards.splice(
randomIndex,
1
)[0];


const card =
getCard(id);


/* ===== 雙方卡 ===== */

if(card.type === "both"){

addHistory(

`${team === "A" ? "🔵 A隊" : "🔴 B隊"} 抽到 🟡【${card.name}】→ 立即使用`

);

showCardModal(card);

saveGame();

return;

}


/* ===== 一般卡 ===== */

if(team === "A"){

state.ownedA.push(id);

}

else{

state.ownedB.push(id);

}


addHistory(

`${team === "A" ? "🔵 A隊" : "🔴 B隊"} 抽到【${card.name}】`

);


renderHands();

saveGame();

}


/* =========================================
   使用卡片
========================================= */

function useCard(team,id){

let list =
team === "A"
? state.ownedA
: state.ownedB;


const index =
list.indexOf(id);


if(index === -1){

return;

}


list.splice(
index,
1
);


const card =
getCard(id);


addHistory(

`${team === "A" ? "🔵 A隊" : "🔴 B隊"} 使用【${card.name}】`

);


showCardModal(card);

renderHands();

saveGame();

}


/* =========================================
   顯示卡片 Modal
========================================= */

function showCardModal(card){

const typeElement =
document.getElementById(
"modalType"
);


if(card.type === "good"){

typeElement.textContent =
"🟢 好卡";

}

else if(card.type === "bad"){

typeElement.textContent =
"🔴 壞卡";

}

else{

typeElement.textContent =
"🟡 雙方卡・立即使用";

}


document.getElementById(
"modalName"
).textContent =
card.name;


document.getElementById(
"modalText"
).textContent =
card.text;


document.getElementById(
"modal"
).classList.add(
"show"
);

}


/* =========================================
   關閉 Modal
========================================= */

function closeModal(){

document.getElementById(
"modal"
).classList.remove(
"show"
);

}


/* =========================================
   顯示比分
========================================= */

function renderScore(){

document.getElementById(
"scoreA"
).textContent =
state.scoreA;


document.getElementById(
"scoreB"
).textContent =
state.scoreB;

}


/* =========================================
   顯示持有卡
========================================= */

function renderHands(){

renderTeamHand(
"A",
state.ownedA,
"handA"
);


renderTeamHand(
"B",
state.ownedB,
"handB"
);


renderTeamHand(
"A",
state.ownedA,
"ownedA"
);


renderTeamHand(
"B",
state.ownedB,
"ownedB"
);

}


function renderTeamHand(
team,
list,
elementId
){

const element =
document.getElementById(
elementId
);


if(list.length === 0){

element.innerHTML =
`<div class="empty">
目前沒有持有卡片
</div>`;

return;

}


element.innerHTML =
list.map(id => {

const card =
getCard(id);


return `

<div class="card-small ${card.type}">

${card.name}

<button
class="use-button"
onclick="useCard('${team}',${id})">

使用

</button>

</div>

`;

}).join("");

}


/* =========================================
   卡片圖鑑
========================================= */

function showCards(type,button){

document
.querySelectorAll(".tabs button")
.forEach(btn => {

btn.classList.remove(
"active"
);

});


button.classList.add(
"active"
);


const list =
document.getElementById(
"cardList"
);


list.innerHTML =
cards

.filter(card => {

return type === "all"
||
card.type === type;

})

.map(card => {

let typeName;

if(card.type === "good"){

typeName =
"🟢 好卡";

}

else if(card.type === "bad"){

typeName =
"🔴 壞卡";

}

else{

typeName =
"🟡 雙方卡";

}


return `

<div class="card ${card.type}">

<div class="card-type">

${typeName}

</div>

<div class="card-name">

${card.name}

</div>

<div class="card-description">

${card.text}

</div>

</div>

`;

})

.join("");

}


/* =========================================
   比賽紀錄
========================================= */

function addHistory(text){

const now =
new Date().toLocaleTimeString(
"zh-TW",
{
hour:"2-digit",
minute:"2-digit",
second:"2-digit"
}
);


state.history.unshift(
`${now}　${text}`
);


state.history =
state.history.slice(
0,
50
);


renderHistory();

}


function renderHistory(){

const element =
document.getElementById(
"history"
);


if(state.history.length === 0){

element.innerHTML =
`<div class="empty">
目前沒有比賽紀錄
</div>`;

return;

}


element.innerHTML =
state.history
.map(item => {

return `

<div class="history-item">

${item}

</div>

`;

})
.join("");

}


/* =========================================
   清除存檔
========================================= */

function clearSave(){

const confirmDelete =
confirm(

"⚠️ 確定要清除所有遊戲資料嗎？\n\n" +

"比分、手牌、已抽卡片與比賽紀錄都會消失。"

);


if(!confirmDelete){

return;

}


localStorage.removeItem(
SAVE_KEY
);


state = {

scoreA:0,

scoreB:0,

ownedA:[],

ownedB:[],

history:[]

};


resetDeck();

renderScore();

renderHands();

renderHistory();

addHistory(
"🔄 已清除所有資料並重新開始"
);

saveGame();

}


/* =========================================
   關閉網頁前保存
========================================= */

window.addEventListener(
"beforeunload",
function(){

saveGame();

}
);


/* =========================================
   啟動遊戲
========================================= */

loadGame();

showCards(
"all",
document.querySelector(
".tabs button"
)
);

renderScore();

renderHands();

renderHistory();


if(state.history.length === 0){

addHistory(
"🏐 遊戲開始"
);

saveGame();

}

else{

document.getElementById(
"saveStatus"
).textContent =
"💾 已恢復上次遊戲進度";

}

</script>

</body>
</html>
