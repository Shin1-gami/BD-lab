# Лабораторна робота 2. Створення складних SQL запитів

  

## Загальна інформація

  

**Здобувач освіти:** [Величко Ростислав]

**Група:** [ІПЗ-32]

**Обраний рівень складності:** [3]

## Виконання завдань

### Рівень 1

#### 1. З'єднання таблиць

**Завдання 1.1:** INNER JOIN - список товарів з категоріями та постачальниками.

```sql
SELECT p.product_name, c.category_name, s.company_name, p.unit_price
FROM products p
INNER JOIN categories c ON p.category_id = c.category_id
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
ORDER BY c.category_name, p.product_name;
```

**Результат виконання:**

<a href="https://ibb.co/wNDDYHhc"><img src="https://i.ibb.co/1fHHbVGz/scr1.png" alt="scr1" border="0"></a>

**Пояснення:** Запит виконує вибірку даних про товари разом із назвами категорій і постачальників. З'єднуються таблиці product, category, company, unit_price.

**Завдання 1.2:** LEFT JOIN - клієнти з кількістю замовлень
```sql
SELECT c.contact_name, c.customer_type, r.region_name,
COUNT(o.order_id)  as order_count
FROM customers c
LEFT  JOIN orders o ON c.customer_id = o.customer_id
LEFT  JOIN regions r ON c.region_id = r.region_id
GROUP BY c.customer_id, c.contact_name, c.customer_type, r.region_name
ORDER BY order_count DESC;
```

**Результат виконання:**

<a href="https://imgbb.com/"><img src="https://i.ibb.co/Ld8tdNC8/scr2.png" alt="scr2" border="0"></a>

**Пояснення:** LEFT JOIN — якщо хочемо побачити всіх клієнтів, навіть тих, у кого немає замовлень.
INNER JOIN — якщо потрібно показати лише тих клієнтів, що мають записи у зв’язаних таблицях.

**Завдання 1.3:** Множинне з'єднання - детальна інформація про замовлення

```sql
SELECT
o.order_id,
o.order_date,
cu.customer_id,
cu.contact_name AS customer_name,
p.product_id,
p.product_name,
oi.quantity,
oi.unit_price AS item_unit_price,
(oi.quantity * oi.unit_price *  (1  - COALESCE(oi.discount,  0)))  AS item_total
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
JOIN customers cu ON o.customer_id = cu.customer_id
WHERE o.order_date >=  '2024-01-01'
ORDER BY o.order_date DESC, o.order_id;
```

**Результат виконання:**

<a href="https://ibb.co/rKdZV2K1"><img src="https://i.ibb.co/FkHBF4kj/scr3.png" alt="scr3" border="0"></a>

**Аналіз складності:** Запит об’єднує 4 таблиці (orders, order_items, products, customers) для показу деталей замовлень після 01.01.2024.
Послідовність JOIN: orders → order_items → products → customers.
Складність — середня, навантаження дають JOIN і ORDER BY.

#### 2. Агрегатні функції

**Завдання 2.1:** Статистика товарів за категоріями

```sql
SELECT c.category_name,
COUNT(p.product_id)  as product_count,
AVG(p.unit_price)  as avg_price,
MIN(p.unit_price)  as min_price,
MAX(p.unit_price)  as max_price
FROM categories c
LEFT  JOIN products p ON c.category_id = p.category_id
GROUP BY c.category_id, c.category_name
ORDER BY product_count DESC;
```
**Результат виконання:**

<a href="https://ibb.co/fG9gQS7K"><img src="https://i.ibb.co/rf3jvtJL/scr4.png" alt="scr4" border="0"></a>

**Завдання 2.2:** Продажі за регіонами з використанням HAVING

```sql
SELECT
r.region_id,
r.region_name,
SUM(oi.quantity * oi.unit_price *  (1  - COALESCE(oi.discount,0)))  AS total_revenue,
COUNT(DISTINCT o.order_id)  AS orders_count
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
JOIN customers cu ON o.customer_id = cu.customer_id
LEFT  JOIN regions r ON cu.region_id = r.region_id
WHERE o.order_status =  'delivered'
GROUP BY r.region_id, r.region_name
HAVING SUM(oi.quantity * oi.unit_price *  (1  - COALESCE(oi.discount,0)))  >  0
ORDER BY total_revenue DESC;
```

**Результат виконання:**

<a href="https://imgbb.com/"><img src="https://i.ibb.co/s90GNcMm/scr5.png" alt="scr5" border="0"></a>

**Завдання 2.3:** Постачальники з кількістю товарів більше 2

```sql
SELECT
s.supplier_id,
s.company_name,
COUNT(p.product_id)  AS product_count
FROM suppliers s
LEFT  JOIN products p ON p.supplier_id = s.supplier_id
GROUP BY s.supplier_id, s.company_name
HAVING COUNT(p.product_id)  >  2
ORDER BY product_count DESC;
```

**Результат виконання:**

<a href="https://imgbb.com/"><img src="https://i.ibb.co/Q3yKxF7J/scr6.png" alt="scr6" border="0"></a>

#### 3. Базові підзапити

**Завдання 3.1:** Товари з ціною вище середньої по категорії

  

```sql
SELECT p.product_name, p.unit_price, c.category_name
FROM products p
INNER  JOIN categories c ON p.category_id = c.category_id
WHERE p.unit_price >  (
SELECT AVG(p2.unit_price)
FROM products p2
WHERE p2.category_id = p.category_id
)
ORDER BY c.category_name, p.unit_price DESC;```
```

**Результат виконання:**

<a href="https://imgbb.com/"><img src="https://i.ibb.co/60ZBftht/scr7.png" alt="scr7" border="0"></a>

**Завдання 3.2:** Клієнти з замовленнями у 2024 році

```sql
SELECT  DISTINCT c.customer_id, c.contact_name, c.customer_type
FROM customers c
WHERE c.customer_id IN  (
SELECT o.customer_id
FROM orders o
WHERE o.order_date >=  '2024-01-01'  AND o.order_date <  '2025-01-01'
);
```
**Результат виконання:**

<a href="https://imgbb.com/"><img src="https://i.ibb.co/Kj3g40cR/scr8.png" alt="scr8" border="0"></a>

**Завдання 3.3:** Товари з загальною кількістю продажів

  

```sql
SELECT
p.product_id,
p.product_name,
p.unit_price,
COALESCE((
SELECT SUM(oi.quantity)
FROM order_items oi
WHERE oi.product_id = p.product_id
),  0)  AS total_quantity_sold,
COALESCE((
SELECT SUM(oi.quantity * oi.unit_price *  (1  - COALESCE(oi.discount,0)))
FROM order_items oi
JOIN orders o ON oi.order_id = o.order_id
WHERE oi.product_id = p.product_id
AND o.order_status =  'delivered'
),  0)  AS total_revenue
FROM products p
ORDER BY total_quantity_sold DESC NULLS LAST;
```

**Результат виконання:**

<a href="https://ibb.co/sps2hvQZ"><img src="https://i.ibb.co/ymgXDn5r/scr9.png" alt="scr9" border="0"></a>

### Рівень 2

  

#### 4. Складні з'єднання

**Завдання 4.1:** RIGHT JOIN - аналіз категорій та товарів

```sql
SELECT c.category_name,
COUNT(p.product_id)  as products_count,
COALESCE(AVG(p.unit_price),  0)  as avg_price
FROM products p
RIGHT  JOIN categories c ON p.category_id = c.category_id
GROUP BY c.category_id, c.category_name
ORDER BY products_count DESC;
```

**Результат виконання:**

<a href="https://imgbb.com/"><img src="https://i.ibb.co/kgVhRcL9/scr10.png" alt="scr10" border="0"></a>

**Завдання 4.2:** Self-join - співробітники та керівники

```sql
SELECT e1.first_name ||  ' '  || e1.last_name as employee,
e1.title as employee_title,
e2.first_name ||  ' '  || e2.last_name as manager,
e2.title as manager_title
FROM employees e1
LEFT  JOIN employees e2 ON e1.reports_to = e2.employee_id
ORDER BY e2.last_name, e1.last_name;
```

**Результат виконання:**

<a href="https://imgbb.com/"><img src="https://i.ibb.co/cczGjYgr/scr11.png" alt="scr11" border="0"></a>

#### 5. Віконні функції

**Завдання 5.1:** Ранжування товарів за ціною в категоріях

```sql
SELECT p.product_name,
c.category_name,
p.unit_price,
RANK() OVER (PARTITION BY c.category_name ORDER BY p.unit_price DESC)  as price_rank,
DENSE_RANK() OVER (PARTITION BY c.category_name ORDER BY p.unit_price DESC)  as price_dense_rank,
ROW_NUMBER() OVER (PARTITION BY c.category_name ORDER BY p.unit_price DESC)  as row_num
FROM products p
JOIN categories c ON p.category_id = c.category_id
ORDER BY c.category_name, p.unit_price DESC;
```

**Результат виконання:**

<a href="https://ibb.co/8gxdWg9Y"><img src="https://i.ibb.co/nM1nHMjP/scr12.png" alt="scr12" border="0"></a>

**Завдання 5.2:** Порівняння замовлень з попередніми датами

```sql
SELECT
c.customer_id,
c.contact_name AS customer_name,
o.order_id,
o.order_date,
LAG(o.order_date) OVER (PARTITION BY c.customer_id ORDER BY o.order_date)  AS previous_order_date,
LEAD(o.order_date) OVER (PARTITION BY c.customer_id ORDER BY o.order_date)  AS next_order_date,
(o.order_date - LAG(o.order_date) OVER (PARTITION BY c.customer_id ORDER BY o.order_date))  AS days_since_previous
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
ORDER BY c.customer_id, o.order_date;
```

**Результат виконання:**

<a href="https://ibb.co/cSJMVC0f"><img src="https://i.ibb.co/Zpdt7Y54/scr13.png" alt="scr13" border="0"></a>

### Рівень 3

#### 6. Матеріалізовані представлення та рекурсивні запити

**Завдання 6.1:** Матеріалізоване представлення для аналізу продажів

```sql
DROP MATERIALIZED VIEW mv_monthly_sales;
CREATE MATERIALIZED VIEW mv_monthly_sales AS
SELECT
EXTRACT(YEAR FROM o.order_date)  AS year,
EXTRACT(MONTH FROM o.order_date)  AS month,
c.category_name,
r.region_name,
SUM(oi.quantity * oi.unit_price *  (1  - oi.discount))  AS total_revenue,
COUNT(DISTINCT o.order_id)  AS orders_count,
AVG(oi.quantity * oi.unit_price *  (1  - oi.discount))  AS avg_order_value
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
JOIN categories c ON p.category_id = c.category_id
JOIN customers cu ON o.customer_id = cu.customer_id
LEFT  JOIN regions r ON cu.region_id = r.region_id
WHERE o.order_status =  'delivered'
GROUP BY year, month, c.category_name, r.region_name;
CREATE INDEX idx_mv_monthly_sales_date ON mv_monthly_sales(year, month);
```

**Пояснення:** Матеріалізовані представлення зберігають результат складного запиту як таблицю, що дозволяє:
1.Прискорити виконання аналітичних запитів;
2.Зменшити навантаження на сервер;
3.Створювати індекси для швидшого доступу;
4.Зручно аналізувати великі обсяги даних без повторних обчислень.

**Завдання 6.2:** Рекурсивний запит для ієрархії співробітників

```sql
WITH RECURSIVE employee_hierarchy AS  (
-- Базовий випадок: без керівника
SELECT employee_id, first_name, last_name, title, reports_to,
0  as level,
CAST(last_name ||  ' '  || first_name as VARCHAR(1000))  as hierarchy_path
FROM employees
WHERE reports_to IS  NULL
UNION  ALL
-- Рекурсивний випадок: підлеглі
SELECT e.employee_id, e.first_name, e.last_name, e.title, e.reports_to,
eh.level +  1,
CAST(eh.hierarchy_path ||  ' -> '  || e.last_name ||  ' '  || e.first_name as VARCHAR(1000))
FROM employees e
JOIN employee_hierarchy eh ON e.reports_to = eh.employee_id
)
SELECT  *  FROM employee_hierarchy
ORDER BY hierarchy_path;
```

**Результат виконання:**

<a href="https://ibb.co/xKM4Rrpb"><img src="https://i.ibb.co/8njhSQWw/scr14.png" alt="scr14" border="0"></a>

## Аналіз продуктивності

  

### Дослідження планів виконання

**Найповільніший запит:**

```sql
SELECT
o.order_id,
o.order_date,
cu.contact_name,
p.product_name,
s.company_name
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
JOIN suppliers s ON p.supplier_id = s.supplier_id
JOIN customers cu ON o.customer_id = cu.customer_id
WHERE o.order_status =  'delivered'
ORDER BY o.order_date DESC;
```

**План виконання (EXPLAIN ANALYZE):**

```
| QUERY PLAN                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sort  (cost=6.14..6.15 rows=2 width=562) (actual time=0.317..0.321 rows=39 loops=1)                                                                     |
|   Sort Key: o.order_date DESC                                                                                                                           |
|   Sort Method: quicksort  Memory: 31kB                                                                                                                  |
|   ->  Nested Loop  (cost=2.91..6.13 rows=2 width=562) (actual time=0.153..0.279 rows=39 loops=1)                                                        |
|         ->  Nested Loop  (cost=2.77..4.74 rows=2 width=348) (actual time=0.141..0.212 rows=39 loops=1)                                                  |
|               ->  Hash Join  (cost=2.63..4.29 rows=2 width=130) (actual time=0.101..0.121 rows=39 loops=1)                                              |
|                     Hash Cond: (oi.order_id = o.order_id)                                                                                               |
|                     ->  Seq Scan on order_items oi  (cost=0.00..1.47 rows=47 width=8) (actual time=0.013..0.017 rows=47 loops=1)                        |
|                     ->  Hash  (cost=2.62..2.62 rows=1 width=126) (actual time=0.075..0.076 rows=26 loops=1)                                             |
|                           Buckets: 1024  Batches: 1  Memory Usage: 11kB                                                                                 |
|                           ->  Hash Join  (cost=1.40..2.62 rows=1 width=126) (actual time=0.059..0.068 rows=26 loops=1)                                  |
|                                 Hash Cond: (cu.customer_id = o.customer_id)                                                                             |
|                                 ->  Seq Scan on customers cu  (cost=0.00..1.15 rows=15 width=122) (actual time=0.010..0.011 rows=15 loops=1)            |
|                                 ->  Hash  (cost=1.39..1.39 rows=1 width=12) (actual time=0.029..0.030 rows=26 loops=1)                                  |
|                                       Buckets: 1024  Batches: 1  Memory Usage: 10kB                                                                     |
|                                       ->  Seq Scan on orders o  (cost=0.00..1.39 rows=1 width=12) (actual time=0.012..0.021 rows=26 loops=1)            |
|                                             Filter: ((order_status)::text = 'delivered'::text)                                                          |
|                                             Rows Removed by Filter: 5                                                                                   |
|               ->  Index Scan using idx_products_product_id on products p  (cost=0.14..0.23 rows=1 width=226) (actual time=0.001..0.001 rows=1 loops=39) |
|                     Index Cond: (product_id = oi.product_id)                                                                                            |
|         ->  Index Scan using suppliers_pkey on suppliers s  (cost=0.14..0.69 rows=1 width=222) (actual time=0.001..0.001 rows=1 loops=39)               |
|               Index Cond: (supplier_id = p.supplier_id)                                                                                                 |
| Planning Time: 1.679 ms                                                                                                                                 |
| Execution Time: 0.471 ms                                                                                                                                |
```

**Запропоновані оптимізації:**

1. Додати комбінований індекс для швидкої фільтрації й сортування, що прискорить фільтрацію по статусу і сортування по даті одночасно

2. Додати індекс на зовнішні ключі, що часто використовуються у з’єднаннях. Це зменшить вартість операцій JOIN

3. Використовувати матеріалізовані представленя для частих звітів про доставлені замовлення

### Створені індекси

**Індекс 1:**

```sql
CREATE INDEX idx_orders_status_date ON orders(order_status, order_date DESC);
```

**Обґрунтування:** Фільтрація за статусом і сортування по даті це головна причина уповільнення. Комбінований індекс дозволяє уникнути Seq Scan і швидко знаходити потрібні рядки в оптимальному порядку.

**Індекс 2:**

```sql
CREATE INDEX idx_order_items_order_id ON order_items(order_id);
```

**Обґрунтування:** З’єднання між orders і order_items відбувається по order_id. Індекс пришвидшує виконання JOIN і зменшує кількість звернень до диску.

## Порівняльний аналіз

### Ефективність різних підходів

**Завдання:** Знайти топ-5 найдорожчих товарів у кожній категорії

**Підхід 1: Віконні функції**

```sql
SELECT product_name, category_name, unit_price, price_rank
FROM (
    SELECT 
        p.product_name,
        c.category_name,
        p.unit_price,
        RANK() OVER (PARTITION BY c.category_name ORDER BY p.unit_price DESC) AS price_rank
    FROM products p
    JOIN categories c ON p.category_id = c.category_id
    WHERE p.unit_price IS NOT NULL
) ranked
WHERE price_rank <= 5;
```

**Підхід 2: Корельований підзапит**

```sql
SELECT p1.product_name, c.category_name, p1.unit_price
FROM products p1
JOIN categories c ON p1.category_id = c.category_id
WHERE (
    SELECT COUNT(*) 
    FROM products p2
    WHERE p2.category_id = p1.category_id 
      AND p2.unit_price > p1.unit_price
) < 5
ORDER BY c.category_name, p1.unit_price DESC;
```

**Час виконання:**

- Віконні функції: 0.318 ms

- Корельований підзапит: 0.443 ms

**Висновок:** Віконні функції працюють швидше, оскільки вони виконуються в один прохід по даних, без багаторазових вкладених підзапитів.
Корельовані підзапити неефективні на великих наборах даних, бо виконуються повторно для кожного рядка основної таблиці.

## Висновки

**Самооцінка**: 5

**Обгрунтування**: У ході роботи були виконані всі завдання, було створено та проаналізовано запити з використанням  JOIN, EXPLAIN ANALYZE, віконних функцій і корельованих підзапитів.