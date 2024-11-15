# 1. Create Window
## 1.1 创建窗口
创建一个窗口对象
```cpp
GLFWwindow* window = glfwCreateWindow(800, 600, "LearnOpenGL", NULL, NULL);
```
这个函数将会返回一个GLFWwindow对象，我们会在其它的GLFW操作中使用到

将窗口的上下文设置为当前运行环境的上下文(可用于切换窗口对象)
```cpp
glfwMakeContextCurrent(window);
```

## 1.2 创建视口
视口与窗口不同，视口定义了窗口上的一个区域，用于呈现最终需要输出的画面：
```cpp
glViewport(0, 0, 800, 600);
```
glViewport函数前两个参数控制窗口左下角的位置。第三个和第四个参数控制渲染窗口的宽度和高度（像素）

OpenGL幕后使用glViewport中定义的位置和宽高进行2D坐标的转换，将OpenGL中的位置坐标转换为你的屏幕坐标(clip -> viewport space)

## 1.3 准备引擎（渲染循环）
创建一个最简单的 “Engine”， while 循环
```cpp
while(!glfwWindowShouldClose(window))
{
    glfwSwapBuffers(window);
    glfwPollEvents();    
}
```

glfwSwapBuffers函数会交换颜色缓冲,
### 1.3.1 双缓冲
单缓冲的问题：每帧会被划分成两个部分：1.等待当前渲染流程结束 2. 将渲染结果呈现至屏幕上

双缓冲：可以利用 “并行”，使呈现图像与绘制图像并行进行

而 OpenGL 的单缓冲据说是：直接呈现缓冲上的内容，如果在单缓冲上绘制，速度慢下来就像是利用扫描线从左上角到右下角依次扫描呈现图像一样

## 1.4 释放资源
```cpp
glfwTerminate();
```