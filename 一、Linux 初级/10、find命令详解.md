
1、目录统计

```bash
1.du 统计大小
	-s 只显示总大小，不细分子文件、子目录
	-h 人性化显示
	[root@breadbomb ~]# du -sh
	76K	.
	[root@breadbomb ~]# du -sh /etc
	33M	/etc

2.df 查看磁盘分区
	-i 查看目录inode号码     ll -i 查看文件inode号码
	-h 人性化显示
```

2、find 命令

```bash
1.语法结构
	a.文件类型查找
		find 路径 -type 类型
		类型参数：
			f 普通文件
			d 目录
			l 软链接
			b 块设备
			c 字节设备
		
		示例：
			#查看当前目录下所有普通文件
			find ./ -type f
			
	b.文件名称查找
		find 路径 -name "文件名/目录名"
		find 路径 -iname "文件名/目录名" 忽略名称大小写
		模糊查找：
			*   匹配任意多个字符（包括0个）
			?   匹配任意1个字符
			[]  匹配括号内任意一个字符
			{}  匹配序列中任意一个
		
		示例：
			[root@breadbomb ~]# find ./ -name "a.txt"
			./a.txt
			./example/a.txt
			
			# 查找 file1、file2、file3
			find . -name "file[123]"
			
			#查找 fileaaa、filebbb、fileccc
			find . -name "file{aaa,bbb,ccc}"
			
	c.文件修改时间查找
		find 路径 -mtime 时间     查找规定时间内修改文件内容的文件
		时间类型：
			num   前第num天
			-num  num天内
			+num  num天前
			
			修改系统时间：
				date -s 时间
				
				#修改时间为2020年1月1日
				date -s 20200101
				#恢复时间
				ntpdate npt1.aliyun.com
			
		示例：
		# 查找 7天内 修改过的文件 
		find . -type f -mtime -7 
		
		# 查找 7天前 改过，最近没动过的文件 
		find . -type f -mtime +7 
		
		# 查找 刚好第3天 修改的文件 
		find . -type f -mtime 3


```