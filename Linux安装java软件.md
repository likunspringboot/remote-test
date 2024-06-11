# Linux安装java软件

# 1、CenterOS7.6中安装JDK17

## 1.1、创建opt/jdk目录

```apl
mkdir /opt/jdk
```

![image-20231123212103962](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123212103962.png)

```apl
注意上传的是linux的jdk不要上传window的压缩包
```

```
通过xftp将jdk传输到opt/jdk当中
```

![image-20231123212154027](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123212154027.png)

```apl
然后进入到 opt/jdk目录发现确实存在已经上传的jdk
```

![image-20231123212322073](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123212322073.png)

```apl
tar -zxvf j然后回车即可得到命令进行解压
```

![image-20231123213151266](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123213151266.png)

```apl
输入 ll命令后如下表示安装完成
```

![image-20231123213347445](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123213347445.png)

```apl
创建一个文件夹来管理
mkdir /usr/local/java
移动解压的jdk到这个文件夹当中
mv jdk-17.0.9/ /usr/local/java/
切换目录发现移动成功
cd /usr/local/java/ 

```

![image-20231123213846804](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123213846804.png)

```apl
在cd /usr/local/java/运行 java -version可以查看版本
```

![image-20231123214553121](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123214553121.png)

```apl
配置环境变量：
(1)  vim /etc/profile 打开文件
(2)在文件的最后添加环境变量
export JAVA_HOME=/usr/local/java/jdk-17.0.9
export PATH=$JAVA_HOME/bin:$PATH
```

![image-20231123220031051](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123220031051.png)

```apl
然后通过  source /etc/profile 让文件生效
再使用  echo $PATH 查看是否生效
```

![image-20231123220148570](C:\Users\20195\AppData\Roaming\Typora\typora-user-images\image-20231123220148570.png)



# CenterOS7.6安装tomcat

```apl
1、创建文件夹： mkdir /opt/tomcat
```

```apl
2、将软件上传到Linux
```

![image-20231124084647058](Linux安装java软件.assets/image-20231124084647058.png)

```apl
进入/opt/tomcat 查看是否上传成功
```

![image-20231124084731934](Linux安装java软件.assets/image-20231124084731934.png)



```apl
tar -zxvf a 然后输入Tab可以快速补全。
```

![image-20231124084858458](Linux安装java软件.assets/image-20231124084858458.png)

```apl
cd apache-tomcat-9.0.22/
ls
cd bin/
./startup.sh  //这个表示启动tomcat


```

![image-20231124085322718](Linux安装java软件.assets/image-20231124085322718.png)

```apl
放开8080端口:
sudo firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd  --reload
firewall-cmd --query-port=8080/tcp
```

![image-20231124085914530](Linux安装java软件.assets/image-20231124085914530.png)

```apl
lsof -i :8082 查看 监听端口被谁占用
kill -9 进程号 ：杀死进程
```



# CenterOS7.6安装idea

```apl
创建一个目录：mkdir /opt/idea
```

```apl
将软件传输到 /opt/idea目录下
```

![image-20231124090508623](Linux安装java软件.assets/image-20231124090508623.png)

```apl
cd /opt/idea/
```

![image-20231124090604691](Linux安装java软件.assets/image-20231124090604691.png)

```apl
tar -zxvf ideaIU-2023.2.5.tar.gz 
```

![image-20231124090921669](Linux安装java软件.assets/image-20231124090921669.png)

# CenterOS7.6安装mysql5.7

```apl
新建 mkdir /opt/mysql
进入目录 cd /opt/mysql
传输成功后输入ls查看
```

![image-20231124092733210](Linux安装java软件.assets/image-20231124092733210.png)

![image-20231124162950475](Linux安装java软件.assets/image-20231124162950475.png)



```apl
rpm -qa|grep mari 来看自带的mysql
rpm -e --nodeps mariadb-libs  删除
rpm -e --nodeps marisa 删除
rpm -qa|grep mari
```

