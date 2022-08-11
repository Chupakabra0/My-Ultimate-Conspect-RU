---
metatable: false
title: Быстрая сортировка в C++
tags:
dateCreated: 5-го августа 2022
dateModified: 10-го августа 2022
---
# Быстрая сортировка в C++

Всего существует несколько разновидностей быстрой сортировки. Отличаются они прежде всего стратегией выбора опорного элемента.

Принято выбирать:
* последний;
* первый;
* средний;
* произвольный.

Быстрая сортировка с последним опорным элементом **(рекомендую)**:

```cpp
template<class Iter, class Pred>
void QuickRightSort(Iter begin, Iter end, Pred pred) {
    const auto size = std::distance(begin, end);

    if (size < 2) {
        return;
    }

    auto [control, pivot] = std::make_pair(begin, std::prev(end));

    for (auto iter = begin; iter != std::prev(end); iter = std::next(iter)) {
        if (pred(*iter, *pivot)) {
            std::iter_swap(iter, control);
            control = std::next(control);
        }
    }

    std::iter_swap(control, pivot);

    QuickRightSort(begin, control, pred);
    QuickRightSort(std::next(control), end, pred);
}
```

 Быстрая сортировка с первым опорным элементом:

```cpp
template<class Iter, class Pred>
void QuickLeftSort(Iter begin, Iter end, Pred pred) {
    const auto size = std::distance(begin, end);

    if (size < 2) {
        return;
    }

    auto [control, pivot] = std::make_pair(begin, begin);

    for (auto iter = std::next(begin); iter != end; iter = std::next(iter)) {
        if (pred(*iter, *pivot)) {
            std::iter_swap(iter, std::next(control));
            control = std::next(control);
        }
    }

    std::iter_swap(control, pivot);

    QuickLeftSort(begin, control, pred);
    QuickLeftSort(std::next(control), end, pred);
}
```

Быстрая сортировка с опорным элементом посередине:

```cpp
template<class Iter, class Pred>
void QuickMiddleSort(Iter begin, Iter end, Pred pred) {
    const auto size = std::distance(begin, end);

     if (size < 2) {
        return;
     }

    auto [iter, jter] = std::make_pair(begin, std::prev(end));
    auto pivotValue   = *std::next(begin, size / 2);

    while (std::distance(iter, jter) >= 0) {
        for (; pred(*iter, pivotValue); iter = std::next(iter));
        for (; pred(pivotValue, *jter); jter = std::prev(jter));

        if (std::distance(iter, jter) >= 0) {
            std::iter_swap(iter, jter);
            iter = std::next(iter);
            jter = std::prev(jter);
        }
    };

    if (std::distance(begin, jter) > 0) {
        QuickMiddleSort(begin, std::next(jter), pred);
    }
    if (std::distance(iter, end) > 0) {
        QuickMiddleSort(iter, end, pred);
    }
}
```