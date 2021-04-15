## JavaWeb 学习

### 1. Web 的概念概述

* #### JavaWeb: 

  	* 使用Java语言开发的互联网项目

* 软件的架构：

   1. C/S:  Client/Server  客户端/服务器端

        * 在用户本地有一个客户端程序，在远程有一个服务器端程序

        * 如; QQ, 迅雷：

        * 优点：

          ​	1. 用户体验好

        * 缺点：

          ​	1. 开发，安装，部署，维护麻烦

   2. B/S: Browser/Server  浏览器/服务器段

      * 只需要一个浏览器，用户通过不同的网址(URL), 客户访问不同的服务器端
      * 优点：
        1. 开发，安装，部署，维护 简单
      * 缺点：
        	1.  如果应用过大，用户体验受到影响
         	2.  对硬件要求过高

* #### B/S 架构详解

  * 资源分类：
     	1. 静态资源：
             	* 使用静态网页开发技术发布的资源
          * 特点：
            	* 所有用户访问，得到的结果是一样的
            	* 如 文本， 图片，音频，视频  HTML, CSS,  JavaScript
            	* 如果用户请求的是静态资源，那么服务器会直接将静态资源发送给浏览器。浏览器中内置了静态资源的解析引擎们可以解析静态资源
     	2.  动态资源：
          * 使用动态网页及时发布的资源
          * 特点：
             * 所有用户访问，得到的结果可能不一样
             * 如：jsp/servlet，php, asp...
             * 如果用户请求的是动态资源，服务器会执行动态资源，转换为静态资源，再发送给浏览器
  * 要学习动态资源，必须先学习静态资源
  * 静态资源：
    * HTML：用于搭建基础网页，展示页面内容
    * CSS：用于美化页面，布局页面
    * JavaScript：控制页面的元素，让页面有一些动态效果

### HTML

### 1. 概念：是最基础的网页开发语言

 *  Hyper Text Markup Language 超文本标记语言
     *  超文本：
        	*  超文本是用超链接的方法，将各种不同空间的文字信息组织在一起的网状文本
     *  标记语言：
        	*  由标签构成的语言。<标签名称> 如html，xml
        	*  标记语言不是编程语言

#### 2. 快速入门

  * 语法：

     1. html文档后缀名  .html  或者 .htm

     2. 标签分为

        	1. 围堵标签： 由开始标签和结束标签 如: <html> </html>
        	2. 自闭和标签：开始标签和结束标签在一起。如换行<br/>
	
       	3. 标签可以嵌套：

        ​	需要正确嵌套，不能你中有我，我中有你

        ​	错误：\<a>\<b>\</a>\</b>

        	4. 在开始标签中可以定义属性。属性是由键值对构成，值需要用引号（单双都可以）引起来
        	
        	5. html的标签不区分大小写，建议使用小写

```html
<html>

	<head>
		<title>title</title>
	</head>

	<body>
		<font color="red"> Hello World</font><br/>

		<font color="green"> Hello World</font>
	</body>
</html>
```

