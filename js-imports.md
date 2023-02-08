---
date: 07-02-2022
title: Modules in JavaScript
tags: ['js', 'es6']
---

I finally understood commonjs/es6 modules. Thankfully, it turns out to be quite simple.

## CommonJS
The CommonJS module system was introduced by Node.js. Modules were imported *at runtime* using the `require` function exposed by node. It was not available in the browser. Exports are defined using the `module.exports` syntax.

## ES6 Modules
Then ES6 came and introduced its own module system. `export default` is used to define a module's default export, while *named exports* are defined using `export const`.

Imports can be static using the `import` directive. The async function `import()` enable importing at runtime, enabling code-splitting, which makes it possible to optimize loading speed, memory usage and bandwidth.

Interesting reference: https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/