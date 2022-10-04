# Node.js
* runs the V8 JavaScript engine - the core of Google Chrome
* runs in a single process, without creating a new thread for every request
* provides a set of async I/O primitives in its standard library - these prevent blocking
* most libraries written using non-blocking paradigms - non-blocking is the norm
* instead of blocking, it resumes the operations when the response comes back - saving CPU time

## Standard Library
Node.js has a comprehensive standard API:
https://nodejs.org/api/

## Example program
Basic web server sample code (uses `http` standard api):
```
const http = require('http')

const hostname = '127.0.0.1'
const port = process.env.PORT

const server = http.createServer((req, res) => {
  res.statusCode = 200
  res.setHeader('Content-Type', 'text/html')
  res.end('<span style="color: red;">Hello World!</span>\n')
})

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`)
})
```

1. `createServer()` method of http creates a new HTTP server and returns it.
2. [request event is called](#L21) when a new request is received - request (an http.IncomingMessage object) and a response (an http.ServerResponse object).

## Many open source frameworks
https://nodejs.dev/learn#nodejs-frameworks-and-tools

## Installing
Mac OS:
```
brew install node
```
Other package managers for Linux and Windows are listed in:
https://nodejs.org/en/download/package-manager/

`nvm` is a popular way to run Node.js:
1. switch the Node.js version
2. install new versions
3. rollback the version
4. test code with old versions

https://github.com/nvm-sh/nvm

### Using nvm
* Install latest version of node
```
nvm install --lts
```
* Install older version of node
```
nvm install v12.14.1
```

## Reading Environment Variables
The process core module of Node.js provides the env property which hosts all the environment variables that were set at the moment the process was started.
e.g.
```
process.env.NODE_ENV // "development"
```
## REPL - Read Evaluate Print Loop
REPL Console:
```
> console.log('test')
test
undefined
>
```
The first value, test, is the output we told the console to print, then we get undefined which is the return value of running console.log().

Tab autocompletes the properties and methods available.  For example, if you type `process.` or `global.` then hit `[tab]`.

### Dot commands
* `.help`
* `.editor`: editor mode, write multiline JavaScript. `[ctrl]+D` to run the code
* `.break`: Same as pressing `[ctrl]+C`
* `.clear`: resets REPL
* `.load`: loads a JavaScript file (relative to working dir)
* `.save`: saves REPL session to a file (specify the filename)
* `.exit`: exits the repl (same as `[ctrl]+C` two times)

## Exiting
Handling SIGTERM (normal `kill`):
```
const express = require('express')

const app = express()

app.get('/', (req, res) => {
  res.send('Hi!')
})

const server = app.listen(3000, () => console.log('Server ready'))

process.on('SIGTERM', () => {
  server.close(() => {
    console.log('Process terminated')
  })
})
```

You can send signals to other processes or to the process itself using:
`process.kill(process.pid, 'SIGTERM')`

## Command line arguments
Iterate all arguments:
```
process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`)
})
```
Minimalist library:
```
const args = require('minimist')(process.argv.slice(2))
args['name'] //joe
```
With minimalist, use double dashes `--`:
```
node app.js --name=joe
```

## Console logging
```
console.log('My %s has %d years', 'cat', 2)
```
* `%s` format a variable as a string
* `%d` format a variable as a number
* `%i` format a variable as its integer part only
* `%o` format a variable as an object
To clear the console:
`console.clear()`

## Counting Elements
`console.count()`

Example:
```
const oranges = ['orange', 'orange']
const apples = ['just one apple']
oranges.forEach(fruit => {
  console.count(fruit)
})
apples.forEach(fruit => {
  console.count(fruit)
})
```
## Print the stack trace
```
const function2 = () => console.trace()
const function1 = () => function2()
function1()
```
Prints stack:
```
Trace
    at function2 (repl:1:33)
    at function1 (repl:1:25)
    at repl:1:1
    at ContextifyScript.Script.runInThisContext (vm.js:44:33)
    at REPLServer.defaultEval (repl.js:239:29)
    at bound (domain.js:301:14)
    at REPLServer.runBound [as eval] (domain.js:314:12)
    at REPLServer.onLine (repl.js:440:10)
    at emitOne (events.js:120:20)
    at REPLServer.emit (events.js:210:7)
```

