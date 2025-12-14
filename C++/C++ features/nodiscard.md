В C++17 завезли `nodiscard`.
Когда функция возвращает `bool`, часто возникает соблазн проигнорировать результат:

```c++
is_valid(user); // ничего не делает!
```

А теперь представьте, что `is_valid()` проверяет критическое условие. Без проверки — баг, возможно даже security-уязвимость.

Чтобы защититься от такого, с C++17 есть nodiscard:
```c++
[[nodiscard]] bool is_valid(const User& user);
```

Теперь, если результат проигнорировать — компилятор предупредит:
*warning: ignoring return value of 'is_valid', declared with attribute 'nodiscard'*

```c++
[[nodiscard]] int compute() {
    return 42;
}

int main() {
    compute(); // warning: ignoring return value
}
```

Компилятор предупреждает: "эй, ты вызвал, но не используешь результат".
Где это особенно важно:
- Функции, которые возвращают ошибки (`std::error_code`, `std::optional, bool` успеха операции);
- Функции, где пропуск результата ломает логику (например, [[RAII]]-объекты, токены отмены, хендлы).

Можно навесить `nodiscard` и на типы (C++20):
```c++
struct [[nodiscard]] Result {
    bool ok;
};

Result foo();
foo(); // warning!
```

Можно ещё улучшить читаемость — использовать `nodiscard("Must check if user is valid")`, чтобы компилятор написал пояснение в варнинге (начиная с C++20).

Лайфхак: ставьте `nodiscard` на все функции, где игнорирование результата — это почти всегда ошибка. Особенно на:
* проверки (is_...)
* операции с возможным фейлом (try_..., parse_...)
* [[RAII]]-объекты с флагами состояния

Зачем `nodiscard` нужен не только для возврата значения
Если ты думаешь, что `nodiscard` — это просто защита от игнора *Result*, то вот фокус: его можно вешать и на классы, и на функции, и даже на enum — и это реально помогает избежать багов.

```c++
struct [[nodiscard]] Error {
    std::string message;
};

Error do_something() {
    return {"Что-то пошло не так"};
}

void foo() {
    do_something(); // warning: ignoring return value of nodiscard type
}
```

```c++
struct Connection {
    [[nodiscard]] bool is_valid() const {
        return valid_;
    }

private:
    bool valid_ = false;
};

void check_connection(const Connection& conn) {
    conn.is_valid(); // warning: result of 'is_valid' is unused
}
```

Даже если функция возвращает `bool` — компилятор предупредит, если ты его проигнорируешь.

`nodiscard` не бросает исключения и не делает функцию безопасной

