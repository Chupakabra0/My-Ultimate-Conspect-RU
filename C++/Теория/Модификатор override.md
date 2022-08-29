---
metatable: false
title: Модификатор override
tags:
dateCreated: 27-го августа 2022
dateModified: 27-го августа 2022
---
# Модификатор override

`override` — это ключевое слово, позволяющее компилятору проверять, переопределяет ли модифицируемый метод какой-либо из виртуальных родительских методов. Если метод не переопределяет виртуальную функцию родительского класса, то компилятор выдаст ошибку.

Это ключевое слово может помочь избежать ошибок, показанных в примере ниже:

```cpp
class A {
public:
    explicit A() = default;

    virtual int F(int a, int b) const {
        return a + b;
    }
};

class B : public A {
public:
    explicit B() = default;

    int Ff(int a, int b) const override { // ошибка, опечатка в названии метода
        return a * b;
    }
};

class C : public A {
public:
    explicit C() = default;

    int F(int a, int b) override { // ошибка, не сохранена константность
        return a - b;
    }
};

class D : public A {
public:
    explicit D() = default;

    int F(double a, double b) const override { // ошибка, другие типы аргументов
        return a / b;
    }
};
```

Использование модификатора `override` никак не влияет на эффективность или производительность программы, но помогает избежать непреднамеренных ошибок. Следовательно, настоятельно рекомендуется использовать модификатор override для каждого из своих переопределений.
