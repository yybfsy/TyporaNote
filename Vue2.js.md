Vue2.js



## 第一章 Vuejs 概述



### 1.1 什么是 Vuejs

Vuejs 是一套构建用户界面的框架，它只关注视图层的内容，它是前端的主流框架之一。

前端 3 大主流框架：
Angular.js
React.js
Vue.js
前端框架主要负责的是 MVC 中的 V 的这一层，主要的工作就是和界面打交道，主要是用来对页面中的数据进行处理，以及制作前端页面相关的特效及动画。



### 1.2 为什么要学习 Vuejs

在实际项目开发中，不论是做前端开发还是后端开发，使用框架技术是最佳的提高效率的方式。
另外使用 Vuejs 来做前端框架，对于处理数据的方面可以完全的替换掉原有的 dom 操作的理念（之前我们常用的原生 js 以及 jquery类库），通过 Vuejs 框架提供的指令，前端开发人员不再关心 dom 是如何渲染的，可以有更多的时间去关注业务逻辑本身。
Vuejs 作为现今最火爆的前端开发框架，学习后可以有效的提高就业的价值。



### 1.3 MVC 和 MVVM 的区别

![](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs001.png)



### 1.4 Vue.js 版本 1 和 2 的区别

Vuejs 当今应用最普遍的有两个版本，分别是 Vue1.js 以及 Vue2.js。值得说明的是版本 2 在版本 1 的基础上进行了大量的改动，所以二者从概念到语法上有着很大的区别，随着版本 2 的成熟以及市场的认可，当前市场中对于新项目的开发已经完全偏向于使用版本 2.
教程：版本 2 Vue2.js

vue2版本浏览器开发插件（火狐）

https://addons.mozilla.org/zh-CN/firefox/addon/vue-js-devtools/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search



## 第二章 Vuejs 基础语法



### 2.1 第一个 Vuejs 案例_HelloWorld

［］表示数组。 ｛｝表示对象，或者用在函数体、程序段等地方，例如，if、else、for、while程序段 ｛｛｝｝是嵌套的对象或程序段

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
    </head>
    <body>
        <!-- 在外层标签div引入 id属性值 将来vuejs会通过该id，找到操作的元素 -->
        <!-- 以下Vue实例vm所控制的这个元素区div，就是我们的V -->
        <div id="app">
            <!-- 在前端页面元素的部分，其中的内容我们暂时以插值表达式的形式来呈现 -->
            <!-- 在两对p标签中分别引入了插值表达式，相当于将p标签对中的内容写活了，内容以变量的形式存在 -->
            <p>{{str1}}</p>
            <P>{{str2}}</P>
        </div>
        <script>
            Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
            //当Vuejs框架包导入进来之后，在浏览器缓存中，就已经存在了一个Vue框架的构造函数
            //我们new出来的这个vm对象，就是页面中对于模型和视图（数据和页面元素）的整体调度者
            //以下创建出来的vm对象，就是我们MVVM中的VM调度者
            var vm = new Vue({
                el : "#app",       //el元素表现的是要指定哪个标签进行相应的vuejs的操作
                data : {           //data是vuejs中对于数据的表达，数据约定俗成的都是以json的形式来呈现的
                     "str1" : "helloworld1",
                     "str2" : "helloworld2"
                     //data属性中，存放的是el中要使用到的数据
                     //这里的data就是MVVM中M，专门用来表现数据的组件
                }
            })
        </script>
    </body>
</html>
```



### 2.2 指令属性的基本使用

（1）v-cloak

使用 v-cloak 主要为了解决插值表达式的闪烁问题使用插值表达式的问题：
在页面加载的过程中，在页面中的{{}}插值表达式首先会被页面认可为是 html 元素中的实在存在的内容。所以浏览器会首先将{{}}展现在页面上，页面加载完毕后，插值表达式{{}}才会真正的转变为动态赋予的值。这就会造成一种现象，如果将来终端在访问服务器的过程中，网速较慢（网络比较卡），那么我们的{{}}会首先展现出来，{{}}展现出来之后，会一闪而过，最终显示的是最终被赋予的值。这就是前端开发中所谓的，插值表达式的闪烁问题。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
        <style>
            [v-cloak]{
                /* 把元素隐藏起来 */
                display: none;
            }
        </style>
    </head>
    <body>

        <div id="app">
            <p v-cloak>{{str1}}</p>
            <p v-cloak>{{str2}}</p>
        </div>
        <script>
            var vm = new Vue({
                el : "#app",
                data : {
                    "str1" : "helloworld",
                    "str2" : "worldhello"
                }
            })
        </script>
    </body>
</html>
```

（2）	v-text

（3）	v-html

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
    </head>
    <body>

        <div id="app">
         <!-- 
            
            在vuejs中，为了为页面中的元素渲染值（为前端标签对中的内容赋值） 
            可以使用3种形式：
                插值表达式{{str}}
                v-text
                v-html
        -->

        <!-- 使用插值表达式为标签对中的内容赋值 -->
        <p>==============={{str1}}===============</p>
        <p v-text="str2">=====================</p>
        <p v-html="str3">=====================</p>
        </div>
        <script>
            var vm = new Vue({
                el : "#app",
                data : {
                    "str1" : "aaa",
                    "str2" : "bbb",
                    "str3" : "ccc"
                }
            })
        </script>
    </body>
</html>
```

```
效果
===============aaa===============
bbb
ccc
```



（4）	插值表达式与 v-text/v-html 的区别
a.	对于元素中已经存在的值，只有插值表达式能够将原有的值保留，在原有的已经存在的值的基础上添加动态数据。
使用 v-text 和 v-html 之所以不能够保留元素标签对中原有的内容，是因为在使用以上两个指定属性之前，会提前将标签对中的内容先清空掉，在赋予动态的值。如果未来的实际项目开发，需求为在原有的内容的基础上，追加动态的值，我们要选择使用插值表达式。
从另一个方面来看，插值表达式虽然会出现{{}}页面闪烁的现象（v-text 和 v-html 不会出现页面闪烁的情况），但是对于原有内容的保留，只有插值表达式能够完成，所以插值表达式具有不可替代的优势。

对比 v-text 和 v-html
v-text:<font color=red>主要是用来赋予纯内容的，如果赋予到元素中的内容本身包是得不到浏览器的解析的。</font>
v-html<font color=red>:除了能够为前端元素赋予内容之外，更重要的是，如果内容本身含有 html 代码，那么赋值后最终展现出来的结果，html 元素会得到浏览器的解析的。</font>
从以上结果判断，v-html 的功能要更加强大，对于前端页面的展现，不可能让使用该系统的用户看到任何 html 代码，而是应该让用户看到解析后的 html 效果。所以在实际项目开发中，使用 v-html 的概率要高于 v-text。
另外使用插值表达式的效果，与 v-text 是一样的，内容中的 html代码时得不到浏览器的解析的。

（5）v-bind

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
    </head>
    <body>

        <div id="app">
                    
        <!-- 以下input标签对value属性中的值，使用vm对象，由vm对象将data中的信息动态的赋予到该value属性值当中 -->
        <!-- 
            
            必须使用指令属性v-bind来完成 
            我们需要将v-bind:加在我们需要绑定的属性的前面
        
        -->
            <input type="text" v-bind:value="str1"/>
            <p :title="str2">content...</p>
            <input type="button" value="submit" :title="str3+'helloworld'"/>

        <script>
            var vm = new Vue({
                el : "#app",
                data : {
                    "str1" : "aaa",
                    "str2" : "bbb",
                    "str3" : "ccc"
                }
            })
        </script>
    </body>
</html>
```



![](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs002.png)

v-bind:是 Vuejs 中，提供用于绑定属性的指令
对于 v-bind 在开发中一共有如下几种使用方式

a.	直接使用指令属性 v-bind 来为元素中的属性进行绑定操作

```html
<input type="text" v-bind:value="str1"/>
```

b.	使用简化后的方式，<font color=red>将 v-bind 去除，直接使用:</font>来对元素中的额属性进行绑定。
因为在实际项目开发中，对于前端元素的绑定是我们的常规操作， v-bind 的使用复用率非常高，所以每一次都直接写 v-bind 会很麻烦，所以 vuejs 为 v-bind 指令属性提供了简写的方式，直接使用:即可。
v-bind:title --> :title
注意：这种简写形式仅仅只是针对于我们的 v-bind，以上所讲解的其他的指令是不具备简写形式的。
在实际项目开发中，我们都是使用这种简写的形式。

```html
<p :title="str2">content...</p>
```

c.在使用 v-bind 对元素中的属性进行绑定的时候，可以直接在操作值的位置进行内容的拼接。

```html
<input type="button" value="submit" :title="str3+'helloworld'"/>
```

（6）v-pre

浏览器解析引擎遇到vue的插值符号时会自动解析，当你想输出不被解析的纯文本时，可以使用v-pre指令。

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-pre指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
			v-pre指令：
					1.跳过其所在节点的编译过程。
					2.可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-pre>Vue其实很简单</h2>
			<h2 >当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
```

（7）v-once

如果显示的信息后续不需要再修改，使用v-once，这样可以提高性能。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-once指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
			v-once指令：
						1.v-once所在节点在初次动态渲染后，就视为静态内容了。
						2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-once>初始化的n值是:{{n}}</h2>
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
```



<b>自定义指令</b>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>自定义指令</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
				需求1：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
				需求2：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。
				自定义指令总结：
						一、定义语法：
									(1).局部指令：
												new Vue({															new Vue({
													directives:{指令名:配置对象}   或   		directives{指令名:回调函数}
												}) 																		})
									(2).全局指令：
													Vue.directive(指令名,配置对象) 或   Vue.directive(指令名,回调函数)

						二、配置对象中常用的3个回调：
									(1).bind：指令与元素成功绑定时调用。
									(2).inserted：指令所在元素被插入页面时调用。
									(3).update：指令所在模板结构被重新解析时调用。

						三、备注：
									1.指令定义时不加v-，但使用时要加v-；
									2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>{{name}}</h2>
			<h2>当前的n值是：<span v-text="n"></span> </h2>
			<!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
			<h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
			<button @click="n++">点我n+1</button>
			<hr/>
			<input type="text" v-fbind:value="n">
		</div>
	</body>
	
	<script type="text/javascript">
		Vue.config.productionTip = false

		//定义全局指令
		/* Vue.directive('fbind',{
			//指令与元素成功绑定时（一上来）
			bind(element,binding){
				element.value = binding.value
			},
			//指令所在元素被插入页面时
			inserted(element,binding){
				element.focus()
			},
			//指令所在的模板被重新解析时
			update(element,binding){
				element.value = binding.value
			}
		}) */

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				n:1
			},
			directives:{
				//big函数何时会被调用？1.指令与元素成功绑定时（一上来）。2.指令所在的模板被重新解析时。
				/* 'big-number'(element,binding){
					// console.log('big')
					element.innerText = binding.value * 10
				}, */
				big(element,binding){
					console.log('big',this) //注意此处的this是window
					// console.log('big')
					element.innerText = binding.value * 10
				},
				fbind:{
					//指令与元素成功绑定时（一上来）
					bind(element,binding){
						element.value = binding.value
					},
					//指令所在元素被插入页面时
					inserted(element,binding){
                        //用于为元素提供焦点（如果可以聚焦）。
						element.focus()
					},
					//指令所在的模板被重新解析时
					update(element,binding){
						element.value = binding.value
					}
				}
			}
		})
		
	</script>
</html>
```





### 2.3 使用 v-on 指令触发事件

（1）	v-on 的基本使用
              v-	on:click="fun1"的形式来绑定事件

​              相当于原生 js 中的 onclick

​              v-bind-->:
​              <font color=red>v-on-->@</font>

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
    </head>
    <body>

        <div id="app">
                    
            <input type="text" /><br>
            <input type="button" value="a" onclick="fun1()"/>
            <input type="button" value="b" v-on:click="fun2"/>
            <input type="button" value="c" @click="fun3"/>

        </div>
            

        <script>
            //使用原生js的点击事件
            function fun1(){
                alert("aaa");
            }
            //vue
            var vm = new Vue({
                el : "#app",
                data : {
                },
                //methods:表示vuejs中对于绑定事件函数的定义，可以同时定义多个函数，多个函数之间使用逗号来进行分隔
                methods : {
                    fun2(){
                        alert("bbb");
                    },
                    fun3(){
                        alert("ccc");
                    }
                }

            })
        </script>
    </body>
</html>
```

（2）	事件修饰符的使用
              a.	stop

​              使用.stop 来对事件的冒泡机制进行阻止

​              js 中的事件的冒泡指的是，在触发了内层元素的同时，也会随之继续触发外层元素（外层元素包裹了内层元素），在做点击的过程中，点击了内层元素，也可以认为是同时点击了外层元素。所以两个事件都会触发。
​              在实际项目开发中，几乎没有太多需求会使用到这种事件冒泡的机制，所以我们需要阻止事件的冒泡。阻止事件冒泡之后的效果是，在我们点击了内层元素之后，内层元素绑定的事件触发，触发完毕后，由于事件冒泡被阻止，就不会继续触发外层元素的事件了。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
    </head>
    <body>

        <div id="app">
            <div style="width: 200px;height: 200px;background-color: red;" @click="fun1">
                <div style="width: 100px;height: 100px;background-color: pink;" @click.stop="fun2">
                
                </div>
            </div>      
        </div>
            
        <script>
            
            var vm = new Vue({
                el : "#app",
                data : {
                },
                //methods:表示vuejs中对于绑定事件函数的定义，可以同时定义多个函数，多个函数之间使用逗号来进行分隔
                methods : {
                    fun1(){
                        alert("触发了外层div");
                    },
                    fun2(){
                        alert("触发了内层div");
                    }
                }

            })
        </script>
    </body>
</html>
```

​              b.prevent
​              使用.prevent 来阻止超链接默认的行为
​              所谓默认的行为指的是超链接中的 href 属性链接
​              在实际项目开发中，不仅仅只是按钮需要我们绑定事件来控制行为，超链接的使用我们也是要遵循这种自己绑定事件触发行为的方式。所以在 a 标签中的 href 链接往往要被我们以特殊的方式处理掉。

               ```html
                   <body>
               
                       <div id="app">
                           <a href="http://www.baidu.com"  @click="fun1">点击1</a>  
                           <a href="http://www.baidu.com"  @click.prevent="fun1">点击2</a>  
                       </div>
                           
                       <script>
                           
                           var vm = new Vue({
                               el : "#app",
                               data : {
                               },
                               //methods:表示vuejs中对于绑定事件函数的定义，可以同时定义多个函数，多个函数之间使用逗号来进行分隔
                               methods : {
                                   fun1(){
                                       alert("触发了外层div");
                                   }
                               }
                           })
                       </script>
                   </body>
               ```



​              c.capture
​              使用.capture 实现捕获触发事件的机制使用的是外层 div 套用内存 div 的例子（其中内层 div 没有选择阻止冒泡），在此基础之上，点击内层的 div，先触发内层 div 的事件，再触发外层 div 的事件。
​              加入了.capture 修饰符之后，先触发的是外层的 div 事件，后触发的是内层 div 事件。被.capture 修改之后，事件优先触发。

```html
    <body>

        <div id="app">
            <div style="width: 200px;height: 200px;background-color: red;" @click.capture="fun1">
                <div style="width: 100px;height: 100px;background-color: pink;" @click="fun2">
                
                </div>
            </div>      
        </div>
            
        <script>
            
            var vm = new Vue({
                el : "#app",
                data : {
                },
                //methods:表示vuejs中对于绑定事件函数的定义，可以同时定义多个函数，多个函数之间使用逗号来进行分隔
                methods : {
                    fun1(){
                        alert("触发了外层div");
                    },
                    fun2(){
                        alert("触发了内层div");
                    }
                }

            })
        </script>
    </body>
```



​              d.self
​              self 实现阻止事件冒泡行为的机制（之前我们讲过了一个.stop）使用.self 实现的是阻止自身冒泡的行为（它不会真正的阻止冒泡）案例：外层 div，内层 div，在内层 div 中加入了 button
​              测试 1：在内层 div 加入.stop 修改符
​              观察实验结果，点击最内层的按钮，触发按钮事件，触发了内层的 div，外层 div 没有触发，也就是说，使用.stop 修改符，不会阻止掉自身事件的触发，在自身事件触发完毕之后，阻止事件继续向外扩散。

​              测试：在内层 div 加入.self 修改符
​              观察实验结果，点击按钮，触发按钮事件，没有触发内层 div 事件，跨过了内层 div 事件的触发后，继续触发了外层 div 的事件。
​              表示使用.self 只是将当前元素（测试中的内层 div）的冒泡行为阻止掉了，但是不会影响冒泡行为继续向外扩散（测试中的外层 div 继续触发了）

```html
    <body>

        <div id="app">
            <div style="width: 200px;height: 200px;background-color: red;" @click="fun1">
                <div style="width: 100px;height: 100px;background-color: pink;" @click.self="fun2">
                    <input type="button" value="按钮" @click="fun3"/>
                
                </div>
            </div>      
        </div>
            
        <script>
            
            var vm = new Vue({
                el : "#app",
                data : {
                },
                //methods:表示vuejs中对于绑定事件函数的定义，可以同时定义多个函数，多个函数之间使用逗号来进行分隔
                methods : {
                    fun1(){
                        alert("触发了外层div");
                    },
                    fun2(){
                        alert("触发了内层div");
                    },
                    fun3(){
                        alert("点击了按钮");
                    }
                }

            })
        </script>
    </body>
```



​              e.once
​              使用.once 修饰符，只触发一次事件处理函数 .once 需要结合.prevent 来使用
​              在我们使用事件修饰符的时候，有可能会存在这样的需求，需要同时为@click 事件使用多个修饰符。例如我们现在就需要同时使用.once 和.prevent 修饰符。在使用的时候，通过绑定事件的@click连续的绑定修饰符就可以了。
​              语法： @click.prevent.once

​              测试：通过超链接的触发来观察
​              在只使用@click 的时候（没有做任何修饰符的修饰），点击超链接，先触发@click，后触发 href 链接。
​              当为@click 添加上@click.prevent.once 之后，点击超链接。
​              第一次点击：只触发了@click 的事件，href 链接没有触发
​              第二次点击（已经点击过一次之后再次点击）：没有触发@click，只触发了 href。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
    </head>
    <body>

        <div id="app">
            <a href="http://www.baidu.com"  @click="fun1">点击1</a>  
            <a href="http://www.baidu.com"  @click.prevent.once="fun1">点击2</a>  
        </div>
            
        <script>
            
            var vm = new Vue({
                el : "#app",
                data : {
                },
                //methods:表示vuejs中对于绑定事件函数的定义，可以同时定义多个函数，多个函数之间使用逗号来进行分隔
                methods : {
                    fun1(){
                        alert("触发了外层div");
                    }
                }
            })
        </script>
    </body>
</html>
```



### 2.4 使用 v-model 指令实现双向数据绑定

v-bind
单向数据绑定

![](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs003.png)

我们可以对 v-bind 的绑定数据的形式得出一个结论，v-bind 只能实现数据的单向绑定，从模型（M）绑定到视图（V），使用 VM 将数据去渲染视图，但是我们无法通过该形式实现数据的双向绑定。

双向数据绑定

![](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs004.png)

在实际项目开发中，不仅仅只是将模型准确的渲染到视图中，视图中的数据的变化，更需要模型去进行有效的记录。所以我们需要使用双向数据绑定的机制。
（1）v-model 的基本使用
          使用 v-model 可以对数据进行双向的绑定操作。
          值得注意的是，由于记载页面元素值的需求都是发生在表单元素中，所以 v-model 只能运用在表单元素中。

​          form

​          **<input>**系列 type:text,hidden,checkbox,radio....

​          **<select>**

​          **<textarea>**

​          ...

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
    </head>
    <body>

        <div id="app">
            <h3>{{str1}}</h3>
            <input type="text" v-model:value="str1"/>   
        </div>
            
        <script>
            
            var vm = new Vue({
                el : "#app",
                data : {
                    "str1" : "aaa"
                }
            });
        </script>
    </body>
</html>
```

（2）使用 v-model 实现简单的计算器功能

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title></title>
        <!-- 引入Vue.js框架 -->
        <script src="lib/vue-2.4.0.js"></script>
    </head>
    <body>

        <div id="app">
            
            <!-- 双向绑定num1 -->
            <input type="text" v-model:value="num1"/> 
            <!-- 双向绑定运算符号 -->
            <select v-model="csgin" >
                <option value="+">+</option>
                <option value="-">-</option>
                <option value="*">*</option>
                <option value="/">/</option>
            </select>  
            <input type="text" v-model:value="num2"/> 
            <!-- 点击事件 -->
            <input type="button" value="=" @click="count" />
            <input type="text" v-model:value="result"/> 

        </div>
            
        <script>
            
            var vm = new Vue({
                el : "#app",
                data : {
                    "num1" : 0,
                    "num2" : 0,
                    "csgin" : "+",
                    "result" : 0
                },
                methods : {
                    count(){
                        if(this.csgin == "+"){
                            //直接取得的数值暂时是不能够直接计算的，默认的情况会按照字符串拼接的形式来触发+符号
                            //默认拼接字符串： 1+1=11
                            //在做数学计算之前，需要将数值格式化，才能够计算，使用parseInt方法做数值格式化的操作
                            this.result = parseInt(this.num1) + parseInt(this.num2);
                        }else if(this.csgin == "-"){
                            this.result = parseInt(this.num1) - parseInt(this.num2);
                        }else if(this.csgin == "*"){
                            this.result = parseInt(this.num1) * parseInt(this.num2);
                        }else if(this.csgin == "/"){
                            this.result = parseInt(this.num1) / parseInt(this.num2);
                        }
                }
            }
            });
        </script>
    </body>
</html>
```



