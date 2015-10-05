# JavaScript Hoisting Worksheet

## Instructions
1. Review each code snippet below.
2. Fill in what will be output to the console.
3. Run the code to see if you were correct.
4. Describe why the code behaved as it did.
5. Re-write the code snippet to maintain the same output, but to avoid hoisting.

```js
var myvar = 'my value'; 
  
(function() { 
	console.log(myvar);
	var myvar = 'local value'; 
})();
```

> output:
>-
>- undefined
>-
> why?
>-
>-because of hoisting the variable is declared but not defined above the console.log.
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
var myvar = 'my value'; 
  
(function() { 
	var myvar;
	console.log(myvar);
	var myvar = 'local value'; 
})();
>-
>-
>-
>-
>-

```js
var flag = true; 
  
function test() {
	if(flag) {
		var flag = false;
		console.log('Switch flag from true to false');
	}
	else {
		flag = true;
		console.log('Switch flag from false to true');
	}
}
test();
```

> output:
>-
>-1st console log will not fire, 2nd will fire
>-
> why?
>-
>-if(flag) evaluates to falsey since flag is undefined, then the else statement fires providing the 2nd console log
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
>-
>-
>-
var flag = true; 
  
function test() {
	var flag;
	if(flag) {
		var flag = false;
		console.log('Switch flag from true to false');
	}
	else {
		flag = true;
		console.log('Switch flag from false to true');
	}
}
>-
>-
>-
>-
>-
>-
>-


```js
var message = 'Hello world'; 
  
function saySomething() {
	console.log(message);
	var message = 'Foo bar';
}
saySomething();
```

> output:
>-
>-undefined
>-
> why?
>-
>-
>-message is declared but not defined above the console.log
>-
>-
>-
> rewrite without hoisting
>-
>-
>-
>-
>-
var message = 'Hello world'; 
  
function saySomething() {
	var message;
	console.log(message);
	var message = 'Foo bar';
}
saySomething();
>-
>-
>-
>-
>-
>-
>-

```js
var message = 'Hello world'; 
  
function saySomething() {
	console.log(message);
	message = 'Foo bar';
}
saySomething();
```

> output:
>-
>-Hello World!
>-
> why?
>-
>-
>-message is redefined below the console log
>-
>-
>-


```js
function test() {
	console.log(a);
	console.log(foo());

	var a = 1;
	function foo() {
		return 2;
	}
}
 
test();
```

> output:
>-
>- 1st log undefined 2nd 2
>-
> why?
>-
>-
>-a is delcared but undefined before the 1st log, the 2nd is logging a function which returns 2
>-
>-
>-
> rewrite without hoisting
>-
>-
>-
>-
>-function test() {
	var a;
	console.log(a);
	console.log(foo());

	var a = 1;
	function foo() {
		return 2;
	}
}
 
test();
>-
>-
>-
>-
>-
>-
>-

```js
(function() {
	console.log(bar);
	foo();

	function foo() {
		console.log('aloha');
	}

	var bar = 1;
	baz = 2;
})();
```

> output:
>-
>-undefined, aloha
>-
> why?
>-
>-
>-bar is declared but undefined before the log. aloha does not rely on a var
>-
>-
>-
> rewrite without hoisting
>-
>-
>-
>-(function() {
	var bar;
	var baz;
	console.log(bar);
	foo();

	function foo() {
		console.log('aloha');
	}

	var bar = 1;
	baz = 2;
})();
>-
>-
>-
>-
>-
>-
>-
>-

```js
var run = false;

function fancy(arg1, arg2) {
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	function run() {
		console.log('Will I run?');
	}
}
fancy();
```

> output:
>-
>-1st log fires, 2nd log does not 3rd does not
>-
> why?
>-
>-
>-since run is defined withing the function fancy as function run, log of a string, it evaluates to true within the function firing the 1st log but does not fire itself. The 2nd log is ignored since the if statement criteria is met.
>-
>-
>-
> rewrite without hoisting
>-
>-
>-
>-
>-
var run = false;

function fancy(arg1, arg2) {
	function run() {
		console.log('Will I run?');
	}
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	function run() {
		console.log('Will I run?');
	}
}
fancy();
>-
>-
>-
>-
>-
>-
>-

```js
var run = false;

function fancy(arg1, arg2) {
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	var run = function() {
		console.log('Will I run?');
	}
}
fancy();
```

> output:
>-
>-I can't run
>-
> why?
>-
>-run is declared but not defined before the if statement, which then evaluates to false only firing the else log. 
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
>-
>-
>-
>-
var run = false;

function fancy(arg1, arg2) {
	var run;
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	var run = function() {
		console.log('Will I run?');
	}
}
fancy();
>-
>-
>-
>-
>-
>-