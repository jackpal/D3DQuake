D3DQuake 0.73
=============

For fun I've ported the Quake engine to run under Direct3D 7.0.

Description	File	Size
D3DQuake program (replaces GLQuake.EXE)	D3DQuake.zip	322 KB
D3DQuake program for Matrox cards	D3DQuake06.zip	322 KB
Shareware version of Quake 1.06	quake106.zip	8.67 MB
Source Code for D3DQuake version v0.73	D3DQuakeSrc.zip	2.65 MB
Introduction

D3DQuake is a modification of the id Software GLQuake version of the Quake 1.09 engine. D3DQuake is just GLQuake modified to use Direct3D 7.0 instead of OpenGL.

Mini FAQ
--------

Q: What is D3DQuake?

A: D3DQuake is GLQuake modified to run on top of Direct3D 7.0 instead of OpenGL. GLQuake uses a fairly small (50 function) subset of OpenGL. It only took a few days to write Direct3D versions of these calls. (It's taken quite a few more days to get all the bugs out.)

Q: Why did you do this?

A: Because I wanted to learn about Quake, and about Direct3D, and I thought it would be cool.

Q: In your day job you work for WebTV, which is a subsidiary of Microsoft. Don't you have an ulterior motive for doing this?

A: Sure! OpenGL is great, but DirectX deserves more respect that it currently gets.. One reason I wrote D3DQuake is that I wanted to see how well Direct3D compares to OpenGL in terms of ease-of-use and performance.

Q: And what did you find?

A: So far, I have to admit that OpenGL's API is cleaner and easier to use than Direct3D. As for performance, I think with enough work, I could match OpenGL's performance. The trouble is that GLQuake uses data structures that are optimized for OpenGL. To speed up D3D I'd have to modify a fairly large chunk of the Quake code. (More or less all the gl_xxx files.)

Q: Will D3DQuake work on any video card that supports Direct3D?

A: No. Right now the D3D card has to have DirectX 7 drivers, and 8 MB of RAM. D3DQuake has only been tested on Windows 2000 with the NVIDIA TNT2 and the NVIDIA GeForce256.

Q: Any relation between your code and the controversial 1996 D3DQuake written by a Microsoft summer intern?

A: Nope. I didn't even know about that when I began writing my version. That version was reported to be only 3% to 5% slower than GLQuake. I wish I knew how they made it that fast!

Known Bugs / Limitations
------------------------

Does not check caps bits.
When run full screen, or run with 16-bit-per-pixel desktop, some levels have bad lighting.
Card Notes (alphabetical)
3dfx
Voodoo3	Runs for a while, but then the textures get messed up. (If you're using prerelease Windows 2000 Voodoo drivers, you will need to define the symbol USE_D3DFRAME and recompile the application.)
ATI
128	Works.
Matrox
G400
G400 MAX	Mixed reports. Some users have reported crashes at startup. One user reported that the D3D graphics are actually better than the GLQuake, due to bugs in the Matrox OpenGL driver.
NVIDIA
TNT2
GeForce 256	Works. (After all, that's the card I use to develop D3DQuake.)
Latest Win2K beta drivers, version 3.75, fix invisible weapon problem with GeForce.
Troubleshooting Tips

If you're having trouble getting D3DQuake to run, first check that normal GLQuake works.
If you send me a bug report, please tell me:
Your graphics card make and model number
The version number of the driver for your video card.
Your version of DirectX
Your version of Windows
Your version of D3DQuake


Code Notes
----------

All the Direct3D-specific code is in the file gl_fakegl.cpp. In addition, I had to make a few changes to the main sources. These changes are #ifdef'd using the preprocessor symbol D3DQUAKE. Presumably, you could merge this code base with any of the other modifications to GLQuake, and it would still work. The only caveat is that if the other modification uses some new feature of OpenGL, you'd have to add support for that new feature.

If you look at the source code for gl_fakegl.cpp, you'll see that it's all pretty straightforward. For the most part, each of the OpenGL calls that Quake uses has a corresponding D3D call. All I had to do was convert the arguments.

To compile, open the WinQuake project in Visual Studio 6.0 or later. Choose either the "Win32 D3D Release" or the Win32 D3D Debug" configuration. Build. The resulting executable can be used the same way as GLQuake.exe.

Current Performance
-------------------

Current performance of D3DQuake is not very good. On a GeForce card it's about half the speed of GLQuake. VTune tells me that 50% of D3DQuake's time is being spent in the file gl_fakegl.cpp. This is a file that I wrote to convert OpenGL calls to D3D calls.

To speed D3DQuake up further I will have to modify Quake's GL-specific code to make it more D3D aware. VTune tells me that I'm spending at least 10% of my time just copying vertecies into buffers to hand to DrawPrimitive. If I use vertex buffers, and change the Quake code to fill the vertex buffer, I bet I could get a significant speedup.

Computer
--------

Pentium II 300, 128 MB RAM

Software	Windows 2000 RC3
3D Accelerator	WinFast GeForce 256 SDR with beta NVIDIA W2K driver 3.6.5
Command line args	-window -nosound -nocdaudio
console args	timedemo demo2
 

Version	FPS	Speed	Remarks
GLQuake	110.7	100%	Normal GLQuake.
D3DQuake v0.1	39.9	36%	Original D3DQuake.
D3DQuake v0.2 Single Texture	43.5	39%	Eliminated some redundant state changes.
D3DQuake v0.2 Multitexture	33.5	30%	Yes, multitexture really is slower than single texture. I must be doing something wrong.
D3DQuake v0.3 Single Texture	49.6	45%	Shortened code paths.
D3DQuake v0.4 Single Texture	50.3	46%	More VTune-directed tweaking.
GLQuake Win98	116.9	100%	
D3DQuake v0.71 Win98	66.0	56%	Use vertex buffers with append mode.
GLQuake Win98	129	100%	Full optimizations
D3DQuake v0.72 Win98	95.6	74%	Full optimizations
