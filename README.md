# Online-quiz-system-mini-project
Online Quiz System mini project document
//index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Online Quiz System</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="quiz-container">
    <h2 id="quiz-title">Online Quiz System</h2>
    <div id="quiz-box">
        <p id="question"></p>

        <label>
            <input type="radio" name="option" value="0">
            <span id="opt0"></span>
        </label>

        <label>
            <input type="radio" name="option" value="1">
            <span id="opt1"></span>
        </label>

        <label>
            <input type="radio" name="option" value="2">
            <span id="opt2"></span>
        </label>

        <label>
            <input type="radio" name="option" value="3">
            <span id="opt3"></span>
        </label>

        <button onclick="nextQuestion()">Next</button>
    </div>

    <div id="result-box" class="hide">
        <h3>Your Score</h3>
        <p id="score"></p>
        <button onclick="restartQuiz()">Restart Quiz</button>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>

// style.css
body {
    font-family: Arial, sans-serif;
    background-color: #f2f2f2;
}

.quiz-container {
    width: 400px;
    margin: 50px auto;
    background: white;
    padding: 20px;
    border-radius: 10px;
}

h2 {
    text-align: center;
}

label {
    display: block;
    margin: 10px 0;
}

button {
    width: 100%;
    padding: 10px;
    margin-top: 15px;
    background-color: #4CAF50;
    color: white;
    border: none;
    font-size: 16px;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}

.hide {
    display: none;
}

// script.js
const quizData = [
    {
        question: "What is the capital of India?",
        options: ["Mumbai", "Delhi", "Chennai", "Kolkata"],
        answer: 1
    },
    {
        question: "Which language is used for web development?",
        options: ["Python", "HTML", "Java", "C"],
        answer: 1
    },
    {
        question: "Who is the father of Computer?",
        options: ["Charles Babbage", "Einstein", "Newton", "Tesla"],
        answer: 0
    },
    {
        question: "What does CPU stand for?",
        options: ["Central Process Unit", "Central Processing Unit", "Computer Personal Unit", "Control Processing Unit"],
        answer: 1
    }
];

let currentQuestion = 0;
let score = 0;

const questionEl = document.getElementById("question");
const options = document.querySelectorAll("input[name='option']");
const optionText = [
    document.getElementById("opt0"),
    document.getElementById("opt1"),
    document.getElementById("opt2"),
    document.getElementById("opt3")
];

function loadQuestion() {
    deselectOptions();
    let q = quizData[currentQuestion];
    questionEl.innerText = q.question;
    for (let i = 0; i < optionText.length; i++) {
        optionText[i].innerText = q.options[i];
    }
}

function deselectOptions() {
    options.forEach(option => option.checked = false);
}

function nextQuestion() {
    let selected = getSelectedOption();
    if (selected === null) {
        alert("Please select an answer");
        return;
    }

    if (selected == quizData[currentQuestion].answer) {
        score++;
    }

    currentQuestion++;

    if (currentQuestion < quizData.length) {
        loadQuestion();
    } else {
        showResult();
    }
}

function getSelectedOption() {
    let answer = null;
    options.forEach(option => {
        if (option.checked) {
            answer = option.value;
        }
    });
    return answer;
}

function showResult() {
    document.getElementById("quiz-box").classList.add("hide");
    document.getElementById("result-box").classList.remove("hide");
    document.getElementById("score").innerText =
        score + " / " + quizData.length;
}

function restartQuiz() {
    currentQuestion = 0;
    score = 0;
    document.getElementById("result-box").classList.add("hide");
    document.getElementById("quiz-box").classList.remove("hide");
    loadQuestion();
}

loadQuestion();
