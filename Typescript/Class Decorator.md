## Class Decorator
```ts
type ClassConstructor = new (...args: any[]) => {}
type Bug = {
  type: string;
  title: string;
  reportingURL: string;
}

function reportableClassDecorator<T extends ClassConstructor>(constructor: T) {
  return class extends constructor {
    reportingURL = 'http://www...';
  }
}

@reportableClassDecorator
class BugReport {
  type = 'report';
  title: string;

  constructor(t: string) {
    this.title = t;
  }
}

const bug = new BugReport('Needs dark mode')
console.log(bug.title);
console.log(bug.type);
console.log((bug as Bug).reportingURL);

// log:
// Needs dark mode
// report
// http://www...
```
