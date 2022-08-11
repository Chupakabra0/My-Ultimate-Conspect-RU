---
metatable: false
title: Сортировка выбором в C++
tags:
dateCreated: 5-го августа 2022
dateModified: 10-го августа 2022
---
# Сортировка выбором в C++

Идея сортировки, пожалуй, самая простая: находиться оптимум (минимум/максимум) и меняется местами с первым элементом. Интервал сортировки сужается, а алгоритм повторяется.

```cpp
template<class Iter, class Pred = std::less<>>
void SelectionSort(Iter begin, Iter end, Pred pred = std::less<>()) {
    const auto size = std::distance(begin, end);

    if (size < 2) {
        return;
    }

    for (auto iter = begin; iter != std::prev(end); iter = std::next(iter)) {
        auto optimum = iter;
        
        for (auto jter = std::next(iter); jter != end; jter = std::next(jter)) {
            if (pred(*jter, *optimum)) {
                optimum = jter;
            }
        }

        std::iter_swap(iter, optimum);
    }
}
```
