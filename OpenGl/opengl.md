## OpenGL框架基本类

  Android 框架中，`GLSurfaceView` 是使用 OpenGL 绘制的图形的视图容器，而 `GLSurfaceView.Renderer` 可控制该视图中绘制的图形。

### 1  GLSurfaceView

  此类是一个 `View`，对于全屏或接近全屏的图形视图，选择`GLSurfaceView`合理一些。此外，如果希望将 OpenGL ES 图形整合到其布局中的一小部分，也可以考虑使用 `TextureView`。SurfaceView也可以用于OpenGL的视图容器，但是需要编写的代码比较多，暂不推荐。

### 2  GLSurfaceView.Renderer

  此接口定义了在GLSurfaceView中绘制图形所需的方法。将此接口的实现类通过 `GLSurfaceView.setRenderer()` 与 `GLSurfaceView` 实例关联起来。`GLSurfaceView.Renderer` 接口要求实现以下方法：

- `onSurfaceCreated()`：系统会在创建 `GLSurfaceView` 时调用一次此方法。通常用来设置仅需发生一次的操作，例如设置 OpenGL 环境参数或初始化 OpenGL 图形对象。
- `onDrawFrame()`：系统会在每次重新绘制 `GLSurfaceView` 时调用此方法。是将图像绘制到GLSurfaceView的主要方法。
- `onSurfaceChanged()`：系统会在 `GLSurfaceView` 几何图形发生变化（包括 `GLSurfaceView` 大小发生变化或设备屏幕方向发生变化）时调用此方法。例如，系统会在设备屏幕方向由纵向变为横向时调用此方法。

### 3 RenderMode

  GLSurfaceView有两种渲染模式：

1. RENDERMODE_CONTINUOUSLY：自动连续调用GLSurfaceView.Renderer去绘制，绘制时会执行GLSurfaceView.Renderer的onDrawFrame()方法；
2. RENDERMODE_WHEN_DIRTY：surface在创建后调用一次；或者在开发者主动调用MyGLSurfaceView的requestRender时才会调用GLSurfaceView.Renderer去绘制（执行onDrawFrame()方法）；


