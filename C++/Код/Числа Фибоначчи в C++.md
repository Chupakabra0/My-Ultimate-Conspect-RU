---
metatable: false
title: Числа Фибоначчи в C++
tags:
dateCreated: 15-го августа 2022
dateModified: 15-го августа 2022
---
# Числа Фибоначчи в C++

Рекуррентная формула последовательности:

$$
F_{n} = \begin{cases}
n, & n < 2 \\
F_{n - 1} + F_{n - 2}, & \text{else}
\end{cases}
$$

Реализации:

- С использованием рекурсии:

```cpp
template<class T>  
T Fibonacci(T n) {  
    return n < 2 ? n : Fibonacci(n - 2) + Fibonacci(n - 1);  
}
```

- С использованием цикла:

```cpp
template<class T>  
T Fibonacci(T n) {  
    if (n < 2) {  
        return n;  
    }  
  
    auto result = T{0};  
    auto [temp1, temp2] = std::make_pair(T{1}, T{0});  
  
    for (auto i = 1; i < n; ++i) {  
        result = temp1 + temp2;  
        temp2  = temp1;  
        temp1  = result;  
    }  
  
    return result;  
}
```

- Метод метапрограммирования (работает только с постоянными компиляции):

```cpp
template<unsigned long long N>  
struct Fibo {  
    static constexpr auto value = Fibo<N - 2ull>::value + Fibo<N - 1ull>::value;  
};  
  
template<>  
struct Fibo<0ull> {  
    static constexpr auto value = 0ull;  
};  
  
template<>  
struct Fibo<1ull> {  
    static constexpr auto value = 1ull;  
};
```

- [Формула Бине](https://ru.wikipedia.org/wiki/%D0%A7%D0%B8%D1%81%D0%BB%D0%B0_%D0%A4%D0%B8%D0%B1%D0%BE%D0%BD%D0%B0%D1%87%D1%87%D0%B8#%D0%A4%D0%BE%D1%80%D0%BC%D1%83%D0%BB%D0%B0_%D0%91%D0%B8%D0%BD%D0%B5) (может давать погрешность)

```cpp
template<class T>  
T Fibonacci(T n) {  
    auto [phiPlus, phiMinus] = std::make_pair((1.0 + sqrt(5.0)) / 2.0, (1.0 - sqrt(5.0) / 2.0));  
  
    return static_cast<T>((pow(phiPlus, n) - pow(phiMinus, n)) / sqrt(5.0));  
}
```