#### 3. 标签

 1. 文件标签： 构成html最基本的标签

    	* html: html文档的根标签
        	* head：头标签。用于指定html文档的一些属性，引入外部的资源
        	* title：标题标签
        	* body：体标签
        	* \<!DOCTYPE html>:  html5中定义该文档是html文档

 2. 文本标签：和文本有关的标签

    ​	* 注释：<!--注释内容 -->

     * \<h1> to \<h6>：标题标签
       	* h1~h6：字体大小逐渐递减
    	* \<p>：段落标签
    	* \<br>：换行标签
     * \<hr>：展示一条水平线
        * 属性：现在已经废弃不用
          	* color 颜色
          	* width：宽度
          	* size：高度
          	* align：对齐方式 ceter，left，right
    	* \<b>：字体加粗
    	* \<i>：斜体
     * \<font>：字体标签， html5已经废弃
       	* 属性：color：颜色，size：大小，face：字体
    * 属性定义：
      * color：
        	1. 英文单词： red， green， blue
         	2. rgb（值1，值2，值3）：值的范围：0~255 如 rgb(0，0，255)
         	3. #值1值2值3： 值的范围：00~FF之间。如#FF00FF
      * width：
        1. 数值： width = ‘20’，数值的单位，默认是 px(像素)
        2. 数值%：占比相对于父元素的比例
    * \<center>：文本相对于父元素剧中，已废弃

    * 案例 ：公司简介 见代码day06_html: 3\_案例1\_公司简介

 3. 图片标签：

     * img标签：
       	* src：指定图片的位置

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>图片标签</title>
    </head>
    <body>
    
        <!--展示一张图片-->
        <img src = "image/jingxuan_2.jpg" align = "right" alt = "古镇" width = "500" height = "300"/>
        <!--
            相对路径
                * 以.开头的路径
                * ./：代表当前目录 ./image/1.jpg
                * ../：代表上一级目录  ../image
            -->
    </body>
    </html>
    ```

    

 4. 列表标签：

     * 有序列表：
        * ol：
        * li：
     * 无序列表
       	* ul：
       	* li：围堵标签，围堵列表中每一项

 5. 链接标签：

     * a:  定义一个超链接
        * 属性：
          	* href：指定访问资源的URL（统一资源定位符）
           * target：指定打开资源的方式
             	* _self：默认值，再当前页面打开
                	* _blank：在空白页面打开

 6. div和span：

    * div: 每一个div占满一整行，块级标签
    * span: 文本信息在一行展示，行内标签，内联标签

	7. 语义化标签：html5中为了提高程序的可读性，提供了一些标签

    	1. \<header>
    	2. \<footer>

    

 8. 表格标签：

    * table：定义表格
      * width：宽度
      * border：边框
      * cellpadding：定义内容和单元格的距离
      * cellspacing：定义单元格之间距离，如果指定为0，则单元格的线会合为一条
      * bgcolor：背景色
      * align: 对齐方式
    * tr：定义行
      * bgcolor：背景色
      * align: 对齐方式
    * td：定义单元格
      * colspan：合并列
      * rowspan：合并行
    * th：定义表头单元格
    * \<caption>： 定义表格标题
    * \<thead>：表示表格的头部份
    * \<tbody>：表示表格的体部分
    * \<tfoot>：表示表格的脚部分

#### 案例：旅游网站首页 day06_html: 7\_综合案例

 1. 确定使用table完成布局

 2. 如果某一个行只有一个单元格，则使用\<tr>\<td>\</td>\</tr>

 3. 如果某一行由多个单元格，则使用

    ​	\<tr>

    ​		\<td>

    ​					\<table>\</table>

    ​		\</td>

    ​	\</tr>
    
    

8. 表单标签

    * 表单：

       * 概念：用于采集用户输入的数据。用于和服务器进行交互。

       * 使用标签：form 用于定义表单。可以定义一个范围，范围代表采集用户数据的一个范围
            * 属性：
                 * action：指定提交数据的URL

                 * method：指定提交方式
                     * 分类：一共七种，两种常用

                         get：
                                1. 请求参数会在地址栏中显示。会封装到请求行
                                2. 请求参数的大小是有限制
                                3. 不太安全

                         post：

                         1. 请求参数不会在地址栏中显示。会封装在请求体中(HTTP协议)
                         2. 请求参数的大小没有限制
                         3. 较为安全

                 * 表单项中的数据要想被提交，必须指定name属性

      * 表单项标签：

        * input标签：可以通过type属性值，改变元素展示样式
          * type属性：
            * text：文本输入框 默认值
              * placeholder： 指定文本输入框的提示信息，当输入框内容发生变化，会自动清空
            * password：密码输入框
            * radio：单选框
              	1. 要想让多个单选框实现单选效果，多个单选框的name属性值必须相同
               	2. 一般会给每一个单选框提供value属性，指定其被选中后提交的值。
               	3. checked可以指定默认值
            * checkbox：多选框
              	1. 一般会给每一个单选框提供value属性，指定其被选中后提交的值。
               	2. checked可以指定默认值
            * file：文件选择框
            * hidden：隐藏域，用于提交一些信息。
            * 按钮：
              	1. submit : 提交按钮
               	2. button：普通按钮
               	3. image：图片提交按钮
                   * 通过src属性指定图片的路径
          * label：指定输入项的文字描述信息
            * 注意：
              * label和for属性一般会和 input 的 id属性值 对应。如果对应了，则点击  label 区域， 会让input输入框的获取焦点
        * select：下拉列表
          * 子元素：option：指定列表项
        * textarea：文本域
          * cols：指定列数，每一行有多少个字符
          * rows：默认多少行。

### CSS：页面的美化和布局控制

	#### 1. 概念：Cascading Style Sheets 层叠样式表
	
	* 层叠：多个样式可以作用在同一个html的元素上，同时生效

#### 2. 好处：

	1. 功能强大
	2. 将内容展示和样式控制分离
	  	1. 降低耦合度。解耦
	  	2. 让分工协作更容易
	  	3. 提高开发效率

#### 3.CSS的使用：CSS与html结合方式

 1. 内联样式

    * 在标签内使用style属性指定css代码

      ```css
      <div style = "color:red">hello css</div>
      ```

 2. 内部样式

     * 在head标签内，定义style标签，style标签的标签体内容就是css代码

     * 如：

       ```css
       <head>
           <meta charset="UTF-8">
           <title>Title</title>
           <style>
               div{
                   color:blue;
               }
           </style>
       </head>
       <body>
       
       <!--
           内部样式
               *在head标签内，定义style标签，style标签的标签体内容就是css代码
       -->
       
       <div>hello css</div>
       ```

 3. 外部样式

    1.  定义css资源文件
    2.  在 head标签内，定义link标签，引入外部的资源文件
       * 如：

    ```css
    <link rel="stylesheet" href = "css/a.css">
    
    <!--a.css文件中-->
    div{
        color: green;
    }
    ```

* 注意：

   1. 三种方式CSS作用范围越来越大

   2. 后前常用的是后两种方式

   3. 第三种格式可以写为：

      ​	\<style>

      ​				\@import "css/a.css"

      ​	\</style>

#### 4. CSS基本语法

 * 格式：

   ​	选择器{

   ​		属性名1:  属性值1;

   ​		属性名2:  属性值2;

   ​		属性名3:  属性值3;

   ​		.........

   ​	}

* 选择器：筛选具有相似特征的元素

* 注意：

  * 每一对属性需要使用; 隔开，最后一对属性可以不加

#### 5.选择器：筛选具有相似特征的元素

 * 分类：

     1. 基础选择器

        1. id选择器 ： 选择 具体的 id 属性值的元素, 建议在一个html页面中id值唯一
           
            语法： #id属性值{}
        2. 元素选择器： 选择具有相同标签名称的元素
            * 语法： 标签名称{}
            * 注意; id选择器优先级高于元素选择器
        3. 类选择器： 选择具有相同class属性值的元素
            * 语法： .class属性值{}
            * 注意：类选择器的优先级高于元素选择器

     2. 扩展选择器

          1. \* 选择所有元素：

             ​	语法： \*{}

           	 2. 并集选择器：

             * 语法：选择器1, 选择器2{}

           	 3. 子选择器：筛选选择器1元素下的选择器2元素

             * 语法： 选择器1   选择器2{}

           	 4. 父选择器：筛选选择器2的父元素 选择器1
 	
           	* 语法： 选择器1 > 选择器2{}
 	
           	 5. 属性选择器：选择元素名称，属性名=属性值的元素

             * 语法：元素名称[属性名称=”属性值“]{}

           	 6. 伪类选择器：选择一些元素具有的状态

             * 语法： 元素：状态{}
             * 如： \<a>
               * 状态：
                 * link：初始化的状态
                 * visited：被访问过的状态
                 * active：正在访问状态
                 * haover：鼠标悬浮状态

#### 6. 属性

  1. 字体、文本

       		1. font-size: 字体大小
              		2. color：文本颜色
              		3. text-align：对齐方式
              		4. line-height：行高

  2. 背景

     ​	* background：复合属性

  3. 边框

     ​	* border：设置边框  复合属性

  4. 尺寸

     * width: 宽度
     * height：高度

  5. 盒子模型：控制布局

     	* margin：外边距
      * padding：内边距
        	* 默认情况下内边距会影响整个盒子的大小
        	* box-sizing: border-box;  设置盒子属性，让width和height就是最终盒子大小
     * float：浮动
       * left
       * right

#### 案例：见day07_html&CSS 11-案例-注册页面-CSS

### JavaScript基础



##### * JavaScript概念：是一门客户端脚本语言

	* 运行在客户端浏览器中的，每一个浏览器都有JavaScript的解析引擎
	* 脚本语言：不需要编译，直接就可以浏览器解析执行

* 功能：
  * 可以用来增强用户和html页面的交互过程，可以用来控制html元素，让页面有一些动态的效果，增强用户的体验
* JavaScript =  ECMAScript  +  JavaScript 自己特有的东西(BOM + DOM);



#### ECMAScript: 客户端脚本语言的标准

  1. 基本语法：

       1.  与html结合方式：

            1. 内部

               	* 定义\<Script>标签，标签体内容就是JS代码

            2. 外部

               * 定义\<Script>标签，通过src属性引入外部的js文件

               * 注意：
                 	1. \<Script>可以定义在html页面任意地方，但是位置会影响执行顺序
                  	2. \<Script>标签可以定义多个

       2. 注释：

            		1. 单行注释：//注释内容
            	 	 	 	 	 	 	 	 	 	 	 	 	 	 		2. 多行注释：/\*注释内容\*/

       3. 数据类型：

            		1. 原始数据类型（基本数据类型）：
             	  		1. number：数字。整数/小数/NaN(Not  a number 一个不是数字的数字类型)
             	  		2. string：字符串。 字符串 "abc"  "a"  'a'
             	  		3. boolean: true和false
             	  		4. null:  一个对象为空的占位符
             	  		5. undefined：未定义。如果一个变量没有给初始化值，则默认赋值为undefined
            	 	 	 	 	 	 	 	 	 	 	 	 	 	 		2. 引用数据类型：对象

       4. 变量：

          	* 变量：一块存储数据的内存空间
           * Java语言是强类型的语言，而JavaScript是弱类型的语言
             	* 强类型：在开辟变量存储空间时，定义了空间能存储的数据类型，只能存储固定的数据类型
                	* 弱类型：在开辟变量存储空间时，不定义空间能存储的数据类型，可以存放任意类型的数据
          * 语法：
            * var 变量名 = 初始化值；

       5. 运算符：

            1. 一元运算符：只有一个运算数的运算符

               ​	++， -- ， +(正号)  -(负号)

                * 注意：JS中，如果运算数不是运算符要求的类型，那么JS引擎会自动将运算数进行类型转换
                   * 其他类型转number：
                     	* string转number：按照字面值转换。如果字面值不是数字，则转为NaN（不是数字的数字）
                     	* boolean转number：true转为1， false转为0

             		2. 算数运算符

               ​	+， -， *， /， %.....

               ​	JS中number类型包含小数，因此 / 可以除出小数

             		3. 赋值运算符

               ​	= += -=

             		4. 比较运算符

               ​	>   <   >=   <=   ===(全等于)

               * 比较方式

               1. 类型不同：先进行类型转换，再进行比较

                  ​	====：全等于。在比较之前，先判断类型，如果类型不一样，直接范围false

               2. 类型相同：直接比较

              字符串：按照字典顺序比较。按位逐一比较，直到得出大小为止

             		5. 逻辑运算符

               ​	&& || ！

               * &&： 与(短路)
               * ||： 或(短路)
               * ！： 非
               *         * 其他类型转boolean
               *               1. number： 0 或 NaN为假，其他为真
               *               2. string： 除了空字符串，其他都是true
               *               3. null & undefined 都是false
               *               4. 对象： 所有对象都是true

             		6. 三元运算符（同Java）

               ​	 ？ ：

       6. 流程控制语句：

             	1. if...else
             	2. switch:
              * 在java中， switch可以接受的数据类型：byte short int char， 枚举(1.5)， String(1.7)
              * 在JS中，switch可以接受任何原始数据类型

              		3. while
              	  	4. do..while
       	 		5. for

7. JS特殊语法：
       
            		1. 语句以; 结尾，如果一行只有一条语句，可以省略;(不建议)
            	        	        	        	        	        	        	        	        	        	        	        	        	 	 2. 变量的定义使用var 关键字，也可以不使用
              	          	          	          	          	          	          	          	          	          	          	          	          	   	   * 用：定义的变量是局部变量
		  * 不用：定义的变量是全局变量（不建议使用）
       	   	   	   	   	   	   	   	   	   	   	   	   	
   	 8. 九九乘法表练习
     	  
     	 ```javascript
     	 <!DOCTYPE html>
     	 <html lang="en">
     	 <head>
     	     <meta charset="UTF-8">
     	     <title>九九乘法表</title>
     	     <style>
     	         td{
     	             border: 1px solid;
     	         }
     	     </style>
     	     <script>
     	         document.write("<table align='center'>");
     	         //1.完成基本for循环嵌套展示乘法表
     	         for (var i = 0; i <= 9 ; i++) {
     	             document.write("<tr>");
     	             for (var j = 1; j <= i ; j++) {
     	                 document.write("<td>");
     	                 //输出
     	                 document.write(i + "*" + j + "=" + (i * j) + "&nbsp;&nbsp;&nbsp;");
     	                 document.write("</td>");
     	             }
     	 /*            //输出换行
     	             document.write("<br>")*/
     	             document.write("</tr>");
     	         }
     	 
     	         //2.完成表格嵌套
     	         document.write("</table>");
     	     </script>
     	 </head>
     	 <body>
     	 
     	 </body>
     	 </html>
     	 ```


​	2. 基本对象：
​	  
​	   1. Function: 函数对象
​	   
​	      Function: 函数(方法)对象
​	          1. 创建
​	              1. var fun = new Function(形式参数列表, 方法体); 不用
​	              2. function 方法名称(形式参数列表){
​	                      方法体
​	              }
​	              3. var 方法名 = function(形式参数列表){
​	                     方法体
​	       }

   2. 方法
      
          3. 属性:
       length: 代表形参的个数
          
          4. 特点:
              1. 方法定义时，形参的类型不用写, 返回值类型也不写
              2. 方法是一个对象，定义相同名称的方法，会覆盖
              3. 在JS 中，方法的调用只与方法的名称有关，和参数列表无关
       4. 在方法声明中有一个隐藏的内置对象（数组）， arguments，封装了所有的实际参数
         
          5. 调用：
       方法名称(实际参数列表);
            
       		2. Array： 数组对象
             
              1. 创建：
                  1. var arr = new Array(元素列表);
                  2. var arr = new Array(默认长度);
                  3. var arr = [元素列表];
                  2. 方法：
                  join(参数): 将数组中元素按照指定的分隔符拼接为字符串
                  push()： 向数组的末尾添加一个或多个元素。并返回新的长度
                  3.属性：
                  length: 表示数组的长度
                  4.特点：
                  1. JS中，数组元素的类型是可变的
                2. JS中，数组的长度是可变的
             
	                 		3. Boolean
             
              		4. Date
              1. 创建：
          
          
           var date = new Date();
          
          2. 方法：
                  toLocaleString()： 返回当前date对象对应时间本地字符串格式
           getTime():  获取毫秒值。返回当前日期对象描述时间和1970年1月1日零点的毫秒值差
          
          	5. Math
          
       
      ​	Math：数学对象
      ​    1. 创建：
      ​        * 特点：Math对象，不用创建，直接使用。Math.方法名();
      
          2. 方法：
              random():  返回0~1之间的随机数。包含0，不含1
              ceil(): 向上取整
              floor()：向下取整
              round(): 四舍五入
       3. 属性：
       PI：圆周率
         
            		6. Number
            		
            		7. String
            		
            		8. RegExp：正则表达式对象
            	   	
            		1. 正则表达式：定义字符串的组成规则的
            		
            			1. 单个字符：[ ]
      
         		  如	[ a]  [ab] : a 或 b  [a-zA-Z0-9_]
         		
         		  	  * 特殊符号代表特殊含义的单个字符
         		  	    * \d:   单个数字字符[0-9]
         		    	* \w：单个单词字符[a-zA-Z0-9_]
         		
         			2. 量词符号：
         		
         		  ？：表示出现0次或1次
         		
         		  *：表示出现0次或多次
         		
         		  +：出现1次或多次
         		
         		  {m, n}：表示 m<= 数量 <=n
         		
         		  	  	* m 如果缺省：{，n}：最多n次
         		  		* n如果缺省：{m，}：最少m次
         		
         			3. 开始结束符号
         		
         		  	  	* ^ :开始符号
         		  		* $: 结尾符号
         	 	   	
         		2. 正则对象：
         		
         			1. 创建：
         		
         		  	    1. var reg = new RegEx(“正则表达式”)
         		  		2. var reg = /正则表达式/;
         		
         			2. 方法：
         		
         		  ​	test(参数)：验证指定的字符串是否符合正则定义的规范
         		
         		9. Global：
         	 	   	
         		1. 特点：全局对象，这个Global对象中封装的方法不需要对象就可以调用。  方法名().
         	
         	2. 方法：
      
        1. 特点：全局对象，这个Global对象中封装的方法不需要对象就可以调用。  方法名().
      
               2. 方法：
                      encodeURI(): url编码   将汉字编码为16进制，每个字节之间加 %
             
      
          decodeURI()：url解码
                 
                encodeURIComponent(): url编码  编码的字符更多
      decodeURIComponent():url解码
           
                  parseInt(): 将字符串转为数字
      
      
          * 逐一判断每一个字符是否是数字，直到不是数字为止，将前面数字部分转为字符串
                
            isNaN()  判断一个值是否是NaN
             * NaN六亲不认。NaN参与的比较全部为false
                
                   eval():  将JavaScript字符串，转成JavaScript脚本执行

#### BOM

1. 概念： Browser Object Model 浏览器对象模型

   	* 将浏览器的各个组成部分封装成对象

2. 组成：

   1. Window： 窗口对象
   2. Navigator：浏览器对象
   3. Screen：显示器屏幕对象
   4. History：历史记录对象
   5. Location：地址栏对象

3. Window： 窗口对象

   1. 创建

   2. 方法：
      1. 与弹出窗口有关的方法：
           alert(): 显示带有一段消息及确认按钮的警告框
           confirm() 显示带有一段信息及确认取消按钮的对话框

              * 如果点击确定，则方法返回true
              * 如果点击取消，则返回false

           prompt() 显示可以提示用户输入的对话框。

             * 返回值：获取用户输入的值

       2. 与打开关闭有关的方法
           close(): 关闭浏览器窗口
               * 谁调用我，我关谁
           open(); 打开一个新的浏览器窗口
                   * 返回一个新的window对象

      3. 与定时器有关的方法
         setTimeout()  在指定时间后，调用函数
         
          * 参数：
             1. js代码片段或者方法
             2. 毫秒值
   * 返回值：唯一标识，用于取消定时器
         
   clearTimeout()  取消由setTimeout() 方法设置的 timeout
         
         setInterval()  按照指定周期(毫秒)来调用函数
      clearInterval() 取消由setInterval() 设置的
      
   3. 属性：

   4. 特点：
      
          * Window对象不需要创建可以直接使用， window使用  window.方法名()；
          * window引用可以省略， 方法名();

4. Location: 地址栏对象

   1. 创建(获取)：
      1. window.location
      2. location
   2. 方法：
      * reload() 重新加载当前文档。刷新
   3. 属性：
      * href  设置或返回完整的 URL(统一资源定位器）

5. History : 历史记录对象
   1. 创建(获取)：
      1. window.history
      2. history
   2. 方法：
      1. back() ：加载  history列表中的前一个 URL界面
      2. froward()：加载  history列表中的下一个 URL界面
      3. go()： 加载history列表中的某个具体页面
         * 参数：
             * 正数：前进几个历史记录
             * 负数：后退几个历史记录
   3. 属性：
      * length:  返回当前窗口历史列表中的  URL 数量

#### DOM：

 * 概念 : Document Object Model 文档对象模型

   	* 将标记语言文档各个组成部分，封装为对象。可以使用这些对象，对标记语言文档进行CURD的动态操作

* W3C DOM 标准被分为 3 个不同的部分：

  * 核心 DOM - 针对任何结构化文档的标准模型

    * Document：文档对象
    * Element：元素对象
    * Attribute：属性对象
    * Text：文本对象

    * Comment：注释对象

    

    * Node: 节点对象，其他五个的父对象

  * XML DOM - 针对 XML 文档的标准模型

  * HTML DOM - 针对 HTML 文档的标准模型



* 核心DOM模型：

  * Document：文档对象
     	1. 创建(获取)：在html对象模型中可以使用window对象来获取
          	1. window.document
          	2. document
      	2. 方法：
           	1. 获取Element对象：
             	1. getElementById()   根据id属性值， 获取元素的对象
             	2. getElementsByTagName()： 根据元素**标签**名称获取元素对象们， 返回值是一个数组
             	3. getElementsByClassName()：根据Class属性值获取元素对象们。返回一个数组
             	4. getElementsByName()：根据name属性值获取元素对象们。返回一个数组
              	2. 创建其他DOM对象：
            1. createAttribute(name)
            2. createComment()
            3. createElement()  掌握
            4. createTextNode()
      	3. 属性：
  * Element：元素对象
    * 获取：通过document对象获取和创建
    * 方法：
      	1. removeAttribute() 删除属性
       	2. addAttribute()创建属性
  * Node: 节点对象，其他五个的父对象
    * 特点：所有dom对象都可以被认为是结点
    * 方法：
      * CRUD dom树：
        * appendChild():  向结点的子节点列表的结尾添加新的子节点
        * removeChild()：删除(并返回)当前结点的指定子结点
        * replaceChilad()：用新节点替换一个子节点
    * 属性：
      * parentNode：返回当前结点的父节点

* HTML DOM

  1. 标签体的设置和获取：innerHTML

  2. 使用html元素对象的属性

  3. 控制元素样式

     1. 使用元素的style属性来设置

        如：	

        ```
        //修改样式方式1
        div1.style.border = "1px solid red";
        
        div1.style.width = "200px";
        
        //font-size --> fontSize
        div1.style.fontSize = "20px";
        ```

     2. 提前定义号类选择器的样式，通过元素的className属性设置其class值，间接选择CSS代码样式

* 功能：控制html文档内容

* 代码：获取页面的标签(元素)对象 Element

  * document.getElementById("id值")： 通过元素的id获取元素对象
  * 操作Element对象：
     	1. 修改属性值：
          	1. 明确获取的对象是哪一个
          	2. 查看API文档，找其中有哪些属性可以设置
     	2. 修改标签体内容：
          	1. 获取元素对象
          	2. 使用innerHTML 修改内容

 	1. 事件
 	 * 功能：某些组件被执行了某些操作后，触发某些代码的执行
 	 * 如果绑定事件
 	    	1. 直接在html标签上, 指定属性(操作), 属性值就是js代码
 	         	1. 事件：onclick---单机事件
 	   		2. 通过js获取元素对象，指定事件属性，设置一个函数

#### 事件监听机制：

 * 概念：某些组件被执行了某些操作后，触发某些代码的执行
   	* 事件：某些操作， 如：单机，双击，键盘按下，鼠标移动
      	* 事件源：组件。如： 按钮  文本 输入框。。。
      	* 监听器：代码。
      	* 注册监听：将事件，事件源，监听器结合在一起。当事件源上发生了某个事件，则触发某个监听器代码
* 常见的事件
  1. 点击事件：
     1. onclick  单机事件
     2. ondbclick 双击事件
  2. 焦点事件：
     1. onblur： 失去焦点
        * 一般用于表单验证
     2. onfocus：元素获得焦点
  3. 加载事件：
     1. onload：一张页面或一副图像完成加载
  4. 鼠标事件
     1. onmousedown 鼠标按下
        * 定义方法时，定义一个event对象接收参数
        * event对象的button属性可以获取鼠标按钮被点击了
     2. onmouseup 鼠标松开
     3. onmousemove 鼠标被移动
     4. onmouseover 鼠标移动到元素上
     5. onmouseout  鼠标从某元素移开
  5. 键盘事件
     1. onkeydown 键盘按下
     2. onkeyup 键盘被松开
     3. onkeypress 某个键盘按键被按下并松开
  6. 选择和改变
     1. onchange：域的内容被改变
     2. onselect：文本被选中
  7. 表单时间
     1. onsubmit：确认按钮被点击
        * 可以阻止 表单提交
        * 方法返回false，阻止表单被提交
     2. onreset：重置按钮被点击

### BootStrap

1. 概念：一个前端开发的框架
   * 框架：一个半成品软件，开发人员可以在框架基础上，进行开发，简化编码
   * 好处：
     	1. 定义了很多的CSS样式和js插件，开发人员可以直接使用这些样式和插件得到丰富的效果
      	2. 响应式布局。
          * 同一套页面可以兼容不通过分辨率的设备
2. 快速入门
   1. 下载bootstrap
   2. 在项目中复制三个文件夹
   3. 创建html页面，引入必要的资源文件

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap HelloWorld</title>

    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="js/jquery-3.2.1.min.js"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="js/bootstrap.min.js"></script>

</head>
<body>
<h1>你好，世界！</h1>


</body>
</html>
```

