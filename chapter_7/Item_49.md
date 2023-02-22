# Item 49: Provide a Type for this in Callbacks

## Understand how this binding works

```d
class C {
 vals = [1, 2, 3];
 logSquares() {
    for (const val of this.vals) {
        console.log(val * val);
    }
 }
}

const c = new C();
c.logSquares();
```

Result

```d
1
4
9
```

## Error occurs when

```d
const c = new C();
const method = c.logSquares;
method();
```

```d
Uncaught TypeError: Cannot read property 'vals' of undefined
```

## <b>Solution</b>

```d
const c = new C();
const method = c.logSquares;
method.call(c); // Logs the squares again
```

## Error occurs when

```d
class ResetButton {
 render() {
    return makeButton({text: 'Reset', onClick: this.onClick});
 }
 onClick() {
    alert(`Reset ${this}`);
 }

}
```

## <b>Solution 1</b>

```d
class ResetButton {
 constructor() {
    this.onClick = this.onClick.bind(this);
 }
 render() {
    return makeButton({text: 'Reset', onClick: this.onClick});
 }
 onClick() {
    alert(`Reset ${this}`);
 }
}
```

## <b>Solution 2</b>

```d
class ResetButton {
 render() {
    return makeButton({text: 'Reset', onClick: this.onClick});
 }
 onClick = () => {
    alert(`Reset ${this}`); // "this" always refers to the ResetButton instance.
 }
}
```

<hr>

## `this` typing example

```d
function addKeyListener(
 el: HTMLElement,
 fn: (this: HTMLElement, e: KeyboardEvent) => void
) {
 el.addEventListener('keydown', e => {
 fn(e);
// ~~~~~ The 'this' context of type 'void' is not assignable
// to method's 'this' of type 'HTMLElement'
 });
```

## <b>Solution </b>

```d
declare let el: HTMLElement;
addKeyListener(el, function(e) {
 this.innerHTML; // OK, "this" has type of HTMLElement
});
```

## Aware of arrow funtion

If you use an arrow function here, you’ll override the value of this. TypeScript will catch the issue.

```d
class Foo {
    registerHandler(el: HTMLElement) {
    addKeyListener(el, e => {
        this.innerHTML;
        // ~~~~~~~~~ Property 'innerHTML' does not exist on type 'Foo'
    });
  }
}
```
