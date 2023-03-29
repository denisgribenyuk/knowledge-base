## Strategy
**Стратегия** — это поведенческий паттерн проектирования, который определяет семейство схожих алгоритмов и помещает каждый из них в собственный класс, после чего алгоритмы можно взаимозаменять прямо во время исполнения программы.

Interface
```ts
interface RouteStrategy {
  buildRoute(distance: number): number
}
```
Strategies
```ts
class RoadStrategy implements RouteStrategy {
  private speed = 80;
  public buildRoute(distance: number): number {
    return distance / this.speed;
  }
}

class PublicTransportStrategy implements RouteStrategy {
  private speed = 60;
  public buildRoute(distance: number): number {
    return distance / this.speed;
  }
}

class WalkingStrategy implements RouteStrategy {
  private speed = 4;
  public buildRoute(distance: number): number {
    return distance / this.speed;
  }
}
```
Context
```ts
class RouteNavigator implements RouteStrategy {
  private routeStrategy!: RouteStrategy;

  public setStrategy(strategy: RouteStrategy): void {
    this.routeStrategy = strategy;
  }

  public buildRoute(distance: number): number {
    return this.routeStrategy?.buildRoute(distance);
  }
}
```
Client code
```ts
function clientCode(strategy: RouteStrategy): number {
  const navigator = new RouteNavigator();
  navigator.setStrategy(strategy);
  const timeSpent = navigator.buildRoute(120);

  return timeSpent;
}

clientCode(new RoadStrategy())
clientCode(new PublicTransportStrategy())
clientCode(new WalkingStrategy())
```
Log
```ts
// 1.5
// 2
// 30
```
