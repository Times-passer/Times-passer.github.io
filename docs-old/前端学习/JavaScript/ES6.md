

## 一、class类、extends继承、super( )、tab栏切换(页签功能)

## 1.面向过程与面向对象

### 1.1面向过程

- 面向过程就是分析出解决问题所需要的**步骤**，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。

<img src="https://i.loli.net/2021/08/13/ZQhNa9piOnFbyv6.png" alt="image-20210813101847149" style="zoom:80%;" />



### 1.2面向对象

- 面向对象是把事务分解成为一个个对象，然后通过不同**对象的方法**分工与合作。

<img src="https://i.loli.net/2021/08/13/afCFgWDH7jyovYm.png" alt="image-20210813101956002" style="zoom:80%;" />

### 1.3面向过程与面向对象对比

|      | 面向过程                                                     | 面向对象                                                     |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 优点 | 性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程。 | 易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护 |
| 缺点 | 不易维护、不易复用、不易扩展                                 | 性能比面向过程低                                             |



## 2.对象与类

### 2.1对象

对象是由属性和方法组成的：是一个无序键值对的集合,指的是一个具体的事物

- 属性：事物的特征，在对象中用属性来表示（常用名词）
- 方法：事物的行为，在对象中用方法来表示（常用动词）

#### 2.1.1创建对象

```js
//以下代码是对对象的复习
//字面量创建对象
var ldh = {
    name: '刘德华',
    age: 18
}
console.log(ldh);

//构造函数创建对象
  function Star(name, age) {
    this.name = name;
    this.age = age;
 }
var ldh = new Star('刘德华', 18)//实例化对象
console.log(ldh);	
```

如上两行代码运行结果为:![](images/img3.png)



### 2.2类

- 在 ES6 中新增加了类的概念，可以使用 class 关键字声明一个类，之后以这个类来实例化对象。类抽象了对象的公共部分，它泛指某一大类（class）对象特指某一个，通过类实例化一个具体的对象

#### 2.2.1创建类

1. 语法:

```js
//步骤1 使用class关键字
class name {
  // class body
}     
//步骤2使用定义的类创建实例  注意new关键字
var xx = new name();     
```

2. 示例

```js
 // 1. 创建类 class  创建一个 明星类
 class Star {
   // 类的共有属性放到 constructor 里面
   constructor(name, age) {
   this.name = name;
   this.age = age;
   }
 }

// 2. 利用类创建对象 new
var ldh = new Star('刘德华', 18);
console.log(ldh);
```

以上代码运行结果: 

![](images/img4.png)

通过结果我们可以看出,运行结果和使用构造函数方式一样

#### 2.2.2通过类创建添加属性和方法

```js
 // 1. 创建类 class  创建一个类
class Star {
    // 类的共有属性放到 constructor 里面 constructor是 构造器或者构造函数
    constructor(uname, age) {
      this.uname = uname;
      this.age = age;
    }//---------------->注意,类里面方法与方法之间不需要添加逗号    
    sing(song) { // 构造方法不需要加function
      console.log(this.uname + '唱' + song);
    }
}
// 2. 利用类创建对象 new
var ldh = new Star('刘德华', 18);
console.log(ldh); // Star {uname: "刘德华", age: 18}
ldh.sing('冰雨'); // 刘德华唱冰雨
```

 以上代码运行结果:

![](images/img5.png)

**注意哟:**

1. 通过class 关键字创建类, 类名我们还是习惯性定义**首字母大写**
2. 类里面有个constructor 函数,可以接受传递过来的参数,同时返回实例对象（**省去return**）
3. constructor 函数 只要 new 生成实例时,就会自动调用这个函数, 如果我们不写这个函数,类也会自动生成这个函数
4. **多个函数方法之间不需要添加逗号分隔**
5. 生成实例 new 不能省略
6. 语法规范, 创建类，类名后面不要加小括号；调用类生成实例，类名后面加小括号； **构造方法不需要加function**



#### 2.2.3 类的继承extends

1. 语法

```js
// 父类
class Father{   
} 

// 子类继承父类
class  Son  extends Father {  
}       
```

2. 示例

```js
class Father {
      constructor(surname) {
        this.surname= surname;
      }
      say() {
        console.log('你的姓是' + this.surname);
       }
}

class Son extends Father{  // 这样子类就继承了父类的属性和方法
}
var damao= new Son('刘');
damao.say();      //结果为 你的姓是刘
```

以上代码运行结果:

![](images/img6.png)

#### 2.2.4 extends + super() 用于调用父类上的构造函数constructor/方法

```js
//定义了父类
class Father {
   constructor(x, y) {
   this.x = x;
   this.y = y;
   }
   sum() {
   console.log(this.x + this.y);
	}
 }
//子元素继承父类
class Son extends Father {
    constructor(x, y) {
        super(x, y); //使用super()才能调用父类中的构造函数
    }
}
var son = new Son(1, 2);
son.sum(); //结果为3
```

##### **注意:**

1. extends 继承中，**调用方法时遵循【就近原则】**

   - 继承中,如果实例化子类输出一个方法,先看子类有没有这个方法,如果有就先执行子类的
   - 继承中,如果子类里面没有,就去查找父类有没有这个方法,如果有,就执行父类的这个方法
   - 如果想在子类里面调用父类的某个xxx方法，就用`super.xxx()`
2. 如果子类想在扩展自己的方法,必须**利用 super 调用父类的构造函数constructor**, super() 必须在子类 this 之前调用（因为**子类没有自己的 `this` 对象**）

**【子类要想使用 this. 必须在使用 this. 之前添加 super( )！！！！！！！！！】**



##### 总结：super( )关键字的作用:

1. 使得子类在**调用父类方法**时，父类的 this. 能够指向子类。进而才能使用父类的方法。

2. 使得子类在编写自己的方法时，能够**使用 this.**



```js
 // 父类有加法方法
 class Father {
   constructor(x, y) {
   this.x = x;
   this.y = y;
   }
   sum() {
   console.log(this.x + this.y);
   }
 }
 // 子类继承父类加法方法 同时 扩展减法方法
 class Son extends Father {
   constructor(x, y) {
   // 利用super 调用父类的构造函数 super 必须在子类this之前调用,放到this之后会报错
   super(x, y);
   this.x = x;
   this.y = y;

  }
  subtract() {
  console.log(this.x - this.y);
  }
}
var son = new Son(5, 3);
son.subtract(); //2
son.sum();//8
```
以上代码运行结果为:

![](images/img7.png)



### 2.2.5 ES6中对象与类的4个注意点

#### 1. 在 ES6 中**类没有变量提升**，所以**必须先定义类，才能通过类实例化对象**

> <img src="images/img2.png" style="zoom: 67%;" />
>
> <img src="images/img1.png" style="zoom: 67%;" />

#### 2. 类里面的共有属性和方法一定要加 this. 使用

>![img8](images/img8.png)
>
>![img9](images/img9.png)

#### 3.  初始化对象后想立马执行的方法，要放在构造函数里写 (同样也要加 this.)

1. 要放在构造函数里写
2. 要加 this.
3. 要加 括号()        【编写某种情况下才触发的话，就不用添加括号()】

>![img10](images/img10.png)

#### 4. this 的指向问题

1. **constructor**中的 this. 指向的是new出来的**实例**对象

2. 类的**方法**，一般也指向的new出来的**实例**对象

3. 函数的 this 指向调用者，所以绑定事件触发的方法中的 this. 指向的就是触发事件的事件源

> ![img11](images/img11.png)

##### 4. 如果咱们就是要调用这个类(实例)的方法，该怎么做呢？

> ![img12](images/img12.png)



## 二、原型链、ES5：继承.call()、数组方法.forEach()、对象方法Object.keys()

## 1.构造函数和原型

在典型的 OOP 的语言中（如 Java），都存在类的概念，类就是对象的模板，对象就是类的实例，但**在 ES6之前，JS 中并没用引入类**的概念。
ES6， 全称 ECMAScript 6.0 ， 2015.06 发版。 但是目前浏览器的 JavaScript 是 ES5 版本，大多数高版本的浏览器也支持 ES6，不过只实现了 ES6 的部分特性和功能。
在 ES6之前 ，对象不是基于类创建的，而是用一种称为**构建函数**的特殊函数来定义对象和它们的特征。  

### 1.1对象的三种创建方式--复习

1. 字面量方式**【注意是用冒号 : ，且没有this：】**

   ```js
   var obj = {
       属性名称：属性值，
       方法名称：function (){
           //函数执行体
       }
   };
   ```

2. new关键字

   ```js
   var obj = new Object();
   obj.属性名称 = 属性值;
   obj.方法名称 = function (){
               //函数执行体
   }
   ```

3. **构造函数**方式**【注意是用 =，且有this：】**

   ```js
   function Person(name,age){
     this.name = name;
     this.age = age;
   }
   var obj = new Person('zs',12);
   ```

### 1.2静态成员和实例成员

构造函数中的属性和方法我们称为成员，成员可以被添加

#### 1.2.1实例成员

**实例成员：**构造函数内部**通过this添加的**成员（只能**通过实例化后的实例对象**来访问）

如下列代码中uname、age、sing 就是实例成员,实例成员只能通过实例化的对象来访问

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
     this.sing = function() {
     console.log('我会唱歌');
    }
}
var ldh = new Star('刘德华', 18);	// 实例化
console.log(ldh.uname);	// 实例成员只能通过实例化的对象来访问
```

#### 1.2.2静态成员

**静态成员：**在**构造函数本身**上继续添加的成员（只能**通过构造函数**来访问）

如下列代码中 sex 就是静态成员,静态成员只能通过构造函数来访问

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
     this.sing = function() {
     console.log('我会唱歌');
    }
}
Star.sex = '男';
var ldh = new Star('刘德华', 18);
console.log(Star.sex);//静态成员只能通过构造函数来访问
```

### 1.3构造函数存在的问题

构造函数方法很好用，但是存在**浪费内存、浪费时间**的问题：

1. 因为在实例化对象时，对象的**方法(函数)**会**单独再开辟一个内存空间来存放复杂数据类型**。

2. 所以用**同一个构造函数实例化多个对象**时，就会造成**开辟多个内存空间，存放同一种方法(函数)**的问题，造成**内存浪费（而且因为存放的地址不一致，所以同一个构造函数实例出来的不同对象的方法，是不相等的）**；而且开辟内存需要花时间，如果实例化对象较多还会造成**时间的浪费**。

![](images/img1.png)

### 1.4构造函数原型(原型对象).prototype

构造函数通过原型分配的**函数**是**所有对象所共享**的。

JavaScript 规定，**每一个构造函数都有一个prototype 属性**，指向另一个对象。注意这个prototype就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。

我们可以把那些不变的方法，直接定义在 prototype 对象上，这样所有对象的实例就可以共享这些方法。



```js
// 1. 构造函数的问题.
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
    // this.sing = function() {
    //     console.log('我会唱歌');
    // }
}
Star.prototype.sing = function () {
    console.log('我会唱歌');
};
var ldh = new Star('刘德华', 18);
var zxy = new Star('张学友', 19);
console.log(ldh.sing === zxy.sing); // true 现在因为存放的地址一致，所以同一个构造函数实例出来的不同对象的方法是相等的
ldh.sing();
zxy.sing();
// 2. 一般情况下,我们的公共属性定义到构造函数里面, 公共的方法我们放到原型对象身上
```

![](images/img7.png)

### 1.5对象原型`.__proto__`

1. 对象都会有一个属性` __proto__` 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 原型对象的属性和方法，就是因为对象有 `__proto__` 原型的存在。
2. `实例.__proto__`和`构造函数.prototype` **是等价**的
   ![i1](images/i1.png)
3. `__proto__`对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个**非标准属性**，因此实际**开发中，不可以使用这个属性**，它只是内部指向原型对象 prototype


![](images/img2.png)



![](images/img3.png)



### 1.6构造函数.constructor

1. 对象原型` .__proto__ `和 构造函数的原型对象`.prototype`里面都有一个` .constructor `属性 ，**.constructor 我们称为构造函数**，因为它**指回构造函数**本身。
2. `.constructor` 主要用于**记录该对象引用于哪个构造函数**，它可以让原型对象 `prototype` 重新指向原来的构造函数。
3. 一般情况下，对象的方法都在构造函数的原型对象` prototype `中设置。如果有多个对象的方法，我们可以直接对` prototype `采取对象形式赋值，但是这样就会覆盖原本的` prototype `，修改后的` prototype `的`.constructor` 就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。

**如果我们修改了原来的原型对象，给原型对象赋值添加方法。则必须手动的利用constructor指回原来的构造函数，才知道这些方法是由哪个构造函数构建的。**如:

```js
 function Star(uname, age) {
     this.uname = uname;
     this.age = age;
 }
 // 对象形式赋值:
 Star.prototype = {
 // 像这样直接给原来的原型对象prototype赋值,则原本prototype自带的constructor也会被覆盖掉,则必须手动添加constructor属性，指回原来的构造函数
   constructor: Star, // 手动添加constructor属性，指回原来的构造函数
   sing: function() {
     console.log('我会唱歌');
   },
   movie: function() {
     console.log('我会演电影');
   }
}
var zxy = new Star('张学友', 19);
console.log(zxy)
```

以上代码运行结果,设置constructor属性如图:

![](images/img8.png)如果未设置constructor属性,如图:

![](images/img9.png)

### 1.7原型链

	每一个实例对象又有一个`__proto__`属性，指向的构造函数的原型对象，构造函数的原型对象也是一个对象，也有`__proto__`属性，这样一层一层往上找就形成了原型链。

**完整版：**

![JS原型链完整版](images/JS原型链完整版.jpg)

**重点版：**

![](images/JS原型链重点版.png)



### 1.8构造函数实例和原型对象三角关系

1. 构造函数的 prototype 属性指向了构造函数原型对象
2. 实例对象是由构造函数创建的,实例对象的`__proto__`属性指向了构造函数的原型对象 prototype
3. 原型对象的`.prototype.constructor`属性指向了构造函数，实例对象的原型的constructor属性也指向了构造函数（`xxx._proto_.constructor`）

