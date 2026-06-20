# 部署指南

## 📦 如何添加默认模型

### 步骤 1：准备模型文件

将你的模型文件（如 `model.glb`）复制到项目的 `default-models/` 文件夹中。

**推荐命名**：
- 将默认模型命名为 `model.glb` 或 `default.glb`，这样会被优先加载
- 网页会自动加载 `default-models/` 文件夹中的第一个模型文件

**注意**：GitHub 有文件大小限制：
- 单个文件最大 **100 MB**
- 仓库总大小建议不超过 **1 GB**

如果你的模型文件超过 100 MB，建议使用外部 CDN 或对象存储（如 GitHub Releases、jsDelivr、Cloudflare R2 等）。

### 步骤 2：提交并推送

```bash
cd "C:\Users\TRSEIMC\WorkBuddy\2026-06-20-08-03-44"
git add default-models/
git commit -m "Add default model"
git push origin main
```

### 步骤 3：等待自动部署

推送后，GitHub Actions 会自动部署到 GitHub Pages。

- 查看部署状态：https://github.com/TCBOMC/3D-Model-Viewer/actions
- 部署完成后访问：https://tcbomc.github.io/3D-Model-Viewer/

**自动生成的文件**：
- Workflow 会自动生成 `default-models/manifest.json` 文件，列出所有可用的模型文件
- 网页会读取这个文件来加载默认模型

---

## 🔧 手动触发部署

如果自动部署失败，可以手动触发：

1. 访问 https://github.com/TCBOMC/3D-Model-Viewer/actions
2. 在左侧选择 **Deploy to GitHub Pages** workflow
3. 点击 **Run workflow** 按钮
4. 选择 `main` 分支，点击 **Run workflow** 确认

---

## ❓ 常见问题

### Q: 网页一直显示"加载默认模型"但无法加载？

**可能原因**：
1. 模型文件没有正确推送到 GitHub
2. 模型文件太大，加载超时
3. 模型文件格式不支持

**解决方法**：
1. 检查 `default-models/` 文件夹是否包含模型文件
2. 打开浏览器开发者工具（F12），查看 Console 和 Network 标签页的错误信息
3. 确保模型文件是支持的格式（`.glb`、`.gltf`、`.ply`、`.obj`、`.stl`）

### Q: 如何检查模型文件是否正确上传？

访问以下 URL（替换为你的实际文件名）：
```
https://raw.githubusercontent.com/TCBOMC/3D-Model-Viewer/main/default-models/model.glb
```

如果能下载文件，说明文件已正确上传。

### Q: 模型文件太大怎么办？

**方案 1：使用外部 CDN**

将模型文件上传到外部 CDN，然后修改网页代码中的默认模型路径。

**推荐的免费 CDN**：
- [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases) - 适合大文件
- [jsDelivr](https://www.jsdelivr.com/) - 自动 CDN 加速
- [Cloudflare R2](https://www.cloudflare.com/products/r2/) - 免费额度高

**方案 2：压缩模型文件**

使用 [Blender](https://www.blender.org/) 或 [glTF Transform](https://gltf-transform.donmccurdy.com/) 压缩模型文件。

---

## 📝 示例：模型文件结构

```
3D-Model-Viewer/
├── index.html
├── default-models/
│   ├── model.glb          # 默认模型（优先加载）
│   ├── manifest.json      # 自动生成，无需手动创建
│   └── .gitkeep
├── .github/
│   └── workflows/
│       └── deploy.yml
└── README.md
```

**说明**：
- `model.glb` 会被自动加载
- 如果有多个模型文件，只有第一个会被加载（按文件名排序）
- `manifest.json` 由 workflow 自动生成，无需手动创建
