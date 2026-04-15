<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ujian Hiragana</title>

<style>
body {
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(135deg, #4facfe, #00f2fe);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.container {
  background: white;
  padding: 25px;
  width: 320px;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 10px 25px rgba(0,0,0,0.2);
}

.hiragana {
  font-size: 60px;
  margin: 20px 0;
}

button {
  width: 100%;
  padding: 10px;
  margin: 5px 0;
  border: none;
  border-radius: 8px;
  background: #4facfe;
  color: white;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background: #007bff;
}

.info {
  margin-bottom: 10px;
  font-size: 14px;
}

.result {
  margin-top: 10px;
  font-weight: bold;
}
</style>
</head>

<body>

<div class="container">
  <h1>Ujian Hiragana</h1>

  <div class="info">
    Skor: <span id="score">0</span>
  </div>

  <div class="hiragana" id="question">あ</div>

  <div id="options"></div>

  <div class="result" id="result"></div>
</div>

<script>
const questions = [
  {h:"あ",a:"a"},{h:"い",a:"i"},{h:"う",a:"u"},{h:"え",a:"e"},{h:"お",a:"o"},
  {h:"か",a:"ka"},{h:"き",a:"ki"},{h:"く",a:"ku"},{h:"け",a:"ke"},{h:"こ",a:"ko"},
  {h:"さ",a:"sa"},{h:"し",a:"shi"},{h:"す",a:"su"},{h:"せ",a:"se"},{h:"そ",a:"so"},
  {h:"た",a:"ta"},{h:"ち",a:"chi"},{h:"つ",a:"tsu"},{h:"て",a:"te"},{h:"と",a:"to"},
  {h:"な",a:"na"},{h:"に",a:"ni"},{h:"ぬ",a:"nu"},{h:"ね",a:"ne"},{h:"の",a:"no"},
  {h:"は",a:"ha"},{h:"ひ",a:"hi"},{h:"ふ",a:"fu"},{h:"へ",a:"he"},{h:"ほ",a:"ho"},
  {h:"ま",a:"ma"},{h:"み",a:"mi"},{h:"む",a:"mu"},{h:"め",a:"me"},{h:"も",a:"mo"},
  {h:"や",a:"ya"},{h:"ゆ",a:"yu"},{h:"よ",a:"yo"},
  {h:"ら",a:"ra"},{h:"り",a:"ri"},{h:"る",a:"ru"},{h:"れ",a:"re"},{h:"ろ",a:"ro"},
  {h:"わ",a:"wa"},{h:"を",a:"wo"},{h:"ん",a:"n"}
];

let current = 0;
let score = 0;

function shuffle(array){
  return array.sort(() => Math.random() - 0.5);
}

function loadQuestion(){
  if(current >= questions.length){
    endGame();
    return;
  }

  document.getElementById("question").innerText = questions[current].h;

  let answers = [questions[current].a];
  while(answers.length < 4){
    let rand = questions[Math.floor(Math.random()*questions.length)].a;
    if(!answers.includes(rand)) answers.push(rand);
  }

  answers = shuffle(answers);

  let html = "";
  answers.forEach(ans=>{
    html += `<button onclick="checkAnswer('${ans}')">${ans}</button>`;
  });

  document.getElementById("options").innerHTML = html;
  document.getElementById("result").innerText = "";
}

function checkAnswer(ans){
  if(ans === questions[current].a){
    score++;
    document.getElementById("score").innerText = score;
    document.getElementById("result").innerText = "✅ Benar";
  } else {
    document.getElementById("result").innerText = "❌ Salah";
  }

  current++;
  setTimeout(loadQuestion, 700);
}

function endGame(){
  document.getElementById("question").innerText = "Selesai!";
  document.getElementById("options").innerHTML = "";
  document.getElementById("result").innerText = "Skor kamu: " + score + "/" + questions.length;
}

loadQuestion();
</script>

</body>
</html>
