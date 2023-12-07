```
create table shop (
	id BIGINT PRIMARY KEY,
	name_shop TEXT
);

insert into shop values (1, 'Fanastik');
insert into shop values (2, 'Qveq');
insert into shop values (3, 'Electronik');
insert into shop values (4, 'Neel');
insert into shop values (5, 'Tools');







create table Products (
	id BIGINT PRIMARY KEY,
	name text,
	price float,
        volume float
);

insert into products values (1, 'tablet', 120.99, 0.6);
insert into products values (2, 'video card', 500, 1);
insert into products values(3, 'chair', 10, 5);
insert into products values(4, 'armchair', 50.69, 6.4);
insert into products values(5, 'telephone', 649.49, 0.2);
insert into products values(6, 'mug', 3.57, 0.2);
insert into products values(7, 'keyboard', 84, 0.7);
insert into products values(8, 'toy car', 39, 0.5);
insert into products values(9, 'flash drive', 9.99, 0.1);
insert into products values(10, 'microphone', 54, 0.3);
insert into products values(11, 'battery', 1, 0.1);
insert into products values(12, 'soccer ball', 35.50, 1.3);
insert into products values(13, 'cap', 5.58, 0.3);
insert into products values(14, 'mask', 2.79, 0.2);
insert into products values(15, 'case S-7', 86, 0.2);
insert into products values(16, 'set of tools', 75.99, 1.6);
insert into products values(17, 'humidifier', 73.56, 1.9);
insert into products values(18, 'heater', 46, 4);
insert into products values(19, 'speakers', 56.66, 3.5);
insert into products values(20, 'console', 567.63, 3);
insert into products values(21, 'calendar', 2.59, 0.4);












create table users (
	id BIGINT PRIMARY KEY,
	username TEXT ,
	email varchar (64),
        address VARCHAR(128)
);

INSERT INTO users (id, username, email, address)
VALUES 
    (1, 'ИванИванов', 'ivan@example.com', 'ул. Ленина, 1'),
    (2, 'ДарьяВерхова', 'dariaverkhova@example.com', 'ул. Ленина, 46'),
    (3, 'НиколайЗлотов', 'alexeyivanovich@example.com', 'ул. Декабристов, 11'),
    (4, 'АннастасияТихова', 'annastasiatikhova@example.com', 'ул. Пушкина, 15'),
    (5, 'ЕвгенияНокина', 'evgeniyanokina@example.com', 'ул. Декабристов, 15'),
    (6, 'АлексейМирнов', 'alexeymirnov@example.com', 'ул. Советская, 7'),
    (7, 'ТинаЛитова', 'tinalitova@example.com', 'ул. Володарского, 9'),
    (8, 'ЯнаНиколаева', 'yananikolaeva@example.com', 'пр. Декабристов, 45'),
    (9, 'ЕгорТарин', 'egortarin@example.com', 'ул. Гагарина, 30'),
    (10, 'АлександраНиколаева', 'alexandranikolaeva@example.com', 'ул. Пушкина, 50');













create table pickuppoint (
	id BIGINT PRIMARY KEY,
	warehouse_name TEXT ,
	storage_capacity float
);



insert into pickuppoint values (1, 'ул. Ленина 44', 1000);
insert into pickuppoint values (2, 'ул. Ленина 105', 1000);
insert into pickuppoint values (3, 'ул. Долгова 56', 1000);
insert into pickuppoint values (4, 'ул. Озёрная 12', 1000);
insert into pickuppoint values (5, 'ул. Южная 98', 1000);
insert into pickuppoint values (6, 'ул. Перова 34', 1000);
















create table orders (
	id BIGINT PRIMARY KEY,
	orderSum float,
	user_id INT,
	FOREIGN KEY (user_id) REFERENCES users(id),
	pickuppoint_id INT,
	FOREIGN KEY (pickuppoint_id) REFERENCES pickuppoint(id),
	order_date date
);




create table orderdetails (
	id BIGINT PRIMARY KEY,
	orders_id INT,
	FOREIGN KEY (orders_id) REFERENCES orders(id),
	products_id INT,
	FOREIGN KEY (products_id) REFERENCES products(id),
	amount float
);





insert into orders VALUES (1, 0, 1, 1, '2023-12-06');
insert into orderdetails values (1, 1, 2, 1), (2, 1, 3, 2);

insert into orders VALUES (2, 0, 2, 1, '2023-12-05');
insert into orderdetails values (3, 2, 11, 2), (4, 2, 13, 3);

insert into orders VALUES (3, 0, 3, 5, '2023-12-04');
insert into orderdetails values (5, 3, 6, 1), (6, 3, 7, 1);

insert into orders VALUES (4, 0, 4, 1, '2023-12-06');
insert into orderdetails values (7, 4, 2, 2), (8, 4, 11, 2);

insert into orders VALUES (5, 0, 5, 1, '2023-12-06');
insert into orderdetails values (9, 5, 2, 1), (10, 5, 6, 2);

with order_sum AS (
	SELECT od.orders_id, SUM(od.amount * p.price) FROM orderdetails od
	JOIN products p ON p.id = od.products_id
	GROUP BY od.orders_id
)
update orders SET ordersum = (SELECT sum from order_sum WHERE orders_id = orders.id)





create table shop_product (
	shop_id INT,
    product_id INT,
    PRIMARY KEY (shop_id, product_id),
    FOREIGN KEY (shop_id) REFERENCES Shop(id),
    FOREIGN KEY (product_id) REFERENCES Products(id)
);

























-- alter table orders add column user_id bigint NOT NULL 
-- alter table orderdetails add column order_date date NOT NULL 
-- insert into orders VALUES (1, 0, 0, 1, 1)
-- alter table orderdetails add column amount int NOT NULL default 1
-- insert into orderdetails values (1, 1, 2, '2023-12-06', 1), (2, 1, 3, '2023-12-06', 2)
-- with order_sum AS (
-- 	SELECT od.orders_id, SUM(od.amount * p.price) FROM orderdetails od
-- 	JOIN products p ON p.id = od.products_id
-- 	GROUP BY od.orders_id
-- )
-- update orders SET ordersum = (SELECT sum from order_sum WHERE orders_id = orders.id)


-- alter table orderdetails drop column order_date

insert into orders VALUES (4, 0, 1, 4, '2023-11-13');
insert into orderdetails VALUES (7, 4, 11, 2), (8, 4, 14, 1);
with order_sum AS (
	SELECT od.orders_id, SUM(od.amount * p.price) FROM orderdetails od
	JOIN products p ON p.id = od.products_id
	GROUP BY od.orders_id
)
update orders SET ordersum = (SELECT sum from order_sum WHERE orders_id = orders.id)
```



