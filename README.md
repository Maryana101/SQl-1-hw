# Домашнее задание к занятию "`SQL. Часть 1`" - `Варфоломеева Марьяна`


### Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

```SQL
select DISTINCT a.district  from address a 
where a.district  like 'K%a' 
and a.district  not like '% %'
```

![Скриншот-1](https://github.com/Maryana101/SQl-1-hw/blob/main/img/1_SQL.png)

### Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

```SQL
select p.payment_date, p.amount 
from payment p 
where date(p.payment_date) BETWEEN  '2005-06-15' and '2005-06-18'
and p.amount > 10
```
![2](https://github.com/Maryana101/SQl-1-hw/blob/main/img/2_SQL.png)

### Задание 3
Получите последние пять аренд фильмов.

```SQL
select f.title , r.rental_date  from rental r 
join inventory i on r.rental_id =i.inventory_id 
join film f on f.film_id =i.film_id 
order by r.rental_date  desc
limit 5
```
![3](https://github.com/Maryana101/SQl-1-hw/blob/main/img/3_SQL.png)

### Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.


Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.


```SQL
select replace(lower(c.first_name), 'll','pp') as first_name , 
	   lower(c.last_name)  as last_name
from customer c 
where c.active =1
and c.first_name  in ('Kelly', 'Willie')
```
![4](hhttps://github.com/Maryana101/SQl-1-hw/blob/main/img/4_SQL.png)

### Задание 5
Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

```SQL
select 
SUBSTR(c.email,1, INSTR(c.email, '@')-1) as user_name,
SUBSTR(c.email, INSTR(c.email, '@')+1, LENGTH(c.email)) as domain
from customer c ;
```
![5](https://github.com/Maryana101/SQl-1-hw/blob/main/img/5_SQL.png)

### Задание 6
Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.
```SQL
select 
    CONCAT(UPPER(LEFT(SUBSTRING_INDEX(c.email, '@', 1), 1)), 
           LOWER(SUBSTRING(SUBSTRING_INDEX(c.email, '@', 1), 2))) as user_name, 
    CONCAT(UPPER(LEFT(SUBSTRING_INDEX(c.email, '@', -1), 1)),
          LOWER(SUBSTRING(SUBSTRING_INDEX(c.email, '@', -1), 2))) as domain
FROM customer c;
```
![6](https://github.com/Maryana101/SQl-1-hw/blob/main/img/6_SQL.png)