### 2.5 使用 class 样式
使用 vuejs 控制样式，会使样式变化的操作更加的灵活
（1）class 样式的使用
案例 1：传递一个 class 样式的数组，通过 v-bind 做样式的绑定
该形式与之前的形式没有太大的区别
:class="[样式 1,样式 2]"
案例 2：通过三目（元）运算符操作以上数组
boolean?true 执行 :false 执行(如果为真则执行右边的内容如果为假执行左边的内容)
案例 3：使用对象（json） 来表达以上三目（元）运算符的操作
{样式:flag}
案例 4：以对象引用样式
:class={}

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    
    <style>
        .style1{
            color:red;
        }
        .style2{
            background-color: aqua;
        }
        .style3{

            font-style: italic;
        }
        .style4{

            font-size: 30px;
        }
    </style>

</head>
<body>
    
    <div id="app">
        <!-- 原生方式 -->
        <span class="style1 style2 style3 style4">Hello Style</span><br>
        <!-- 通过 v-bind 做样式的绑定 -->
        <span :class="['style1','style2','style3','style4']">Hello Style</span><br>
        <!-- 使用三元运算进行判断是否使style4生效 -->
        <span :class="['style1','style2','style3',flag?'style4':'']">Hello Style</span><br>
        <!-- 使用对象（json） 来表达以上三目（元）运算符的操作 -->
        <span :class="['style1','style2','style3',{'style4': flag}]">Hello Style</span><br>
        <!-- 以对象引用样式 -->
        <span :class="{style1:true,style2:true,style3:true,style4:flag}">Hello Style</span>
        

    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                flag : false
            },
            //methods:表示vuejs中对于绑定事件函数的定义，可以同时定义多个函数，多个函数之间使用逗号来进行分隔
            methods:{
            }

        });

    </script>

</body>
</html>
```

案例 5：通过以直接模型 M 的形式做样式渲染
注意：这样使用必须直接将具体的 boolean 值结果（true/false）赋值，不能以 this.模型的形式来做引用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    
    <style>
        .style1{
            color:red;
        }
        .style2{
            background-color: aqua;
        }
        .style3{

            font-style: italic;
        }
        .style4{

            font-size: 30px;
        }
    </style>

</head>
<body>
    
    <div id="app">
       
        <span :class="mystyle">Hello Style</span>
        
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                //这样使用必须直接将具体的 boolean 值结果（true/false）赋值，不能以 this.模型的形式来做引用
                mystyle : {style1:true,style2:true,style3:true,style4:false}
            },
            methods:{
            }

        });

    </script>

</body>
</html>
```



（2）style 样式补充
在实际项目开发中，对于 style 样式的使用，没有 class 使用的广泛，通常 style 属性仅仅只是对个别指定元素的样式进行的进一步补充使用。
案例 1：引用样式对象
:style="引用样式对象"
注意：在写 color 这样的样式属性的时候，由于仅仅只是一个单词，所以不需要加引号，开发中的大多数的样式都是包含横杠（-）的，例如：font-style，background-color 等等，在使用这样带有-的演示属性的时候，必须套用在引号中。
'font-style'
'background-color'
color
案例 2：引用样式对象数组
:style="[样式对象引用 1,样式对象引用 2]"

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
</head>
<body>
    
    <div id="app">
       
        <span :style="mystyle">Hello Style</span><br>
        <span :style="[mystyle,mystyle2]">Hello Style</span>
        
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                //引用样式对象
                mystyle : {color : 'red','font-size' : '30px'},
                mystyle2 : {'font-style' : 'italic','background-color' : 'aqua'}

            },
            methods:{
            }

        });

    </script>

</body>
</html>
```



### 2.5 v-for 指令和 v-if 指令的应用
（1）v-for 指令的基本使用
案例 1：遍历字符串数组
案例 2：遍历对象数组
案例 3：遍历对象的属性和属性值
案例 4：遍历整型数字

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
</head>
<body>
    
    <div id="app">
       
        <!-- 使用插值表达式 引用数组 通过下标展现所需元素 -->
        <!-- <p>{{citylist[0]}}</p>
        <p>{{citylist[1]}}</p>
        <p>{{citylist[2]}}</p>
        <p>{{citylist[3]}}</p> -->
        <!-- 
            使用v-for指令遍历字符串数组 
            语法 ： 元素 in 数组
        -->
        <!-- 
            <p v-for="city in citylist">
                {{city}}
            </p>
         -->
        <!-- <p v-for="(city,i) in citylist">
            {{i}}==={{city}}
        </p> -->
        <!-- 每一次遍历出来的，代表一个城市信息对象 -->
        <p v-for="city in clist">
            {{city.id}}----{{city.name}}
        </p>
        <!--
            遍历对象的属性和属性值：
            必须以取出键值对的形式来遍历
            (value值(属性值),key键(属性名)) in 对象
            (value值(属性值),key键(属性名),i下标) in 对象
        -->
        <p v-for=" (value,key) in city1 ">
            {{key}}---{{value}}
        </p>

        
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                citylist : ["北京","上海","长沙","深圳"],
                clist : [
                    {id:"A001",name:"北京"},
                    {id:"A002",name:"上海"},
                    {id:"A003",name:"长沙"},
                    {id:"A004",name:"深圳"},
                ],
                city1 : {id:"A001",name:"北京"}

            },
            methods:{
            }

        });

    </script>

</body>
</html>
```



（2）v-for 指令使用注意事项

- **V-for循环遍历数组时推荐使用of**，语法格式为`(item，index)`
  - item:迭代时不同的数组元素的值
  - index:当前元素的索引
- **V-for循环遍历对象时推荐使用in**，语法格式为`(item,name,index)`
  - item:迭代时对象的键名键值
  - name:迭代时对象的键名
  - index:当前元素的索引
- 在遍历对象时，会按 `Object.keys()` 的结果遍历，但是**不能**保证它的结果在不同的 JavaScript 引擎下都一致。
- v-for也可以在实现了[可迭代协议](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols#可迭代协议)的值上使用，包括**原生的Map和Set**。

对于 key 属性的使用案例
key 属性的作用：
在实际项目开发中，使用 v-for 仅仅只是将元素遍历出来，并展现在页面中。如果在将来的其他需求中，使用到指定的遍历出来的某个元素，那么视图并没有为我们提供一个有效的辨识指定元素的方式。
所以在遍历元素的过程中，需要为每一条遍历出来的元素做一个有效的标识，这个标识就是该元素在页面中的唯一标识，在将来使用到该元素的时候，页面可以通过该标识认准该元素。在 v-for 的使用过程中，添加 key 属性及属性值就是做这个标识的最好的手段。
所以我们需要养成一个在遍历元素的过程中，为 key 属性赋值的好习惯。
对于 key 属性的应用，值得注意的是：

- key 属性值必须是一个数值或者字符串，对象不能当做属性值。否则系统会提出警告，将来不能有效的应用。

- key 属性的应用，必须要搭配绑定 v-bind 指令，在使用的时候必须是以该形式":key"来使用，否则系统不会生效。

- 对 key 属性所赋的值，必须是记录的唯一标识，我们通常使用的是记录的 id。

  ```html
          <!-- 每一次遍历出来的元素，代表一个城市信息对象 key可以作为数据库中的唯一表示-->
          <p v-for="(city,i) in cityList" :key="city.id">
  
              <!-- 对象以  .属性名 的形式来取得属性值 -->
              {{i}}------------------{{city.id}}-----------{{city.name}}
  
          </p>
  ```



（3）v-if 指令和 v-show 指令的使用和区别
案例 1：v-if 的使用
案例 2：v-show 的使用

```html
    <div id="app">
        <!--
        v-if:boolean true/flase
        当值为true：则展现标签对中的信息
        当值为false：则不展现标签对中的信息
        -->
        <p v-if = true>
            显示该文本！v-if方法1
        </p>  
        <p v-if = flag>
            显示该文本！v-if方法2
        </p> 
        <p v-show = true>
            显示该文本！v-show方法1
        </p>
        <p v-show = flag>
            显示该文本！v-show方法2
        </p>
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                flag : false
            },
            methods:{
            }

        });

    </script>
```

简单的比较 v-if 指令和 v-show 指令，效果是一模一样的
点击浏览器（F12）中的查看器观察显示页面元素信息
如果 flag 为 true，观察到的结果是一致的

![](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs005.png)

如果 flag 为 false，观察到的结果是不同的

![](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs006.png)

其中 v-if 中的元素是本身就没有的，v-show 中的元素是存在的，只是通过 false 属性值，系统为该元素新增了 display:none，表示不展现该元素

通过观察得到结论：
     v-if 为 true：创建条件元素 为 false：去除该元素

​     v-show 为true：展现条件元素 为 false：隐藏该元素

在实际项目开发中，一般的需求情况下，我们使用 v-if 就可以了。但是如果对于元素的展现与否需要频繁的切换，我们需要使用 v-show的形式展现或者隐藏元素，因为 v-if 在每次切换为 true 的时候都需要重新的创建元素，降低页面展现元素的效率。

v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。

```html
<div id="app">
    <div v-if="Math.random() > 0.5">
      Sorry
    </div>
    <div v-else>
      Not sorry
    </div>
</div>
 
----------
<div id="app">
    <div v-if="type === 'A'">
      A
    </div>
    <div v-else-if="type === 'B'">
      B
    </div>
    <div v-else-if="type === 'C'">
      C
    </div>
    <div v-else>
      Not A/B/C
    </div>
</div>
```



综合应用：
完成一个基本信息系统（学生信息管理系统）的查询列表操作，可对该列表进行添加操作，可进行删除操作,可以进行查询。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    <style>
        .hFontColor{
            color:brown;
        }
        /* 文字居中 */
        .hAlign{
            text-align: center;
        }
        /* 所有的td标签居中 */
        td{
            text-align: center;
        }
        [v-cloak]{
                /* 把元素隐藏起来 */
                display: none;
            }
        
    </style>
</head>
<body>
    <div id="app">
        <!--
            模拟表结构：
                student
                id：编号
                name：姓名
                gender：性别
                age：年龄
        -->
        <!--          
            基础建设：
                搭建用来填写信息的文本框
                搭建表格结构
                搭建添加信息按钮，删除信息的按钮 
                搭建一些基础的样式
        -->
        <!--
            vuejs建设：
             data：
                    模型
                    对象集合，编号，姓名，性别，年龄
             methods：
                    添加方法，删除方法
                    扩展：查询信息列表方法
        -->
        <!--  以对象引用样式 -->
        <h3 :class="hstyle">学生信息管理系统</h3>
        <!-- 水平线 width表示宽长的百分比 -->
        <hr width="100%">
        <br/>
        编号：<input type="text" v-model="id"/>&nbsp;&nbsp; <!-- A0001 -->
        姓名：<input type="text" v-model="name"/>&nbsp;&nbsp;
        性别：<input type="text" v-model="sex"/>&nbsp;&nbsp;
        年龄：<input type="text" v-model="age"/>&nbsp;&nbsp;

        <input type="button" value="保存学员" @click="save"/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
         <!--
            搜索的方式，可以触发按钮进行搜索，也可以通过如下方式，在触发敲键盘之后，触发搜索的方法
            键盘弹起事件：keyup() 是在键盘松手就会触发
        -->
        <input type="text" v-model="sname" @keyup="search"/>
        <!-- <input type="button" value="搜索学员" @click="search"/> -->
        <br/>
        <br/>
        <!-- 搭建元素表格 -->
        <!-- cellpadding:表格单元边界与单元内容之间的间距设置 cellspacing:表格单元格间距设置 -->
        <table border="1" width="100%" align="center" cellpadding="6px" cellspacing="0px"> 
            <tr>
                <td>序号</td> 
                <td>编号</td>
                <td>姓名</td>
                <td>性别</td>
                <td>年龄</td>
                <td>操作</td> <!-- 为删除超链接提供入口 -->
            </tr>
            <!-- 内容部分 读取模型slist中的数据 使用v-for的形式对slist做遍历 -->
            <!--
                每一个s，就是每一个遍历出来的学生对象，将来在取得学生信息的时候，通过{{s.属性}}来取值
                i变量是遍历出来元素的下标，从0开始做标记，在序号中，应该是以下标+1的方式开始标记（序号从1开始计数）
            -->
            <!-- :key 记录的唯一标识 -->
            <tr v-for="(s,i) in slist" :key="s.id">
                <td v-cloak>{{i+1}}</td>
                <td v-cloak>{{s.id}}</td>
                <td v-cloak>{{s.name}}</td>
                <td v-cloak>{{s.sex}}</td>
                <td v-cloak>{{s.age}}</td>
                <td>
                    <!--
                        使用href="javascript:void(0)"将超链接的href行为禁用掉，该超链接只能以绑定事件的形式来触发行为
                        与之前学习的click的prevent的用处是一样的
                    -->
                    <!--
                        根据编号执行删除操作
                        注意：
                            在方法中传递实参，不需要使用插值表达式
                            使用方式：del(s.id)
                            而不是：del({{s.id}})
                    -->
                    <a href="javascript:viod(0)" @click="del(s.id)">删除学员</a>
                </td>
            </tr>
        </table>
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                slist : [
                    {id:"A0001",name:"zs",sex:"男",age:18},
                    {id:"A0002",name:"ls",sex:"男",age:20},
                    {id:"A0003",name:"ww",sex:"男",age:22},
                ],
                searchList : [
                    {id:"A0001",name:"zs",sex:"男",age:18},
                    {id:"A0002",name:"ls",sex:"男",age:20},
                    {id:"A0003",name:"ww",sex:"男",age:22},
                ],
                id : "",
                name : "",
                sex : "",
                age : "",
                sname : "",
                hstyle : {hFontColor : true,hAlign : true}
            },
            methods:{
                save(){
                     /*

                        通过在页面中对文本框进行信息的完善（对视图V进行数据的填充）
                        根据使用对于视图中值的绑定方式是v-model的方式，会实现双向数据绑定
                        通过对视图的数据的填充，同时也是对模型中数据的填充
                        在我们触发的save方法当中，取得模型中的值，就相当于是取得了在页面文本框填充的数据
                        将这些数据收集起来，形成一个对象，将该对象添加到我们的sList对象数据中就可以了

                    */
                   var s = {id:this.id,name:this.name,sex:this.sex,age:this.age}
                   //将对象s存放到slit的数组中
                   this.slist.push(s);
                },
                del(id){
                    //id:需要删除记录的id，根据id来进行删除
                    /*
                        遍历sList中所有的对象
                        从每一个对象中取得id信息，将每一个id与参数id进行比较
                        如果id值相等，证明我们找到了需要删除的记录
                        将该记录从sList中移除掉
                    */
                   for(var i = 0; i < this.slist.length; i++){
                       //如果id值相等，证明我们找到了需要删除的记录
                       if(this.slist[i].id == id){
                           //将该记录从sList中移除掉
                           //splice() 方法向/从数组中添加/删除项目，然后返回被删除的项目。
                           //arrayObject.splice(index,howmany,item1,.....,itemX)
                           //howmany 要删除的项目数量。如果设置为 0，则不会删除项目。
                           this.slist.splice(i,1);
                       }
                   } 

                },
                search(){
                      /*     
                        将sList备份searchList
                        将sList清空掉（等待搜索出来的对象，对sList进行重新的转配过程）

                        遍历searchList，取得每一个对象，根据对象取得名字
                        如果名字中包含输入的关键字，则证明该对象已经搜索到了，将该对象转配到sList中
                        最终展现的信息是最新经过搜索后的sList

                        注意：
                            一定要先将sList进行备份，使用其他的对象数组是不能够展现信息的，
                            因为v-for循环当中已经写好了，需要遍历的就是sList
                    */
                   //用来遍历对象信息用的
                   /*
                        我们刚才所使用的备份数据的方式，searchList是在方法中声明的局部变量
                        该变量是在触发当前方法的时候，为sList做备份
                        例如：
                            经过搜索s关键字之后，sList中经过重新装配的对象有zs和ls
                            当再一次进行搜索，再一次触发该方法的时候，为searchList备份的sList，就只能备份zs和ls这两个对象了
                            所以造成的结果，是数据越来越少，能够搜索的有效的数据的范围，仅仅只是在上一次搜索后产生的对象数组

                        对于备份的信息，一定要写成模型，而且备份的方式，是完全copy需要备份的信息
                    */
                    //searchList = this.sList;


                   //用来装配新的对象
                   this.slist = [];
                   
                   for(var i = 0; i < this.searchList.length; i++){
                       /*
                            使用indexOf方法做判断
                            如果判断结果大于等于0，说明该名称是有效的搜索项
                        */
                       if(this.searchList[i].name.indexOf(this.sname) >= 0 ){
                           //将搜索到的有效对象，重新装配到slist中的
                           this.slist.push(this.searchList[i]);
                       }
                   }
                }
            }

        });

    </script>

</body>
</html>
```

### 2.6 计算属性



在vue.js中，有methods和computed两种方式来动态当作方法来用的。

-  首先最明显的不同 就是调用的时候，methods要加上`()`
-  我们可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。

而使用 methods ，在重新渲染的时候，函数总会**重新调用**执行。

计算属性关键词: **computed**。
计算属性在处理一些复杂逻辑时是很有用的。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src="lib/vue-2.4.0.js"></script>
</head>
<body>
<div id="app">
    <!-- 1.直接拼接，方法过于繁琐   -->
    <h2>{{firstName}}{{lastName}}</h2>
    <!-- 2.通过定义methods   -->
    <h2>{{getFullName()}}</h2>
    <!-- 3.通过computed   -->
    <h2>{{fullName}}</h2>

</div>

<script>
    const vm = new Vue({

        el: "#app",
        data: {
            firstName: "hello",
            lastName: "world"
        },
        methods: {
            getFullName: function () {
                return this.firstName + ' ' + this.lastName
            }
        },
        //计算属性() 定义函数不加动词
        computed: {
            fullName: function () {
                return this.firstName + ' ' + this.lastName
            }
        }

    });

</script>

</body>
</html>
```

setter：设置值时触发，

getter：获取值时触发，

vue中computed属性默认为getter(只有只读性)，但是它还提供了setter，可以由因变量去影响自变量。



### 2.7 过滤器

1.	功能: 对要显示的数据进行特定格式化后再显示
2.	注意: 并没有改变原本的数据, 是产生新的对应的数据
3.	过滤器：
      				定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
      				语法：
      						1.注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}
      						2.使用过滤器：<font color=red>{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名"</font>
      				备注：
      						1.过滤器也可以接收额外参数、多个过滤器也可以串联
      						2.并没有改变原本的数据, 是产生新的对应的数据

```html
		<!DOCTYPE html>
		<html>
			<head>
				<meta charset="UTF-8" />
				<title>过滤器</title>
				<script type="text/javascript" src="../lib/vue-2.4.0.js"></script>
				<script src="https://cdn.bootcdn.net/ajax/libs/dayjs/1.10.6/dayjs.min.js"></script>
			</head>
			<body>
				<!-- 
					过滤器：
						定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
						语法：
								1.注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}
								2.使用过滤器：{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名"
						备注：
								1.过滤器也可以接收额外参数、多个过滤器也可以串联
								2.并没有改变原本的数据, 是产生新的对应的数据
				-->
				<!-- 准备好一个容器-->
				<div id="root">
					<h2>显示格式化后的时间</h2>
					<!-- 计算属性实现 -->
					<h3>现在是：{{fmtTime}}</h3>
					<!-- methods实现 -->
					<h3>现在是：{{getFmtTime()}}</h3>
					<!-- 过滤器实现 -->
					<h3>现在是：{{time | timeFormater}}</h3>
					<!-- 过滤器实现（传参） -->
					<h3>现在是：{{time | timeFormater('YYYY_MM_DD') | mySlice}}</h3>
					<h3 :x="msg | mySlice">尚硅谷</h3>
				</div>
		
				<div id="root2">
					<h2>{{msg | mySlice}}</h2>
				</div>
			</body>
		
			<script type="text/javascript">
				Vue.config.productionTip = false
				//全局过滤器
				//slice(x,y) 
				// 传入两个参数 一个是开始截取的下标 一个是结束截取的下标
				Vue.filter('mySlice',function(value){
					return value.slice(0,4)
				})
				
				new Vue({
					el:'#root',
					data:{
						time:1621561377603, //时间戳
						msg:'你好，尚硅谷'
					},
					computed: {
						fmtTime(){
							return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
						}
					},
					methods: {
						getFmtTime(){
							return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
						}
					},
					//局部过滤器
					filters:{
						timeFormater(value,str='YYYY年MM月DD日 HH:mm:ss'){
							// console.log('@',value)
							return dayjs(value).format(str)
						}
					}
				})
		
				new Vue({
					el:'#root2',
					data:{
						msg:'hello,atguigu!'
					}
				})
			</script>
		</html>
```



### 2.8 生命周期

 生命周期：
			1.又名：生命周期回调函数、生命周期函数、生命周期钩子。
			2.是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。
			3.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。
			4.生命周期函数中的this指向是vm 或 组件实例对象。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-pre指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../lib/vue.js"></script>
	</head>
	<body>
		
		<div id="root">
            <!-- opacity 样式透明度设置 -->
			<h2 :style="{opacity}">欢迎学习Vue</h2>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
			el:'#root',
			data:{
				opacity:1
			},
            methods: {
                
            },
            //vue完成模板的解析并把初始的真实的Dom元素放入页面后（挂载完毕）调用mounted
            mounted () {
                console.log('mouted')
                setInterval(() => {
                this.opacity -= 0.01
                if(this.opacity <= 0) this.opacity = 1  },16)
            }
		})
        //通过外部的定时器来实现（不推荐）
        //setInterval() 方法可按照指定的周期（以毫秒计）来调用函数或计算表达式。
        //自减透明度，当小于零时又让透明度回到1
        /* setInterval(() => {
            vm.opacity -= 0.01
            if(vm.opacity < 0) vm.opacity = 1  },16)
         */
	</script>
