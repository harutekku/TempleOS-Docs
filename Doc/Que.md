# Queue
A Queue is a bunch of `MAlloc()`ed chunks of mem linked together in a circle with one ptr to the next value and another ptr to the last value. These ptrs must be stored in the first locations in the structure.
