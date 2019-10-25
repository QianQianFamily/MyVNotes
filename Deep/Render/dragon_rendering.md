# dragon_rendering

1. Download the dragon model :
http://graphics.stanford.edu/data/3Dscanrep/

2. Rendering problem:
![image_issue1](_v_images/image_issu_1562768095_20722.png)

Solution : Enable Face Full and Cull back face.

![](_v_images/1562768309_18700.png)

Solution: Enable Depth test

![](_v_images/1562768472_30834.png)

Fixed.

Try to cull back face and abs(normal*light_direction)
![](_v_images/1562768876_11412.png)


Questions:
What is front face?
glFrontFace  . The initial value is GL_CCW.
Tips:

In a scene composed entirely of opaque closed surfaces, back-facing polygons are never visible. Eliminating these invisible polygons has the obvious benefit of speeding up the rendering of the image