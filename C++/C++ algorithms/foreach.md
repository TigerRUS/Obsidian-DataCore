```c++
#include <string>
#include <iostream>

struct Student
{
	std::string name = "";
	int age = 0;
};

int main()
{
	std::string str = "gjklfkdlgkl";
	for (const auto& c : str) // Используем const и ссылку, чтобы избежать копирования
		std::cout << c;
	std::cout << std::endl;

	Student arr[]{ {"Ivan", 3}, {"John", 56} };
	for (const auto& c : arr)
		std::cout << c.name << " " << c.age << std::endl;

	return 0;
}
```
