# Item 11: Recognize the Limits of Excess Property Checking

## When you assign an object literal to a variable or pass it as an argument to a function, it undergoes excess property checking.

## Excess property checking is an effective way to find errors, but it is distinct from the usual structural assignability checks done by the TypeScript type checker. Conflating these processes will make it harder for you to build a mental model of assignability.

## Be aware of the limits of excess property checking: introducing an intermediate variable will remove these checks.

-   duck typing? does not happen
-   Excess property checking does not happen when you use a type assertion
```js
interface Room {
    numDoors: number;
    ceilingHeightFt: number;
}

const r1: Room = {
    numDoors: 1,
    ceilingHeightFt: 10,
    elephant: 'present', // error // excess property check
};

const obj = {
    numDoors: 1,
    ceilingHeightFt: 10,
    elephant: 'present',
};

const r2: Room = obj; // ok
```

