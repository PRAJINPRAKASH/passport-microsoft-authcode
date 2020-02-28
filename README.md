# Passport-Microsoft-AuthCode

[Passport](http://passportjs.org/) strategy for authenticating with [Microsoft](http://www.microsoft.com/)
one time authorization code using the OAuth 2.0 API.

This module lets you authenticate using Microsoft in your Node.js applications.
By plugging into Passport, Microsoft authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Installation

    $ npm install passport-microsoft-authcode

## Usage

#### Require Strategy

Require the `passport-microsoft-authcode` Strategy along with `passport`

```js
var passport = require('passport');
var MicrosoftAuthCodeStrategy = require('passport-microsoft-authcode').Strategy;
```

#### Configure Strategy

The Microsoft authentication strategy authenticates users using a Microsoft
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a app ID and app secret.

```js
passport.use(new MicrosoftAuthCodeStrategy({
    clientID: MICROSOFT_CLIENT_ID,
    clientSecret: MICROSOFT_CLIENT_SECRET
  },
  function(accessToken, refreshToken, profile, done) {
    User.findOrCreate({ microsoftId: profile.id }, function (err, user) {
      return done(err, user);
    });
  }
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'microsoft-authcode'` strategy, to authenticate requests.

```js
app.post('/auth/microsoft/authcode',
  passport.authenticate('microsoft-authcode'),
  function (req, res) {
    // do something with req.user
    res.send(req.user? 200 : 401);
  }
);
```

The post request to this route should include a JSON object with the key `code` set to the one time authorization code you receive from microsoft.

## Credits

  - [Shobhit Singhal](https://github.com/shobhitsinghal624)
  - [Jared Hanson](https://github.com/jaredhanson)

## License

(The MIT License)

Copyright (c) 2020 PRAJIN PRAKASH

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

