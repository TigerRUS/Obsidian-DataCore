Как упростить дебаг через `std::format` и `std::source_location`

Когда вы отлаживаете сложный баг, бывает сложно быстро понять, где и почему произошла ошибка.

```c++

#include <iostream>
#include <format>
#include <source_location>

void log(const std::string& message,
         const std::source_location location = std::source_location::current())
{
    std::cout << std::format("[{}:{} - {}] {}\n",
                             location.file_name(),
                             location.line(),
                             location.function_name(),
                             message);
}

int divide(int a, int b)
{
    if (b == 0) {
        log("Попытка деления на ноль");
        return 0;
    }
    return a / b;
}
```

```cpp
output:
[main.cpp:16 - divide] Попытка деления на ноль
```