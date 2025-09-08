# Итераторы и функция enumerate() в Python

## Теоретическая основа для собеседования

### 1. Основные понятия
- **Итерируемый объект** - объект, который можно перебирать в цикле (списки, строки, словари)
- **Итератор** - объект, который возвращает элементы по одному
- **Протокол итератора** - методы `__iter__()` и `__next__()`

### 2. Разница между итерируемым объектом и итератором
- **Итерируемый** - имеет метод `__iter__()` (можно перебирать)
- **Итератор** - имеет методы `__iter__()` и `__next__()` (возвращает элементы)

### 3. Принцип работы for-цикла
```python
# Цикл for "под капотом":
iterable = [1, 2, 3]
iterator = iter(iterable)
while True:
    try:
        item = next(iterator)
        # обработка item
    except StopIteration:
        break
```

## 1. Функция enumerate()

### Базовое использование
```python
fruits = ['apple', 'banana', 'cherry']
for index, fruit in enumerate(fruits):
    print(f"Индекс {index}: {fruit}")
# Вывод:
# Индекс 0: apple
# Индекс 1: banana
# Индекс 2: cherry
```

### С указанием начального индекса
```python
for i, fruit in enumerate(fruits, start=1):
    print(f"Позиция {i}: {fruit}")
# Вывод:
# Позиция 1: apple
# Позиция 2: banana
# Позиция 3: cherry
```

### Практическое применение
```python
# Создание словаря с индексами
fruits_dict = {i: fruit for i, fruit in enumerate(fruits)}
print(fruits_dict)  # {0: 'apple', 1: 'banana', 2: 'cherry'}

# Поиск элемента с индексом
target = 'banana'
for i, fruit in enumerate(fruits):
    if fruit == target:
        print(f"Найден на позиции {i}")
        break
```

## 2. Функции iter() и next()

### Создание итератора
```python
numbers = [1, 2, 3, 4, 5]
numbers_iterator = iter(numbers)

print(next(numbers_iterator))  # 1
print(next(numbers_iterator))  # 2
print(next(numbers_iterator))  # 3
```

### Обработка StopIteration
```python
iterator = iter([1, 2])
print(next(iterator))  # 1
print(next(iterator))  # 2
try:
    print(next(iterator))  # StopIteration
except StopIteration:
    print("Конец последовательности")
```

### Итерация по строке
```python
text = "hello"
text_iterator = iter(text)
result = []

for char in text_iterator:
    result.append(char)

print(result)  # ['h', 'e', 'l', 'l', 'o']
```

## 3. Range как итерируемый объект

### Использование с iter()/next()
```python
num_range = range(3)
range_iterator = iter(num_range)

print(next(range_iterator))  # 0
print(next(range_iterator))  # 1
print(next(range_iterator))  # 2
# print(next(range_iterator))  # StopIteration
```

### Сравнение с циклом for
```python
# Эквивалентные конструкции:
for i in range(3):
    print(i)

# и
range_iter = iter(range(3))
while True:
    try:
        i = next(range_iter)
        print(i)
    except StopIteration:
        break
```



## Практические примеры

### Обработка данных с индексами
```python
data = ['Alice', 'Bob', 'Charlie']
processed = []
for i, name in enumerate(data, 1):
    processed.append(f"{i}. {name.upper()}")
print(processed)  # ['1. ALICE', '2. BOB', '3. CHARLIE']
```



### Генератор с enumerate
```python
matrix = [[1, 2], [3, 4]]
flat_with_indices = [(i, val) for i, row in enumerate(matrix) for val in row]
print(flat_with_indices)  # [(0, 1), (0, 2), (1, 3), (1, 4)]
```

## Вопросы для собеседования

1. **Чем отличается итерируемый объект от итератора?**
   - Итерируемый можно перебирать, итератор возвращает элементы
   - Итератор - одноразовый, итерируемый может использоваться многократно

2. **Как работает цикл for внутри?**
   - Создает итератор через iter()
   - Вызывает next() до StopIteration

3. **Что такое StopIteration?**
   - Исключение, сигнализирующее о конце последовательности

4. **Можно ли resetить итератор?**
   - Нет, нужно создать новый через iter()

5. **Зачем нужен параметр start в enumerate()?**
   - Для указания начального значения индекса

6. **Какие объекты являются итерируемыми?**
   - Списки, строки, словари, множества, range, файлы

7. **Как создать бесконечный итератор?**
   - Через itertools.count() или собственный класс без StopIteration

8. **Чем полезен enumerate()?**
   - Получение индекса и элемента одновременно
   - Упрощение кода с индексами

9. **Как обработать несколько итераторов одновременно?**
   - Через zip() или itertools.zip_longest()

10. **Когда использовать iter()/next() вместо for?**
    - Для ручного контроля итерации
    - При работе с потоками данных
    - В низкоуровневых операциях