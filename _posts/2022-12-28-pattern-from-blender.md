---
layout: post
title: Making a Pattern from Blender
date: 2022-12-28 20:45:00 +0100
categories: blog computer-assisted
---

For the [Hedeby Quiver]({% post_url 2022-12-28-hedeby-quiver %}, I decided to try to generate the pattern myself, with 3d-modeling and UV coordinate maps, rather than building on the approach taken by the Leather Working Reverend.

I was encouraged in the ambition by the [Seams to Sewing Pattern](http://thomaskole.nl/s2s/) plugin by Thomas Kole. So, building on the documentation pages for the plugin, I set out learning enough blender to pull off the project.

Here's how that went:

# Modeling the quiver

<figure class="figure">
<img src="{{ '/assets/img/blender/01-startstate.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Starting state of a new Blender project.
</figcaption>
</figure>

First, remove the cube (select it, and use `x` or an appropriate menu). Next, we will add a _Capsule_ (and build the quiver as a chopped off and drawn out capsule shape).

<figure class="figure">
<img src="{{ '/assets/img/blender/02-capsule.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Cube is removed, we've put in a capsule instead.
</figcaption>
</figure>

To get the sizing we want from the capsule, let's:
* rotate it by 90º around the Y-axis to stand it upright
* scale it by 0.1 along the Y- and Z-axes to squeeze it
* translate it by 2m along the X-axis to stand it on top of the origin plane.

<figure class="figure">
<img src="{{ '/assets/img/blender/03-mapped.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Slender capsule shape standing on the origin.
</figcaption>
</figure>

Now, it's time to convert this from an _Metaball_ to a _Mesh_ so that we can go in and chop it up into the pieces we need.

Select the capsule, go to the _Layout_ context and the Object menu. Find the Convert submenu and choose to convert it to a _Mesh_.

At this point, we _could_ try to do something to increase the polygon count and get a smoother shape -- I didn't. Instead, now that we have a mesh it's time to go in and carve out the pieces we want to keep.

I used the _Measure_ tool to figure out where 0.7m tall would fall on this shape, and used that to guide my cutting of the shape. Once you know where to cut, the process I followed is to select vertices _above_ my designated cut and remove them (and everything defined by or connected to them).
I discovered doing this that I would need to subdivide the edges near my cut (so that I could cut halfway between two rows of vertices) and needed to rotate the mesh and add to my selection to get the things behind the object as well.

Hold shift and keep selecting to get the things you need.

<figure class="figure">
<img src="{{ '/assets/img/blender/04-subdividing.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Just before subdividing to find the cut edges.
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/05-subdivided.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Edges subdivided.
</figcaption>
</figure>

Speedy removal can be done by selecting in Face Select mode, and delete using the `X` button and choosing _Face_ removal.

<figure class="figure">
<img src="{{ '/assets/img/blender/06-select.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Selected a bunch of faces.
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/07-delete.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Selected faces deleted
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/08-select.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Select the rest of the faces (from the other direction).
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/09-quiver.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
The _finished_ quiver shape (next is not about _sculpting_ any more)
</figcaption>
</figure>




# Carving out a pattern

To carve out a pattern, we will go in and create _Seams_. There should be a way to then _use_ the resulting seams for pulling the shape apart, but since I couldn't make it work, we will instead separate the seam edges ourselves afterwards.

Use the _Zoom_ and _Pan_ controls on the right to get a close enough view of the mesh to pick out the details you need.

When doing this, I quickly realized there are some clusters of vertices that are very tightly connected, so maybe to make it all easier we will start by _Merging by distance_. Select everything (with `A`), and go to Mesh -> Merge -> By Distance. Then open up the small popup block bottom right labeled _Merge by Distance_ to change the settings for merging by distance. Click the `>` symbol to open it up, and start increasing the _Merge Distance_ until the little text-information at the bottom tells you that some (maybe 60 or so) vertices have been merged. 0.1m works for me.

<figure class="figure">
<img src="{{ '/assets/img/blender/10-merged.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Here's the state after nearby vertices have been merged together.
</figcaption>
</figure>


Pick _Vertex Select_ mode, and go through selecting vertices where you want seams between the pieces, and then use the _Vertex_ -> _Connect Vertex Path_ (or `J`) to make sure you have edges everywhere you need them. Once you have all the edges in place, go to _UV_ -> _Mark Seam_.

<figure class="figure">
<img src="{{ '/assets/img/blender/11-seamstart.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Starting one of the Hedeby quiver seams.
</figcaption>
</figure>

Keep going, and subdivide the mesh if you need to. Most things you can do with `J` (connect vertex path), but some things may need for you to select, remove (with `X`) and then reintroduce faces (select vertices, press `F` to create a face spanned by them).

<figure class="figure">
<img src="{{ '/assets/img/blender/12-markseam.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Selected a path and go to UV -> Mark Seam
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/13-tothetop.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Follow the paths, mark the seams, all the way to the top.
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/14-allseams.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
All seams for the Hedeby quiver in place.
</figcaption>
</figure>

Now it is time to cut this surface up into the separate surface patches we need. Choose Edge Selection mode, and select any one of the Seam marked edges. Then _Select_ -> _Select Similar_ -> _Seam_ to select all the seam edges. Then go for _Mesh_ -> _Split_ -> _Faces by Edges_ to cut the pieces apart.

You can check your work by selecting anything in one component, and pressing `L` to select the entire connected component. If you get just your separated patch, you're in good shape.

<figure class="figure">
<img src="{{ '/assets/img/blender/15-selectseam.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Select all the seam edges.
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/16-separate.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Separate Faces by Edges.
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/17-selected.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
One connected component selected.
</figcaption>
</figure>

Now we are getting close to where we can use the UV Layout engine to create pattern parts for a concrete sewing pattern for the quiver.

To be able to track how the UV coordinate map interacts with the shape, we will prepare the setup a little bit first. We will need to connect UV coordinates to the surface of the model somehow, so we will start by going to the _UV Editing_ context. On the left hand side, do _Image_ -> _New_ and choose _Generated Type_ to be something like _Color Grid_. You should see a bunch of colors and letters and numbers show up.

<figure class="figure">
<img src="{{ '/assets/img/blender/18-uvgrid.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
The UV Coordinate Map grid to test coordinate mapping.
</figcaption>
</figure>

Next, we move to the _Shading_ context to connect this UV map to the object itself. In the bottom left panel (with the grid), find the button that looks like this: <img src="{{ '/assets/img/blender/19-button.png' | absolute_url }}" height="12pt" />. Click it and choose the color grid you put in in the earlier step.

Next, in the bottom right pane, find the button that looks like this: <img src="{{ '/assets/img/blender/20-button.png | absolute_url }}" height="12pt" />. Click _New_ to create a new Material definition for the surface.

Then, still in the bottom right panel, go to _Add_ -> _Input_ -> _UV Map_ to create a UV Map node. Place the node somewhere to the right of the other boxes, and connect its output to the _Base Color_ connection point in the middle box, by clicking on the little dot where it says UV and dragging over to the dot next to Base Color.

<figure class="figure">
<img src="{{ '/assets/img/blender/21-uvnode.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Here's how we create a UV node.
</figcaption>
</figure>

<figure class="figure">
<img src="{{ '/assets/img/blender/22-connected.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Connecting the nodes to each other.
</figcaption>
</figure>

The quiver still does not look terribly exciting, but that's because we have not yet connected the UV coordinate map to the mesh itself. So let's go to _Edit Mode_ in the top right panel (where we see the quiver model floating around) and let's create a UV coordinate map.

Press `A` to select the entire mesh, and then press `U` (or go to the _UV_ menu), and choose _Unwrap_.

You will get an error message about non-uniform scales, which turns out to be because we did a bunch of rescaling operations - but didn't quite _finish_ the operations early on. Switch to _Object Mode_, click on the mesh to select it, and press Ctrl+`A` and choose _Scale_ (or go to _Object_ -> _Apply_ -> _Scale_) to apply our earlier transformations.

<figure class="figure">
<img src="{{ '/assets/img/blender/23-fixscale.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Applying the scale so that we can successfully unwrap the mesh onto the UV coordinate plane.
</figcaption>
</figure>


Then back to Edit Mode, press `A` to select the entire mesh, and `U` to choose _Unwrap_. Switch to _UV Editing_ context to see the effects of doing this - you can now see the unwrapped mesh laid out on the UV plane to the left. If you find the four balls to the far right on the menu bar of the right hand panel and click the _Material Preview_ or the _Render Preview_ viewing mode, you can see the pieces of your mesh color in according to where they are in the UV plane.

<figure class="figure">
<img src="{{ '/assets/img/blender/24-uvlayout.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Seeing the full UV layout.
</figcaption>
</figure>

You should now be able to select something (vertex, edge, face, anything) on the UV plane to the left, and use `L` to select an entire connected component. You can then maneuver this around the UV plane (use `G` to move, or `R` to rotate, moving the mouse to actually move and rotate).

Also helpful is to go, in the left hand (UV plane) panel, to the _Overlay_ button and select the Display Stretch option. For things like leather work, it's probably more helpful to use the _Area_ display mode than the _Angle_ display mode - to see where the mesh is stretched out the most.

<figure class="figure">
<img src="{{ '/assets/img/blender/25-displaystretch.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
How to display the amount of stretch in a UV mapping.
</figcaption>
</figure>


You can also at this stage in the left hand panel go to _UV_ -> _Minimize Stretch_ to see if it can come up with a better mapping of the pieces for you. Roll the scroll wheel _down_ as far as possible to relax the mesh as much as you can.

<figure class="figure">
<img src="{{ '/assets/img/blender/26-minimizestretch.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
How to minimize the stretch in a UV mapping
</figcaption>
</figure>

If you are ambitious, you can start using the three hand-shaped tools at the bottom to try to reduce the stretch (get as close to blue as possible), especially for the high-curvature piece to the left. Rescale it (select something, then `L` for the entire thing, then `S` and move the mouse to try different scales) and then start moving things around where it's still not blue. Periodically select the component (with `L`) and do _Minimize Stretch_ again to see if it gets better. You will have to change the shape yourself -- _Minimize Stretch_ only moves the interior pieces around for you.

<figure class="figure">
<img src="{{ '/assets/img/blender/27-modified.png' | absolute_url }}" class="figure-img img-fluid rounded" />
<figcaption class="figure-caption">
Final state before export.
</figcaption>
</figure>


Once you're at a state where you are happy with the design, you can export the resulting UV coordinate map (and then use it as a sewing pattern). In the left hand panel, choose _UV_ -> _Export UV Layout_. In the save file dialog, make sure you select _All UVs_, and pick a nice export format (such as SVG). Pick directory, filename, and export it.

The resulting SVG you can import into eg Illustrator or something else that you can print from, or instruct laser cutters, or however you want to use the pattern you put together.

My Blender render of the intended final outcome, with leather textures in different colors to show the composition, can be seen here:

![]({{ '/assets/img/blender/28-render.png' | absolute_url }})







