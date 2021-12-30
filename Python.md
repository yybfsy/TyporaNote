# Python



## Python基础



**变量**

变量就是一个存储数据的时候当前数据所在的内存地址的名字而已。

变量名 = 值

变量名自定义，要满⾜标识符命名规则。



**标识符**

标识符命名规则是Python中定义各种名字的时候的统一规范，具体如下：

- 由数字、字母、下划线组成
- 不能数字开头
- 不能使用内置关键字
- 严格区分⼤小写



**数据类型**

在 Python 里为了应对不同的业务需求，也把数据分为不同的类型。

![ ](https://gitee.com/yybovo/note-images/raw/master/Typora/python001.png)

检测数据类型的方法： type()

检测数据标识的方法： id()

检测数据值的方法： 变量名

```python
name = '宋君婉'
print(name)
print('标识',id(name))
print('类型',type(name))
print('值',name)

# 标识 1984748811920
# 类型 <class 'str'>
# 值 宋君婉
```



 

**格式化输出**

按照一定的格式输出内容。

 

**格式化符号**



| **格式符号** | **转换**                         |
| :----------: | -------------------------------- |
|      %s      | 字符串（也可以用来当做%d 和 %f） |
|      %d      | 有符号的十进制整数               |
|      %f      | 浮点数                           |
|      %c      | 字符                             |
|      %u      | 无符号十进制整数                 |
|      0b      | 转换二进制整数（0b1234）         |
|      %o      | 八进制整数                       |
|      %x      | 十六进制整数（小写ox）           |
|      %X      | 十六进制整数（大写OX）           |
|      %e      | 科学计数法（小写'e'）            |
|      %E      | 科学计数法（大写'E'）            |
|      %g      | %f和%e的简写                     |
|      %G      | %f和%E的简写                     |

​                %06d，表示<font color=red>输出的整数</font>显示位数，不足以0补全，超出当前位数则原样输出

​                 %.2f， 表示<font color=red>小数点后</font>显示的小数位数。

  ```python
  age = 18
  name = 'Tom'
  weight = 80.5
  stu_id = 1 # %06d，表示输出的整数显示位数，不足以0补全，超出当前位数则原样输出
  print('我的名字是%s,今年%d岁了，体重%.2f公斤，我的学号是%03d' %(name,age,weight,stu_id))
  
  #输出 我的名字是Tom,今年18岁了，体重80.50公斤，我的学号是001
  ```

​     

格式化字符串除了`%s`，还可以写为`f '{表达式}'`

  ```python
  # f '{表达式}'
  print(f'我的名字是{name},今年{age}岁了，体重{weight}公斤，我的学号是{stu_id}')
  
  #输出 我的名字是Tom,今年18岁了，体重80.5公斤，我的学号是1
  ```

`f-`格式化字符串是Python3.6中新增的格式化方法，该方法更更简单易读。

**浮点类型**

浮点数整数部分和小数部分

浮点数储存不精确性

使用浮点数进行计算时，可能会出现小数点位不确定的情况

- 解决方案

  - 导入模块

  ```python
  from decimal import Decimal
  print(Decimal('1.1')+Decimal('2.2')) # 3.3
  ```

**字符串类型**

字符串又称为不可变的字符序列

可以使用单引号`''`双引号`""`三引号`''' '''`或`""" """`来定义

单引号和双引号定义字符串必须在<font color=red>一行</font>

三引号定义字符串可以分布在连续的多行

```
str1 = """人生苦短,
我用python"""
#控制台
#人生苦短,
#我用python

```

**类型转换**

| 函数名  | 作用                       | 注意事项                                                     | 举例                  |
| :-----: | :------------------------- | :----------------------------------------------------------- | :-------------------- |
|  str()  | 将其他数据类型转成字符串   | 也可用引号转换                                               | str(123)    '123'     |
|  int()  | 将其他类型转换成整数       | 文字类和小数类字符串，无法转换成整数。浮点数转换成整数，抹零取整 | int('123')  int(9.8)  |
| float() | 将其他数据类型转换成浮点数 | 文字类无法转成整数。整数转成浮点类，末尾为0                  | float('9.9') float(9) |

 

**转义字符**

- \n ：换行。

- \t ：制表符，一个tab键（4个空格）的距离。

- \r：回车 ，return光标移动到下一行开头
- \b：退格，回退一个字符（清除掉该符号的前一个字符）



**原字符**

不希望转义符起作用，在字符串之前加上r，或R

```python
print(r'hello\\world')
```



**结束符**

print(**"xxx"**,end=**""**)

在Python中，print()， 默认自带end="\n" 这个换⾏结束符，所以导致每两个print 直接会换行展示，用户可以按需求更改结束符。

 ```python
 print("hello",end="\t")
 print("world",end="\t")
 print("hello",end="\t")
 print("python",end="\t")
 
 # hello   world	  hello	  python	
 ```



 **保留字**

一些单词被赋予了特定的意义，这些单词不能被任何对象当成名字。

```python
import keyword
print(keyword.kwlist)

# ['False', 'None', 'True', '__peg_parser__', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']

```



**注释**

注释分为两类：单行注释 和 多行注释。

单行注释

只能注释一行内容，语法如下：

多行注释

可以注释多行内容，⼀一般⽤用在注释⼀一段代码的情况， 语法如下：

注释的分类

单行： `# `注释内容，快捷键ctrl+/

多行： `""" `注释内容 `""" `或` '''` 注释内容` '''`

 ```python
 """
 第一行注释
 第二行注释
 第三注释
 """
 '''
 注释1
 注释2
 注释3
 '''
 ```

冷知识 

中文编码声明注释-->python文件开头加上声明注释可以指定文件的编码格式

```python
#encoding:gbk
#encoding:utf-8
```



**函数**



**input()**函数

作用：接收来自用户的输入

返回值类型：输入值的类型为str

值的储存：使用=对输入的值进行存储

```python
present = intpu('一念永恒的主角是？')

#present 变量
#= 运算符 将输入函数的结果赋值给变量present
#intput('一念永恒的主角是？') 需要输入的回答
```



**常用运算符**

标准运算符：`+`、`-`、`*`、`/`、`//`(整除)

取余运算符：`%`

幂运算符：`**`

<img src="https://gitee.com/yybovo/note-images/raw/master/Typora/python002png" alt="image-20211215212738349" style="zoom:50%;" />

**赋值运算符**

执行顺序：左-->右

支持链式赋值  a=b=c=20

支持参数赋值 +=、-+、*=、/=、//=、%=

支持系列解包赋值 a,b,c = 20,30,40

```python
a,b = 10,20
print('交换之前:',a,b)
a,b = b,a
print('交换之后:',a,b)
# 交换之前: 10 20
# 交换之后: 20 10
```



**比较运算符**

对变量或表达式的结果进行大小、真假等比较

`>`,`<`,`>=`,`<=`,`!=`

`==`  对象value的比较

`is` ,` is not`  对象的id的比较

```python
a=10
b=10
print(a==b) #true 说明a与b的value 相等
print(a is b) #true 说明a与b的id表示 相等（与java不同）
print(a is not b) #false a的id与b的id不相等

list1 = [11,22,33,44]
list2 = [11,22,33,44]
print(list1 == list2) #true
print(list1 is list2) #false
print(id(list1)) #3070913388224
print(id(list2)) #3070913298944
print(list1 is not list2) #true
```



**布尔运算符**

`and`，`or`，`not`，`in`(表示在不在当中)，`not in`

![image-20211216102222720](https://gitee.com/yybovo/note-images/raw/master/Typora/python003.png)

```python
s = 'helloworld'
print('w' in s) #Ture
print('k' in s) #False
print('w' not in s) #False
print('k' not in s) #True
```



**位运算符**

将数据转换成二进制进行计算

位与&  对应数位都是1，结果数位才是1，否则为0

位或|   对应数位都是0，结果数位才是0，否则为1

左移位运算符<<   高位溢出舍弃，低位补0

右移位运算符>>   低位溢出舍弃，高位补0

```python
#十进制的4转换为二进制为 0 0 0 0 0 1 0 0
#十进制的8转换为二进制为 0 0 0 0 1 0 0 0
#位与& 对比相应数位是否都是1如果有则是1，如果没有则是0
#位或| 对比相应数位是否都是0如果有则是0，如果没有则是1
#左移位运算符<<  位数全部向前移一位，高位溢出舍弃，低位补0 一位相当于乘2 4*2=8
#右移位运算符>>  位数全部向前移一位，低位溢出舍弃，高位补0 一位相当于除2 4/2=2

print(4&8) #按位与 0
print(4|8) #按位或 二进制为1100十进制为12 12
print(4<<1) #向前移一位 8
print(4<<2) #向前移两位 16
print(8>>1) #向后移一位 4
print(8>>2) #向后移两位 2
```



**运算符的优先级**

![image-20211216110624281](https://gitee.com/yybovo/note-images/raw/master/Typora/python004.png)

<font color=red>( )-->算术运算-->位运算-->比较运算-->布尔运算-->赋值运算</font>



**对象的布尔值**

- Python一切皆对象，所有对象都有一个布尔值
  - 获取对象的布尔值
    - 使用内置函数bool()

对象布尔值为False的有

False，数值()，None ，空字符串，空列表，空元组，空字典，空集合

```
print(bool(False))
print(bool(0))
print(bool(0.0))
print(bool(None))
print(bool(''))
print(bool(""))
print(bool([])) #空列表
print(bool(list())) #空列表
print(bool(())) #空元组
print(bool(tuple())) #空元组
print(bool({})) #空字典
print(bool(dict())) #空字典
print(bool(set())) #空集合
```



**双分支结构**

语法结构

`if 条件表达式 :
    条件执行体1
else :
    条件执行体2`

```python
num = int(input('请输入一个整数'))

if num%2==0:
    print(num,'是一个偶数')
else:
    print(num,'是一个奇数')
```

**多分支结构**

语法结构

`if 条件表达式1 :
    条件执行体1
elif 条件表达式2 ：
    条件执行体2 :
elif 条件表达式N :
    条件执行体N
else:
    条件执行体N+1`

```python
num = int(input('请输入您的成绩:'))
if num>=90 and num<=100 :
    print('您的排行为A')
elif num>=80 and num<90:
    print('您的排名为B')
elif num>=70 and num<80:
    print('您的排名为c')
else:
    print('您未达到排名分数')

```

**进阶** 嵌套结构

```python
answer = input('您是会员嘛y/n')
money = float(input('请输入您的购物金额'))
if answer == 'y':
    if money >= 200:
        money = money*0.75
        print('打七五折，付款金额为：', money)
    elif money >= 100:
        money = money * 0.90
        print('打九折，付款金额为：', money)
    else:
        print('不打折，付款金额为：', money)
else:
    if money >= 200:
        money = money * 0.85
        print('打八五折，付款金额为：', money)
    else:
        print('不打折，付款金额为：', money)
```

**条件表达式**

条件表达式是if...else的简写

语法结构
x `if` 判断条件 `else` y

运算规则
如果判断条件的布尔值为True，条件表达式的返回值为x，否则条件表达式的返回值为False

```python
num_a = int(input('请输入第一个整数'))
num_b = int(input('请输入第二个整数'))
#比较大小
"""if num_a >= num_b:
    print(num_a, '大于等于', num_b)
else:
    print(num_a, '小于等于', num_b)"""
print((str(num_a)+'大于等于'+str(num_b)) if num_a >= num_b else (str(num_a)+'小于等于'+str(num_b)))

```

**pass语句**

先搭建语法结构，还没想好代码怎么写的时候使用

使用范围

- if语句的条件执行体
- for-in语句的循环体
- 定义函数时的函数体

```python
answer = input('您是会员嘛y/n')
money = float(input('请输入您的购物金额'))
if answer == 'y':
    pass
else:
    pass
```

**内置函数range()**

用于生成一个整数列

创建range对象的三种方式
![](https://gitee.com/yybovo/note-images/raw/master/Typora/python005.png)

返回值是一个迭代器对象
range类型的优点，不管range对象表示的整数序列多长，所有range对象占用的内存空间都是相同的，因为仅仅需要储存start，stop和step，只有当用到range对象时，才会去计算序列中的相关元素
in与not in判断整数序列是否存在（不存在）指定的整数

```python
# range() 的三种创建方式
# 第一种创建方式，只有一个参数（小括号中只给一个数）
r = range(10) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]，默认从0开始，默认相差一成为步长
print(r)
print(list(r)) # 用于查看range对象中的整数序列 -->list是列表的意思

# 第二种创建方式，给两个参数
r = range(1, 10) # 指定起始值，从1开始，到10结束（不包含10），步长默认为1
print(list(r)) # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# 第三种创建方式，给三个参数
r = range(1, 10, 2) # 步长修改为2 从1开始 1,3,5,7,9
print(list(r)) # [1, 3, 5, 7, 9]

# 判定指定的整数 在序列是否存在in，not in
print(10 in r) # false
print(9 in r) # true
print(10 not in r) # true
print(9 not in r) # false
```

**循环结构**

循环分类
`while`
`for -in`

语法结构
while 条件表达式：
     条件执行体（循环体）

选择结构if与循环结构while的区别

- if是判断一次，条件为True执行一次
- while是判断N+1次，条件为True执行N次

```python
a = 0
sum = 0
while a < 5:
    sum += a
    a += 1
print('和为', sum) # 和为 10

#求100之内的偶数和
a = 0
sum = 0
while a <= 100:
    if not bool(a % 2): # 简写 a%2==0 因为每个对象都有布尔值零的布尔值为False 进行取反求偶数和 if not bool(a%2) 不为零(Ture)则跳出if判断
        sum += a
    a += 1
print('偶数和为', sum)
```

**for - in循环**

in表达从（字符串、序列等）中依次取值，又称为遍历
for-in遍历的对象必须是可迭代对象

语法结构
for 自定义的变量 in 可迭代对象：
      循环体

循环体内不需要访问自定义变量，可以将自定义变量替代为下划线

```python
for item in 'Python': # 第一次取出来的是P，将P赋值item，将item的值输出
    print(item)

# range() 产生一个整数序列，--> 也是一个可迭代对象
for i in range(10):
    print(i) # 遍历数组

# 若果在循环对象中不需要使用自定义变量，可将自定义变量写为 _
for _ in range(5):
    print("人生苦短，我用python") # 遍历五遍

# 求100之类的偶数和
sum = 0
for i in range(1, 101):
    if not bool(i % 2):
      sum += i
print("1-100之和为", sum)

# 求100-999之间的水仙花数
# 举例
# 153=1*1*1+5*5*5+3*3*3

for item in range(100, 1000):
    ge = item % 10 # 个位
    shi = item // 10 % 10 # 十位
    bai = item // 100 # 百位
    if ge**3+shi**3+bai**3 == item:
        print(item, "是水仙花数")


```

**流程控制语句break**

- break语句
  用于结束循环结构，通常与分支结构if一起使用
  <img src="https://gitee.com/yybovo/note-images/raw/master/Typora/python006.png" alt="image-20211218104828695" style="zoom: 80%;" />

```python
# 从键盘录入密码，最多录入3次，如果正确就结束循环
for _ in range(3):
    pwd = input("请输入密码！")
    if pwd == '123':
        print("密码正确！")
        break
    else:
        print("输入错误！请重新输入")

# while循环实现
a = 0
while a < 3:
    pwd = input("请输入密码！")
    if pwd == '123':
        print("密码正确！")
        break
    else:
        print("输入错误！请重新输入")
    a += 1
```

**流程控制语句continue**

- 用于结束当前循环，进入下一次循环，通常与分支结构中的if一起使用
  ![image-20211218110300802](https://gitee.com/yybovo/note-images/raw/master/Typora/python007.png)

```python
# 要求输出1到50之间所有不是5的倍数，5,10,15,20....
# 只要不能被5整除的数都不是5的倍数
for item in range(1, 51):
    if item % 5 == 0:
        continue
    print(item, "不是5的倍数")

```

**else语句**

与else语句配合使用的三种情况
![image-20211218111310417](https://gitee.com/yybovo/note-images/raw/master/Typora/python008.png)

```python
for _ in range(3):
    pwd = input("请输入密码：")
    if pwd == '123':
        print("密码正确")
        break
    else:
        print("密码错误，请重新输入")
else:
    print('对不起，您的账号已锁定，请联系工作人员...')
    
a = 0
while a < 3:
    pwd = input("请输入密码：")
    if pwd == '123':
        print("密码正确")
        break
    else:
            print("密码错误，请重新输入")
    a += 1
else:
    print('对不起，您的账号已锁定，请联系工作人员...')
```

**嵌套循环**

循环结构中又嵌套了另外的完整的循环结构，其中内层循环做为外层循环的循环体执行

![image-20211218115223120](https://gitee.com/yybovo/note-images/raw/master/Typora/python009.png)

```python
# 输出一个三行四列的矩形
for i in range(1, 4):
    for j in range(1, 5):
        print('*', end='\t') # 不换行输出
    print() # 换行

# 输出一个直角三角形
for i in range(1, 5):
    for j in range(1, i+1):
        print('*',end='')
    print()

# 99乘法表
for i in range(1,10):
    for j in range(1,i+1):
        print(i,'*',j,'=',i*j,end='\t')
    print()
```

**二重循环中的break和continue**

二次循环中的break和continu用于控制本次循环
![image-20211218121255489](https://gitee.com/yybovo/note-images/raw/master/Typora/python010.png)

```python

for i in range(5):
    for j in range(1, 11):
        if j % 2 == 0:
            break
        print(j, end='')#111111


for i in range(5):
    for j in range(1, 11):
        if j % 2 == 0:
            continue
        print(j, end='')# 1357913579135791357913579
```



## 列表

变量可以储存一个元素、而列表是一个”大容器“可以存储N多个元素，程序可以方便地对这些数据进行整体操作。

列表相当于其它语言中的数组。

列表示意图
![image-20211218194154176](https://gitee.com/yybovo/note-images/raw/master/Typora/python011.png)

```python
# 变量储存的是一个对象的引用
lst = ['hello', 'world', 98]
print(id(lst))
print(type(lst))
print(lst)
```

![image-20211218200604578](https://gitee.com/yybovo/note-images/raw/master/Typora/python012.png)

### 列表的创建方式

- 使用中括号
- 使用内置函数list()

```python
# 使用[] 创建列表
lst = ['hello', 'world', 98]
# 使用内置函数创建列表
lst2 = list(['hello', 'world', 98])
```

### 列表的特点

- 列表元素按顺序有序排序
- 索引映射唯一个数据
- 列表可以存储重复数据
- 任意数据类型混存
- 根据需要动态分配和回收内存

### 列表的查询操作

![image-20211218202017037](https://gitee.com/yybovo/note-images/raw/master/Typora/python013.png)

```python
# 获取列表中指定元素的索引
lst = ['hello', 'world', 98, 'hello']
print(lst.index('hello')) # 查找()里的索引，如果列表有相同元素只返回列表中相同元素的第一个索引
# print(lst.index('python')) # ValueError: 'python' is not in list
print(lst.index('hello', 1, 4)) # (要查找索引的元素，起始索引，结束索引)

```

![image-20211218203550600](https://gitee.com/yybovo/note-images/raw/master/Typora/python014.png)

列表名[start(起始索引): stop(结束索引): step(步长)]

```python
lst = [10, 20, 30, 40, 50, 60, 70]
# print(lst[1:6:1]) # [20, 30, 40, 50, 60]
lst2 = lst[1:6:1]
print(id(lst)) # 2657030357248
print(id(lst2)) # 2657030255424
# 说明切片列表是产生的新的地址
```

### 列表元素的查询操作

判断指定元素在列表是否存在
元素 `in` 列表名
元素 `not in` 列表名

列表元素的遍历
`for` 迭代变量 `in` 列表名 :
         操作

```python
# 判断
lst = ['hello', 'world', 10, 20]
print(10 in lst) # True
print(100 in lst) # False
print(10 not in lst) # False
print(100 not in lst) # True
# 遍历
for item in lst:
    print(item, end='\t') # hello	world	10	20
```

### 列表元素的增加操作

方法
`append() ` 在列表的末尾添加一个元素
`extend()` 在列表的末尾至少添加一个元素
`insert()` 在列表的任意位置添加一个元素
`切片`           在列表的任意位置添加至少一个元素

```python
lst = [10, 20, 30, 40]
lst.append(50)
print(lst) # [10, 20, 30, 40, 50]
lst2 = ['hello', 'world']
# lst.append(lst2) # lst2作为一个元素添加到列表的末尾
# print(lst) # [10, 20, 30, 40, 50, ['hello', 'world']]

# 先列表的末尾一次性添加多个元素
lst.extend(lst2)
print(lst) #[10, 20, 30, 40, 50, 'hello', 'world']

# 在任意位置添加一个元素
lst.insert(0, '插班生') # 在1的索引插入元素
print(lst) # ['插班生', 10, 20, 30, 40, 50, 'hello', 'world']
lst.insert(-1, '插班生') # 在-1的索引插入元素
print(lst) # ['插班生', 10, 20, 30, 40, 50, 'hello', '插班生', 'world'] 出现错误！！！

lst3 = ['白小纯', '宋君婉', '杜凌菲']
# 切片 在任意的位置上添加N多个元素
lst[1:] = lst3 # ['插班生', '白小纯', '宋君婉', '杜凌菲'] 从索引1开始直接覆盖
print(lst) # ['插班生', '白小纯', '宋君婉', '杜凌菲']
```

### 列表元素的删除操作

![image-20211219131426462](https://gitee.com/yybovo/note-images/raw/master/Typora/python015.png)

```python
lst = [10, 20, 30, 40, 50, 60, 30]
lst.remove(30) # 从列表移除一个元素，如果有重复元素只移第一个元素
print(lst) # [10, 20, 40, 50, 60, 30]
# lst.remove(100) # ValueError: list.remove(x): x not in list

# pop()根据索引移除元素
lst.pop(1)
print(lst) # [10, 40, 50, 60, 30]
lst.pop() # 如果不指定参数（索引），将删除列表中的最后一个元素

# 切片 删除操作 删除至少一个元素，将产生一个新的列表对象
new_list = lst[1:3]
print('原列表', lst) # 原列表 [10, 40, 50, 60]
print('切片后的列表', new_list) # 切片后的列表 [40, 50]
# 不产生新的列表对象，而是删除原列表中的内容
lst[1:3] = []
print(lst) # [10, 60]

# 清除列表中的所有元素
lst.clear()
print(lst) #[]

# del语句将列表对象删除
del lst
# print(lst) # NameError: name 'lst' is not defined
```

### 列表元素的修改操作

列表元素的修改操作
为指定索引的元素赋予一个新值
为指定的切片赋予一个新值

```python
lst = [10, 20, 30, 40]
# 一次修改一个值
lst[2] = 100
print(lst) # [10, 20, 100, 40]
# 切片
lst[1:3]=['插班生1', '插班生2', '插班生3']
print(lst) # [10, '插班生1', '插班生2', '插班生3', 40]
```

### 列表元素的排序操作

常见的两种方式

- 调用sort()方法，列有中的所有元素默认按照从小到大的顺序进行排序，可以指定reverse = True，进行降序 排序

  ```python
  lst = [20, 40, 10, 98, 54]
  print('排序前的列表', lst, id(lst)) # 排序前的列表 [20, 40, 10, 98, 54] 2170865434752
  # 开始排序 调用列表对象的sort方法，升序排序
  lst.sort()
  print('排序后的列表', lst, id(lst))# 排序后的列表 [10, 20, 40, 54, 98] 2170865434752
  # 通过关键字参数，将列表中的元素进行降序排序
  lst.sort(reverse=True)
  print(lst) # [98, 54, 40, 20, 10]
  ```

- 调用内置函数sorted(),可以指定reverse=True、进行降序排序、原列表不发生改变。

  ```python
  lst = [20, 40, 10, 98, 54]
  # 使用内置函数sorted()对列表进行排序，将产生一个新的列表对象
  print(sorted(lst, reverse=False)) # [10, 20, 40, 54, 98]
  print(sorted(lst, reverse=True)) # [98, 54, 40, 20, 10]
  print(lst) # [20, 40, 10, 98, 54]
  ```

### 列表生成式

列表生成式简称"生成列表的公式"

- 语法格式

  ![image-20211219141547976](https://gitee.com/yybovo/note-images/raw/master/Typora/python016.png)

- 注意事项："表示列表元素的表达式"中通常包含自定义变量

```python
lst = [i for i in range(1, 10)]
print(lst) # [1, 2, 3, 4, 5, 6, 7, 8, 9]
lst = [i*i for i in range(1, 10)]
print(lst) # [1, 4, 9, 16, 25, 36, 49, 64, 81]

# 列表中的元素为2,4,6,8,10....
lst2 = [i*2 for i in range(1, 6)]
print(lst2) # [2, 4, 6, 8, 10]
```



## 字典

Python内置的数据结构之一，与列表一样是一个可变序列
以键值对的方式储存数据，字典是一个无序的序列

```python
scores = {'张三' ： 100, '李四' : 98, '王五': 45}
```

![image-20211219144523995](https://gitee.com/yybovo/note-images/raw/master/Typora/python017.png)

**实现原理**

字典的实现原理与查字典类似，查字典是先根据部首或拼音查找汉字对应的页码，Python中的字典是根据key查找value所在的位置。

### 字典的创建

- 使用花括号

  ```python
  scores={ '张三': 100, '李四': 98, '王五': 45 }
  ```

- 使用内置函数dict()

  ```python
  dict( name ='jack', age = 20 )
  ```

### 字典的常用操作

- 字典中元素的获取

![image-20211219192557393](https://gitee.com/yybovo/note-images/raw/master/Typora/python018.png)

- `[]`取值与使用get()取值的区别
  - `[]`如果字典不存在指定的key，抛出keyError异常。
  - get()方法取值，如果字典中不存在指定的key，并不会抛出keyError而是None，可以通过参数设置默认的value，以便指定的key不存在时返回的默认值

```python
scores = {'张三': 100, '李四': 90, '王五': 80}
# 第一种方式，使用[]
print(scores['张三'])
# print(scores['赵六']) # KeyError: '赵六'

# 第二种方式，使用get()方法
print(scores.get('张三'))
print(scores.get('赵六')) # None
print(scores.get('白小纯', '不存在')) # 通过参数设置默认的value，以便指定的key不存在时返回的默认值
```

- key的判断
  ![image-20211219193956896](https://gitee.com/yybovo/note-images/raw/master/Typora/python019.png)

- 字典元素的删除

  ```python
  del scores['张三']
  ```

- 字典元素的新增

  ```python
  scores['jack']=90
  ```

  ```python
  scores = {'张三': 100, '李四': 90, '王五': 80}
  print('张三' in scores) # True
  print('张三' not in scores) # False
  
  
  del scores['张三'] # 删除指定的key-value对
  print(scores) # {'李四': 90, '王五': 80}
  # scores.clear() # 清空字典的元素
  print(scores) # {}
  
  scores['张三']=100
  print(scores) # {'李四': 90, '王五': 80, '张三': 100}
  ```

- 获取字典视图的三个方法

![image-20211219195139629](https://gitee.com/yybovo/note-images/raw/master/Typora/python020.png)

```python
scores = {'张三': 100, '李四': 90, '王五': 80}
# 获取所有的key
keys = scores.keys()
print(keys) # dict_keys(['张三', '李四', '王五'])
print(type(keys)) # <class 'dict_keys'>
print(list(keys)) # ['张三', '李四', '王五'] 将所有的key组成的视图转成列表

# 获取所有的value
values = scores.values()
print(values) # dict_values([100, 90, 80])
print(type(values)) # <class 'dict_values'>
print(list(values)) # [100, 90, 80] 将所有的value组成的视图转成列表

# 获取所有的key和value
print(scores.items()) # dict_items([('张三', 100), ('李四', 90), ('王五', 80)])
print(type(scores.items())) # <class 'dict_items'>
print(list(scores.items())) # [('张三', 100), ('李四', 90), ('王五', 80)] 转换之后的列表元素是由元组组成的
```

- 字典元素的遍历

  ```python
  scores = {'张三': 100, '李四': 90, '王五': 80}
  # 字典元素的遍历
  for item in scores:
      print(item, scores.get(item),scores[item], end='\t') # 张三 100 100	李四 90 90	王五 80 80	
  ```

### 字典的特点

- 字典中的所有元素都是一个key-value对，key不允许重复，value可以重复
- 字典中的元素是无序的
- 字典中的key必须是不可变对象
- 字典也可以根据需要动态的伸缩
- 字典会浪费比较大的内存，是一种使用空间换时间的数据结构

### 字典生成式

- 内置函数`zip()`
  - 用于将可迭代的对象作为参数，将底下中对应的元素打包成一个元组，然后返回由这些元组组成的列表

![image-20211219201515562](https://gitee.com/yybovo/note-images/raw/master/Typora/python021.png)

```python
item = ['Fruits', 'Books', 'Others']
price = [96, 78, 85]
lst = zip(item,price)
print(list(lst)) # [('Fruits', 96), ('Books', 78), ('Others', 85)]
```



![image-20211219202133321](https://gitee.com/yybovo/note-images/raw/master/Typora/python022.png)

```python
item = ['Fruits', 'Books', 'Others']
price = [96, 78, 85]
lst = {item: price for item, price in zip(item, price)}
print(lst) # {'Fruits': 96, 'Books': 78, 'Others': 85}
lst1 = {item.upper(): price for item, price in zip(item, price)} #upper() 值大写的属性
print(lst1) # {'FRUITS': 96, 'BOOKS': 78, 'OTHERS': 85}
```



## 元组

 Python内置的数据结构之一，是一个不可变序列

```python
t = ( 'Python', 'hello', 90 )
```



### 不可变序列与可变序列

- 不可变序列：字符串、元组
  - 不可变序列：没有增、删、改的操作
- 可变序列：列表、字典
  - 可变序列：可以对序列执行增、删、改操作，对象地址不发生更改

```python
"""可变序列 列表，字典"""
lst = [10, 20, 45]
print(id(lst)) # 1876356276032
lst.append(300)
print(id(lst)) # 1876356276032
"""不可变序列，字符串，元组"""
s = 'hello'
print(id(s)) # 1876354885168
s = s + 'wrold'
print(id(s)) # 1876354873520
```

**为什么要将元组设计成不可变序列**

- 在多任务环境下，同时操作对象时不需要加锁
- 在程序中尽量使用不可变序列

注意事项
元组中储存的是对象的引用

- 如果元组中的对象本身是不可变对象，则不能再引起其他对象
- 如果元组中的对象是可变对象，则可变对象的引用不允许改变，单数据可以改变

![image-20211220201436703](https://gitee.com/yybovo/note-images/raw/master/Typora/python023.png)

```python
t = ('python', [10,20], 'hello')
print(t) # ('python', [10, 20], 'hello')
print(type(t)) # <class 'tuple'>
print(id(t[0]), id(t[1]), id(t[2])) # 2205326926768 2205328383936 2205326992944
t[1].append(100)
print(t) # ('python', [10, 20, 100], 'hello') 列表是可变序列，所以可以向列中添加元素，而列表内存地址不变
print(id(t[1])) # 2205328383936
```



### 元组的创建方式

- 元组的创建方式

  - 直接小括号

    ```python
    t = ('python', 'java', 90)
    # 简写可以去掉小括号
    t = 'python', 'java', 90
    ```

  - 使用内置函数tuple()

    ```python
    t = tuple( 'python', 'java', 90 )
    ```

  - 只包含一个元组的元素需要使用逗号和小括号

    ```python
    # 如果元组只有一个元素不管加不加小括号只要没有逗号会成str类型
    t = ( 10, )
    ```

### 元组的遍历

- 元组是可迭代对象，所以可以使用for...in进行遍历

  ```python
  t = tuple(('python', 'hello', 90))
  for item in t:
      print(item, end='\t') # python	hello	90	
  ```


## 集合



python语言提供的内置数据结构
与列表、字典一样都属于可变类型的序列
集合是没有value的字典
![image-20211221185216459](https://gitee.com/yybovo/note-images/raw/master/Typora/python024.png)

### 集合的创建方式

<font color=red>集合的元素不能重复</font>

- 直接{}

  ```python
  s = {'python', 'hello', 90}
  ```

- 使用内置函数set()

  ```python
  s = set(range(6))
  print(s) # {0, 1, 2, 3, 4, 5}
  print(set([3, 4, 53, 56])) # {56, 3, 4, 53}
  print(set((3,4,43,435))) # {43, 3, 4, 435}
  print(set('Python')) # {'h', 'n', 'P', 'o', 't', 'y'}
  print(set({124, 3, 4, 4, 5})) # {4, 3, 124, 5}
  # s = {} 是空字典不是空集合
  print(set()) # set() 这个才是空集合
  ```

### 集合的相关操作

**集合元素的判断操作**

in 或 not in

**集合元素的新增操作**

- 调用add()方法，一次添加一个元素

- 调用update()方法至少添加一个元素

  ```python
  s = {10, 20, 30, 405, 60}
  s.add('白小纯')
  print(s) # {20, 405, 10, '白小纯', 60, 30}
  s.update({'杜凌菲', '宋君婉'})
  s.update({100, 20, 10})
  print(s) # {100, 10, 20, 405, '宋君婉', '白小纯', '杜凌菲', 60, 30} 元组，列表都可以放入然后转成集合元素
  ```

**集合元素的删除操作**

- 调用remove()方法，一次删除一个指定元素，如果指定的元素不存在抛出KeyError

- 调用discard()方法，一次删除一个指定元素，如果指定元素不存在不抛出异常

- 调用pop()方法，一次只删除一个任意元素

- 调用clear()方法，清空集合

  ```python
  s = {10, 20, 30, 405, 60}
  s.remove(60)
  print(s)
  # s.remove('白小纯') KeyError: '白小纯
  
  s.discard(405)
  print(s) # {20, 10, 30}
  s.discard('白小纯') # 指定元素不存在也不会报错
  
  s.pop() # 删除任意元素（随机的）
  # s.pop(30) # TypeError: set.pop() takes no arguments (1 given) 不能添加参数
  print(s)
  
  s.clear() # 清除所有元素
  print(s) # set()
  ```

### 集合间的关系

<img src="https://gitee.com/yybovo/note-images/raw/master/Typora/python025.png" alt="image-20211221193032948" style="zoom: 50%;" />

- 两个集合是否相等
  可以使用运算符`==`或`!=`进行判断

  ```python
  s = {10, 20, 30, 40}
  s1 = {30, 40, 20, 10}
  print(s == s1) # True
  ```

- 一个集合是否是另一个集合的子集
  可以调用方法issubset进行判断
  b是a的子集

  ```python
  # 一个集合是否是另一个集合的子集
  s = {10, 20, 30, 40}
  s1 = {30, 40, 20}
  print(s.issubset(s1)) # False
  print(s1.issubset(s)) # True
  ```

- 一个集合是否是另一个集合的超集(可以理解为父集)
  可以调用方法issuperset进行判断
  a是b的超集

  ```python
  # 一个集合是否是另一个集合的超集
  s = {10, 20, 30, 40, 50}
  s1 = {30, 40, 20}
  s2 = {30, 20, 90}
  print(s.issuperset(s1)) # True
  print(s.issuperset(s2)) # False
  ```

- 两个集合是否没有交集
  可以调用方法isdisjoint进行判断

  ```python
  # 判断两个集合有没有交集 (没有交集是True,有交集是False)
  s = {10, 20, 30, 40, 50}
  s1 = {30, 40, 20}
  s2 = {80, 60, 90}
  print(s.isdisjoint(s1)) # False
  print(s.isdisjoint(s2)) # True
  ```

**集合的数学操作**

<img src="https://gitee.com/yybovo/note-images/raw/master/Typora/python026.png" alt="image-20211221194623330" style="zoom:50%;" />

```python
# 交集 intersection()
s1 = {10, 20, 30, 40}
s2 = {20, 30, 80, '白小纯'}
print(s1.intersection(s2)) # {20, 30}
print(s1 & s2) # intersection() 与 & 等价 交集操作

# 并集 union()
print(s1.union((s2))) # {40, 10, '白小纯', 80, 20, 30}
print(s1| s2) # union() 与 | 等价 并集操作

# 差集 difference()
print(s1.difference(s2)) # {40, 10}  s1-(s1 U s2)也就s1减去s1和s2的交集
print(s2.difference(s1)) # {80, '白小纯'}
print(s1 - s2) # difference() 与 - 等价 差集操作
print(s2 - s1)

# 对称差集 symmetric_difference()
print(s1.symmetric_difference(s2)) # {'白小纯', 40, 10, 80}
print(s1 ^ s2) # symmetric_difference() 与 ^ 等价 对称差集
```

### 集合生成式

- 用于生成集合的公式

  ```python
  { i * i for in range(1,10) }
  ```

- 将`{}`修改为`[]`就是列表生成式

- 没有元组生成式



## 总结

![image-20211221201741417](https://gitee.com/yybovo/note-images/raw/master/Typora/python027.png)

## 字符串

在python中字符串是基本数据类型，是一个不可变的字符序列

### 字符串驻留机制

仅保存一份相同且不可变字符串的方法，不同的值被存放在字符串的柱留池中，python的驻留机制对相同的字符串只保留一份拷贝，后续创建相同字符串时，不会开辟新空间，而是叭该字符串的地址赋给新创建的变量。

```python
a = 'python'
b = "python"
c = '''python'''
print(id(a), id(b), id(c)) # 2638843831216 2638843831216 2638843831216
```

**驻留机制的交互模式**

- 字符串的长度为0或1时

- 符合标识符的字符串

- <font color=red>字符串只在编译时进行驻留，而非运行时</font>

- [-5,256]之间的整数数字

  ```python
  a = '-6'
  b = '-6'
  import sys # 导入sys包 调用方法强制驻留
  a = sys.intern(b)
  print(id(a),id(b)) # 1550655710128 1550655710128
  ```

  sys中的intern方法强制2个字符串指向同一个对象
  Pycharm对字符串进行了优化处理

**字符串驻留机制的优缺点**

- 当需要值相同的字符串时，可以直接从字符串池里拿来使用，避免频繁的创建和销毁，提升效率和节约内存，因此拼接字符串和修改字符串是会比较影响性能的。

- 在需要进行字符串拼接时建议使用str类型的join方法，而非+，因为join()方法是先计算出所有字符中的长度，而后在拷贝，只new一次对象，效率要比"+"效率高

  ```python
  'ab'.join('c')
  ''.join(['ab', 'c'])
  ```

### 字符串的常用操作

**字符串的查询操作的方法**

![image-20211222160704648](https://gitee.com/yybovo/note-images/raw/master/Typora/python028.png)

```python
s = 'aybshdsaybd'
print(s.index('ay')) # 0
print(s.find('ay')) # 0
print(s.rindex('ay')) # 7
print(s.rfind('ay')) # 7
```

**字符串大小写转换操作的方法**

![image-20211222162927492](https://gitee.com/yybovo/note-images/raw/master/Typora/python029.png)

```python
s = 'hello,PYTHON' #转换格式之后都会生成新的字符串对象
print(s.upper()) # HELLO,PYTHON
print(s.lower()) # hello,python
print(s.swapcase()) # HELLO,python
print(s.capitalize()) # Hello,python
print(s.title()) # Hello,Python
```

**字符串内容对齐操作的方法**

<img src="https://gitee.com/yybovo/note-images/raw/master/Typora/python030.png" alt="image-20211222163832165" style="zoom:80%;" />

```python
s = 'hello,Python'
print(s.center(20, '*')) # 20是指字符加填充符的长度，*指填充符 居中 ****hello,Python****
print(s.ljust(20, '*')) # 左对齐 hello,Python********
print(s.rjust(20, '*')) # 右对齐 ********hello,Python
print(s.zfill(20)) # 右对齐 00000000hello,Python 用0填充
print('-8888'.zfill(8)) # -0008888
```

**字符串批分操作方法**

![image-20211222165254294](https://gitee.com/yybovo/note-images/raw/master/Typora/python031.png)

```python
s = 'hello world Python'
lst = s.split() # 默认是按空格劈分
print(lst) # ['hello', 'world', 'Python']
s1 = 'hello|world|Python'
print(s1.split(sep='|', maxsplit=1)) #  sep指定劈分符，maxsplit指定劈分次数 ['hello', 'world|Python']
print(s1.rsplit(sep='|', maxsplit=1)) #  从右侧开始劈分 ['hello|world', 'Python']
```

**判断字符串操作的方法**

![image-20211222170615559](https://gitee.com/yybovo/note-images/raw/master/Typora/python032.png)

```python
# 判断是不是合法的标识符
print('yyb'.isidentifier()) # True
print('yyb%'.isidentifier()) # False
# 判断是不是全部由空白字符串组成
print('  '.isspace()) # True
print(' 1 '.isspace()) # False
# 判断是不是全部由字母组成
print('abcdef'.isalpha()) # True
print('1abc'.isalpha()) # False
# 判断全部由十进制组成
print('123'.isdecimal()) # True
print('12adc'.isdecimal()) # Fasle
print('ⅠⅡⅣ'.isdecimal()) # Fasle
# 判断是否全部由数字组成
print('12345'.isnumeric()) # True
print('1a2a3a'.isnumeric()) # Fasle
# 判断是否全部由数字和字母组成
print('12345'.isalnum()) # True
print('123abc'.isalnum()) # True
print('白小纯1'.isalnum()) # True
print('123ab '.isalnum()) # Fasle
```

**字符串操作的其他方法**

![image-20211222175126841](https://gitee.com/yybovo/note-images/raw/master/Typora/python033.png)

```python
s = 'hello,Python'
print(s.replace('Python', 'java')) # (要被替换的字符，替换字符) hello,java
s = 'hello,Python,Python,Python'
print(s.replace('Python', 'Java', 2)) # (要被替换的字符，替换字符, 替换的次数) hello,Java,Java,Python

lst = ['hello', 'java', 'python']
print(' '.join(lst)) # hello java python
lst1 = ('hello', 'java', 'python')
print('|'.join(lst1)) # hello|java|python
print('*'.join('Python')) # P*y*t*h*o*n
```

### 字符串的比较操作

- 运算符：>、>=、<、<=、==、!=
- 比较规则：首先比较两个字符串中的第一个字符串，如果相等则继续比较下一个字符，依次比较下去，直到两个字符中的字符不相等时，其比较结果就是两个字符串的比较结果，两个字符串中的所有后续字符将不再比较。
- 比较原理：两上字符进行比较时，比较的是其ordinal value（原始值），调用内置函数ord可以得到指定字符的ordinal value。与内置函数ord对应的是内置函数chr，调用内置函数chr时指定ordinal value可以得到其对应的字符（就是ASCLL码值的转换）。

```python
print('apple' > 'app') # True
print('apple' > 'banana') # False
print(ord('a'), ord('b')) # 97 98
print(chr(97), chr(98)) # a b
```

### 字符串的切片操作

- 字符串是不可变类型
  不具备增，删，改等操作
  切片操作将产生新的对象

![image-20211222183039273](https://gitee.com/yybovo/note-images/raw/master/Typora/python034.png)

```python
s = 'hello,Python'
s1 = s[:5] # 由于没有指定起始位置，所有从0开始
s2 = s[6:] # 由于没有指定结束位置，所以切到字符串的最后元素
s3 = '!'
print(s1) # hello
print(s2) # Python
print(s3) # !
newstr = s1+s3+s2
print(newstr) # hello!Python
print(s[-6::1]) # Python
```

### 格式化字符串

**格式化字符串的两种方式**

![image-20211222185541120](https://gitee.com/yybovo/note-images/raw/master/Typora/python035.png)

 ```python
 # (1) % 占位符
 name = '张三'
 age = 20
 print('我叫%s,今年%d岁' %(name, age)) # 我叫张三,今年20岁
 
 # (2) {}
 print('我叫{0},今年{1}，我真的叫：{0}'.format(name, age)) # 我叫张三,今年20，我知道叫：张三
 print('{0: .3}'.format(3.1415926)) # .3表示的是一共是3位数 3.14
 print('{0: .3f}'.format(3.1415926)) # .3f表示的是一共是3位小数 3.142
 
 # (3) f-string
 print(f'我叫{name},今年{age}岁') # 我叫张三,今年20岁
 ```

**格式化符号**



| **格式符号** | **转换**                         |
| :----------: | -------------------------------- |
|      %s      | 字符串（也可以用来当做%d 和 %f） |
|      %d      | 有符号的十进制整数               |
|      %f      | 浮点数                           |
|      %c      | 字符                             |
|      %u      | 无符号十进制整数                 |
|      0b      | 转换二进制整数（0b1234）         |
|      %o      | 八进制整数                       |
|      %x      | 十六进制整数（小写ox）           |
|      %X      | 十六进制整数（大写OX）           |
|      %e      | 科学计数法（小写'e'）            |
|      %E      | 科学计数法（大写'E'）            |
|      %g      | %f和%e的简写                     |
|      %G      | %f和%E的简写                     |

​                %06d，表示<font color=red>输出的整数</font>显示位数，不足以0补全，超出当前位数则原样输出

​                %6d，表示<font color=red>输出的整数</font>前后宽度为6，不足的话前面生成相应的空格

​                 %.2f， 表示<font color=red>小数点后</font>显示的小数位数。

  ```python
age = 18
name = 'Tom'
weight = 80.5
stu_id = 1 # %06d，表示输出的整数显示位数，不足以0补全，超出当前位数则原样输出
print('我的名字是%s,今年%d岁了，体重%.2f公斤，我的学号是%03d' %(name,age,weight,stu_id))

#输出 我的名字是Tom,今年18岁了，体重80.50公斤，我的学号是001
  ```

​     

格式化字符串除了`%s`，还可以写为`f '{表达式}'`

  ```python
# f '{表达式}'
print(f'我的名字是{name},今年{age}岁了，体重{weight}公斤，我的学号是{stu_id}')

#输出 我的名字是Tom,今年18岁了，体重80.5公斤，我的学号是1
  ```

`f-`格式化字符串是Python3.6中新增的格式化方法，该方法更更简单易读。

### 字符串的编码转换

![image-20211222193609848](https://gitee.com/yybovo/note-images/raw/master/Typora/python036.png)

编码与解码方式
编码：将字符串转换为二进制数据
解码：将bytes类型的数据转换成字符串类型

```python
s = '天涯共此时'
# 编码
print(s.encode(encoding='GBK')) # 在GBK这种编码格式中，一个中文占两个字节
print(s.encode(encoding='UTF-8')) # 在UTF-8编码格式中，一个中文占三个字节

# 解码
# byte 代表就是一个二进制数据(字节类型数据)
byte = s.encode(encoding='GBK') # 编码
print(byte.decode(encoding='GBK')) # 解码

byte = s.encode(encoding='UTF-8') # 编码
print(byte.decode(encoding='UTF-8')) # 解码
```



## 函数

函数就是执行特定任任何以完成特定功能的一段代码

优点

- 复用代码
- 隐藏细节
- 提高可维护性
- 提高可读性便于调试

**函数的创建**

```python
def 函数名 ([输入参数]):
    函数体
    [return xxx]

# 创建
def calc(a, b):
    c = a + b
    return c


# 调用
result = calc(10, 20)
print(result) # 30

```

### 函数调用的参数传递

- 位置实参
  根据形参对应的位置进行实参传递

  ```python
  # 创建
  def calc(a, b): # a,b称为形式参数，简称形参，形参的位置是在函数的定义处
      c = a + b
      return c
  
  
  # 调用
  result = calc(10, 20) # 10,20称为实际参数的值，实参
  print(result) # 30
  ```

- 关键字实参
  根据形参名进行实参传递
  <img src="https://gitee.com/yybovo/note-images/raw/master/Typora/python037.png" alt="image-20211222193609848" style="zoom: 50%;" />

### 函数调用的参数传递内存分析图

![image-20211223201544247](https://gitee.com/yybovo/note-images/raw/master/Typora/python038.png)

```python
def fun(arg1, arg2):
    print('arg1', arg1) # arg1 11
    print('arg2', arg2) # arg2 [11, 33, 44]
    arg1 = 100
    arg2.append(10)
    print('arg1', arg1) # arg1 100
    print('arg2', arg2) # arg2 [11, 33, 44, 10]
    # return

n1 = 11
n2 = [11, 33, 44]
print('n1', n1) # n1 11
print('n2', n2) # n2 [11, 33, 44]
fun(n1, n2)
print('n1', n1) # n1 11
print('n2', n2) # n2 [11, 33, 44, 10]
```

### 参数传递

在 python 中，类型属于对象，变量是没有类型的：

```python
a=[1,2,3]  
a="Runoob"
```

以上代码中，**[1,2,3]** 是 List 类型，**"Runoob"** 是 String 类型，而变量 a 是没有类型，她仅仅是一个对象的引用（一个指针），可以是 List 类型对象，也可以指向 String 类型对象。

**可更改(mutable)与不可更改(immutable)对象**

在 python 中，strings, tuples, 和 numbers 是不可更改的对象，而 list,dict 等则是可以修改的对象。

- **不可变类型：**变量赋值 **a=5** 后再赋值 **a=10**，这里实际是新生成一个 int 值对象 10，再让 a 指向它，而 5 被丢弃，不是改变a的值，相当于新生成了a。
- **可变类型：**变量赋值 **la=[1,2,3,4]** 后再赋值 **la[2]=5** 则是将 list la 的第三个元素值更改，本身la没有动，只是其内部的一部分值被修改了。

python 函数的参数传递：

- **不可变类型：**类似 c++ 的值传递，如 整数、字符串、元组。如fun（a），传递的只是a的值，没有影响a对象本身。比如在 fun（a）内部修改 a 的值，只是修改另一个复制的对象，不会影响 a 本身。
- **可变类型：**类似 c++ 的引用传递，如 列表，字典。如 fun（la），则是将 la 真正的传过去，修改后fun外部的la也会受影响

python 中一切都是对象，严格意义我们不能说值传递还是引用传递，我们应该说传不可变对象和传可变对象。

### python 传不可变对象实例

**实例(Python 2.0+)**

```python
#!/usr/bin/python 
# -*- coding: UTF-8 -*-  
def ChangeInt( a ):    
    a = 10  b = 2 
    ChangeInt(b) 
    print b # 结果是 2
```



实例中有 int 对象 2，指向它的变量是 b，在传递给 ChangeInt 函数时，按传值的方式复制了变量 b，a 和 b 都指向了同一个 Int 对象，在 a=10 时，则新生成一个 int 值对象 10，并让 a 指向它。

### 传可变对象实例

**实例(Python 2.0+)**

```python
#!/usr/bin/python 
# -*- coding: UTF-8 -*-  
# 可写函数说明 
def changeme( mylist ):   
    "修改传入的列表"   
    mylist.append([1,2,3,4])   
    print "函数内取值: ", mylist   
    return  
# 调用changeme函数 
mylist = [10,20,30] 
changeme( mylist ) 
print "函数外取值: ", mylist
```



实例中传入函数的和在末尾添加新内容的对象用的是同一个引用，故输出结果如下：

```python
函数内取值:  [10, 20, 30, [1, 2, 3, 4]]
函数外取值:  [10, 20, 30, [1, 2, 3, 4]]
```

### 函数的返回值

- <font color=red>函数返回多个值时，结果为元组</font>

  ```python
  def fun(num):
      odd = [] # 存奇数
      even = [] # 存偶数
      for i  in num:
          if i % 2: # 0为False 非0位True来判断
              odd.append(i)
          else:
              even.append(i)
      return odd, even
  print(fun([10, 29, 34, 23, 44, 53, 55])) # ([29, 23, 53, 55], [10, 34, 44])
  ```

- 如果函数没有返回值【函数执行完毕之后，不需要给调用处提供数据】 return可以省略不写

- 函数的返回值，如果是一个，直接返回类型

### 函数的参数定义

函数定义时，给形参设置默认值，只有与默认值不符的时候才需要传递实参

```python
def fun(a, b=10):
    print(a, b)

# 函数的调用
fun(100) # 100 10 只传一个参数，b采用默认值
fun(20, 30) # 20 30 30将默认值10替换
```

- 个数可变的位置参数(一个方法内只能设置一个可变的位置参数)
  定义函数时，可能无法事先确定传递位置的个数时，使用可变的位置参数
  使用*定义个数可变的位置形参
  结果为一个元组

  ```python
  def fun(* args):
      print(args)
  
  fun(10) # (10)
  fun(10, 20, 30) # (10, 20, 30)
  ```

- 个数可变的关键字形参(一个方法内只能设置一个可变的关键字形参)
  定义函数时，无法事先确定传递的关键字实参的个数时，使用可变的关键字形参
  使用**定义个数可变的关键字形参
  结果为一个字典

  ```python
  def fun(** args):
      print(args)
  
  fun(a=10) # {'a': 10}
  fun(a=10, b=20, c=30) # {'a': 10, 'b': 20, 'c': 30}
  ```

  <font color=red>在一个函数定义过程中，既有个数可变的关键字形参，也有个数可变的位置形参，要求，个数可变的位置形参，放在个数可变的关键字形参之前。</font>

### 函数的参数总结

![image-20211224170204211](https://gitee.com/yybovo/note-images/raw/master/Typora/python039.png)

```python
def fun(a, b, c): # a, b, c在函数定义处，所以是形式参数
    print('a=', a, end=' ')
    print('b=', b, end=' ')
    print('c=', c, end='\n')

# 函数的调用
fun(10, 20, 30) # 函数调用时的参数传递，称为位置传参 a= 10 b= 20 c= 30
# lst = [11, 22, 33]
lst = (11, 22, 33)
fun(*lst) # 在函数调用时，将列表中的每个元素都转换为位置实参传入 a= 11 b= 22 c= 33
print('--------------------')
fun(a=100, b=200, c=300) # 函数的调用，所以是关键字实参 a= 100 b= 200 c= 300
dic = {'a': 111, 'b': 222, 'c': 333} #在函数调用时，将列表中的每个元素都转换为关键字实参传入 a= 100 b= 200 c= 300
fun(**dic)
```

### 变量的作用域

程序代码能访问该变量的区域

- 根据变量的有效范围可分为

  - 局部变量
    在函数内定义并使用的变量，只在函数内部有效，局部变量使用<font color=red>global</font>声明，这个变量就会出全局变量

    ```python
    def fun():
        global age
        age = 20;
        print(age)
    fun() # 20
    print(age) # 20
    ```

  - 全局变量
    函数体外定义的变量，可作用与函数内外

### 递归函数

如果一个函数的函数体内调用了该函数本身，这个函数就称为递归函数

递归的组成部分
递归调用与递归终止条件

递归的调用过程
每递归调用一次函数，都会在栈内分配一个栈帧
每执行一次函数，都会释放相应空间

递归的优缺点
缺点：占用内存多、效率低下
优点：思路和代码简单

<img src="https://gitee.com/yybovo/note-images/raw/master/Typora/python040.png" alt="image-20211224184211632" style="zoom:50%;" />

```python
def fac(n):
    if n == 1:
        return 1
    else:
        return n*fac(n-1)

print(fac(6)) # 720

# 斐波那契数列
def fib(n):
    if n==1:
        return 1
    elif n==2:
        return 1
    else:
        return fib(n-1)+fib(n-2)

print(fib(6)) # 8
```



## Bug

### Python的异常处理机制

Python提供了异常处理机制，可以在异常出现时捕获，然后内部"消化"、让程序继续运行

```python
try:
    n1 = int(input('请输入一个整数:'))
    n2 = int(input('请输入另一个整数:'))
    result = n1/n2
    print('结果为：',result)
except ZeroDivisionError:
    print('除数不能为0！！！')
```

**多个except结构**

捕获异常的顺序按照先子类后父类的顺序，为了避免遗漏可能出现的异常，可以在最后增加BaseException

```python
try:
    n1 = int(input('请输入一个整数:'))
    n2 = int(input('请输入另一个整数:'))
    result = n1/n2
    print('结果为：',result)
except ZeroDivisionError:
    print('除数不能为0！！！')
except ValueError:
    print('不是数字哦！')
except BaseException as e:
    print(e)
```

**try...except...else结构**

如果try块中没有抛出异常，则执行else块，如果try中抛出异常，则执行except块

```python
try:
    a = int(input('请输入一个整数 ')) # 1
    b = int(input('请输入第二个整数')) # 0
    result = a / b
except BaseException as e:
    print('出错了', e) # 出错了 division by zero
else:
    print('计算机结果为：', result)
```

**try...except...else...finally结构**

finally块无论是否发送异常都会被执行

```python
try:
    n1 = int(input('请输入一个整数：')) # 1
    n2 = int(input('请输入第二个整数：')) # 2
    result = n1/n2
except BaseException as e:
    print('出错了') # 出错了
    print(e) # division by zero
else:
    print('结果为：', result)
finally:
    print('无论是否产生异常，总会被执行的代码') # 无论是否产生异常，总会被执行的代码
print('程序结束') # 程序结束
```

**traceback模块**

使用traceback模块打印异常信息

```python
# 没导入之前
# print(10/0)
#报错
# Traceback (most recent call last):
#   File "D:\Python program\pythonProject\test.py", line 749, in <module>
#     print(10/0)
# ZeroDivisionError: division by zero


import traceback
try:
    print('---------------')
    num = 10/0
except:
    traceback.print_exc()
# ---------------
# Traceback (most recent call last):
#   File "D:\Python program\pythonProject\test.py", line 760, in <module>
#     num = 10/0
# ZeroDivisionError: division by zero
```



### Python常见的异常类型

![image-20211226200308555](https://gitee.com/yybovo/note-images/raw/master/Typora/python041.png)



## 面向对象

**类与对象**

数据类型

- 不同的数据类型属于不同的类
- 使用内置函数查看类型

Python中一切皆对象



### 类的创建

类的组成：类属性、实例方法、静态方法、类方法

```python
# 在类之外定义的称为函数，在类之内定义的称为方法
class Student:
    native_pace='常德' # 直接写在类方法的变量，称为类属性
    def __init__(self, name, age):
        self.name = name # self.name 称为实体属性，进行了一个赋值的操作，将局部变量的name赋值给实体类
        self.age = age

    # 实例方法
    def eat(self):
        print('学生在吃饭...')

    # 静态方法
    @staticmethod
    def method():
        print('我使用了staticmethod进行修饰，所以我是静态方法')

    # 类方法
    @classmethod
    def cm(cls):
        print('我是类方法，因为我使用了classmethod进行修饰')
```

### 对象的创建

对象的创建又称为类的实例化

语法：
`实例名 = 类名()`

意义：有了实例，就可以调用类中的内容

![image-20211227182014380](https://gitee.com/yybovo/note-images/raw/master/Typora/python042.png)

```python
# 创建对象
stu1 = Student('张三', 20)
stu1.eat() # 学生在吃饭... 对象名.方法名()
print(stu1.name) # 张三
print(stu1.age) # 20


print('-------------------')

Student.eat(stu1) # 与上面用实例调用方法的功能相同 学生在吃饭...
# 类名.方法名(类的对象)-->实际上就是方法定义处的self
```

### 类属性、类方法、静态方法

类属性：类中方法外的变量称为类属性、被该类的所有对象所共享

类方法：使用@classmethod修饰的方法，使用**类名直接访问**的方法

静态方法：使用@staticmethod修饰的方法，使用**类名直接访问**的方法

```python
# 访问类属性
print(Student.native_pace)
# 调用类方法
Student.cm()
# 调用静态方法
Student.sm()
```

### 动态绑定属性和方法

Python是动态语言，在创建对象之后，可以动态地绑定属性和方法

```python
stu1 = Student('张三', 20)
stu1.gender = '男' # 动态绑定性别
print(stu1.name, stu1.age, stu1.gender)
stu1.show = show # 动态绑定方法
stu1.show()
```



## 面向对象的三大特征

> Python内置类属性
>
> **`__dict__ `**: 类的属性（包含一个字典，由类的数据属性组成）
>
> **`__doc__`** :类的文档字符串
>
> **`__name__`**: 类名
>
> **`__module__`**: 类定义所在的模块（类的全名是'__main__.className'，如果类位于一个导入模块mymod中，那么className.__module__ 等于 mymod）
>
> **`__bases__`** : 类的所有父类构成元素（包含了一个由所有父类组成的元组）

```python
class A:
    pass


class B:
    pass


class C(A, B):
    def __init__(self, name, age):
        self.name = name
        self.age = age

# 创建C类的对象
x = C('Jack', 20) # x是c类型的一个实例对象
print(x.__dict__) # 实例对象的属性字典 {'name': 'Jack', 'age': 20}
print(C.__dict__) # 对象的属性字典 {'__module__': '__main__', '__init__': <function C.__init__ at 0x000002690B27C430>, '__doc__': None}
print('-----------------------------')
print(x.__class__) # <class '__main__.C'> 输出了对象所属的类
print(C.__bases__) # C类的父类类型的元素 (<class '__main__.A'>, <class '__main__.B'>)
print(C.__base__) #  <class '__main__.A'> 输出继承父类的第一个父类类型元素
print(C.__mro__) # 类的层次结构 (<class '__main__.C'>, <class '__main__.A'>, <class '__main__.B'>, <class 'object'>)
print(A.__subclasses__()) # 该类的子类的列表 [<class '__main__.C'>]
```

> Python内置方法
>
> **`__len__()`**:通过重写`__len__()`方法，让内置函数len()的参数可以是自定义类型
>
> **`__add__()`**：通过重写`__add__()`方法，可使用自定义对象具有“+”功能
>
> **`__new__()`**:用于创建对象
>
> **`__init__()`**:对创建对象进行初始化

```python
a = 20
b = 100
c = a + b # 两个整数类型的对象的相加操作
d = a.__add__(b)

print(c) # 120
print(d) # 120

class Student:
    def __init__(self, name):
        self.name = name

    def __add__(self, other): # 必须写不然无法实现
        return self.name + other.name # 强制对象相加

    def __len__(self):
        return len(self.name) # 强制计算对象的长度


stu1 = Student('张三')
stu2 = Student('李四')

s = stu1 + stu2 # 实现了两个对象的加法运算
print(s) # 张三李四

lst = [11, 22, 33, 44, 55]
print(len(lst)) # 计算列表元素的长度 5
print(lst.__len__()) # 5

print(len(stu1)) # 2
```



### 封装

提高程序的安全性

- 将数据（属性）和行为（方法）包装到类对象中。在方法内部对属性进行操作，z在类对象的外部调用方法。这样，无需关系方法内部的具体实现细节，从而隔离了复杂度。

- 在Python中没有专门的修饰符用于属性的私有，如果该属性不希望在类对象外部被访问，前边使用两个"_"。

> **`__foo__`**: 定义的是特殊方法，一般是系统定义名字 ，类似 **__init__()** 之类的。
>
> **`_foo`**: 以单下划线开头的表示的是 protected 类型的变量，即保护类型只能允许其本身与子类进行访问，不能用于 **from module import \***
>
> **`__foo`**: 双下划线的表示的是私有类型(private)的变量, 只能是允许这个类本身进行访问了。
>
> **dir()** 函数不带参数时，返回当前范围内的变量、方法和定义的类型列表；带参数时，返回参数的属性、方法列表。如果参数包含方法__dir__()，该方法将被调用。如果参数不包含__dir__()，该方法将最大限度地收集参数信息。

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.__age = age # 年龄不希望在类的外部被使用，所以加了两个__
    def show(self):
        print(self.name,self.__age)

stu = Student('张三', 20)
print(stu.name)
stu.show()
# print(dir(stu)) # 返回当前范围内的变量、方法和定义的类型列表
print(stu.__Student__age) # 在类的外部可以通过 __Student__age 进行访问
```

运行结果

```python
张三
张三 20
20
```



### 继承

即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系

面向对象的编程带来的主要好处之一是代码的重用，实现这种重用的方法之一是通过继承机制。

通过继承创建的新类称为**子类**或**派生类**，被继承的类称为**基类**、**父类**或**超类**。

- 如果一个类没有继承任何类，则默认继承object
- <font color=red>Python支持多继承</font>
- 定义子类时，必须在其构造函数中调用父类的构造函数

```python
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def info(self):
        print(self.name, self.age)


class Student(Person):
    def __init__(self, name, age, stu_no):
        super().__init__(name, age)
        self.stu_no = stu_no


class Teacher(Person):
    def __init__(self, name, age, teachofyear):
        super().__init__(name, age)
        self.teachofyear = teachofyear


stu = Student('张三', 20, '1001')
stu.info() # 张三 20

teacher = Teacher('李四', 34, 10)
teacher.info() # 李四 34
```

*多继承格式：*

```python
class A(object):
    pass


class B(object):
    pass


class C(A, B):
    pass
```

#### 方法重写

- 子类重写后的方法中可以通过super().xxx()调用父类被重写的方法

  ```python
  class Person(object):
      def __init__(self, name, age):
          self.name = name
          self.age = age
  
      def info(self):
          print(self.name, self.age)
  
  
  class Student(Person):
      def __init__(self, name, age, stu_no):
          super().__init__(name, age)
          self.stu_no = stu_no
  
      def info(self):
          super(Student, self).info()
          print('学生ID', self.stu_no)
  
  
  class Teacher(Person):
      def __init__(self, name, age, teachofyear):
          super().__init__(name, age)
          self.teachofyear = teachofyear
  
      def info(self):
          super(Teacher, self).info()
          print('教龄', self.teachofyear)
  
  
  stu = Student('张三', 20, '1001')
  stu.info()
  
  teacher = Teacher('李四', 34, 10)
  teacher.info()
  ```

  *运行结果*

  ```python
  张三 20
  学生ID 1001
  李四 34
  教龄 10
  ```

#### Object类

- object类是所有类的父类，因此所有类都有object类的属性和方法。
- 内置函数dir()可以查看指定对象所有属性
- Object有一个`__str__()`方法，用于返回一个对于"对象的描述"，对应于内置函数str()经常用于print()方法，帮我们查看对象的信息，所以我们经常会对`__str__()`进行重写

```python
class Student(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return '我的名字是{0}，今年{1}岁'.format(self.name, self.age) # 类似java重写toString()方法


stu = Student('张三', 18)
print(dir(stu))
# ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__']
print(stu)
# 我的名字是张三，今年18岁 
```

### 多态

提高程序的可拓展性和可维护性。
多态就是“具有多种形态”，它指的是：即便不知道一个变量所引用的对象到底是什么类型，仍然可以痛殴这个变量调用方法，在运行过程中根据变量所引用对象的类型，动态决定调用那个对象中的方法。

#### 静态语言与动态语言

静态语言实现多态的三个条件

- 继承
- 方法重写
- 父类引用指向子类对象

动态语言的多态崇尚“鸭子类型”当看到一只鸟走起来像鸭子、游泳起来像鸭子、收起来也像鸭子，那么这只鸟就可以被称为鸭子。在鸭子类型中，不需要关心对象是什么类型，到底是不是鸭子，只关心对象的行为

```python
class Animal(object):
    def eat(self):
        print('动物要吃东西')


class Dog(Animal):
    def eat(self):
        print('狗吃骨头')


class Cat(Animal):
    def eat(self):
        print('猫吃鱼')


class Person(object): # 继承的object
    def eat(self):
        print('人吃饭')


def fun(animal):
    animal.eat()

fun(Dog()) # 狗吃骨头
fun(Cat()) # 猫吃鱼
print('-----------------------------')
fun(Person()) # 人吃饭
```

