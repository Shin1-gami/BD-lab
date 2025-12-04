
# Звіт з лабораторної роботи №6  
Тема: Робота з СУБД MongoDB та реалізація операцій  
Дисципліна: Бази даних  
Варіант: 3 
Студент: Величко Ростислав  
Група: ІПЗ-32 

---

## 1. Мета роботи
Освоїти принципи роботи з NoSQL документо-орієнтованою базою даних MongoDB, навчитися виконувати базові операції створення, читання, оновлення та видалення документів, відкрити механізми запитів та індексації, розвинути розуміння відмінностей між реляційними та документальними підходами до зберігання даних

---

## 2. Хід роботи

### 2.1. Створення бази даних і колекцій (Рівень 1)
<a href="https://ibb.co/jZf4RR9g"><img src="https://i.ibb.co/S7yvrrDR/scr1.png" alt="scr1" border="0"></a>
#### 2.1.1. Перемикання на БД `library`

`use library` 

#### 2.2.1. Створення колекцій з валідацією
<a href="https://ibb.co/275g8QHv"><img src="https://i.ibb.co/4ZJPsG38/1.png" alt="1" border="0"></a>
 
---

### 2.3. Заповнення колекцій даними – Рівень 1

#### 2.3.1. Колекція `authors`

<a href="https://ibb.co/BVhsMnwZ"><img src="https://i.ibb.co/JRYkJ3C7/2.png" alt="2" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/DPnmNPCW/3.png" alt="3" border="0"></a>

#### 2.3.2. Колекція `books` 

<a href="https://ibb.co/3mxhYcf9"><img src="https://i.ibb.co/GQZP3Rs4/4.png" alt="4" border="0"></a>
<a href="https://ibb.co/6cczwjc7"><img src="https://i.ibb.co/ymmtPHmc/5.png" alt="5" border="0"></a>
<a href="https://ibb.co/QFmHf2jV"><img src="https://i.ibb.co/7JypXwND/6.png" alt="6" border="0"></a>
<a href="https://ibb.co/NnFTXfJ7"><img src="https://i.ibb.co/dJfmSXV7/7.png" alt="7" border="0"></a>

#### 2.3.3. Колекція `users` 

<a href="https://ibb.co/GStW0KT"><img src="https://i.ibb.co/3ZMp7Dz/8.png" alt="8" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/F4x0Ddp7/9.png" alt="9" border="0"></a>

----------

### 2.4. Виконання CRUD-операцій (Рівень 1)

#### 2.4.1. Операції читання

<a href="https://ibb.co/G3bcsrbZ"><img src="https://i.ibb.co/XkvSyGvn/10.png" alt="10" border="0"></a>
<a href="https://ibb.co/4Rk282kd"><img src="https://i.ibb.co/WvC0k0Ct/11.png" alt="11" border="0"></a>
<a href="https://ibb.co/qLWBrYXV"><img src="https://i.ibb.co/V0QVqYr5/12.png" alt="12" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/ynbTSfY8/13.png" alt="13" border="0"></a>
<a href="https://ibb.co/Z1cbxxMs"><img src="https://i.ibb.co/bRNGXXKh/14.png" alt="14" border="0"></a>
<a href="https://ibb.co/rfyy4hnk"><img src="https://i.ibb.co/XkJJSPmX/15.png" alt="15" border="0"></a>
<a href="https://ibb.co/NnTSgFCk"><img src="https://i.ibb.co/k6m1VGBr/16.png" alt="16" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/wrzS8K6m/17.png" alt="17" border="0"></a>
<a href="https://ibb.co/PZ7ZBMDs"><img src="https://i.ibb.co/jvcv7zJ9/18.png" alt="18" border="0"></a>
<a href="https://ibb.co/xqdxVNrf"><img src="https://i.ibb.co/LdHV43sJ/19.png" alt="19" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/xSDygNT4/20.png" alt="20" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/1Y2LLcsR/21.png" alt="21" border="0"></a>
<a href="https://ibb.co/DfJ9nYhV"><img src="https://i.ibb.co/yF96Jptf/22.png" alt="22" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/gLjyg9zc/23.png" alt="23" border="0"></a>
<a href="https://ibb.co/MxHHCRgZ"><img src="https://i.ibb.co/FL11DBhm/24.png" alt="24" border="0"></a>
<a href="https://ibb.co/NgZsbXKc"><img src="https://i.ibb.co/ZRWV73xq/25.png" alt="25" border="0"></a>
<a href="https://ibb.co/zHW4NQPq"><img src="https://i.ibb.co/0VpGQmYH/26.png" alt="26" border="0"></a>
<a href="https://ibb.co/7t2nmmd3"><img src="https://i.ibb.co/Jj5vJJwY/27.png" alt="27" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/7tkvPGVt/28.png" alt="28" border="0"></a>
<a href="https://ibb.co/tMRCb84C"><img src="https://i.ibb.co/Rp8HCz9H/29.png" alt="29" border="0"></a> 

