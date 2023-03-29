## Factory method
**Фабричный метод** — это порождающий паттерн проектирования, который определяет общий интерфейс для создания объектов в суперклассе, позволяя подклассам изменять тип создаваемых объектов.

Interface
```ts
interface Product {
  operation(): string;
};
```
Abstract creator
```ts
abstract class Creator {
  public abstract factoryMethod(): Product;

  public someOperation(): string {
    const product = this.factoryMethod();

    return product.operation();
  };
};
```
Product class
```ts
class ConcreteProduct1 implements Product {
  public operation(): string {
    return '{one object}';
  };
};

class ConcreteProduct2 implements Product {
  public operation(): string {
    return '{two object}';
  };
};
```
Creator class
```ts
class ConcreteCreator1 extends Creator {
  public factoryMethod(): Product {
    return new ConcreteProduct1();
  };
};

class ConcreteCreator2 extends Creator {
  public factoryMethod(): Product {
    return new ConcreteProduct2();
  };
};
```
Client code
```ts
function clientCode(creator: Creator): string {
  return creator.someOperation();
};

clientCode(new ConcreteCreator1());
clientCode(new ConcreteCreator2());
```
Log
```ts
// {one object}
// {two object}
```