![](images/img4.png)



### 1.9原型链和成员的查找机制

**任何对象都有原型对象（也就是prototype属性）任何原型对象也是一个对象，该对象就有`__proto__`属性。**

这样一层一层往上找,就形成了一条链,我们称此为**原型链**。

```html
当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
如果没有就查找它的原型（也就是 __proto__指向的 prototype 原型对象）。
如果还没有就查找原型对象的原型（Object的原型对象）。
依此类推一直找到 Object 为止（null）。
__proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。
```

### 1.10原型对象中this指向

构造函数中的this和原型对象的this,都指向我们new出来的实例对象

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
var that;
Star.prototype.sing = function() {
    console.log('我会唱歌');
    that = this;
}
var ldh = new Star('刘德华', 18);
// 1.在构造函数中,里面this指向的是 实例对象 ldh
console.log(that === ldh);//true
// 2.原型对象函数里面的this指向的是 实例对象 ldh
```

![](images/img6.png)

### 1.11通过原型为数组扩展内置方法

注意：数组和字符串内置对象不能给原型对象覆盖操作 Array.prototype = {xxx:} ，只**能是Array.prototype.xxx = function(){}** 的方式  

```js
 Array.prototype.sum = function() {
   var sum = 0;
   for (var i = 0; i < this.length; i++) {
   sum += this[i];
   }
   return sum;
 };
 //给所有数组类添加sum方法
```



## 2.在ES6之前没有extends用.call继承

ES6之前并没有给我们提供 extends 继承。我们可以通过**构造函数+原型对象**模拟实现继承， 被称为**组合继承**。  

### 2.1 .call()

`fun.call(thisArg, arg1, arg2, ...)  `

- .call() 可以**调用这个函数( fun )**，并且**修改函数运行时 .this 的指向( thisArg )**。

  > thisArg ：当前调用函数 this 的指向对象（如果没有传递该参数，非严格模式下默认为全局对象window；严格模式下默认为undefined）
  > arg1， arg2：传递给fun函数的参数  

```js
 function fn(x, y) {
     console.log(this);
     console.log(x + y);
}
  var o = {
  	name: 'andy'
  };
  fn.call(o, 1, 2);//调用了函数此时的this指向了对象o,
```

![](images/img10.png)

### 2.2子构造函数使用.call继承父构造函数中的[属性和方法]

```js
  // 1.父构造函数
 function Father(uname, age) {
   // this 指向父构造函数的对象实例
   this.uname = uname;
   this.age = age;
   this.money = function () {
         console.log(100000);
   };
 }
  // 2.子构造函数 
function Son(uname, age, score) {
  // this 指向子构造函数的对象实例
  // 3.使用call方式实现子继承父的属性
  Father.call(this, uname, age);
  this.score = score;
}
var son = new Son('刘德华', 18, 100);
console.log(son);
```

**尽管没用到 money 方法，但是 .call 还是继承了下来**

![i2](images/i2.png)



### 2.3 继承父类方法且不干涉父类的原型对象

`Son.prototype = Father.prototype;  `

这样直接赋值会造成一个问题：如果修改了子原型对象,父原型对象也会跟着一起变化

**如果我们想让子类继承父类的方法，并且在给子类添加新方法时，不会影响到父类的原型对象怎么办？**

1. `Son.prototype = new Father();`
   **new 一个 Father 对象，让 Son.prototype 指向它**
2. `Son.prototype.constructor = Son;`
   **如果利用对象的形式修改了原型对象,别忘了利用constructor 指回原来的构造函数**

![利用原型链继承父的方法，且添加子方法时，不会加到父的原型对象中](images/利用原型链继承父的方法，且添加子方法时，不会加到父的原型对象中.png)



```js
// 1. 父构造函数
function Father(uname, age) {
  // this 指向父构造函数的对象实例
  this.uname = uname;
  this.age = age;
}
Father.prototype.money = function() {
  console.log(100000);
};

// 2 .子构造函数 
 function Son(uname, age, score) {
      // this 指向子构造函数的对象实例
      Father.call(this, uname, age);
      this.score = score;
 }

// Son.prototype = Father.prototype;  这样直接赋值会有问题,如果修改了子原型对象,父原型对象也会跟着一起变化
  Son.prototype = new Father();
  // 如果利用对象的形式修改了原型对象,别忘了利用constructor 指回原来的构造函数
  Son.prototype.constructor = Son;

  // 这个是子构造函数专门的方法
  Son.prototype.exam = function() {
    console.log('孩子要考试');
  }
  var son = new Son('刘德华', 18, 100);
  console.log(son);
```

如上代码结果如图:

![](images/img12.png)



## 3.ES5新增方法

### 3.1 数组方法.forEach()遍历数组

`arr.forEach((x, y, z) => console.log(x, y, z));`

- 相当于数组遍历的 for循环 **没有返回值**

```js
 arr.forEach(function(value, index, array) { // 这3个参数可以随意取名字
       //参数一是:数组元素
       //参数二是:数组元素的索引
       //参数三是:当前的数组
     console.log(value); //打印每个数组元素
     console.log(index); //打印数组元素的索引号
     console.log(array); //打印操作的数组本身
 })
  //相当于数组遍历的 for循环 没有返回值
```

### 3.2 数组方法.filter()筛选数组

- filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，主要用于筛选数组
- 注意它直接**返回一个新数组**  ，记得return

```js
  var arr = [12, 66, 4, 88, 3, 7];
  var newArr = arr.filter(function(value, index,array) { //返回新数组，所以赋值
  	 //参数一是:数组元素
     //参数二是:数组元素的索引
     //参数三是:当前的数组
     return value >= 20; //筛选条件，记得return
  });
  console.log(newArr);//[66,88] //返回值是一个新数组
```

### 3.3 数组方法.some()

- some() 方法用于检测数组中的元素是否满足指定条件. 通俗点 查找数组中是否有满足条件的元素
- 注意它**返回值是布尔值**, 如果查找到这个元素, 就返回true , 如果查找不到就返回false.

- 如果**找到第一个满足条件的元素就终止循环**，不再继续查找.  

```js
 var arr = [10, 30, 4];
 var flag = arr.some(function(value,index,array) {
     //参数一是:数组元素
     //参数二是:数组元素的索引
     //参数三是:当前的数组
     return value < 3;
  });
console.log(flag);//false返回值是布尔值,只要查找到满足条件的一个元素就立马终止循环
```



### 3.4 some和forEach、filter区别

- 如果查询数组中唯一的元素, 用some方法更合适,在some 里面 遇到 return true 就是终止遍历 迭代效率更高
- **在 .forEach 和 .filter 里面 return 不会终止迭代**，只会使得这次循环后面的代码不再执行，直接跳到下一个元素的循环



### 3.5 筛选商品案例

1. 把数据渲染到页面中 (forEach)
2. 根据价格显示数据 (filter)  
3. 根据商品名称显示数据

#### 3.5.1. 定义数组对象数据

   ```js
   var data = [{
               id: 1,
               pname: '小米',
               price: 3999
           }, {
               id: 2,
               pname: 'oppo',
               price: 999
           }, {
               id: 3,
               pname: '荣耀',
               price: 1299
           }, {
               id: 4,
               pname: '华为',
               price: 1999
           }, ];
   ```

#### 3.5.2. 使用forEach遍历数据并渲染到页面中

   ```js
   function setDate(mydata) {
       tbody.innerHTML = '';	// 先清空原来 tbody 里面的数据，否则会重复
       mydata.forEach(function (value) {
           // console.log(value);
           var tr = document.createElement('tr');
           tr.innerHTML =
               '<td>' +
               value.id +
               '</td><td>' +
               value.pname +
               '</td><td>' +
               value.price +
               '</td>';
           tbody.appendChild(tr);
       });
   }
   ```

#### 3.5.3. 根据价格使用.filter筛选数据

   1. **获取到搜索按钮并为其绑定点击事件**

      ```js
      var search_price = document.querySelector('.search-price');
      var start = document.querySelector('.start');
      var end = document.querySelector('.end');
      ```

   2. **使用filter将用户输入的价格信息筛选出来**

      ```js
      search_price.addEventListener('click', function() {
          var newDate = data.filter(function(value) {
              //start.value是开始区间
              //end.value是结束的区间
              return value.price >= start.value && value.price <= end.value;
          });
          // 把筛选完之后的对象渲染到页面中
          setDate(newDate);
       });
      ```

   3. **将筛选出来的数据重新渲染到表格中**

      1. 将渲染数据的逻辑封装到一个函数中

         ```js
         function setDate(mydata) {
               // 先清空原来tbody 里面的数据
           tbody.innerHTML = '';
           mydata.forEach(function(value) {
             var tr = document.createElement('tr');
             tr.innerHTML = '<td>' + value.id + '</td><td>' + value.pname + '</td><td>' + value.price + '</td>';
               tbody.appendChild(tr);
           });
          }
         ```

      2. 将筛选之后的数据重新渲染

         ```js
          search_price.addEventListener('click', function() {
              var newDate = data.filter(function(value) {
              return value.price >= start.value && value.price <= end.value;
              });
              console.log(newDate);
              // 把筛选完之后的对象渲染到页面中
              setDate(newDate);
         });
         ```

#### 3.5.4. 根据商品名称使用.some筛选

```js
  1. 获取用户输入的商品名称
var product = document.querySelector('.product');
var search_pro = document.querySelector('.search-pro');
  2. 为查询按钮绑定点击事件,将输入的商品名称与这个数据进行筛选
search_pro.addEventListener('click', function() {
    var arr = []; // 因为some只能返回布尔值，所以用这个数组接收some返回的结果
    data.some(function(value) {
        if (value.pname === product.value) {
            // console.log(value);
            arr.push(value);
            return true; // return true之后就不再执行some循环
        }
    });
    // 把拿到的数据渲染到页面中
    setDate(arr);
})
```



### 3.6 trim方法去除字符串两端的空格(判断输入内容是否为空)

~~~js
var input = document.querySelector('input');
var btn = document.querySelector('button');
var div = document.querySelector('div');
btn.onclick = function () {
        if (input.value === '') {	//用户输入全是空格时依然会判定成功
          alert('请输入内容');
        } else {
          div.innerHTML = str;
        }
      };
~~~

```js
btn.onclick = function () {
    var str = input.value.trim();
    if (str === '') {	//这样能解决 用户输入全是空格依然判定成功的bug
        alert('请输入内容');
    } else {
        div.innerHTML = str;
    }
};
```



### 3.7 Object.keys(对象) 获取对象的属性名

- Object.keys(对象) 获取到当前对象中的属性**名**

- **返回由属性名组成的数组(因为返回的是数组，可以和.forEach()等方法搭配使用)**

```js
 var obj = {
     id: 1,
     pname: '小米',
     price: 1999,
     num: 2000
};
var result = Object.keys(obj)
console.log(result)//[id，pname,price,num]
```

### 3.8 Object.defineProperty()

Object.defineProperty() 定义新属性或修改原有的属性

`Object.defineProperty(obj, prop, descriptor)`

- **obj：**必需。目标对象
- **prop：**必需。需定义或修改的属性名
- **descriptor：**必需。目标属性所拥有的特性

Object.defineProperty() 第三个参数 descriptor 说明：
				**第三个参数 descriptor 是一个对象{ }**

- **value:** 设置属性的值，**默认为undefined**
- **writable:** 值是否可以重写。 true | false **默认为false**
- **enumerable:** 目标属性是否在遍历的时候被选出来。 true | false **默认为false**
- **configurable:** 目标属性是否可以被删除、是否可以再次修改**特性（能不能再用Object.defineProperty()改它特性）** true | false 默认为false

~~~js
// 1. 以前的对象添加和修改属性的方式
// obj.num = 1000;
// obj.price = 99;
// console.log(obj);
// 2. Object.defineProperty() 定义新属性或修改原有的属性
Object.defineProperty(obj, 'num', {
    value: 1000,
    enumerable: true,
});
console.log(obj);
Object.defineProperty(obj, 'price', {
    value: 9.9,
});
console.log(obj);
Object.defineProperty(obj, 'id', {
    // 如果值为false 不允许修改这个属性值 默认值也是false
    writable: false,
});
obj.id = 2;
console.log(obj);
Object.defineProperty(obj, 'address', {
    value: '中国山东蓝翔技校xx单元',
    // 如果只为false 不允许修改这个属性值 默认值也是false
    writable: false,
    // enumerable 如果值为false 则不允许遍历, 默认的值是 false
    enumerable: false,
    // configurable 如果为false 则不允许删除这个属性 不允许在修改第三个参数里面的特性 默认为false
    configurable: false,
});
console.log(obj);
console.log(Object.keys(obj));
delete obj.address;
console.log(obj);
delete obj.pname;
console.log(obj);
Object.defineProperty(obj, 'address', {
    value: '中国山东蓝翔技校xx单元',
    // 如果只为false 不允许修改这个属性值 默认值也是false
    writable: true,
    // enumerable 如果值为false 则不允许遍历, 默认的值是 false
    enumerable: true,
    // configurable 如果为false 则不允许删除这个属性 默认为false
    configurable: true,
});
console.log(obj.address);
~~~



## 三、this指向、严格模式、.call()、.apply()、.bind()、闭包、作用域、递归、深拷贝浅拷贝

## 1.函数的定义和调用

### 1.1函数的定义方式

1. 方式1 函数声明方式 function 关键字 (命名函数)

   ```js
   function fn(){}
   ```

2. 方式2 函数表达式(匿名函数)

   ```js
   var fn = function(){}
   ```

3. 方式3 new Function() 

   ```js
   var f = new Function('a', 'b', 'console.log(a + b)');
   f(1, 2);
   
   var fn = new Function('参数1','参数2'..., '函数体')
   注意
   /*Function 里面参数都必须是字符串格式
   第三种方式执行效率低，也不方便书写，因此较少使用
   所有函数都是 Function 的实例(对象)  
   函数也属于对象
   */
   ```

### 1.2函数的调用

```js
/* 1. 普通函数 */
function fn() {
	console.log('人生的巅峰');
}
 fn(); 
