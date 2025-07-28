# Celeb-look-quiz

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>What Celeb Is Your Look?</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #f8cdda, #1d2b64);
      color: #333;
      margin: 0;
      padding: 20px;
      display: flex; flex-direction: column; align-items: center;
    }
    h1 {
      color: #fff;
      margin-bottom: 10px;
    }
    #quiz-container {
      background: #fff;
      border-radius: 12px;
      max-width: 600px;
      padding: 25px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.2);
    }
    .question {
      font-size: 1.2em;
      margin-bottom: 15px;
    }
    .answers button {
      display: block;
      width: 100%;
      background: #f0f0f0;
      border: none;
      padding: 12px 15px;
      margin: 8px 0;
      border-radius: 8px;
      font-size: 1em;
      cursor: pointer;
      transition: background 0.3s;
    }
    .answers button:hover {
      background: #d1c4e9;
    }
    #result {
      margin-top: 20px;
      font-size: 1.3em;
      font-weight: bold;
      color: #5a2a83;
    }
    #restart-btn {
      margin-top: 20px;
      padding: 10px 20px;
      background: #5a2a83;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    #restart-btn:hover {
      background: #7e54b6;
    }
  </style>
</head>
<body>

<h1>What Celeb Is Your Look?</h1>
<div id="quiz-container">
  <div id="question-container">
    <div class="question" id="question"></div>
    <div class="answers" id="answers"></div>
  </div>
  <div id="result" style="display:none;"></div>
  <button id="restart-btn" style="display:none;">Try Again</button>
</div>

<script>
  const quizData = [
    {
      question: "What’s your go-to outfit for a night out?",
      answers: [
        { text: "Bold, glamorous, and eye-catching (think glitter and power!)", letter: "A" },
        { text: "Chic and elegant — simple but makes a statement", letter: "B" },
        { text: "Casual cool — comfy but stylish, like you just woke up flawless", letter: "C" },
        { text: "Feminine and polished — classic with a modern twist", letter: "D" },
        { text: "Fun and flirty — playful with a pop star sparkle", letter: "E" },
        { text: "Edgy and fashion-forward — always setting trends", letter: "F" },
        { text: "Bold and fearless — mixing styles and breaking rules", letter: "G" },
        { text: "Sleek and timeless — black dress or sharp blazer vibes", letter: "H" },
        { text: "Classic and laid-back — think polo tops and effortless jeans", letter: "I" },
      ]
    },
    {
      question: "Pick your fave accessory:",
      answers: [
        { text: "Statement earrings that sparkle", letter: "A" },
        { text: "Designer sunglasses or a sleek clutch", letter: "B" },
        { text: "Trendy sneakers or a cool hat", letter: "C" },
        { text: "Delicate jewelry, like pearls or simple rings", letter: "D" },
        { text: "High ponytail scrunchie or sparkly hair clips", letter: "E" },
        { text: "Chunky boots or layered necklaces", letter: "F" },
        { text: "Bold rings and standout pieces",
