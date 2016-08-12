
# August

### Week 2

Been brushing up on recursion lately, got these two code samples from Lecture 10 Programming Abstractions (Standford)

```python

# gets all the permutations of a string
def permute(soFar, rest):
	
	if rest == '':
		print soFar
	else:
		for i in range( len(rest) ):
			next = soFar + rest[i]
			remaining = rest[:i] + rest[i+1:]
			permute(next, remaining)


# finds all subsets of a string
def subsets(soFar, rest):
	
	if rest == '':
		print soFar
	else:
		subsets(soFar + rest[0], rest[1:]
		subsets(soFar, rest[1:]

```
