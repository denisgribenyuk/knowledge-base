## Adapter, Wrapper
**Адаптер** - это структурный паттерн проектирования, который позволяет объектам с несовместимыми интерфейсами работать вместе.

Class Target
```ts
class Target {
  public request(): string {
    return 'Target: I am target';
  }
}
```
Class Adaptee
```ts
class Adaptee {
  public specificRequest(): string {
    return 'Adaptee: I am adaptee';
  }
}
```
Class Adapter
```ts
class Adapter extends Target {
  private adaptee: Adaptee;

  constructor(adaptee: Adaptee) {
    super();
    this.adaptee = adaptee;
  }

  public request(): string {
    return this.adaptee.specificRequest();
  }
}
```
Client code
```ts
function clientCode(target: Target): void {
  console.log(target.request());
}

const target = new Target();
const adaptee = new Adaptee();
const adapter = new Adapter(adaptee);

clientCode(target);
clientCode(adapter);
```
Log
```ts
// Target: I am target
// Adaptee: I am adaptee 
```
