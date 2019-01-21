Shader and shader modifiers constructs in SceneKit
==================================================

## Creating a grid of dots

An easy way to create a "grid of dots" thanks to shader modifier is to use a simple `SCNPlane` with a uniform color (e.g. white), then use a simple shader modifier as follows.

    uniform float DOT_DIST = 6.0; // Centimeters, distance between each dots on the surface.
    uniform float DOT_SIZE = 0.02; // Meters, sizes of the dots on the grid

    // Get the position of the current surface in world coordinates.
    vec4 planePos = u_inverseViewTransform * vec4(_surface.position, 1.0);

    // Then, compute the closest intersection of the virtual grid of dots. Each dot will sit on an intersection of this grid.
    vec2 closestGridPoint = vec2(round(planePos.x * 100.0 / DOT_DIST) * DOT_DIST, round(planePos.z * 100.0 / DOT_DIST) * DOT_DIST);
    vec2 gridCoord = vec2(closestGridPoint.x / 100.0, closestGridPoint.y / 100.0);

    // Compute the distance of our current surface to the closest grid intersection.
    vec2 posOnPlane = vec2(planePos.x, planePos.z);
    float distToGridPoint = length(posOnPlane - gridCoord);

    // Finally, discard any fragment that doesn't end up within the surfaces of the dots.
    if (distToGridPoint > DOT_SIZE) {
      discard;
    }

Breaking it down, we first get the position of the current "surface" in SceneKit's term, which is to say the current fragment. We use the provided `_surface.position` which is expressed in view space.
We then convert it to world space thanks to another provided value, the `u_inverseViewTransform` which has already been computed for us.

The next step is basically the gist of this shader. We compute the position of the closest "grid point", i.e. the closest intersection of our grid. Our grid square have the size `DOT_DIST * DOT_DIST`.
We find the 2D coordinates of the closest intersection to our current fragment, then determine the distance between this fragment and this intersection.

Finally, we simply discard any fragment which lies outside of the circles defined by the grid points and our desired dot radius (i.e. `DOT_SIZE`).
