## Factory
**Фабричный метод** — это порождающий паттерн проектирования, который определяет общий интерфейс для создания объектов в суперклассе, позволяя подклассам изменять тип создаваемых объектов.

Interface
```ts
interface Product {
  productName: string;
  cost: number;
};
```
Creator class
```ts
class ConcreteCreator1 implements Product {
  public productName;
  public cost;

  constructor(productName: string) {
    this.productName = productName;
    this.cost = 150;
  };
};
class ConcreteCreator2 implements Product {
  public productName;
  public cost;

  constructor(productName: string) {
    this.productName = productName;
    this.cost = 500;
  };
};
```
Creator
```ts
type ProductClass = { new(name: string): Product };

class Creator {
  static productList: { [key: string]: ProductClass } = {
    product1: ConcreteCreator1,
    product2: ConcreteCreator2,
  };

  public create(productName: string, type: string): Product {
    const ConcreteProduct = Creator.productList[type];
    const product = new ConcreteProduct(productName);

    return product;
  };
};
```
Client code
```ts
function clientCode(productName: string, type: string) {
  const creator = new Creator();
  return creator.create(productName, type);
};
clientCode('object1', 'product1');
clientCode('object2', 'product2');
```
Log
```ts
// ConcreteCreator1 { productName: 'object1', cost: 150 }
// ConcreteCreator2 { productName: 'object2', cost: 500 }
```
