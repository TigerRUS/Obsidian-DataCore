Оператор == для проверки точного совпадение строк:
```c++
std::string str1 = "hello";
std::string str2 = "hello";

if (str1 == str2) {
    std::cout << "Строки равны!\n";
}
```

Функция `compare()`
Если нужно получить порядок строк в алфавитном сравнении:
```c++
std::string str1 = "apple";
std::string str2 = "banana";

if (str1.compare(str2) < 0) {
    std::cout << "apple идет перед banana\n";
}
```
`compare()` возвращает:  
- 0, если строки равны  
- < 0, если str1 меньше str2  
- > 0, если str1 больше str2  

*Сравнение без учета регистра*
В C++ нет встроенного метода, но можно использовать `std::transfore`:
```c++
#include <algorithm>
#include <cctype>
#include <string>

bool caseInsensitiveCompare(const std::string& a, const std::string& b) {
    return std::equal(a.begin(), a.end(), b.begin(), b.end(),
                      [](char c1, char c2) { return std::tolower(c1) == std::tolower(c2); });
}

std::string str1 = "Hello";
std::string str2 = "hello";

if (caseInsensitiveCompare(str1, str2)) {
    std::cout << "Строки равны без учета регистра!\n";
}
```

*Сравнение подстрок*
Если нужно проверить, начинается ли строка с подстроки:
```c++
std::string text = "hello world";
std::string prefix = "hello";

if (text.rfind(prefix, 0) == 0) {
    std::cout << "Строка начинается с 'hello'!\n";
}
```

`rfind(prefix, 0) == 0` проверяет, что `prefix` стоит в начале строки.

- == для простого сравнения
- `compare()` – если важно узнать порядок
- `std::tolower()` - сравнение без учёта регистра
- `rfind()` - сравнение с подстрокой