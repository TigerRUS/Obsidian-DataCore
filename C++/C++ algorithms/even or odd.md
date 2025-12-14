```cpp
#include <iostream>
#include <cmath>
#include <array>

int main()
{
	int result{};

	int a = 10;
	int b = 7;

	srand(time(NULL));

	for (;;)
	{
		int value = rand() % 42;
		result = (value % 2 == 0) + 1;
	}
	
	for (;;)
	{
		int value = rand() % 42;
		bool cond = (value % 2 == 0);
		result = cond * a + (!cond) * b;
	}

	std::array<bool, 2> arr = { 0, 1 };

	for (;;)
	{
		int value = rand() % 42;
		result = arr[value % 2 == 0];
	}

	return 0;
}
```