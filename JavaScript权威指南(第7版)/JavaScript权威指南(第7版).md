# JavaScript权威指南

[toc]

> JavaScript简介: 
>
> - JavaScript是一门高级、动态、解释型语言
>
> - 保存JavaScript代码的文件通常使用扩展名 .js
>
> - console.log() 函数在终端窗口或在浏览器开发者工具的控制台中显示文本和其他JavaScript值



## 一、基础语法



### 1. 词法结构

#### （1）JavaScript程序的文本

- （1）JavaScript**区分大小写**
- （2）JavaScript将常规空格、制表符、ASCII控制符、Unicode间格识别为**空格**
- （3）JavaScript将换行符、回车符和回车/换行序列识别为**行终止符**

#### （2）注释

- **单行注释**
  - 以 **//** 开头到一行末尾的内容 
- **多行注释**
  - 位于 **/*** 和 ***/**之间，可以跨行，不能嵌套

```js
// 单行注释
/* 注释 */
/*
 * 多行注释
 * 每行开头的*不是必须的，只是为了美观
 */
```

#### （3）字面量

> 是一种直接出现在程序中的**数据值**

```js
// 以下都是字面量
12
1.2
"hello"
'world'
true
false
null
```

#### （4）标识符和保留字

- **标识符**
  - 就是一个名字
  - 用于在JavaScript代码中命名常量、变量、属性、函数和类，以及为循环提供标记
  - 命名规则
    - 必须以字母、下划线__或美元符$开头
    - 数字不能作为第一个字符
- **保留字**
  - 为语言自身使用而保留的一些标识符
  - 不能作为标识符使用

```js
as			const			export			get				null			target			void	
async		continue		extends			if				of				this			while
await		debugger		false			import			return			throw			with
break		default			finally			in				set				true			yield
case		delete			for				instanceof		static			try
catch		do				from			let				super			typeof	
class		else			function		new				switch			var
```

​		js也保留或限制某些关键字的使用，这些关键字当前未被语言所用，但将来可能使用

```js
enum	implements		interface	package		private		protected	public
```

#### （5）Unicode

- JavaScript程序是使用Unicode字符集编写的
- 在字符串和注释中可以使用任意Unicode字符
- 建议（可移植性和易编辑）
  - 在标识符中只使用ASCII字母和数字
- Unicode转义序列
  - 以 \u 开头
  - 后跟4位十六进制数字(包括大写或小写的字母A-F)，或包含在一对花括号内的1~6位十六进制数字

#### （6）可选分号

- ; 用于分隔语句
  - 如果两条语句分别写在两行，通常可以省略分号
  - 在程序末尾，如果接下来的记号是 } ，也可以省略分号
- JavaScript只在下一个非空格字符无法被解释为当前语句的一部分时才把换行符当做分号



### 2. 类型、值和变量

> JavaScript类型分为：
>
> 1. 原始类型
>    1. 数值（例如：1、1.1）
>    2. 字符串（例如：'hello'、“world”）
>    3. 布尔值（true、false）
>    4. null
>    5. undefined
> 2. 对象类型
>    1. 对象：是属性的集合，例如：{name: 'zs'}
>    2. 数组：表示一个数字值得有序集合，例如：[1, 2, 3]

#### （1）数值

> JavaScript的主要数值类型Number用于表示整数和近似实数
>
> 当数值真正出现在JavaScript程序中时，就叫做数值字面量

- **整数字面量**

```js
// 10进制整数字面量
0
3
1000
// 十六进制整数字面量：以0x或0X开头后面跟十六进制数字字符串 0-9、A-F、a-f
0xff	// => 255: (15*16 + 15)
0xBADCAFE
// ES6增加二进制和八进制表示整数
0b10101		// => 21: (1*2**4 + 0*2**3 + 1*2**2 + 0*2**1 + 1*2**0) 二进制
0o377		// => 255：（3*8**2 + 7*8**1 + 7*8**0）八进制
```

- **浮点字面量**

```js
3.14
.333
6.02e23		// 6.02 × 10^23
1.47E-32	// 1.47 × 10^（-32）
```

- **数值字面量中的分隔符**

```js
// 可以用下划线将数值字面量分隔为容易看清的数字段
let billion = 1_000_000_000;	// 以下划线作为千分位分隔符
let bytes = 0x89_AB_CD_EF;		// 作为子节分隔符
let bits = 0b0001_1101_0111;	// 作为半字节分隔符
let fraction = 0.123_456_789;	// 作为小数分隔符
```

