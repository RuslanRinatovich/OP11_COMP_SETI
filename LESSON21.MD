# Урок №21. Условия, функции и проверка форм

## Цели урока

- 🔍 Научиться проверять условия с помощью `if / else`
- 📦 Понять, что такое функции и зачем они нужны
- ✅ Освоить базовую проверку форм (пароль, email, пустые поля)
- 🛠️ Сделать интерактивные формы с обратной связью
- ⚠️ Разобраться с тонкостями сравнения в JavaScript (`==` vs `===`)

---

# Часть 1. Теория (90 минут)

## 1. Повторение прошлого урока (10 минут)

Быстро опросить студентов:

| Вопрос | Ответ |
|--------|-------|
| 🔹 Как найти элемент по `id="header"`? | `document.querySelector("#header")` |
| 🔹 Как поменять текст внутри абзаца? | `элемент.textContent = "новый текст"` |
| 🔹 Как привязать действие к клику кнопки? | `кнопка.onclick = function() { ... }` |
| 🔹 Как найти элемент по `name="username"`? | `document.querySelector('[name="username"]')` |
| 🔹 Как изменить цвет фона элемента? | `элемент.style.backgroundColor = "red"` |

---

## 2. Условия if и else (20 минут)

### ❓ Зачем нужны условия?

Программа должна принимать решения в зависимости от ситуации.

**Примеры из реальной жизни:**
- 🚪 Если пользователь ввёл правильный пароль → пустить на сайт, иначе → показать ошибку
- 🎂 Если возраст больше 18 → доступ разрешён, иначе → запрещён
- 💰 Если сумма покупки больше 1000 рублей → дать скидку, иначе → без скидки

### 📐 Операторы сравнения (обязательно запомнить)

| Оператор | Значение | Пример | Результат |
|----------|----------|--------|-----------|
| `>` | больше | `10 > 5` | `true` |
| `<` | меньше | `3 < 8` | `true` |
| `>=` | больше или равно | `5 >= 5` | `true` |
| `<=` | меньше или равно | `4 <= 3` | `false` |

### 📝 Синтаксис if

```javascript
if (условие) {
    // код, который выполнится, если условие истинно
}
```

**Пример 1. Простая проверка:**

```javascript
let age = 20;
if (age >= 18) {
    console.log("Доступ разрешён");
}
// Вывод: Доступ разрешён
```

### 📝 Конструкция if / else

Если условие НЕ выполняется, можно выполнить другой код.

```javascript
let age = 16;
if (age >= 18) {
    console.log("Доступ разрешён");
} else {
    console.log("Доступ запрещён. Вы слишком молоды");
}
// Вывод: Доступ запрещён. Вы слишком молоды
```

### 📝 Конструкция if / else if / else (несколько вариантов)

```javascript
let score = 85;

if (score >= 90) {
    console.log("Отлично");
} else if (score >= 70) {
    console.log("Хорошо");
} else if (score >= 50) {
    console.log("Удовлетворительно");
} else {
    console.log("Неудовлетворительно");
}
// Вывод: Хорошо
```

> 💡 **Как это работает:** Программа проверяет условия по порядку. Как только находит истинное — выполняет его и выходит из всей конструкции.

---

## 3. ⚠️ Важное отступление: строгое и нестрогое сравнение в JavaScript (15 минут)

В JavaScript есть два типа операторов сравнения: **нестрогие** (`==` и `!=`) и **строгие** (`===` и `!==`). Это одна из самых частых причин ошибок у начинающих.

### 📊 Таблица сравнения

| Оператор | Название | Что делает | Пример | Результат |
|----------|----------|------------|--------|-----------|
| `==` | нестрогое равенство | сравнивает значения, ПРИВОДЯ ТИПЫ | `5 == "5"` | `true` |
| `!=` | нестрогое неравенство | проверяет, не равны ли значения (с приведением типов) | `5 != "5"` | `false` |
| `===` | строгое равенство | сравнивает значения БЕЗ приведения типов | `5 === "5"` | `false` |
| `!==` | строгое неравенство | проверяет, не равны ли значения (без приведения типов) | `5 !== "5"` | `true` |