## XML

1. 概念：Extersible Markup Language 可扩展标记语言

		* 可扩展：标签都是自定义的。 \<user>   \<student>

* 功能：
  * 存储数据
    	1. 配置文件
     	2. 在网络中传输

* xml与html区别
  	1. xml 标签都是自定义的，html的标签是预定义的
   	2. xml语法严格，html语法不严格
   	3. xml存储数据， html展示数据。

​	与properties竞争

​			\<user>

​				/<name>zhnagsan/</name>

​				\<age>23\</age>

​		\</user>

* ​		W3C：万维网联盟

2. 语法：

   * 基本语法：

     	1. xml 文档后缀名 .xml
     	2. xml第一行 必须定义为文档声明  （必须是第一行， 即使空行都不可以 ）
     	3. xml文档中，有且仅有一个根标签
     	4. 属性值必须使用引号(' '  或 “ ”)
     	5. 标签必须正确关闭
     	6. xml标签名称区分大小写

   * 快速入门：

     ```xml
     <?xml version='1.0' ?>
     
     <users>
     	<user id = '1'>
     		<name>zhangsan</name>
     		<age>23</age>
     	</user>
     
     	<user id = '2'>
     		<name>lisi</name>
     		<age>25</age>
     	</user>
     </users>
     ```

   * 组成部分：

     1. 文档声明

        1. 格式：\<?xml version='1.0'  encoding = 'gbk'  ?> 
        2. 属性列表：
           * version：版本号，必须属性
           * encoding：编码方式。 告知解析引擎 当前文档使用的字符集   默认 ISO-8859-1
           * standalone：是否独立  现在大多数不设置了
             * 取值：
               * yes: 不依赖其他文件
               * no：依赖其他文件

     2. 指令（了解）：结合CSS的 

        * ```xml
          <?xml-stylesheet type="text/css" href="a.css" ?>
          ```

     3. 标签：标签名称自定义的

         * 规则：
           1. 名称可以包含字母，数字，以及其他字符
           2. 名称不能以数字或者标点符号开始
           3. 名称不能以字母 xml （或者 XML ，Xml 等） 开始
           4. 名称不能含空格

     4. 属性：

        ​	id 属性值 唯一

     5. 文本

        * CDATA 区： 在该区域的数据会被原样展示
          * 格式： \<![CDATA[  数据 ]]>

   * 约束：规定xml文档的书写规则

     * 作为框架使用者（程序员）：

       1. 能够在xml中引入约束文档
       2. 能够简单的读懂约束文档

     * 分类：

       	1. DTD ： 一种简单约束文档
       	2. Schema：一种复杂的约束文档

     * DTD：

       * 引入dtd文档到xml文档中
         * 内部dtd：将约束规则定义在xml文档中
         * 外部dtd：将约束规则定义在外部文件中
           * 本地：\<!DOCTYPE 根标签名 SYSTEM  "dtd文件位置">
           * 网络：\<!DOCTYPE 根标签名 PUBLIC "dtd文件名字"  "dtd文件位置URL">

     * Schema:

       * 引入：

         1.填写xml文档的根元素
         2.引入xsi前缀.  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         3.引入xsd文件命名空间.  xsi:schemaLocation="http://www.itcast.cn/xml  student.xsd"
         4.为每一个xsd约束声明一个前缀,作为标识  xmlns="http://www.itcast.cn/xml" 

       ```xml
        <a:students   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       			   xsi:schemaLocation="http://www.itcast.cn/xml  student.xsd"
       			   xmlns:a="http://www.itcast.cn/xml"
        		    >
       ```

       3. 解析：操作xml文档，将文档中的数据读取到内存中

       * 操作xml文档

         1. 解析(读取) : 将文档中的数据读取到内存中
         2. 写入：将内存中数据保存到xml中。持久化储存

       * 解析xml方式

         1. DOM: 将标记语言文档一次性加载进内存，在内存中形成DOM树 （服务器端）
            	* 优点：操作方便，可以对文档进行CRUD所有操作
            	* 缺点：占内存
         2. SAX：逐行读取，基于事件驱动的。（移动端）
            * 优点：不占内存。
            * 缺点，只能读取，不能增删改

       * xml常见的解析器：

         1. JAXP：sun公司提供的解析器，支持dom和sax两种思想
         2. DOM4J：一款优秀的解析器
         3. Jsoup：解析HTML的，可以直接解析某个URL地址.HTML文本内容。提供了一套非常省力的API，可以通过DOM，CSS以及类似于jQuery的操作方法来取出和操作数据。
         4. PULL：Android操作系统内置解析器。sax方式

       * Jsoup：

         * 快速入门：

           * 步骤：
             1. 导入jar包
             2. 获取Document对象
             3. 获取对用的标签Element对象
             4. 获取数据

           ```java
                   //2.获取document对象，根据xml文档获取
                   //2.1 获取student.xml的path
                   String path = JsoupDemo01.class.getClassLoader().getResource("student.xml").getPath();
                   //2.2 解析xml文档，加载文档进内存，获取dom树----> Document
                   Document document = Jsoup.parse(new File(path), "utf-8");
                   //获取元素对象 Element
                   Elements elements = document.getElementsByTag("name");  //返回了一个集合
           
                   System.out.println(elements.size());
                   //3.1获取第一个name的Element对象
                   Element element = elements.get(0);
                   //3.2获取数据
                   String name = element.text();
                   System.out.println(name);
           ```

       * 对象的使用
          * Jsoup：工具类，可以解析html或xml对象，返回Document
             * parse: 解析html或xml文档，返回Document
                * parse(File in, String charseName):  解析xml或html文件
                * parse(String html) 解析xml或html字符串
                * parse(URL url, int timeoutMillis) :  通过网络路径获取指定的html或xml文档对象
          * Document：文档对象，代表内存中的dom树
             * 获取Element对象
               	* getElementsByTag（String Tagname）根据标签名称获取元素对象集合
               	* getElementsByAtrribute（String key）根据属性名称获取元素对象集合
               	* getElementsByAtrributeValue（String key， String Value）根据对应的属性值，属性名称获取元素对象集合
               	* getElementById(String id): 根据id属性值获取唯一的element对象
          * Elements： 元素Element对象的集合。 可以当作ArrayList\<Element>来使用
          * Element:元素对象
             	1. 获取子元素对象
                 	* getElementsByTag（String Tagname）根据标签名称获取元素对象集合
                 	* getElementsByAtrribute（String key）根据属性名称获取元素对象集合
                 	* getElementsByAtrributeValue（String key， String Value）根据对应的属性值，属性名称获取元素对象集
                 	* getElementById(String id): 根据id属性值获取唯一的element对象
              	2. 获取属性值
                * String attr(String key): 根据属性名称，获取属性值
            
              	3. 获取文本内容
              	* String text()：获取文本内容
              	* String html(): 获取标签体的所有内容（包括子标签的字符串内容）
          * Node：节点对象
            
            	* 是Document和Element的父类
       * 快捷查询方式：
         1. selector：选择器
            * 使用方法 Elements select（String cssQuery）
              * 语法：参考Selector中定义的语法
         2. Xpath：**XPath**即为XML路径语言（XML Path Language），它是一种用来确定XML文档中某部分位置的语言。
            * 使用Jsoup的Xpath需要额外导jar包
     * 查询W3Cshool参考手册，使用Xpath完成语法查询
       
