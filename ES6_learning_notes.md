**一、环境搭建**
  -
**1. webpack**

  * 入口（entry）
  * 输出（output）
  * loader：让webpack处理那些非Javascript的文件，将所有类型的文件=>webpack可以处理的模块
  * 插件（plugins）：例 `const webpack = require ('webpack')`
  
**2. gulp**


**二、声明与表达式**
  -
**2.1. let与const**
  * **let命令**
     +   **代码块内有效**
      

           		{
                	let a = 0;
                	var b = 1;
                	a    //0
                    }
                    a      //报错 ReferenceError：a is not defined
                    b     //1
					
			let在代码块内有效，var在全局有效
     + **不能重复声明**
                  

           		
                	let a = 1;
                	let a = 2;
                	var b = 3;
                	var b = 4;
                	a   //   Identifier 'a' has already been declared
                	b   // 4
                	
          let只能声明一次， var 可以声明多次
     + **迭代计数使用**
         for循环计数器很适合使用let
         
           		
                	for(var i = 0; i < 10; i++) {
                		setTimeout(function(){
                			console.log(i);
                			})
                	}   
                	//   输出十个10
                	//   变量i使用var声明的，全局有效，所以全局中只有一个变量i，setTimeout定时器是在循环结束后才执行，

                   for(var j = 0; j < 10; j++){
                   		setTimeout(function(){
                   			console.log(j);
                   			})
                   }	
                   //   输出0123456789
                    //  变量j用let循环，只在本轮循环中有效，每次循环的j都是一个新的变量，所以setTimeout定时器里的j其实是不同的
                        变量，即最后输出12345。 （若每次循环的变量j都是重新声明的，如何知道前一个循环的值？  这是因为
                        在javaScript引擎内部会记住前一次循环的值
                	
     + **无变量提升**
     
           		
                	console.log(a);    //ReferenceError: a is not defined
                	let a = 1;
                	
                	console.log(b);    //undefined
                	var b =  2
                	
                	
		变量b用var声明存在变量提升，所以当脚本开始运行时，b已经存在了，但是还没赋值，所以会输出undefined
		变量a用let声明不存在变量提升，在声明变量a之前，a不存在，所以会报错
  * **const命令**
  	const 声明一个**只读变量**，声明之后之后**不允许改变**。（const保证的是变量指向的内存地址的数据不允许改动，对于简单类型
  	来说（number，string，boolean），值就保存在变量指向的那个内存地址，因此，const声明的简单类型变量等同于常量。
  	而对于复杂类型（object，array，function）来说，变量指向的内存地址其实是保存了一个指向实际数据的指针，所以const只能
    保证指针是固定的，而指针指向的数据结构变不变就无法控制，所以使用const声明复杂类型对象时要慎重）
  	
                	
                	//暂时性死区
                	//ES6规定， 代码块内若存在let或const，代码块会对这些命令声明的变量从块的开始就形成一个封闭的作用域，
                	代码块内，在声明p之前使用它会报错

					var p = "a";
					if(true){
						console.log(p);       //ReferenceError: P is not defined
						const p = "123";
					}
                	
**2.2. ES6解构赋值**

 * **数组模型解构**
            	
            	//基本类型                          		
              	let [a, b, c] = [1, 2, 3];
				// a = 1
				// b = 2
				// c = 3
    			
    			//可嵌套
				let [a, [[b], c]] = [1, [[2], 3]];
				// a = 1
				// b = 2
				// c = 3

				//可忽略
				let [a, , b] = [1, 2, 3];
				// a = 1
				// b = 3


				//不完全解构
				let [a = 1, b] = [ ]; // a = 1, b = undefined


				//剩余运算符
				let [a, ...b] = [1, 2, 3];
				//a = 1
				//b = [2, 3]



				//解构默认值
				let [a = 3, b = a] = [];     // a = 3, b = 3
				let [a = 3, b = a] = [1];    // a = 1, b = 1
				let [a = 3, b = a] = [1, 2]; // a = 1, b = 2
  * **对象模型解构**

            	//基本类型
            	let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
				// foo = 'aaa'
				// bar = 'bbb'
 
				let { baz : foo } = { baz : 'ddd' };
				// foo = 'ddd'




				//可嵌套可忽略
				let obj = {p: ['hello', {y: 'world'}] };
				let {p: [x, { y }] } = obj;
				// x = 'hello'
				// y = 'world'
				let obj = {p: ['hello', {y: 'world'}] };
				let {p: [x, {  }] } = obj;
				// x = 'hello'


   				//不完全解构
				let obj = {p: [{y: 'world'}] };
				let {p: [{ y }, x ] } = obj;
				// x = undefined
				// y = 'world'



				//剩余运算符
				let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40};
				// a = 10
				// b = 20
				// rest = {c: 30, d: 40}



				//解构默认值
				let {a = 10, b = 5} = {a: 3};
				// a = 3; b = 5;
				let {a: aa = 10, b: bb = 5} = {a: 3};
				// aa = 3; bb = 5;
  ****


              			
              	计算参数之和
              	function sum(...num){
   				 var sumNum = 0;
   				 for(let i=0;i<num.length;i++){
        			sumNum += parseInt(num[i])
 							   }
  					  console.log(sumNum)
					 }

					sum(1,2,3)      //6
					sum(1,2,"3")     //6
					sum(1,3,"6和4")   //10