/* 2. 对象的方法 */
var o = {
  sayHi: function() {
  	console.log('人生的巅峰');
  }
}
o.sayHi();
/* 3. 构造函数*/
function Star() {};
new Star();
/* 4. 绑定事件函数*/
 btn.onclick = function() {};   // 点击了按钮就可以调用这个函数
/* 5. 定时器函数*/
setInterval(function() {}, 1000);  这个函数是定时器自动1秒钟调用一次
/* 6. 立即执行函数(自调用函数)*/
(function() {
	console.log('人生的巅峰');
})();
```



## 2.this

### 2.1函数内部的this指向

这些 this 的指向，是当我们调用函数的时候确定的。调用方式的不同决定了this 的指向不同

一般指向我们的调用者.

![](images/img1.png)



### setInterval() / setTimeout() 若想处理外部的变量，一定要用【不带形参的匿名函数/箭头函数】



#### 错误做法：

如果像下面这样把传入 setInterval()  的函数 flag 定义在外面，

那么传入外部变量n的时候，相当于**只是传了一下当前n的值，并没有把n的地址传进去！！！**

~~~js
var timer = null;
let n = 10;
timer = setInterval(flag, 200, n);

function flag(x) {
    x -= 1;
    console.log(x); // 一直打印9
    console.log(n); // 一直打印10
    if (x == 0) clearInterval(timer);
}
~~~



#### 问题原因

这是由于 setTimeout() 调用的代码**运行在与当前函数完全分离的执行环境上**。

**导致 setTimeout() 中的 `this` 关键字会指向 `window` (或`全局`)对象。**详细可参考[MDN setTimeout](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout)



#### 正确做法：（注意，箭头函数/匿名函数不能写任何形参！！！）：

~~~js
法1 箭头函数：
var timer = null;
let n = 10;
timer = setInterval(
    () => {	// 注意！这里不能写任何形参！！！
        n -= 1;
        console.log(n);
        if (n == 0) clearInterval(timer);
    },
    200,
    n // 这里已经把n传进去了
);
------------------------------------------------------------------------------------
法2 匿名函数：
var timer = null;
let n = 10;
timer = setInterval(
    function () {	// 注意！这里不能写任何形参！！！
        n -= 1;
        console.log(n);
        if (n == 0) clearInterval(timer);
    },
    200,
    n // 这里已经把n传进去了
);
~~~

如果你写了形参，那还是会出错（一直打印9）

~~~js
var timer = null;
let n = 10;
timer = setInterval(
    (x) => {
        x -= 1;
        console.log(x); // 一直打印9
        if (x == 0) clearInterval(timer);
    },
    200,
    n
);
------------------------------------------------------------------------------------
var timer = null;
let n = 10;
timer = setInterval(
    function (x) {	
        x -= 1;
        console.log(x); // 一直打印9
        if (x == 0) clearInterval(timer);
    },
    200,
    n
);
~~~







### 2.2改变函数内部 this 指向

#### 2.2.1 .call()方法

- **`call()`** 方法使用一个指定的 `this` 值和参数来调用一个函数。

call() 方法的作用和 apply() 方法类似，区别就是`call()`方法接受的是**参数列表**，而`apply()`方法接受的是**一个参数数组**。

- **返回值：**有 return 的话返回 return，没有则返回 undefined

```js
fn.call(thisArg, arg1, arg2, ...)
        
thisArg
可选的。在 function 函数运行时使用的 this 值。请注意，this可能不是该方法看到的实际值：如果这个函数处于非严格模式下，则指定为 null 或 undefined 时会自动替换为指向全局对象，原始值会被包装。
        
arg1, arg2, ...
fn需要的参数。
```

应用场景:  经常用来继承：

```js
var o = {
	name: 'andy'
}
 function fn(a, b) {
      console.log(this);
      console.log(a+b)
};
fn(1,2)// 此时的this指向的是window 运行结果为3
fn.call(o,1,2)//此时的this指向的是对象o,参数使用逗号隔开,运行结果为3
```

以上代码运行结果为:

![](images/img4.png)



#### 2.2.2 .apply()方法

- **`apply()`** 方法调用一个具有给定`this`值的函数，以及以一个**数组（或[类数组对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#working_with_array-like_objects)）的形式**提供的参数。
- **返回值：**有 return 的话返回 return，没有则返回 undefined

```js
func.apply(thisArg, [argsArray])
```

应用场景:  经常跟数组有关系：

```js
// 2. apply()  应用 运用的意思
var o = {
    name: 'andy',
};

function fn(arr) {
    console.log(this);
    console.log(arr); // 'pink'
}
fn.apply(o, ['pink']);
// 1. 也是调用函数 第二个可以改变函数内部的this指向
// 2. 但是他的参数必须是数组(伪数组)
// 3. apply 的主要应用 比如说我们可以利用 apply 借助于数学内置对象求数组最大值
// Math.max(1,2,3); 原本的Math.max() 是要传入好几个参数的
var arr = [1, 66, 3, 99, 4];
var max = Math.max.apply(Math, arr); // 我们使用的是Math对象的max方法，并且不需要改变this指向，所以还是指回Math
var min = Math.min.apply(Math, arr);
console.log(max, min);
```



#### 2.2.3 .bind()方法

- **`bind()`**方法**不会调用函数**，但是**能改变函数内部 .this 指向**

- **返回值：原函数改变 this 之后产生的新函数**，所以记得要赋值给变量才能使用

应用场景：不立即调用函数，但想改变this指向（比如setTimeout 定时器函数）

```js
 var o = {
 name: 'andy'
 };

function fn(a, b) {
	console.log(this);
	console.log(a + b);
};
var f = fn.bind(o, 1, 2); //此处的f是bind返回的新函数
f();	//调用新函数  this指向的是对象o 参数使用逗号隔开
```

~~~js
// 4. 我们有一个按钮,当我们点击了之后,就禁用这个按钮,3秒钟之后开启这个按钮
var btns = document.querySelectorAll('button');
for (var i = 0; i < btns.length; i++) {
    btns[i].onclick = function() {
        this.disabled = true;
        setTimeout(function() {
            this.disabled = false; // 定时器函数里面的this 原本指向的是window
        }.bind(this), 2000); // 这个this 在setTimeout之外，在onclick之内，指向的是 btns 这个对象
    }
}
~~~



#### 2.2.4 call、apply、bind三者的异同

- 共同点 : 都可以改变this指向
- 不同点：
  - .call 和 .apply 传递的参数不一样,**call传递参数使用逗号隔开,apply使用数组传递**
  - .call 和 .apply 会调用函数, .bind  **不会调用函数**
  - .call 和 .apply **返回 return或者undefined**；.bind **返回一个 修改this之后的函数**


- 应用场景：
  1. call 经常做**继承**. 
  2. apply经常跟**数组**有关系.  比如借助于数学对象实现数组最大值最小值
  3. bind  不调用函数,但是还想改变this指向. 比如改变**定时器**内部的this指向. 



## 3.严格模式

### 3.1什么是严格模式

JavaScript 除了提供正常模式外，还提供了严格模式（strict mode）。ES5 的严格模式是采用具有限制性 JavaScript变体的一种方式，即在严格的条件下运行 JS 代码。

严格模式在 IE10 以上版本的浏览器中才会被支持，旧版本浏览器中会被忽略。

严格模式对正常的 JavaScript 语义做了一些更改： 

1.消除了 Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为。

2.消除代码运行的一些不安全之处，保证代码运行的安全。

3.提高编译器效率，增加运行速度。

4.禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class,enum,export, extends, import, super 不能做变量名

### 3.2开启严格模式

严格模式可以应用到整个脚本或个别函数中。因此在使用时，我们可以将严格模式分为为脚本开启严格模式和为函数开启严格模式两种情况。

- 情况一 :为脚本开启严格模式

  - 有的 script 脚本是严格模式，有的 script 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他
    script 脚本文件。

    ```html
    
    //或者 
    <script>
      　'use strict'; //当前script标签开启了严格模式，单引号双引号都行
    </script>
    
    <script>
        (function (){
          //在当前的这个自调用函数中有开启严格模式，当前函数之外还是普通模式
            "use strict";
               var num = 10;
            function fn() {}
        })();
    </script>
    ```

- 情况二: 为函数开启严格模式

  - 要给某个函数开启严格模式，需要把“use strict”;  (或 'use strict'; ) 声明放在函数体所有语句之前。

    ```js
    function fn(){
    　　"use strict";
    　　return "123";
    } 
    //当前fn函数开启了严格模式
    ```

### 3.3严格模式中的变化

严格模式对 Javascript 的语法和行为，都做了一些改变。

```js
'use strict'