## JavaWeb


​       
###  概念回顾

        	1. 软件架构
        	  	1. C/S：客户端/服务器端
        	  	2. B/S：浏览器/服务器端
        	2. 资源分类
        		1. 静态资源：所有的用户访问后，得到的结果都是一样的
        	    * 如： html， css， javascript
        		2. 动态资源：每个用户访问相同资源后，得到结果可能不一样
        	    * 如：servlet/jsp，php，asp。。。。
        	    * 注意： **浏览器只有静态资源解析引擎**，**所有的动态资源都要在服务器中转换成静态资源*，返回给浏览器，称为响应**
        	3. 网络通信三要素
        		1. IP：电子设备（计算机）在网络中唯一标识
        		2. 端口：应用程序在计算机中的唯一标识。0~65536
        		3. 传输协议：规定数据传输的规则
        	    	1. tcp：安全协议，三次握手。速度稍慢
        	2. udp：不安全协议。速度快

### web服务器软件：

       	* 服务器：安装了服务器软件的计算机
       	* 服务器软件：接受用户请求，处理请求，做出响应
        * web服务器软件：接受用户请求，处理请求，做出响应。
          	* 在web服务器软件中，可以部署web项目，让用户通过浏览器来访问这些项目
             	* web容器
       * 常见的java相关web服务器软件
         * webLogic：oracle公司，大型的JavaEE服务器 支持所有的JavaEE规范，收费的
         * webSphere: IBM公司，大型的JavaEE服务器 支持所有的JavaEE规范，收费的
         * JBOSS: JBOSS公司，，大型的JavaEE服务器 支持所有的JavaEE规范，收费的
  * Tomcat：Apache基金组织，中小型JavaEE 服务器，仅仅支持少量的JavaEE规范servlet/jsp， 开源，免费
    

    
* JavaEE： Java语言在企业级开发中使用的技术规范综合，一共规定了13项大规范
  
