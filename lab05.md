  

# Звіт з лабораторної роботи №5
Дисципліна: Бази даних
Тема: Керування БД, оптимізація продуктивності та автоматизація
Студент: Величко Ростислав
Група: ІПЗ-32

---
## Мета роботи
Навчитися аналізувати та оптимізувати продуктивність баз даних через створення індексів та аналіз планів виконання запитів, опанувати механізми автоматизації за допомогою тригерів та представлення, освоїти базові операції адміністрування СУБД, включаючи керування правами доступу та резервне копіювання.
## Рівень 1: Базова оптимізація та безпека

### 1. Аналіз запитів

```sql
EXPLAIN ANALYZE
SELECT o.order_id, c.name, s.name, oi.quantity
FROM  "Order" o
JOIN Client c ON o.client_id = c.client_id
JOIN OrderItem oi ON o.order_id = oi.order_id
JOIN  Service s ON s.service_id = oi.service_id
WHERE o.status = 'Відкрите';
```
Результат:
<a href="https://ibb.co/WN58VzyM"><img src="https://i.ibb.co/GfpYHM28/lab5explain.png" alt="lab5explain" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a><br />

### 2. Створення індексів

```sql
CREATE  INDEX  idx_order_status  ON  "Order"(status);
CREATE  INDEX  idx_orderitem_service_id  ON OrderItem(service_id);
CREATE  INDEX  idx_order_date  ON  "Order"(date);
```
Результат:
<a href="https://ibb.co/zhddpsyL"><img src="https://i.ibb.co/jvttmhcx/lab5index.png" alt="lab5index" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
Аналіз після індексу:
<a href="https://ibb.co/LD61C1W2"><img src="https://i.ibb.co/20PdjdQf/lab5fterindex.png" alt="lab5fterindex" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a><br />

### 3. Створення представлень (VIEW)

```sql
CREATE  VIEW  open_orders_view  AS
SELECT o.order_id, c.name AS client, o.status, SUM(oi.quantity * s.price) AS total
FROM  "Order" o
JOIN Client c ON c.client_id = o.client_id
JOIN OrderItem oi ON oi.order_id = o.order_id
JOIN  Service s ON s.service_id = oi.service_id
WHERE o.status = 'Відкрите'
GROUP BY o.order_id, c.name, o.status;

CREATE  VIEW  employee_order_stats  AS
SELECT e.emp_id, e.name, COUNT(o.order_id) AS total_orders
FROM Employee e
LEFT JOIN  "Order" o ON o.emp_id = e.emp_id
GROUP BY e.emp_id;
```
Результат:
<a href="https://ibb.co/r2m4XRDP"><img src="https://i.ibb.co/7tX20dsc/lab5view.png" alt="lab5view" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://ibb.co/KcbKDQkP"><img src="https://i.ibb.co/DPzrY6yJ/lab5view2.png" alt="lab5view2" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>

### 4. Тригери для логування вставок

```sql
CREATE  TABLE  order_log (
log_id SERIAL  PRIMARY KEY,
order_id INT,
action  VARCHAR(10),
changed_at TIMESTAMP  DEFAULT  NOW()
);

CREATE OR REPLACE  FUNCTION  log_order_insert()
RETURNS TRIGGER AS $$
BEGIN
INSERT INTO order_log(order_id, action)
VALUES (NEW.order_id, 'INSERT');
RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE  TRIGGER  trg_order_insert
AFTER  INSERT  ON  "Order"
FOR EACH ROW
EXECUTE  FUNCTION log_order_insert();
```
Результат:
<a href="https://imgbb.com/"><img src="https://i.ibb.co/Nds67wFy/lab5triger1.png" alt="lab5triger1" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>

<a href="https://imgbb.com/"><img src="https://i.ibb.co/1fBGckyN/lab5trigger2.png" alt="lab5trigger2" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>

<a href="https://imgbb.com/"><img src="https://i.ibb.co/zVNXCkrw/lab5triger3.png" alt="lab5triger3" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
  

### 5. Створення користувача з обмеженими правами

```sql
CREATE  USER  viewer  WITH  PASSWORD  'view123';
GRANT  CONNECT  ON  DATABASE autoservice TO viewer;
GRANT USAGE ON  SCHEMA public TO viewer;
GRANT  SELECT  ON Client, Car, Service  TO viewer;
```
Результат:
<a href="https://imgbb.com/"><img src="https://i.ibb.co/HDRy1RgR/lab5createview.png" alt="lab5createview" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
  

