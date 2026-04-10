
# Quick Refresher(if you are familiar with the pattern)

entire pattern — 3 things:

1. **Interface** — `Strategy` with a virtual method
2. **Concrete classes** — `StrategyA`, `StrategyB` implement it differently
3. **Context** — holds a strategy and calls it, without knowing which one it is

# The concept

When you have **one goal** but **multiple ways** to achieve it
Instead of writing massive block of if/else statements, you plug in the specific "strategy" you need at runtime

# Real World Analogy: Navigating Maps

Buidling a GPS map
goal : go from A  to B
multiple ways to achieve it (strategies) :
- strategy A : walking (shortcut through parks)
- strategy B: driving (prefer highways)
- strategy C: public transit (follow bus/train schedules)

The **goal** is one, but algorithm changes based on the user choice

# Implementation Before knowing this pattern

```cpp
function buildRoute(transportType)
{
if(tarnsportType == 'walking') { /* 50 lines of walking logic*/}
elseif(transportType == 'driving') { /* 50 lines of traffic logic*/}
// becomes a nightmare to maintain!
}
```

## Structure

There are three key players:

**Context** — the class that uses a strategy. It holds a reference to a strategy object and delegates work to it, but doesn't know the concrete implementation.

**Strategy Interface** — a common contract (interface or abstract class) that all concrete strategies must follow.

**Concrete Strategies** — the actual implementations of the algorithm (e.g., `CarRoute`, `BikeRoute`, `WalkRoute`)


# Example in C++

```cpp
#include <iostream>
#include <memory>

// Strategy Interface
class Strategy {
public:
    virtual void execute() = 0;
    virtual ~Strategy() = default;
};

// Concrete Strategies
class StrategyA : public Strategy {
public:
    void execute() override {
        std::cout << "Executing Strategy A\n";
    }
};

class StrategyB : public Strategy {
public:
    void execute() override {
        std::cout << "Executing Strategy B\n";
    }
};

// Context
class Context {
    std::unique_ptr<Strategy> strategy;
public:
    void setStrategy(std::unique_ptr<Strategy> s) {
        strategy = std::move(s);
    }

    void doWork() {
        strategy->execute();
    }
};

// Main
int main() {
    Context ctx;

    ctx.setStrategy(std::make_unique<StrategyA>());
    ctx.doWork();   // Executing Strategy A

    ctx.setStrategy(std::make_unique<StrategyB>());
    ctx.doWork();   // Executing Strategy B
}
```

