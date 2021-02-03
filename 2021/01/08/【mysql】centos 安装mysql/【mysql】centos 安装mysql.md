# 【mysql】centos 安装mysql

mysql是我们最常用的开源的关系型数据库，mysql不同版本有时候安装的方式也不尽相同，下面以mysql5.7.28版本为例梳理一下安装细节：

1.下载mysql-5.7.28，URL：https://downloads.mysql.com/archives/community/ 我这里下载的是64位版本

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206223141847-158152537.png)

 下载后文件为：mysql-5.7.28-linux-glibc2.12-x86_64.tar.gz

 

\2. 卸载自带的mariadb和mysql

检查是否安装了mariadb和mysql，有时候默认安装了

```
rpm -qa | grep mariadb
rpm -qa | grep mysql
```

如果没有，就可以安装mysql，如果有，需要先卸载（remove后为上面命令查询到的内容，全文件名，我这里没有，没法展示）

```
yum remove mariadb-xxx
```

 

3.解压文件，修改目录名方便配置

```
tar -zxvf mysql-5.7.28-linux-glibc2.12-x86_64.tar.gz -C /opt/soft/
cd /opt/soft
mv mysql-5.7.28-linux-glibc2.12-x86_64 mysql-5.7.28
```

 

4.在/usr/local/目录下创建到/opt/soft/mysql-5.7.28的软链接

```
cd /usr/local
ln -s /opt/soft/mysql-5.7.28 mysql
```

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206223541446-246835672.png)

 

5.添加mysql用户，修改mysql目录权限，并用此用户执行应用

```
useradd -s /bin/false -M mysql
cd /opt/soft
chown -R mysql:mysql mysql-5.7.28
```

 

6.拷贝配置文件，将mysql的配置文件拷贝为/etc/目录下的my.cnf，并修改配置文件

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
vim /etc/my.cnf[mysqld]
# binlog 配置
log-bin=/usr/local/mysql/logs/mysql-bin.log
expire-logs-days=14
max-binlog-size=500M
server-id=1
# GENERAL
basedir=/usr/local/mysql
datadir=/usr/local/mysql/data
socket=/usr/local/mysql/mysql.sock
user=mysql
default-storage-engine=InnoDB
character-set-server=utf8lower_case_table_names = 1explicit_defaults_for_timestamp=true
[mysqld_safe]
log-error=/usr/local/mysql/mysql-error.log
pid-file=/usr/local/mysql/mysqld.pid
[client]
socket=/usr/local/mysql/mysql.sock
[mysql]
default-character-set=utf8
socket=/usr/local/mysql/mysql.sock
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

7.安装mysql，进入mysql目录执行以下命令

```
cd /opt/soft/mysql-5.7.28
bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
```

如果出现如下错误，说明需要安装依赖包：

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206204025053-609859232.png)

 安装autoconf依赖包：

```
yum -y install autoconf
```

再次执行脚本

如果出现以下错误，说明在my.cnf中指定的binlog配置文件的logs文件夹不存在：

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206204921524-155353802.png)

 在/usr/local/mysql/下创建logs文件夹就行了，并改为mysql用户

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206205102036-2078103300.png)

再次执行脚本

出现以下信息，代表成功，要保存一下密码，

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206225227432-756771816.png)

 

8.拷贝启动程序，将mysql的启动程序拷贝到/etc/init.d/目录下

```
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld
```

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200205224121762-1591100937.png)

 

 9.安装完，启动mysql服务

```
service mysqld start
```

如果出现如下错误：

```
[root@s144 support-files]# service mysqld start
Starting MySQL.2020-01-31T23:14:27.412533Z mysqld_safe error: log-error set to '/usr/local/mysql/mysql-error.log', however file don't exists. Create writable for user 'mysql'.
 ERROR! The server quit without updating PID file (/usr/local/mysql/data/s144.pid).
```

说明mysql-error.log不存在，手动去创建，并修改权限

```
cd /opt/soft/mysql-5.7.28
touch mysql-error.log
chown mysql:mysql mysql-error.log
```

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206230023984-1929932614.png)

 出现SUCCESS，说明启动成功

 ![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206230211710-1092214077.png)

 

10.配置环境变量，编辑/etc/profile，方便在任何地方用mysql命令

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
vim /etc/profile
```

\#mysql
export MYSQL_HOME=/usr/local/mysql
export PATH=$PATH:$MYSQL_HOME/bin

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

别忘记重新编译 /etc/profile

```
source /etc/profile
```

 

11.登录mysql，修改密码

首次登录没有密码，提示输入密码时，输入第7步安装时生成的密码：p5j2jfX7am.h

```
mysql -uroot -p
```

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206230815269-811672369.png)

 这里要先使用alter user重置密码，不然会报错，我这里 修改mysql root用户密码 为 111111 ：

```
mysql> alter user 'root'@'localhost' identified by '111111';
mysql> flush privileges;
```

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206231601228-1594582365.png)

 至此本机登录密码修改完成，若是想让其他机器访问，需要配置远程访问：

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '111111' WITH GRANT OPTION;
```

使用远程工具测试一下：

![img](https://img2018.cnblogs.com/i-beta/480564/202002/480564-20200206231804083-1287096483.png)

 至此搭建mysql-5.7.28版本就完成了

 

12.一些常用命令 

```
service mysqld start 　　　 #启动
service mysqld stop        #关闭 　　　
service mysqld restart　　  #重启 　　　
service mysqld status 　　  #查看运行状态 
```