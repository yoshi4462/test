<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>反射神経テスト</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>反射神経テスト</h1>
    <p>画面が赤くなったらすぐにクリックしてください！</p>
    <div id="testArea" class="test-area"></div>
    <p id="result"></p>
    <button id="startButton">スタート</button>
  </div>
  <script src="script.js"></script>
</body>
</html>

{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f4f4f4;
  }
  
  .container {
    text-align: center;
  }
  
  .test-area {
    width: 300px;
    height: 300px;
    background-color: #3498db;
    margin: 20px auto;
    border-radius: 10px;
    cursor: pointer;
  }
  
  button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
  }

let startTime;
let reactionTime;
let timeoutId;

const testArea = document.getElementById('testArea');
const result = document.getElementById('result');
const startButton = document.getElementById('startButton');

startButton.addEventListener('click', startTest);

function startTest() {
  result.textContent = '';
  testArea.style.backgroundColor = '#3498db';
  startButton.disabled = true;

  // ランダムな時間 (2〜5秒) 後に色を変える
  const randomTime = Math.floor(Math.random() * 3000) + 2000;

  timeoutId = setTimeout(() => {
    testArea.style.backgroundColor = 'red';
    startTime = new Date();
  }, randomTime);

  testArea.addEventListener('click', handleClick);
}

function handleClick() {
  // 背景が赤くなってからクリックした場合のみ反応時間を計測
  if (testArea.style.backgroundColor === 'red') {
    reactionTime = (new Date() - startTime) / 1000; // 秒で表示
    result.textContent = `反応時間: ${reactionTime}秒`;
    resetTest();
  } else {
    result.textContent = 'まだ赤くなっていません！';
  }
}

function resetTest() {
  clearTimeout(timeoutId);
  startButton.disabled = false;
  testArea.removeEventListener('click', handleClick);
}
