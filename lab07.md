# Звіт з лабораторної роботи №7

Тема: Повний цикл розробки NoSQL застосування з інтеграцією  
Дисципліна: Бази даних  
Студент: Величко Ростислав  
Група: ІПЗ-32
Варіант: 3

---

#  1. Мета  роботи

Застосувати знання роботи з базами даних NoSQL для створення повноцінного веб-застосунку, навчитися проектувати документні схеми для реальних предметних областей, опанувати інтеграцію MongoDB з фронтенд-технологіями, розвинути навички аналізу та оптимізацію продуктивності документо-орієнтованих систем
    
---

# 2.Хід роботи
 ## 2.1. Створення колекцій
Створено базу:
`blog_system`

У базі створено такі колекції:
`users categories
posts` 

---

## 2.2. Створення seed-файлів

###  seed_users.js

Створює тестових користувачів із полями:

`{
  username, email, avatar_url, role
}` 

<a href="https://ibb.co/NdkCzK5V"><img src="https://i.ibb.co/8LRsV9qK/seedusers.png" alt="seedusers" border="0"></a>
### seed_categories.js

Додає категорії:

`{
  name, slug, description
}` 

<a href="https://ibb.co/C58kXr0y"><img src="https://i.ibb.co/PZj7bSCy/seedcategor.png" alt="seedcategor" border="0"></a>
### seed_posts.js

Формує стартові пости:

`{
  title, content, excerpt,
  author, category, tags, statistics: { views, likes, comments_count }
}` 

<a href="https://ibb.co/hRpMFcR9"><img src="https://i.ibb.co/C5xtK658/seedposts1.png" alt="seedposts1" border="0"></a>
<a href="https://ibb.co/yz5Xw9P"><img src="https://i.ibb.co/xnGDpkL/seedposts2.png" alt="seedposts2" border="0"></a>

Запуск:

`node seed_users.js
node seed_categories.js
node seed_posts.js` 

----------

# 2.3. Розробка серверної частини

Створено файл:

`server.js` 

### Реалізовано такі API-маршрути:

- Маршрут

- Метод

- Призначення

`/api/posts`

- GET

- Отримати 10 останніх постів

`/api/posts`

- POST

- Створити новий пост

`/api/posts/:id/view`

- POST

- Збільшити кількість переглядів

`/api/posts/:id/like`

- POST

- Додати лайк

`/api/posts/by-tag/:tag`

- GET

- Пошук за тегом

`/api/posts/page/:num`

- GET

- Пагінація

<a href="https://ibb.co/spCKwM5R"><img src="https://i.ibb.co/9mhbTCwg/server1.png" alt="server1" border="0"></a>
<a href="https://ibb.co/LXfJ4kZ2"><img src="https://i.ibb.co/NdzmwVyH/server2.png" alt="server2" border="0"></a>
<a href="https://ibb.co/LXFSYKWc"><img src="https://i.ibb.co/0R7qm5S6/server3.png" alt="server3" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/8DWpB0b5/server4.png" alt="server4" border="0"></a>

Сервер запускається командою:

`node server.js` 

---

# 2.4. Розробка клієнтської частини

У каталозі `public/` створено:

`index.html` 

### Реалізовано:

### Завантаження постів з реальної бази

`async  function  loadRealPosts() { const res = await  fetch("/api/posts"); const posts = await res.json();
    allPosts = posts; renderPosts(posts);
}` 

---

### Показ карток постів у сітці

Відображаються:

-   назва
    
-   автор
    
-   категорія
    
-   перегляди
    
-   лайки
    
-   уривок статті
    

----------

### Модальне вікно статті

При кліку:

-   показується повний текст
    
-   викликається API переглядів
    
-   можна поставити лайк
    

``await  fetch(`/api/posts/${id}/view`, { method: "POST" });`` 

---

###  Пошук по назві та опису

`allPosts.filter(p => p.title.includes(term))` 

<a href="https://ibb.co/yG4Rkm7"><img src="https://i.ibb.co/8TYBxnt/index11.png" alt="index11" border="0"></a>
<a href="https://ibb.co/yFZ4gXdK"><img src="https://i.ibb.co/hF4Y2yLr/index12.png" alt="index12" border="0"></a>
<a href="https://ibb.co/mCmY9vDJ"><img src="https://i.ibb.co/svhDK5mj/index13.png" alt="index13" border="0"></a>

