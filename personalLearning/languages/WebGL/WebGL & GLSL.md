# Fundamentals
> WebGL is less of a 3D API and more of a rasterization API. This is because you need lots of background 3D math knowledge to render objects in WGL, whereas a 3D API like three.js would handle it for you, and let you write in objects rather than 3D math.

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

### WebGL Environment & Clip Space

- clip space coordinates are the WebGL-specific range from [-1, 1] in both X and Y
- WGL also wants you to provide the colors to paint primitives placed in clip space.
###### Essentially, we create VERTEX shaders to describe how to transform primitives, and use FRAGMENT shaders to describe how to transform *fragments* within primitives. 
^[fragments are grid-aligned to fit the rasterization space of pixels]
												![[Pasted image 20230309081500.png]]

### GLSL Programs
- in GLSL, when we define each of our shaders (vertex, fragment) we need to *link* the shaders, then *compile* them into a single program for the GPU to run. This compiled executable is the "program".
- the program runs multiple times to apply th *shader* to the graphics before it is rasterized, but there are cases in which the shader needs additional data to influence how it shades.
	- because we are working in a C-based language, there are strict memory allocations and to manipulate data we need to be aware of memory and how our *attributes* are allocated (and where!)

- attributes (variables) are stream-based variables. we *stream* data into them from a data buffer (array).
- however, to create and use a buffer, we need to **bind** them to a global resource (variable)
	- like binding an array to the `ARRAY_BUFFER` binding
^[this lets any function then refer to that specific buffer through that bind point]
- when loading data into the buffer, we must *know* what's going to be going inside it
	- it's also pretty important to note that any data structures from JavaScript (arrays, etc) must be TYPED
		- we can typecast with special functions, like `new Float32Array()`

> To summarize the flow of writing code for *initialization* of the program & environment.
1. Create and write a VERTEX shader
	1. manipulates primitive coordinates within space
2. Create and write a FRAGMENT shader
	1. manipulates fragment attributes (colors, etc)
3. Link & Compile both shaders into SINGLE program (object)
4. Create and bind buffer resources and load initial buffer data
5. Set up attribute location calls to "find" the attributes we created within the program

The render loop is more complex because we have to start dealing with memory allocations, and iterating through arrays based on data types and size.
- We can't just iterate array indices like in JS, but rather walk through it with pointers based on the type/size of data.
	- when we use `vertexAttribPointer`, it binds the array buffer that is binded to the bind point to the attribute we assign it to. this frees the bind point up for other buffers, while the assigned attribute is now pointed to the buffer.

Once we set up our render loop, we call `drawArrays` to draw.

For all data passing, we must first create that `attribute`, `uniform` in the shader program, so it can be used in the shader.
1. then, in runtime rendering, we must then get the location of that data binding based on the program and the name we gave it
2. then, we can use pointers to link attributes and data points to buffers to pass data.

WebGLs runtime is simple because we create 2 shaders, link and compile them, tell the WGL environment how to render the canvas (the target) and initialize the data that gets passed to the shaders.

###### The REAL complexity of WGL lies in the shader, because we can use the shader to build on the 2D rasterization to model 3D.


## Under the Hood
![[vertex-shader-anim.gif]]
> This is an animation that shows that its like to call `drawArrays` in WebGL, where we have an array of vertices defined by primitives. It's called 9 times because the `drawArrays` call is given a count of 9, in which it runs 9 times, once per vertex. 

1. The vertex shader is passed the data from the vertex array buffer into the attribute, and calculates the new position of the vertex based on the uniform matrix.
	- This process converts the vertices into clip-space coordinates to be rasterized, while at the same time, applies any transformations

2. WebGL handles the rasterization by figuring out which pixels correspond best to the vertices in the model
3. For each pixel (fragment), the fragment shader runs to "color" it.

# GLSL
> Graphics Library Shading Language

GLSL is the language that we write our shaders in, which allows our web-context (WebGL) to compile those shaders into a program, which can then be ran on the GPU.

> Why run programs on the GPU? Because otherwise, they would need to be ran on the CPU. Graphical calculations and transformations are intensive because they happen very often, and even though modern multi-threaded CPUs can handle it, the GPU is *designed* and *optimized* for graphical.

WebGL (any all other rendering engines) **require** two different shaders: vertex & fragment.
- the rendering loop will run the vertex shader once for every buffered vertex, which then translates those screen-space coordinates into a special coordinates for rasterization
- once all vertices have been *rasterized*, the engine knows the places of the vertices, then will operate on all the *fragments* (pixel representations) that make up the points of the drawing.

## [Data Types](https://www.khronos.org/opengl/wiki/Data_Type_(GLSL))

> [!scalars]
> 1. bool
> 2. int
> 3. uint (unsigned int)
> 4. float
> 5. double

>[!vectors]
> 1. bvec (bool)
> 2. ivec (int)
> 3. uvec (unsigned)
> 4. vec (floating)
> 5. dvec (double)

>[!important]
>when constructing a vector (or matrix), you must append an integer [2, 4] that describes the size of the vector.
>for example, vec4 is a 4-component floating point type vector

>[!swizzling]
>Swizzling is the ability to access and re-arrange components of vectors. If we have `vec4 v`, then:
>![[Pasted image 20230309153312.png]]
>which means that we can swap or repeat components by accessing them:
>`v.yyyy = vec4(v.y, v.y, v.y, v.y)`

GLSL has some nice syntactic shorthands that help you cut down on repeating code:
`vec4 s = sin(v) = vec4(sin(v.x), sin(v.y), sin(v.z), sin(v.w))`

>[!matrices]
> 1. matn
> 	- mat2 = 2x2
> 2. matnxm
> 	1. mat2x4 = 2x4

>[!arrays]
> not multidimensional, must be created with a size
> ex. `uniform vec2 u_someVec2[3]` means that we are creating a uniform global, of paired vectors
> furthermore, this uniform is an array when then contains vector pairs.
> - we can also reference these indices using the typical array accessor `u_someVec2[0]` for example.

GLSL also supports `struct` types to define custom (grouped) members
```
struct Example {
	bool active;
	vec2 pairVector;
}

uniform Example u_thing
...

// access member of struct with DOT (.) notation
u_thing.active
```

## Vertex Shaders

Vertex shaders run on primitive coordinates, and perform some transformation on coordinates to convert those supplied coords into *clipspace* coordinates (ranging from [-1, 1]). 
- `gl_Position` 
- vertex shaders can be supplied data from 3 different sources:
	1. attributes
		>  pointer-based variables that read values from buffers
	2. uniforms
		> value that stays constant for all vertices of a single *draw*
	3. textures
		> 2D arrays of data
		
- uniforms have special functions associated to the type of uniform you want to set
	- `uniform1f` for float
	- `uniform2f` for vec2
	- ...

## Fragment Shaders

Fragment shaders are called once per rasterized pixel to calculate the color of the pixel that is being drawn.
- `gl_FragColor`
- ``


Something unique about fragment shaders is that they can be given data from the vertex shader itself, through *varyings*. 
- Varyings must be declared (with the same name) between both the vertex and fragment shader

``` Vertex

uniform vec4 u_offset;
varying vec4 v_positionWithOffset;

void main(){
	gl_Position = a_position + u_offset;
	v_positionWithOffset = a_position + u_offset;
}

```

``` Fragment Shader

varying vec4 v_positionWithOffset;

void main(){
	gl_FragColor = v_positionWithOffset * 0.5 + 0.5;
}
```