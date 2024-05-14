# Lesson 3: Fork and Join

Cores are hardware objects, while threads are created through programming.

## Fork-join model

### Master thread

Master thread is always there and is specified by `0`. When a program is running normally, the master thread runs in serially.

### Fork-join model

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/Fork_join.svg/1200px-Fork_join.svg.png)

When the computer comes acroos a parallel region, the master thread forks into a finite amount of threads and the task gets done parallelly. One it is finished, the threads join again into the master thread. This can be demonstrated using the fork-join model.

## Number of threads

1. The number of the threads in a region can be specified using `omp_set_num_threads(num_threads)`, where `num_threads` is an integer.

2. The number of threads can be defined locally using:

```cpp
#pragma omp parallel num_threads(num_threads)
// code... 
```

3. The number of threads can also be defined in the bash environment using:

```bash
export OMP_NUM_THREADS=num_threads
```

Even if the program is not parallelized, a thread of id 0 always exists. If you want to be sure that your command is done (just once), it is recommended to use the master thread.

Using `OMP_NUM_THREADS` can be handy, because this method does not require changing the number and recompiling. So, everyone can define their own number.

The number of threads can be obtained using `omp_get_num_threads()`.

`main.cpp`:

```cpp
#include <iostream>
#include <omp.h>

using namespace std;

int main() {
	#pragma omp parallel num_threads(3)
	{
		int thread_id = omp_get_thread_num();
		cout << "Hello from " << thread_id << endl;
	}
	return 0;
}
```

```bash
g++ -fopenmp main.cpp && ./a.out
```

Output:

```
Hello from 0Hello from 
Hello from 2
1
```

## False sharing

<!-- TODO: explanation -->

### Cache line

The chunks of memory handled by the cache are called cache lines. The size of these chunks is called the cache line size. Common cache line sizes are 32, 64 and 128 bytes.

## References

- [Complete C++ Scientific Programming Bundle - 21 Hours!](https://www.udemy.com/course/cpp-for-scientific-programming/)
- [Fork–join model](https://en.wikipedia.org/wiki/Fork%E2%80%93join_model)
- [3.2. Cache Lines and Cache Size](http://www.nic.uoregon.edu/~khuck/ts/acumem-report/manual_html/ch03s02.html)
