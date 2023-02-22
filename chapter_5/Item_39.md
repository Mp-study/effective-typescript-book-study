## Item 39 : any를 구체적으로 변형해서 사용하기

- any[]
    - array prototype 메서드들이 체크됨
    - 메서드의 결과 값대로 return 값 타입이 추론됨
    - 그 값이 any지만 array가 아닌지 체크함
- any[][]
    - 배열의 배열 any
- {[key: string]: any}
    - 값을 알 수 없는 객체 any
    - 만약 타입을 `object`로 한다면 key 열거는 가능하지만 key에 접근할 수 없음.