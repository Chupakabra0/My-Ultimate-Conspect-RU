---
metatable: false
title: Ссылка vs. указатель
tags:
dateCreated: 10-го августа 2022
dateModified: 10-го августа 2022
---
# Ссылка vs. указатель

Фактически в C++ являются своего рода ссылочными типами с некоторым количеством принципиальных отличий:

- ссылка не может быть инициализирована, указатель же может указывать "в никуда", то есть в `nullptr`.
- ссылка не может быть изменена после инициализации, то есть нельзя заставить переменную-ссылку ссылаться на другой объект.
- нельзя объявить массив ссылок, равно как и использовать ссылку в качестве параметризации STL контейнеров.
- не существует "арифметика ссылок", зато существует "арифметика указателей".
- ссылки не обладают квалификатором `const`,  так как в этом нет необходимости.
* в ссылку нельзя выделить память из кучи при помощи оператора `new` и освободить её с помощью `delete`.