# Ground Mirror Demo

地面反射效果演示

This is a demonstration of a ground mirror effect using Three.js.

---

[English](#english) | [中文](#中文)

## English

### 💡 Introduction

This project showcases a realistic ground reflection effect, often seen on wet or glossy surfaces. It goes beyond simple planar reflections by introducing distortions and blur, which can be dynamically controlled through a GUI. Users can also upload custom textures to see how they affect the reflection.

### 🚀 How to Run

Simply open the `index.html` file in a modern web browser that supports WebGL. No local server is needed.

### ✨ Features

A control panel built with `lil-gui` allows you to tweak the following parameters in real-time:

-   **Size X/Z**: Adjusts the width and length of the reflection plane.
-   **Position Y**: Controls the vertical position of the mirror.
-   **Blur**: Sets the blurriness of the reflection, simulating different surface smoothness.
-   **Offset**: Controls the intensity of the distortion applied to the reflection, based on the normal map. This creates a wavy or bumpy effect.
-   **Color**: Tints the reflection with a specific color.
-   **Clip Bias**: Adjusts the reflection's clipping plane to prevent self-reflection artifacts.
-   **Opacity**: Controls the opacity of the objects affected by the reflection, creating a semi-transparent look.
-   **Custom Textures**:
    -   **Upload White Texture**: Upload a "white film" texture. The alpha channel of this texture controls the transparency of different parts of the reflection.
    -   **Upload Normal Texture**: Upload a normal map to create detailed distortions on the reflected image.

### 🛠️ How It Works

The core of this effect is a custom `GroundMirror` class that extends Three.js's `Reflector`. Here's a breakdown of the technique:

1.  **Reflection Texture**: A `ReflectorNode` is used to capture the scene from the reflection's perspective, generating a reflection texture.
2.  **UV Perturbation**: Instead of using the screen-space UV coordinates directly to sample the reflection texture, the coordinates are perturbed:
    -   A **normal map** is sampled.
    -   The R and G channels (representing X and Y normals) are used to create an offset vector.
    -   This offset is scaled by the `Offset` GUI parameter.
    -   The final, distorted UV is calculated by adding this offset to the original screen-space UV.
3.  **Blur**: The perturbed reflection texture is then processed by a `BlurNode`. The `Blur` parameter from the GUI controls the radius of the blur, creating effects from a perfectly sharp mirror to a very diffused reflection.
4.  **Material Composition**: The final blurred and distorted reflection is applied as an `environment` map to a `PhongNodeMaterial`. This allows the plane to interact with scene lighting while displaying the reflection.

### 💻 Technologies Used

-   [Three.js](https://threejs.org/) (r134)
-   [lil-gui](https://github.com/georgealways/lil-gui)

---

## Miscellaneous

https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221kjSUzqFoRgJJaFY0aKAX5YUpEaEUvLNV%22%5D,%22action%22:%22open%22,%22userId%22:%22114071867668135233535%22,%22resourceKeys%22:%7B%7D%7D&usp=sharing

<img width="1760" height="1288" alt="Image" src="https://github.com/user-attachments/assets/c352fdd9-4c5c-4a27-bc31-81f662da4283" />

---

## 中文

### 💡 简介

本项目是一个使用 Three.js 实现的地面反射效果演示，通常用于模拟潮湿或光滑的表面。它超越了简单的平面反射，通过引入可动态调节的扭曲和模糊效果，实现了更逼真的视觉表现。用户还可以上传自定义纹理，观察它们如何影响反射效果。

### 🚀 如何运行

只需在支持 WebGL 的现代浏览器中打开 `index.html` 文件即可。无需本地服务器。

### ✨ 功能

项目提供了一个基于 `lil-gui` 的控制面板，让你可以实时调整以下参数：

-   **X/Z 尺寸 (Size X/Z)**: 调整反射平面的宽度和长度。
-   **Y 位置 (Position Y)**: 控制反射平面的垂直高度。
-   **模糊 (Blur)**: 设置反射的模糊程度，用于模拟不同光滑度的表面。
-   **偏移 (Offset)**: 控制法线贴图对反射的扰动强度，从而产生水波纹或凹凸不平的效果。
-   **颜色 (Color)**: 为反射添加一层指定的色调。
-   **裁切偏移 (Clip Bias)**: 调整反射的裁切平面，以防止出现自反射的瑕疵。
-   **不透明度 (Opacity)**: 控制受反射影响的物体的透明度，以实现半透明效果。
-   **自定义纹理 (Custom Textures)**:
    -   **上传白膜纹理**: 上传一张“白膜”纹理，其 Alpha 通道将控制反射不同区域的透明度。
    -   **上传法线纹理**: 上传一张法线贴图，用于在反射图像上创建精细的扭曲效果。

### 🛠️ 实现原理

该效果的核心是一个自定义的 `GroundMirror` 类，它继承自 Three.js 的 `Reflector`。其技术原理如下：

1.  **反射纹理**: 使用 `ReflectorNode` 从反射视角捕捉场景，生成一张基础的反射纹理。
2.  **UV 扰动**: 在采样反射纹理时，不直接使用屏幕空间的 UV 坐标，而是对其进行扰动：
    -   对一张**法线贴图**进行采样。
    -   利用其 R 和 G 通道（代表法线的 X 和 Y 方向）创建一个偏移向量。
    -   该偏移量受 GUI 中的 `Offset` 参数控制。
    -   将原始的屏幕空间 UV 与该偏移量相加，得到最终带有扰动的 UV 坐标。
3.  **模糊处理**: 经过扰动的反射纹理会被送入一个 `BlurNode` 进行处理。GUI 中的 `Blur` 参数控制模糊半径，可以创造出从完美镜面到非常模糊的各种反射效果。
4.  **材质合成**: 最终，经过模糊和扭曲的反射将作为一个 `environment` 环境贴图，应用到一个 `PhongNodeMaterial` 材质上。这使得该平面在显示反射的同时，还能与场景中的光照进行交互。

### 💻 技术栈

-   [Three.js](https://threejs.org/) (r134)
-   [lil-gui](https://github.com/georgealways/lil-gui)
