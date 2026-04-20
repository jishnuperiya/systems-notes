```
┌─────────────────────┐  high address
│       Stack         │  ← local variables, function calls
├─────────────────────┤
│         ↓           │
│         ↑           │
├─────────────────────┤
│        Heap         │  ← new Dog()  — the OBJECT lives here (vptr + members)
├─────────────────────┤
│   .rodata / .bss    │  ← vtable lives here (read-only, fixed at compile time)
├─────────────────────┤
│       .text         │  ← the actual function code (Dog::speak, etc.)
└─────────────────────┘  low address
```

for the code example refer: [[02_vtable]]

