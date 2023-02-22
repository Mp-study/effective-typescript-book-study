## Item 22 : 타입 좁히기

- if 사용하는 방법
    
    ```jsx
    const el = document.getElementById('foo'); // 타입이 HTMLElement | null
    
    if(el) {
      el.innerHTML = 'hi'
      // el 타입 HTMLElement
    } else {
      alert('No element #foo')
      // el 타입이 null
    }
    ```
    
- Array.isArray같은 일부 내장 함수 사용
    
    ```jsx
    function contains(text: string, terms: string | string[]) {
      const termList = Array.isArray(terms) ? terms : [terms];
      termList // 타입이 string[]
    }
    ```
    
- insteardof
    
    ```jsx
    function contains(text: string, search: string | RegExp) {
      if (search instanceof RegExp) {
        search // 타입이 RegExp
        return !!search.exec(text)
      }
      search // 타입이 string
      return text.includes(search)
    }
    ```
    
- 속성 확인
    
    ```jsx
    function pickAB(ab: A | B) {
      if ("a" in ab) {
        ab // 타입이 A
      } else {
        ab // 타입이 B
      }
      ab // 타입이 A | B
    }
    ```
    
- 태그된 유니온(tagged union), 구별된 유니온(discriminated union)
    
    ```jsx
    interface UploadEvent {
      type: "upload"
      filename: string
      contents: string
    }
    
    interface DownloadEvent {
      type: "download"
      filename: string
    }
    
    type AppEvent = UploadEvent | DownloadEvent
    
    function handleEvent(e: AppEvent) {
      switch(e.type) {
        case 'download':
          e // 타입이 DownloadEvent
          break;
    
        case 'upload':
          e // 타입이 UploadEvent
          break;
      }
    }
    ```
    
- 사용자 정의 타입 가드
    
    ```jsx
    const isDefined = <T>(x: T | undefined): x is T => {
      return x !== undefined;
    };
    ```