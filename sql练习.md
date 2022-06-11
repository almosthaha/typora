# sql练习

## 第1题：组合两个表:

题目：

表: Person

+-------------+---------+
| 列名         | 类型     |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
personId 是该表的主键列。
该表包含一些人的 ID 和他们的姓和名的信息。


表: Address

+-------------+---------+
| 列名         | 类型    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
addressId 是该表的主键列。
该表的每一行都包含一个 ID = PersonId 的人的城市和州的信息。


编写一个SQL查询来报告 Person 表中每个人的姓、名、城市和州。如果 personId 的地址不在 Address 表中，则报告为空  null 。

以 任意顺序 返回结果表。

查询结果格式如下所示。



示例 1:

输入: 
Person表:
+----------+----------+-----------+
| personId | lastName | firstName |
+----------+----------+-----------+
| 1        | Wang     | Allen     |
| 2        | Alice    | Bob       |
+----------+----------+-----------+
Address表:
+-----------+----------+---------------+------------+
| addressId | personId | city          | state      |
+-----------+----------+---------------+------------+
| 1         | 2        | New York City | New York   |
| 2         | 3        | Leetcode      | California |
+-----------+----------+---------------+------------+
输出: 
+-----------+----------+---------------+----------+
| firstName | lastName | city          | state    |
+-----------+----------+---------------+----------+
| Allen     | Wang     | Null          | Null     |
| Bob       | Alice    | New York City | New York |
+-----------+----------+---------------+----------+
解释: 
地址表中没有 personId = 1 的地址，所以它们的城市和州返回 null。
addressId = 1 包含了 personId = 2 的地址信息。



答案：select p.FirstName,p.lastname,a.city,a.state 

from person p left join address a

on p.personid = a.personid



知识点总结：

①A inner join B：取交集  （内连接适合多表都存在的数据）

②A left join B：取A全部，B没有对应的值，则为null  （外连接适合存在有一个为空的情况）

③A right join B：取B全部，A没有对应的值，则为null

④A full outer join B：取并集，彼此没有对应的值为null

上述4种的对应条件，在on后填写。



## 第2题: 超过经理收入的员工

表：Employee 

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| name        | varchar |
| salary      | int     |
| managerId   | int     |
+-------------+---------+
Id是该表的主键。
该表的每一行都表示雇员的ID、姓名、工资和经理的ID。


编写一个SQL查询来查找收入比经理高的员工。

以 任意顺序 返回结果表。

查询结果格式如下所示。

 

示例 1:

输入: 
Employee 表:
+----+-------+--------+-----------+
| id | name  | salary | managerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | Null      |
| 4  | Max   | 90000  | Null      |
+----+-------+--------+-----------+
输出: 
+----------+
| Employee |
+----------+
| Joe      |
+----------+
解释: Joe 是唯一挣得比经理多的雇员。



答案：

第一种(用join解法)

select 
a.name as Employee
from Employee as a 
join Employee as b
on a.managerId = b.id
where a.salary > b.salary



第二种(用where and )

select
    e1.Name AS Employee 
FROM
    Employee e1,
    Employee e2
where
    e1.ManagerId = e2.Id AND e1.Salary > e2.Salary



## 第3题：查找重复的电子邮箱

示例：

+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
根据以上输入，你的查询应返回以下结果：

+---------+
| Email   |
+---------+
| a@b.com |
+---------+
说明：所有电子邮箱都是小写字母。

答案：查询后只显示一条数据

```sql
-- 解法1
select email from person group by email having count(email)>1

--解法2
select email from (select count(1) as t,email from person group by email)r  where r.t>1;

--解法3
select distinct(p1.Email) from Person p1  
join Person  p2 on p1.Email = p2.Email AND p1.Id!=p2.Id
```

知识点总结：having用于分组后的过滤，放到group by 后面，常和聚合函数一起用 where 用于全表数据集的筛选，在分组动作的前面



分组查询查询后显示多条相同数据：

Select * From 表 Where 重复字段 In (Select 重复字段 From 表 Group By 重复字段 Having Count(*)>1)

![image-20220527091730517](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527091730517.png)



分组查询后统计查询的数量:

SELECT COUNT(brand_name) '公司个数',brand_name
FROM tb_brand 
GROUP BY brand_name 
HAVING COUNT(brand_name)>5

![image-20220527092009219](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220527092009219.png)



分组后查询



## 第4题：从不订购的客户

题目：某网站包含两个表，Customers 表和 Orders 表。编写一个 SQL 查询，找出所有从不订购任何东西的客户。

Customers 表：

+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+
Orders 表：

+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+
例如给定上述表格，你的查询应返回：

+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+

答案：

第一种：左连接 使用左连接要注意 null 不能用=，要用is判断

```sql
select Name Customers
from Customers c
left join Orders o
on c.Id=o.CustomerId
where o.Id is null

```

第二种：no exist

```sql
select Name Customers
from Customers c
where not exists(select 1 from Orders o where o.CustomerId=c.Id)
```

