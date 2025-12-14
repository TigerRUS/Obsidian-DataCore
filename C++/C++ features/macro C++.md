Проблема: `#define` — это зло.  
Они не уважают область видимости, не отлаживаются нормально, не подчиняются типам и могут вызвать кучу проблем, особенно в больших проектах.

Вместо `#define PI 3.14`  
Используем:  `constexpr double PI = 3.14;`

Вместо `#define SQUARE(x) ((x)*(x))`  
Используем шаблон:
```c++
template<typename T>
constexpr T square(T x) {
	return x * x;
}
```

Вместо `#ifdef DEBUG ... #endif` 
Используем:
```c++
#ifdef DEBUG
inline constexpr bool is_debug = true;
#else
inline constexpr bool is_debug = false;
#endif

...

if constexpr (is_debug) {
    std::cout << "Debug mode\n";
}
```





