# JavaSE



我更新了一下！！！

## 基础



**变量类型/变量的四要素**
常用类型：
		int-整数，比如1,23,4,-100
		double-小数，比如1.1,1.0,-100.1,100
		char-字符，比如'a','1','@','+','_'都是字符，用单引号
		String-字符串，比如"这是字符串","abc","12xxx3","456"使用双引号
		boolean-布尔类型

注意
	double a = 1; 整数可以赋值给小数
	int a = 1.1; 报错！！！
	char a = ''; a = '123'; 都报错！字符有且只有1个符号！
	String a = ""; 可以，字符串个数可以是0个也可以是多个
	变量可以先定义，然后再赋值，但是【没有赋值之前不能使用】



**变量名命名规范：**

- 不能用数字开头

- 只能用用字母、_、$开头

- 不能使用关键字（Double、String这些是类名，可以作为变量名，但不推荐）

- 不能重命名
  注意：命名一般不适用_$,一般以小写字母开头

**算术运算符+、-、*、/、%**
	算术运行中：所有数字运算只要有一个是小数，结果就是小数，比如：2.0+1=3.0
	两个整数相除：得到的一定是整数！比如5/2=2;1/2=0;
	+可以用在字符串上，+两边只要有一个是字符串，这就是拼接操作，而不是加法！
	%表示求余，比如：5%2=1,4%2=0
	
**简写、自加、自减**
	a+=b 相当于 a = a + b
	a*=b; a/=b; a-=b; a%=b; 相当于 a = a%b;
	a++; ++a; 就是变量本身加1
	a--; --a; 就是变量本身减1
	

**字节、位**

	- 位：bit，0和1组成
	- 字节byte=8位，8bit（操作系统：64位）
	- 1024个字节=1KB
	- 1024个KB=1MB
	- 1024个MB=1GB
	- 1024个GB=1TB

**类型转换（自动转换和强制转换）**
强制转换发生在数字之间：不能强制转换字符串为数字！
自动转换：小类型赋值给大类型，自动转换
强制转换：将大类型强制转换为小类型，比如小数强制转换为整数，int a = (int)1.23;

**boolean类型和比较运算**

1. 比较得到的结果就是布尔类型：true或者false
2. 比较运算符：> 大于，< 小于，>= 大于等于（不小于），<= 小于等于（不大于），== 等于， != 不等于
3. boolean b1 = a4 * (1 + 2) > 5 - a4 / 3; 先做算术运算，再做比较运算，最后赋值运算

**逻辑运算符**

1. && 用来连接多个条件（boolean），只有全部满足（true）结果为true
2. || 用来连接多个条件（boolean），只要一个满足（true）结果为true
3. 优先级：算术运算 > 比较运算 > 逻辑运算 > 赋值运算
4. &&操作	   true    false
	 true       √        ×
	 false      ×        ×
5. ||操作	   true    false
	 true       √        √
	 false      √        ×
6. !操作	   true    false
	        ×        √

**Scanner扫描器**

1. 第1步：导入扫描器（放类的上面即可）import java.util.Scanner;
2. 第2步：生产扫描器（可以创造多个）Scanner input = new Scanner(System.in);
3. 第3步：使用扫描器（从控制台扫描输入整数、小数、字符串）
4. 输入一个整数：int a1 = input.nextInt();
5. 输入小数：double a2 = input.nextDouble();
6. 输入字符串：String a3 = input.next();

**数据类型**
整数：byte short int long
小数：float double
字符：char
布尔：boolean

**短路运算**
&& 也叫登录与运算，|| 也叫短路或运算
a1 = 5 > 3 || 1 / 0 != 0; // 不报错，短路运算，或者前面有一个是true，后面不需要继续运算
a1 = 5 <= 3 && 1 / 0 != 0; // 不报错，短路运算，并且只要有一个为false，结果为false

**字符串、字符输入**

1. 字符串比较 == 与 equals，字符串应该都是用equals进行比较：字符串1.equals(字符串2)
2. 如果需要输入一个字符：1.输入1个长度的字符串，进行截取；2.输入整数进行转化：(char) input.nextInt();

**== 与 equals(重要) ==**

 它的作⽤是判断两个对象的地址是不是相等。即，判断两个对象是不是同⼀个对象(基本数据 类型==⽐较的是值，引⽤数据类型==⽐较的是内存地址)。

**equals() : 它的作⽤也是判断两个对象是否相等。**但它⼀般有两种使⽤情况： 

情况 1：类没有覆盖 equals() ⽅法。则通过 equals() ⽐较该类的两个对象时，等价于通过 “==”⽐较这两个对象。 情况 2：类覆盖了 equals() ⽅法。⼀般，我们都覆盖 equals() ⽅法来⽐较两个对象的内容是 否相等；若它们的内容相等，则返回 true (即，认为这两个对象相等)。

```java
public class test1 {
   public static void main(String[] args) {
       String a = new String("ab"); // a 为⼀个引⽤
       String b = new String("ab"); // b为另⼀个引⽤,对象的内容⼀样
       String aa = "ab"; // 放在常量池中
       String bb = "ab"; // 从常量池中查找
       if (aa == bb) // true
          System.out.println("aa==bb");
       if (a == b) // false，⾮同⼀对象
          System.out.println("a==b");
       if (a.equals(b)) // true
          System.out.println("aEQb");
       if (42 == 42.0) { // true
       System.out.println("true");
       }
    }
}
```



**null表示空，没有值！用于引用类型！**

> 所有的普通类型都不能赋值null
> 所有的引用类型都可以赋值null，表示值为空，在堆中没有任何动作，没有开辟空间
> 判断某个对象是否null，使用==即可
> 值为null的对象没有内容，也就没有属性、方法一说！调用属性和方法就报错！

```java
// 字符串和null比较
String s = null;
System.out.println(s == null);      // true
// System.out.println(s.equals(null)); // NullPointerException空指针异常
```



**if语句**
if语句的结构：
	 if(条件){
	 	满足条件运行的代码
	 }

1. 条件必须是布尔值：true/false/5>3/5!=4/5>3&&4<2/5>3||4<2
2. 只有满足条件才会运行大括号中的代码，不满足跳过
3. 以下代码完全一样：if(hasAward){}，if(score >= 90){}，if(hasAward == true){}
4. 以下代码完全一样：if(hasAward != true)，if(hasAward == false)，if(! hasAward)
5. 注意：两个==是比较，一个=是赋值

**if...else语句**
if...else语句的结构：
	 if(条件){
	 	满足条件运行的代码
	 }else{
	 	上面的条件不满足运行的代码
	 }

1. 条件必须是布尔值
2. if...else只有一句代码可以省略，但是不推荐！
3. else后面没有括号
4. else不能单独使用

**if...elseif...else**
多重分支语句，其特点：

1. 多个条件，只有一个运行
2. elseif可以有多个（0~n个）
3. else 可以有可以没有（0~1个）
4. elseif 和 else 不能单独使用，必须和if一起

**多重分支选择结构switch：**
switch和if不同：

1. 括号里不是条件，不能使用条件，是一个表达式
2. 表达式匹配的值case不能重复，默认用default匹配
3. 表达式不能是boolean、double小数，只能是int/char/String
特点：default可以写在前面，case排序随意，break可以省略，但是要注意
说明：boolean类型只有true和false；double类型小数有精度损失！

**嵌套选择结构：if可以嵌套使用switch，switch可以嵌套if，if嵌套if等**

**三元运算符**

1. 语法结构：变量 = 条件 ? 满足条件的值 : 不满足条件的值;
2. 条件可以是任意返回boolean类型值的表达式都可以
	int b = 5 > 3 ? 5 : 3;
	int c = (5 > 3 && 3 != 4) ? (6 > 4 ? 6 : 4) : (3);
	char d = "abc".equals(b + "a") ? '对' : '×';

**Random、Math.Random**

第1步：导入随机生成器import java.util.Random;或者import java.util.*;

第2步：创建新的随机生成器Random random = new Random();

第3步：使用随机生成器随机生成数字
double r1 = random.nextDouble(); // 随机数小数，范围0~1
int r2 = random.nextInt(); // 随机生成整数，范围很小~很大
int r3 = random.nextInt(10); // 随机生成10以内（不包含10）的整数：0~9
生成 [-10, -1]： r3 = random.nextInt(10) - 10;
生成 [10-100] 长度91个，起点10：方法：random.nextInt(长度) + 起点;

4. Math也可以用于生成随机数：范围0~1小数
5. 随机生成器的创建：可以传递一个seed种子：new Random(666)，保证生成随机数顺序不变



**while循环**
格式：while(条件){ 满足条件运行的代码 }
循环的要素：
	1. 循环条件;
	2. 循环变量;
	3. 循环内容：重复的事情;
	4. 更新循环条件

debug模式进行程序调试
	1. Eclipse 调试快捷键F6
	2. IDEA 调试快捷键F8

