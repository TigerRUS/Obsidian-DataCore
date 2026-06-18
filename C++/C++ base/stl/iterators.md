1. **Input / Output итераторы (одноразовые)**
Это самые слабые итераторы. Их можно использовать *только один раз*
```c++
#include <iostream>
#include <iterator>  // для istream_iterator, ostream_iterator
#include <vector>
#include <algorithm>
int main() {
    // === Input итератор (читаем с клавиатуры) ===
    std::cout << "Введите 3 числа через пробел: ";
    std::istream_iterator<int> input_it(std::cin);  // начало ввода
    std::istream_iterator<int> end;                 // маркер конца (пустой)
    // Можно прочитать ТОЛЬКО ОДИН РАЗ
    int a = *input_it;  // взяли первое число
    ++input_it;         // перешли ко второму
    int b = *input_it;  // взяли второе
    ++input_it;
    int c = *input_it;  // взяли третье
    std::cout << "Вы ввели: " << a << ", " << b << ", " << c << std::endl;
    // === Output итератор (пишем в поток) ===
    std::vector<int> numbers = {10, 20, 30};
    
    std::ostream_iterator<int> output_it(std::cout, " ");  // разделитель — пробел
    
    // Пишем числа через output-итератор
    for (int x : numbers) {
        *output_it = x;  // записываем в cout
        ++output_it;     // переходим к следующей позиции
    }
    std::cout << std::endl;
    return 0;
}
```

2. **Forward итераторы (однонаправленные, многоразовые)**
Могут двигаться только вперед (`++`), но *можно проходить по диапазону несколько раз*.
```c++
#include <iostream>
#include <forward_list>  // односвязный список
int main() {
    std::forward_list<int> fl = {1, 2, 3, 4, 5};
    
    // Получаем forward-итератор
    auto it = fl.begin();
    
    // Можно пройти вперед
    ++it;  // теперь указывает на 2
    std::cout << "Второй элемент: " << *it << std::endl;
    
    // НЕЛЬЗЯ: --it (ошибка компиляции) — назад ходить нельзя
    
    // Можно проходить несколько раз (пересоздаем итератор)
    auto it2 = fl.begin();
    std::cout << "Первый проход: ";
    for (auto i = fl.begin(); i != fl.end(); ++i) std::cout << *i << " ";
    
    std::cout << "\nВторой проход: ";
    for (auto i = fl.begin(); i != fl.end(); ++i) std::cout << *i << " ";
    
    return 0;
}
```

3. **Bidirectional итераторы (двунаправленные)**
Умеют ходить и вперед (`++`), и назад (`--`). Поддерживаются у `list`, `set`, `map`.
```c++
#include <iostream>
#include <list>
int main() {
    std::list<int> lst = {10, 20, 30, 40, 50};
    
    auto it = lst.begin();   // указывает на 10
    ++it;                    // теперь на 20
    ++it;                    // теперь на 30
    std::cout << "Текущий: " << *it << std::endl;  // 30
    
    --it;                    // вернулись на 20
    std::cout << "Назад: " << *it << std::endl;    // 20
    
    // Можно ходить туда-сюда сколько угодно
    std::cout << "Идем в конец и обратно: ";
    for (auto i = lst.begin(); i != lst.end(); ++i) std::cout << *i << " ";
    std::cout << "\nОбратно: ";
    for (auto i = --lst.end(); i != lst.begin(); --i) std::cout << *i << " ";
    std::cout << *lst.begin() << std::endl;
    
    return 0;
}
```

4. **Random Access итераторы (произвольный доступ)**
Самые мощные. Поддерживают всё: `+`, `-`, `[]`, сравнения (`<`, `>`).
```c++
#include <iostream>
#include <vector>
int main() {
    std::vector<int> vec = {100, 200, 300, 400, 500};
    
    auto it = vec.begin();  // указывает на 100
    
    // Арифметика
    it = it + 3;            // прыгнули на 400
    std::cout << "vec[3] = " << *it << std::endl;
    
    // Индексация (как у указателя)
    std::cout << "it[1] = " << it[1] << std::endl;  // 500 (it[0] это 400, it[1] это 500)
    
    // Разность итераторов
    auto it2 = vec.end() - 1;  // указывает на 500
    std::cout << "Расстояние: " << (it2 - it) << std::endl;  // 1 (между 400 и 500)
    
    // Сравнения
    if (it < it2) {
        std::cout << "it идет раньше it2" << std::endl;
    }
    
    return 0;
}
```

5. **Специальные итераторы-адаптеры**
Они не указывают на существующие элементы, а *генерируют* или *вставляют* значения.

`back_insert_iterator` — вставка в конец
```c++
#include <iostream>
#include <vector>
#include <iterator>
#include <algorithm>
int main() {
    std::vector<int> v1 = {1, 2, 3};
    std::vector<int> v2 = {10, 20, 30};
    
    // Создаем итератор, который вызывает push_back()
    std::back_insert_iterator<std::vector<int>> back_it(v1);
    
    // Копируем v2 в конец v1 через back_insert_iterator
    std::copy(v2.begin(), v2.end(), back_it);
    
    // Теперь v1 = {1, 2, 3, 10, 20, 30}
    for (int x : v1) std::cout << x << " ";
    std::cout << std::endl;
    
    return 0;
}
```

`front_insert_iterator` — вставка в начало
```c++
#include <iostream>
#include <list>
#include <iterator>
#include <algorithm>
int main() {
    std::list<int> lst = {4, 5, 6};
    
    // Вставляем в начало списка
    std::front_insert_iterator<std::list<int>> front_it(lst);
    
    // Добавляем 1, 2, 3 в начало (обратите внимание — они вставятся в обратном порядке!)
    *front_it = 1;
    ++front_it;
    *front_it = 2;
    ++front_it;
    *front_it = 3;
    
    // lst = {3, 2, 1, 4, 5, 6} (потому что каждый раз вставляется в начало)
    for (int x : lst) std::cout << x << " ";
    
    return 0;
}
```

`istream_iterator` / `ostream_iterator` — работа с потоками
Универсальный пример: прочитать все числа из консоли в вектор:
```c++
#include <iostream>
#include <vector>
#include <iterator>
#include <algorithm>
int main() {
    std::cout << "Введите числа (Ctrl+Z / Ctrl+D для конца): ";
    
    // Читаем все числа с клавиатуры до конца файла
    std::istream_iterator<int> input_begin(std::cin);
    std::istream_iterator<int> input_end;
    
    std::vector<int> numbers(input_begin, input_end);  // конструктор сам прочитает всё!
    
    std::cout << "Вы ввели: ";
    std::copy(numbers.begin(), numbers.end(),
              std::ostream_iterator<int>(std::cout, " "));
    
    return 0;
}
```

`move_iterator` (C++11) — перемещение вместо копирования
```c++
#include <iostream>
#include <vector>
#include <iterator>
#include <string>
int main() {
    std::vector<std::string> src = {"apple", "banana", "cherry"};
    std::vector<std::string> dst;
    
    // Перемещаем элементы (не копируем!)
    std::move_iterator<std::vector<std::string>::iterator> move_begin(src.begin());
    std::move_iterator<std::vector<std::string>::iterator> move_end(src.end());
    
    dst.insert(dst.begin(), move_begin, move_end);
    
    // src теперь содержит пустые строки (элементы перемещены)
    std::cout << "src[0] теперь: '" << src[0] << "' (пусто)" << std::endl;
    std::cout << "dst[0]: " << dst[0] << std::endl;
    
    return 0;
}
```