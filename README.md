<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>MicroWin - Improve 1% Every Day</title>

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
:root {
  --primary: linear-gradient(135deg,#0f2027,#2c5364,#6a11cb);
  --card-bg:#ffffff;
  --text-dark:#111;
  --text-light:#777;
}

body {
  margin:0;
  font-family:Inter,sans-serif;
  background:linear-gradient(135deg,#0f2027,#2c5364,#6a11cb);
  color:white;
  display:flex;
  flex-direction:column;
  align-items:center;
}

.container{
  width:100%;
  max-width:420px;
  padding:20px;
}

.header{
  display:flex;
  justify-content:space-between;
  align-items:center;
}

.streak{
  font-weight:600;
  background:rgba(255,255,255,0.2);
  padding:8px 14px;
  border-radius:20px;
}

.card{
  margin-top:20px;
  background:white;
  color:#111;
  padding:20px;
  border-radius:20px;
  box-shadow:0 8px 20px rgba(0,0,0,0.2);
}

.card h3{
  margin-top:0;
}

.btn{
  margin-top:15px;
  padding:12px;
  border:none;
  width:100%;
  border-radius:12px;
  cursor:pointer;
  font-weight:600;
}

.primary{
  background:#6a11cb;
  color:white;
}

.secondary{
  background:#eee;
}

.graph-container{
  margin-top:20px;
  background:white;
  padding:20px;
  border-radius:20px;
}

.navbar{
  position:fixed;
  bottom:0;
  width:100%;
  max-width:420px;
  display:flex;
  justify-content:space-around;
  background:white;
  padding:10px 0;
  border-top-left-radius:20px;
  border-top-right-radius:20px;
}

.navbar button{
  background:none;
  border:none;
  font-weight:600;
  color:#6a11cb;
  cursor:pointer;
}

.level{
  margin-top:10px;
  font-size:14px;
}

.fade{
  animation:fade 0.5s ease-in-out;
}

@keyframes fade{
  from{opacity:0;transform:translateY(10px)}
  to{opacity:1;transform:translateY(0)}
}
</style>
</head>

<body>

<div class="container">

  <div class="header">
    <h2>MicroWin</h2>
    <div class="streak">🔥 Streak: <span id="streak">0</span></div>
  </div>

  <div class="card fade">
    <h3>Today’s 1% Win</h3>
    <p id="task">Do 5 pushups after brushing teeth.</p>
    <p style="color:#777;font-size:14px;">Why it matters: Builds consistency.</p>
    <p style="color:#999;font-size:12px;">Estimated time: 2 mins</p>

    <button class="btn primary" onclick="completeTask()">✔ I Did It</button>
    <button class="btn secondary" onclick="replaceTask()">Replace Task</button>

    <div class="level">
      🌱 Level: <span id="level">Seed</span>
    </div>
  </div>

  <div class="graph-container">
    <h3>365-Day Growth Projection</h3>
    <canvas id="growthChart"></canvas>
  </div>

  <div class="card" id="futureCard">
    <h3>Future You</h3>
    <p id="futureText">Keep going 30 days to unlock your next level.</p>
  </div>

</div>

<div class="navbar">
  <button onclick="showHome()">Home</button>
  <button onclick="showFuture()">Future</button>
  <button onclick="showProgress()">Progress</button>
</div>

<script>

let streak = localStorage.getItem("streak") || 0;
document.getElementById("streak").innerText = streak;

function completeTask(){
  streak++;
  localStorage.setItem("streak",streak);
  document.getElementById("streak").innerText=streak;
  updateLevel();
  alert("🎉 MicroWin Completed!");
}

function replaceTask(){
  const tasks=[
    "Read 2 pages of a book.",
    "Meditate for 3 minutes.",
    "Write 3 lines of gratitude.",
    "Practice coding for 5 minutes.",
    "Speak one positive affirmation."
  ];
  document.getElementById("task").innerText=
  tasks[Math.floor(Math.random()*tasks.length)];
}

function updateLevel(){
  let level="Seed";
  if(streak>7) level="Sapling";
  if(streak>30) level="Tree";
  if(streak>90) level="Forest";
  document.getElementById("level").innerText=level;
}

updateLevel();

/* Growth Chart */
const ctx=document.getElementById("growthChart").getContext("2d");
const data=[];
let value=1;
for(let i=0;i<=365;i++){
  data.push(value);
  value*=1.01;
}
new Chart(ctx,{
  type:"line",
  data:{
    labels:Array.from({length:366},(_,i)=>i),
    datasets:[{
      label:"1% Daily Growth",
      data:data,
      borderColor:"#6a11cb",
      fill:false,
      tension:0.3
    }]
  },
  options:{
    responsive:true,
    plugins:{
      legend:{display:false}
    },
    scales:{
      x:{display:false},
      y:{display:false}
    }
  }
});

/* Future Projection Logic */
function showFuture(){
  let futureMsg="If you continue for 30 days, your confidence will grow significantly.";
  if(streak>30) futureMsg="90 Day Mark: Noticeable skill shift.";
  if(streak>90) futureMsg="180 Days: People start recognizing the change.";
  if(streak>180) futureMsg="365 Days: 37x Version of You.";
  document.getElementById("futureText").innerText=futureMsg;
}

function showHome(){
  alert("Home Screen");
}

function showProgress(){
  alert("Detailed analytics coming soon in Pro.");
}

</script>

</body>
</html>
