---
metatable: false
title: RVO
tags:
dateCreated: 22-го августа 2022
dateModified: 22-го августа 2022
---
# RVO

RVO (Return Value Optimization) — это одна из оптимизаций компилятора, которая позволяет избежать лишнего копирования объектов, которые возвращаются из функции.

Причина появления RVO довольно очевидна, взглянем на следующий код:

```cpp
#include <iostream>

struct A {
	explicit A() {
		std::cout << "default ctor" << std::endl;
	}

	A(const A&) {
		std::cout << "copy ctor" << std::endl;
	}

	A(A&&) noexcept {
		std::cout << "move ctor" << std::endl;
	}

	~A() noexcept {
		std::cout << "dtor" << std::endl;
	}

	static A CreateA() {
        return A{};
    }
};

	
int main() {
	auto a = A::CreateA(); 
    return EXIT_SUCCESS;
}
```

Без RVO с C++11 (с C++17 отключить RVO нельзя) в консоль будут выведены такие сообщения:

```
default ctor
move ctor
dtor
move ctor
dtor
dtor
```

Эти строки свидетельствуют о вызовах:

1. Конструктора по умолчанию в методе `CreateA()`.
2. Перемещения в временную переменную, чтобы сохранить значение, которое вернулось из метода `CreateA()`.
3. Деструктора для объекта `A` в контексте метода `CreateA()`.
4. Перемещения из временной переменной в переменную `a` в функции `main()`.
5. Деструктора у временной переменной.
6. Деструктора у переменной `a`.

При наличии RVO имеем такой вывод:

```
default ctor
dtor
```

Объект класса единственный раз был создан внутри метода `CreateA()` и был единственный раз уничтожен после возвращения `EXIT_SUCCESS` из функции `main()`.

О тонкостях RVO можно почитать [тут](https://shaharmike.com/cpp/rvo/).