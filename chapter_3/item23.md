# Item 23: Create Objects All at Once

## Prefer to build objects all at once rather than piecemeal.
## Use object spread ({...a, ...b}) to add properties in a type-safe way.
## Know how to conditionally add properties to an object.

```js
// simple
const president = {...firstLast, ...(hasMiddle ? {middle: 'S'} : {})};

// multiple
function addOptional<T extends object, U extends object>( a: T, b: U | null): T & Partial<U> {          
    return {...a, ...b};
}

const president = addOptional(firstLast, hasMiddle ? {middle: 'S'} : null);
president.middle // OK, type is string | undefined
```
