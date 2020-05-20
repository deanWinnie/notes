# 第3章 基本概念 #
## 3.4数据类型 ##
**3.4.6 string类型**  
数值、布尔值、对象和字符串都有string方法，null和undefined没有这个方法,null和undefined可以用string方法
tostring可以以二进制等形式输出  

	var num=10
	console.log(num.toString());//"10"
	console.log(num.toString(2));//"1010"
	console.log(num.toString(8));//"12"
	console.log(num.toString(10));//"10"
	console.log(num.toString(16));//"a"
	//string方法
	var val1=null
	var val2
	console.log(string(val1));//"null"
	console.log(string(val2));//"undefined"  
## 3.5 操作符 ##  
**3.5.3 布尔操作符**  
**逻辑与**  
逻辑与操作可以应用于任何类型的操作，而不仅仅是布尔值。在有一个操作数不是布尔值得情况下，逻辑与操作就不一定返回布尔值；此时，它遵循以下规则：
如果第一个操作数是对象，则返回第二个操作数；  
如果第二个操作数是对象，则只有在一个操作数的求值结果为true的情况下才会返回该对象；  
如果有一个操作数是null，则返回null；  
如果有一个操作数是NaN，则返回NaN；  
如果有一个操作数是undefined，则返回undefined； 


	

