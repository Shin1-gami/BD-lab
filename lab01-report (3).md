# Лабораторна робота 1. Робота з СУБД PostgreSQL та основи SQL

  

## Загальна інформація

**Здобувач освіти:** Величко Ростислав

**Група:** ІПЗ-32

**Обраний рівень складності:** 3

**Посилання на проєкт:** https://supabase.com/dashboard/project/biwedgqqurtgbpttjglm

  

---

  

## Виконання завдань

  

### 1. Список таблиць

```sql

-- Запит для отримання списку таблиць

SELECT table_name

FROM information_schema.tables

WHERE table_schema = 'public'

ORDER BY table_name;

```

  

**Результат:**

У базі даних створено 8 основних таблиць:

`categories`, `customers`, `employees`, `order_items`, `orders`, `products`, `regions`, `suppliers`.

  

**Скріншот:**
![enter image description here](https://snipboard.io/QYiT6w.jpg)

  

---

  

### 2. Отримати всі записи з таблиці `customers`

```sql

SELECT * FROM customers;

```

  

**Результат:**

Отримано 15 записів клієнтів, включаючи як фізичних осіб, так і юридичні особи з різних міст України.

  

**Скріншот:**

![enter image description here](https://snipboard.io/uID7X9.jpg)

  

  
---

  

### 3. Показати контактні дані всіх співробітників

```sql

SELECT first_name, last_name, phone, email FROM employees;

```

  

**Результат:**

Отримано 8 записів співробітників, включаючи ім'я, прізвище, телефон, email.

  

**Скріншот:**

![enter image description here](https://snipboard.io/5nbmHl.jpg)


---

### 4. Знайти всіх клієнтів з міста Київ

```sql

SELECT  *  FROM customers WHERE city =  'Київ';

```

**Результат:**

Знайдено 4 клієнтів з міста Київ.

  

**Скріншот:**

![enter image description here](https://snipboard.io/0o6xI4.jpg)



---

### 5. Вивести товари, які коштують більше 25000 грн.

```sql

SELECT product_name, unit_price FROM products WHERE unit_price >  25000;

```

**Результат:**

Отримано список товарів з 13 записів які коштують більше 25000 грн.
  

**Скріншот:**

![enter image description here](https://snipboard.io/cDTdPq.jpg)



---

### 6. Показати всі замовлення зі статусом 'delivered'.

```sql

SELECT  *  FROM orders WHERE order_status =  'delivered';

```

**Результат:**

Отримано 26 записів замовлень зі статусом 'delivered'.
  

**Скріншот:**

![enter image description here](https://snipboard.io/niqjIK.jpg)

---

### 7. Знайти співробітників, які працюють у відділі продажів.

```sql

SELECT first_name, last_name, title, phone, email FROM employees WHERE title ILIKE  '%продаж%';

```

**Результат:**

Отримано 3 записи співробітників, які працюють у відділі продажів.
  

**Скріншот:**

![enter image description here](https://snipboard.io/P6Cb5I.jpg)

---

### 8. Відсортувати товари за зростанням ціни.

```sql

SELECT product_name, unit_price FROM products ORDER BY unit_price ASC;

```

**Результат:**

Отримано 25 записів товарів за зростанням ціни.
  

**Скріншот:**

![enter image description here](https://snipboard.io/fs20eZ.jpg)

---

### 9. Показати клієнтів в алфавітному порядку за іменем контактної особи.

```sql

SELECT contact_name, city, phone, email FROM customers ORDER BY contact_name ASC;

```

**Результат:**

Отримано 15 записів клієнтів в алфавітному порядку за іменем контактної особи.
  

**Скріншот:**
![enter image description here](https://snipboard.io/HtOiWT.jpg)

---

### 10. Вивести замовлення від найновіших до найстаріших.
```sql

SELECT order_id, customer_id, order_date, order_status FROM orders ORDER BY order_date DESC;

```

**Результат:**

Отримано 31 записів замовлень від найновіших до найстаріших.
  

**Скріншот:**
![enter image description here](https://snipboard.io/IGD8AB.jpg)

---

### 11. Показати перші 10 найдорожчих товарів.
```sql

SELECT product_name, unit_price FROM products ORDER BY unit_price DESC  LIMIT  10;

```

**Результат:**

Отримано 10 перших записів найдорожчих товарів.
  

**Скріншот:**
![enter image description here](https://snipboard.io/2xprMn.jpg)

---

### 12. Вивести 5 останніх замовлень (за датою).
```sql

SELECT order_id, customer_id, order_date, order_status FROM orders ORDER BY order_date DESC  LIMIT  5;

```

**Результат:**

Отримано 5 останніх записів замовлень за датою.
  

**Скріншот:**
![enter image description here](https://snipboard.io/VNhryS.jpg)


---

### 13. Отримати перших 8 клієнтів в алфавітному порядку.
```sql

SELECT contact_name, city, phone, email FROM customers ORDER BY contact_name ASC  LIMIT  8;

```

**Результат:**

Отримано 8 перших записів клієнтів в алфавітному порядку.
  

**Скріншот:**
![enter image description here](https://snipboard.io/fHOPlX.jpg)


---

### 14. Знайти всіх клієнтів, чиї імена починаються на "Іван".
```sql

SELECT  *  FROM customers WHERE contact_name LIKE  'Іван%';

```

**Результат:**

Отримано 1 запис клієнта, чиє ім'я починається на "Іван".
  

**Скріншот:**
![enter image description here](https://snipboard.io/7I54Mo.jpg)


---

### 15. Вивести товари, в назві яких є слово "phone" або "телефон".
```sql

SELECT product_name, unit_price

FROM products

WHERE product_name ILIKE  '%phone%'  OR product_name ILIKE  '%телефон%';

```

**Результат:**

Отримано 1 запис товару, в назві якого є слово "phone" або "телефон".
  

**Скріншот:**
![enter image description here](https://snipboard.io/ac9zXi.jpg)

---

### 16. Придумати та виконати 3 власні запити з використанням LIKE для пошуку за різними зразками (початок, кінець, містить).

### 16.1. Пошук постачальників у містах, назва яких закінчується на 'ів'.
```sql

SELECT company_name, city FROM suppliers WHERE city LIKE  '%ів';

```
**Бізнес-логіка:**
Допомагає знайти всіх постачальників, що знаходяться у містах, назви яких закінчуються на 'ів'. Це може бути корисним для аналізу географічного розподілу постачальників або для таргетованих логістичних операцій.


**Результат:**

Отримано 3 записи постачальників, назва яких закінчується на 'ів'.
  

**Скріншот:**
![enter image description here](https://snipboard.io/QjR4Kb.jpg)

### 16.2. Знайти співробітників, що проживають на вулиці Дерибасівська. 

```sql

SELECT first_name, last_name, address FROM employees WHERE address LIKE  '%Дерибасівська%';

```
**Бізнес-логіка:**
Запит може бути корисним для HR-відділу, коли потрібно швидко знайти співробітників, які проживають на конкретній вулиці або в певному районі для організації корпоративних заходів або для аналізу маршрутів транспортування.


**Результат:**

Отримано 1 запис співробітника, що проживає на вулиці Дерибасівська

**Скріншот:**
![enter image description here](https://snipboard.io/IX7tgz.jpg)

### 16.3. Знайти всі категорії, що починаються на "Телевізори".

```sql

SELECT category_name, description FROM categories WHERE category_name LIKE  'Телевізори%';

```
**Бізнес-логіка:**
Запит може використовуватись для швидкої ідентифікації та перегляду всіх категорій, що відносяться до групи "Телевізори та аудіо", навіть якщо назва категорії може змінюватися. Це допомагає менеджерам з контенту підтримувати порядок у каталозі товарів.


**Результат:**

Отримано 1 запис категорії, що починаються на "Телевізори"
  

**Скріншот:**
![enter image description here](https://snipboard.io/ac9zXi.jpg)

---

### 17. Знайти товари дорожчі за 15000 грн і дешевші за 50000 грн.
```sql

SELECT product_name, unit_price

FROM products

WHERE unit_price >  15000  AND unit_price <  50000;

```

**Результат:**

Отримано 16 записів товарів в діапазоні від 15000 грн до 50000 грн.
  

**Скріншот:**
![enter image description here](https://snipboard.io/NGRxwS.jpg)

### 18. Вивести клієнтів з Києва або Львова, які є компаніями.
```sql

SELECT contact_name, company_name, city, customer_type

FROM customers

WHERE  (city =  'Київ'  OR city =  'Львів')  AND customer_type =  'company';

```

**Результат:**

Отримано 3 записи клієнтів з Києва або Львова, які є компаніями.
  

**Скріншот:**
![enter image description here](https://snipboard.io/MCLQXJ.jpg)

### 19. Створити 4 власні запити з комбінаціями логічних операторів для різних таблиць.
### 19.1 Знайти співробітників, які не є менеджерами, але отримують більше 25000 грн.
```sql

SELECT first_name, last_name, title, salary

FROM employees

WHERE  NOT title LIKE  '%Менеджер%'  AND salary >  25000;
```
**Бізнес-логіка:**
Допомагає HR-менеджеру виявити високооплачуваних співробітників, які не займають керівних посад, для можливого перегляду їхніх обов'язків або підвищення.

**Результат:**

Отримано 2 записи співробітників, які не є менеджерами, але отримують більше 25000 грн.
  

**Скріншот:**
![enter image description here](https://snipboard.io/GjH496.jpg)

### 19.2 Знайти замовлення Новою Поштою або Делівері у травні-червні 2024.
```sql

SELECT order_id, ship_via, order_date

FROM orders

WHERE  (ship_via =  'Нова Пошта'  OR ship_via =  'Делівері')

AND  (order_date BETWEEN  '2024-05-01'  AND  '2024-06-30');
```
**Бізнес-логіка:**
Дозволяє керівнику відділу логістики оцінити ефективність роботи конкретних перевізників у певні місяці.

**Результат:**

Отримано 5 записів замовлень Новою Поштою або Делівері у травні-червні 2024
  

**Скріншот:**
![enter image description here](https://snipboard.io/Vzc1sd.jpg)

### 19.3 Знайти товари, які потребують поповнення або належать до ігрових консолей.
```sql

SELECT p.product_name, p.units_in_stock, c.category_name

FROM products p

JOIN categories c ON p.category_id = c.category_id

WHERE p.units_in_stock <  10  OR c.category_name =  'Ігрові консолі та ігри';
```
**Бізнес-логіка:**
Дозволяє швидко ідентифікувати товари, які потребують поповнення, або ті, що належать до пріоритетної категорії, щоб забезпечити їх постійну наявність.

**Результат:**

Отримано 10 записів товарів, які потребують поповнення або належать до ігрових консолей.
  

**Скріншот:**
![enter image description here](https://snipboard.io/jlznDs.jpg)

### 19.4 Відстежити поточні регіональні замовлення.
```sql

SELECT order_id, ship_city, order_status

FROM orders

WHERE order_status !=  'delivered'  AND  NOT ship_city =  'Київ';
```
**Бізнес-логіка:**
Допомагає відділу логістики відстежувати поточні замовлення, які потребують доставки в регіони, відмінні від столиці, що може вимагати особливої уваги до термінів або вартості доставки.

**Результат:**

Отримано 2 записи поточних регіональних замовлень.
  

**Скріншот:**
![enter image description here](https://snipboard.io/TlM5Xn.jpg)

### 20. Вивести клієнтів з міст Київ, Харків, Одеса, Дніпро.
```sql

SELECT contact_name, city

FROM customers

WHERE city IN  ('Київ',  'Харків',  'Одеса',  'Дніпро');

```

**Результат:**

Отримано 12 записів клієнтів з міст Київ, Харків, Одеса, Дніпро.
  

**Скріншот:**
![enter image description here](https://snipboard.io/7kTGrn.jpg)

### 21. Знайти товари в ціновому діапазоні від 10000 до 30000 грн.
```sql

SELECT product_name, unit_price

FROM products

WHERE unit_price BETWEEN  10000  AND  30000;

```

**Результат:**

Отримано 13 записів товарів в ціновому діапазоні від 10000 до 30000 грн.
  

**Скріншот:**
![enter image description here](https://snipboard.io/9jq7vN.jpg)

### 22. Придумати та виконати по 2 запити для кожного оператора (IN, BETWEEN, IS NULL/IS NOT NULL).
### 22.1 Знайти замовлення, які обробляли співробітники з ID 2, 5 або 6.
```sql

SELECT product_name, unit_price

FROM products

WHERE unit_price BETWEEN  10000  AND  30000;

```
**Бізнес-логіка:**
Використовується для аналізу продуктивності конкретних менеджерів, дозволяє швидко отримати інформацію про всі замовлення, які вони обробили.

**Результат:**

Отримано 27 записів замовлень, які обробляли співробітники з ID 2, 5 або 6.
  

**Скріншот:**
![enter image description here](https://snipboard.io/gzkD6W.jpg)

### 22.2 Знайти постачальників, які розташовані у Львівській, Харківській або Одеській областях.
```sql

SELECT company_name, city, r.region_name

FROM suppliers s

JOIN regions r ON s.region_id = r.region_id

WHERE r.region_name IN  ('Львівська область',  'Харківська область',  'Одеська область');

```
**Бізнес-логіка:**
Корисно для відділу закупівель, щоб швидко ідентифікувати партнерів у ключових регіонах України для оптимізації логістичних маршрутів.

**Результат:**

Отримано 4 записи постачальників, які розташовані у Львівській, Харківській або Одеській областях.
  

**Скріншот:**
![enter image description here](https://snipboard.io/mLPj1Z.jpg)

### 22.3 Знайти співробітників, народжених між 1980 і 1990 роками.
```sql

SELECT first_name, last_name, birth_date

FROM employees

WHERE birth_date BETWEEN  '1980-01-01'  AND  '1990-12-31';

```
**Бізнес-логіка:**
Запит використовується HR-відділом для аналізу вікового складу команди, що може бути важливим для планування програм навчання та розвитку.

**Результат:**

Отримано 5 записів співробітників, народжених між 1980 і 1990 роками.
  

**Скріншот:**
![enter image description here](https://snipboard.io/Zykriq.jpg)

### 22.4 Знайти замовлення з ціною доставки у діапазоні від 100 до 200 грн.
```sql

SELECT order_id, freight

FROM orders

WHERE freight BETWEEN  100  AND  200;

```
**Бізнес-логіка:**
Застосовується для аналізу вартості доставки, дозволяючи логістичному відділу визначити середні витрати на пересилання товарів або виявити аномально високі/низькі тарифи.

**Результат:**

Отримано 15 записів замовлень з ціною доставки у діапазоні від 100 до 200 грн.
  

**Скріншот:**
![enter image description here](https://snipboard.io/WDKgqn.jpg)


### 22.5 Знайти співробітників, які не мають прямого керівника.
```sql

SELECT first_name, last_name, title

FROM employees

WHERE reports_to IS  NULL;

```
**Бізнес-логіка:**
Запит дозволяє виявити керівних працівників.

**Результат:**

Отримано 1 запис співробітника з посадою "Генеральний директор".
  

**Скріншот:**
![enter image description here](https://snipboard.io/DUwFSA.jpg)

### 22.6 Знайти замовлення, які ще не були відправлені.
```sql

SELECT order_id, order_status, required_date

FROM orders

WHERE shipped_date IS  NULL;

```
**Бізнес-логіка:**
Запит дозволяє швидко відстежити всі замовлення, які знаходяться в обробці та очікують відправки.

**Результат:**

Отримано 4 записи замовлень, які ще не були відправлені.
  

**Скріншот:**
![enter image description here](https://snipboard.io/pUZ1MQ.jpg)

### 23. Створити 5 складних запитів, які поєднують різні типи умов (LIKE + AND/OR, BETWEEN + IN, тощо)
### 23.1 Знайти конкретних корпоративних клієнтів для маркетингової кампанії.
```sql

SELECT contact_name, company_name, city

FROM customers

WHERE customer_type =  'company'  AND  (city =  'Київ'  OR city =  'Харків')  AND contact_name LIKE  'Коваленко%';

```
**Бізнес-логіка:**
Знайти клієнтів-компаній з Києва або Харкова, чиї контактні імена починаються на 'Коваленко'.

**Результат:**

Отримано 1 запис корпоративних клієнтів для маркетингової кампанії.
  

**Скріншот:**
![enter image description here](https://snipboard.io/VsuHtK.jpg)

### 23.2 Вивести товари, які не є смартфонами та знаходяться на складі в кількості від 5 до 15 одиниць.
```sql

SELECT p.product_name, p.units_in_stock, c.category_name

FROM products p

JOIN categories c ON p.category_id = c.category_id

WHERE c.category_name !=  'Смартфони та телефони'  AND p.units_in_stock BETWEEN  5  AND  15;

```
**Бізнес-логіка:**
Запит для менеджера зі складу, щоб перевірити наявність певних товарів (крім смартфонів) і планувати поповнення, уникаючи надмірних запасів.

**Результат:**

Отримано 14 записів товарів, які не є смартфонами та знаходяться на складі в кількості від 5 до 15 одиниць.
  

**Скріншот:**
![enter image description here](https://snipboard.io/PAYhs1.jpg)

### 23.3 Знайти співробітників, чиї прізвища починаються на 'С' або 'П' і які були прийняті на роботу після 2021 року.
```sql

SELECT first_name, last_name, hire_date

FROM employees

WHERE  (last_name LIKE  'С%'  OR last_name LIKE  'П%')  AND hire_date >  '2021-12-31';
```
**Бізнес-логіка:**
Допомагає HR-менеджеру швидко знайти "нових" співробітників із певними прізвищами для внутрішніх звітів або вітальних листів.

**Результат:**

Отримано 1 запис співробітника, чиє прізвище починається на 'С' або 'П' і яка була прийнята на роботу після 2021 року
  

**Скріншот:**
![enter image description here](https://snipboard.io/k24nlT.jpg)

### 23.4 Знайти замовлення, які мають статус 'delivered', були відправлені через 'Нову Пошту' та містять товар з назвою, що містить 'MacBook'.
```sql

SELECT o.order_id, o.order_date, p.product_name

FROM orders o

JOIN order_items oi ON o.order_id = oi.order_id

JOIN products p ON oi.product_id = p.product_id

WHERE o.order_status =  'delivered'

AND o.ship_via =  'Нова Пошта'

AND p.product_name LIKE  '%MacBook%';

```
**Бізнес-логіка:**
Використовується для глибокого аналізу продажів. Дозволяє виявити конкретні успішні транзакції для популярних товарів і аналізувати ефективність обраного логістичного партнера.

**Результат:**

Отримано 0 записів.
  

**Скріншот:**
![enter image description here](https://snipboard.io/dFC5E1.jpg)

### 23.5 Знайти замовлення, які були оформлені клієнтами-фізичними особами з міст, що не входять до списку (Київ, Харків, Львів) і ціна доставки яких більша за 150 грн.
```sql

SELECT o.order_id, c.contact_name, c.city, o.freight

FROM orders o

JOIN customers c ON o.customer_id = c.customer_id

WHERE c.customer_type =  'individual'

AND c.city NOT  IN  ('Київ',  'Харків',  'Львів')

AND o.freight >  150;

```
**Бізнес-логіка:**
Запит для аналізу клієнтів з регіонів, що не є великими міськими центрами, та витрат на доставку. Допомагає виявити додаткові витрати, пов'язані з доставкою у віддаленіші райони.

**Результат:**

Отримано 2 записи замовлень, які були оформлені клієнтами-фізичними особами з міст, що не входять до списку (Київ, Харків, Львів) і ціна доставки яких більша за 150 грн.
  

**Скріншот:**
![enter image description here](https://snipboard.io/O1Wzap.jpg)

### 24. Створити 5 складних запитів, які поєднують різні типи умов (LIKE + AND/OR, BETWEEN + IN, тощо)
### 24.1 Відсортувати товари спочатку за категорією (за зростанням), а потім за ціною (за спаданням).
```sql

SELECT product_name, c.category_name, unit_price

FROM products p

JOIN categories c ON p.category_id = c.category_id

ORDER BY c.category_name ASC, p.unit_price DESC;

```
**Бізнес-логіка:**
Корисно для формування каталогу товарів на сайті або в друкованому прайсі, де спочатку групуються товари за категоріями, а потім у кожній категорії вони сортуються від найдорожчого до найдешевшого.

**Результат:**

Отримано 25 записів відсортованих товарів спочатку за категорією, а потім за ціною.
  

**Скріншот:**
![enter image description here](https://snipboard.io/InhkJO.jpg)

### 24.2 Відсортувати клієнтів спочатку за типом (компанія/фізична особа), а потім за датою реєстрації (від найновіших).
```sql

SELECT contact_name, company_name, customer_type, registration_date

FROM customers

ORDER BY customer_type ASC, registration_date DESC;

```
**Бізнес-логіка:**
Дозволяє маркетинговому відділу швидко розділити клієнтів на групи для різних розсилок і бачити найновіших клієнтів у кожній групі.

**Результат:**

Отримано 15 записів клієнтів спочатку за типом (компанія/фізична особа), а потім за датою реєстрації (від найновіших).
  

**Скріншот:**
![enter image description here](https://snipboard.io/n6Xl7U.jpg)

### 24.3 Відсортувати співробітників за містом (за зростанням) та прізвищем (за зростанням).
```sql

SELECT first_name, last_name, city

FROM employees

ORDER BY city ASC, last_name ASC;

```
**Бізнес-логіка:**
Корисно для складання внутрішнього довідника компанії, де співробітники групуються за місцем роботи, а потім сортуються за прізвищами для легшого пошуку.

**Результат:**

Отримано 8 записів відсортованих співробітників за містом (за зростанням) та прізвищем (за зростанням).
  

**Скріншот:**
![enter image description here](https://snipboard.io/v8Mbcp.jpg)

### 24.4 Отримати другу сторінку з 10 товарів.
```sql

SELECT product_name, unit_price

FROM products

ORDER BY product_name

LIMIT  10  OFFSET  10;

```
**Бізнес-логіка:**
Запит використовується в системах електронної комерції для реалізації пагінації в каталозі товарів, що дозволяє завантажувати дані частинами, оптимізуючи продуктивність сайту.

**Результат:**

Отримано 10 записів другої сторінки товарів.
  

**Скріншот:**
![enter image description here](https://snipboard.io/ESgVfH.jpg)

### 24.5 Отримати третю сторінку з 5 замовлень
```sql

SELECT order_id, order_date, order_status

FROM orders

ORDER BY order_date DESC

LIMIT  5  OFFSET  10;

```
**Бізнес-логіка:**
Використовується в адміністративній панелі для перегляду списку замовлень, дозволяючи менеджерам переходити між сторінками з даними, не завантажуючи весь список одночасно.

**Результат:**

Отримано 5 записів третьої сторінки з 5 замовлень.
  

**Скріншот:**
![enter image description here](https://snipboard.io/2smxqw.jpg)

---

### 25. Знайти товари, в назві яких є "Samsung" або "Apple", але немає слова "чохол".
```sql

SELECT product_name, unit_price

FROM products

WHERE (product_name ILIKE  '%Samsung%'  OR product_name ILIKE  '%Apple%')

AND product_name NOT  ILIKE  '%чохол%';

```

**Результат:**

Отримано 5 записів товарів Samsung або Apple, які не є чохлами.
  

**Скріншот:**
![enter image description here](https://snipboard.io/9qTKIR.jpg)

---

### 26. Створити 4 власні складні запити з комбінаціями LIKE та логічних операторів.
### 26.1 Знайти клієнтів з великих міст, чиє ім'я починається на "І".
```sql

SELECT contact_name, city

FROM customers

WHERE city IN  ('Київ',  'Харків',  'Львів')

AND contact_name LIKE  'І%';

```
**Бізнес-логіка:**
Допомагає відділу продажів ідентифікувати потенційних клієнтів з конкретних регіонів. Наприклад, ми шукаємо всіх клієнтів з Києва, Харкова чи Львова, чиє ім'я починається з "І". Це може бути корисним для таргетування рекламних кампаній або для планування зустрічей з ключовими клієнтами у цих містах.

**Результат:**

Отримано 1 запис клієнта з великого міста, чиє ім'я починається на "І".
  

**Скріншот:**
![enter image description here](https://snipboard.io/hInYBe.jpg)

### 26.2 Знайти товари, які не є преміум-моделями.
```sql

SELECT product_name, unit_price

FROM products

WHERE product_name NOT  LIKE  '%Pro%'  
AND product_name NOT  LIKE  '%Ultra%';

```
**Бізнес-логіка:**
Запит корисний для відділу маркетингу або закупівель. Він дозволяє швидко знайти всі товари, які не належать до преміум-лінійки (часто позначаються "Pro" або "Ultra") і можуть бути використані для акцій або розпродажу.

**Результат:**

Отримано 23 записи товарів, які не є преміум-моделями.
  

**Скріншот:**
![enter image description here](https://snipboard.io/oC546d.jpg)

### 26.3 Знайти співробітників з Києва або Львова, чиє прізвище починається на 'М'.
```sql

SELECT first_name, last_name, city

FROM employees

WHERE  (city =  'Київ'  OR city =  'Львів')

AND last_name LIKE  'М%';

```
**Бізнес-логіка:**
HR-відділ може використовувати цей запит для формування списків співробітників, які проживають у великих містах і мають певні прізвища. Це може бути частиною аналізу кадрового резерву або підготовки до внутрішніх корпоративних заходів.

**Результат:**

Отримано 1 запис співробітника з Києва або Львова, чиє прізвище починається на 'М'.

**Скріншот:**
![enter image description here](https://snipboard.io/xA6roQ.jpg)

### 26.4 Знайти контактні особи постачальників, які є Олександром або Іриною та мають вказану електронну пошту.
```sql

SELECT contact_name, company_name, email

FROM suppliers

WHERE  (contact_name LIKE  'Олександр%'  OR contact_name LIKE  'Ірина%')

AND email IS  NOT  NULL;

```
**Бізнес-логіка:**
Запит допомагає відділу закупівель швидко ідентифікувати ключових контактних осіб у постачальників для прямого зв'язку. Шукаємо конкретних осіб, перевіряючи, чи є у них email для подальшої комунікації.

**Результат:**

Отримано 0 записів.
  

**Скріншот:**
![enter image description here](https://snipboard.io/1rpwcK.jpg)

--- 

### 27. Знайти товари дорожчі 20000 грн (категорії 1 або 2) АБО товари дешевші 5000 грн будь-якої категорії.
```sql

SELECT product_name, unit_price

FROM products

WHERE unit_price BETWEEN  10000  AND  30000;

```

**Результат:**

Отримано 12 записів товарів які дорожчі 20000 грн (категорії 1 або 2) АБО товари дешевші 5000 грн будь-якої категорії.


**Скріншот:**
![enter image description here](https://snipboard.io/lYUabi.jpg)

--- 

### 28. Написати 3 запити з складними вкладеними умовами, використовуючи дужки для групування логіки.
### 28.1 Пошук товарів для акції "Літній розпродаж".
```sql

SELECT product_name, unit_price, c.category_name

FROM products p

JOIN categories c ON p.category_id = c.category_id

WHERE  (c.category_name IN  ('Телефони',  'Ноутбуки')  AND p.unit_price BETWEEN  10000  AND  30000);

```
**Бізнес-логіка:**
Запит допомагає відділу маркетингу виявити товари, які відповідають критеріям для включення в акцію "Літній розпродаж". Нам потрібні товари, що належать до категорій "Телефони" або "Ноутбуки", і їхня ціна знаходиться в діапазоні від 10 000 до 30 000 гривень.

**Результат:**

Отримано 0 записів.


**Скріншот:**
![enter image description here](https://snipboard.io/vlYLtb.jpg)

### 28.2 Виявлення пріоритетних замовлень.
```sql

SELECT order_id, order_date, shipped_date, ship_via, freight

FROM orders

WHERE (ship_via =  'Нова Пошта'  AND freight >  200)

OR

(shipped_date IS  NULL  AND order_date <  '2024-06-15');

```
**Бізнес-логіка:**
Запит дозволяє відділу логістики швидко ідентифікувати замовлення, які потребують першочергової обробки. Пріоритет надається замовленням, що відповідають одній із двох умов: або вони відправлені "Новою Поштою" і мають високу вартість доставки (понад 200 грн), або вони ще не відправлені та були оформлені до 15.06.2024.

**Результат:**

Отримано 3 записи пріорітетних замовлень.


**Скріншот:**
![enter image description here](https://snipboard.io/bqkdtH.jpg)

### 28.3 Аналіз кадрового складу для HR.
```sql

SELECT first_name, last_name, birth_date, title

FROM employees

WHERE

(birth_date BETWEEN  '1990-01-01'  AND  '1999-12-31')

AND

(title LIKE  '%Менеджер з продажів%'  OR title LIKE  '%Старший розробник%');

```
**Бізнес-логіка:**
Допомагає виявити працівників, які народилися в 90-х роках (з 1990 по 1999) і мають одну з двох посад: "Менеджер з продажів" або "Старший розробник". Такі дані можуть бути використані для планування програм розвитку або формування команди для конкретних проєктів.

**Результат:**

Отримано 0 записів.


**Скріншот:**
![enter image description here](https://snipboard.io/vlYLtb.jpg)

---
  
## Висновки

**Самооцінка:** 4

**Обґрунтування:** Тому що не було зроблено всі завдання 3 рівня.