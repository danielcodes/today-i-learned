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


