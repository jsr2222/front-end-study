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



# 13.生成器函数的声明及调用

```javascript
//生成器其实就是一个特殊的函数
function * gen(){
	console.log("hello generator")
}

let iterator = gen();
//生成器函数要调用next()方法才会执行
iterator.next();

//函数代码的分隔符
function * gen(){
    yield '一只没有耳朵';
    yield '一只没有尾部';
    yield '真奇怪';
}

let iterator = gen();
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
```

![image-20210926211545565](../../Typora/img/image-20210926211545565.png)

==由图可见，生成器函数 + yield分隔符可以使代码一行一行输出==



## 生成器函数的参数传递



![image-20210926212324277](../../Typora/img/image-20210926212324277.png)



## 生成器函数解决回调地狱问题

![image-20210926212951432](../../Typora/img/image-20210926212951432.png)



## 生成器函数实现异步操作

```javascript

function getUsers(){
    setTimeout(()=>{
        let data = '用户信息';
        iterator.next(data);
    },1000)
}

function getOrders(){
    setTimeout(()=>{
        let data = '订单数据';
        iterator.next(data);
    },1000)
}

function getGoods(){
    setTimeout(()=>{
        let data = '商品数据';
        iterator.next(data);
    },1000)
}

function * gen(){
    let users = yield getUsers();
    console.log(users);
    let orders = yield getOrders();
    console.log(orders);
    let goods = yield getGoods();
    console.log(goods);
}

let iterator = gen();
iterator.next();
//输出：用户信息
//	   订单数据
//     商品数据
```

# 14、Promise介绍

```javascript
//实例化Promise对象
const p = new Promise(function(resolve,reject){
    setTimeout(function(){
        //成功时
        // let data = '数据库中的用户数据';
        // resolve(data);

        //失败时
        let err = '数据读取失败';
        reject(err);
    },1000);
})

//调用promise对象的then方法
p.then(function(value){
    console.log(value);
},function(reason){
    console.error(reason)
})
```

## Promise封装读取文件

```javascript
//1.引入fs模块
const fs = require('fs');

//2.调用方法读取文件
fs.readFile('./resources/为学.md', (err, data)=>{
    //如果失败，则抛出错误
    if(err) throw err;
    //如果成功，则输出内容
    console.log(data.toString())
})
```

```javascript
//1.引入fs模块
const fs = require('fs');

//2.调用方法读取文件

//3.使用Prominse封装
const p = new Promise(function(resolve, reject){
    fs.readFile('./resources/为学.md', (err, data)=>{
        //如果失败，则抛出错误
        if(err) reject(err);
        //如果成功，则输出内容
        resolve(data)
    });
    
});

p.then(function(value){
    console.log(value.toString());
},function(reason){
    console.log("读取失败！！")
})
```

## Promise封装AJAX

```javascript
//1.创建对象 
const xhr = new XMLHttpRequest();

//2.初始化
xhr.open("GET","https://api.apiopen.top/getJoke");

//3.发送
xhr.send();

//4.绑定事件，处理响应结果
xhr.onreadystatechange = function(){
    //判断
    if(xhr.readyState === 4){
        //判断响应状态码 200-299
        if(xhr.status >= 200 && xhr.status < 300){
            //表示成功
            console.log(xhr.response);
        }else{
            //如果失败
            console.error(xhr.status);
        }
    }
}
```

```javascript
//Promise封装AJAX
const p = new Promise((resolve, reject) => {
    //1.创建对象
    let XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;
 
    let xhr = new XMLHttpRequest();

    //2.初始化
    xhr.open("GET", "http://api.apiopen.top/getJoke");

    //3.发送
    xhr.send();

    //4.绑定事件，处理响应结果
    xhr.onreadystatechange = function () {
        //判断
        if (xhr.readyState === 4) {
            //判断响应状态码 200-299
            if(xhr.status >= 200 && xhr.status < 300){
                //表示成功
                resolve(xhr.response);
            }else{
                //如果失败
                reject(xhr.status);
            }
        }
    }
})

p.then(function(value){
    console.log(value);
},function(reason){
    console.error(reason);
}
)
```

## Promise对象的catch方法

```javascript
const p = new Promise((resolve, reject)=>{
	setTimeout(()=>{
        //设置p对象的状态为失败，并设置失败的值
        reject("出错了");
    }, 1000)
});

p.catch(function(reason){
	console.warn(reason);
})
```



