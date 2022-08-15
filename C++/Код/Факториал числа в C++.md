---
metatable: false
title: Факториал числа в C++
tags:
dateCreated: 15-го августа 2022
dateModified: 15-го августа 2022
---
# Факториал числа в C++

Рекуррентная формула последовательности:

$$
F_{n} = \begin{cases}
1, & n < 2 \\
n \cdot F_{n-1}, & \text{else}
\end{cases}
$$

Реализации:

- С использованием рекурсии:

```cpp
template<class T>  
T Factorial(T n) {  
    return n < 2 ? 1 : Factorial(n - 1) * n;  
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
template<unsigned long long N>  
struct Fact {  
    static constexpr auto value = Fact<N - 1>::value * N;  
};  
  
template<>  
struct Fact<0ull> {  
    static constexpr auto value = 1ull;  
};  
  
template<>  
struct Fact<1ull> {  
    static constexpr auto value = Fact<0ull>::value;  
};
```

- С использованием гамма-функции $\Gamma(n)$ (может давать погрешность):

```cpp
#include <cmath>

template<class T>  
T Factorial(T n) {  
    return std::tgamma(n + 1);
}
```