## Method Decorator
```ts
class User {
  private name = 'Vladimir';

  @greet
  public getUserName(): string {
    return this.name;
  }
}

function greet(
  classPrototype: {}, 
  methodName: string, 
  descriptor: PropertyDescriptor
  ): void {
    
  const method = descriptor.value;
  
  descriptor.value = function () {
    const result = method.call(this);
    
    return `Hello, ${result}!`;
  }
}

const user = new User();
console.log(user.getUserName())

// logs:
// Hello, Vladimir!
```
