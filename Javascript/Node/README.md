# Node.js

## Debugging

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
