<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Защита аккаунта</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; }
        .container { max-width: 400px; margin: auto; padding: 20px; border: 1px solid #ccc; border-radius: 10px; }
        input { width: 100%; padding: 8px; margin: 10px 0; }
        button { padding: 10px 20px; cursor: pointer; }
        .error { color: red; }
    </style>
</head>
<body>

<div class="container">
    <h2>Введите ответы на вопросы</h2>
    <p id="question1"></p>
    <input type="text" id="answer1">
    
    <p id="question2"></p>
    <input type="text" id="answer2">
    
    <p id="question3"></p>
    <input type="text" id="answer3">

    <button onclick="checkAnswers()">Подтвердить</button>
    <p class="error" id="errorMsg"></p>
</div>

<script>
    // База вопросов и функций преобразования
    const questions = [
        { q: "Ваш первый год учебы?", transform: x => x * 3, correct: "2005" },
        { q: "Номер вашей первой машины?", transform: x => x * 5 + 100, correct: "1234" },
        { q: "Последние 4 цифры первого телефона?", transform: x => x * 2 - 50, correct: "5678" }
    ];

    // Выбираем случайные 3 вопроса
    const selectedQuestions = questions.sort(() => 0.5 - Math.random()).slice(0, 3);

    // Отображаем вопросы на странице
    document.getElementById("question1").innerText = selectedQuestions[0].q;
    document.getElementById("question2").innerText = selectedQuestions[1].q;
    document.getElementById("question3").innerText = selectedQuestions[2].q;

    let attempts = 3; // Количество попыток

    function checkAnswers() {
        let userAnswers = [
            document.getElementById("answer1").value,
            document.getElementById("answer2").value,
            document.getElementById("answer3").value
        ];

        // Проверяем ответы
        let correct = true;
        for (let i = 0; i < 3; i++) {
            let transformed = selectedQuestions[i].transform(parseInt(selectedQuestions[i].correct));
            if (parseInt(userAnswers[i]) !== transformed) {
                correct = false;
                break;
            }
        }

        if (correct) {
            window.location.href = "https://www.instagram.com"; // Переход на Instagram
        } else {
            attempts--;
            if (attempts > 0) {
                document.getElementById("errorMsg").innerText = `❌ Неверный ответ! Осталось попыток: ${attempts}`;
            } else {
                document.getElementById("errorMsg").innerText = "⛔ Доступ заблокирован!";
                document.querySelector("button").disabled = true;
            }
        }
    }
</script>

</body>
</html>
