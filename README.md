# jsdoc-import-typedef

This is a fork of [json](https://github.com/jsdoc/jsdoc) to deal with typescript type check import way - https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html#import-types

## Motivation

There are some issues in jsdoc related to this problem and a feature is open here: https://github.com/jsdoc/jsdoc/issues/1645. But the feature will be very complex and maybe can take some time to be done. And I need this fix asap.

## Cause

jsdoc uses [catharsis](https://github.com/hegemonic/catharsis) to parse the expressions and `catharsis.parse` doesn't accept the typescript `import` expression (ex: `@param p { import("./a").Pet }`).

This raises `Invalid type expression` like seem here https://github.com/hegemonic/catharsis/blob/master/bin/parse.js#L48

Instead of patch catharsis, I apply the fix in jsdoc, using a regexp to remove this pattern before the string is parsed by `catharsis.parse`. 

In this case, `@param p { import("./a").Pet }` will be interpreted like `@param p { Pet }` in jsdoc.

Works great if you are using Typescript to type check your jsdoc - (https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html) and is compatible with all jsdoc templates.

## For more information

+ Documentation is available at [jsdoc.app](https://jsdoc.app/).
+ Contribute to the docs at
[jsdoc/jsdoc.github.io](https://github.com/jsdoc/jsdoc.github.io).
+ [Join JSDoc's Slack channel](https://jsdoc-slack.appspot.com/).
+ Ask for help on the
[JSDoc Users mailing list](http://groups.google.com/group/jsdoc-users).
+ Post questions tagged `jsdoc` to
[Stack Overflow](http://stackoverflow.com/questions/tagged/jsdoc).

## License

JSDoc is copyright (c) 2011-present Michael Mathews <micmath@gmail.com> and
the [contributors to JSDoc](https://github.com/jsdoc/jsdoc/graphs/contributors).

JSDoc is free software, licensed under the Apache License, Version 2.0. See the
`LICENSE` file for more details.
