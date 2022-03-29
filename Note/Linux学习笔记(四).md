# Linux学习笔记(四)

#### 1、桥接模式



#### 2、NAT模式



#### 3、仅主机模式



#### 4、网络配置

```
Linux查看网络配置：ifconfig
Windows查看网络配置：ipconfig
ping 目的主机 （测试当前服务器是否可以连接目的主机）
```

```
方法一、自动获取
	linux启动后会自动获取IP,缺点是每次自动获取的ip地址可能不一样。
```

```
方法二、指定ip
	修改配置文件：
		vim /etc/sysconfig/network-scripts/ifcfg-ens33
		修改：
			BOOTPROTO=static
		增加：
			IPADDR=192.168.145.128  #Ip地址
			GATEWAY=192.168.145.2  #网关
			DNS1=192.168.145.2  #域名解析器
```

```
重启网络服务或者重启系统生效
	service network restart
	reboot
```

5、设置主机名和hosts映射

```
设置主机名：
	linux查看主机名：hostname
	修改文件 /etc/hostname 写入修改后的主机名
	重启后生效
```

```
设置hosts映射
	1.通过主机名能够找到某个linux系统
		在C:Windows\System32\drivers\etc\hosts文件指定即可
		案例: 192.168.200.130 hspedu100
	2.通过主机名找到windows系统
		在/etc/hosts 文件指定
```

