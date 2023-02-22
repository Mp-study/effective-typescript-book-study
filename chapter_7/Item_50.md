# Item 50: Prefer Conditional Types to Overloaded Declarations

## Example

```d
function double(x) {
 return x + x;
}
```

## Bad typing 😟

```d
function double(x: number|string): number|string;
function double(x: any) { return x + x; }

const num = double(12); // string | number
const str = double('x'); // string | number
```

## Better typing 😍

```d
function double<T extends number|string>(x: T): T;
function double(x: any) { return x + x; }

const num = double(12); // Type is 12
const str = double('x'); // Type is "x"
```

## Best typing 😍😍

```d
function double(x: number): number;
function double(x: string): string;
function double(x: any) { return x + x; }

const num = double(12); // Type is number
const str = double('x'); // Type is string
```
