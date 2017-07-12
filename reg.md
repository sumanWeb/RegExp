

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



[慕课网学习正则笔记](http://www.imooc.com/video/12528/0)