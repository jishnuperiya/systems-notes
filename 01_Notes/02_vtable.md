**virtual dispatch table**

remember when you **create an object**,  you get a box in memory with the member variables and its values. and if you create an object of a **class which has atleast one virtual fucntion** you get an additional member varialble called vptr, added automatically by the compiler as first member.

```
MyObject (in memory)
┌─────────┬──────────────────┐
│  vptr   │  actual members  │
│ (8 bytes│  (name, age...)  │
└────┬────┴──────────────────┘
     │
     ▼
vtable for MyClass
┌──────────────────────┐
│ ptr → MyClass::speak │
│ ptr → MyClass::move  │
└──────────────────────┘
```

and every class with virtual function gets a hidden vtable which is an **array of function pointers**

### Code example

```cpp
class Animal {
public:
    virtual void speak() { cout << "..."; }
    virtual void move()  { cout << "moving"; }
    int age = 0;
};

class Dog : public Animal {
public:
    void speak() override { cout << "Woof!"; }
    // move() not overridden — inherits Animal's
};
```

**Animal's vtable:**

|Slot|Points to|
|---|---|
|0|`Animal::speak`|
|1|`Animal::move`|

**Dog's vtable:**

|Slot|Points to|
|---|---|
|0|`Dog::speak` ← overridden|
|1|`Animal::move` ← inherited|

#### Dispatch mechanism

when you do this, 

```cpp
Animal* a = new Dog();
a->speak();
```
2 things runs in order:
- memory is allocated in the heap for the Dog object.
- Dog construtor runs

so when you do `new Dog()` you get a chunk of memory which look like this:

```
Address   Contents
───────────────────────────────────
0x1000    vptr → 0x4000 (Dog's vtable)
0x1008    age = 0                      ← inherited from Animal
```

and Dog's vtable is sitting in read only segment ( refer: [[02_full memory picture]]) in the memory:
```
Address   Contents
───────────────────────────────────
0x4000    → Dog::speak      ← overridden
0x4008    → Animal::move    ← inherited
```


So when you do:

cpp

```cpp
Animal* a = new Dog();
```

`a` holds `0x1000` — a pointer to that chunk. That's it. Just an address.

When you call `a->speak()`, the CPU:

1. Goes to `0x1000` — the object
2. Reads the first 8 bytes — that's the vptr: `0x4000`
3. Goes to `0x4000` — the vtable
4. Reads the first entry — that's `Dog::speak`
5. Calls it

The CPU doesn't know or care that `a` is typed as `Animal*`. It just follows pointers.

