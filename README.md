# Project Initialization

## initialization

In the terminal environment, type the following command to initialize the project:

```bash
npm init -y
```

-y shorthand flag: it should take all the defaults

## configuration

### package.json

After initialization, the project folder should contain a file named `package.json`.

```bash
npm config list

npm set init.author.name "<Your Name>"
npm set init.author.email "you@example.com"
npm set init.author.url "example.com"
npm set init.license "MIT"
```

### index.js

In the project's root folder, create a folder name `src`, and then in the `src` folder, create a file named `index.js`.

```javascript
console.log("node.js is running");
```

### nodemon

Nodemon helps with creating an always-running node process. Use the following command to install the package nodemon:

```bash
npm install nodemon --save-dev
```

Now package.json looks like this:

```json5
{
  ...
  "main": "index.js",
  "scripts": {
    "start": "nodemon src/index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  ...
}
```

### Babel

Recent JavaScript language features (ECMAScript) are not included in the recent Node.js versions. Babel helps to transpile the code into Vanilla JavaScript. To install Babel, simply: 

```bash
npm install @babel/core @babel/node --save-dev
```

Next, add the npm start script to `package.json`:

```json5
{
  ...
  "main": "index.js",
  "scripts": {
    "start": "nodemon --exec babel-node src/index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  ...
}
```

After editing the `package.json` file, add the preset to the application configuration.

```bash
npm install @babel/preset-env --save-dev
```

In the project's root directory, create a `.babelrc` file with the configuration:

```json5
{
  "presets": [
    "@babel/preset-env"
  ]
}
```

### dotenv

In the project's root directory, create a `.dotenv` file with any environmental variables:

```bash
MY_SECRET=hereismysecret
```

Then, in the terminal, install dotenv:

```bash
npm install dotenv --save
```

Import dotenv into `src/index.js` to use environment variables:

```javascript
import 'dotenv/config';

console.log('nodemon src/index.js');

console.log(process.env.MY_SECRET);
```

### Mocha and Chai for testing

Mocha will be our test runner which is responsible for encapsulating our tests in test suites (describe-block) and test cases (it-block). Chai will be our assertion library to run equality checks or other test related scenarios.

To install Mocha:

```bash
npm install @babel/register --save-dev
```

```bash
npm install mocha --save-dev
```

Then, in the `package.json` file, include a test script:

```json5
{
  ...
  "main": "index.js",
  "scripts": {
    "start": "nodemon --exec babel-node src/index.js",
    "test": "mocha --require @babel/register 'src/**/**spec.js'"
  },
  "keywords": [],
  ...
}
```

As we use `**` in between, Mocha will run recursively through the src/ folder to find all files in the application.

To install Chai, run:

```bash
npm install chai --save-dev
```

Later, we can specify the first test file `src/spec.js`:

```javascript
import { expect } from 'chai';

describe('true or false', () => {
  it('true is true', () => {
    expect(true).to.eql(true);
  });

  it('false is false', () => {
    expect(false).to.eql(false);
  });
});
```

Note that there are other packages for testing, such as sinon.
