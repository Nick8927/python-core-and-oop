# Циклы в Python: for и while

## Теоретическая основа для собеседования

### 1. Основные понятия
- **Цикл** - конструкция для многократного выполнения блока кода
- **Итерация** - одно повторение цикла
- **Итерируемый объект** - объект, по которому можно пройтись циклом (списки, строки, словари и т.д.)

### 2. Когда использовать циклы
- Для обработки коллекций данных
- При автоматизации повторяющихся задач
- Для реализации сложной логики с условиями
- При работе с последовательностями чисел

### 3. Сравнение циклов
| Характеристика | for | while |
|----------------|-----|-------|
| Когда использовать | Когда известно количество итераций | Когда условие выхода неизвестно заранее |
| Управление | По элементам последовательности | По условию |
| Риск бесконечного цикла | Нет | Да |

## 1. Цикл for

### Базовый синтаксис
```python
for элемент in последовательность:
    тело_цикла
```

### Примеры использования
```python
# Итерация по списку
fruits = ['apple', 'banana', 'cherry']
for fruit in fruits:
    print(fruit)

# Итерация по строке
for char in "Python":
    print(char)

# С range()
for i in range(3):       # 0, 1, 2
    print(i)

for i in range(1, 10, 2): # 1, 3, 5, 7, 9
    print(i)
```

## 2. Цикл while (полное руководство)

### Базовый синтаксис
```python
while условие:
    тело_цикла
```

### Полные примеры
```python
# Простой счетчик
count = 0
while count < 5:
    print(count)
    count += 1

# Обработка ввода
while True:
    user_input = input("Введите 'quit' для выхода: ")
    if user_input.lower() == 'quit':
        break
    print(f"Вы ввели: {user_input}")

# Работа с флагами
running = True
while running:
    command = input("Введите команду: ")
    if command == 'exit':
        running = False
    else:
        print(f"Выполняю: {command}")
```

### Особенности while
1. **Бесконечные циклы**:
```python
while True:
    # Будет выполняться вечно
    # Требуется break или return для выхода
```

2. **Else в while**:
```python
while condition:
    # основной блок
else:
    # выполняется, если цикл завершился без break
```

3. **Сложные условия**:
```python
while x < 10 and y > 0:
    # выполняется, пока оба условия True
```

## 3. Управление циклами

### Операторы управления
```python
# break - выход из цикла
for num in range(10):
    if num == 5:
        break
    print(num)  # 0 1 2 3 4

# continue - переход к следующей итерации
for num in range(5):
    if num == 2:
        continue
    print(num)  # 0 1 3 4

# pass - заглушка
for item in collection:
    pass  # TODO: реализовать позже
```

## 4. Вложенные циклы

### Примеры
```python
# Таблица умножения
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} * {j} = {i*j}")

# Поиск в матрице
matrix = [[1, 2], [3, 4]]
target = 3
found = False
for row in matrix:
    for num in row:
        if num == target:
            found = True
            break
    if found:
        break
```

## 5. Генераторы и циклы

### List comprehension
```python
squares = [x**2 for x in range(10)]
```

### Dict comprehension
```python
square_dict = {x: x**2 for x in range(5)}
```

## Практические примеры

### Обработка пользовательского ввода
```python
while True:
    age = input("Введите ваш возраст: ")
    if age.isdigit() and 0 < int(age) < 120:
        break
    print("Некорректный ввод!")
```

### Поиск простых чисел
```python
n = 100
primes = []
for num in range(2, n+1):
    is_prime = True
    for i in range(2, int(num**0.5)+1):
        if num % i == 0:
            is_prime = False
            break
    if is_prime:
        primes.append(num)
```

### Анализ текста
```python
text = "Python is an awesome programming language"
word_count = {}
for word in text.lower().split():
    if word in word_count:
        word_count[word] += 1
    else:
        word_count[word] = 1
```

## Вопросы для собеседования

1. **Чем отличается for от while?**
   - `for` итерируется по последовательности, `while` выполняется пока условие истинно

2. **Как избежать бесконечного цикла while?**
   - Гарантировать изменение условия в теле цикла
   - Использовать break с условием выхода

3. **Когда использовать break/continue?**
   - `break` - для досрочного выхода
   - `continue` - для пропуска итерации

4. **Как работает else в циклах?**
   - Выполняется, если цикл завершился без break

5. **Как перебрать словарь в цикле?**
   - По ключам: `for key in dict`
   - По парам: `for key, value in dict.items()`

6. **Как получить индекс в for?**
   - Через `enumerate()`: `for i, item in enumerate(items)`

7. **Как сделать обратный цикл?**
   - `for i in range(len(items)-1, -1, -1)`
   - Или `for item in reversed(items)`

8. **Как выйти из вложенных циклов?**
   - Использовать флаг или `return` в функции
   - Или `break` с меткой (в Python 3.10+)

9. **Как ускорить работу циклов?**
   - Использовать генераторы
   - Перенести логику в функции
   - Применять встроенные функции map/filter

10. **Когда использовать while True?**
    - Для обработки событий
    - Чтения потоков данных
    - Ожидания внешних условий