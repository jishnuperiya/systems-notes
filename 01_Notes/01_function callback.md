
instead of function deciding everything, you give another function that can be called

```cpp
#include<iostream>
#include<functional>


void process(int x, std::function<void(int)> callback)
{
  callback(x);
}
void myCallback(int value)
{
  std::cout<< "callback got: " << value << "\n";
}

int main()
{
  process( 5 , myCallback);
}
```

why use them?

callbacks let us customize behaviour without changing the function itself.


callbacks can be implemented using multiple ways:

- **function pointers** ([[01_Function Pointer]])
   ```cpp
   void (*fptr)(int)
   ```
- **std::function** ([[00_std function]])
```cpp
std::function<void(int)>
```
type erased wrapper - more flexible, slight overhead

- templates
```cpp
template<typename Func>
void process(int x, Func callback)
{
  callback(x);
}
```
zero overhead. compile time
code bloat. 

**Tradeoffs**

| Approach         | Pros             | Cons          |
| ---------------- | ---------------- | ------------- |
| Function pointer | Simple, fast     | Limited       |
| std::function    | Flexible         | Some overhead |
| Template         | Fastest, generic | Code bloat    |

