# Flink-流数据分析工具使用指南

# 商品链接

[Flink-流数据分析工具](https://marketplace.huaweicloud.com/contents/992480da-64a3-4ba8-90cb-686d1832e96a#productid=OFFI1111485128289529856)

# 商品说明

Apache Flink 是一个开源的分布式流处理框架，专为大规模数据处理设计，支持流处理和批处理一体化。它能够在无界和有界数据流上进行有状态计算，具有高吞吐量、低延迟的特性，广泛应用于实时数据处理场景。

本商品通过 鲲鹏服务器 + Huawei Cloud EulerOS 2.0 64bit 进行安装部署，新增对 GaussDB 的实时写入与实时采集。

# 商品购买

您可以在云商店搜索 **Flink-流数据分析工具**。

其中，地域、规格、推荐配置使用默认，购买方式根据您的需求选择按需/按月/按年，短期使用推荐按需，长期使用推荐按月/按年，确认配置后点击“立即购买”。

下面以按需方式举例:

![](images/img.png)

![](images/img2.png)

![](images/img3.png)

# 商品使用

## Flink 使用

### 采用 Flink-connector-jdbc 的方式写入 GaussDB
1. 环境准备。

a. GaussDB 数据库实例购买以及库表创建：
```shell
# 以下为测试代码示例

# 创建db：test_db
create database test_db;

# 创建schema：player
create schema player;

# 创建表：players3
CREATE TABLE players3 (
player_id INT,
team_id INT,
player_name VARCHAR,
height VARCHAR,
update_time timestamp,
PRIMARY KEY (player_id) NOT ENFORCED
);
```

b.启动 Flink 服务（本镜像采用的是 Flink 1.17版本）：
```shell
cd /opt/module/flink-1.17.0/bin/
./start-cluster.sh
```

2. 将数据写入 GaussDB。

a. 切换目录：
```shell
cd /opt/module/flink-1.17.0/bin/
```

b. 启动 `flink-sql` 服务：
```shell
./sql-client.sh embedded
```

c. 写入 GaussDB 测试：
```shell
# 以下为测试代码示例

CREATE TABLE players3 (
player_id INT,
team_id INT,
player_name VARCHAR,
height VARCHAR,
update_time timestamp,
PRIMARY KEY (player_id) NOT ENFORCED
) WITH (
'connector' = 'jdbc',
'url' = 'jdbc:gaussdb://1.1.1.1:8000/db?currentSchema=schema',
'username' = 'user',
'password' = '123456',
'table-name' = 'players3');

insert into players3 (player_id,team_id,player_name) values (6001,6001,'6001'),(6002,6002,'');

select * from players3;
```

d. 插入成功:

![](images/img4.png)

### 采用 Flink-connector-cdc 的方式从 GaussDB写入 Doris

1. 连接配置文档，建议目录 `/root/myconfig.txt`。
```shell
# 以下为 GaussDB 配置

hostname = *.*.*.*
# GaussDB 的用户名
gauss_username = username
# GaussDB 的密码
gauss_password = *****
# GaussDB 的数据库名称
gauss_database = databasename
# GaussDB 的 source 表名：模式名称.表名 或者 模式名称.*  (全表)
white_table_list = *.*
gauss_replication_mode = 1
# GaussDB 的 source 复制槽
gauss_replication_slot = flink
# GaussDB 的 source 并行度
parallel_decode_num = 10
# GaussDB 的 source 批大小
sending_batch = 0

# 以下为 Doris 配置
# Doris 的 jdbc
doris_jdbc = jdbc:mysql://*.*.*.*:9030/database?rewriteBatchedStatements=true
# Doris 的用户名
doris_username = username
# Doris 的密码
doris_password = ******
```

2. 准备 `flink` 环境。

a. 新环境先删两个文件，`/root/.ssh` 下的 `known_hosts  known_hosts.old`。

b. 启动 flink 环境，运行时输入你创建服务器密码：
```shell
/opt/module/flink-1.17.0/bin/start-cluster.sh
```

c. 启动 `GaussToDorisAuto` 程序：
```shell
/opt/module/flink-1.17.0/bin/flink run -m *.*.*.*:8081 -c com.gaussdb.process.GaussToDorisAuto /root/GaussCDCToDoris-1.0-SNAPSHOT.jar --filePath /root/myconfig.txt
```

d. 在 GaussDB 数据库新增数据，查看 Doris 是否同步（Doris 表结构需最后多一个名称是 `op_type_column`，类型是 `VARCHAR(50)` 的字段）

## 参考文档
- [Flink 官网](https://flink.apache.org/)

更多问题可通过 [**issue**](https://github.com/HuaweiCloudDeveloper/flink-image/issues) 或 **华为云云商店指定商品的服务支持** 与我们取得联系。