* Tomcat：web服务器软件
       
   1. 下载
      
   2. 安装：解压安装包即可
      
      * 注意：目录不要有中文和空格
      
   3. 卸载：删除目录
      
   4. 启动：
      
      * bin/startup.bat  双击运行文件
      
      * 访问；浏览器输入：  http://localhost:8080  回车访问自己
      
        ​									 http://别人的ip:8080  访问别人
      
      * 可能遇到问题：
      
               1. 黑窗口一闪而过：
                  * 原因：没有正确配置JAVA_HOME环境变量
           * 解决方案：正确配置JAVA_HOME环境变量
      
        2. 启动报错
      
           1. 暴力：找到占用的端口号，并且找到对应的进程，杀死该进程
      
              * netstat -ano    （cmd）
      
           2. 温柔：修改自身的端口号
      
              * config/server.xml
      
                     * ```xml
                       <Connector port="8080" protocol="HTTP/1.1"
                                  connectionTimeout="20000"
                                  redirectPort="8443" />
                ```
       
                     * 一般会将tomcat的默认端口号修改为80.80端口号是http协议的默认端口号。
                
                    * 好处：在访问时，不用输入端口号
                ```
             ```
           
             ```
      
       5. 关闭：
          
              	1. 正常关闭：
                      	* bin/shutdown.bat
                      	* ctrl + c
       	2. 强制关闭：
              	* 点击启动窗口的x
      
       **Tomcat文件结构**
      
         1. bin  可执行文件
         2. conf 配置文件
        3. lib 依赖jar包
        4. logs 日志文件
       5. temp 临时文件
  6. webapps： 存放web项目
       7. work：存放运行时的数据
  
     6. 配置：
  
         * 部署项目的方式：
  
             1. 直接将项目放到wedapps目录下
         
                * /hello：项目的访问路径-->虚拟目录
     
       * 简化部署：将项目达成一个war包，再将war包放置到webapps目录下。
               * war包会自动解压缩
       
          2. 配置config/server.xml文件
            
                ​	在\<Host>标签体中配置
          
                ```xml
                    <!-- 部署项目 -->
             <Context docBase="E:\hello" path="hehe"/>
             ```
          
       * docBase: 项目存放的路径
             * path：虚拟目录
       
          3. 在conf\Catalina\localhost 创建任意名称xml文件。在文件中编写
            
             ​		\<Context docBase="E:\hello"/>
            
             		* 虚拟目录：文件的名称
       
       * 静态项目和动态项目：
       
         * 目录结构
         
           * java动态项目目录结构：
         
             ---  项目的根目录
         
             ​		-- WEB-INF目录：
         
             ​			--web.xml：web核心配置文件
         
             ​			--classes目录：放置字节码文件的目录
         
                ​			--lib目录：放置依赖的jar包
           
          * 将Tomcat集成到IDEA中，并且创建JavaEE项目，部署项目

### Servlet：server applet

 *  概念：运行在服务器端的小程序
    	*  Servlet就是一个接口，定义了java类被浏览器访问到(tomcat识别)的规则。
        	*  将来我们定义一个类，实现Servlet接口，复写方法。



*  快速入门：

   1. 创建JavaEE项目
   2. 定义一个类，实现Servlet接口
   3. 实现接口中的抽象方法
   4. 配置Servlet  在 web.xml中配置

   ```xml
       <!--配置servlet-->
       <servlet>
           <servlet-name>demo1</servlet-name>
           <servlet-class>cn.web.servlet.ServletDemo01</servlet-class>
       </servlet>
       
       <servlet-mapping>
           <servlet-name>demo1</servlet-name>
           <url-pattern>/demo1</url-pattern>
       </servlet-mapping>
   ```

* Servlet执行原理

  * 对象的创建和方法调用都是服务器执行的。

  ```xml
  <!--配置servlet-->
  <servlet>
      <servlet-name>demo1</servlet-name>
      <servlet-class>cn.web.servlet.ServletDemo01</servlet-class>
  </servlet>   
  <!--
  	1. tomcat将全类名对应的字节码文件加载进内存。 Class,forNmae()
  	2. 创建对象.cls.newInstance();
  	3. 调用方法---serviece
  -->
  
  <servlet-mapping>
      <servlet-name>demo1</servlet-name>
      <url-pattern>/demo1</url-pattern>
  </servlet-mapping>
  ```

1.  当服务器接受到客户端浏览器的请求后，会解析请求URL路劲，获取访问Servlet的资源路径
2. 查找web.xml 文件，是否有对应的\<url-pattern>标签体内容。
3. 如果有，则找到对应的\<servlet-class>全类名
4. tomcat会将字节码文件加载进内存，并且创建其对象
5. 调用其方法

* Servlet中的生命周期：

   1. 被创建：执行init方法，只执行一次

      * Servlet什么时候被创建?

        * 默认情况下，第一次被访问时，Servlet被创建

        * 可以配置指定Servlet的创建时间

          * 在\<servlet>标签下配置

          1. 第一次被访问时，创建
             * \<load-on-startup>的值为负数

          2. 在服务器启动时，创建
             * \<load-on-startup>的值为0或正整数

      * Servlet的init方法，只执行一次，说明一个Servlet在内存只存在一个对象，Servlet是单例的

        * 多用户同时访问时，可能存在线程安全问题。
        * 解决：尽量不要在Servlet中定义成员变量。即使定义了成员变量，也不要对其修改值

   2. 提供服务：执行service方法，执行多次

      * 每次访问Servlet时，Service方法都会被调用一次

   3. 被销毁：执行destroy方法，执行一次

      * Servlet被销毁时执行。
      * 只有服务器正常关闭时，才会执行destory方法。
      * destory 方法在  Servlet 被销毁前执行，一般用于释放资源。

* Servlet3.0：

  * 好处：

    * 支持注解配置。可以不需要web.xml了

  * 步骤：

    1. 创建JavaEE项目，选择Servlet版本3.0以上，可以不创建web.xml

    2. 定义一个类，实现Servlet接口

    3. 复写方法

    4. 在类上使用@WebServlet注解，进行配置

       * ```java
         @WebServlet("资源路径")
         ```

### IDEA与Tomcat相关配置

 1. IDEA会为每一个tomcat部署的项目单独建立一份配置文件

    	* 查看控制台的log：Using CATALINA_BASE:   "C:\Users\WangTao\.IntelliJIdea2019.2\system\tomcat\_JavaWeb"

	2.  工作空间项目     和  tomcat部署的部署的web项目

     * tomcat真正访问的是   “tomcat部署的web项目”，  “tomcat部署的web项目”  对应着   “工作空项目”   的web目录下的所有资源
     * **WEB-INF目录下的资源不能被浏览器直接访问**
* 断点调试：使用“小虫子”启动（debug调试）

6. Servlet体系结构

   Servlet --- 接口

   ​		|

   GenericServlet   --- 抽象类

   ​		|

   HttpServlet ---  抽象类

   

    * GenericServlet： 将Servlet及口中的其他方法做了默认空实现，只将Servlet() 方法作为抽象

      	* 将来定义Servlet类时候，可以继承GenericServlet， 实现service() 方法即可

   * HttpServlet接口：对HTTP协议的一种封装，简化操作

     1. 定义类继承HttpServlet
     2. 复写doGet/doPost方法

     

     ​	Servlet

      0. 判断请求方式

         String  method = req.getMethod();

         if("GET".equals(method)){

         ​		//get方式获取数据

         ​		doGet();

         }else if ("POST".equals(method)){

         ​		// post方式获取数据

         ​		doPost();

         }

     doGet(){}

     doPost(){}

   7. Servlet相关配置
      1. urlpartten：Servlet访问路径
         * 一个servlet可以定义多个访问路径： @WebServlet({"/d4","/dd4","/ddd4"})
      2. 路径定义规则：
         1. /xxx
         2. /xxx/xxx: 多层路径，目录结构
         3. *.do

   ### HTTP

    * 概念： Hyper Text Transfer Protocol 超文本传输协议
      	
      	
      	* 传输协议：定义了，客户端和服务器端发送数据时，的数据格式
   * 特点：
     	1. 基于TCP/IP 的高级协议
      	2. 默认端口号80
      	3. 基于请求响应模型   请求与响应一一对应
      	4. 无状态的  ：  每次请求与响应相互独立，不能交互数据
   * 历史版本：
     * 1.0： 每一次请求/响应 都会建立一次链接
  * 1.1复用链接（支持长连接 和请求流水线）
   
* **请求消息数据格式**
  
   1. 请求行
   
      ​	请求方式 请求 url  请求协议/版本
   
      ​	GET /login.html  HTTP/1.1
   
      
   
          * 请求方式：
             * HTTP协议有七种请求方式，常用的有两种
                * GET ：
                  1. 请求参数在请求行中，在url后面。
                  2. 请求的url长度有限制
                  3. 不安全
                * POST：
                  	1. 请求参数在请求体中
                   	2. 请求的url长度没有限制
                		3. 相对安全
   
   2. 请求头：客户端浏览器告诉服务器，一些信息
   
      ​	请求头名称：请求致
   
          * 常见的请求头：
             	1. User-Agent： 浏览器告诉服务器，访问服务器使用的浏览器版本
                 * 可以在服务器端获取该头的信息，解决浏览器的兼容性问题
               	2. Referer：http://localhost/login.html
                * 告诉服务器，当前请求从哪里来
                  * 作用：
                     	1. 防盗链：
                         * 盗链（盗取超链接）
                  	2. 统计工作：
   
   3. 请求空行
   
      ​	空行，用于分割POST请求的请求头和请求体
   
   4. 请求体(正文)
   
      * 封装POST请求消息的请求参数的
   
    
   
  * 字符串格式：
  
    GET /login.html  HTTP/1.1
  
    Host: localhost 
  
    Connection: keep-alive   (链接活着，可以被复用)
  
    Cache-Control: max-age=0 
  
    Upgrade-Insecure-Requests: 1 
  
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) 
  
    Referer:http://localhost/login.html
  
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,
  
    Accept-Encoding: gzip, deflate, br 
  
    Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6 
  

  

​				uername = zhangsan

* **响应消息数据格式**

  1. 响应行

     1. 组成：协议/版本  响应状态码  状态码描述

     2. 响应状态码：服务器告诉客户端浏览器，本次请求和响应的一个状态

        1. 状态码都是三位数字  200  500

           * 分类：
             1. 1XX：服务器接收客户端消息，但没有接收完成，等待一段时间后，发送1xx状态码
             2. 2XX：成功 代表：200
             3. 3XX：重定向。代表：302（重定向），304（访问缓存）（浏览器本地有缓存的文件）
             4. 4XX：客户端错误。
                 * 代表：
                   	* 404（请求路径没有对应的资源）
                   	* 405（请求方式没有对应的doXXX方法）
               5. 5XX：服务器端错误。代表：500（服务器内部出现异常）

  2. 响应头

        1. 格式：头名称：值
        2. 常见的响应头：
           1. Content-Type：服务器告诉客户端本次响应体数据格式以及编码格式
           2. Content-disposition：服务器告诉客户端以什么格式打开响应体数据值：
              * in-line：默认值，在当前页面内打开
              * attachment；filename = xxx；以附件形式打开响应体。文件下载

  3. 相应空行

  4. 响应体：传输的数据

* 响应字符串格式：
  
     ```
     HTTP/1.1 200   
     <!--响应头-->
     Set-Cookie: JSESSIONID=998FB50B3F14926C519FA48A38AEFEB6; Path=/day15; HttpOnly
     Content-Type: text/html;charset=UTF-8
     Content-Length: 100
     Date: Sun, 04 Apr 2021 02:01:30 GMT
     Keep-Alive: timeout=20
     Connection: keep-alive
     			 <!--响应空行-->
     <html>
       <head>
         <title>$Title$</title>
       </head>
       <body>
       hello, response
       </body>
  </html>
  ```
  
     

### Request：

 1. request对象和response对象的原理

     	1. request和response 对象是由服务器创建的，我们来使用它们
          	2. request它们是来获取请求消息，response对象是来设置响应消息

​    

    	* **请求响应过程**
    
     	1. tomacat服务器会根据请求url中的资源路径，创建对应的ServletDemo1的对象。
     	2. tomcat服务器，会创建request和response对象，request对象中封装请求消息数据。
     	3. tomcat将request和response两个对象传递给service方法，并且调用service方法
     	4. 程序员(我们)，可以通过request对象获取请求消息数据，通过response对象设置响应消息数据
     	5. 服务器在给浏览器做出响应前，会从response对象中拿程序员设置的响应消息数据。


​    

​    

	2. request对象继承体系结构
	
	​	ServletRequest      ---- 接口
	
	​				|   继承
	
	​	HttpServletRequest       ---- 接口
	
	​				|    实现
	
	​	org.apache.catalina.connector.RequestFacade   类(tomcat)


​    

	3. request功能：
	
		1. 获取请求消息数据
	
	      1. 获取请求行数据
	
	         * GET / day14/demo1?name=zhangsan  HTTP/1.1
	
	         * 方法：
	
	            1. 获取请求方式：GET
	
	               * String  getMethod( )
	
	           	2. **获取虚拟目录**：/day14
	
	               * String  getContextPath( )
	
	           	3. 获取Servlet路径;  /demo1
	
	               * String getServletPath( )
	
	           	4. 获取GET方式的请求参数：name=zhangsan
	
	               * String getQueryString( )
	
	           	5. **获取请求URI**：/ day14/demo1
	
	               * String getRequestURI( )： / day14/demo1
	
	               * StringBuffer getRequestURL( )     http://localhost/day14/demo1


​                     

                   * URL: 统一资源定位符：http://localhost/day14/demo1   中华人民共和国
                   * URI：统一资源标识符： / day14/demo1                            共和国
    
               	6. 获取协议及版本号：HTTP/1.1
    
                   ​	* String getProtocol( )	
    
               	7. 获取客户机IP地址	
    
                   ​	* String getRemoteAddr( )
    
          2. 获取请求头数据
    
             * 方法：
               * **String getHeader(String name) ：** 通过请求头名称获取请求头的值
               * Enumeration\<String>  getHeaderNames( )：获取所有的请求头名称 
    
          3. 获取请求体数据
    
             * 请求体;zhiyou POST请求方式才有请求体，在请求体中封装了POST请求的请求参数
    
             * 步骤：
    
                1. 获取流对象
    
                    1. BufferedReader  getReader()； 获取字符输入流，只能操作字符数据
    
                    2. ServletInputStream getInputStream(): 获取字节输入流，操作所有类型的数据
    
                       ​	* 在文件上传知识点后讲解
    
                2. 再从流对象中拿数据
    
    	2. 其他功能：
    
        	1. 获取请求参数通用方式： 不论get 还是 post请求方式都可以使用
    
            	1. getParameter(String name):   根据参数名称获取参数值    username = zs&password=123
             	2. String[] getParameterValues(String name): 根据参数名称获取参数值数组    hobby=xx&hobby=game
             	3. Enumeration\<String>   getParameterNames(): 获取所有请求的参数名称
             	4. Map<String,String[]> getParameterMap():  获取所有参数的键值对
                   * 中文乱码问题
                     		* get方式： tomcat8已经将 get方式乱码问题解决了
                       * post方式：会乱码
                         		* 解决：在获取参数前。设置request编码   request.setCharacterEncoding("utf-8");
    
        	2. 请求转发：一种在服务器内部的资源跳转方式
    
            	1. 步骤：
                	1. 通过request对象获取请求转发器对象; RequestDispatcher getRequestDispatcher(String path)
                	2. 使用RequestDispatcher对象来进行转发：forward(ServletRequest request, ServletResponse response)
            	2. 特点：
                	1. 浏览器地址栏路径不发生变化
                	2. 只能转发到当前服务器内部资源中。
                	3. 转发是一次请求
    
        	3. 共享数据：
    
            * 域对象：一个有作用范围的对象，可以在范围内共享数据
            * request域：代表一次请求的范围，一般用于请求转发的多个资源中共享数据
            * 方法：
              1. serAttribute(String name, Object obj) : 存储数据
              2. Object getAttribute（String name）: 通过键获取值
              3. void removeAttribute（String name）: 删除数据
    
        	4. 获取ServletContext：
    
            ServletContext getServletContext( );

#### 案例：用户登录

 * 用户登录案例需求：

   1. 编写login.html登录页面
      	username & password 两个输入框
   2. 使用Druid数据库连接池技术,操作mysql，day14数据库中user表
   3. 使用JdbcTemplate技术封装JDBC
   4. 登录成功跳转到SuccessServlet展示：登录成功！用户名,欢迎您
   5. 登录失败跳转到FailServlet展示：登录失败，用户名或密码错误

 * 分析

 * 开发步骤

   1. 创建项目，导入html页面。配置文件，jar包

   2. 创建数据库环境

      ```sql
      CREATE DATABASE day14;
      USE day14;
      
      
      CREATE TABLE USER(
      	id INT PRIMARY KEY AUTO_INCREMENT,
      	username VARCHAR(20) UNIQUE NOT NULL,
      	PASSWORD VARCHAR(20) NOT NULL
      );
      ```

      

   3. 创建包cn.itcast.domain，创建类User

      ```java
      package cn.itcast.domain;
      
      
      /**
       * 用户的javaBean(实体类)
       */
      public class User {
          private int id;
          private String username;
          private String password;
      
          public int getId() {
              return id;
          }
      
          public void setId(int id) {
              this.id = id;
          }
      
          public String getUsername() {
              return username;
          }
      
          public void setUsername(String username) {
              this.username = username;
          }
      
          public String getPassword() {
              return password;
          }
      
          public void setPassword(String password) {
              this.password = password;
          }
      
          @Override
          public String toString() {
              return "User{" +
                      "id=" + id +
                      ", username='" + username + '\'' +
                      ", password='" + password + '\'' +
                      '}';
          }
      }
      
      ```

   4. 创建包cn.itcast.dao，创建类UserDao，提供login方法

      ```java
      /**
       * 操作数据库中User表
       */
      public class UserDao {
          //声明JDBCTemplate对象共用
          private JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
          /**
           * 登录方法
           * @param loginUser  只有用户名和密码
           * @return 包含用户名全部数据, 没有查询到，返回null
           */
          public User login(User loginUser){
      
              try {
                  //1.编写SQL
                  String sql = "select * from user where username = ? and password = ?";
                  //2.调用query方法
                  User user = template.queryForObject(sql,
                          new BeanPropertyRowMapper<User>(User.class),
                          loginUser.getUsername(), loginUser.getPassword());
                  return user;
              }catch(DataAccessException e){
                  e.printStackTrace(); //记录日志
                  return null;
              }
          }
      }
      ```

   5. 编写cn.itcast.web.servlet.LoginServlet类

   6. login.html中form表单的action路径写法

      * 虚拟目录 + servlet的资源路径

   7. BeanUtils工具类，简化数据封装

      * 用于封装JavaBean的

         1. JavaBean：标准的Java类

             	1. 要求：
             	 	1. 类必须被public修饰
             	 	2. 必须提供空参构造器
             	 	3. 成员变量必须使用private修饰
             	 	4. 提供getter与setter方法
            	2. 功能：封装数据

          	2. 概念：当成员变量的getter，Setter方法属性名与成员变量名不同时，两者不同。

            	成员变量：
      
            ​	属性：setter 和 getter 方法截取后的产物
      
            ​			例如： getUsername() ---- > Username --->  username
      
            3. 方法：
      
               	1. setProperty()：
                     	2. getProperty()：
                        	3. populate(Object obj， Map map)：将map集合的键值对信息，封装到对应的JavaBean对象中

   ### Response

   * 功能：设置响应消息

     1. 设置响应行
        1. 格式：HTTP/1.1 200 ok
        2. 设置状态吗：setStatus(int sc)
     2. 设置响应头: setHeader(String name, String value)
     3. 设置响应体:
        * 使用步骤：
          1. 获取输出流
             	* 字符输出流： PrintWriter getWriter()
             	* 字节输出流：ServletOutputSteream getOutputStream()
          2. 使用输出流，将数据输出到客户端浏览器

   * 案例：

     1. 完成重定向：

        * 重定向：资源跳转的一种方式

        * 代码：

          ```java
                  //访问/responseDemo1 会自动跳转到/responseDemo2资源
                  //1. 设置状态码302
                  response.setStatus(302);
                  //2.设置响应头location
                  response.setHeader("location","/day15/responseDemo2");
          
                  //简单的重定向方法
                  response.sendRedirect("/day15/responseDemo2");
          ```

        * 重定向的特点

          1. 地址栏发生变化
          2. 重定向可以访问其他服务器资源
          3. 重定向是两次请求，不能使用request对象共享数据

        * 转发的特点：

          1. 转发地址栏路径不变
          2. 转发只能访问当前服务器下的资源
          3. 转发是一次请求，可以使用request对象共享数据

        * forward  和 redirect区别（转发与重定向的区别）

        * 路径写法：

          1. 路径的分类：

             1. 相对路径：通过相对路径不可以确定唯一资源

                * 如：./index.html

                * 不以/ 开头，以 . 开头

                  

                * 规则：找到当前和目标资源之间的相对位置关系

                  * ./：当前目录
                  * ../：后退一级目录

             2. 绝对路径：通过绝对路径，确定唯一资源

                * 如：https://localhost/day15/respinseDemo2         /day15/respinseDemo2  
                * 以 / 开头的路径

                

                * 规则：判断定义的路径是给谁用？判断请求从哪发出
                  * 给客户端浏览器使用：需要加虚拟目录（项目的访问路径）
                    * 建议虚拟目录动态获取 ： request.getContextPath();
                    * \<a>, \<form>，重定向
                  * 给服务器用：不需要加虚拟目录 
                  * 请求转发

     2. 服务器输出字符数据到浏览器

        * 步骤：

          1. 获取字输出流
          2. 输出数据

        * 注意：

          * 乱码问题：

            1. PrintWriter pw = response.getWriter(); 获取流的默认编码为ISO-8859-1

            2. 设置该流的默认编码

            3. 告诉浏览器响应体使用的编码

               ```
               //简单的形式设置编码  并且应该在获取流之前设置
               response.setContentType("text/html;charset=utf-8");
               ```

     3. 服务器输出字节数据到浏览器

         * 步骤：
           1. 获取字输出流
           2. 输出数据

     4. 验证码

        1. 本质：图片
        2. 目的：防止恶意表单注册

   ### ServletContext对象

   1. 概念：代表整个web应用，可以和程序的容器（服务器）来通信

   2. 获取：

      1. 通过request对象获取

         ​	request.getServletContext();

      2. 通过HttpServlet获取

         ​	this.getServletContext();

   3. 功能：

      1. 获取MIME类型：

         * MIME类型：在互联网通信过程中定义的一种文件数据类型
           * 格式：大类型/小类型     text/html      image/jpeg
         * 获取：String getMimeType（String file）

      2. 域对象：共享数据

         1. setAttribute(String name, Object value)

         2. getAttribute(String name)

         3. removeAttribute(String name)

            

         * **ServletContext对象范围：所有用户的请求数据**
         * 生命周期长，不安全，谨慎使用

      3. 获取文件的真实（服务器）路径

         1. 方法：String getRealPath(String )

         ```java
                 //获取文件的服务器路径
                 String realPath = context.getRealPath("/b.txt"); //web路径下资源访问
                 System.out.println(realPath);
                 //File file = new File(realPath);
         
                 String c = context.getRealPath("/WEB-INF/c.txt");  //WED-INF目录下的资源访问
                 System.out.println(c);
         
                 String a = context.getRealPath("/WEB-INF/classes/a.txt"); //src目录下的资源访问
                 System.out.println(a);
         ```

   #### 案例：

   * 文件下载需求：
      	1. 页面显示超链接
      	2. 点击超链接后弹出下载提示框
      	3. 完成图片文件下载
   * 分析：
     1. 超链接指向的资源如果能被浏览器解析，则在浏览器中展示，如果不能解析，则弹出下载提示框。不满足需求
     2. 任何资源都必须弹出下载提示框
     3. 使用响应头设置资源的打开方式：
        * content-disposition：attachment; filename=xxx
   * 步骤：
     1. 定义页面。编辑超链接属性，指向Servlet，传递资源的名称filename
     2. 定义servlet
        1. 获取文件名称
        2. 使用字节输入流加载文件进内存
        3. 指定response的响应头content-disposition：attachment；filename=xxx
        4. 将数据写出到response输出流

   * 问题：
     * 中文文件名问题：
       * 解决思路：
         1. 获取客户端使用的浏览器版本信息
         2. 根据不同的版本信息，设置不同的filename编码方式

   ## 会话

   1. 概念：一次会话中，包含多次请求和响应
      	* 一次会话：浏览器第一次给服务器资源发送请求，会话建立，直到有一方断开为止
   2.  功能：在一次会话的范围内的多次请求间，共享数据 
   3. 方式：
      1. 客户端会话技术：Cookie
      2. 服务器端会话技术：Session

   ### Cookie

   1. 概念：客户端会话技术，将数据保存到客户端的技术

   2. 快速入门：

      * 使用步骤：
        1. 创建Cookie对象，绑定数据
           * new Cookie（String name, String value）
        2. 发送Cookie对象
           * response.addCookie（Cookie cookie）
        3. 获取Cookie，拿到数据
           * Cookie[]  = request.getCookies()

   3. 实现原理

      * 基于响应头set-cookie和  请求头cookie实现

   4. cookie的细节

      1. 一次可以发送多个cookie吗？
         * 可以
         * 可以创建多个cookie对象，使用response对象调用多次addCookie方法即可
      2. cookie在浏览器中保存多长时间？
         1. 默认情况下，浏览器关闭后，Cookie数据被销毁
         2. 持久化存储：
            * setMaxAge(int seconds)
              1. 正数：将Cookie数据写到硬盘的文件中。持久化存储。cookie存活时间。
              2. 负数：默认值
              3. 零：删除cookie信息
      3. cookie能不能存中文？
         * 在tmocat 8 之前，cookie不能直接存储中文数据。
           * 需要将中文数据转码---一般采用URL编码(%E3)
         * 在 tomcat 8 之后，cookie支持存储中文，特殊字符还是不支持，建议使用URL编码
      4. cookie获取范围多大?
         1. 假设在一个tomcat服务器中部署了多个 web 项目，那么这些web项目中的Cookie能不能共享？
            * 默认情况下不能共享
            * setPath(String path)：设置cookie的获取范围。默认情况下，设置当前的虚拟目录。
              * 如果要共享，则可以将path设置为 "/"
         2. 不同tomcat服务期间cookie共享问题？
            * setDomain(String path)：如果设置一级域名相同，那么多个服务器之间cookie可以共享
              * setDomain(".baidu.com")，那么tieba.baidu.com 和 new.baidu.com中cookie可以共享

   5. cookie的特点和作用

      1. cookie存储数据在客户端浏览器

      2. 浏览器对于单个cookie 的大小有限制(4kb)  以及 对同一个域名下的总cookie数量也有限制（20个）

         

      * 作用：
        	1. cookie一般用于存储少量且不太敏感的数据
         	2. 在不登录的情况下，完成服务器对客户端的身份识别

   6. 案例：记住上一次访问时间

      1. 需求：
         1.  访问一个Servlet，如果是第一次访问，则提示：您好，欢迎您首次访问。
         2.  如果不是第一次访问，则提示：欢迎回来，您上次访问时间为:显示时间字符串
      2. 分析：
         1. 可以采用cookie完成
         2. 在服务器中servlet判断是否有一个为latTime的cookie
            1. 有：不是第一次访问
               1. 响应数据：欢迎回来，您上首次访问时间为：
            2. 没有：不是第一次访问
               1. 响应数据：您好！欢迎首次访问
               2. 写回cookie：lastTime= 时间字符串

   ### JSP入门

   1. 概念：Java Server Pages：java服务器端页面

      * 可以理解为：一个特殊的页面，其中既可以定义html标签，又可以定义java代码
      * 用于简化书写！！！

   2. 原理：

      * JSP 本质上就是一个Servlet

   3. JSP的脚本：JSP定义Java代码的方式

      1. \<%  代码  %>：定义的java代码在service方法中。service方法中可以定义什么，该脚本就可以定义什么
      2. \<%!  代码 %>：定义的Java代码，在jsp转换后的java类的成员位置。   会出现线程安全问题，尽量不用
      3. \<%=  代码 %>：定义的java代码，会输出到页面上。输出语句中定义什么，该脚本可以定义什么。

      

   4. JSP的内置对象：

      * 在JSP页面中，不需要获取和创建，可以直接使用的对象
      * jsp一共有9个内置对象
      * 今天学习3个
        1. request
        2. response
        3. out：字符输出流对象，可以将数据输出到页面上。和response.getWriter( ) 类似
            *  response.getWriter( )  与 out.print() 区别
                *  在tomcat服务器真正给客户端做出响应前，会先找response缓冲区数据，再找out缓冲区数据
                *  response.getWriter( )数据输出永远在 out.print()之前

   ### Session

   1. 概念：服务器端会话技术，在一次会话的多次请求间共享数据，将数据保存在服务器端对象中。HttpSession

   2. 快速入门：

      HttpSession对象

       1. 获取Session对象

          HttpSession session = request.getSession();

       2. 使用Session对象

      ​		Object  getAttributr(String name)

      ​		void setAttributr(String name, Object value)

      ​		coid removeAttribute(String name)

   3. 原理：

      服务器如何确保在一次会话范围内，多次获取的Session的对象是同一个？Session是依赖于Cookie的

      * Session的实现是依赖于Cookie的。Session创建后会把id通过Cookie发送给客户端。

   4. 细节：

      1. 客户端关闭后，服务器不关闭，两次获取的Session是同一个吗？

          * 默认情况下，不是。

          * 如果需要相同，则可以创建Cookie，键为JSESSIONID，设置最大存货时间，让cookie持久化保存

            ```java
                    //期望客户端关闭后，session也能相同
                    Cookie c = new Cookie("JSESSIONID",session.getId());
                    c.setMaxAge(60*60);
                    response.addCookie(c);
            ```

      2. 客户端不关闭，服务器不关闭，两次获取的Session是同一个吗？

         * 不是同一个，服务器关闭，session对象就销毁了。但是要确保数据不丢失（tomcat已经完成，IDEA无法实现）
           * session的钝化：
             * 在服务器正常关闭前，将session对象序列化到硬盘上
           * session的活化：
             * 在服务器启动后，将session文件转化为内存中的session对象即可

      3. session是么时候销毁

         1. 服务器关闭

         2. session对象调用  invalidate()

         3. session默认失效时间30min   可以自己配置

            选择性的配置修改

            \<session-config>

            ​	\<session-timeout>30\</session-timeout>

            \</session-config>

   5. session 特点

      1. session用于存储一次会话的多次请求的数据，存在服务器端
      2. session可以存储任意类型，任意大小的数据

      * session与cookie区别
        	1. session村塾数据在服务器端，而cookie在客户端
         	2. session没有数据大小限制，cookie有
         	3. session数据相对安全，cookie数据相对不安全

      #### 案例：验证码

      1. 案例需求
         1. 访问带有验证码的登录页面login.jsp
         2. 用户输入用户名，密码以及验证码。
         	* 如果用户名和密码输入有误，跳转登录页面，提示:用户名或密码错误
         	* 如果验证码输入有误，跳转登录页面，提示：验证码错误
         	* 如果全部输入正确，则跳转到主页success.jsp，显示：用户名,欢迎您

      

      ### JSP：

       1. 指令

          * 作用：用于配置JSP页面，导入资源文件

          * 格式：

            <%@ 指令名称 属性名1=属性值1 属性名2 =属性值2.....%>

          * 分类：

            1. page：配置JSP页面的
               * contentType：等同于response.setContentType()
                 1. 设置响应体的mime类型及字符集
                 2. 设置当前jsp页面jsp编码(只能是高级的开发工具IDE，如果是低级工具，需要设置pageEncoding)
               * import：导包
               * errorPage：当前页面发生异常后，会自动跳转到指定的错误页面
               * isErrorPage：表示当前页面是否是错误页面
                 * true：是，可以使用内置对象exception
                 * false：不是，不可以使用内置对象exception
            2. include：页面包含的，导入页面的资源文件。（把相同的页面信息写成一个资源）
               * <%@include file="top.jsp"%>
            3. taglib：导入资源  标签库
               * <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
                 * prefix：前缀，自定义的

       2. 注释

          1. html注释 

             \<!-- -->：只能注释html页面

          2. jsp注释（推荐使用）

             <%-- --%>：可以注释所有

             

       3. 内置对象

          * 在jsp页面中，不需要创建，直接使用的对象

          * 一共有9个：

            ​			变量名									真实类型										作用

            * pageContext						  PageContext								当前页面共享数据，还可以获取其他八个对象
            * request                                   HttpServletRequest                     一次请求的多个资源(转发)
            * session                                    HttpSession                                   一次会话的多个请求
            * application                             ServletContext                             所有用户间共享数据
            * response                                HttpServletResponse                     响应对象
            * page                                             Object                                         当前页面对象（Servlet） this
            * out                                             JspWriter                                       输出对象，数据输出到页面上
            * config                                       ServlertConfig                                 Servlet配置对象
            * exception                                Throwable                                       异常对象

      ### MVC 开发模式

        1. jsp演变历史

             	 1. 早期只有servlet，只能使用response输出标签数据，非常麻烦
                    	 2. 有了jsp，简化了servlet开发。过度使用jsp，在jsp中既有大量java代码，又有jhtml标签，难以维护，难以分工
                           	 3. 再后来，java的web开发，借鉴mvc开发模式，使得程序设计更加合理。

      	 2. MVC：

                	 1. M：Model，模型  JavaBean
                * 完成具体的业务逻辑操作 如：查询数据库，封装对象
                	 2. V：View，视图    JSP
                * 展示数据
                	 3. C：Controller，控制器   Servlet
                   
                	 1. 获取客户端输入
                	 2. 调用模型
   	 3. 将数据交给视图展示
          
           * 优缺点：
             1. 优点：
                1. 耦合性低，方便维护，利于分工
                2. 重用性高
             2. 缺点：
          1. 使得项目架构变得复杂，对开发人员要求更高
      
### EL表达式

1. 概念：Expression Language 表达式语言
   
2. 作用：替换和简化jsp页面中java代码的编写
   
3. 语法：${表达式}
   
4. 注意：
   
         * jsp默认支持表达式。如果要忽略el表达式
           1. 设置jsp中page指令中的 isELIgnored="true"，忽略当前页面中所有的el表达式
     2. \\${el表达式}：忽略这个el表达式
     
5. 使用：
   
   1. 运算：
      
            * 运算符：
              1. 算术运算符： + - * /(div)  %(mod)
              2. 比较运算符：> < >= <= == !=
              3. 逻辑运算符：&&(and)   ||(or)  !(not)
              4. 空运算符：empty
                 * 功能：用于判断字符串，集合，数组对象是否为null并且长度是否为0
                 * ${empty list}：判断字符串，集合，数组对象是否为null 或者 长度为 0
           * ${not empty list}: 判断字符串，集合，数组对象是否不为空 并且长度 > 0
      
   2. 获取值
      
      1. el表达式只能从域对象中获取值
      
      2. 语法：
      
         1. ${域名称.键名}：从指定域中获取只当键的值
      
                  * 域名称
                    1. pageScope           --- > pageContext
                    2. requestScope      ---->request
                    3. sessionScope     ------>session
                    4. applicationScope ----->application(ServletContext)
                  * 举例：在request域中存储了 name=张三
            * 获取：${requestScope.name}
      
         2. ${键名}：表示依次从最小的域中查找是否有该键对应的值，直到找到为止
      
            ​	${键名}
      
            
      
         3. 获取对象，List集合，Map集合
      
            1. 对象：${域名称.键名.属性名}
      
               * 本质上会去调用对象的getter方法
      
            2. List集合：${域名称.键名[索引]}
      
               
      
            3. Map集合：
      
                     * ${域名.键名.key名称}
               
               * ${域名.键名["key名称"]}
      
      3. 隐式对象
      
               * el表达式中有11个隐式对象
               * pageContext：
                 * 获取jsp其他八个隐式对象
             * ${pageContext.request.contextPath}  动态获取虚拟目录
      
### JSTL

 1. 概念 ：Javaserver Pages Tag Library   JSP标准标签库
    
    * 是由Apache组织提供的开源免费的jsp标签
      
	2. 作用：用于简化和替换jsp页面上的java代码
    
    
    
	3. 使用步骤：
      
          	1. 导入JSTL相关jar包
          	2. 引入标签库： taglib指令：<%@taglib %>
    	3. 使用标签
    
	4. 常用的JSTL标签
      
    	1. if： 相当于java代码的if语句
       
              1. 属性：
                  * test 必须属性，接受boolean表达式
                      * 如果表达式为true，贼显示if标签体内容，如果为false，则不显示标签体内容
            * 一般情况下，test属性值会结合el表达式疫情使用
       
        2. 注意： c: if 标签没有else情况 想要else的话，就再定义一个标签
       
    	2. choose：相当于java代码的switch语句
       
              	1. 使用coose标签取出数字           相当于switch声明
              	2. 使用when标签做数字判断           相当于case
         	3. otherwise标签做其他情况的声明  相当于default
       
    	3. foreach：相当于java代码的for语句
       
              1.完成重复操作
                  for(int i = 0; i < 10; i++){}
                  *  属性：
                      begin：开始值
                      end：结束值
                      var：临时变量
                      step：步长
                      varStatus: 循环状态对象
                             index: 容器中元素索引，从0开始
                             count: 循环次数，从1开始
              2.遍历容器
              	Lsit<User> list;
                for(User user : list){}
              
              * 属性
                  items： 容易对象
            var：容器中元素的临时变量
      
	5. 练习：
    
    需求：再request域中存有一个User对象的List集合，需要使用 jstl+el 将list集合展示到jsp页面的表格table中
    
### 三层架构: 软件设计架构

      	1. 界面层(表示层/web层): 用户看到的界面。用户可以通过界面上的组件和服务器进行交互：接收用户参数，封装数据，调用业务逻辑层完成出列，转发jsp页面完成显示。  **cn.itcast.项目名.web**   SpringMVC框架
      	2. 业务逻辑层(service层)：处理业务逻辑的。组合DAO层中的简单方法，形成复杂的功能(业务逻辑操作) **cn.itcast.项目名.service**      Spring框架
    3. 数据访问层(dao层  Data Access Object)：操作数据存储文件的。 定义了对于数据库最基本的CRUD操作   **cn.itcast.项目名.dao**      MyBatis框架

#### 案例：用户信息查询列表展示

 1. 需求：用户信息的增删改查操作
    
 2.  设计：
     
     1. 技术选型：Servlet + JSP + MySQL + JDBCTempleat + Duird + BeanUtilS + tmcat
     
     2. 数据库设计：
     
              ```sql
              CREATE DATABASE day17;   -- 创建数据库
              USE day17;	    	 -- 使用数据库
              	
              CREATE TABLE USER(	 -- 创建表
              	id INT PRIMARY KEY AUTO_INCREMENT,
              	NAME VARCHAR(20) NOT NULL,
              	gender VARCHAR(5),
              	age INT,
              	address VARCHAR(32),
              	qq VARCHAR(20),
              	email VARCHAR(50)	
              );
        ```
        
        ```
     
 3. 开发
    
           	1. 环境搭建
                	1. 创建数据库环境
                	2. 创建项目，导入需要的jar包
                	2. 编码
      
 4. 测试
    
 5. 部署运维

