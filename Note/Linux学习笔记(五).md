# Linux学习笔记(五)

#### 1、查看系统目前有哪些正在执行，以及它们的执行状况

```
ps 选项
```

```
选项说明：
	-a ：显示当前终端的所有进程信息
	-u ：以用户的格式显示进程信息
	-x ：显示后台进程运行的参数
	-e ：显示所有进程
	-f ：全格式
```

```
参数说明：
	System V	展示风格
	USER :		用户名称
	PID :		进程号
	%CPU :		进程占用CPU的百分比
	%MEM :		进程占用物理内存的百分比
	VSZ :		进程占用的虚拟内存大小(单位:KB)
	RSS :		进程占用的物理内存大小(单位:KB)
	TT :		终端名称,缩写
	STAT :		进程状态，其中'S-睡眠，s-表示该进程是会话的先导进程，N-表示进程拥有比普通				优先级更低的优先级，R-正在运行，D-短期等待，Z-僵死进程，T-被跟踪或者被停				止等等
	STARTED :	进程的启动时间
	TIME :		CPU时间，即进程使用CPU的总时间
	COMMAND :	启动进程所用的命令和参数，如果过长会被截断显示

```

#### 2、终止进程

```
kill 选项 进程号    通过进程号终止进程
killall 进程名称      通过进程名称终止进程
```

```
选项说明：
	-9 ：表示强迫进程立即停止
```

#### 3、查看进程树

```
pstree 选项
```

```
选项说明：
	-p ：显示进程的PID
	-u ：显示进程的所属用户
```

#### 4、服务管理指令

```
service 服务名 [start|stop|restart|reload|status]
```

```
说明：
	在CentOS7.0后很多服务不再使用service ,而是 systemctl
	service指令管理的服务在/etc/init.d查看
```

#### 5、查看服务名

```
方式一：
	使用setup指令
	选择系统服务，可以看到全部。
	带*号的表示自启动，可以通过空格键进行更改
	按tab键切换光标，然后按enter确认退出
```

```
方式二：
	在/etc/init.d查看
```

#### 6、开机流程

```
开机 -> BIOS -> /boot -> systemd进程1 -> 运行级别 -> 运行级别对应的服务
```

#### 7、给服务指定运行级别

```
查看所有服务： chkconfig --list 
查看具体某个服务： chkconfig 服务名 --list
给服务指定运行级别：chkconfig --level 5 服务名 on/off
需要重启机器后生效
```

```
示例：
	对network服务进行各种操作，把network在3运行级别,关闭自启动
	chkconfig --level 3 network off
	chkconfig --level 3 network on
```

#### 8、systemctl管理指令

```
systemctl [start|stop|restart|status] 服务名
```

```
systemctl list-unit-files [| grep服务名](查看服务开机启动状态, grep可以进行过滤)
systemctl enable 服务名(设置服务开机启动)
systemctl disable 服务名(关闭服务开机启动)
systemctl is-enabled 服务名(查询某个服务是否是自启动的)
```

#### 9、防火墙打开或者关闭指定端口

```
打开端口:	firewall-cmd --permanent--add-port=端口号/协议
关闭端口:	firewall-cmd --permanent --remove-port=端口号/协议
重新载入,才能生效: 	firewall-cmd --reload
查询端口是否开放:	firewall-cmd --query-port=端口/协议
```

#### 10、动态监控进程

```
top 选项
```

```
选项说明：
	-d秒数	指定top命令每隔几秒更新。默认是3秒
	-i		 使top不显示任何闲置或者僵死进程。
    -p		 通过指定监控进程ID来仅仅监控某个进程的状态。
```

```
交互操作说明：
	p	以CPU使用率排序，默认就是此项
	M	以内存的使用率排序
	N	以PID排序
	q	退出top
```

#### 11、监控网络状态

```
netstat 选项
```

```
选项说明：
	-an		按一定顺序排列输出
	-p		显示哪个进程在调用
```

#### 12、rpm

```
查询已安装的rpm列表：	rpm -qa
查询软件包是否安装：	   rpm -q 软件报包名
查询软件包信息：		rpm -qi 软件包名
查询软件包中的文件：	   rpm -ql 软件包名
查询文件所属的软件包：	  rpm -qf 文件的全路径名
```

```
卸载rpm包：
	rpm -e 包名
```

```
安装rpm包：
	rpm -ivh 包名
	
	i ：install安装
	v ：verbose提示
	h ：hash进度条
```

#### 13、yum

```
查询yum服务器是否有需要安装的软件 ：	yum list | grep xx软件列表
安装指定yum包 ：	yum install 包名
```