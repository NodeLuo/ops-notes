
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


3.系统时间同步

4.关闭Selinux

5.关闭firewalld

6.关闭NetworkManager

7.修改默认的YUM仓库

8.字符集优化

9.xshell连接优化

10.安装常用软件命令
```