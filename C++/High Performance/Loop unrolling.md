``` c++
void linear(const std::vector<uint32_t>& arr)
{
    uint32_t sum = 0;
    for (uint32_t i = 0; i < arr.size(); ++i)
    {
        sum += square(arr[i]);
    }
}

void unrolled4(const std::vector<uint32_t>& arr)
{
    uint32_t sum = 0;
    for (uint32_t i = 0; i < arr.size(); i+=4)
    {
        sum += square(arr[i]);
        sum += square(arr[i + 1]);
        sum += square(arr[i + 2]);
        sum += square(arr[i + 3]);
    }
}```

