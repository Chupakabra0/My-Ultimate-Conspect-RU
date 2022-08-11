---
metatable: false
title: Замерить время выполнения в C++
tags:
dateCreated: 3-го августа 2022
dateModified: 10-го августа 2022
---
# Замерить время выполнения в C++

C++11 позволяет замерить время выполнения программы при помощи библиотеки `<chrono>`:

```cpp
#include <cstdlib>
#include <chrono>

int main(int argc, char** argv) {
	const auto begin = std::chrono::high_resolution_clock::now();
	
	// код, время работы которого нужно замерить
	
	const auto end = std::chrono::high_resolution_clock::now();
	
	const auto time = std::chrono::duration_cast<std::chrono::seconds>(end - begin).count();

	return EXIT_SUCCESS;
}
```

Также можно воспользоваться более старым методом с использованием библиотеки `<ctime>`:

```cpp
#include <cstdlib>
#include <ctime>

int main(int argc, char** argv) {
    const auto begin = clock();

    // код, время работы которого нужно замерить
    
    const auto end = clock();

    const auto time = (end - begin) / CLOCKS_PER_SEC;

	return EXIT_SUCCESS;
}
```