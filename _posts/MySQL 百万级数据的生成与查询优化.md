# MySQL 百万级数据的生成与查询优化

## 生成测试数据

使用 Shell 脚本或者 Python 脚本

方法一：Python

```python
python -c "for i in range(1, 1+2000000): print(i)" > test.txt
```

方法二：Shell 

```shell
for((i=1;i<=2000000;i++));  
do   
echo $i >> test.txt
done 
```

对比：

python 脚本的生成速度远高于 shell 脚本，但是shell 是Linux自带的，python可能需要自己去下载。



## 生成临时表

使用脚本生成的 test.txt 文件中，每行只有一个数字，每行数据是递增的。

因此需要在数据库新建一个临时表 tmp_table，并导入 txt 文件中的数据。

```sql
CREATE TABLE tmp_table (
    id INT,
    PRIMARY KEY (id)
);
```

导入数据

```sql
load data infile '/var/lib/mysql-files/test.txt' replace into table tmp_table;
```

**注意：**导入数据时有可能会报错，原因是mysql默认没有开secure_file_priv（ 这个参数用来限制数据导入和导出操作的效果，例如执行LOAD DATA、SELECT … INTO OUTFILE语句和LOAD_FILE()函数。这些操作需要用户具有FILE权限。）

**解决办法：**在mysql的配置文件中（my.ini 或者 my.conf）中添加 secure_file_priv = /Users/LJTjintao/temp/`, 然后重启mysql 解决

![img](D:\GitHub\blog\img\in-post\1.jpg)

![img](D:\GitHub\blog\img\in-post\2.jpg)



## 测试表

```sql
CREATE TABLE `t_motion` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `filename` char(14) NOT NULL,
  `device_id` int(11) NOT NULL,
  `camera_id` int(11) NOT NULL,
  `create_time` datetime NOT NULL ON UPDATE CURRENT_TIMESTAMP,
  `update_time` datetime NOT NULL ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```



**以临时表为基础数据，插入数据到t_motion中**

```sql

INSERT INTO t_motion
SELECT
  id,
  CEILING(RAND() * 900000000000+100000000000),
  CEILING(Rand() * 100),
  CEILING(Rand() * 10),
  NOW(),
  NOW()
FROM
  tmp_table;
```



**更新创建时间字段让插入的数据的创建时间更加随机**

```sql
UPDATE t_motion
SET create_time = DATE_SUB(
	create_time,
	INTERVAL FLOOR(1 +(RAND() * 7)) YEAR
);
```