#### 2.4.2. Оновлення

<a href="https://imgbb.com/"><img src="https://i.ibb.co/JR73VqfD/30.png" alt="30" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/Sw4xKPNW/31.png" alt="31" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/YFVYcDqs/32.png" alt="32" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/KcrdYZXC/33.png" alt="33" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/VckFz0Cw/34.png" alt="34" border="0"></a>

#### 2.4.3. Видалення

<a href="https://imgbb.com/"><img src="https://i.ibb.co/gFyDk9Y4/35.png" alt="35" border="0"></a>
<a href="https://ibb.co/YB3NBNwW"><img src="https://i.ibb.co/3m7TmTQs/36.png" alt="36" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/4n4k97JY/37.png" alt="37" border="0"></a> 

----------

### 2.5. Створення індексів і аналіз продуктивності (Рівень 1–2)

<a href="https://imgbb.com/"><img src="https://i.ibb.co/WNKWQLcK/38.png" alt="38" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/XxTkM58R/39.png" alt="39" border="0"></a>
<a href="https://ibb.co/Kxn4TBXw"><img src="https://i.ibb.co/zVd9qCrJ/40.png" alt="40" border="0"></a>
<a href="https://ibb.co/ZRZKy4pB"><img src="https://i.ibb.co/V0KDXncg/41.png" alt="41" border="0"></a>
<a href="https://ibb.co/5gL6F6FZ"><img src="https://i.ibb.co/Xrtb8b8H/42.png" alt="42" border="0"></a>
<a href="https://ibb.co/JjhcC9VH"><img src="https://i.ibb.co/RT5g7qfc/43.png" alt="43" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/B2FDWBrK/44.png" alt="44" border="0"></a> 

Для порівняння продуктивності:

1.  Виконав запит до створення індексу:

<a href="https://ibb.co/5W1h9WY2"><img src="https://i.ibb.co/MDgkhD89/45.png" alt="45" border="0"></a>
<a href="https://ibb.co/Xfk72P3j"><img src="https://i.ibb.co/Kcz20gLb/46.png" alt="46" border="0"></a>
<a href="https://ibb.co/QFV0MC5h"><img src="https://i.ibb.co/vxW9kQtf/47.png" alt="47" border="0"></a>
<a href="https://ibb.co/cKwWrVhq"><img src="https://i.ibb.co/Cp6jHDKL/48.png" alt="48" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/9HxGdJwV/49.png" alt="49" border="0"></a>

2.  Створити індекс та виконав той самий запит ще раз та порівняв поля:
    
 <a href="https://ibb.co/gFStsJq9"><img src="https://i.ibb.co/k64qYXbB/50.png" alt="50" border="0"></a>
<a href="https://ibb.co/0yddSNj6"><img src="https://i.ibb.co/TMFFSXB7/51.png" alt="51" border="0"></a>
<a href="https://ibb.co/pj7Dg32Y"><img src="https://i.ibb.co/PGLpR5xq/52.png" alt="52" border="0"></a>
<a href="https://ibb.co/tw8RVPTP"><img src="https://i.ibb.co/Y4pgHTFT/53.png" alt="53" border="0"></a>
<a href="https://ibb.co/v4KFZ3L8"><img src="https://i.ibb.co/m5Mj69h7/54.png" alt="54" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/LDTW85qM/55.png" alt="55" border="0"></a>

---

### 2.6. Агрегаційні запити (Рівень 2)

