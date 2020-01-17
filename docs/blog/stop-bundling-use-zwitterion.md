# Stop bundling - use Zwitterion

1/16/2020

# TLDR

[Zwitterion](https://github.com/lastmjs/zwitterion) is a web dev server that lets you import anything, if by anything you mean: JavaScript ES2015+, TypeScript, JSON, JSX, TSX, AssemblyScript, Rust, C, C++, WebAssembly, and in the future anything that compiles to JavaScript or WebAssembly. Zwitterion is designed to be an instant replacement for your current web development static file server, and is NOT a bundler. It eschews bundling for a simpler experience.

Install and use it like this:

```bash
npm install zwitterion
npx zwitterion
```

It lets you do stuff like this:

```javascript
import { add } from './index.ts';
import asModuleInit from './index.as';
import rustModuleInit from './index.rs';
import cModuleInit from './index.c';
import cppModuleInit from './index.cpp';
import watModuleInit from './index.wat';
import wasmModuleInit from './index.wasm';
import { jsxElement } from './index.jsx';
import { tsxElement } from './index.tsx';
import helloWorld from './index.json';

async function run() {

    const asModule = await asModuleInit();
    const rustModule = await rustModuleInit();
    const cModule = await cModuleInit();
    const cppModule = await cppModuleInit();
    const watModule = await watModuleInit();
    const wasmModule = await wasmModuleInit();

    console.log('TypeScript add', add(0 , 0));
    console.log('AssemblyScript add', asModule.add(0, 1));
    console.log('Rust add', rustModule.add(0, 2));
    console.log('C add', cModule.add(0, 3));
    console.log('CPP add', cppModule.add(0, 4));
    console.log('Wat add', watModule.add(0, 5));
    console.log('Wasm add', wasmModule.add(0, 6));
    console.log(jsxElement);
    console.log(tsxElement);
    console.log(helloWorld);
}

run();
```

That was real code. It runs in browsers, now. See the full example [here](https://github.com/lastmjs/zwitterion/tree/master/examples/basic).

Now for some background.

# The web is beautiful

The web is a beautiful thing. Very beautiful. Billions of people interact with web browsers. There are billions of websites. It's one of the greatest application platforms of all time. But it has some drawbacks, some limitations we might say.

# Limitations of web browsers

Web browsers are not always up-to-date on the latest language standards. They do not support the latest versions of JavaScript. They do not support any version of TypeScript. They don't run Rust, C, C++, AssemblyScript, or many other languages that may be useful on the web.

# Bundlers

To overcome these limitations, the web development community has come up with a few solutions. Most notably, these solutions are known as bundlers. You may have heard of extremely popular bundlers such as [webpack](https://github.com/webpack/webpack), [parcel](https://github.com/parcel-bundler/parcel), and [rollup](https://github.com/rollup/rollup). These tools will take your code, compile/transpile everything down to JavaScript or WebAssembly, potentially do other transformations, and bundle everything into one or a handful of files, suitable for serving up to a client. This works rather well, usually.

## Bundlers are confusing

Sometimes though, bundlers do not work well at all. In my experience, they have been complicated and confusing. Just recently, after years of web development experience, it took me hours to fix a webpack configuration to add TypeScript to a project. Hours! For someone with experience, this is unacceptable. Just imagine the burden on newcomers!

Bundlers come with a few other negative trade-offs. First, they change the way your code runs in the browser from how you've written it. For example, you may think that your code is using the ES modules system, but really this system has been almost entirely removed...you are using a bundler after all. This can lead to subtle differences in behavior that cause problems. It has happened to me.

Second, bundlers sometimes require you to author your source code differently than you would have if you were not using the bundler. In the end, you must get the bundle to the client. The bundle is not something that exists in your source code, and dealing with its existence is sometimes an extra complication (I believe parcel abstracts this away very well, but I don't believe webpack or rollup are good at this).

Third, bundlers can be slow to bundle. A bundler concatenates all of your code into one or a few files. It must do this before you can run your code in the browser. With a small project, you may not notice the bundle time. but as your project grows, this time will inevitably increase.

Fourth, their configurations can be confusing. I don't know why this is, but they just seem to be confusing. Mileage will vary depending on bundler and task to perform, but they've left a bad taste in my mouth.

Because of these problems and potentially more, all in all, it is my opinion that bundlers are unnecessarily complex.

# Not bundlers

I propose a different paradigm to bundling, in fact one that is diametrically opposed to bundling. Don't bundle at all. I present to you [Zwitterion](https://github.com/lastmjs/zwitterion), a web dev server that can import anything, if by anything you mean: JavaScript ES2015+, TypeScript, JSON, JSX, TSX, AssemblyScript, Rust, C, C++, WebAssembly, and in the future anything that compiles to JavaScript or WebAssembly. Zwitterion is designed to be an instant replacement for your current web development static file server, and is NOT a bundler. It eschews bundling for a simpler experience.

Zwitterion relies on the ES modules system alone to share code. It does not try to hide or abstract this away from you. It can also be extended to support any language that can compile to JavaScript or WebAssembly and that has its own file extension. For example, [vue](https://github.com/vuejs/vue) and [svelte](https://github.com/sveltejs/svelte) both have their own file formats for creating components. Extending Zwitterion to support these would be rather straightforward.

Zwitterion achieves its magic by transforming files as they are requested. If you request a TypeScript file, you get back a transpiled JavaScript file. If you request a Rust file, you get back a JavaScript file that exports the exports of the compiled Rust WebAssembly module.

Zwitterion also auto-reloads and caches transformed code. And because it is not bundling code, it is very quick and nimble.

# Example code

Zwitterion allows you to write code like this, hit refresh, and enjoy the dev life:

## TypeScript

`./app.ts`:

```typescript
import { helloWorld } from './hello-world.ts';

console.log(helloWorld());
```

`./hello-world.ts`:

```typescript
export function helloWorld(): string {
  return 'Hello world!';
}
```

## JSX

`./app.js`:

```javascript
import { helloWorldElement } from './hello-world.jsx';

ReactDOM.render(
  helloWorldElement,
  document.getElementById('root')
);
```

`./hello-world.jsx`:

```javascript
export const hellowWorldElement = <h1>Hello, world!</h1>;
```

## TSX

`./app.js`:

```javascript
import { helloWorldElement } from './hello-world.tsx';

ReactDOM.render(
  helloWorldElement,
  document.getElementById('root')
);
```

`./hello-world.tsx`:

```javascript
export const hellowWorldElement: JSX.Element = <h1>Hello, world!</h1>;
```

## AssemblyScript

`./app.js`:

```javascript
import addModuleInit from './add.as';

runAssemblyScript();

async function runAssemblyScript() {
  const adddModule = await addModuleInit();

  console.log(addModule.add(1, 1));
}

```

`./add.as`:

```typescript
export function add(x: i32, y: i32): i32 {
  return x + y;
}
```

## Rust

`./app.js`

```javascript
import addModuleInit from './add.rs';

runRust();

async function runRust() {
  const addModule = await addModuleInit();

  console.log(addModule.add(5, 5));
}
```

`./add.rs`

```rust
#![no_main]

#[no_mangle]
pub fn add(x: i32, y: i32) -> i32 {
  return x + y;
}
```

## C

`./app.js`

```javascript
import addModuleInit from './add.c';

runC();

async function runC() {
  const addModule = await addModuleInit();

  console.log(addModule.add(5, 5));
}
```

`./add.c`

```c
int add(int x, int y) {
  return x + y;
}
```

## C++

`./app.js`

```javascript
import addModuleInit from './add.cpp';

runCPP();

async function runCPP() {
  const addModule = await addModuleInit();

  console.log(addModule.add(5, 5));
}
```

`./add.cpp`

```c++
extern "C" {
  int add(int x, int y) {
    return x + y;
  }
}

```

## WebAssembly Text Format (Wat)

`./app.js`

```javascript
import addModuleInit from './add.wat';

runWat();

async function runWat() {
  const addModule = await addModuleInit();

  console.log(addModule.add(5, 5));
}
```

`./add.wat`

```Lisp
(module
  (func $add (param $x i32) (param $y i32) (result i32)
    (i32.add (get_local $x) (get_local $y))
  )
  (export "add" (func $add))
)
```

## WebAssembly (Wasm)

`./app.js`

```javascript
import addModuleInit from './add.wasm';

runWasm();

async function runWasm() {
  const addModule = await addModuleInit();

  console.log(addModule.add(5, 5));
}
```

`./add.wasm`

```
Imagine this is a compiled Wasm binary file with a function called `add`
```

# Performance

It's important to note that because Zwitterion does not bundle files nor engage in tree shaking (for now), this may impact the performance of your application. HTTP2, HTTP3, ES modules, and other future technological improvments may help with performance, but at this point in time signs tend to point toward worse performance. Zwitterion has plans to improve performance by automatically generating HTTP2 server push information from the static build, and looking into tree shaking, but it is unclear what affect this will have. Stay tuned for more information about performance as Zwitterion matures.

With all of the above being said, the performance implications are unclear. Measure for yourself.

If you're interesetd, you can read the following for more information on the performance implications of bundling versus not bundling with HTTP2:

* https://medium.com/@asyncmax/the-right-way-to-bundle-your-assets-for-faster-sites-over-http-2-437c37efe3ff
* https://stackoverflow.com/questions/30861591/why-bundle-optimizations-are-no-longer-a-concern-in-http-2
* http://engineering.khanacademy.org/posts/js-packaging-http2.htm
* https://blog.newrelic.com/2016/02/09/http2-best-practices-web-performance/
* https://mattwilcox.net/web-development/http2-for-front-end-web-developers
* https://news.ycombinator.com/item?id=9137690
* https://www.sitepoint.com/file-bundling-and-http2/
* https://medium.freecodecamp.org/javascript-modules-part-2-module-bundling-5020383cf306
* https://css-tricks.com/musings-on-http2-and-bundling/

I am pretty confident that any performance limitations can eventually be overcome. I can't wait to get some benchmarks out for you!

# Conclusion

The whole point of Zwitterion is that it strives to offer the simplest development experience possible, if you want to use extra features outside of what web browsers can currently support. It is not a bundler, it is the future. Thanks for reading.