---
metatable: true
title: GCD в C++. Алгоритм Евклида.
tags:
dateCreated: 22-го августа 2022
dateModified: 22-го августа 2022
---

# GCD в C++. Алгоритм Евклида.

```cpp
#include <algorithm>

template<class T1, class T2>  
auto GCD(T1 a, T2 b) {  
    if (a == 0) {  
        return b;  
    }  
    if (b == 0) {  
        return a;  
    }  
  
    const auto [min, max] = std::minmax(a, b);  
  
    return GCD(max % min, min);  
}
```
