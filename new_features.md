From the chipmunk forum page, I came to know that the **chipmunk v7 overall is quite similar to chipmunk v6**.
* The biggest things to note are shape filters replacing layers/groups, the new collision handler C API and the more explicit names.

* **Autogeometry Library**-It's lets you turn procedural functions or images into collision geometry. Level design and asset creation is a time consuming portion of game development, and Chipmunk2D can significantly aid in creating the physics shapes. Chipmunk2D's automatic geometry generation can create fitted collision geometry from images. Now one doesn't need to type coordinates to generate collision shapes. The Autogeometry generation can create the physics shape for the terrain of your game from an image in milliseconds, allowing rapid iteration with just your graphics tools. This geometry can even be generated on the fly at runtime providing for spectacular techniques, such as deformable objects and terrain [Demo video on youtube](https://www.youtube.com/watch?v=oacZwUGP11c). Here is a [youtube video](https://www.youtube.com/watch?v=QObxwXH6Ri8) which explains the autogeometry feature.

* **ARM NEON optimizations for mobile CPUs**(requires an ARM CPU with a NEON coprocessor)

* **Multi-Threaded Solver** - cpHastySpace allows one to enable extra [threads](https://www.google.co.in/search?client=ubuntu&channel=fs&q=what+are+threads+in+CS+&ie=utf-8&oe=utf-8&gfe_rd=cr&ei=uqXaWNqsF8uL8Qf2u5OADg) for the solver to use as well.
