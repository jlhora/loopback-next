---
lang: en
title: 'Debugging with VS Code'
keywords: LoopBack 4.0, LoopBack 4, Node.js, TypeScript, Debug
sidebar: lb4_sidebar
permalink: /doc/en/lb4/Debugging-with-vscode.html
---

If you are using Visual Studio Code, below are some tips to help you debug your
LoopBack applications.

The monorepo `loopback-next` contains a folder `.vscode` at root level for
debugging the test files. When start debugging, it will stop at any breakpoint
triggered by the tests. There are two predefined configurations defined in file
`.vscode/launch.json`:

- Run Mocha tests: Debug all tests inside the `/packages` folder.
- Debug Current Test File: Only debug the tests inside the current open file.
