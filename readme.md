Third-Party Type Definitions

In general, most packages found on npmjs.com have type definitions that can be installed in addition to the package. Typically searching the name of the package followed by types will locate the type definitions, or you can simply try running npm i --save-dev @types/packageName which will often work.

Type definitions are increasingly created by the creators of the package, but it's also common for them to be created by third parties and maintained by the open source community. So it's possible that type definitions could be outdated, missing specific functions, or were never created in the first place.
Using Types With Third-Party Modules

In the example above, we can see that we are accessing functions available to us from the lodash library. If you're unfamiliar with lodash, it is a library for performing various functions on arrays, numbers, strings, and other data. When using an editor with IntelliSense abilities, we are able to easily see the types used in lodash.

Navigating to the node_modules/@types/lodash folder we can see all of the definitions for the lodash library.

In the following example, we can see that the dropRight function uses a generic to allow for use of an array of any type.

// dropRight in use 
// dropRight takes in an array and then the amount of numbers to drop as arguments
console.log(_.dropRight([1, 2, 3, 4, 5], 2));
console.log(_.dropRight(['cat', 'dog', 'rabbit', 'horse'], 1));

// dropRight type definition
dropRight<T>(array: List<T> | null | undefined, n?: number): T[];

Thinking Like a TypeScript Developer

Visit https://www.npmjs.com/ and locate type definitions for node. Visit the GitHub repository listed and copy in an interface, class, or generic that's being used for any one of Node.js's core modules.
Your reflection
var User = Type.create({
  properties: {
    name: String,
    id: {
      type: Number,
      enumerable: false
    },
    class: {
      type: String,
      value: 'USER',
      readonly: true,
      wrtiable: false,
      enumerable: false
    }
  }
});
Things to think about

Well done. Understanding how Type Definitions work can be very helpful when you don't fully understand how a third-party tool should be used.
Using Third-Party Modules Without Type Definitions

You may run into some situations where there the third-party modules don't have any definitions. TypeScript will still run as expected, you can just expect it to compile with errors. It's best practice to add type definitions, so if you ever run into a situation where the types aren't defined, you can simply create them to reduce errors when compiling.
To Create Type Definitions When One Is Missing:

    Create a types folder in your root directory with a subfolder specifically for 3rdparty types.
    Create a file in your 3rdparty folder called index.d.ts (it could be a more specific name than index).
    Within your definitions file, import the node module with the missing definition.
    Use the declare keyword to declare which module the definition will before followed by curly braces to contain the definition.
    Write the definition which will likely be a class or an interface for a function. It's common to see interfaces for function since the function is actually defined elsewhere.
    Open tsconfig.json and find //"typeRoots": ,. Uncomment the line and update it to include your new types directory. "typeRoots": ["./types"],
    The function should then be useable in your code.

import _ from 'lodash';

declare module 'lodash' {
  interface LoDashStatic {
    multiply(multiplier: number, multiplicand: number): number;
  }
}

New Terms
Term 	Definition
lodash 	A popular library for performing utility functions for things like arrays and numbers
Further Reading

Checkout Definitely Typed, the largest online repository for type definitions for the most popular NPM packages.

Search TypeScript's site for packages with definitions or for packages that have definitions on Definitely Typed.
;
Use strong checks to prevent developer errors

    One way to do this is to use noImplicitAny in tsconfig.json to prevent errors created by Typescript assuming Any type.
    Turn on all strict checking by setting strict to true in your tsconfiig.json settings.

Pay attention to when to use Implicit vs Explicit typing

const

    Typing: Implicit
    Value is immutable so type can't be changed

let

    Typing: Explicit
    Value and type can be changed

Function with controlled inputs

    Typing: Implicit
    Output is controlled and code is simpler

Single-line arrow function

    Typing: Implicit
    Simpler code

Longer function

    Typing: Explicit
    Easier to read

Use the Latest EcmaScript Features

TypeScript is great at staying up to date with what's available in EcmaScript, just make sure to check which version of TypeScript is in use for your project.
Migration Strategies

    Look at the project structure
    Decide whether to migrate all at once or file-by-file.
    Add Typescript to each service if project uses microservice architecture.
    For monolithic architecture, move to a src/dist to keep working files separate from complied Javascript.
        Check if this affects any of the other paths within the project, as they might not be automatically updated (although most IDEs do).
        If it doesn't automatically update, you can use a path module.
    To exclude folders you don't want to be migrated, utilize the configuration file.

Third-party Module Type Definitions

    To find the definitions, search through dependencies and dev-dependencies going through each dependency and adding definitions for each. If a dependency doesn't have definitions, you can create your own.

Typescript Migration Strategies

Typescript Migration Strategies

By setting allowJS to true in the config file, you. can follow the following approaches:

    Work for nested files to main files
        Use file extension to track which files are migrated
        Fewer errors in the console and IDE
    Work from main files to nested:
        Main parts migrated first
        More errors in console and IDE
    Update all files to .ts
        Code will compile, but run with errors.

Which Migration method do you think you would want to use on an already in-production application, and why would you choose that method?
Your reflection
work from nested files to main file
Things to think about

There's no right answer here, just the best for the team and application since TypeScript does us the favor of compiling even when there are errors.
Further Reading

A guide to the migration options for TypeScript from the JavaScript blog 2ality by Dr. Axel Rauschmayer: Strategies for Migrating to TypeScript.
;