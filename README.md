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
        { text: "Bold rings and standout pieces", letter: "G" },
        { text: "Minimalist jewelry — simple but stunning", letter: "H" },
        { text: "Classic watch or casual belt", letter: "I" },
      ]
    },
    {
      question: "What’s your hair vibe?",
      answers: [
        { text: "Big, voluminous, and flawless", letter: "A" },
        { text: "Sleek and glossy, always on point", letter: "B" },
        { text: "Natural waves or a messy bun — effortlessly cool", letter: "C" },
        { text: "Neat and polished, with soft curls or a bun", letter: "D" },
        { text: "High ponytail or sleek straight hair, super iconic", letter: "E" },
        { text: "Short or long, always rocking the latest cut", letter: "F" },
        { text: "Bold styles — braids, colors, or unique cuts", letter: "G" },
        { text: "Smooth and elegant, often tied back", letter: "H" },
        { text: "Natural, easygoing, and simple", letter: "I" },
      ]
    },
    {
      question: "Your fave style inspiration:",
      answers: [
        { text: "Runway glam and red carpet moments", letter: "A" },
        { text: "Supermodel elegance and poise", letter: "B" },
        { text: "Street style and everyday chic", letter: "C" },
        { text: "Feminine, eco-friendly, and smart vibes", letter: "D" },
        { text: "Pop star glamour and fun energy", letter: "E" },
        { text: "Trendsetting and fearless fashion moments", letter: "F" },
        { text: "Fearless, bold, and unapologetically you", letter: "G" },
        { text: "Classic Hollywood sophistication", letter: "H" },
        { text: "Effortless casual cool", letter: "I" },
      ]
    },
    {
      question: "Your perfect shoes:",
      answers: [
        { text: "Heels that make a statement", letter: "A" },
        { text: "Designer stilettos or classy boots", letter: "B" },
        { text: "Sneakers or ankle boots for comfort", letter: "C" },
        { text: "Ballet flats or elegant heels", letter: "D" },
        { text: "Platform boots or cute sneakers with sparkle", letter: "E" },
        { text: "Chunky boots or edgy heels", letter: "F" },
        { text: "Statement heels or fierce boots", letter: "G" },
        { text: "Classic pumps or sleek boots", letter: "H" },
        { text: "Casual loafers or white sneakers", letter: "I" },
      ]
    }
  ];

  const celebResults = {
    A: { name: "Beyoncé", desc: "Bold, glamorous, and totally unforgettable." },
    B: { name: "Adriana Lima", desc: "Chic, elegant, and runway ready." },
    C: { name: "Gigi Hadid", desc: "Casual cool with a fierce street style edge." },
    D: { name: "Emma Watson", desc: "Feminine, polished, and smart with a modern twist." },
    E: { name: "Ariana Grande", desc: "Fun, playful, and full of pop star sparkle." },
    F: { name: "Zendaya", desc: "Edgy, fearless, and always setting trends." },
    G: { name: "Rihanna", desc: "Bold, fearless, and unapologetically unique." },
    H: { name: "Angelina Jolie", desc: "Sleek, timeless, and effortlessly sophisticated." },
    I: { name: "Jennifer Aniston", desc: "Classic, laid-back, and forever cool with that polo top vibe." }
  };

  let currentQuestionIndex = 0;
  let scores = { A: 0, B: 0, C: 0, D: 0, E: 0, F: 0, G: 0, H: 0, I: 0 };

  const questionEl = document.getElementById('question');
  const answersEl = document.getElementById('answers');
  const resultEl = document.getElementById('result');
  const restartBtn = document.getElementById('restart-btn');

  function showQuestion() {
    const q = quizData[currentQuestionIndex];
    questionEl.textContent = q.question;
    answersEl.innerHTML = '';
    q.answers.forEach(answer => {
      const btn = document.createElement('button');
      btn.textContent = answer.text;
      btn.addEventListener('click', () => selectAnswer(answer.letter));
      answersEl.appendChild(btn);
    });
  }

  function selectAnswer(letter) {
    scores[letter]++;
    currentQuestionIndex++;
    if (currentQuestionIndex < quizData.length) {
      showQuestion();
    } else {
      showResult();
    }
  }

  function showResult() {
    questionEl.style.display = 'none';
    answersEl.style.display = 'none';
    restartBtn.style.display = 'inline-block';

    let maxScore = 0;
    let topLetter = '';
    for (const letter in scores) {
      if (scores[letter] > maxScore) {
        maxScore = scores[letter];
        topLetter = letter;
      }
    }

    const celeb = celebResults[topLetter];
    resultEl.style.display = 'block';
    resultEl.innerHTML = `You’re <strong>${celeb.name}</strong> — ${celeb.desc}`;
  }

  restartBtn.addEventListener('click', () => {
    currentQuestionIndex = 0;
    scores = { A: 0, B: 0, C: 0, D: 0, E: 0, F: 0, G: 0, H: 0, I: 0 };
    questionEl.style.display = 'block';
    answersEl.style.display = 'block';
    resultEl.style.display = 'none';
    restartBtn.style.display = 'none';
    showQuestion();
  });

  showQuestion();
</script>

</body>
</html>



