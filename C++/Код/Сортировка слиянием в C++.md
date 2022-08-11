---
metatable: false
title: Сортировка слиянием в C++
tags:
dateCreated: 5-го августа 2022
dateModified: 10-го августа 2022
---
# Сортировка слиянием в C++

Идея алгоритма полностью соответствует идеологии "разделяй и властвуй". Контейнер делится на две части, которые сортируются некоторым алгоритмом (в основном используют рекурсивный вызов этой же сортировки), а потом объединяются.

В реализации используется $O(n)$ дополнительной памяти.

```cpp
template<class Iter, class Pred = std::less<>>
void MergeSort(Iter begin, Iter end, Pred pred = std::less<>()) {
    const auto size = std::distance(begin, end);

    if (size < 2) {
        return;
    }

    if (size == 2) {
        auto prevEnd = std::prev(end);

        if (pred(*prevEnd, *begin)) {
            std::iter_swap(prevEnd, begin);
        }

        return;
    }

    std::vector<std::remove_cvref_t<decltype(*begin)>> temp(size); // C++ 20 stuff
    // std::vector<typename decltype(begin)::value_type> more old one but without C-arrays support
    
    std::copy(begin, end, temp.begin());

    auto [left, right] = std::make_pair(temp.begin(), std::next(temp.begin(), size / 2));
    auto [leftLimit, rightLimit] = std::make_pair(right, temp.end());

    MergeSort(left, right, pred);
    MergeSort(right, temp.end(), pred);

    for (; begin != end; begin = std::next(begin)) {
        // if left vector has copied
        if (left == leftLimit) {
            *begin = *right;
            right = std::next(right);
        }
        // if right vector has copied
        else if (right == rightLimit) {
            *begin = *left;
            left = std::next(left);
        }
        // if el from left fits better than el from right
        else if (pred(*left, *right)) {
            *begin = *left;
            left = std::next(left);
        }
        // else
        else {
            *begin = *right;
            right = std::next(right);
        }
    }
}
```