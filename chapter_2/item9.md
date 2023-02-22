Item 9: Prefer Type Declarations to Type Assertions

## Prefer type declarations (: Type) to type assertions (as Type).
The symbols after a type declaration (:) or an assertion (as) are in type space while everything after an = is in value space

## Know how to annotate the return type of an arrow function.
```js
const elNull = document.getElementById('foo'); // Type is HTMLElement | null

const el = document.getElementById('foo')!; // Type is HTMLElement
```
## Use type assertions and non-null assertions when you know something about types that TypeScript does not.
```js
const button = e.currentTarget as HTMLButtonElement;
```
