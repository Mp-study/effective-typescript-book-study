# Item 45: Put TypeScript and @types in devDependencies

> <b>dependencies</b>
>
> > These are packages that are required to run your JavaScript. If you import lodash at runtime, then it should go in dependencies.

<br/>

> <b>devDependencies</b>
>
> > These packages are used to develop and test your code but are not required at
> > runtime.

<br/>

> <b>peerDependencies</b>
>
> > These are packages that you require at runtime but don’t want to be responsible
> > for tracking.

<br/>

## Example

```bash
$ npm install react
$ npm install --save-dev @types/react
```

```d
{
    "dependencies": {
        "react": "^16.8.6"
    },
    "devDependencies": {
        "@types/react": "^16.8.19",
        "typescript": "^3.5.3"
    }
}

```
