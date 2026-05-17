
1、不关闭NetworkManager

```bash
管理网络有两个服务：
	（1）network         默认使用，通过network正常使用网卡
	（2）NetworkManager  默认开启，需要关闭和禁止开机运行
	
		若不关闭NetworkManager，会争抢网络控制权，初始未对NetworkManager进行IP地址配置，使用服务器过程中，IP会变为空
```

2、SSH连接优化

```bash
1.SSH服务   能让我们使用远程连接工具连接服务器，默认开启

	优化远程连接速度：
		（1）修改配置文件（将UseDNS改成no）
			[root@breadbomb ~]# grep UseDNS /etc/ssh/sshd_config
			#UseDNS yes
			UseDNS no
		
		（2）重启SSH服务
			systemctl restart sshd
	
	正向解析：将域名解析成IP
	反向解析：将IP解析成域名
	
	查看公网IP:
		curl cip.cc
```

3、字符集优化

```bash
1.作用：可以让中文在Linux系统中正常显示

2.常用字符集：
	（1）UTF-8
	（2）GBK
	系统默认字符集必须和远程连接工具（xshell/CRT）一致

3.查看系统字符集：
	echo $LANG
	
	示例：
	[root@breadbomb ~]# echo $LANG
	en_US.UTF-8 #语言.编码
	
	a.临时修改：
		LANG='zh-CN.UTF-8'
	b.永久修改：
		/etc/locale.conf
		
		示例：
		[root@breadbomb ~]# cat /etc/locale.conf
		LANG="en_US.UTF-8"
```

4、PATH变量

```bash
1.作用：执行命令时会使用PATH变量中的路径

[root@breadbomb ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin

2.查看命令的绝对路径：
	which 命令
	
	示例：
	[root@breadbomb ~]# which pwd
	/usr/bin/pwd

3.查看登录用户名称：
	whoami
	
	示例：
	[root@breadbomb ~]# whoami
	root

4.命令执行流程：
	（1）用户输入命令
	（2）系统自动查找PATH路径是否有用户输入的命令
	（3）如果存在，则执行命令返回结果
	（4）如果不存在，提示command not found
	
	绝对路径执行命令：
		[root@breadbomb ~]# /usr/bin/echo 'hello'
		hello
	
	永久生效：将变量写入/etc/profile

```