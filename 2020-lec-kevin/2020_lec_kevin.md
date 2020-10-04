# 9/29

## Video Recordings

`09_17_2019` and `09_19_2019`

- Storage class - 02

  - automatic/local/stack variables

  - Static variables: the variable is kept at the start of the program

    - global: discouraged
    - file
    - block/function:  see example below

    Differences are just access

Function static variables:

```c
int f() {
  static int count = 0; // initialize in the first call only
  count++;
  return count;
}

int main() {
  int s = 0;
  for (int i = 0; i < 10; i++) {
    s += f();
  }
  printf("%d", s); // 55
}
```

- Address space - 02

  - Every process thinks it has the entire address space (often 512G)
  - Heap: allocate memory at runtime `malloc()`

  

- Pointers - 04
  - `int` and `int *` are incompatible types

    - cannot do `int *p = 1996`

  - `int *` and `double *` are incompatible types

    - but can force

    - ```c
      int i = 3;
      double d = 3.14;
      int *p = &i;
      double *q = &d;
      p = (int *)&d; // legal, but undefined behaviour
      ```

  - `void *`: not dereferencable



## Live

Review

Consider the code (suppose the address of `d` is 2000)

```c
int i = 1234;
double d = 3.14;
int *pi = &i;
double *pd = &d;
int x = *(int *)(pd);
```

| Expression   | Value                                            | Type       |
| ------------ | ------------------------------------------------ | ---------- |
| `pd`         | 2000                                             | `double *` |
| `(int *)pd`  | 2000                                             | `int *`    |
| `*(int *)pd` | `int` representation of the first 4 bytes of `d` | `int`      |



Recursion and stack

```c
int f(int x) {
  if (x <= 1) {
    return 1;
  } else {
    int y = x * f(x - 1);
    return y;
  }
}
```

When recursion goes deeper, stack goes down. When recursion returns, stack goes up. Print `x` and `&x` to see the change of stack.