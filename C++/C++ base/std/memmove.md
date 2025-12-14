Функция memmove используется для копирования блока памяти из одного места в другое. Она объявлена в заголовочном файле `<cstring>`
Она принимает аргументы типа `void*` и `const void*` , что позволяет ей работать с любыми типами данных. Она просто копирует указанное количество байтов из исходного буфера в целевой.

`memmove` может обрабатывать перекрывающиеся буферы. В отличие от `memcpy`, которая просто копирует данные из одного места в другое, `memmove` может безопасно перемещать данные, даже если исходный и целевой буферы перекрываются.

Функция `memmove` может быть полезна для удаления элементов из массива. Например, если вы хотите удалить элемент из массива и сдвинуть оставшиеся элементы влево, вы можете использовать memmove для перемещения данных в массиве.

```c++
#include <iostream>
#include <cstring>
int main() {
	char str[] = "1234567890";
	std::cout << str << '\n';
	std::memmove(str + 4, str + 3, 3); // копирует из [4, 5, 6] в [5, 6, 7]
	std::cout << str << '\n';
}
```

The function is declared in the `<cstring>` header file (or `<string.h>` in C). 
```c++
#include <cstring>

void* std::memmove(void* dest, const void* src, std::size_t count);
```

- `dest`: A pointer to the destination memory block.
- `src`: A pointer to the source memory block.
- `count`: The number of bytes to be copied.
- **Return Value**: Returns a pointer to the destination (`dest`)