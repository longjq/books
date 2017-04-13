# php查漏补遗

------

### 本地运行php脚本

运行php文件：php.exe  -f  "php文件路径"
`php.exe -f index.php`
运行php代码：php.exe  -r  "php脚本代码"
`php.exe -r "echo \"helloworld!!\";";`

### 时区

#### 设置时区

默认时区不对，需要调整时区

方式一：通过php.ini方式调整

`date.timezone=[Asia/Shanghai|PRC]`

方式二：在php文件中设置（此方法必须每次php业务代码执行前执行）

`date_default_timezone_set('America/Los_Angeles');`设置当前时区
`date_default_timezone_get();`返回当前时区

### POST提交

#### POST与GET变量名相同时

当POST和GET提交的数据名称相同的时候，POST的值会覆盖掉GET的值，可以在`php.ini`中修改。

`request_order="GP"`G=GET‘、P=POST，后者覆盖前者，反之亦然

### 预定义变量

####$_Server

大约有30个左右的信息，我们只要知道其中5个左右！

```
$_SERVER[‘REMOTE_ADDR’]：获取访问者的ip地址(如果用户使用了代理请求或者后端使用了负载，此方法获取的是代理的IP，使用$_SERVER[‘x_forwarded_for’]获取真实的用户IP)
$_SERVER[‘SERVER_ADDR’]：获取服务器所在的ip地址
$_SERVER[‘SERVER_NAME’]：获取服务器的名字，其实就是站点设置中的servername
$_SERVER[‘DOCUMENT_ROOT’]：获取站点的真实物理地址，其实就是站点设置中的documentroot
$_SERVER[‘PHP_SELF’]：获取当前网页地址（不含域名部分）
$_SERVER[‘SCRIPT_FILENAME’]：获取当前网页地址物理路径
$_SERVER[‘QUERY_STRING’]获取当前网页地址中的所有get数据（就是？号后面部分），但只是一个整体的字符串而已。

```

#### $GLOBALS

它也是一个“重复性数据”，它里面存储了我们自己定义的所有“全局变量”
```
$v1 = 1;	//定义了一个全局变量，
此时，就有了这样一个数据：$GLOBALS[‘v1’]，其值就是1
echo $v1 ;	//输出1
echo $GLOBALS[‘v1’]；	//输出1
```
### 常量

#### 设置

````
// 语法一
define("PI",3.14);
define("NAME","Zhencheng");
// 语法二
const AGE=32;
const SEX='man';
````

#### 取值

```
//语法一，直接输出常量名
echo PI;
echo NAME;
//语法二。使用constant()函数获取
echo constant("AGE");
echo constant("SEX")
```

#### 判断

```
if( defined("PI") ){
  echo "已经设置了PI常量";
}
```

#### 常量的“坑”

```
// MONEY常量未定义
echo "Money：".MONEY;

//当使用一个未定义的常量的时候，系统会直接将该常量当做“有值”的常量去使用，并且其值就是该常量名——虽然也会报错[经测试PHP7下，报WARNING级别错误]！
```

####预定义常量
M_PI:		        就是圆周率的常量值；
PHP_OS:		        就是php运行所在的操作系统
PHP_VERSION:      就是php的版本号
PHP_INT_MAX:      php中的最大的整数值
更多可参考：php手册>附录>保留字列表>预定义常量

####魔术常量
根据系统环境变化的值
`__FILE__`		:代表当前网页文件的完整物理路径
`__DIR__`			:代表当前网页文件所在的文件夹
`__LINE__`		:代表当前这个常量名所在的”行号”

####字符串
除了常见的单、双引号还有`单引号定界符`和`双引号定界符`
```
// "aaa"代表开始，aaa;代表结束，中间所有代表字符串
// "aaa"双引号，中间可以包括(\\、\n、\r、\t、\$)转移符
// 'aaa'单引号，原封不动输出中间的内容
$name1 = <<<"aaa"
111\n\n1
2\t2\r2\$2
aaa;
echo $name1;
echo "\n==============================\n";
$name2 = <<<'aaa'
111\n\n\n\n1
2\t2\r2\$2
aaa;
echo $name2;
```
#### 布尔值

```
if($name){
  //$name存在值
}else{
	//出现false的情况，代表变量存储的是如下的值是0,   0.0,   “”,   “0”,   null,   array(),   false,   还有一个是“未定义的变量”，“未定义的变量”还会出现Notice级别的异常
}
```
#### 类型转换
var_dump()：用于输出变量的“完整信息”，几乎只用于调试代码。


getType($变量名)：获取该变量的类型名字，返回的是一个表示该类型名字的字符串，比如：“string”，“bool”，“double”，“int”
setType($变量名，“目标类型”)：将该变量强制改变为目标类型；
isset(), empty(), unset();。。。。省略！

is_XX类型() 系列函数：判断某个数据是否为某种类型，有如下一些：
is_int($x);		判断$x是否是一个整数类型；
is_float($x);
is_string($x);
is_bool($x);
is_array($x);
is_object($x);
is_null($x);
is_numeric($x);		判断$x是否是一个数字！
is_scalar($x);		判断$x是否是一个“标量类型”



![img](http://img.dahe.cn/qf/2016/7/31/1724S0LOFJ.jpeg)