## Calculate the time spent
`console.time()` and `console.timeEnd()`

```
const doSomething = () => console.log('test')
const measureDoingSomething = () => {
  console.time('doSomething()')
  //do something, and measure the time it takes
  doSomething()
  console.timeEnd('doSomething()')
}
measureDoingSomething()
```

## Color the output
`console.log('\x1b[33m%s\x1b[0m', 'hi!')`

You install it with `npm install chalk`, then you can use it:
```
const chalk = require('chalk')
console.log(chalk.yellow('hi!'))
```

## Create a progress bar
Progress package for progress bar: `npm install progress`

```
const ProgressBar = require('progress')

const bar = new ProgressBar(':bar', { total: 10 })
const timer = setInterval(() => {
  bar.tick()
  if (bar.complete) {
    clearInterval(timer)
  }
}, 100)
```

## Command line input
`readline` module:
```
const readline = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout
})

readline.question(`What's your name?`, name => {
  console.log(`Hi ${name}!`)
  readline.close()
})
```

`readline-sync` package if you need to show a password as `*`'s.

More complete solution is `inquirer`:
`npm install inquirer` 

Example code:
```
const inquirer = require('inquirer')

var questions = [
  {
    type: 'input',
    name: 'name',
    message: "What's your name?"
  }
]

inquirer.prompt(questions).then(answers => {
  console.log(`Hi ${answers['name']}!`)
})
```


## Module System
Use `require(...)`

Example, importing from library.js:
`const library = require('./library')`

Example of exporting:
```
const car = {
  brand: 'Ford',
  model: 'Fiesta'
}

