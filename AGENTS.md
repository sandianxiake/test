# 发版详情页面

## 项目概述
发版详情展示页面，左侧目录导航 + 右侧内容详情，双向锚点联动。

## 技术栈
- Vue 3 + Vite
- Intersection Observer API 实现滚动联动

## 目录结构
```
/workspace/projects/
├── .coze                          # 项目配置
├── scripts/
│   ├── coze-preview-build.sh      # 预览构建脚本
│   └── coze-preview-run.sh        # 预览运行脚本
└── src/
    ├── App.vue                    # 入口组件
    ├── main.js                    # 入口文件
    ├── style.css                  # 全局样式
    └── components/
        └── ReleasePage.vue        # 发版详情页（核心组件）
```

## 核心功能
- 左侧目录（固定 200px）点击 → 右侧滚动定位
- 右侧滚动 → 左侧高亮当前项并自动滚动
- 滚动到底部自动停止

## 运行
```bash
pnpm dev
```

## 预览服务
- 端口：5000
- 构建：`bash scripts/coze-preview-build.sh`
- 运行：`bash scripts/coze-preview-run.sh`
