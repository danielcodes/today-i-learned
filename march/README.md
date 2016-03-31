# March

### Week 5, 03/28/16

#### Javascript

Started reading the 4th book from the YDKJS series, [Types & Grammar](https://github.com/getify/You-Dont-Know-JS/tree/master/types%20%26%20grammar)

Some things that stood out,

* undefined vs. undeclared, undefined is a value (in scope), undeclared means the variable has yet to be created (not in scope)

```javascript
//in console
var b;

b // undefined
c // ReferenceError
```

* converting array-like values to actual array

```javascript
//previously had this problem before so it's not that new
//but it's pretty good information

//the arguments object of a function is array-like
//two ways to do it

//use the slice method from Array.prototype
var arr = Array.prototype.slice.call( arguments );

//ES6 solution
var arr = Array.from( arguments );
```

* Special numbers, NaN and -0

```javascript
//NaN is a number computation that went wrong
var a = 3 / "hi"; // NaN

//NaN is not equal to itselt, wut?
a === NaN //false

//to test for NaN, use ES6 feature or polyfill
Number.isNaN( a ); // true


//+0 and -0 are two different values
//not common, but used in applications where the sign indicates something (ie. direction)

var a = 0 / -3; // -0

//to test for it, hard check against 0 and use it in an operation to get -Infinity
a === 0 && 1/a === -Infinity

//ES6 has a utility for these special cases, Object.is()
var a = 3 / "hi"; // NaN
var b = 4 * -0; // -0

Object.is(a, NaN); // true
Object.is(b, -0); // true
```

#### Read the docs

Painfully sifting through the Wikipedia APi for a Free Code Camp project, currently having difficulty finding relevancy to searches.

The basics:

* Hit this endpoint, `https://en.wikipedia.org/w/api.php`
* parameters that I've used so far are `action=query, titles=pages-to-search, format=json'`, this returns an object which has a pageid
* To get to that wikipedia page, `https://en.wikipedia.org/?curid=ID-FROM-QUERY`

From here it's easy to look for a page and based on the found ID, return the wiki page on that topic.

Things get hairier when trying to find relevant links based on that query, passing `prop=links` returns a set of internal links residing in the page but no ID, to get those add `generator=links`. Found this here, http://stackoverflow.com/questions/18432650/how-to-get-all-linksid-of-specific-page-in-wikipedia-by-pageid

Sometimes links in a page arent't good enough and can contain unimportant references to page, try getting the pages that contain the query title, use `list=backlinks` which will require to provide a `btitle`

The results are not quite as relevant as I want them to be, so will keep working on this.


#### You done goofed up

* While playing with Postman, I couldn't seem pass parameters to my API call. What confused me was that the header tab also has the same key-value pair interface as the parameters. Gah, wasted so much time.

![Postman parameters](/img/postman_params.png)


### Week 4, 03/21/16

#### Javascript

The built-in `Array.prototype.sort()`, I use it from time to time and everytime I have to look up the documentation because I can never remember what it does. The function takes one argument, a compares function, if nothing is passed it turns the elemnts into strings and compares their unicode values. If a compare function is passed, it evaluates in the following manner:

Say, `Compare(a, b)`:
* negative, places `a` before `b`
* zero, leave unchanged
* positive, `b` is placed before `a`

```javascript

//a typical use case, sort in ascending order
[4, 3, 2, 1].sort(function(a, b){
  console.log("comparing a ", a, " with b ", b);
  return a-b;
})

/*
comparing a  4  with  3
comparing a  4  with  2
comparing a  3  with  2
comparing a  4  with  1
comparing a  3  with  1
comparing a  2  with  1
[1, 2, 3, 4]
*/

```

This takes a little time to sink in, because you have to think in terms of the return value (-, 0, +). 
ie. 4 - 3 gives 1 and so a positive value means b is placed before a, so it sorts `3, 4`

#### Finding location through the browser

Read up on the `geolocation` object, https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/Using_geolocation 

The example is pretty clear:

```javascript
//if geolocation object is not present, exit early
if (!navigator.geolocation){
  //write some message
  return;
}

function success(position) {
  var latitude  = position.coords.latitude;
  var longitude = position.coords.longitude;

  //do something, my usage is going to be for an API call
};

function error() {
  //error handling
};

//make the function call
navigator.geolocation.getCurrentPosition(success, error);
```

#### You done goofed up

* Always use `target="_blank"` when creating links on codepens, painfully found out about this when the twitter button that I needed to create was giving me some weird frame bug
* Don't forget to add the `http://` when testing API's on hurl.it


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

#### Git

While pushing the bit I learned on Js `new` and `prototype`, the commit pushed had a typo. From here, I could have pushed another commit up to fix the typo but I opted to `squash` this commit into one.

I first needed a way to remove the latest pushed commit, this was done with:

`git push -f origin HEAD^:master`

I then followed the tutorial referenced below, and managed to squash the commit in 2 simple steps:

```sh
# since I wanted to modify the last 2 commits
git rebase -i HEAD~2

# another screen pops up
pick 01d1124 "some commit msg"
pick 6340aaa "some commit msg"

# change 'pick' to squash to meld to commit into one
pick 01d1124 "some commit msg"
squash 6340aaa "some commit msg"

# save and exit, done.
```

Funny enough, I couldn't completely get rid of the commit, as once it was pushed up to GitHub, it saved it's hash reference. So, even though, I rewritten Git history, the commits are stll visible.


#### Functional Programming for JS

I have been intrigued by functional programming as of lately and been putting off reading thim Medium piece on it (referenced below). 

Some takeaways:

* _Pure functions_, this function is solely dependent on input
* _Function composition_, define a compose function that takes two functions and combine them together (process from rightmost function first). Alternatively, a pipe utility can be defined, to process things from left -> right.
* _Function currying_, creates a function that has partial arguments. ie. an add function that takes two arguments, currying can create an add function with a locked-in argument, `add5(a)` which takes the remaining argument
* _Monads, functors and fancy words_, monads are containers for values, transform them with `map`
* _Referential transparency and immutability_, two things that are the same but aren't equal (wut?)
* _Lazy evaluation_, thunks and generators, as the name says, do not perform an action unless told to. Outtermost reduction with reference sharing, whatever that means
* Clojure patterns and features, data focused, lisp? lost.

Conclusion, explore Lodash

## References

#### JS stuff
* https://github.com/getify/You-Dont-Know-JS/blob/master/this%20&%20object%20prototypes/ch5.md
* https://github.com/getify/You-Dont-Know-JS/blob/master/this%20&%20object%20prototypes/ch2.md

#### Git stuff
* http://stackoverflow.com/questions/448919/how-can-i-remove-a-commit-on-github
* http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html

#### Functional Programming for JS
* https://medium.com/@chetcorcos/functional-programming-for-javascript-people-1915d8775504#.v8v5c3q0f


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


