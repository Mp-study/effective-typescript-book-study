# Item 24: Be Consistent in Your Use of Aliases

## Aliasing can prevent TypeScript from narrowing types. If you create an alias for a variable, use it consistently.

## Use destructuring syntax to encourage consistent naming.

## Be aware of how function calls can invalidate type refinements on properties. Trust refinements on local variables more than on properties.

- if you introduce an alias, use it consistently.
- use destructuring to decide alias

```js
function isPointInPolygon(polygon: Polygon, pt: Coordinate) { 
    const {bbox} = polygon;
    if (bbox) {
        const {x, y} = bbox;
        if (pt.x < x[0] || pt.x > x[1] ||
            pt.y < x[0] || pt.y > y[1]) { 
                return false;
        }    
    }
// ...
}
```


