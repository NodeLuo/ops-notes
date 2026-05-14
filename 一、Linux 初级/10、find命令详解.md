
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
	find 路径 类型
	
```