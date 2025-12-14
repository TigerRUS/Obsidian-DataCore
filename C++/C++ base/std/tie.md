```c++
#include <iostream>
#include <string>
#include <set>
#include <tuple>

struct S {
	int n = 0;
	std::string s = "";
	float d = 0.0;
	bool operator<(const S& rhs) const {
		return std::tie(n, s, d) < std::tie(rhs.n, rhs.s, rhs.d);
	}
};

int main() {
	std::set<S> set_of_s;
	S value{42, "Test", 3.14};
	
	std::set<S>::iterator iter;
	bool inserted = false;
	
	std::tie(iter, inserted) = set_of_s.insert(value);
	
	if (inserted)
		std::cout << "Value was inserted successfully\n";
}
```

`std::tie` — это функция, которая создает кортеж ссылок на `lvalue` из своих аргументов или экземпляров `std::ignore`.

Она может использоваться для распаковки кортежей или пары значений в отдельные переменные. Например, если у вас есть функция, которая возвращает `std::pair` или `std::tuple`, вы можете использовать `std::tie`, чтобы присвоить значения этого кортежа отдельным переменным.

В этом примере мы используем `std::tie` для распаковки результата вызова `set_of_s.insert(value)` в две переменные: итератор `iter` и логическую переменную `inserted`. 
Это позволяет нам проверить, было ли значение успешно вставлено в набор.