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
**逻辑或**  
如果第一个操作数是对象，则返回第一个操作数；  
如果第一个操作数的求值结果为false，则返回第二个操作数；   
如果两个操作数是null，则返回null；  
如果两个操作数是NaN，则返回NaN；  
如果两个操作数是undefined，则返回undefined； 
## 3.6 操作符 ##     
**3.6.5 for-in语句**  
for-in语句是一种精准的迭代语句，可以用来枚举对象的属性。
for-in语法 

	for(property in expression) statement  
示例 
 
	 var obj={
            "name":"dean",
            "age":16,
            "sex":"man",
            "hobby":"basketball",
            1:"3"
        }
        for(var ex in obj){
            document.write(ex+"<br>");//输出对象的每个属性名，无序输出
        }  
**3.6.6 label语句**  
可以给for循环来添加一个变量名。然后由break或continue来引用。 示例：

	var num = 0;
        testFor: 
        for (var i=0;i<10;i++) {
            for (var j = 0;j<10;j++) {
                if (i == 5 && j == 5) {
                    break testFor;
                }
                num++
            }
        }
        console.log(num); // 55
        var num2=0;
        labelFor: 
        for (var i=0;i<10;i++) {
            for (var j = 0;j<10;j++) {
                if (i == 5 && j == 5) {
                    continue labelFor;
                }
                num2++
            }
        }
        console.log(num2); // 95  
##  3.7 函数  ##
**3.7.2 没有重载**   
js中的函数是没有重载的  
示例：
  
	function addNum(num){
            return num+100;
        }
        function addNum(num){
            return num+200;
        }
        console.log(addNum(100))//300
# 第4章 变量、作用域、内存问题 #
##  4.1 基本类型和引用类型的值  ##
**4.1.3 传递参数**  
所有函数的参数都是按值传播的。  
示例：  
	
	function addTen(num){
            num+=10;
            return num;
        }
    var count=20;
    var result=addTen(count);
    alert(count);//20
    alert(result);//30
    /*
     *对象参数传递
     */
    function setName(obj){
            obj.name='dean';
            onj=new Object();
            obj.name='winnie';
        }
     var person=new Object();
     setName(person);
     alert(person.name);  

# 第5章 引用类型 #  
##  5.2 Array类型  ##  
**5.2.3 栈方法**  
栈是一种后进先出的数据结构，数组中有push()和pop()方法实现了类似栈的行为。  
push()方法可以接受任意数量的参数，把他们逐个添加到数组末尾，并返回修改后数组的长度。  
pop()方法从数组末尾移除最后一项，减少数组的length值，返回移除值。 
 
	var colors=new Array();
    var count=colors.push('black','white');
    alert(count);  //2

    count=colors.push('blue');
    alert(count); //3

    var item=colors.pop();
    alert(item); //blue

**5.2.4 队列方法**  
队列是一种先进先出的数据结构，数组中有shift()和push()方法实现了类似队列的行为。  
 
	

