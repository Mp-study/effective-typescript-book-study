## Item 20 : 다른 타입에는 다른 변수 사용하기

- 한 변수 안에 여러 타입을 섞어 쓰면 안 된다.

### EX1)

```jsx
let id = "12-34-56";
fetchProduct(id); //string으로 사용
id = 123456;
fetchProductBySerialNumber(id); //number로 사용
```