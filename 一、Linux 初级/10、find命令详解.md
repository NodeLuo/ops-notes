
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

2、find 命令 （find默认是递归查找）

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
		
	d.文件大小查找
		find 路径 -size 大小+单位
		大小类型：
			num   准确大小
			+num  大于num的文件
			-num  小于num的文件
		单位类型：
			c 字节    1c = 1字节
			k 千字节  1k = 1024字节 
			M 兆     1M = 1024k
			G 吉     1G = 1024M
			
		示例：
		#查找10M的文件和目录
		find . -size 10M
		#查找大于10M的文件和目录
		find . -size +10M
		#查找小于10M的文件和目录
		find . -size -10M
		
	e.指定深度查找
		find 路径 -maxdepth 深度数字
		
		示例：
		#查找当前目录下的一级目录和文件
		find . -maxdepth 1


2.综合运用
	find 路径 -type 类型 -name "文件名/目录名" -mtime 修改时间 -size 大小+单位
	
	注意：同一种参数可多次使用
	#查找当前目录下大于5M小于10M的文件
	find . -size +5M -size -10M
	等价于
	find . -size +5M -and -size -10M (省略了-and 可简写-a)
	
	#查找当前目录下小于5M或大于10M的文件
	find . -size -5M -or -size +10M （-or不可省略 可简写-o）
```

3、find结果与其他命令结合使用（分为两类命令）

```bash
1.删除查找到的文件或目录（结尾类）
	find . -name "*.txt" | xargs rm -r
	解析：
		xargs 可以将前面结果放置到结尾，类似于xargs rm -rf a.txt b.txt ...
		xargs 后面的命令别名失效,即rm 不等于 rm -i
		
2.复制查找到的文件或目录（指定位置类）
	find . -name "a.txt" | xargs -i cp {} /opt/
	解析：
		xargs -i 将前面结果插入到{}中，相当于cp a.txt /opt/
```