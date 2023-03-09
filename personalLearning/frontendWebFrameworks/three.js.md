# Three JS

---

- threejs is a javascript package that ******************abstracts WebGL.******************
    - this means that using 3js manipulates WebGL under the hood, and makes it easier to create easy object-space models.

---

- The renderer is given a SCENE and a CAMERA and renders what the camera is seeing in the scene.
- Concepts within the blue are considered as OBJECTS, we create MESH objects, light OBJECTS, etc.
- We pass geometry, material, or texture parameters to the objects we create.
- These meta-objects describe things about the objects we pass them to
- These can be multiplicitly shared between multiple objects

![Untitled](Three%20JS%200d67735b9e484e54a46b2e559a27b606/Untitled.png)

---

# Cameras

- The camera is given FOUR arguments
    - Field of View (FOV)
        - degrees - the angle of the FOV
    - Display Aspect
        - the aspect ratio of the canvas (default 2)
    - Near
        - the clipping plane that is the closest to the camera, objects between the camera and the NEAR plane are NOT rendered
    - Far
        - clipping plane farthest from the camera.

![Untitled](Three%20JS%200d67735b9e484e54a46b2e559a27b606/Untitled%201.png)

![Untitled](Three%20JS%200d67735b9e484e54a46b2e559a27b606/Untitled%202.png)

- The 4 lines that project from the camera, given the two clipping planes create a frustrum.
    
    > A frustrum is another shape primitive, just like a sphere, or cube. It’s a pyramid with the tip cut off.
    > 

- We also give a 3D co-ordinate to position the camera.

- Why not have inifnite near/far bounds?
    - Because rendering units scale with the depth distance - when there’s a huge gap in the near and far clipping planes, the units between them become REALLY small.
    - Sometimes so small, that rendering artifacts occur, like “z-fighting” from the rendering engine not having enough precision to determine the z-order (what’s drawn in front of what) properly.
- We can use a setting called *****************logarithmicDepthBuffer*****************, but that is very expensive and does not solve the original issue

- PerspectiveCamera is what creates a frustrum, because to create a perspective it requires having depth of near/far.
- OrthographicCamera does not create a frustrum because its view is orthographic, it eliminates the 3D perspective. The camera view creates a rectangular prism because it projects a rectangle.
    - it still has near/far clipping planes however.

```jsx
camera.left = -canvas.width / 2;
camera.right = canvas.width / 2;
camera.top = canvas.height / 2;
camera.bottom = -canvas.height / 2;
camera.near = -1;
camera.far = 1;
camera.zoom = 1;
```

```jsx
camera.left = 0;
camera.right = canvas.width;
camera.top = 0;
camera.bottom = canvas.height;
camera.near = -1;
camera.far = 1;
camera.zoom = 1;
```

---

## Scenes & Scene Graph

> ThreeJS groups objects in a hierarchy, nodes are in parent-child relationships, and each parent is a “local scene”. Overall, all nodes children to the root node compose the global scene.
> 

## Materials

- Materials are object configurations that describe what other objects look like, typically with the base color, and how lighting interacts with the material. There are different “algorithms” that define materials (phong, lambert, basic, etc). Materials also describe how the object is shaded.
- MeshBasicMaterial
    - not affected by lights
- MeshLambertMaterial
    - computes lighting ONLY at vertices
- MeshPhongMaterial
    - computes light at EVERY pixel
        - which means that it supports SPECULAR highlights
    - makes it computationally more expensive
- MeshToonMaterial
    - based on Phong materials, but uses a GRADIENT MAP to shade, so you can achieve cartoon-like shading with sharp shadows

### Special Data Materials

- Materials used for getting rendering data of the object, such as shadows, depth, and geometric normal.
- ShadowMaterial
    - material shaded to display what parts of the mesh are in shadow and which are not
- MeshDepthMaterial
    - float representing the depth of each of the mesh’s pixels, from 0 being from the ****near**** camera and 1 being the ***far*** camera argument.
