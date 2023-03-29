## Поиск в ширину (BFS)
```ts
// Обход в ширину работает только для невзвешенных графов
// Создаем (граф) хэш-таблицу
const graph = {
  	'cab': ['car', 'cat'],
	'car': ['cat', 'bar'],
	'cat': ['mat', 'bat'],
	'mat': ['bat'],
	'bar': ['bat'],
	'bat': []
}
// Функция принимает граф, стартовую и финишную точки
function searchPath(graph: Record<string, string[]>, startItem: string, searchItem: string) {
// Записываем в очередь первые узлы графа
const search_queue: string[] = graph[startItem];
// Создаем список проверенных узлов
const searched: string[] = [];
// Пока в очереди есть элементы на проверку...
	while (search_queue.length) {
		// Извлекаем первый элемент из очереди
		let nextItem = search_queue.shift() || '';
		// Проверяем, проверялся ли этот элемент ранее, если true - прерываем текущую итерацию
		if (searched.includes(nextItem)) continue;
		// Проверяем, тот ли это элемент который мы ищем, если да - возвращаем true
		if (nextItem === searchItem) {
			return true;
		} else {
			// Иначе, добавляем в конец очереди все соседние узлы элемента
			graph[nextItem].forEach((element: string) => {
				search_queue.push(element);
			});
			// Проверенный элемент добавляем в список проверенных
			searched.push(nextItem);
		}
	}
	// Если цикл закончился, а искомый элемент не был найден - возвращаем false
	return false;
}
```
