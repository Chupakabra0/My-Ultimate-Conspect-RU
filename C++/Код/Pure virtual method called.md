---
metatable: false
title: Pure virtual method called
tags:
dateCreated: 29-го августа 2022
dateModified: 29-го августа 2022
---
# Pure virtual method called

Код, позволяющий вызвать подобную ошибку такой:

```cpp
#include <iostream>
#include <memory>

class A {
public:
    explicit A() {
        this->H();
    }

    virtual int F(int a, int b) const = 0;

    void H() {
        this->F(1, 1);
    }

    ~A() {
        this->H();
    }
};

class B : public A {
public:
    explicit B() = default;

    int F(int a, int b) const override {
        return a * b;
    }
};

int main() {
    std::unique_ptr<A> a = std::make_unique<B>();
    return EXIT_SUCCESS;
}
```
