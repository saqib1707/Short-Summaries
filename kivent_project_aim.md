**Brief introduction**
Right now the cymunk(physics) component stores data in python object.This means that u have to keep the python object alive(in memory) to track and manage the lifecycle of a physics(chipmunk) object that actually does not need the overhead of keeping a python object alive at all. But this is not the correct way since we need to keep refernce to these objects somewhere. The main aim moving forward is to have all data stored in C structs and generate python objects whenever the user wishes to interact with the data from the underlying data structures.
The chipmunk api is already set up to work like this as it is a C library but the cymunk api uses the python lifecycle(in OOP lifecycle refers to the time from the creation of an object to the destruction of that object and lifetime of a particular object may vary from one run to another) to manage the lifecycle of chipmunk objects which is a bad match for kivent.

So taking the example of shapes class of chipmunk for instance, u should still make wrapper python objects (matlab abhi bhi python wrapper objects banane hai jaise cymunk me available hai) using cdef'd classes that allow u to interact with the various attributes of chipmunk objects.

But the biggest difference is that these objects will not be responsible for managing the lifecycle of the chipmunk objects rather the gamesystem will be responsible for this. This is similar to the model system in kivent right now, if u request to change the vertex model it will provide u with a python object which will let u interact with the data, but it does not manage the existence of that data.


**Minutes with Kovak- 17th March**

Me:The kivent_cymunk right now uses the python object to manage the lifecycle of physics object but it is better that the life cycle is managed by the game system and not by the python wrapper objects.So that it would lead to more memory optimizations or one can say less use of effective memory as the python objects would not be stored for large time.
Will there be any visual difference apart from memory optimizations that can be seen after the project is implemented.?? 
**Kovak**:In cymunk u must keep the object alive so that garbage collection( In CS garbage collection is a form of automatic memory management system. In GC, the garbage collector tries to reclaim garbage or memory occupied by objects that are no longer in use by the program.  CPython uses the reference counting or the reference cycle algorithm to do garbage collection) doesn't trigger. For keeping the object alive=> u must somewhere store reference to that object and that reference needs to be a python object or another option is to manually control its reference counting and not let it got to zero or in short manually perform the reference counting associated.
This means the components cannot be an array of C structs alone, and need to keep alive a parallel list of python components that hold the references to keep the cymunk objects alive and then when creating/deleting we must interact with those object.
[Here](https://github.com/tito/cymunk/blob/master/cymunk/body.pxi#L16) we see the current way of cymunk creating a body, [here](https://github.com/tito/cymunk/blob/master/cymunk/body.pxi#L25) we see how it gets deleted

The point is that kivent has its own method of managing the life cycle of objects that enables it to avoid the overhead of python object garbage collection entirely. Chipmunk objects can live independently of the python object that currently houses them in cymunk.

**Minutes with Kovak - 28th March**
Me: for testing purpose I was thinking to use time as a metric. Will it be good enough to tell the difference between right now kivent_cymunk and the kivent_chipmunk
Kovak: the biggest difference I expect to see is in the time it takes to create or remote a physics entity though the frame time per update probably won't change significantly.
I typically use cProfile and examine the average time for the update,init_component and remove_component.



**What does reference means in python and in C++?**
You see, in C++ (and other languages), a variable (and object fields, and entries in collections, etc.) is a storage location and you write a value (for instance, an integer, an object, or a pointer) to that location. In this model, references are an alias for a storage location (of any kind) - when you assign to a non-reference variable, you copy a value (even if it's just a pointer, it's still a value) to the storage location; when you assign to a reference, you copy to a storage location somewhere else. Note that you cannot change a reference itself - once it is bound (and it has to as soon as you create one) all assignments to it alter not the reference but whatever is referred to.
In Python (and other languages), a variable (and object fields, and entries in collections, etc.) is a just a name. Values are somewhere else (e.g. sprinkled all over the heap), and a variable refers (not in the sense of C++ references, more like a pointer minus the pointer arithmetic) to a value. Multiple names can refer to the same value (which is generally a good thing). Python (and other languages) calls whatever is needed to refer to a value a reference, despite being pretty unrelated to things like C++ references and pass-by-reference. Assigning to a variable (or object field, or ...) simply makes it refer to another value. The whole model of storage locations does not apply to Python, the programmer never handles storage locations for values. All he stores and shuffles around are Python references, and those are not values in Python, so they cannot be target of other Python references.


Want to understand what [reference](https://www.youtube.com/watch?v=z_55F4zSjoA) in python means. 
Want to understand what [reference count](https://www.youtube.com/watch?v=oQ8hztC7hGY) in python means.
Another link for reference counting and [garbage collection](https://medium.com/python-pandemonium/cpython-memory-management-479e6cd86c9#.ggb8uvaw7)
Another one related to [garbage collection](https://www.digi.com/wiki/developer/index.php/Python_Garbage_Collection).


