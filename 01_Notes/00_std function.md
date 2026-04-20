include -> functional

**std::function<bool(int)>pred_**  -> means any callable that takes an int and returns a bool

any callable mean?:

- **labmda**   :  auto f = [ ] (int x) { return x % 2 == 0; }

- **function** **pointer**: bool isEven(int x) { return x % 2 == 0}

- **functor** ( class with oeprator()) :
		struct isEven {
	     bool operator(int x) { return x % 2 == 0}
        }
    
so all of these:
```cpp
1. [](int x) { reutrn x % 2 == 0;}
2. isEven{}
3. isEven()
```

become same type:

```cpp
std::function<bool(int)>
```

this is called type erasure

**what is std::function**  - a type erase wrapper that can store any callable matching a specific signature - lamda, function pointer, functor and invoke it uniformly



