# Item 47: Export All Types That Appear in Public APIs

## Suppose you want to create some secret, unexported types

```d
interface SecretName {
 first: string;
 last: string;
}

interface SecretSanta {
 name: SecretName;
 gift: string;
}

export function getGift(name: SecretName, gift: string): SecretSanta {
 // ...
```

## One way is to use the Parameters and ReturnType generic types:

```d
type MySanta = ReturnType<typeof getGift>; // SecretSanta
type MyName = Parameters<typeof getGift>[0]; // SecretName
```

Export types that appear in any form in any public method.
\
Your users will be able to extract them anyway,
\
so you may as well make it `easy` for them.
