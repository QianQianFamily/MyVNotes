# place new

A really cool introduction for place new:
https://www.geeksforgeeks.org/placement-new-operator-cpp/

Syntax:  new (address) (type) initializer

### new vs placement new ###
- Normal new allocates memory in heap and constructs objects there whereas using placement new, object construction can be done at known address.
-  With normal new, it is not known that, at what address or memory location its pointing to, whereas the address or memory location that its pointing is known while using placement new.
-  The deallocation is done using delete operation when allocation is done by new but there is no placement delete, but if it is needed one can write it with the help of destructor.

### Advantages of placement new operator over new operator ###
-  The address of memory allocation is known before hand.
-  Useful when building a memory pool, a garbage collector or simply when performance and exception safety are paramount.
-  There’s no danger of allocation failure since the memory has already been allocated, and constructing an object on a pre-allocated buffer takes less time.
-  This feature becomes useful while working in an environment with limited resources.