</html>
```



生命周期流程		

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png)

1)	初始化显示
*	beforeCreate()
*	created()
*	beforeMount()
*	mounted()
2)	更新状态: this.xxx = value
*	beforeUpdate()
*	updated()

3. 销毁 vue 实例: vm.$destory()

*	beforeDestory()
*	destoryed()



常用的生命周期方法

mounted(): 发送 ajax 请求, 启动定时器等异步任务

beforeDestory(): 做收尾工作, 如: 清除定时器

```HTML
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>引出生命周期</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
				常用的生命周期钩子：
						1.mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。
						2.beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。

				关于销毁Vue实例
						1.销毁后借助Vue开发者工具看不到任何信息。
						2.销毁后自定义事件会失效，但原生DOM事件依然有效。
						3.一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 :style="{opacity}">欢迎学习Vue</h2>
			<button @click="opacity = 1">透明度设置为1</button>
			<button @click="stop">点我停止变换</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		 new Vue({
			el:'#root',
			data:{
				opacity:1
			},
			methods: {
				stop(){
					this.$destroy()
				}
			},
			//Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂载完毕）调用mounted
			mounted(){
				console.log('mounted',this)
				this.timer = setInterval(() => {
					console.log('setInterval')
					this.opacity -= 0.01
					if(this.opacity <= 0) this.opacity = 1
				},16)
			},
			beforeDestroy() {
				clearInterval(this.timer)
				console.log('vm即将驾鹤西游了')
			},
		})

	</script>
</html>
```



## 第三章 组件化开发



### 3.1 认识组件化

vue.js 有两大法宝，一个是数据驱动，另一个就是组件化，那么问题来了，什么叫做组件化，为什么要组件化？接下来我就针对这两个问题一一解答，所谓组件化，就是把页面拆分成多个组件，每个组件依赖的 CSS、JS、模板、图片等资源放在一起开发和维护。 因为组件是资源独立的，所以组件在系统内部可复用，组件和组件之间可以嵌套，如果项目比较复杂，可以极大简化代码量，并且对后期的需求变更和维护也更加友好。

组件化思想的应用：

- 有了组件化的思想，我们在之后的开发中就要充分的利用它。
- 尽可能的将页面拆分成一个个小的、可复用的组件。
- 这样让我们的代码更加方便组织和管理，并且扩展性也更强。

![images](https://gitee.com/yybovo/note-images/raw/master/Typora/71F2A9A2851F41DAAD787B94EEE11C40)

![images](https://img-blog.csdnimg.cn/20181220155021919)

### 3.2 组件的基本使用

- 组件的使用分成三个步骤：
  - 创建组件构造器
  - 注册组件
  - 使用组件

<img src="https://gitee.com/yybovo/note-images/raw/master/Typora/5B361E08D4BE40BEBA9322676D25CB47" alt="images" style="zoom: 67%;" />



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue-2.4.0.js"></script>
</head>
<body>

<div id="app">
    <!--3.使用组件-->
    <my-cpn></my-cpn>
</div>

<script>
    //1.创建组件构造对象
    //属性 template ：模板
    const cpnC = Vue.extend({
        template:`
        <div>
            <h2>我是标题</h2>
            <p>我是段落1111</p>
            <p>我是段落2222</p>
        </div>`
    })
    //2.注册组件
    Vue.component('my-cpn',cpnC)

    const vm = new Vue({
        el : "#app",
        data : {
            message : '你好啊'
        }
    })
</script>
</body>
</html>
```

- 1.Vue.extend()：
  - 调用Vue.extend()创建的是一个组件构造器。 
  - 通常在创建组件构造器时，传入template代表我们自定义组件的模板。
  - 该模板就是在使用到组件的地方，要显示的HTML代码。
  - 事实上，这种写法在Vue2.x的文档中几乎已经看不到了，它会直接使用下面我们会讲到的语法糖，但是在很多资料还是会提到这种方式，而且这种方式是学习后面方式的基础。

- 2.Vue.component()：
  - 调用Vue.component()是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称。
  - 所以需要传递两个参数：1、注册组件的标签名 2、组件构造器

- 3.组件必须挂载在某个Vue实例下，否则它不会生效。



<b>非单文件组件</b>

1.	模板编写没有提示
2.	没有构建过程, 无法将 ES6 转换成 ES5
3.	不支持组件的 CSS
4.	真正开发中几乎不用

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title></title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../lib/vue.js"></script>
	</head>
	<body>
		<!-- 
			Vue中使用组件的三大步骤：
					一、定义组件(创建组件)
					二、注册组件
					三、使用组件(写组件标签)

			一、如何定义一个组件？
						使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别；
						区别如下：
								1.el不要写，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。
								2.data必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。
						备注：使用template可以配置组件结构。

			二、如何注册组件？
							1.局部注册：靠new Vue的时候传入components选项
							2.全局注册：靠Vue.component('组件名',组件)

			三、编写组件标签：
							<school></school>
		-->
		<!-- 准备好一个容器-->
		<div id="root">
            <!-- 3.编写组件标签 -->
            <hello></hello>
            <hr>
            <school></school>
            <hr>
            <student></student>
		</div>
        <div id="root2">
            <!-- 3.编写组件标签 -->
            <hello></hello>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
        //1.第一步，创建学校组件
        const school = Vue.extend({
            // el:'root'    组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
            template:`
            <div>
                <h2>{{shcoolName}}</h2>
                <h2>{{address}}</h2>
            </div>
            `,
            data () {
                return {
                    shcoolName:'湖南软件职业大学',
                    address:'湖南湘潭市雨湖区',
                }
            }
        })
        //1.第一步，创建学生组件
        const student = Vue.extend({
            template:`
            <div>
                <h2>{{studentName}}</h2>
                <h2>{{age}}</h2>
                <button @click='btnC'>按钮<button>
            </div>
            `,
            data(){
                return{
                    studentName:'龙宫礼奈',
                    age:17
                }
            },
            methods:{
                btnC(){
                    alert(this.studentName)
                }
            }
        })
        //第一步，创建hello组件
        const hello = Vue.extend({
            template:`
            <div>
               <h2>你好啊！{{name}}</h2>
            </div>
            `,
            data(){
                return{
                    name:'龙宫礼奈',
                }
            },
        })

        //全局注册组件
        Vue.component('hello',hello)

	new Vue({
			el:'#root',
			data:{
				// shcoolName:'湖南软件职业大学',
                // address:'湖南湘潭市雨湖区',
                // studentName:'龙宫礼奈',
                // age:17
			},
            methods: {
               
            },
            //2.组件注册(局部注册)
            components: {
                school,
                student
            }
		})

    new Vue({
        el:'#root2',
    })
        
	</script>

</html>
```

几个注意点：
					1.关于组件名:
								一个单词组成：
											第一种写法(首字母小写)：school
											第二种写法(首字母大写)：School
								多个单词组成：
											第一种写法(kebab-case命名)：my-school
											第二种写法(CamelCase命名)：MySchool (需要Vue脚手架支持)
								备注：
										(1).组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行。
										(2).可以使用name配置项指定组件在开发者工具中呈现的名字。

​					2.关于组件标签:
​								第一种写法：`<school></school>`
​								第二种写法：`<school/>`
​								备注：不用使用脚手架时，`<school/>`会导致后续组件不能渲染。

​					3.一个简写方式：
​								  const school = Vue.extend(options) 可简写为：const school = options



<b>单文件组件</b>

一个.vue 文件的组成(3 个部分)
模板页面
`<template>页面模板</template>`

JS 模块对象

```js
<script> 
  export default {
    data() {
      return {}
    }, 
    methods: {}, 
    computed: {}, 
    components: {}
  }
</script> 
```

样式

`<style>样式定义</style>`



1.	引入组件
2.	映射成标签
3.	使用组件标签



### 3.3 全局组件和局部组件

- 当通过调用Vue.component()注册组件时，组件的注册是全局的
  - 该组件可以在任意Vue示例下使用。
- 如果注册的组件是挂载在某个实例中, 那么就是一个局部组件

![images](https://gitee.com/yybovo/note-images/raw/master/Typora/05AC77A4549C4FAF9DFCA6DDFDCBD857)



### 3.4 父组件和子组件



<font color=red>子组件必须要在父组件之前</font>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title></title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../lib/vue.js"></script>
	</head>
	<body>

		<!-- 准备好一个容器-->
		<div id="root">
            <!-- 3.编写组件标签 -->
            <app></app>
		</div>
        
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

        //1.第一步，创建学生组件
        const student = Vue.extend({
            template:`
            <div>
                <h2>{{studentName}}</h2>
                <h2>{{age}}</h2>
            </div>
            `,
            data(){
                return{
                    studentName:'龙宫礼奈',
                    age:17
                }
            },
        
        })

        //1.第一步，创建学校组件
        const school = Vue.extend({
            // el:'root'    组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
            template:`
            <div>
                <h2>{{shcoolName}}</h2>
                <h2>{{address}}</h2>
                <student></student>
            </div>
            `,
            data () {
                return {
                    shcoolName:'湖南软件职业大学',
                    address:'湖南湘潭市雨湖区',
                }
            },
            //2.组件注册(局部注册)
            components: {
                student
            }
        })

        //定义hello组件
        const hello = Vue.extend({
            template:`
                <h1>{{msg}}</h1>
            `,
            data(){
                return{
                    msg:'你好礼奈同学!!!'
                }
            }
        })

        //定义app根组件
        const app = Vue.extend({
            template:`
            <div>
                <hello></hello>
                <school></school>
            </div>
            `,
            components:{
                school,
                hello
            }
        })
        
        
new Vue({
			el:'#root',
			data:{
				// shcoolName:'湖南软件职业大学',
                // address:'湖南湘潭市雨湖区',
                // studentName:'龙宫礼奈',
                // age:17
			},
            methods: {
               
            },
            //2.组件注册(局部注册)
            components: {
                app
            }
		})   
	</script>

</html>
```



<b>VueComponent</b>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title></title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../lib/vue.js"></script>
	</head>
	<body>
        <!-- 
			关于VueComponent：
						1.school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的。

						2.我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的实例对象，
							即Vue帮我们执行的：new VueComponent(options)。

						3.特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent！！！！

						4.关于this指向：
								(1).组件配置中：
											data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【VueComponent实例对象】。
								(2).new Vue(options)配置中：
											data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象】。

						5.VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。
							Vue的实例对象，以后简称vm。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
            <!-- 3.编写组件标签 -->
            <school></school>
            <hello></hello>
		</div>
        
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

        

        //1.第一步，创建学校组件
        const school = Vue.extend({
            // el:'root'    组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
            template:`
            <div>
                <h2>{{shcoolName}}</h2>
                <h2>{{address}}</h2> 
            </div>
            `,
            data () {
                return {
                    shcoolName:'湖南软件职业大学',
                    address:'湖南湘潭市雨湖区',
                }
            },
            
        })
        //定义hello组件
        const hello = Vue.extend({
            template:`
                <h1>{{msg}}</h1>
            `,
            data(){
                return{
                    msg:'你好礼奈同学!!!'
                }
            }
        })
        console.log('@',school==hello)//false
        console.log('#',hello)

        
new Vue({
			el:'#root',
			data:{
				
			},
            methods: {
               
            },
            //2.组件注册(局部注册)
            components: {
                school,
                hello
            }
		})   
	</script>

</html>
```



<b>内置关系</b>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>VueComponent</title>
		<script type="text/javascript" src="../lib/vue.js"></script>
	</head>
	<body>
        <!-- 
				1.一个重要的内置关系：VueComponent.prototype.__proto__ === Vue.prototype
				2.为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<school></school>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
        Vue.prototype.x = 99
        //定义school组件
		const school = Vue.extend({
			name:'school',
			template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
                    <button @click='showX'>按钮</button>
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					address:'北京'
				}
			},
            methods: {
                showX(){
                    alert('x='+this.x);
                }
            }
		})


		new Vue({
			el:'#root',
            data:{
                msg:'你好'
            },
            components: {
                school
            }
			
		})
        console.log(school.prototype.__proto__ === Vue.prototype)//true




        //原型的概念 对于构造函数创建对象方法的时候，若多个对象共有属性或方法，则可使用原型进行初始化
        //定义一个构造函数
        /* function Demo(){
            this.a = 1,
            this.b = 2
        }
        //创建一个Demo实例对象
        const d = new Demo();
        console.log(Demo.prototype)//显示原型属性
        console.log(d.__proto__)//显示原型属性
        console.log(Demo.prototype === d.__proto__)//true

        //程序员通过显示原型属性操作原型对象，追加一个x属性，值为99
        Demo.prototype.x = 99
        console.log('@',d) */
	</script>
</html>
```





### 3.5 注册的语法糖

在上面注册组件的方式，可能会有些繁琐。
Vue为了简化这个过程，提供了注册的语法糖。
主要是省去了调用Vue.extend()的步骤，而是可以直接使用一个对象来代替。
语法糖注册全局组件和局部组件：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue-2.4.0.js"></script>
</head>
<body>
<div id="app">
    <cpn1></cpn1>
    <cpn2></cpn2>
</div>
<script>
    //全局组件注册语法糖
    //1.创建组件构造器
    // const cpnC1 =Vue.extend()
    //2.注册全局组件
    Vue.component(
        'cpn1',{
        template : `
        <div>
           <h2>我是标题</h2>
           <p>我是内容111</p>
        </div>`
    })
    //注册局部组件的语法糖
    const vm = new Vue({
        el : "#app",
        data : {
        },
        components : {
            'cpn2' : {
                template: `
                <div>
                <h2>我是标题</h2>
                <p>我是内容222</p>
                </div>`
            }
        }
    })
</script>
</body>
</html>
```



### 3.6 模板的分类写法

通过语法糖简化了Vue组件的注册过程，另外还有一个地方的写法比较麻烦，就是template模块写法。
如果能将其中的HTML分离出来写，然后挂载到对应的组件上，必然结构会变得非常清晰。
Vue提供了两种方案来定义HTML模块内容：
使用<kbd><script></kbd>标签
使用<kbd><template></kbd>标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue-2.4.0.js"></script>
</head>
<body>

<div id="app">
    <cpn1></cpn1>
    <cpn2></cpn2>
</div>
<!--script标签 注意：类型必须是text/x-template-->
<!--<script type="text/x-template" id="cpn">
<div>
    <h2>我是标题</h2>
    <p>我是段落111</p>
</div>
</script>-->
<!--template标签-->
<template id="cpn">
    <div>
        <h2>我是标题</h2>
        <p>我是段落222</p>
    </div>
</template>
<script>
    //全局组件注册语法糖
    Vue.component(
        'cpn1',{
            template : '#cpn1'
        })
    const vm = new Vue({
        el : "#app",
        data : {
        }
    })
</script>
</body>
</html>
```



### 3.7 数据的存放

组件对象也有一个data属性(也可以有methods等属性),只是这个data属性必须是一个函数,而且这个函数返回一个对象，对象内部保存着数据.

* 子组件不能直接访问父组件
* 子组件中有自己的data, 而且必须是一个函数.
* 为什么必须是一个函数.
  - 如果不是一个函数，Vue直接就会报错。
  - 组件是可复用的vue实例，一个组件被创建好之后，就可能被用在各个地方而组件不管被复用了多少次，<font color=red>组件中的data数据都应该是相互隔离，互不影响的</font>
  - 组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一份新的data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据<font color=red>而单纯的写成对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都会变的结果。</font>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue-2.4.0.js"></script>
</head>
<body>

<div id="app">
    <cpn></cpn>
    <cpn></cpn>
    <cpn></cpn>
</div>

<template id="cpn">
    <div>
        <h2>当前计数：{{counts}}</h2>
        <button @click="increment">+</button>
        <button @click="decrement">-</button>
    </div>
</template>
<script>
    //全局组件注册语法糖
    const obj = {
        counts : 0
    }
    Vue.component(
        'cpn',{
            template : '#cpn',
            //数据不会相互影响 返回的不是同一个对象
           /* data(){
                return{
                    counts : 0
                }
            }*/
            //数据会相互影响 返回的是同一个对象
            data(){
                 return obj
            },
            methods:{
                increment(){
                    this.counts++
                },
                decrement(){
                    this.counts--
                }
            }
        })
    const vm = new Vue({
        el : "#app",
        data : {
        },
        methods: {}
    })
</script>
</body>
</html>
```



### 3.8 父子组件的通信

子组件是不能引用父组件或者Vue实例的数据的。
但是，在开发中，往往一些数据确实需要从上层传递到下层：比如在一个页面中，我们从服务器请求到了很多的数据。
其中一部分数据，并非是我们整个页面的大组件来展示的，而是需要下面的子组件进行展示。
这个时候，并不会让子组件再次发送一个网络请求，而是直接让大组件(父组件)将数据传递给小组件(子组件)。

如何进行父子组件间的通信呢？
Vue官方提到

- 通过props向子组件传递数据
- 通过事件向父组件发送消息

在下面的代码中，直接将Vue实例当做父组件，并且其中包含子组件来简化代码。
真实的开发中，Vue实例和子组件的通信和父组件和子组件的通信过程是一样的。

#### 3.8.1 props基本用法

<font color=red>在vue的中文官网有这样的说明：HTML 中的特性名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名。
重申一次，如果你使用字符串模板，那么这个限制就不存在了。
当组件中template及props等使用驼峰式命名，在html中对应的改成短横线命名方式。</font>

- props选项是使用一个数组。

- 除了数组之外，我也可以使用对象，当需要对props进行类型等验证时，就需要对象写法了。

- 验证都支持哪些数据类型呢？

  String、Number、Boolean、Array、Object、Date、Function、Symbol

- props的值有两种方式：
  方式一：字符串数组，数组中的字符串就是传递时的名称。

  方式二：对象，对象可以设置传递时的类型，也可以设置默认值等父传子: props

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script src="lib/vue.js"></script>
  </head>
  <body>
  
  <div id="app">
     <!--<cpn  :cmovies="movies"></cpn>-->
     <!--<cpn :cmovies="movies" :cmessage="message"></cpn>-->
      <cpn :cmessage="message" :cmovies="movies"></cpn>
  </div>
  
  <template id="cpn">
      <div>
          <ul>
              <li v-for="item in cmovies">{{item}}</li>
          </ul>
          <p>{{cmessage}}</p>
      </div>
  </template>
  
  <script>
  
      //创建组件构造器(子组件)
  
      const cpn = ({
          template:`#cpn`,
          //字符串数组
          //props : ['cmovies','cmessage'],
          props : {
              //类型限制
              // comvies:Array,
              // cmessage:String,
  
              //提供一些默认值
              //属性 required Boolean类型 使用组件实例使用必须传属性(:message)不然会报错
              cmessage:{
                  type:String,
                  default:'aaaaa',
                  required:true
              },
          // 类型是对象或者数组时, 默认值必须是一个函数
          cmovies: {
              type: Array,
              default() {
                  return []
              }
          }
          },
          data(){
              return{
  
              }
          },
          methods:{
          }
      })
  
      //root组件(当成父组件)
      const vm = new Vue({
          el : "#app",
          data : {
              message : '你好啊',
              movies : ['恶灵','亡灵','地平线']
          },
          //局部注册组件
          components : {
             cpn
          }
      })
  </script>
  </body>
  </html>
  
  
  Vue.components('my-components',{
    props: {
      // 基础的类型检查('null' 匹配任何类型)
      propA： Number,
      // 多个可能的类型
      propB: [String, Number],
      // 必填的字符串
      propC: {
        type: String,
        required: true
      },
      // 带有默认的数字
      propD: {
        type: Number,
        default: 100
      },
      // 带有默认值的对象
      propE: {
        type: Object,
        // 对象或数组默认值必须从一个工厂函数获取
        default: function (){
          return {message: 'Hello'}
        }
      },
      // 自定义验证函数
      propF: {
        validator: function (value) {
          // 这个值必须匹配下列字符串中的一个
          return ['success', 'warning', 'danger'].indexOf(value) !== -1
        }
      }
    }
  })
  ```

  - 当我们有自定义构造函数时，验证也支持自定义的类型

  ```html
  function Person (firstName, LastName){
    this.firstName = firstName
    this.lastName = lastName
  }
  
  Vue.component('blog-post', {
    props: {
      author: Person
    }
  })
  ```




- props用于父组件向子组件传递数据，还有一种比较常见的是子组件传递数据或事件到父组件中。

- 我们应该如何处理呢？这个时候，我们需要使用自定义事件来完成。

- 什么时候需要自定义事件呢？
  - 当子组件需要向父组件传递数据时，就要用到自定义事件了。
  - 我们之前学习的v-on不仅仅可以用于监听DOM事件，也可以用于组件间的自定义事件。
  
- 自定义事件的流程：
  - 在子组件中，通过$emit()来触发事件。
  - 在父组件中，通过v-on来监听子组件事件。
  
  子组件可以使用 $emit 触发父组件的自定义事件。
  
  vm.$emit( event, arg ) //触发当前实例上的事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue.js"></script>
</head>
<body>
<!--父组件模板-->
<div id="app">
    <!-- 监听子组件事件item-click -->
    <cpn @item-click="cpnClick"></cpn>
</div>

<!--子组件模板-->
<template id="cpn">
    <div>
        <button v-for="item in categories"
                @click="btnClick(item)">
            {{item.name}}
        </button>
    </div>
</template>

<script src="../js/vue.js"></script>
<script>

    // 1.子组件
    const cpn = {
        template: `#cpn`,
        data() {
            return {
                categories: [
                    {id: 'aaa', name: '热门推荐'},
                    {id: 'bbb', name: '手机数码'},
                    {id: 'ccc', name: '家用家电'},
                    {id: 'ddd', name: '电脑办公'},
                ]
            }
        },
        methods: {
            btnClick(item) {
                // 发射事件: 自定义事件
                this.$emit('item-click', item)
            }
        }
    }

    // 2.父组件
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊'
        },
        components: {
            cpn
        },
        methods: {
            <!-- 定义好一个函数 -->
            cpnClick(item) {
                console.log('cpnClick', item.id, item.name);
            }
        }
    })