分页的好处：

	1. 减轻内存开销
	2. 提升用户体验

### Filter与Listener

#### Filter 过滤器

1. 概念

   * web中的过滤器：当访问服务器的资源时, 过滤器可以将请求拦截，完成一些特殊的功能
   * **过滤器的作用**：
     * 一般用于完成通用的操作。 如：登录校验，统一编码处理， 敏感字符过滤...

2. 快速入门：

   1. 步骤：

      1. 定义一个类，实现接口Filter
      2. 复写方法
      3. 配置拦截路径
         1. web.xml
         2. 注解配置

      ```java
      /**
       * 过滤器快速入门
       */
      @WebFilter("/*")//访问所有资源前，都会执行该过滤器
      public class FilterDemo1 implements Filter {
          @Override
          public void init(FilterConfig filterConfig) throws ServletException {
      
          }
      
          @Override
          public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
              System.out.println("FilterDemo1被执行了......");
      
              //放行
              filterChain.doFilter(servletRequest,servletResponse);
          }
      
          @Override
          public void destroy() {
      
          }
      }
      ```

      

3. 过滤器细节

   1. web.xml

      ```java
          <filter>
              <filter-name>demo1</filter-name>
              <filter-class>cn.itcast.web.filter.FilterDemo1</filter-class>
          </filter>
          <filter-mapping>
              <filter-name>demo1</filter-name>
              <url-pattern>/*</url-pattern>
          </filter-mapping>
      ```

   2. 过滤器执行流程

      1. 执行过滤器
      2. 执行放行后的资源
      3. 回来执行过滤器放行代码下的代码

   3. 过滤器生命周期方法

      1.  init : 在服务器启动后，会创建Filter对象，然后调用init方法，执行一次，用于加载资源
      2. doFilter: 每一次请求被拦截资源时，会执行。执行多次
      3.  destroy： 服务器关闭后，Filter对象被销毁，如果服务器正常关闭，则会执行方法。执行一次，用于释放资源

   4. 过滤器配置详解

      * 拦截路径配置：
        1. 具体资源路径：/index.jsp   只有访问index.jsp 资源，过滤器才会被执行
        2. 拦截目录：/user/*  访问/user下的所有资源，过滤器都会被执行
        3. 后缀名拦截：*.jsp   访问所有jsp资源时，过滤器都会被执行
        4. 拦截所有资源：/*    访问所有资源时，过滤器都会被执行
      * 拦截方式配置：资源被访问的方式
        * 注解配置：
          * 设置：dispatcherTypes属性
            1. REQUEST: 默认值. 浏览器直接请求资源
            2. FORWARD: 转发访问资源
            3. INCLUDE: 包含访问资源
            4. ERROR: 错误跳转资源
            5. ASYNC: 异步访问资源
        * web.xml配置
          * 设置; \<dispatcher>\</dispatcher>标签即可

   5. 过滤器链(配置多个过滤器)

      * 执行顺序：如果有两个过滤器：过滤器1和过滤器2

        1. 过滤器1
        2. 过滤器2
        3. 资源执行
        4. 过滤器2
        5. 过滤器1

      * 过滤器先后顺序问题：

        1. 注解配置：按照类名的字符串比较规则比较，值小的先执行

           ​	* 如 AFilyer 和 BFilter ，AFilyer 先执行了

        2. web.xml配置：\<filter-mapping>谁定义在上，谁先执行

4. 案例：

   1. 案例_登录验证：
      * 需求：
        1. 访问day17_case案例的资源。验证其是否登录
        2. 如果登录了，则直接放行。
        3. 如果没有登录，则跳转到登录页面，提示"您尚未登录，请先登录"。
   2. 案例2_敏感词汇过滤
      * 需求：
         	1. 对day17_case案例录入的数据进行敏感词汇过滤
         	2. 敏感词汇参考《敏感词汇.txt》
         	3. 如果是敏感词汇，替换为 *** 
      * 分析：
        1. 对request对象进行增强。增强获取参数的相关方法
        2. 放行，传递代理对象
      * 增强对象的功能：
        * 设计模式：一些通用的解决固定问题的方式
          1. 装饰模式：
          2. 代理模式：
             * 概念：
               1. 真实对象：被代理的对象
               2. 代理对象：
               3. 代理模式：代理对象代理真实对象，达到增强真实对象功能的目的
             * 实现方式：
               1. 静态代理：有一个类文件描述代理模式
               2. 动态代理：再内存中形成代理类
                  * 实现步骤：
                    1. 代理对象和真实对象实现相同的接口
                    2. 代理对象 = Proxy.newProxyInstance();
                    3. 使用代理对象带哦用方法。
                    4. 增强方法
                  * 增强方式：
                    1. 增强参数列表
                    2. 增强返回值类型
                    3. 增强方法体执行逻辑

### Listener 监听器

* 概念：web三大组件之一。

  * 事件监听机制
    * 事件：一件事情
    * 事件源：事件发生的地方
    * 监听器：一个对象
    * 注册监听：将事件，事件源，绑定在一起。当事件源上发生某个事件后，执行监听器代码

* ServletContextListener: 监听ServletContext对象的创建和销毁

  * 方法

    * void contextDestroyed(ServletContextEvent sce)：ServletContext对象被销毁之前会调用该方法
    * void contextInitialized(ServletContextEvent sce)；ServletContext对象创建后会调用该方法

  * 步骤：

    1. 定义一个类，实现ServletContextListener接口

    2. 复写方法

    3. 配置

       1. web.xml配置

          * ```xml
            	<listener>
                    <listener-class>cn.itcast.web.Listener.ContextLoaderListener</listener-class>
                </listener>
            
                <!--指定初始化参数信息-->
                <context-param>
                    <param-name>contextConfigLocation</param-name>
                    <param-value>/WEB-INF/classes/applicationContext.xml</param-value>
                </context-param>
            ```

       2. 注解配置

          * @WebListener

### JQuery

1. 概念：一个JavaScript框架。简化JS开发

   * jQuery是一个快速、简洁的JavaScript框架，是继Prototype之后又一个优秀的JavaScript代码库（*或JavaScript框架*）。jQuery设计的宗旨是“write Less，Do More”，即倡导写更少的代码，做更多的事情。它封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML文档操作、事件处理、动画设计和Ajax交互。
   * JavaScript框架：本质上就是一些js文件，封装了js原生代码

2. 快速入门

   1. 步骤：

      1. 下载JQuery

         * 目前jQuery有三个大版本：
           	1.x：兼容ie678,使用最为广泛的，官方只做BUG维护，
           		 功能不再新增。因此一般项目来说，使用1.x版本就可以了，
           		 最终版本：1.12.4 (2016年5月20日)
           	2.x：不兼容ie678，很少有人使用，官方只做BUG维护，
           		 功能不再新增。如果不考虑兼容低版本的浏览器可以使用2.x，
           		 最终版本：2.2.4 (2016年5月20日)
           	3.x：不兼容ie678，只支持最新的浏览器。除非特殊要求，
           		 一般不会使用3.x版本的，很多老的jQuery插件不支持这个版本。
           		 目前该版本是官方主要更新维护的版本。最新版本：3.2.1（2017年3月20日）
         * jquery-xxx.js与jquery-xxx.min.js
           1. jquery-xxx.js: 开发版本，给程序员看，良好的缩进和注释
           2. jquery-xxx.min.js：生产版本。程序中使用，没有缩进。体积小一些，程序加载更快

      2. 导入JQuery的js文件：导入min.js文件

      3. 使用

         ```js
         var $divs = $("div");
         alert($divs.length); //也可以当作数组来使用
         ```

3. JQuery对象和JS对象的区别与转换

   1. JQuery对象在操作时更加方便。
   2. JQuery对象和Js对象方法是不通用的
   3. 两者相互转换
       * jq-->js：jq对象[索引]  或者 jq对象.get(索引)
       * js-->jq：$(js对象)

4. 选择器：筛选具有相似特征的元素（标签）

   1. 基本的语法学习：

      1. 事件绑定

         ```js
             $(function () {
                 $("#b1").click(function () {
                     alert("abc");
                 });
             });
         ```

      2. 入口函数（js中的onload函数）

         ```js
         window.onload  和 $(function)区别
             * window.onload 只能定义一次，如果定义多次，后面的会覆盖前面的
             * $(function) 可以定义多次
         ```

      3. 样式控制

         ```js
         $(function () {
             //$("#div1").css("background-color","red");
             $("#div1").css("backgroundColor","pink");
         });
         ```

   2. 分类

      1. 基本选择器
         1. 标签选择器（元素选择器）
            * 语法：$("html标签名") 获得所有匹配标签名称的元素（TagName）
         2. id选择器
            * 语法：$("#id的属性值")获得与指定id属性值匹配的元素（Id）
         3. 类选择器
            * 语法：$(”.class的属性值“) 获得与指定的class属性值匹配的元素
         4. 并集选择器
            * 语法：$(”选择器1，选择器2“) 获得多个选择器选中的所有元素
      2. 层级选择器
         1. 后代选择器 A B 为 标签名
            * 语法：$("A B")  选择A元素内部的所有B元素
         2. 子选择器
            * 语法：$("A > B")  选择A元素内部的所有B子元素
      3. 属性选择器
         1. 属性名称选择器 A 为 标签名
            * 语法：$("A[属性名]") 包含指定属性的选择器
         2. 属性选择器
            * 语法：$("A[属性名='值']") 包含指定属性等于指定值的选择器
         3. 符合选择器
            * 语法：$("A[属性名=‘值’]\[]...") 包含多个属性条件的选择器
      4. 过滤选择器
         1. 首元素选择器
            * 语法：:first 获得选择元素中的第一个元素
         2. 尾元素选择器
            * 语法：:last 获得选择的元素中最后一个元素
         3. 非元素选择器
            * 语法：:not(selecter) 不包括指定内容的元素
         4. 偶数选择器
            * 语法：:event 偶数，从0开始计数
         5. 奇数选择器
            * 语法：:odd 奇数，从0开始计数
         6. 等于索引选择器
            * 语法：:eq(index) 指定索引元素
         7. 大于索引选择器
            * 语法：:gt(index) 大于指定索引元素
         8. 小于选择器
            * 语法：:lt(index) 小于指定索引元素
         9. 标题选择器
            * 语法：:header 获得标题(h1~h6)元素，固定写法
      5. 表单过滤选择器
         1. 可用元素选择器
            * 语法：:enabled 获得可用元素
         2. 不可用元素选择器
            * 语法：:disabled 获得不可用元素
         3. 选中选择器
            * 语法：:checked 获得单选/复选框选中的元素
         4. 选中选择器
            * 语法：:selected 获得下拉框选中的元素

5. DOM操作

   1. 内容操作

      1. html()：获取/设置元素的标签体内容 \<a>\<font>内容\</font>\</a>   ---> \<font>内容\</font>
      2. text()：获取/设置元素的标签体纯文本内容 \<a>\<font>内容\</font>\</a>  -----> 内容
      3. val()：获取/设置元素的value属性值

   2. 属性操作

      1. 通用属性操作

         1. attr()：获取/设置元素的属性
         2. removeAttr()：删除属性
         3. prop()：获取/设置元素的属性
         4. removeProp()：删除属性

         * attr  和 prop 区别
           1. 如果操作元素的固有属性，则建议使用prop
           2. 如果操作的是元素自定义属性，则建议使用attr

      2. 对class属性操作

         1. addClass()：添加class属性值
         2. removeClass()：删除class属性值
         3. toggleClass()；切换class属性
            * toggleClass(“one”)：判断元素对象上存在class = “one”，则将属性值one删除。   如果元素对象上不存在class = “one”，则添加
         4. css();

   3. CRUD操作

      1. append()：父元素将子元素追加到末尾

         * 对象1.append(对象2)：将对象2添加到对象1元素内部，并且在末尾

      2. prepend()：父元素将子元素追加到开头

         * 对象1.prepend(对象2)：将对象2添加到对象1元素内部，并且在开头

      3. appendTo()：

         * 对象1.appendTo(对象2)：将对象1添加到对象2元素内部，并且在末尾

      4. prependTo()：

         * 对象1.prependTo(对象2)：将对象1添加到对象2元素内部，并且在开头

         

      5. after()：添加元素到元素的后边

         * 对象1.after(对象2)：将对象2添加到对象1后面，对象1和对象2是兄弟关系

      6. before()：

         * 对象1.before(对象2)：将对象2添加到对象1前面，对象1和对象2是兄弟关系

      7. insertAfter：

         * 对象1.insertAfter(对象2)：将对象1添加到对象2后面，对象1和对象2是兄弟关系

      8. insertBefore：

         * 对象1.insertAfter(对象2)：将对象1添加到对象2前边，对象1和对象2是兄弟关系

      9. remove():  移除元素

         * 对象.remove()：将对象删除

      10. empty(): 清空元素的后代元素

          * 对象.empty()：将对象的后代元素全部清空，但是保留当前对象以及其属性结点

6. 案例

### JQuery高级

1. 动画
   1. 三种方式显示和隐藏元素
      1. 默认显示和隐藏的方式
         1. show([speed],[easing],[fn])
            1. 参数：
               1. speed：动画的速度 三个预定义的值（"slow","normal","fast"）
               2. easing：用来指切换效果，默认是”swing“，可用参数”linear“
                  * swing：动画执行时的效果是 先慢，中间快，最后又慢
                  * linear：动画执行时速度是匀速的
               3. fn：在动画完成时执行的函数，每个元素执行一次。
         2. hide([speed],[easing],[fn])
         3. toggle([speed],[easing],[fn]) //切换
      2. 滑动显示和隐藏方式
         1. slideDown([speed],[easing],[fn])
         2. slideUp([speed],[easing],[fn])
         3. slideToggle([speed],[easing],[fn])
      3. 淡入淡出显示和隐藏方式
         1. fadeIn([speed],[easing],[fn])
         2. fadeOut([speed],[easing],[fn])
         3. fadeTogle([speed],[easing],[fn])

2. 遍历

   1. js遍历方式

      * for(初始化值；循环结束条件；步长)

   2. jq遍历方式

      1. jq对象.each(callback)

         1. 语法：

            jq对象.each(function (index, element){}）；

            * index: 就是元素集合中的索引
            * element：就是集合中的每一个元素对象
            * this：集合中的每一个元素对象

         2. 回调函数返回值

            * 如果当前function返回为false，则结束循环(break)
            * 如果返回为true，则结束本次循环，继续下次循环(false)

      2. $.each(object,[callback])

      3. for..of

         * for(元素对象  of 容器对象)

3. 事件绑定

   1. jquery标准的绑定方式

      jq对象.事件方法(回调函数)；

      * 注：如果调用事件方法，不传回调函数，会触发浏览器默认行为
        * 表单对象.submit()；//让表单提交

   2. on绑定事件/off解除绑定

      jq对象.on("事件名称",回调函数)

      jq对象.off("事件名称")

      ​	*  如果off方法不传递任何参数，则将组件上所有的事件全部删除

   3. 事件切换：toogle

      jq对象.toogle(fn1,fn2....)

      	* 当单机jq对象对应的组件后，会执行fn1。再次点击会执行fn2.....
      	* 注意：1.9版本后 toggle() 方法删除，jQuery Migrate(迁移) 插件可以恢复此功能

4. 案例：见day21_JQuery高级 04-JQuery综合案例

5. 插件：增强JQuery的功能

   1. 实现方式：
      1. $.fn.extend(object)
         * 增强通过Jquery获取的对象的功能  $("#id")
      2. $.extend(object)
         * 增强JQuery对象自身的功能  $/jQuery



































   




