quickbase
==============

[![npm license](https://img.shields.io/npm/l/quickbase.svg)](https://www.npmjs.com/package/quickbase) [![npm version](https://img.shields.io/npm/v/quickbase.svg)](https://www.npmjs.com/package/quickbase) [![npm downloads](https://img.shields.io/npm/dm/quickbase.svg)](https://www.npmjs.com/package/quickbase)

A lightweight, flexible promise based Quick Base API.

Written in TypeScript, targets Nodejs and the Browser

This library targets the new RESTful JSON-based API, not the old XML-based API. If you want to use the old XML-based API, then please use [v2.x](https://github.com/tflanagan/node-quickbase/tree/v2.x/src) of this library.

```
IE 11 Users, if you are receiving this error:
XMLHttpRequest: Network Error 0x80070005, Access is denied.

In order to use the new RESTful JSON-based API in Internet Explorer, you must change a security setting. This is not a limitation of the library, just how Quick Base's new API works.

Internet Options -> Security -> Custom Level
Scroll down to and find the "Miscellaneous" section
Ensure "Access data sources across domains" is set to "Enable"
Click "OK", "Yes", "OK"
```

Install
-------
```
# Latest Stable Release
$ npm install quickbase

# Latest Commit
$ npm install tflanagan/quickbase

# Also available via Bower
$ bower install quickbase
```

Documentation
-------------

[TypeDoc Documentation](https://tflanagan.github.io/quickbase/)

Server-Side Example
-------------------
```typescript
import { QuickBase } from 'quickbase';

const quickbase = new QuickBase({
    realm: 'www',
    userToken: 'xxxxxx_xxx_xxxxxxxxxxxxxxxxxxxxxxxxxx'
    // Use tempToken if utilizing an authentication token sent
    // up from client-side code. If possible, this is preferred.
    // tempToken: 'xxxxxx_xxx_xxxxxxxxxxxxxxxxxxxxxxxxxx'
});

(async () => {
    try {
        const results = await quickbase.getApp({
            appId: 'xxxxxxxxx'
        });

        console.log(results.name);
    }catch(err){
        console.error(err);
    }
})();
```

Client-Side Example
-------------------
Import `QuickBase` by loading `quickbase.browserify.min.js`

```javascript
var quickbase = new QuickBase({
    realm: 'www'
});

// Using a Temporary Token
quickbase.getTempToken().then(function(results){
    quickbase.setTempToken(results.temporaryAuthorization);

    return quickbase.getApp({
        appId: 'xxxxxxxxx'
    });
}).then(function(results){
    console.log(results.name);
}).catch(function(err){
    console.error(err);
});

// Using a Temporary Table Token
quickbase.getTempTableToken({
    tableId: 'xxxxxxxxx'
}).then(function(results){
    quickbase.setTempToken(results.temporaryAuthorization);

    return quickbase.getTable({
        tableId: 'xxxxxxxxx'
    });
}).then(function(results){
    console.log(results.name);
}).catch(function(err){
    console.error(err);
});
```

License
-------
Copyright 2014 Tristian Flanagan

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
