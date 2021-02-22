[Top-level README](../README.md)

# About
This module is the Custom Resource manager for Global DynamoDB version 2019 and it is extracted from [this GitHub repository](https://github.com/blmille1/cloudformation-templates/blob/master/multi-region-failover/README.md).

More specifically, [this file](https://github.com/blmille1/cloudformation-templates/blob/master/multi-region-failover/lambdas/cfnGlobalDynamodbManager/global-dynamodb-manager.js) has been extracted from the template repository and made available here as a standalone package.  The reason that the repo isn't using this module is because `sam build` makes it impossible to test NPM modules locally, which means that I'd have to publish every change until I finally get it right.  Therefore, I update this NPM package with the contents of that file when I update it.

# Usage
You may refer to [this app.js file in the templates repo](https://github.com/blmille1/cloudformation-templates/blob/master/multi-region-failover/lambdas/cfnGlobalDynamodbManager/app.js), although you'd need to change out the require to refer to this NPM package.  You'll also want to [check out template.yml](https://github.com/blmille1/cloudformation-templates/blob/master/multi-region-failover/template.yml) to know what parameters need to be passed and also the permissions.

The whole template is quite complicated, so you'll probably want to clone that repository and play around with it a bit.  Please refer to [the README.md file over there](https://github.com/blmille1/cloudformation-templates/blob/master/multi-region-failover/README.md) for more details.

```bash
# Go to the directory of your Custom Resource that will be responding to Global DynamoDB Table requests
npm install cfn-global-dynamodb-custom-resource-manager
```

```js
'use strict';
const GlobalDynamodbManager = require('cfn-global-dynamodb-custom-resource-manager');

exports.handler = async (event, context) => {
    console.log(JSON.stringify(event), JSON.stringify(context));
    let manager = new GlobalDynamodbManager();
    await manager.processEvent(event, context);
};
```