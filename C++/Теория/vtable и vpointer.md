---
metatable: false
title: vtable и vpointer
tags:
dateCreated: 22-го августа 2022
dateModified: 22-го августа 2022
---
# vtable и vpointer

vtable — это механизм, который используется для поддержки динамического полифорфизма в C++. Эта таблица содержит в себе указатели на конкретные реализации методов у потомков.

Любой класс, который использует виртуальные функции имеет свою собственную виртуальную таблицу.

vpointer — это указатель на vtable, который создаётся сразу же при создании экземпляра класса. Этот указатель увеличивает размер класса на размер этого самого указателя. Размер vpointer-а увеличивает размер класса на размер `void*`.

Пример использования механизма виртуальной таблицы:

```cpp
#include <iostream>
#include <memory>

struct A {
	virtual void f() {
		std::cout << "A" << std::endl;
	}
};

struct B : public A {
	void f() override {
		std::cout << "B" << std::endl;
	}
};

int main(const int argc, char** argv) {
	std::unique_ptr<A> a = std::make_unique<B>();
	a->f(); // выведет B

	return EXIT_SUCCESS;
}
```