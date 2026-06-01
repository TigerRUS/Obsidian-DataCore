Как упростить дебаг через `std::format` и `std::source_location`  
  
Когда вы отлаживаете сложный баг, бывает сложно быстро понять, где и почему произошла ошибка. С C++20 стало гораздо проще автоматизировать логирование и сделать его по-настоящему информативным.  

```c++
#include <iostream>
#include <format>
#include <source_location>

void log(const std::string& message,
const std::source_location location = std::source_location::current())
{
std::cout « std::format("[{}:{} - {}] {}\n",
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

[main.cpp:16 - divide] Попытка деления на ноль
```

Вы больше не пишете руками `__FILE__`, `__LINE__` и `__func__`. Всё это делает `std::source_location`. А с `std::format` — красиво и читаемо.

