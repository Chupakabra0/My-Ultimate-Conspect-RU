---
metatable: false
title: PIMPL
tags:
dateCreated: 24-го августа 2022
dateModified: 24-го августа 2022
---
# PIMPL

PIMPL (Pointer to IMPLementation) — это идиома, смысл которой заключается в создании указателя на конкретную реализацию класса/функции для более глубокого уровня инкапсуляции: сокрытия не только реализации, но и её зависимостей. Крайне полезна при создании кроссплатформенных приложений.

Пример:

```cpp
class widget {
    // public members
private:
    struct impl; // forward declaration
    std::unique_ptr<impl> pImpl;
};

struct widget::impl { // widget.cpp (implementation)
   // implementation details
};
```