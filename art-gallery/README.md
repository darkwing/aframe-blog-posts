## ToDo
- Finalize dimensions, then come back to this post and ensure they're still correct
- Take screenshots

[intro: some stuff about VR growing in popularity, there being a WebVR API, etc.]

A-Frame is an amazing Mozilla-led project aimed at providing web developers an easy way to create VR experiences that can be enjoyed both in the browser and VR devices.  A-Frame provides an easy to use, HTML-based API for creating shapes, animations, and interaction.  You can create a rich, interactive environment without writing a single line of JavaScript!

Let's create our first practical A-Frame environment: an art gallery that we can walk around!  This simple scene will help us learn the following:

- The relationships a scene has with its children entities
- How to use simple shapes like box to create walls
- How to use images as textures
- How to rotate and position entities within the room

## Getting Started

A-Frame provides a <a href="https://github.com/aframevr/aframe-boilerplate">boilerplate</a> for creating creating WebVR scenes.  Simply download the boilerplate and execute the following to get started:

[npm install code]

You'll see your browser open a new tab with a sample A-Frame scene.  Notice you can click and drag the scene to change the perspective; you can also use your keyboard's WASD keys to get closer or further away from the sample scene.  Since we're looking to create our art gallery, however, we can delete all of the shapes from the `index.html` file and simply leave the `&lt;a-scene&gt;` element.

[TODO:  Add some text about `&lt;a-scene&gt;` and how it wraps everything]

## Creating the Room

The first step in developing the art gallery is creating the room: 4 walls, a floor, and a ceiling.  We'll use the `&lt;a-box&gt;` element to do just that:

```html
html
```

Dimensions are always measured in meters, so our room is `40` meters wide, `40` meters deep, and `10` meters high.  Let's have a look at each pieces of the code above:


- The exterior walls [FINISH]
- The ceiling's position is `0 9 0`, which elevates it to the top of the exterior walls
- The floor's position is `0 0 0`, which keeps it below our viewpoint


We've also added a specific color to each entity within the room -- that will help us get a feel for the dimensions and where each piece of the room starts and ends, i.e. no gaps between the walls and the floor and ceiling.  Voila!  We've created our first WebVR room with just a few HTML elements!

## Room Textures and Images

Once we're content with the way our room is pieced together, we can use images to make the floor, walls, and ceiling look a bit more realistic.  Once we have the image textures we'd like to use, we'll add them as children `&lt;img&gt;` elements to one `&lt;a-assets&gt;` element:

```html
html
```

The role of the `&lt;a-assets&gt;` tag is to preload all media (images, audio, video) before first rendering the scene -- this provides for a more elegant rendering experience.  Each `&lt;img&gt;` should be given an ID for which it can be referenced by when we'd like to use it.

To add our images as textures to the walls, ceiling, and floor, all we need to do is add a `src` key and value to the `material` attribute of each box:

```html
html
```

We also added a `repeat` property which directs the image to repeat every `{x} {y}` meters.  The larger the repeat values, the more stretched the image texture will display.  With our sample images added, the room will go from a few colors to a scene that resembles a real room!

[img room with textures]

## Adding Art

A gallery wouldn't be complete without art so now we need to add some imagery to the walls.  Once we have images we'd like to use, we'll need to add them as `&lt;img&gt;` elements within `&lt;a-assets&gt;`, giving each a unique `id`, just as we did the wall textures:

```html
html
```

We'll use a series of `&lt;a-plane&gt;` elements to for the art.  Each `&lt;a-plane&gt;` element will use the `material` attribute's `src` key and value to set the image as the plane's texture.  Here's one simple example of placing an image on the wall directly in front of us:

```html
html
```

Let's quickly examine the element above:

- We set a `width` and `height` for the plane (the image will stretch if not [WHAT TERM IS IT?]
- We set the `material` attribute's `src` value to the `id` of the desired image within `&lt;a-assets&gt;`
- We position the plane up against the wall via the `position` property using `x y z` format:

- `x` is `0` to position the image straight ahead of us
- `y` is `4.5` to position the top of the image roughly half-way up the wall
- `z` is one half the total size of the room, minus `0.01` meters to avoid z-fighting (meaning two images at the exact same z position, thus creating an undesired clipping effect)

Adding an image straight ahead of the viewpoint is easy, so now let's add an image to the left and right of our first image:

```html
html
```

The only change aside from the image to use is a change in the `position` attribute's `x` value; negative value moves the image to the left, positive to the right.

Placing images on the left, right, and back wall will require us to introduce a new attribute to each plane: `rotation`.  The `rotation` attribute, like `position`, accepts 3 space-separated values for `x`, `y`, and `z`, but in this case represents rotation in degrees.  Placing images on the left wall will require a rotation of `0 90 0`, the right requires `0 -90 0`, and the back wall panes require rotation of `0 180 0`:

```html
html
```

Now when you move around the room using the WASD keys and your mouse, you'll see images on all sides of the room!  If you own an HTC Vive, you can even walk around the gallery yourself!

[closing]
