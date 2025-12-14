```c++
uint32_t set_bit(uint32_t num, uint32_t index, bool value)
{
    if (value)
    {
        uint32_t mask = 1 << value; //000001000000
        return num | mask;
    }
    else
    {
        uint32_t mask = ~(1 << value); //11111101111111
        return num & mask;
    }
}