# travis-deploy-once

[![Build Status](https://travis-ci.org/semantic-release/travis-deploy-once.svg?branch=master)](https://travis-ci.org/semantic-release/travis-deploy-once)
[![license](https://img.shields.io/github/license/semantic-release/travis-deploy-once.svg)](https://github.com/semantic-release/travis-deploy-once/blob/master/LICENSE)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![Codecov](https://img.shields.io/codecov/c/github/semantic-release/travis-deploy-once.svg)](https://codecov.io/gh/semantic-release/travis-deploy-once)


You want to test as many node versions as possible and deploy if all of them pass.
This module allows you do just that in a script running in Travis' after_success hook.

Only the job with the highest node version (i.e. the build leader) will run your script.

```bash
npm install --save travis-deploy-once
```

```js
const deployOnce = require('travis-deploy-once')

try {
  // Options can also be set as environment variables with the same name
  var result = await deployOnce({
    // GitHub oAuth token
    GH_TOKEN: 'asd',
    // Want to control which job is the build leader?
    // Set your preferred job id
    BUILD_LEADER_ID: 1  
  })
} catch (err) {
  // something went wrong, and err will tell you what
}

if (result === true) deployMyThing()
if (result === false) console.log('Some job(s) failed')
if (result === null) console.log('Did not run as the build leader')
```
