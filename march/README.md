# March

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


