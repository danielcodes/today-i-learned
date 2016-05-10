# May

### Week 2, 05/09/2016

Started Chapter 2, callbacks.

Our brain thinks of events in a linear manner, async code are subactions within these events, they occure after.

The real problem with callbacks is that when using them, third party code might use in an incorrect manner (there is a list of issues). IE. a callback to process payment data can be called multiple times and thus overcharge the customer, etc (other misuses). This leads to a lot of hacky code for error handling.


### Week 1, 05/02/2016

Finally started the Async and performance book fron YDKJS

Learned that callbacks are thrown into an event loop that a queue, this means that there is an order in which things happen. (first in, first out)

Learned that asynchronous means `now and later`, parallel does not mean the same thing as parallel means occurring at the same time

### More from the async chapter 1

How to handle cases where ajax calls will touch on the same data but in a controlled behaviour

* Order of data, check for the source url
* Dependency on a variable, do a check that the variable isn't undefined
* Latch, first one wins, check if the variable is undefined, if so, don't do anything

Breaking up a call for processing data, got lost. I mean, needs review

There is a job queue. Again, clueless.

### C++ GUI set up, again

Man oh man, I thought I was done programming with GUI's in C++. Technically I am, but grading GUI assignments does require me to set up the environment which is the most painful part

Spent the majority of Friday attempting to set up FLTK on Linux without much success, learning a lot of things in the process though

