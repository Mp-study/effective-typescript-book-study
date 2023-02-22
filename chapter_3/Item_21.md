## Item 21 : 타입 넓히기

### EX1)

```jsx
const mixed = ['x', 1];
```

- `('x' | 1)[]`
- `[’x’, 1]`
- `[string, nubmer]`
- `(string|number)[]`
- `any[]`
- …
- `|` (유니언 타입)을 사용해서 타입은 넓혀줄 수 있다
- as const를 쓰면 단일 타입으로 고정시킬 수 있다