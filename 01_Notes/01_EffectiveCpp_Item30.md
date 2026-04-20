
**basic idea**
inline functions - looks like function and can call them wihtout the overhead of function calls!
you get more than avoiding the cost of function call with inilne keyword: compiler optimizations are designed for stretches of code that lack function calls(because compiler should see the fn body inorder to optimize).

**advantage and disadvantage and small vs big functions**
so advantage of inline: no function call overhead + access to compiler optimization
disadvantage of inline: code bloat - binary size increases
**note**: for smaller functions, the code generated for function call are generally more than code generated for the function body! - so inline lead to smaller objoect code in this instance.

**inline is a request- not a command**
implicit : functions inside a class defenition
explicit: with inline keyword

when does compiler ignore the request?
- when function is complicated. functions which contains loops or recursive
- calls to virtual fuctions (virtual itself means wait until runtime to figure out which function to call)
- if called through a function pointer:

```cpp
inline void f(){} // assuming compilers are willing to inline calls to f
void (*pf)() = f: // pf points to f
----
f();              // this call will be inlined. because its a normal call
pf();             // this call probably wont. because its though a func pointer
```









