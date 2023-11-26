# Деделюк Володимир | ІПЗс-23-1 

###### Ця програма є простою системою для зберігання, читання, оновлення та видалення даних користувачів у текстовому файлі.

## Створення або перевірка наявності файлу

```javascript
const fs = require('fs');
const filename = 'user_data.txt';

if (!fs.existsSync(filename)) {
    fs.writeFileSync(filename, ''); 
    console.log(`Файл ${filename} був створений.`);
}
```

Код перевіряє, чи існує файл `user_data.txt`. Якщо файл відсутній, він створює порожній файл та виводить повідомлення про його створення.

## Запис користувача в файл

```javascript
function writeUserData(name, age) {
    const data = `${name},${age}\n`;

    fs.appendFile(filename, data, (err) => {
        if (err) throw err;
        console.log('Дані успішно записано в файл.');
    });
}
```

Функція отримує ім'я та вік користувача, створює рядок у форматі "ім'я,вік" і додає його у файл

## Читання даних користувача з файлу

```javascript
function readUserData() {
    fs.readFile(filename, 'utf8', (err, data) => {
        if (err) throw err;

        if (data.trim() === '') {
            console.log('Файл користувача порожній.');
        } else {
            console.log('Дані користувача в файлі:');
            console.log(data);
            askUserAction();
        }
    });
}
```

Функція читає дані з файлу та виводить їх у консоль. Якщо файл порожній, виводиться відповідне повідомлення.

## Видалення даних користувача з файлу

```javascript
function deleteUserData() {
    fs.unlink(filename, (err) => {
        if (err) throw err;
        console.log('Дані користувача успішно видалено з файлу.');
    });
}
```

Функція видаляє файл із даними користувача.

## Оновлення даних користувача в файлі

```javascript
function updateUserData(nameToUpdate, newAge) {
```

Функція питає користувача про новий вік для конкретного імені та оновлює відповідні дані в файлі.

## Функції для взаємодії з користувачем

- `askUserAction()`: Питає користувача, чи хоче він змінити чи видалити дані користувача.
- `updateOrDeleteUserData()`: Питає користувача про ім'я користувача, якого він хоче змінити або видалити, і перевіряє, чи такий користувач існує.
- `askUpdateOrDelete(name)`: Питає користувача, чи хоче він змінити чи видалити дані для конкретного користувача.

## Введення початкових даних користувача

```javascript
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.question('Введіть ім\'я користувача: ', (name) => {
    rl.question('Введіть вік користувача: ', (age) => {
        rl.close();
        writeUserData(name, age);
        readUserData();
    });
});
```

Код використовує `readline` для запитання імені та віку користувача та записує їх у файл.

