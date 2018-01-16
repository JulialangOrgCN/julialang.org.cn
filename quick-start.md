# [快速上手][3] #

## 约定 ##
- 朱莉娅：Julia
- 派森：Python（另一种广泛应用的、语法自然的编程语言）
- 位：一个仅能保持高低电瓶的门电路（高表示“1”、低表示“0”，也可能反着规定，对应内存中一个比特）
  - 字节
  - 字
  - 字长
  - Int64
  - Int32
- 整型：所有的整数（-7、0、1、2012）

朱莉娅是易理解的（homoiconic）函数式的（编程）语言，专注技术计算。
由于具备易理解的宏、一流的函数、低层的控制等全部全部能力，朱莉娅像派森一样易学易用。

## 语法 ##
### 注释 ###
- 单行

	`# 这是一行注释，以“#”开始、以换行结束。`

- 多行

	`#= 这是一段注释，以“#=”开始；`

	`继续注释；`

	`以“=#”结束。 =#`

### 基本类型及其运算 ###
**朱莉娅的一切都是表达式**

- 数值类型

	9527 # => 9527 Int64 六十四位整型

	9527.9527 # => 9527.9527 Float64 六十四位浮点

	9527 + 9527im # => 9527 + 9527im Complex{Int64} 实部和虚部都是六十四位整型的复数

	[1314//9527 # => 1314//9527 Rational{Int64} 六十四位整型的有理数][0]

- 数值运算

	1314 + 9527 # => 10841 加法

	9527 - 1314 # => 8213 减法

	1314 * 9527 # => 12518478 乘法

	9527 / 1314 # => 7.250380517503805 除法

	9527 \ 1314 # => 0.13792379552849796 整型除法 **相当于“1314 / 9527”**

	2 ^ 2 # => 4 幂

	9527 % 1314 # => 329 取余

- [按位运算][1]

	~9527 # => -9528

	1314 & 9527 # => 1314

	1314 | 9527 # => 9527

	1314 ⊻ 9527 # => 8213

	8 >>> 2 # => 2

    8 >> 2 # => 2

	-8 >>> 2 # => 4611686018427387902 逻辑右移

	-8 >> 2 # => -2

	1 << 2 # => 4 算数左移

	-1 << 2 # => -4 算数左移

	1 << 62 # => 算数左移

	-1 << 62 # => 算数左移

	1 << 63 #=> -9223372036854775808 溢出

	-1 << 63 # => -9223372036854775808 算数左移

	1 << 64 # => 0 逻辑左移

	-1 << 64 # => 0 逻辑左移

- 布尔类型

	true

	false

- 布尔运算

	!true # => false 否

    !false # => true 否

	1314 == 1314 # => true

	1314 == 9527 # => false

	1314 != 1314 # => false

	1314 != 9527 # => true

	1314 < 9527 # => true

	1314 > 9527 # => false

	1314 <= 9527 # => true

	1314 >= 9527 # => false

	1 < 2 < 3 # => true

	1 < 3 < 2 # => false

	1 < 3 > 2 # => true

- 字符类型

	'$' # => 字符

- 字符序列类型

	"this is string" # => 英文半角双引号包裹起来
  - ASCIIString
  - UTF8String

- 字符序列运算

	"this is string"[1] # => 索引 **序列在Julia中的索引从一开始**

	"1314 + 9527 = $(1314 + 9527)" # => "1314 + 9527 = 10841" 美刀符号（$）可以用于在字符序列中插值（可以在圆括号内放入任何表达式）

	@printf "%d is less than %f" 1314.0 9527.0 # => 1314 is less than 9527.000000 字符序列格式化宏

	"julia" > "bob" # => true

	"j" > "bob" # => true **字符序列的比较按照字典秩序进行**

	"julia" == "julia" # => true

	"1314 + 9527 = 10841" == "1314 + 9527 = $(1314 + 9527)" # => true 字符序列中的插值表达式总是先执行

- 内建函数

	div(9527,1314) # => 7 去尾除法

	bits(1314) # => 0000000000000000000000000000000000000000000000000000010100100010 六十四位整型的二进制序列

	bits(1314.0) # => 0100000010010100100010000000000000000000000000000000000000000000 六十四位浮点（的科学计数法）的二进制序列

	println("here is julialang.org.cn") # => 标准输出

	typeof(9527) # => Int64 获取对象类型

	subtypes(Number) # => [Complex, Real] 获取子类

	supertype(String) # => AbstractString 获取亲类

- 内建标识
  - 关键字
  - 特殊符

		π # => 圆周率

- 命名规则
  - 标识符以字母或下划线开头并由字母下划线数字感叹号组成
  - 变量名可以通过下划线明确单词分隔，除非多歌单词难以阅读，否则不鼓励用下划线
  - 类型名用大驼峰（CamelCase）替代下划线作分隔
  - 函数（包括宏）名全部小写，不用下划线（必须一个单词表明意图）
  - 可能修改输入的函数名以感叹号结尾，这种函数叫做“mutating”或“in-place”

		array = [9, 5, 2, 7]

		sort(array) # => [2,5,7,9] 对数组array排序（默认升序）返回排序后的新数组

		sort!(array) # => [2,5,7,9] 对数组array排序（默认升序）返回排序后的数组array **对数组array本身做了修改**

- 变量

	av = 9527

	_av7 = "1314"

	_av_7 = 9527

	av_7_! = 1314

	￥ = 9527 # => 甚至可以用Unicode字符

- 数组类型（列表）

	array = Int64[] # => 空六十四位整型数组

	array = [1314, 9527] # => 两个元素的一维六十四位整型数组

	array = [1314; 9527] # => 两个元素的一维六十四位整型数组

	matrix = [1314 9527; 9527 1314] # => 四个元素的二维六十四位整型数组

	array = Int8[1, 3, 1, 4] # => 四个元素的一维八位整型数组

	array = [1:5;] # => 五个元素的一维六十四位整型数组 **切记有个分号**

- 数组运算

	a = [9, 5, 2, 7] # => 定义一维数组a

	b = [9; 5; 2; 7] # => 定义一维数组b

	a[1] # => 9 索引数组a的第一个元素

	a[end] # => 7 索引数组a的最后一个元素

	a[2:end] # => [5, 2, 7] 通过range索引数组a的第二个（含）到最后一个（含）元素

	push!(a, 1) # => [9, 5, 2, 7, 1] 向数组a追加一个元素1并返回a

	append!(a, b) # => [9, 5, 2, 7, 1, 9, 5, 2, 7] 把数组b中的所有元素按原有顺序依次追加到数组a中

	pop!(b) # => 返回并删除数组b的最后一个元素

	shitf!(a) # => 返回并删除数组a的第一个元素9 此时数组a变成[5, 2, 7, 1, 9, 5, 2, 7]

	unshift!(a, 4) # => 把4插入到数组a的开始并返回a 此时数组a变成[4, 5, 2, 7, 1, 9, 5, 2, 7]

	splice!(a, 2) # => 删除数组a的第二个元素 删除指定索引的元素

	in(9, a) # => 判断数组a中是否存在9这个元素 返回true/false

	length(a) # => 获取数组a元素的数量

- 元组：不可修改的数组

	tup = (1, 3, 1, 4) # => 四个元素的六十四位整型元组

	tup = 1, 3, 1, 4 # => 可以省略英文版叫圆括号

	tup[1] tup[end] tup[2:end] length(tup) in(3, tup)

	a, b, c, d = tup # => 解包

	tup[2] = 888 # => LoadError: MethodError: no method matching setindex!

	tup = (7,) # => 只有一个元素的元组 **和tup=(7)不同**

	a, b, c, d = d, c, b, a # => 通过元组可以方便的做交换

- 字典类型

	emptyd = Dict()

	d = Dict("9"=>9, "5"=>5, "2"=>2, "7"=>7)

- 字典运算

	d["9"] # => 9 根据键获取值

	keys(d) # => Iterator 遍历可以得到"9","5","2","7" 键的顺序和初始化或插入顺序无关

	values(d) # => Iterator 遍历可以得到9,5,2,7 值的顺序由键的顺序决定

	in("9"=>9, d) # => 判断字典d中是否存在以"9"为键且以9为值的元素

	haskey(d, "9") # => 判断字典中是否存在"9"这个键

	get(d, "9", 9) # => 避免用d["9"]当字典d中不存在"9"这个键时报错（KeyError）——用默认返回值9代替

- 集合类型

	emptyset = Set()

	set = Set([9, 5, 2, 7])

	set_ = Set([1, 3, 1, 4, 888])

- 集合运算

	push!(set, 888)

	in(888, set)

	intersect(set, set_) # => 888 交集

	union(set, set_) # => 9,5,2,7,1,3,4,888 并集

	setdiff(set, set_) # => 9,5,2,7,1,3,4 差集

- 异常处理

	try

		any expression

	catch e

		println(e)

	end

- 异常类型
  - 内建

		UndefValError # => 未定义的变

		BoundsError # => 越界

		MethodError # => 未定义的方法

		KeyError # => 不存在的键

  - 定制

- 流程控制
  - if elseif else end
  - for

	dogs = ["sm", "im"] # => 定义一个数组

	for dog = dogs

		println("$dog fucks bitch")

	end

	for dog in dogs # => 可以用in替代=

	for k in Dict("sm"=>"dog", "im"=>"dog") # => 可以遍历字典的键（在通过键获取值）

	for (k, v) in Dict("sm"=>"dog", "im"=>"dog") # => 可以同时遍历字典的键值

  - while

- 函数

	function  fuck(who, whom)

		do something

		return what # => 可以用都好分隔同时返回多个

	end

	function fucking(those...) # => 多个入参放入those元组

	fuck(("sm", "im")...) # => 可以给普通占位入参这样初始化

	function fucked(x, y, z="bitch") # => 可以定义可选的初始化入参

	fucked("sm", "im") # => OK

	fucked("sm", "im", "bawdy") # => OK

	fucked("wanton") # => **UndefValError 未定义的变量**

	function fuckoff(x, y, z="bitch"; k="key-parameter") # => 其中x/y是普通占位入参、z是可选的初始化入参、z是键入参

- 函数式编程：朱莉娅中函数式一等公民

	function outer(x)

		inner = function(y)

			return x + y

		end

		return inner

	end

  - (f -> f > 0)(9527) # => true # => Lambda
  - inner --- f -> x + f # => outter --- ?
  - map(f -> f + 888, [9, 5, 2, 7])
  - filter(f -> f > 0, [9, -5, 2, -7])
  - [(f -> f * 7)(i) for i in [9, 5, 2, 7]] # => 数组解析

- 类型
  - 任何对象都有类型
  - 变量自身是没有类型的
  - 任何类型都有且仅有一个亲类型

	DataType # => 表示类型（包括自身的类型）

- 类型定义

	type Dog

		name::String

		owner::String

	end

  - 默认构造函数入参是按定义属性的顺序普通占位

	dog = Dog("bitch", "sb")

  - 可以通过复用值的类型构造同类对象

	doggy = typeof(dog)("doggy", "sb")

  - 类似结构体的类型称作具体类型（具型）
  - 具型不能有子类型
  - 具型可以直接实例化
  - 通过abstract定义的类型称作泛型
  - 在类定义内外均可给类定义更多地构造函数

	abstract Cat # => 仅此一行注册到类型层级

	type Tiger <: Cat # => 这样派生/继承发展出子类型

		age::Real

		roar::AbstractString

		Tiger(age::Real) = Tiger(age, "miaow") # => 内部构造函数定义

	end

	Tiger(roar::AbstractString) = Tiger(9, roar) # => 外部构造函数定义

  - [可以通过new实例化类型覆盖默认构造函数并禁止外部构造函数][2]

	type Lion <: Cat

		color::AbstractString

		name::String

		Lion() = new ("yellow", "kaka")

		Lion(name::String) = Lion("orange", name)

	end

	Lion(color::AbstractString) = Lion(color, "messi")

  - Dispatch

	朱莉娅中所有命名函数都是一般函数，这意味着由若干小方法构建。

	每个构造函数对于类型来说都是一般函数。

	以非构造函数为例，给Lion添加函数meow

	function meow(baby::Lion)

		println(baby.name) # => 通过点（.）运算符访问对象属性

	end

	function meow(baby::Tiger)

		println("wow")

	end

	这里重点想说：尽管函数名都是meow、都有一个入参，可是入参类型不同，也不算重复、不会覆盖，类似重载。

	meow(Lion("brown", "zidane")) # => zidane

	meow(Tiger(99, "MIAOW")) # => wow

---
[0]: https://www.zhihu.com/question/264640747 "循环节"
[1]: http://python-history.blogspot.com/2009/02/early-language-design-and-development.html "The Problem With Numbers In Python From ABC"
[2]: https://github.com/JuliaLang/julia/issues/24002 "invalid redefinition of constant Lion"
[3]: https://learnxinyminutes.com/docs/julia/ "二十分钟牵手朱莉娅"