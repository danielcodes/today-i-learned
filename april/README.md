# April

### Week 3, 04/18/2016

#### Javascript

Going through chapter 5 of YDKJS - Types and Grammar, https://github.com/getify/You-Dont-Know-JS/blob/master/types%20%26%20grammar/ch5.md

Learned a bit about operator precedence

```javascript
//&& takes first precedence, || second and ? : third
//ternary operands are grouped from right to left
```

### Week 2, 04/11/2016

#### Flask

Started playing with Flask's file upload, implemented the 'hello world' version provided in the docs http://flask.pocoo.org/docs/0.10/patterns/fileuploads/. I did run into a couple of issues:

```python
# this did not not work for me when I passed '/uploads'
UPLOAD_FOLDER = '/path/to/the/uploads'

#instead I had to use this
UPLOAD_FOLDER = './uploads'

# once the file was uploaded and in the filesystem I needed a way to retrieve it and so I made placed the the upload folder in /static
UPLOAD_FOLDER = './static/uploads/'

# now, the db will save the name and to retrieve is just string concatenation
```

The gist is here, https://gist.github.com/danielcodes/4c3feb1c10d6aed009bdfecdbf268952

#### Javascript

Diving into Chapter 4: Coercion, https://github.com/getify/You-Dont-Know-JS/blob/master/types%20%26%20grammar/ch4.md

Lots of interesting bit between explicit and implicit coercion,

```javascript

//To explicitly convert to any of the primitives, wrap values in their native functions
Number(value), String(value), Boolean(value)

//to boolean, use double !!, one changes to boolean but also flips the truthy/falsy value, need 2 to retain it
a = 4;
!4 // false
!!4 // true

//Implictly
//number to string
a = 45;
b = a + ""; // now a string

//string to number
a = "67"
b = a - 0; // apply the - operator
```

Also found out that `||` and `&&` are a lie, the values these two return are according to a boolean test on the first operand. Based on the result an operand is returned, not necesarily a boolean.

Lastly, learned the truth about `==` vs. `===`, which is comparison with and without coercion. 

```javascript
"42" == true // false

// boolean true is first turned to a number 1, then "42" is turned to 42 and voila 42 == 1 is false
```

The final tally of the crazy stuff that can arise from coersion,

```javascript
//a list of 7, this all returns true

"0" == false
false == 0
false == ""
false == []

"" == 0
"" == []
0 == []
```

* How to avoid getting bitten, do not use loose equals (==) for `false` or `true` (these are coerced to 1 or 0 respectively)
* If using `"", 0 or []` as comparison operands, reconsider loose equals

### Week 1, 04/04/2016

#### Golang

Finally downloaded Go (1.6), and went through this tutorial https://golang.org/doc/code.html to set up my GOPATH and get a feel for project structure.

#### Flask-SQLAlchemy

I had been meaning to finish my little CRUD flask app for a while now, and am always forgetting these procedural steps to create objects.

```python
import db, Kendama

ken = Kendama("Ozora Natural", "Ozora", "First natty kendama", "no link")

#gotta add it to session and commit it
db.session.add(ken)
db.session.commit()

#gotta know how to query too
kens = Kendama.query.all()
```

#### Javascript

Javascript literals are implicitly wrapped in objects a thus methods can be called on these data structures. Read up here, https://github.com/getify/You-Dont-Know-JS/blob/master/types%20%26%20grammar/ch3.md  

Sparse arrays are dangerous to work with, avoid.

Falsy values in javascript, it is easier to check when things are falsy than truthy (longer and possibily infinite list)

```javascript
//there 6 of them
undefined, null, false, 0, NaN and ""
```

Finally decided to take a deeper look into `reduce`, I looked at 2 places, the docs at MDN and a partial lesson on egghead.io

* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce 
* https://egghead.io/series/reduce-data-with-javascript

Cool things I learned:

* if no initial value is provided, the iteration starts from the 2nd element (1 index)
* `map` and `filter` are variations of `reduce`

```javascript
//map and map with reduce
var a = [1, 2, 3, 4];

//map to double values
a.map(function(value){
  return value*2;
});

//initial value is an empty array, aka our accumulator pre iterations
a.reduce(function(accumulator, value){
  //start pushing doubled values into the empty array
  accumulator.push(value * 2);
  return accumulator; 
}, []);


//filter and filter with reduce
//filter evens
a.filter(function(value){
  return value%2 == 0;
});

//again, pass initial value of []
a.reduce(function(accumulator, value){

  //only push into accumulator if even
  if(value%2 == 0){
	accumulator.push(value);
  }

  return accumulator; 
}, []);
```

`reduce` can even help improve performance if there is a `map filter` chain, by limiting the number of operations. Cool :+1:

