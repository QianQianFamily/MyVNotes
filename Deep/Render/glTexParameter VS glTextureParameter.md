# glTexParameter VS glTextureParameter

Don't mess them up，

When using glTexParameter, you need to bind the texture first.
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);

glTextureParameter is introduced in GL4.5, you can use the texture ID without binding it.
glTextureParameteri(texture, GL_TEXTURE_WRAP_S, GL_REPEAT);

See
https://stackoverflow.com/questions/26589683/access-violation-when-calling-gltextureparameteri-with-opengl-and-devil

