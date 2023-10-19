##Задание 1

```
SELECT c.customer_id, c.first_name, COUNT(*) AS quantity FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, o.order_date
HAVING COUNT(*) > 2 AND o.order_date BETWEEN '2023-07-18' AND '2023-10-18'
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/21f6dae9-e2a6-40ae-be1c-a6078c817f74)


##Задание 2


```

```



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


##Задание 4

```
SELECT first_name, last_name, email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
JOIN products p ON p.product_id = o.product_id
WHERE p.price > 1000 AND p.category != 'Electronics';
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/d2c44bee-a610-4d59-a84b-f9d59bc616dd)





##Задание 6

```
WITH tab AS (
    SELECT customer_id,
    MAX (order_date) AS max_date,
	MIN(order_date) AS min_date FROM orders
    GROUP BY customer_id
),

tabl AS (
    SELECT customer_id, max_date - min_date AS difference FROM tab
)

SELECT customer_id FROM tabl WHERE difference = (SELECT MAX(difference) FROM tabl);
```


![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/c2ffc9f1-8ccf-4fb0-b671-2c6afe075da3)



##Задание 8

```
SELECT category, p.price,(p.price * 0.9) AS discovnt_price FROM products p
WHERE category ='Clothing'
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/c21a0cec-38d0-419b-9548-484ae28b125b)

