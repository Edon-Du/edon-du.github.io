#### 环境准备

- canal 服务器 centos8
  - CPU: 2
  - RAM: 4096M
- 业务数据库服务器一
  - CPU: 1
  - RAM: 2048M
  - 采用mysql8
- 业务数据库服务器二
  - CPU: 1
  - RAM: 2048M
  - 采用mysql8

##### 搭建canal-deployer服务

- 用于伪装mysql从库，从主库拉去binlog,解析后获取数据流
- 参考地址
  - https://github.com/alibaba/canal/wiki/QuickStart
  - https://my.oschina.net/u/3095034/blog/3018150

##### 搭建canal-adapter适配器

- 监听canal-deployer指定的instance拉取数据流
- 创建不同的适配器配置文件，来同步指定的表或指定的字段
- mysql8需更换/lib下的mysql-connector-java为8.x版本
- 参考地址
  - https://github.com/lisonz/canal/tree/master/client-adapter

##### 搭建canal-admin进行服务实例web可视化

- 参考地址
  - https://github.com/alibaba/canal/wiki/Canal-Admin-QuickStart

- 采用mysql7

  ```mysql
  #查询并设置Server接受的数据包大小
  SHOW VARIABLES LIKE '%max_allowed_packet%';
  ```

##### linux使用到命令

```shell
#kill掉指定端口进程
kill -9 $(netstat -tlnp | grep :8089 | awk '{print $7}' | awk -F '/' '{print $1}')
#查询端口占用情况
netstat -anp|grep 8089
```



