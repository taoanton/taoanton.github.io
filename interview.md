#面试

##问题
请问GET和POST方法有什么区别
PHP中的错误类型有哪些？
COOKIE和SEESION的区别
禁用COOKIE 后 SEESION 还能用吗?

##开启错误
###开发环境
display_errors = On
display_startup_errors = On
error_reporting = -1
log_errors = On
###生产环境
为了在生产环境中隐藏错误显示，将你的 php.ini 进行如下配置：
display_errors = Off
display_startup_errors = Off
error_reporting = E_ALL
log_errors = On

###字符串
大小写

###数组
索引数组、关联数组
数组大小 count、sizeof
list($a,$b,$c) = array('', '');

$array1 = ['one', 'two', 'three'];
$array2 = [1=>'one', 2=>'two', 3=>'three'];
json_encode($array1);
json_encode($array2);

###编码


###反射



###日期和时间
获取当前时间，转换成指定格式 2015-10-01，再转成时间戳

###oo
权限控制修饰符

##版本控制
git创建本地分支
git合并分支
git拉取代码与本地冲突解决

##linux


##html+css


##正则
(.*)与(.*?)的区别


##database
数据库连接类，特点
如何查看sql的执行效率
MyISAM与innoDB存储引擎有何差别
varcher和char有何差别

##编码规范
psr编码规范

##异常

算法：
二分，冒泡
设计模式：
单例，工厂
##end
待遇、职业规划、爱好