## ТРИГГЕРЫ

```
CREATE OR REPLACE FUNCTION update_order_sum()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE orders
    SET orderSum = (
        SELECT SUM(od.amount * p.price)
        FROM orderdetails od
        JOIN products p ON p.id = od.products_id
        WHERE od.orders_id = NEW.orders_id
    )
    WHERE id = NEW.orders_id;
    
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_order_sum_trigger
AFTER INSERT OR UPDATE ON orderdetails
FOR EACH ROW EXECUTE FUNCTION update_order_sum();


Этот триггер обновляет сумму заказа в таблице orders после добавления новых деталей заказа.
```


```
CREATE OR REPLACE FUNCTION update_order_date()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE orders
    SET order_date = CURRENT_DATE
    WHERE id = NEW.orders_id AND NEW.amount > 0;
    
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_order_date_trigger
AFTER INSERT OR UPDATE ON orderdetails
FOR EACH ROW EXECUTE FUNCTION update_order_date();


Этот триггер обновляет дату заказа в таблице orders при изменении суммы заказа (если сумма больше нуля).


```


```
CREATE OR REPLACE FUNCTION update_shop_product_price()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE shop_product
    SET price = NEW.price
    WHERE product_id = NEW.id;
    
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_shop_product_price_trigger
AFTER UPDATE ON products
FOR EACH ROW EXECUTE FUNCTION update_shop_product_price();

Этот триггер следит за изменениями в таблице products и автоматически обновляет цены в таблице shop_product для соответствующих продуктов.

```


