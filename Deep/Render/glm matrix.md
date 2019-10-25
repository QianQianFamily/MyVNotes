# glm matrix

```c++
        glm::mat4 matrix = glm::translate(glm::mat4(), t);
        matrix = glm::rotate(matrix, glm::radians(yaw), yaxis);
        matrix = glm::translate(matrix, -t);
```

等价于
TransformMatix(t)* RotationMatrix( yaw ) * TransformMatrix(-t)
先 位移 -t, 再选择， 再位移 t, 变换顺序和书写顺序是反着的。