# 15、set集合介绍和API

```javascript
//声明一个set
let s = new Set();
let s2 = new Set(['大事儿'，'小事儿','好事儿','坏事儿','小事儿']);//重复的只会算一个

//元素个数
console.log(s2.size);
//添加新的元素
s2.add('喜事儿');
//删除元素
s2.delete('坏事儿');
//判断集合中是否有这个值
console.log(s2.has('糟心事'));
//清空
s2.clear();

//遍历
for(let v of s2){
    console.log(v);//输出：大事儿
                   //     小事儿
    			   //     好事儿
        		   //     坏事儿
```



# 16、Map的介绍和API

![image-20210927202553246](../../Typora/img/image-20210927202553246.png)



# 17、class介绍

![image-20210927203356992](../../Typora/img/image-20210927203356992.png)

```javascript
class Phone{
    //构造方法，名字不能修改
    constructor(brand, price){
        this.brand = brand;
        this.price = price;
    }
    
    //方法必须使用该语法， 不能使用ES5的对象完整形式
    call(){
        console.log("我可以打电话");
    }
}

let onePlus = new Shouji("1+", 1999);
```



## 17.1、ES5构造函数继承

```javascript
//手机
function Phone(brand, price){
	this.brand = brand;
    this.price = price;
}

Phone.prototype.call = function(){
    console.log("我可以搭电话");
}

//智能手机
function SmartPhone(brand, price, color, size) {
    Phone.call(this, brand, price);
    this.color = color;
    this.size = size;
}

//设置子级构造函数的原型
SmartPhone.prototyoe = new Phone;
SmartPhone.prototype.constructor = SmartPhone;

//声明 子类的方法
SmartPhone.prototype.playGame = function(){
    console.log("我可以玩游戏");
}

SmartPhone.prototype.photo = function(){
    console.log("我可以拍照");
}

const chuizi = new SmartPhone('锤子'， 2499, '黑色', '5.5inch');
```



## 17.2 ES6 class的类继承

```javascript
class Phone{
    //构造方法
    construtor(brand, price){
        this.brand = brand;
        this.price = price;
    }
    
    //父类的成员属性
    call(){
        console.log("我可以打电话！");
    }
}

class SmartPhone extends Phone {
    //构造方法
    constructor(brand, price, color, size){
        super(brand, price);
        this.color = color;
        this.size = size;
    }
    
    photo(){
        console.log("拍照");
    }
    
    playGame(){
        console.log("玩游戏");
    }
}

const xiaomi = new 	SmartPhone('小米', 799， '黑色', '4.7inch');

```



## 17.3 子类对父类方法的重写

```javascript
class Phone{
    //构造方法
    construtor(brand, price){
        this.brand = brand;
        this.price = price;
    }
    

    //父类的成员属性
    call(){
        console.log("我可以打电话！");
    }

}

class SmartPhone extends Phone {
    //构造方法
    constructor(brand, price, color, size){
        super(brand, price);
        this.color = color;
        this.size = size;
    }
    

    photo(){
        console.log("拍照");
    }
    
    playGame(){
        console.log("玩游戏");
    }
    
    //子类对父类call方法的重写
    

}

const xiaomi = new 	SmartPhone('小米', 799， '黑色', '4.7inch');
```



## 17.4 class中的geter和seter设置



# 18、ES6的数值方法拓展

![image-20210928140950172](../../Typora/img/image-20210928140950172.png)

![image-20210928141223925](../../Typora/img/image-20210928141223925.png)



# 19、ES6的对象方法拓展



![image-20210928142141690](../../Typora/img/image-20210928142141690.png)

![image-20210928142544507](../../Typora/img/image-20210928142544507.png)



# 20、async和await

**async 和 await 两种语法结合可以让异步代码像同步代码一样**



## 20.1 async

![image-20210928152317849](../../Typora/img/image-20210928152317849.png)

