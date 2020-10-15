# 9/29

## Recordings

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



# 10/1

`09_24_2019`

- `NULL` pointer - 04

  - In header files, `#define NULL ((void *) 0)`, so that `NULL + 1` is illegal

- Arrays - 05

  - `sizeof()` returns **byte** size

  - Theorem #1: `*(p + 1) == a[1]`
  - C allows a pointer to the next address to the last element of the array
  - Theorem #2: array name, in most cases, is the address of its first element: `a => &a[0]`
    - Exception 1: `sizeof(a)` is the byte size of the whole array
    - Exception 2: `a++` is illegal
  - Theorem #3 (generalize of the previous 2): `*(x + y) == x[y]`
  - `0[a] => *(0 + a) <=> *(a + 0) <=> a[0]`

- Heap - 05

  - Purpose: share address among functions



# 10/6

`09_26_2019`

- `char []` and string literals
  - `0` at the end is not fundamental. Instead it is a special case
  - `0` is just a marker that marks the end of a string
  - `char *p = "abc"`. Cannot change `p[0]` because it is stalled in static/code region
  - `printf("%s", "hello" + 1)` will print `ello` because the type of the second element is `char *`



- `strcpy`, `strcat`

  - Diagram at `38:00`. Pay attention to the stack pointer.

  - ```c
    void strcat(char *t, char *s) {
      while (*t) { t++; }
      strcpy(t, s);
    }
    ```

  - `strncpy` and `strncat` are the safer versions when `t` is shorter than `s`



- `argv`
  - stored right above the stack



# 10/8

- const

  - const can be get rid of

    ```c
    void foo(const char *t) {
      char *t2 = (char *)t; // then *t2 = 0 is legal
    }
    ```

- function pointer

  - ```c
    int (*f1)(const void *v1, const void *v2); // f1 is a variable, a pointer to a function returning int
    // can do f1 = *compareInt;
    int *f2(const void *v1, const void *v2); // function prototype, returns int *
    ```

  - Counter-clockwise spiraling (lecture `1:04:35`)

  - `compareInt` is the same as `&compareInt` as a syntax sugar because function name itself has no meaning



# Exam 1

- ` str[cpy, ncpy, cmp, ncmp]`

- lab 1 & 2 solutions



