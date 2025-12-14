В C++ "политика выполнения" (*execution policy*) относится к паралельным алгоритмам STL, позволяя указать, как выполнять операции (последовательно, параллельно или с векторизацией) с помощью `std::execution::seq`, `std::execution::par`, `std::execution::par_unseq`, что упрощает распараллеливание кода, например, в `std::for_each`, `std::transform`, `std::reduce` и др., значительно ускоряя их на многоядерных системах. 

```c++
#include <iostream>
#include <vector>
#include <numeric> // для std::accumulate (традиционный) и std::reduce
#include <execution> // для политик выполнения

int main() {
    std::vector<int> data(1000000, 1); // Большой вектор

    // 1. Традиционное последовательное суммирование (без политики)
    long long sum_seq = std::accumulate(data.begin(), data.end(), 0LL);
    std::cout << "Последовательная сумма: " << sum_seq << std::endl;

    // 2. Параллельное суммирование (с использованием std::reduce и политики)
    // std::reduce поддерживает политики выполнения
    long long sum_par = std::reduce(std::execution::par, data.begin(), data.end(), 0LL);
    std::cout << "Параллельная сумма: " << sum_par << std::endl;

    // 3. Последовательное суммирование (явно с политикой)
    long long sum_seq_policy = std::reduce(std::execution::seq, data.begin(), data.end(), 0LL);
    std::cout << "Последовательная сумма (с политикой): " << sum_seq_policy << std::endl;

    return 0;
}
```

- `std::execution::seq`: Последовательное выполнение (поведение по умолчанию для многих алгоритмов).
- `std::execution::par`: Параллельное выполнение (использует потоки для разделения работы).
- `std::execution::par_unseq`: Параллельное и векторизованное выполнение (использует [[SIMD]] инструкции и потоки).
- `std::execution::unseq`: Только векторизованное выполнение ([[SIMD]])