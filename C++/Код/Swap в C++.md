---
metatable: false
title: Swap в C++
tags:
dateCreated: 2-го августа 2022
dateModified: 10-го августа 2022
---
# Swap в C++

Существуют несколько способов написать функцию `swap`.  В реализациях будут использоваться типы-ссылки, а не указатели.

* При помощи использования временной переменной:
  
```cpp
template<class T1, class T2>
void swap(T1& a, T2& b) {
	const auto c = a;
	a = b;
	b = c; 
}
```

* При помощи использования сложения и вычитания:
  
```cpp
template<class T1, class T2>
void swap(T1& a, T2& b) {
    a = a + b;
    b = a - b;
    a = a - b;
}
```

* При помощи использования исключающего "или" (XOR):
  
```cpp
template<class T1, class T2>
void swap(T1& a, T2& b) {
    a ^= b;
    b ^= a;
    a ^= b;
}
```

* При помощи возвращения пар значений:
  
```cpp
template<class T1, class T2>
std::pair<T1, T2> swap(const T1& a, const T2& b) {
    return std::make_pair(b, a);
}
```