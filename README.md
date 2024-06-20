- 👋 Hi, I’m @Garo2011
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Garo2011/Garo2011 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
// Пример массива вопросов с дубликатами
let questions = [
    { question: "Какого цвета небо?", answer: "Синий", difficulty: 1 },
    { question: "Сколько пальцев на руке?", answer: "Пять", difficulty: 2 },
    { question: "Какого цвета небо?", answer: "Синий", difficulty: 1 }, // Дубликат
    { question: "Что такое корень квадратный из 144?", answer: "12", difficulty: 3 },
    { question: "Как называется столица Японии?", answer: "Токио", difficulty: 4 },
    { question: "Как называется столица Японии?", answer: "Токио", difficulty: 4 }, // Дубликат
];

// Функция для удаления дубликатов из массива объектов
function removeDuplicates(array) {
    let uniqueQuestions = new Map();

    array.forEach(item => {
        // Используем JSON.stringify для создания уникального ключа
        let key = JSON.stringify(item);
        uniqueQuestions.set(key, item);
    });

    // Преобразуем Map обратно в массив объектов
    return Array.from(uniqueQuestions.values());
}

// Удаление дубликатов из массива вопросов
let uniqueQuestions = removeDuplicates(questions);

// Переменные для игры
let currentQuestionIndex = 0;
let totalCredits = 0;
const creditsPerQuestion = 25;

// Функция для начала игры
function startGame() {
    document.getElementById('start-game').classList.add('hide');
    document.getElementById('question-container').classList.remove('hide');
    displayQuestion();
}

// Функция для отображения текущего вопроса
function displayQuestion() {
    const question = uniqueQuestions[currentQuestionIndex];
    document.getElementById('question').innerText = question.question;
}

// Функция для проверки ответа
function checkAnswer() {
    const playerAnswer = document.getElementById('answer').value;
    const correctAnswer = uniqueQuestions[currentQuestionIndex].answer;

    if (playerAnswer.toLowerCase() === correctAnswer.toLowerCase()) {
        totalCredits += creditsPerQuestion;
        alert('Правильный ответ!');
    } else {
        alert(`Неверный ответ. Правильный ответ: ${correctAnswer}`);
    }

    currentQuestionIndex++;
    document.getElementById('answer').value = '';

    if (currentQuestionIndex < uniqueQuestions.length) {
        displayQuestion();
    } else {
        endGame();
    }
}

// Функция для завершения игры и вывода результатов
function endGame() {
    document.getElementById('question-container').classList.add('hide');
    document.getElementById('result-container').classList.remove('hide');
    document.getElementById('result').innerText = `Ваш результат: ${totalCredits} кредитов.`;
}

// Добавление обработчиков событий
document.getElementById('start-game').addEventListener('click', startGame);
document.getElementById('submit-answer').addEventListener('click', checkAnswer);
