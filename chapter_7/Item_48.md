# Item 48: Use TSDoc for API Comments

## JSDoc-style comments

```d
/** Generate a greeting. Result is formatted for display. */
function greetJSDoc(name: string, title: string) {
 return `Hello ${title} ${name}`;
}
```

## TSDoc-style comments

```d
/**
 * Generate a greeting.
 * @param name Name of the person to greet
 * @param salutation The person's title
 * @returns A greeting formatted for human consumption.
 */
function greetFullTSDoc(name: string, title: string) {
 return `Hello ${title} ${name}`;
}
```

This lets editors show the relevant documentation for each parameter
\
as you’re writing out a function call

### You can also use TSDoc with type definitions

```d
/** A measurement performed at a time and place. */
interface Measurement {
 /** Where was the measurement made? */
 position: Vector3D;
 /** When was the measurement made? In seconds since epoch. */
 time: number;
 /** Observed momentum */
 momentum: Vector3D;
}
```

### TSDoc comments are formatted using Markdown, so if you want to use bold, italic, or bulleted lists

```d
/**
 * This _interface_ has **three** properties:
 * 1. x
 * 2. y
 * 3. z
 */
interface Vector3D {
 x: number;
 y: number;
 z: number;
}
```
