## Item 60 : allowjs로 타입스크립트와 자바스크립트 같이 사용하기

- allowJs 컴파일러 옵션으로 타입스크립트와 자바스크립트를 같이 사용할 수 있음.
- 적용하는 법
    - 번들러, 플러그인 방식으로 통합되어 있다면 간단히 적용가능(`npm install —save-dev tsify` 를 통해)
    - 프레임워크 없이 빌드 체인 직접 구성한 경우 `outDir` 옵션(이 옵션은 `TS`가 `outDir`에 지정된 디렉터리에 소스 디렉터리와 비슷한 구조로 코드 생성한후 이 디렉터리를 대상으로 빌드 체인 실행)