---
metatable: false
title: Линейный поиск в C++
tags:
dateCreated: 5-го августа 2022
dateModified: 10-го августа 2022
---
# Линейный поиск в C++

```cpp
template<class Iter, class Val>
Iter LinearSearch(Iter begin, Iter end, Val val) {
    for (; begin != end; begin = std::next(begin)) {
        if (val == *begin) {
            break;
        }
    }

    return begin;
}
```