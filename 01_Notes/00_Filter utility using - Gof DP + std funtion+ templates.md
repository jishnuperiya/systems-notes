
### using strategy pattern:

https://github.com/jishnuperiya/cpp-sandbox/blob/main/strategy_pattern/filter_problem.cpp
a filter interface + different filter implementations

### using std:.function

in the strategy pattern we had a filter interface + a virtual appl() funtion.

lets try similar runtime polymorphic filtering using **type erasure**.
link: 


### using templates

link:

### when to use what?

Think in terms of **cost of abstraction**:

templates:  “Decide everything at compile time → fastest”
std function:  “Decide at runtime → flexible but some cost”
strategy:  “Old-school runtime polymorphism → more rigid + overhead”
