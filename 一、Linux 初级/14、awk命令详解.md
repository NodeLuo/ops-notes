
1、awk命令详解

```bash
作用：
	（1）取行
	（2）取列
	（3）模糊过滤
	（4）数据统计 数据运算
	（5）支持for if 数组等
	（6）格式化输出	

注意：awk 默认输出每一行

1.语法格式
	awk 参数 '模式{动作}' 文件名

2.参数
	-F 输入指定字段分隔符
	-v 定义自定义变量
	-f 从脚本文件读取awk规则，不写命令行
	-W 兼容扩展内容
	-- 结束参数，文件以-开头时使用
	
	示例：
		# 冒号为分隔符
		#一行中以冒号为分隔符，分割出多段，$1取第一段
		awk -F: '{print $1}' /etc/passwd
		# 定义变量 
		awk -v name="linux" '{print name,$1}' test.txt

3.awk内置全局变量
	（1）行
		NR         当前总行数，多文件累计行数
		FNR        单个文件行号，每个文件重新计数
		FILENAME   当前处理的文件名
	
	（2）字段列
		$0         整行全部内容
		$1$2...    第1列、第2列...
		NF         当前行字段总列数
		$NF        最后一列字段
		$(NF-1)    倒数第二列
	
	（3）分隔符
		FS         输入字段分隔符，默认空格
		OFS        输出字段分隔符，默认空格
		RS         输入行分隔符，默认换行
		ORS        输出行分割符，默认换行
	
	示例：
		#输出第二行
		[root@breadbomb ~]# awk 'NR==2' a.txt
		aaaa:bbb:ccc
		
		#单文件于多文件行数区别
		[root@breadbomb ~]# awk 'NR==2' a.txt b.txt
		aaaa:bbb:ccc
		[root@breadbomb ~]# awk 'FNR==2' a.txt b.txt
		aaaa:bbb:ccc
		aaaa:bbb:ccc


```