</script>
```

#### 3.8.2 父子组件的访问方式： $children

- 有时候需要父组件直接访问子组件，子组件直接访问父组件，或者是子组件访问跟组件。
  - 父组件访问子组件：使用$children或$refs
  - 子组件访问父组件：使用$parent
- $children的缺陷：
  - 通过$children访问子组件时，是一个数组类型，访问其中的子组件必须通过索引值。
  - 但是当子组件过多，我们需要拿到其中一个时，往往不能确定它的索引值，甚至还可能会发生变化。
  - 有时候，我们想明确获取其中一个特定的组件，这个时候就可以使用$refs

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs011.png)

#### 3.8.3 父子组件的访问方式： $refs

- $refs的使用：
  - $refs和ref指令通常是一起使用的。
  - 首先，我们通过ref给某一个子组件绑定一个特定的ID。
  - 其次，通过this.$refs.ID就可以访问到该组件了。

```html
<child-cpn1 ref="child1"></child-cpn1>
<child-cpn2 ref="child2"></child-cpn2>
<button @click="showRefsCpn"></button>

showRefscpn() {
      console.log(this.$refs.child1.message);
       console.log(this.$refs.child2.message);
    }
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue-2.4.0.js"></script>
</head>
<body>

<div id="app">
    <cpn ref="aaa"></cpn>
    <button @click="btnClick">按钮</button>
</div>

<template id="cpn">
    <div>我是子组件</div>
</template>

<script>

    const vm = new Vue({
        el : "#app",
        data : {
        },
        methods: {

            btnClick(){
                //1.children
              /*console.log(this.$children)
              for (let c of this.$children){
                    console.log(c.name);
                    c.showMessage();
                }*/
                //2.refs
                console.log(this.$refs.aaa.name);
            }
        },
        components : {
            cpn : {
                template : '#cpn',
                methods : {
                    showMessage(){
                        console.log('showMessage')
                    }
                },
                data(){
                    return{
                        name : '我是子组件的name'
                    }
                }


            }
        }
    })
</script>
</body>
</html>
```

#### 3.8.4 父子组件的访问方式： $parent

- 如果想在子组件中直接访问父组件，可以通过$parent
- 注意事项：
  - 尽管在Vue开发中，我们允许通过$parent来访问父组件，但是在真实开发中尽量不要这样做。
  - 子组件应该尽量避免直接访问父组件的数据，因为这样耦合度太高了。
  - 如果我们将子组件放在另外一个组件之内，很可能该父组件没有对应的属性，往往会引起问题。
  - 另外，更不好做的是通过$parent直接修改父组件的状态，那么父组件中的状态将变得飘忽不定，很不利于我的调试和维护

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs012.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue-2.4.0.js"></script>
</head>
<body>
<div id="app">
    <cpn></cpn>
</div>
<template id="cpn">
    <div >
        <h2>我是cpn组件</h2>
        <cpnn></cpnn>
    </div>
</template>
<template id="cpnn">
    <div >
        <h2>我是子组件</h2>
        <button @click="btnClick">按钮</button>
    </div>
</template>

<script>

    const vm = new Vue({
        el : "#app",
        data : {
            message:'你好'
        },
        methods: {

        },
        components : {
            cpn : {
                template : '#cpn',
                data(){
                    return{
                        name : '我是cpn组件的name'
                    }
                },
                components: {
                    cpnn: {
                        template: '#cpnn',
                        methods: {
                            btnClick(){
                                //1.访问父组件$sprent
                                // console.log(this.$parent);
                                // console.log(this.$parent.name);
                                //2.访问根组件$root
                                console.log(this.$root);
                                console.log(this.$root.message);
                            }
                        }
                    }
                }
            }
        }
    })
</script>
</body>
</html>
```



### 3.9 插槽Slot（高级）

- 组件的插槽：
  - 组件的插槽也是为了让我们封装的组件更加具有扩展性。
  - 让使用者可以决定组件内部的一些内容到底展示什么。

- 如何封装合适呢？抽取共性，保留不同。
  - 最好的封装方式就是将共性抽取到组件中，将不同暴露为插槽。
  - 一旦我们预留了插槽，就可以让使用者根据自己的需求，决定插槽中插入什么内容。
  - 是搜索框，还是文字，还是菜单。由调用者自己来决定。

- 插槽的基本使用 `<slot></slot>`
- 插槽的默认值 `<slot>button</slot>`
- 如果有多个值, 同时放入到组件进行替换时, 一起作为替换元素

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs013.png)

<b>具名插槽slot</b>

当子组件的功能复杂时，子组件的插槽可能并非是一个。
比如封装一个导航栏的子组件，可能就需要三个插槽，分别-代表左边、中间、右边。
那么，外面在给插槽插入内容时，如何区分插入的是哪一个呢？
这个时候，我们就需要给插槽起一个名字

如何使用具名插槽呢？
非常简单，只要给slot元素一个name属性即可
`<slot name='myslot'></slot>`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue-2.4.0.js"></script>
</head>
<!--
1.插槽的基本使用 <slot></slot>
2.插槽的默认值 <slot>button</slot>
3.如果有多个值, 同时放入到组件进行替换时, 一起作为替换元素
-->
<body>
<div id="app">
    <cpn><span slot="left">呵呵呵</span></cpn>
    <cpn><button slot="left">呵呵呵</button></cpn>
</div>
<template id="cpn">
    <div >
        <h2>我是组件</h2>
        <slot name="left"><span>左边</span></slot>
        <slot name="center"><span>中间</span></slot>
        <slot name="right"><span>右边</span></slot>
        <slot>哈哈哈</slot>
    </div>
</template>


<script>

    const vm = new Vue({
        el : "#app",
        data : {
            message:'你好'
        },
        methods: {

        },
        components : {
            cpn : {
                template : '#cpn',
                data(){
                    return{

                    }
                },
                components: {

                }
            }
        }
    })
</script>
</body>
</html>
```



<b>编译作用域</b>

- 官方给出了一条准则：父组件模板的所有东西都会在父级作用域内编译；子组件模板的所有东西都会在子级作用域内编译。
- 在子组件中，使用特殊的元素`<slot>`就可以为子组件开启一个插槽。
- 该插槽插入什么内容取决于父组件如何使用。



<b>作用域插槽</b>

父组件替换插槽的标签，但是内容由子组件来提供。

在父组件使用子组件时，从子组件中拿到数据：
通过`<template slot-scope="slot">`获取到slot属性
在通过slot.data就可以获取到刚才我们传入的data了

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/vue.js"></script>
</head>
<body>
<div id="app">
    <cpn></cpn>
    <cpn>
        <!--目的是获取子组件中的pLanguages-->
        <!--2.5.x以下需要使用模板，以上则不需要-->
        <template slot-scope="slot">
            <!--引用插槽对象-->
            <!--<span v-for="item in slot.data">{{item}}-</span>-->
            <!--join()方法将一个数组（或一个类数组对象）的所有元素连接一个字符串并返回这个字符串。-->
            <span>{{slot.data.join(' - ')}}</span>
        </template>
    </cpn>
</div>

<template id="cpn">
    <div >
        <h2>我是组件</h2>
        <slot :data="pLanguages">
            <ul>
                <li v-for="item in pLanguages">{{item}}</li>
            </ul>
        </slot>
    </div>
</template>


<script>

    const vm = new Vue({
        el : "#app",
        data : {
            message:'你好'
        },
        methods: {

        },
        components : {
            cpn : {
                template : '#cpn',
                data(){
                    return{
                        pLanguages:['javascript','c++','java','c#','python','Go']
                    }
                }
            }
        }
    })
</script>
</body>
</html>
```



## 第四章 模块化开发



### 4.1 JavaScript原始功能

- 在网页开发的早期，js制作作为一种脚本语言，做一些简单的表单验证或动画实现等，那个时候代码还是很少的。

  - 直接将代码写在`<script>`标签中即可

- 随着ajax异步请求的出现，慢慢形成了前后端的分离

  - 客户端需要完成的事情越来越多，代码量也是与日俱增。
  - 为了应对代码量的剧增，我们通常会将代码组织在多个js文件中，进行维护。
  - 但是这种维护方式，依然不能避免一些灾难性的问题

  

### 4.2 利用匿名函数的解决方案

- 可以使用匿名函数来解决方面的重名问题
- 先创建两个js文件
  - 在aaa.js文件中，我们使用匿名函数

```js
(function() {
  var lazy = true
})
```

- 但是如果在main.js文件中，想要用到lazy，应该如何处理呢？

  - 显然，另外一个文件中不容易使用，因为lazy是一个局部变量。

  

### 4.3 使用模块作为出口

常见的模块化规范：CommonJS、AMD、CMD，也有ES6的Modules

<b>CommonJS</b>

- 模块化有两个核心：导出和导入

  CommonJS的导出：

```js
modul.exports = {
  lazy: true,
  test(a, b) {
    return a + b
  },
  demo(a, b) {
    return a * b
  }
}
```

​     CommonJS的导入

```js
//CommonJs模块
let {test, demo, lazy} = require('moduleA')

//等同于
let _mA = require('moduleA')
let test = _mA.text
let demo = _mA.demo
let lazy = _mA.lazy
```



<b>ES6的export指令</b>(使用该模块化会自动开启严格模式规范)

- export指令用于导出变量，比如下面的代码：



```js
//info.js
export let name = 'why'
export let age = 18
export let height = 1.78
```

- 上面的代码还有另外一种写法：



```js
//info.js
let name = 'why'
let age = 18
let height = 1.78

export {name, age, height}
```

- 上面我们主要输出变量，也可以输出函数或者输出类
- 某些情况下，一个模块中包含某个的功能，我们并不希望给这个功能命名，而且让导入者可以自己来命名
  - 这个时候就可以使用export default



```js
// info.js
export default function () {
  console.log('default function')
}
```

- 我们来到main.js中，这样使用就可以了
- 这里的myLazy是我自己命名的，你可以根据需要命名它对应的名字



```js
import myLazy from './info.js'
myLazy()
```

- 另外，需要注意：
  - export default在同一个模块中，不允许同时存在多个
- 我们使用export指令导出了模块对外提供的接口，下面我们就可以通过import命令来加载对应- 的这个模块了



import

- <font color=red>需要在HTML代码中引入两个js文件，并且类型需要设置为module</font>

```html
<script src="info.js" type="module"></script>
<script src="main.js" type="module"></script>
```

- import指令用于导入模块中的内容，比如main.js的代码



```js
import {name, age, height} from "./info.js"
console.log(name, age, heigth)
```

- 如果我们希望某个模块中所有的信息都导入，一个个导入显然有些麻烦：
  - 通过*可以导入模块中所有的export变量
  - 但是通常情况下我们需要给*起一个别名，方便后续的使用

```js
import * as info from './info.js'
console.log(info.name, info.age, info.height, info.friends)
```



```html
//index界面，导入各种js文件
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="aaa.js" type="module"></script>
    <script src="bbb.js" type="module"></script>
    <script src="main.js" type="module"></script>
</head>
<body>

</body>
</html>

//aaa.js
var name = '小明'
var age = 18
var flag = true

function sum(num1,num2) {
    return num1+num2
}
if (flag){
    console.log(sum(20,30))
}
//export指令用于导出变量
//导出方式一：
export {
    flag,sum
}
//导出方式二：
export var num1 = 1000;
export var height = 1.88;

//导出函数/类
export function mul(num1,num2) {
    return num1-num2;
}

export class Person{
    run(){
        console.log('在奔跑');
    }
}

//export default 默认导出
// const address = '常德市'
// export default address
export default function (argument) {
    console.log(argument);
}

//bbb.js
//import指令用于导入模块中的内容
import {sum} from './aaa.js'

var name = '小红'
var flag = false
console.log(sum(100,200));

//main.js
//导入{}中定义的变量
import {flag,sum} from "./aaa.js";

if (flag){
    console.log('我是天才');
}

//导入直接export定义的变量
import {num1,height} from "./aaa.js";

console.log(num1);
console.log(height);

//导入export的function
import {mul,Person} from "./aaa.js";

console.log(mul(200,200));
const p = new Person();
p.run();

//导入默认的变量
//aaa 相当于 address ,function()

import aaa from "./aaa.js";
console.log(aaa)

//全部导入 bbb别名 通过bbb.xxx 调用
import * as bbb from "./aaa.js";

console.log(bbb.flag);
console.log(bbb.height);
```



## 第五章 Vue Webpack



### 5.1 Webpack的概念

从本质上来讲，webpack是一个现代的JavaScript应用的静态模块打包工具。

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs014.png)

在ES6之前，要想进行模块化开发，就必须借助于其他的工具，可以进行模块化开发。并且在通过模块化开发完成了项目后，还需要处理模块间的各种依赖，并且将其进行整合打包。而webpack其中一个核心就是让我们可能进行模块化开发，并且会帮助我们处理模块间的依赖关系。而且不仅仅是JavaScript文件，我们的CSS、图片、json文件等等在webpack中都可以被当做模块来使用这就是webpack中模块化的概念。

官网：https://webpack.docschina.org/

Webpack打包

将Webpack中的各种资源模块进行打包合并成一个或多个包(Bundle)。并且在打包的过程中，还可以对资源进行处理，比如压缩图片，将scss转成css，将ES6语法转成ES5语法，将TypeScript转成JavaScript等等操作。



#### 5.1.1 webpack和gulp对比

- grunt/gulp的核心是Task
  - 可以配置一系列的task，并且定义task要处理的事务（例如ES6、ts转化，图片压缩，scss转成css）
  - 让grunt/gulp来依次执行这些task，而且让整个流程自动化。
  - grunt/gulp也被称为前端自动化任务管理工具。



- 什么时候用grunt/gulp呢？

  - 如果工程模块依赖非常简单，甚至是没有用到模块化的概念。

  - 只需要进行简单的合并、压缩，就使用grunt/gulp即可。

  - 但是如果整个项目使用了模块化管理，而且相互依赖非常强，我们就可以使用更加强大的webpack了。

    

- grunt/gulp和webpack有什么不同呢？
  - grunt/gulp更加强调的是前端流程的自动化，模块化不是它的核心。
  - webpack更加强调模块化开发管理，而文件压缩合并、预处理等功能，是他附带的功能。



#### 5.1.2 Webpack 安装

- 安装webpack首先需要安装Node.js，Node.js自带了软件包管理工具npm

  - 官网https://nodejs.org/en/download/下载相应node.js的版本

  -  安装成功，测试安装是否成功，运行CMD，分别输入**node -v** 和 **npm -v** 分别查看node和npm的版（npm随安装程序自动安装，作用就是对Node.js依赖的包进行管理）

  - 配置npm在安装全局模块时的路径和缓存cache的路径（因为在执行例如npm install webpack -g等命令全局安装的时候，默认会将模块安装在C:\Users\用户名\AppData\Roaming路径下的npm和npm_cache中，不方便管理且占用C盘空间）所以这里配置自定义的全局模块安装目录，在node.js安装目录下新建两个文件夹 node_global和node_cache

    然后在cmd命令下执行如下两个命令：

    ```
    npm config set prefix "D:\nodejs\node_global"
    
    npm config set cache "D:\nodejs\node_cache"
    ```

    执行完后，配置环境变量，如下：

    - “环境变量” -> “系统变量”：新建一个变量名为 “**NODE_PATH**”， 值为**“D:\nodejs\node_modules”**，

      ![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs015.png)

    - “环境变量” -> “用户变量”：编辑用户变量里的**Path**，将相应npm的路径（“C:\Users\用户名\AppData\Roaming\npm”）改为：“**D:\nodejs\node_global**”

      ![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs016.png)

  - 测试

    在cmd命令下执行 **npm install webpack -g** 安装webpack

     在cmd命令下执行 **webpack -v** 查看webpack版本

    安装完，执行webpack -v命令出现以下提示

    ```js
    One CLI for webpack must be installed. These are recommended choices, delivered as separate packages:
     - webpack-cli (https://github.com/webpack/webpack-cli)
       The original webpack full-featured CLI.
    We will use "npm" to install the CLI via "npm install -D".
    Do you want to install 'webpack-cli' (yes/no): no
    You need to install 'webpack-cli' to use webpack via CLI.
    You can also install the CLI manually.
    ```

    

    ```js
    //使用全局的方式安装webpack-cli
    npm install webpack-cli -g
    ```

    原因

    如果你webpack和webpack-cli是局部安装的，想要使用webpack命令必须进入node_modules/.bin/webpack才能执行webpack命令，.bin目录包含的是一系列可以执行的命令，但是如果你是全局安装的webpack-cli，就不需要进入bin目录，webpack就能够寻找到它的命令路径了。

- 局部安装webpack（后续才需要）
  - --save-dev`是开发时依赖，项目打包后不需要继续使用的

- 为什么全局安装后，还需要局部安装呢？
  - 在终端直接执行webpack命令，使用的全局安装的webpack
  - 当在package.json中定义了scripts时，其中包含了webpack命令，那么使用的是局部webpack
  
    

### 5.2 webpack的起步



创建如下文件和文件夹：
文件和文件夹解析：

- dist文件夹：用于存放之后打包的文件

- src文件夹：用于存放我们写的源文件

- main.js：项目的入口文件。具体内容查看下面详情。

- mathUtils.js：定义了一些数学工具函数，可以在其他地方引用，并且使用。具体内容查看下面的详情。

- index.html：浏览器打开展示的首页html

- package.json：通过npm init生成的，npm包管理的文件（暂时没有用上，后面才会用上）

- mathUtils.js文件中的代码：

  ```js
  function add(num1,num2) {
      return num1 + num2
  }
  
  function mul(num1,num2) {
      return num1 * num2
  }
  
  //CommonJS 模块化规范
  module.exports = {
      add,
      mul
  }
  ```

- main.js文件中的代码：

  ```js
  //导入变量
  const {add,mul} = require('./mathUtils.js')
  
  console.log(add(20, 30));
  console.log(mul(20, 30));
  ```

现在的js文件中使用了模块化的方式进行开发，他们可以直接使用吗？不可以。因为如果直接在index.html引入这两个js文件，浏览器并不识别其中的模块化代码。另外，在真实项目中当有许多这样的js文件时，我们一个个引用非常麻烦，并且后期非常不方便对它们进行管理。
使用webpack工具，对多个js文件进行打包。
webpack就是一个模块化的打包工具，所以它支持我们代码中写模块化，可以对模块化的代码进行处理。
另外，如果在处理完所有模块之间的关系后，将多个js打包到一个js文件中，引入时就变得非常方便了。
命令如下

```
D:\web-program\webpack>cd demo01

//webpack-cil版本4.0以上的，第二个文件路径前面要加一个关键字-o，表示创建文件
// 4.x版本的使用这个命令：
//启动webpack的时候定义环境

D:\web-program\webpack\demo01>webpack ./src/main.js -o ./dist/bundle.js --mode development(此命令会在dist目录下创建一个bundle.js，然后生成main.js文件)

D:\web-program\webpack\demo01>webpack ./src/main.js -o ./dist --mode development

```

- info.js代码

```js
//使用es6 模块化规范
export const name = 'why';
export const age = 21;
export const height = 1.88;
```

- main.js修改后代码

```js
//1.使用CommonJS 模块化规范
const {add,mul} = require('./js/mathUtils.js')

console.log(add(20, 30));
console.log(mul(20, 30));
//2.使用es6 模块化规范
import {name,age,height} from "./js/info";

console.log(name);
console.log(age);
console.log(height);


```

- 再使用webpack重新编译打包

#### 5.2.1入口和出口

- 每次使用webpack的命令都需要写上入口和出口作为参数，就非常麻烦，这时候就有一种方法可以将这两个参数写到配置中，在运行时，直接读取。就是创建一个webpack.config.js文件

```js
const path = require('path')

