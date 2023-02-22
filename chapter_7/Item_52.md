# Item 52: Be Aware of the Pitfalls of Testing Types

### Suppose you’ve written a type declaration for a map function provided by a utility library

```d
declare function map<U, V>(array: U[], fn: (u: U) => V): V[];
```

### How can you check that this type declaration results in the expected types?

```d
map(['2017', '2018', '2019'], v => Number(v));
```

### One way is to assign the result to a variable with a specific type:

```d
const lengths: number[] = map(['john', 'paul'], name => name.length);
```

### Defining helper

```d
function assertType<T>(x: T) {}
assertType<number[]>(map(['john', 'paul'], name => name.length));
```

```d
const n = 12;
assertType<number>(n); // OK
```

```d
const beatles = ['john', 'paul', 'george', 'ringo'];

assertType<{name: string}[]>(
 map(beatles, name => ({
    name,
    inYellowSubmarine: name === 'ringo'
 }))
);
```

### function returns another funtion

```d
const add = (a: number, b: number) => a + b;
assertType<(a: number, b: number) => number>(add); // OK

const double = (x: number) => 2 * x;
assertType<(a: number, b: number) => number>(double); // OK
```

### Break apart the function and test its pieces using the generic parameters and Return Type types

```d
const double = (x: number) => 2 * x;
let p: Parameters<typeof double> = null!;
assertType<[number, number]>(p);
// ~ Argument of type '[number]' is not
// assignable to parameter of type [number, number]
let r: ReturnType<typeof double> = null!;
assertType<number>(r); // OK
```

### the use of a non-arrow function so that we could test the type of this

```d
const beatles = ['john', 'paul', 'george', 'ringo'];

assertType<number[]>(map(
 beatles,
 function(name, i, array) {
// ~~~~~~~ Argument of type '(name: any, i: any, array: any) => any' is
// not assignable to parameter of type '(u: string) => any'
 assertType<string>(name);
 assertType<number>(i);
 assertType<string[]>(array);
 assertType<string[]>(this);
 // ~~~~ 'this' implicitly has type 'any'
 return name.length;
 }
));
```

### Declaration that passes the checks

```d
declare function map<U, V>(
 array: U[],
 fn: (this: U[], u: U, i: number, array: U[]) => V
): V[];
```

```d
const beatles = ['john', 'paul', 'george', 'ringo'];
map(beatles, function(
 name, // $ExpectType string
 i, // $ExpectType number
 array // $ExpectType string[]
) {
 this // $ExpectType string[]
 return name.length;
}); // $ExpectType number[]
```
