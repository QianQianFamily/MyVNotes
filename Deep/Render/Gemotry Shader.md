# Gemotry Shader

1. 一个GS可以输出多个Primitive,即包含多个EndPrimitive().
2. out的layout里面指定max_vertices，这个是一个GS里面所有Primitive的顶点数目上限，不是单个Primitive的顶点数目上限。