**printf**
	printf不会换行 %n换行
	%s=字符串，%S=大写，%b=布尔，%t=时间格式
	%d=整数，%f=小数，%e=科学计数，%o=八进制，%x=十六进制，%X=十六进制大写
	%5s表示右对齐，%-5s左对齐
	%1$s表示第1个参数，%2$s第2个参数

**判断输入是否正确：**
	if(input.hasNextXxx()){
		Xxx a = input.nextXxx();
	}
	input.hasNextInt() => 输入整数
	input.hasNextDouble() => 输入小数
	对于字符串来讲，一般不需要

**++/--**
	switch(i ++) 与 switch(++ i)，先判断后判断

**while循环**

1. while(条件){ 满足条件运行的代码 }
2. 循环的要素：1. 循环条件;2. 循环变量;3. 循环内容：重复的事情;4. 更新循环条件

**do...while循环**

1. do{ 满足条件运行的代码 }while(条件);
2. do...while和while循环同样具有四个要素
3. 区别：while先判断条件再运行代码；do...while先运行然后再判断你条件，do...while至少运行一次！
4. 所有的循环通用，while能做的do...while也能做；do...while能做的while也能做，无优劣之分，只有合适更合适之分

**次数确定和不确定循环示例：**

1. 不停的询问你是不是猪(y/n),如果回答n就继续不停的询问，直到你回答y时就显示,'你终于承认你是猪了',并退出循环
2. 不停的询要'十块钱,给不给'，如果回答'不给'，就不停的问，问到给为止，最后输出: '拿着十块钱打撸去!'

**for循环**

1. 简洁：对于次数确定的循环非常方便
2. 变量属于for内部的【局部】变量！
3. for/while/do...while没有级别之分，有合适不合适
4. for循环小括号中的两个分号不能少，其他都可以省略

