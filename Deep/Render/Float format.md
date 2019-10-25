# Float format

https://en.wikipedia.org/wiki/Minifloat


Vertex data and Normalisation[https://gamedev.stackexchange.com/questions/9792/opengl-vertex-attributes-normalisation]
'''
It's all about saving space. And with vertex attributes, less space can mean higher performance (if you're vertex transfer bound).
Colors typically don't need much more than 8-bits per component. Sometimes you need 16-bits, if it's a HDR light value or something. But for surface characteristics (which is what most vertex attributes are), 8 bits is fine. So unsigned normalized bytes are a good vertex format.
Texture coordinates do not need 32-bits of floating-point precision. A 16-bit value from [0, 1] is sufficient. So normalized unsigned shorts are a reasonable vertex format.
Normals never need 32-bits of precision. They're directions. 8-bit signed normalized bytes tend to be a bit small, but 10-bit normalized values are good enough most of the time. OpenGL (3.3+) even allows you to use 10-bit normals via a 10/10/10/2 bit packed format, stored in a single 32-bit unsigned integer.
You can even play games with vertex positions, if you find yourself in grave need of more memory.
'''

Normalized Interger(https://www.khronos.org/opengl/wiki/Normalized_Integer)