3D graphics troubleshooting
===========================

## Model, geometry, triangles are not visible

- Are the normals facing the correct side?
- Is the rendering done double sided?
- Is it culled by the current frustum?
- Is it in the current camera field of view/frustum?
- Is the geometry complete and consistent?
- Is there transparency involved with erroneous values? (i.e. conversion from opacity to transparency without inverting values)

