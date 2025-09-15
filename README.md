<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title>Student Portfolio</title>

  <!-- Stylesheet -->
  <link rel="stylesheet" href="style.css">

  <!-- Custom Styles (for quiz and blog) -->
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f9f9f9;
      color: #333;
    }

    /* Quiz Section */
    .quiz-container {
      max-width: 500px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    .quiz-container .question {
      font-size: 20px;
      margin-bottom: 15px;
    }

    .quiz-container .options button {
      display: block;
      width: 100%;
      margin-bottom: 10px;
      padding: 10px;
      font-size: 16px;
      cursor: pointer;
    }

    .quiz-container .result {
      font-weight: bold;
      margin-top: 15px;
    }

    .quiz-container .next-btn {
      margin-top: 20px;
      padding: 10px 15px;
      font-size: 16px;
    }

    /* Blog Section */
    .blog-container {
      max-width: 800px;
      margin: 20px auto;
      padding: 10px;
    }

    .post {
      background: white;
      padding: 15px;
      margin-bottom: 20px;
      border-radius: 8px;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
    }

    .post h2 {
      margin: 0 0 10px;
    }

    .post small {
      color: gray;
      font-size: 12px;
    }
  </style>

  <!-- Scripts -->
  <script defer src="script.js"></script>

  <!-- EmailJS SDK -->
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script>
    (function(){
      emailjs.init("YOUR_PUBLIC_KEY"); // Replace with your EmailJS Public Key
    })();
  </script>
</head>

<body>
  <!-- Navbar -->
  <header>
    <nav class="navbar">
      <div class="logo">MyPortfolio</div>
      <ul class="nav-links" id="nav-links">
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#quiz">Quiz</a></li>
        <li><a href="#blog">Blog</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
      <div class="menu-toggle" id="menu-toggle">&#9776;</div>
    </nav>
  </header>

  <!-- Hero Section -->
  <section id="home" class="hero">
    <div class="hero-content">
      <h1>Hello, I'm <span>MONESH S</span></h1>
      <p>I am the student</p>
      <a href="#projects" class="btn">View My Work</a>
    </div>
  </section>

  <!-- About Section -->
  <section id="about" class="about">
    <h2>About Me</h2>
    <div class="about-content">
      <img src="IMG_20250814_WA0046.jpg" alt="Profile Photo">
      <p>
        I am a student enthusiastic about technology and design. I love building interactive,
        user-friendly web applications and exploring new tools in the tech world.
      </p>
    </div>
  </section>

  <!-- Projects Section -->
  <section id="projects" class="projects">
    <h2>My Projects</h2>
    <div class="project-grid">
      <div class="project-card">
        <h3>Project 1</h3>
        <p>A simple responsive website.</p>
      </div>
      <div class="project-card">
        <h3>Project 2</h3>
        <p>JavaScript-based quiz app.</p>
      </div>
      <div class="project-card">
        <h3>Project 3</h3>
        <p>Personal blog with CMS.</p>
      </div>
    </div>
  </section>

  <!-- Quiz Section -->
  <section id="quiz" class="quiz-section">
    <h2>Random Quiz</h2>
    <div class="quiz-container">
      <div class="question" id="question">Loading question...</div>
      <div class="options" id="options"></div>
      <div class="result" id="result"></div>
      <button class="next-btn" onclick="loadRandomQuestion()">Next Question</button>
    </div>
  </section>

  <!-- Blog Section -->
  <section id="blog" class="blog-section">
    <h2>My Blog</h2>
    <div class="blog-container" id="postsContainer"></div>
  </section>

  <!-- Contact Section -->
  <section id="contact" class="contact">
    <h2>Contact Me</h2>
    <form id="contact-form">
      <input type="text" id="name" name="user_name" placeholder="Your Name" required>
      <input type="email" id="email" name="user_email" placeholder="Your Email" required>
      <textarea id="message" name="message" placeholder="Your Message" required></textarea>
      <button type="submit">Send</button>
    </form>
    <p id="form-status"></p>
  </section>

  <!-- Footer -->
  <footer>
    <p>&copy; 2025 MONESH S | All rights reserved</p>
  </footer>

  <!-- Scripts for Quiz and Blog -->
  <script>
    // Quiz Logic
    const quizData = [
      { question: "What is the capital of France?", options: ["Paris", "Rome", "Berlin", "Madrid"], answer: "Paris" },
      { question: "Which planet is known as the Red Planet?", options: ["Venus", "Saturn", "Mars", "Jupiter"], answer: "Mars" },
      { question: "What is 5 + 7?", options: ["10", "12", "11", "13"], answer: "12" },
      { question: "Who wrote 'Romeo and Juliet'?", options: ["Shakespeare", "Hemingway", "Dickens", "Austen"], answer: "Shakespeare" },
      { question: "Which element has the chemical symbol 'O'?", options: ["Gold", "Oxygen", "Silver", "Iron"], answer: "Oxygen" }
    ];

    function loadRandomQuestion() {
      const questionContainer = document.getElementById('question');
      const optionsContainer = document.getElementById('options');
      const resultContainer = document.getElementById('result');

      resultContainer.textContent = '';

      const randomIndex = Math.floor(Math.random() * quizData.length);
      const currentQuestion = quizData[randomIndex];

      questionContainer.textContent = currentQuestion.question;
      optionsContainer.innerHTML = '';

      currentQuestion.options.forEach(option => {
        const btn = document.createElement('button');
        btn.textContent = option;
        btn.onclick = () => {
          if (option === currentQuestion.answer) {
            resultContainer.textContent = 'Correct!';
            resultContainer.style.color = 'green';
          } else {
            resultContainer.textContent = `Wrong! The correct answer was: ${currentQuestion.answer}`;
            resultContainer.style.color = 'red';
          }
        };
        optionsContainer.appendChild(btn);
      });
    }

    window.onload = function() {
      loadRandomQuestion();
      loadPosts();
    };

    // Blog Logic
    function loadPosts() {
      const postsContainer = document.getElementById("postsContainer");
      const posts = JSON.parse(localStorage.getItem("blogPosts")) || [];

      postsContainer.innerHTML = "";
      posts.reverse().forEach(post => {
        const postEl = document.createElement("div");
        postEl.classList.add("post");
        postEl.innerHTML = `
          <h2>${post.title}</h2>
          <small>${new Date(post.date).toLocaleString()}</small>
          <p>${post.content}</p>
        `;
        postsContainer.appendChild(postEl);
      });
    }
  </script>
</body>
</html>
