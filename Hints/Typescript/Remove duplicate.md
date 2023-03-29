## Remove duplicate

```ts
interface Car {
  name: string;
  price: number;
}

const numlist: number[] = [1, 2, 1, 3, 3, 4, 5, 6, 7, 7, 1];
const objList: Car[] = [
  { name: 'audi', price: 230 },
  { name: 'bmw', price: 370 },
  { name: 'bmw', price: 400 },
  { name: 'ford', price: 120 },
  { name: 'audi', price: 330 },
  { name: 'opel', price: 250 },
  { name: 'vw', price: 370 },
  { name: 'vw', price: 500 },
  { name: 'vw', price: 310 },
]

const withoutDuplicateNumList = numlist.filter((e, i, a) => a.indexOf(e) === i);
const withoutDuplicateObjList = objList.filter((e, _, a) => a.find(el => el.name === e.name) === e);

console.log(withoutDuplicateNumList);
console.log(withoutDuplicateObjList);
```
Log:
```ts
[ 1, 2, 3, 4,  5, 6, 7 ];
[
  { name: 'audi', price: 230 },
  { name: 'bmw', price: 370 },
  { name: 'ford', price: 120 },
  { name: 'opel', price: 250 },
  { name: 'vw', price: 370 }
]
```
