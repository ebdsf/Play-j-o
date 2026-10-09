
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#080a12">
<title>Jogo do Jão | Uma Aventura Musical</title>

<style>
:root {
  --bg: #080a12;
  --panel: #111522;
  --red: #ff244f;
  --blue: #4097ff;
  --text: #f5f3fa;
  --muted: #aaaabd;
  --border: #30384d;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: var(--bg);
  color: var(--text);
  font-family: Arial, Helvetica, sans-serif;
  min-height: 100vh;
}

button {
  font: inherit;
  cursor: pointer;
  transition: .2s;
}

button:focus-visible {
  outline: 2px solid white;
  outline-offset: 3px;
}

.layout {
  display: grid;
  grid-template-columns: 225px minmax(0, 1fr);
  min-height: 100vh;
}

/* MENU LATERAL */

.sidebar {
  background: #070911;
  border-right: 1px solid #24283a;
  padding: 26px 16px;
  display: flex;
  flex-direction: column;
  gap: 28px;
}

.logo {
  font-size: 43px;
  font-weight: 900;
  font-style: italic;
  color: var(--red);
  letter-spacing: -3px;
}

.logo small {
  display: block;
  color: white;
  font-size: 10px;
  font-style: normal;
  letter-spacing: 3px;
  margin-top: 3px;
}

.nav {
  display: grid;
  gap: 8px;
}

.nav button {
  background: transparent;
  color: var(--text);
  border: 0;
  border-radius: 8px;
  padding: 14px 12px;
  text-align: left;
}

.nav button:hover,
.nav button.active {
  background: #28111e;
  color: var(--red);
}

.profile {
  margin-top: auto;
  border-top: 1px solid var(--border);
  padding-top: 20px;
}

.profile-row {
  display: flex;
  align-items: center;
  gap: 12px;
}

