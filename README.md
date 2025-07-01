select username from users where exists (select total_amount from orders where users.user_id=orders.user_id);
+---------------+
| username      |
+---------------+
| nehaprakash   |
| parvathygowri |
| rudradev      |
+---------------+
3 rows in set (0.037 sec)

mysql> select * from users where user_id in ( select total_amount from orders where users.user_id=orders.user_id);
Empty set (0.026 sec)

mysql> select * from users where user_id in ( select user_id from orders);
+---------+---------------+---------------+---------+------------+-----------+---------------------+
| user_id | username      | password_hash | email   | first_name | last_name | created_at          |
+---------+---------------+---------------+---------+------------+-----------+---------------------+
|       1 | nehaprakash   | neha          | neha123 | neha       | prakash   | 2025-06-30 13:02:09 |
|       2 | rudradev      | rudi          | rudi555 | rudra      | dev       | 2025-06-28 10:15:08 |
|       3 | parvathygowri | paru          | paru23  | parvathy   | gowri     | 2025-06-30 13:05:11 |
+---------+---------------+---------------+---------+------------+-----------+---------------------+
3 rows in set (0.010 sec)

mysql> select * from users where user_id not in ( select user_id from orders);
+---------+-------------+---------------+----------+------------+-----------+---------------------+
| user_id | username    | password_hash | email    | first_name | last_name | created_at          |
+---------+-------------+---------------+----------+------------+-----------+---------------------+
|       4 | nishasarang | nishu         | nishu343 | nisha      | sarang    | 2025-07-01 11:56:00 |
+---------+-------------+---------------+----------+------------+-----------+---------------------+
1 row in set (0.009 sec)

 ysql> select username from users where not exists (select total_amount from orders where users.user_id=orders.user_id);
+-------------+
| username    |
+-------------+
| nishasarang |
+-------------+
1 row in set (0.011 sec)

mysql> select * from users where user_id = ( select total_amount from orders where users.user_id=orders.user_id and total_amount>500);
Empty set (0.012 sec)

mysql> select * from users where user_id = any ( select user_id from orders where total_amount>500);
+---------+-------------+---------------+---------+------------+-----------+---------------------+
| user_id | username    | password_hash | email   | first_name | last_name | created_at          |
+---------+-------------+---------------+---------+------------+-----------+---------------------+
|       1 | nehaprakash | neha          | neha123 | neha       | prakash   | 2025-06-30 13:02:09 |
+---------+-------------+---------------+---------+------------+-----------+---------------------+
1 row in set (0.012 sec)

mysql> select * from users where user_id = all ( select user_id from orders where total_amount>500);
+---------+-------------+---------------+---------+------------+-----------+---------------------+
| user_id | username    | password_hash | email   | first_name | last_name | created_at          |
+---------+-------------+---------------+---------+------------+-----------+---------------------+
|       1 | nehaprakash | neha          | neha123 | neha       | prakash   | 2025-06-30 13:02:09 |
+---------+-------------+---------------+---------+------------+-----------+---------------------+
1 row in set (0.015 sec)

mysql> select * from users where user_id = any ( select user_id from orders where total_amount<500);
+---------+---------------+---------------+---------+------------+-----------+---------------------+
| user_id | username      | password_hash | email   | first_name | last_name | created_at          |
+---------+---------------+---------------+---------+------------+-----------+---------------------+
|       2 | rudradev      | rudi          | rudi555 | rudra      | dev       | 2025-06-28 10:15:08 |
|       3 | parvathygowri | paru          | paru23  | parvathy   | gowri     | 2025-06-30 13:05:11 |
+---------+---------------+---------------+---------+------------+-----------+---------------------+
2 rows in set (0.008 sec)

mysql> select * from users where user_id = all ( select user_id from orders where total_amount<500);
Empty set (0.008 sec)

mysql> select * from users where user_id = all ( select user_id from orders where status='paid');
Empty set (0.007 sec)

mysql> select * from users where user_id = any ( select user_id from orders where status='paid');
+---------+---------------+---------------+---------+------------+-----------+---------------------+
| user_id | username      | password_hash | email   | first_name | last_name | created_at          |
+---------+---------------+---------------+---------+------------+-----------+---------------------+
|       2 | rudradev      | rudi          | rudi555 | rudra      | dev       | 2025-06-28 10:15:08 |
|       3 | parvathygowri | paru          | paru23  | parvathy   | gowri     | 2025-06-30 13:05:11 |
+---------+---------------+---------------+---------+------------+-----------+---------------------+
2 rows in set (0.008 sec)
