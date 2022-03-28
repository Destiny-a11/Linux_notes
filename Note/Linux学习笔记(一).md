# Linux学习笔记

#### 1、查看当前目录的绝对路径

```
pwd
```

#### 2、查看目录和文件ls

```
ls 选项 目录/文件
```

```
选项：
	-a ：显示当前目录所有文件和目录，包括隐藏的
	-l ：以列表的方式显示信息
```

#### 3、新建目录

```
mkdir 选项 目录名
```

```
选项：
	-p ：创建多级目录
```

```
示例：
	1.在/home下新建目录temp
		mkdir /home/temp
	2.在/home下创建animal目录，并在animal下创建cat目录
		mkdir -p /home/animal/cat
```

#### 4、新建文件

```
touch 文件名
```

```
示例：
	1.在/home下创建Hello.txt文件
		touch /home/Hello.txt
```

#### 5、删除空目录

```
rmdir 目录
```

#### 6、删除目录/文件

```
rm 选项 目录
```

```
选项：
	-r ：递归删除整个文件夹
	-f ：强制删除不提示
```

#### 7、拷贝文件/目录

```
cp 选项 原文件/目录 目标目录
```

```
选项：
	-r ：递归复制整个文件夹
```

```
示例：
	1.将/home/hello.txt拷贝到/home/bbb目录下
		cp /home/hello.txt /home/bbb
	2.将/home/bbb整个目录拷贝到/opt目录下
		cp -r /home/bbb /opt
注意：
	强制覆盖不提示的方法：\cp
	例如：在次将/home/bbb整个目录拷贝到/opt目录下
		\cp -r /home/bbb /opt
```

#### 8、移动目录/重命名

```
mv 原目录/文件 目标目录/文件
```

```
注意： 原目录/文件与目标目录/文件相同即为重命名
示例：
	1.将/home/cat.txt 重命名为 pig.txt
		mv /home/cat.txt /home/pig.txt
	2.将/home/pig.txt 移动到 /root目录下
		mv /home/pig.txt /root
	3.将/opt目录下的bbb整个目录移动到/home目录下
		mv /opt/bbb /home
```

#### 9、查看文件内容

```
cat 选项 文件
```

```
选项：
	-n ：显示行号
注意：该命令只能查看文件不能修改文件
```

#### 10、查看文件内容

```
more 文件
```

```
操作说明：
	操作				功能说明
	----------------------------------------
	空白键(space)		代表向下翻一页
	Enter			  代表向下翻[一行]
	q				  代表立刻离开more ，不再显示该文件内容
	Ctrl+F			  向下滚动一屏
	Ctrl+B            返回上一屏
	=				  输出当前行的行号
	:f   			  输出文件名和当前行的行号
```

#### 11、查看文件内容

```
less 文件
```

```
操作说明：
	操作					功能说明
	---------------------------------------
	空白键			   	   向下翻动一页;
	[pagedown]			 向下翻动一页;
	[pageup]			 向上翻动一页;
	/字串					向下搜寻『字串』的功能;n:向下查找;N:向上查找;
	?字串					向上搜寻『字串』的功能;n:向上查找;N:向下查找;
	q					 离开less这个程序;

```

#### 12、查看文件开头部分

```
head 选项 文件
```

```
注意：
	默认查看前10行
选项：
	-n num：查看前num行
```

```
示例：
	1.查看/etc/profile前10行内容
		head /etc/profile
	2.查看/etc/profile前5行内容
		head -n 5 /etc/profile
```

#### 13、查看文件末尾部分/监视文件更新

```
tail 选项 文件
```

```
注意：
	默认查看倒数10行
选项：
	-n num：查看倒数num行
	-f ：实时追踪文件的所有更新
```

```
示例：
	1.查看/etc/profile后10行内容
		tail /etc/profile
	2.查看/etc/profile后5行内容
		tail -n 5 /etc/profile
	3.监控/home/mydate.txt更新
		tail -f /home/mydate.txt
```

#### 14、输出内容到控制台

```
echo 内容
```

```
示例：
	1.输出hello到控制台
		echo “hello”
```

#### 15、输出定向和追加

```
输出定向：内容 > 文件
追加：内容 >> 文件
```

