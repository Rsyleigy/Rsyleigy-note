# Clickhouse

# ClickHouse-23.2.1.2537 单机安装部署文档（RPM版安装）

## 1、下载rpm文件

```markdown
rpm和gz包的区别：
# 文件类型：
	rpm是一种二进制文件格式，通常用于RedHat、CentOS等基于RPM包管理器的Linux发行版；而gz则是一种压缩文件格式，通常用于源代码或二进制可执行程序的发布。

# 安装方式：
	rpm可以通过命令行工具（例如yum或rpm命令）进行安装、升级和卸载，也可以使用图形界面工具进行操作；而gz需要先解压缩，然后根据不同的程序安装方式进行安装和配置。

# 依赖性检测：
	rpm可以自动检测并处理安装所需的运行库和依赖项，避免了手动安装依赖项的烦恼；而gz则需要手动检查和安装所需的依赖项。

# 版本控制：
	rpm可以对软件版本进行管理，并支持安装多个版本的软件，方便用户进行升级和回滚；而gz则需要手动管理不同版本的软件包，较为麻烦。
```

#### 下载地址：https://packages.clickhouse.com/rpm/stable/

![image-20230526003421252](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526003421252.png)

![image-20230526003451910](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526003451910.png)

![image-20230526003513166](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526003513166.png)

![image-20230526003536541](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526003536541.png)

## 2、上传rmp文件到Linux中

> 我的目录是 /usr/local/soft/clickhouse-install  其中clickhouse-install是自己创建的

![image-20230526004114121](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526004114121.png)

## 3、开始安装

```markdown
1、进入目录：
	cd /usr/local/soft/clickhouse-install

2、使用rpm命令安装
	sudo rpm -ivh *.rpm
	注意：安装过程需要输入密码，密码不要复杂，123456即可

3、启动服务
	systemctl start clickhouse-server.service

4、状态查看
	systemctl status clickhouse-server.service

5、停止服务
	systemctl stop clickhouse-server.service
	
6、重启服务
	systemctl restart clickhouse-server.service

```

> 安装时输入密码截图，输入的时候不会显示

![image-20230526004635245](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526004635245.png)

> 运行成功状态截图

![image-20230526004756297](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526004756297.png)

## 4、远程工具连接

> 首先修改clickhouse配置文件让其可以被外界访问

```markdown
1、打开clickhouse配置文件
	vim /etc/clickhouse-server/config.xml

2、搜索并放开下面配置的注释
	<listen_host>0.0.0.0</listen_host>

3、保存即可
	:wq!

4、重启
	systemctl restart clickhouse-server
	
查看端口号被哪个服务所占用
netstat -lnpt | grep 9001

使用命令行进入clickhouse客户端
clickhouse-client --port 9001 --password 123456
```

![image-20230526005055859](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526005055859.png)

> 打开DBeaver,新建连接，选择ClickHouse

![image-20230526005524443](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526005524443.png)

> 点击“下一步”，设置JDBC连接，配置主机，用户名和密码

![image-20230526005634955](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526005634955.png)

> 点击“编辑驱动设置”，配置ClickHouse驱动包,下载完成后，点击“确定”

![image-20230526005900031](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526005900031.png)

> 测试连接

![image-20230526005946480](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526005946480.png)

> 然后就可以操作啦