## Рівень 2: Розширення логіки та контроль

### 6. Представлення з ON UPDATE правилом

```sql
CREATE  VIEW  client_car_view  AS
SELECT c.client_id, c.name, car.make, car.model
FROM Client c
JOIN Car car ON car.client_id = c.client_id;

CREATE  RULE  update_client_name  AS
ON UPDATE  TO client_car_view DO INSTEAD
UPDATE Client SET  name = NEW.name WHERE client_id = NEW.client_id;
```
Результат:
<a href="https://imgbb.com/"><img src="https://i.ibb.co/SDRtg8T4/level21.png" alt="level21" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://ibb.co/MDcgV4rJ"><img src="https://i.ibb.co/TB4w8S6N/level212rule.png" alt="level212rule" border="0"></a>

### 7. Тригер валідації імен

```sql
CREATE OR REPLACE  FUNCTION  validate_employee_name()
RETURNS TRIGGER AS $$
BEGIN
IF  LENGTH(NEW.name) < 3  THEN
RAISE EXCEPTION 'Name too short';
END  IF;
RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE  TRIGGER  trg_validate_name
BEFORE  INSERT  OR  UPDATE  ON Employee
FOR EACH ROW
EXECUTE  FUNCTION validate_employee_name();
```
Результат:
<a href="https://imgbb.com/"><img src="https://i.ibb.co/FbX6c22N/level22trigervalidation.png" alt="level22trigervalidation" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/F4VvFM87/level22trigervalidation2.png" alt="level22trigervalidation2" border="0"></a>
### 8. Повне логування змін

```sql
CREATE  TABLE  audit_log (
log_id SERIAL  PRIMARY KEY,
table_name TEXT,
operation TEXT,
record_id INT,
old_values JSONB,
new_values JSONB,
changed_at TIMESTAMP  DEFAULT  NOW(),
changed_by TEXT  DEFAULT CURRENT_USER
);

CREATE OR REPLACE  FUNCTION  log_changes()
RETURNS TRIGGER AS $$
BEGIN
IF TG_OP = 'UPDATE'  THEN
INSERT INTO audit_log(table_name, operation, record_id, old_values, new_values)
VALUES (TG_TABLE_NAME, 'UPDATE', NEW.order_id, row_to_json(OLD), row_to_json(NEW));
ELSIF TG_OP = 'DELETE'  THEN
INSERT INTO audit_log(table_name, operation, record_id, old_values)
VALUES (TG_TABLE_NAME, 'DELETE', OLD.order_id, row_to_json(OLD));
END  IF;
RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE  TRIGGER  trg_order_log_all
AFTER  UPDATE  OR  DELETE  ON  "Order"
FOR EACH ROW
EXECUTE  FUNCTION log_changes();
```
Результат:
<a href="https://imgbb.com/"><img src="https://i.ibb.co/bgkbQjQL/level23.png" alt="level23" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://ibb.co/V0cCzpSL"><img src="https://i.ibb.co/mrVy2FqR/level232.png" alt="level232" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/Wvx3L73q/level233.png" alt="level233" border="0"></a>
### 9. Часткові індекси

```sql
CREATE  INDEX  idx_order_open  ON  "Order"(status)
WHERE  status = 'Відкрите';

CREATE  INDEX  idx_recent_orders  ON  "Order"(date)
WHERE  date > CURRENT_DATE - INTERVAL '30 days';
```
Результат:
<a href="https://imgbb.com/"><img src="https://i.ibb.co/Q7vfjw1B/level241.png" alt="level241" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/bMC2y9Z3/level242.png" alt="level242" border="0"></a>
### 10. Резервне копіювання
У pgAdmin:
- ПКМ по базі - Backup - формат: Custom
Відновлення:
- Створити нову БД - Restore - обрати файл

## Рівень 3: Адміністрування, безпека, оптимізація

### 11. Матеріалізоване представлення
```sql
CREATE MATERIALIZED VIEW monthly_order_summary AS
SELECT DATE_TRUNC('month', date) AS  month, COUNT(*) AS total_orders
FROM  "Order"
GROUP BY DATE_TRUNC('month', date);

REFRESH MATERIALIZED VIEW monthly_order_summary;
```
Результат:
<a href="https://ibb.co/27FgFC7M"><img src="https://i.ibb.co/hRgDg4Rd/level26.png" alt="level26" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
Оновлення автоматично:

