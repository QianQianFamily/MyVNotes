# glsl_texture

texture2D
texture2D 在opengl 3.3过时了，之后使用 texture

texture
做一个纹理读取，纹理坐标是 normalized 坐标【0，1】， 具体的读取可能会涉及到多个像素插值得到返回的结果。


texelFetch
读图片的一个像素，坐标是texel space, [0, size]的整数， 它不会读多个值然后插值。