![image-20231124093414362](Linux安装java软件.assets/image-20231124093414362.png)



![image-20231124093707019](Linux安装java软件.assets/image-20231124093707019.png)

```apl
解压：tar -xvf mysql-5.7.19-1.el7.x86_64.rpm-bundle.tar 
```

![image-20231124163224667](Linux安装java软件.assets/image-20231124163224667.png)

```apl
开始安装mysql:
rpm -ivh mysql-community-common-5.7.19-1.el7.x86_64.rpm
rpm -ivh mysql-community-libs-5.7.19-1.el7.x86_64.rpm
rpm -ivh mysql-community-client-5.7.19-1.el7.x86_64.rpm
rpm -ivh mysql-community-server-5.7.19-1.el7.x86_64.rpm
```

![image-20231124163812723](Linux安装java软件.assets/image-20231124163812723.png)

```apl
运行 systemctl start mysqld.service 启动mysql
```

![image-20231124164016516](Linux安装java软件.assets/image-20231124164016516.png)

```apl
设置 root用户密码
Mysql自动会给root用户设置随机密码，运行 grep "password" /var/log/mysqld.log 即可查看
运行 mysql -u root -p 用初始密码登录
root密码复杂策略：SET GLOBAL validate_password_policy=LOW; SET GLOBAL validate_password_length=6;
设置密码为123456：  ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
开启访问权限：
GRANT ALL ON *.* TO 'root'@'%' IDENTIFIED BY '123456';

让密码生效：flush privileges;
quit 退出mysql
```

![image-20231124164229907](Linux安装java软件.assets/image-20231124164229907.png)

```apl
 查看 mysql是否启动:  systemctl status mysqld
 启动mysql:          systemctl start mysqld.service
 开机自动启动mysql:   systemctl enable mysqld
 关闭mysql: sudo systemctl stop mysqld.service
如果你想禁用 MySQL 自动启动，可以使用以下命令：sudo systemctl disable mysqld.service
```

![image-20231124170248311](Linux安装java软件.assets/image-20231124170248311.png)

```apl
最后关闭防火墙3306，让window上的navicat可以连接
firewall-cmd --add-port=3306/tcp --permanent
firewall-cmd --reload
firewall-cmd --query-port=3306/tcp

```

<img src="Linux安装java软件.assets/image-20231124173115982.png" alt="image-20231124173115982" style="zoom:67%;" />

# Linux部署项目

```apl
创建目录将jar放到这个目录:
mkdir /usr/local/app
cd /usr/local/app/

启动：java -jar takeaway-0.0.1-SNAPSHOT.jar

ps -ef | grep java  # 找到 Java 进程的 PID
```

![image-20231124174104257](Linux安装java软件.assets/image-20231124174104257.png)

# linux安装redis

```apl
上传安装包到linux中
```

![image-20231130091332061](Linux安装java软件.assets/image-20231130091332061.png)

```apl
解压： tar -zxvf redis-7.0.14\ .tar.gz -C /usr/local
      cd /usr/local
```

![image-20231130091523547](Linux安装java软件.assets/image-20231130091523547.png)

```apl
切换到 cd redis-7.0.14
安装 redis的依赖环境gcc,命令: yum install gcc-c++
```

![image-20231130091807094](Linux安装java软件.assets/image-20231130091807094.png)

```apl
运行 make命令进行编译
```

```apl
切换目录： cd src
运行: make install
```

![image-20231130092040633](Linux安装java软件.assets/image-20231130092040633.png)

## redis启动和停止

```apl
./redis-server 注意需要在redis的src目录下执行
```

![image-20231130092516589](Linux安装java软件.assets/image-20231130092516589.png)

```apl
修改配置
首先 vim redis.conf进入
进入后立即按 /dae即可看到下图
```

![image-20231130093322328](Linux安装java软件.assets/image-20231130093322328.png)

```apl
修改配置如下:将 daemonize no 修改为daemonize yes
```

![image-20231130093521109](Linux安装java软件.assets/image-20231130093521109.png)

