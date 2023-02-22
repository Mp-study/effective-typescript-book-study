# Item 32: Prefer Unions of Interfaces to Interfaces of Unions

## Interfaces of Unions 👎

```d
interface Layer {
 layout: FillLayout | LineLayout | PointLayout;
 paint: FillPaint | LinePaint | PointPaint;
}
```

## Unions of Interfaces 👍

```d
interface FillLayer {
 layout: FillLayout;
 paint: FillPaint;
}

interface LineLayer {
 layout: LineLayout;
 paint: LinePaint;
}

interface PointLayer {
 layout: PointLayout;
 paint: PointPaint;
}

type Layer = FillLayer | LineLayer | PointLayer;
```

## Pattern `"Tagged Union"` 👍👍

```d
interface Layer {
 type: 'fill' | 'line' | 'point';
 layout: FillLayout | LineLayout | PointLayout;
 paint: FillPaint | LinePaint | PointPaint;
}
```

## 😍😍

```d
function drawLayer(layer: Layer) {
  if (layer.type === 'fill') {
    const { paint } = layer; // Type is FillPaint
    const { layout } = layer; // Type is FillLayout
  } else if (layer.type === 'line') {
    const { paint } = layer; // Type is LinePaint
    const { layout } = layer; // Type is LineLayout
  } else {
    const { paint } = layer; // Type is PointPaint
    const { layout } = layer; // Type is PointLayout
  }
}
```

## Use `Now-familiar union of interfaces`

### Example

```d
interface Person {
  name: string;
  birth?: {
    place: string;
    date: Date;
  }
}
```

will complain,

```d
const alanT: Person = {
 name: 'Alan Turing',
 birth: {
  // ~~~~ Property 'date' is missing in type
  // '{ place: string; }' but required in type
  // '{ place: string; date: Date; }'
  place: 'London'
 }
}
```

and also need to check properties like below

```d
function eulogize(p: Person) {
  console.log(p.name);

  const {birth} = p;

  if (birth) {
    console.log(`was born on ${birth.date} in ${birth.place}.`);
  }

}
```

instead use Now-familiar union of interfaces pattern below.

```d
interface Name {
 name: string;
}

interface PersonWithBirth extends Name {
 placeOfBirth: string;
 dateOfBirth: Date;
}

type Person = Name | PersonWithBirth;
```

Then, will get same benefits as with the nested object 😍

```d
function eulogize(p: Person) {
  if ('placeOfBirth' in p) {
      p // Type is PersonWithBirth
      const {dateOfBirth} = p // OK, type is Date
  }
}
```
