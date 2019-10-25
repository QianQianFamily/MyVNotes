# Apex_camera_rotate_pan

## Rotate
1. 将BoundingBox的中心移到原点，得到位移矩阵M1。
2. 要绕当前相机空间的Y轴旋转， 先把Y轴变换到BoundingBox本地坐标， Inverse(ViewMat)*Y_Axis得到旋转轴。
3. 得到旋转矩阵 M2
4. 再把BoundingBox移动到原初 ， M3
5. 最后更新相机矩阵 ViewMat*M3*M2*M1 （* vertex）
意义为：
先移动到原点，再绕一个轴旋转，再移回原初，再作view空间变换，旋转轴变换后就是当前的Y轴。
（X轴转动同理）

```c++
void ApexControl::rotate(CameraControl* pCamera,float deltaX, float deltaY)
{
    auto center3 = pCamera->getCurrentBox().center();
    auto currentViewMat =  Global::renderWindow().getViewMatrix();
    auto currentViewMatInverse = glm::inverse(currentViewMat);

    if( abs(deltaX) > 1 )
    {
        float angle = 2*deltaX*360.0f/Global::renderWindow().getWinWidth();

        auto up = currentViewMatInverse*Vec4(0,1,0,0);

        auto identifyMat = glm::identity<Matrix4>();
        auto centerToOrigin = glm::translate(identifyMat, -center3);

        Vec3 up3 = Vec3(up.x,up.y,up.z);
        auto rotMat = glm::rotate( identifyMat, glm::radians(angle), up3);

        auto originToCenter = glm::translate(identifyMat, center3);

        auto finalMat = currentViewMat*originToCenter* rotMat *centerToOrigin ;

        Global::renderWindow().setViewMatrix( finalMat );
    }

    //else
    if( fabs(deltaY) > 1)
    {
        float angle = 2*deltaY*360.0f/Global::renderWindow().getWinHeight();
        auto currentViewMat =  Global::renderWindow().getViewMatrix();
        auto right = currentViewMatInverse*Vec4(1,0,0,0);


        auto identifyMat = glm::identity<Matrix4>();
        auto centerToOrigin = glm::translate(identifyMat, -center3);

        Vec3 right3 = Vec3(right.x,right.y,right.z);
        auto rotMat = glm::rotate( identifyMat, glm::radians( angle) , right3);

        auto originToCenter = glm::translate(identifyMat, center3);

        auto finalMat =  currentViewMat*originToCenter* rotMat* centerToOrigin ;

        Global::renderWindow().setViewMatrix( finalMat );
    }
}
```


## Pan
首先计算 鼠标移动距离的NDC坐标， dx，dy
然后 生成一个x,y方向的位移矩阵， 然后乘上当前的投影矩阵
 projmat*viewmat*vertex = [x,y,z,w]
 再左乘位移矩阵，以第一行为例，
[1,0,0,dx] * [x,y,z,w] = x + dx*w
除以w后得到 x/w + dx
x/w 就是以前的NDC的x坐标，现在偏移了dx.

```c++
void ApexControl::pan(CameraControl* pCamera,float deltaX, float deltaY)
{
    float offsetX = 2*deltaX/Global::renderWindow().getWinWidth();
    float offsetY = 2*deltaY/Global::renderWindow().getWinHeight();
    auto identifyMatrix = glm::identity<Matrix4>();
    auto offsetMatrix = glm::translate( identifyMatrix, Vec3(offsetX,-offsetY,0) );
    auto finalMat = offsetMatrix * Global::renderWindow().getProjMatrix();
    Global::renderWindow().setProjMatrix( finalMat );

}
```