### 🐛 Главная тонкость JavaScript: приведение типов

Когда вы используете `==` или `!=`, JavaScript пытается **преобразовать** значения к одному типу, чтобы их можно было сравнить. Это может давать **неожиданные результаты**.

### 😱 Шокирующие примеры (но это работает именно так)

```javascript
// Число и строка
console.log(5 == "5");        // true (строка "5" превратилась в число 5)
console.log(5 === "5");       // false (разные типы: number vs string)

// Пустые значения
console.log("" == false);     // true (пустая строка → 0, false → 0)
console.log("" === false);    // false (string vs boolean)

// null и undefined
console.log(null == undefined);   // true (особый случай)
console.log(null === undefined);  // false (разные типы)

// 0 и false
console.log(0 == false);      // true (0 → false, false → 0)
console.log(0 === false);     // false (number vs boolean)

// Пустая строка и 0
console.log("" == 0);         // true (пустая строка → 0)
console.log("" === 0);        // false

// Массивы (здесь вообще магия)
console.log([] == false);     // true (пустой массив → пустая строка → 0 → false)
console.log([] == 0);         // true
console.log([1] == 1);        // true (массив превращается в строку "1", потом в число 1)
console.log([1,2] == "1,2");  // true (массив превращается в строку "1,2")
```

### 🎯 Правило, которое нужно запомнить

**Всегда используйте `===` и `!==`** (строгие операторы), если вы точно не понимаете, зачем вам нужны нестрогие.

```javascript
// ❌ ПЛОХО (может привести к багам)
if (inputValue == 5) { ... }

// ✅ ХОРОШО (понятно и предсказуемо)
if (inputValue === 5) { ... }
```

### 📋 Полная таблица неочевидных сравнений

| Сравнение | `==` | `===` | Почему? |
|-----------|------|-------|---------|
| `0 == false` | `true` | `false` | 0 → false |
| `"0" == false` | `true` | `false` | "0" → 0 → false |
| `0 == "0"` | `true` | `false` | строка → число |
| `null == undefined` | `true` | `false` | особое правило JS |
| `NaN == NaN` | `false` | `false` | NaN никогда не равен NaN |
| `[] == ""` | `true` | `false` | массив → пустая строка |
| `[] == 0` | `true` | `false` | массив → "" → 0 |
| `[1] == 1` | `true` | `false` | массив → "1" → 1 |
| `[1,2] == "1,2"` | `true` | `false` | массив → строка |

### 🔧 Практические примеры из реальной жизни

**Пример 1. Проверка значения из input**

```javascript
// Пользователь ввёл число в поле input
let userInput = document.querySelector("#ageInput").value;
// ВНИМАНИЕ! value ВСЕГДА возвращает строку

// ❌ НЕПРАВИЛЬНО (может сработать неожиданно)
if (userInput == 18) {
    console.log("Вам ровно 18");
}
// Если пользователь ввёл "18" (строка), то "18" == 18 даст true

// ✅ ПРАВИЛЬНО (явно преобразуем тип)
let age = Number(userInput);
if (age === 18) {
    console.log("Вам ровно 18");
}
```

**Пример 2. Проверка на пустоту**

```javascript
let text = "";  // пустая строка

// ❌ НЕПРАВИЛЬНО (сработает, но не очевидно)
if (text == false) {
    console.log("Текст пустой");  // сработает, но почему?
}

// ✅ ПРАВИЛЬНО (явно и понятно)
if (text === "") {
    console.log("Текст пустой");
}

// ✅ ТОЖЕ ПРАВИЛЬНО (проверка на ложные значения)
if (!text) {
    console.log("Текст пустой или falsy-значение");
}
```

**Пример 3. Проверка наличия значения в массиве**

```javascript
let foundIndex = [10, 20, 30].indexOf(20);  // возвращает 1

// ❌ ПЛОХО (если элемент найден под индексом 0)
if (foundIndex == true) {  // true превратится в 1, а индекс 0 даст false
    console.log("Элемент найден");  // НЕ СРАБОТАЕТ при индексе 0!
}

// ✅ ХОРОШО (проверяем явно)
if (foundIndex !== -1) {
    console.log("Элемент найден на позиции " + foundIndex);
}
```