```
示例：
	1.将/home目录详细信息写入到/home/1.txt文件中
		ls -l > /home/1.txt
	2.将日历信息追加到/home/1.txt文件中
		cal >> /home/1.txt
```

#### 16、软连接/符号连接

```
ln -s 原文件/目录 软连接名
```

```
示例：
	1.在/home目录下创建一个软连接myroot连接到/root目录
		ln -s /root /home/myroot
	2.删除软连接
		rm -f /home/myroot
```

#### 17、查看历史命令

```
history
```

#### 18、压缩和解压（gzip/gunzip）

```
压缩文件：gzip 文件
解压文件：gunzip 文件.gz
```

```
注意：
	只能压缩文件不能压缩目录
示例：
	1.将/home/1.txt压缩
		gzip /home/1.txt
	2.解压/home/1.txt.gz
		gunzip /home/1.txt.gz
	
```

#### 19、压缩和解压（zip/unzip）

```
压缩文件：zip 选项 压缩后文件名.zip 原文件/目录 
解压文件：unzip 选项 压缩文件名.zip
```

```
zip选项：
	-r ：递归压缩整个文件夹
unzip选项：
	-d 目录 ：指定解压后文件的存放目录
```

```
示例：
	1.压缩/home/bbb整个目录
		zip -r bbb.zip bbb
	2.解压
		unzip -d /home/ccc bbb.zip
```

#### 20、压缩和解压tar

```
tar 选项 文件名.tar.gz 打包内容
压缩：tar -zcvf 打包后文件名.tar.gz 需要打包的内容
接压：tar -zxvf 打包文件名.tar.gz -C 解压到指定目录
```

```
选项						功能
-c						 产生.tar打包文件
-v 						 显示详细信息
-f						 指定压缩后的文件名
-z						 打包同时压缩
-x						 解包.tar文件
```

```
示例：
	1.将/home.pig.txt 和 /home/cat.txt 压缩成 pc.tar.gz
		tar -zcvf pc.tar.gz /home/pig.txt /home/cat.txt
	2.将pc.tar.gz 解压到/home/bbb目录
		tar -zxvf pc.tar.gz -C /home/bbb
```

#### 21、显示当前时间

```
date
```

```
1) date								(功能描述:显示当前时间)
2) date "+%Y"						(功能描述:显示当前年份)
3) date "+%m"						(功能描述;显示当前月份)
4)date "+%d"						(功能描述:显示当前是哪一天)
5) date "+%Y-%m-%d %H:%M:%S"		(功能描述:显示年月日时分秒)

```

#### 22、设置当前时间

```
date -s 字符串时间
```

```
例如：
	1.设置系统当前时间为2020-11-03 20:02:10
		date -s "2020-11-03 20:02:10"
```

#### 23、查看日历

```
cal 选项
```

```
注意：
	不加选项表示当月日历
示例：
	1.显示2022年日历
		cal 2022
```

#### 24、搜索查找(find)

```
find 搜索范围 选项
```

```
说明：find指令从指定目录向下递归的遍历各个子目录，将满足条件的文件或目录显示在终端
选项：
	-name 查询方式				按照指定的文件名查找模式查找文件
	-user 用户名				 查找属于指定用户名所有文件
	-size 文件大小				按照指定的文件大小查找文件。
```

```
示例：
	1.按文件名查找，在/home目录下查找hello.txt
		find /home -name hello.txt
	2.在/home目录下查找大于1M的文件
	（注意：+：大于，-：小于，不写表示等于）
		find /home -size +1M
```

#### 25、定位指令（locate）

```
locate 需要搜索的文件
```

```
说明：
	由于locate 指令基于数据库进行查询，所以第一次运行前，必须使用updatedb 指令创建locate数据库。
```

#### 26、过滤查找（grep）和管道符号（|）

```
grep 选项 查找的内容
管道符号(|)表示将前一个命令的处理结果输出传递给后面的命令处理。
```

```
选项：
	-n 显示匹配行及行号
	-i 忽略字母大小写
```

```
示例：
	1.在hello.txt文件中查找yes所在行
		cat /home/hello.txt | grep -n "yes"
```