- **JavaScript中的算术**

> 算术操作符操作数值：+    -    *    /    %    **
>
> Math对象的属性提供了函数和常量操作复杂计算
>
> ```js
> Math.pow(2, 53)					// => 9007199254740992: 2的53次方
> Math.round(.6)					// => 1: 舍入到最接近的整数
> Math.ceil(.6)					// => 1：向上舍入到一个整数
> Math.floor(.6)					// => 0: 向下舍入到一个整数
> Math.abs(-5)					// => 5: 绝对值
> Math.max(x, y, z)				// 返回最大值 
> Math.min(x, y, z)				// 返回最小值
> Math.random()					// 伪随机数x，0≤x<1 
> Math.PI							// π: 圆周率
> Math.E							// e: 自然对数的底数
> Math.sqrt(3)					// => 3**0.5: 3的平方根 
> Math.pow(3, 1/3)				// => 3**(1/3): 3的立方根
> Math.sin(0)						// 三角函数：还有Math.cos、Math.atan
> Math.log(10)					// 10的自然对数
> Math.log(100)/Math.LN10			// 以10为底100的对数
> Math.log(512)/Math.LN2			// 以2为底512的对数
> Math.exp(3)						// Math.E的立方
> 
> // es6 Math对象新增函数
> Math.cbrt(27)					// => 3: 立方根
> Math.hypot(3, 4)				// => 5: 所有参数平方和的平方根
> Math.log10(100)					// => 2: 以10为底的对数
> Math.log2(1024)					// => 10: 以2为底的对数
> Math.log1p(x)					// (1+x)的自然对数，精确到非常小的x
> Math.expm1(x)					// Math.exp(x)-1
> Math.sign(x)					// 对 < == 或 >0 的参数返回-1、0、1
> Math.imul(2, 3)					// => 6: 优化的32位整数乘法
> Math.clz32(0xf)					// => 28: 32位整数中前导0的位数
> Math.trunc(3.9)					// => 3: 剪掉分数部分得到的整数
> Math.fround(x)					// 舍入到最接近的32位浮点数
> Math.sinh(x)					// 双曲线正弦，还有Math.cosh()和Math.tanh()
> Math.asinh(x)					// 双曲线反正弦，还有Math.acosh()和Math.atanh()
> ```
>
> - JavaScript中的算术在遇到上溢出、下溢出或被零除时不会发生错误
>   - 上溢出结果：Infinity
>   - 下溢出结果：-Infinity
> - 0除0没有意义，返回结果为 NaN
>
> ```js
> // es6定义了下列Number属性
> Number.parseInt()			// 同全局的parseInt()函数
> Number.ParseFloat()			// 同全局的parseFloat()函数
> Number.isNaN(x)				// 判断x是不是NaN
> Number.isFinite(x)			// 判断x是数值还是无穷
> Number.isInteger(x)			// 判断x是不是整数
> Number.isSafeInteger(x)
> Number.MIN_SAFE_INTEGER		// => -(2**53 - 1)
> Number.MAX_SAFE_INTEGER		// => 2**53 -1
> Number.EPSILON				// => 2** -52: 数值与数值之间最小差
> ```
>
> - 非数值和任何值比较都不相等， 也不等于自己
>
>   
>
> - es6 新增数值类型**BigInt**
>
>   - 主要是为了表示64位整数
>   - 字面量写作一串数字后跟小写字母n
>   - ` 1234n` 、 ` 0b1111n`、 ` 0o7777n` 、` 0xffffn`
>   - 可以使用 BigInt() 函数把数值或字符串转换为 BigInt 值
>
> - 日期和时间
>
>   ```js
>   let timestamp = Date.now();		// 当前时间的时间戳 1617170547993
>   let now = new Date();			// 当前时间的日期对象 Date Wed Mar 31 2021 14:02:27 GMT+0800 (中国标准时间)
>   let ms = now.getTime();			// 转换为毫秒时间戳 1617170547993
>   let iso = now.toISOString();	// 转换为标准格式的字符串 "2021-03-31T06:02:27.993Z"
>   ```



#### （2）文本





### 3. 表达式和操作符

### 4. 语句

### 5. 对象

### 6. 数组



## 二、高级语法

### 1. 函数

### 2. 类

### 3. 模块

### 4. 标准库

### 5. 迭代器和生成器

### 6. 异步JavaScript

### 7. 元编程



## 三、js应用

### 1. 浏览器中的JavaScript

### 2. Node服务器端JavaScript

### 3. JavaScript工具和扩展



### 



