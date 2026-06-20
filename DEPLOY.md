# 部署指南

## 📦 如何添加默认模型

### 步骤 1：准备模型文件

将你的模型文件（如 `model.glb`）复制到项目的 `default-models/` 文件夹中。

**注意**：GitHub 有文件大小限制：
- 单个文件最大 **100 MB**
- 仓库总大小建议不超过 **1 GB**

如果你的模型文件超过 100 MB，建议使用外部 CDN 或对象存储（如 GitHub Releases、jsDelivr、Cloudflare R2 等）。

### 步骤 2：配置 config.json

编辑 `config.json`，指定默认模型的路径：

```json
{
  "defaultModels": [
    {
      "name": "My 3D Model",
      "path": "./default-models/model.glb",
      "autoLoad": true
    }
  ]
}
```

**路径说明**：
- `./default-models/model.glb` - 相对路径，指向仓库中的文件
- `https://example.com/model.glb` - 绝对 URL，指向外部资源

### 步骤 3：提交并推送

```bash
cd "C:\Users\TRSEIMC\WorkBuddy\2026-06-20-08-03-44"
git add default-models/ config.json
git commit -m "Add default model"
git push origin main
```

### 步骤 4：等待自动部署

推送后，GitHub Actions 会自动部署到 GitHub Pages。

- 查看部署状态：https://github.com/TCBOMC/3D-Model-Viewer/actions
- 部署完成后访问：https://tcbomc.github.io/3D-Model-Viewer/

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
2. 模型文件路径配置错误
3. 模型文件太大，加载超时

**解决方法**：
1. 检查 `default-models/` 文件夹是否包含模型文件
2. 检查 `config.json` 中的路径是否正确
3. 打开浏览器开发者工具（F12），查看 Console 和 Network 标签页的错误信息

### Q: 如何检查模型文件是否正确上传？

访问以下 URL（替换为你的实际文件名）：
```
https://raw.githubusercontent.com/TCBOMC/3D-Model-Viewer/main/default-models/model.glb
```

如果能下载文件，说明文件已正确上传。

### Q: 模型文件太大怎么办？

**方案 1：使用外部 CDN**

将模型文件上传到外部 CDN，然后在 `config.json` 中使用绝对 URL：

```json
{
  "defaultModels": [
    {
      "name": "My Model",
      "path": "https://cdn.example.com/model.glb",
      "autoLoad": true
    }
  ]
}
```

**推荐的免费 CDN**：
- [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases) - 适合大文件
- [jsDelivr](https://www.jsdelivr.com/) - 自动 CDN 加速
- [Cloudflare R2](https://www.cloudflare.com/products/r2/) - 免费额度高

**方案 2：压缩模型文件**

使用 [Blender](https://www.blender.org/) 或 [glTF Transform](https://gltf-transform.donmccurdy.com/) 压缩模型文件。

---

## 📝 示例：完整的 config.json

```json
{
  "defaultModels": [
    {
      "name": "Damaged Helmet",
      "path": "https://raw.githubusercontent.com/KhronosGroup/glTF-Sample-Models/master/2.0/DamagedHelmet/glTF-Binary/DamagedHelmet.glb",
      "autoLoad": true
    },
    {
      "name": "Local Model",
      "path": "./default-models/local-model.glb",
      "autoLoad": false
    }
  ],
  "settings": {
    "autoLock": false,
    "defaultSpeed": 6.0,
    "showFPS": true
  }
}
```

**说明**：
- 第一个模型（`autoLoad: true`）会自动加载
- 第二个模型（`autoLoad: false`）不会自动加载，但可以在代码中手动加载
- 支持混合使用本地文件和外链 URL