```sql
CREATE OR REPLACE  FUNCTION  refresh_mv()
RETURNS TRIGGER AS $$
BEGIN
REFRESH MATERIALIZED VIEW monthly_order_summary;
RETURN  NULL;
END;
$$ LANGUAGE plpgsql;

CREATE  TRIGGER  trg_refresh_mv
AFTER  INSERT  OR  UPDATE  OR  DELETE  ON  "Order"
FOR EACH STATEMENT
EXECUTE  FUNCTION refresh_mv();
```
<a href="https://imgbb.com/"><img src="https://i.ibb.co/bRytTSgh/level262.png" alt="level262" border="0"></a>
### 12. Каскадне видалення

```sql
CREATE OR REPLACE  FUNCTION  delete_order_items()
RETURNS TRIGGER AS $$ BEGIN
DELETE  FROM OrderItem WHERE order_id = OLD.order_id;
RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE  TRIGGER  trg_delete_order_items
BEFORE  DELETE  ON  "Order"
FOR EACH ROW
EXECUTE  FUNCTION delete_order_items();
```
Результат:
<a href="https://ibb.co/GvSY91B4"><img src="https://i.ibb.co/MD0wfjWx/level271.png" alt="level271" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/Rk4tDNHg/level272.png" alt="level272" border="0"></a>
### 13. Ієрархія ролей

```sql
CREATE  ROLE  readonly;
GRANT  SELECT  ON ALL TABLES IN  SCHEMA public TO  readonly;

CREATE  ROLE  readwrite;
GRANT  readonly  TO  readwrite;
GRANT  INSERT, UPDATE, DELETE  ON ALL TABLES IN  SCHEMA public TO  readwrite;

CREATE  ROLE  admin;
GRANT  readwrite  TO  admin;
GRANT ALL PRIVILEGES ON  DATABASE autoservice TO  admin;

CREATE  USER  manager  WITH  PASSWORD  'manager123';
GRANT  admin  TO manager;
```
Результат:
<a href="https://ibb.co/MWZ6vr8"><img src="https://i.ibb.co/H1BdS6N/level281.png" alt="level281" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://ibb.co/yBWfLG4c"><img src="https://i.ibb.co/qFkybXJ3/level282.png" alt="level282" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/SXkwkZHF/level283.png" alt="level283" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/ZRCBqcrQ/level284.png" alt="level284" border="0"></a>
### 14. Процедура обслуговування

```sql
CREATE  TABLE  maintenance_log (
log_id SERIAL  PRIMARY KEY,
operation TEXT,
executed_at TIMESTAMP  DEFAULT  NOW()
);

CREATE  OR  REPLACE  PROCEDURE maintain_db()
LANGUAGE plpgsql
AS $$
BEGIN
ANALYZE;
REINDEX DATABASE autoservice;
INSERT INTO maintenance_log(operation) VALUES ('Maintenance done');
END;
$$;

CALL maintain_db();
```
Результат:
<a href="https://imgbb.com/"><img src="https://i.ibb.co/rRpYX6W3/level291.png" alt="level291" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://ibb.co/27hXLtWc"><img src="https://i.ibb.co/jvf7xMb3/level292.png" alt="level292" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/dJ7vtbGQ/level293.png" alt="level293" border="0"></a>
### 15. Моніторинг

```sql
-- Найменш використовувані індекси
SELECT pg_class.relname, idx_scan, idx_tup_read
FROM pg_stat_user_indexes
JOIN pg_class ON pg_class.oid = pg_stat_user_indexes.indexrelid
WHERE idx_scan < 50;

-- Аналіз запиту вручну
EXPLAIN ANALYZE
SELECT * FROM  "Order"
WHERE  status = 'Відкрите'
ORDER BY  date  DESC;
```
Результат:
<a href="https://ibb.co/m57xSc1X"><img src="https://i.ibb.co/605dNWV1/level31.png" alt="level31" border="0"></a><br /><a target='_blank' href='https://uk.imgbb.com/'></a>
<a href="https://ibb.co/PsCRW8JZ"><img src="https://i.ibb.co/hx8kdvrR/level32.png" alt="level32" border="0"></a>

---

## Висновки
Під час виконання лабораторної роботи було реалізовано всі рівні лабораторної роботи, було набуто навички індексації, представлення, тригерів, прав доступу, логування та оптимізації. Було виявлено продуктивні вузькі місця та оптимізовано запити.