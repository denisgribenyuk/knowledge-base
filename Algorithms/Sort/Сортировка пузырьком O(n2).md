## Сортировка пузырьком
```ts
function bubbleSort(arr: number[]) {
  while (true) {
    let isUnsorted = false

    for (let i = 0; i <= arr.length - 1; i++) {
      let curr = arr[i];
      let next = arr[i + 1];
      if (curr > next) {
        arr[i + 1] = curr;
        arr[i] = next;
        isUnsorted = true
      }
    }

    if (!isUnsorted) {
      break
    }
  }

  return arr
}
```
