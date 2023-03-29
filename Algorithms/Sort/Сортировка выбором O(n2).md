## Сортировка выбором _O(n2)_
```ts
function smallest(arr) {
  let smallest = arr[0];
  let smallest_index = 0;

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < smallest) {
      smallest = arr[i];
      smallest_index = i;
    }
  }

  return smallest_index;
}

function selectionSort(arr) {
  const newArr = [];
  const length = arr.length;
  for (let i = 0; i < length; i++) {
    let smallest = this.smallest(arr);
    newArr.push(...arr.splice(smallest, 1));
  }
  return newArr;
}
```