// 1. 我们的变量名必须先声明再使用
num = 10 
console.log(num)//严格模式后使用未声明的变量
--------------------------------------------------------------------------------
// 2.我们不能随意删除已经声明好的变量
var num2 = 1;
delete num2;//严格模式不允许删除变量
--------------------------------------------------------------------------------
// 3. 严格模式下全局作用域中函数中的 this 是 undefined。
function fn() {
 console.log(this); // undefined。
}
fn();  
---------------------------------------------------------------------------------
// 4. 严格模式下,如果构造函数不加new，直接调用, 则会报错 (this 指向的是undefined)
function Star() {
	 this.sex = '男';
}
Star(); // 报错
----------------------------------------------------------------------------------
// 5. 严格模式下，定时器 this 还是指向 window 
setTimeout(function() {
  console.log(this); 	// 指向 window
}, 2000);  
-----------------------------------------------------------------------------
// 6. 严格模式下函数里面的参数不允许有重名
function fn(a, a) {		// 报错
    console.log(a + a);
};
fn(1, 2); 
-----------------------------------------------------------------------------
// 7.函数必须声明在顶层.新版本的 JavaScript 会引入“块级作用域”（ ES6 中已引入）。为了与新版本接轨，
不允许在非函数的代码块内声明函数
```

[更多严格模式要求参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)



## 4.高阶函数

高阶函数是对其他函数进行操作的函数，它接收函数作为参数或将函数作为返回值输出。

![](images/img2.png)

此时fn 就是一个高阶函数

函数也是一种数据类型，同样可以作为参数，传递给另外一个参数使用。最典型的就是作为回调函数。

同理**函数也可以作为返回值传递**回来



## 5.  作用域、闭包

### 5.0 **ES6块级作用域：**

每个{}大括号内就算一个块级作用域 ❎

**每个函数内**，或者**用 let / const 定义的变量 / 常量** 存在一个块级作用域 ✅



#### 5.0.1 作用域链

内部函数访问外部函数的变量，采取的是链式查找

**根据作用域链从函数内往外找，来决定 变量/方法 取哪一个值（哪怕是undefined也算找到）**

~~~js
function fun() {
    window.a = 10
    console.log(a) // 打印undefined
    var a = 20     // 注意这里有变量提升，打印undefined只不过是因为“作用域链”
}
fun()


function fun() {
    a = 10  // 如果是不加var，是先执行window.a = 10呢？还是变量提升var a呢？
    console.log(a) // 答案是先变量提升var a，那么a = 10 就不能解释成window.a = 10 了
    var a = 20
    }
fun() // 所以打印10 
~~~



#### 5.0.2 连续声明变量

连续声明变量时，没有用 var / let / const  声明的，**相当于在全局声明（window.xxx）**

~~~js
function test(){
    var a = 1, b = 1;
    return b;
}
function test1(){
    var a1 = b1 = 1; // 相当于先 window.b1 = 1	然后 var a1 = b1
}
test();
// console.log(a); // undefined a是局部的
// console.log(b); // undefined b是局部的

test1();
// console.log(a1)；// undefined a1是局部的
console.log(b1); // 1 说明b1是全局的，相当于 window.b1 = 1
~~~



#### 5.0.3 var 的变量声明提升

JS引擎运行.js分为2步：**预解析**、代码执行

1. 预解析：js引擎会把.js	里面的所有 **var  和  function**  提到**当前作用域**的最前面

~~~js
var name = 'a';
(function () {
    if (typeof name == 'undefined') {
        var name = 'b'
        console.log('111' + name)
    } else {
        console.log('222' + name)
    }
})()
// 结果是 111b
因为if else 虽然有{}，但它不是函数，所以没有块级作用域，它处在 立即执行函数的块级作用域
所以 立即执行函数的作用域 只要发现里面有 var 哪怕判断条件不对，都会先把 var 提升到当前作用域上面声明

上面的例子相当于
var name = 'a';
(function () {
    var name	// 变量声明提升
    if (typeof name == 'undefined') {
        name = 'b'
        console.log('111' + name)
    } else {
        console.log('222' + name)
    }
})()
~~~

2. 代码执行：按照书写顺序从上往下执行

~~~js
function fun() {
    a = 10
}
fun()
console.log(a)
// 10
----------------------------------------------------------------------------
即使函数声明提升了，但是代码执行顺序从上往下，都还没到执行函数内部的时候呢
console.log(a)
function fun() {
    a = 10
}
fun()
// 报错，a未定义
~~~



#### 5.0.4 预解析的执行顺序

预解析分为：变量预解析（变量提升）和  函数预解析（函数提升）

1. 变量（包括函数表达式）提升：只提升变量声明，不提升变量赋值

2. 函数提升：只提升函数(function)声明，不调用函数

3. **js代码执行顺序**：传入的参数 > 函数提升 > 变量提升(只声明不赋值) >  window. （你连声明都没声明就直接赋值，我才挂到 window. 上） 

   **传参赋值 会优先于 变量提升 执行**
   变量提升中，**函数声明 会优先于 变量声明 执行**

~~~js
 函数声明和赋值相当于是一起执行的！！！
function fun() {
    console.log(a)
    var a
    function a() {
        return 666
    }
}
fun()
// 打印 ƒ a() {return 666}
所以上面相当于
function fun() {
    function a() {
        return 666
    }
    var a
    console.log(a)
}
fun()
----------------------------------------------------------------------------
 传参赋值 先于函数变量提升执行；又因为函数声明和赋值相当于是一起执行的，所以被函数覆盖
function fun(a) {
    function a() {
        return 666
    }
    console.log(a)
}
fun(100)
// 打印 ƒ a() {return 666}
----------------------------------------------------------------------------
 函数提升 > 变量提升
function fun() {
    var a = 10
    function a() {}
    console.log(a) // 结果是 10
}
fun()

上面例子相当于
function fun() {
    function a() {}
    var a 	// 注意，此时a 是 ƒ a() {}，并不是undefined
    a = 10	// 后面才赋值成了10
    console.log(a)
}
fun()
----------------------------------------------------------------------------
 变量提升 > window. 
function fun() {
    a = 10
    console.log(a) // 打印 10
    var a = 20
    }
fun()

上面例子相当于
function fun() {
    var a	// 优先于 window. 
    a = 10
    console.log(a) // 打印 10
	a = 20
    }
fun()
----------------------------------------------------------------------------
 综合起来：传入的参数 > 函数提升 > 变量提升(只声明不赋值) >  window. 
function fun(a) {
    console.log(a)
    var a = 10
    function a() {
        return 666
    }
}
fun(100)
// 打印 ƒ a() {return 666}

所以上面相当于
function fun(a) {
    var a = 100
    function a() {
        return 666
    }
    var a
    console.log(a)
    a = 10
}
fun(100)
~~~



~~~js
参数 > 变量
function fun(a) {
    var a
    console.log(a)
    a = 10
}
fun(100)
// 打印 100
----------------------------------------------------------------------------
函数 > 变量
function fun() {
    function a() {
        return 666
    }
    var a
    console.log(a)
    a = 10
}
fun()
// 打印 ƒ a() {return 666}
~~~



4. 声明变量**并不是调到最前面**，而是紧跟在**同级的，原本就有的声明之后**

~~~js
var a = 18;	// 拆分成 var a; 和 a = 18;
fun();
function fun() {
    var b = 9;
    console.log(a);
    console.log(b);
    var a = '123';
}

// 相当于以下代码
var a;
function fun() {	// 函数并不是调到最前面，而是紧跟在原本就有的声明之后
          	var b;
    		var a; // a并不是调到最前面，而是紧跟在原本就有的声明之后
    		b = 9;
          	console.log(a);
          	console.log(b);
          	a = '123';
      }
a = 18 ;
fun();
// 最后打印 undefined 和 9
~~~



面试题：

~~~js
f1();
console.log(c);
console.log(b);
console.log(a); 
function f1() {
        var a = b = c = 9;	//相当于a有声明，局部变量；b和c没声明，是全局变量
        console.log(a);
        console.log(b);
        console.log(c);
      }
//输出5个9，最后报错
~~~



#### 5.0.5 let / const 的暂时性死区，类似变量提升

原文链接：https://blog.csdn.net/qq_58875046/article/details/123067627

~~~js
var a = 456;
(function() {
    console.log(a)
    let a=123
})()

如果let没有变量提升的话输出的应该是456
但是如果你执行代码的话会报错 Cannot access 'a' before initialization 初始化前无法访问“a”

想不到吧！从这里其实可以看出let存不存在变量提升有争议了，值在变量显式赋值之前不能对变量进行读写，否则就会报错，这也就是所谓的let和const的暂时性死区。
~~~

##### 暂存死区

与通过  var 声明的有初始化值 undefined 的变量不同，通过 let 声明的变量直到它们的定义被执行时才初始化。在变量初始化前访问该变量会导致 ReferenceError。该变量处在一个自块顶部到初始化处理的“暂存死区”中。

看过很多文章后用大佬的话做下总结

1. let有无变量提升取决于你如何定义变量提升。 若[变量提升」是指变量可在声明语句之前被调用，则let没有变量提升；若[变量提升」是指变量在声明语句之前就被执行上下文记住，则let有变量提升。【**let 声明的变量，虽然不能在声明前知道它的值，但是能让上下文知道存在这个变量**】

2. JS代码是即时编译与执行的，一个函数作用域会拥有一个执行上下文，执行上下文是一块存储空间。**执行上下文内又有名为「变量环境」和「词法环境」2个环境。**

3. 由**var和function**声明的变量，在代码编译完成后，执行之前，其变量名和值就被存储在**「变量环境」**中了，所以在代码执行阶段的任何时刻，都可以调用它们，自然也能在声明语句之前调用了。

4. 由**const和let**声明的变量，在代码编译完成后、执行之前，其变量名被存储在**「词法环境」**中，代码执行过程中会从**依据【词法环境→变量环境→闭包/上一个作用域】的顺序来查找变量**，而**词法环境所存储的值被要求只有在声明语句之后才能调用**。所以会存在暂时性死区，但变量又确确实实被执行上下文提前记住了，所以可以把暂时性死区理解为「变量暂时不能使用的阶段」。所以得出结论①





### 5.1 JS的两个作用域(闭包、this )

[https://tsejx.github.io/javascript-guidebook/](https://tsejx.github.io/javascript-guidebook/core-modules/executable-code-and-execution-contexts/compilation/lexical-scope)

作用域共有两种主要的工作模式：

1. 词法作用域/静态作用域（JS）

2. 动态作用域（.this）

JavaScript 采用的是 **词法作用域**（Lexical Scope），也称为 **静态作用域**。

因为 JavaScript 采用的是词法作用域，因此函数的作用域在函数**定义的时候就决定**了。

> 
>
> 那为什么要介绍动态作用域呢？
>
> 
>
> 实际上动态作用域是 JavaScript 另一个重要机制 [this](https://tsejx.github.io/javascript-guidebook/core-modules/executable-code-and-execution-contexts/execution/this) 的表亲。作用域混乱多数是因为词法作用域和 `this` 机制相混淆。
>
> **动态作用域** 并不关心函数和作用域是如何声明以及在何处声明，它只关心它们从何处调用。
>
> 换句话说，[作用域链](https://tsejx.github.io/javascript-guidebook/core-modules/executable-code-and-execution-contexts/execution/scope-chain) 是基于 **调用栈** 的，而不是代码中的作用域嵌套。
>
> 



##### 总结：

https://www.bilibili.com/video/BV1Kv411778c

闭包：词法作用域 -> 定义时确定

this：动态作用域 -> 调用时确定



牢记：词法作用域是在 **定义** 时确定的，而动态作用域是在 **运行** 时确定的



~~~js
const a = 2;

function foo() {
    console.log(a);
}

function bar() {
    const a = 3;
    foo();
}

bar(); // 2 (词法作用域)

- 如果处于词法作用域，变量 a 首先在 foo 函数中查找，没有找到。于是 顺着作用域链到全局作用域 中查找，找到并赋值为 2。所以控制台输出 2
- 如果处于动态作用域，同样地，变量 a 首先在 foo 中查找，没有找到。这里会 顺着调用栈 在调用 foo 函数的地方，也就是 bar 函数中查找，找到并赋值为 3。所以控制台输出 3
~~~



### 5.2什么是闭包

闭包（closure）指有权访问另一个函数作用域中变量的函数。简单理解就是 ，一个作用域可以访问另外一个函数内部的局部变量。 

**自己的局部变量被另一个函数用的，才是闭包函数**

![](images/img3.png)

### 5.3闭包的作用

作用：**延伸变量的作用范围**



~~~js
function test() {
    const a = 1;
    return function () {
        console.log('a', a);
    };
}
const fn = test();
const a = 2;
fn(); // a 1


function test(fn) {
    const a = 1;
    fn();
}
const a = 2;
function fn() {
    console.log('a', a);
}
test(fn); // a 2
~~~



```js
 function fn() {
   var num = 10;
   function fun() {
       console.log(num);
 	}
    return fun;	// 使用return 把局部变量传递出去，使得num局部变量不会立即销毁，它会等全部函数都调用完了才销毁
 }
// 使得全局作用域可以调用局部变量num
var f = fn();
f();
```

### 5.4闭包的案例

#### 5.4.1 利用闭包的方式得到当前 li 的索引号

重点：利用**立即执行函数**

```js
// 闭包应用-点击li输出当前li的索引号
// 1. 我们可以利用动态添加属性的方式
var lis = document.querySelector('.nav').querySelectorAll('li');
for (var i = 0; i < lis.length; i++) {
    lis[i].index = i;	// 方法1.的重点在这
    lis[i].onclick = function() {
        // console.log(i);
        console.log(this.index);
    }
}

// 2. 利用闭包的方式得到当前小li 的索引号
for (var i = 0; i < lis.length; i++) {
    // 利用for循环创建了4个立即执行函数
    // 立即执行函数也称为小闭包；因为立即执行函数里面的任何一个函数都可以使用立即执行函数的k变量
    (function(k) {	
        lis[k].onclick = function() {
            console.log(k);
        }
    })(i);	// 方法2.的重点在这；立即执行函数()()第二个括号可以传入参数
}

// 3. 使用ES6的let
var lis = document.querySelector('.nav').querySelectorAll('li');
      for (let i = 0; i < lis.length; i++) { // 方法3.的重点在于把var i改成let i
        lis[i].onclick = function () {
          console.log(i);
        };
      }
```



#### 5.4.2 3秒钟之后,打印所有li元素的内容

```js
 for (var i = 0; i < lis.length; i++) {
   (function(k) {
     setTimeout(function() {
     console.log(lis[k].innerHTML);
     }, 3000)
   })(i);
}
```



#### 5.4.3 闭包应用-计算打车价格

```js
/*需求分析
打车起步价13(3公里内),  之后每多一公里增加 5块钱.  用户输入公里数就可以计算打车价格
如果有拥堵情况,总价格多收取10块钱拥堵费*/

 var car = (function() {
     var start = 13; // 起步价  局部变量
     var total = 0; // 总价  局部变量
     return {
       // return的是一个对象，该对象里面含有2种不同的方法
       price: function(n) {
         if (n <= 3) {
           total = start;
         } else {
           total = start + (n - 3) * 5
         }
         return total;
       },
       // 拥堵之后的费用
       yd: function(flag) {
         return flag ? total + 10 : total;
       }
	}
 })();
console.log(car.price(5)); // 23	像调用对象一样调用return里面2种不同的方法
console.log(car.yd(true)); // 33
```

### 5.5 retun 一个函数，产生闭包

- 一般来说，**return 一个函数**，才能为执行闭包函数里面的函数创造条件，才会产生闭包（这也是为啥第4章要先提一下高阶函数）

~~~js
function makeFunc() {
    var name = 'Mozilla';
    function displayName() {
        alert(name);
    }
    return displayName;
}

makeFunc();		//光是这样，是不能调用displayName()这个内部函数的

makeFunc()();	//通过立即执行函数，就能调用displayName()

var myFunc = makeFunc();
myFunc();		
/* 
这样也能调用displayName()
以上代码相当于：
1.先执行myFunc()；但是由于myFunc = makeFunc()，所以myFunc需要等makeFunc()返回值返回后再执行
2.然后执行makeFunc()，返回了displayName() 这个函数
3.再回过头来执行myFunc()，也就是执行了displayName()   
*/
~~~

- 有些操作**必须要执行一个函数，比如DOM事件**，这时候 return 一个函数 就非常重要了：

~~~html
<body>
    <a href="#" id="size-12">12</a>
    <a href="#" id="size-14">14</a>
    <a href="#" id="size-16">16</a>
    
    <script type="module">
        function makeSizer(size) {
                document.body.style.fontSize = size + 'px';
        }
        document.getElementById('size-12').onclick = makeSizer(12);
        document.getElementById('size-14').onclick = makeSizer(14);
        document.getElementById('size-16').onclick = makeSizer(16);
        // 这样是不能达到点击按钮切换字体大小的效果的
    </script>
</body>
---------------------------------------------------------------------------------
<body>
    <a href="#" id="size-12">12</a>
    <a href="#" id="size-14">14</a>
    <a href="#" id="size-16">16</a>
    
    <script type="module">
        function makeSizer(size) {
            return function () {	// return 一个函数 就可以了
                document.body.style.fontSize = size + 'px';
            };
        }
        document.getElementById('size-12').onclick = makeSizer(12);
        document.getElementById('size-14').onclick = makeSizer(14);
        document.getElementById('size-16').onclick = makeSizer(16);
    </script>
</body>
~~~

案例对比：

```js
var name = "The Window";
var object = {
    name: "My Object",
    getNameFunc: function() {
        return function() {
            return this.name;
        };
    }
};

console.log(object.getNameFunc()())
// 打印出来的是The Window

以上代码相当于：
1.先执行第一个括号，也就是先执行 object.getNameFunc()	
2.然后object.getNameFunc()返回了一个 “函数”
3.再执行第二个括号，也就是再执行 “函数”()

----------------------------------------------------------------------------------
var name = 'The Window';
var object = {
    name: 'My Object',
    getNameFunc: function () {
        var that = this;
        return function () {
            return that.name;
        };
    },
};
console.log(object.getNameFunc()());
// 打印出来的是My Object

以上代码相当于：
1.先执行第一个括号，也就是先执行 object.getNameFunc()	
2.然后var that = this; 之后object.getNameFunc()再返回一个 “函数”，
  因为等一下要执行的“函数”里面含有getNameFunc()的局部变量的that，所以它是闭包函数
3.再执行第二个括号，也就是再执行 “函数”()

```







## 6.递归、深拷贝

### 6.1什么是递归

**递归：**如果一个函数在内部可以调用其本身，那么这个函数就是递归函数。简单理解:函数内部自己调用自己, 这个函数就是递归函数

**注意：**递归函数的作用和循环效果一样，由于递归很容易发生“栈溢出”错误（stack overflow），所以必须要加退出条件return。

### 6.2利用递归求1~n的阶乘

```js
//利用递归函数求1~n的阶乘 1 * 2 * 3 * 4 * ..n
 function fn(n) {
     if (n == 1) { //结束条件
       return 1;
     }
     return n * fn(n - 1);
 }
 console.log(fn(3));
