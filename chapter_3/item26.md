# Item 26: Understand How Context Is Used in Type Inference

- TypeScript doesn’t just infer types based on values. It also considers the context in which the value occurs. This usually works well but can sometimes lead to surprises.

## Be aware of how context is used in type inference.
## If factoring out a variable introduces a type error, consider adding a type declaration.
## If the variable is truly a constant, use a const assertion (as const). But be aware that this may result in errors surfacing at use, rather than definition.

컨텍스트 and 타입 추론
