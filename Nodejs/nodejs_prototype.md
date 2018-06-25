#PROTOTYPE

`JS的继承通过PROTOTYPE对象(原型对象);`

#构造函数的缺点

function Foo (name, age) {
    this.name = name;
    this.age = age;
    this.common = function() {
        console.log("THIS IS COMMON");
    }
}

var Foobar = new Foo("fubar", 11);
var Barfoo = new Foo("barfu", 22);

Foobar.name; //"fubar"
Foobar.age; //11

Foobar.common === Barfu.common; //false

`多个构造函数的多个实例之间无法共享属性，导致系统资源的浪费;`
common方法生成在每个实例对象上，因此生成了两次，导致了系统资源的浪费；

#解决方法=> PROTOTYPE
`JS继承机制的设计思想：所有继承自原型对象的实例对象都能共享原型对象的属性和方法;`
每一个函数默认有prototype属性，指向一个对象，普通函数的prototype属性无用，构造函数的prototype自动成为实例对象的原型；

var Foobar = function(name) {
    this.name = "Fubar";
}

foobar.prototype.age = 11;

var varfoo = new Foobar("foo");
varfoo.age; // 11;



