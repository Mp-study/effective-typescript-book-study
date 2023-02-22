### 아이템 16 number 인덱스 시그니처보다는 Array, 튜플, ArrayLike를 사용하기

- 타입스크립트는 Array에 숫자 키를 허용하고, 문자열 키와 다른 것으로 인식합니다

```tsx
interface Array<T> {
 //...
 [n:number]: T;
}

//test?
const test:Array<string> = ['test', 'test2'];

const val = test[0];
const va2 = test['1'];
```

- Object.keys 같은 구문은 여전히 문자열로 반환(배열을 순회하는 코드에 대한 실용적인 허용)
- index의 타입이 중요하다면 `for-of`, `forEach`, `for(;;)` (break가 필요하다면) 루프 사용
- 어떤 길이를 가지는 배열과 비슷한 형태의 튜플을 사용하고 싶다면 ArrayLike 타입 사용
- 인덱스 시그니처에 number(런타임에서는 어차피 string으로 인식)를 사용하기보다 Array나 튜플 또는 ArrayLike 타입을 사용하는게 좋음