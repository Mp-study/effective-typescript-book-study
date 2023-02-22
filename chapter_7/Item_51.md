# Item 51: Mirror Types to Sever Dependencies

## Suppose you’ve written a library for parsing CSV files

### As a convenience for your NodeJS users, you allow the contents to be either a string or a NodeJS Buffer

```d
function parseCSV(contents: string | Buffer): {[column: string]: string}[] {
 if (typeof contents === 'object') {
 // It's a buffer
 return parseCSV(contents.toString('utf8'));
 }
 // ...
}
```

### The type definition for Buffer comes from the NodeJS type declarations, which you must install

```d
npm install --save-dev @types/node
```

## Rather than using the declaration of Buffer from @types/node, you can

```d
interface CsvBuffer {
 toString(encoding: string): string;
}
function parseCSV(contents: string | CsvBuffer): {[column: string]: string}[] {
 // ...
}
```

```d
parseCSV(new Buffer("column1,column2\nval1,val2", "utf-8")); // OK
```
