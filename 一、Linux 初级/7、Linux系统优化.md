
1、知识补充

```bash
1. > 和 >>
	只要可以在屏幕上显示的内容，都可以使用> 和 >> 存放到文件中

2.vim中块模式的操作（常用于批量注释，缩进）
	a.使用crtl+v进行块模式
	b.选中需要修改的几行，点击i或者a
	c.输入需要插入或追加的东西，比如空格
	d.修改完后按两下ESC，会显示修改结果

```

2、系统命令

```bash
1.less #一页一页的查看文件内容，常用于查看大文件
	-N 显示行号
	语法：
		less filename
	操作：
		（1）空格、f  #向下翻一页
		（2）b       #向上翻一页
		（3）/       #搜索内容         n 向下查找  N 向上查找
		（4）q       #退出less命令
		（5）G       #快速到文件尾部    nG 快速到第n行
		（6）g       #快速到文件开头    ng 快速到第n行

2.more #查看文件内容，显示当前百分比
	语法：
		more filename
	操作：
		只支持翻页 空格/f--下一页  b--上一页 q--退出

3.wc #统计
	语法：
		wc filename
	操作：
		（1）直接执行wc filename ,输出：行数 单词数 字节数 文件名
			（2）-l 统计行数
		（3）-w 统计单词数
		（4）-c 统计字节数
		（5）-L 统计最长行的长度（不是单词，是长度，一个一个字母）

4.sort #排序 默认按照第一个数字/字母排序，比如 1 10 2 21 3
	参数：
		-r  #逆序排序
		-n  #按数字大小正序排序
		-k2 #按第二列排序

5.uniq #去重 （只有相邻的可以去重，所以需要提前排序）
	参数：
		-c 去重统计次数
		
	注意：有时候相邻的两行表面上相同，但会多出空格或tab
	     可以使用 cat -A 查看以什么结尾

6.xargs
	参数：
		-n2 按照两列展示

7.systemctl #系统服务操作
	操作：
		systemctl stop 服务    #停止服务
		systemctl start 服务   #开启服务
		systemctl restart 服务 #重启服务
		systemctl enable 服务  #开机自启服务
		systemctl disable 服务 #开机禁止自启服务
		systemctl status 服务  #查看服务状态
		systemctl reload 服务  #重新加载服务
		
```

3、系统优化

```bash
1.查看系统版本
	（1）cat /etc/redhat-release
	（2）hostnamectl
	
	示例：
		[root@breadbomb ~]# cat /etc/redhat-release
		CentOS Linux release 7.9.2009 (Core)
		
		[root@breadbomb ~]# hostnamectl
	   Static hostname: breadbomb
	         Icon name: computer-vm
	           Chassis: vm
	        Machine ID: d03bc42e44a64d90ae01396fa940aefe
	           Boot ID: a18ac63b4ba645f7973bf03991e1c959
	    Virtualization: vmware
	  Operating System: CentOS Linux 7 (Core)          #系统版本
	       CPE OS Name: cpe:/o:centos:centos:7
	            Kernel: Linux 3.10.0-1160.el7.x86_64   #内核版本
	      Architecture: x86-64


2.查看系统的内核版本
	（1）uname -a 显示所有内核信息
	（2）uname -r 显示内核版本
	
	示例：
		[root@breadbomb ~]# uname -a
		Linux breadbomb 3.10.0-1160.el7.x86_64 #1 SMP Mon Oct 19 16:18:59 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
		
		[root@breadbomb ~]# uname -r
		3.10.0-1160.el7.x86_64



3.系统时间同步
	时间分为系统时间和硬件时间，两种时间必须一致
	（1）系统时间
		date #查看系统时间
		
		修改时间：
			date -s 20200101 #将时间修改成2020年1月1日
		
		显示自定义格式时间：
			[root@breadbomb ~]# date +%F-%H-%M-%S
			2026-05-16-21-42-33
		
		同步系统时间：
			ntpdate #同步时间 需要安装 yum -y install ntpdate
			
			ntpdate ntp1.aliyun.com #使用阿里云时间服务器进行同步
		
		
	（2）硬件时间
		clock #查看硬件时间
		
		同步硬件时间：
			hwclock #同步时间
				-w  #将系统时间同步给硬件时间
			
			hwclock -w #系统时间同步给硬件时间


4.关闭Selinux
	Selinux 作用：限制root管理员，需要关闭，并且有《信息安全问题》
	
	Selinux 会开机自启，需要临时+关闭开机自启
	
	（1）查看Selinux
		getenforce #查看Selinux
	（2）临时关闭Selinux
		setenforce 1 | 0 # 1表示开启（Enforcing） 0表示关闭（Permissive）
		setenforce 0
		
		关闭后使用getenforce 查看是否为 Permissive
	（3）关闭开机启动
		/etc/selinux/config
		
		将下面的修改成disabled
			#SELINUX=enforcing
			SELINUX=disabled


5.关闭firewalld
	作用：流量限制 流量分析 攻击行为
	
	（1）查看防火墙状态
		systemctl status firewalld
	
	（2）临时关闭防火墙
		systemctl stop firewalld
	
	（3）禁止开机自动启动
		systemctl disable firewalld
	
	什么时候开启防火墙：
		a.公网
		b.用户可直接访问的服务器 NAT转换 DMZ映射
		c.有公网的云服务器
	什么时候关闭防火墙：
		a.局域网
		b.没有公网IP
		c.内部测试服务器
		d.高并发场景

6.关闭NetworkManager

7.修改默认的YUM仓库 （sl cowsay 娱乐性软件）
	（1）更换阿里云仓库
		a.备份
			mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
		b.安装
			curl -o /etc/yum.repos.d/CentOS-Base.repohttps://mirrors.aliyun.com/repo/Centos-7.repo
		c.查看
			yum repolist

	（2）配置 EPEL 仓库 （wget需要提前安装）
		a.安装
			wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
		b.清除缓存
			yum clean all && yum makecache
		c.查看
			yum repolist | grep epel   # 输出示例：epel/x86_64     Extra Packages

	使用：
		yum -y install cowsay sl
		cowsay "内容"
		sl #直接回车
8.字符集优化

9.xshell连接优化

10.安装常用软件命令
```