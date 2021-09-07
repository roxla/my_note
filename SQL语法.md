最基本：

增删改查



## 普通查询

查询：SELECT ->从数据表中获取数据

### 单表全字段查询  -> 将整个表的内容输出出来

语法：

SELECT  * FROM table_name

例子：

SELECT * FROM emp



### 单表个别字段查询

语法：

SELECT  字段1,字段2...  FROM table_name

例子：

SELECT name,salary FROM emp



### 条件查询 -> 对输出的结果进行条件筛选，只留下想看的内容

语法：

SELECT  字段1,字段2...  FROM table_name WHERE  条件1 and/or 条件2

例子：

SELECT *FROM emp WHERE age<25 and salary >5000



### 聚合函数  -> 对某一列求和、求平均值、求最大值、求最小值、求数据条数 汇总数据

语法：

SUM(列名) AVG(列名) MAX(列名) MIN(列名) COUNT(*) 



## 添加数据

增加：INSERT -> 往数据表中插入一条新的数据

语法：

### 个别字段插入：

INSERT INTO table_name (字段1,字段2...) VALUES (值1,值2...)

### 全字段插入：

INSERT INTO table_name VALUES (值1,值2...)

例子：

INSERT into emp (name,salary) VALUES ('zl',66666)



##  修改数据 

修改：UPDATE -> 更新数据表中的数据，从旧的状态修改成新的状态

语法：

UPDATE table_name SET 要更改的字段名 1= 新值1,要更改的字段名 2= 新值2 WHERE 条件

例子：

UPDATE emp SET salary = 88888,age = 44 WHERE id = 4



## 删除数据

删除：DELETE ->从数据表中删除数据

语法：

DELETE FROM table_name WHERE 条件

例子：

DELETE FROM emp where id = 8



课堂案例：

新建一个product表

有5个字段

id int -- 商品编号，主键

product_name varchar --商品名称

classify_name varchar -- 分类名称

sale_price double -- 售价

cost_price double --成本价



基本增删改查：

需求：

添加一条数据到产品表中，商品名称为“苹果手机”，售价200

```sql
INSERT INTO product (product_name,sale_price) VALUES ('苹果手机',200); 
```

删除表中成本价为20且商品名称为“华为手机”的数据

```sql
DELETE FROM product WHERE cost_price = 20 and product_name = '华为手机'
```

查询商品编号小于5的数据，只看编号，商品名称和售价

```sql
SELECT id,product_name,sale_price FROM product WHERE id< 5
```

查询分类名称为手机或者售价小于等于50的商品

```sql
SELECT * FROM product WHERE classify_name='手机' OR sale_price <= 5
```

修改商品名称为“小米手机”的商品，售价改为20

```sql
UPDATE product SET sale_price=20 WHERE product_name='小米手机'
```

