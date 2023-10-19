##Задание 1

```
SELECT c.customer_id, c.first_name, COUNT(*) AS quantity FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, o.order_date
HAVING COUNT(*) > 2 AND o.order_date BETWEEN '2023-07-18' AND '2023-10-18'
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/21f6dae9-e2a6-40ae-be1c-a6078c817f74)
