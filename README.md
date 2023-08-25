# swc-1.3.79-bug

1. Use @swc/core version 1.3.78, install dependencies, and run `npx swc src/ -d dist-1.3.78`.
2. Modify package.json to use @swc/core version 1.3.79, and run `npx swc src/ -d dist-1.3.79`.
3. Compare dist-1.3.78 and dist-1.3.79. When importing @swc/helpers, version 1.3.79 adds the node_modules path.

## .swcrc
```
{
  "exclude": [
    ".*(spec|test|oly-map).js$"
  ],
  "jsc": {
    "parser": {
      "syntax": "typescript",
      "tsx": true
    },
    "baseUrl": ".",
    "paths": {
      "~/*": [
        "./src/*"
      ]
    },
    "externalHelpers": true
  }
}
```

## dist-1.3.78/index.js
```
import { _ as _class_call_check } from "@swc/helpers/_/_class_call_check";
import test from "./util/test";
var X = function X() {
    "use strict";
    _class_call_check(this, X);
};
console.log(test, X);

```

## dist-1.3.79/index.js
```
import { _ as _class_call_check } from "node_modules/@swc/helpers/esm/_class_call_check";
import test from "./util/test";
var X = function X() {
    "use strict";
    _class_call_check(this, X);
};
console.log(test, X);

```
