# recaptcha-promise

This Node module aims to provide simple, asynchronous, promise-based ReCAPTCHA
response verification.

_This software is in no way affiliated with or endorsed by Google._


## Installation

Add to your project's dependencies:

```sh
npm install recaptcha-promise
```


## Usage

**UPDATE NOTICE**: If you are currently using version 0.x of this package, fear
not! Everything still works the same in this version. Nonetheless, if you do
have the time, consider upgrading to the newer usage patterns.

### Creating an instance

This is the recommended way. First, an instance is created with your secret key.
It can then be used to verify as many challenges as needed.

```js
const recaptcha = require('recaptcha-promise').create({
  secret: 'YOUR_SECRET_KEY'
})

// In an HTTP handler:

// ... with Promises:
recaptcha.verify(userResponse).then(function (success) {
  console.log(success ? 'Response valid' : 'Response invalid')
})

// ... or in an async context:
async function handleRequest (userResponse) {
  const success = await recaptcha.verify(userResponse)
  console.log(success ? 'Response valid' : 'Response invalid')
}
handleRequest(/* ... */)
```

### The global instance

This exists mostly for legacy reasons. If you do not want to dependency-inject
the `RecaptchaVerify` object, you can configure this package with your secret
key globally:

```js
// note the missing .create(...) call
const recaptcha = require('recaptcha-promise')

recaptcha.init({
  secret: 'YOUR_SECRET_KEY'
})
```

You can then use `recaptcha` exactly the same as above. You can also require it
elsewhere and it will still have the secret key ready.

### Passing a remote address

If you have the client's remote address available, you can pass it as a second
parameter to the `verify` function.
