title: PHP测试驱动开发 
date: 2014-12-20  15:45:11
tags: 测试驱动开发 TDD php 
---



#php 测试驱动开发 TDD
# PHP开发分享
- [测试驱动开发](#tdd)  
    - [phpunit](#phpunit)  
        - [断言测试](#assert)  
        - [测试替身](#mock)  
        - [命令行测试](#phpunitCommondLine)  
        - [代码覆盖率报告](#coverage)  
- [PHP CodeSniffer  PHP代码探测器检查编码标准](#phpCodeSniffer)
- [PHPDocumentor api文档生成工具](#phpDocumentor)  
- [PHP-FIG 框架互操作组 PHP编码规范](#php-fig)  
- [PHP the right way PHP学习指南](#phptherightway)  

<a name="tdd"></a>
## 测试驱动开发(TDD)

测试驱动开发（Test-driven development）是极限编程中倡导的程序开发方法，以其倡导先写测试程序，然后编码实现其功能得名。测试驱动开发始于20世纪90年代。测试驱动开发的目的是取得快速反馈并使用“illustrate the main line”方法来构建程序。

###TDD的目标

`Clean Code That Works`

这句话的含义是，事实上我们只做两件事情：让代码奏效（Work）和让代码洁净（Clean），前者是把事情做对，后者是把事情做好。想想看，其实 我们平时所做的所有工作，除去无用的工作和错误的工作以外，真正正确的工作，并且是真正有意义的工作，其实也就只有两大类：增加功能和提升设计，而TDD 正是在这个原则上产生的。如果您的工作并非我们想象的这样，（这意味着您还存在第三类正确有意义的工作，或者您所要做的根本和我们在说的是两回事），那么 这告诉我们您并不需要TDD，或者不适用TDD。而如果我们偶然猜对（这对于我来说是偶然，而对于Kent Beck和Martin Fowler这样的大师来说则是辛勤工作的成果），那么恭喜您，TDD有可能成为您显著提升工作效率的一件法宝。请不要将信将疑，若即若离，因为任何一项 新的技术——只要是从根本上改变人的行为方式的技术——就必然使得相信它的人越来越相信，不信的人越来越不信。这就好比学游泳，唯一能学会游泳的途径就是 亲自下去游，除此之外别无他法。这也好比成功学，即使把卡耐基或希尔博士的书倒背如流也不能拥有积极的心态，可当你以积极的心态去成就了一番事业之后，你 就再也离不开它了。相信我，TDD也是这样！想试用TDD的人们，请遵循下面的步骤：


###TDD的优点

『充满吸引力的优点』

1.完工时完工。表明我可以很清楚的看到自己的这段工作已经结束了，而传统的方式很难知道什么时候编码工作结束了。  
2.全面正确的认识代码和利用代码，而传统的方式没有这个机会。  
3.为利用你成果的人提供Sample，无论它是要利用你的源代码，还是直接重用你提供的组件。  
4.开发小组间降低了交流成本，提高了相互信赖程度。  
5.避免了过渡设计。  
6.系统可以与详尽的测试集一起发布，从而对程序的将来版本的修改和扩展提供方便。  
7.TDD给了我们自信，让我们今天的问题今天解决，明天的问题明天解决，今天不能解决明天的问题   ，因为明天的问题还没有出现(没有TestCase)，除非有TestCase否则我决不写任何代码；明天也不必担心今天的问题，只要我亮了绿灯。  

『不显而易见的优点』

8.逃避了设计角色。对于一个敏捷的开发小组，每个人都在做设计。  
9.大部分时间代码处在高质量状态，100％的时间里成果是可见的。  
10.由于可以保证编写测试和编写代码的是相同的程序员，降低了理解代码所花费的成本。  
11.为减少文档和代码之间存在的细微的差别和由这种差别所引入的Bug作出杰出贡献。  
12.在预先设计和紧急设计之间建立一种平衡点，为你区分哪些设计该事先做、哪些设计该迭代时做提供了一个可靠的判断依据。

『有争议的优点』

13.事实上提高了开发效率。每一个正在使用TDD并相信TDD的人都会相信这一点，但观望者则不同，不相信TDD的人甚至坚决反对这一点，这很正常，世界总是这样。
14.发现比传统测试方式更多的Bug。  
15.使IDE的调试功能失去意义，或者应该说，避免了令人头痛的调试和节约了调试的时间。  
16.总是处在要么编程要么重构的状态下，不会使人抓狂。（两顶帽子）  
17.单元测试非常有趣。

TDD的步骤
> 编写TestCase  --> 实现TestCase  --> 重构
> （不可运行） &nbsp; &nbsp; &nbsp; &nbsp;（可运行）   &nbsp;    &nbsp; &nbsp; （重构） 

<table><tr><td>(1) 快速新增一个测试用例  </td><td>新的TestCase</td></tr><tr><td>(2) 编译所有代码，刚刚写的那个测试很可能编译不通过</td><td>原始的TODO List</td></tr><tr><td>(3) 做尽可能少的改动，让编译通过</td><td>Interface</td></tr><tr><td>(4) 运行所有的测试，发现最新的测试不能编译通过</td><td>－(Red Bar) </td></tr><tr><td>(5) 做尽可能少的改动，让测试通过 </td><td>Implementation</td></tr><tr><td>(6) 运行所有的测试，保证每个都能通过 </td><td>－(Green Bar) </td></tr><tr><td>(7) 重构代码，以消除重复设计</td><td>Clean Code That Works</td></tr></table>

书籍：
>  测试驱动开发 http://book.douban.com/subject/25735501/

练习：
>  https://github.com/daylerees/test-driven-development-example

<a name="phpunit"></a>
##phpunit
PHPUnit是一个轻量级的PHP测试框架， 当前最新版本 PHPUnit 4.4.0
>  https://phpunit.de/

###安装 （linux）
```bash
$ wget https://phar.phpunit.de/phpunit.phar  
$ chmod  +x phpunit.phar  
$ sudo mv phpunit.phar /usr/local/bin/phpunit
```
>  其他平台安装方式请参考PHPUnit手册第1章

phpunit默认执行指定目录下*Test.php文件中的测试用例，并且是迭代的遍历所有子目录。phpunit命令提供了一些可选参数，可以使得批量处理Test Case变得容易。


<a name="assert"></a>
##phpunit断言
```
布尔类型
assertTrue   断言为真
assertFalse  断言为假

NULL类型
assertNull    断言为NULL
assertNotNull  断言非NULL

数字类型
assertEquals             断言等于
assertNotEquals          断言不等于
assertGreaterThan        断言大于
assertGreaterThanOrEqual 断言大于等于
assertLessThan           断言小于
assertLessThanOrEqual    断言小于等于

字符类型
assertEquals          断言等于
assertNotEquals       断言不等于
assertContains        断言包含
assertNotContains     断言不包含
assertContainsOnly    断言只包含
assertNotContainsOnly 断言不只包含

数组类型
assertEquals          断言等于
assertNotEquals       断言不等于
assertArrayHasKey     断言有键
assertArrayNotHasKey  断言没有键
assertContains        断言包含
assertNotContains     断言不包含
assertContainsOnly    断言只包含
assertNotContainsOnly 断言不只包含

对象类型
assertAttributeContains           断言属性包含
assertAttributeContainsOnly       断言属性只包含
assertAttributeEquals             断言属性等于
assertAttributeGreaterThan        断言属性大于
assertAttributeGreaterThanOrEqual 断言属性大于等于
assertAttributeLessThan           断言属性小于
assertAttributeLessThanOrEqual    断言属性小于等于
assertAttributeNotContains        断言不包含
assertAttributeNotContainsOnly    断言属性不只包含
assertAttributeNotEquals          断言属性不等于
assertAttributeNotSame            断言属性不相同
assertAttributeSame               断言属性相同
assertSame                        断言类型和值都相同
assertNotSame                     断言类型或值不相同
assertObjectHasAttribute          断言对象有某属性
assertObjectNotHasAttribute       断言对象没有某属性

class类型
class类型包含对象类型的所有断言，还有
assertClassHasAttribute          断言类有某属性
assertClassHasStaticAttribute    断言类有某静态属性
assertClassNotHasAttribute       断言类没有某属性
assertClassNotHasStaticAttribute 断言类没有某静态属性

文件相关
assertFileEquals     断言文件内容等于
assertFileExists     断言文件存在
assertFileNotEquals  断言文件内容不等于
assertFileNotExists  断言文件不存在

XML相关
assertXmlFileEqualsXmlFile        断言XML文件内容相等
assertXmlFileNotEqualsXmlFile     断言XML文件内容不相等
assertXmlStringEqualsXmlFile      断言XML字符串等于XML文件内容
assertXmlStringEqualsXmlString    断言XML字符串相等
assertXmlStringNotEqualsXmlFile   断言XML字符串不等于XML文件内容
assertXmlStringNotEqualsXmlString 断言XML字符串不相等

```

##laravel断言

```
assertResponseOk  Assert回应为OK
assertResponseStatus(403) Assert 回应状态码

Assert 回应为重定向
$this->assertRedirectedTo('foo');
$this->assertRedirectedToRoute('route.name');
$this->assertRedirectedToAction('Controller@method');

Assert 回应带数据的视图
$this->assertViewHas('name');
$this->assertViewHas('age', $value);

Assert 回应带数据的 Session
$this->assertSessionHas('name');
$this->assertSessionHas('age', $value);


```

<a name="mock"></a>
##测试替身 Mock
单元测试过程中经常会遇到被测试函数A依赖另一个函数B，但是已经有针对B的测试，没有必要在测试A的时候重复测试B。
PHPUnit提供了Mock API来帮我们解决这个问题。
```
public function testBit(){
  $oClientMock = $this->getMock('SomeClient'); // 创建mock对象

  $oClientMock->expects($this->once()) // 设定次数

  ->method('ExecuteCommand') // 设定方法

  ->with(CPU_BIT_CMD) // 设定方法入参

  ->will($this->returnValue('some')); // 设定方法返回值

  $oHardware = new MHardware($oClientMock);

  $this->assertEquals('32', $oHardware->CpuBit()); // 调用方法并断言

}

```
###使用mock一般有下面几步：

> getMock 创建mock对象（必须有）  
> method 设置期望调用的方法（必须有）  
> expects 设置方法调用的次数（必须有）  
> with 设置调用方法时的入参（可选）  
> will 设置调用方法后的返回值（可选）  

###getMock函数签名详解

getMock有7个参数，一般只需要使用第一个参数指定被mock的类即可，但是如果需要更灵活的配置mock，有必要了解其他参数：

String – Required – 需要mock的类的名称
Array – Optional – 需要mock的函数名称数组，默认情况下，会mock所有函数（即给所有函数一个空的实现），但是如果设置了需要mock的函数，那么其他函数将不会被mock，按照原来的方式执行。
Array – Optional – 需要传入给构造函数的参数，getMock方法帮你调用了构造函数，所以这里通过一个数组，给你设置构造函数参数的机会
String – Optional – 给这个mock类起一个名称，这样可以使用这个新名称创建许多同样的mock类实例。
Boolean – Optional – true将调用原始对象的构造函数，false将不掉用，默认为true
Boolean – Optional – true将可以调用原始类的clone函数，false则无法调用。
Boolean – Optional – false将禁止__autoload函数被调用，当mock对象被创建时。


###匹配器（Matchers）

匹配器相当于调用mock方法的量词，作为expects函数的参数传给mock对象，用于设定期望的调用次数，主要有下面几个：
```
once() 期望方法只调用一次，否则测试失败
never() 期望方法从不被调用，否则测试失败
any() 期望调用任意次，测试永远不会因此失败。
at($index) 期望方法被第$indexd调用的行为，$index从0开始，一般会配合with或will使用。值得注意的是$index是针对特定mock对象而言的，而不是针对特定mock对象的特定方法。也就是说，mock对象A任意一个方法被调用一次，$index会增加1。
exactly($times) 期望执行准确的次数，否则测试失败
atLeastOnce() 期望执行至少一次，否则测试失败
```

###约束（Constraints）

约束和with一起使用，用于设定mock函数的输入，约束有很多，主要分为一下几大类

[数组]
```
arrayHasKey(mixed $key) 断言入参数组是否有指定的键
contains(mixed $value) 断言入参数组是否有指定的值
```
[逻辑]
```
logicalAnd($constraint,$constraint) 断言两个参数逻辑和
logicalNot($constraint) 断言参数逻辑否
logicalOr($constraint,$constraint) 断言两个参数逻辑或
logicalXor($constraint,$constraint) 断言两个逻辑异或
```
[字符串]
```
matchesRegularExpression($pattern) 断言入参是否匹配正则表达式
stringContains($string, $case) 断言入参是否包含表达式
stringEndsWith( $suffix) 断言入参是否有此后缀
stringStartsWith(string $prefix) 断言入参是否有次前缀
```
[比较]
```
identicalTo($value) 断言入参===当前值
equalTo($value, $delta = 0, $maxDepth = 10) 断言入菜是否==当前值
lessThan($value) 断言入参<当前值
lessThanOrEqual(mixed $value) 断言入参<=当前值
greaterThan(mixed $value) 断言入参>当前值
greaterThanOrEqual(mixed $value) 断言入参>=当前值
```
[类和对象]
```
attribute($constraint, $attributeName) 将约束赋给指定属性或对象
attributeEqualTo($attributeName, $value, $delta = 0, $maxDepth = 10) 断言value是否与当前对象的某个属性相等
classHasAttribute($attributeName) 断言当前类是否具有摸个属性
classHasStaticAttribute($attributeName) 断言当前类是否具有某个静态属性
hasAttribute($attributeName) 断言当前对象是否有指定的属性
```
[基本类型]
```
isFalse() 断言当前值为FALSE
isTrue() 断言当前对象是否为TRUE
isInstanceOf(string $className) 断言当对象是某个类的实例
isNull() 断言当前对象是否为NULL
isType($type) 断言当前对象是某个具体的类型
```
[其他]
```
anything() 接受任何入参
fileExists() 断言当前入参代表的文件是否存在
```

###返回
```
设定返回值，与will一起使用，用于设定mock函数的返回值，主要方法方法如下：
returnValue($value) 返回字面意思
throwException($exception) 此方法在调用时抛出指定异常
returnArgument($index) 返回第$index个参数，从0开始
returnCallback($fun) 返回值通过回调函数生成,函数签名与被mock的函数相同
onConsecutiveCalls(arg0,arg1,…) 设定返回值列表，这样可以控制被返回值的顺序，更灵活的控制返回值，最好与匹配器any或atLeastOnce结合使用。
```

<a name="phpunitCommondLine"></a>
###命令行测试
一些简单的常用命令

测试指定的目录下*Test.php文件中的测试用例
```bash
phpunit tests
```
如果你希望更细粒度的控制执行特定用例，可以使用“--filter”参数  
测试指定类
```bash

phpunit --filter ClassNameTest
PHPUnit 4.4.0 by Sebastian Bergmann.

Time: 2.49 seconds, Memory: 6.75Mb
OK (1 test, 0 assertions)
```

测试指定类的方法
```bash
phpunit --filter ClassNameTest::testClassMethod
```

测试整个项目
```bash
phpunit
```

<a name="coverage"></a>
###代码覆盖率

测试并生成代码覆盖率文件
```
--coverage-clover <file>  生成带有代码覆盖率信息的 XML 格式的日志文件.
--coverage-crap4j <file>  生成 Crap4j 格式的代码覆盖率报告.
--coverage-html <dir>     生成 HTML 格式的代码覆盖率报告.
--coverage-php <file>     生成一个序列化后的 PHP_CodeCoverage 对象，此对象含有代码覆盖率信息.
--coverage-text=<file> 生成带有代码覆盖率信息的日志文件或命令行输出
--coverage-xml <dir>      生成带有代码覆盖率信息的 XML 格式的日志文件.
```

测试结果
```
--log-junit  <file> 为运行的测试生成 JUnit XML 格式的日志文件。
--log-tap  <file> 为运行的测试生成(TAP) 格式的日志文件。
--log-json  <file> 生成 JSON 格式的日志文件。
--testdox-html <file> 为运行的测试生成HTML格式的日志文件
--testdox-text <file> 为运行的测试生成纯文本格式的日志文件

phpunit --coverage-html coverage-html --testdox-html test-result
```

> 更多命令行选项请参考PHPUnit手册第3章 命令行测试执行器


## Mockery
Mockery是一个PHP mock 对象框架 
> https://github.com/padraic/mockery


## phpunit xml配置文件

<phpunit> 元素的属性用于配置 PHPUnit 的核心功能
```
<?xml version="1.0" encoding="UTF-8"?>
<phpunit backupGlobals="false"
          backupStaticAttributes="false"
          bootstrap="bootstrap/autoload.php"
          colors="true"
          convertErrorsToExceptions="true"
          convertNoticesToExceptions="true"
          convertWarningsToExceptions="true"
          processIsolation="false"
          stopOnFailure="false"
          syntaxCheck="false"
          >
</phpunit>
```

测试套件
```
  <testsuites>
    <testsuite name="Application Test Suite">
      <directory>./tests/</directory>
    </testsuite>
  </testsuites>
```

包含或排除文件
<filter> 元素及其子元素用于配置代码覆盖率报告的黑名单与白名单
```
  <filter>
    <blacklist>
      <directory suffix=".php">./vendor</directory>
      <directory suffix=".php">./bootstrap</directory>
    </blacklist>
    <whitelist>
      <directory suffix=".php">app</directory>
    </whitelist>
  </filter>
```

日志记录
```
  <logging>
    <!--代码覆盖率-->
    <log type="coverage-html" target="./coverage-html" charset="UTF-8"
  highlight="false" lowUpperBound="35" highLowerBound="70"/>

    <!--测试结果-->
    <log type="testdox-html" target="./coverage-html/test-result.html"/>
  </logging>
```


