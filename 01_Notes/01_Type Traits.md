
core idea: ask questions about type before the program runs

### Basic Idea

type trait is a templated struct.

for example:
´`std::is_integral<int>:: value` is commonly used

under the hood, its -

```cpp
template<typename T>
strut is_integral;
```
and the struct is_integral has a static member called value.
the value is a bool variable, return true or false based on T.

there is also a helper variable temlate in the struct:

`bool is_integral_v = is_integral<int>::value`
so easy to write, if you prefer.

thats it. very simple idea.


## Categories

there are 3 :
- Query traits
- Transformational traits

### 1 . Query traits
produce a bool

example:

```cpp
std::is_integral_v<T> 
std::is_pointer_v<T> ****
std::is_const_v<T>
std::is_same_v<T1, T2> 
std::is_base_of_v<t1, t2>
```

### 2. Transforming types
```cpp
std::remove_const<const int>::type      // int
std::remove_reference<int&>::type       // int
std::remove_pointer<int*>::type         // int
std::add_pointer<int>::type             // int*
std::add_const<int>::type               // const int
std::make_unsigned<int>::type           // unsigned int
```
c++ 17 : remove_const_t -> shortcut


type traits are very useful in compile time control / compile time branching
for these kind of metaprogramming utilities:
- if constexpr
- sfinae(enable_if)
- trait based selelction
**control which code is compiled**
**make compile time decisions**

