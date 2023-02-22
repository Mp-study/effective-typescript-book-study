## Item 19 :  추론 가능한 타입을 사용해 장황한 코드 작성하기

- 숙련된 타입스크립트 사용자는 필요한 곳에만 타입을 명시
- 초보자는 추론되는 부분까지 타입을 명시하는 경우가 있음
- 추론 가능한 타입을 사용해 장황한 코드 방지
- 라이브러리를 사용할 때 라이브러리에 파라미터 타입이 정해져 있는 경우에도 타입선언을 하지 않음

### EX1)

```jsx
const cache: {[ticket: string]: number} = {};

function getQuote(ticker: string): Promise<number> {
	if (ticker in cache) {
		return cache[ticker];
		// 'number' 형식은 'Promise<number>' 형식에 할당할 수 없습니다.
	}
}
```

- 리턴 타입은 number | Promise 하지만 if에 number를 리턴하기 때문에 안 됨
- 해결 방법은 리턴 타입을 Promise<number>로 두고 `promise.resolve(값);` 을 리턴

### EX2)

```jsx
interface Vector2D { x: number; y: number;}

function add(a: Vector2D, b: Vector2D) {
	return { x: a.x + b.x, y: a.y + b.y };
}
```

- 이런 경우 return type을 지정해줘야 덕타이핑 예방할 수 있음