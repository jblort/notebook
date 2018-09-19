Quaternions
===========

## Definition

4D vectors that represent a rotation around an arbitrary axis. Their main usage is to avoid the gimbal lock issue that stems from Euler Angles and the order of applications of the different rotation components.
They also can be easily interpolated, making for predictable and smooth rotation effects.

Formally, a quaternion is defined as:

    q = q0 + q1 * i + q2 * j + q3 * k

With the following relation:

    ijk = -1

It's useful to note the following relations as well:

    ij = k, ji = -k
    jk = i, kj = -i
    ki = j, ik = -j

This shows that quaternion products of `i`, `j`, `k` behave like the cross product.
It's useful to compare quaternions to complex numbers. Quaternions are to numbers in |R^3 what complex numbers are to real numbers.

A quaternion is composed of a real part (the scalar `w`) and an vector part.

Given a (normalized) axis and an angle, the corresponding quaternion rotation is defined as:

    sin_a = sin (angle / 2)
    cos_a = cos (angle / 2)
    qx = axis.x * sin_a
    qy = axis.y * sin_a
    qz = axis.z * sin_a
    qw = cos_a


## Operations

Quaternions aren't used as is, but an intermediary representation to manipulate and combine rotations in an easy way.

### Conjugate

The conjugate of a quaternion (similar to the conjugate of a complex number) is simply: 

    q^* = (-q.x, -q.y, -q.z, w)

That is, the vector (or imaginary part) is negated, and the scalar kept as is.

### Normalizing a quaternion

In a way similar to vectors, quaternions are normalized by computing their norm as such:

    n_q = || q || = sqrt ( q * q^* )

Then the scalar part and vector part are divided by the norm.

    normalize ( q ) = ( q.x / n_q,
                        q.y / n_q,
                        q.z / n_q,
                        q.w / n_q) 

### Inverse of a quaternion

When the quaternion is a unit quaternion, the inverse is simply the conjugate.

Otherwise, the inverse is as follow:

            q^* 
    q^-1 = —————
           |q|^2  

### Multiplying quaternions

This gives us the combined rotation of these quaternions

Formally:

    qr = q1.q2
       = ( w1.v2 + w2.v1 + v1 x v2, w1.w2 - v1.v2 )

with 

    v1 = (x, y, z) of q1
    v2 = (x, y, z) of q2
    w1 = w         of q1
    w2 = w         of q2

and `.`, `x`, respectively the dot and the cross products.

An optimisation:

    xr = w1*x2 + x1*w2 + y1*z2 -z1*y2
    yr = w1*y2 + y1*w2 + z1*x2 -x1*z2
    zr = w1*z2 + z1*w2 + z1*x2 -x1*z2
    wr = w1*w2 + x1*x2 + y1*y2 -z1*z2


### Rotating a vector

A quaternion can be used directly to rotate a vector (in homogeneous coordinates) as such:

    v' = q * v * q^-1
