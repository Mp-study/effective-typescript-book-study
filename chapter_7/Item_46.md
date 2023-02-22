# Item 46: Understand the Three Versions Involved in Type Declarations

- The version of the package
- The version of its type declarations (@types)
- The version of TypeScript

If any of these versions get out of sync with one another, you can run into errors that may not be clearly related to dependency management.

<br/>

<b>Don't worry</b>

```text
You install a package as a direct dependency, and you install its types as a dev dependency
```

Example,

```d
$ npm install react
+ react@16.8.6
$ npm install --save-dev @types/react
+ @types/react@16.8.19
```

<b>This can go wrong in a few ways.</b>

- First, you might update a library but forget to update its type declarations.
- Second, your type declarations might get ahead of your library
- Third, the type declarations might require a newer version of TypeScript than you’re using in your project.

Adjusting versions by npm install `somelib` and `@types/somelib` will resolve the problems. Not a big issue.