```
修改密码：vim redis.conf进入
进入后立即按 /requirepass foobared即可看到下图
```

![image-20231130094200305](Linux安装java软件.assets/image-20231130094200305.png)

```
修改密码为123456
```

![image-20231130094333561](Linux安装java软件.assets/image-20231130094333561.png)

```apl
查看redis是否在后台运行：ps -ef | grep redis
```

![image-20231130094539078](Linux安装java软件.assets/image-20231130094539078.png)

![image-20231130095048256](Linux安装java软件.assets/image-20231130095048256.png)

![image-20231130095256871](Linux安装java软件.assets/image-20231130095256871.png)

```apl
启动服务：src/redis-server ./redis.conf
```

![image-20231130102129181](Linux安装java软件.assets/image-20231130102129181.png)

```apl
修改配置文件，让远程服务器可以连接redis
首先 vim redis.conf 进入
进入后立即按 /bind即可看到下图
```

```apl
将防火墙关闭
#查看6379/tcp端口是否已开
firewall-cmd --zone=public --query-port=6379/tcp
#查看系统所有开放的端口
firewall-cmd --zone=public --list-ports
#配置防火墙，打开8123端口
sudo firewall-cmd --zone=public --add-port=6379/tcp --permanent
#重新启动防火墙
sudo systemctl restart firewalld.service

```

```apl
在windoe中连接：redis-cli.exe -h 192.168.175.130 -p 6379 -a 123456
192.168.175.130 表示Linunx主机地址
6379 表示端口号
123456表示Linuxn设置的密码
```



# mysql读写分离

## 1、环境准备

```
1、准备好两台虚拟机分别安装好Mysql并且使用navicat连接到linux中。
```

<img src="Linux安装java软件.assets/image-20231204173255885.png" alt="image-20231204173255885" style="zoom: 67%;" />

```apl
2、在主库192.168.175.130修改mysql的配置文件
vim /etc/my.cnf
log-bin=mysql-bin #[必须]启用二进制日志
server-id=100 #[必须]服务器唯一ID
```

<img src="Linux安装java软件.assets/image-20231204173731270.png" alt="image-20231204173731270" style="zoom:67%;" />

```apl
重启mysql服务 systemctl restart mysqld
```

![image-20231204173950879](Linux安装java软件.assets/image-20231204173950879.png)

```apl
登录mysql数据库，mysql -u root -p
执行下面的sql语句
GRANT REPLICATION SLAVE ON *.* to 'xiaoming'@'%' identified by 'Root@123456';
注：上面sql的作用是创建一个用户xiaoming,密码是Root@123456,并且授予xiaoming用户REPLICATION SLAVE权限。常用与建立复制
时所需要的用户权限，也就是slave必须被master授权具有该权限的用户，才能通过该用户复制
```

![image-20231204174935464](Linux安装java软件.assets/image-20231204174935464.png)

```apl
登录mysql数据库执行 show master status; 记录结果下的File和Position的值。
注意这时候不要再执行语句了因为file和position会改变接下来我们修改从库的配置
```

![image-20231204175105267](Linux安装java软件.assets/image-20231204175105267.png)

```apl
修改从库的配置
修改mysql的配置文件
vim /etc/my.cnf
配置上：server-id=101 #[必须]服务器唯一ID,主库的ID是100，这里从库我们设置为101
```

<img src="Linux安装java软件.assets/image-20231204175510073.png" alt="image-20231204175510073" style="zoom: 67%;" />

```apl
重启mysql服务 systemctl restart mysqld
```

![image-20231204175641714](Linux安装java软件.assets/image-20231204175641714.png)

```apl
现在开始从库设计：
登录数据库 mysql -u root -p 执行下面语句
change master to
master_host='192.168.175.130',master_user='xiaoming',master_password='Root@123456',master_log_file='mysql-bin.000001',master_log_pos= 133148;
将线程跑起来：
START SLAVE;
停止线程:STOP SLAVE IO_THREAD;


```