exports.car = car
```
Importing
```
const car = require('./items').car
```

## NPM
1. *Local Installation* - local packages are installed in the directory where you run `npm install <package-name>`.
  
      e.g. install package to local directory:
      ```
      npm install lodash
      ```
      1. npm adds `lodash` to `node_modules`.
      2. adds the dependency to `package.json`

2. *Global installation* - global packages are all put in a single place in your system (exactly where depends on your setup), regardless of where you run `npm install -g <package-name>`

      e.g install to global location:
      ```
      npm install -g lodash
      ```
      
      Where is the global location?
      * On macOS or Linux - `/usr/local/lib/node_modules`
      * Windows`C:\Users\YOU\AppData\Roaming\npm\node_modules`

      If you have multiple node versions: `/Users/joe/.nvm/versions/node/v8.9.0/lib/node_modules`

3. To uninstall packages, just run with `uninstall` (add `-g` to uninstall globally) instead:
`npm uninstall lodash`


4. *Local or Global?* It is best practice to always install and use local packages whenever possible.  A package should be installed globally when it provides an executable command that you run from the shell (CLI), and it's reused across projects.

      Require can only be used with local packages:
      `require('package-name')`
      
      You can list all globally installed packages using `npm list -g --depth 0`.

## Using imports
`const _ = require('lodash')`

## package.json files
```
{
  "name": "test-project",
  "version": "1.0.0",
  "description": "A Vue.js project",
  "main": "src/main.js",
  "private": true,
  "scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "test": "npm run unit",
    "lint": "eslint --ext .js,.vue src test/unit",
    "build": "node build/build.js"
  },
  "dependencies": {
    "vue": "^2.5.2"
  },
  "devDependencies": {
    "autoprefixer": "^7.1.2",
    "babel-core": "^6.22.1",
    "babel-eslint": "^8.2.1",
    "babel-helper-vue-jsx-merge-props": "^2.0.3",
    "babel-jest": "^21.0.2",
    "babel-loader": "^7.1.1",
    "babel-plugin-dynamic-import-node": "^1.2.0",
    "babel-plugin-syntax-jsx": "^6.18.0",
    "babel-plugin-transform-es2015-modules-commonjs": "^6.26.0",
    "babel-plugin-transform-runtime": "^6.22.0",
    "babel-plugin-transform-vue-jsx": "^3.5.0",
    "babel-preset-env": "^1.3.2",
    "babel-preset-stage-2": "^6.22.0",
    "chalk": "^2.0.1",
    "copy-webpack-plugin": "^4.0.1",
    "css-loader": "^0.28.0",
    "eslint": "^4.15.0",
    "eslint-config-airbnb-base": "^11.3.0",
    "eslint-friendly-formatter": "^3.0.0",
    "eslint-import-resolver-webpack": "^0.8.3",
    "eslint-loader": "^1.7.1",
    "eslint-plugin-import": "^2.7.0",
    "eslint-plugin-vue": "^4.0.0",
    "extract-text-webpack-plugin": "^3.0.0",
    "file-loader": "^1.1.4",
    "friendly-errors-webpack-plugin": "^1.6.1",
    "html-webpack-plugin": "^2.30.1",
    "jest": "^22.0.4",
    "jest-serializer-vue": "^0.3.0",
    "node-notifier": "^5.1.2",
    "optimize-css-assets-webpack-plugin": "^3.2.0",
    "ora": "^1.2.0",
    "portfinder": "^1.0.13",
    "postcss-import": "^11.0.0",
    "postcss-loader": "^2.0.8",
    "postcss-url": "^7.2.1",
    "rimraf": "^2.6.0",
    "semver": "^5.3.0",
    "shelljs": "^0.7.6",
    "uglifyjs-webpack-plugin": "^1.1.1",
    "url-loader": "^0.5.8",
    "vue-jest": "^1.0.2",
    "vue-loader": "^13.3.0",
    "vue-style-loader": "^3.0.1",
    "vue-template-compiler": "^2.5.2",
    "webpack": "^3.6.0",
    "webpack-bundle-analyzer": "^2.9.0",
    "webpack-dev-server": "^2.9.1",
    "webpack-merge": "^4.1.0"
  },
  "engines": {
    "node": ">= 6.0.0",
    "npm": ">= 3.0.0"
  },
  "browserslist": ["> 1%", "last 2 versions", "not ie <= 8"]
}
```
* `version` indicates the current version (`~` before version means leftmost marjor version is fixed but the rest can change, `~` before version means major and middle version are fixed and minor can change).  For more syntax, see [here](https://nodejs.dev/learn/semantic-versioning-using-npm)
* `name` sets the application/package name
* `description` is a brief description of the app/package
* `main` set the entry point for the application
* `private` if set to true prevents the app/package to be accidentally published on npm
* `scripts` defines a set of node scripts you can run
* `dependencies` sets a list of npm packages installed as dependencies
* `devDependencies` sets a list of npm packages installed as development dependencies
* `engines` sets which versions of Node.js this package/app works on
* `browserslist` is used to tell which browsers (and their versions) you want to support


### NPM and package.json
When you install an npm package using `npm install <package-name>`, you are adding it as a dependency under `dependencies`.

* Add `-D` flag, or `--save-dev` to add it to `devDependencies` instead: `npm install -D <package-name>`
* Add `--production` to exclude dev dependencies: `npm install --production <package-name>`

## NPX
`npx` runs code published in the npm registry. - `npx commandname`

# Call Stack
Function calls get added to the call stack (similar to other languages, this is a FIFO queue for code queued to run), setTimeout (and setInterval) get added to the ES [Message Queue](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#queue).  This affects the order that calls are made.

```
const bar = () => console.log('bar')

const baz = () => console.log('baz')

const foo = () => {
  console.log('foo')
  setTimeout(bar, 0)
  baz()
}

foo()
```
Output:
```
foo
baz
bar
```
1. foo() is called.
2. In foo() we call setTimeout(bar) - instruct it to run immediately passing 0 as the timer.
3. Call baz().
4. Finally bar() is called.

### ES6 Job Queue
ES6 added the Job Queue which is used by Promises API.  It manages a queue that is processed separately, after the currently scoped call stack and before the Message Queue. 
```
v
```
### process.nextTick
Run code immediately after the call stack code and job queue (Promises), but before the message queue (setTimeout) / the next event loop iteration.
```
process.nextTick(() => {
  //do something
})
```

# Environments

Node.js assumes it's always running in a development environment. You can signal Node.js that you are running in production by setting the `NODE_ENV=production` environment variable.

See [here for details](https://nodejs.dev/learn/nodejs-the-difference-between-development-and-production).
