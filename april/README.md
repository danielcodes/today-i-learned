# April

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