```

![](images/img6.png)

### 6.3利用递归求斐波那契数列

```js
// 利用递归函数求斐波那契数列(兔子序列)  1、1、2、3、5、8、13、21...
// 用户输入一个数字 n 就可以求出 这个数字对应的兔子序列值
// 我们只需要知道用户输入的n 的前面两项(n-1 n-2)就可以计算出n 对应的序列值
function fb(n) {
  if (n === 1 || n === 2) {
        return 1;
  }
  return fb(n - 1) + fb(n - 2);
}
console.log(fb(3));
```

### 6.4利用递归遍历数据

```js
var data = [{
            id: 1,
            name: '家电',
            goods: [{
                id: 11,
                gname: '冰箱',
                goods: [{
                    id: 111,
                    gname: '海尔'
                }, {
                    id: 112,
                    gname: '美的'
                }, ]
            }, {
                id: 12,
                gname: '洗衣机'
            }]
        }, {
            id: 2,
            name: '服饰'
        }];
// 我们想要做输入id号,就可以返回的数据对象
// 1. 利用 forEach 去遍历里面的每一个对象
function getID(json, id) {
    var o = {};
    json.forEach(function (item) {
        // console.log(item); // 2个数组元素
        if (item.id == id) {
            // console.log(item);
            o = item;
            // return item; 这个return item没有意义，因为在forEach的回调函数中，不会return，所以改这串代码只需要让o去接收下面getID的返回值就可以了
            // 2. 我们想要得里层的数据 11 12 可以利用递归函数
            // 里面应该有goods这个数组并且数组的长度不为 0
        } else if (item.goods && item.goods.length > 0) {
            o = getID(item.goods, id);
        }
    });
    return o;
}
console.log(getID(data, 1));
console.log(getID(data, 2));
console.log(getID(data, 11));
console.log(getID(data, 12));
console.log(getID(data, 111));
```



### 6.5 浅拷贝和深拷贝

1. 浅拷贝**只有第一层会在内存中开辟新的地址存放**，更深层的还是拷贝**原来对象的引用（地址）**
2. 深拷贝拷贝多层，**每一层的数据在内存中开辟新的地址存放**

#### 6.5.1 常见的浅拷贝方法



##### ES6新增浅拷贝方法：`Object.assign(target,...sources)`

~~~js
target
目标对象。
sources
源对象。
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }  说明该函数返回target

~~~



##### 扩展运算符 ...

~~~js
const arr = ['lin', 'is', 'handsome']
const newArr = [...arr]

arr[2] = 'rich' // 改变原来的数组

console.log(newArr) // ['lin', 'is', 'handsome'] // 新数组不变

console.log(arr == newArr) // false 两者指向不同地址
~~~

~~~js
const obj = {
  name: 'lin'
}

const newObj = { ...obj }

obj.name = 'xxx' // 改变原来的对象

console.log(newObj) // { name: 'lin' } // 新对象不变

console.log(obj == newObj) // false 两者指向不同地址
~~~



##### 数组的 .slice(0) 截取

~~~js
const arr = ['lin', 'is', 'handsome']
const newArr = arr.slice(0)

arr[2] = 'rich' // 改变原来的数组

console.log(newArr) // ['lin', 'is', 'handsome']

console.log(arr == newArr) // false 两者指向不同地址
~~~



##### 数组的 [].concat() 拼接

~~~js
const arr = ['lin', 'is', 'handsome']
const newArr = [].concat(arr)

arr[2] = 'rich' // 改变原来的数组

console.log(newArr) // ['lin', 'is', 'handsome'] // 新数组不变

console.log(arr == newArr) // false 两者指向不同地址
~~~



##### 数组静态方法 Array.from() 浅拷贝

~~~js
const arr = ['lin', 'is', 'handsome']
const newArr = Array.from(arr)

arr[2] = 'rich' // 改变原来的数组

console.log(newArr) // ['lin', 'is', 'handsome']

console.log(arr == newArr) // false 两者指向不同地址
~~~





#### 6.5.2 深拷贝

实现深拷贝，就是**利用递归函数，一直给他解析，直到是简单数据类型，然后再赋值的过程**

~~~js
// 深拷贝拷贝多层, 每一级别的数据都会拷贝.
var obj = {
    id: 1,
    name: 'andy',
    msg: {
        age: 18,
    },
    color: ['pink', 'red'],
};
var o = {};

// 封装函数
function deepCopy(newobj, oldobj) {
    for (var k in oldobj) {
        // 判断我们的属性值属于那种数据类型
        // 1. 获取属性值  oldobj[k]
        var item = oldobj[k];
        // 2. 判断这个值是否是数组 (先判断数组再判断对象，因为数组是对象的子集)
        if (item instanceof Array) {
            newobj[k] = [];
            deepCopy(newobj[k], item);
        } else if (item instanceof Object) {
            // 3. 判断这个值是否是对象
            newobj[k] = {};
            deepCopy(newobj[k], item);
        } else {
            // 4. 属于简单数据类型
            newobj[k] = item;
        }
    }
}
deepCopy(o, obj);
console.log(o);

o.msg.age = 20;
console.log(obj);
~~~



## 四、正则表达式

## 1.正则表达式概述

### 1.1什么是正则表达式

正则表达式（ Regular Expression ）是用于匹配字符串中字符组合的模式。在JavaScript中，正则表达式也**是对象**。

正则表通常被用来检索、替换那些符合某个模式（规则）的文本，例如**验证表单**：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配)。此外，正则表达式还常用于过滤掉页面内容中的一些敏感词(**替换**)，或从字符串中获取我们想要的特定部分(**提取**)等 。

其他语言也会使用正则表达式，本阶段我们主要是利用JavaScript 正则表达式完成表单验证。

### 1.2 正则表达式的特点

1. 灵活性、逻辑性和功能性非常的强。
2. 可以迅速地用极简单的方式达到字符串的复杂控制。
3. 对于刚接触的人来说，比较晦涩难懂。比如：^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$
4. 实际开发,一般都是直接复制写好的正则表达式. 但是要求会使用正则表达式并且根据实际情况修改正则表达式.   比如用户名:   /^[a-z0-9_-]{3,16}$/

[正则表达式在线测试网址](https://c.runoob.com/)



## 2.正则表达式在js中的使用

### 2.1正则表达式的创建

在 JavaScript 中，可以通过两种方式创建一个正则表达式。

方式一：通过调用 **RegExp** 对象的构造函数创建 【一定要有正斜杠】

```js
var regexp = new RegExp(/123/);
console.log(regexp);
```

方式二：利用字面量创建 正则表达式【一定要有正斜杠】

```js
 var rg = /123/;
```

### 2.2  .test()判断正则表达式

`.test()` 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 true 或 false，其参数是测试字符串。

```js
var rg = /123/;
console.log(rg.test(123));//匹配字符中是否出现123  出现结果为true
console.log(rg.test('abc'));//匹配字符中是否出现123 未出现结果为false
```

![](images/img4.png)



## 3.正则表达式中的特殊字符

### 3.1正则表达式的组成

一个正则表达式可以由简单的字符构成，比如 /abc/，也可以是简单和特殊字符的组合，比如 /ab*c/ 。其中特殊字符也被称为元字符，在正则表达式中是具有特殊意义的专用符号，如 ^ 、$ 、+ 、\*等。

特殊字符非常多，可以参考： 

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)

jQuery 手册：正则表达式部分

[正则测试工具]( <http://tool.oschina.net/regex)

### 3.2边界符 ^ $

正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符

| 边界符 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| ^      | 表示匹配**行首**的文本                                       |
| $      | 表示匹配**行尾**的文本                                       |
| ^...$  | 必须是...，如果使用了^[xyz]$，那就是x或y或z **(单个字符多种情况)** |

注意，^a 不代表**以a开始**，而是代表**行首必须是a**

其实你**不加 ^ 直接开始写**你想匹配的东西，默认意思就是从整个字符串的**任意位置开始匹配**

```js
var re = /^a/
console.log(re.test('a666')) //true
console.log(re.test('6a66')) //false

var re = /a/
console.log(re.test('a666')) //true
console.log(re.test('6a66')) //true
```





**如果 ^和 $ 在一起，表示必须是完全一致**。

```js
var rg = /abc/; // 正则表达式里面不需要加引号 不管是数字型还是字符串型

/abc/ 只要包含有abc这个字符串返回的都是true:
console.log(rg.test('abc')); // true
console.log(rg.test('abcd')); // true
console.log(rg.test('aabcd')); // true
console.log('---------------------------');
var reg = /^abc/;
console.log(reg.test('abc')); // true
console.log(reg.test('abcd')); // true
console.log(reg.test('aabcd')); // false
console.log('---------------------------');
var reg1 = /^abc$/; // 精确匹配 要求必须是 abc字符串才符合规范
console.log(reg1.test('abc')); // true
console.log(reg1.test('abcd')); // false
console.log(reg1.test('aabcd')); // false
console.log(reg1.test('abcabc')); // false
```

### 3.3字符类

字符类表示有一系列字符可供选择，只要匹配其中一个就可以了。所有可供选择的字符都放在方括号内。

#### 3.3.1 [] 方括号（或）

表示有一系列字符可供选择，只要**匹配其中一个就可以了（或运算）**

- **方括号内部加上 ^** 表示**取反**，表示【不能】包含方括号内的字符。
- `var reg2 = /[a-zA-Z]/` 表示：从 a-z 以及 A-Z（中括号内的**与运算**就是**直接加**）
- `var reg2 = /^[a-zA-Z0-9_-]$/`  因为短斜杠本身有 xx到xx 的意思，所以只要短斜杠前后都有字符，就会当做 xx到xx ；所以【`[b-a] ` 或者 `[a-1]` 都会报错】
- 所以如果**想包含短斜杠，要放中括号的最后**

```js
var rg = /[abc]/; // 只要包含 a或b或c 都返回为true
console.log(rg.test('andy'));//true
console.log(rg.test('baby'));//true
console.log(rg.test('color'));//true
console.log(rg.test('red'));//false
----------------------------------------------------------------------------------
// 只能有一个字母，要么a要么b要么c；才返回 true
// 你可以理解为，逻辑运算符(与或非)优先级靠后，所以才导致这种情况
var rg1 = /^[abc]$/; 
console.log(rg1.test('aa'));//false
console.log(rg1.test('a'));//true
console.log(rg1.test('b'));//true
console.log(rg1.test('c'));//true
console.log(rg1.test('abc'));//false
----------------------------------------------------------------------------------
var reg = /^[a-z]$/ //26个英文字母任何一个字母返回 true  - 表示的是a 到z 的范围  
console.log(reg.test('a'));//true
console.log(reg.test('z'));//true
console.log(reg.test('A'));//false
-----------------------------------------------------------------------------------
//字符组合
var reg1 = /^[a-zA-Z0-9]$/; // 26个英文字母(大写和小写都可以)任何一个字母返回 true  
------------------------------------------------------------------------------------

//【方括号内部加上 ^】表示取反，表示【不能】包含方括号内的字符。
var reg2 = /^[^a-zA-Z0-9]$/;
console.log(reg2.test('a'));//false
console.log(reg2.test('B'));//false
console.log(reg2.test(8));//false
console.log(reg2.test('!'));//true
```

#### 3.3.2 量词符{}

量词符用来设定某个模式出现的次数。

- {n,m} 里面n最小为0

- n不能为空【 { ,m}是不存在的 】
- {n,m}不能有空格【{n, m} 是不行的】

| 量词  | 说明                |
| ----- | ------------------- |
| *     | 重复0次或更多次  ≥0 |
| +     | 重复1次或更多次  ≥1 |
| ?     | 重复0次或1次        |
| {n}   | 重复n次             |
| {n,}  | 重复n次或更多次  ≥n |
| {n,m} | 重复n到m次   m≥x≥n  |

~~~js
// 6. {3, 16}  大于等于3 并且 小于等于16
      var reg = /^a{0,5}$/;
      console.log(reg.test(''));
      console.log(reg.test('a'));
      console.log(reg.test('aa'));
      console.log(reg.test('aaaaaa'));
      console.log(reg.test('aaa'));
      console.log(reg.test('aaaaaaaaaaaaaaaaaaaaa'));
~~~



#### 3.3.3 案例：用户名表单验证

功能需求:

1. 如果用户名输入合法, 则后面提示信息为:  用户名合法,并且颜色为绿色
2. 如果用户名输入不合法, 则后面提示信息为:  用户名不符合规范, 并且颜色为红色

![](images/img2.png)

![](images/img1.png)

分析:

1. 用户名只能为英文字母,数字,下划线或者短横线组成, 并且用户名长度为6~16位.
2. 首先准备好这种正则表达式模式/^[a-zA-Z0-9-_]{6,16}$/
3. 当表单失去焦点就开始验证. 
4. 如果符合正则规范, 则让后面的span标签添加 right类.
5. 如果不符合正则规范, 则让后面的span标签添加 wrong类.

```js
<input type="text" class="uname"> <span>请输入用户名</span>
 <script>
 //  量词是设定某个模式出现的次数
 var reg = /^[a-zA-Z0-9_-]{6,16}$/; // 这个模式用户只能输入英文字母 数字 下划线 中划线
 var uname = document.querySelector('.uname');
 var span = document.querySelector('span');
 uname.onblur = function() {
   if (reg.test(this.value)) {
   console.log('正确的');
   span.className = 'right';
   span.innerHTML = '用户名格式输入正确';
   } else {
   console.log('错误的');
   span.className = 'wrong';
   span.innerHTML = '用户名格式输入不正确';
   }
 }
</script>
```

#### 3.3.4 括号总结

1.大括号{}  量词符  里面表示重复**次数**

2.中括号[]  字符集合  匹配方括号中的**任意字符**

3.小括号()  表示**优先级**

[正则表达式在线测试网址](https://c.runoob.com/)

~~~~js
var reg = /^abc{3}$/; // 它只让c重复三次:abccc
console.log(reg.test('abc'));	//false
console.log(reg.test('abcabcabc'));	//false
console.log(reg.test('abccc'));	//true

// 小括号 表示优先级
var reg = /^(abc){3}$/; // 加上小括号才能让abc重复三次
console.log(reg.test('abc'));	//false
console.log(reg.test('abcabcabc'));	//true
console.log(reg.test('abccc'));	//false
~~~~



### 3.4 预定义类\

预定义类指的是某些常见模式的简写方式

- **这些都是反斜杠 \\**

| 预定义类 | 说明                                                        |
| -------- | ----------------------------------------------------------- |
| .        | （小数点）匹配**除换行符\n之外**的任何单个字符              |
| \d       | 匹配0-9之间的任一数字，相当于[0-9]                          |
| \D       | 匹配所有0-9以外的字符，相当于\[^0-9]                        |
| \w       | 匹配任意的字母、数字和下划线，相当于[A-Za-z0-9_]            |
| \W       | 除所有字母、数字和下划线以外的字符，相当于\[^A-Za-z0-9_]    |
| \s       | 匹配空格（包括换行符、制表符、空格符等）相等于[ \t\r\n\v\f] |
| \S       | 匹配非空格的字符，相当于\[^ \t\r\n\v\f]                     |





#### 3.4.1 **案例:验证座机号码**

```js
// 座机号码验证:  全国座机号码  两种格式:   010-12345678  或者  0530-1234567
// “|”代表“或”的意思
var reg = /^\d{3}-\d{8}|\d{4}-\d{7}$/;

