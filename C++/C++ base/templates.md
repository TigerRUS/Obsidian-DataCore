1. *CTAD (Class Template Argument Deduction, C++17)*
   Не надо вручную указывать аргументы:
```c++
std::pair p(42, 3.14); // вместо std::pair<int, double> p(42, 3.14);
std::vector v = {1,2,3}; // компилятор сам выведет std::vector<int>
```
   Помогает сократить код и избежать опечаток.

2. *Fold-выражения (C++17) для арг-паков:*
```c++
auto sum = [](auto... args){
   return (args + ...);  // ((a + b) + c) + ...
};
std::cout << sum(1,2,3,4); // 10
```
   Позволяют писать операции над любым числом параметров без рекурсии.

3. *SFINAE → Concepts (C++20)*
   Старый стиль через enable_if легко сломать:
```c++
template<class T>
std::enable_if_t<std::is_integral_v<T>, T>
foo(T x) { return x*2; }
```
   С Concepts чище и понятнее:
```c++
template<std::integral T>
T foo(T x) { return x*2; }
```

4. *CRTP (Static polymorphism) Быстрее виртуалок и без RTTI:*
```c++
template<class D>
struct Base {
   void interface() { static_cast<D*>(this)->impl(); }
};
struct Derived : Base<Derived> {
   void impl() { std::cout<<"OK\n"; }
};
```
