<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>INTERACTIVE QUIZ</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: pink;
      margin: 0;
      padding: 20px;
    }

    .quiz-container {
      max-width: 600px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    h2 {
      text-align: center;
      color: #333;
      font-size: 28px;
    }

    .question {
      margin-bottom: 15px;
    }

    .question p {
      font-weight: bold;
      color: #333;
      font-size: 18px;
    }

    label {
      display: block;
      margin-bottom: 5px;
      color: #555;
      font-size: 16px;
    }

    input[type="radio"] {
      margin-right: 10px;
    }

    button {
      padding: 10px 15px;
      background-color: #28a745;
      color: white;
      border: none;
      cursor: pointer;
      display: block;
      margin: 20px auto 10px;
      font-size: 16px;
    }

    button:hover {
      background-color: #218838;
    }

    .result {
      text-align: center;
      font-weight: bold;
      margin-top: 20px;
      font-size: 18px;
      color: #222;
    }

    /*  Mobile Styles */
    @media (max-width: 600px) {
      body {
        padding: 10px;
      }

      .quiz-container {
        padding: 15px;
      }

      h2 {
        font-size: 22px;
      }

      .question p {
        font-size: 16px;
      }

      label {
        font-size: 14px;
      }

      button {
        width: 100%;
        font-size: 14px;
      }

      .result {
        font-size: 16px;
      }
    }

    /* Tablets */
    @media (min-width: 601px) and (max-width: 1024px) {
      h2 {
        font-size: 24px;
      }

      .question p {
        font-size: 17px;
      }

      label {
        font-size: 15px;
      }

      button {
        font-size: 15px;
      }
    }
  </style>
</head>
<body>

  <div class="quiz-container">
    <h2>JavaScript Quiz</h2>
    <div id="quiz"></div>
    <button onclick="submitQuiz()">Submit Quiz</button>
    <div class="result" id="result"></div>
  </div>

  <script>
    const questions = [
      {
        question: "What does HTML stand for?",
        options: ["Hyper Trainer Marking Language", "Hyper Text Markup Language", "Hyper Text Marketing Language"],
        answer: 1
      },
      {
        question: "Which language is used for styling web pages?",
        options: ["HTML", "JQuery", "CSS"],
        answer: 2
      },
      {
        question: "Which is not a JavaScript framework?",
        options: ["Python Script", "React", "Angular"],
        answer: 0
      }
    ];

    const quizContainer = document.getElementById("quiz");

    questions.forEach((q, i) => {
      const questionDiv = document.createElement("div");
      questionDiv.className = "question";
      questionDiv.innerHTML = `<p>${i + 1}. ${q.question}</p>` + q.options.map((opt, j) =>
        `<label><input type="radio" name="q${i}" value="${j}"> ${opt}</label>`).join("");
      quizContainer.appendChild(questionDiv);
    });

    function submitQuiz() {
      let score = 0;
      questions.forEach((q, i) => {
        const selected = document.querySelector(`input[name="q${i}"]:checked`);
        if (selected && parseInt(selected.value) === q.answer) score++;
      });
      document.getElementById("result").innerText = `You scored ${score} out of ${questions.length}`;
    }
  </script>
  <button onclick="loadUserData()">Load User Info</button>
<div id="userData"></div>
<script>
    function loadUserData() {
  const userDataContainer = document.getElementById("userData");
  userDataContainer.innerHTML = "Loading user data...";

  fetch("https://jsonplaceholder.typicode.com/users")
    .then(response => response.json())
    .then(data => {
      userDataContainer.innerHTML = "<h3>User Information</h3>";
      data.slice(0, 5).forEach(user => {  // show only 5 users for brevity
        const userCard = document.createElement("div");
        userCard.style.border = "1px solid #ccc";
        userCard.style.padding = "10px";
        userCard.style.marginBottom = "10px";
        userCard.style.borderRadius = "5px";
        userCard.innerHTML = `
          <strong>${user.name}</strong><br>
          Email: ${user.email}<br>
          City: ${user.address.city}
        `;
        userDataContainer.appendChild(userCard);
      });
    })
    .catch(error => {
      userDataContainer.innerHTML = "Failed to load data.";
      console.error("Error fetching data:", error);
    });
}

    </script>


</body>
</html>
