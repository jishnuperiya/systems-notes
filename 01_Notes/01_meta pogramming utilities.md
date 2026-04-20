
**Big picture:**
1. type knowledge layer (traits)
2. decision layer

### type knowledge layer (traits)
[[01_Type Traits]]

### decision layer
- if constexpr and concepts 
- these 2 replaced sfinae - i will skip it for now

std::enable_if is part of older metaprogramming style(SFINAE)
today its mostly replaced by:
- if constexpr
- concepts


## If constexpr



## Concepts

```cpp
template<typename T>

concept ConceptName = /* constraint expression */;
```

examples:
1. using type traits
```cpp
template<typename T>
concept Integral = std::is_integral_v<T>;
```

2. using requires
```cpp
template<typename T>
concept HasSize = requires(T a) {
    { a.size() } -> std::convertible_to<std::size_t>;
};
```

**how to constrain templates with concepts**

1. directly in the parameter list
```cpp
template<structure_predicate P>
void my_function(P pred);
```

2. using require clause:
```cpp
template<typename P>
requires structure_predicate<P>
void my_function(P pred);
```

this is also possible:

```cpp
static_assert(structure_predicate<MyPredicateType>);
```

why assert ? why not jsut depend on the constrain the templated code itself? - one good thing is that we can write a nice error message:

```cpp
static_assert(structure_predicate<MyType>, "MyType must satisfy structure_predicate");
```
you dont need static assert in most cases. normally using concpets in template parameters are sufficient.