---

# 2.5. Порівняльний аналіз реляційної та документної моделі

### Реляційна модель (PostgreSQL):

-   Чітко структурована

-   Потрібні JOIN
    
-   Висока цілісність
    
-   Швидка аналітика
    
-   Складніша денормалізація
    

### Документна модель (MongoDB):

-   Дані зберігаються у вигляді JSON
    
-   Немає JOIN → простіший запит
    
-   Швидка робота з вкладеними структурами
    
-   Немає фіксованої схеми
    
-   Ідеально підходить для блогів, каталогів, профілів
    

### Приклад MongoDB документа:

`{  "title":  "Кобзар",  "author":  {  "name":  "Тарас Шевченко",  "birth_year":  1814  },  "genres":  ["поезія",  "романтизм"],  "available":  true  }` 

Запит:

`db.books.find({ available: true })` 

Використовує лише 1 колекцію — JOIN не потрібні.

----------

# ## 3. Висновки

У ході лабораторної роботи було:
-  встановлено та налаштовано MongoDB  
 - створено базу даних та колекції  
 - додано дані через seed-файли  
 - реалізовано повноцінний REST-API  
 - створено функціональний веб-інтерфейс
  
 реалізовано:
-  перегляди
    
-   лайки
    
-   пошук
    
-   пагінацію
    
-   модальні вікна
    
 виконано порівняльний аналіз SQL і NoSQL
MongoDB продемонструвала високу гнучкість та ефективність для веб-проєктів типу блогів, новинних стрічок і контент-систем.

# Додаткові скріншоти
<a href="https://ibb.co/Z1tKXRBd"><img src="https://i.ibb.co/7N8VCxnv/2.png" alt="2" border="0"></a>
<a href="https://ibb.co/Y7smRTLM"><img src="https://i.ibb.co/6RCznJWx/3.png" alt="3" border="0"></a>
<a href="https://ibb.co/Q3MtKg3T"><img src="https://i.ibb.co/S4BG3j4M/4.png" alt="4" border="0"></a>
<a href="https://ibb.co/ynBYbLCp"><img src="https://i.ibb.co/pvrR9CTQ/5.png" alt="5" border="0"></a>
<a href="https://ibb.co/N0tkPSg"><img src="https://i.ibb.co/GZn1LTf/6.png" alt="6" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/DPrPkShD/7.png" alt="7" border="0"></a>
<a href="https://ibb.co/S4qkrTx0"><img src="https://i.ibb.co/mVQn8sBt/8.png" alt="8" border="0"></a>
<a href="https://ibb.co/ZRTnBjT2"><img src="https://i.ibb.co/xK5p1k5F/9.png" alt="9" border="0"></a>
<a href="https://ibb.co/xqfsJtHp"><img src="https://i.ibb.co/fdnS4zvh/10.png" alt="10" border="0"></a>
<a href="https://ibb.co/jkP5Jnxk"><img src="https://i.ibb.co/2316ZGL3/11.png" alt="11" border="0"></a>
<a href="https://ibb.co/8gmpNWXJ"><img src="https://i.ibb.co/whdXB9YT/12.png" alt="12" border="0"></a>
<a href="https://ibb.co/7trVwGPg"><img src="https://i.ibb.co/RTQPxCfh/13.png" alt="13" border="0"></a>
<a href="https://ibb.co/xK7W57vX"><img src="https://i.ibb.co/CpHg0Hdm/14.png" alt="14" border="0"></a>
<a href="https://ibb.co/hxr1ZqR1"><img src="https://i.ibb.co/ymKBY3nB/15.png" alt="15" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/SwTjqvXh/16.png" alt="16" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/GfD8ZMP2/17.png" alt="17" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/93cjwB9G/18.png" alt="18" border="0"></a>


<a href="https://ibb.co/SDQ9DSxM"><img src="https://i.ibb.co/6cvfcQZT/19.png" alt="19" border="0"></a>

<a href="https://ibb.co/ZRd4LJyP"><img src="https://i.ibb.co/vC1ywB2G/20.png" alt="20" border="0"></a>

