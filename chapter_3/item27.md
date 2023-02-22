## Item 27: Use Functional Constructs and Libraries to Help
Use Lodash 

```js
const bestPaid = _(allPlayers)
    .groupBy(player => player.team)
    .mapValues(players => _.maxBy(players, p => p.salary)!) .values()
    .sortBy(p => -p.salary)
    .value() // Type is BasketballPlayer[]
```

