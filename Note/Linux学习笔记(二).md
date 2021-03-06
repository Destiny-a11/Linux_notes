# Linux学习笔记（二）

#### 1、新建用户、并设置密码

```
useradd 用户名
passwd 用户名
新增用户直接指定组：useradd -g 用户组 用户名 
```

#### 2、删除用户

```
删除用户并保留家目录：userdel 用户名
删除用户并删除家目录：userdel -r 用户名
```

#### 3、查询用户信息

```
id 用户名
```

#### 4、切换用户

```
su - 用户名
```

#### 5、查看当前登录用户

```
who am i
```

#### 6、新增组

```
groupadd 组名
```

#### 7、删除组

```
groupdel 组名
```

#### 8、修改用户的组

```
usermod -g 用户组 用户名
```

#### 9、修改文件的所有者

```
chown 其它用户名 文件/目录名
chown -R 其它用户名 目录名
```

#### 10、修改文件/目录的所在组

```
chgrp 其它组名 文件/目录名
chgrp -R 其它组名 目录名
```

#### 11、权限介绍

```
-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc
0-9位说明
第О位确定文件类型(d,- ,1 , c , b)
l是链接，相当于 windows的快捷方式
d是目录，相当于windows的文件夹
c是字符设备文件，鼠标，键盘
b是块设备，比如硬盘
第1-3位确定所有者（该文件的所有者）拥有该文件的权限。---User
第4-6位确定所属组（同用户组的）拥有该文件的权限，---Group
第7-9位确定其他用户拥有该文件的权限---Other
```

```
[r]代表可读(read):可以读取,查看
[w]代表可写(write)可以修改,但是不代表可以删除该文件,删除一个文件的前提条件是对该文件所在的		目录有写权限，才能删除该文件.
[x]代表可执行(execute);可以被执行
```

#### 12、修改权限

```
chmod
```

```
u:所有者	
g:所有组
o:其他人
a:所有人
```

```
chmod	u=rwx,g=rx,o=x	文件/目录名    //所有者设置读写执行，所有组设置写执行，										 	 //其他人设置执行权限
chmod	o+w	文件/目录名   //给其它人增加写的权限
chmod	a-x	文件/目录名	 //给所有人增加执行的权限
```

#### 13、实时任务调度（crond）

```
crontab 选项
```

```
-e 编辑crontab定时任务
-l 查询crontab任务
-r 删除当前用户所有的crontab任务
```

```
添加任务步骤：
	1.编写任务脚本或者命令
	2.执行 crontab -e
	3.输入脚本文件或者命令 如：*/1**** ls -l /etc > /tmp/to.txt  表示每一分钟执行一次
```

```
占位符说明：
	第一个* ：一个小时当中的第几分钟      0-59
	第二个* ：一天当中的第几个小时	    0-23
	第三个* ：一个月当中的第几天			1-31
	第四个* ：一年当中的第几月			 1-12
	第五个* ：一周当中的星期几			 0-7（0和7都表示星期日）
```

```
特殊符号说明
	* ：代表任何时间，第一个*就代表一小时中每分钟都回执行一次的意思
	, ：代表不连续时间，比如0 8,12,16***命令”，就代表在每天的8点0分，12点0分，16点0分都			执行一次命令
	- ：代表连续的时间范围。比如“0 5 * * 1-6命令”，代表在周一到周六的凌晨5点0分执行命令
	*/n ：代表每隔多久执行一次。比如“*/10 * * * *命令”，代表每隔10分钟就执行一遍命令
```

```
conrtab -r:				终止任务调度。
crontab -l:				列出当前有那些任务调度
service crond restart	[重启任务调度]
```

#### 14、定时任务（at）

```
at 选项 时间
ctrl+d 结束at命令的输入。（按两次ctrl+d）
```

```
注意：at命令是一次性定时计划任务
	 atd守护进程每60秒检查作业队列。
```

```
查看进程：ps -ef
查看atd进程是否启动：ps -ef | grep atd
```

```
at时间指定方法：
	1.以hh:mm（小时:分钟）形式指定，假如时间已经过去，则第二天执行。 例如：04:00
	2.使用midnight、noon、teatime等模糊词语指定
	3.加入AM、PM以12小时制指定。 例如：12pm
	4.指定日期。 例如：04:00 2021-03-01
	5.使用相对计时法。 now+数字+时间单位
	6.使用today、tomorrow来指定
```

```
示例：
	1.两天后的下午五点执行.....
		at 5pm + 2days
```

#### 15、查询系统整体磁盘情况查询

```
df -h
```

#### 16、查询指定目录的磁盘占用情况

```
du 选项 目录
```

```
选项：
	-s 				指定目录占用大小汇总
	-h				带计量单位
	-a				含文件
	--max-depth=1 	子目录深度
	-c				列出明细的同时，增加汇总值
```

```
示例：
	1.查询/opt目录的磁盘占用情况，深度为1
		du -hac --max-depth=1 /opt
```

#### 17、安装以树状显示目录的tree

```
yum install tree
```

#### 18、查询文件/目录个数

```
示例：
	1.统计/opt目录下文件的个数
		ls -l /opt | grep "^-" | wc -l
	2.统计/opt目录下目录的个数
		ls -l /opt | grep "^d" | wc -l
	3.统计/opt目录下文件的个数，包括子目录里的
		ls -lR /opt | grep "^-" | wc -l
	4.统计/opt目录下目录的个数，包括子目录里的
		ls -lR /opt | grep "^d" | wc -l
	5.以树状结构显示/home目录
		tree /home
```

#### 19、虚拟机增加硬盘

```
1.虚拟机添加硬盘
2.分区
3.格式化
4.挂载
5.设置可以自动挂载
```

```
步骤一：（虚拟机添加硬盘）
	在【虚拟机】菜单中，选择【设置】，然后设备列表里添加硬盘，然后一路【下一步】，中间只有选择磁盘大小的地方需要修改，至到完成。然后重启系统（才能识别）!
```

```
步骤二：（分区）
	命令：fdisk /dev/磁盘名（如sdb）
	
	m		显示命令列表
	p		显示磁盘分区同fdisk -1
	n		新增分区
	d		删除分区
	w		与入并退出
	
	开始对/sdb分区：
		开始分区后输入n，新增分区，然后选择p ，分区类型为主分区。两次回车默认剩余全部空间。最后输入w写入分区并退出，若不保存退出输入q。
```

```
步骤三：（格式化）
	命令：mkfs -t ext4(分区类型) /dev/sdb1(磁盘分区名)
```

```
步骤四：（挂载）
	挂载：mount 设备名称 挂载目录
	删除挂载：umount 设备名称/挂载目录
注意：用命令行挂载，重启后悔失效
```

```
步骤五：（设置可以自动挂载）
	永久挂载:通过修改/etc/fstab 实现挂载
	添加完成后执行mount -a即刻生效
```

![1](C:\Users\lihuazhan\Desktop\1.png)

