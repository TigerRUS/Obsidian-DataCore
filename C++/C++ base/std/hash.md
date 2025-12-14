предоставляет хеш-функцию для хэширования различных типов данных, включая встроенные и пользовательские.

`std::hash` используется, например, в ассоциативных контейнерах, таких как `std::unordered_map` и `std::unordered_set`, для быстрого доступа к элементам по ключу.

Для пользовательского типа данных требуется явная специализация структуры `std::hash` для корректной работы хэширования.

```c++
#include <iostream>
#include <functional>
#include <string>

struct Person {
	std::string name;
	int age;
	
	// Операторы сравнения для использования в ассоциативных контейнерах
	bool operator==(const Person& other) const {
		return name == other.name && age == other.age;
	}
	
	bool operator!=(const Person& other) const {
		return (*this == other);
	}
};

// Специализация структуры std::hash для типа Person namespace std {
template<>
	struct hash<Person> {
		std::size_t operator() (const Person& p) const {
			// Комбинируем хеши полей имени и возраста
			std::size_t nameHash = std::hash<std::string>{}(p.name);
			std::size_t ageHash = std::hash<int>{}(p.age);
			return nameHash ageHash;
		}
	};
}

int main() {
	Person person{ "John Doe", 25};
	
	std::hash<Person> personHasher; // Cоздам зкзмпляр xеш-функции для типа Рerson
	std::size_t hashValue = personHasher (person); // Вычисляем хеш-значение
	
	std::cout << "Hash value: " << hashValue << std::endl;
	
	return 0;
}
```