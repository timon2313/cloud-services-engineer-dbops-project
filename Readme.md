# Создание БД и пользователя

## Подключение к Postgres
```shell
psql -U user -h <host> -p 5432 -d postgres
```

## Создание новой БД
```sql
CREATE DATABASE store;
```

## Подключение к БД
```shell
\c store
```

## Создание пользователя
```sql
CREATE USER store_user WITH PASSWORD 'password';
```

## Доступ к БД
```sql
GRANT ALL PRIVILEGES ON DATABASE store TO store_user;
```

## Доступ к таблицам
```sql
GRANT USAGE, CREATE ON SCHEMA public TO store_user;
```

# Запрос на получение количества отправленных заказов за последние 7 дней посуточно.
```sql
SELECT o.date_created, SUM(op.quantity) 
FROM orders AS o
JOIN order_product AS op ON o.id = op.order_id
WHERE o.status = 'shipped' AND o.date_created > now() - INTERVAL '7 DAY'
GROUP BY o.date_created; 
``
