**Taken from README.textile**

Chipmunk is a simple , lightweight fast and portable 2D rigid body physics library written in C. 
New things added in chipmunk2D 7-
	* ARM NEON optimizations
	* Autogeometry code
	* Multithreaded solver

Features in Chipmunk2D-
	* Designed specially for 2D video games.
	* Circle, convex polygon, and beveled line segment collision primitives
	* Multiple collision primitives can be attached to a single rigid body.
	* Fast broad phase collision detection by using a bounding box tree with great temporal coherence or a spatial hash.
	* Extremely fast impulse solving by utilizing Erin Catto's contact persistence algorithm.
	* Supports sleeping objects that have come to rest to reduce the CPU load.
	* Support for collision event callbacks based on user definable object types.
	* Flexible collision filtering system with layers, exclusion groups and callbacks.
	* Can be used to create all sorts of effects like one way platforms or buoyancy areas
	* Supports nearest point, segment (raycasting), shape and bounding box queries to the collision detection system.
	* Collision impulses amounts can be retrieved for gameplay effects, sound effects, etc.
	* Large variety of joints - easily make vehicles, ragdolls, and more.
	* Joint callbacks.
	* Can be used to easily implement breakable or animated joints.
	* Maintains a contact graph of all colliding objects.
	* Lightweight C99 implementation with no external dependencies outside of the Std. C library

About the demos given in chipmunk repo

The demos all just set up a Chipmunk simulation space and the demo app draws the graphics directly out of that. This makes it easy to see how the Chipmunk API works without worrying about the graphics code.	

**About Autogeometry feature in chipmunk 7.0.1**

Its a collection of utilities for vectorizing the image data and simplifying the geometry for it.It doesn't works on images exclusively , one could just give it a mathematical function like perlin noise if one want to make a procedurally generated map. 
There is something called convex decomosition which can break concave shapes to chipmunk friendly convex ones.
Possible things that can be done with it-
1. Given a background image of your level , generate a set of optimized line segments to fit the outline of it.
2. Given a mask for your terrain, you can update  it on the fly for worms style destructible terrain.
3. Given a mathematical function like perlin noise , generate procedural terrain4. Given an image for a sprite, automatically generate a convex polygon to fit around it. It will be able to generate a set of convex polygons for concave shapes.

Collision Detection Algorithm
Multithreaded solver for Robot Structual Analysis


Basically my responsibility is to make a python wrapper for a chipmunk C library . Right now kivent has been wrapped using cymunk which has chipmunk6. Chipmunk 7 has certain new features but there is not much difference.

**Difference between chipmunk 6 and 7**

Chipmunk Pro as of version 6.x included 3 main features: an optimized solver (threads + ARM NEON support), the Autogeometry library that let you turn procedural functions or images into collision geometry, and the Objective-Chipmunk wrapper for Objective-C. In Chipmunk 7 (master branch in GitHub), we have made Objective-Chipmunk BSD licensed, but the optimizations and the Autogeometry are still Pro features.
For wrapping v7 , it will be stable till now.

v7 overall is quite similar to v6. The biggest things to note are shape filters replacing layers/groups, the new collision handler C API and the more explicit names.

For wrapping c/c++ using python-
[link](http://intermediate-and-advanced-software-carpentry.readthedocs.io/en/latest/c++-wrapping.html)

Unlike most C/C++ Python wrapping solutions, Cython is not just a wrapper tool. Instead, it is a full-featured programming language with a Python-like syntax, but with optional added static typing. Additionally, Cython provides a compiler that translates Cython code into C or C++ code, which can subsequently be compiled to a Python extension module by a standard C/C++ compiler.


Link to [cython tutorial](https://dmtn-013.lsst.io/)

Cython Official [Documentation](http://docs.cython.org/en/latest/src/reference/language_basics.html)

[Memory Handlers KivEnt](http://kivent.org/docs/memory_handlers.html)
