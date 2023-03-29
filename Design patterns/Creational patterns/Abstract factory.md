## Abstract factory
**Абстрактная фабрика** — это порождающий паттерн проектирования, который позволяет создавать семейства связанных объектов, не привязываясь к конкретным классам создаваемых объектов.

Interfaces
```ts
interface AbstractFactory {
  createProductA(): AbstractProductA;
  createProductB(): AbstractProductB;
};

interface AbstractProductA {
  create(): string;
};

interface AbstractProductB {
  create(): string;
};
```
Concrete factory
```ts
class ConcreteFactory1 implements AbstractFactory {
  public createProductA(): AbstractProductA {
    return new ConcreteProductA1();
  };
  public createProductB(): AbstractProductB {
    return new ConcreteProductB1();
  };
};

class ConcreteFactory2 implements AbstractFactory {
  public createProductA(): AbstractProductA {
    return new ConcreteProductA2();
  };
  public createProductB(): AbstractProductB {
    return new ConcreteProductB2();
  };
};
```
Concrete product
```ts
class ConcreteProductA1 implements AbstractProductA {
  public create(): string {
    return 'was created ConcreteProductA1.';
  };
};

class ConcreteProductA2 implements AbstractProductA {
  public create(): string {
    return 'was created ConcreteProductA2.';
  };
};

class ConcreteProductB1 implements AbstractProductB {
  public create(): string {
    return 'was created ConcreteProductB1.';
  };
};

class ConcreteProductB2 implements AbstractProductB {
  public create(): string {
    return 'was created ConcreteProductB2.';
  };
};
```
Client code
```ts
function clientCode(factory: AbstractFactory) {
  const productA = factory.createProductA();
  const productB = factory.createProductB();

  return [
    productA.create(),
    productB.create(),
  ];
};

clientCode(new ConcreteFactory1());
clientCode(new ConcreteFactory2());
```
Log
```ts
// was created ConcreteProductA1.
// was created ConcreteProductA2.
// was created ConcreteProductB1.
// was created ConcreteProductB2.
```
