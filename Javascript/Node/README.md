# Node.js

## Debugging

1. Insert necessary `debugger` statements
2. Run `node inspect main.js` 
3. Run `repl` once a breakpoint is hit
4. Run `cont` to continue to other breakpoints

## Arguments

Pass the argument to the start script:

```
npm start -- 10100
```

Read the value:

```js
var args = process.argv.slice(2);

console.log(args[0]);

// Prints "10100"
```

Resources:
* http://www.marcusoft.net/2015/08/npm-scripting-configs-and-arguments.html
* https://nodejs.org/docs/latest/api/process.html#process_process_argv
