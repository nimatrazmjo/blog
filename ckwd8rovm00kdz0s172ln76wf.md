## Javascript:  Best Practices for Functions

In this article, I am going to explain, how to write clean functions in javascript. what tools should you use to help you with following the best practices and consistency.

## What is ESLint

According to Wikipedia

> ESLint is a static code analyses tool for identifying problematic patterns found in Javascript code. Rules in ESLint are configurable, and customized rules can be defined and loaded. ESLint covers both code quality and coding styles issue.
> 

ESLint is a utility that flags deviations from selected best practices, right in your editors as you code. ESLint is widely used by Javascript developer to catch and correct issues before testing and deploying.

to initialize ESLint in your project you will need to run following comment and it will crate `.eslintrc.js` file.

```tsx
cd project-folder && npx eslint --init
```

answer a few question while generating `.eslintrc.js` file. Following content will be generated.

```tsx
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: [
    'airbnb-base',
  ],
  parserOptions: {
    ecmaVersion: 13,
    sourceType: 'module',
  },
  rules: {
  },
};
```

The above code contain `module.exports` and within that, we have a couple  keys. and you will need to add functions roles inside of `rules` object as you follow.

## 1 - use function expression instead of function declaration.

function declaration will get hoisted and it will be created globally, on the other hand, function expression does not create globally, and It will not get hoisted. Function expressions are invoked to avoid polluting the global scope.

So instead of 

```jsx
function print(str) {
	return str;
}

console.log(print('Hello!'));
```

use

```jsx
const print = function (str) {
	return str;
}

console.log(print('Hello!'));
```

In order to use function expression instead of function declaration, you will need to add the following key and value in `rules` object of `.eslintrc.js` file. It will keep you in the right track as you are developing with a function style rule.

```tsx
'func-style':['error', 'expression'],
```

## 2 - Do not use new keyword to construct a function.

There are many reason to do not use new keyword to construct function. The most important reason is that it will create a potential security hole. also it will slightly impact your app's performance.

ESLint supports the no-new-func rule to flag function constructors and you need to add this to `.eslintrc` file.

```tsx
'no-new-func': 'error',
```

## 3 - Leave Parameters value untouched.

Assignment to variables declared as function parameters can be misleading and lead to confusing behavior, as modifying function parameters will also **mutate** the arguments object. Often, assignment to function parameters is unintended and indicative of a mistake or programmer error.

```jsx
'use strict';

const bonusResult = (input) => {
	if (input < 100) {
		input = 100;
  } else if (input > 100 && input < 500) {
		input = input * 1.5;
	} else if (input >= 500) {
		input = input * 2;
  }
	return input;
}

console.log(bonusResult(50));
console.log(bonusResult(150));
console.log(bonusResult(600));
```

Instead

```jsx
'use strict'
const bonusResult = (input) => {
	let result; // create new variable
	if (input < 100) {
		result = 100;
  } else if (input > 100 && input < 500) {
		result = input * 1.5;
	} else if (input >= 500) {
		result = input * 2;
  }
	return result; // return the result
}

console.log(bonusResult(50));
console.log(bonusResult(150));
console.log(bonusResult(600));

```

In order to avoid reassign function parameter, you will need to add the following key and value in `rules` object of `.eslintrc.js` file. It will keep you in the right track as you are developing with a function style rule.

```tsx
'no-param-reassign':'error',
```

## 4 - Use arrow syntax for anonymous functions:

It is preferred to use arrow function in the callback function.  the normal function in callback function is lengthy and makes the code harder to read.  ESLint supports the prefer arrow callback rule, which lets you specify that ESLint should throw an error if your code doesn't use an arrow function for a callback. I'll add this to my eslintrc file. 

To allow ESLint warn you of using arrow function in callback function, you will need to add following key values to `.eslintrc.js` file.

```tsx
'prefer-arrow-callback': 'error'
```

Finally, my `.eslintrc.js` should look like this:

```tsx
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: [
    'airbnb-base',
  ],
  parserOptions: {
    ecmaVersion: 13,
    sourceType: 'module',
  },
  rules: {
    strict: ['error', 'global'], // give warning if strict is not added
    'func-style': ['error', 'expression'], // give warning if function declaration used
    'no-new-func': 'error', // give warning if new keyboard is used to instantiate function
    'no-param-reassign': 'error', // give warning if a function parameter value reassigned
    'prefer-arrow-callback': 'error', // give warning if arrow function has not been used in call back function
  },
};
```

***Let's do, clean, and follow some best practices in real example.***

```tsx
'use strict';

const values = [16,7,55];

function projection(array, result = 0) { //1 use function declaration
  const max = array.reduce(function (a, b) { // 2 didnt used arrow function in callback
    return Math.max(a, b);
  });

  if ( max < 10) {
    result = 'Poor'; //3 reassign the function parameter
  } else if (max < 100) {
    result = 'Fair';
  } else {
    result = 'Good';
  }
  return result;
}

console.log(projection(values));
```

To clean up and follow the best practices of above function:

```tsx
const values = [16, 7, 55];

const projection = (array) => { // you can use arrow function also for better readibility
  
   let status;
  const max = array.reduce((a, b) => Math.max(a, b));

  if (max < 10) {
    status = 'Poor';
  } else if (max < 100) {
    status = 'Fair';
  } else {
    status = 'Good';
  }
  return status;
}

console.log(projection(values));

// I removed, second paramter of the function, because I haven't used it inside of my functions.
```

Thanks for reading! I hope you learn something for it 🙂

Source:   [Linkedin course : Javascript: Best practices for functions and classes. tought by Sasha Vodnik](https://www.linkedin.com/learning/javascript-best-practices-for-functions-and-classes) 