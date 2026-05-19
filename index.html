<!-- =====================================================
INDEX.HTML
===================================================== -->

<!DOCTYPE html>
<html>

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Offline Exam PWA</title>

<link rel="manifest" href="manifest.json">

<style>

body{
    margin:0;
    font-family:Arial;
    background:#f2f2f2;
}

.screen{
    display:none;
    padding:20px;
}

.active{
    display:block;
}

button{
    width:100%;
    padding:15px;
    margin-top:15px;
    border:none;
    border-radius:10px;
    background:#2563eb;
    color:white;
    font-size:18px;
}

.option{
    background:white;
    padding:15px;
    margin-top:10px;
    border-radius:10px;
    border:2px solid #ddd;
}

.selected{
    background:#dbeafe;
    border:2px solid #2563eb;
}

#timer{
    font-size:24px;
    color:red;
    text-align:center;
    margin-bottom:20px;
}

textarea{
    width:100%;
    height:120px;
}

</style>

</head>

<body>

<!-- HOME -->

<div id="homeScreen" class="screen active">

    <h1>Offline Exam</h1>

    <input id="examCode"
           placeholder="Enter Exam Code"
           style="width:100%;padding:15px;font-size:18px;">

    <button onclick="downloadExam()">
        Download Exam
    </button>

    <button onclick="startExam()">
        Start Offline Exam
    </button>

</div>

<!-- EXAM -->

<div id="examScreen" class="screen">

    <div id="timer"></div>

    <h2 id="questionText"></h2>

    <div id="optionsContainer"></div>

    <button onclick="nextQuestion()">
        Next
    </button>

</div>

<!-- FINISH -->

<div id="finishScreen" class="screen">

    <h1>Exam Finished</h1>

    <h2 id="scoreText"></h2>

    <button onclick="uploadResults()">
        Upload Results
    </button>

    <textarea id="logBox"></textarea>

</div>

<script>

/////////////////////////////////////////////////////////
// SERVICE WORKER
/////////////////////////////////////////////////////////

if("serviceWorker" in navigator){

    navigator.serviceWorker.register("sw.js");

}

/////////////////////////////////////////////////////////
// GOOGLE SCRIPT URL
/////////////////////////////////////////////////////////

const API_URL =
"https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec";

/////////////////////////////////////////////////////////
// VARIABLES
/////////////////////////////////////////////////////////

let exam = null;

let currentQuestion = 0;

let score = 0;

let selectedAnswer = null;

let answers = [];

let logs = [];

let timeLeft = 0;

let timerInterval = null;

/////////////////////////////////////////////////////////
// SCREEN CONTROL
/////////////////////////////////////////////////////////

function showScreen(id){

    document.querySelectorAll(".screen")
    .forEach(s=>{

        s.classList.remove("active");

    });

    document.getElementById(id)
    .classList.add("active");
}

/////////////////////////////////////////////////////////
// DOWNLOAD EXAM
/////////////////////////////////////////////////////////

async function downloadExam(){

    const examCode =
        document.getElementById("examCode").value;

    const response =
        await fetch(
            API_URL + "?mode=getExam&examId=" + examCode
        );

    const data = await response.json();

    localStorage.setItem(
        "ACTIVE_EXAM",
        JSON.stringify(data)
    );

    alert("Exam downloaded");
}

/////////////////////////////////////////////////////////
// START EXAM
/////////////////////////////////////////////////////////

function startExam(){

    const stored =
        localStorage.getItem("ACTIVE_EXAM");

    if(!stored){

        alert("No exam downloaded");

        return;
    }

    exam = JSON.parse(stored);

    currentQuestion = 0;

    score = 0;

    answers = [];

    logs = [];

    timeLeft = exam.duration;

    startTimer();

    showScreen("examScreen");

    renderQuestion();
}

/////////////////////////////////////////////////////////
// RENDER QUESTION
/////////////////////////////////////////////////////////

function renderQuestion(){

    selectedAnswer = null;

    const q = exam.questions[currentQuestion];

    document.getElementById("questionText")
    .innerText =
        (currentQuestion + 1)
        + ". "
        + q.question;

    const container =
        document.getElementById("optionsContainer");

    container.innerHTML = "";

    q.options.forEach((opt,index)=>{

        const div =
            document.createElement("div");

        div.className = "option";

        div.innerText = opt;

        div.onclick = ()=>{

            document.querySelectorAll(".option")
            .forEach(o=>{

                o.classList.remove("selected");

            });

            div.classList.add("selected");

            selectedAnswer = index;
        };

        container.appendChild(div);

    });
}

/////////////////////////////////////////////////////////
// NEXT QUESTION
/////////////////////////////////////////////////////////

function nextQuestion(){

    if(selectedAnswer === null){

        alert("Select answer");

        return;
    }

    const q = exam.questions[currentQuestion];

    answers.push(selectedAnswer);

    if(selectedAnswer === q.answer){

        score++;
    }

    currentQuestion++;

    autosave();

    if(currentQuestion >= exam.questions.length){

        finishExam();

    }else{

        renderQuestion();
    }
}

/////////////////////////////////////////////////////////
// TIMER
/////////////////////////////////////////////////////////

function startTimer(){

    updateTimer();

    timerInterval = setInterval(()=>{

        timeLeft--;

        updateTimer();

        if(timeLeft <= 0){

            finishExam();

        }

    },1000);
}

function updateTimer(){

    const mins =
        Math.floor(timeLeft / 60);

    const secs =
        timeLeft % 60;

    document.getElementById("timer")
    .innerText =
        mins + ":" +
        String(secs).padStart(2,"0");
}

/////////////////////////////////////////////////////////
// AUTOSAVE
/////////////////////////////////////////////////////////

function autosave(){

    localStorage.setItem(
        "EXAM_PROGRESS",
        JSON.stringify({
            answers,
            currentQuestion,
            score,
            logs
        })
    );
}

/////////////////////////////////////////////////////////
// LOGGING
/////////////////////////////////////////////////////////

document.addEventListener(
    "visibilitychange",
    ()=>{

        if(document.hidden){

            logs.push({
                event:"HIDDEN",
                time:Date.now()
            });

        }else{

            logs.push({
                event:"VISIBLE",
                time:Date.now()
            });

        }

        autosave();
    }
);

window.addEventListener(
    "online",
    ()=>{

        logs.push({
            event:"ONLINE_DETECTED",
            time:Date.now()
        });

        autosave();
    }
);

window.addEventListener(
    "offline",
    ()=>{

        logs.push({
            event:"OFFLINE",
            time:Date.now()
        });

        autosave();
    }
);

/////////////////////////////////////////////////////////
// FINISH
/////////////////////////////////////////////////////////

function finishExam(){

    clearInterval(timerInterval);

    showScreen("finishScreen");

    document.getElementById("scoreText")
    .innerText =
        "Score: "
        + score
        + " / "
        + exam.questions.length;

    document.getElementById("logBox")
    .value =
        JSON.stringify(logs,null,2);
}

/////////////////////////////////////////////////////////
// UPLOAD RESULTS
/////////////////////////////////////////////////////////

async function uploadResults(){

    const payload = {

        student:"STUDENT01",

        examId:exam.examId,

        score:score,

        answers:answers,

        logs:logs

    };

    await fetch(API_URL,{

        method:"POST",

        body:JSON.stringify(payload)

    });

    alert("Results uploaded");
}

</script>

</body>
</html>
