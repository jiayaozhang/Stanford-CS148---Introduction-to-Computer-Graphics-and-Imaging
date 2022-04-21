# Stanford CS148 Introduction to Computer Graphics and Imaging

The short course would last 10 weeks for learning

Weekly two courses and one homework would be uploaded and finished.

teached by Ron Fedkiw

Ron Fedkiw awarded an Academy Award from The Academy of Motion Picture Arts and Sciences (twice: 2008 and 2015)

website link: https://web.stanford.edu/class/cs148/assignments.html


## Introduction

Why graphics?

Video Games: http://www.gamelook.com.cn/2015/06/218771
example ：
cpu: Geforece(Nvidia), HD7970(AMD), PowerVR(Imagination), Adreno(Qualcomm)
memory : PS4(Sony)，Switch(Nintendo), XBox(Mirosoft)
pc game : Uncharted(Naughty Dog)，HALO(Mirosoft), Call Of Duty(ActionVision), GTA(Rockstar)
PC no graphics card: Civilization(Firaxis)，Doom(id), StarCraft(Blizzard), Counter-Strike(Valve), Minecraft(Mojang)
web game : World of Warcraft(Blizzard), LOL(Riot)
phone game : Angry Birds(Rovio), COC(SuperCell)

Software:  ILM, RenderMan(Pixar), Weta, Dreamworks, AfterEffect, Houdini

* CADs, Animators, Modelers

* 2D image processing

* Visualization

* virtual and augmented reality

* user interface

## Light and Colors

C = 299,799,458 m/s (In Vacuum)
Refraction(折射) & total internal reflection(relection))
Wave Particle Duality(wave)

Photon(光子) : A quantum of light that has a position, a direction of propagation, and a wavelength.

Colors
Color Space : RGB, XYZ, Munsell, Lab, HSV


### Quiz

1. What is the difference between radiance and irradiance?
2. Explain what a BRDF is and why it is important for graphics.
3. In the mathematical definition of luminance, why are the bounds of the integral 380nm to 800nm?
4. What is a steradian? Draw a picture if it helps.
5. A [FILL_THIS_BLANK] describes how much energy is available at each [FILL_THIS_BLANK] lambda.
6. Name 3 types of cones.
7. CIE has defined three primaries to be monochromatic light sources - what are those?
8. How long did it take for you to (a) read the material and (b) answer these questions?
9. Briefly explain why both scanline renderers and ray tracers are useful?


## Scanline Rendering

This chapter tells Rendering and Rasterization, how to draw basic lines, circle Rasterization: Bresenham’s Algorithm, Midpoint Algorithm

Render: The process of generating an image from a description of a scene by means of a computer program.
https://en.wikipedia.org/wiki/Rendering_(computer_graphics)

A scene file contains objects in a strictly defined language or data structure; it would contain geometry, viewpoint, texture, lighting, and shading information as a description of the virtual scene.
Shading – how the color and brightness of a surface varies with lighting
Texture-mapping – a method of applying detail to surfaces

Therefore, a few loose families of more-efficient light transport modelling techniques have emerged:

rasterization, including scanline rendering, geometrically projects objects in the scene to an image plane, without advanced optical effects;
ray casting considers the scene as observed from a specific point of view, calculating the observed image based only on geometry and very basic optical laws of reflection intensity, and perhaps using Monte Carlo techniques to reduce artifacts;
ray tracing is similar to ray casting, but employs more advanced optical simulation, and usually uses Monte Carlo techniques to obtain more realistic results at a speed that is often orders of magnitude slower.
Two Way to Render an Image :

Rasterization(光栅化)
Raytracing(光线跟踪)
Ray tracing aims to simulate the natural flow of light, interpreted as particles. Often, ray tracing methods are utilized to approximate the solution to the rendering equation by applying Monte Carlo methods to it.

Rasterize : To convert vector data to raster-pixel or dot-format.

Bresenham’s Algorithm (1967)，将Wiki和PPT结合起来

非常简单的绘制直线算法，还有一个Xiaolin Wu’s line algorithm, a similarly fast method of drawing lines with antialiasing
Equation of a line : y = mx + b

To derive Bresenham’s algorithm, two steps must be taken. The first step is transforming the equation of a line from the typical slope-intercept form into something different; and then using this new equation for a line to draw a line based on the idea of accumulation of error.