<a href="https://ibb.co/GvB9C4t5"><img src="https://i.ibb.co/DDsYwH8R/56.png" alt="56" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/srHYRbV/57.png" alt="57" border="0"></a>
<a href="https://ibb.co/R4d5hrRn"><img src="https://i.ibb.co/XkMwy0cB/58.png" alt="58" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/q3XZSzmj/59.png" alt="59" border="0"></a>
<a href="https://ibb.co/m53TtHXB"><img src="https://i.ibb.co/PGdj459Y/60.png" alt="60" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/HLbVMpK1/61.png" alt="61" border="0"></a>
<a href="https://ibb.co/HD5FwM6L"><img src="https://i.ibb.co/XZc20d1f/62.png" alt="62" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/jvXgfJyV/63.png" alt="63" border="0"></a>

----------

### 2.7. Об’єднання колекцій за допомогою `$lookup` (Рівень 2)

<a href="https://imgbb.com/"><img src="https://i.ibb.co/S4mFh3rP/64.png" alt="64" border="0"></a> 


<a href="https://imgbb.com/"><img src="https://i.ibb.co/v68gF7yP/65.png" alt="65" border="0"></a>
<a href="https://ibb.co/2YvjR1zw"><img src="https://i.ibb.co/Tq4HJxQZ/66.png" alt="66" border="0"></a>
<a href="https://ibb.co/sJck5cpG"><img src="https://i.ibb.co/Cs4NJ4pZ/67.png" alt="67" border="0"></a>

---

### 2.8. Текстовий пошук (Рівень 2–3)


<a href="https://imgbb.com/"><img src="https://i.ibb.co/39HQnGLn/68.png" alt="68" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/6cBtLf5B/69.png" alt="69" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/0R7mDMhs/70.png" alt="70" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/d4tJXBG8/71.png" alt="71" border="0"></a>

---

### 2.9. Валідація схеми (JSON Schema, Рівень 3)

Модифікуємо колекцію `books`, посиливши обмеження:

<a href="https://ibb.co/SXNK1z3F"><img src="https://i.ibb.co/bg1rykKc/72.png" alt="72" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/4gtsGRB5/73.png" alt="73" border="0"></a> 

Спроба вставити некоректний документ:
<a href="https://imgbb.com/"><img src="https://i.ibb.co/ym5mN6nT/74.png" alt="74" border="0"></a>

---
### 3 Порівняльний аналіз
Реляційний підхід (PostgreSQL)
```sql
CREATE TABLE authors (
    author_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    birth_year INT,
    nationality VARCHAR(50)
);

CREATE TABLE books (
    book_id SERIAL PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    author_id INT REFERENCES authors(author_id),
    publication_year INT,
    pages INT,
    available BOOLEAN DEFAULT TRUE
);

CREATE TABLE genres (
    genre_id SERIAL PRIMARY KEY,
    genre_name VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE book_genres (
    book_id INT REFERENCES books(book_id),
    genre_id INT REFERENCES genres(genre_id),
    PRIMARY KEY (book_id, genre_id)
);
```

<a href="https://ibb.co/3907qD5Q"><img src="https://i.ibb.co/nNDbvHqt/101.png" alt="101" border="0"></a>

Документний підхід (MongoDB)
``` 
{
  _id: ObjectId("..."),
  title: "Кобзар",
  author: {
    name: "Тарас Шевченко",
    birth_year: 1814,
    nationality: "український"
  },
  genres: ["поезія", "романтизм"],
  publication_year: 1840,
  pages: 238,
  available: true
}
```
---
## Висновки
У ході виконання лабораторної роботи було детально опрацьовано принципи роботи з документоорієнтованою СУБД MongoDB. Я створив повноцінну базу даних бібліотеки, додав структуровані та вкладені документи, виконав базові операції CRUD, реалізував складні запити з логічними операторами та операторами для масивів, налаштував індекси й проаналізував їх вплив на продуктивність.  
Було розглянуто можливості агрегаційного конвеєра, текстового пошуку, об’єднання колекцій через `$lookup`, створення представлень (view) та застосування JSON Schema для валідації структури документів.   
Порівняння реляційного та документного підходів показало, що MongoDB забезпечує високу гнучкість, простоту масштабування та зручність роботи з об’єктними структурами, що робить її ефективною для систем із динамічною або нерегулярною структурою даних.