# 3D Model Viewer

基于 Three.js 的网页端 3D 模型查看器，支持 Mesh 和点云模型，具备游戏引擎风格的 WASD + 鼠标自由漫游控制。

## ✨ 功能特性

- 🎮 **FPS 风格相机控制**：WASD 移动 + 鼠标环视，Shift 加速，空格上升，C 下降
- 📦 **Mesh 模型支持**：GLB / GLTF / OBJ / STL
- ☁️ **点云模型支持**：PLY（自动识别点云/网格）
- 🎨 **点云着色模式**：原始颜色 / 高度映射 / 法线映射
- 🔗 **URL 加载**：直接输入模型 URL 在线加载
- 📊 **模型信息面板**：顶点数、面数统计
- 🖱️ **拖放支持**：直接拖文件到页面即可加载
- 🎯 **默认模型配置**：支持配置打开网页时自动加载的默认模型

## 🚀 快速开始

### 方法一：直接部署到 GitHub Pages

1. Fork 或新建仓库，将本项目的所有文件推送到仓库
2. 在仓库 **Settings → Pages** 中，Source 选择 `main` 分支，`/` (root) 文件夹
3. 保存后等待 1-2 分钟，访问 `https://<用户名>.github.io/<仓库名>/`

### 方法二：本地使用

直接用浏览器打开 `index.html` 即可（部分浏览器需 HTTP 服务，可运行 `python -m http.server 8080`）。

## 🎯 配置默认模型

支持配置打开网页时自动加载的默认模型，无需用户手动上传。

### 使用方法

1. **准备模型文件**：将模型文件（如 `model.glb`）放入 `default-models/` 文件夹

2. **推送到 GitHub**：将更改推送到 `main` 分支，GitHub Actions 会自动部署到 GitHub Pages

3. **自动加载**：网页会自动加载 `default-models/` 文件夹中的第一个模型文件

### 支持的模型文件

网页会自动识别以下文件（按优先级）：
- `model.glb` / `model.gltf`
- `default.glb` / `default.gltf`
- `scene.glb` / `scene.gltf`
- 任何其他 `.glb`、`.gltf`、`.ply`、`.obj`、`.stl` 文件

**注意**：
- 将你想要作为默认模型的文件命名为 `model.glb` 或 `default.glb`，确保它会被优先加载
- 如果没有模型文件，网页会正常显示，不会尝试加载默认模型

## 🤖 自动部署 Workflow

本项目包含 GitHub Actions workflow，自动部署到 GitHub Pages。

### Workflow 触发条件

- 推送到 `main` 分支（当以下文件变更时）：
  - `index.html`
  - `config.json`
  - `default-models/**`（默认模型文件夹）
  - `.github/workflows/deploy.yml`
- 手动触发（在 GitHub 仓库 **Actions** 页面点击 **Run workflow**）

### Workflow 功能

1. 检查代码
2. 构建（如果需要）
3. 部署到 GitHub Pages

### 使用方法

1. 将模型文件放入 `default-models/` 文件夹
2. 修改 `config.json` 配置默认模型
3. 提交并推送到 `main` 分支
4. GitHub Actions 自动部署到 GitHub Pages
5. 访问 `https://<用户名>.github.io/<仓库名>/` 查看效果

## 🎮 操作说明

### 鼠标模式

支持两种鼠标控制模式，按 **`Alt`** 键切换：

| 模式 | 说明 |
|------|------|
| **点击锁定**（默认） | 点击画面后鼠标被锁定，自由转动视角；按 `Esc` 释放 |
| **按住锁定** | 只有按住鼠标左键时才锁定并转动视角，松开即释放 |

### 按键

| 按键 | 功能 |
|------|------|
| 点击画面 / 按住左键 | 锁定鼠标，进入漫游模式（取决于当前鼠标模式） |
| W / A / S / D | 前后左右移动 |
| 鼠标 | 环顾四周 |
| Shift | 加速移动 |
| 空格 | 上升 |
| C | 下降 |
| Alt | 切换鼠标模式 |
| Esc | 释放鼠标（仅点击锁定模式） |

## 📦 支持的格式

| 格式 | 类型 | 说明 |
|------|------|------|
| .glb / .gltf | Mesh | 推荐格式，支持材质和动画 |
| .ply | 点云 / Mesh | 自动识别，点云将渲染为粒子 |
| .obj | Mesh | 通用网格格式 |
| .stl | Mesh | 3D 打印常用格式 |

## 🔗 加载在线模型示例

在 URL 输入框中粘贴以下地址测试：

```
https://raw.githubusercontent.com/KhronosGroup/glTF-Sample-Models/master/2.0/DamagedHelmet/glTF-Binary/DamagedHelmet.glb
```

## 🛠️ 技术栈

- [Three.js r162](https://threejs.org/)（通过 CDN ES Module 引入）
- 纯前端，无后端依赖，可直接部署到 GitHub Pages
- GitHub Actions 自动部署
