#JS OBJECT

#1. object本身的方法
直接定义在object对象的方法;
例: Object.print = function () { console.log("cout") };

#2. object实例方法
定义在object.prototype的方法, 可以被object实例直接使用
例:
Object.prototype.print = function () {
    console.log(this);
}

var obj = new Object();
obj.print();


#3. Object()
Object本身是一个函数, 可以将任意值转化为对象, 常用于保证某个值一定是对象
当参数为空（null或undefined）时, 返回一个空对象 
以下效果相同:
var obj = new Object();
var obj = new Object(null);
var obj = new Object(undefined);

obj instanceof Object; //true
运算符instanceof用来判断一个对象是否是指定构造函数的实例;

`若参数是原始类型的值，Object方法将其转化为对应包装对象的实例;`
var obj = new Object(1);
obj instanceof Object; //true
obj instanceof Number; //true

var obj = new Object('aaa');
obj instanceof String; //true

var obj = new Object(false);
obj instanceof Boolean; //true

`若该方法的参数是对象, 则返回该对象，不需要转换;`
var arr = [];
var obj = new Object(arr);
arr == obj; //true

var value = {};
var obj = new Object(value);
obj == value; //true

var func = function() {};
var obj = new Object(func);
obj == func; //true

`可用来判断变量是否为对象;`
function isObject(value) {
    return value = Object(value);
}
isObject([]); //true
isObject(true); //false

#Object构造函数
`Object不仅可作为工具函数使用，还可作为构造函数, 生成新的Object对象;`
var obj = new Object();

`var obj = new Object() 与 var obj = {}等价`

`Object作为构造函数时其使用方法与作为工具函数时一致;`
Object(value)与new Object(value)的语义不同，前者是将value转化为对象，后者是生成一个新的对象, 其值是value;

#Object静态方法
即Object自身的方法;

Object.keys, Object.getOwnPropertyNames 方法用来遍历对象的属性；
Object.keys方法的参数是对象，返回值是数组，数组的成员是该对象的所有属性名；







