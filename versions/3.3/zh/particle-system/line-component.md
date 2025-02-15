# Line 组件

Line 组件用于渲染 3D 场景中给定的点连成的线段。Line 组件渲染的线段是有宽度的，并且总是面向摄像机，这与 billboard 组件相似。

属性| 功能
---|---
**texture**    | 线段中显示的贴图。
**worldSpace** | 线段中各个点的坐标采用哪个坐标系，勾选使用世界坐标系，不选使用本地坐标系。
**positions**  | 每个线段端点的坐标。
**width**      | 线段宽度，如果采用曲线，则表示沿着线段方向上的曲线变化。
**tile**       | 贴图平铺次数。
**offset**     | 贴图坐标的偏移。
**color**      | 线段颜色，如果采用渐变色，则表示沿着线段方向上的颜色渐变。

Line 组件接口请参考 [Line API](__APIDOC__/zh/#/docs/3.3/zh/particle/Class/Line)。