![万年历](https://gitee.com/yybovo/note-images/raw/master/Typora/%E4%B8%87%E5%B9%B4%E5%8E%86.png)

```java
public class H {

	public static void main(String[] args) {
		// 万年历
		int year = 2021;
		int month = 9;
		// 一、求出本月1号是星期几
		// 1. 求出总天数：从1900年1月1日到2020年12月31日
		int allDays = 0;
		for(int y = 1900; y < year; y ++) {
			// 分平年还是闰年
			if(y % 400 == 0 || (y % 4 == 0 && y % 100 != 0)) {
				allDays += 366;
			} else {
				allDays += 365;
			}
		}
		// 2. 从2021年1月1日到2021（year）年12（month）月1日
		for(int m = 1; m < month; m ++) {
			switch(m) {
			case 1:
			case 3:
			case 5:
			case 7:
			case 8:
			case 10:
			case 12:
				allDays += 31;
				break;
			case 4:
			case 6:
			case 9:
			case 11:
				allDays += 30;
				break;
			case 2:
				if(year % 400 == 0 || (year % 4 == 0 && year % 100 != 0)) {
					allDays += 29;
				} else {
					allDays += 28;
				}
				break;
			}
		}
		
		// 3. 加上12月1号这一天
		allDays += 1;
		
		// 4. 总天数对7求余，求出星期几
		int week = allDays % 7;
		if(week == 0) {
			week = 7;
		}
		System.out.println(year + "年" + month + "月1号星期：" + week);
		
		// 二、求出该月总共的天数
		int daysOfMonth = 0;
		switch(month) {
		case 1:
		case 3:
		case 5:
		case 7:
		case 8:
		case 10:
		case 12:
			daysOfMonth = 31;
			break;
		case 4:
		case 6:
		case 9:
		case 11:
			daysOfMonth = 30;
			break;
		case 2:
			if(year % 400 == 0 || (year % 4 == 0 && year % 100 != 0)) {
				daysOfMonth = 29;
			} else {
				daysOfMonth = 28;
			}
			break;
		}
		
		// 打印分两步：
		System.out.println("星期一\t星期二\t星期三\t星期四\t星期五\t星期六\t星期日");
		// 1. 打印空格，比如星期4打印3个
		for(int i = 0; i < week - 1; i ++) {
			System.out.print("\t");
		}
		// 2. 打印日期
		for(int i = 1; i <= daysOfMonth; i ++) {
			System.out.print(i + "\t");
			// 没7天换行
			if((i + week - 1) % 7 == 0) {
				System.out.println();
			}
		}
	}
}
```

**foreach**

首先说一下foreach有的也叫增强for循环，foreach其实是for循环的一个特殊简化版。

<font color=red>相比于for...i：简单，但是只能使用变量，无法给变量赋值！for...i通用。</font>

　　再说一下foreach的书写格式：

　　　　　for（元素类型  元素名称 ： 遍历数组（集合）（或者能进行迭代的））{

　　　　　　语句

　　　　　}

**foreach和for的区别**

　　foreach虽然是for循环的简化版本，但是并不是说foreach就比for更好用，foreach适用于循环次数未知，或者计算循环次数比较麻烦情况下使用效率更高，但是更为复杂的一些循环还是需要用到for循环效率更高。

　　我们看看下面的例子：

```java
 1 public static void main(String[] args) {
 2         List<String> arr = new ArrayList<String>();
 3         arr.add("你好");
 4         arr.add("我好");
 5         arr.add("大家好");
 6         
 7         //foreach循环
 8         for(String str : arr){                    　　//这里的str就是为了获取每次循环的arr中的值
 9             System.out.println(str);           　　　 //就相当于 String str=arr[i]
10         }
11     }
```

　　但是相比较之下我们用for循环输入就略显麻烦

```java
public static void main(String[] args) {
        List<String> arr = new ArrayList<String>();
        arr.add("你好");
        arr.add("我好");
        arr.add("大家好");
        
        //for循环
        for(int i=0;i<arr.size();i++){
            System.out.println(arr.get(i));    //要获取list中元素需要用get方法    
        }
    }
```

　　除了这种普通的集合还可以对像map这种键值对使用

　　例如：　

```java
public static void main(String[] args) {
        Map<String,String> mapstr = new HashMap<String,String>();
        mapstr.put("王", "男");
        mapstr.put("李", "男");
        mapstr.put("张", "女");
        　　　　　　　　　　　　　　　　　　　　//entrySet方法是为了获取键值对的集合
        for(Map.Entry<String, String> s : mapstr.entrySet()){   //这里的Map.Entry<String, String>其实就是一个类型 用来表示键值对的类型
            System.out.println("key="+s.getKey());            //这里其实还是相当于 s=maostr.entrySet，只不过s存储的是键值对。
            System.out.println("value="+s.getValue());        //所以可以用get方法获取出来存储的键值对。
        }
    }
```

　　另外foreach不支持在循环中添加删除操作，因为在使用foreach循环的时候数组（集合）就已经被锁定不能被修改，否则会报出java.util.ConcurrentModificationException异常

　　例如：

```java
public static void main(String[] args) {
        List<String> arr = new ArrayList<String>();
        arr.add("你好");
        arr.add("我好");
        arr.add("大家好");
        
        //foreach循环
        for(String str : arr){                    
            System.out.println(str);            
            arr.add("1");                    //对arr进行添加    
        }
    }
```

　　关于不能添加删除原理以及如何在foreach中添加删除我们下篇再说。

　　所以总结如下：

　　foreach适用于只是进行集合或数组遍历，for则在较复杂的循环中效率更高。

　　foreach不能对数组或集合进行修改（添加删除操作），如果想要修改就要用for循环。

　　所以相比较下来for循环更为灵活。

 



**其他类型**
int/double/char/String/boolean
整数：byte-字节(1byte=8bit)；short-短整型(2bytes=16位)；
int-整数(4bytes=32位)；long-长整型(8bytes=64位)
小数：float-单精度(4bytes=32位)；double-双精度小数（8bytes=64位）



**变量命名要规范：**

1. 能正确表达变量所代表的意思（要么全英文，要么全拼音）
2. 符合要求
3. 类名：大写开头，每个单词首字母大写，ClassA，MyClass、
4. 变量名：小写字母开头，后面的每个单词大写开头，sum，sumOfXxxx

**循环中断关键字(break、continue)**

1. break：跳出循环，循环【直接结束】，不再继续；不能使用在循环（switch）外
2. continue：继续下一轮循环，本次循环后面的代码不会运行了，所以循环时间缩短，并【没有结束】
3. 共同点：都只能使用在循环里；都会影响循环的运行时间；后面都不能直接放代码

**嵌套循环**
外层循环
内层循环，注意内层循环中代码运行次数为：外次数 x 内次数

**ASCII**
使用1个字节保存，char占用2个字节

![ASCII码对照表](https://gitee.com/yybovo/note-images/raw/master/Typora/ASCII.jpg)

**文档注释**

```java
	/**
	 * 这是Java Doc文档注释
	 * @param age 参数表示年龄参数
	 * @param name 名字参数表示名字xxx
	 * @return 返回一个整数，如果你很牛逼就是666
	 */
	public int test(int age, String name) {
		return 666;
	}
```



## 数组



使用数组保存一组【相同类型】的数据，开辟空间后长度【固定不变】

使用new开辟空间：int[] a1 = new int[10]; 使用下标获取元素a1[0]/a1[1]

数组的长度获取：数组名.length；数组的最后一个元素：a1[a1.length - 1]

数组的应用：1.定义数组类型和变量；2.开辟空间；3.使用数组名和下标进行赋值，使用

ArrayIndexOutOfBoundsException 数组下标越界异常，表示下表已经超出范围

简写方法 int[] array1 = new int[]{1, 2, 3}; int[] array2 = {1, 1, 2};

1. 应用
  - 使用for应用数组：求和、赋值、输出、最值
  - 应用：求最值、合并数组、查找元素
  - 默认值：int[]->0, double[]->0.0, char[]->' ', boolean[]->false，String[]->null
  - 数组的复制：
    - 新建数组，开辟空间和要复制的原数组长度一致
    - 使用循环，将原数组的每一个元素复制给新元素对应下表的元素
    - 使用Arrays.toString(数组名)打印数组的每一元素

3. 进制单位
	十进制：int a = 1234;
	二进制一般是 a = 0b110011
	八进制一般是 a = 0123745
	十六进制一般是 a = 0xFF11AA



基本类型包括整数、小数、字符、布尔等都是拷贝的值，字符串String也是拷贝值
<font color=red>数组都是拷贝的是地址，不是值，所以会相互影响！</font>

**<font color=red>数组排序</font>**

- 冒泡排序
  ![冒泡](https://gitee.com/yybovo/note-images/raw/master/Typora/%E5%86%92%E6%B3%A1.gif)

  ```java
  import java.util.Arrays;
  
  public class Test03 {
  	public static void main(String[] args) {
  		//冒泡排序
  		int[] arrays = {9, 2, 3, 6, 5, 4, 1, 7, 8};
  		for (int i = 0; i < arrays.length-1; i++) { //i 循环次数
  			for (int j = 0; j < arrays.length-i-1; j++) { //j 数组索引  arrays.length-i-1 排序次数
  				if (arrays[j] > arrays[j+1]) { //判断数组元素大小
  					int temp = arrays[j];
  					arrays[j] = arrays[j+1];
  					arrays[j+1] = temp;
  				}
  			}
  		}
  		System.out.println(Arrays.toString(arrays));
  	}
  
  }
  
  ```


- 选择排序
  ![选择](https://gitee.com/yybovo/note-images/raw/master/Typora/%E9%80%89%E6%8B%A9.gif)

  ```java
  import java.util.Arrays;
  
  public class Test04 {
  
  	public static void main(String[] args) {
  		// 选择排序
  		int[] arrays = {9, 2, 3, 6, 5, 4, 1, 7, 8};
  		for (int i = 0; i < arrays.length-1; i++) {//循环次数
  			int minIndex = i;//设定最小索引
  			for (int j = i+1; j < arrays.length; j++) {
  				if (arrays[j] < arrays[minIndex]) {//比较选出最小索引
  					   minIndex = j;
  				}
  			}
  			//最小元素互换位置
  			int temp = arrays[i];
  			arrays[i] = arrays[minIndex];
  			arrays[minIndex] = temp;
  		}
  		System.out.println(Arrays.toString(arrays));
  	}
  
  }
  ```

- 插入排序
  ![插入](https://gitee.com/yybovo/note-images/raw/master/Typora/%E6%8F%92%E5%85%A5.gif)

  ```java
  import java.util.Arrays;
  
  public class Test05 {
  
  	public static void main(String[] args) {
  		//插入排序
  		int[] arrays = {8,2,5,9,1,6,3,7,4};
  		for (int i = 0; i < arrays.length; i++) {
  			for (int j =i; j > 0; j--) {
  				if (arrays[j] < arrays[j-1]) {
  					int temp = arrays[j-1];
  					arrays[j-1] = arrays[j];
  					arrays[j] = temp;			
  					
  				}
  			}
  		}
  		System.out.println(Arrays.toString(arrays));
  	}
  }
  
  ```

算法优劣：
	1. 空间复杂度：你在使用这个算法时，需要使用多少内存空间，就是临时变量大小
	2. 时间复杂度：你的算法的效率，比如10个数字排序1秒，100个排序10秒
		- 常数级别：比如10个要1秒，100个也是1秒，1亿个也是1秒（对于排序不存在）
		- 对数级别：比如10个1秒，100个2秒，1000个3秒，1亿9秒（排序不存在，树结构中存在）
		- 线性级别：比如10个要10秒，100个要100秒，200个200秒（对于排序不存在）
		- 线性对数级别：比如快速排序
		- 平方级别：比如1个1秒，2个4秒，10个100秒，100个10000秒（普通算法就是）

Arrays.sort(array); 排序

```java
		// Arrays.sort方法排序
        int[] array = {1, 3, 2, 5, 4};
		Arrays.sort(array);  //{1,}
```

System.arraycopy(原数组, 原数组的起始位置, 目标数组, 目标数组起始位置, 拷贝的长度);

```java
		// 复制数组
		int[] array = {1, 3, 2, 5, 4};
		int[] array1 = new int[array1
		.length];
		// System.arraycopy(原数组,开始位置,新数组,新位置,长度) 复制一个数组到另一个数组
		System.arraycopy(array1, 0, array1, 0, array1.length);
		System.out.println(Arrays.toString(array1));//{1, 3, 2, 5, 4}
```

Arrays.toString(array); 输出调试

### 二维数组

创建二维数组：new 数组名`[行数][列数=每行个数]`
单个元素：array1[1][0] = 1;最后一行第1个和最后一个：array1`[29][0]`;array1`[29][19]`
直接定义和赋值：double[][] array2 = new double[][]{new double[]{1,2,3},...}，或者{{1,2,3},{1.1,2.1,3.1}...};
二维数组名`[二维数组长度][元素个数]`：开辟空间可以省略元素个数，但是长度不能省：new String`[5][]`;
循环数组的总元素个数：一维数组个数=array.length，一维数组的长度=array[i].length

```java
int[][] a = {{1,2,3},{2,3,4},{3,4,5}};
System.out.println(Arrays.deepToString(a)); //[[1, 2, 3], [2, 3, 4], [3, 4, 5]]
```





## 面向对象

面向对象基础：属性、方法
	类是一个模板、抽象的概念：public class 类名
	类由属性和方法组成
	属性：成绩、性别、姓名、年龄，属性表示一种标签、特点、静态特征
	方法：上课、玩游戏、吃喝拉撒…… 方法表示类、对象的动态特征、功能的行为
	定义属性：和定义变量一样！但是有区别：

属性定义在类中，不能写在main入口中

属性可以添加public关键字，普通变量不行

属性可以不赋值有默认值，也可以赋值覆盖默认值，普通变量如果要使用必须赋值！

作用范围：方法中可以使用属性
类中定义方法：public void 方法名(){ 方法内容=代码块 }，运行方法时，方法中代码块被调用，方法中可以使用属性
对象使用方法：对象名.方法名();

对象：

- 创建对象：对象 = new 类名();

- 把创建的对象赋值给变量，使用变量来操作对象 Student a1 = new Student();

- 获取或者设置对象的具体属性值：对象名.属性名 = 值; a1.name = "蔡徐坤";

- 对象的属性没有设置都有默认值！和数组类似

- 使用方法：就是运行方法中的代码：对象.方法名()



### 面向对象基础：属性、方法
类是一个模板、抽象的概念：public class 类名

类由属性和方法组成

属性：成绩、性别、姓名、年龄，属性表示一种标签、特点、静态特征

方法：上课、玩游戏、吃喝拉撒…… 方法表示类、对象的动态特征、功能的行为

定义属性：和定义变量一样！但是有区别：
1. 属性定义在类中，不能写在main入口中
2. 属性可以添加public关键字，普通变量不行
3. 属性可以不赋值有默认值，也可以赋值覆盖默认值，普通变量如果要使用必须赋值！
4. 作用范围：方法中可以使用属性

类中定义方法：public void 方法名(){ 方法内容=代码块 }，运行方法时，方法中代码块被调用，方法中可以使用属性

对象使用方法：对象名.方法名();

对象：
	1. 创建对象 => 对象 = new 类名();
	2. 把创建的对象赋值给变量，使用变量来操作对象 Student a1 = new Student();
	3. 获取或者设置对象的具体属性值：对象名.属性名 = 值; a1.name = "蔡徐坤";
	4. 对象的属性没有设置都有默认值！和数组类似
	5. 使用方法：就是运行方法中的代码：对象.方法名()

方法
	无参方法：public void 方法名(){...}
	有参方法：参数由调用者传递进来
		public void 方法名(参数类型1 参数名1, 参数类型2 参数名2, ...){
			方法内容
			可以使用属性
			可以使用参数
		}
		使用参数：参数的顺序不能变，实际上就是参数个数、参数类型要一一匹配！
	有返回值：public 返回值类型 方法(){ return 返回值; }
		1. 无返回值也可以使用return
		2. 有返回值必须有return，各种情况都要有返回值
		3. return后面不能有其他代码
		4. return返回的是整个方法，而不像嵌套循环中的break
	方法中调用另一个方法：运行另一个方法中的代码块

### 局部变量、临时变量、this
​	this变量：表示当前类（当前对象）
​	属性，也叫全局变量
​	普通变量，也叫局部变量
​	方法中使用变量：就近原则，可以使用this区分局部变量和全局变量



### 方法返回值

​	return关键字，用于方法的返回，比如return 1; return "abc";
​	void表示无返回值，无返回方法，可以使用return;，注意后面不能带值！
​	public 返回类型 方法名(参数可以有、可以没有){
​		方法内容
​		return 返回值;
​	}
​	return 特点：

- 表示返回值，后面返回方法指定类型的值
- 也可以直接返回，用在无返回方法中，直接return结束方法（break只能结束当前循环）
- 有返回值的方法，必须在任何情况下都要有返回！
- 方法不能返回多个值！要么void无返回，要么只能返回一个值

### 方法重载和重写的区别

> 重载就是同样的⼀个⽅法能够根据输⼊数据的不同，做出不同的处理 
>
> 重写就是当⼦类继承⾃⽗类的相同⽅法，输⼊数据⼀样，但要做出有别于⽗类的响应时，你 就要覆盖⽗类⽅法
>
> 方法重写：运行期决定方法调用
> 方法重载：编译器类型决定

### 方法重载
​	方法名字相同，通过不同的方法参数实现方法重载
​	不能通过返回值决定是否是方法重载！
​	参数不同：参数类型、参数个数、参数顺序
​	注意：传递参数可能会被自动转型，比如：
​		a.sum(1, 2); // sum(int, int)
​		a.sum(1.0, 2.0); // sum(double, double)
​		a.sum(1, 2.0); // 自动转型，sum(double, double)

意义：相同含义的方法写成相同的名字，通过参数签名来确定不同的方法调用，方便使用者

相同名字，参数签名必须不同：参数类型、参数的个数、参数的顺序（相当于类型），<font color=red>无法通过返回类型进行重载</font>

方法重载并不能减少代码量，但是利于数据封装、方便调用者使用

<font color=red>方法签名：由方法名、形参列表、返回值以及方法体构成的。</font>

### 方法重写

重写发⽣在运⾏期，是⼦类对⽗类的允许访问的⽅法的实现过程进⾏重新编写。 

- 返回值类型、⽅法名、参数列表必须相同，抛出的异常范围⼩于等于⽗类，访问修饰符范围 ⼤于等于⽗类。 

- 如果⽗类⽅法访问修饰符为 private/final/static 则⼦类就不能重写该⽅法，但是被 static 修饰 的⽅法能够被再次声明。 

- 构造⽅法⽆法被重写 综上：重写就是⼦类对⽗类⽅法的重新改造，外部样⼦不能改变，内部逻辑可以改变

```
/*
 * extends表示继承：A extends B，表示A继承了B类
 * 1. Cat类继承了Animal类，自动拥有了Animal的属性和方法
 * 2. Cat类叫做子类，Animal类叫做父类
 * 3. Java中继承是：单继承，一个类只能继承【一个】父类
 */
public class Cat extends Animal{
	public String color;
	
	public void catchMouse() {
		System.out.println("咖啡猫抓老鼠！");
	}
	
	// 子类依然可以写和父类一样签名的方法：
	// 猫叫的时候能够显示其特性，这种覆盖父类方法的方式叫做：重写
	// 重写时，都应该加上@Override注解，加注解的原因：1.说明是重写，2.防止不小心重写
	@Override
	public void howl() {
		System.out.println("猫在嚎叫：喵……");
	}
}
```

⽅法的重写要遵循“两同两⼩⼀⼤”（以下内容摘录⾃《疯狂 Java 讲义》,issue#892 ）： 

- “两同”即⽅法名相同、形参列表相同；
-  “两⼩”指的是⼦类⽅法返回值类型应⽐⽗类⽅法返回值类型更⼩或相等，⼦类⽅法声明抛出 的异常类应⽐⽗类⽅法声明抛出的异常类更⼩或相等；
-  “⼀⼤”指的是⼦类⽅法的访问权限应⽐⽗类⽅法的访问权限更⼤或相等。 

⭐ <font color=red>关于重写的返回值类型 这⾥需要额外多说明⼀下，上⾯的表述不太清晰准确：如果⽅法的返 回类型是void和基本数据类型，则返回值重写时不可修改。但是如果⽅法的返回值是引⽤类型， 重写时是可以返回该引⽤类型的⼦类的。</font>



| 区别点     | 重载⽅法 | 重写⽅法                                                     |
| ---------- | -------- | ------------------------------------------------------------ |
| 发⽣范围   | 同⼀个类 | ⼦类                                                         |
| 参数列表   | 必须修改 | ⼀定不能修改                                                 |
| 返回类型   | 可修改   | ⼦类⽅法返回值类型应⽐⽗类⽅法返回值类型更⼩或相等           |
| 异常       | 可修改   | ⼦类⽅法声明抛出的异常类应⽐⽗类⽅法声明抛出的异常类更⼩或相等； |
| 访问修饰符 | 可修改   | ⼀定不能做更严格的限制（可以降低限制）                       |
| 发⽣阶段   | 编译期   | 运⾏期                                                       |

```java
public class Hero {
   public String name() {
    return "超级英雄";
 }
}
// 子类依然可以写和父类一样签名的方法：
// name()能够显示其特性，这种覆盖父类方法的方式叫做：重写
// 重写时，都应该加上@Override注解，加注解的原因：1.说明是重写，2.防止不小心重写
public class SuperMan extends Hero{
   @Override
   public String name() {
    return "超⼈";
   }
   public Hero hero() {
    return new Hero();
   }
}
public class SuperSuperMan extends SuperMan {
   public String name() {
    return "超级超级英雄";
   }
   @Override
   public SuperMan hero() {
    return new SuperMan();
  }
}
```



### 引用：

​	类型：
​		基本数据类型（原始、简单）：byte(1字节)/short（2）/int（4）/long（8，64位） float（4）/double（8） char（2）/boolean
​		引用数据类型（对象、复杂）：String、Random、Scanner、数组int[]/char[]...、所有的自定义对象
​		String特殊性：
​			字符串是引用类型
​			传递参数、返回字符串都是值类型
​			String s = "abc";
​			String s = new String("abc");
​	方法参数
​		所有基本类型（int/double/boolean/char）和字符串都是传值！
​		而不是传递变量本身！
​		int a = 100; b1.change1(a); 这里a传递进去的是值，而不是参数
​	方法返回值：数组、对象 - 引用类型
​	Student s1 = new Student();
​	         |         |
​	        引用      对象
​	Student s2 = s1; // 这里s1和s2指向的是同一个对象！
​	对象引用
​		所有基本数据类型和字符串传递参数都是传递的值！
​		返回也是返回的值！
​		<font color=red>只要是new都是创建新的对象（在内存的堆中创建新的对象）</font>

```java
import java.util.Arrays;

public class A {
	int a = 0; // 属性=全局变量
	
	public void change(int a) {
		a = 100;
	}
	public void change(String a) {
		a = "xyz";
	}
	public void change() {
		a = 1; // 修改属性
	}
	public void change(int[] a) {
		System.out.println(a);
		a[0] = 100;
	}
	
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.a); // 0
		a1.change();
		System.out.println(a1.a); // 1
		
		// 普通类型作为参数：传递的是值，而不是变量本身！
		int a = 1;
		a1.change(a);
		System.out.println("a = " + a); // 1
		// String字符串传递的也是值！
		String b = "abc";
		a1.change(b);
		System.out.println("b = " + b); // abc
		
		// 普通类型：byte/short/int/long/float/double/char/boolean
		// 引用类型：String/数组/所有对象，比如Random、Teacher、Object...
		
		// 其他类型：传递的是【引用】，相当于就是本身！
		int[] array = {1,2,3}; //相当于int[] array = new int[]{1,2,3}
		System.out.println(array);
		a1.change(array);
		System.out.println(Arrays.toString(array)); //  100,2,3
		
		// 特列：String，属于引用类型，但是作为参数传递的是值，而不是引用，类似普通类型
		String s1 = "abc";
		String s2 = new String();
	}
}
```

![image-20211223123843940](https://gitee.com/yybovo/note-images/raw/master/Typora/javase001.png)

**栈和堆**

<font color=red>栈内存存储的是局部变量，而堆内存存储的是实体；</font>

<font color=red>栈内存的更新速度要快于堆内存，因为局部变量的生命周期很短；</font>

<font color=red>栈内存存放的变量生命周期一旦结束就会被释放，而堆内存存放的实体会被垃圾回收机制不定时的回收</font>

​	方法使用方法：
​		类中访问属性可以加this：this.属性 = xxx;
​		方法中调用其他方法：this.方法(); 
​		只要不引起歧义，类中都可以省略this

方法的参数传值
	所有基本类型（byte/short/int/long/float/double/boolean/char）和字符串都是传【值】！
	而不是传递变量本身！
	int a = 100; b1.change1(a); 这里a传递进去的是值，而不是参数
	其他类型：对象、自定义类对象、数组等，全部是传递【引用】

### 封装

封装把⼀个对象的属性私有化，同时提供⼀些可以被外界访问的属性的⽅法，如果属性不想被外 界访问，我们⼤可不必提供⽅法给外界访问。但是如果⼀个类没有提供给外界访问的⽅法，那么 这个类也没有什么意义了。

private私有属性：只能在类的内部访问，在外部任意地方无法直接访问

数据封装：1. 私有数据（private属性）；2. 提供必要的访问权限，getXxx获取属性值，setXxx设置属性值（public方法）

访问器：public 类型 getXxx(){} getter访问器，访问数据； public void setXxx(Xxx){} setter访问器，修改数据

只读属性（readonly property）：只有getter访问器，不提供setter访问器的属性，就是只读属性

只写属性，只有setter没有getter，意义不大

数据封装的方式：1. 设置private属性；2.设置public的getter、setter访问器；3. 有些属性不能修改，设置为只读属性，只提供getter方法

布尔类型boolean属性getter访问器[一般]使用：isXxx()，比如public boolean isAdult(){}, public boolean isPassed(){};

<font color=red>【所有】的属性、数据都应该封装起来（private），有利于管理、重构、数据合法性</font>

> 举个例子，如果属性修饰是用public后期在修改成private时都会报错，也能在通过set设置属性值来设置各种条件来保证数据的合法性。

### 包package、修饰符

package 包，相当于文件夹，设置包：package xxx.xxx.xxx; 路径必须匹配！
导包：import xxx.xxx.ClassXXX; 导包后可以使用这个类
全部导入：import xxx.xxx.*;
private 私有，外部都不能访问
缺省的，默认的，只能在同一个包中访问，在不同的包不能访问
protected 受保护的，不同的包不能访问，但是不同包中继承的子类可以访问
public 公开，任意地方可以访问
访问级别：private < 默认的 < protected < public

### 对象数组、对象返回值、对象参数、游离对象、匿名对象

A a = new A(); a为引用，new A()则在内存中创建对象，分配内存存储数据，a只是指向这个对象，所以a成为引用

A b = a; 这里b并不是一个新的对象，只是一个引用名字，继续引用a指向的那个对象，如果b改变那么a指向的对象也会改变

new A(); 这里在内存堆里创建了一个对象，但是没有任何引用，成为匿名、游离的对象，会被JVM垃圾回收

对象参数：对象作为引用传递到方法中内容可以被改变；普通数据类型传递的是值类型，原来的变量不会被改变

对象返回值：直接返回属性，多次调用仍然是同一个对象；返回new 类()则每一次都是返回一个新的对象，各不相关

参数的传递：1. 引用类型都是传递引用； 2. 基础数据类型传递值； 3. 字符串是引用类型，但是传递值

对象与null，String与null判断：赋值为null的对象引用无法使用任何属性和方法

### 对象数组

普通数组：普通类型的数组，int[]/String[]/char[]...
对象数组：比如，需要创建一个班15个学生的一个数组，每一个学生（数组元素）都是Student类型的对象
		数组元素的类型[] 数组名 = new 类型[数组长度];
		Student[] students = new Student[5];
		for(Student s : students) {
			System.out.println(s);
    }
两种赋值方式：
		students[0] = new Student();
		students[0].name = "张三";
		Student s3 = new Student();
		s3.name = "尼古拉斯赵四";
		students[1] = s3;
**防止空指针异常：**
ArrayIndexOutOfBoundsException - 数组下标越界
NullPointerException - 空指针异常，对象是null，但是去使用了对象的属性或者方法
必须判断对象是否为空，否则使用null对象的方法、属性时会报空指针异常
		if(students[i] == null) {
			System.out.println("空对象");
		} else {
			// 可以正常使用对象的属性、方法
			students[i].name = "xxx";
		}

### 构造函数

解决使用set方法随意赋值属性，反复重新给赋值属性
使用构造函数进行传值会生成一个对象，再次调用就会生成另一个新的对象。

**构造函数的特性**

- 名字与类名相同。
- 没有返回值，但不能⽤ void 声明构造函数。
- ⽣成类的对象时⾃动执⾏，⽆需调⽤。

构造方法=构造函数，和方法类似，写法： public 类名(参数){...}，比如 public A(int a){}

构造方法使用在创建对象的时候：类名 对象变量 = new 类名(传参数); 比如 A a1 = new A(123);

构造方法用于构造对象，用于：可以设置属性、能够限制属性值、并且只能设置一次的属性、一次性逻辑封装

说明：

- 所有的类，如果没有手动写构造函数，java会自动添加一个默认的构造函数
- 如果写了构造函数，不管是不是空构造函数都会[覆盖自动的构造函数]
- 允许多个构造函数，类似方法重载

**构造函数重载：**
构造函数可以调用另一个构造，不能使用类名，必须使用this(参数)
调用另外一个构造函数时，this()必须放在第一行的位置
public Teacher(){
	<font color=red>// 调用另一个构造函数，this()必须是第一行</font>
	this("xxx", 18...);
}
public Teacher(String name, int age...){...}

```java
public class Student {
	
	private String name;
	private int age = 1;
	private char gender;
	
	/*
	 * 1. 如果类没有手写构造方法，就会自动生成一个空构造方法
	 * 2. 如果手写任意构造方法，系统不会自动生成空构造方法了！
	 * 3. 构造方法重载：可以写多个构造方法，包括空构造方法
	 * 4. 构造方法调用其他构造方法的方式：this(参数)
	 * 5. 调用其他构造函数的代码this()必须放在【第一行】！
	 */
	// 多个构造方法：构造方法重载！
	public Student(String name) {
		this(name, '男');
		System.out.println("==== 调用了构造方法2：带1个参数");
	}
	
	public Student() {
		this("无名氏");
		System.out.println("==== 调用了构造方法3：无参构造方法");
	}
	
	public Student(String name, char gender) {
		// 必须放第一行
		this(name, gender, 1);
		System.out.println("==== 调用了构造方法1：2个参数");
		/*
		 * this.name = name; this.gender = gender; this.age = 1;
		 */
	}
	
	// 参数多的构造方法相当于：模板
	public Student(String name, char gender, int age) {
		System.out.println("==== 调用了构造方法4：3个参数");
		this.name = name;
		this.gender = gender;
		if(age < 1) {
			age = 1;
		}
		this.age = age;
	}
	
	/*
	 * // 可以定义一个私有方法给构造函数使用：
	 * private void temp(int age) { if(age < 1) { age = 1; } this.age = age; }
	 */
	
	// getter
	public String getName() {
		return name;
	}
	public int getAge() {
		return age;
	}
	public char getGender() {
		return gender;
	}
	
	// 入口
	public static void main(String[] args) {
		// 调用构造方法
		Student s1 = new Student("张三", '男');
		Student s2 = new Student();
//		Student s3 = new Student('男', "张三");
		Student s3 = new Student("李四");
		Student s4 = new Student("张三", '男', 1);
	}

}
```

构造方法：既可以访问普通成员、也可以访问静态成员，类似【非静态】普通方法。静态方法可以正常使用构造方法，说明构造方法类似【静态】方法。构造方法相当于特殊的【静态方法】：可以访问普通成员。

### 继承

继承是使⽤已存在的类的定义作为基础建⽴新类的技术，新类的定义可以增加新的数据或新的功 能，也可以⽤⽗类的功能，但不能选择性地继承⽗类。通过使⽤继承我们能够⾮常⽅便地复⽤以 前的代码。 

关于继承如下 3 点请记住：

- <font color=red>⼦类拥有⽗类对象所有的属性和⽅法（包括私有属性和私有⽅法），但是⽗类中的私有属性 和⽅法⼦类是⽆法访问，只是拥有。</font>

- ⼦类可以拥有⾃⼰属性和⽅法，即⼦类可以对⽗类进⾏扩展。 

- ⼦类可以⽤⾃⼰的⽅式实现⽗类的⽅法。（以后介绍）。

extends关键字 A extends B 那么A继承了B的所有属性和方法
子类继承父类的属性和方法，但是无法访问父类的private成员
所有的类如果没有写父类，那么默认继承于Object，可以省略
对于同名属性/方法：

- 方法同名叫：重写；属性同名叫：重名，不小心重名，避免
- 如果子类有的话，就直接使用子类的
- 如果子类没有，往父类找，如果父类没有继续找到，一直到Object，否则报错
- 如果子类、父类都有：父类的会被覆盖，直接使用子类，除非使用this/super

<font color=red>protected可见性：外部包的子类是可以访问的！</font>
	可见性范围：public > protected(同一个包+子类) > 默认的(同一个包) > private

同一个包：子类可以调用父类的protected方法和默认可见性的方法 
而private以及默认可见性在外部都不可以访问

```java
// 动物类
// Animal类实际上也是继承于Object类，可以省略！
public class Animal extends Object{
	// 动物的属性
	public String type;
	private int age; // 私有属性，子类不可见
	double weight; // 默认可见性的尚需经，子类可见
	protected double speed; // 受保护的可见性的属性，子类可见
	
	// 动物的方法
	public void run() {
		System.out.println("----" + type + "品种的动物在跑！");
	}
	
	public void howl() {
		System.out.println("----动物嚎叫");
	}
	
	// getter方法
	public int getAge() {
		System.out.println("----来自父类的方法调用");
		return age;
	}
}


/*
 * extends表示继承：A extends B，表示A继承了B类
 * 1. Cat类继承了Animal类，自动拥有了Animal的属性和方法
 * 2. Cat类叫做子类，Animal类叫做父类
 * 3. Java中继承是：单继承，一个类只能继承【一个】父类
 */
public class Cat extends Animal{
	public String color;
	
	public void catchMouse() {
		System.out.println("咖啡猫抓老鼠！");
	}
	
	// 子类依然可以写和父类一样签名的方法：
	// 猫叫的时候能够显示其特性，这种覆盖父类方法的方式叫做：重写
	// 重写时，都应该加上@Override注解，加注解的原因：1.说明是重写，2.防止不小心重写
	@Override
	public void howl() {
		System.out.println("猫在嚎叫：喵……");
	}
}

//测试类
public class Main {

	public static void main(String[] args) {
		// 新建一个猫类
		Cat c1 = new Cat();
		c1.color = "咖啡色";
		c1.catchMouse();
		
		// 这些属性和方法来自：Animal类
		c1.type = "咖啡猫";
		c1.run(); // 使用的是父类的方法
		c1.howl(); // 使用的是哪个？
		System.out.println("来自父类的属性：" + c1.type);
		
		// 子类无法使用父类的private属性和方法
		// c1.age = 6;
		System.out.println("猫的年龄：" + c1.getAge());
		
		// 同一个包：子类可以调用父类的protected方法和默认可见性的方法
		c1.weight = 20; // 默认可见性
		c1.speed = 50;  // proetected受保护的
		
		// 新建一个Pig对象
		System.out.println("-------------------");
		Pig p1 = new Pig();
		p1.run();
		p1.howl();
		
		p1.type = "宁乡黑猪";
		System.out.println("品种：" + p1.type);
		p1.run(); // 这个方法没有重写！所以调用的是父类的方法！
		
		/*
		 * 调用方法：
		 * 1. 如果子类没有重写父类的方法：子类和父类都是调用父类的方法
		 * 2. 如果子类重写父类的方法：子类是调用自己的方法，而不是父类
		 * 总结：子类调用方法时，如果子类有则调用自己的方法，否则往上查找父类的方法，如果父类继续查找爷爷类，如果还没找到就报错！
		 * 所有的类最终继承于Object类！
		 */
	}

}
```

**父类构造方法**
父类属性如果不小心覆盖：this.属性和super.属性
方法重写调用父类方法：super.方法()，子类方法：this.方法()，this可以省略

父类构造函数：

- 子类构造时，必须父类先构造，也就是必须调用父类构造函数
- 如果父类是空参数构造函数，子类可以【不用手动】调用父类构造函数
- 如果父类没有空参数构造函数，那么子类必须手动调用父类任意一个构造函数
- 使用super(参数)调用父类构造函数

子类构造的同时，父类的属性会被继承，也拥有了父类的属性值
子类构造的同时，父类肯定先被new构造出来！也就是说：子类构造方法一定隐含地调用了父类构造函数
<font color=red>子类构造方法默认调用父类的空构造函数</font>，所以如果父类没有空构造函数子类无法自动调用
子类构造方法必须调用父类构造方法：要么使用super()手动调用，要么自动调用父类空构造方法！

### **this**

this 是自身的一个对象，代表对象本身，可以理解为：**指向对象本身的一个指针**。

this 的用法在 Java 中大体可以分为3种：

- 普通的直接引用

这种就不用讲了，this 相当于是指向当前对象本身。

- 形参与成员名字重名，用 this 来区分：

*实例*

```java
class Person {
    private int age = 10;
    public Person(){
    System.out.println("初始化年龄："+age);
}
    public int GetAge(int age){
        this.age = age;
        return this.age;
    }
}
 
public class test1 {
    public static void main(String[] args) {
        Person Harry = new Person();
        System.out.println("Harry's age is "+Harry.GetAge(12));
    }
}
```

运行结果：

```java
初始化年龄：10
Harry's age is 12
```

可以看到，这里 age 是 GetAge 成员方法的形参，this.age 是 Person 类的成员变量。

- 引用构造函数

这个和 super 放在一起讲，见下面。

<hr/>

### super

super 可以理解为是指向自己超（父）类对象的一个指针，而这个超类指的是离自己最近的一个父类。

super 也有三种用法：

- 普通的直接引用

与 this 类似，super 相当于是指向当前对象的父类，这样就可以用 **super.xxx** 来引用父类的成员。

- 子类中的成员变量或方法与父类中的成员变量或方法同名

*实例*

```java
class Country {
    String name;
    void value() {
       name = "China";
    }
}
  
class City extends Country {
    String name;
    void value() {
    name = "Shanghai";
    super.value();      //调用父类的方法
    System.out.println(name);
    System.out.println(super.name);
    }
  
    public static void main(String[] args) {
       City c=new City();
       c.value();
       }
}
```

运行结果：

```java
Shanghai
China
```

可以看到，这里既调用了父类的方法，也调用了父类的变量。若不调用父类方法 value()，只调用父类变量 name 的话，则父类 name 值为默认值 null。

**3.引用构造函数**

- **super(参数)**：调用父类中的某一个构造函数（应该为构造函数中的第一条语句）。
- **this(参数)**：调用本类中另一种形式的构造函数（应该为构造函数中的第一条语句）。

*实例*

```java
class Person { 
    public static void prt(String s) { 
       System.out.println(s); 
    } 
   
    Person() { 
       prt("父类·无参数构造方法： "+"A Person."); 
    }//构造方法(1) 
    
    Person(String name) { 
       prt("父类·含一个参数的构造方法： "+"A person's name is " + name); 
    }//构造方法(2) 
} 
    
public class Chinese extends Person { 
    Chinese() { 
       super(); // 调用父类构造方法（1） 
       prt("子类·调用父类"无参数构造方法"： "+"A chinese coder."); 
    } 
    
    Chinese(String name) { 
       super(name);// 调用父类具有相同形参的构造方法（2） 
       prt("子类·调用父类"含一个参数的构造方法"： "+"his name is " + name); 
    } 
    
    Chinese(String name, int age) { 
       this(name);// 调用具有相同形参的构造方法（3） -> Chinese(String name)
       prt("子类：调用子类具有相同形参的构造方法：his age is " + age); 
    } 
    
    public static void main(String[] args) { 
       Chinese cn = new Chinese(); 
       cn = new Chinese("codersai"); 
       cn = new Chinese("codersai", 18); 
    } 
}
```



运行结果：

```java
父类·无参数构造方法： A Person.
子类·调用父类”无参数构造方法“： A chinese coder.
父类·含一个参数的构造方法： A person's name is codersai
子类·调用父类”含一个参数的构造方法“： his name is codersai
父类·含一个参数的构造方法： A person's name is codersai
子类·调用父类”含一个参数的构造方法“： his name is codersai
子类：调用子类具有相同形参的构造方法：his age is 18
```

从本例可以看到，可以用 super 和 this 分别调用父类的构造方法和本类中其他形式的构造方法。

例子中 Chinese 类第三种构造方法调用的是本类中第二种构造方法，而第二种构造方法是调用父类的，因此也要先调用父类的构造方法，再调用本类中第二种，最后是重写第三种构造方法。

<hr/>

### super 和 this的异同

- super(参数)：调用基类中的某一个构造函数（应该为构造函数中的第一条语句）
- this(参数)：调用本类中另一种形成的构造函数（应该为构造函数中的第一条语句）
- super:　它引用当前对象的直接父类中的成员（用来访问直接父类中被隐藏的父类中成员数据或函数，基类与派生类中有相同成员定义时如：super.变量名 super.成员函数据名（实参） this：它代表当前对象名（在程序中易产生二义性之处，应使用 this 来指明当前对象；如果函数的形参与类中的成员数据同名，这时需用 this 来指明成员变量名）
- 调用super()必须写在子类构造方法的第一行，否则编译不通过。每个子类构造方法的第一条语句，都是隐含地调用 super()，如果父类没有这种形式的构造函数，那么在编译的时候就会报错。
- super() 和 this() 类似,区别是，super() 从子类中调用父类的构造方法，this() 在同一类内调用其它方法。
- super() 和 this() 均需放在构造方法内第一行。
- 尽管可以用this调用一个构造器，但却不能调用两个。
- this 和 super 不能同时出现在一个构造函数里面，因为this必然会调用其它的构造函数，其它的构造函数必然也会有 super 语句的存在，所以在同一个构造函数里面有相同的语句，就失去了语句的意义，编译器也不会通过。
- this() 和 super() 都指的是对象，所以，均不可以在 static 环境中使用。包括：static 变量,static 方法，static 语句块。
- 从本质上讲，this 是一个指向本对象的指针, 然而 super 是一个 Java 关键字。



### static

静态变量属于整个类，和每一个具体的对象无关

静态属性、静态方法，同样可以有getter和setter，需要封装

静态成员不能访问普通成员，但是普通成员可以任意访问静态成员，因为静态成员共享，普通成员独享

构造函数也是一种静态方法，可以在其他静态方法中访问，典型应用：工厂模式，将构造函数设置为private私有

静态代码块：static{}，用于初始化静态成员，在对象初始化之前就会运行

静态导入：import static 导入静态字段

> static-静态的，可以修饰类、可以修饰属性、修饰方法
> static修饰的属性表示【类】自有的，而不是对象的，和对象无关
> static修饰的字段可以直接使用类名访问：类名.静态属性、类名.静态方法()
> static静态成员只能访问【静态成员】
> 反过来，普通成员既可以访问【普通成员】，也可以访问【静态成员】
> 构造方法相当于特殊的【静态方法】：可以访问普通成员，也可以被静态成员访问

**static关键字主要有两种作用：**

- 为某特定数据类型或对象分配单一的存储空间，而与创建对象的个数无关。

- 实现某个方法或属性与类而不是对象关联在一起

具体而言，在Java语言中，static主要有4中使用情况：成员变量、成员方法、代码块和内部类

（1）static成员变量：

Java类提供了两种类型的变量：用static关键字修饰的静态变量和不用static关键字修饰的实例变量。静态变量属于类，在内存中只有一个复制，只要静态变量所在的类被加载，这个静态变量就会被分配空间，因此就可以被使用了。对静态变量的引用有两种方式，分别是“类.静态变量"和”对象.静态变量" 推荐`类.静态变量`

```java
//Teacher类
	// static：静态的，静态属性
	public static int scount = 0;

    // 静态方法：无法调用普通方法，无法使用普通字段
	// 静态方法、字段【只能使用静态成员】！
	public static void test() {
		System.out.println("=== 静态方法调用");
//		System.out.println("=== 静态方法调用名字：" + name);
//		show();
//		this.show();
	}
----------------------------------------------
//测试类
    // 静态变量和方法应该使用类名来访问，不应该使用对象
	System.out.println("=== 静态变量：" + Teacher.scount);
	// 静态方法调用
	Teacher.test();
```

实例变量属于对象，只有对象被创建后，实例变量才会被分配内存空间，才能被使用，它在内存中存在多个复制，只有用“对象.实例变量”的方式来引用。

*实例*

```java
// 教师类
// 创建的对象个数有要求：统计对象创建数量
public class Teacher {
	// 普通属性
	public String name = "未知名老师";
	public int count = 0;
	// static：静态的，静态属性
	public static int scount = 0;
	
	// 构造方法：既可以访问普通成员、也可以访问静态成员，类似【非静态】普通方法
	// 静态方法可以正常使用构造方法，说明构造方法类似【静态】方法
	// 构造方法相当于特殊的【静态方法】：可以访问普通成员
	public Teacher() {
		this.count ++;
		scount ++;
		if(Teacher.scount > 5) {
			System.out.println("~~~已经超出工位，无法满足需求！");
		}
	}
	
	// 静态方法：可以调用构造函数
	public static void makeTeacher() {
		Teacher t = new Teacher();
		t.show();
	}
	
	// 静态方法：无法调用普通方法，无法使用普通字段
	// 静态方法、字段【只能使用静态成员】！
	public static void test() {
		System.out.println("=== 静态方法调用");
//		System.out.println("=== 静态方法调用名字：" + name);
//		show();
//		this.show();
	}
	
	// 普通方法：可以无阻碍的使用静态成员、普通成员
	public void show() {
		System.out.println("--- 普通方法调用名字：" + name);
		// 可以正常访问
		test();
		Teacher.test();
		System.out.println("=== 普通方法调用静态成员：" + scount);
		System.out.println("=== 普通方法调用静态成员：" + Teacher.scount);
	}
}

//测试类

public class Test {

	public static void main(String[] args) {
		// 统计对象数量
		int count = 0;
		Teacher t1 = new Teacher();
		t1.name = "王老五";
		count ++;
		Teacher t2 = new Teacher();
		t2.name = "张三";
		count ++;
		Teacher t3 = new Teacher();
		count ++;
		
		A a = new A();
		a.test();
		
		/*
		 * static-静态的，可以修饰类、可以修饰属性、修饰方法
		 * 1. static修饰的属性表示【类】自有的，而不是对象的，和对象无关
		 * 2. static修饰的字段可以直接使用类名访问：类名.静态属性、类名.静态方法()
		 * 3. static静态成员只能访问【静态成员】
		 * 4. 反过来，普通成员既可以访问【普通成员】，也可以访问【静态成员】
		 * 5. 构造方法相当于特殊的【静态方法】：可以访问普通成员，也可以被静态成员访问
		 */
		
		System.out.println("教师对象个数（局部变量）：" + count);
		System.out.println("--- 教师对象个数（普通变量）：" + t3.count);
		// 可以使用对象来访问静态字段，但是不推荐！
		System.out.println("=== 教师对象个数（静态变量）：" + t3.scount);
		// 静态变量和方法应该使用类名来访问，不应该使用对象
		System.out.println("=== 静态变量：" + Teacher.scount);
		
		// 静态方法调用
		Teacher.test();
		// 不能使用类名去调用普通方法，必须使用对象实例
		// Teacher.show();
		t1.show();
		t2.show();
		
		System.out.println("=-----------");
		Teacher.makeTeacher();

		System.out.println("=-----------");
		// 运行另一个类的入口类（不运行没有作用！）
		Main.main(null);
		new Main().test();
	}

}
```


（2）static成员方法：

Java中提供了static方法和非static方法。static方法是类的方法，不需要创建对象就可以被调用，而非static方法是对象的方法，只有对象被创建出来后才可以被使用

static方法中不能使用this和super关键字，不能调用非static方法，只能访问所属类的静态成员变量和成员方法，因为当static方法被调用时，这个类的对象可能还没被创建，即使已经被创建了，也无法确定调用哪个对象的方法。同理，static方法也不能访问非static类型的变量。

单例设计模式：

static一个很重要的用途就是实现单例设计模式。单利模式的特点是该类只能有一个实例，为了实现这一功能，必须隐藏类的构造函数，即把构造函数声明为private，并提供一个创建对象的方法，由于构造对象被声明private，外界无法直接创建这个类型的对象，只能通过该类提供的方法来获取类的对象，要达到这样的目的只能把创建对象的方法声明为static，程序实例如下：

```java
//Student类 要求只能创建三个对象，之后的对象都为null
public class Student {
	
	public static int count = 0;
	
	// 从根源上解决对象创建限制：使用private私有构造方法
	private Student() {
		System.out.println("--- 创建了一个对象");
		count ++;
	}
	// 中间人：解决创建对象和对象数量限制问题
	// 使用static方法，外部可以直接通过类名访问
	// 静态方法内部：可以访问构造方法！
	public static Student makeInstance() {
		// 已经创建了3个
		if(Student.count >= 3) {
			System.out.println("创建失败，返回一个null对象！");
			return null;
		}
		// 调用构造方法
		return new Student();
	}
}

//测试类
public class Test {

	public static void main(String[] args) {	
		// 通过静态方法构造对象
		Student s1 = Student.makeInstance();
		Student s2 = Student.makeInstance();
		Student s3 = Student.makeInstance();
		System.out.println(s3);
		// Student.count --;
		Student s4 = Student.makeInstance();
		System.out.println(s4);
		
		System.out.println("总数：" + Student.count);
	}

}
```

*结果*

```java
--- 创建了一个对象
--- 创建了一个对象
--- 创建了一个对象
test.zjj1217.Student@15db9742
创建失败，返回一个null对象！
null
总数：3
```



(3)static代码块
static代码块在类中是独立于成员变量和成员函数的代码块的。注意： 这些static代码块只会被执行一次

(4)static与final结合使用表示的意思：
对于变量，若使用static  final修饰，表示一旦赋值不能修改，并且通过类名可以访问。
对于方法，若使用static final修饰，表示该方法不可被覆盖，并且可以通过类名直接访问。

public class Test{
	public static int testStatic(){
		static final int i=0;
		System.out.println(i++);
		
	}
	public static void main(String[] args){
		Test test=new Test();
		test.testStatic();
	}

**静态⽅法和实例⽅法有何不同 **

- 在外部调⽤静态⽅法时，可以使⽤"类名.⽅法名"的⽅式，也可以使⽤"对象名.⽅法名"的⽅ 式。⽽实例⽅法只有后⾯这种⽅式。也就是说，调⽤静态⽅法可以⽆需创建对象。 
- 静态⽅法在访问本类的成员时，只允许访问静态成员（即静态成员变量和静态⽅法），⽽不 允许访问实例成员变量和实例⽅法；实例⽅法则⽆此限制。

### final

表示最终的：也就是不能改变

可以修饰类（不能继承），修饰方法（不能被重写），final修饰变量（不能再次赋值）

final可以修饰成员属性，类成员：【没有默认值】，必须要赋值，如果不赋值那么必须在构造函数里初始化！

良好规范：属性都要使用private；能用final一定用final；普通属性、能读、但是不能赋值，比如数组.length

设计一个属性，只能访问不能更改：
public final int a; // final变量，但是不赋初始值
public A(int a) {
	this.a = a; // 通过构造函数的参数赋值！
}



关于 final 关键字的⼀些总结 final 关键字主要⽤在三个地⽅：变量、⽅法、类。

- 对于⼀个 final 变量，如果是基本数据类型的变量，则其数值⼀旦在初始化之后便不能更 改；如果是引⽤类型的变量，则在对其初始化之后便不能再让其指向另⼀个对象。
- 当⽤ final 修饰⼀个类时，表明这个类不能被继承。final 类中的所有成员⽅法都会被隐式地 指定为 final ⽅法。
- 使⽤ final ⽅法的原因有两个。第⼀个原因是把⽅法锁定，以防任何继承类修改它的含义； 第⼆个原因是效率。在早期的 Java 实现版本中，会将 final ⽅法转为内嵌调⽤。但是如果⽅ 法过于庞⼤，可能看不到内嵌调⽤带来的任何性能提升（现在的 Java 版本已经不需要使⽤ final ⽅法进⾏这些优化了）。类中所有的 private ⽅法都隐式地指定为 final。



### 父类、子类、静态属性的运行顺序

<font color=red>初始化属性（和初始化块同级别） -> 构造函数 -> 子类同样的顺序</font>

```java
//父类
public class SA {
	
	// 7
	public static int sa = stest();
	
	// 1
	public int a = test();
	
	// 2
	public SA() {
		System.out.println("=== 构造函数：调用A的构造函数a=" + a + ",sa=" + sa);
	}
	
	private int test() {
		System.out.println("=== 属性初始化：赋值给a变量");
		return 1;
	}
	private static int stest() {
		System.out.println("=== 静态属性初始化：赋值给sa变量");
		return 123;
	}
}

//子类
public class SB extends SA{
	
	// 8
	public static int sb = stest();
	
	// 3
	public int b = test(); 
	
	// 4
	public SB() {
		System.out.println("~~~ 【子类】构造函数：调用B的构造函数");
	}
	
	private int test() {
		System.out.println("~~~ 【子类】属性初始化：赋值给b变量");
		return 2;
	}
	private static int stest() {
		System.out.println("~~~ 【子类】静态属性初始化：赋值给sb变量");
		return 222;
	}
}
//测试类
		// 运行顺序：1->[5]->2->3->[6]->4（初始化块和属性同优先级）
		// 初始化属性（和初始化块同级别） -> 构造函数 -> 子类同样的顺序
		// B obj = new B();
		
		// 运行顺序：【7->8】 ->1->2-> ->3->4
		// 初始化顺序：父类静态成员 -> 子类静态成员 -> 父类属性 -> 父类构造 -> 子类属性 -> 子类构造
//		SB obj = new SB();
		SB.sb = 1;
		SB.sb = 1;
		SB.sb = 1;
		new SB();
		new SB();
		new SB();
```



### 在⼀个静态⽅法内调⽤⼀个⾮静态成员为什么是⾮法的? 

由于静态⽅法可以不通过对象进⾏调⽤，因此在静态⽅法⾥，不能调⽤其他⾮静态变量，也不可 以访问⾮静态变量成员。

### 多态

所谓多态就是指程序中定义的引⽤变量所指向的具体类型和通过该引⽤变量发出的⽅法调⽤在编 程时并不确定，⽽是在程序运⾏期间才确定，即⼀个引⽤变量到底会指向哪个类的实例对象，该 引⽤变量发出的⽅法调⽤到底是哪个类中实现的⽅法，必须在由程序运⾏期间才能决定。 

在 Java 中有两种形式可以实现多态：继承（多个⼦类对同⼀⽅法的重写）和接⼝（实现接⼝并 覆盖接⼝中同⼀⽅法）。

**继承的多态**

父类和子类
引用类型、对象类型
		Animal   a   =  new Cat()
		  |      |          |
	   引用类型  引用     具体对象
父类更加抽象，子类更加具体；所以：父类范围 > 子类范围

- 父类类型 引用变量 = 子类对象； Animal a = new Cat();

- 子类类型 引用变量 != 父类对象；不允许！Cat a = new Animal();

- 父类类型引用子类对象时，子类的方法怎么处理？Animal a = new Cat(); a.抓老鼠？

- 父类应用子类对象后，这个引用丧失了子类的特性！比如 a.catchMouse() 不允许，原因是编译不通过

- 编译的时候 Animal a = new Cat() 这里编译器只知道 a 是一个动物，而不能推测一定是猫

- 假设可以推测 a 动物就是一只猫，但是 a = new Dog() ，这时候产生异常，实际对象并不具有抓老师方法

-  父类引用的具体类型可以强制转化为具体的子类类型：Animal a = new Cat(); ((Cat)a).catchMouse() 强制转换可行

- 不能随意强制转换：(Dog)a 类型错误导致转换异常，可以使用 instanceof 对类型进行判断后再安全转换！
  多态就是应用父类引用指向不同的子类

  Animal a = new Cat(); a = new Dog(); a = new Pig();

  Cat a = new Cat(); a != new Dog(); 报错！
  如果强转类型不对会抛出异常：((Dog)a).watchDoor();

**instanceof**

- 父类引用可以引用子类对象、引用，比如 Animal a = new Cat(); 反过来不行！Cat c=new Animal();

- 强制转换：Animal a=new Cat(); Cat c=(Cat)a;

- instanceof 判断引用的类型：if(a instanceof Cat){b = (Cat)a;} 先判断类型是否符合，再安全进行强制转换

- 注意：子类既是子类型、也是父类型，a = new Cat(), a instanceof Cat == true; a instanceof Animal == true;

*用例*

```java
//父类
public class Animal {
	private String name;
	
	public void run() {
		System.out.println(name + "动物在跑！");
	}
	
	public void howl() {
		System.out.println(name + "动物在嚎叫！");
	}
}

//子类
public class Cat extends Animal {
	
	@Override
	public void howl() {
		System.out.println("喵星人在喵喵喵……");
	}
	
	// 子类特有的方法
	public void catchMouse() {
		System.out.println("~~~ 猫抓老鼠！");
	}
}

//子类
public class Dog extends Animal {
	
	// 重写方法快捷键：Ctrl+O
	@Override
	public void howl() {
		System.out.println("旺财在汪汪汪……");
	}

	// 子类特有的方法
	public void watchDoor() {
		System.out.println("~~~ 旺财看门狗！");
	}
}

```

*测试用例*

多态：使用父类引用子类对象，子类暂时失去特有的方法

```java
		// 多态：使用父类引用子类对象，子类暂时失去特有的方法
		System.out.println("-------多态1--------");
		Animal a1 = new Cat();
		a1.run();  // 没有重写：父类方法
		a1.howl(); // 重写：子类方法
		
		a1 = new Dog();
		a1.run();
		a1.howl();
```

*测试用例*

可以强制转换：安全
使用instanceof关键字进行类型的判断：

```java
         /*
		 * 使用instanceof关键字进行类型的判断：
		 * 1. A instanceof B 用来判断A对象是否是B类型，返回结果为boolean
		 * 2. 比如：obj instanceof Dog 判断obj对象是否是Dog类型，如果返回true，那么可以安全的向下转型
		 */
		Animal a1 = new Cat();
		if(a1 instanceof Dog) {
			System.out.println("~这个对象却是是一个Dog类型：");
			((Dog)a1).watchDoor();
		}
		// a1 instanceof Cat 返回是true，说明a1是Cat类型
		if(a1 instanceof Cat) {
			System.out.println("~这个对象却是是一个Cat类型：");
			((Cat)a1).catchMouse();
		} else {
			System.out.println("~这个对象不是Cat类型！！！");
		}
		System.out.println("a1 instanceof Animal = " + (a1 instanceof Animal));
		System.out.println("a1 instanceof Object = " + (a1 instanceof Object));
	}

}
```







