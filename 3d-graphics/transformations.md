Transformations
===============
## Homogeneous coordinates (in computer graphics)

Basically mapping all our 3D points in a 4D space by multiplying the three coordinates `x`, `y`, and `z` by a scale factor `w`, and appending this scale factor to the vector with the scaled coordinates, i.e.:
  ` (x, y, z) -> (x'w, y'w, z'w, w)`

To map the 4D coordinates back into 3D space, we divide the first three coordinates by the last component. 
Most of the time that factor will be 1 and we can see that we just find back our original coordinates. However it can take other values, for example `0`, which means that our three coordinates represents in fact a vector, or a "point to infinity".

## Perspective projection matrix

When using negative-z as the forward axis, the field of view `θ`, the aspect ratio `a`, the near and far plane values respectively `n` and `f`, and mapping to the range `[-1;1]`:
Let's define:
* `d = 1 / tan(Θ / 2)` -> `d` is the distance between our PoV and our projection plane, assuming its height is `2` and `y<sub>NDC</sub>` range is `[-1;1]`.
* `s = n + f / n - f` -> First step to map our near/far interval to the `z<sub>NDC</sub>` range. This scales from the size of `[-near;-far]` to the size of `[-1;1]`.  
* `t = 2nf / n - f` -> Second step to map our near/far interval to the `z<sub>NDC</sub>` range. This translate the scaled interval to the target, i.e. `[-near<sub>scaled</sub>;-far<sub>scaled</sub>]` to `[-1;1]`.

Pseudocode:
```
   let matrix = matrix4x4
   matrix = d/a 0  0  0
             0  d  0  0
             0  0  s  t
             0  0 -1  0
```

A couple notes:
* `d` is computed by using pythagoras on the rectangle triangle formed by `d`, half the projection plane, and the left (or right) frustum plane. Given a fov of `θ`, we thus have `1 / d = tan(θ / 2)`. Solving for `d`, we find `d = 1 / tan (θ / 2)`.
* The `-1` that seems randomly in there is used with homogeneous coordinates. Without this, `x` and `y` are expressed with `z`. Using homogeneous coordinates, and setting `w` to `z` (or here `-z` as we're looking down the negative z-axis), we can remove the non-linear part of `x` and `y` expressions.