![image-20230526010012822](https://gitee.com/xiaohuya1/image29_demo1/raw/master/img/image-20230526010012822.png)

## 5、学习一个新的组件的方式（学习思想）

### 学习数据库（Hbase, ClickHouse等）

```markdown
# 步骤1：了解数据库的分类，特点，特性，历史背景，应用场景

# 步骤2：安装（单机版，集群部署），启动，修改配置文件，查看状态

# 步骤3：如何建库，建表

# 步骤4：数据类型

# 步骤5：函数，特有函数

# 步骤6：尝试自己写一个分析案例

# 步骤7：学习数据库的特性，独有的特有功能，架构等高级用法

# 步骤8：使用java，python, scala等语言连接数据库做操作
```

### 学习框架组件（例如Hadoop, Hive, Spark等）

```markdown
# 步骤1：找到官网，看组件的概述，了解组件能干什么，适用于什么场景

# 步骤2：安装（单机版，集群部署），启动，修改配置文件，查看状态

# 步骤3：配置环境变量

# 步骤4：针对不同的组件，学习架构，熟悉架构中的小组件，熟悉组件的工作原理

# 步骤5：使用一个小案例，将组件跑通

# 步骤6：思考与其他组件结合的方式

# 步骤7：使用java，python, scala等语言操作组件，跑通一个案例
```

## 学习平台（阿里云DataWorks, 袋鼠云的平台，Dophinscheduler等）

```markdown
# 步骤1: 找到官网，熟悉平台能做什么，尝试注册账号

# 步骤2：看文档，操作平台，完成一个最小的案例

# 步骤3: 部分平台可以在Linux中搭建，尝试搭建一下

# 步骤4：使用java，python, scala等语言，连接平台并操作
```





# Clickhouse-23.2.1.2537 学习

## 一、Clickhouse概述

> clickhouse 官网网址：https://clickhouse.com/

![image-20230526091704292](C:\Users\ASUS\Desktop\Clickhouse-23.2.1.2537 学习.assets\image-20230526091704292.png)

```markdown
OLTP(联机事务处理系统)
	例如mysql等关系型数据库，在对于存储小数据量的时候，查询数据并分析速度很快，OLTP本身其实是一个逻辑上的概念，指的是某个数据库，主要是针对增删改操作的。
	里面的数据会经常的发生变化。
OLAP(联机分析处理系统)
	指的是数据库中的数据长期不变，有着大量的历史数据，并且可以随时的做分析，而增删改操作很少。
```

> OLAP 种类数据库的特点

```
1、绝大多数是读请求
2、数据以相当大的批次(> 1000行)更新，而不是单行更新;或者根本没有更新。
3、已添加到数据库的数据不能修改。
4、对于读取，从数据库中提取相当多的行，但只提取列的一小部分。
5、宽表，即每个表包含着大量的列
6、查询相对较少(通常每台服务器每秒查询数百次或更少)
7、对于简单查询，允许延迟大约50毫秒
8、列中的数据相对较小：数字和短字符串(例如，每个URL 60个字节)
9、处理单个查询时需要高吞吐量(每台服务器每秒可达数十亿行)
10、事务不是必须的
11、对数据一致性要求低
12、每个查询有一个大表。除了他以外，其他的都很小。
13、查询结果明显小于源数据。换句话说，数据经过过滤或聚合，因此结果适合于单个服务器的RAM中
```

## 二、表操作

### 数据类型

> 注意事项：
>
> 1、建表写数据类型的时候，**严格区分大小写**Int32,不能写成int32
>
> 2、建表的时候，**必须要指定表引擎**（详细引擎的使用，后面介绍）

#### a. 整数类型

```
UInt8, UInt16, UInt32, UInt64, UInt128, UInt256, Int8, Int16, Int32, Int64, Int128, Int256
```

```
Int8 — [-128 : 127]
Int16 — [-32768 : 32767]
Int32 — [-2147483648 : 2147483647]
Int64 — [-9223372036854775808 : 9223372036854775807]
Int128 — [-170141183460469231731687303715884105728 : 170141183460469231731687303715884105727]
Int256 — [-57896044618658097711785492504343953926634992332820282019728792003956564819968 : 57896044618658097711785492504343953926634992332820282019728792003956564819967]
```

```
UInt8 — [0 : 255]
UInt16 — [0 : 65535]
UInt32 — [0 : 4294967295]
UInt64 — [0 : 18446744073709551615]
UInt128 — [0 : 340282366920938463463374607431768211455]
UInt256 — [0 : 115792089237316195423570985008687907853269984665640564039457584007913129639935]
```

#### b. 字符串类型

```
String：可变长字符串

FixedString(长度)：固定长字符串，参数是字节数，执行效率比String要高
```

#### c. 日期类型

```markdown
Date 年-月-日

Date32 年-月-日

DateTime 年-月-日 时-分-秒

DateTime64 年-月-日 时-分-秒.毫秒

案例：
# 建表语句：
	create table date_test (date1 Date,date2 Date32,date3 DateTime,date4 DateTime64) ENGINE = TinyLog;

# 插入语句：
	insert into date_test values ('2023-11-21','2023-11-21','2023-11-21','2023-11-21');
	insert into date_test values (1711435333589,1711435333589,1711435333589,1711435333589);  //2024-03-26 15:33:38
	
```

#### d. UUID类型

```
clickhouse提供了一个函数：generateUUIDv4() 生成一个 00000000-0000-0000-0000-000000000000 的编号 编号的类型就是UUID类型
                                                bee32020-a6cb-49a6-a10b-427381b11613
```

#### e. 可为空  Nullable

```
例如建表的时候，有一个id字段类型时Int32，如果当id不确定的时候，我们应该使用null进行填充，而不应该用默认值0，所以，我们这里应该添加的是null
Nullable(Int32)

create table test1 (id Int32,name String) ENGINE = TinyLog;

insert into students_test values (null,'张玮2','男','特训营24期');
```

#### f. 数组 Array(T)

```markdown
字段类型是数组，对于同一个数组，在建表的时候指定数据类型，注意：在MergeTree表引擎中是不允许出现数组嵌套的
注意：需要使用array()函数，将元素组成数组，将来还可以使用toTypeName()查看某一列的数据类型
# 举例：
	create table t1 (col1 Array(Int8)) ENGINE = TinyLog;
	insert into t1 values array(11,12,13);
```

#### g. 小数类型

```markdown
# Decimal(P,S),Decimal32(S),Decimal64(S),Decimal128(S)
有符号的定点数，可在加、减和乘法运算过程中保持精度。对于除法，最低有效数字会被丢弃（不舍入）

P - 精度。有效范围：[1:38]，决定可以有多少个十进制数字（包括分数）。
S - 规模。有效范围：[0：P]，决定数字的小数部分中包含的小数位数。
Decimal(4,2)

举例：12.12234  Decimal(7,5)
P: 7
S: 5
```



### 1、建表语句（入门案例）

```sql
create table users3 (id Int8,name FixedString(12),gender Nullable(FixedString(3)),clazz String) ENGINE = TinyLog;
```

### 2、插入数据

```markdown
# 基本格式
	INSERT INTO [db.]table [(c1, c2, c3)] VALUES (v11, v12, v13), (v21, v22, v23), ...

# 举例
	insert into students_test values (1001,'陆澳','男','特训营24期'),(1002,'李佳豪','男','特训营24期'),(1003,'郭香香','女','特训营24期');
	insert into students_test values (1004,'王宇杰','男','特训营24期'),(1005,'张怀远','男','特训营24期'),(1006,'史俊超','女','特训营24期');
	insert into students_test (name,gender,clazz) values ('张玮','男','特训营24期');

# 查看表结构
	desc 表名;
```

![image-20230526110031047](C:\Users\ASUS\Desktop\Clickhouse-23.2.1.2537 学习.assets\image-20230526110031047.png)



## 三、引擎

### 1、数据库引擎

#### 1.1 Atomic

> clickhouse数据库建库默认指定的数据库引擎

```
它支持非阻塞的DROP TABLE和RENAME TABLE查询和原子的EXCHANGE TABLES t1 AND t2查询。默认情况下使用Atomic数据库引擎。
```

#### 1.2 MySQL

> MySQL引擎用于将远程的MySQL服务器中的表映射到ClickHouse中，并允许您对表进行`INSERT`和`SELECT`查询，以方便您在ClickHouse与MySQL之间进行数据交换
>
> `MySQL`数据库引擎会将对其的查询转换为MySQL语法并发送到MySQL服务器中，因此您可以执行诸如`SHOW TABLES`或`SHOW CREATE TABLE`之类的操作。
>
> 但您无法对其执行以下操作：
>
> - `RENAME`
> - `CREATE TABLE`
> - `ALTER`

```markdown
# 在clickhouse中创建数据库并指定远程的MySQL服务，将其中的某一个数据库映射过来(就将这新建的数据库看成一个远程客户端连接了mysql)

# 建库语句
    CREATE DATABASE [IF NOT EXISTS] db_name [ON CLUSTER cluster]
    ENGINE = MySQL('host:port', ['database' | database], 'user', 'password')
    
# 举例
	create database IF NOT EXISTS bigdata24_mysql ENGINE = MySQL('192.168.169.100:3306','bigdata24','root','123456');
	
# 参数理解：
    host:port — MySQL服务地址，既可以是ip地址，也可以是主机名（如果是主机名，要配置hosts映射）
    database — MySQL数据库名称
    user — MySQL用户名
    password — MySQL用户密码
```



### 2、表引擎

#### 2.1 日志引擎

##### a. Log

> `Log` 与 `TinyLog` 的不同之处在于，«标记» 的小文件与列文件存在一起。这些标记写在每个数据块上，并且包含偏移量，这些偏移量指示从哪里开始读取文件以便跳过指定的行数。这使得可以在多个线程中读取表数据。对于并发数据访问，可以同时执行读取操作，而写入操作则阻塞读取和其它写入。`Log`引擎不支持索引。同样，如果写入表失败，则该表将被破坏，并且从该表读取将返回错误。`Log`引擎适用于临时数据，write-once 表以及测试或演示目的。

```markdown
# 建表，指定表引擎为Log
	create table students_log (id Int32,name String,gender FixedString(3),clazz String) ENGINE = Log;

# 添加数据
	insert into students_log values (1001,'尚平','男','特训营29期'),(1002,'丁义杰','男','特训营29期'),(1003,'汪权','男','特训营29期');
```

##### b. TinyLog

> 最简单的表引擎，用于将数据存储在磁盘上。每列都存储在单独的压缩文件中。写入时，数据将附加到文件末尾。
>
> 并发数据访问不受任何限制：
>
> - 如果同时从表中读取并在不同的查询中写入，则读取操作将抛出异常
> - 如果同时写入多个查询中的表，则数据将被破坏。
>
> 这种表引擎的典型用法是 write-once：首先只写入一次数据，然后根据需要多次读取。查询在单个流中执行。换句话说，此引擎适用于相对较小的表（建议最多1,000,000行）。如果您有许多小表，则使用此表引擎是适合的，因为它比Log引擎更简单（需要打开的文件更少）。当您拥有大量小表时，可能会导致性能低下，但在可能已经在其它 DBMS 时使用过，则您可能会发现切换使用 TinyLog 类型的表更容易。**不支持索引**。

##### c. StripeLog

> **写数据：**
>
> `StripeLog` 引擎将所有列存储在一个文件中。对每一次 `Insert` 请求，ClickHouse 将数据块追加在表文件的末尾，逐列写入。
>
> ClickHouse 为每张表写入以下文件：
>
> - `data.bin` — 数据文件。
> - `index.mrk` — 带标记的文件。标记包含了已插入的每个数据块中每列的偏移量。
>
> `StripeLog` 引擎不支持 `ALTER UPDATE` 和 `ALTER DELETE` 操作。
>
> **读取数据：**
>
> 带标记的文件使得 ClickHouse 可以并行的读取数据。这意味着 `SELECT` 请求返回行的顺序是不可预测的。使用 `ORDER BY` 子句对行进行排序。

```markdown
CREATE TABLE stripe_log_table(timestamp DateTime,message_type String,message String) ENGINE = StripeLog


INSERT INTO stripe_log_table VALUES (now(),'REGULAR','The first regular message')
INSERT INTO stripe_log_table VALUES (now(),'REGULAR','The second regular message'),(now(),'WARNING','The first warning message')

# 建表，指定表引擎为Log
	create table students_stripelog (id Int32,name String,gender FixedString(3),clazz String) ENGINE = StripeLog;

# 添加数据
	insert into students_stripelog values (1001,'陆澳','男','特训营24期'),(1002,'李佳豪','男','特训营24期'),(1003,'郭香香','女','特训营24期');
```

#### 2.2 合并树家族

##### MergeTree

> Clickhouse 中最强大的表引擎当属 `MergeTree` （合并树）引擎及该系列（`*MergeTree`）中的其他引擎。
>
> `MergeTree` 系列的引擎被设计用于插入极大量的数据到一张表当中。数据可以以数据片段的形式一个接着一个的快速写入，数据片段在后台按照一定的规则进行合并。相比在插入时不断修改（重写）已存储的数据，这种策略会高效很多。
>
> 主要特点:
>
> - 存储的数据按主键排序。
>
>   这使得您能够创建一个小型的稀疏索引来加快数据检索。
>
> - 如果指定了 [分区键](https://clickhouse.com/docs/zh/engines/table-engines/mergetree-family/custom-partitioning-key) 的话，可以使用分区。
>
>   在相同数据集和相同结果集的情况下 ClickHouse 中某些带分区的操作会比普通操作更快。查询中指定了分区键时 ClickHouse 会自动截取分区数据。这也有效增加了查询性能。
>
> - 支持数据副本。
>
>   `ReplicatedMergeTree` 系列的表提供了数据副本功能。更多信息，请参阅 [数据副本](https://clickhouse.com/docs/zh/engines/table-engines/mergetree-family/replication) 一节。
>
> - 支持数据采样。
>
>   需要的话，您可以给表设置一个采样方法。

```markdown
# 建表语句规范：
CREATE TABLE [IF NOT EXISTS] [db.]table_name [ON CLUSTER cluster]
(
    name1 [type1] [DEFAULT|MATERIALIZED|ALIAS expr1] [TTL expr1],
    name2 [type2] [DEFAULT|MATERIALIZED|ALIAS expr2] [TTL expr2],
    ...
    INDEX index_name1 expr1 TYPE type1(...) GRANULARITY value1,
    INDEX index_name2 expr2 TYPE type2(...) GRANULARITY value2
) ENGINE = MergeTree()
ORDER BY expr
[PARTITION BY expr]
[PRIMARY KEY expr]
[SAMPLE BY expr]
[TTL expr [DELETE|TO DISK 'xxx'|TO VOLUME 'xxx'], ...]
[SETTINGS name=value, ...]


# 案例
# 建表语句
	create table goods_orders (id String,uname String,goods_name String,price Int64,date Date32) ENGINE = MergeTree() order by date PARTITION BY date;
	
# 插入语句 
	insert into goods_orders values ('1001','尚平','oppo手机',7000,'2023-11-21'),('1002','汪权','机械革命电脑',10000,'2023-11-22'),('1003','丁义杰','iphone14',5000,'2023-11-21'),('1004','黄杰','AI吸尘器',17000,'2023-11-22');
	
	insert into goods_orders values ('1005','丁仕祥','小天才手表',8000,'2023-11-22'),('1006','陈叶芯','投影仪',20000,'2023-11-21'),('1007','刘志龙','水杯',20,'2023-11-22'),('1008','黄磊','iwatch',3000,'2023-11-21');
```

> 注意：默认是针对每一批数据按照分区字段的值进行分区

![image-20230526155256411](C:\Users\ASUS\Desktop\Clickhouse-23.2.1.2537 学习.assets\image-20230526155256411.png)

> 根据上图所示，并不会立刻的将所有的相同的分区进行合并，如果想要很快的看到结果，可以手动的进行合并

```sql
optimize table 表名 final;

optimize table goods_orders final;
```

> 手动合并后结果/或者是过一段时间自动合并结果

![image-20230526155449499](C:\Users\ASUS\Desktop\Clickhouse-23.2.1.2537 学习.assets\image-20230526155449499.png)

> 今后开发的时候，常用的表引擎：针对数据量小的表引擎用TinyLog, 数据量大表引擎就用MergeTree

## 四、常用函数

### 4.1 算术函数

> 对于所有算术函数，结果类型为结果适合的最小数值类型（如果存在这样的类型）。最小数值类型是根据数值的位数，是否有符号以及是否是浮点类型而同时进行的。如果没有足够的位，则采用最高位类型。简单理解：会自动的根据我们的数值大小，来选用最适合的数据类型存储。

```markdown
# plus(a, b), a + b operator
计算数值的总和。 您还可以将Date或DateTime与整数进行相加。在Date的情况下，和整数相加整数意味着添加相应的天数。对于DateTime，这意味着添加相应的秒数。

# minus(a, b), a - b operator
计算数值之间的差，结果总是有符号的。

您还可以将Date或DateTime与整数进行相减。见上面的’plus’。

# multiply(a, b), a * b operator
计算数值的乘积。

# divide(a, b), a / b operator
计算数值的商。结果类型始终是浮点类型。 它不是整数除法。对于整数除法，请使用’intDiv’函数。 当除以零时，你得到’inf’，‘- inf’或’nan’。

# intDiv(a,b)
计算数值的商，向下舍入取整（按绝对值）。 除以零或将最小负数除以-1时抛出异常。

# max2(a,b)
value1 — 第一个值，类型为Int/UInt或Float。
value2 — 第二个值，类型为Int/UInt或Float。

# max2(value1, value2)
value1 — 第一个值，类型为Int/UInt or Float。
value2 — 第二个值，类型为Int/UInt or Float。
```

![image-20230526160302944](C:\Users\ASUS\Desktop\Clickhouse-23.2.1.2537 学习.assets\image-20230526160302944.png)

### 4.2 比较函数

> 比较函数始终返回0或1（UInt8）。
>
> 可以比较以下类型：
>
> - 数字
> - String 和 FixedString
> - 日期
> - 日期时间
>
> 以上每个组内的类型均可互相比较，但是对于不同组的类型间不能够进行比较。
>
> 例如，您无法将日期与字符串进行比较。您必须使用函数将字符串转换为日期，反之亦然。
>
> 字符串按字节进行比较。较短的字符串小于以其开头并且至少包含一个字符的所有字符串。

```markdown
等于，a=b和a==b 运算符
不等于，a!=b和a<>b 运算符
少, < 运算符
大于, > 运算符
小于等于, <= 运算符
大于等于, >= 运算符
```

### 4.3 数据类型转换

> 当你把一个值从一个类型转换为另外一个类型的时候，你需要注意的是这是一个不安全的操作，可能导致数据的丢失。数据丢失一般发生在你将一个大的数据类型转换为小的数据类型的时候，或者你把两个不同的数据类型相互转换的时候。



