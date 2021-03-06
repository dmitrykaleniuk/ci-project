# dima-ci
[![Travis][build-badge]][build]
[![Coveralls][coveralls-badge]][coveralls]

[build-badge]: https://img.shields.io/travis/dmitrykaleniuk/ci-project/master.png?style=flat-square
[build]: https://travis-ci.org/dmitrykaleniuk/ci-project

[coveralls-badge]: https://img.shields.io/coveralls/dmitrykaleniuk/ci-project/master.png?style=flat-square
[coveralls]: https://coveralls.io/github/dmitrykaleniuk/ci-project


# CI&CD with TravisCi and Heroku.

This project was created with [Create React App](https://github.com/facebook/create-react-app) for CI testing purposes.


## App information
Connected Travis CI to run tests and if passed -> deploy.

For automated project deployement I used Heroku cloud application platform.

Framework: nodejs


# To setup TravisCi I added .travis.yml file with such config:
<pre>
  sudo: false
  language: node_js
    node_js:
      - 10
  branches:
    only:
      - master
  deploy:
    provider: heroku
    api_key:
      secure: [HERE YOUR API KEY FROM HEROKU ACCOUNT]
    app: [APP NAME]
</pre>

# To create beautiful badges added this code to .travis.yml:
 <pre>
  after_success:
  - cat ./coverage/lcov.info | ./node_modules/codecov.io/bin/codecov.io.js
  - cat ./coverage/lcov.info | ./node_modules/coveralls/bin/coveralls.js
 </pre>
 
 And to display it added in README.md file:
 <pre>
  [![Travis][build-badge]][build]
  [![Coveralls][coveralls-badge]][coveralls]

  [build-badge]: https://img.shields.io/travis/dmitrykaleniuk/ci-project/master.png?style=flat-square
  [build]: https://travis-ci.org/dmitrykaleniuk/ci-project

  [coveralls-badge]: https://img.shields.io/coveralls/dmitrykaleniuk/ci-project/master.png?style=flat-square
  [coveralls]: https://coveralls.io/github/dmitrykaleniuk/ci-project
 </pre>

## API key configuration
API key can be found in HEROKU->AccountSettings->API key
Then this key should be encrypted with travis tool:

<pre>
  travis encrypt pasteAPIKeyHere --add deploy.api_key --org
</pre>


## Available Scripts

In the project directory, you can run:

### `yarn start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `yarn test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.
