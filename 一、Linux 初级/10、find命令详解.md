
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
	a.查找文件类型
		find 路径 -type 类型
		类型参数：
			f 普通文件
			d 目录
			l 软链接
			b 块设备
			c 字节设备
		
		示例：
			find ./ -type f 查看当前目录下所有普通文件
			
	b. 查找文件名称
		find 路径 -name "文件名/目录名"
		模糊查找：
		
		
		示例：
			[root@breadbomb ~]# find ./ -name "a.txt"
			./a.txt
			./example/a.txt

```