
### The problem first

say you have a shape hierarchy:

```cpp
class Shape { };
class Circle  : public Shape { double radius; };
class Rect    : public Shape { double w, h; };
class Triangle: public Shape { double base, height; };
```

Now you want to **do things** to shapes — draw them, compute area, serialize to JSON, export to SVG...

The **naive approach** is to add a virtual function for each operation:
```cpp
class Shape {
    virtual void draw() = 0;
    virtual double area() = 0;
    virtual string toJSON() = 0;  // and on and on...
};
```

This gets painful fast. Every new operation means **touching every class**. And if these classes are in a library you don't own — you can't touch them at all.

### The Core Tension

There are two axes of change:

```
              Circle   Rect   Triangle
             ──────────────────────────
draw()       │
area()       │
toJSON()     │
exportSVG()  │
```

- Adding a **new shape** (new column) → easy with virtual functions
- Adding a **new operation** (new row) → painful, touch every class

Visitor flips this. It makes adding **new operations easy**, at the cost of making new shapes harder.

---

### The Visitor Pattern

The idea: instead of putting the operation inside the shape, you **pass a visitor object into the shape**, and the shape calls back the right method on it.

cpp

```cpp
// Forward declarations
class Circle;
class Rect;
class Triangle;

// 1. Visitor interface — one method per shape type
class Visitor {
public:
    virtual void visit(Circle& c)   = 0;
    virtual void visit(Rect& r)     = 0;
    virtual void visit(Triangle& t) = 0;
};

// 2. Shape accepts a visitor
class Shape {
public:
    virtual void accept(Visitor& v) = 0;
};

class Circle : public Shape {
public:
    double radius;
    void accept(Visitor& v) override { v.visit(*this); }  // calls visit(Circle&)
};

class Rect : public Shape {
public:
    double w, h;
    void accept(Visitor& v) override { v.visit(*this); }  // calls visit(Rect&)
};
```

---

### Now Adding Operations is Easy

Want to add `draw`? Just write a new visitor:

cpp

```cpp
class DrawVisitor : public Visitor {
public:
    void visit(Circle& c)   override { cout << "Drawing circle r=" << c.radius; }
    void visit(Rect& r)     override { cout << "Drawing rect " << r.w << "x" << r.h; }
    void visit(Triangle& t) override { cout << "Drawing triangle"; }
};
```

Want `toJSON`? Another visitor:

cpp

```cpp
class JSONVisitor : public Visitor {
public:
    void visit(Circle& c)   override { cout << "{type:circle, r:" << c.radius << "}"; }
    void visit(Rect& r)     override { cout << "{type:rect, w:" << r.w << "}"; }
    void visit(Triangle& t) override { cout << "{type:triangle}"; }
};
```

Using it:

cpp

```cpp
vector<Shape*> shapes = { new Circle{5}, new Rect{3,4} };

DrawVisitor drawer;
JSONVisitor  json;

for (auto s : shapes) {
    s->accept(drawer);  // draws it
    s->accept(json);    // serializes it
}
```

---

### The Magic: Double Dispatch

This is the clever mechanical trick underneath. Normal virtual dispatch is **single dispatch** — the method chosen depends on one object's type.

cpp

```cpp
s->accept(v);   // dispatch on s's type → Circle::accept, Rect::accept, etc.
```

Inside `Circle::accept`:

cpp

```cpp
void accept(Visitor& v) { v.visit(*this); }  // dispatch on v's type → DrawVisitor, JSONVisitor, etc.
```

Two virtual dispatches in a chain. The right `visit()` is chosen based on **both** the shape type and the visitor type. That's double dispatch.

---

### When to Use It

**Good fit:**

- You have a stable set of types but frequently add new operations
- You can't modify the classes (library code) but can make them accept visitors
- Compilers, interpreters, AST walkers — classic use case

**Bad fit:**

- You add new types often — every new type means updating every visitor
- The operations are simple enough that just a virtual function is fine

---

### One Line Summary

> Visitor lets you add new operations to a class hierarchy **without modifying the classes** — by moving the operation outside and using double dispatch to route to the right implementation.

