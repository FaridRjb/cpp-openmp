# Lesson 2: Introduction

## Concurrency vs parallelism

Concurrency is when multiple tasks can run in overlapping periods. It's an illusion of multiple tasks running in parallel because of high-speed switching by the CPU. (Two tasks can't run simultaneously in a single-core CPU thread). Parallelism is when tasks run in parallel on multiple threads.

## Sharing memory

Writing on a storage disk takes a lot of time. Sharing the data on a shared memory, in other words, a RAM is faster. The cache is much closer to the processors, reducing the time consumed even in comparison with the RAM.

### Symmetric Multiprocessor (SMP)

SMP involves a multiprocessor computer hardware and software architecture where two or more identical processors are connected to a single, shared main memory, have full access to all input and output devices, and are controlled by a single operating system instance that treats all processors equally, reserving none for special purposes.

### Non-Uniform Memory Access (NUMA)

NUMA is a computer memory design used in multiprocessing, where the memory access time depends on the memory location relative to the processor.

## Code initialization

OpenMP supports C, C++, and Fortran.

### Header

This header is necessary in both C and C++.

```cpp
#include <omp.h>
```

### Parallel region

In order to make a part of a program parallel (or a parallel region), use:

```cpp
#pragma omp parallel
{
	// code...
}
```

The method `omp_get_thread_num()` gives the ID of the thread that is operating.

### Compile

Depending on the language, use `gcc` or `g++`, and then,

```bash
g++ -fopenmp filename
```

The output will have a name either `a` or `a.out`. The name can be specified using the following command:

```bash
g++ -fopenmp filename -o outputfilename
```

`main.cpp`:

```cpp
#include <iostream>
#include <omp.h>

using namespace std;

int main() {
	#pragma omp parallel
	{
		int thread_id = omp_get_thread_num();
		cout << "Hello from" << thread_id << endl;
	}
	return 0;
}
```

```bash
g++ -fopenmp main.cpp && ./a.out
```

Output:

```
Hello fromHello from02Hello from
Hello from5

4
Hello from1
Hello from7
Hello from6
Hello from3
```

## References

- [Complete C++ Scientific Programming Bundle - 21 Hours!](https://www.udemy.com/course/cpp-for-scientific-programming/)
- [What is the difference between concurrency and parallelism?](https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism)
- [Symmetric multiprocessing](https://en.wikipedia.org/wiki/Symmetric_multiprocessing)
- [Non-uniform memory access](https://en.wikipedia.org/wiki/Non-uniform_memory_access)
- [3.2.4  omp_get_thread_num](https://www.openmp.org/spec-html/5.0/openmpsu113.html#tailopenmpsu113.html)
