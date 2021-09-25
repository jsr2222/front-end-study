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



## 4.模板字符串

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



## 5.对象的简化写法

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



## 6.箭头函数

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