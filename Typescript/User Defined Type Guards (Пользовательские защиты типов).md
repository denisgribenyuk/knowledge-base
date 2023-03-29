## User Defined Type Guards
Защиты типов — это встроенная особенность _TypeScript_, позволяющая уточнять типы с _typeof_ и _instanceof_ Когда есть функция, уточняющая типы своих параметров и возвращающая _boolean_ , можно использовать пользовательскую защиту типа, гарантирующую, что уточнение будет передано при каждом использовании этой функции. Уточнение типа в функции _isString_ осталось в области действия своей функции и не перешло в другие области.
```ts
function isString(a: unknown): boolean {
  return typeof a === 'string';
};

function parseInput(input: string | number) {
  let formattedInput: string;
  if (isString(input)) {
    formattedInput = input.toUpperCase();
    // Ошибка! Свойство "toUpperCase" не существует в типе "string | number".
  }
}
```
Мы можем сообщить модулю проверки не только, что _isString_ возвращает _boolean_, но также, что если _boolean_ будет _true_, то переданный нами в _isString_ аргумент является _string_ .
```ts
function isString(a: unknown): a is string {
  return typeof a === 'string';
};

function parseInput(input: string | number) {
  let formattedInput: string;
  if (isString(input)) {
    formattedInput = input.toUpperCase();
  }
}
```
