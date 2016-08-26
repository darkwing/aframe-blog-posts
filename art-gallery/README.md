[TODO]
<ul>
 	<li>Finalize dimensions, then come back to this post and ensure they're still correct</li>
 	<li>Take screenshots</li>
</ul>

[intro: some stuff about VR growing in popularity, there being a WebVR API, etc.]

A-Frame is an amazing Mozilla-led project aimed at providing web developers an easy way to create VR experiences that can be enjoyed both in the browser and VR devices.  A-Frame disarms the imposter syndrome that comes with learning VR coding by providing an easy to use, HTML-based API for creating shapes, animations, and interaction.  You can create a rich, interactive environment without writing a single line of JavaScript!

Let's create our first practical A-Frame environment: an art gallery that we can walk around!  This simple scene will help us learn the following:
<ul>
 	<li>The relationships a scene has with its children entities</li>
 	<li>How to use simple shapes like box to create walls</li>
 	<li>How to use images as textures</li>
 	<li>How to rotate and position entities within the room</li>
</ul>


##Getting Started

A-Frame provides a <a href="https://github.com/aframevr/aframe-boilerplate">boilerplate</a> for creating creating WebVR scenes.  Simply download the boilerplate and execute the following to get started:

[npm install code]

You'll see your browser open a new tab with a sample A-Frame scene.  Notice you can click and drag the scene to change the perspective; you can also use your keyboard's WSAD keys to get closer or further away from the sample scene.  Since we're looking to create our art gallery, however, we can delete all of the shapes from the <code>index.html</code> file and simply leave the <code>&lt;a-scene&gt;</code> element.

[TODO:  Add some text about <code>&lt;a-scene&gt;</code> and how it wraps everything]



##Creating the Room

The first step in developing the art gallery is creating the room: 4 walls, a floor, and a ceiling.  We'll use the <code>&lt;a-box&gt;</code> element to do just that:

```html
html
```

Dimensions are always measured in meters, so our room is <code>40</code> meters wide, <code>40</code> meters deep, and <code>10</code> meters high.  Let's have a look at each pieces of the code above:
<ul>
 	<li>The exterior walls [FINISH]</li>
 	<li>The ceiling's position is <code>0 9 0</code>, which elevates it to the top of the exterior walls</li>
 	<li>The floor's position is <code>0 0 0</code>, which keeps it below our viewpoint</li>
</ul>
We've also added a specific color to each entity within the room -- that will help us get a feel for the dimensions and where each piece of the room starts and ends, i.e. no gaps between the walls and the floor and ceiling.  Voila!  We've created our first WebVR room with just a few HTML elements!



##Room Textures and Images

Once we're content with the way our room is pieced together, we can use images to make the floor, walls, and ceiling look a bit more realistic.  Once we have the image textures we'd like to use, we'll add them as children <code>&lt;img&gt;</code> elements to one <code>&lt;a-assets&gt;</code> element:

```html
html
```

The role of the <code>&lt;a-assets&gt;</code> tag is to preload all media (images, audio, video) before first rendering the scene -- this provides for a more elegant rendering experience.  Each <code>&lt;img&gt;</code> should be given an ID for which it can be referenced by when we'd like to use it.

To add our images as textures to the walls, ceiling, and floor, all we need to do is add a <code>src</code> key and value to the <code>material</code> attribute of each box:

```html
html
```

We also added a <code>repeat</code> property which directs the image to repeat every <code>{x} {y}</code> meters.  The larger the repeat values, the more stretched the image texture will display.  With our sample images added, the room will go from a few colors to a scene that resembles a real room!

[img room with textures]



##Adding Art

A gallery wouldn't be complete without art so now we need to add some imagery to the walls.  Once we have images we'd like to use, we'll need to add them as <code>&lt;img&gt;</code> elements within <code>&lt;a-assets&gt;</code>, giving each a unique <code>id</code>, just as we did the wall textures:

```html
html
```

We'll use a series of <code>&lt;a-plane&gt;</code> elements to for the art.  Each <code>&lt;a-plane&gt;</code> element will use the <code>material</code> attribute's <code>src</code> key and value to set the image as the plane's texture.  Here's one simple example of placing an image on the wall directly in front of us:

```html
html
```

Let's quickly examine the element above:
<ul>
 	<li>We set a <code>width</code> and <code>height</code> for the plane (the image will stretch if not [WHAT TERM IS IT?]</li>
 	<li>We set the <code>material</code> attribute's <code>src</code> value to the <code>id</code> of the desired image within <code>&lt;a-assets&gt;</code></li>
 	<li>We position the plane up against the wall via the <code>position</code> property using <code>x y z</code> format:
<ul>
 	<li><code>x</code> is <code>0</code> to position the image straight ahead of us</li>
 	<li><code>y</code> is <code>4.5</code> to position the top of the image roughly half-way up the wall</li>
 	<li><code>z</code> is one half the total size of the room, minus <code>0.01</code> meters to avoid z-fighting (meaning two images at the exact same z position, thus creating an undesired clipping effect)</li>
</ul>
</li>
</ul>
Adding an image straight ahead of the viewpoint is easy, so now let's add an image to the left and right of our first image:

```html
html
```

The only change aside from the image to use is a change in the <code>position</code> attribute's <code>x</code> value; negative value moves the image to the left, positive to the right.

Placing images on the left, right, and back wall will require us to introduce a new attribute to each plane: <code>rotation</code>.  The <code>rotation</code> attribute, like <code>position</code>, accepts 3 space-separated values for <code>x</code>, <code>y</code>, and <code>z</code>, but in this case represents rotation in degrees.  Placing images on the left wall will require a rotation of <code>0 90 0</code>, the right requires <code>0 -90 0</code>, and the back wall panes require rotation of <code>0 180 0</code>:

```html
html
```

Now when you move around the room using the WSAD keys and your mouse, you'll see images on all sides of the room!

[closing]