### 🧠 Что такое falsy-значения?

В JavaScript есть значения, которые в логическом контексте становятся `false`. Их нужно знать.

**Falsy-значения (всего 8):**

| Значение | Тип | Пояснение |
|----------|-----|-----------|
| `false` | boolean | само false |
| `0` | number | ноль |
| `-0` | number | минус ноль |
| `0n` | bigint | ноль как BigInt |
| `""` | string | пустая строка |
| `null` | null | ничего |
| `undefined` | undefined | не определено |
| `NaN` | number | не число |

**Все остальные значения в JavaScript считаются truthy (истинными).**

```javascript
// falsy-значения
if (false) { }      // не выполнится
if (0) { }          // не выполнится
if ("") { }         // не выполнится
if (null) { }       // не выполнится
if (undefined) { }  // не выполнится
if (NaN) { }        // не выполнится

// truthy-значения (выполнятся)
if (true) { }
if (1) { }
if (-5) { }
if ("привет") { }
if ([])) { }        // пустой массив — truthy!
if ({}) { }         // пустой объект — truthy!
```

> ⭐ **Важно:** `[]` (пустой массив) и `{}` (пустой объект) являются **truthy**, хотя `== false` даёт `true` из-за приведения типов. Это ещё одна причина использовать `===`!

---

## 4. Логические операторы (10 минут)

Иногда нужно проверить несколько условий одновременно.

### Оператор `&&` (И)

Все условия должны быть истинными.

```javascript
let age = 20;
let hasTicket = true;

if (age >= 18 && hasTicket === true) {
    console.log("Проходите в кинотеатр");
} else {
    console.log("Вход запрещён");
}
// Вывод: Проходите в кинотеатр
```

### Оператор `||` (ИЛИ)

Хотя бы одно условие должно быть истинным.

```javascript
let day = "суббота";

if (day === "суббота" || day === "воскресенье") {
    console.log("Ура, выходной!");
} else {
    console.log("Рабочий день");
}
// Вывод: Ура, выходной!
```

### Оператор `!` (НЕ)

Инвертирует условие (делает истину ложью, а ложь — истиной).

```javascript
let isLoggedIn = false;

if (!isLoggedIn) {
    console.log("Пожалуйста, войдите в систему");
}
// Вывод: Пожалуйста, войдите в систему
// Потому что !false = true
```

### Пример с проверкой пароля (несколько условий)

```javascript
let password = "abc123";

if (password.length >= 6 && password !== "123456") {
    console.log("Пароль подходит");
} else {
    console.log("Пароль слишком короткий или слишком простой");
}
```

---

## 5. Функции (20 минут)

### ❓ Что такое функция?

**Функция** — это "кирпичик" кода, который можно назвать по имени и выполнить в любой момент.

**Простая аналогия:** Функция — это как рецепт приготовления пиццы. Вы записываете рецепт один раз, а потом можете готовить по нему сколько угодно раз.

### ❓ Зачем нужны функции?

