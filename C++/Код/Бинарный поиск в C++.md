---
metatable: false
title: Бинарный поиск в C++
tags:
dateCreated: 5-го августа 2022
dateModified: 10-го августа 2022
---
# Бинарный поиск в C++

```cpp
template<class Iter, class Val, class Pred = std::less<>>
Iter BinarySearch(Iter begin, Iter end, Val val, Pred pred = std::less<>()) {
    std::function<Iter(Iter, Iter, Val, Pred)> body
        = [&body, &end](auto b, auto e, auto v, auto p) {
        const auto size = std::distance(b, e);

        if (size == 0) {
            return end;
        }

        auto middle = std::next(b, size / 2);

        if (v == *middle) {
            return middle;
        }
        
        return p(v, *middle)
	        ? body(b, middle, v, p)
	        : body(std::next(middle), e, v, p);
    };

    return body(begin, end, val, pred);
}
```
