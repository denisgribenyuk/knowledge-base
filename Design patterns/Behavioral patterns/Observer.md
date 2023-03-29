## Observer
**Наблюдатель** - это поведенческий паттерн проектирования, который создаёт механизм подписки, позволяющий одним объектам следить и реагировать на события, происходящие в других объектах.

Interface
```ts
interface Subject {
  state: number;
  attach(observer: Observer): void;
  detach(observer: Observer): void;
  notify(): void;
};

interface Observer {
  update(subject: Subject): void;
};
```
Concrete subject
```ts
class ConcreteSubject implements Subject {
  public state!: number;
  private observers: Observer[] = [];

  public attach(observer: Observer): void {
    const isExist = this.observers.includes(observer);
    if (!isExist) {
      this.observers.push(observer);
    };
  };

  public detach(observer: Observer): void {
    const observerIndex = this.observers.indexOf(observer);
    if (observerIndex !== -1) {
      this.observers.splice(observerIndex, 1);
    };
  };

  public notify(): void {
    for (const observer of this.observers) {
      observer.update(this);
    };
  };

  public someBusinessLogic(): void {
    this.state = Math.floor(Math.random() * (10 + 1));
    console.log(`Subject: My state has just changed to: ${this.state}`);
    this.notify();
  };
};
```
Concrete observers
```ts
class ConcreteObserverA implements Observer {
  public update(subject: Subject): void {
    console.log(`ConcreteObserverA got ${subject.state}`);

  };
};

class ConcreteObserverB implements Observer {
  public update(subject: Subject): void {
    console.log(`ConcreteObserverB got ${subject.state}`);
  };
};
```
Client code
```ts
const subject = new ConcreteSubject();

const observerA = new ConcreteObserverA();
subject.attach(observerA);

const observerB = new ConcreteObserverB();
subject.attach(observerB);

subject.someBusinessLogic();
```
Log
```ts
// Subject: My state has just changed to: 10
// ConcreteObserverA got 10
// ConcreteObserverB got 10
```
