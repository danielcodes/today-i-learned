# March

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






