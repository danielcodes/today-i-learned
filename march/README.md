# March

### Week 3, 03/14/16 

#### Javascript

A little brush up on what `new` does in JS, since I just found out what `prototype` is. When `new` is called with a function 4 things happend:

* new object, object is prototype linked to the functionName.prototype, object is set as `this` for that function call and this new object is returned

```javascript

//type this in your browser console to test things out
//a good ol function
function Foo(){
	console.log("hello from the console");
}

var a = new Foo(); //"hello from the console"

//based on the small definition above, this new object is prototype-linked to Foo.prototype

Foo.prototype //just an object
Foo.prototype.name = "dummy name";

a.name //"dummy name", traversing the prototype chain it finds name on Foo.prototype
a.name = "dan" //created a name property for a itself

Foo.prototype.name //"dummy name"
a.name //"dan"

```

No classes in JS, only linked objects, when a property is not found in `a` it does a lookup on its prototype chain. No hard copying of the objects properties like in languages that have a class design pattern.

#### From solving Free Code Camp algorithms, 03/18/16

Problem was to find the symmetric difference of x amount of sets, my initial solution was super long and I knew there had to a better and shorter way of doing things. The shorter solution using ES6 features is here, https://gist.github.com/danielcodes/3e8c5e25d84cdab99664. Main takeaways were turning the arguments object into an array, a bit of practice with 'fat arrow' notation, using the sets to create containers of unique values and some practice with the spread operator.

```javascript
//a function's passed can be accessed through the arguments object which is array-like
var args = Array.prototype.slice.call(arguments) //or [...arguments]

//the fat arrow replaces the need to use function keyword
//pretty fun to use
var addNumbers = (x, y) => (x + y);

//sets have unique values
var list = [1,1,4,4,5,6];
var blah = new Set(list); //Set {1, 4, 5, 6}

//the spread operator, has Python's **kwargs feel for argument unpacking
var list = [1, 3, 5, 6];
Math.max(...list); //6

```


## References

* https://github.com/getify/You-Dont-Know-JS/blob/master/this%20&%20object%20prototypes/ch5.md
* https://github.com/getify/You-Dont-Know-JS/blob/master/this%20&%20object%20prototypes/ch2.md


### Week 2, 03/07/16

#### Javascript

More from the YDKJS series, more on objects (Chapter 3)

Two ways to declared objects:

```javascript
//literal form
var obj = {
	key: value
	//..
};

//using new
var obj = new Object();
obj.key = value
```

* Not everything is an object, object is one of the six primitive types in JS (string, number, boolean, null, undefined and object).
* Object properties can be configured through property descriptors, **writable, enumerable and configurable**
* Property mutability can be controlled with methods, `preventExtensions(), seal() and freeze()`
* Can iterate over values of data structures with `for..of` syntax

#### Bootstrap

Have been messing a lot with Bootstrap lately to get some robust pages up fast.

Most of the designs have consisted of:

```html
<div class="container">
	<!--some header-->

	<div class="row">
		<div class="col-md-4"></div>
		<div class="col-md-4"></div>
		<div class="col-md-4"></div>
	</div>

	<!--some footer-->
</div>
```

Outer `div` with container class for responsiveness, and most of the content goes in a `div` with row class that subsequently have several other `div` with column classes. Lost in `divs`

### Week 1, 03/01/16

From the You-Don't-Know-JS series, the 4 rules used to find what object **this** is bound to.

```javascript
//4 rules
//default, implicit, explicit and new

var a = "yo, this is global";

function foo(){
	console.log(this.a);
}

//default
foo(); //prints global a

//an obj that has a property reference to foo
var obj = {a: "this belongs to an object", foo: foo};

//implicit
obj.foo(); //prints obj.a

//explicit, using call or apply
foo.call(obj); //tell the func foo to bind this to obj

//using the new operator
//new object is created from a function call, with this bound to that new object

```

## References

* https://github.com/getify/You-Dont-Know-JS/blob/master/this%20%26%20object%20prototypes/ch2.md