第三种：no in

```sql
select Name Customers
from Customers c
where c.Id not in (
    select CustomerId from Orders
)
```

## 第5题: 删除重复的电子邮箱



表: Person

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| email       | varchar |
+-------------+---------+
id是该表的主键列。
该表的每一行包含一封电子邮件。电子邮件将不包含大写字母。


编写一个 SQL 删除语句来 删除 所有重复的电子邮件，只保留一个id最小的唯一电子邮件。

以 任意顺序 返回结果表。 （注意： 仅需要写删除语句，将自动对剩余结果进行查询）

查询结果格式如下所示。

 

示例 1:

输入: 
Person 表:
+----+------------------+
| id | email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
输出: 
+----+------------------+
| id | email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
解释: john@example.com重复两次。我们保留最小的Id = 1。



第一种：

```
delete u
from Person u , Person v
where v.id < u.id and u.email = v.email 
```

分析: （从select到delete的推理演变）

1.我们可以使用以下代码，将此表与它自身在*电子邮箱*列中连接起来。

SELECT p1.* FROM Person p1,    Person p2 WHERE    p1.Email = p2.Email ;

2.然后我们需要找到其他记录中具有相同电子邮件地址的更大 ID。所以我们可以像这样给 `WHERE` 子句添加一个新的条件。

SELECT p1.*
FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email AND p1.Id > p2.Id
;

因为我们已经得到了要删除的记录，所以我们最终可以将该语句更改为 `DELETE`。

DELETE p1 FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email AND p1.Id > p2.Id



第二种解法：

DELETE from Person 

Where Id not in (

  Select Id 

  From(

  Select MIN(Id) as id

  From Person 

  Group by Email

  ) 

)



## 第6题：上升的温度

题目：

表： Weather

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
id 是这个表的主键
该表包含特定日期的温度信息


编写一个 SQL 查询，来查找与之前（昨天的）日期相比温度更高的所有日期的 id 。

返回结果 不要求顺序 。

查询结果格式如下例。

 

示例 1：

输入：
Weather 表：
+----+------------+-------------+

| id   | recordDate | Temperature |
| ---- | ---------- | ----------- |
|      |            |             |
+----+------------+-------------+
| 1    | 2015-01-01 | 10   |
| ---- | ---------- | ---- |
|      |            |      |
| 2    | 2015-01-02 | 25   |
| ---- | ---------- | ---- |
|      |            |      |
| 3    | 2015-01-03 | 20   |
| ---- | ---------- | ---- |
|      |            |      |
| 4    | 2015-01-04 | 30   |
| ---- | ---------- | ---- |
|      |            |      |
+----+------------+-------------+
输出：
+----+
| id |
+----+
| 2  |
| 4  |
+----+
解释：
2015-01-02 的温度比前一天高（10 -> 25）
2015-01-04 的温度比前一天高（20 -> 30）



答案：

```
select
r1.id as id
from weather r1 
join
weather r2
on
DATEDIFF(r1.recordDate, r2.recordDate) = 1 
where
r1.Temperature > r2.Temperature;
```

题解：left join 跟 datediff函数的使用 datediff是两个日期的天数差集 r1>r2的话 结果为正数，反之，结果为负数

为什么这里用left join，left除了外连接还能用于哪些场景



## 第七题：游戏的玩家分析

题目：活动表 Activity：

+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| player_id    | int     |
| device_id    | int     |
| event_date   | date    |
| games_played | int     |
+--------------+---------+
表的主键是 (player_id, event_date)。
这张表展示了一些游戏玩家在游戏平台上的行为活动。
每行数据记录了一名玩家在退出平台之前，当天使用同一台设备登录平台后打开的游戏的数目（可能是 0 个）。


写一条 SQL 查询语句获取每位玩家 第一次登陆平台的日期。

查询结果的格式如下所示：

Activity 表：
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-05-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |
+-----------+-----------+------------+--------------+

Result 表：
+-----------+-------------+
| player_id | first_login |
+-----------+-------------+
| 1         | 2016-03-01  |
| 2         | 2017-06-25  |
| 3         | 2016-03-02  |
+-----------+-------------+

答案（考察group by ,聚合函数）

```
select player_id,min(event_date) first_login
from activity
group by player_id
```

分析：应该对每一个对应的语句，函数，所适应的场景有充分的了解

这样在不同的场景下才可以游刃有余

## 第8题 超过5名学生的课

题目：

表: Courses

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| student     | varchar |
| class       | varchar |
+-------------+---------+
(student, class)是该表的主键列。
该表的每一行表示学生的名字和他们注册的班级。


编写一个SQL查询来报告 至少有5个学生 的所有类。

以 任意顺序 返回结果表。

查询结果格式如下所示。

 

示例 1:

输入: 
Courses table:
+---------+----------+
| student | class    |
+---------+----------+
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |
+---------+----------+
输出: 
+---------+ 
| class   | 
+---------+ 
| Math    | 
+---------+
解释: 
-数学课有6个学生，所以我们包括它。
-英语课有1名学生，所以我们不包括它。
-生物课有1名学生，所以我们不包括它。
-计算机课有1个学生，所以我们不包括它。

答案：

```sql
SELECT class
FROM Courses
GROUP BY class 
    HAVING count(class) >= 5
```

解析：这里要注意至少，之多等关键词

第9题：订单最多客户

题目：

表: Orders

+-----------------+----------+
| Column Name     | Type     |
+-----------------+----------+
| order_number    | int      |
| customer_number | int      |
+-----------------+----------+
Order_number是该表的主键。
此表包含关于订单ID和客户ID的信息。


编写一个SQL查询，为下了 最多订单 的客户查找 customer_number 。

测试用例生成后， 恰好有一个客户 比任何其他客户下了更多的订单。

查询结果格式如下所示。

 

示例 1:

输入: 
Orders 表:
+--------------+-----------------+
| order_number | customer_number |
+--------------+-----------------+
| 1            | 1               |
| 2            | 2               |
| 3            | 3               |
| 4            | 3               |
+--------------+-----------------+
输出: 
+-----------------+
| customer_number |
+-----------------+
| 3               |
+-----------------+
解释: 
customer_number 为 '3' 的顾客有两个订单，比顾客 '1' 或者 '2' 都要多，因为他们只有一个订单。
所以结果是该顾客的 customer_number ，也就是 3 。

答案：

```
select customer_number
from Orders
group by customer_number
order by count(order_number) desc
limit 1
```

题解：order by 跟 limit的使用 从高到低是降序，desc

## 第9题 趣味电影院

某城市开了一家新的电影院，吸引了很多人过来看电影。该电影院特别注意用户体验，专门有个 LED显示板做电影推荐，上面公布着影评和相关电影描述。

作为该电影院的信息部主管，您需要编写一个 SQL查询，找出所有影片描述为非 boring (不无聊) 的并且 id 为奇数 的影片，结果请按等级 rating 排列。

 

例如，下表 cinema:

+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   1     | War       |   great 3D   |   8.9     |
|   2     | Science   |   fiction    |   8.5     |
|   3     | irish     |   boring     |   6.2     |
|   4     | Ice song  |   Fantacy    |   8.6     |
|   5     | House card|   Interesting|   9.1     |
+---------+-----------+--------------+-----------+
对于上面的例子，则正确的输出是为：

+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   5     | House card|   Interesting|   9.1     |
|   1     | War       |   great 3D   |   8.9     |
+---------+-----------+--------------+-----------+

分析：运算符在sql中的应用

```sql
SELECT
*
FROM cinema
WHERE id % 2 = 1 AND description != 'boring'
ORDER BY rating DESC;
```

MySQL 中判断奇数的 6 种方法：

mod(x, 2) = 1 ，如果余数是 1 就是奇数。
power(-1, x) = -1 ， 如果结果是 -1 就是奇数
x % 2 = 1 ，如果余数是 1 就是奇数。
x & 1 = 1 ，如果是 1 就是奇数
x regexp '[1, 3, 5, 7, 9]$' = 1 如果为 1 就是奇数
x>>1<<1 != x 如果右移一位在左移一位不等于原值，就是奇数

## 第10题 变更性别

题目：

Salary 表：

+-------------+----------+
| Column Name | Type     |
+-------------+----------+
| id          | int      |
| name        | varchar  |
| sex         | ENUM     |
| salary      | int      |
+-------------+----------+
id 是这个表的主键。
sex 这一列的值是 ENUM 类型，只能从 ('m', 'f') 中取。
本表包含公司雇员的信息。


请你编写一个 SQL 查询来交换所有的 'f' 和 'm' （即，将所有 'f' 变为 'm' ，反之亦然），仅使用 单个 update 语句 ，且不产生中间临时表。

注意，你必须仅使用一条 update 语句，且 不能 使用 select 语句。

查询结果如下例所示。

 

示例 1:

输入：
Salary 表：
+----+------+-----+--------+
| id | name | sex | salary |
+----+------+-----+--------+
| 1  | A    | m   | 2500   |
| 2  | B    | f   | 1500   |
| 3  | C    | m   | 5500   |
| 4  | D    | f   | 500    |
+----+------+-----+--------+
输出：
+----+------+-----+--------+
| id | name | sex | salary |
+----+------+-----+--------+
| 1  | A    | f   | 2500   |
| 2  | B    | m   | 1500   |
| 3  | C    | f   | 5500   |
| 4  | D    | m   | 500    |
+----+------+-----+--------+
解释：
(1, A) 和 (3, C) 从 'm' 变为 'f' 。
(2, B) 和 (4, D) 从 'f' 变为 'm' 。

答案：update salary set sex = if(sex='m','f','m');

分析：if中表达式的使用

if(sex='m','f','m') 跟三元运算符差不多