module.exports = {
    //入口：可以是字符串/数组/对象，这里我们只有一个，所以写一个字符串即可
    entry:'./src/main.js',
    //出口：通常是一个对象，里面只是包括两个重要属性，path 和 filename
    output:{
        //path:绝对路径 可以动态获取路径 node语法
        path:path.resolve(__dirname,'dist'),
        filename:'bundle.js'
    },
    // 设置mode
    mode: 'development'
}
```

- npm init 命令npm初始化

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs017.png)

- 自动生成一个packge.json文件
- 使用命令npm install 安装上面文件的所有依赖
- 使用webpack命令编译



package.json中定义启动

- package.json中的scripts的脚本在执行时，会按照一定的顺序寻找命令对应的位置。

  ```json
  {
    "name": "meetwebpack",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build": "webpack"
    },
    "author": "",
    "license": "ISC"
  }
  
  //"build": "webpack" 为手动添加 在使用npm run build命令后映射之后使用webpack的快捷方式
  ```

  - 首先，会寻找本地的node_modules/.bin路径中对应的命令。
  - 如果没有找到，会去全局的环境变量中寻找。
  - 执行build指令`npm run build`(优先局部webpack)

局部安装webpack(在项目内部安装webpack)

目前，我们使用的webpack是全局的webpack，如果我们想使用局部来打包呢？
因为一个项目往往依赖特定的webpack版本，全局的版本可能很这个项目的webpack版本不一致，导出打包出现问题。所以通常一个项目，都有自己局部的webpack。

- 第一步，项目中需要安装自己局部的webpack这里我们让局部安装webpack3.6.0。Vue CLI3中已经升级到webpack4，但是它将配置文件隐藏了起来，所以查看起来不是很方便。 
- 第二步，通过node_modules/.bin/webpack启动webpack打包

```
npm install webpack@3.6.0 -save-dev
node_modules\.bin\webpack --mode development
```



### 5.3 webpack的loader

#### 5.3.1 css-loader/style-loader

loader是webpack中一个非常核心的概念。
在我们之前的实例中，我们主要是用webpack来处理我们写的js代码，并且webpack会自动处理js之间相关的依赖。
但是，在开发中我们不仅仅有基本的js代码处理，我们也需要加载css、图片，也包括一些高级的将ES6转成ES5代码，将TypeScript转成ES5代码，将scss、less转成css，将.jsx、.vue文件转成js文件等等。
对于webpack本身的能力来说，对于这些转化是不支持的。
但是webpack扩展对应的loader就可以啦。
loader使用过程：
步骤一：通过npm安装需要使用的loader
步骤二：在webpack.config.js中的modules关键字下进行配置
大部分loader我们都可以在webpack的官网中找到，并且学习对应的用法。

安装文档：https://webpack.docschina.org/loaders/css-loader/

- 使用<font color=red>npm install --save-dev css-loader ,  npm install --save-dev style-loader</font>命令安装css和style loader

  ```
  npm install --save-dev css-loader
  npm install --save-dev style-loader
  ```

- 在webpack.config.js文件中添加

```js
const path = require('path')

module.exports = {
    //入口：可以是字符串/数组/对象，这里我们只有一个，所以写一个字符串即可
    entry:'./src/main.js',
    //出口：通常是一个对象，里面只是包括两个重要属性，path 和 filename
    output:{
        //path:绝对路径 可以动态获取路径 node语法
        path:path.resolve(__dirname,'dist'),
        filename:'bundle.js'
    },
    // 设置mode
    mode: 'development',
    //配置css-loader文件
    module: {
        rules: [
            {
                test: /\.css$/i,
                use: ["style-loader", "css-loader"],
                //"style-loader" 只负责加载将css文件加载
                //"css-loader" 解析css文件
                // css-loader只负责将css文件进行加载
                // style-loader负责将样式添加到DOM中
                // 使用多个loader时, 是从右向左
            },
        ],
    },
}
```

- 在main.js项目中引入normal.css文件

  ```js
  main.js
  //1.使用CommonJS 模块化规范
  const {add,mul} = require('./js/mathUtils.js')
  
  console.log(add(20, 30));
  console.log(mul(20, 30));
  //2.使用es6 模块化规范
  import {name,age,height} from "./js/info";
  
  console.log(name);
  console.log(age);
  console.log(height);
  
  //3.依赖css文件
  require('./css/normal.css')
  ```

  ```css
  normal.css
  body{
      background-color: pink;
  }
  ```

- 执行npm run build命令打包



#### 5.3.2 less-loader/less

如果在项目中使用less、scss、stylus来写样式，webpack也可以帮助我们处理
这里以less为例，其他也是一样的。

安装文档：https://webpack.docschina.org/loaders/less-loader/

- 先创建一个less文件，依然放在css文件夹中

  ```less
  special.less
  @fontSize:50px;
  @fontColor:red;
  
  body{
    font-size: @fontSize;
    color: @fontColor;
  }
  ```

- 需要先安装 `less` 和 `less-loader`，让webpack会使用less对less文件进行编译

  ```
   npm install less less-loader --save-dev
  ```

- 修改对应的配置文件,添加一个rules选项，用于处理.less文件

  ```js
  const path = require('path')
  
  module.exports = {
      //入口：可以是字符串/数组/对象，这里我们只有一个，所以写一个字符串即可
      entry:'./src/main.js',
      //出口：通常是一个对象，里面只是包括两个重要属性，path 和 filename
      output:{
          //path:绝对路径 可以动态获取路径 node语法
          path:path.resolve(__dirname,'dist'),
          filename:'bundle.js'
      },
      // 设置mode
      mode: 'development',
      //配置css-loader文件
      module: {
          rules: [
              {
                  test: /\.css$/i,
                  use: ["style-loader", "css-loader"],
                  //"style-loader" 只负责加载将css文件加载
                  //"css-loader" 解析css文件
                  // css-loader只负责将css文件进行加载
                  // style-loader负责将样式添加到DOM中
                  // 使用多个loader时, 是从右向左
              },
              {
                  test: /\.less$/,
                  use: [{
                      loader: "style-loader", // creates style nodes from JS strings
                  }, {
                      loader: "css-loader" // translates CSS into CommonJS
                  }, {
                      loader: "less-loader", // compiles Less to CSS
                  }]
              },//less版本太高可能使用与官方文档的module代码报错
          ],
      },
  
  }
  ```

- 执行npm run build命令打包



#### 5.3.3 url-loader/file-loader

图片文件处理

官网文档：https://webpack.docschina.org/loaders/url-loader/

**v5 后弃用**：请考虑使用 [`asset modules`](https://webpack.docschina.org/guides/asset-modules/) 代替。

用于将文件转换为 base64 URI 的 loader。

- 首先，在项目中加入两张图片。一张较小的图片test01.jpg(小于8kb)，一张较大的图片test02.jpeg(大于8kb)
  待会儿我们会针对这两张图片进行不同的处理。

- 安装 `url-loader`：

  ```
  npm install url-loader --save-dev
  ```

- 配置webpack.config.js文件(webpack5之前的方法具体参考：https://blog.csdn.net/rlrw_t/article/details/117992694)

  我们发现webpack自动帮助我们生成一个非常长的名字这是一个32位hash值，目的是防止名字重复。但是，真实开发中，我们可能对打包的图片名字有一定的要求比如，将所有的图片放在一个文件夹中，跟上图片原来的名称，同时也要防止重复。所以，我们可以在options中添加上如下选项：
  img：文件要打包到的文件夹
  name：获取图片原来的名字，放在该位置
  hash:8：为了防止图片名称冲突，依然使用hash，但是我们只保留8位
  ext：使用图片原来的扩展名
  但是，我们发现图片并没有显示出来，这是因为图片使用的路径不正确
  默认情况下，webpack会将生成的路径直接返回给使用者
  但是，我们整个程序是打包在dist文件夹下的，所以这里我们需要在路径下再添加一个dist/

  ```js
    module.exports = {
    entry: './src/main.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'bundle.js',
      //webpack 提供一个非常有用的配置，该配置能帮助你为项目中的所有资源指定一个基础路径，它被称为公共路径(publicPath)。webpack5不需要
      publicPath: 'dist/'
    },
    module: {
      rules: [         
            {
                  test: /\.(png|jpg|gif|jpeg)$/,
                  use: [
                      {
                          loader: 'url-loader',
                          options: {
                              // 当加载的图片, 小于limit时, 会将图片编译成base64字符串形式.
                              // 当加载的图片, 大于limit时, 需要使用file-loader模块进行加载.
                              limit: 13000,
                              name: 'img/[name].[hash:8].[ext]',
                          },
                      }
                  ]
              },
          ]
    }
  ```

- 执行npm run build命令打包



#### 5.3.4 babel-loader

ES6语法并没有转成ES5，那么就意味着可能一些对ES6还不支持的浏览器没有办法很好的运行我们的代码。
在前面我们说过，如果希望将ES6的语法转成ES5，那么就需要使用babel。
而在webpack中，我们直接使用babel对应的loader就可以了。

官方文档：https://webpack.docschina.org/loaders/babel-loader/

- 安装babel-loadder

  ```
  npm install -D babel-loader @babel/core @babel/preset-env webpack
  ```

- 配置webpack.config.js文件

  ```js
    {
        test: /\.m?js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
            plugins: ['@babel/plugin-proposal-object-rest-spread']
          }
        }
      }
  ```

- 执行npm run build命令打包



### 5.4 webpack中配置Vue



后续项目中，我们会使用Vuejs进行开发，而且会以特殊的文件来组织vue的组件。
所以，下面我们来学习一下如何在我们的webpack环境中集成Vuejs
现在，我们希望在项目中使用Vuejs，那么必然需要对其有依赖，所以需要先进行安装
注：因为我们后续是在实际项目中也会使用vue的，所以并不是开发时依赖.

- 安装vue

  ```
  npm  install vue --save
  ```

- 接下来就可以按照我们之前学习的方式来使用Vue了

  ```html
  //5.使用vue进行开发
  //模块化导入
  import Vue from 'vue'
  
  const vm = new Vue({
      el:'#app',
      data:{
          message:'hello webpack!',
      },
      methods:{
  
      }
  })
  
  index.html中引用数据
  <div id="app">
      <h2>{{message}}</h2>
  </div>
  
  ```

- 修改完成后，重新打包，运行程序：
  打包过程没有任何错误(因为只是多打包了一个vue的js文件而已)
  但是运行程序，没有出现想要的效果，而且浏览器中有报错

  runtime-only -> 代码中, 不可以有任何的template

  runtime-compiler -> 代码中,可以有template, 因为有compiler可以用于编译template

  ![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs018.png)

  ```js
  //使用的是runtime-only版本的Vue
  //在webpack.config.js配置
  resolve: {
          // alias: 别名
          //extensions指定了from后可导入的文件类型。
          extensions: ['.js', '.css', '.vue'],
          alias: {
              'vue$': 'vue/dist/vue.esm.js'
          }
      }
  ```

- index.html中引入main.js必须在body标签内才能被引用

正常运行之后，我们来考虑另外一个问题：
如果希望将data中的数据显示在界面中，就必须是修改index.html
如果我们后面自定义了组件，也必须修改index.html来使用组件
但是html模板在之后的开发中，我并不希望手动的来频繁修改，是否可以做到呢？
定义template属性：
在前面的Vue实例中，我们定义了el属性，用于和index.html中的#app进行绑定，让Vue实例之后可以管理它其中的内容
这里，我们可以将div元素中的{{message}}内容删掉，只保留一个基本的id为div的元素
但是如果我依然希望在其中显示{{message}}的内容，应该怎么处理呢？
我们可以再定义一个template属性，代码如下：

```js
//5.使用vue进行开发
//模块化导入

import Vue from 'vue'

const vm = new Vue({
    el:'#app',
    template:
    `
    <div>
        <h2>{{aaa}}</h2>
        <button @click="btnClick">按钮</button>
        <h2>{{name}}</h2>
    </div>
    `
    ,
    data:{
        aaa:'hello webpack!',
        name:'幻想',
    },
    methods:{
        btnClick(){
            alert('hello');
        }
    }
})

```

重新打包，运行程序，显示一样的结果和HTML代码结构
那么，el和template模板的关系是什么呢？
在我们之前的学习中，我们知道el用于指定Vue要管理的DOM，可以帮助解析其中的指令、事件监听等等。
而如果Vue实例中同时指定了template，那么template模板的内容会替换掉挂载的对应el的模板。
这样做有什么好处呢？
这样做之后我们就不需要在以后的开发中再次操作index.html，只需要在template中写入对应的标签即可
但是，书写template模块非常麻烦怎么办呢？
没有关系，稍后我们会将template模板中的内容进行抽离。
会分成三部分书写：template、script、style，结构变得非常清晰

<b>Vue组件化开发引入</b>

在学习组件化开发的时候，我说过以后的Vue开发过程中，我们都会采用组件化开发的思想。
那么，在当前项目中，如果我也想采用组件化的形式进行开发，应该怎么做呢？
查看下面的代码：	
当然，我们也可以将下面的代码抽取到一个js文件中，并且导出。

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs019.png)

```js
//5.使用vue进行开发
//模块化导入

import Vue from 'vue'
const App = {
    template :   `
    <div>
        <h2>{{aaa}}</h2>
        <button @click="btnClick">按钮</button>
        <h2>{{name}}</h2>
    </div>
    `,
    data(){
        return{
            aaa:'hello webpack!',
            name:'幻想',
        }
    },
    methods:{
        btnClick(){
            alert('hello');
        }
    }
}

const vm = new Vue({
    el:'#app',
    template:'<App/>',
    data:{
    },
    components:{
        App
    }
})

```

进而我们可以把子组件模块化放在另一个js中，然后在main.js中引用

```js
app.js
export default {
        template :   `
        <div>
            <h2>{{aaa}}</h2>
            <button @click="btnClick">按钮</button>
            <h2>{{name}}</h2>
        </div>
        `,
        data(){
            return{
                aaa:'hello webpack!',
                name:'幻想',
            }
        },
        methods:{
            btnClick(){
                alert('hello');
            }
        }
}

main.js
import Vue from 'vue'
import App from './vue/app'

const vm = new Vue({
    el:'#app',
    template:'<App/>',
    data:{
    },
    components:{
        App
    }
})
```

但是一个组件以一个js对象的形式进行组织和使用的时候是非常不方便的
一方面编写template模块非常的麻烦
另外一方面如果有样式的话，我们写在哪里比较合适呢？
现在，我们以一种全新的方式来组织一个vue的组件
但是，这个时候这个文件可以被正确的加载吗？
必然不可以，这种特殊的文件以及特殊的格式，必须有人帮助我们处理。
谁来处理呢？vue-loader以及vue-template-compiler。

- 把组件放到vue文件中，再到main.js文件中引入

  ```js
  <template>
      <div>
          <h2 class="title">{{message}}</h2>
          <button @click="btnClick">按钮</button>
          <h2>{{name}}</h2>
          <Cpn/>
      </div>
  </template>
  
  <script>
  
      export default {
          name: "App",
          data() {
              return {
                  message: 'Hello Webpack',
                  name: 'coderwhy'
              }
          },
          methods: {
              btnClick() {
  
              }
          }
      }
  </script>
  
  <style scoped>
      .title {
          color: green;
      }
  </style>
  
  //main.js
  import App from './vue/App'
  ```

  

- 配置vue-loader以及vue-template-compiler。

```
npm install vue-loader vue-template-compiler --save-dev
```

- 配置webpack.config.js文件

```js
           {
                test:/\.vue$/,
                use:['vue-loader']
            }
```





### 5.5 webpack的plugin

plugin是指插件，通常是用于对某个现有的架构进行扩展。
webpack中的插件，就是对webpack现有功能的各种扩展，比如打包优化，文件压缩等等。
loader和plugin区别
loader主要用于转换某些类型的模块，它是一个转换器。
plugin是插件，它是对webpack本身的扩展，是一个扩展器。
plugin的使用过程：
步骤一：通过npm安装需要使用的plugins(某些webpack已经内置的插件不需要安装)
步骤二：在webpack.config.js中的plugins中配置插件。



#### 5.5.1 添加版权的Plugin

使用一个最简单的插件，为打包的文件添加版权声明
该插件名字叫BannerPlugin，属于webpack自带的插件。
按照下面的方式来修改webpack.config.js的文件：

```js
//webpack.config.js
//属于webpack自带的插件
const webpack = require('webpack')
module.exports = {
    plugins: [
        new webpack.BannerPlugin('最终版权归...')
    ],
   }
```

重新打包程序：查看bundle.js文件的头部

```
/*! 最终版权归... */
```

#### 5.5.2 打包html的plugin

目前，我们的index.html文件是存放在项目的根目录下的。
我们知道，在真实发布项目时，发布的是dist文件夹中的内容，但是dist文件夹中如果没有index.html文件，那么打包的js等文件也就没有意义了。
所以，我们需要将index.html文件打包到dist文件夹中，这个时候就可以使用HtmlWebpackPlugin插件
HtmlWebpackPlugin插件可以为我们做这些事情：
自动生成一个index.html文件(可以指定模板来生成)
将打包的js文件，自动通过script标签插入到body中
安装HtmlWebpackPlugin插件

```
npm install html-webpack-plugin --save-dev
```

使用插件，修改webpack.config.js文件中plugins部分的内容如下：

```js
plugins: [
        new webpack.BannerPlugin('最终版权归...'),
        new htmlWebpackPlugin({
            template:'index.html'
        }),
    ],
```

这里的template表示根据什么模板来生成index.html,另外，<font color=red>需要删除之前在output中添加的publicPath属性</font>
否则插入的script标签中的src可能会有问题.

#### 5.5.3 js压缩的Plugin

在项目发布之前，我们必然需要对js等文件进行压缩处理
这里，我们就对打包的js文件进行压缩

```
npm install uglifyjs-webpack-plugin@1.1.1 --save-dev
```

我们使用一个第三方的插件uglifyjs-webpack-plugin，并且版本号指定1.1.1，和CLI2保持一致

修改webpack.config.js文件，使用插件：

```
plugins:[
      new uglifyJsPlugin()
]
```

npm run buid 重新打包

查看打包后的bunlde.js文件，是已经被压缩过了。



### 5.6 搭建本地服务器

webpack提供了一个可选的本地开发服务器，这个本地服务器基于node.js搭建，内部使用express框架，可以实现我们想要的让浏览器自动刷新显示我们修改后的结果。
不过它是一个单独的模块，在webpack中使用之前需要先安装它

```
npm install --save-dev webpack-dev-server
```

devserver也是作为webpack中的一个选项，选项本身可以设置如下属性：
contentBase：为哪一个文件夹提供本地服务，默认是根文件夹，我们这里要填写./dist
port：端口号
inline：页面实时刷新
historyApiFallback：在SPA页面中，依赖HTML5的history模式
webpack.config.js文件配置修改如下：

```js
devServer:{
      contentBase:'.dist',
      inline:true
    },
```

我们可以再配置另外一个scripts：
--open参数表示直接打开浏览器

```
在package.json中添加
"dev": "webpack-dev-server"
"dev":"webpack-dev-server --open"
然后使用指令
npm run dev

```



## 第六章  Vue 周边库



### 6.1 Vue CLI 初始化脚手架

#### 6.1.1 说明

1. Vue 脚手架是 Vue 官方提供的标准化开发工具（开发平台）。

2. 最新的版本是 4.x。

3. 文档: https://cli.vuejs.org/zh/。

   

#### 6.1.2 具体步骤

第一步（仅第一次执行）：全局安装@vue/cli。

> ```bash
> npm install -g @vue/cli
> # OR
> yarn global add @vue/cli
> ```

第二步：<font color=red>切换到你要创建项目的目录</font>，然后使用命令创建项目

> ```bash
> vue create xxxx
> ```

第三步：启动项目(进入创建的项目的目录)

> ```bash
> npm run serve
> ```

  App running at:
  - Local:   http://localhost:8080/
  - Network: http://192.168.1.106:8080/

备注

1.设置淘宝镜像下载下载数度快
npm config set registry http://registry.npm.taobao.org 

2.Vue 脚手架隐藏了所有 webpack 相关的配置，若想查看具体的 webpakc 配置，

请执行：vue inspect > output.js

(自动生成output.js文件用来配置 参考:https://cli.vuejs.org/zh/)



#### 6.1.3 模板项目的结构



EditorConfig和Prettier一样，都是用来配置格式化你的代码的，这个格式化代码，要和你lint配置相符！否则会出现你格式化代码以后，却不能通过你的代码校验工具的检验

EditorConfig 文件中的设置用于在基本代码库中维持一致的编码风格和设置，例如缩进样式、选项卡宽度、行尾字符以及编码等，而无需考虑使用的编辑器vscode使用editorconfig插件以及.editorconfig配置文件说明详解
或 IDE

editorConfig不是什么软件，而是一个名称为.editorconfig的自定义文件。该文件用来定义项目的编码规范，编辑器的行为会与.editorconfig 文件中定义的一致，并且其优先级比编辑器自身的设置要高，这在多人合作开发项目时十分有用而且必要

有些编辑器默认支持editorConfig，如webstorm；而有些编辑器则需要安装editorConfig插件，如ATOM、Sublime、VS Code等

当打开一个文件时，EditorConfig插件会在打开文件的目录和其每一级父目录查找.editorconfig文件，直到有一个配置文件root=true

EditorConfig的配置文件是从上往下读取的并且最近的EditorConfig配置文件会被最先读取. 匹配EditorConfig配置文件中的配置项会按照读取顺序被应用, 所以最近的配置文件中的配置项拥有优先权

如果.editorconfig文件没有进行某些配置，则使用编辑器默认的设置

解读博客：https://www.jb51.net/article/185751.htm

**配置.editorconfig**

在当前项目根目录下添加.editorconfig文件

editorconfig文件是定义一些格式化规则（此规则并不会被vscode直接解析）

```
#表示是最顶层的配置文件，发现设为true时，才会停止查找.editorconfig文件
root = true
 
