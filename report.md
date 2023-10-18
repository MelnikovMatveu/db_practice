## task 2
``` SELECT name, age FROM person WHERE address = 'Kazan' ```
![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/d4ee0bf7-ee12-48d4-91df-32394a000a34)

## task 3
```
SELECT "name", "age" FROM "person"
WHERE "gender" = 'female'
ORDER BY "name" ASC;
```
![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/5ae2dfc4-f960-4ac6-b4ca-94f2efc0180f)


## task 4


```
SELECT name, rating FROM pizzeria WHERE rating BETWEEN 3 AND 5
ORDER BY rating ASC;
```

```
SELECT name, rating FROM pizzeria WHERE rating > 3.5
ORDER BY rating ASC;
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/0c0e6c25-6ad7-41c8-971c-52eabe2b6bcf)



## task 5

```
SELECT "person_id" FROM "person_visits"
WHERE "visit_date" BETWEEN '2022-01-01' AND '2022-01-07';
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/958951b4-f8ba-4568-bb0e-9ea60367235e)


## task 6

```
SELECT name FROM person WHERE person.id IN
(SELECT "person_id" FROM "person_order" WHERE "menu_id" = 1 OR "menu_id" = 3 OR "menu_id" = 8);
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/5010610c-c1a9-433e-9bb0-30f19153133a)


## task 7

```
SELECT EXISTS
(SELECT * FROM person WHERE name = 'Dmitriy')
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/d0e50be3-81ae-4b87-aaf4-33aa1743a068)


```
SELECT EXISTS
(SELECT * FROM person WHERE name = 'ana')
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/5253096a-4623-42b4-ac54-d9a9d1c21916)






##Задание 1
```
SELECT name FROM person ORDER BY name
```
![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/af7d9862-b3ed-479f-b25c-f4a42966a630)


##Задание 2

```
CREATE VIEW v_generated_dates AS
select generate_series('2022-01-01', '2022-01-31', interval '1 day')::date
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/52f07a49-8ddc-49a8-9f84-cdf45110ff34)



##Задание 3

```
SELECT * FROM v_generated_dates
WHERE generate_series NOT IN (SELECT visit_date FROM person_visits)
ORDER BY generate_series
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/fb2edbea-0fc3-4938-a207-5a1fa28bc3ce)


##Задание 4

```
SELECT person_id FROM R EXCEPT ALL SELECT person_id FROM S
UNION ALL 
(SELECT person_id FROM S EXCEPT ALL SELECT person_id FROM R)
```

![image](https://github.com/MelnikovMatveu/db_practice/assets/145557573/f0e09589-4b27-4373-9702-2566358119b2)


##Задание 5

```
SELECT customer_id COUNT(*)
FROM orders
WHERE order_date BETWEEN '2023-02-01' AND '2023-05-01'  

```
