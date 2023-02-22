# Item 30: Don’t Repeat Type Information in Documentation

## Bad and ambiguous code 👎

Codes and comments, their exaplanation and behaviors are different.

```d
/**
 * Returns a string with the foreground color.
 * Takes zero or one arguments. With no arguments, returns the
 * standard foreground color. With one argument, returns the foreground color
 * for a particular page.
 */
function getForegroundColor(page?: string) {
 return page === 'login' ? {r: 127, g: 127, b: 127} : {r: 0, g: 0, b: 0};
}

```

## Better code and comment 👍

```d
/** Get the foreground color for the application or a specific page. */
function getForegroundColor(page?: string): Color {
 // ...
}
```

## Even better comment 👍👍

Annotation comment convention will explain in details if anything is missing or coded wrongly.

```d
/**
 * Generate a greeting.
 * @param name Name of the person to greet
 * @param salutation The person's title
 * @returns A greeting formatted for human consumption.
 */
function greetFullTSDoc(name: string, title: string) {
 return `Hello ${title} ${name}`;
}
```