# Unix-style newlines with a newline ending every file 对于所有的文件 始终在文件末尾插入一个新行
[*]
end_of_line = crlf
insert_final_newline = true
 
# 对于所有的js文件，设置文件字符集为utf-8
[*.js]
charset = utf-8
 
# 设置所有JS,vue的缩进为
[*.{js,vue}]
 
indent_style = tab
```





```html
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <!-- 针对IE浏览器的一个特殊配置，含义是让IE浏览器以最高的渲染级别渲染页面 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- 开启移动端理想视口 -->
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <!-- 配置页签图标 -->
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <!-- 配置网页标题 -->
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
    <!-- 当浏览器不支持js时noscript中的元素会被渲染 -->
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <!-- 容器 -->
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
      
      

```



```js
/* 该文件是整个项目的入口文件 */
// 引入vue
import Vue from 'vue'
// 引入App组件，是所有组件的父组件
import App from './App.vue'
// 关闭vue的生产提示
Vue.config.productionTip = false

/* 
	关于不同版本的Vue：
	
		1.vue.js与vue.runtime.xxx.js的区别：
				(1).vue.js是完整版的Vue，包含：核心功能+模板解析器。
				(2).vue.runtime.xxx.js是运行版的Vue，只包含：核心功能；没有模板解析器。

		2.因为vue.runtime.xxx.js没有模板解析器，所以不能使用template配置项，需要使用
			render函数接收到的createElement函数去指定具体内容。
*/

new Vue({
  // 将App组件放入容器中
  render: h => h(App),
  // render:q=> q('h1','你好啊')
}).$mount('#app')


```



脚手架文件结构

> ├── node_modules 
> ├── public
> │   ├── favicon.ico: 页签图标
> │   └── index.html: 主页面
> ├── src
> │   ├── assets: 存放静态资源
> │   │   └── logo.png
> │   │── component: 存放组件
> │   │   └── HelloWorld.vue
> │   │── App.vue: 汇总所有组件
> │   │── main.js: 入口文件
> ├── .gitignore: git版本管制忽略的配置
> ├── babel.config.js: babel的配置文件
> ├── package.json: 应用包配置文件 
> ├── README.md: 应用描述文件
> ├── package-lock.json：包版本控制文件



关于不同版本的Vue

1. vue.js与vue.runtime.xxx.js的区别：
   1. vue.js是完整版的Vue，包含：核心功能 + 模板解析器。
   2. vue.runtime.xxx.js是运行版的Vue，只包含：核心功能；没有模板解析器。
2. 因为vue.runtime.xxx.js没有模板解析器，所以不能使用template这个配置项，需要使用render函数接收到的createElement函数去指定具体内容。



vue.config.js配置文件

1. 使用vue inspect > output.js可以查看到Vue脚手架的默认配置。
2. 使用vue.config.js可以对脚手架进行个性化定制，详情见：https://cli.vuejs.org/zh

```
vue.config.js
module.exports = {
  pages: {
    index: {
      //入口
      entry: 'src/main.js',
    },
  },
	lintOnSave:false, //关闭语法检查
	//开启代理服务器（方式一）
	/* devServer: {
    proxy: 'http://localhost:5000'
  }, */
	//开启代理服务器（方式二）
	devServer: {
    proxy: {
      '/atguigu': {
        target: 'http://localhost:5000',
				pathRewrite:{'^/atguigu':''},
        // ws: true, //用于支持websocket
        // changeOrigin: true //用于控制请求头中的host值
      },
      '/demo': {
        target: 'http://localhost:5001',
				pathRewrite:{'^/demo':''},
        // ws: true, //用于支持websocket
        // changeOrigin: true //用于控制请求头中的host值
      }
    }
  }
}
```



### 6.2 ref 与props



ref

- 作用：用于给节点打标识
- 读取方式：this.$refs.xxxxx



1. 被用来给元素或子组件注册引用信息（id的替代者）
2. 应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）
3. 使用方式：
   1. 打标识：```<h1 ref="xxx">.....</h1>``` 或 ```<School ref="xxx"></School>```
   2. 获取：```this.$refs.xxx```

```vue
<template>
  <div>
      <h1 v-text="msg" ref="title"></h1>
      <button ref="btn" @click="showDom">点我获取上方DOM元素</button>
      <School ref="sch"/>
  </div>
</template>

<script>
//引入school组件
import School from './components/School.vue'

