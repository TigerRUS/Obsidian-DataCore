Реализация шаблонов с использованием *explicit instantiation* (явная инстанциация).

Все мы знаем, что шаблоны в C++ реализуются в заголовочных файлах. Это значит, что каждый .cpp файл, который включает такой заголовок, заново инстанцирует шаблон. Результат - долгое время компиляции и раздутый бинарник.

Разделяем интерфейс и реализацию:
```c++
// MyTemplate.hpp

#pragma once

template<typename T>
class MyTemplate {
public:
    void doSomething();
};
```

```c++
// MyTemplate.cpp

#include "MyTemplate.hpp"
#include <iostream>

template<typename T>
void MyTemplate<T>::doSomething() {
    std::cout << "Doing something\n";
}

// Явная инстанциация
template class MyTemplate<int>;
```

Теперь в клиентском коде:
```c++
#include "MyTemplate.hpp"

int main() {
    MyTemplate<int> obj;
    obj.doSomething();
}
```

- Сокращение времени компиляции
- Чище зависимости
- Потенциально меньший размер бинарника

*explicit instantiation работает, только если вы заранее знаете типы, с которыми будете использовать шаблон.*