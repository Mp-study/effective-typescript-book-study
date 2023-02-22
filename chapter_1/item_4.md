## 아이템 4 구조적 타이핑에 익숙해지기

- 자바스크립트가 덕 타이핑(duck typing) 기반이고 타입스크립트가 이를 모델링하기 위해 구조적 타이핑을 사용함을 이해해야 합니다. 어떤 인터페이스에 할당 가능한 값이라면 타입 선언에 명시적으로 나열된 속성들을 가지고 있을 겁니다. 타입은 봉인되어 있지 않습니다.

```tsx
interface Vector2D {
	x: number;
	y: number;
}

function calculateLength(v: Vector2D) {
	return Math.sqrt(v.x * v.x + v.y * v.y);
}

interface NamedVector {
	name: string;
	x: number;
	y: number;
}

const v:NamedVector = { x: 3, y:4, name:'Zee' };
calculateLength(v);

// 타입스크립트 타입 시스템은 자바스크립트의 런타임 동작을 모델링
// NamedVector의 구조가 Vector2D와 호환되기 때문에 calculateLength 호출이 가능

interface Venctor3D {
	x: number;
	y: number;
	z: number;
}

function normalize(v: Vector3D) {
	const length = calculateLength(v);
	return {
		x: v.x / length,
		y: v.y / length,
		z: v.z / length,
	}
}

normalize({ x: 3, y: 4, z: 5 });
// { x: 0.6, y: 0.8, z:1 };

// Vector3D와 호환되는 {x, y, z} 객체로 calculateLength를 호출하면, 구조적 타이핑 관점에서
// x와 y가 있어서 Vector2D와 호환됩니다. 따라서 오류가 발생하지 발생하지 않았습니다.
// 함수를 작성할 때, 호출에 사용되는 매개변수의 속성들이 매개변수 타입에 선언된 속성만을 가질거라 생각하기 쉬움
// 이러한 타입은 봉인된(sealed) 또는 정확한(precise) 타입이라 불리우는데 타입스크립트는 아님
// 좋든 싫든 열려(open) 있음
```

- 클래스 역시 구조적 타이핑 규칙을 따른다는 것을 명심해야 합니다. 클래스의 인스턴스가 예상과 다를 수 있습니다.
- 구조적 타이핑을 사용하면 유닛 테스팅을 손쉽게 할 수 있습니다.