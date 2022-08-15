---
metatable: true
title: Факториал числа в C++
tags:
dateCreated: 15-го августа 2022
dateModified: 15-го августа 2022
---
# Факториал числа в C++

- С использованием рекурсии:

```cpp
template<class T>  
T Factorial(T n) {  
    return n < 1 ? 1 : Factorial(n - 1) * n;  
}
```

-  С использованием цикла:

```cpp
template<class T>  
T Factorial(T n) {  
    auto result = T{1};  
  
    for (auto i = n; i > 1; --i) {  
        result *= i;  
    }  
  
    return result;  
}
```

- Метод метапрограммирования (работает только с постоянными компиляции):

```cpp
template<long long N>  
struct Fact {  
    static constexpr auto value = Fact<N - 1>::value * N;  
};  
  
template<>  
struct Fact<0> {  
    static constexpr auto value = 1ll;  
};  
  
template<>  
struct Fact<1> {  
    static constexpr auto value = Fact<0>::value;  
};
```

- С использованием гамма-функции $\Gamma(n)$:

```cpp
#include <cmath>

template<class T>  
T Factorial(T n) {  
    return std::tgamma(n + 1);
}
```