```javascript
//async 函数
async function fn(){
    //1.只要返回的结果不是一个 Promise类型的对象，返回的结果就是成功 Promise       对象
    return 'hhh';
    return ;
    
    //2.抛出错误， 返回的结果是一个失败的 Promise
    throw new Error('出错了');
    
    //3.返回的结果如果是一个成功的 promise 对象，则fn函数返回的也是成功的       promise对象，且值就是该promise的值‘成功的数据’
    return new Promise((resolve, reject)=>{
		resolve('成功的数据')
    })
    
    //4.返回的结果如果是一个失败的 promise 对象，则fn函数返回的也是失		  败的promise对象，且值就是该promise的值‘失败的数据’
    return new Promise((resolve, reject)=>{
		reject('失败的数据')
    })
}

const result = fn();
console.log(result);
```



## 20.2 await函数

![image-20210928152353067](../../Typora/img/image-20210928152353067.png)

```javascript
//创建 promise 对象
const p = new Promise((resolve, reject) => ){
	resolve("success,zhe number is 1234");

})

// await 要放在 async 函数中
async function main() {
    let result = await p;
    console.log(result);
}


//创建 promise 对象
const p = new Promise((resolve, reject) => ){

	reject("fail, please try again");
})

// await 要放在 async 函数中
async function main() {
    try{
        let result = await p;
        console.log(result);
    }catch (e) {
        console.log(e);
    }   
}
```



## 20.3 async 和 await 结合读取文件内容

```javascript
//1.引入 fs 模块
const fs = require("fs");

//读取文件1
function readwenjian1() {
    return new Promise((resolve, reject) => {
		fs.readFile("./wenjian1.md", (err, data) => {
            //如果失败
            if (err) reject(err);
            //如果成功
            resolve(data);
        })
    })
}

//读取文件2
function readwenjian2() {
    return new Promise((resolve, reject) => {
		fs.readFile("./wenjian2.md", (err, data) => {
            //如果失败
            if (err) reject(err);
            //如果成功
            resolve(data);
        })
    })
}

//声明一个 async 函数
async function main(){
    //获取文件内容
    let data1 = await readwenjian1();
    let data2 = await readwenjian2();
}

//调用
main();
```



## 20.4 async 和  await 结合发送 AJAX 请求

```javascript
//发送 AJAX 请求， 返回的结果是 Promise 对象
function sendAJAX(url) {
    return new Promise((resolve, reject) => {
        //1.创建对象
        const x = new XMLHttpRequest();
        
        //2.初始化
        x.open('GET', url);
        
        //3.发送
        x.send();
        
        //4.事件绑定
        x.onreadystatechange = function() {
            if(x.readyState === 4) {
                if(x.status >= 200 && x.status < 300) {
                    //成功
                    resolve(x.response);
                }else{
                    //如果失败
                    reject(x.status);
                }
            }
        }
    })
}

//1.promise then 方法测试
sendAJAX("http://api.apiopen.top/getJoke").then(value=>{
    成功的回调
},reason=>{
    失败的回调
})

//2.async 与 await 测试
async function main(){
    //发送AJAX请求
    let result = await sendAJAX("http://api.apiopen.top/getJoke");
}


main();
```



# 21.ES9 拓展运算符和 rest 参数

```javascript
function connect({host, port, ...user}) {
    console.log(host);
    console.log(port);
    console.log(user);
}

connect({
    host: '127.0.0.1',
    port: 3306,
    username: 'root',
    password: 'root',
    type:'master'
})

const skillOne = {
    q: '天音波'
}

const skillTwo = {
    w: '金钟罩'
}

const skillThree = {
    e: '天雷破'
}

const skillFour = {
    r: '猛龙摆尾'
}

const mangseng = {...skillOne, ...skillTwo, ...skillThree, ...skillFour};

console.log(mangseng);
```



 # 22.ES9正则拓展-命名捕获分组

```javascript
//声明一个字符串
let str = '<a href="http://www.atguigu.com">尚硅谷</a>;

//提取 url 与 标签文本
const reg = /<a href="(.*)">(.*)<\/a>/;

//执行
const result = reg.exec(str);

console.log(result);
```



# 23.ES9正则拓展-正向、反向断言

```javascript
//声明字符串
let str = 'JS1222222你知道吗555啦啦啦';

//正向断言
const reg = /\d+(?=啦)/;
const result = reg.exec(str);

//反向断言
const reg = /(?<吗)\d+/;
const result = reg.exec(str);
console.log(result);
```



# 24.ES9正则扩展-dotALL模式

# 25.ES10-ES11新特性



![image-20210928194956290](../../Typora/img/image-20210928194956290.png)

