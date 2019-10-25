# Opengl

A simple example showing how to utilize debug message callbacks (e.g. for detecting OpenGL errors):
```c++
void GLAPIENTRY
MessageCallback( GLenum source,
                 GLenum type,
                 GLuint id,
                 GLenum severity,
                 GLsizei length,
                 const GLchar* message,
                 const void* userParam )
{
  fprintf( stderr, "GL CALLBACK: %s type = 0x%x, severity = 0x%x, message = %s\n",
           ( type == GL_DEBUG_TYPE_ERROR ? "** GL ERROR **" : "" ),
            type, severity, message );
}

// During init, enable debug output
glEnable              ( GL_DEBUG_OUTPUT );
glDebugMessageCallback( MessageCallback, 0 );
```
