Удобный способ работы с перечислениями в C++ — приведение enum к строке и обратно.

Во многих проектах используется enum, чтобы задать ограниченный набор значений. Но как вывести значение enum в лог? Или, наоборот, прочитать из строки и получить нужное значение enum?

C++ сам по себе не умеет конвертировать enum в строку и обратно. Вот простая реализация этого функционала через std::unordered_map:

```c++
enum class LogLevel {
    Debug,
    Info,
    Warning,
    Error
};

const std::unordered_map<LogLevel, std::string> LogLevelToString = {
    {LogLevel::Debug, "Debug"},
    {LogLevel::Info, "Info"},
    {LogLevel::Warning, "Warning"},
    {LogLevel::Error, "Error"},
};

const std::unordered_map<std::string, LogLevel> StringToLogLevel = {
    {"Debug", LogLevel::Debug},
    {"Info", LogLevel::Info},
    {"Warning", LogLevel::Warning},
    {"Error", LogLevel::Error},
};

std::string to_string(LogLevel level) {
    return LogLevelToString.at(level);
}

LogLevel to_log_level(const std::string& str) {
    return StringToLogLevel.at(str);
}
```

Такой подход хорошо работает, если enum не слишком большой. Если значений много — можно автоматизировать генерацию через макросы или использовать библиотеки вроде magic_enum.