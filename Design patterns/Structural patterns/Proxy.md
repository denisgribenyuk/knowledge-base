## Proxy
Заместитель — это структурный паттерн проектирования, который позволяет подставлять вместо реальных объектов специальные объекты-заменители. Эти объекты перехватывают вызовы к оригинальному объекту, позволяя сделать что-то до или после передачи вызова оригиналу (контроль доступа, кеширование, изменение запроса и прочее).

Interface
```ts
interface Subject {
  request(): void;
}
```
Real subject
```ts
class RealSubject implements Subject {
  public request(): void {
    console.log('RealSubject: Handling request.');
  }
}
```
Proxy
```ts
class ProxySubject implements Subject {
  private realSubject: RealSubject;

  constructor(realSubject: RealSubject) {
    this.realSubject = realSubject;
  }

  public request(): void {
    if (this.checkAccess()) {
      this.realSubject.request();
      this.logAccess();
    }
  }

  private checkAccess(): boolean {
    console.log('Proxy: Checking access prior to firing a real request.');

    return true;
  }

  private logAccess(): void {
    console.log('Proxy: Logging the time of request.');
  }
}
```
Client code
```ts
function clientCode(subject: Subject) {
  subject.request();
}

const realSubject = new RealSubject();
clientCode(realSubject);

const proxy = new ProxySubject(realSubject);
clientCode(proxy);
```
Log
```ts
// RealSubject: Handling request.
// Proxy: Checking access prior to firing a real request.
// RealSubject: Handling request.
// Proxy: Logging the time of request.
```
