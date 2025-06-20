# Problem Parking Lot

## Data Science Learning

- learning what effect really means, understanding motivations behind finding the effect size instead of just using abosolute average difference to compare things, understanding comparing groups vs comparing variables.
-

## Synapse Flux

### 3d modeling in blender

-

### react three fiber

#### Immediate problems

using typescript is bothering the demo code I need to learn to set up proper type definitions for my code. there is a copilot converation about this.

- I don't know why we need to useRef to animate

_task:_ recreate scene without looking at the starter code.
_problem list:_

- didn't know how to position the box and sphere just the same as they had been without knowing coordinates.

  - for now I just used the experience file as-is it only involves a transleation of one of the meshes on the x by 2 and then the plane gets rotated -90 degrees and translated down a few units.

- didn't really know all the parameters available for directional lighting

  - postponing learning that api until I need to play around with lights more specifically.

- didn't know whether to add the args to the boxgeometry or the position attribute to the parent mesh

- receive shadow not working for game demo

  - this turns out to be a setting that also has to be enabled on the3 Canvas element.

- _I have trouble positioning things in 3d space with just an array of x y z coordinates_

- _I am learning rapier_

- I need to nkow about transformer architecture

  - I don't know what kinematic position is

- forgot the syntax to import threejs, and I need to remember what the glob i mport significance is

  - import \* as THREE from 'three'

- learned a new pattern for setting the scale of the mesh and having meshes share geometries, hope I remember!

_I don't know what StrictMode Component does other than that it renders the component twice I think which can cause duplicate content_

_I don't remember why the canvas was created at the top level or why the camera belongs to that and not inside the experience_

_I forgot how to think about field of view, other than that it is the amount the camera can see, like we can see pretty wide with peripheral vision. is fov for cameras horizontal or vertical? 45 degrees seems to be a good norm_

_the camera is at [4,0,4] which I assume is x,y,z. is the coordinate system one that has z forward backward or up down? I think z is forward backward and y is up down, so this is a camera at ground level moved away from the orgin 4 on each side_

_how do I import my own mesh from blender into the scene for my threejs project?_
_orbit controls?_
_wasd movement within the scene?_
_for the environment, how many meshes should it be constructed from? is there a scaffolding type thing I should be doing?_

- enabling orbit controls -
- remembering how I put the cube here -
  - best I can remember (10 mins)
    - I created an Experience component
    - I created a mesh object and react three fiber does a lto of the work behind the scenes
    - I had to set up a camera object for the scene I think
    - the mesh object had to have a material and a geometry, from what I remember by making them children react three fiber was able to use their names to set up a scene graph and correctly parent them according to the structure of the jsx. I'm a bit fuzzy abut this was cool.
    - react three fiber used a lot of sensible defaults so I didn't have to do as much boilerplate as I did when we were doing the lessons and setting these things up originally
  - interpreting what I can from the code (10 mins):
    - first off this is typescript, cool
    - canvas at the top level under the root node whic is created in react with a reference to the dom by react functions
      - I need to internalize this pattern and what is called
      - camera is at canvas level
      - expereince is a child of canvas
        - experience is a simple arrow function with no arguments that has declarative elements like a directional light and a mesh object in it which does in fact have a box geometry and a mesh standard material
        - the directional light has a position and intensity attributes, and the mesh has scale and rotation at the parent level and the material only has the color which is blue.
    -

## linear algebra project (I don't have one right now)