![image-20231204190911294](Linux安装java软件.assets/image-20231204190911294.png)

```apl
查看状态：show slave status;
```

```apl
在linux执行：mysqladmin flush-hosts -u root -p
在navicat执行：SET GLOBAL max_connect_errors=10000;

```

![image-20231204224450634](Linux安装java软件.assets/image-20231204224450634.png)

# linux安装nginx



```apl
1、 安装依赖包:  yum -y install gcc pcre-devel zlib-devel openssl openssl-devel 
2、 创建文件夹 mkdir /opt/nginx 
             cd /opt/nginx 并将nginx安装包上传到这个目录
```

![image-20231205144748930](Linux安装java软件.assets/image-20231205144748930.png)

```apl
解压：tar -axvf nginx-1.16.1.tar.gz 
     进入这个目录: cd nginx-1.16.1/
```

![image-20231205144923639](Linux安装java软件.assets/image-20231205144923639.png)

![image-20231205144955862](Linux安装java软件.assets/image-20231205144955862.png)

```apl
 创建目录用来安装nginx的目录： mkdir -p /usr/local/nginx
 安装到/usr/local/nginx中   ./configure --prefix=/usr/local/nginx
 真正安装 make && make install


```

![image-20231205145447600](Linux安装java软件.assets/image-20231205145447600.png)



```apl
切换目录：cd /usr/local/nginx
 安装tree命令       yum install tree
  运行命令来显示树形结构:      tree
```

![image-20231205145730668](Linux安装java软件.assets/image-20231205145730668.png)



## 1、查看版本号

```apl
首先需要确保在sbin目录下：
./nginx -v
```

## 2、检查配置文件的正确性

```apl
./nginx -t
```

![image-20231205150840038](Linux安装java软件.assets/image-20231205150840038.png)

## 3、启动和停止

```apl
启动：./nginx
停止：./nginx -s stop
查看进程 ps -ef | grep nginx
```

![image-20231205151436217](Linux安装java软件.assets/image-20231205151436217.png)

```apl
切换到html目录下
关闭防火墙：systemctl stop firewalld 
          ipaddr 来找到ip地址在浏览者中打开
          
```

<img src="Linux安装java软件.assets/image-20231205151952611.png" alt="image-20231205151952611" style="zoom:50%;" />

<img src="Linux安装java软件.assets/image-20231205152041553.png" alt="image-20231205152041553" style="zoom:50%;" />



```apl
重新加载配置文件：./nginx -s reload
```

## 4、配置环境变量

```apl
回到root目录
进入  vim /etc/profile
追加：PATH=/usr/local/nginx/sbin:$JAVA_HOME/bin:$PATH
让文件生效： source /etc/profile

```

<img src="Linux安装java软件.assets/image-20231205153413395.png" alt="image-20231205153413395" style="zoom:67%;" />

![image-20231205153506999](Linux安装java软件.assets/image-20231205153506999.png)



## 5、启动和停止

```apl
当配置好环境变量后：
启动：nginx
停止：nginx -s stop
查看进程 ps -ef | grep nginx
重新更新conf文件：nginx -s reload

```

## 6、nginx部署静态资源

```apl
1、部署静态资源需要静态资源放到nginx的html目录
2、进入 198.168.175.134 nginx的conf目录配置反向代理即vim.nginx.conf
server{
   listen 82; #监听端口
   server_name localhost; #服务器名称即域名
   location / {
      proxy_pass http://192.168.175.130:8080; #配置反向代理配置，将请求转发到指定服务
   }
}
```

```apl
192.168.175.130 web服务器
```



```apl
配置负载均衡

upstream targetserver{  # targetserver表示一组服务器
    server 192.168.175.130:8081; 
    server 192.168.175.135:8082;
}

server{
   listen 8080; #监听端口
   server_name localhost; #服务器名称即域名
   location / {
      proxy_pass http://targetserver; #配置反向代理配置，将请求转发到指定服务
   }
}

```

















