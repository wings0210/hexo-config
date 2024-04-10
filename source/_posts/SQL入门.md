---
title: SQL入门
date: 2024-01-10 11:19:47
tags: SQL
categories: SQL相关
---

# 一、概述

***SQL关键字分为普通关键字和DDL（数据定义语言）***



# 二、DDL关键字

在SQL语言中，DDL（数据定义语言）关键字的顺序通常是以下方式：

1. ***CREATE：用于创建数据库对象，如表、视图、索引等。***

2. ***ALTER：用于修改数据库对象的结构，如添加、修改或删除列、约束等。***

3. ***DROP：用于删除数据库对象，如表、视图、索引等。***

4. ***TRUNCATE：用于截断表，即删除表中的所有数据。***

5. **RENAME：用于重命名数据库对象，如表、列等。**

   

下面是一些具体的SQL语句示例，以说明这些DDL关键字的顺序：

1. 创建表（CREATE TABLE）：

```sql
CREATE TABLE Customers (
    CustomerID INT,
    CustomerName VARCHAR(50),
    Email VARCHAR(100)
);
```

1. 修改表结构（ALTER TABLE）：

```sql
ALTER TABLE Customers
ADD Phone VARCHAR(20);
```

1. 删除表（DROP TABLE）：

```sql
DROP TABLE Customers;
```

1. 截断表（TRUNCATE TABLE）：

```sql
TRUNCATE TABLE Customers;
```

1. 重命名表（RENAME TABLE）：

```sql
RENAME TABLE Customers TO Clients;
```



# 三、关键字顺序规则

## 1）关键字概述

以下是一些常见的关键字：

1. ***SELECT：用于从数据库中检索数据。***

2. ***FROM：指定要检索数据的表或视图。***

3. ***WHERE：用于指定检索条件。***

4. ***GROUP BY：用于按指定的列对结果进行分组。***

5. ***HAVING：用于指定分组后的条件。***

6. ***ORDER BY：用于对结果进行排序。***

7. ***INSERT INTO：用于向表中插入数据。***

8. ***VALUES：指定要插入的值。***

9. ***UPDATE：用于更新表中的数据。***

10. ***SET：指定要更新的列和值。***

11. ***DELETE FROM：用于从表中删除数据。***

    

以下是一些具体的SQL语句示例，以说明这些关键字的顺序：

1. 检索数据（SELECT）：

```sql
SELECT CustomerName, Email
FROM Customers
WHERE Country = 'USA'
ORDER BY CustomerName;
```

1. 插入数据（INSERT INTO）：

```sql
INSERT INTO Customers (CustomerName, Email)
VALUES ('John', 'john@example.com');
```

1. 更新数据（UPDATE）：

```sql
UPDATE Customers
SET Email = 'newemail@example.com'
WHERE CustomerID = 1;
```

1. 删除数据（DELETE FROM）：

```sql
DELETE FROM Customers
WHERE CustomerID = 2;
```

# 

## 2）具体顺序举例



***1、CRUD主体***

***2、联表+连接条件（内联只包含符合连接条件的记录，外联还包含不符合连接条件的记录）***

***3、CRUD条件***

***4、分组聚合条件（按照某列字段值进行分类记录）***

***5、分组筛选***

***6、排序***

具体示例：

```sql
SELECT c.CustomerName, o.OrderID, SUM(od.Quantity * od.UnitPrice) AS TotalAmount
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
JOIN OrderDetails od ON o.OrderID = od.OrderID
WHERE c.Country = 'USA'
GROUP BY c.CustomerName, o.OrderID
HAVING TotalAmount > 1000
ORDER BY TotalAmount DESC;
```



# 四、一些小细节



## 1）左联和右联区别

左联：以左表为主表，即以左表的字段为键，来扩充交叉得新表

右联：以右表为主表，即以右表的字段为键，来扩充交叉得新表





## 2）具体例子说明

假设我们有以下数据：

Customers 表：

| CustomerID | CustomerName |
| ---------- | ------------ |
| 1          | John         |
| 2          | Mary         |
| 3          | David        |

Orders 表：

| OrderID | CustomerID | OrderDate  |
| ------- | ---------- | ---------- |
| 101     | 1          | 2022-01-01 |
| 102     | 2          | 2022-02-01 |
| 103     | 2          | 2022-03-01 |
| 104     | 4          | 2022-04-01 |

使用左联接（LEFT JOIN）的示例查询语句如下：

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

执行上述查询语句后，将返回以下结果：

| CustomerName | OrderID |
| ------------ | ------- |
| John         | 101     |
| Mary         | 102     |
| Mary         | 103     |
| David        | NULL    |

​        在这个结果中，我们可以看到左表 "Customers" 中的所有行都被返回，而右表 "Orders" 中只有符合连接条件的行被返回。由于 "David" 在 "Orders" 表中没有匹配的订单，所以对应的 "OrderID" 列显示为 NULL。



现在，让我们使用右联接（RIGHT JOIN）的示例查询语句：

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
RIGHT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

执行上述查询语句后，将返回以下结果：

| CustomerName | OrderID |
| ------------ | ------- |
| John         | 101     |
| Mary         | 102     |
| Mary         | 103     |
| NULL         | 104     |
