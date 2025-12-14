```cpp
#include <iostream>
#include <algorithm>

int main()
{
    std::string line = "1234567";

    for (auto start = line.begin(), end = line.end() - 1; start < end; start++, end--)
    {
        std::iter_swap(start, end);
    }

    std::cout << line << std::endl;
}
```