- MeshNormalMaterial
    - shades the normals of geometry, which are the direction that triangles/pixels face in the 3D axis.
        - X = red
        - Y = green
        - Z = blue

### Shader Materials

- ShaderMaterial is for custom shading logic using the Three.JS shading system, while
- RawShaderMaterial is for custom shaders

### Physically Based Rendering materials (PBRs)

- Phong & Lambert use simple math and are not realistic renders
- MeshStandardMaterial
    - roughness & metalness
- MeshPhysicalMaterial
    - is similar to Standard, but has a ******************clearcoat******************

### Material Cost & Rank

(fastest to slowest)

1. Basic
2. Lambert
3. Phong
4. Standard
5. Physical

![Untitled](Three%20JS%200d67735b9e484e54a46b2e559a27b606/Untitled%203.png)

![MeshStandardMaterial](Three%20JS%200d67735b9e484e54a46b2e559a27b606/Untitled%204.png)

MeshStandardMaterial

![Untitled](Three%20JS%200d67735b9e484e54a46b2e559a27b606/Untitled%205.png)

---

# Textures

- Textures are pre-made and pre-loaded image resources that can serve as “skins” for meshes.
- Each geometry supports different numbers of textures
    - 1 - 6 textures for a cube (1 per face)
    - 1 - 2 for cones
    - 1 - 3 for cylinders