export default {
    name:'App',
    components: {School},
    data () {
        return {
            msg:'欢迎学习Vue！'
        }
    },
    methods: {
        showDom(){
            console.log(this.$refs.title)//真实DOM元素
            console.log(this.$refs.btn//真实DOM元素
            console.log(this.$refs.sch)//School组件的实例对象（vc）
        }
    }
}
</script>
```



props



- 作用：用于父组件给子组件传递数据

- 读取方式一: 只指定名称

  - props: ['name', 'age', 'setName']

- 读取方式二: 指定名称和类型

  - props: {

    ​             name: String, 

    ​             age: Number, 

    ​             setNmae: Function

    }

- 读取方式三: 指定名称/类型/必要性/默认值

  - props: {

    ​             name: {type: String, required: true, default:xxx

    ​            }

```vue
传递数据：<Demo name="xxx",sex="X",:age=""/>
接收数据
<script>
export default {
    name:'Student',
    data () {
        return {
             msg:'欢迎来到寒蝉',
            /* name:'龙宫礼奈',
            sex:'女',
            age:17 */ 
        }
    },
    // 简单声明接收
    // props: ['name','sex','age']

    // 接收的同时对数据进行类型限制
    /* props: {
        name:String,
        sex:String,
        age:Number
    } */

    // 接收的同时对数据进行类型限制+默认值的指定+必要性的限制
    props: {
        name:{
            type:String,//name的类型是字符串
            required:true,//name是必要的
        },
        sex:{
            type:String,
            required:true
        },
        age:{
            type:Number,
            default:99//默认值 
        }
    }
}
</script>
```



### 6.3 mixin 混入

Vue 插件是一个包含 install 方法的对象

通过 install 方法给 Vue 或 Vue 实例添加方法, 定义全局指令等

功能：可以把多个组件共用的配置提取成一个混入对象

使用方式：

- 第一步定义混合：

  ```js
  {
      data(){....},
      methods:{....}
      ....
  }
  ```

- 第二步使用混入：

  - 全局混入：```Vue.mixin(xxx)```

    ```js
    //hunhe.js
    export const hunhe = {
        methods: {
            showName(){
                alert(this.name);
            }
        },
    }
    
    
    //main.js
    // 引入Vue
    import Vue from "vue"
    // 引入App
    import App from "./App.vue"
    //引入mixin
    import {hunhe} from "./mixin"
    // 关闭Vue生产提示
    Vue.config.productionTip = false
    
    //全局混入
    Vue.mixin(hunhe)
    
    // 创建vm
    new Vue({
        el:"#app",
        data:{},
        methods: {},
        render: h => h(App)
    })
    ```

    

  - 局部混入：```mixins:['xxx']	```

    ```vue
    //Student.vue
    <template>
      <div class="demo">
          <h1>{{msg}}</h1>
          <h2 @click="showName">学生名称：{{name}}</h2>
          <h2>学生性别：{{sex}}</h2>
      </div>
    </template>
    
    <script>
    import {hunhe} from '../mixin' 
    
    export default {
        name:'Student',
        data () {
            return {
                msg:'欢迎来到寒蝉',
                name:'龙宫礼奈',
                sex:'女'
            }
        },
        //局部混入
        // mixins: [hunhe]
        
    }
    </script>
    
    <style>
    .demo{
        background-color: pink;
    }
    </style>
    
    ```



### 6.4 插件

1. 功能：用于增强Vue

2. 本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据。

3. 定义插件：

   ```js
   对象.install = function (Vue, options) {
       // 1. 添加全局过滤器
       Vue.filter(....)
   
       // 2. 添加全局指令
       Vue.directive(....)
   
       // 3. 配置全局混入(合)
       Vue.mixin(....)
   
       // 4. 添加实例方法
       Vue.prototype.$myMethod = function () {...}
       Vue.prototype.$myProperty = xxxx
   }
   ```

4. 使用插件：```Vue.use()```

### 6.5 scope样式

作用：让样式在局部生效，防止冲突。

写法：```<style scoped>```

```vue
<style lang="css" scoped>
/* 
lang : 语言 如css less... 
scoped : 当style标签具有该scoped属性时，其CSS将仅应用于当前组件的元素
    除css语言其他语言都要安装编译器  譬如 npm i less-loader@7
*/
.demo{
    background-color: orange;
}
</style>>
```



<b>Todo-list案例</b>

组件化编码流程（通用）

- 实现静态组件：抽取组件，使用组件实现静态页面效果

- 展示动态数据：
  - 数据的类型、名称是什么？
  - 数据保存在哪个组件？

- 交互——从绑定事件监听开始

  

1. 组件化编码流程：

   ​	(1).拆分静态组件：组件要按照功能点拆分，命名不要与html元素冲突。

   ​	(2).实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：

   ​			1).一个组件在用：放在组件自身即可。

   ​			2). 一些组件在用：放在他们共同的父组件上（<span style="color:red">状态提升</span>）。

   ​	(3).实现交互：从绑定事件开始。

2. props适用于：

   ​	(1).父组件 ==> 子组件 通信

   ​	(2).子组件 ==> 父组件 通信（要求父先给子一个函数）

3. 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的！

4. props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做。

```vue
App.vue
<template>
  <div>
    <div id="root">
        <div class="todo-container">
            <div class="todo-wrap">
            <!-- 把函数传入MyHeader子组件中再把数据传入父组件 -->
            <MyHeader :addTodo="addTodo"/>
            <!-- 把MyHeader数据传入MyList子组件 -->
            <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
            <MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
            </div>
        </div>
    </div>
</div>
</template>

<script>
	import MyHeader from './components/MyHeader'
	import MyList from './components/MyList'
	import MyFooter from './components/MyFooter.vue'

export default {
    name:'App',
    components: {MyFooter,MyHeader,MyList},
    //由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
    data () {
      return {
        todos:[
          {id:'001',title:'吃饭',done:true},
          {id:'002',title:'睡觉',done:true},
          {id:'003',title:'打豆豆',done:false}
        ]
      }
    },
    methods: {
      //添加一个todo
      addTodo(todoObj){
        //unshift() 方法将把它的参数插入 arrayObject 的头部
        this.todos.unshift(todoObj)
      },
      //勾选or取消一个todo
      checkTodo(id){
        this.todos.forEach((todo)=>{
          if(todo.id === id) todo.done = !todo.done
        })
      },
      //删除一个todo
			deleteTodo(id){
				this.todos = this.todos.filter( todo => todo.id !== id )
			},
      //全选or取消全选
      checkAllTodo(done){
				this.todos.forEach((todo)=>{
					todo.done = done
				})
			},
      //清除所有已经完成的todo
			clearAllTodo(){
				this.todos = this.todos.filter((todo)=>{
					return !todo.done
				})
			}
    }
}
</script>

<style >
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

</style>
```

```js
main.js
// 引入Vue
import Vue from "vue"
// 引入App
import App from "./App.vue"
// 关闭Vue生产提示
Vue.config.productionTip = false

// 创建vm
new Vue({
    el:"#app",
    data:{},
    methods: {},
    render: h => h(App)
})
```

```vue
MyFooter.vue
<template>
	<div class="todo-footer" v-show="total">
		<label>
			<!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
			<input type="checkbox" v-model="isAll"/>
		</label>
		<span>
			<span>已完成{{doneTotal}}</span> / 全部{{total}}
		</span>
		<button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
	</div>
</template>

<script>
	export default {
		name:'MyFooter',
		props:['todos','checkAllTodo','clearAllTodo'],
		computed: {
			//总数
			total(){
				return this.todos.length
			},
			//已完成数
			doneTotal(){
				//此处使用reduce方法做条件统计
				/* const x = this.todos.reduce((pre,current)=>{
					console.log('@',pre,current)
					return pre + (current.done ? 1 : 0)
				},0) */
				//简写
				return this.todos.reduce((pre,todo)=> pre + (todo.done ? 1 : 0) ,0)
			},
			//控制全选框
			isAll:{
				//全选框是否勾选
				get(){
					return this.doneTotal === this.total && this.total > 0
				},
				//isAll被修改时set被调用
				set(value){
					this.checkAllTodo(value)
				}
			}
		},
		methods: {
			/* checkAll(e){
				this.checkAllTodo(e.target.checked)
			} */
			//清空所有已完成
			clearAll(){
				this.clearAllTodo()
			}
		},
	}
</script>

<style scoped>
	/*footer*/
	.todo-footer {
		height: 40px;
		line-height: 40px;
		padding-left: 6px;
		margin-top: 5px;
	}

	.todo-footer label {
		display: inline-block;
		margin-right: 20px;
		cursor: pointer;
	}

	.todo-footer label input {
		position: relative;
		top: -1px;
		vertical-align: middle;
		margin-right: 5px;
	}

	.todo-footer button {
		float: right;
		margin-top: 5px;
	}
</style>
```

```vue
MyHeader.vue
<template>
  <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
  </div>
</template>

<script>
//导入nanoid 安装nanoid 唯一ID生成器  npm i nanoid
import {nanoid} from 'nanoid'

export default {
    name:'MyHeader',
    data () {
      return {
        title:''  
      }
    },
    methods: {
      //e
      add(){
      // 校验数据
      if(!this.title.trim()) return alert ('输入不能为空')
      //将用户的输入包装成一个todo对象
      // const todoObj = {id:nanoid(),title:e.target.value,done:false}
      const todoObj = {id:nanoid(),title:this.title,done:false}
      //把todo对象传入父组件的函数,父组件获得对象再传入给MyList对象
      this.addTodo(todoObj)
      //清空输入
      // e.target.value = ""
      this.title = ''
      // console.log(todoObj)
      }
    },
    //接收从App传递过来的addTodo
		props:['addTodo'],
    
}
</script>

<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
```

```vue
MyItem.vue
<template>
	<li>
		<label>
			<input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
			<!-- 如下代码也能实现功能，但是不太推荐，因为有点违反原则，因为修改了props -->
			<!-- <input type="checkbox" v-model="todo.done"/> -->
			<span>{{todo.title}}</span>
		</label>
		<button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
	</li>
</template>

<script>
	export default {
		name:'MyItem',
		//声明接收todo、checkTodo、deleteTodo
		props:['todo','checkTodo','deleteTodo'],
		methods: {
			//勾选or取消勾选
			handleCheck(id){
				//通知App组件将对应的todo对象的done值取反
				this.checkTodo(id)
			},
			//删除
			handleDelete(id){
        // confirm()方法用于显示一个带有指定消息和确认及取消按钮的对话框。如果访问者点击"确定"，此方法返回true，否则返回false。
				if(confirm('确定删除吗？')){
          //通知App组件将对应的todo对象删除
					this.deleteTodo(id)
        }
			}
		},
	}
</script>

<style scoped>
	/*item*/
	li {
		list-style: none;
		height: 36px;
		line-height: 36px;
		padding: 0 5px;
		border-bottom: 1px solid #ddd;
	}

	li label {
		float: left;
		cursor: pointer;
	}

	li label li input {
		vertical-align: middle;
		margin-right: 6px;
		position: relative;
		top: -1px;
	}

	li button {
		float: right;
		display: none;
		margin-top: 3px;
	}

	li:before {
		content: initial;
	}

	li:last-child {
		border-bottom: none;
	}

	li:hover{
		background-color: #ddd;
	}
	
	li:hover button{
		display: block;
	}
</style>
```

```vue
MyList.vue
<template>
  <ul class="todo-main">
        <!-- 遍历数组数据 -->
        <MyItem v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
    </ul>
</template>

<script scoped>
import MyItem from './MyItem.vue'

export default {
    name:'MyList',
    components: {MyItem},

    //声明接收App传递过来的数据，其中todos是自己用的，checkTodo和deleteTodo是给子组件MyItem用的
    props: ['todos','checkTodo','deleteTodo'],
    
}
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
```









### 6.6 





###  路由



- 一个路由就是一组映射关系（key - value）

- key 为路径, value 可能是 function 或 component



路由分类

- 后端路由：

  - 理解：value 是 function, 用于处理客户端提交的请求。

  - 工作过程：服务器接收到一个请求时, 根据请求路径找到匹配的函数来处理请求, 返回响应数据。

- 前端路由：
  - 理解：value 是 component，用于展示页面内容。
  - 工作过程：当浏览器的路径改变时, 对应的组件就会显示。



## 第七章 





## 第八章 Axios



### 8.1 HTTP 相关



MDN 文档
https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Overview

1.	前后应用从浏览器端向服务器发送HTTP 请求(请求报文)
2.	后台服务器接收到请求后, 调度服务器应用处理请求, 向浏览器端返回HTTP响应(响应报文)
3.	浏览器端接收到响应, 解析显示响应体/调用监视回调

HTTP 请求报文

1. 请求行:
   method url
   GET /product_detail?id=2 
   POST /login

2.	多个请求头
Host: www.baidu.com
Cookie: BAIDUID=AD3B0FA706E; BIDUPSID=AD3B0FA706;
Content-Type: application/x-www-form-urlencoded 或者 application/json
3.	请求体
username=tom&pwd=123
{"username": "tom", "pwd": 123}



HTTP 响应报文

1.	响应状态行: status statusText
2.	多个响应头
Content-Type: text/html;charset=utf-8 Set-Cookie: BD_CK_SAM=1;path=/
3.	响应体
html 文本/json 文本/js/css/图片...



post 请求体参数格式

4.	Content-Type: application/x-www-form-urlencoded;charset=utf-8用于键值对参数，参数的键值用=连接, 参数之间用&连接例如: name=%E5%B0%8F%E6%98%8E&age=12
5.	Content-Type: application/json;charset=utf-8
用于json 字符串参数
例如: {"name": "%E5%B0%8F%E6%98%8E", "age": 12}
6.	Content-Type: multipart/form-data
   用于文件上传请求



常见的响应状态码

200   ok                                   请求成功。一般用于GET 与POST 请求

201   Created                         已创建。成功请求并创建了新的资源

401   Unauthorized               未授权/请求要求用户的身份认证

404   Not Found                    服务器无法根据客户端的请求找到资源

500   Internal Server Error  服务器内部错误，无法完成请求



不同类型的请求及其作用

1.	GET: 从服务器端读取数据
2.	POST: 向服务器端添加新数据
3.	PUT: 更新服务器端已经数据
4.	DELETE: 删除服务器端数据



API 的分类

1. REST API: restful

   (1)	发送请求进行CRUD 哪个操作由请求方式来决定
   (2)	同一个请求路径可以进行多个操作
   (3)	请求方式会用到GET/POST/PUT/DELETE

2. 非REST API: restless
   (1)	请求方式不决定请求的CRUD 操作
   (2)	一个请求路径只对应一个操作
   (3)    一般只有GET/POST





### 8.2 Vue中发送网络请求方式



选择一: 传统的Ajax是基于XMLHttpRequest(XHR)

缺点
非常好解释, 配置和调用方式等非常混乱.
编码起来看起来就非常蛋疼.
所以真实开发中很少直接使用, 而是使用jQuery-Ajax

选择二: 使用jQuery-Ajax

相对于传统的Ajax非常好用.
缺点
首先,  在Vue的整个开发中都是不需要使用jQuery了.
那么, 就意味着为了方便我们进行一个网络请求, 特意引用一个jQuery, 不合理
jQuery的代码1w+行.
Vue的代码才1w+行.
完全没有必要为了用网络请求就引用这个重量级的框架.

选择三: 官方在Vue1.x的时候, 推出了Vue-resource.

Vue-resource的体积相对于jQuery小很多.
另外Vue-resource是官方推出的.
缺点
在Vue2.0退出后, Vue作者就在GitHub的Issues中说明了去掉vue-resource, 并且以后也不会再更新.
那么意味着以后vue-reource不再支持新的版本时, 也不会再继续更新和维护.
对以后的项目开发和维护都存在很大的隐患.

选择四: 在说明不再继续更新和维护vue-resource的同时, 作者还推荐了一个框架: axios
axios有非常多的优点, 并且用起来也非常方便.

### 8.3 使用json-server 搭建REST API



json-server 用来快速搭建REST API 的工具包

使用json-server

1.	在线文档: https://github.com/typicode/json-server
2.	全局下载: npm install -g json-server
3.	目标根目录下创建数据库json 文件: db.json

> ```js
> {
>     "posts": [
>       {
>         "id": 1,
>         "title": "json-server",
>         "author": "typicode"
>       },
>       {
>         "id": 2,
>         "title": "json-server2",
>         "author": "typicode2"
>       }
>     ],
>     "comments": [
>       {
>         "id": 1,
>         "body": "some comment",
>         "postId": 1
>       }
>     ],
>     "profile": {
>       "name": "typicode"
>     }
>   }
> //posts 文章 comments  评论 profile  个人 可以通过s判断多与单的关系
> ```

4. 启动服务器执行命令: json-server --watch db.json(下面是创建成功的语句提示)

   ```
   PS D:\web-program\ceshi\restful> json-server --watch db.json
   
     \{^_^}/ hi!
   
     Loading db.json
     Done
   
     Resources
     http://localhost:3000/posts
     http://localhost:3000/comments
     http://localhost:3000/profile
   
     Home
     http://localhost:3000
   ```

   通过get restful方式查询id为1的文章http://localhost:3000/posts/1 返回的是json格式的对象

   通过 get 非restful方式查询id为1的文章http://localhost:3000/posts?id=1 返回的是数组

   

使用axios 访问 restful 测试

必须在实用json-server启动服务器情况下测试

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <button onclick="testGet()">Get请求</button>
    <button onclick="testPost()">Post请求</button>
    <button onclick="testPut()">Put请求</button>
    <button onclick="testDelete()">Delete请求</button>
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.20.0/axios.min.js"></script>
    <script>
        //使用get请求
        //获取http://localhost:3000/posts接口的信息
        function testGet(){
            axios.get(
                // 'http://localhost:3000/posts'     Array [ {…}, {…} ] 
                // 'http://localhost:3000/posts/1'   Object { id: 1, title: "json-server", author: "typicode" }
                'http://localhost:3000/posts?id=1'   //Array [ {…} ]
                ).then(response => {
                console.log('/posts get',response.data)
            })
        }
        //使用post请求
        function testPost(){
            axios.post(
                'http://localhost:3000/posts' ,{"title": "json-server3",  "author": "typicode3"} //添加数据 Object { title: "json-server3", author: "typicode3", id: 3 }
                ).then(response => {
                console.log('/posts post',response.data)
            })
        }
        //使用put请求
        function testPut(){
            axios.put(
                'http://localhost:3000/posts/3' ,{"title": "json-server2333",  "author": "typicode2333"} //修改数据 Object { title: "json-server2333", author: "typicode2333", id: 3 }
                ).then(response => {
                console.log('/posts post',response.data)
            })
        }
        //使用delete请求
        function testDelete(){
            axios.delete(
                'http://localhost:3000/posts/2'  //删除数据 Object {  }返回对象为空
                ).then(response => {
                console.log('/posts post',response.data)
            })
        }
    </script>
</body>
</html>
```



### 8.4 XHR 的理解和使用

MDN 文档：https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest

1.	使用XMLHttpRequest (XHR)对象可以与服务器交互, 也就是发送ajax 请求
2.	前端可以获取到数据，而无需让整个的页面刷新。
3.	这使得Web 页面可以只更新页面的局部，而不影响用户的操作。

区别一般http 请求与ajax 请求

1.	ajax 请求是一种特别的http 请求
2.	对服务器端来说, 没有任何区别, 区别在浏览器端
3.	浏览器端发请求: 只有 XHR 或 fetch 发出的才是 ajax 请求, 其它所有的都是非ajax 请求
4.	浏览器端接收到响应
(1)	一般请求: 浏览器一般会直接显示响应体数据, 也就是我们常说的刷新/跳转页面
(2)	ajax 请求: 浏览器不会对界面进行任何更新操作, 只是调用监视的回调函数并传入响应相关数据



API

1. XMLHttpRequest(): 创建XHR 对象的构造函数

2. status: 响应状态码值, 比如200, 404

3. statusText: 响应状态文本

4. readyState: 标识请求状态的只读属性
   0 : 初始

   1 : open()之后
   2 : send()之后
   3 : 请求中
   4 : 请求完成

5. onreadystatechange: 绑定readyState 改变的监听

6. responseType: 指定响应数据类型, 如果是'json', 得到响应后自动解析响应体数据

7. response: 响应体数据, 类型取决于responseType 的指定

8. timeout: 指定请求超时时间, 默认为0 代表没有限制

9. ontimeout: 绑定超时的监听

10. onerror: 绑定请求网络错误的监听

11. open(): 初始化一个请求, 参数为: (method, url[, async])

12. send(data): 发送请求

13. abort(): 中断请求

14. getResponseHeader(name): 获取指定名称的响应头值

15. getAllResponseHeaders(): 获取所有响应头组成的字符串

16. setRequestHeader(name, value): 设置请求头



XHR 的ajax 封装(简单版axios)

- 函数的返回值为promise, 成功的结果为response, 异常的结果为error

- 能处理多种类型的请求: GET/POST/PUT/DELETE

- 函数的参数为一个配置对象
  {
  url: '', // 请求地址
  method: '', // 请求方式GET/POST/PUT/DELETE
  params: {}, // GET/DELETE 请求的query 参数
  data: {}, // POST 或DELETE 请求的请求体参数
  }

- 响应json 数据自动解析为js

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>使用XHR封装ajax请求参数</title>
</head>
<body>
  <button onclick="testGet()">发送GET请求</button><br>
  <button onclick="testPost()">发送POST请求</button><br>
  <button onclick="testPut()">发送PUT请求</button><br>
  <button onclick="testDelete()">发送Delete请求</button><br>


  <script>

    /* 1. GET请求: 从服务器端获取数据*/
    function testGet() {
      axios({
        // url: 'http://localhost:3000/posts',
        url: 'http://localhost:3000/posts2',
        method: 'GET',
        params: {
          id: 1,
          xxx: 'abc'
        }
      }).then(
        response => {
          console.log(response)
        },
        error => {
          alert(error.message)
        }
      )
    }

    /* 2. POST请求: 服务器端保存数据*/
    function testPost() {
      axios({
        url: 'http://localhost:3000/posts',
        method: 'POST',
        data: {
          "title": "json-server---", 
          "author": "typicode---"
        }
      }).then(
        response => {
          console.log(response)
        },
        error => {
          alert(error.message)
        }
      )
    }

    /* 3. PUT请求: 服务器端更新数据*/
    function testPut() {
      axios({
        url: 'http://localhost:3000/posts/1',
        method: 'put',
        data: {
          "title": "json-server+++", 
          "author": "typicode+++"
        }
      }).then(
        response => {
          console.log(response)
        },
        error => {
          alert(error.message)
        }
      )
    }

    /* 2. DELETE请求: 服务器端删除数据*/
    function testDelete() {
      axios({
        url: 'http://localhost:3000/posts/2',
        method: 'delete'
      }).then(
        response => {
          console.log(response)
        },
        error => {
          alert(error.message)
        }
      )
    }

    /* 
    1.函数的返回值为promise, 成功的结果为response, 失败的结果为error
    2.能处理多种类型的请求: GET/POST/PUT/DELETE
    3.函数的参数为一个配置对象
      {
        url: '',   // 请求地址
        method: '',   // 请求方式GET/POST/PUT/DELETE
        params: {},  // GET/DELETE请求的query参数
        data: {}, // POST或DELETE请求的请求体参数 
      }
    4.响应json数据自动解析为js的对象/数组
    */
    function axios({
      url,
      method='GET',
      params={},
      data={}
    }) {
      // 返回一个promise对象
      return new Promise((resolve, reject) => {

        // 处理method(转大写)
        method = method.toUpperCase()

        // 处理query参数(拼接到url上)   id=1&xxx=abc
        /* 
        {
          id: 1,
          xxx: 'abc'
        }
        */
        let queryString = ''
        Object.keys(params).forEach(key => {
          queryString += `${key}=${params[key]}&`
        })
        if (queryString) { // id=1&xxx=abc&
          // 去除最后的&
          queryString = queryString.substring(0, queryString.length-1)
          // 接到url
          url += '?' + queryString
        }


        // 1. 执行异步ajax请求
        // 创建xhr对象
        const request = new XMLHttpRequest()
        // 打开连接(初始化请求, 没有请求)
        request.open(method, url, true)

        // 发送请求
        if (method==='GET' || method==='DELETE') {
          request.send()
        } else if (method==='POST' || method==='PUT'){
          request.setRequestHeader('Content-Type', 'application/json;charset=utf-8') // 告诉服务器请求体的格式是json
          request.send(JSON.stringify(data)) // 发送json格式请求体参数
        }

        // 绑定状态改变的监听
        request.onreadystatechange = function () {
          // 如果请求没有完成, 直接结束
          if (request.readyState!==4) {
            return
          }
          // 如果响应状态码在[200, 300)之间代表成功, 否则失败
          const {status, statusText} = request
          // 2.1. 如果请求成功了, 调用resolve()
          if (status>=200 && status<=299) {
            // 准备结果数据对象response
            const response = {
              data: JSON.parse(request.response),
              status,
              statusText
            }
            resolve(response)
          } else { // 2.2. 如果请求失败了, 调用reject()
            reject(new Error('request error status is ' + status))
          }
        }
      })
    }
  </script>
</body>
</html>
```



### 8.5 axios 的理解和使用

axios 是什么?

1.	前端最流行的ajax 请求库
2.	react/vue 官方都推荐使用axios 发ajax 请求
3.	文档: http://www.axios-js.com/zh-cn/docs/



axios 特点

- 基本promise 的异步ajax 请求库

- 浏览器端/node 端都可以使用

- 支持请求／响应拦截器

- 支持请求取消

- 请求/响应数据转换

- 批量发送多个请求



axios 常用语法

> axios(config): 通用/最本质的发任意类型请求的方式
> axios(url[, config]): 可以只指定url 发get 请求
> axios.request(config): 等同于axios(config)
> axios.get(url[, config]): 发get 请求
> axios.delete(url[, config]): 发delete 请求
> axios.post(url[, data, config]): 发post 请求
> axios.put(url[, data, config]): 发put 请求
>
> axios.defaults.xxx: 请求的默认全局配置
> axios.interceptors.request.use(): 添加请求拦截器
> axios.interceptors.response.use(): 添加响应拦截器
>
> axios.create([config]): 创建一个新的axios(它没有下面的功能)
>
> axios.Cancel(): 用于创建取消请求的错误对象
> axios.CancelToken(): 用于创建取消请求的token 对象
> axios.isCancel(): 是否是一个取消请求的错误
> axios.all(promises): 用于批量执行多个异步请求
> axios.spread(): 用来指定接收所有成功数据的回调函数的方法



axios.create(config)

1. 根据指定配置创建一个新的axios, 也就就每个新axios 都有自己的配置

2. 新axios 只是没有取消请求和批量发请求的方法, 其它所有语法都是一致的

3. 为什么要设计这个语法?
   (1)	需求: 项目中有部分接口需要的配置与另一部分接口需要的配置不太一样, 如何处理
   (2)	解决: 创建 2 个新 axios, 每个都有自己特有的配置, 分别应用到不同要求的接口请求中

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <meta http-equiv="X-UA-Compatible" content="ie=edge">
     <title>axios.create()</title>
   </head>
   <body>
     <!-- 
     1). axios.create(config)
       a. 根据指定配置创建一个新的axios, 也就就每个新axios都有自己的配置
       b. 新axios只是没有取消请求和批量发请求的方法, 其它所有语法都是一致的
       c. 为什么要设计这个语法?
         需求: 项目中有部分接口需要的配置与另一部分接口需要的配置不太一样, 如何处理
         解决: 创建2个新axios, 每个都有自己特有的配置, 分别应用到不同要求的接口请求中
     -->
     <script src="https://cdn.bootcss.com/axios/0.19.0/axios.js"></script>
     <script>
       axios.defaults.baseURL = 'http://localhost:3000'
   
       // 使用axios发请求
       axios({
         url: '/posts' // 请求3000
       })
   
       // axios({
       //   url: '/xxx' // 请求4000
       // })
   
       const instance = axios.create({
         baseURL: 'http://localhost:4000'
       })
   
       // 使用instance发请求
       // instance({
       //   url: '/xxx'  // 请求4000
       // })
       instance.get('/xxx')
     </script>
   </body>
   </html>
   ```

   



拦截器函数/ajax 请求/请求的回调函数的调用顺序

1.	说明: 调用axios()并不是立即发送ajax 请求, 而是需要经历一个较长的流程
2.	流程: 请求拦截器2 => 请求拦截器1 => 发ajax 请求 => 响应拦截器1 => 响应拦截器2 => 请求的回调
3.	注意: 此流程是通过 promise 串连起来的, 请求拦截器传递的是 config, 响应拦截器传递的是response

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title></title>
  <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.20.0/axios.min.js"></script>
</head>
<body>
    <!--  
    requestInterceptors: [{fulfilled1(){}, rejected1(){}}, {fulfilled2(){}, rejected2(){}}]
    responseInterceptors: [{fulfilled11(){}, rejected11(){}}, {fulfilled22(){}, rejected22(){}}]
    chain: [
      fulfilled2, rejected2, fulfilled1, rejected1, 
      dispatchReqeust, undefined, 
      fulfilled11, rejected11, fulfilled22, rejected22
    
    ]
    promise链回调: config 
                  => (fulfilled2, rejected2) => (fulfilled1, rejected1)   // 请求拦截器处理
                  => (dispatchReqeust, undefined) // 发请求
                  => (fulfilled11, rejected11) => (fulfilled22, rejected22) // 响应拦截器处理
                  => (onResolved, onRejected) // axios发请求回调处理
    -->


  <script>
    //添加请求拦截器
    axios.interceptors.request.use(
        config => {
            console.log('request interceptor1 onResolved')
            //必须返回cinfig
            return config
        },
        error  => {
            console.log('request interceptor1 onRejected')
            return Promise.reject(error);
        }
    )
    axios.interceptors.request.use(
        config => {
            console.log('request interceptor2 onResolved')
            return config
        },
        error  => {
            console.log('request interceptor2 onRejected')
            return Promise.reject(error);
        }
    )
    //添加响应拦截器
    axios.interceptors.response.use(
      response => {
        console.log('response interceptor1 onResolved()')
        return response
      },
      function (error) {
        console.log('response interceptor1 onRejected()')
        return Promise.reject(error);
      }
    )
    axios.interceptors.response.use(
      response => {
        console.log('response interceptor2 onResolved()')
        return response
      },
      function (error) {
        console.log('response interceptor2 onRejected()')
        return Promise.reject(error);
      }
    )

    axios.get('http://localhost:3000/posts')
    .then(response => {
        console.log('data',response.data)
    })
    .catch(error =>{
        console.log('error',error.message)
    })
    axios.get('http://localhost:3000/posts2')
    .then(response => {
        console.log('data',response.data)
    })
    .catch(error =>{
        console.log('error',error.message)
    })
  </script>
</body>
</html>
```





取消请求

1.	基本流程
配置cancelToken 对象
缓存用于取消请求的cancel 函数
在后面特定时机调用cancel 函数取消请求
在错误回调中判断如果error 是cancel, 做相应处理
2.	实现功能
   点击按钮, 取消某个正在请求中的请求
   在请求一个接口前, 取消前面一个未完成的请求









- 安装axios依赖

> ```bash
> npm install axios
> ```

- 发送get请求演示

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs022.png)



### 发送并发请求

有时候, 我们可能需求同时发送两个请求
使用axios.all, 可以放入多个请求的数组.
axios.all([]) 返回的结果是一个数组，使用 axios.spread 可将数组 [res1,res2] 展开为 res1, res2

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs023.png)



### 全局配置

在上面的示例中, 我们的BaseURL是固定的
事实上, 在开发中可能很多参数都是固定的.
这个时候我们可以进行一些抽取, 也可以利用axiox的全局配置

> axios.defaults.baseURL = ‘123.207.32.32:8000’
> axios.defaults.headers.post[‘Content-Type’] = ‘application/x-www-form-urlencoded’;

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs024.png)





### 常见的配置选项

> 请求地址
> url: '/user',
>
> 请求类型
> method: 'get',
>
> 请根路径
> baseURL: 'http://www.mt.com/api',
>
> 请求前的数据处理
> transformRequest:[function(data){}],
>
> 请求后的数据处理
> transformResponse: [function(data){}],
>
> 自定义的请求头
> headers:{'x-Requested-With':'XMLHttpRequest'},
>
> URL查询对象
> params:{ id: 12 },

> 查询对象序列化函数
> paramsSerializer: function(params){ }
> request body
> data: { key: 'aa'},
>
> 超时设置s
> timeout: 1000,
>
> 跨域是否带Token
> withCredentials: false,
>
> 自定义请求处理
> adapter: function(resolve, reject, config){},
>
> 身份验证信息
> auth: { uname: '', pwd: '12'},
>
> 响应的数据格式 json / blob /document /arraybuffer / text / stream
> responseType: 'json',
>
> 

### axios的实例

从axios模块中导入对象时, 使用的实例是默认的实例.当给该实例设置一些默认配置时, 这些配置就被固定下来了.但是后续开发中, 某些配置可能会不太一样.比如某些请求需要使用特定的baseURL或者timeout或者content-Type等.这个时候, 我们就可以创建新的实例, 并且传入属于该实例的配置信息.

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs025.png)

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs026.png)

```vue 
<template>
  <h2>{{categories}}</h2>
</template>

<script>
  import axios from 'axios'
  // import android from 'android'

  export default {
    name: "HelloWorld",
    data() {
      return {
        categories: ''
      }
    },
    created() {
      axios({
        url: 'http://123.207.32.32:8000/category'
      }).then(res => {
        this.categories = res;
      })
      // android.ios({
      //
      // })
    }
  }
</script>

<style scoped>

</style>

```

### axios封装

![ ](https://gitee.com/yybovo/note-images/raw/master/Typora/vuejs027.png)

```js
import axios from 'axios'

export function request(config) {
  // 1.创建axios的实例
  const instance = axios.create({
    baseURL: 'http://123.207.32.32:8000',
    timeout: 5000
  })

  // 2.axios的拦截器
  // 2.1.请求拦截的作用
  instance.interceptors.request.use(config => {
    // console.log(config);
    // 1.比如config中的一些信息不符合服务器的要求

    // 2.比如每次发送网络请求时, 都希望在界面中显示一个请求的图标

    // 3.某些网络请求(比如登录(token)), 必须携带一些特殊的信息
    return config
  }, err => {
    // console.log(err);
  })

  // 2.2.响应拦截
  instance.interceptors.response.use(res => {
    // console.log(res);
    return res.data
  }, err => {
    console.log(err);
  })

  // 3.发送真正的网络请求
  return instance(config)
}

// export function request(config) {
//   return new Promise((resolve, reject) => {
//     // 1.创建axios的实例
//     const instance = axios.create({
//       baseURL: 'http://123.207.32.32:8000',
//       timeout: 5000
//     })
//
//     // 发送真正的网络请求
//     instance(config)
//       .then(res => {
//         resolve(res)
//       })
//       .catch(err => {
//         reject(err)
//       })
//   })
// }

// export function request(config) {
//   // 1.创建axios的实例
//   const instance = axios.create({
//     baseURL: 'http://123.207.32.32:8000',
//     timeout: 5000
//   })
//
//   // 发送真正的网络请求
//   instance(config.baseConfig)
//     .then(res => {
//       // console.log(res);
//       config.success(res);
//     })
//     .catch(err => {
//       // console.log(err);
//       config.failure(err)
//     })
// }

// export function request(config, success, failure) {
//   // 1.创建axios的实例
//   const instance = axios.create({
//     baseURL: 'http://123.207.32.32:8000',
//     timeout: 5000
//   })
//
//   // 发送真正的网络请求
//   instance(config)
//     .then(res => {
//       // console.log(res);
//       success(res);
//     })
//     .catch(err => {
//       // console.log(err);
//       failure(err)
//     })
// }

// function test(aaa, bbb) {
//   // aaa('Hello World')
//   bbb('err message')
// }
//
// test(function (res) {
//   console.log(res);
// }, function (err) {
//   console.log(err);
// })

main.js
import Vue from 'vue'
import App from './App'

import axios from 'axios'

Vue.config.productionTip = false

new Vue({
  el: '#app',
  render: h => h(App)
})



// const obj = {
//   name: 'kobe',
//   age: 30
// }
//
// const {name, age} = obj;
//
// const names = ['why', 'kobe', 'james']
// // const name1 = names[0]
// // const name2 = names[1]
// // const name3 = names[2]
// const [name1, name2, name3] = names;


// 1.axios的基本使用
// axios({
//   url: 'http://123.207.32.32:8000/home/multidata',
//   // method: 'post'
// }).then(res => {
//   console.log(res);
// })
//
// axios({
//   url: 'http://123.207.32.32:8000/home/data',
//   // 专门针对get请求的参数拼接
//   params: {
//     type: 'pop',
//     page: 1
//   }
// }).then(res => {
//   console.log(res);
// })


// 2.axios发送并发请求
// axios.all([axios({
//   url: 'http://123.207.32.32:8000/home/multidata'
// }), axios({
//   url: 'http://123.207.32.32:8000/home/data',
//   params: {
//     type: 'sell',
//     page: 5
//   }
// })]).then(results => {
//   console.log(results);
//   console.log(results[0]);
//   console.log(results[1]);
// })

// 3.使用全局的axios和对应的配置在进行网络请求
// axios.defaults.baseURL = 'http://123.207.32.32:8000'
// axios.defaults.timeout = 5000
//
// axios.all([axios({
//   url: '/home/multidata'
// }), axios({
//   url: '/home/data',
//   params: {
//     type: 'sell',
//     page: 5
//   }
// })]).then(axios.spread((res1, res2) => {
//   console.log(res1);
//   console.log(res2);
// }))
//
//
// // axios.defaults.baseURL = 'http://222.111.33.33:8000'
// // axios.defaults.timeout = 10000
//
// axios({
//   url: 'http://123.207.32.32:8000/category'
// })


// 4.创建对应的axios的实例
// const instance1 = axios.create({
//   baseURL: 'http://123.207.32.32:8000',
//   timeout: 5000
// })
//
// instance1({
//   url: '/home/multidata'
// }).then(res => {
//   console.log(res);
// })
//
// instance1({
//   url: '/home/data',
//   params: {
//     type: 'pop',
//     page: 1
//   }
// }).then(res => {
//   console.log(res);
// })
//
//
// const instance2 = axios.create({
//   baseURL: 'http://222.111.33.33:8000',
//   timeout: 10000,
//   // headers: {}
// })


// 5.封装request模块
import {request} from "./network/request";


// request({
//   url: '/home/multidata'
// }, res => {
//   console.log(res);
// }, err => {
//   console.log(err);
// })

// request({
//   baseConfig: {
//
//   },
//   success: function (res) {
//
//   },
//   failure: function (err) {
//
//   }
// })

request({
  url: '/home/multidata'
}).then(res => {
  console.log(res);
}).catch(err => {
  // console.log(err);
})


```





## Vuejs 实战



### Vuejs 动画

在系统操作的过程中，用户体验有很多种，例如系统本身强大的功能体验，服务高效响应的体验，界面优化及视觉效果体验等等。其中视觉上的动画相关的体验，是带给用户最直观的体验。

系统页面中的动画，主要是用来以多元化的形式动态的展现信息。

![images](https://gitee.com/yybovo/note-images/raw/master/Typora/DAEC9F33FB0D4FFD859241047AC847F0) 

需求：点击按钮，展现信息，再次点击按钮，隐藏信息

测试 1：
我们第一次加入动画效果
对于 Vuejs 动画的引用
需要使用样式
.v-enter
.v-leave-to
.v-enter-active
.v-leave-active
测试 2：通过以上 4 组样式的设定，可以完成信息的动画展现
测试 3：我们先来完成简单的信息淡入淡出的效果以及滑入滑出的效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    <!-- 自定义两组Vuejs的样式，来控制transition内部的元素实现动画的效果 -->
    <style>
        /* 
          v-enter 这是一个时间点，是进入之前，元素的起始状态，此时还没有开始进入
          v-leave-to 这是一个时间点，是动画离开之后，离开的终止状态，此时，元素动画已经结束
        */
        .v-enter,.v-leave-to{
            /* 设置起始状态和结束状态元素的透明度为0(表示隐藏元素) */
            opacity: 0;
            /* 
              该形式为普通淡出淡入的动画效果，使用起来最简单，应用最广泛
            */
            /* transform: opacity; */
            /* 该形式为滑入效果 X表示X轴方位(横)，Y表示Y轴方位(竖) ，z表示z轴方位(切面) */
            transform: translateX(150px);
        }
        /*

            .v-enter-active 这是一个时间段，表示元素入场的过程
            .v-leave-active 这是一个时间段，表示元素离场的过程

        */
        .v-enter-active,.v-leave-active{
            /* 设置在指定的事件内完成动画的全部入场和离场效果 */
            transition: all 2.8s;
        }
    </style>
   
</head>
<body>
    <div id="app">
    
    <!-- 点击flag实现Boolean值的转换 -->
    <!-- 通过v-if判断boolea值实现显示和隐藏的转换 -->
       <input type="button" @click="flag=!flag" value="点击"/>
       <br>
       <br>
       <!--
            对于以下p标签中的信息，我们需要使用动画进行控制
            需要使用transition元素，将需要被动画控制的元素包裹起来，对于当前信息的展现，我们需要包裹的就是p标签
            transition元素，Vue官方为我们提供的元素切换时的过渡动画
        -->
        <transition>
            <p v-if="flag">helloworld</p>
        </transition>
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                flag : false
            },
            methods:{
            }

        });

    </script>

</body>
</html>
```

测试 4：实现弹入弹出的效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    <!-- 自定义两组Vuejs的样式，来控制transition内部的元素实现动画的效果 -->
    <style>
        .v-enter-active{
            /* 设置弹进时长 */
            animation: bounce-in .5s;
        }
        .v-leave-active{
            /* 
               设置弹入时长 
               正常的弹入弹出，都需要将reverse属性值加上
            */
            animation: bounce-in .5s reverse;
        }
        /*
            使用vue搭配css动画效果的实现
            @keyframes：是CSS3定义的动画规则
            bounce-in：表示弹入弹出的效果
            transform: scale 弹栋时缩放的大小定义
        */
        @keyframes bounce-in{
            0%{
                transform: scale(0);
            }
            50%{
                transform: scale(1.5);
            }
            100%{
                transform: scale(1);
            }
        }


    </style>
   
</head>
<body>
    <div id="app">
    
    <!-- 点击flag实现Boolean值的转换 -->
    <!-- 通过v-if判断boolea值实现显示和隐藏的转换 -->
       <input type="button" @click="flag=!flag" value="点击"/>
       <br>
       <br>
       <!--
            对于以下p标签中的信息，我们需要使用动画进行控制
            需要使用transition元素，将需要被动画控制的元素包裹起来，对于当前信息的展现，我们需要包裹的就是p标签
            transition元素，Vue官方为我们提供的元素切换时的过渡动画
        -->
        <transition>
            <p v-if="flag">helloworld!你好世界！helloworld!你好世界helloworld!你好世界helloworld!你好世界</p>
        </transition>
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                flag : false
            },
            methods:{
            }

        });

    </script>

