## Item 38 : any 타입은 가능한 한 좁은 범위에서만 사용하기

- 함수를 변수에 할당할 때 변수에 any타입을 지정했는데 이건 No no

```tsx
const x: any = expressionReturningFoo(); //X
processBar(x);

const x = expressionReturningFoo(); //O
processBar(x as any);

//혹은
const x = expressionReturningFoo(); //O
// @ts-ignore
processBar(x);
```

- 예를들면 `expressionReturningFoo()`의 결과 값이 object였을 때 x에 any를 넣으면 `x.fooMethod();` 이런 식으로는 체크가 되지 않음.
- return any x
- 객체 전체 any x 일부에만 as any