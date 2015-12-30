#### Data provider for testarmada
##### file format 
Provider should only support `.js`. `.js` support is to allow user generate some random data on the fly, like user registration scenario that requires fresh email account every time.

Each `.js` data file should return a json object.
##### supported files
```
   ${ENV}.js          : to define main test data
   ${ENV_INSTANCE}.js : (optional) to define extra data that only applies to certain instance
```
##### default file location
```bash
  ${REPO_ROOT}/config/data
```
##### file loading rules
###### basic
```bash
 # to only load from ${REPO_ROOT}/config/data/local.js
 DC=local ./node_modules/.bin/magellan --test xxxxx ......

 # to only load from ${REPO_ROOT}/config/data/prod-a.js
 DC=prod-a ./node_modules/.bin/magellan --test xxxxx ......
``` 
###### advantage
```bash
 # load both ${REPO_ROOT}/config/data/staging.js and ${REPO_ROOT}/config/data/staging-2.js
 # config in staging-2.js will be used if common config exists.
 DC=staging DC_INS=2 ./node_modules/.bin/magellan --test xxxxx ......
```

##### usage
```javascript
 /** data file
 *{
 * "beijing": {
 *     "name": "Beijing",
 *     "country": "China",
 *     "description": "It is the most populous city in the China"
 *   },
 *   "timestamp": function () {
 *     return new Date().getTime();
 *  }
 *}
 */
 var td = require("dp");

 console.log(td.beijing, td.beijing.description);
 console.log(td.timestamp());
```