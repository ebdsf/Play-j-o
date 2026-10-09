
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jogo do Jão</title>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #100d18, #32102b, #111827);
      color: white;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .container {
      width: 100%;
      max-width: 500px;
      text-align: center;
      background: rgba(255, 255, 255, 0.07);
      border: 1px solid rgba(255, 255, 255, 0.15);
      border-radius: 24px;
      padding: 30px 22px;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
    }

    .tag {
      color: #ff789c;
      letter-spacing: 4px;
      font-size: 12px;
      font-weight: bold;
      margin-bottom: 18px;
    }

    h1 {
      font-size: 42px;
      margin-bottom: 12px;
    }

    h1 span {
      color: #ff527f;
    }

    .subtitle {
      color: #d4cbd9;
      line-height: 1.6;
      margin-bottom: 25px;
    }

    .info {
      display: flex;
      justify-content: space-between;
      margin-bottom: 22px;
      color: #f4c4d4;
      font-size: 14px;
    }

    #question {
      font-size: 21px;
      line-height: 1.4;
      margin-bottom: 22px;
    }

    .answers {
      display: grid;
      gap: 12px;
    }

    .answer, .main-button {
      border: none;
      border-radius: 12px;
      padding: 15px;
      font-size: 16px;
      cursor: pointer;
      transition: 0.2s;
    }

    .answer {
      background: #292235;
      border: 1px solid #51405d;
      color: white;
      text-align: left;
    }

    .answer:hover:not(:disabled) {
      background: #493044;
      transform: translateY(-2px);
    }

    .answer:disabled {
      cursor: default;
      opacity: 0.9;
    }

    .correct {
      background: #176747 !important;
      border-color: #35d99a !important;
    }

    .wrong {
      background: #762c43 !important;
      border-color: #ff6b88 !important;
    }

    #feedback {
      min-height: 30px;
      margin-top: 18px;
      font-size: 15px;
    }

    .main-button {
      background: #ff527f;
      color: white;
      font-weight: bold;
      width: 100%;
      margin-top: 12px;
    }

    .main-button:hover {
      background: #e93c6b;
      transform: scale(1.02);
    }

    .hidden {
      display: none;
    }

    .footer {
      color: #a99caf;
      font-size: 12px;
      margin-top: 24px;
    }
  </style>
</head>

<body>
  <main class="container">
    <div class="tag">QUIZ DOS FÃS</div>

    <section id="start">
      <h1>JOGO DO <span>JAO</span></h1>

      <p class="subtitle">
        Você conhece mesmo o universo do Jão?
        Teste seus conhecimentos e descubra sua pontuação!
      </p>

      <button class="main-button" onclick="startGame()">
        Começar jogo
      </button>
    </section>

    <section id="game" class="hidden">
      <div class="info">
        <span id="progress">Pergunta 1/5</span>
        <span id="score">Pontos: 0</span>
      </div>

      <h2 id="question"></h2>

      <div class="answers" id="answers"></div>

      <p id="feedback" aria-live="polite"></p>

      <button
        class="main-button hidden"
        id="next"
        onclick="nextQuestion()">
        Próxima pergunta
      </button>
    </section>

    <section id="result" class="hidden">
      <h1 id="resultTitle">Fim de jogo!</h1>
      <p class="subtitle" id="resultText"></p>

      <button class="main-button" onclick="startGame()">
        Jogar novamente
      </button>
    </section>

    <p class="footer">
      Jogo de fã, sem vínculo oficial com o artista.
    </p>
  </main>

  <script>
    const questions = [
      {
        question: "Qual é o nome verdadeiro do Jão?",
        answers: [
          "João Vitor Romania Balbino",
          "João Pedro Silva",
          "João Lucas Martins",
          "João Victor Santos"
        ],
        correct: 0
      },
      {
        question: "Qual é o nome do álbum de estreia do Jão?",
        answers: [
          "Anti-Herói",
          "Lobos",
          "Pirata",
          "SUPER"
        ],
        correct: 1
      },
      {
        question: "Qual destes álbuns do Jão foi lançado em 2021?",
        answers: [
          "Lobos",
          "SUPER",
          "Pirata",
          "Anti-Herói"
        ],
        correct: 2
      },
      {
        question: "Qual é o nome do álbum lançado em 2023?",
        answers: [
          "Pirata",
          "Lobos",
          "Anti-Herói",
          "SUPER"
        ],
        correct: 3
      },
      {
        question: "Qual é o nome artístico do cantor?",
        answers: [
          "Jão",
          "Jota",
          "Joãozinho",
          "J.V."
        ],
        correct: 0
      }
    ];

    let currentQuestion = 0;
    let points = 0;
    let answered = false;

    function startGame() {
      currentQuestion = 0;
      points = 0;

      document.getElementById("start").classList.add("hidden");
      document.getElementById("result").classList.add("hidden");
      document.getElementById("game").classList.remove("hidden");

      showQuestion();
    }

    function showQuestion() {
      answered = false;

      const q = questions[currentQuestion];

      document.getElementById("progress").textContent =
        `Pergunta ${currentQuestion + 1}/${questions.length}`;

      document.getElementById("score").textContent =
        `Pontos: ${points}`;

      document.getElementById("question").textContent = q.question;
      document.getElementById("feedback").textContent = "";
      document.getElementById("next").classList.add("hidden");

      const answers = document.getElementById("answers");
      answers.innerHTML = "";

      q.answers.forEach((answer, index) => {
        const button = document.createElement("button");

        button.className = "answer";
        button.textContent = answer;
        button.onclick = () => checkAnswer(index, button);

        answers.appendChild(button);
      });
    }

    function checkAnswer(index, button) {
      if (answered) return;

      answered = true;

      const q = questions[currentQuestion];
      const buttons = document.querySelectorAll(".answer");

      buttons.forEach((b, i) => {
        b.disabled = true;

        if (i === q.correct) {
          b.classList.add("correct");
        }
      });

      if (index === q.correct) {
        points++;
        document.getElementById("feedback").textContent =
          "Acertou! Você conhece o Jão!";
      } else {
        button.classList.add("wrong");
        document.getElementById("feedback").textContent =
          "Não foi dessa vez! A resposta certa está em verde.";
      }

      document.getElementById("score").textContent =
        `Pontos: ${points}`;

      const next = document.getElementById("next");
      next.textContent =
        currentQuestion === questions.length - 1
          ? "Ver resultado"
          : "Próxima pergunta";

      next.classList.remove("hidden");
    }

    function nextQuestion() {
      currentQuestion++;

      if (currentQuestion < questions.length) {
        showQuestion();
      } else {
        showResult();
      }
    }

    function showResult() {
      document.getElementById("game").classList.add("hidden");
      document.getElementById("result").classList.remove("hidden");

      document.getElementById("resultTitle").textContent =
        points === questions.length
          ? "Você é fã de verdade!"
          : "Fim de jogo!";

      document.getElementById("resultText").textContent =
        `Você acertou ${points} de ${questions.length} perguntas!`;
    }
  </script>
</body>
</html>