var reg = /^\d{3,4}-\d{7,8}$/; // 这样会出现3-7 和4-8 的情况，不严谨
```

#### 3.4.2 **表单`<input>`验证案例**

##### **手机号验证：**

```js
//手机号验证:/^1[3|4|5|7|8]\d{9}$/;
//验证通过与不通过更换元素的类名与元素中的内容
 if (reg.test(this.value)) {
    // console.log('正确的');
    this.nextElementSibling.className = 'success';
    this.nextElementSibling.innerHTML = '<i class="success_icon"></i> 恭喜您输入正确';
   } else {
       // console.log('不正确');
      this.nextElementSibling.className = 'error';
      this.nextElementSibling.innerHTML = '<i class="error_icon"></i>格式不正确,请从新输入 ';
 }
```

##### **QQ号、昵称验证：**

```js
//QQ号验证: /^[1-9]\d{4,}$/; 
//昵称验证:/^[\u4e00-\u9fa5]{2,8}$/  	\u4e00-\u9fa5表示第一个到最后一个汉字
//验证通过与不通过更换元素的类名与元素中的内容 ,将上一步的匹配代码进行封装,多次调用即可
 function regexp(ele, reg) {
    ele.onblur = function() {
      if (reg.test(this.value)) {
        // console.log('正确的');
        this.nextElementSibling.className = 'success';
        this.nextElementSibling.innerHTML = '<i class="success_icon"></i> 恭喜您输入正确';
   } else {
     // console.log('不正确');
     this.nextElementSibling.className = 'error';
     this.nextElementSibling.innerHTML = '<i class="error_icon"></i> 格式不正确,请从新输入 ';
            }
        }
 };
```

##### **密码验证：**

```js
//密码验证:/^[a-zA-Z0-9_-]{6,16}$/
//再次输入密码只需匹配与上次输入的密码值 是否一致
```



~~~js
window.onload = function() {
    var regtel = /^1[3|4|5|7|8]\d{9}$/; // 手机号码的正则表达式
    var regqq = /^[1-9]\d{4,}$/; // 10000
    var regnc = /^[\u4e00-\u9fa5]{2,8}$/;
    var regmsg = /^\d{6}$/;
    var regpwd = /^[a-zA-Z0-9_-]{6,16}$/;
    var tel = document.querySelector('#tel');
    var qq = document.querySelector('#qq');
    var nc = document.querySelector('#nc');
    var msg = document.querySelector('#msg');
    var pwd = document.querySelector('#pwd');
    var surepwd = document.querySelector('#surepwd');
    regexp(tel, regtel); // 手机号码
    regexp(qq, regqq); // qq号码
    regexp(nc, regnc); // 昵称
    regexp(msg, regmsg); // 短信验证
    regexp(pwd, regpwd); // 密码框
    // 表单验证的函数
    function regexp(ele, reg) {
        ele.onblur = function() {
            if (reg.test(this.value)) {
                // console.log('正确的');
                this.nextElementSibling.className = 'success';
                this.nextElementSibling.innerHTML = '<i class="success_icon"></i> 恭喜您输入正确';
            } else {
                // console.log('不正确');
                this.nextElementSibling.className = 'error';
                this.nextElementSibling.innerHTML = '<i class="error_icon"></i> 格式不正确，请从新输入 ';
            }
        }
    };

    surepwd.onblur = function() {
        if (this.value == pwd.value) {
            this.nextElementSibling.className = 'success';
            this.nextElementSibling.innerHTML = '<i class="success_icon"></i> 恭喜您输入正确';
        } else {
            this.nextElementSibling.className = 'error';
            this.nextElementSibling.innerHTML = '<i class="error_icon"></i> 两次密码输入不一致';

        }
    }

}
~~~



### 3.5 修饰符 g i

`/表达式/[switch]  `

switch(也称为修饰符) 按照什么样的模式来匹配. 有三种值：  

- g： 全局匹配	（**如果正则表达式最后不加g ，则只会替换一次！所以当字符串里有多处需要被替换，记得加g**）
- i： 忽略大小写
- gi： 全局匹配 + 忽略大小写

```js
var str = 'andy和red';
var newStr = str.replace('andy', 'baby');
console.log(newStr)//baby和red
//等同于 此处的andy可以写在正则表达式内
var newStr2 = str.replace(/andy/, 'baby');
console.log(newStr2)//baby和red

//不加g
var str = 'abcabc'
var nStr = str.replace(/a/,'哈哈') // "哈哈bcabc"

//全部替换g
var str = 'abcabc'
var nStr = str.replace(/a/g,'哈哈') // "哈哈bc哈哈bc"

//忽略大小写i
var str = 'aAbcAba';
var newStr = str.replace(/a/gi,'哈哈') // "哈哈哈哈bc哈哈b哈哈"
```





## 4. 正则替换replace

`str.replace(regexp|substr, newSubStr|function)`

- str为被修改的字符串
- 第一个参数为需要修改的部分（可以是一个字符串或是一个正则表达式）
- 第二个参数是替换第一个参数的内容
- 该方法并不改变调用它的字符串本身，而只是返回一个新的替换后的字符串。



### **案例:过滤敏感词汇**

```html
<textarea name="" id="message"></textarea> <button>提交</button>
<div></div>
<script>
    var text = document.querySelector('textarea');
    var btn = document.querySelector('button');
    var div = document.querySelector('div');
    btn.onclick = function() {
    	div.innerHTML = text.value.replace(/激情|gay/g, '**');
    }
</script>
```



## 五、ES6中的新概念：let、const、解构赋值、箭头函数、剩余参数、Array、String、Set



## 1. ES6相关概念

### 1.1 什么是ES6

ES 的全称是 ECMAScript , 它是由 ECMA 国际标准化组织,制定的一项脚本语言的标准化规范。

ES6 实际上是一个泛指，泛指 **ES2015 及后续**的版本。  

![](images/es-version.png)

### 1.2 为什么使用 ES6 ?

每一次标准的诞生都意味着语言的完善，功能的加强。JavaScript语言本身也有一些令人不满意的地方。

- 变量提升特性增加了程序运行时的不可预测性
- 语法过于松散，实现相同的功能，不同的人可能会写出不同的代码



## 2. ES6新增语法

### 2.1 let

ES6之前只有**全局作用域**和**函数作用域**

ES6新增**块级作用域**，**每个{}就是一个块级作用域**

#### 2.1.1 具有块级作用域

let声明的变量**只在所处于的块级作用域内有效**

```javascript
if (true) {
    let b = 20;
    console.log(b);
    if (true) {
        let c = 30;
    }
    console.log(c); // c is not defined
}
console.log(b); // b is not defined
```

**注意：**使用let关键字声明的变量才具有块级作用域，使用var声明的变量不具备块级作用域特性。

~~~js
/* 在一个大括号中 使用let关键字声明的变量才具有块级作用域 var关键字是不具备这个特点的 */
if (true) {
    var abc = 200;
    let num = 100;
}
console.log(abc); // 200
console.log(num); // num is not defined
~~~

~~~js
/* -------防止循环变量变成全局变量--------- */
for (var i = 0; i < 2; i++) {}
console.log(i);	// 2

for (let i = 0; i < 2; i++) {}
console.log(i);	// i is not defined
~~~



#### 2.1.2 不存在变量提升

var 才存在变量提升

~~~js
console.log(b); // undefined
var b = 200;

等价于：

var b; // undefined
console.log(b); // undefined
b = 200;
~~~

```javascript
console.log(a); // a is not defined 
let a = 20;
```



#### 2.1.3 暂时性死区

let 虽然没有变量提升，但是块级作用域里面**只要有 let 声明，该作用域里面用到这个变量时，就会以该作用域里面的为基准**

所以使用 let 声明的变量，要在 let 声明之后。

```javascript
 var tmp = 123;
 if (true) { 
     tmp = 'abc'; // 此时的tmp拿的是全局变量里的tmp，可以成功赋值
     console.log(tmp) // 'abc'
 }  

var tmp = 123;
 if (true) { 
     tmp = 'abc'; //Cannot access 'tmp' before initialization 初始化前无法访问“tmp”
     console.log(tmp); //Cannot access 'tmp' before initialization 初始化前无法访问“tmp”
     let tmp;
 }
```



#### 2.1.4 经典面试题

```javascript
 var arr = [];
 for (var i = 0; i < 2; i++) {
     arr[i] = function () {
         console.log(i); 
     }
 }
 arr[0]();	// 2
 arr[1]();	// 2

```

![](images/let面试题.png)

**经典面试题图解：**此题的关键点在于变量i是全局的，函数执行时输出的都是全局作用域下的i值。

```javascript
 let arr = [];
 for (let i = 0; i < 2; i++) {
     arr[i] = function () {
         console.log(i); 
     }
 }
 arr[0]();	// 0
 arr[1]();	// 1

```

![](images/let面试题2.png)

**经典面试题图解：**此题的关键点在于每次循环都会产生一个块级作用域，每个块级作用域中的变量都是不同的，函数执行时输出的是自己上一级（循环产生的块级作用域）作用域下的i值.

#### 2.1.5 小结

- let关键字就是用来声明变量的
- 使用let关键字声明的变量具有块级作用域
- 在一个大括号中 使用let关键字声明的变量才具有块级作用域 var关键字是不具备这个特点的
- 防止循环变量变成全局变量
- 使用let关键字声明的变量没有变量提升
- 使用let关键字声明的变量具有暂时性死区特性

### 2.2 const

声明常量，常量就是值（内存地址）不能变化的量

#### 2.2.1 具有块级作用域

```javascript
 if (true) { 
     const a = 10;
 }
console.log(a) // a is not defined
```

#### 2.2.2 声明常量时必须赋值

```javascript
const PI; // Missing initializer in const declaration
```

#### 2.2.3 常量赋值后，值不能修改

如果是基本数据类型（原始数据类型），不能更改值（栈）

如果是复杂数据类型（对象数据类型），能更改对象里面的值（堆），不能更改地址值（栈）

```javascript
const PI = 3.14;
PI = 100; // Assignment to constant variable.

const ary = [100, 200];
ary[0] = 'a';
ary[1] = 'b';
console.log(ary); // ['a', 'b']; 
ary = ['a', 'b']; // Assignment to constant variable.
```

#### 2.2.4 小结

- const声明的变量是一个常量
- 既然是常量不能重新进行赋值，如果是基本数据类型，不能更改值；**如果是复杂数据类型，不能更改地址值**
- 声明 const时候必须要给定值

### 2.3 let、const、var 的区别

- 使用 **var** 声明的变量，其作用域为该语句所在的**函数内**，且**存在变量提升**现象
- 使用 **let** 声明的变量，其作用域为该语句所在的**代码块{}内**，**不存在变量提升**
- 使用 **const** 声明的是**常量**，在后面出现的代码中不能再修改该常量的值

|                    | var          | let        | const      |
| ------------------ | ------------ | ---------- | ---------- |
| **作用域**         | 函数级作用域 | 块级作用域 | 块级作用域 |
| **是否变量提升？** | 是           | 否         | 否         |
| **值可改？**       | 值可更改     | 值可更改   | 值不可更改 |

![](images/var&let&const区别.png)



### 2.4 解构赋值

ES6中允许从数组中提取值，按照对应位置，对变量赋值，对象也可以实现解构

#### 2.4.1 数组解构

```javascript
 let [a, b, c, d] = [1, 2, 3];
 console.log(a); //1
 console.log(b); //2
 console.log(c); //3
 console.log(d); //undefined
```

#### 2.4.2 对象解构

```javascript
 let person = { name: 'zhangsan', age: 20 }; 
 let { name, age } = person;
 console.log(name); // 'zhangsan' 
 console.log(age); // 20

 let {name: myName, age: myAge} = person; // myName myAge 属于别名
 console.log(myName); // 'zhangsan' 
 console.log(myAge); // 20
 console.log(age);	// age is not defined
```

#### 2.4.3 小结

- 解构赋值就是把数据结构分解，然后给变量进行赋值
- 如果结构不成功，变量跟数值个数不匹配的时候，变量的值为undefined
- 数组解构用中括号包裹，多个变量用逗号隔开；对象解构用花括号包裹，多个变量用逗号隔开
- 利用解构赋值能够让我们方便的去取对象中的属性跟方法



### 2.5 箭头函数

ES6中新增的定义函数的方式。

```javascript
() => {} //()：代表是函数； =>：必须要的符号，指向哪一个代码块；{}：函数体
const fn = () => {}//代表把一个函数赋值给fn
```

函数体中**只有一句代码**，且代码的**执行结果就是返回值**，可以**省略大括号**

```javascript
 function sum(num1, num2) { 
     return num1 + num2; 
 }
 //es6写法
 const sum = (num1, num2) => num1 + num2; 

```

如果**形参只有一个**，可以**省略小括号**

```javascript
 function fn (v) {
     return v;
 } 
//es6写法
 const fn = v => v;

```



#### 2.5.1 理解箭头函数中的this

1. 箭头函数没有`prototype`(原型)，所以箭头函数本身没有this

2. 箭头函数的this在定义的时候继承自**外层第一个普通函数的this**。

3. 如果箭头函数**外层没有普通函数**，严格模式和非严格模式下它的this都会**指向`window`(全局对象)**

   **注意：对象没有作用域**

```javascript
const obj = { name: '张三'} 