</body>
</html>
```

测试 5    设置我们自己的 v-前缀可以有效的区分不同元素使用动画

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    <!-- 自定义两组Vuejs的样式，来控制transition内部的元素实现动画的效果 -->
    <style>
        .tran1-enter-active{
            /* 设置弹进时长 */
            animation: bounce-in 1.5s;
        }
        .tran1-leave-active{
            /* 
               设置弹入时长 
               正常的弹入弹出，都需要将reverse属性值加上
            */
            animation: bounce-in 1.5s reverse;
        }

        .tran2-enter-active{
            /* 设置弹进时长 */
            animation: bounce-in .5s;
        }
        .tran2-leave-active{
            /* 
               设置弹入时长 
               正常的弹入弹出，都需要将reverse属性值加上
            */
            animation: bounce-in .5s reverse;
        }
        /*
            使用vue搭配css动画效果的实现
            @keyframes：是CSS3定义的动画规则
            bounce-in：表示弹入弹出的效果
            transform: scale 弹栋时缩放的大小定义
        */
        @keyframes bounce-in{
            0%{
                transform: scale(0);
            }
            50%{
                transform: scale(1.5);
            }
            100%{
                transform: scale(1);
            }
        }


    </style>
   
</head>
<body>
    <div id="app">
    
    <!-- 点击flag实现Boolean值的转换 -->
    <!-- 通过v-if判断boolea值实现显示和隐藏的转换 -->
       <input type="button" @click="flag1=!flag1" value="点击"/>
       <br>
       <input type="button" @click="flag2=!flag2" value="点击"/>
       <br>
       <!--
            对于以下p标签中的信息，我们需要使用动画进行控制
            需要使用transition元素，将需要被动画控制的元素包裹起来，对于当前信息的展现，我们需要包裹的就是p标签
            transition元素，Vue官方为我们提供的元素切换时的过渡动画
        -->
        <transition name=tran1>
            <p v-if="flag1">
                helloworld!你好世界！helloworld!你好世界helloworld!你好世界helloworld!你好世界<br>
                helloworld!你好世界！helloworld!你好世界helloworld!你好世界helloworld!你好世界<br>
                helloworld!你好世界！helloworld!你好世界helloworld!你好世界helloworld!你好世界
            </p>
        </transition>
        <transition name=tran2>
            <p v-if="flag2">
                helloworld!你好世界！helloworld!你好世界helloworld!你好世界helloworld!你好世界<br>
                helloworld!你好世界！helloworld!你好世界helloworld!你好世界helloworld!你好世界<br>
                helloworld!你好世界！helloworld!你好世界helloworld!你好世界helloworld!你好世界
            </p>
        </transition>
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                flag1 : false,
                flag2 : false
            },
            methods:{
            }

        });

    </script>

</body>
</html>
```

测试6： 使用第三方样式类库实现动画效果，这样就不用我们自己处理动画效果了，直接引用即可。
使用动画的钩子函数完成特殊的动画效果（钩子函数：钩子函数是在一个事件触发的时候，在系统级捕获到了他，然后做一些操作。一段用以处理系统消息的程序。“钩子”就是在某个阶段给你一个做某些处理的机会。）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    <!-- 引入第三方样式类库 -->
    <link rel="stylesheet" href="./css/animate.css">
</head>
<body>
    <div id="app">
    
    <!-- 点击flag实现Boolean值的转换 -->
    <!-- 通过v-if判断boolea值实现显示和隐藏的转换 -->
       <input type="button" @click="flag=!flag" value="点击"/>
       <br>
       <br>
        <!-- 
            animate.css提供了
            enter-active-class和leave-active-class
            用来操作元素进场和离场的效果
            以弹出的形式处理进场和离场
            animated bounceIn
            animated bounceOut
         -->
        <!-- <transition enter-active-class="animated bounceIn" leave-active-class="animated bounceOut">
            <p v-if="flag">helloworld!你好世界!</p>
        </transition> -->

        <!--
            我们可以将class="animated"写在元素中
            这样在enter-active-class和leave-active-class中就不用重复写animated了

            使用:duration="毫秒值" 来统一设置入场和离场动画时长
        -->
        <!-- <transition enter-active-class="bounceIn" leave-active-class="bounceOut" :duration="6000">
            <p v-if="flag" class="animated">helloworld!你好世界!</p>
        </transition> -->

        <!-- 使用 :buration"{enter:200,leave:400}"来分别设置入场和离场的时长 -->
        <transition enter-active-class="bounceIn" leave-active-class="bounceOut" :duration="{enter:200,leave:400}">
            <p v-if="flag" class="animated"  >helloworld!你好世界!</p>
        </transition>
    </div>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                flag : false
            },
            methods:{
            }

        });

    </script>

</body>
</html>
```

测试 7：完成商品进入购物车的特效

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    <!-- 自定义两组Vuejs的样式，来控制transition内部的元素实现动画的效果 -->
    <!-- border-radius: 给div元素添加圆角的边框： -->
    <style>
        .ball{
            width: 15px;
            height: 15px;
            border-radius: 50%;
            background-color: red;
        }

    </style>
   
</head>
<body>
    <div id="app" style="height:170px">
    
       <input type="button" @click="flag=!flag" value="点击购物车"/>
       <br>
       <!-- 以下@定义的属性。一会使用动画的钩子函数进行相应处理 -->
       <transition
           @before-enter="beforeEnter"
           @enter="enter"
           @after-enter="afterEnter"
       >
           <div class="ball" v-show="flag"></div>
       </transition>

    </div>

    <img src="./image/gwc.png"/>
    
    <script>
        var vm = new Vue({

            el : "#app",    
            data : {
                flag : false
            },
            methods:{
                //注意：动画钩子函数也是具有参数的，一般都会有一个参数叫做el，这个el就是钩子函数的第一个参数
                //el表示的是要执行动画的那个DOM元素，是一个原生JS的DOM元素
                //大家也可以认为，el是通过document.getElementById('')的方式获取到的原生DOM对象
                beforeEnter(el){
                    //beforeEnter表示动画入场之前，此时，动画尚未开始，可以在beforeEnter中，设置元素开始动画之前的起始样式
                    //el.style.transform设置小球开始动画之前的起始位置
                    //translate(0,0)表示的是在坐标为0，0的位置
                    el.style.transform = "translate(0,0)"
                },
                enter(el,done){
                    //这行代码，没有实际的作用，但是如果不写，就不会出现动画的效果
                    //可以认为，el.offsetWidth会强制启动动画
                    el.offsetWidth

                    //enter表示动画开始之后的样式的设置，这里，可以设置小球完成动画之后的结束状态
                    //all 1s ease 为一秒钟完成所有过度效果
                    el.style.transform = "translate(150px,350px)"
                    el.style.transition = 'all 1s ease'

                    //这里的done，起始就是afterEnter这个函数，也就是说，done就是afterEnter函数的引用
                    done()
                },
                afterEnter(el){
                    //在动画完成之后，会调用afterEnter
                    this.flag =! this.flag
                }
            }

        });

    </script>

</body>
</html>
```

测试 8：在信息列表中动态操作信息显示

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src="./lib/vue-2.4.0.js"></script>
    <style>
        li{
            border: 1px dashed black;  /* 设置边框样式 */
            margin: 5px; /* 简写属性在一个声明中设置所有外边距属性。该属性可以有 1 到 4 个值。 */
            line-height: 50px; /* 属性设置行间的距离（行高）。 */
            padding-left: 8px; /* 属性设置元素左内边距 */
            font-size: 2s2px;
            width: 80%;

        }
        /* 鼠标事件 */
        li:hover{
            background-color: hotpink;
            transition: all 0.8s ease;
        }
        .v-enter,
        .v-leave-to{
            opacity: 0;
            transform: translateY(60px);
        }
        .v-enter-active,
        .v-leave-active{
            transition: all 0.6s ease;
        }

        /* 下面的.v-move和.v-leave-active需要配合使用，能够实现列表后续的元素，渐渐的飘上来的这种效果 */
        .v-move{
            transition: all 0.6s ease;
        }
        .v-leave-active{
            position: absolute;
        }
    </style>
</head>
<body>
    
    
    <div id="app" >
        <!-- <label>标签在HTML中的作用是定义input元素的标注。 -->
        <!--
            定义文本框及按钮
        -->
        <div>
        <label>
            Id:
            <input type="text" v-model="id"/>
        </label> 
        <label>
            Name:
            <input type="text" v-model="name"/>
        </label>
        <input type="button" value="添加" @click="add"/>
        </div>
        <!-- 定义动画区域 -->
        <!-- ul -->
        <!--
            在我们实现列表过渡的时候，如果需要过渡的元素，是通过v-for循环渲染出来的，
                则不能使用transition进行包裹，必须要使用transition-group来进行包裹
            如果要为v-for循环创建的元素设置动画，必须为每一个元素设置 :key属性（必须是当前记录的id）
            给transition添加appear属性 ，在页面刚展现出来的时候，实现入场时候的效果
            通过为transition-group元素，设置tag属性，指定transition-group渲染为指定的元素
                如果不指定tag属性，默认渲染为span元素
        -->
        <transition-group appear tag="ul">
            <li v-for="(item,i) in list" :key="item.id" @click="del(i)">
                {{item.id}} --- {{item.name}} 
            </li>
        </transition-group>
        <!-- ul -->
    </div>



    <script>
        
        var vm = new Vue({

            el : "#app",
            data : {
                id : "",
                name : "",
                list : [
                    {id:1,name:'zs'},
                    {id:2,name:'ls'},
                    {id:3,name:'ww'},
                    {id:4,name:'zl'},
                    {id:5,name:'sq'}
                ]

            },

            methods:{
                add(){
                    //为列表添加对象
                    this.list.push({id:this.id,name:this.name})
                    //将文本框中的数据清空掉
                    this.id = '';
                    this.name = '';
                },
                del(i){
                    this.list.splice(i,1);
                }

            }

        })

    </script>

</body>
</html>
```

案例9 书籍购物车案例

```
html部分
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--  引入css样式  -->
    <link rel="stylesheet" href="style.css">

</head>
<body>

<div id="app">
    <div v-if="books.length">
    <table>
        <thead>
        <tr>
            <td></td>
            <td>书籍名称</td>
            <td>出版日期</td>
            <td>价格</td>
            <td>购买数量</td>
            <td>操作</td>
        </tr>
        </thead>
        <tbody>
        <!--    循环集合对象    -->
        <tr v-for="(item,index) in books" :key="item.id">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.date}}</td>
            <td>{{item.price | showPrice}}</td>
            <td>
                <!--绑定事件 count的值不能为负数-->
                <button @click="decrement(index)" :disabled="item.count == 1">-</button>
                {{item.count}}
                <button @click="increment(index)">+</button>
            </td>
            <td><button @click="removeBtnClick(index)">移除</button></td>
        </tr>
        </tbody>
    </table>
    <div>总价: {{totalPrice | showPrice}}</div>
</div>
    <!--当购物车没有书籍是会根据v-else显示购物车为空-->
    <div v-else>购物车为空</div>
</div>
<!--  引入vue框架  -->
<script src="../lib/vue.js"></script>
<!--  引入js  -->
<script src="main.js"></script>
</body>

js部分
const app = new Vue({
    el: '#app',
    data: {
        books: [
            {
                id: 1,
                name: '《算法导论》',
                date: '2006-9',
                price: 85.00,
                count: 1
            },
            {
                id: 2,
                name: '《UNIX编程艺术》',
                date: '2006-2',
                price: 59.00,
                count: 1
            },
            {
                id: 3,
                name: '《编程珠玑》',
                date: '2008-10',
                price: 39.00,
                count: 1
            },
            {
                id: 4,
                name: '《代码大全》',
                date: '2006-3',
                price: 128.00,
                count: 1
            },
        ]
    },
    methods: {
        increment(index) {
            this.books[index].count++
        },
        decrement(index) {
            this.books[index].count--
        },
        removeBtnClick(index){
            this.books.splice(index,1)
        }
    },
    //过滤器
    filters: {
        showPrice(price){
            //toFixed() 方法可把 Number 四舍五入为指定小数位数的数字。
            return '￥'+price.toFixed(2)
        }
    },
    //计算属性来计算所有书的总价格
    computed: {
        totalPrice(){
            // 1.普通的for循环
      // let totalPrice = 0
      // for (let i = 0; i < this.books.length; i++) {
      //   totalPrice += this.books[i].price * this.books[i].count
      // }
      // return totalPrice

      // 2.for (let i in this.books)
      // let totalPrice = 0
      // for (let i in this.books) {
      //   const book = this.books[i]
      //   totalPrice += book.price * book.count
      // }
      //
      // return totalPrice

      // 3.for (let i of this.books)
      // let totalPrice = 0
      // for (let item of this.books) {
      //   totalPrice += item.price * item.count
      // }
      // return totalPrice

      return this.books.reduce(function (preValue, book) {
        return preValue + book.price * book.count
      }, 0)
    }
  }
})

css部分
 table{
     border: 1px solid #e9e9e9;
     border-collapse: collapse;
     border-spacing: 0;
 }
th,td{
    padding:8px 16px;
    border: 1px solid #e9e9e9;
    text-align: left;
}
th{
    background-color: #f7f7f7;
    color: #5c6b77;
}
```













## 附录

### ES6知识点



#### let/var

ES6 新增了`let`命令，用来声明局部变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效，而且有暂时性死区的约束

用var来声明变量，而且JS只有函数作用域和全局作用域，没有块级作用域，所以`{}`限定不了var声明变量的访问范围。

`let`，可以声明块级作用域的变量。

```html
{
  let i = 9; //i变量只在 花括号内有效！！！
}
console.log(i); 
```

`let`非常适合用于 `for`循环内部的块级作用域。JS中的for循环体比较特殊，每次执行都是一个全新的独立的块作用域，用let声明的变量传入到 for循环体的作用域后，不会发生改变，不受外界的影响。

let没有变量提升与暂时性死区
用`let`声明的变量，不存在变量提升。而且要求必须 等`let`声明语句执行完之后，变量才能使用，不然会报`Uncaught ReferenceError`错误。

let变量不能重复声明
let不允许在相同作用域内，重复声明同一个变量。否则报错：`Uncaught SyntaxError: Identifier 'XXX' has already been declared`



#### const的使用

const的作用就是将变量声明为一个常量，不能被修改，不可以再次赋值，它的指向是不可以改变的，只能指向某处固定区域，不能再指向其它地方

在ES6开发中，优先使用const，只有需要修改某个标识符值的时候采用let

1.声明后必须初始化赋值，如：const name='aaa'，不可以 const name;

2.常量的含义是指向的对象不能修改，但是可以修改对象中的属性

如：

const obj = {name:'aaa',age:18}

obj.name='bbb'



#### 对象字面量的增强写法（简写方法）

1.对象属性的增强写法

```html
//ES5写法
const name = "yuan";
const age = "21";
const sex = "man";
const obj = {
  name: name,
  age: age,
  sex: sex
}

//ES6写
const name = "yuan";
const age = "21";
const sex = "man";
const obj = {
  name,
  age,
  sex
}

```

2.对象方法的增强写法

```html
//ES5写法
const name = "yuan";
const obj = {
  getName: function(){
    console.log("my name is " + name);
  }
}
//ES6写法
const name = "yuan";
const obj = {
  getName(){
    console.log("my name is " + name);
  }
}

```



#### **``**的用法

es6中允许使用**``**创建字符串模块，可以直接写回车空格编写html或文本。
可代替**‘** **’**和**“** **”**的使用

```html
let html = `
<div>
	<p>hahaha</p>
</div>
`
```

在‘‘中可以使用{}直接把变量与字符串拼起来，无需使用加号

```html
let search = 1;

//es5中
let url="www.baidu.com?search="+search;

//es6中
let url=`www.baidu.com?search=${search}`;
```

 
