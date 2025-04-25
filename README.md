# guangdong-map
### GitHub Pages部署Next.js应用的详细说明

我为你生成了部署到GitHub Pages所需的配置文件，下面我将详细解释每个文件的作用、部署步骤以及可能遇到的问题。

## 文件说明

### 1. `next.config.mjs`

这是Next.js的配置文件，主要设置了：

- `output: 'export'` - 将应用导出为静态HTML文件，这是GitHub Pages部署的必要设置
- `distDir: 'out'` - 指定构建输出目录
- `basePath` - 设置应用的基本路径，对应GitHub Pages的仓库名
- `assetPrefix` - 确保静态资源（JS、CSS等）使用正确的URL路径
- `trailingSlash: true` - 添加尾部斜杠，有助于GitHub Pages的路由处理
- `images.unoptimized: true` - 禁用Next.js的图像优化，因为GitHub Pages不支持服务端功能


### 2. `package.json`

包含项目依赖和脚本命令：

- `build` 和 `export` 脚本 - 用于生成静态文件
- 列出了项目所需的依赖，包括echarts、React和Next.js


### 3. `.github/workflows/deploy.yml`

GitHub Actions工作流配置文件，自动化部署过程：

- 触发条件：当推送到main分支或手动触发时
- 构建步骤：安装依赖、构建应用、导出静态文件
- 部署步骤：将生成的静态文件部署到GitHub Pages


### 4. `.nojekyll`

空文件，告诉GitHub Pages不要使用Jekyll处理你的文件，避免某些文件被忽略。

### 5. `tailwind.config.js` 和 `postcss.config.js`

Tailwind CSS的配置文件，确保样式正确应用。

### 6. `tsconfig.json`

TypeScript配置文件，定义了编译选项和路径别名。

### 7. `app/globals.css`

全局CSS文件，包含Tailwind的基础样式和自定义变量。

## 部署步骤

1. **准备GitHub仓库**：

1. 创建一个新的GitHub仓库，名称建议为`guangdong-map`（或你喜欢的名称）
2. 如果使用其他名称，记得修改`next.config.mjs`中的`basePath`和`assetPrefix`



2. **添加配置文件**：

1. 将上述生成的配置文件添加到你的项目中
2. 确保你的项目结构包含这些文件



3. **推送代码**：

```shellscript
git init
git add .
git commit -m "Initial commit for GitHub Pages"
git branch -M main
git remote add origin https://github.com/你的用户名/guangdong-map.git
git push -u origin main
```


4. **配置GitHub Pages**：

1. 转到GitHub仓库的"Settings" > "Pages"
2. 在"Source"部分，选择"GitHub Actions"
3. 如果看不到此选项，可能需要先等待Actions工作流运行一次



5. **等待部署**：

1. GitHub Actions会自动运行工作流
2. 部署完成后，你可以在Actions标签页查看进度
3. 成功后，你的应用将可以通过`https://你的用户名.github.io/guangdong-map/`访问





## 可能遇到的问题及解决方案

1. **基本路径问题**：

1. **症状**：页面加载但样式或JavaScript不工作
2. **原因**：`basePath`和`assetPrefix`配置不正确
3. **解决方案**：确保这些值与你的仓库名称匹配



2. **构建失败**：

1. **症状**：GitHub Actions工作流失败
2. **原因**：依赖安装问题或构建错误
3. **解决方案**：检查Actions日志，解决相应错误，可能需要更新依赖版本



3. **空白页面**：

1. **症状**：部署成功但显示空白页面
2. **原因**：可能是客户端渲染问题或路径错误
3. **解决方案**：检查浏览器控制台错误，确保所有资源路径正确



4. **地图数据加载失败**：

1. **症状**：页面加载但地图不显示
2. **原因**：JSON数据路径问题
3. **解决方案**：确保`guangdong.json`文件正确导入，考虑使用相对路径



5. **服务端功能不工作**：

1. **症状**：依赖服务端功能的特性不工作
2. **原因**：GitHub Pages只支持静态文件托管
3. **解决方案**：将服务端逻辑转换为客户端逻辑，或使用外部API



6. **路由问题**：

1. **症状**：导航到子页面后刷新出现404
2. **原因**：GitHub Pages不支持客户端路由
3. **解决方案**：使用哈希路由或为每个路由生成静态HTML文件



7. **部署后更新不显示**：

1. **症状**：推送新代码后，网站未更新
2. **原因**：缓存问题或部署未完成
3. **解决方案**：检查GitHub Actions是否完成，尝试强制刷新浏览器（Ctrl+F5）





## 特别注意事项

1. **仓库可见性**：

1. 如果你的仓库是私有的，需要升级GitHub账户才能使用GitHub Pages



2. **自定义域名**：

1. 如果想使用自定义域名，可以在GitHub Pages设置中配置
2. 记得更新`next.config.mjs`中的`basePath`和`assetPrefix`



3. **大文件限制**：

1. GitHub Pages有文件大小限制，如果你的应用过大，可能需要优化或考虑其他托管服务



4. **构建性能**：

1. 如果构建时间过长，考虑优化构建过程或使用缓存策略





通过以上步骤和注意事项，你应该能够成功将广东省数据可视化地图部署到GitHub Pages上。如果遇到特定问题，可以查看GitHub Actions的日志获取更详细的错误信息。