Rasterizing Circle : Midpoint Algorithm

Filling Triangles, two methods for filling:

Check if each pixel in bounding box is inside the triangle(Parallelizable)
Rasterize border; sweep from left to right(Less Computation)
Barycentric Coordinates(重心坐标)

## Scanline Rendering & Geometric Modeling

Transformation(变换)：translation(平移，矩阵加法), scaling(缩放,矩阵乘法), rotation(旋转，矩阵乘法)

Viewing:

Convert between coorinates systems
Virtual camera, e.g. perspective projections
it includes Orthographic projection(正投影)和Perspective projection)(透视投影): When the human eye views a scene, objects in the distance appear smaller than objects close by - this is known as perspective. While orthographic projection ignores this effect to allow accurate measurements, perspective projection shows distant objects as smaller to provide additional realism.

Modeling:

Create objects in a convenient orientation
Use multiple instances of a given shape
Kinematics - characters/robots
Linear Transformation
Homogenous Coordinates(齐次坐标) ：
Given a point (x, y) on the Euclidean plane, for any non-zero real number Z, the triple (xZ, yZ, Z) is called a set of homogeneous coordinates for the point.

Homogeneous coordinates have a range of applications, including computer graphics and 3D computer vision, where they allow affine transformations and, in general, projective transformations to be easily represented by a matrix.

Homogeneous coordinates are ubiquitous in computer graphics because they allow common vector operations such as translation, rotation, scaling and perspective projection to be represented as a matrix by which the vector is multiplied

By the chain rule, any sequence of such operations can be multiplied out into a single matrix, allowing simple and efficient processing.

By contrast, using Cartesian coordinates, translations and perspective projection cannot be expressed as matrix multiplications, though other operations can.

许多图形应用涉及到几何变换，主要包括平移、旋转、缩放。以矩阵表达式来计算这些变换时，平移是矩阵相加，旋转和缩放则是矩阵相乘，综合起来可以表示为p’ = m1p+ m2（注：因为习惯的原因，实际使用时一般使用变化矩阵左乘向量）(m1旋转缩放矩阵， m2为平移矩阵， p为原向量 ，p’为变换后的向量)。引入齐次坐标的目的主要是合并矩阵运算中的乘法和加法，表示为p’ = pM的形式。即它提供了用矩阵运算把二维、三维甚至高维空间中的一个点集从一个坐标系变换到另一个坐标系的有效方法。
其次，它可以表示无穷远的点。n+1维的齐次坐标中如果h=0，实际上就表示了n维空间的一个无穷远点。https://oncemore2020.github.io/blog/homogeneous/

仿射变换（Affine Transformation) ，又称仿射映射，是指在几何中，一个向量空间进行一次线性变换并接上一个平移，变换为另一个向量空间。

齐次变换矩阵其实就是将仿射变换矩阵推广到齐次坐标系，从而将平移，缩放，旋转等变换合成到一个矩阵中；消除矩阵运算中的加减法，只留下乘法，以实现快速运算。

Hierarchical Modeling (层次建模)

Camera and Projection Matrices

* The world is in 3D
* But our Screen is in 2D
* Imagine our screen is a camera looking out into the world
* Tasks

1. Convert 3D world Coordinates to Camera Coordinates (虚拟camera，使用透视投影)
2. Project the Camera Coordinate on 2D screen

OpenGL Projection Matrix: 参见下面的推导过程：
http://www.songho.ca/opengl/gl_projectionmatrix.html
http://www.scratchapixel.com/lessons/3d-basic-rendering/perspective-and-orthographic-projection-matrix/projection-matrix-introduction


## Geomretic Modeling 
 

## BRDF & Lighting Equation


## Shading


## Texture Mapping


## Texture Synthesis


## Ray Tracing 


## Sampling


## Relection and Transmission


## Acceleration Structures


## Global illumination


## Photon Mapping


## Advanced Rendering


## Final Project


### HW 1. Blender Basics

### HW 2. OpenGL

### HW 3. Geometric modeling

### HW 4. Lignting & shading

### HW 5. Texturing

### HW 6. Sampling

### HW 7. Acceleration structures

### HW 8. Photon mapping

