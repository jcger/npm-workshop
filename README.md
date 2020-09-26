# npm guide

## Pre-workshop

### Slides

Slides [link](https://docs.google.com/presentation/d/1AhJSteary5P33iyeBB_N0aGgtBPhvH7vPB6emWlkCB8/edit?usp=sharing)

### login

As we are going to publish packages into npm and we don't want to polute our company account, start by logging out:

```sh
npm logout
```

Login back into npm:

```sh
npm login
```

Checkout that you are logged in as `npm-workshop` by executing

```sh
npm whoami
```

## Workshop

### Exercise 1: Create a package.json file

We want to publish our addition module, therefore we need a `package.json` file. Create one.

After it's done, change the `name` property inside the package.json file in order to avoid collitions. For example, use your name initials (Bart Simpson would rename the package as `addition-module-bs`)

### Exercise 2: Install dependencies and run scripts

We want to make sure that our test are working (npm run test fails right now). Install the `jest` dependency, which is our chosen javascript testing framework and edit the test script so it launches `jest`.

> Bonus: run jest without using `npm run`

### Exercise 3: Basic info about installed packages

After installing your fist dependency, the `node_modules` folder and the `package-lock.json` file have been created. Check what `jest` version has been installed without opening the `package.json` file

### Exercise 4: Publish a package

After being able to check that our test works we feel confident enough to publish our first npm module. Checkout the log after running `npm publish`

### Exercise 5: Use published package

Create a new project, execute `npm init -y`, install your recent published package and create a `index.js` file that requires the addition-module and uses it. Run it and checkout that it works

### Exercise 6: Link packages

Add a new call to adds a third param to our exported function. Iterate our addition package so it is able to add 3 arguments. Link the packages so you are able to test it locally

> Bonus: check out what happens if you unlink the `addition-module` and run you code

### Exercise 7: Publish betas

Publish the recent changes to your addition-module as `beta` and install this version in your new module

---

## Solutions

### Exercise 1 solution

```sh
npm init -y
```

Change the name to `addition-module-[your name initials]`

```json
{
  "name": "addition-module-jg",
  "version": "1.0.0",
  "description": "",
  "main": "sum.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git@github.mpi-internal.com:julian-gernun/workshop-npm.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

### Exercise 2 solution

```sh
npm i --save-dev jest
```

Modify the test script inside the package.json file

```json
{
  "name": "addition-module-jg",
  "version": "1.0.0",
  "description": "",
  "main": "sum.js",
  "scripts": {
    "test": "jest"
  },
  "repository": {
    "type": "git",
    "url": "git@github.mpi-internal.com:julian-gernun/workshop-npm.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "jest": "^26.1.0"
  }
}
```

```sh
npm run test

// runs jest test
```

Bonus

```sh
npx jest
```

### Exercise 3 solution

```sh
npm ls jest
```

### Exercise 5 solution

```sh
mkdir new-module
cd new-module
npm init -y
npm install addition-module-jg
```

```javascript
// index.js
const sum = require("addition-module-jg");

console.log(sum(1, 2));
// output: 3
```

```json
// package.json
{
  "name": "use-addition-module",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "addition-module-jg": "^1.0.0"
  }
}
```

### Exercise 6 solution

```javascript
// index.js
const sum = require("addition-module-jg");

console.log(sum(1, 2, 3));
// output: 3
```

```sh
npm link # in the addition-module-jg folder
```

```sh
npm link addition-module-jg # in our new module folder
```

```sh
node index.js
// output: 6
```

Bonus

```sh
npm unlink addition-module-jg
```

Execution breaks as the package has been removed completely

### Exercise 7 solution

```sh
npm version 1.0.0-beta.0 # in the addition-module-jg folder
```

```json
// new module's package.json
{
  ...
  "dependencies": {
    "addition-module-jg": "beta"
  }
}
```

```sh
npm install # in the new module's folder
```