function fn () { 
     console.log(this);
     return () => { 
         console.log(this);//this 指向的是外层的this
     } 
 } 

// 这两个打印出来都是obj
 const resFn = fn.call(obj); // 外层的this改为obj
 resFn(); // 所以箭头函数里面的this也是obj

// 这两个打印出来都是window
let j = fn();
j();

// 立即执行函数2次打印都是window
fn()();
```

2. **不能用call方法修改里面的this**

~~~js
const obj = { name: '张三'} 
 function fn () { 
     console.log(this);
     return () => { 
         console.log(this);
     } 
 } 

const resFn = fn.call(); // window
resFn.call(obj); // window  按.call的语法，明明应该是obj，打印出来却还是window
~~~



#### 2.5.2 面试题

箭头函数this指向的是被声明的作用域里面，而**对象没有作用域**，所以箭头函数虽然在**对象中被定义**，但是this**指向的是全局作用域**

```javascript
var age = 100;

var obj = {
	age: 20,
	say: () => {
		alert(this.age)	// this指向window
	}
}

obj.say();
```

~~~js
const obj = {
    a: function() { console.log(this) },
    b: {
    	c: () => {console.log(this)}
	}
}
obj.a()   // obj对象【当函数作为对象的方法被调用时，this就会指向该对象】
obj.b.c()  // window 
【c方法定义在b对象下，原本应该找b对象的this，但是对象没有作用域，所以往上一直找到obj的this】

~~~



#### 2.5.3 小结

- 箭头函数中不绑定this，箭头函数中的this指向是它所定义的位置，可以简单理解成，定义箭头函数时的作用域的this指向谁，它就指向谁
- 箭头函数的优点在于解决了this执行环境所造成的一些问题。比如：解决了匿名函数this指向的问题（匿名函数的执行环境具有全局性），包括 setTimeout 和 setInterval 中使用 this 所造成的问题



### 2.6 剩余参数...

剩余参数语法允许我们**将多个不定数量的参数表示为一个数组**，不定参数定义方式，这种方式很方便的去声明不知道参数情况下的一个函数

```javascript
function sum (first, ...args) {
     console.log(first); // 10
     console.log(args); // [20, 30] 
 }
 sum(10, 20, 30)

```

#### 2.6.1 剩余参数和解构配合使用

```javascript
let students = ['wangwu', 'zhangsan', 'lisi'];
let [s1, ...s2] = students; 
console.log(s1);  // 'wangwu' 
console.log(s2);  // ['zhangsan', 'lisi']

```



## 3. ES6 的内置对象扩展

### 3.1 Array 的扩展方法

#### 3.1.1 扩展运算符...（展开语法）

扩展运算符可以将数组或者对象转为用逗号分隔的参数序列

```javascript
let ary = ['a', 'b', 'c'];

console.log(...ary);  // a b c
 // 相当于下面的代码
console.log('a', 'b', 'c');  // a b c
```

##### 应用扩展运算符合并数组

```javascript
// 方法一 
 let ary1 = [1, 2, 3];
 let ary2 = [3, 4, 5];
 let ary3 = [...ary1, ...ary2];
 // 方法二 
 ary1.push(...ary2);
```

##### （★）将伪数组或可遍历对象转换为真正的数组

```javascript
let oDivs = document.getElementsByTagName('div'); 
oDivs = [...oDivs];
```



#### 3.1.2 构造函数方法：Array.from()

将伪数组或可遍历对象**转换**为真正的**数组**（和上面的例子一样）

```javascript
//定义一个集合
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
}; 
//转成数组
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

方法还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组

```javascript
 let arrayLike = { 
     "0": 1,
     "1": 2,
     "length": 2
 }
 let newAry = Array.from(arrayLike, item => item *2)//[2,4]
```

注意：如果是对象，那么属性需要写对应的索引



#### 3.1.3 实例方法：find()

用于找出第一个符合条件的**数组成员(下例是一个对象)**，如果没有找到则返回 **undefined**

```javascript
let ary = [{
     id: 1,
     name: '张三'
 }, { 
     id: 2,
     name: '李四'
 }]; 
 let target = ary.find((item) => item.id == 2);
//找数组里面符合条件的值，当数组中元素id等于2的查找出来，注意，只会匹配第一个

```



#### 3.1.4实例方法：findIndex()

用于找出第一个符合条件的数组成员的**索引**，如果没有找到返回 **-1**

```javascript
let ary = [1, 5, 10, 15];
let index = ary.findIndex((value, index) => value > 9); 
console.log(index); // 2
```



#### 3.1.5 实例方法：includes()

判断某个数组**是否包含**给定的值，返回**布尔值**。

```javascript
[1, 2, 3].includes(2) // true 
[1, 2, 3].includes(4) // false
```



### 3.2 String 的扩展方法

#### 3.2.1 模板字符串

1. ES6新增的创建字符串的方式，使用**反引号``**定义【Tab键上面那个键】

2. 在反引号内部可以**使用`${}`来引用变量**，【不用再 引引加加 了】

```javascript
let name = `zhangsan`;	// 这说明用``或者''  都能代表字符串
正确输出：
console.log(name);
console.log(`${name}`);
错误输出：
console.log(${name});
```

```javascript
let name = '张三'; 
let sayHello = `hello,my name is ${name}`; // hello, my name is zhangsan
```

3. 模板字符串中**可以换行**

```javascript
 let result = { 
     name: 'zhangsan', 
     age: 20,
     sex: '男' 
 } 
 let html = ` <div>
     <span>${result.name}</span>
     <span>${result.age}</span>
     <span>${result.sex}</span>
 </div> `;

```

4. 在模板字符串中**可以调用函数**

```javascript
const sayHello = function () { 
    return '哈哈哈哈 追不到我吧 我就是这么强大';
 }; 
 let greet = `${sayHello()} 哈哈哈哈`;
 console.log(greet); // 哈哈哈哈 追不到我吧 我就是这么强大 哈哈哈哈

```



#### 3.2.2 实例方法：.startsWith() 和 .endsWith()

- startsWith()：表示参数字符串是否在原字符串的头部，返回布尔值
- endsWith()：表示参数字符串是否在原字符串的尾部，返回布尔值

```javascript
let str = 'Hello world!';
str.startsWith('Hello') // true 
str.endsWith('!')       // true
```



#### 3.2.3 实例方法：.repeat(n)

repeat方法表示将原字符串**重复n次**，**返回一个新字符串**

```javascript
'x'.repeat(3)      // "xxx" 
'hello'.repeat(2)  // "hellohello"
```



### 3.3 Set 数据结构

ES6 提供了新的数据结构  Set。它**类似于数组**，但是成员的值都是**唯一**的，**没有重复的值**。

Set本身是一个构造函数，用来生成  Set  数据结构

```javascript
const s = new Set();
```

1. Set函数接受一个**数组作为参数**，用来初始化。

如果不用数组，只会接收第一个参数

```javascript
const set = new Set([1, 2, 3, 4, 4]);//{1, 2, 3, 4}
```

![1](images/1.png)

2. 利用Set 实现数组去重

~~~js
const s3 = new Set([1, 2, 3, 4, 4]);
console.log(s3);
const ary = [...s3];
console.log(ary);
~~~



#### 3.3.1 实例方法

- `.add(value)`：添加某个值，**返回 Set 结构本身**
- `.delete(value)`：删除某个值，返回一个**布尔值**，表示**删除是否成功**
- `.has(value)`：返回一个**布尔值**，表示该值**是否为 Set 的成员**
- `.clear()`：**清除所有**成员，**返回 undefined** 值

注意：增加/删除/查找 的是元素的值，不是索引

```javascript
const s4 = new Set();
// 向set结构中添加值 使用add方法
const r1 = s4.add('a').add('b').add('c');
console.log(s4);
console.log(r1);

// 从set结构中删除值 用到的方法是delete
const r2 = s4.delete('c');
console.log(s4);
console.log(r2);

// 判断某一个值是否是set数据结构中的成员 使用has
const r3 = s4.has('a');
console.log(r3);
const r4 = s4.has('d');
console.log(r4);

// 清空set数据结构中的值 使用clear方法
s4.clear();
console.log(s4);
console.log(s4.clear());
```



#### 3.3.2 遍历

Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。

```javascript
const s5 = new Set(['a', 'b', 'c']);
s5.forEach((value) => console.log(value));
```



## 六、ES6模块化

## 1. 使用ES6模块化前置条件

### 1.1 在 .js 文件中使用ES6模块化语法

在\<script>标签里，加上type="module"

~~~html
想在main.js 文件里使用，就在引入main.js 的html文件里，加上type="module"
<script src="js/main.js" type="module"></script>
~~~



### 1.2 在 Node.js 中使用ES6模块化语法

Node.js 中**默认仅支持 CommonJS** 模块化规范，

若想基于 node.js 体验与学习 ES6 的模块化语法，需要按照如下两个步骤进行配置：

1. 确保安装了 **v14.15.1 或更高版本的 node.js**
   win-r  -->  cmd  -->  输入 node -v 查询版本号
2. 在 package.json 的根节点中添加 **"type":"module"** 节点
   - 在当前目录(文件夹)下使用终端，输入 `npm init -y` **快速初始化包管理文件**(`npm init`也可以初始化，-y是默认都选yes)
   - package.json 是默认没有 `"type": "module"`的，我们得在 package.json 中手动添加：
     ![image-20220327161912711](6. ES6模块化.assets/image-20220327161912711.png)



## 2. 默认导出、默认导入(按对象)

### 2.1 默认导出 `export default {}`

1. 每个模块中，只**允许使用唯一的一次**`export default {}`否则会报错！

2. **导出的是一个对象**，你在{ }内部输入的变量、函数，即为导出对象的属性、方法

3. 该方法导出的**对象名由导入的文件决定** （下面的xxx）

   

### 2.2 默认导入 `import xxx from './xxx.js'`

1. 默认导入的 import 后面**不允许添加花括号！**
2. xxx 为导入的对象取名，**可以和导出文件的变量名不同**，但注意**不允许数字开头**
3. 后续要使用的话，就**像个对象一样去使用它**（用 xxx.属性名 或者 xxx.方法）
4. **同级目录下**，在导入文件中，**输入导出文件的文件名再点 Tab 键**，即可**快速导入**（如下，在 demo.js 中输入 add 再点 Tab就会自动生成导入代码）

~~~js
// add.js 导出文件名
let name = times;

function pl(x, y) {
  return x + y;
}

export default {
  name,
  pl,
};

----------------------------------------------------------------
// demo.js 导入文件名
import sb from './add.js';

console.log(sb.name);	// times
console.log(sb.pl(2, 3));	// 5
~~~



## 3. 按需导出、按需导入(按属性/方法)

### 3.1 按需导出 `export let xxx/function xxx`

- **在定义变量/函数时，往前面加 export** 就是按需导出
- 每个模块中可以使用**多次**按需导出



### 3.2 按需导入 `import {xxx} from './xxx.js'`

1. 按需导入的 import 后面**需要添加花括号**，且必须和导出文件的**变量名一致**
2. 如果不想使用原来的变量名，可以**使用 as 关键字进行重命名**





## 4. 同时使用 默认导入 和 按需导入

1. import 后面 **用逗号分隔**默认和按需导入

2. 在大括号**外**的就是**默认**导入（如下面的 sb）

3. 在大括号**内**的就是**按需**导入

~~~js
// add.js 导出文件名
export let name = 'times';

export function pl(x, y) {
  return x + y;
}

export default {
  a: 1,
  b: 2,
};

----------------------------------------------------------------
// demo.js 导入文件名
import sb, { name, pl } from './add.js';

console.log(name);	// times
console.log(pl(2, 3));	// 5
console.log(sb);	// { a: 1, b: 2 }
~~~



## 5. 直接导入并运行

1. **导出模块不需要写 export** ，只需要写执行的代码
2. **导入模块直接写 `import './xxx.js'`**  即可直接导入并运行 xxx.js 文件里面的代码

~~~js
// add.js 导出文件名
console.log(321);

// demo.js 导入文件名
import './add.js';	//321
~~~



## 七、异步：Promise、async和await

## 1. 事件循环 Event Loop

### 1.1 js代码的执行流程

- 事件循环首先处理在**调用堆栈（执行栈）**中的所有代码【先同步任务】

- 等到执行栈为空（同步任务都做完后），**再开始执行任务队列**【后异步任务】

![image-20220414203600885](7. 异步：Promise、async和await .assets/image-20220414203600885.png)



### 1.2 异步任务里的微任务和宏任务

![image-20220327235011514](7. 异步：Promise、async和await .assets/image-20220327235011514.png)

ES6 规范中，microtask 称为 jobs，macrotask 称为 task
**宏任务是由宿主发起**的，而**微任务由JavaScript自身发起**。

> 在ES3以及以前的版本中，JavaScript本身没有发起异步请求的能力，也就没有微任务的存在。在ES5之后，JavaScript引入了Promise，这样，不需要浏览器，JavaScript引擎自身也能够发起异步任务了。

|                          | 微任务（microtask）(jobs)                                    | 宏任务（macrotask）(task)                                    |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 谁发起的                 | JS引擎                                                       | 宿主（Node、浏览器）                                         |
| 具体事件                 | (1) Promise.then【new Promise 里的算同步】  (2) MutaionObserver  (3) Object.observe（已废弃；Proxy 对象替代）  (4) process.nextTick（Node.js） | (1) **绑定事件.addEventListener 、.onclick** 、**window.onload【是宏任务，慢于同步任务；只不过会放到宏任务队列最前面】**(2) **setTimeout、setInterval**  (3) UI rendering/UI事件  (4) postMessage，MessageChannel  (5) setImmediate，I/O（Node.js） |
| 运行顺序                 | 先                                                           | 后                                                           |
| 会触发新一轮Tick(循环)吗 | 不会(按队执行)                                               | 会(按个执行)                                                 |



