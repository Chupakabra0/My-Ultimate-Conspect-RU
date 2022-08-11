---
metatable: false
title: Ключевое слово mutable
tags:
dateCreated: 10-го августа 2022
dateModified: 10-го августа 2022
---
# Ключевое слово mutable

`mutable` — ключевое слово, которое добавляет возможность меняться чему-либо даже в условиях константного контекста.

## Мутабельные члены-классов

Если объект гарантирует неизменность своего состояния (например, через вызов константного метода), то "мутабельный" член класса всё равно может быть изменён.

Может быть полезным для обеспечения потокобезопасности через мутабельный `mutex`:

```cpp
class A {
public:
	explicit A(int var) : var(var) {
	
	}

	void Method() const {
		std::scoped_lock l(this->mutex); // this->mutex changes itself state
		// some kind of calculations...
	}

private:
	mutable std::mutext mutex;
	int var;
}
```

##  Мутабельные лямбда-выражения

Обычно оператор вызова функции замыкания является константным. Другими словами — лямбда не может модифицировать переменные, захваченные по значению.

Но ключевое слово `mutable` может быть применено ко всей лямбда-функции, что сделает все её переменные изменяемыми:

```cpp
#include <iostream>  
  
int main() {  
    auto x = 2;  
    auto func = [x, y = 22]() mutable {  
        std::cout << "x = " << x++ << std::endl << "y = " << y++ << std::endl << std::endl;  
    };  
  
    for (auto i = 0; i < 10; ++i) {  
        func();  
    }  
  
    return EXIT_SUCCESS;  
}
```
