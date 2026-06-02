как элегантно управлять временем жизни ресурса с помощью `std::unique_ptr` и кастомного deleter'а. 
  
**Задача**: у нас есть не-C++ ресурс, например, `FILE*` из `stdio.h`. Мы хотим, чтобы он автоматически закрывался, как только выходит из области видимости.  
  
Вместо ручного вызова `fclose`, используем `std::unique_ptr` с кастомным deleter'ом:  

```c++
#include <memory>
#include <cstdio>

int main() {
    // Кастомный deleter для FILE*
    auto fileDeleter = [](FILE* f) {
        if (f) {
            std::puts("Файл закрывается автоматически!");
            std::fclose(f);
        }
    };

    // Умный указатель с кастомным deleter'ом
    std::unique_ptr<FILE, decltype(fileDeleter)> file(std::fopen("data.txt", "r"), fileDeleter);

    if (!file) {
        std::perror("Не удалось открыть файл");
        return 1;
    }

    // Файл будет автоматически закрыт в конце блока main()
}
```

Такой подход безопаснее, чем `fopen/fclose`, особенно в реальных проектах с множеством return'ов и исключениями. А главное — код остаётся чистым и идиоматичным.