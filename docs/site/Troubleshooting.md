---
lang: en
title: 'Troubleshooting'
keywords: LoopBack 4.0, LoopBack 4, Node.js, TypeScript, Debug
sidebar: lb4_sidebar
permalink: /doc/en/lb4/Troubleshooting.html
---

In general, when you are developing an application, use the `npm` command to run
it. This enables you to see stack traces and console output immediately.

For example:

```
$ cd myapp
$ npm start
```

LoopBack 4 also provides multiple ways to help you verify or diagnose the app.

## Setting Debug Strings

If you get an error but it doesn't provide enough information, you can turn on
debug mode by starting your application using `DEBUG=<DEBUG_STRING> npm start`.
[Setting debug strings](Setting-debug-strings.md) for details.

## Running VS Code Tasks

If you're using Visual Studio Code, refer to
[Debugging with VS Code page](Debugging-with-vscode.md) for debugging tips.

## Running Tests with Mocha

You can debug tests by running mocha commands as documented on page
[Debugging with Mocha tests](Debugging-tests-with-mocha.md).

## Resolving Binding Error

With high extensibility, a LoopBack application usually contains tens of
bindings. A common error caused by missing bindings is "a binding key not
bound", for example:

```
500 Error: The key 'services.hasher' is not bound to any value in context application
```

To fix it, you should set the value for the binding key in the application.

For example, go to your application, typically it is in `src/application.ts`
file:

```ts
import {Hasher} from '/services/hasher';

export class TodoListApplication extends BootMixin(
  ServiceMixin(RepositoryMixin(RestApplication)),
) {
  constructor(options: ApplicationConfig = {}) {
    super(options);
    // Add your binding here
    this.bind(services.hasher).toClass(Hasher);
  }
}
```

See more details in
[Binding documentation page](https://loopback.io/doc/en/lb4/Binding.html).

## Updating Compiled Files

The TypeScript application is compiled to JavaScript files and runs. Forgetting
to rebuild could run into errors. Make sure you rebuild the project before
re-running the application. By default, if you start the application using
`npm start`, it rebuilds the project for you.

In some cases, the compiled JS files might not get updated properly even you
build the project. For example, you deleted a Controller file but still get
errors about the removed Controller during application startup, it implies the
compiled JS files probably didn't get updated.

To fix it, run `npm run clean` to delete all the compiled files. By doing so, it
forces the build to generate the compiled JS files next time when you start the
application using `npm start` or call `npm run build`.

## Submitting Sample Application for Problem Determination

If you couldn't figure out what is going wrong or would like to report an issue,
you can submit a simplified application that contains the problematic code using
the sandbox.

The `/sandbox` directory in the `loopback-next` monorepo can be used to utilize
the latest source code as symbolically-linked dependencies. See its
[README](https://github.com/strongloop/loopback-next/tree/master/sandbox) for
usage instructions.

To submit the sample, you can create a LoopBack application and copy over the
sandbox files, then publish it to the github.
