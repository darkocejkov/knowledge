> JavaScript API that allows web applications built with HTML, CSS and JS to use OpenGL concepts.

WebGL is self-described as a "rasterization" API rather than a 3D library, because all it does is allows JavaScript to provide data to the GPU for the purpose of rendering through rasterization.
- in fact, webGL authors consider a library like [[three.js]] to be a true 3D rendering library as it abstracts webGL to allow for the creativity of 3D rendering, and not a 3D-rendering-but-with-heavy-3D-math library.
- this is because in order to effectively use webGL for anything complex, you need to proficiently use 3D/linear maths.