.avatar {
  width: 46px;
  height: 46px;
  border-radius: 50%;
  background: linear-gradient(135deg, #243d67, #a51d43);
  display: grid;
  place-items: center;
  font-size: 23px;
}

.profile small,
.muted {
  color: var(--muted);
  font-size: 12px;
}

.xp-bar {
  height: 7px;
  background: #272c3e;
  border-radius: 10px;
  overflow: hidden;
  margin: 13px 0 7px;
}

.xp-fill {
  width: 0;
  height: 100%;
  background: linear-gradient(90deg, var(--red), #ff9dba);
  transition: width .3s;
}

/* CABEÇALHO */

.hero {
  min-height: 300px;
  padding: 38px;
  position: relative;
  display: flex;
  align-items: center;
  overflow: hidden;
  border-bottom: 1px solid #25293a;
  background:
    radial-gradient(ellipse at 80% 45%, #54213e 0%, transparent 40%),
    linear-gradient(115deg, #111421, #080a12 70%);
}

.hero::after {
  content: "J";
  position: absolute;
  right: 8%;
  top: -80px;
  font-size: 400px;
  line-height: 1;
  font-weight: 900;
  font-style: italic;
  color: rgba(255, 36, 79, .10);
  pointer-events: none;
}

.hero-content {
  position: relative;
  z-index: 1;
  max-width: 540px;
}

.eyebrow {
  color: var(--red);
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 3px;
  margin-bottom: 14px;
}

h1 {
  font-size: clamp(34px, 5vw, 55px);
  line-height: 1.08;
  margin-bottom: 17px;
}

.hero p {
  color: #d0ceda;
  line-height: 1.7;
  max-width: 440px;
}

.primary {
  background: var(--red);
  color: white;
  border: 0;
  border-radius: 9px;
  padding: 14px 22px;
  margin-top: 23px;
  font-weight: bold;
}

.primary:hover {
  background: #d91640;
  transform: translateY(-2px);
}

.secondary {
  background: transparent;
  color: white;
  border: 1px solid var(--border);
  border-radius: 9px;
  padding: 12px 18px;
  margin-top: 15px;
}

.secondary:hover {
  border-color: var(--red);
}

/* CONTEÚDO */

.content {
  padding: 30px;
  min-width: 0;
}

.screen {
  display: none;
}

.screen.visible {
  display: block;
}

.section-head {
  margin-bottom: 24px;
}

.section-head h2 {
  font-size: 27px;
  margin-top: 8px;
}

.section-head p {
  color: var(--muted);
  margin-top: 9px;
  line-height: 1.6;
}

/* CARTÕES DOS ÁLBUNS */

.phases {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 15px;
}

.phase {
  background: #0c101a;
  border: 1px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
  min-width: 0;
  transition: transform .2s, border-color .2s;
}

.phase:not(.locked):hover {
  transform: translateY(-4px);
  border-color: var(--red);
}

.cover {
  height: 170px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.cover::before {
  content: "";
  position: absolute;
  width: 145px;
  height: 145px;
  border: 1px solid rgba(255,255,255,.2);
  border-radius: 50%;
}

.cover::after {
  content: "";
  position: absolute;
  width: 100px;
  height: 100px;
  border: 1px solid rgba(255,255,255,.12);
  border-radius: 50%;
}

.cover span {
  position: relative;
  z-index: 1;
  font-size: clamp(21px, 2.4vw, 34px);
  font-weight: 900;
  font-style: italic;
  text-shadow: 0 3px 18px #000;
  transform: rotate(-8deg);
}

.lobos {
  background:
    radial-gradient(ellipse at 50% 70%, #a8a3a3, transparent 42%),
    linear-gradient(140deg, #777783, #222430 60%, #090b12);
}

.anti {
  background:
    radial-gradient(ellipse at 40% 50%, #086eb1, transparent 45%),
    linear-gradient(145deg, #061b40, #07101d);
}

.pirata {
  background:
    radial-gradient(ellipse at 60% 55%, #48a5c0, transparent 40%),
    linear-gradient(160deg, #0d526e, #071724);
}

.super {
  background:
    radial-gradient(ellipse at 50% 40%, #f33150, transparent 50%),
    linear-gradient(135deg, #8f0e28, #220714);
}

.phase-body {
  padding: 15px;
}

.phase h3 {
  font-size: 18px;
  margin-bottom: 10px;
}

.phase p {
  color: #c2c2d1;
  font-size: 13px;
  line-height: 1.6;
  min-height: 105px;
}

.phase button {
  width: 100%;
  padding: 11px 5px;
  border: 0;
  border-radius: 7px;
  background: var(--red);
  color: white;
  margin-top: 12px;
  font-size: 12px;
  font-weight: bold;
}

.phase button:hover:not(:disabled) {
  background: #d91640;
}

.phase button:disabled {
  background: #202638;
  color: #929ab0;
  cursor: not-allowed;
}

.phase-progress {
  font-size: 11px;
  color: #9eabc5;
  text-align: center;
  margin-top: 12px;
}

/* TELAS DO JOGO */

.back {
  background: transparent;
  border: 1px solid #41465c;
  color: white;
  padding: 10px 14px;
  border-radius: 8px;
  margin-bottom: 24px;
}

.back:hover {
  border-color: var(--red);
}

.quest-card {
  max-width: 740px;
  margin: 0 auto;
  padding: 28px;
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 14px;
}

.quest-meta {
  display: flex;
  justify-content: space-between;
  gap: 12px;
  color: #ff8aa5;
  font-size: 13px;
  margin-bottom: 18px;
}

.quest-card h2 {
  font-size: 25px;
  line-height: 1.4;
  margin: 23px 0;
}

.options {
  display: grid;
  gap: 12px;
}

.option {
  text-align: left;
  padding: 15px;
  color: white;
  background: #191e2d;
  border: 1px solid #343b52;
  border-radius: 9px;
}

.option:hover:not(:disabled) {
  border-color: var(--blue);
  background: #1b2940;
}

.option.correct {
  background: #124c39;
  border-color: #42d8a0;
}

.option.wrong {
  background: #642033;
  border-color: #ff6a8a;
}

.feedback {
  margin-top: 18px;
  color: #ddd9e6;
  line-height: 1.7;
  min-height: 24px;
}

.hidden {
  display: none !important;
}

.result {
  text-align: center;
  padding: 38px 20px;
}

.result h2 {
  font-size: 32px;
  margin: 16px 0;
}

.result p {
  color: #c2c2d1;
  line-height: 1.8;
}

.list-card {
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 20px;
  margin-top: 20px;
  line-height: 1.8;
}

.list-item {
  padding: 13px 0;
  border-bottom: 1px solid #292e40;
}

.list-item:last-child {
  border-bottom: 0;
}

.done {
  color: #54dfaa;
}

.pending {
  color: #929ab0;
}

.footer {
  text-align: center;
  padding: 0 15px 20px;
  font-size: 11px;
  color: #77798c;
}

/* RESPONSIVIDADE */

@media (max-width: 1050px) {
  .phases {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 650px) {
  .layout {
    grid-template-columns: 1fr;
  }

  .sidebar {
    padding: 15px;
    gap: 13px;
  }

  .logo {
    font-size: 29px;
  }

  .logo small {
    display: inline;
    margin-left: 8px;
  }

  .nav {
    display: flex;
    overflow-x: auto;
    gap: 5px;
  }

  .nav button {
    white-space: nowrap;
    padding: 11px 10px;
    font-size: 12px;
  }

  .profile {
    display: none;
  }

  .hero {
    min-height: 265px;
    padding: 25px 20px;
  }

  .hero::after {
    right: -8%;
    top: -20px;
    font-size: 270px;
  }

  .content {
    padding: 23px 14px;
  }

  .phases {
    gap: 10px;
  }

  .cover {
    height: 125px;
  }

  .phase-body {
    padding: 11px;
  }

  .phase h3 {
    font-size: 15px;
  }

  .phase p {
    font-size: 12px;
    min-height: 130px;
  }

  .phase button {
    font-size: 11px;
  }

  .section-head h2 {
    font-size: 23px;
  }

  .quest-card {
    padding: 19px 14px;
  }

  .quest-card h2 {
    font-size: 21px;
  }
}

@media (max-width: 360px) {
  .phases {
    grid-template-columns: 1fr;
  }

  .cover {
    height: 180px;
  }

  .phase p {
    min-height: 0;
  }
}
</style>
</head>

<body>

<div class="layout">

  <aside class="sidebar">

    <div class="logo">
      JÃO
      <small>JOGO DE AVENTURA</small>
    </div>

    <nav class="nav">
      <button class="active" data-nav="home" onclick="navigate('home', this)">
        ⌂ Início
      </button>

      <button data-nav="home" onclick="navigate('home', this)">
        ▧ Fases
      </button>

      <button data-nav="missions" onclick="navigate('missions', this)">
        ☆ Missões
      </button>

      <button data-nav="achievements" onclick="navigate('achievements', this)">
        ♜ Conquistas
      </button>
    </nav>

    <div class="profile">
      <div class="profile-row">
        <div class="avatar">♪</div>
        <div>
          <strong>Fã em construção</strong><br>
          <small id="level">Nível 1</small>
        </div>
      </div>

      <div class="xp-bar">
        <div class="xp-fill" id="xpFill"></div>
      </div>

      <small id="xpText">0 / 100 XP</small>
    </div>

  </aside>

  <main>

    <header class="hero">
      <div class="hero-content">
        <div class="eyebrow">SUA AVENTURA COMEÇA AQUI</div>

        <h1>O universo do<br>Jão te espera.</h1>

        <p>
          Explore as fases, complete missões e descubra
          o quanto você conhece a trajetória do cantor.
          Somente os verdadeiros fãs chegarão ao final!
        </p>

        <button class="primary" onclick="startPhase(0)">
          COMEÇAR A JORNADA →
        </button>
      </div>
    </header>

    <div class="content">

      <!-- MAPA DE FASES -->

      <section id="home" class="screen visible">

        <div class="section-head">
          <div class="eyebrow">MAPA DE FASES</div>
          <h2>Escolha sua jornada</h2>
          <p>Cada álbum abre um novo capítulo da aventura.</p>
        </div>

        <div class="phases" id="phases"></div>

      </section>

      <!-- MISSÕES -->

      <section id="missions" class="screen">

        <div class="eyebrow">SEU PROGRESSO</div>
        <h2>Missões</h2>

        <p class="muted" style="margin-top:12px; line-height:1.7">
          Complete desafios, acumule XP e mostre que conhece o universo do Jão.
        </p>

        <div class="list-card" id="missionList"></div>

        <button class="primary" onclick="navigate('home')">
          CONTINUAR AVENTURA →
        </button>

      </section>

      <!-- CONQUISTAS -->

      <section id="achievements" class="screen">

        <div class="eyebrow">SUAS CONQUISTAS</div>
        <h2>Galeria de conquistas</h2>

        <p class="muted" style="margin-top:12px; line-height:1.7">
          Cada conquista registra um passo da sua jornada.
        </p>

        <div class="list-card" id="achievementList"></div>

      </section>

      <!-- PERGUNTAS -->

      <section id="playing" class="screen">

        <button class="back" onclick="navigate('home')">
          ← Voltar ao mapa
        </button>

        <div class="quest-card">

          <div class="quest-meta">
            <span id="phaseName">FASE LOBOS</span>
            <span id="questionCount">Missão 1/5</span>
          </div>

          <div class="xp-bar">
            <div class="xp-fill" id="questionProgress"></div>
          </div>

          <h2 id="question">Pergunta do desafio</h2>

          <div class="options" id="options"></div>

          <p class="feedback" id="feedback" aria-live="polite"></p>

          <button
            class="primary hidden"
            id="nextButton"
            onclick="nextQuestion()">
            PRÓXIMO DESAFIO →
          </button>

        </div>

      </section>

      <!-- RESULTADO -->

      <section id="result" class="screen">

        <div class="quest-card result">

          <div class="eyebrow">RESULTADO DA MISSÃO</div>

          <h2 id="resultTitle">Você conseguiu!</h2>

          <p id="resultText"></p>

          <button class="primary" onclick="navigate('home')">
            VOLTAR AO MAPA →
          </button>

          <br>

          <button
            class="secondary"
            id="retryButton"
            onclick="startPhase(0)">
            JOGAR NOVAMENTE
          </button>

        </div>

      </section>

    </div>

    <div class="footer">
      Projeto de fã, sem vínculo oficial com Jão.
    </div>

  </main>

</div>

<script>
/* ===========================
   DADOS DAS FASES E PERGUNTAS
=========================== */

const phases = [
  {
    name: "LOBOS",
    theme: "lobos",
    description:
      "O começo de tudo. Descubra os primeiros passos da trajetória do Jão.",

    questions: [
      {
        q: "Qual é o nome verdadeiro do Jão?",
        a: [
          "João Vitor Romania Balbino",
          "João Pedro Silva",
          "João Lucas Martins",
          "João Victor Santos"
        ],
        correct: 0,
        info: "O nome completo do cantor é João Vitor Romania Balbino."
      },
      {
        q: "Qual foi o álbum de estreia do Jão?",
        a: ["Pirata", "Lobos", "Anti-Herói", "SUPER"],
        correct: 1,
        info: "Lobos foi lançado em 2018."
      },
      {
        q: "Em que ano o álbum Lobos foi lançado?",
        a: ["2016", "2017", "2018", "2019"],
        correct: 2,
        info: "Lobos chegou ao público em 2018."
      },
      {
        q: "Qual destes também é um álbum do Jão?",
        a: [
          "Melodrama",
          "Pirata",
          "Doce 22",
          "Escândalo Íntimo"
        ],
        correct: 1,
        info: "Pirata é o terceiro álbum de estúdio do cantor."
      },
      {
        q: "Qual álbum do Jão foi lançado em 2023?",
        a: ["SUPER", "Lobos", "Pirata", "Anti-Herói"],
        correct: 0,
        info: "SUPER foi lançado em 2023."
      }
    ]
  },

  {
    name: "ANTI-HERÓI",
    theme: "anti",
    description:
      "Encare desafios sobre sentimentos, álbuns e curiosidades da carreira.",

    questions: [
      {
        q: "Em que ano foi lançado Anti-Herói?",
        a: ["2018", "2019", "2021", "2023"],
        correct: 1,
        info: "Anti-Herói foi lançado em 2019."
      },
      {
        q: "Qual álbum veio antes de Anti-Herói?",
        a: ["SUPER", "Pirata", "Lobos", "Nenhum"],
        correct: 2,
        info: "Lobos foi o álbum de estreia do Jão."
      },
      {
        q: "Qual é o nome artístico do cantor?",
        a: ["Jota", "Jão", "JV", "João V."],
        correct: 1,
        info: "O cantor é conhecido artisticamente como Jão."
      },
      {
        q: "Qual destes álbuns foi lançado em 2021?",
        a: ["Lobos", "Anti-Herói", "Pirata", "SUPER"],
        correct: 2,
        info: "Pirata foi lançado em 2021."
      },
      {
        q: "Qual álbum veio depois de Pirata?",
        a: ["Lobos", "SUPER", "Anti-Herói", "Nenhum"],
        correct: 1,
        info: "SUPER foi lançado em 2023."
      }
    ]
  },

  {
    name: "PIRATA",
    theme: "pirata",
    description:
      "Navegue por desafios e curiosidades do universo musical do Jão.",

    questions: [
      {
        q: "Em que ano Pirata foi lançado?",
        a: ["2019", "2020", "2021", "2023"],
        correct: 2,
        info: "Pirata foi lançado em 2021."
      },
      {
        q: "Qual álbum antecedeu Pirata?",
        a: ["Lobos", "Anti-Herói", "SUPER", "Nenhum"],
        correct: 1,
        info: "Anti-Herói chegou em 2019."
      },
      {
        q: "Qual é o nome do álbum lançado em 2018?",
        a: ["Pirata", "Lobos", "SUPER", "Anti-Herói"],
        correct: 1,
        info: "O álbum de estreia é Lobos."
      },
      {
        q: "Qual álbum foi lançado em 2023?",
        a: ["Pirata", "Lobos", "SUPER", "Anti-Herói"],
        correct: 2,
        info: "SUPER chegou em 2023."
      },
      {
        q: "Qual é o nome verdadeiro do Jão?",
        a: [
          "João Vitor Romania Balbino",
          "João Pedro Lima",
          "João Lucas Costa",
          "João Victor Souza"
        ],
        correct: 0,
        info: "O nome completo do cantor é João Vitor Romania Balbino."
      }
    ]
  },

  {
    name: "SUPER",
    theme: "super",
    description:
      "Chegue à última fase e prove o que sabe sobre a discografia do cantor.",

    questions: [
      {
        q: "Em que ano SUPER foi lançado?",
        a: ["2020", "2021", "2022", "2023"],
        correct: 3,
        info: "SUPER foi lançado em 2023."
      },
      {
        q: "Qual álbum veio primeiro?",
        a: ["SUPER", "Pirata", "Lobos", "Anti-Herói"],
        correct: 2,
        info: "Lobos abriu a discografia de álbuns de estúdio do cantor."
      },
      {
        q: "Qual álbum foi lançado em 2019?",
        a: ["Lobos", "Pirata", "Anti-Herói", "SUPER"],
        correct: 2,
        info: "Anti-Herói foi lançado em 2019."
      },
      {
        q: "Qual é o nome verdadeiro do Jão?",
        a: [
          "João Vitor Romania Balbino",
          "João Pedro Silva",
          "João Lucas Martins",
          "João Victor Santos"
        ],
        correct: 0,
        info: "O nome completo do cantor é João Vitor Romania Balbino."
      },
      {
        q: "Qual álbum foi lançado em 2021?",
        a: ["Lobos", "Anti-Herói", "Pirata", "SUPER"],
        correct: 2,
        info: "Pirata foi lançado em 2021."
      }
    ]
  }
];


/* ===========================
   ESTADO DO JOGO
=========================== */

let unlocked = 1;
let phaseIndex = 0;
let questionIndex = 0;
let phaseScore = 0;
let totalXP = 0;
let totalCorrect = 0;

let completed = [];
let perfect = [];
let answered = false;


/* ===========================
   NAVEGAÇÃO
=========================== */

function navigate(id, button) {
  document.querySelectorAll(".screen").forEach(screen => {
    screen.classList.remove("visible");
  });

  document.getElementById(id).classList.add("visible");

  document.querySelectorAll(".nav button").forEach(btn => {
    btn.classList.remove("active");
  });

  if (button) {
    button.classList.add("active");
  } else {
    const matchingButton = document.querySelector(
      `.nav button[data-nav="${id}"]`
    );

    if (matchingButton) {
      matchingButton.classList.add("active");
    }
  }

  if (id === "home") renderPhases();
  if (id === "missions") renderMissions();
  if (id === "achievements") renderAchievements();
}


/* ===========================
   MOSTRAR AS FASES
=========================== */

function renderPhases() {
  const container = document.getElementById("phases");

  container.innerHTML = "";

  phases.forEach((phase, index) => {
    const locked = index >= unlocked;
    const done = completed.includes(index);

    const card = document.createElement("article");

    card.className = "phase" + (locked ? " locked" : "");

    const cover = document.createElement("div");
    cover.className = "cover " + phase.theme;

    const title = document.createElement("span");
    title.textContent = phase.name;

    cover.appendChild(title);

    const body = document.createElement("div");
    body.className = "phase-body";

    const heading = document.createElement("h3");
    heading.textContent = phase.name;

    const description = document.createElement("p");
    description.textContent = phase.description;

    const button = document.createElement("button");
    button.disabled = locked;

    button.textContent = locked
      ? "🔒 BLOQUEADO"
      : done
        ? "JOGAR NOVAMENTE ↻"
        : "JOGAR →";

    button.addEventListener("click", () => startPhase(index));

    const progress = document.createElement("div");
    progress.className = "phase-progress";

    progress.textContent = done
      ? "✓ FASE CONCLUÍDA"
      : locked
        ? "Complete a fase anterior"
        : "5 missões disponíveis";

    body.append(heading, description, button, progress);
    card.append(cover, body);

    container.appendChild(card);
  });
}


/* ===========================
   INICIAR UMA FASE
=========================== */

function startPhase(index) {
  if (index < 0 || index >= unlocked) return;

  phaseIndex = index;
  questionIndex = 0;
  phaseScore = 0;

  navigate("playing");
  showQuestion();
}


/* ===========================
   MOSTRAR PERGUNTA
=========================== */

function showQuestion() {
  answered = false;

  const phase = phases[phaseIndex];
  const q = phase.questions[questionIndex];

  document.getElementById("phaseName").textContent =
    "FASE " + phase.name;

  document.getElementById("questionCount").textContent =
    `Missão ${questionIndex + 1}/${phase.questions.length}`;

  document.getElementById("questionProgress").style.width =
    `${(questionIndex / phase.questions.length) * 100}%`;

  document.getElementById("question").textContent = q.q;
  document.getElementById("feedback").textContent = "";

  document.getElementById("nextButton").classList.add("hidden");

  const options = document.getElementById("options");

  options.innerHTML = "";

  q.a.forEach((answer, index) => {
    const button = document.createElement("button");

    button.className = "option";
    button.textContent = answer;

    button.addEventListener("click", () => {
      checkAnswer(index, button);
    });

    options.appendChild(button);
  });
}


/* ===========================
   VERIFICAR RESPOSTA
=========================== */

function checkAnswer(index, selected) {
  if (answered) return;

  answered = true;

  const q = phases[phaseIndex].questions[questionIndex];

  const options = document.querySelectorAll(".option");

  options.forEach((button, i) => {
    button.disabled = true;

    if (i === q.correct) {
      button.classList.add("correct");
    }
  });

  if (index === q.correct) {
    phaseScore++;
    totalCorrect++;
    totalXP += 20;

    document.getElementById("feedback").textContent =
      "Resposta certa! +20 XP. " + q.info;

  } else {
    selected.classList.add("wrong");

    document.getElementById("feedback").textContent =
      "Não foi dessa vez! " + q.info;
  }

  updateProfile();

  const next = document.getElementById("nextButton");

  next.textContent =
    questionIndex === phases[phaseIndex].questions.length - 1
      ? "FINALIZAR FASE →"
      : "PRÓXIMA MISSÃO →";

  next.classList.remove("hidden");
}


/* ===========================
   PRÓXIMA PERGUNTA
=========================== */

function nextQuestion() {
  questionIndex++;

  if (questionIndex < phases[phaseIndex].questions.length) {
    showQuestion();
  } else {
    finishPhase();
  }
}


/* ===========================
   FINALIZAR FASE
=========================== */

function finishPhase() {
  const index = phaseIndex;
  const total = phases[index].questions.length;

  const passed = phaseScore >= 3;

  let bonusXP = 0;

  if (passed && !completed.includes(index)) {
    completed.push(index);
    bonusXP += 30;
  }

  if (phaseScore === total && !perfect.includes(index)) {
    perfect.push(index);
    bonusXP += 20;
  }

  totalXP += bonusXP;

  if (passed && index + 1 === unlocked && unlocked < phases.length) {
    unlocked++;
  }

  updateProfile();

  document.getElementById("questionProgress").style.width = "100%";

  document.getElementById("resultTitle").textContent =
    passed ? "Fase concluída!" : "Continue tentando!";

  let message =
    `Você acertou ${phaseScore} de ${total} perguntas. `;

  if (passed) {
    message +=
      "Você completou a fase e avançou na sua jornada! ";

    if (bonusXP >= 30 && !perfect.includes(index)) {
      message += "Bônus de conclusão contabilizado. ";
    }
  } else {
    message +=
      "Você precisa acertar pelo menos 3 perguntas para concluir esta fase. ";
  }

  if (phaseScore === total) {
    message += "Você acertou tudo e conquistou o bônus de perfeição!";
  }

  document.getElementById("resultText").textContent = message;

  const retry = document.getElementById("retryButton");

  retry.onclick = () => startPhase(index);

  navigate("result");
}


/* ===========================
   ATUALIZAR XP E NÍVEL
=========================== */

function updateProfile() {
  const level = Math.floor(totalXP / 100) + 1;
  const currentXP = totalXP % 100;

  document.getElementById("level").textContent =
    "Nível " + level;

  document.getElementById("xpText").textContent =
    `${currentXP} / 100 XP`;

  document.getElementById("xpFill").style.width =
    currentXP + "%";
}


/* ===========================
   LISTA DE MISSÕES
=========================== */

function renderMissions() {
  const items = [
    {
      name: "Primeiro passo",
      description: "Conclua sua primeira fase.",
      done: completed.length >= 1
    },
    {
      name: "Fã dedicado",
      description: "Conclua duas fases.",
      done: completed.length >= 2
    },
    {
      name: "Jornada completa",
      description: "Desbloqueie e conclua todas as fases.",
      done: completed.length === phases.length
    },
    {
      name: "Conhecedor",
      description: "Acerte 10 perguntas.",
      done: totalCorrect >= 10
    },
    {
      name: "Perfeccionista",
      description: "Acerte todas as perguntas de uma fase.",
      done: perfect.length >= 1
    }
  ];

  const container = document.getElementById("missionList");

  container.innerHTML = "";

  items.forEach(item => {
    const row = document.createElement("div");

    row.className = "list-item";

    const title = document.createElement("strong");
    title.className = item.done ? "done" : "pending";

    title.textContent =
      (item.done ? "✓ " : "○ ") + item.name;

    const description = document.createElement("p");
    description.className = "muted";
    description.style.marginTop = "5px";
    description.textContent = item.description;

    const status = document.createElement("span");
    status.className = item.done ? "done" : "pending";
    status.textContent = item.done ? "Concluída" : "Pendente";

    row.append(title, description, status);

    container.appendChild(row);
  });
}


/* ===========================
   GALERIA DE CONQUISTAS
=========================== */

function renderAchievements() {
  const items = [
    {
      name: "Primeiro passo",
      description: "Conclua sua primeira fase.",
      done: completed.length >= 1
    },
    {
      name: "Fã dedicado",
      description: "Conclua duas fases.",
      done: completed.length >= 2
    },
    {
      name: "Jornada completa",
      description: "Conclua todas as quatro fases.",
      done: completed.length === phases.length
    },
    {
      name: "Conhecedor",
      description: "Acerte pelo menos 10 perguntas.",
      done: totalCorrect >= 10
    },
    {
      name: "Perfeccionista",
      description: "Acerte todas as perguntas de uma fase.",
      done: perfect.length >= 1
    }
  ];

  const container = document.getElementById("achievementList");

  container.innerHTML = "";

  items.forEach(item => {
    const row = document.createElement("div");

    row.className = "list-item";

    const title = document.createElement("strong");
    title.className = item.done ? "done" : "pending";

    title.textContent =
      (item.done ? "🏆 " : "🔒 ") + item.name;

    const description = document.createElement("p");
    description.className = "muted";
    description.style.marginTop = "5px";
    description.textContent = item.description;

    const status = document.createElement("span");
    status.className = item.done ? "done" : "pending";
    status.textContent = item.done
      ? "Desbloqueada"
      : "Ainda bloqueada";

    row.append(title, description, status);

    container.appendChild(row);
  });
}


/* ===========================
   INICIALIZAR JOGO
=========================== */

renderPhases();
updateProfile();
renderMissions();
renderAchievements();

</script>

</body>
</html>