- Traditionally, rendering engines have much better performance when you use Texture Altases ([https://en.wikipedia.org/wiki/Texture_atlas](https://en.wikipedia.org/wiki/Texture_atlas))
    - because instead of loading hundreds of small resources, you load many
    - and can then include a small amount of data on the side that describes the atlas mapping of each texture
- in 3JS we use texture loaders to load external image resources
    - can manage the loading using a LoadingManager object, with event subscriptions (onLoad)
    - or can pass a callback to the loader
- Textures can be very performance heavy, and the cost depends on the dimension of the texture/image.
    - this is because in ThreeJS, textures take $w * h * 4 * 1.33 \;bytes$ of memory, so even though an image is compressed to be small, a 3024 x 3761 image would then take 60 mb of memory.

### Filters & Mipmaps

- When dealing with 3D rendering, certain artifacts occur when we render textures with high pixel detail in very small sizes.
    - Not all the detail can fit, and we must cut detail and display something that would be the closest approximation to the texture.
    - This is usually achieved by averaging pixel neighbours to find the average color, but that’s an expensive calculation
        - So, GPUs accelerate this through what are called MIPMAPS
- Mipmapping is a technique where copies of the texture are created, each copy (called a “mip”) being 1/2 as tall and 1/2 as wide, being drawn smaller and with less detail, approximating the larger texture.
    - This means that the GPU can then choose between all these mips to find the best fit to the size of the object being rendered.
        - Why use a 16x16 texture on a cube that’s 2x2?
    - The ‘best fit’ comes from filtering:
        - magFilter property to either **************nearest************** or ************linear************ for when the texture is drawn LARGER than the original size.
        - minFilter for texture drawn smaller than original
            - Filtering picks arbitrary pixels from the texture to “blend them” to achieve a lower resolution.

---

# Lights

- Pretty obvious what “lights” are meant to do - light up a scene. There are many different types of lights that do different things.
- AmbientLight
    - not directional, does not “cast shadows” (because it does not have a direction)
    - creates a flat light, illuminates ALL objects equally
        - $color = matColor * lightColor * lightIntensity$
- HemisphereLight
    - takes 2 colors, sky and ground and creates “global” object lighting based on the orientation of objects
- DirectionalLight
    - represents “the sun”
    - is not a “point”, thus the light that comes from it represents an infinite plane of light creating parallel rays
    - requires 2 3D coords, a position for the light, and the “target” it points to.
- PointLight
    - creates a point that light emits from, and creates rays of light from all directions
        - think of “lightbulb”
    - has a ********distance******** prop, when 0 is infinite, otherwise has a limit
- SpotLight
    - point lights that shine in a cone, so it has a target
- RectAreaLight
    - represents a long fluorescent light
        - only works with Standard / Physical materials (PBRs)
    

<aside>
⭐ physicallyCorrectLights / renderer.useLegacyLights

- is a WebGL setting that changes the props of lights to use Power (Watts as measured in Lumens), and a decay (2 = realistic)
</aside>

---

# Shadows

- are complicated, there are many different solutions to “casting” shadows.
- by default, 3JS uses ***********shadow maps***********
    - for every light that casts shadows, objects marked to cast shadows are rendered from the POV of the light
    - ex. 20 objects + 5 lights, each object and light cast shadows.
        - all 20 objects are drawn ONCE for EACH light, thus - they are drawn $draws = nLights + 1$, because they are drawn/rendered an extra time incorporating all previous draw data.’
    - thus, shadow maps are expensive but accurate.
- Other lighting methods include light maps or ambient occlusion maps to “pre-compute” lighting effects, which may leave artifacts or hints, but result in faster lighting.
- we can also use “fake shadows” by using shadow textures
    - we can create an empty object “floating” just above the ground, and attach the texture to materials to meshes.
    - Each object would be have a shadow mesh associated with it, an d we can “automate” these shadows by calculating the opacity of the shadow texture based on the distance of the object to the ground plane.
- 3 light types cast shadows:
    - Directional
        - Orthographic Camera
    - Point
        - 6 * Spotlight = a point cube
            - 1 draw per face
    - Spot
        - Perspective Camera
        - each requires turning a setting ON, and we must turn shadowMap ON in the WebGLRenderer
- for every shadow-casting light, a camera is created which defines the “domain” or region that shadows are calculated for. Thus, if the shadows become to large, they get clipped because they are outside the camera view.
    - also, shadow maps are done through textures as well - so the size of the rendered shadow texture depends on the size of the light-camera’s viewbox. Having a camera that is extremely wide then makes the shadows comparatively low resolution.
        - but we can change the shadow’s default width and height (512x512) to make it better - at a performance cost

---

# Fog

- is simulated, not volumetric
- creates fading for objects in the far plane
- FogExp2 is an object that simulates real-world fog because it fades exponentially
- materials have ***fog*** boolean attributes that allow toggling whether or not fog applies to those materials (default = true)
- 

---

# Render Targets

- is a way to select where things are rendered to, typically done to textures, so we can real-time render scenes onto a texture, to apply to other meshes
- shadow maps use render targets

---

# Primitives

- Box
- Circle
- Cone
- Cylinder
- Dodecahedron
- Extrude
- Icosahedron
- Lathe

- Octahedron
- Parametric
- Plane
- Polyhedron
- Ring
- Shape
- Sphere
- Tetrahedron

- Text
- Torus
- Torus Knot
- Tube
- Edges
- Wireframe

---

# Post Processing

- the application of some effect/filter to a rendered image, after the initial scene processing.
- typical process of rendering involves the 2D image rendering of an image into the browser’s Canvas.
    - we can apply post-processing effects by injecting effects to a target (render target), and rendering that target instead of the base scene.
- EffectComposer
    - Pass objects
    - call EffectComposer.render to a *********render target,********* applying each pass you specify
- Pass objects are post processing effects
    - ex. vignette, blurs, blooms, grain, hue, saturation, etc.
- EffectComposer works by creating TWO render targets
    - rtA & rtB
        - Scene → *Render Pass* → rtA
            - rtA → *Bloom* → rtB
            - rtB → *Film* → rtA
            - rtA → *Copy* → Canvas
- Passes has 4 options
    - enabled
    - needsSwap T/F
        - swap rTA and rtB after finishing this pass
    - clear
    - renderToScreen