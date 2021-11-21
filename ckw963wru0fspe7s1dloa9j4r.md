## Deno - A modern runtime for Javascript and Typescript

In the article I am going to cover.

- What is Deno?
- What is the benefit of Deno over Node.js?
- Should you use Deno instead of Node.js?

## What is Deno

Deno is a runtime for Javascript and Typescript that is based on v8 javascript engine and the Rust Porgramming lanaguage. It was created by Ryan Dahl, orginial creator of Node.js. It has been released in.

In 2018,  [Ryan Dahl](https://en.wikipedia.org/wiki/Ryan_Dahl)  has announce Deno in his talk  [10 things I Regret About Node.js](https://www.youtube.com/watch?v=M3BM9TB-8yA). 

## What is its benefit of Deno over Node.js?

####  modern Javascript - ES Modules.
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1637485330628/9pDnY8JIZ.png)

#### No package.json and node_modules

In Node.js, package.json is the heard of project, however, in Deno their is no package.json nor node_modules. Deno is no longer dependent on NPM. Every package is loaded in from a URL.

In Node.js, to use a package, you would have to install it first from `NPM`
```
npm install moment
```
then 
```
const moment = require('moment');
```

it will install the package locally inside `node_modules`, and add that package on `package.json` file. However with Deno, the package is imported from a URL. For instance,

```
import { moment } from 'https://deno.land/x/moment/moment.ts';
```

**Note**: in Node.js file extension is no needed while load the package. In Demo file extension is required as you see above.

####  Typescript works out of the box, no configuration needed.
Getting Typescript to work with NodeJS has a multi step to process. You'd have to install typescript, update the package.json, add tsconfig.json, and make sure your modules have @types supported.

In Deno, all you have to do is save your file as .ts instead of .js, and the typscript compiler is already baked right in.

#### Top-Level await: :

 Normally, when using async/await in Node.js, you have to wrap your awaits inside of an asynchronous function, and you have to label it async. Deno makes it possible to use the await function in the global scope without having to wrap it inside an async function, which is a great feature. for example


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1637489833435/uBhOjur_t.png)

#### Built-in testing: 

Deno has a built-in test runner that you can use for testing JavaScript or TypeScript code.

#### A single executable file: 

If you have used Golang, the idea of shipping just a single executable file will be familiar. This is now present in JavaScript with the help of Deno. So say bye to downloading hundreds of files to set up your development environment.

Deno has many other advantages, 

### Should you use Deno instead of Node.js?

Deno’s goal is not to be a Node replacement, but an alternative. I would say that the majority of developers are happy with the way Node.js is evolving and aren’t really looking to switch things up.

Deno’s focus on security and the possibility of bundling the entire codebase into a single file presents a great opportunity for Deno to become the go-to tool for JavaScript developers when it comes to creating utility scripts that may have otherwise been written in languages such as Bash or Python.

If you’re trying to decide which one to choose, I would stick with Node. It is mature and stable, so there won’t be any unexpected behaviors that could negatively impact the development of an application.

As of Deno 1.0.0, the `Deno` namespace APIs are stable. That means we will strive to make code working under 1.0.0 continue to work in future versions.

However, not all of Deno's features are ready for production yet. Features which are not ready, because they are still in draft phase, are locked behind the `--unstable` command line flag.
```
deno run --unstable mod_which_uses_unstable_stuff.ts
```

Passing this flag does a few things:

It enables the use of unstable APIs during runtime.
It adds the `lib.deno.unstable.d.ts` file to the list of TypeScript definitions that are used for type checking. This includes the output of `deno types`.
You should be aware that many unstable APIs have **not undergone a security review**, are likely to have **breaking API changes** in the future, and are **not ready for production**.

Standard modules
Deno's standard modules (https://deno.land/std/) are not yet stable. We currently version the standard modules differently from the CLI to reflect this. Note that unlike the Deno namespace, the use of the standard modules do not require the `--unstable` flag (unless the standard module itself makes use of an unstable Deno feature).