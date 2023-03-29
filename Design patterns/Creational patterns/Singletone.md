## Singletone
**Одиночка** — это порождающий паттерн проектирования, который гарантирует, что у класса есть только один экземпляр, и предоставляет к нему глобальную точку доступа.

Singleton class
```ts
class Singleton {
  private static instance: Singleton;

  private constructor() { };

  public static getInstance(): Singleton {
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    };

    return Singleton.instance;
  };
};
```
Client code
```ts
function clientCode() {
  const s1 = Singleton.getInstance();
  const s2 = Singleton.getInstance();

  if (s1 === s2) {
    console.log('Singleton works');
  } else {
    console.log('Singleton failed');
  }
}

clientCode();
```
Log
```ts
// Singleton works
```
