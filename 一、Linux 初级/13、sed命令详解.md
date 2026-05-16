
1、sed命令

```bash
1.sed 参数
	-n 只输出匹配到的行
	-i 直接修改原文件
	-i.bak 修改原文件，自动生成备份文件
	-e 执行多条sed命令
	-E 使用扩展正则（不用转义括号）

2.行匹配规则
	a.数字行号
		3   ：第3行
		2,5 ：2-5行
		$   ：最后一行
	b.正则匹配行
		/关键词/ ：里面用正则就行

3.操作命令
	s 字符串替换
	d 删除行
	p 打印输出行
	a 行后追加内容
	i 行前插入内容
	c 整行替换
	q 匹配后直接退出

4.修饰符
	替换命令格式：
		s/原内容/新内容/修饰符
	修饰符：
		g 全局替换（整行全部替换）
		i 忽略大小写
		2 只替换第二个匹配内容

示例：
	（1）删除操作
		# 删除空行 
		sed '/^$/d' test.txt 
		
		# 删除注释行（#开头） 
		sed '/^#/d' test.txt 
		
		# 删除第3行 
		sed '3d' test.txt 
		
		# 删除2到6行 
		sed '2,6d' test.txt 
		
		# 删除最后一行 
		sed '$d' test.txt 
		
		# 删除包含error的行 
		sed '/error/d' test.txt
		
	
	（2）筛选打印 （sed会默认打印所有行，筛选后p再打印，所以需要-n取消默认行为）
		# 只显示3-8行 
		sed -n '3,8p' test.txt 
		
		# 只显示包含success的行 
		sed -n '/success/p' test.txt 
		
		# 不包含fail的行 
		sed -n '/fail/!p' test.txt
		
		# 筛选行区间
		注意：多个区间符合都输出，未闭合则输出到结尾，但必须先匹配开头
		[root@breadbomb ~]# sed -n '/aa/,/cc/p' ./a.txt
		aaaa
		bbbbb
		ccccc

	（3）

5.作用：
	a.模糊过滤文件内容
	b.查找指定行
	c.对文件内容增删改查
	d.格式化输出内容，后向引用

```