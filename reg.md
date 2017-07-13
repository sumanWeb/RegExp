

## JavaScript 通过内置对象 RegExp 支持正则 表达式 ##

### 有两种方法实例化RegExp对象 ###

* 字面量

* 构造函数

**字面量**

**\b**  单词边界;

> var reg  = / \ bis\b/g ;

> 'he is a boy. this is a dog .where  is she?' . replace( reg ,  "IS"); 

> he IS a boy. this IS a dog .where IS she;

> 会全部替换 IS

>  var reg = new RegExp ('\\bis\\b', 'g');

> he IS a boy. this IS a dog .where IS she;

> 会全部替换 IS;


## **修饰符**

* g : **global 全文搜索, 不添加, 搜索	到 第一个匹配停止** ;
* i  :  **ignore case 忽略大小写 默认大小写敏感**;
>'he is a boy. this Is a dog .where  is she?' . replace( /\bis\b/ gi,  0"); 

* m : **multiple lines 多行搜索**


##元字符

- 正则表达式由两种基本字符类型组成

        原义文本字符 
        a b c  d e f g 
        元字符

## 元字符是在正则表达式中	特殊含义的非字面字符 ##


#### 元字符 ####
一个
>  \ * ? ( ) { }  [ ]  

| 字符        | 含义           |
| ------------- |:-------------:| 
|  \t     | 水平制表符 | 
| \v      | 垂直制表符      |  
| \n | 换行符   |    
| \r | 回车符|
|\0  |空字符|
|\f|换页符|

|\cX|与X对应的控制字符(Ctrl +x)|

## 字符类 
- 一般情况下正则表达式一个字符对应字符串一个字符;
- 表达式 ab\t 的含义是 'ab'  tab;
-  我们可以使用元字符 [ ] 来构建一个简单的类;
-  所谓类是指符合某些特性的对象，一个泛指，而不是特指某个字符;
-  我们可以使用元字符 [ ] 来构建一个简单的类;
-  所谓类是指符合某些特性的对象，一个泛指，而不是特指某个字符;
-  表达式[abc] 把字符 a 或 b 或 c 归为一列,表达式可以匹配这类的字符;

		"a1b2c3d4".replace(/[abc]/g,"X");
		"X1X2X3d4"


##### 字符类取反 
- 使用元字符 ^ 创建 (反向类/负向类);
- 反向类的意思是不属于某类的内容;
- 表达式[ ^abc] 表示 不是字符 a或b或c 的内容;

		"a1b2c3d4".replace(/[^abc]/g,"X");
		"aXbXcXXX"	

#####范围类  ####
- 使用字符类匹配数字[0123456789];
- 正则表达式还提供了范围类;
- 所我们可以使用[a-z] 来连续两个字符表示(从 a-z 的任意字符);
- 这是一个闭区间,也就是包含a 和 z本身;

			'a1b2d3x4z9'.replace(/[a-z]/g,"Q");
			'Q1Q2Q3Q4Q9'

- 在[ ] 组成的类内部是可以连写的[a-zA-Z];
  
			'a1b2d3x4z9xXADd'.replace(/[a-zA-Z]/g,"Q");
			'Q1Q2Q3Q4Q9QQQQQ'
			"2016-09-12".repalce(/[0-9]-/g,"A");
			"AAAAAAAAAA"

##### 预定义类 


|字符|等价类|含义|
|--|:-:|:--:|
|.|[^\r\n]|除了回车符和换行符之外的所有字符|
|\d|[0-9]|数字字符|
|\D|[^0-9]|非数字字符|
|\s|[\t\n\xOB\f\r]|空白字符|
|\S|[^\t\n\xOB\f\r]|非空白字符|
|\w|[a-zA-Z_0-9]|(单词字符)字母数字下划线
|\W|[^a-zA-Z_0-9]|非单词字符|

		匹配一个 ab+ 数字+ 任意字符 的字符串
		ab[0-9][^\r\n];
		ab\d.

####### 边界
###### 正则表达式还提供了几个常用的边界匹配字符

|字符|含义|
|-|-|
|^|以xxxxxx开始|
|$|以xxxxxx结束|
|\b|单词边界|
|\B|非单词边界|

			'This is a boy'.replace(/is/g, '0');
			"Th0 0 a boy" ;
			'This is a boy'.replace(/\bis\b/g, '0');
			"This 0 a boy";
			'This is a boy'.replace(/\Bis\b/g, '0');
			"Th0 is a boy"	
			
					"@123@abc@'.replace(/@./g,"Q");
					"Q23Qbc@";
					"@123@abc@'.replace(/^@./g,"Q");
				     "Q23@abc@"
					"@123@abc@'.replace(/.@/g,"Q");
					"@12QabQ"
					"@123@abc@'.replace(/.@$/g,"Q");
					"@123@abQ"

				      "
					@123
					@456
					@789
					".repalce(/^@\d/g,"X")
					"
					X23
					@456
					@789
					"
					    "
					@123
					@456
					@789
					".repalce(/^@\d/gm,"X")
					"
					X23
					X56
					X89
					"

				
#####量词
- 我们 希望一个连续匹配出现n次数字的字符串
		\d\d\d\d\d\d\d\d\d\d\\d\d\d\d\d\d\d\d\d

|字符|含义|
|--|--|
|?|出现零次或者一次(最多出现一次)|
|+|出现一次或者多次(至少出现一次)|
|*|出现零次或者多次(任意次)|
|{n}|出现n次|
|{n,m}|出现n到m次|
|{n,}|至少出现n次|



##### JavaScript 贪婪模式 与非贪婪模式
- \d{3,6}
- 尽可能多的匹配 直到匹配失败;
			'12345678'.replace(/\d{3,6}/g,"X");
			"X78"
 	
###### 非贪婪模式
- 让正则表达式尽可能少的匹配,也就是说一旦成功匹配不再继续尝试就是非贪婪模式;
- 做法简单,在量词后加上  ? 即可;
			-'1234567890'.match(/\d{3,5}?/g);
			- ["123","456","789"];
			
			- '12345678'.replace(/\d{3,6}/g,"x");
			- x78 	
			
			- '12345678'.replace(/\d{3,6}?/g,"x");
			- xx78 


##### 分组
- 匹配 字符串Byron 连续出现3次的场景;
          		Byron{3} --------->n 连续出现3次
- 使用( )可以达到分组的功能,使用量词作用于分组;
			(Byron){3}---------->整个单词出现3次
			
			'a1b2c3d4'.replace(/[a-z]\d{3}/g,"X");
			'a1b2c3d4'
			
			'a1b2c3d4'.replace(/([a-z]\d){3}/g,"X");
			'Xd4'

##### 或

使用 | 可以达到或的效果
- Byron | Casper	
- Byr(on|Ca)sper
			- ByronCasper.replace(/Byron | Casper/g,'X');
			-  "XX"
			 -ByronsperByrCasper.repalce(/Byr(on|Ca)sper/g,"X");
			 - "XX"	

##### 反向引用
- 2015-12-25 => 12/25/2015
		-                                                成了一个变量 
		-"2015-12-25".replace(/\d{4}-\d{2}-\d{2}/g,"$2$3$1");

		-"2015-12-25".replace(/(\d{4})-(\d{2})-(\d{2})/g,"$2/$3/$1");

##### 忽略分组
不希望捕获某些分组,只需要在分组内加上？: 就可以了
> (?:Byron).(ok) ------------> "Byron"- any character- "ok"(group #1);


##### 前瞻
 
- 正则表达式从文本头部向尾部开始解析,文本尾部反向,成为'前'
- 前瞻 就是在正则表达式匹配到规则的时候，向前检查时候符合断言,后顾/后瞻 方向相反
- JavaScript 不支持后顾
-  符合 和不符合特定断言称为 肯定/正向 匹配 和 否定/负向 匹配


|名称|正则|含义|
|-|-|-|
|正向前瞻|exp(?=assert)||
|负向前瞻|exp(?!assert)||
|正向后顾|exp(?<=assert)|JavaScript不支持|
|负向后顾|exp(?<=!assert)|javaScript不支持|



>\w(?=\d)
>'a2*3'.replace(/w(?=\d)/g,"X");
>'X2*3'
>'a2*34v8'.replace(/w(?=\d)/g,"X");
>"X2*X4X8"
>'a2*34vV'.replace(/w(?=\d)/g,"X");
>X2*X4VV
>'a2*34vV'.replace(/w(?!\d)/g,"X");
>'aX*3XvV'





##### 对象属性
- global :是否全文搜索,默认是false;
- ignore case :是否大小写敏感 默认是false;
- multiline :多行搜索,默认是false	;
- lastIndex:  是当前表达式	匹配内容的最后一个字符的下一个位置;
- source ：正则表达式的文本字符串;

###	RegExp.prototype.test(str);
- 用于测试字符串参数中是否存在匹配正则表达式模式的字符串;
- 如果存在则返回 true,否则 返回 false;

###关于 lastIndex
>var reg2=/\w/g;

>while(reg2.test("ab")){
>	console.log(reg2.last	)
>		}
>		当前匹配结果 第一次 a 最后下一个 就是b 就是2
>		 
###	RegExp.prototype.exec(str);
- 使用正则表达式模式对字符串执行搜索,并将更新全局RegExp对象的属性以反映匹配结果 
- 如果没有匹配的文本则返回null,否则返回一个结果数组;
			-index声明匹配文本的第一个字符的位置
			- input 存放被检索的字符串string

###非全局调用
- 调用非全局的RegExp 对象 exec ( )时,返回数组;
- 第一个元素是与正则表达式相匹配的文本
- 第二个元素是RegExpObject 的第一个子表达相匹配的文本(如果有的话)
- 第三个元素是RegExpObject 的第二个子表达相匹配的文本(如果有的话)
		var reg3 = /\d(\w)\d/;
		var reg4 = /\d(\w)\d/g;	
		var ts = '1a2b3c45e';
		var ret  = reg3.exec(ts);												\d(\w)\d,(\w)	 // 第一匹配结果的时候 
		console.log(reg3.lastIndex + ' \t ' +ret.index + '\t' + ret.toString());  // "0  0    1a2 ,a "     // lastIndex 不生效
		console.log(reg3.lastIndex + ' \t ' +ret.index + '\t' + ret.toString());  // "0  0    1a2 ,a "
		
		全局搜索的时候
		vat ts="$1az2bb3cy4dd5ee"
		while(ret = reg4.exec(ts)){
		console.log(reg4.lastIndex + '\t' + ret.index +"\t" +ret.toString());	
		}
		'' 5  1   1az2,a,z";
		'' 11 7  3cy4,c,y";
		
### String.prototype.search(reg);
- search ( )方法用于检索 字符串 中制定的子字符串,或检索与正则 表达式相匹配的子字符串; 	
- 方法返回第一个匹配结果**index** ,查不到 返回  -1;
- search ( ) 方法不执行 全局匹配,它将忽略标志 g ,并且总是从字符串的开始进行检索
				-	"a1b2c3d1".search("1");
				-	1		  
				-	"a1b2c3d1".search("10");
				-	-1
				-	"a1b2c3d1".search(/1/);
				-	1
				-	会尝试帮我们转成正则   (1)-->(/1/)
### String.prototype.match(reg);
				- match ( )方法将检索字符串,以找到一个或者多个与RegExp匹配的文本
				- RegExp 是否具有标志 g 对 结果影响很大
				- 如果RegExp没有标志g 那么 match( )方法 就只能在字符串 中执行 一次匹配
				- 如果没有找到任何匹配的文本,将返回 null
				- 否则 它将返回一个个数组,其中存放了与它找到的匹配文本有关的 信息;	
				- 返回数组的第一个元素存放的是匹配文本, 而其余的元素存放的是与正则表达式的子表达式匹配的文本
				- 除了常规的数组元素之外,返回的数据还含有2个对象属性;
				-  index 声明匹配文本的起始字符在字符串的位置
				-  input 声明	对 StringObject 的引用
		
		var reg3 = /\d(\w)\d/;
		var reg4 = /\d(\w)\d/g;	
		var ts = '$1a2b3c45e';
		var ret  = ts.match(reg3);		
		console.log(ret);   [ "1a2" , "a"];
		console.log(ret.index + '\t' +reg3.lastIndex);	  "1    0"'	;  没管 	lastIndex						
#### 全局调用
- 如果 RegExp具有标志 g 则match ( ) 方法 将 执行 全局 检索找到 字符串中的所有匹配子字符串
		- 如果没找到任何匹配的子串,则返回null
		- 如果找到了 一个或者 多个匹配子串  , 则返回一个数组
-  数组元素中存放的式字符串中所有的匹配子串，而没有 index 属性 或 input 属性	
		var reg3 = /\d(\w)\d/;
		var reg4 = /\d(\w)\d/g;	
		var ts = '$1a2b3c45e';
		var ret  = ts.match(reg4);		
		console.log(ret);   [ "1a2" , "3c4"];   //没有分组信息了
		console.log(ret.index + '\t' +reg3.lastIndex);	  "undefined    0"'	;  没管 	lastIndex
##### String.prototype.split(reg);
-  我们经常使用 split 方法 把字符串分割成字符数组
-  'a,b,c,d'.split(','); //[ "a","b","c","d"]; 
-  一些复杂的分割情况下我们可以使用正则表达式解决
-  "a1b2c3d".split(/\d/); [ "a","b","c","d"];	


##### String.prototype.replace(reg);

[RegExp](http://www.imooc.com/learn/706)