~~~html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <button id="button">点击</button>

    <script>
      const buttonElement = document.querySelector('#button')
      window.onload = function () {
        console.log('onload')

        buttonElement.onclick = function () {
          queueMicrotask(() => {
            console.log('queueMicrotask onclick')
          })
          console.log(6)
        }
      }

      buttonElement.addEventListener('click', function funcA() {
        queueMicrotask(() => {
          console.log('queueMicrotask 1')
        })
        console.log('1')
      })
      buttonElement.addEventListener('click', function funcB() {
        queueMicrotask(() => {
          console.log('queueMicrotask 2')
        })
        console.log('2')
      })

      console.log(666)
    </script>
  </body>
</html>

输出结果：
页面加载后：
    666
    onload
点击按钮后：
    1
    queueMicrotask 1
    2
    queueMicrotask 2
    6
    queueMicrotask onclick
~~~



### 1.3 任务队列

- 事件循环从微任务开始，**先执行的是微任务！**
- **微任务按队执行，宏任务按个执行**

总结：要执行宏任务的前提是清空了所有的微任务

> ![image-20220328003749368](7. 异步：Promise、async和await .assets/image-20220328003749368.png)

~~~js
console.log('A'); // 同步任务1

new Promise((resolve, reject) => {
  console.log('初始化'); // 同步任务2
  resolve();
}).then(() => { // 放入微任务队列1
  console.log('二次初始化');
});

setTimeout(() => {  // 放入宏任务队列1
  console.log('C');
  queueMicrotask(() => {  // 在原本空的微任务队列里新增任务并跳过去执行
    console.log('CC');
  });
}, 0);

// 在 JavaScript 中通过 queueMicrotask() 使用微任务
queueMicrotask(() => {  // 放入微任务队列2
  console.log('B');
  setTimeout(() => {  // 放入宏任务队列2，此时微任务队列为空
    console.log('BB');
  }, 0);
});

console.log('D'); // 同步任务3

输出结果：
    A
    初始化
    D
    二次初始化
    B
    C
    CC
    BB
~~~

~~~js
const wait = (ms) => new Promise((resolve) => setTimeout(resolve, ms));
wait().then(() => console.log(4)); 
// 先执行wait() 返回了一个Promise（Promise算同步），继续执行Promise，发现有setTimeout ，放入宏任务队列。暂且看下一行代码。【最后】
Promise.resolve() // Promise同步代码，执行了resolve()，代表成功，接着执行，发现then，放入微任务队列。暂且看下一行代码。【回过头来先执行微任务，打印2。又发现then，加入到微任务，但微任务按队执行，所以继续执行，打印3】
    .then(() => console.log(2))
    .then(() => console.log(3));
console.log(1); // 同步代码，打印1

// 1, 2, 3, 4

~~~







## 2. 生成器(Generator)函数*

### 2.1 生成器函数

- 在 function 后面加上 `*` 就是生成器函数
- 生成器函数内可以使用 关键字 `yield`  生成独立的值  
- 生成器函数和普通函数的不同之处：每执行一次next 生成器的执行环境上下文从栈中弹出，但由于 迭代器 保存着对它的引用所以**它的上下文环境不会被销毁**，类似于闭包



### 2.2 迭代器.next()

- `const xxx = 生成器函数(); `该 xxx 即为该生成器的**迭代器，且此时不会执行1次生成器函数**
- `迭代器.next()` 返回一个**对象**，该对象里面含有 `.value` 和 `.done` 两个属性
- `.value` 的属性值为 **yield 右边的值**
- `.done` 的属性值为 **true/false 表示迭代器是否执行完成**
  【注意，下面例子中有2个yield，前2次 next 返回的.done值都是 false ，第3次 next 才会返回true】

~~~js
function* WeaponGenerator() {
    yield 'Katana';
    yield 'Wakizashi';
}

const weaponsIterator = WeaponGenerator(); //迭代器，此时不执行生成器函数

const result1 = weaponsIterator.next(); //从右往左执行生成器函数，直到遇见yield
assert(
    typeof result1 === 'object' &&
    result1.value === 'Katana' &&
    !result1.done,	//false
    'Katana received!'
);

const result2 = weaponsIterator.next();
assert(
    typeof result2 === 'object' &&
    result2.value === 'Wakizashi' &&
    !result2.done,	//false
    'Wakizashi received!'
);

const result3 = weaponsIterator.next();
assert(
    typeof result3 === 'object' &&
    result3.value === undefined &&
    result3.done,	//true
    'There are no more results!'
);
~~~



### 2.3 迭代器函数配合 for...of...

- for...of...循环不会关心迭代器委托到另一个生成器上，它只关心**在 done 状态为 true 之前，一直调用 .next 方法** 
- let 后面的变量（warrior），保存的是 `.value` 的值，而不是对象

~~~js
function* WarriorGenerator() {
    yield 'Sun Tzu';
    yield* NinjaGenerator();
    yield 'Genghis Khan';
}

function* NinjaGenerator() {
    yield 'Hatori';
    yield 'Yoshi';
}

for (let warrior of WarriorGenerator()) {
    assert(warrior !== null, warrior);
}
~~~



### 2.4 递归遍历DOM vs 用生成器遍历DOM树 

递归遍历DOM：

~~~js
function traverseDOM(element, callback) {
    callback(element);
    element = element.firstElementChild;
    while (element) {
        traverseDOM(element, callback);
        element = element.nextElementSibling;
    }
}

const subTree = document.getElementById("subTree");
traverseDOM(subTree, function(element) {
    assert(element !== null, element.nodeName);
});
~~~

用生成器遍历DOM树

~~~js
function* DomTraversal(element){
    yield element;
    element = element.firstElementChild;
    while (element) {
        yield* DomTraversal(element);	//先遍历子节点
        element = element.nextElementSibling;	//再出栈，遍历兄弟节点
    }
}

const subTree = document.getElementById("subTree");
for(let element of DomTraversal(subTree)) {
    assert(element !== null, element.nodeName);
}
~~~



### 2.5 与生成器交互

1. 用 `.next(参数)`
2. 用 `.throw` 也能达到传值效果
   只不过它只能传给 `.catch(e)` 中的e
   传不到 x = yield 的x中

~~~js
function* NinjaGenerator() {
    let x = 1;
    try {
        x = yield 'Hattori';
        console.log('The expected exception didn’t occur'); //③因为抛出异常，所以这句就不执行了
    } catch (e) {
        console.log(x); //④ 1
        console.log(e === 'Catch this!'); //⑤ true
    }
}

const ninjaIterator = NinjaGenerator();
const result1 = ninjaIterator.next();
console.log(result1.value === 'Hattori'); //① true

ninjaIterator.throw('Catch this!'); //② 传给.catch(e)的e，x没接收到
~~~



## 3. Promise 对象

### 3.1 Promise 函数的使用

- 创建一个 promise 需要**传入一个函数** ，这个函数被称为**执行函数** 
- 传入 Promise 构造函数后，**执行函数会立刻调用**  

~~~js
const ninjaPromise = new Promise((resolve, reject) => {
    resolve("Hatori");
    //reject("An error resolving a promise!");
});

~~~

- 代码调用 Promise 对象内置的 `.then` 方法，我们向这个方法中传入了两个回调函数：
  一个**成功回调函数**和一个**失败回调函数**。  

~~~js
ninjaPromise.then(ninja => { //成功回调函数
    assert(ninja === "Hatori", "We were promised Hatori!");
}, err => { //成功回调函数
    fail("There shouldn’t be an error");
});
~~~

- `.catch` 方法同样也可以在promise进入被拒绝状态时，为其提供错误回调函数  

~~~js
const promise = new Promise((resolve, reject) => {
    reject('Explicitly reject a promise!');
});

promise
    .then(() => fail("Happy path, won't be called!"))
    .catch(() => pass('Third promise was also rejected'));
~~~



Promise 只有3种状态：

- 一个 promise 对象从**等待（pending）状态**开始，此时我们对承诺的值一无所知。因此一个等待状态的 promise 对象也称为未实现（ unresolved）的 promise。  

- 在程序执行的过程中，如果 promise 的 **resolve 函数被调用**， promise 就会进入**成功（fulfilled）状态**，在该状态下我们能够成功获取到承诺的值  
- 另一方面，如果 promise 的 **reject 函数被调用**，或者如果一个未处理的异常在 promise 调用的过程中发生了， promise 就会进入到**失败状态**， 尽管在该状态下我们无法获取承诺的值，但我们至少知道了原因。
- 一旦某个 promise **进入到成功或者失败状态，它的状态就不能再切换了**  

![image-20220414215110434](7. 异步：Promise、async和await .assets/image-20220414215110434.png)







### 3.2 Promise 函数的优点

简单回调函数所带来的问题 ：

1. 当长时间异步任务运行完，调用回调函数的代码一般不会和这段异步代码位于事件循环的同一步骤。导致的结果就是，**错误经常会丢失**  
2. 如果要在嵌套的回调函数再插入几步简直是一种痛苦，增加错误处理也会大大**增加代码的复杂度**
3. 执行很多并行任务时会**书写很多重复的**失败回调函数**代码**



### 3.3 Promise 函数的执行顺序(遵循事件循环)

~~~js
report('At code start');

const ninjaDelayedPromise = new Promise((resolve, reject) => {
    report('A');
    setTimeout(() => {
        report('B');
        resolve('Hatori');
    }, 500);
});

assert(ninjaDelayedPromise !== null, 'C');

ninjaDelayedPromise.then((ninja) => {
    assert(ninja === 'Hatori', 'D');
});

const ninjaImmediatePromise = new Promise((resolve, reject) => {
    report('E');
    resolve('Yoshi');
});

ninjaImmediatePromise.then((ninja) => {
    assert(ninja === 'Yoshi', 'F');
});

report('At code end');

输出结果：
At code start
A
C
E
At code end
F
B
D
~~~



### 3.4 使用 Promise.all 等待多个 promise (与)

一旦数组中的 promise 全部被解决，这个返回的 promise 就会被解决。

而一旦其中有一个 promise 失败了，那么整个新 promise 对象也会被拒绝。  

~~~js
Promise.all([getJSON("data/ninjas.json"),
             getJSON("data/mapInfo.json"),
             getJSON("data/plan.json")]).then(results => {
    const ninjas = results[0], mapInfo = results[1], plan = results[2];

    assert(ninjas !== undefined 
           && mapInfo !== undefined 
           && plan !== undefined,
           "The plan is ready to be set in motion!");
}).catch(error => fail("A problem in carrying out our plan!"));
~~~



### 3.5使用 Promise.race 实现 promise 竞赛 （或）

一旦数组中某一个 promise 被处理或被拒绝，这个返回的 promise 就同样会被处理或被拒绝。  

~~~js
Promise.race([getJSON("data/yoshi.json"),
              getJSON("data/hatori.json"),
              getJSON("data/hanzo.json")])
    .then(ninja => {
    assert(ninja !== null, ninja.name + " responded first");
}).catch(error => fail("Failure!"));
~~~



### 3.6 将 Promise 和生成器结合

这个例子有点儿不同，但它结合了我们前面所学到的很多内容。
- 函数是第一类对象——我们向 async 函数传入了一个参数，该参数也是函数。
- 生成器函数——用它的特性来挂起和恢复执行。
- promise——帮我们处理异步代码。
- 回调函数——在 promise 对象上注册成功和失败的回调函数。
- 箭头函数——箭头函数的简洁适合用在回调函数上。  

- 闭包——在我们控制生成器的过程中, 迭代器在 async 函数内被创建，随之我们在 promise 的回调函数内通过闭包来获取该迭代器  

~~~js
'use strict';
async(function* () {
    try {
        const ninjas = yield getJSON('data/ninjas.json');
        const missions = yield getJSON(ninjas[0].missionsUrl);
        const missionDescription = yield getJSON(missions[0].detailsUrl);

        assert(
            ninjas !== null && missions !== null && missionDescription !== null,
            'All ready!'
        );
    } catch (e) {
        fail("We weren't able to get mission details");
    }
});

function async(generator) {
    const iterator = generator();

    function handle(iteratorResult) {
        if (iteratorResult.done) {
            return;
        }

        const iteratorValue = iteratorResult.value;

        if (iteratorValue instanceof Promise) {
            iteratorValue
                .then((res) => handle(iterator.next(res)))
                .catch((err) => iterator.throw(err));
        }
    }

    try {
        handle(iterator.next());
    } catch (e) {
        iterator.throw(e);
    }
}
~~~



**改进案例：**

~~~js
getJSON("data/ninjas.json", (err, ninjas) => {
    if(err) { console.log("Error fetching ninjas", err); return; }
    	getJSON(ninjas[0].missionsUrl, (err, missions) => {
            if(err) { console.log("Error locating ninja missions", err); return; }
            console.log(misssions);
    	})
});
~~~

不同于把错误处理和控制流混合在一起, 我们使用类似以下写法结束了代码的凌乱：  

~~~js
async(function*() {
    try {
        const ninjas = yield getJSON("data/ninjas.json");
        const missions = yield getJSON(ninjas[0].missionsUrl);
        //All information recieved
    }
    catch(e) {
        //An error has occurred
    }
});
~~~

最终结果结合了同步代码和异步代码的优点。有了同步代码，我们能更容易地理解、使用标准控制流以及异常处理机制、 try-catch 语句的能力。而对于异步代码来说，我们有着天生的非阻塞：当等待长时间运行的异步任务时，应用的执行不会被阻塞。  





## 4. async和await

### 4.1 await 的作用：

1. 通过 await 关键字，能够将后面跟的 Pormise 对象中的 **resolve(data) 中的 data 提取出来**，使得我们可以直接**拿到成功的值**来赋值给变量【对象 -> 值】
   - return 的值是promise resolved时候的value
   - .throw 的值是promise rejected时候的reason
2. await 作用之一就是会**等着执行完**之后**再执行下一行**代码

> ![image-20220327223422720](7. 异步：Promise、async和await .assets/image-20220327223422720.png)



### 4.2 注意事项

1. 如果要在function中**使用 await** ,则**function必须被async修饰**
2. 在async方法中，第一个 await **之前的代码会同步执行**，await **之后的代码会异步执行**

> ![image-20220327222910958](7. 异步：Promise、async和await .assets/image-20220327222910958.png)









