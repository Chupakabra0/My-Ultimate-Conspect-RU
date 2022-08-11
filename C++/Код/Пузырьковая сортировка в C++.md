---
metatable: false
title: Пузырьковая сортировка в C++
tags:
dateCreated: 3-го августа 2022
dateModified: 10-го августа 2022
---
# Пузырьковая сортировка в C++

```cpp
template<class Iter, class Pred = std::less<>>
void BubbleSort(Iter begin, Iter end, Pred pred = std::less<>()) {
    const auto size = std::distance(begin, end);

    if (size < 2) {
        return;
    }

    auto isSorted = false;
    
    while (!isSorted) {
        isSorted = true;

        for (auto it = std::next(begin); it != end; it = std::next(it)) {
            auto current  = it;
            auto previous = std::prev(it);

            if (pred(*current, *previous)) {
                std::iter_swap(current, previous);
                isSorted = false;
            }
        }
        end = std::prev(end); // необязательная оптимизация
    }
}
```