- ✅ Чтобы не писать один и тот же код много раз (DRY — Don't Repeat Yourself)
- ✅ Чтобы разбить программу на понятные части
- ✅ Чтобы запускать код по событию (клик, загрузка страницы)
- ✅ Чтобы легче находить и исправлять ошибки

### 📝 Создание (объявление) функции

```javascript
function имяФункции() {
    // код, который будет выполнен при вызове
}
```

### 📞 Вызов функции

```javascript
имяФункции();   // просто пишем имя со скобками
```

### 🔧 Пример 1. Функция без параметров

```javascript
function showHello() {
    console.log("Привет, мир!");
}

showHello();   // Привет, мир!
showHello();   // Привет, мир! (можно вызвать много раз)
```

### 🔧 Пример 2. Функция с параметрами

Параметры — это входные данные для функции.

```javascript
function greetUser(name) {
    console.log("Привет, " + name + "! Добро пожаловать.");
}

greetUser("Анна");   // Привет, Анна! Добро пожаловать.
greetUser("Пётр");   // Привет, Пётр! Добро пожаловать.
```

### 🔧 Пример 3. Функция с несколькими параметрами

```javascript
function addNumbers(a, b) {
    let result = a + b;
    console.log(a + " + " + b + " = " + result);
}

addNumbers(5, 3);   // 5 + 3 = 8
addNumbers(10, 7);  // 10 + 7 = 17
```

### 🔧 Пример 4. Функция, которая возвращает результат

Ключевое слово `return` возвращает значение наружу.

```javascript
function sum(a, b) {
    let result = a + b;
    return result;   // возвращаем значение
}

let total = sum(5, 3);
console.log(total);   // 8
```

> ⚠️ **Важно:** После `return` функция прекращает свою работу. Код после `return` не выполняется.

```javascript
function test() {
    return "Привет";
    console.log("Это никогда не выполнится");  // ❌ игнорируется
}
```

### 🔧 Пример 5. Функция для проверки пароля

```javascript
function isPasswordStrong(password) {
    if (password.length >= 6) {
        return true;   // пароль подходит
    } else {
        return false;  // пароль слишком короткий
    }
}

let pwd1 = "123456";
let pwd2 = "123";

console.log(isPasswordStrong(pwd1));  // true
console.log(isPasswordStrong(pwd2));  // false

// Используем в условии
if (isPasswordStrong(pwd1)) {
    console.log("Пароль надёжный");
} else {
    console.log("Пароль слишком короткий");
}
```

### 🔧 Функции и события (клик на кнопку)

```html
<button id="myBtn">Нажми на меня</button>

<script>
    function sayHello() {
        alert("Здравствуйте!");
    }

    let button = document.querySelector("#myBtn");
    button.onclick = sayHello;   // ВНИМАНИЕ: без скобок!
</script>
```

> ⭐ **Очень важно!** Когда привязываем функцию к событию, пишем имя функции **БЕЗ скобок**.
> - `sayHello` — передаём ссылку на функцию (выполнится при клике)
> - `sayHello()` — вызываем функцию сразу (выполнится в момент написания кода)

---

## 6. Проверка форм (валидация) (20 минут)

### ❓ Зачем проверять формы?

- 🚫 Чтобы пользователь не отправил пустую форму
- 🔒 Чтобы пароль был не слишком коротким
- 📧 Чтобы email содержал символ @ и точку
- 📅 Чтобы год рождения был разумным (например, не 2500 год)

### 💻 Пример 1. Проверка на пустоту

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Проверка email</title>
    <style>
        #errorMsg { margin-top: 10px; font-weight: bold; }
        .error { color: red; }
        .success { color: green; }
    </style>
</head>
<body>
    <h2>Проверка email</h2>
    <input type="text" id="email" placeholder="Введите ваш email">
    <button id="submitBtn">Отправить</button>
    <p id="errorMsg"></p>

    <script>
        let submit = document.querySelector("#submitBtn");
        let emailInput = document.querySelector("#email");
        let error = document.querySelector("#errorMsg");

        submit.onclick = function() {
            let email = emailInput.value;
            
            if (email === "") {
                error.textContent = "Ошибка: поле email не может быть пустым!";
                error.className = "error";
            } else {
                error.textContent = "Спасибо! Email принят.";
                error.className = "success";
            }
        };
    </script>
</body>
</html>
```

### 💻 Пример 2. Проверка длины пароля

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Проверка пароля</title>
    <style>
        #pwdMsg { margin-top: 10px; font-weight: bold; }
        .error { color: red; }
        .success { color: green; }
        .warning { color: orange; }
    </style>
</head>
<body>
    <h2>Проверка надёжности пароля</h2>
    <input type="password" id="password" placeholder="Введите пароль">
    <button id="checkPwd">Проверить</button>
    <p id="pwdMsg"></p>

    <script>
        let checkBtn = document.querySelector("#checkPwd");
        let pwdInput = document.querySelector("#password");
        let msg = document.querySelector("#pwdMsg");

        function checkPassword(password) {
            if (password.length < 6) {
                return { text: "❌ Слишком короткий (минимум 6 символов)", class: "error" };
            } else if (password.length > 20) {
                return { text: "⚠️ Слишком длинный (максимум 20 символов)", class: "warning" };
            } else if (password === "123456" || password === "qwerty" || password === "password") {
                return { text: "⚠️ Слишком простой пароль", class: "warning" };
            } else {
                return { text: "✅ Хороший пароль!", class: "success" };
            }
        }

        checkBtn.onclick = function() {
            let password = pwdInput.value;
            let result = checkPassword(password);
            msg.textContent = result.text;
            msg.className = result.class;
        };
    </script>
</body>
</html>
```

### 💻 Пример 3. Проверка email (содержит @ и точку)

```javascript
function isValidEmail(email) {
    // Проверяем, есть ли символ @
    if (email.indexOf("@") === -1) {
        return false;
    }
    
    // Проверяем, есть ли точка после @
    let atIndex = email.indexOf("@");
    let dotAfterAt = email.indexOf(".", atIndex);
    
    if (dotAfterAt === -1) {
        return false;
    }
    
    // Проверяем, что email не пустой и не начинается с @
    if (email.length < 5 || email[0] === "@") {
        return false;
    }
    
    return true;
}

// Пример использования
console.log(isValidEmail("test@mail.ru"));     // true
console.log(isValidEmail("test@mail"));        // false (нет точки)
console.log(isValidEmail("testmail.ru"));      // false (нет @)
console.log(isValidEmail("@mail.ru"));         // false (начинается с @)
```

### 💻 Пример 4. Полная проверка формы регистрации

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Регистрация</title>
    <style>
        body { font-family: Arial; padding: 20px; }
        .form-group { margin-bottom: 15px; }
        label { display: inline-block; width: 150px; }
        input { padding: 5px; width: 200px; }
        button { padding: 8px 20px; }
        .error { color: red; font-size: 14px; margin-top: 5px; }
        .success { color: green; font-weight: bold; }
        .form-group { margin-bottom: 15px; }
    </style>
</head>
<body>
    <h2>📝 Форма регистрации</h2>
    
    <div class="form-group">
        <label>Логин:</label>
        <input type="text" id="login" placeholder="не менее 3 символов">
        <span class="error" id="loginError"></span>
    </div>
    
    <div class="form-group">
        <label>Пароль:</label>
        <input type="password" id="password" placeholder="не менее 6 символов">
        <span class="error" id="passwordError"></span>
    </div>
    
    <div class="form-group">
        <label>Подтверждение пароля:</label>
        <input type="password" id="confirmPassword">
        <span class="error" id="confirmError"></span>
    </div>
    
    <div class="form-group">
        <label>Email:</label>
        <input type="text" id="email" placeholder="example@mail.ru">
        <span class="error" id="emailError"></span>
    </div>
    
    <button id="registerBtn">Зарегистрироваться</button>
    <p id="resultMsg"></p>

    <script>
        let loginInput = document.querySelector("#login");
        let passwordInput = document.querySelector("#password");
        let confirmInput = document.querySelector("#confirmPassword");
        let emailInput = document.querySelector("#email");
        let registerBtn = document.querySelector("#registerBtn");
        let resultMsg = document.querySelector("#resultMsg");
        
        let loginError = document.querySelector("#loginError");
        let passwordError = document.querySelector("#passwordError");
        let confirmError = document.querySelector("#confirmError");
        let emailError = document.querySelector("#emailError");

        function clearErrors() {
            loginError.textContent = "";
            passwordError.textContent = "";
            confirmError.textContent = "";
            emailError.textContent = "";
            resultMsg.textContent = "";
        }

        function validateLogin(login) {
            if (login === "") {
                return "Логин не может быть пустым";
            }
            if (login.length < 3) {
                return "Логин должен быть не менее 3 символов";
            }
            return null;
        }

        function validatePassword(password) {
            if (password === "") {
                return "Пароль не может быть пустым";
            }
            if (password.length < 6) {
                return "Пароль должен быть не менее 6 символов";
            }
            return null;
        }

        function validateConfirm(password, confirm) {
            if (confirm === "") {
                return "Подтвердите пароль";
            }
            if (password !== confirm) {
                return "Пароли не совпадают";
            }
            return null;
        }

        function validateEmail(email) {
            if (email === "") {
                return "Email не может быть пустым";
            }
            if (email.indexOf("@") === -1) {
                return "Email должен содержать символ @";
            }
            let atIndex = email.indexOf("@");
            let dotAfterAt = email.indexOf(".", atIndex);
            if (dotAfterAt === -1) {
                return "Email должен содержать точку после @";
            }
            if (email.length < 5) {
                return "Email слишком короткий";
            }
            return null;
        }

        registerBtn.onclick = function() {
            clearErrors();
            
            let login = loginInput.value;
            let password = passwordInput.value;
            let confirm = confirmInput.value;
            let email = emailInput.value;
            
            let isValid = true;
            
            let loginErr = validateLogin(login);
            if (loginErr) {
                loginError.textContent = loginErr;
                isValid = false;
            }
            
            let passwordErr = validatePassword(password);
            if (passwordErr) {
                passwordError.textContent = passwordErr;
                isValid = false;
            }
            
            let confirmErr = validateConfirm(password, confirm);
            if (confirmErr) {
                confirmError.textContent = confirmErr;
                isValid = false;
            }
            
            let emailErr = validateEmail(email);
            if (emailErr) {
                emailError.textContent = emailErr;
                isValid = false;
            }
            
            if (isValid) {
                resultMsg.textContent = "✅ Регистрация прошла успешно! Добро пожаловать, " + login + "!";
                resultMsg.style.color = "green";
                resultMsg.style.fontWeight = "bold";
                
                // Очищаем поля (опционально)
                // loginInput.value = "";
                // passwordInput.value = "";
                // confirmInput.value = "";
                // emailInput.value = "";
            } else {
                resultMsg.textContent = "❌ Пожалуйста, исправьте ошибки в форме";
                resultMsg.style.color = "red";
            }
        };
    </script>
</body>
</html>
```

---

# Часть 2. Практика за компьютерами (90 минут)

## Этап 1. Разбор примеров (30 минут)

Студенты набирают следующие примеры и проверяют их работу. Каждый пример сохраняют в отдельный HTML-файл.

### Пример А. Проверка имени (if/else)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Пример А</title>
</head>
<body>
    <input type="text" id="userName" placeholder="Введите имя">
    <button id="checkBtn">Проверить</button>
    <p id="message"></p>

    <script>
        let button = document.querySelector("#checkBtn");
        let input = document.querySelector("#userName");
        let output = document.querySelector("#message");

        button.onclick = function() {
            let name = input.value;
            if (name === "") {
                output.textContent = "Ошибка: имя не может быть пустым!";
                output.style.color = "red";
            } else {
                output.textContent = "Привет, " + name + "!";
                output.style.color = "green";
            }
        };
    </script>
</body>
</html>
```

### Пример Б. Функция sum

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Пример Б</title>
</head>
<body>
    <input type="number" id="num1" placeholder="Число 1">
    <input type="number" id="num2" placeholder="Число 2">
    <button id="sumBtn">Сложить</button>
    <p id="result"></p>

    <script>
        function sum(a, b) {
            return a + b;
        }

        let btn = document.querySelector("#sumBtn");
        let input1 = document.querySelector("#num1");
        let input2 = document.querySelector("#num2");
        let resultP = document.querySelector("#result");

        btn.onclick = function() {
            let a = Number(input1.value);
            let b = Number(input2.value);
            let total = sum(a, b);
            resultP.textContent = "Сумма: " + total;
        };
    </script>
</body>
</html>
```

### Пример В. Проверка длины пароля

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Пример В</title>
</head>
<body>
    <input type="password" id="password" placeholder="Введите пароль">
    <button id="checkPwd">Проверить</button>
    <p id="pwdMsg"></p>

    <script>
        let checkBtn = document.querySelector("#checkPwd");
        let pwdInput = document.querySelector("#password");
        let msg = document.querySelector("#pwdMsg");

        function checkPassword(pwd) {
            if (pwd.length < 6) {
                return "Слишком короткий (минимум 6 символов)";
            } else if (pwd.length > 20) {
                return "Слишком длинный (максимум 20 символов)";
            } else {
                return "Пароль подходит";
            }
        }

        checkBtn.onclick = function() {
            let password = pwdInput.value;
            let result = checkPassword(password);
            msg.textContent = result;
            
            if (result === "Пароль подходит") {
                msg.style.color = "green";
            } else {
                msg.style.color = "red";
            }
        };
    </script>
</body>
</html>
```

---

## Этап 2. Самостоятельные задания (60 минут)

### Задание 1. Чётное или нечётное (15 минут)

Создайте файл `task1.html` со следующим:
- Поле ввода числа (`<input type="number">`)
- Кнопка «Проверить»
- Абзац для вывода результата

**Что должна делать программа:**
При клике на кнопку определить, чётное число ввёл пользователь или нечётное. Вывести в абзац: «Чётное» или «Нечётное».

**Подсказка:** число чётное, если остаток от деления на 2 равен 0. Проверка: `if (число % 2 === 0)`

**Дополнительное требование:** если поле пустое — вывести сообщение «Введите число».

---

### Задание 2. Калькулятор скидки (20 минут)

Создайте файл `task2.html` со следующим:
- Поле «Стоимость товара» (число)
- Поле «Возраст покупателя» (число)
- Кнопка «Рассчитать»
- Абзац для вывода итоговой цены

**Правила скидки:**
| Возраст | Скидка |
|---------|--------|
| до 18 лет | 10% |
| от 60 лет и старше | 20% |
| остальные (18-59) | 0% |

**Формула:** цена со скидкой = цена - (цена * скидка / 100)

**Пример вывода:** «Итоговая цена: 900 рублей» (если была скидка 10% от 1000)

**Дополнительное требование:** использовать отдельную функцию для расчёта скидки.

---

### Задание 3. Проверка формы регистрации (25 минут) — ГЛАВНОЕ ЗАДАНИЕ

Создайте файл `task3.html` со следующими полями:

1. **Логин** (текстовое поле) — не менее 3 символов
2. **Пароль** (поле `type="password"`) — не менее 6 символов
3. **Подтверждение пароля** (поле `type="password"`)
4. **Email** (текстовое поле) — должен содержать символ `@` и точку `.`
5. **Кнопка «Зарегистрироваться»**
6. **Область для вывода ошибок** (абзац или div)

**Что проверяем при клике на кнопку:**

| Поле | Условие | Сообщение об ошибке |
|------|---------|---------------------|
| Логин | длина < 3 | Логин должен быть не менее 3 символов |
| Пароль | длина < 6 | Пароль должен быть не менее 6 символов |
| Подтверждение | не совпадает с паролем | Пароли не совпадают |
| Email | не содержит @ или не содержит точку | Введите корректный email (с @ и точкой) |

**Если все проверки пройдены:**
Вывести зелёное сообщение «Регистрация успешна!»

**Дополнительно (для сильных студентов):**
- Проверить, что email содержит точку ПОСЛЕ символа `@`
- Добавить проверку, что логин не содержит пробелов
- Добавить кнопку «Очистить форму»

**Подсказка для проверки email:**
```javascript
let email = emailInput.value;
if (email.indexOf("@") === -1) {
    // нет символа @
}
let atIndex = email.indexOf("@");
let dotAfterAt = email.indexOf(".", atIndex);
if (dotAfterAt === -1) {
    // нет точки после @
}
```

---

### Задание 4. Дополнительное (для тех, кто сделал всё быстро)

**Калькулятор индекса массы тела (ИМТ)**

Создайте файл `task4.html` со следующим:
- Поле «Рост (см)» (число)
- Поле «Вес (кг)» (число)
- Кнопка «Рассчитать ИМТ»
- Абзац для вывода результата

**Формула:** ИМТ = вес / (рост_в_метрах * рост_в_метрах)

**Важно:** рост в метрах = рост в сантимет
