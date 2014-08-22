D3DQuake 0.1 Release Notes
==========================

Jack Palevich, jack@palevich.com

Introduction
------------

D3DQuake is a modification of the id Software GLQuake version of the Quake 1.09 engine. D3DQuake is just GLQuake modified to use Direct3D 7.0 instead of OpenGL.

Mini FAQ
--------

Q: What is D3DQuake?

A: D3DQuake is GLQuake modified to run on top of Direct3D 7.0 instead of OpenGL. GLQuake uses a fairly small (50 function) subset of OpenGL. It only took a few days to write Direct3D versions of these calls.

Q: Why did you do this?

A: Because I wanted to learn about Quake, and about Direct3D, and I thought it would be cool.

Q: In your day job you work for WebTV, which is a subsidiary of Microsoft. Don't you have an ulterior motive for doing this?

A: Sure! OpenGL is great, but DirectX deserves more respect that it currently gets.. One reason I wrote D3DQuake is that I wanted to see how well Direct3D compares to OpenGL in terms of ease-of-use and performance.

Q: So will D3DQuake work on any video card that supports Direct3D?

A: No. Right now the D3D card has to have DirectX 7 drivers, 8 MB of RAM and 32-bit textures. D3DQuake has  only been tested on Windows 2000 with the NVIDIA TNT2 and the NVIDIA GeForce256.

Known Bugs / Limitations
------------------------

Does not use multitexturing.
Requires 32 bpp textures.
Uses 32 bpp textures for light maps.

Code Notes
----------

All the Direct3D-specific code is in the file gl_fakegl.cpp. In addition, I had to make a few small changes to the main sources. These patches are #ifdef'd using the preprocessor symbol D3DQUAKE. Presumably, you could merge this code base with any of the other modifications to GLQuake, and it would still work. The only caveat is that if the other modification uses some new feature of OpenGL, you'd have to add support for that new feature.

If you look at the source code for gl_fakegl.cpp, you'll see that it's all pretty straightforward. For the most part, each of the OpenGL calls that Quake uses has a corresponding D3D call. All I had to do was convert the arguments.

To compile, open the WinQuake project in Visual Studio 6.0 or later. Choose either the "Win32 D3D Release" or the Win32 D3D Debug" configuration. Build. The resulting executable can be used the same way as GLQuake.exe.

Future Work
-----------

Enable multitexturing.
Fix the TextureTable implementation to look up textures more quickly. Right now it's O(n) It should be a hash table or a sparse array.
Do some performance comparisons with OpenGL, and fix any performance bottlenecks.

Acknowledgements
----------------

I'd like to thank id Software, especially John Carmack, for releasing the sources to Quake. And I'd like to thank the members of the DIRECTXDEV mailing list for answering my questions.




