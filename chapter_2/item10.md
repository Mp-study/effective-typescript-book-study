# Item 10: Avoid Object Wrapper Types (String, Number, Boolean, Symbol, BigInt)

## Understand how object wrapper types are used to provide methods on primitive values. Avoid instantiating them or using them directly.

- call by reference
- call by value
```js
"hello" === new String("hello") //false
new String("hello") === new String("hello") // false
```
there’s usually no reason to instantiate them directly.

## Avoid TypeScript object wrapper types. Use the primitive types instead: string instead of String, number instead of Number, boolean instead of Boolean, symbol instead of Symbol, and bigint instead of BigInt.



!intersting
As a final note, it’s OK to call BigInt and Symbol without new, since these create primitives:

```js
typeof BigInt(1234) "bigint"
typeof Symbol('sym') "symbol"
```
- These are the BigInt and Symbol values, not the TypeScript types
