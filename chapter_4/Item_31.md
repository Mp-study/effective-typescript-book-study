# Item 31: Push Null Values to the Perimeter of Your Types

## Without "strictNullChecks" option

```d
function extent(nums: number[]) {
 let min, max;

 for (const num of nums) {
    if (!min) {
        min = num;
        max = num;
    } else {
        min = Math.min(min, num);
        max = Math.max(max, num);
        }
    }
  return [min, max];
}
```

## Bug occurs 😥

- If the min or max is zero, it may get overridden. For example, extent([0, 1,
  2]) will return [1, 2] rather than [0, 2].

- If the nums array is empty, the function will return `[undefined, undefined]`. \
  \
  This sort of object with several `undefineds` will be difficult for clients to work with and is exactly the sort of type that this item discourages. \
  \
  We know from reading the source code that `min` and `max` will either both be `undefined` or neither, but that information isn’t represented in the type system.

<br />

## With "strictNullChecks" option will directly notice the issues

```d
function extent(nums: number[]) {
    let min, max;

    for (const num of nums) {
        if (!min) {
            min = num;
            max = num;
        } else {
            min = Math.min(min, num);
            max = Math.max(max, num);
            // ~~~ Argument of type 'number | undefined' is not
            // assignable to parameter of type 'number'
        }
    }

    return [min, max];
}

```

```d
const [min, max] = extent([0, 1, 2]);
const span = max - min;
 // ~~~ ~~~ Object is possibly 'undefined'
```

## `Fully null` or `Fully non-null` 👍

```d
function extent(nums: number[]) {
  let result: [number, number] | null = null;

  for (const num of nums) {
      if (!result) {
         result = [num, num];
      } else {
        result = [Math.min(num, result[0]), Math.max(num, resul[1])];
      }
  }

  return result;
}
```

```d
const [min, max] = extent([0, 1, 2])!;
const span = max - min; // OK
```

Or

```d
const range = extent([0, 1, 2]);
if (range) {
 const [min, max] = range;
 const span = max - min; // OK
}
```

## ❗️ `Do not use` a `mix` of null and non-null values
