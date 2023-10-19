##Задание 1

```
SELECT c.customer_id, c.first_name, COUNT(*) AS quantity FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, o.order_date
HAVING COUNT(*) > 2 AND o.order_date BETWEEN '2023-07-18' AND '2023-10-18'
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/21f6dae9-e2a6-40ae-be1c-a6078c817f74)


##Задание 4

```
SELECT first_name, last_name, email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
JOIN products p ON p.product_id = o.product_id
WHERE p.price > 1000 AND p.category != 'Electronics';
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/d2c44bee-a610-4d59-a84b-f9d59bc616dd)


##Задание 3

```
WITH tmp_shit AS (
	SELECT p.product_id, SUM(p.price) AS "price_sum" FROM products p
	GROUP BY p.product_id, p.price
),
global_avg_price AS (
	SELECT AVG(p.price) FROM products p
)

SELECT c.first_name, c.last_name, c.email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
JOIN tmp_shit t ON t.product_id = o.product_id
WHERE t.price_sum > (SELECT * FROM global_avg_price);

```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/617302df-333e-4cf6-a73f-389ef9cefbe1)
