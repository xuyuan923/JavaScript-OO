# 构造函数

```js
function People(name){
	this.name = name;
}
var person = new People('Cassie Xu');
console.log(person.name);
```

```js
function People(name) {
  this.name = name;
  this.greet = function() {
    console.log('Hello, my name is ' + this.name + '!');
  };
}
var person = new People('Cassie Xu');
person.greet();
```

# 原型

```js
function People(name) {
  this.name = name;
}
People.prototype = {
  greet: function() {
    console.log('Hello, my name is ' + this.name + '!');
  }
};
var person = new People('Cassie Xu');
person.greet();
console.log(person.__proto__ === People.prototype); // true
```

```js
var a = { foo: 1 };
var b = { bar: 2 };
b.__proto__ = a;
console.log(b.foo); 
console.log(b.bar); 
```

```js
var a = {};
console.log(a.__proto__); // {}
console.log(a.__proto__.__proto__); // null
```

# 继承

```js
function Parent(){}
Parent.prototype = {
	greet: function(){
	console.log('hello world');
}
}
function Child(){}
Child.prototype = new Parent();
var c = new Child();
c.greet(); //console.log('hello world');
```

```js
function Parent() {
	this.name = 'xxx',
	this.date = 'xxx'
}
Parent.prototype.greet = function() {
  console.log('JavaScript rocks');
}

function Child() {}
Child.prototype = Object.create(Parent.prototype);
//硬记的知识	
Child.prototype.constructor = Child;
var child = new Child();
child.greet();
```

# this

```js
var person = {
    firstName: "Penelope",
    lastName: "Barrymore",
    sayFullName: function () {
        console.log(this.firstName + " " + this.lastName); //=> "Penelope Barrymore"
        console.log(person.firstName + " " + person.lastName); //=> "Penelope Barrymore"
    }
};
person.sayFullName();
```

```js
var firstName = 'John',
  	lastName = 'Wu';
var person = {
    firstName: "Penelope",
    lastName: "Barrymore",
    sayFullName: function () {
        console.log(this.firstName + " " + this.lastName); 
    }
};
person.sayFullName(); //=> "Penelope Barrymore"
var sayFullName = person.sayFullName;
sayFullName(); // window is calling it!
```

```js
funtion foo(){
	'use strict';
	console.log(this) //undefined
}
```

# 自执行函数

```js
(function(c){
	var a = 1;
	var b = 2;
	console.log(a+b+c);
})(3)
// c = 3
```

# 闭包

```js
var a = {};
a.foo = function(callback) {
  // do something and call callback in whatever way
}
a.bar = function() {
  this.num = 1;
  var that = this;
  //闭包，这里that可以访问到a.bar的作用域
  this.foo(function(newNum) {
    that.num = newNum;
  });
  console.log(this.num);
}
a.bar();
```