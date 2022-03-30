# Linux配置JavaEE开发环境

#### 1、JDK1.8安装

```
步骤一：
	在/opt/下创建jdk目录：mkdir /opt/jdk
步骤二：
	通过xftp将文件包上传到/opt/jdk目录下
步骤三：
	切换到/opt/jdk目录下并解压
	cd /opt/jdk
	tar -zxvf jdk包名/tar.gz
步骤四：
	在/usr/local下创建jdk目录
	mkdir /usr/local/jdk
步骤五：
	将解压后的文件移动到/usr/local/jdk
	mv /opt/jdk/jdk文件名 /usr/local/jdk
步骤六：
	设置环境变量
	vim /etc/profile
	在文件末尾加上：
	export JAVA_HOME=/usr/local/jdk/jdk文件名
	export PATH=$JAVA_HOME/bin:$PATH
步骤七：
	让新的环境变量生效
	source /etc/profile
	
测试：
	javac -version
	java -version
```

#### 2、tomcat安装

```
步骤一：
	在/opt下新建tomcat目录：mkdir /opt/tomcat/
步骤二：
	通过xftp将文件包传入到/opt/tomcat目录下
步骤三：
	解压文件包:tar -zxvf 文件名.tar.gz
步骤四：
	进入解压后的bin目录,启动tomcat
	./startup.sh
步骤五：
	开放端口8080
	firewall-cmd --permanent --add-port=8080/tcp
	firewall-cmd --reload

测试：
	在windows下访问：IP号:8080
```

#### 3、IDEA安装

```
步骤一：
	在/opt下新建IDEA目录:mkdir IDEA
步骤二：
	下载文件并解压
步骤三：
	在图形化界面运行./idea.sh
步骤四：破解
	网上找破解码
```

#### 4、mysql安装

```
1.新建文件夹/opt/mysql，并cd进去
2.运行wget http://dev.mysql.com/get/mysql-5.7.26-1.el7.x86_64.rpm-bundle.tar，下载mysql安装包
3.解压
4.centos7.6自带的类mysql数据库是mariadb，会跟mysql冲突，要先删除。
5.运行rpm -qa|grep mari，查询mariadb相关安装包
6.运行rpm -e --nodeps mariadb-libs，卸载
7.然后开始真正安装mysql，依次运行以下几条
    rpm -ivh mysql-community-common-5.7.26-1.el7.x86_64.rpm
    rpm -ivh mysql-community-libs-5.7.26-1.el7.x86_64.rpm
    rpm -ivh mysql-community-client-5.7.26-1.el7.x86_64.rpm
    rpm -ivh mysql-community-server-5.7.26-1.el7.x86_64.rpm
8.运行systemctl start mysqld.service，启动mysql
9.然后开始设置root用户密码
	Mysql自动给root用户设置随机密码，运行grep "password" /var/log/mysqld.log可看到当	前密码
10.运行mysql -u root  -p，用root用户登录，提示输入密码可用上述的，可以成功登陆进入mysql命令行
11.设置root密码，对于个人开发环境，如果要设比较简单的密码（生产环境服务器要设复杂密码），可以运行set global validate_password_policy=0;  提示密码设置策略
（validate_password_policy默认值1，）
12.set password for 'root'@'localhost' =password('hspedu100');
13.运行flush privileges;使密码设置生效
```

