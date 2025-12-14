Если ваш код активно использует `std::string`, но вам нужно просто просматривать данные без ненужных аллокаций и копирований, то `std::string_view` — это то, что нужно!

Пример проблемы:  
```c++
std::string extract_extension(const std::string& filename) {  
	size_t pos = filename.rfind('.');  
	if (pos == std::string::npos) return "";  
	return filename.substr(pos);  
}
```
Казалось бы, код работает, но есть нюанс: `substr(pos)` создаёт новую строку, что лишний раз тратит память.

Оптимизированный вариант:  
```c++
std::string_view extract_extension(std::string_view filename) {  
	size_t pos = filename.rfind('.');  
	if (pos == std::string_view::npos) return {};  
	return filename.substr(pos);  
}
```

Здесь `std::string_view` просто создаёт представление на часть строки без копирования данных.