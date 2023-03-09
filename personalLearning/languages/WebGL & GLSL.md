# Fundamentals

> WebGL is less of a 3D API and more of a rasterization API. This is because you need lots of background 3D math knowledge to render objects in WGL, whereas a 3D API like three.js would handle it for you, and let you write in objects rather than 3D math.
> 

## [Rasterization](https://www.youtube.com/watch?v=t7Ztio8cwqM)?

Rasterization is the way we display model-based objects onto pixel-based screens. All pixel monitors have tiny (squre) pixels composed of Red, Green and Blue lights. (255, 255, 255) represents white whereas (0, 0, 0) represents black, the combination of 8bit  (0 - 255) color for each (R, G, B) in between. How do we actually draw objects living in memory, modelled by math and absolute vectors onto the screen? We ********rasterize******** an image into a pixel grid to approximate the model, projecting it.

## WebGL

- runs on the GPU, it is hardware accelerated, making it fast to draw and render (at least faster than what would be computed)
- uses points, lines, and triangles to build 3D vector graphics
- the code is written in what’s called GLSL, or OpenGL Shader Language, which allows WGL to run on the GPU
    - there are a PAIR of functions that we write:
        - vertex shader
            - computes vertex positions, which then is returned to WebGL to rasterize
        - fragment shader
            - called when rasterizing the primitives after the vertex shader
            - computes colors for each pixel of the primitive
        - the vertex + fragment shader pair is called a “program”
    - GLSL is a strictly typed C/C++ language
- [WebGL State Diagram](https://webglfundamentals.org/webgl/lessons/resources/webgl-state-diagram.html)
- WGL is about configuring the state for the “program(s)” to run, and when we want to draw we can call `gl.drawArrays` or `gl.drawElements`
    - data that needs to be given to the vertex and fragment shaders must also be given to the GPU, and is done through 4 different methods:

### Data Passing

1. Attributes + Buffers
    1. buffers are arrays of binary data, containing things like positions, normals, texture coords, vertex colors (anything really)
        1. not random access, because vertex shaders are executed more than once, each time it does it pulls out values from specified buffers and assigned to attributes
    2. attributes are specifications of how data is pulled from the buffers to be given to the vertex shader
2. Uniforms
    1. “global” variables set before shader is executed
3. Textures
    1. arrays of data that can be random access in shader, usually image data (but can be easily anything other than color data)
4. Varyings
    1. is how vertex shaders pass data to fragment shaders
    2. values set in varyings from vertex shader are ************interpolated************ while executing the fragment shader