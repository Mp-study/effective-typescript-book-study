## Item 58 : 모던 자바스크립트로 작성하기

- ECMAScript 모듈 사용
- 프로토타입 대신 클래스 사용
- var대신 let/const 사용(호이스팅 관점에서)
- for(;;)대신 for-of 또는 배열 메서드 사용
- 함수 표현식보다 화살표 함수 사용(`this`문제와 연관지어서 설명하고 컴파일러 옵션에 `noImplictThis` 또는 `strict`를 설정하면 `TS`가 `this` 바인딩 관련 오류를 표시해줌)
- 단축 객체 표현과 구조 분해 할당 사용
- 함수 매개변수 기본값 사용
- 저수준 프로미스나 콜백 대신 `async/await` 사용하기
- 연관 배열에 객체 대신 Map과 Set사용(`constructor`라는 `Object.prototype`을 예시로 듦)
- 타입스크립트에 `use strict` 넣지 않기(`TS`의 안전성 검사가 엄격 모드보다 훨씬 더 엄격한 체크를 하기 때문)