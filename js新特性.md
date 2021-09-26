# 1.let变量

## 1.1.变量声明方式

```javascript
//声明变量
let a;
let b,c,d;
let e = 100;
let f = 512,g = 'dsd',h = [];

```

## 1.2.let变量特性

1.let变量不能重复声明

2.块级作用域

3.let不存在变量提升   

```javascript
//存在变量提升的情况
console.log(song);//可以正常输出
var song = '小星星'

//不存在变量提升的情况
console.log(song);//报错
let song = '小星星'
```

4.不允许作用域链

```javascript
{
    let school = '123';
    function fn(){
        console.log(school);
    }
    fn();//函数可以正常输出，因为函数体内没有定义school，则往外一层找school，即不影响作用域链
}
```

# 2.const常量

## 2.1声明方式

```javascript
//声明常量
const SCHOOL = '浙江工业大学';
```

## 2.2.const特性

1.一定要赋初值

2.一般常量名大写（潜规则）

3.常量的值不能修改

4.块级作用域

5.对于数组和对象的元素修改，不算做对常量的修改，不会报错

```javascript
const TEAM = ['UZI','MXLG','Ming','Leyme'];
TEAM.push('Meiko');//地址不变，不会报错
TEAM = 100；//报错
```



# 3.变量的解构赋值

```javascript
//Es6 允许按照一定模式从数组和对象中提取值，对变量进行赋值--解构赋值

//1.数组的解构
const F4 = ['小沈阳','刘能','赵四','宋小宝'];
let [xiao,liu,zhao,song] = F4;

//2.对象的解构
const zhao = {
	name:'jsr',
    age:'18',
    xiaopin:function(){
        console.log("hahahaha")
    }
};

let {name, age, xiaopin} = zhao;

zhao.xiaopin();
//方法解构之后调用方便
xiaopin();

```



# 4.模板字符串

```javascript
//ES6 引入新的声明字符串的方式 ``
let str = `我也是一个字符串`

//内容中可以直接出现换行符
let str = `<ul>
			<li>333</li>
			<li>333</li>
		   </ul>`;

//变量拼接
let lovest = '魏翔';
let out = `${lovest}是我心目中最搞笑的演员`;
console.log(out);//魏翔是我心目中最搞笑的演员
```



# 5.对象的简化写法

```javascript
//ES6允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。
//这样的书写更加间接
let name = 'jsr';
let skill = function(){
    console.log('hahahaah');
}

const person = {
    name,
    skill,
    hobby(){
        console.log("xixixix")
  }
}
```



# 6.箭头函数

```javascript
//ES6允许使用箭头(=>)定义函数
//声明一个函数
let fn = function(){   
}

let fn = (a,b) => {
	return a + b;
}
//调用函数
let result = fn(1,2);

//1.箭头函数的this是静态的，this始终指向函数声明时所在作用域下的this的值
function getName(){
    console.log(this.name);
}
let getName2 = () => {
    console.log(this.name);
}

//设置window对象的name属性
window.name = 'jsr';
const NAME = {
	name:"JSR"
}

//直接调用
getName();//jsr
getName2();//jsr

//call 方法调用
getName.call(school);//JSR
getName2.call(school);//jsr 箭头函数的this静态

```

```javascript
//不能作为构造器实例化对象
let Person = (name, age) => {
    this.name = name;
    this.age = age;
}
let me = new Person('jsr',18);
console.log(me);//报错！！！！
```

```javascript
//不能使用arguments变量
let fn = () => {
    console.log(arguments);
}
fn(1,2,3);//报错！！！！！！
```

```javascript
//箭头函数的简写
//1 省略小括号，当形参有且只有一个的时候
let add = n => {
return n + n;
}

//2.当代码题只有一条语句的时候，可以省略花括号，省略花括号的话，return必须省略
//而且语句的执行结果就是函数的返回值
let pow = n => n*n;
```



**箭头函数适合与this无关的回调、定时器。数组的方法回调，不适合与this有关的。**



#  7.函数参数的默认值设计

```javascript
//ES6允许给函数参数赋值初始值
//1.形参初始值 具有默认值的参数，一般位置要靠后
function add(a,b,c=10){
    return a + b + c;
}
let result = add(1,2);

//2.与解构赋值结合
function connect({host="127.0.0.1",username,password,port}){
	console.log(host)
}
connect({
    host:'localhost',
    username:'root',
    password:'root',
    port:3306
})

```

# 8.rest参数

```javascript
//ES6引入rest参数，用于获取函数的实参，用来代替grguments
//1.ES5获取实参的方式
function date(){
    console.log(arguments);
}
date('j','s','r');

//rest 参数(必须放在最后)
function date(a,b,...args){
    console.log(a);
    console.log(b);
    console.log(args);
}
date(1,2,3,4,5,6);
```

# 9.spread扩展运算符

```javascript
//...扩展运算符能将数组转换为逗号分隔的参数序列
//声明一个数组
const tfboys = ['易烊千玺','王源','王俊凯'];
//声明一个函数
function chunwan(){
    console.log(arguments);
}

chunwan(...tfboys);//chunwan('易烊千玺','王源','王俊凯')

//数组的合并
const arr1 = ['jsr'];
const arr2 = ['lct'];
//法1：使用concat合并数组
const arr = arr1.concat(arr2);
//法2：使用拓展运算符合并数组
const arr = [...arr1,...arr2];

//数组的克隆
const sanzhihua = ['E','G','M'];
const sanyecao = [...sanzhihua];//sanyecao =['E','G','M']
```



# 10.Symbol的介绍和创建

```javascript
//创建Symbol
let s = Symbol();
let s2 = Symbol('jsr');
let s3 = Symbol('jsr');

console.log(s2 === s3);//false
//Symbol.for 创建
let s4 = Symbol.for('尚硅谷');
let s5 = Symbol.for('尚硅谷');

console.log(s4 === s5);//true

//Symbol不能与其他数据进行运算


```

## 10.1、对象中添加Symbol类型的属性

```javascript
//向对象中添加symbol方法 up down
let game = {
    name:'jjj',
    up(){
        console.log('hhh')
    },
    down(){
        console.log('hhhddd') 
	}
}
let methods = {
    up:Symbol(),
    down:Symbol()
};
game[methods.up] = function(){
console.log("我可以改变形状");
}
game[methods.down] = function(){
console.log("我不可以改变形状");
}

//法2
let youxi = {
	name:"狼人杀"，

[Symnol('say')]:function(){

​		console.log("我是狼人")
​	}，

[Symnol('say')]:function(){

​		console.log("我是平民")
​	}，
}
```



## 10.2、Symbol的内置属性

![image-20210926132424758](../../Typora/img/image-20210926132424758.png)

![image-20210926132924611](../../Typora/img/image-20210926132924611.png)



# 11.js数据类型总结

**URSNB--你真牛逼**

1. u ---- undefined
2. s ---- string symbol
3. o ---- object
4. n ---- null number
5. b ---- boolean



# 12.迭代器

```javascript
//声明一个数组
const xiyou = ['唐僧'，'孙悟空','猪八戒','沙僧']

let iterator = xiyou[Symbol.iterator]();
//调用对象的next方法
console.log(iterator.next());
console.log(iterator.next());
```

**工作原理**

1. 创建一个指针对象，指向当前数据结构的起始位置
2. 第一次调用对象的next方法，指针自动指向数据结构的第一个成员
3. 接下来不断调用next方法，指针一直往后移动，直到指向最后一个成员
4. 每调用next方法返回一个包含value和done属性的对象