как избавиться от болей с `#include`  в больших C++ проектах.
Когда проект растёт, количество инклудов становится пугающим. Компиляция тормозит, зависимости запутаны, порядок подключения начинает влиять на поведение программы.

Решение — **Precompiled Headers (PCH)**.

1. Создаём файл pch.h, в котором собираем самые часто используемые инклюды:
```c++
// pch.h  
[#pragma](https://vk.com/feed?q=%23pragma&section=search) once  
[#include](https://vk.com/feed?q=%23include&section=search) <iostream>  
[#include](https://vk.com/feed?q=%23include&section=search) <vector>  
[#include](https://vk.com/feed?q=%23include&section=search) <map>  
// и т.д.  
```

2. Добавляем его в компиляцию с флагом:
`g++ -x c++-header pch.h -o pch.h.gch` 

3. Теперь любой другой файл, который первым инклудит pch.h, компилируется быстрее.

Cовременные системы сборки, вроде CMake, умеют работать с PCH почти автоматически. Достаточно указать: `target_precompile_headers(my_target PRIVATE pch.h)`
Главное, чтобы в pch.h не попадали редко используемые или изменяющиеся файлы — иначе получите обратный эффект.