Every Python object contains a reference counter which is incremented by Py_INCREF() and decremented by Py_DECREF(). If the counter becomes zero, Python might delete the object. 
For every call to Py_INCREF(), there should eventually be a call to Py_DECREF(). Call Py_INCREF() for objects that you want to keep around for a while. Call Py_DECREF() when you are done with them. 
For every call to Py_INCREF(), there should eventually be a call to Py_DECREF(). Call Py_INCREF() for objects that you want to keep around for a while. Call Py_DECREF() when you are done with them. 


**Memory Problems with C/C++**
 In languages like C or C++, the programmer is responsible for dynamic allocation and deallocation of memory on the heap. In C, this is done using the functions malloc() and free(). In C++, the operators new and delete are used with essentially the same meaning; they are actually implemented using malloc() and free().
 If a block's address is forgotten but free() is not called for it, the memory it occupies cannot be reused until the program terminates. This is called a memory leak.
 On the other hand, if a program calls free() for a block and then continues to use the block, it creates a conflict with re-use of the block through another malloc() call. This is called using freed memory. 
 Since python makes use of malloc and free function hence it has to avoid memory leaks as well as make good use of freed memory. This method is called reference counting. So every python object stores a counter .When a pointer to the object is stored somewhere then counter is incremented and when that pointer is freed then counter is decremented. When the counter = 0 then the last pointer pointing to that object has also been freed and the object is freed. 
