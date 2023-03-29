## Class for testing

```ts
class Test {
  static assertEquals<T>(returned: T, expected: T): void {
    if (returned === expected) {
      console.log(true);
    } else {
      console.log(`> Expected "${expected}", but return "${returned}"`);
    }
  }
}
```
