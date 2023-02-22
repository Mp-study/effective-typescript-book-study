# Item 8: Know How to Tell Whether a Symbol Is in the Type Space or Value Space



this in value space is JavaScript’s this keyword (Item 49). As a type, this is the TypeScript type of this, aka “polymorphic this.” It’s helpful for implementing method chains with subclasses.



## Know how to tell whether you’re in type space or value space while reading a TypeScript expression. Use the TypeScript playground to build an intuition for this.
- use TypeScript playground to have an intuition on this spaces

```js
interface Cylinder { 
    radius: number; 
    height: number;
}

const Cylinder = (radius: number, height: number) => ({radius, height});

function calculateVolume(shape: unknown) { 
    if (shape instanceof Cylinder) { // instanceof is JavaScript’s runtime operator
        shape.radius
        // ~~~~~~ Property 'radius' does not exist on type '{}'
    } 
}
```


## Every value has a type, but types do not have values. Constructs such as type and interface exist only in the type space.


## "foo" might be a string literal, or it might be a string literal type. Be aware of this distinction and understand how to tell which it is.

```js
const a: 'foo' = 'foo';
const a: string = 'foo';    
```

## typeof, this, and many other operators and keywords have different meanings in type space and value space.
```js
type T1 = typeof p; // Type is Person 
type T2 = typeof email;
// Type is (p: Person, subject: string, body: string) => Response 

const v1 = typeof p; // Value is "object"
const v2 = typeof email; // Value is "function"
```
typeof always operates on values


## Some constructs such as class or enum introduce both a type and a value.
enum, class can be value or type

