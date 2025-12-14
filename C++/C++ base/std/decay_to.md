```c++
#include <type_traits>
#include <iostream>

int main() {
    // const int& -> int
    static_assert(std::is_same_v<std::decay_t<const int&>, int>);
    
    // int[10] -> int*
    static_assert(std::is_same_v<std::decay_t<int[10]>, int*>);
    
    // void(int) -> void(*)(int)
    static_assert(std::is_same_v<std::decay_t<void(int)>, void(*)(int)>);
    
    std::cout << "All assertions passed!" << std::endl;
}
```

`std::decay_t` — один из самых полезных *type traits* в C++. Он имитирует процесс передачи параметра по значению, «разрушая» исходный тип.

*Что именно делает decay_t?*
• Убирает cv-квалификаторы
• Превращает ссылки в соответствующие типы без ссылок
• Преобразует массивы в указатели
• Преобразует функции в указатели на функции

*Где это используется?*
• В шаблонном программировании для упрощения работы с типами
• В `std::make_shared` и `std::make_unique` для определения типа создаваемого объекта
• При написании обобщенного кода, где нужна правильная дедукция типов

название *«decay» («разрушение»)* действительно отражает суть — тип «разрушается» до базового представления!
