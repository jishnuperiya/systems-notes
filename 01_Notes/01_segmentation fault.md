
No, a segmentation fault is not always caused by double deletion. A segmentation fault happens whenever your program tries to access memory it is not allowed to, such as:

- Dereferencing a null or dangling pointer
- Accessing memory after it has been freed (use-after-free)
- Buffer overflows (writing/reading outside array bounds)
- Double deletion (deleting the same pointer twice)
- Stack overflows (infinite recursion)


## double deletion

always remember who own the pointer.
when your class own a ponter and when you copy it or assign it, who own?

use unique_pointer. when you pass unique pinter, do std::move so that ownership is transferred

