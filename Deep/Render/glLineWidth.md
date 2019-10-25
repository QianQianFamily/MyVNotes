# glLineWidth

1. Wide line是一个deprecated feature.
2. 只有 1.0 的宽度是规范支持的。
3. Line渲染时有两种模式 Aliased和Smooth， 通过glEnable(GL_LINE_SMOOTH)来打开，默认是不打开的。
4. 打开之后，即使设置宽带是1， 线也会占用周围的像素。 放大看是阶梯状的，进一步打开Blend, 视觉效果要平滑一些。
```c++
        pContext->glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
        pContext->glEnable(GL_BLEND);
        pContext->glEnable(GL_LINE_SMOOTH);
        pContext->glHint(GL_LINE_SMOOTH_HINT, GL_NICEST);
```
5. 可用通过接口查询设备目前支持的线宽：
  ```c++
          float lineWidth[2];
        pContext->glGetFloatv(GL_LINE_WIDTH_RANGE, lineWidthRange);
        std::cout << lineWidthRange[0] << lineWidthRange[1] << std::endl;
 ```
     规范中说， GL_LINE_WIDTH_RANGE 是旧的称呼，新代码应该使用 GL_ALIASED_LINE_WIDTH_RANGE, GL_SMOOTH_LINE_WIDTH_RANGE。
    本机(NVIDIA Quadro M1200)测试结果：
    CompatibilityProfile GL_ALIASED_LINE_WIDTH_RANGE : [0.5, 10] 有效
    CoreProfile GL_ALIASED_LINE_WIDTH_RANGE : [1, 10] ,但是无论怎么设都只有1个像素宽。
    CoreProfile GL_SMOOTH_LINE_WIDTH_RANGE : [1,1] 

6. 为了更好的兼容性，建议通过geometry shader生成triangles的方式来画线。