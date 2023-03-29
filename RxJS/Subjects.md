## Subjects
Отличия между _Observable и Subject_
```
                                          Observable    Subject 
Имеет список подписчиков                      ✖            ✔   
Выполняется заново для каждого подписчика     ✔            ✖  
```
Каждый _Subject_ одновременно является и наблюдаемым объектом _Observable_ и наблюдателем _Observer_ поэтому реализует как метод subscribe для получения данных, так и методы _next(v)_, _error(e)_ и _complete()_ для отправки данных. Так как _Subject_ может выходить в роли Наблюдателя, это означает что вы можете передать _Subject_ как аргумент метода _subscribe_.
```ts
import { Subject, from } from 'rxjs';

const subject = new Subject<number>();

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});

subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

const observable = from([1, 2, 3]);

observable.subscribe(subject); // Можно подписаться передав Subject

// Logs:
// observerA: 1
// observerB: 1
// observerA: 2
// observerB: 2
// observerA: 3
// observerB: 3
```
_BehaviorSubject_ хранит последнее полученное значение и автоматически отправляет его при появлении нового подписчика.
```ts
import { BehaviorSubject } from 'rxjs';
const subject = new BehaviorSubject(0); // 0 изначальное значение
console.log(`Current value is: ${subject.value}`)

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});

subject.next(1);
subject.next(2);

subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subject.next(3);

// Logs
// Current value is: 0
// observerA: 0
// observerA: 1
// observerA: 2
// observerB: 2
// observerA: 3
// observerB: 3
```
_ReplaySubject_ запоминает множество значений и отправляет эти значения новым подписчикам.
```ts
import { ReplaySubject } from 'rxjs';
const subject = new ReplaySubject(3); // отправляет последние 3 значения новым подписчикам

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});

subject.next(1);
subject.next(2);
subject.next(3);
subject.next(4);

subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subject.next(5);

// Logs:
// observerA: 1
// observerA: 2
// observerA: 3
// observerA: 4
// observerB: 2
// observerB: 3
// observerB: 4
// observerA: 5
// observerB: 5
```
_AsyncSubject_ отправляет только последнее значение своим подписчикам, но только после того как буден вызван _complete()_
```ts
import { AsyncSubject } from 'rxjs';
const subject = new AsyncSubject();

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});

subject.next(1);
subject.next(2);
subject.next(3);
subject.next(4);

subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subject.next(5);
subject.complete();

// Logs:
// observerA: 5
// observerB: 5
```
