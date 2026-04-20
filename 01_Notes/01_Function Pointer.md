
# Core Idea


when program runs, memory is organized like this:

```
[ Text (Code) Segment ]   ← functions live here
[ Data Segment ]          ← global/static variables
[ Heap ]                  ← dynamic allocation (new/malloc)
[ Stack ]                 ← function calls, local variables
```

```cpp
int add(int a, int b) { return a + b; }
```

the machine instructions for add goes to the text segment

```cpp
int (*fptr)(int, int) = add;
```

fptr holds the address of add function in the text segment.

fptr is on stack
it stores the address of add (which is in text segment - where compiled instructions of add are stored)


# Uses

1. **function callbacks** : [[01_function callback]]
pass behaviour into functions

```cpp
void execute(int (*op)(int,int)) {
    std::cout << op(2, 3);
}
```
you can pass `add`, `multiply` etc

2. **strategy like behaviour**

this is basically like a low level strategy pattern:

```cpp
int compute(int a, int b, int (*op)(int,int)) {
    return op(a, b);
}
```

