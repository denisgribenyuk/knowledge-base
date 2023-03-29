## Быстрая сортировка _O(n log n)_
```ts
function qsort(arr: number[]): number[] {
  // Базовый случай - пустой массив, или массив с одним элементом
  if (arr.length < 2) {
    return arr;
  } else {
    // Рекурсивный случай
    // Рандомно выбираем опорный элемент
    const pivot = arr[Math.ceil(arr.length / 2)]
    // Формируем два подмассива: элементы меньше опорного и больше опорного

    const less = arr.filter(e => e < pivot)
    const greater = arr.filter(e => e > pivot)

    // Уходим в рекурсию
    return [...qsort(less), pivot, ...qsort(greater)]
  }
}
```
