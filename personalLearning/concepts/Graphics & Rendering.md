# OpenGL

<aside>
💡 “Open Graphics Library”

- Cross Language and Platform programming interface used to render 2D and 3D vector graphics, usually through a GPU to get hardware accelerated rendering.
</aside>

- A *specificiation* of how to render graphics, a standard.
    - as such, all major OS systems serve an **IMPLEMENTATION** of it
- Graphics drivers upgrade and implement OpenGL functionality

# 3D/2D Vector Rendering

- Simulating and modeling vector graphics requires breaking down objects into their points.
- We first must keep track of a plot of points, and model 3D/2D objects by their **vertices.**
- Vertices are connected into **primitives,** which are essentially triangles, of which objects are constructed out of **meshes** that attempt to simulate some 3D object’s planes and faces by these primitives.
- Primitives connect into fragments, when are then displayed on the screen using a technique called **rasterizing**, which attempts to best represent the model (in software), onto a finite amount of pixels and resolution.
    
    ![Untitled](Web%20Graphics%202D%20&%203D%2082068ea2ab524d56b472cecf53c60d3a/Untitled.png)
    
    ### Shading
    
    Is an approach to drawing the pixels, through the use of algebraic operations. Based on variables of the scene/environment, different shaders compute different colors and brightness values for a given object.
    
    ![Untitled](Web%20Graphics%202D%20&%203D%2082068ea2ab524d56b472cecf53c60d3a/Untitled%201.png)
    
    - Shading / Shaders are written in a specific OpenGL language (GLSL) that is based on C that allows you to fluently describe linear transformations, to display pixels in different ways

# WebGL

- Is a JavaScript library based on OpenGL, that uses HTML Canvas elements to center and render scenes for vector-space rendering.
- WebGL implements OpenGL in the context of the web, and allows browsers to use hardware-accelerated rendering techniques to render more complex scenes, faster.
- Libraries / Tools such as **ThreeJS** and **Spline** allow you to comfortably write JavaScript in simpler ways that implement WebGL for drawing.