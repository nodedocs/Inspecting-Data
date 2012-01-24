Node provides a utility function, for debugging purposes, that returns a string representation of an object.  `util.inspect()` can be a true lifesaver while working with properties of large, complex objects. 

Let's provide a basic example. `util.inspect()` can be used on any object - a good demonstration will be one of Node's built-in objects.  Try this in the REPL (type `node` at your command line with no arguments):

```js
var util = require('util')
util.inspect(console)
```

The output will be:

```js
'{ log: [Function], info: [Function], warn: [Function], error: [Function], dir: [Function], time: [Function], timeEnd: [Function], trace: [Function], assert: [Function] }'
```

This is a listing of all the enumerable properties of the `console` object.  It is also worth noting that `console.dir` is a wrapper around `util.inspect` that uses its default arguments.

In the REPL, `util.inspect` will immediately return its output - this is not usually the case.  In the context of normal Node.js code in a file, something must be done with the output.  The simplest thing to do:

```js
console.log(util.inspect(myObj));
```

`util.inspect` can also be passed several optional arguments, shown here with their defaults:

```js
util.inspect(object, showHidden=false, depth=2, colorize=true);
```

For example, `util.inspect(myObj, true, 7, true)` would inspect `myObj`, showing all the hidden and non-hidden properties up to a depth of `7` and colorize the output.  Let's go over the arguments individually.

The `depth` argument is the number of levels deep into a nested object to recurse - it defaults to 2.  Setting it to `null` will cause it to recurse 'all the way', showing every level.  Compare the (size of) the outputs of these two `util.inspect` statements in the REPL:

```js
var http = require('http');
util.inspect(http, true, 1);
util.inspect(http, true, 3);
```

The optional argument `showHidden` is a boolean that determines whether or not the 'non-enumerable' properties of an object will be displayed - it defaults to `false`, which tends to result in vastly more readable output.  This isn't something a beginner needs to worry about most of the time, but it's worth demonstrating briefly.  Once more, try the following in the REPL:

```js
var util = require('util');
util.inspect(console, true);
```

Finally, the optional argument `colorize` is a boolean that adds ANSI escape codes to the string output. When logged to a terminal window, it should be pretty printed with colors.

```js
var util = require('util');
console.log(util.inspect({a:1, b:"b"}, false,2,true));
````
