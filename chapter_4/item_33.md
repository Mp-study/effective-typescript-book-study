## 아이템 33 string 타입보다 더 구체적인 타입 사용하기

- ‘문자열을 남발하여 선언된’ 코드를 피합시다. 모든 문자열을 할당할 수 있는 string타입보다는 더 구체적인 타입을 사용하는 것이 좋습니다.
- 변수는 범위를 보다 정확하게 표현하고 싶다며 string 타입보다는 문자열 리터럴 타입의 유니온을 사용하면 됩니다. 타입 체크를 더 엄격히 할 수 있고 생산성을 향상시킬 수 있습니다.

```tsx
function pluck<T>(records:T[], key:string): any[] {
	return records.map(r => r[key]) // '{}' 형식에 인덱스 시그니처가 없으므로 요소에 암시적으로 'any' 형식이 있습니다.
}

function pluck<T>(records: T[], key: keyof T) {
	return records.map(r => r[key]);
}

=> function pluck<T>(records: T[], key: keyof T): T[keyof T][];
=> function pluck<T>(records: T[], key: K): T[K][]
```

- 객체의 속성 이름을 함수 매개변수를 받을 때는 string보다 keyof T를 사용하는 것이 좋습니다.