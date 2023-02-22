# Item 28: Prefer Types That Always Represent Valid States

## Not valid enough 👎

```d
interface State {
 pageText: string;
 isLoading: boolean;
 error?: string;
}
```

## Valid state 👍

```d
interface RequestPending {
 state: 'pending';
}

interface RequestError {
 state: 'error';
 error: string;
}

interface RequestSuccess {
 state: 'ok';
 pageText: string;
}

type RequestState = RequestPending | RequestError | RequestSuccess;

interface State {
 currentPage: string;
 requests: { [page: string]: RequestState };
}
```

Use `a tagged union` (also known as a `“discriminated union”`) to explicitly model

```q
type RequestState = RequestPending | RequestError | RequestSuccess
```

\
Try to program as simple as possible for easier typing.

## Bad code design 👎

```d
interface CockpitControls {
 /** Angle of the left side stick in degrees, 0 = neutral, + = forward */
 leftSideStick: number;
 /** Angle of the right side stick in degrees, 0 = neutral, + = forward */
 rightSideStick: number;
}
```

which will result difficult to maintain and extend logics

```d
function getStickSetting(controls: CockpitControls) {
 const {leftSideStick, rightSideStick} = controls;
 if (leftSideStick === 0) {
 return rightSideStick;
 } else if (rightSideStick === 0) {
 return leftSideStick;
 }
 // ???
}
```

## Bad code design 👍

```d
interface CockpitControls {
 /** Angle of the stick in degrees, 0 = neutral, + = forward */
 stickAngle: number;
}
```

Narrowing down variable scopes and its meaning, will lead you to maintain code alot better.
